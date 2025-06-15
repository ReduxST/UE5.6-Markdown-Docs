# Ray Tracing Performance Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ray-tracing-performance-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ray-tracing-performance-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:46

---

For projects that need to maintain a real-time performance budget, it's important to set a frame budget in order to achieve that target frame rate. Typically, that would be 30 or 60 frames per second (FPS). There are many opportunities for optimizing and improving performance of your projects by making adjustments to content or workflows.

This guide covers some starting points for optimizing Ray Tracing features of Unreal Engine and ways you can pin-point trouble areas through debugging the scene and investigating those issues.

## Overview of Ray Tracing Costs

Hardware Ray Tracing uses a two-level **Bounding Volume Hierarchy** (BVH) to accelerate ray traversal. The **Top Level Acceleration Structure** (TLAS) contains all mesh instances for the whole scene. The meshes referenced by those instances are **Bottom Level Acceleration Structures** (BLAS).

The diagram below gives a visual representation of how the BVH works for ray traversal.

![diagram of ray tracing acceleration structure](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d39592cb-529a-4313-bbd6-bf38ac84d354/ray-tracing-acceleration-structure-diagram.png)

There are three main categories of costs associated with Ray Tracing:

1.  Building the Bottom Level Acceleration Structures for dynamically deforming meshes, like skinned meshes and hair.
2.  Building the Top Level Acceleration Structure for the scene and the Shader Binding Table (SBT).
3.  Ray traversal for each feature that uses Ray Tracing.

For development of your project, you can test the ray tracing cost of specific types of geometry with console variables. This is useful for measuring their costs or disabling them entirely for Ray Tracing features. You'll find them listed under `r.RayTracing.Geometry.*`.

| Geometry Type | Console Variable | Default State |
| --- | --- | --- |
| Static Meshes | `r.RayTracing.Geometry.StaticMeshes` | Enabled |
| Skeletal Meshes | `r.RayTracing.Geometry.SkeletalMeshes` | Enabled |
| Instanced Static Meshes | `r.RayTracing.Geometry.InstancedStaticMeshes` | Enabled |
| Landscape Terrain | `r.RayTracing.Geometry.Landscape` | Enabled |
| Geometry Cache | `r.RayTracing.Geometry.GeometryCache` | Enabled |
| Geometry Collection | `r.RayTracing.Geometry.GeometryCollection` | Disabled |
| Niagara Meshes | `r.RayTracing.Geometry.NiagaraMeshes` | Enabled |
| Niagara Ribbons | `r.RayTracing.Geometry.NiagaraRibbons` | Enabled |
| Niagara Sprites | `r.RayTracing.Geometry.NiagaraSprites` | Enabled |
| Procedural Meshes | `r.RayTracing.Geometry.ProceduralMeshes` | Enabled |

## Bottom Level Acceleration Structure Updates

While the BLAS for Static Meshes are only built once at load (or during the cook on consoles), dynamically deforming meshes have to rebuild every frame and this can incur significant cost. The BLAS rebuilds are a GPU operation, and are typically proportional to the total number of triangles being deformed. **Using a large number of Skeletal Meshes with a large number of triangles can quickly become a major GPU cost.**

BLAS rebuild costs can be observed in the GPU Profiler under the following areas:

-   Scene > CommitRayTracingGeometryUpdates
-   Scene > CommitHairRayTracingGeometryUpdates
-   Scene > RayTracingGeometry

Geometry types which rebuild every frame include:

-   Skinned meshes through GPUSkinCache
-   Landscape is rebuilt to support its continuously morphing level of detail (LOD)
-   Geometry Collections for Chaos Destruction
-   Hair
-   Procedural Mesh
-   Niagara Particle Systems

High polygon Skeletal Meshes are the most common cause of high BLAS build costs. Skeletal Meshes can use the property **Ray Tracing Min LOD** found in the [Skeletal Mesh Editor](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine), which prevents the highest LODs from being used for Ray Tracing features.

Use the console command `D3D12.DumpRayTracingGeometries` when running a project with D3D12 to get a list of all the memory allocations for dynamic BLAS rebuilds dumped to the log. This list can be used to optimize your project.

### World Position Offset on Static Mesh Components

World Position Offset (WPO) is challenging to support efficiently with Ray Tracing features because it requires dynamically rebuilding the BLAS, as well as unique memory for each instance.

By default, Unreal Engine ignores WPO when building Ray Tracing Scene, which can cause self-intersections artifacts. Static Mesh Components can opt-in to using WPO with ray tracing with the **Evaluate World Position Offset** setting. However, it only works for a short distance around the camera, 50 meters unless otherwise specified.

Use the following to enable and adjust the supported WPO distance from the camera:

-   `r.RayTracing.Geometry.StaticMeshes.WPO 1`
-   `r.RayTracing.Geometry.StaticMeshes.WPO.CullingRadius 5000.0f`

The dynamic BLAS builds caused by WPO show up in the GPU profiler under `Scene > RayTracingGeometry > RayTracingDynamicGeometryUpdate`.

Instanced components, like Instanced Static Mesh Component, do not support WPO by default because of its extreme cost. Components that have a **Evaluate World Position Offset** toggle do not enable it by default. Toggling it on can significantly increase memory pressure and slow render times because it effectively converts every instance in a single mesh with a separate BLAS.

### Managing Ray Tracing Memory Cost

Ray tracing can significantly increase memory requirements. For each mesh that is visible to ray tracing, a ray tracing bottom-level acceleration structure needs to be allocated. Generally, the memory requirement for a bottom-level acceleration structure scales linearly with the number of triangles / vertices, but the exact size is platform-dependent. Also, all visible meshes will allocate their BLAS, which can consume a significant amount of memory. To overcome this problem, you can use the **Reference Based Residency** system that only allocated BLAS that are directly referenced by TLAS. This also allows specifying the memory budget for the remaining BLAS. Anything not referenced, or that is above budget, will get evicted.

You can enable the Reference Based Residency system by using the console command `r.RayTracing.UseReferenceBasedResidency`. This is disabled by default. Set to **1** to enable.

On platforms that support both inline ray tracing and ray tracing shaders, you can use the per-platform option for fine-grained control over how ray tracing is enabled. You can find this in the Project Settings under **Platforms > \[Platform\] > Ray Tracing Mode**. It includes the following modes:

-   **Disabled:** All ray tracing on this platform is disabled.
-   **Inline:** Only inline ray tracing passes are enabled, such as Lumen Hardware Ray Tracing mode with Surface Cache and Barycentrics / Traversal debug view. In this mode, ray tracing material shaders and select global shaders are not compiled. This saves memory and CPU cost by not having to prepare binding for ray tracing shaders.
-   **Full:** Every feature of ray tracing is supported on this platform.

## Top Level Acceleration Structure Build

The Top Level Acceleration Structure is rebuilt every frame, and has a cost on the Rendering Thread, RHI Thread, and the GPU. These costs are mostly proportional to how many mesh instances go into the acceleration structure.

Using the stat command `Stat SceneRendering`, you will find the number of instances being rebuilt every frame under **Ray tracing instances**.

![ray tracing instances in stat scenerendering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b05cdae-c2a8-4712-97f0-53e37ba63616/stat-scenerendering-1.png)

To measure the cost of the Rendering Thread, use the command `Stat SceneRendering` and look for the **GatherRayTracingWorldInstances**.

![gather ray tracing world instances in stat scenerendering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bf5826c-2b18-4bbc-a45e-fb0514db05f5/stat-scenerendering-2.png)

To measure the cost of the RHI Thread, you can use per-RHI stats, such as `Stat D3D12RayTracing`.

![measure cost of rhi thread in stat d3d12raytracing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a9521ac-f8d9-47d1-a535-e52e7611b426/stat-scenerendering-3.png)

GPU cost can be measured with the stat command `Stat GPU`. Look at entries for **RayTracingScene** and **RayTracing** to get an idea of their costs.

![GPU cost measured with stat GPU](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5829768-ac22-4644-aa97-26f9365963f1/stat-scenerendering-4.png)

In order to achieve a 30 frames per second target on next generation consoles, scenes should generally have 100,000 instances or fewer in the Ray Tracing Scene after culling. On Windows, the number of instances can vary significantly.

### Culling

Scenes with ray tracing require objects outside of the camera view to be present in the scene, especially for highly reflective surfaces. This increases the cost of rendering the scene. Culling objects that aren't visible or needed helps with optimizing performance.

Since ray tracing needs to keep objects visible, even when they aren't in view, the console variable `r.RayTracing.Culling` provides some options to help optimize what is visible outside of the current view and over what distance.

The following options are provided:

-   **1** culls objects behind the camera by distance and solid angle (default ray tracing culling method).
-   **2** culls objects in front of and behind the camera by distance and solid angle.
-   **3** culls objects in front and behind the camera by distance or solid angle.

Each culling option progressively culls more objects in the ray tracing scene.

Because the TLAS is rebuilt every frame, mesh instances can be culled based on their distance or angle to the camera when setting option 3.

Additionally, the **Radius** and **Angle** that the Ray Tracing Culling option uses can be configured on their on using the following console commands:

-   `r.RayTracing.Culling.Radius`: Sets a distance around the camera beyond which objects are culled. Default radius is 10000 (100 meters).
-   `r.Raytracing.Culling.Angle`: Culls meshes whose projected angle is smaller than 5 degrees. The default is 1.

For an open world project, such as City Sample, the culling **Radius** was increased to 15000 (150 meters), while the culling **Angle** was reduced to 0.5 (2.5 degrees) in account for large areas with lots of reflective surfaces that needed objects to be visible over farther distances.

Culling causes a lack of coverage in the Ray Tracing Scene and is best paired with the [Far Field](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#farfield) to provide traces for distant geometry.

Mesh components tagged with a **Ray Tracing Group Id** greater than 0 can be culled as an aggregate using `r.RayTracing.Culling.UserGroupIds 1`. This method can be useful if your scene is built out of many disparate parts, but you'd like to cull them as a single object.

![ray tracing details panel settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58ce26cd-5693-42cd-a56a-15afe7990258/ray-tracing-details-settings.png)

Ray Tracing Group Id property found on a selected Actor in a Level.

## Ray Traversal Cost

Ray queries are spawned by features which use [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine), such as Ray Tracing Shadows, Lumen Global Illumination, and Lumen Reflections. GPUs solve these Ray queries with dedicated hardware that traverses the acceleration structures to find a hit.

An example of ray traversal costs in the Profile GPU log output would be:

2.36ms LumenReflections 1 draw 1 prims 0 verts 13 dispatches 4.1% 0.67ms ReflectionHardwareRayTracing \[default\] 1 draw 1 prims 0 verts 1 dispatch 1 groups

The cost of ray traversal is proportional to the number of Ray queries issued by the lighting feature, and the amount of mesh overlap in the scene.

When meshes overlap, the ray must traverse them all independently to find the closest hit, because Ray Tracing uses a two-level acceleration structure. The mesh overlap can cause extremely slow ray traversal in scenes built by piecing different assets together as needed (also called kitbashing).

![overlapping meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bff217bc-7531-4cea-8c82-c1a21048427b/overlapping-meshes-kit-bashed.png)

Example of kitbashed assets used to layer rocks in the Unreal Engine 5 "Valley of the Ancients" technical demo.

In order for scenes to be compatible with Hardware Ray Tracing, mesh overlap **must** be kept to a minimum.

There are other common causes of high ray traversal costs, the first being skyboxes — they overlap the entire scene and must be traversed by every ray, even if they are not hit. Another is grass — it has large bounds and high geometry complexity.

In these cases (or any others that are similar), you can choose to have those ray tracing tracing skip those meshes. Select the Actors in the world and use their Details panel to disable **Visible in Ray Tracing**.

### Ray Traversal Debug Visualization Modes

The following debug modes are currently only available on console platforms.

There are two debug modes that are useful for investigating high traversal costs: Performance and Traversal.

To enable these modes, you'll use the following commands:

```
	`show raytracingdebug 1 	r.RayTracing.DebugVisualizationMode [mode]`

Copy full snippet
```
show raytracingdebug 1 r.RayTracing.DebugVisualizationMode \[mode\]

"\[Mode\]" is replaced by the visualization method you want to see: `Performance` or `Traversal Node`. For example, it would be `r.RayTracing.DebugVisualizationMode Traversal Node`.

### Performance Debug Visualization

**Performance** debug visualization shows a heatmap of the TraceRay call, showing the combined time of BVH traversal and material evaluation time (executing Closest Hit/Miss shaders).

![performance debug visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98eb6e33-4337-478a-b6ab-1748e41e6535/vis-performance-debug.png)

Ray Tracing Performance debug visualization.

The colors of the visualization go from purple (no cost) to yellow (high cost). The heatmaps scale can be adjusted to fit your project's needs using `r.RayTracing.DebugTiming Scale`.

This mode is most useful to find problematic objects and materials for Ray Tracing. If Ray Tracing cost is too high, it is a good idea to check if what's showing in that mode looks reasonable.

For example, the objects visible in the main view are also present in debug mode, no undesired objects are present and the material cost looks as expected for those objects. If there is nothing that stands out, it might be because the slow down is not caused by one single object but the combination of different smaller issues.

### Traversal Debug Visualization

The **Traversal** debug visualization shows a heatmap of only BVH traversal — how many iterations it takes to find a hit. For Lumen passes that don't use materials or similar passes that use simple hit shading/inline, the highest cost is usually the BVH traversal.

The colors of the heatmap goes from green (few iterations) to red (many iterations). Intuitively, the more iterations that happen, the slower the traversal. The values are in the range of 50-100 iterations for a typical scene. For a complicated scene, including multiple overlapping high polygon meshes, there are around 100-150 iterations.

Anything above that suggests there might be a problem, for example, it would not be uncommon for a broken mesh to see 1000+ iterations. The Traversal Triangle debug visualization is useful for checking individual meshes triangles.

For Traversal debugging, there are three modes to select from:

| Traversal Debug mode | Command Name | Description | Visualization View |
| --- | --- | --- | --- |
| **Node Intersection Count** | `Traversal Node` | 
Used to investigate scene traversal costs. For example, when many instances are overlapping in TLAS.

These are BVH nodes in the internal, platform-specific representations of BLAS.



 | 

 |
| **Triangle Intersection Count** | `Traversal Triangle` | Shows the hits of nodes that contain only triangles (leaf nodes). | 

 |
| **Total Intersection Count** | `Traversal All` | Sum of BVH node hits and triangle node hits. | 

 |

### Hit Shading Costs

When a ray hits a triangle, the material is evaluated and used for shading the hit point. For complex materials using procedural texturing and many virtual textures, this can be a very expensive process.

The **Ray Tracing Quality Switch** node is an expression that can be used in your Materials to provide a cheaper implementation for shading ray hits.

![ray tracing quality switch material node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc169bd8-cfcd-4157-a000-a070d464acd6/material-ray-tracing-quality-switch-node.png)

The node can replace entire parts of your Material logic to lower the overall cost of Ray Tracing features. Using this node affects all ray tracing effects for this material.

A simple example (see below) would be a material that includes logic that is costly for ray tracing effects. The RayTracingQualitySwitch node includes two inputs: Normal and RayTraced.

The **Normal** input contains all the logic needed for the material and is how it would appear on surfaces in the world. The **RayTraced** input should have less complexity in the logic path that increases the cost of ray tracing effects, like the Normal map.

Click image for full size.

### Far Field

Ray Tracing supports a **Far Field** representation that extends Lumen Global Illumination and Reflections to one kilometer from the camera by default. The Far Field makes use of [Hierarchical Level of Detail (HLOD) meshes generated by World Partition](/documentation/en-us/unreal-engine/world-partition---hierarchical-level-of-detail-in-unreal-engine) by default. The HLOD1 mesh is used for Far Field representation.

Currently, only Lumen lighting features make use of [Ray Tracing Far Field](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#farfield), and only when enabled for the project with the command `r.LumenScene.FarFields 1`.

On selected meshes that should be visible to the Far Field, toggle the **Ray Tracing Far Field** setting.

![ray tracing far field setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57ee0371-39f6-4f9c-91fa-95ba0a433aab/ray-tracing-far-field.png)

In the editor, the Far Field can be visualized using the ray tracing debug visualization mode for `FarField`. Enter the following commands:

```
	`r.RayTracing.DebugVisualizationMode FarField 	Showflag.RayTracingDebug 1`

Copy full snippet
```
r.RayTracing.DebugVisualizationMode FarField Showflag.RayTracingDebug 1

In the visualization below, the far-field is the tinted red geometry using the HLOD1 meshes generated by World Partition. Anything closer to the camera is the high-detail geometry.

![far field visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad4d00f2-c86c-438d-8071-8818aef5e311/ray-tracing-far-field-visualization.png)

Lumen's Ray Tracing Far Field debug visualization. Far-field geometry is tinted red.

## Additional Ray Tracing Debug Visualization Modes

The **Ray Tracing Debug** visualization modes enable you to gather information about the ray tracing scene.

You can access these visualization modes from the Level Viewport using the **View Modes** dropdown selection, or by entering the console command `r.RayTracing.DebugVisualizationMode` followed by the name of the visualization mode.

![Ray Tracing Debug Visualization Modes selected through the Level viewport.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffd2edac-8749-44bc-bd35-542d8323358c/ray-tracing-debug-visualization-modes-dropdown.png)

### Picker Debug Visualization Mode

The `Picker` debug visualization mode displays information about the ray-tracing geometry and the instance under the cursor. The Picker mode can operate on two different domains: **Triangles** and **Instances**.

You can swap between these modes using the console command `r.RayTracing.Debug.PickerDomain` followed by **0**\* for Triangles (default) or **1** for Instances.

|   |   |
| --- | --- |
| 
 | 

 |
| Triangles Debug Picker Domain | Instance Debug Picker Domain |
| *Click image for full size.* | *Click image for full size.* |

On the left side of the viewport, information about the ray-tracing geometry is displayed along with which Picker Domain is currently being used.

![Debug Picker information displayed in the level viewport.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a6631e1-bfc0-49ce-871b-ce0b0c16340e/debug-picker-domain-display-information.png)

### Dynamic Instances Debug Visualization Mode

The `Dynamic Instance` debug visualization mode shows dynamic instances within the ray-tracing scene. Every frame, dynamic instances are rebuilt and show as either **Red** for static instances or **Green** for dynamic instances.

![Ray Tracing Debug Visualization Dynamic Instances](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecd33a0e-6158-4d56-9253-1c5c2e07d7ae/debug-vis-dynamic-instances.png)