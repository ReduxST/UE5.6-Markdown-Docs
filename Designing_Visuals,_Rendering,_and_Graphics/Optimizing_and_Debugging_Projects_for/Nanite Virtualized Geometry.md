# Nanite Virtualized Geometry

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:02

---

Nanite is Unreal Engine 5's virtualized geometry system which uses a new internal mesh format and rendering technology to render pixel scale detail and high object counts. It intelligently does work on only the detail that can be perceived and no more. Nanite's data format is also highly compressed, and supports fine-grained streaming with automatic level of detail.

[![Example Scenes with Nanite](https://dev.epicgames.com/community/api/documentation/image/76e6cac9-ba45-4fbc-aedd-9fec0965e229?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/76e6cac9-ba45-4fbc-aedd-9fec0965e229?resizing_type=fit)

## Benefits of Nanite

-   Multiple orders of magnitude increase in geometry complexity, higher triangle and objects counts than has been possible before in real-time
    
-   Frame budgets are no longer constrained by polycounts, draw calls, and mesh memory usage
    
-   Now possible to directly import film-quality source arts, such as ZBrush sculpts and photogrammetry scans
    
-   Use high-poly detailing rather than baking detail into normal map textures
    
-   Level of Detail (LOD) is automatically handled and no longer requires manual setup for individual mesh's LODs
    
-   Loss of quality is rare or non-existent, especially with LOD transitions
    

Although the advantages can be game-changing, there are practical limits that still remain. For example, instance counts, triangles per mesh, material complexity, output resolution, and performance should be carefully measured for any combination of content and hardware. Nanite will continue to expand its capabilities and improve performance in future releases of Unreal Engine.

## Differences Between a Nanite Mesh and Static Mesh

A Nanite mesh is a Static Mesh with Nanite enabled on it. A Nanite mesh is still essentially a triangle mesh at its core with a lot of level of detail and compression applied to its data. On top of that, Nanite uses an entirely new system for rendering that data format in an extremely efficient way.

All that is required for a Static Mesh to take advantage of Nanite is a flag to enable it. Authoring content for Nanite is no different than traditional meshes except that Nanite can handle orders of magnitude more triangles and instances than is possible for traditionally rendered geometry. Move the camera close enough and Nanite will draw the original source triangles that were imported.

Nanite meshes support multiple UVs and vertex colors. Materials are assigned to sections of the mesh such that those materials can use different shading models and dynamic effects which can be done in the shaders. Material assignment can be swapped dynamically, just like any other Static Mesh, and Nanite doesn't require any process to bake down materials.

[Virtual Textures](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-texturing-in-unreal-engine) are not required to be used with Nanite, but they are highly recommended. Virtual Textures are an orthogonal Unreal Engine feature with similar goals for texture data that Nanite achieves with mesh data.

Working with Nanite should be familiar to workflows for Static Meshes, but there are many things not yet supported. See the [Supported Features](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) section of this page for more details.

## How does Nanite work?

Nanite integrates as seamlessly as possible into existing engine workflows while using a novel approach to storing and rendering mesh data.

-   During import — meshes are analyzed and broken down into hierarchical clusters of triangle groups.
    
-   During rendering — clusters are swapped on the fly at varying levels of detail based on the camera view and connect perfectly without cracks to neighboring clusters within the same object. Data is streamed in on demand so that only visible detail needs to reside in memory. Nanite runs in its own rendering pass that completely bypasses traditional draw calls. Visualization modes can be used to inspect the Nanite pipeline.
    

Since Nanite relies on the ability to rapidly stream mesh data from disk on demand. Solid State Drives (or SSDs) are recommended for runtime storage.

## What Types of Meshes Should Nanite Be Used For?

Nanite should generally be enabled wherever possible. Any Static Mesh that has it enabled will typically render faster, and take up less memory and disk space.

More specifically, a mesh is an especially good candidate for Nanite if it:

-   Contains many triangles, or has triangles that will be very small on screen
    
-   Has many instances in the scene
    
-   Acts as a major occluder of other Nanite geometry
    
-   Casts shadows using [Virtual Shadow Maps](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine)
    

An example of an exception to these rules is something like a sky sphere: its triangles will be large on screen, it doesn't occlude anything, and there is only one in the scene. Typically these exceptions are rare and performance loss for using Nanite with them is fairly minimal so the recommendation is to not be overly concerned about where Nanite shouldn't be enabled if Nanite supports the use case.

Some use cases are not supported by Nanite currently. See the [Supported Features](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) section of this page for more details.

## Enabling Nanite Support on Meshes

Nanite can be enabled on supported geometry in the following ways:

-   [On import](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine)
    
-   [Using individual mesh editors](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine)
    
-   [Batched selection in the Content Browser](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine)
    

Converting geometry to Nanite requires some processing time for each mesh. On large projects, use of a shared Derived Data Cache (DDC) is especially helpful if there are many Nanite Assets. Please refer to the [Shared DDC](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine) documentation for more information.

### Importing a Mesh

When importing a mesh intended for us with Nanite, check the box for **Build Nanite**.

[![Nanite FBX Import Options](https://dev.epicgames.com/community/api/documentation/image/f03fafa7-52f6-4a06-b789-e1f579856879?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f03fafa7-52f6-4a06-b789-e1f579856879?resizing_type=fit)

We recommend disabling the **Generate Lightmap UVs** property when not using precomputed lighting with [Lightmass](https://dev.epicgames.com/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine).

When enabled, highly detailed goemetry adds significant time to importing and building Static Mesh Data. The property also adds an additional UV channel, which includes a significant amount of data for very dense meshes. If your project doesn't require baked lighting, there's no need to incur either cost.

### Enabling Nanite on Assets

In cases where you already have your project populated with content that you want to enable Nanite on, you have two options: enabling assets in batches using the Content Browser or enabling individual assets through their own editors.

#### Enable Nanite on Meshes in Batches

For batches of Static or Skeletal Mesh Assets that you want to enable Nanite for, use the **Content Browser** to select them all. **Right-click** and choose **Nanite > Enable** from the context menu.

[![Enable Nanite on Batches of Asset in the Content Browser](https://dev.epicgames.com/community/api/documentation/image/b2407a32-de73-4603-94ab-04a248c420ab?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b2407a32-de73-4603-94ab-04a248c420ab?resizing_type=fit)

#### Enable Nanite on Individual Meshes

Open the editor of any mesh that supports Nanite, such as static meshes and [Geometry Collections](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-collections-user-guide) (Chaos physics-driven fracture meshes), and enable Nanite through the **Details** panel.

In the Static Mesh Editor, locate the **Nanite Settings** and check the box for **Enable Nanite Support**.

[![Enable Nanite in the Static Mesh Editor](https://dev.epicgames.com/community/api/documentation/image/2ce1f1d1-2515-419b-8744-7ddc4624b579?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2ce1f1d1-2515-419b-8744-7ddc4624b579?resizing_type=fit)

In the Geometry Collections Editor, locate the **Nanite** section and check the box for **Enable Nanite**.

[![Enable Nanite on Geometry Caches](https://dev.epicgames.com/community/api/documentation/image/39938bd4-defb-4899-8569-26eecda1754e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/39938bd4-defb-4899-8569-26eecda1754e?resizing_type=fit)

## Supported Features of Nanite

This section describes how best to work with Nanite in an Unreal Engine project with details on what is and is not supported and possible limitations.

### Geometry

Nanite can be enabled on Static Meshes and [Geometry Collections](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-collections-user-guide).

A Nanite-enabled mesh can be used with the following Component types:

-   Static mesh
    
-   Skeletal mesh
    
-   Instanced static mesh
    
-   Spline mesh
    
-   Hierarchical instanced static mesh
    
-   Geometry collection
    
-   Foliage painter
    
-   Landscape grass
    

Nanite has limited support for the deformation of rigid meshes. Nanite supports dynamic translation, rotation, and non-uniform scaling of these meshes, whether it is dynamic or static. This means moving any position of a Nanite mesh in a way that is more complex than can be expressed in a single 4x3 matrix multiply, uniformly applied to the entire mesh.

Deformation is limited with:

-   (Beta) World Position Offset (WPO) in Materials.
    
    -   Nanite meshes using WPO displacement are split into smaller clusters whereby each of those clusters have their own individual bounds and are culled individually on the GPU. Clamp the WPO in order to manage how many clusters of the Nanite mesh are culled.
        
    -   Foliage using WPO is less problematic because the foliage is filled with holes and cannot really occlude itself.
        

Deformation is not supported with:

-   Morph Targets
    

The maximum number of instances that can be present in the scene is hard-locked to 16 million instances, which includes all instances that are streamed in, not just ones enabled for use with Nanite. Only instances streamed in are counted towards the total.

Per vertex tangents are not stored from the Static Mesh when it is enabled for Nanite. Instead, tangent space is implicitly derived in the pixel shader. Tangent data is not stored in order to reduce data size. This difference in tangent space using this approach could cause discontinuities at edges. However, this particular issue has not shown to be significant, and there are plans to support vertex tangents in a future release.

### Materials

Nanite supports materials that have their Blend Mode set to **Opaque** and **Masked**. When an unsupported material type is detected, a default material is assigned to the Nanite-enabled mesh and a warning is placed in the **Output Log** with additional information.

Additional material features notes:

-   Nanite-enabled meshes can receive decals projected onto their surfaces but do not support [Mesh Decals](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mesh-decals-in-unreal-engine), which require materials to use a **Translucent** Blend Mode.
    
-   **Wireframe** checkbox is not supported.
    
-   The **Vertex Interpolator** node and **Custom UVs** are supported but will be evaluated three times per pixel.
    
-   **Custom** expression nodes, or any nodes that use them (such as the `ParallaxOcclusionMapping` material function) might result in artifacts with Nanite. This is expected since Nanite doesn't yet have analytic derivative support yet.
    

### Rendering

The following rendering features are not currently supported:

-   View-specific filtering of objects using:
    
    -   Minimum Screen Radius
        
    -   Distance culling
        
-   Forward Rendering
    
-   Stereo rendering for Virtual Reality
    
-   Split Screen
    
-   Multisampling Anti-Aliasing (MSAA)
    
-   Lighting Channels
    
-   Ray-tracing against Nanite meshes
    
    -   The Fallback Mesh is used for Nanite-enabled meshes by default. Lower the **Fallback Relative Error** parameter in the Static Mesh Editor to use more of the source mesh's triangles.
        
    -   (Experimental) Initial support for native ray-tracing of Nanite meshes is enabled with the console variable `r.RayTracing.Nanite.Mode 1`. This preserves all detail while using significantly less GPU memory than zero-error Fallback Meshes.
        
-   Some visualization view modes do not yet support displaying Nanite meshes
    
    Use caution with some visualization modes in the Static Mesh Editor when viewing highly detailed geometry. Viewing Normals and UV can cause problems with editor performance.
    

### Supported Platforms

Nanite is currently supported on PlayStation 5, Xbox Series S|X, and PCs with graphics cards meeting these specifications, using the latest drivers with DirectX 12 with Shader Model 6 (SM6):

-   NVIDIA: Maxwell-generation cards or newer
    
-   AMD: GCN-generation cards or newer
    
-   All newer versions of Windows 10 (newer than version 1909.1350) and Windows 11 with support for [DirectX 12 Agility SDK](https://devblogs.microsoft.com/directx/gettingstarted-dx12agility) are supported.
    
    -   Windows 10 version 1909 — The revision number should exceed or be equal to .1350.
        
    -   Windows 10 version 2004 and 20H2 — The revision number should exceed or be equal to .789.
        
    -   DirectX 12 with Shader Model 6.6 atomics, or Vulkan (VK\_KHR\_shader\_atomic\_int64)
        
-   Apple Silicon M2 or newer.
    
-   Linux with a NVIDIA GeForce 2080 or newer.
    
-   Latest Graphics Drivers
    

PlayStation 4 and Xbox One also support Nanite, but support on these platforms is currently considered experimental. It is expected that the performance of Nanite on these platforms with very high fidelity content may not meet the requirements of a shippable game.

For additional information about hardware and software specifications recommended by Epic Games, see [Hardware and Software Specifications](understanding-the-basics\installing-unreal-engine\hardware-software-specifications).

## Nanite Fallback Mesh and Precision Settings

Static and Skeletal Meshes include additional properties that control the precision of the Nanite representation and the Fallback Mesh generated from the full-detail mesh.

These settings are located in the Mesh Editor's **Details** panel under the **Nanite Settings** section.

[![Static Mesh Editor Nanite Settings](https://dev.epicgames.com/community/api/documentation/image/239c86d0-3365-4aa0-94a5-0a1eed6de73f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/239c86d0-3365-4aa0-94a5-0a1eed6de73f?resizing_type=fit)

Nanite settings include the following properties:

| Property | Description |
| --- | --- |
| 
**Enable Nanite Support**

 | 

Enables this mesh to be used with Nanite and to generate a Fallback Mesh in situations where Nanite cannot be used.

 |
| 

**Preserve Area**

 | 

Enables Nanite meshes that would lose surface area due to simplification to redistribute that lost area to the remaining triangles by dilating out the open boundary edges. This is most useful for foliage where leaves tend to become disjoint triangles and quads through simplification. The effect of this setting is to scale each leaf up. For geometry ribbons, like blades of grass, it has the effect of thickening them. This setting should be enabled on all foliage meshes and nothing else.

 |
| 

**Explicit Tangents**

 | 

When true, the original model tangents are stored and used per asset. This setting means tangents are stored explicitly on disk instead of being derived implicitly at runtime. The Tangent Precision setting becomes available for additional control of vertex tangents. Enabling the setting increases storage by roughly 10% but can be preferable when implicit tangents are not precise enough.

 |
| 

**Lerp UVs**

 | 

Whether to interpolate UVs when simplifying. This should be enabled whenever possible. For real UV coordinates, this allows calculating the lowest error optimal UVs for new vertices when simplifying, assuming the UVs are used as normal texture coordinates and will interpolate across the face of the triangles. This should be disabled if data stored in the UVs isn't valid to interpolate. For example, if indexes are stored in UVs. Lerping an index doesn't make snese and would break the shader trying to use it.

If disabled, error from UVs is no longer accounted for when Nanite selects the LOD to render because error due to arbitrary vertex attributes that aren't interpolatable can't be generally reasoned about.



 |
| 

**Position Precision**

 | 

Choose the precision this mesh should use when generating the vertex positions of a Nanite mesh. **Auto** determines the appropriate precision based on the size of the mesh. The precision can be overridden to improve precision or optimize disk footprint.

 |
| 

**Normal Precision**

 | 

Choose the precision this mesh should use when generating the vertex normals of a Nanite mesh. **Auto** determines the appropriate precision based on the size of the mesh. The precision can be overridden to improve precision or optimize disk footprint.

 |
| 

**Minimum Residency (Root Geometry)**

 | 

Sets the memory byte size this mesh should always keep in memory and has the rest streamed in. Higher values require more memory, but for some meshes, this can mitigate streaming pop-in issues from occurring.

 |
| 

**Keep Triangle Percent**

 | 

The percentage of triangles to keep from the source mesh. Reduce this percentage to optimize disk size.

 |
| 

**Trim Relative Error**

 | 

Sets the maximum amount of relative error that is allowed to be removed for the Nanite mesh. All detail in the source mesh with less visual impact than this relative error amount is removed. The relative error does not have a unit size and is relative to the size of the mesh. By default, Nanite stores all of the original source mesh's triangles.

 |
| 

**Fallback Target**

 | 

Determine which targeting system to use when generating a fallback mesh.

**Auto:** Automatically create a fallback mesh based on project settings. **Fallback Triangle Percent:** Sets the percentage of triangles that remain when reducing the source mesh for Nanite. **Fallback Relative Error:** Reduce until the specified error is reached relative to the mesh size. All detail in the generated Fallback Mesh with less visual impact than this relative error amount is removed.

 |
| 

**Source Import Filename**

 | 

The file path used to import a high resolution mesh for use with Nanite. The high resolution version of the mesh is used in place of LOD0 by systems that can benefit from more detailed geometry, such as Nanite and Geometry Modeling in Unreal Engine.

 |
| 

**Displacement UV Channel**

 | 

UV channel to use when sampling displacement maps.

 |
| 

**Displacement Maps**

 | 

Add and edit displacement maps.

 |
| 

**Max Edge Length Factor**

 | 

Controls the maximum distance allowed between each vertex of the mesh on screen. This can be used to prevent over-simplification of meshes that are intended to be deformed, such as animation using world position offset, and spline meshes. This should be left at 0 by default unless explicitly needed to fix issues caused by over-simplification.

 |

### Vertex Precision

Nanite quantizes mesh vertex positions to maximize memory density and minimize disk footprint. The quantization step size is a power of two that can be selected to match the requirements of individual meshes using the **Position Precision** property. By default, **Auto** picks the appropriate precision based on the size of the mesh and its triangle density. You can manually override by selecting a precision size to improve precision or optimize disk footprint.

[![Static Mesh Editor Nanite Settings for Position Precision](https://dev.epicgames.com/community/api/documentation/image/45358caf-bc13-4a0f-8c37-990a7139b29f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/45358caf-bc13-4a0f-8c37-990a7139b29f?resizing_type=fit)

Qantinization is a form of lossy compression. Lossy compression is particularly challenging when working with modular mesh pieces, or other meshes that have shared boundaries. Especially when those boundaries need to align perfectly to not introduce holes or cracks in the geometry.

To ensure consistency, quantization happens in unnormalized object coordinates centered around the mesh origin. This ensures that the quantization never causes cracks when the mesh uses the same precision setting, and the translation between the mesh center is a multiple of that precision.

### Trimming data

There are times when you'll need to reduce the amount of data Nanite stores to optimize for disk size. Nanite includes settings which allow you to trim the detail data from a stored Nanite mesh at any time during production, meaning that you can safely overshoot quality up front and adjust accordingly later on.

To trim the detail data, you will want to use the **Keep Triangle Percent** and **Trim Relative Error** properties. You can think of them as a pre-decimate option before being stored as a Nanite mesh. In Nanite's case, detail doesn't need to be uniform across the mesh. It removes the least significant data first and is more akin to lossy compression.

Use **Keep Triangle Percent** to set the percentage of triangles to keep from the source mesh.

Use **Trim Relative Error** to set the maximum amount of relative error that is allowed when trimming the data from the source mesh. Any triangle that if removed would incur a relative error less than this amount is removed. Or another way to think about this is all detail with less visual impact than this value is trimmed. The relative error does not have a unit size and is relative to the size of the mesh.

The defaults for both of these properties are such that nothing is trimmed by default, and Nanite stores all of the original source mesh's triangles.

Trimming data is important to reducing disk size (in other words, download size), not for improving performance. See Data Size section below for more on this topic.

### Fallback Mesh

Many parts of Unreal Engine need access to the traditional vertex buffer provided by traditionally rendered meshes. When you enable Nanite for a Static Mesh, it generates a coarse representation (called a Fallback Mesh) of the highly detailed mesh. The Fallback Mesh is used when Nanite rendering is not supported. It is also used when it wouldn't be ideal to use the full-detail mesh, like when a complex collision is needed, using lightmaps for baked lighting is required, and for hardware ray tracing reflections with Lumen.

The **Fallback Triangle Percent** property represents the percentage of triangles from the original source mesh that are used to generate the Fallback Mesh. You can specify the percentage of triangles to keep between 0 and 100 percent, where large percentages keep more of the original mesh's detail.

The **Fallback Relative Error** sets the maximum amount of relative error that is allowed when removing details from the source mesh. Any triangles that if removed would incur a relative error less than this amount are removed with detail of less visual impact being first to go. The relative error does not have a unit size and is relative to the size of the mesh.

For example, if you wanted your mesh to not have any decimation at all, you would use a Fallback Triangle Percentage of 100 and a Fallback Relative Error of 0.

In the comparison below, there is the highly detailed Nanite mesh created from the original source mesh which is compared with default settings of a generated Nanite Fallback Mesh.

![High Poly Nanite Mesh](https://dev.epicgames.com/community/api/documentation/image/ed275137-6198-4aaa-a9dc-2999dd99dc6a?resizing_type=fit&width=1920&height=1080)

![Nanite Generated Fallback Mesh | Default Settings](https://dev.epicgames.com/community/api/documentation/image/122fd9d2-f7c8-4809-bf9f-64acc0888460?resizing_type=fit&width=1920&height=1080)

High Poly Nanite Mesh

Nanite Generated Fallback Mesh | Default Settings

Use the Fallback Relative Error to specify how much of the original detail is retained from the original source mesh, and the Fallback Percentage to set how much of that detail is used.

In the comparison below, the Fallback Mesh keeps 100 percent of the Fallback Triangle Percent but adjusts the Fallback Relative Error to use more of the triangles from the original source mesh. When adjusting these values, you can use the Nanite details for Nanite Triangles in the viewport as an indicator when changing their values.

![Nanite Generated Fallback Mesh | Default Settings](https://dev.epicgames.com/community/api/documentation/image/7784c832-5223-4020-a9d5-a8219433574d?resizing_type=fit&width=1920&height=1080)

![Nanite Generated Fallback Mesh | Adjusted Settings for Quality](https://dev.epicgames.com/community/api/documentation/image/13d71a07-ed15-45a9-8210-b16bb43aa669?resizing_type=fit&width=1920&height=1080)

Nanite Generated Fallback Mesh | Default Settings

Nanite Generated Fallback Mesh | Adjusted Settings for Quality

#### Fallback Mesh Visualization

In the Static Mesh Editor, you can toggle between the fully detailed Nanite mesh and the Nanite Fallback Mesh using the viewports **Nanite Fallback** option in the **Show** dropdown menu. Alternatively, you can use the hotkey **Ctrl + N** to quickly toggle between the two visualization options.

[![Static Mesh Editor Nanite Fallback Mesh Toggle](https://dev.epicgames.com/community/api/documentation/image/a934096c-d836-4dc5-a273-a8493bb86d4d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a934096c-d836-4dc5-a273-a8493bb86d4d?resizing_type=fit)

#### Using Custom Fallback Mesh LODs for Nanite-enabled Meshes

The Fallback Mesh is used for engine features, such as complex per-poly collision, ray tracing, light baking, and so on. It is also used for platforms that do not support Nanite. When generating the Fallback Mesh, a Nanite-enabled mesh always uses the **LOD0** slot of the source mesh for auto-generating the fallback mesh. However, there are times when it is desirable to use a manually specified fallback mesh, or a series of traditional LODs, rather than an auto-generated one.

This level of control would allow you to use Nanite in a project but also directly control the geometry seen in ray-traced reflections, or on platforms that do not support Nanite.

Follow the steps below to specify your own custom fallback mesh, or to use a series of LODs:

1.  Set the **Fallback Triangle Percent** to **0** so that the fallback mesh is as small as possible since it will be ignored when using this approach.
    
2.  Add one or more LODs to the mesh using this [traditional LOD setup](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-levels-of-detail-in-blueprints-and-python-in-unreal-engine) procedure.
    
3.  Use the **LOD Import** dropdown to **Import LOD Level 1** from the **LOD Settings** section.
    
4.  Set the **Minimum LOD** to **1** under the **LOD Settings** section. This causes the Nanite-generated Fallback Mesh to be ignored.
    

Complex Collision presents a special case. Use the **LOD for Collision** property under **General Settings** to specify which LOD should be used for collision. Any LOD can be used for collision, including LOD0.

This particular approach may not be feasible to make Nanite projects automatically compatible with non-Nanite-supporting platforms, and should be tested and evaluated for your project.

Nanite efficiently handles very large numbers of instances, but if Nanite is disabled, there could be an overwhelming number of draw calls for the traditional render pipeline. You can test this in your project for feasibility using the `r.Nanite 0` to toggle Nanite support off and on.

See the [Console Variables and Commands](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) section of this page for more information.

## Working with Nanite-Enabled Content

In most cases, Nanite scales extremely well within screen resolution. It does so based on two techniques: fine-grained level of detail and occlusion culling. Typically this means, regardless of the geometric complexity of the source data in the scene, the number of triangles Nanite attempts to actually draw to the screen is consistent and proportional to the number of pixels.

Nanite follows the design principle that there is no use in drawing far more triangles than there are pixels.

However, there are some cases of content that break the techniques Nanite uses to scale, but this doesn't mean it should not be used at all for this content, or that it will not render faster than the traditional rendering pipeline. It only means that for this type of content, scaling with pixels — and not scene complexity — no longer applies to them. Use the [Profiling](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) features provided by Unreal Engine to monitor these types of situations when they occur.

### Aggregate Geometry

Aggregate geometry is geometry that has many disjointed parts that become a volume in the distance, such as hair, leaves on trees, and grass. This type of geometry breaks the level of detail and occlusion culling techniques of Nanite. Nanite is inherently a hierarchical level of detail structure that relies on being able to simplify small triangles into larger triangles and choosing the coarser one when it determines the difference is smaller than can be perceived. For continuous surfaces, this works well, but not for aggregate geometry that from a distance appears more like a partially opaque cloud than a solid surface. As such, Nanite is more likely to determine it cannot reduce aggregate geometry nearly as aggressively as it would typical solid surfaces, thus resulting in more triangles being drawn for the same number of pixels covered.

Another optimization that aggregate geometry breaks is Occlusion Culling. Although it is very fine-grained, its granularity is not per pixel. Geometry that is filled with holes — and worse yet, layers upon layers of geometry filled with holes — causes excessive overdraw because many depth layers need to build up before that area on the screen will block anything behind it. One way to think about this is to consider an 8x8 pixel region on screen and how many depth layers need to be drawn before every pixel is filled. Excessive overdraw means that for the same number of pixels covered, Nanite attempts to draw more triangles causing it to render slower.

Foliage is the most obvious case for causing problems with occlusion culling, but even then, it does not mean that Nanite should not be used on foliage-type meshes at all. Refer to the [Foliage Using Nanite](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) section below for more. It is good to experiment with different use cases and see what works well for your projects. Use profiling tools to confirm good performance from Nanite with these types of meshes.

### Closely Stacked Surfaces

Occlusion culling with traditional meshes makes kitbashing workflows nearly impossible on a large scale due to practical limitations. The fine-grained nature of occlusion culling with Nanite makes it possible to use these types of workflows during development with less concern. As is explained in the Aggregate Geometry section above, overdraw can come from hidden surfaces being very close to visible surfaces below them. If any geometry is buried well below the visible surface, Nanite detects and culls it fairly cheaply, such that it can mostly be considered free of cost. However, when there is stacked geometry that is close together near the top-most surface, Nanite is not able to determine which is on top or bottom, causing both to be drawn simultaneously.

This particular issue with culling is a worst-case scenario where Nanite does not know which surface is on top, and just draws all the layers instead. Imprecision like this scales with screen size and distance, so while 10 centimeters may separate layers and look fine while close to the surface, farther distances away can cause the difference in distance to be smaller than a pixel, resulting in overdraw.

![Game View](https://dev.epicgames.com/community/api/documentation/image/fd2bc359-ebae-46ea-8f31-89bda9390d6d?resizing_type=fit&width=1920&height=1080)

![Many Nanite instances closely stacked together](https://dev.epicgames.com/community/api/documentation/image/956b9641-e675-49a4-9c8d-2c42fab1df12?resizing_type=fit&width=1920&height=1080)

Game View

Many Nanite instances closely stacked together

In the example below, if the camera is moved to look down at the area where the character is standing, the Nanite **Overdraw** visualization shows how these stacked surfaces are being rendered. Brighter areas indicate more overdraw is happening in those areas than others.

[![Nanite Overdraw Visualization](https://dev.epicgames.com/community/api/documentation/image/be3d9c68-0980-42d3-aba3-2e29872b16fc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/be3d9c68-0980-42d3-aba3-2e29872b16fc?resizing_type=fit)

The Overdraw visualization is the most effective way to find issues of overdraw. While some amount of overdraw should be expected, excessive amounts of it result in Nanite culling and rasterization costs becoming higher, and Nanite's scaling independently of scene complexity will become less effective in the process.

### Faceted and Hard-edge Normals

One issue to be mindful of is when importing highly detailed meshes that have faceted normals, meaning that the normal between two different polygons was not smoothed. This issue is common and easy to miss and caution should be taken to avoid this particular issue because low amounts of vertex sharing in a mesh can become significantly more expensive both in rendering performance and data size. Ideally, the number of vertices for a mesh should be less than the number of triangles it has. If the ratio is 2:1 or higher, then there is likely a problem, especially if this results in a high triangle count. Having a ratio of 3:1 means the mesh is completely faceted where every triangle has its own three vertices, none of which are shared with another triangle. Most often, this is caused by the normals not being the same because they are not smoothed.

With that in mind, more vertices means more data to store. It also means more vertex transform work, and ratios higher than 2:1 fall down some slow rendering paths. Intentional use in hard surface modeling shouldn't cause any issues, and there is no reason not to use them. However, accidental 100% facet very dense meshes are far more expensive than intended. Another thing to watch out for is imported normals on dense organic-type surfaces generated in other DCC packages that have hard normal thresholds that might be sensible on lower polygon meshes, but can add unnecessary expense with Nanite.

For example, In the two meshes below, the mesh on the left has faceted normals while the one on the right has smoothed normals. When comparing these using the Nanite **Triangles** visualization, there are noticeable differences in the number of triangles used by Nanite to draw them. The faceted one on the left draws significantly more triangles than the smoothed one on the right.

|   |   |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/0167f7ef-9c68-4cfb-907d-45732dd4b89b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0167f7ef-9c68-4cfb-907d-45732dd4b89b?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/95469aa9-ecf9-4cf8-9506-c5a67b562343?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/95469aa9-ecf9-4cf8-9506-c5a67b562343?resizing_type=fit)



 |
| 

Nanite-enabled meshes with faceted (left) and smoothed (right) normals

 | 

Nanite Triangle Visualization of Nanite-enabled meshes with faceted (left) and smoothed (right) normals

 |
| 

Click the image for full size.

 | 

Click the image for full size.

 |

### Nanite Skeletal Mesh

This feature of Nanite is currently experimental.

[![](https://dev.epicgames.com/community/api/documentation/image/84be709e-fa73-4758-ac97-06789a689894?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/84be709e-fa73-4758-ac97-06789a689894?resizing_type=fit)

Nanite Skeletal Meshes include support for:

-   A new Skeletal Mesh API making it simpler to achieve rendering them.
    
-   One draw call for an entire mesh.
    
-   Shadowing from Virtual Shadow Maps.
    
-   No geometry LODs. Nanite Skeletal Mesh uses animation LODs.
    
-   Instancing with animation banks.
    

### Foliage Using Nanite

Foliage using Nanite is considered Beta and is being actively researched and developed. This seciton provides some guidance on using foliage geometry with Nanite.

For assets like trees with default Nanite settings you might find that the canopies tend to thin out with distance. These cases are a particular form of [Aggregate Geometry](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) where each disjoint part (a leaf or grass blade) has open edges at its boundary. Enabling **Preserve Area** is useful to prevent this thinning out when Nanite is enabled. When Nanite simplifies the geometry in the distance by reducing the number of triangles, it eventually needs to start removing some of these disjoint elements completely. Without Nanite having more information the result will look thinned out because there was major surface area loss. Preserve Area will redistribute that lost area to the remaining triangles by dilating out the open boundary edges. Dilation for symmetric shapes like leaves has the same effect as scaling them up. In non-symmetric cases like ribbons, for example, blades of grass, it has the effect of thickening them.

We recommend using **Preserve Area** for all foliage meshes, but *not* for meshes that are not intended to be used as scene foliage.

![Without Preserve Area](https://dev.epicgames.com/community/api/documentation/image/50d09663-706b-41a1-b663-25d620f4b606?resizing_type=fit&width=1920&height=1080)

![With Preserve Area Enabled](https://dev.epicgames.com/community/api/documentation/image/858d0f45-57bc-44ea-9e2c-27b635873957?resizing_type=fit&width=1920&height=1080)

Without Preserve Area

With Preserve Area Enabled

The Nanite **Cluster** visualization provides a clearer look at how the Preserve Area setting redistributes lost area.

![Nanite Cluster Visualization | Without Preserve Area](https://dev.epicgames.com/community/api/documentation/image/652c1340-cd79-4614-9ceb-4685ed3a2d45?resizing_type=fit&width=1920&height=1080)

![Nanite Cluster Visualization | With Preserve Area Enabled](https://dev.epicgames.com/community/api/documentation/image/91ef1d49-ad5b-47a3-af3d-8efa114c19e1?resizing_type=fit&width=1920&height=1080)

Nanite Cluster Visualization | Without Preserve Area

Nanite Cluster Visualization | With Preserve Area Enabled

Below are some recommendations when using and authoring foliage assets with Nanite in mind. We are still experimenting and learning ourselves what are the best approaches. So far, we have seen that foliage using Nanite should be authored differently than before, but if you play to its strengths, you can get faster, higher-quality results using Nanite.

-   Use **Preserve Area** (enabled in the Static Mesh Editor).
    
-   Use geometry instead of masked cards.
    
    -   Masked materials are fairly expensive compared to Opaque ones. The fastest results are likely obtained by not using them at all.
        
    -   The traditional card approach (many elements are represented with a single card) with Nanite can be slower than non-Nanite. Do not expect that enabling Nanite on card-based foliage will always be a performance improvement.
        
    -   Masked-out pixels cost nearly as much as drawn pixels.
        
    -   Geometry foliage has shown to be faster with Nanite than card approaches, both Nanite cards and non-Nanite cards. It also looks better.
        
        -   The [Megascans: Grass](https://www.fab.com/listings/50d9a417-73ed-4132-9421-6be3d4f7432e) pack on Fab offers good examples for testing. The pack offers both masked and high-poly geometry where each element is independent and masked low-poly cards where many elements are represented by a single card.
            
-   When using World Position Offset (WPO), more vertices equal higher cost. WPO logic must be limited and monitored.
    
-   The issues explained in the [Aggregate Geometry](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) section of this page still apply. Dense forests (like the examples above) will render much slower than the same scene with all meshes replaced with solid shapes of the same triangle count.
    

### Using Max World Position Offset Displacement with Nanite

In your materials and material instances, you can use the **Max World Position Offset Displacement** setting to set an upper limit to the amount of offset WPO is allowed to have. This can be especially useful for Nanite meshes because they are split into smaller clusters whereby each of those clusters have their own individual bounds and are culled individually on the GPU. Clamping WPO is a good way to manage this.

You can find the **Max World Position Offset Displacement** setting under the material's **Details > World Position Offset** category, or under **Material Property Overrides** in a material instance.

[![Max World Position Offset Displacement setting](https://dev.epicgames.com/community/api/documentation/image/3f8d6f8b-66e1-4c34-88bf-eb5c555be4a3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3f8d6f8b-66e1-4c34-88bf-eb5c555be4a3?resizing_type=fit)

For more details, see [Material Properties](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-properties).

### Nanite Static Displacement Mapping

This feature of Nanite is currently experimental.

The Static Mesh Editor includes an option to add detail to Nanite-enabled meshes through an offline adaptive tessellator. The tessellator generates an optimized Nanite mesh using displacement maps baked into it. This texture-driven approach is non-destructive and allows you to control the amount of tessellation and displacement through scalar parameters.

[![Examples with and without Nanite Static Displacement mapping](https://dev.epicgames.com/community/api/documentation/image/e43dda87-e2a8-4f2e-a0ae-1ffbe0bbbc93?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e43dda87-e2a8-4f2e-a0ae-1ffbe0bbbc93?resizing_type=fit)

In the Details panel under Nanite Settings, do the following:

1.  Set the **Trim Relative Error** to a value other than 0 to control the amount of tessellation.
    
    -   A good default is 0.04, but you should keep it above 0.02. This value targets an error level when tessellating the mesh. Going too small will simply use a lot of triangles and inflate build times.
        
2.  Add **Displacement Maps**.
    
3.  Expand the **Index** element and add a **Texture** to use for displacement.
    
    -   If your mesh has more than one material slot, each Displacement Maps index is mapped to the corresponding material slot. For example, Material Slot 0 would map to Displacement Maps Index 0, Material Slot 1 would map to Index 1, and so on.
        
4.  Set a **Magnitude** to control the amount of displacement.
    
5.  Click **Apply Changes**.
    

### Nanite Tessellation

This feature of Nanite is currently experimental.

Nanite tessellation is dynamic programmable displacement that allows for Nanite meshes to be modified at runtime using a displacement map or procedural material. This is unlike World Position Offset which can only operate on the original mesh vertices, Nanite displacement tessellates the mesh at runtime into additional triangles to conform to the detail of the displacement map. Only as much triangle detail required for the current pixel density is generated.

The benefits of Nanite tessellation include:

-   Using source meshes that include less detail in the authoring pipeline.
    
-   Material-driven and animated displacement.
    
-   Creating detailed Nanite landscapes.
    

|   |   |
| --- | --- |
| 
[![With Nanite Tessellation](https://dev.epicgames.com/community/api/documentation/image/31a6b724-4562-496a-a674-4e687d0f25e6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/31a6b724-4562-496a-a674-4e687d0f25e6?resizing_type=fit)



 | 

[![Without Nanite Tessellation](https://dev.epicgames.com/community/api/documentation/image/37296521-21d3-4edb-956f-7a7aa279aadf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/37296521-21d3-4edb-956f-7a7aa279aadf?resizing_type=fit)



 |
| 

With Nanite Tessellation

 | 

Without Nanite Tessellation

 |

*Click image for full size.*

To enable Nanite tessellation, you need to set the following console variables in the **ConsoleVariables.ini** or your project’s .ini configuration files:

C++

`// This is read-only and must be set in the config file for the project. r.Nanite.AllowTessellation=1  // This can be dynamically toggled at runtime. r.Nanite.Tessellation=1`

// This is read-only and must be set in the config file for the project. r.Nanite.AllowTessellation=1 // This can be dynamically toggled at runtime. r.Nanite.Tessellation=1

Copy full snippet(5 lines long)

Once these variables are set, you can set up tessellation using the Material Editor by following these steps:

1.  Select the main material node.
    
2.  In the **Details** panel under the **Nanite** settings, check the box for **Enable Tessellation**.
    
3.  Connect a Texture Sample to the **Displacement** input on the main material node.
    

[![](https://dev.epicgames.com/community/api/documentation/image/71b68e59-4155-497d-b78b-40927fd9df88?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/71b68e59-4155-497d-b78b-40927fd9df88?resizing_type=fit)

The Displacement input value range is 0-1.

There are two settings to configure when using tessellation in a material:

-   **Magnitude:** This is the height of the displacement measured from min to max that the Displacement pin’s 0-1 range maps to. It also dictates the bounds that are used for culling, so only set this as large as is necessary.
    
    This value has a significant impact on performance, and can have other unintended effects. For more information, see the “Things to know” section below.
    
-   **Center:** This specifies what displacement value corresponds to no change from the base mesh. So if mid gray is the center and you want equal displacement both in and out of the mesh, use 0.5. If you want to only push outwards, set this to 0.
    

Additionally, in a material, you can optimize Nanite Tessellation with **Displacement Fade** enabled in the Details panel. It has two settings:

-   **Start Fade Size (Pixels):** How large the max displacement should be, in on-screen pixels, when beginning to fade out displacement. This value should be a **larger** number than the End Fade Size value.
    
-   **End Fade Size (Pixels):** How large the max displacement should be, in on-screen pixels, when fading out should complete, and displacement should be disabled. This value should be **smaller** than the Start Fade Size.
    

**Things to know:**

-   Only works on Nanite meshes. Tessellation and displacement are ignored on non-Nanite meshes or in cases where Nanite isn’t supported.
    
-   Displacement doesn’t change shading (unlike offline renderers). You need to supply a corresponding normal map or derive a normal from the displacement derivatives. For the sake of quality and compression, we recommend having an additional normal map.
    
-   Scalar displacement only. Vector displacement is not currently supported.
    
-   Displacement is along the unnormalized interpolated vertex normal. There is no option currently to control the displacement direction in the shader. It is always along the normal.
    
-   Displacement is in local space, and is before any sort of object scale. That means the displacement Magnitude specified in the material is in object space units before the scaling of the mesh. This is often what you want but may not be. For example, in cases where you want a tiling brick on a cube you scaled to be a wall. We will likely add an option for world space in the future to address these cases.
    
-   Tessellation and displacement works on Landscape as well, so long as Nanite has been generated for it. Unfortunately, the meshes Landscape generates have a significant scale automatically applied to them so be sure to use much smaller Magnitude for Landscape materials. Like 64x smaller. This will likely be addressed in the future using the option mentioned in the previous point.
    
-   Keep the Magnitude setting’s value as small as is necessary. Instead, try to use the entire 0-1 range of the Displacement output. Don’t set the Magnitude to 100 and then scale down the value you plug into the Displacement output to compensate. The reason for this is because the Magnitude value is used to bound patches for culling. If the Magnitude is large it can have serious impacts on performance, especially with Virtual Shadow Maps.
    
-   There is currently no solution for crack-free displacement, like what Unreal Engine 4 had with hardware tessellation. This means that UV seams, hard edge normals, or any vertex attribute affecting the displacement that isn’t smooth will cause cracks.
    
-   Tessellation can be combined with World Position Offset. WPO in this case is applied to the base mesh vertices before tessellation. Displacement, like always, applies to the diced triangle vertices after tessellation.
    
-   Tessellation is not compatible with Pixel Depth Offset. PDO will be ignored if tessellation is enabled.
    
-   Tessellation can be combined with Opacity Mask but for performance reasons the masking is done at diced triangle rate, not per pixel. For most use cases this should be fine but will not work well with dithering since that really needs to be per pixel.
    
-   It’s possible for texture compression artifacts to be obvious for displacement maps and appear like staircase stepping. Texture compression setting Alpha, which uses BC4, works decently in many cases. Stored in the alpha of an RGBA with Default/DXT5/BC3 should get similar results. Sometimes uncompressed may be required but floating point is likely overkill. Channel packing, especially packing height with normals, with any compressed format will likely show artifacts. This may run counter to prior experience when heightmaps were used for other purposes.
    
-   Displacement is relative to the flat triangles of the base mesh. That means it does not start from a curved surface like PN triangles or Catmull-Clark subdivision surfaces. Tessellation doesn’t inherently smooth the surface.
    

### Nanite Splines

Spline meshes are used for deforming meshes along the shape of a spline, such as roads and paths over a landscape terrain. Nanite-enabled meshes support splines by default and can be created as [Landscape Splines](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-splines-in-unreal-engine) and [Blueprint Splines](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-splines-in-unreal-engine).

[![Nanite Spline Example](https://dev.epicgames.com/community/api/documentation/image/9b13f805-a33c-4e40-b61d-1265b83586e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b13f805-a33c-4e40-b61d-1265b83586e0?resizing_type=fit)

*Example scene with Nanite mesh in foreground and Nanite Spline. This scene shows the Lit and Nanite Triangles visualization.*

Nanite spline meshes can have potential for visual issues. One such way is when creating a spline mesh with a Nanite-enabled static mesh, it is possible for the spline mesh to drop to a lower resolution as the camera travels away from it. This happens because Nanite doesn’t take into account deformation of spline meshes when generating its lower level of detail (LOD). As a result, simplifications that are unnoticeable at the same distance when undeformed can become obvious when stretched along a spline curve.

You can mitigate this deformation issue with the **Max Edge Length Factor** setting found in the Static Mesh Editor under **Nanite Settings** in the Details panel. This parameter mitigates this issue by coercing Nanite to keep enough detail to maintain a desired amount of distance between vertices of the mesh on screen, preventing the mesh from rendering below some threshold of vertex density.

[![Nanite Setting Max Edge Length Factor](https://dev.epicgames.com/community/api/documentation/image/948e5ba2-d62c-48b1-83e2-e75db6a2429b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/948e5ba2-d62c-48b1-83e2-e75db6a2429b?resizing_type=fit)

The default Max Edge Length Factor is 0. This indicates that the edge length will not be considered for this mesh. Values greater than 0 represent a desired distance between any two connected vertices in screen space. More specifically, this distance is represented as a multiple of the smallest desired Nanite triangle edge (as configured by `r.Nanite.MaxPixelsPerEdge`).

#### Upgrading to Nanite Splines from a Previous Engine Version

For projects made with Unreal Engine 5.3 and earlier, Spline Mesh Components that used Nanite-enabled static meshes would previously render Fallback meshes generated from the Nanite mesh as ordinary static meshes. Because rendering splines with Nanite is now enabled by default in Unreal Engine 5.4, these meshes will now render as Nanite, which can result in visual differences.

To retain the previous behavior of having Nanite’s fallback mesh render as the spline mesh, you can set `r.SplineMesh.RenderNanite` to **0**.

## Hybrid Non-Nanite and Nanite Content Workflows

The following sections highlight workflows you can use in your Nanite-enabled projects that need to also support non-Nanite features and platforms without duplicating assets.

### Importing a High-Resolution Mesh for Nanite

You can import a high resolution mesh to be your Nanite representation for any existing non-Nanite Static Meshes through the **Content Browser** or the **Static Mesh Editor**.

From the **Content Browser**, you can use the right-click context menu on a Static Mesh Asset to select **Level of Detail > High Res > Import High Res** and navigate to the file you want to import.

[![Content Browser right-click import high resolution level of detail option for assets.](https://dev.epicgames.com/community/api/documentation/image/6e3323b8-7ad0-4ac2-9a06-8b858e478440?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6e3323b8-7ad0-4ac2-9a06-8b858e478440?resizing_type=fit)

Alternatively, you can use the **Static Mesh Editor** to import a high resolution mesh using the **Nanite** Settings in the **Details** panel. Click **Import** and navigate to the file you want to import.

[![Static Mesh Editor Nanite import high resolution mesh options.](https://dev.epicgames.com/community/api/documentation/image/4682049e-5a49-4744-b447-debccc6f1bb7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4682049e-5a49-4744-b447-debccc6f1bb7?resizing_type=fit)

Using this workflow, the pre-existing Static Mesh and its level of detail (LOD) chain become the **Fallback Mesh** rather than having the import process automatically generate a Fallback Mesh from the Nanite geometry.

This workflow respects the **Disallow Nanite** setting on Static Mesh Actors in your scenes and is explained more in the [Static Mesh Component Options](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) section below.

### Material Workflows

There are two ways you can improve your non-Nanite and Nanite workflows with materials: by using a node in the material graph to break up logic paths, or by using an override material only used for rendering with Nanite.

#### Nanite Pass Switch Node

The **Nanite Pass Switch** node allows you to define specialized behavior in a material graph when rendered with Nanite.

[![Nanite Pass Switch Material Node](https://dev.epicgames.com/community/api/documentation/image/cf2d1f1c-1705-41ef-85e6-52f61faabd99?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cf2d1f1c-1705-41ef-85e6-52f61faabd99?resizing_type=fit)

Use the **Default** input when rendering into non-Nanite passes, to handle the material as it would be normally. Use the **Nanite** input for any material logic you want to simplify or be specifically rendered to Nanite passes. For example, in cases where a material uses a feature not supported by Nanite, you could keep the same logic for the Default input and use a friendlier logic for the Nanite input.

#### Nanite Override Material

The **Nanite Override Material** slot is available on Materials and Material Instances. When you set an override material, any Nanite-enabled meshes that have the Material or Material Instance assigned will use the referenced Nanite Override Material instead. This means that you can create materials specific to Nanite workflows rather than managing logic directly inside the material graph using the Nanite Pass Switch node.

[![Nanite Override Material Slot in a Material Instance.](https://dev.epicgames.com/community/api/documentation/image/9c08084c-2278-47ed-a42c-496a2d8afb9b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9c08084c-2278-47ed-a42c-496a2d8afb9b?resizing_type=fit)

In Material Instances, the Nanite Override Material slot is forcibly defaulted to **None** so that setting the override in a parent Material will not cause it to automatically be inherited in any of the child instances of that material.

In the example below, the Static Mesh Asset for the statue has Nanite enabled and it has a Material Instance applied. The Material Instance has its **Nanite Override Material** set with some simple color changes for demonstration purposes. The Static Mesh Actor on the left displays the Nanite Override Material since the mesh is being rendered with Nanite. The Static Mesh Actor on the right displays the same material until **Disallow Nanite** is set on the actor, disabling the Nanite Override Material to show the non-Nanite base material of the Material Instance.

### Static Mesh Component Option: Disallow Nanite

You can set when Nanite-enabled Static Meshes should use their Nanite representation using the **Disallow Nanite** setting on individual scene actors. This means you can have a mix of Nanite and non-Nanite actors which use the same Static Mesh Asset.

[![Static Mesh Component setting for Disallow Nanite.](https://dev.epicgames.com/community/api/documentation/image/80da2b18-407d-44b6-9a30-454e33021b35?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/80da2b18-407d-44b6-9a30-454e33021b35?resizing_type=fit)

The example below shows a single Nanite-enabled Static Mesh Asset where the left is the Nanite mesh representation and the right has Disallow Nanite enabled.

[![Example visualization with a Nanite-enabled and Disallowed Nanite Mesh](https://dev.epicgames.com/community/api/documentation/image/b7d83d89-bffa-463f-8c03-ad901d478823?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b7d83d89-bffa-463f-8c03-ad901d478823?resizing_type=fit)

### Landscape Terrain

You can enable Nanite on landscape actors. Nanite landscape meshes are rebuilt in the background to not disrupt user workflow while in the editor. Nanite landscape does not improve landscape resolution but does provide the user the leverage of Nanite runtime features such as GPU culling, automatic geometry streaming, and LODs. It generally boosts runtime performance, especially for demanding features such as VSM.

To learn how to enable and use Nanite with your landscape, see the [Using Nanite with Landscapes](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-nanite-with-landscapes-in-unreal-engine) documentation.

### Performance of Typical Content

For comparison purposes, the following GPU timings were taken from the Unreal Engine 5 technical demo [Lumen in the Land of Nanite](https://www.youtube.com/watch?v=qC5KtatMcUw) on a PlayStation 5:

-   Average render resolution of 1400p temporally upsampled to 4K.
    
-   ~2.5 milliseconds (ms) to cull and rasterize all Nanite meshes (which was nearly everything in this demo)
    
    -   Nearly all geometry used was a Nanite mesh
        
    -   Nearly no CPU cost since it is 100% GPU-driven
        
-   ~2ms to evaluate materials for all Nanite meshes
    
    -   Small CPU cost with 1 draw call per material present in the scene.
        

When considering these GPU times together, it's approximately 4.5ms combined for what would be equivalent to Unreal Engine 4's depth prepass plus the base pass. This makes Nanite well-suited for game projects targeting 60 FPS.

Numbers like these should be expected from content that doesn't suffer from the aforementioned performance pitfalls in previous sections. Very high instance counts and large numbers of unique materials can also cause increased costs and is an area of Nanite development that is being actively worked on.

## Data Size

Because of the micro detail that Nanite is able to achieve, it might be assumed that it means a large increase in geometry data resulting in larger game package sizes and downloads for players. However, the reality isn't that dire. In fact, Nanite's mesh format is significantly smaller than the standard Static Mesh format because of Nanite's specialized mesh encoding.

For example, using the Unreal Engine 5 sample Valley of the Ancients, Nanite meshes average 14.4 bytes per input triangle. This means an average one million triangle Nanite mesh will be ~13.8 megabytes (MB) on disk.

Comparing a traditional low poly mesh plus its Normal map to a high poly Nanite mesh, you would see something like:

|   |   |
| --- | --- |
| 
**Low Polygon Mesh**

-   Triangles: **19,066**
    
-   Vertices: **10,930**
    
-   Num LODs: **4**
    
-   Nanite: **Disabled**
    

Static Mesh Compressed Packaged Size: **1.34MB**

 | 

**Nanite Mesh**

-   Triangles: **1,545,338**
    
-   Vertices: **793,330**
    
-   Num LODs: n/a
    
-   Nanite: **Enabled**
    

Static Mesh compressed package size: **19.64MB**

 |

![Low Polygon Static Mesh | with a 4k Normal Map](https://dev.epicgames.com/community/api/documentation/image/0b6377fc-f9f8-4f80-911d-892de5eb28de?resizing_type=fit&width=1920&height=1080)

![High Poly Static Mesh | with a 4k Normal Map](https://dev.epicgames.com/community/api/documentation/image/62c007d3-6c3f-4b2c-b44d-a00beca751fd?resizing_type=fit&width=1920&height=1080)

Low Polygon Static Mesh | with a 4k Normal Map

High Poly Static Mesh | with a 4k Normal Map

The compressed package size isn't the entire size of the asset though. There are also unique textures only used by this mesh that have to be accounted for. Many of the materials used by meshes have their own unique textures made up of different Normal, BaseColor, Metallic, Specular, Roughness, and Mask textures.

This particular asset only uses two textures (BaseColor and Normal) and thus is not as costly on disk space as one with many other unique textures. For example, note the size of the Nanite mesh with ~1.5 million triangles is smaller in size (at 19.64MB) than a 4k normal map texture.

| Texture Type | Texture Size | Size on Disk |
| --- | --- | --- |
| 
**BaseColor**

 | 

4k x 4k

 | 

**8.2MB**

 |
| 

**Normal**

 | 

4k x 4k

 | 

**21.85MB**

 |

The total compressed package size for this mesh and its textures is:

-   Low Poly Mesh: **31.04MB**
    
-   High Poly Mesh: **49.69MB**
    

Because the Nanite mesh is very detailed already we can try replacing the unique normal map with a tiling detail normal that is shared with other assets. Although this results in some loss in quality in this case, it is fairly small and certainly much smaller than the difference in quality between the low and high poly versions. So a 1.5M triangle Nanite mesh can both look better and be smaller than a low poly mesh with a 4k normal map.

Total compressed package size for the Nanite-enabled mesh and textures: **27.83MB**

![High Poly Static Mesh | with 4k Normal Map](https://dev.epicgames.com/community/api/documentation/image/5a1603b5-ded8-417f-bb68-230d188ee0cf?resizing_type=fit&width=1920&height=1080)

![Nanite Mesh | with 4k Detail Normal Map](https://dev.epicgames.com/community/api/documentation/image/c74450aa-4d05-44d2-a9ef-941be4994f4e?resizing_type=fit&width=1920&height=1080)

High Poly Static Mesh | with 4k Normal Map

Nanite Mesh | with 4k Detail Normal Map

There are plenty of experiments that can be done with texture resolution and detail normal maps, but this particular comparison is to demonstrate that the data sizes of Nanite meshes are not too dissimilar from data that artists are already familiar with.

Lastly, we can compare the Nanite compression to the standard Static Mesh format using the high poly, where both are identical at LOD0.

|   |   |
| --- | --- |
| 
**High Poly Static Mesh**

-   Triangles: **1,545,338**
    
-   Vertices: **793,330**
    
-   Num LODs: **4**
    
-   Nanite: **Disabled**
    

Static Mesh Compressed Packaged Size: **148.95MB**

 | 

**Nanite Mesh**

-   Triangles: **1,545,338**
    
-   Vertices: **793,330**
    
-   Num LODs: n/a
    
-   Nanite: **Enabled**
    

Static Mesh compressed package size: **19.64MB**

 |

Comparing the Nanite compression from earlier with a size of **19.64MB** is **7.6x** smaller than the standard Static Mesh compression with 4 LODs.

Nanite compression and data sizes are key areas that will be improved in future releases of Unreal Engine.

### General Advice on Data Size

Nanite and [Virtual Texturing](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-texturing-in-unreal-engine) systems, coupled with fast SSDs, have lessened concern over runtime budgets of geometry and textures. The biggest bottleneck now is how to deliver this data to the user.

Data size on disk is an important factor when considering how content is delivered — on physical media or downloaded over the internet — and compression technology can only do so much. The average end user's internet bandwidth, optical media sizes, and hard drive sizes have not scaled at the same rate as hard drive bandwidth and access latency, GPU compute power, and software technology like Nanite. Pushing that data to users is proving challenging.

Rendering highly detailed meshes efficiently is less of a concern with Nanite, but storage of its data on disk is now the key area that must be kept in check.

## Visualization Modes

Nanite includes a number of visualization modes to inspect its data in the current scene.

In the Level viewport under the **View Modes** dropdown, hover over **Nanite Visualization** and choose from the selection.

[![Nanite Visualization Menu in the Viewport](https://dev.epicgames.com/community/api/documentation/image/bb779413-aeff-4821-ae87-8ed4fa7d8d57?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bb779413-aeff-4821-ae87-8ed4fa7d8d57?resizing_type=fit)

The **Overview** visualization displays the rendered scene in the center of the image with select Nanite visualizations around the screen for reference.

[![Nanite Overview Visualization](https://dev.epicgames.com/community/api/documentation/image/75ffc2da-5b0c-49d8-b0da-bf93b45f409f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/75ffc2da-5b0c-49d8-b0da-bf93b45f409f?resizing_type=fit)

The following Nanite visualization modes are available to choose from:

| Nanite Visualization | Description |
| --- | --- |
| 
**Mask**

 | 

Visualization that marks Nanite (green) and Non-Nanite (red) geometry.

 |
| 

**Triangles**

 | 

Display all triangles of the Nanite meshes in the current scene.

 |
| 

**Patches**

 | 

Display all patches of the Nanite meshes in the current scene.

 |
| 

**Clusters**

 | 

Display colored representations of all grouping of triangles being rendered in the current scene view.

 |
| 

**Primitives**

 | 

Visualization that colors components all the same color for all instances in an Instance Static Mesh (ISM).

 |
| 

**Instances**

 | 

Visualization that applies a different color for each instance in the scene.

 |
| 

**Overdraw**

 | 

Displays the amount of overdraw happening for scene geometry. All evaluated pixels, including masked-out pixels, are added to the overdraw view. Smaller objects that are closely stacked together create more overdraw than larger ones.

 |
| 

**Lightmap UV**

 | 

Visualization that displays the UV coordinates of Nanite mesh surfaces.

 |
| 

**Evaluate WPO**

 | 

Colors Nanite-enabled geometry that are using world position offset (green) versus ones that are not (red).

 |
| 

**Pixel Programmable**

 |  |
| 

**Tessellation**

 | 

Visualization for Nanite mesh using tessellation and amount of tessellation happening on only tessellated meshes.

 |
| 

**Raster Bins**

 | 

Displays groups that represent batches of geometry.

 |
| 

**Shading Bins**

 |  |

Nanite includes an **Advanced** visualizations mode that enables additional visualization options in the **Nanite Visualization** menu. These visualizations are useful for programmers who are debugging or profiling various low-level aspects of Nanite.

Enable this advanced visualization mode with the console variable `r.Nanite.Visualize.Advanced 1`.

## Console Variables and Commands

The following stats and console variables are available for use in debugging and configuring Nanite.

Nanite rendering can be enabled and disabled globally at runtime using the console variable `r.Nanite 0`. Disabling Nanite is a good way to emulate platforms where it is not supported.

### Nanite Fallback Rendering Modes

Nanite provides fallback mesh rendering modes when Nanite is either disabled or unsupported by a platform. You can control which mode is used with the console variable `r.Nanite.ProxyRenderMode`.

-   **0** is the default mode and falls back to rendering fallback meshes, or screen space-driven LODs if set. This includes the recognition of **Min LOD** in the Static Mesh Editor properties (described in the [Fallback Mesh](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) section above).
    
-   **1** disables all rendering of Nanite-enabled meshes.
    
-   **2** works similarly to mode 1 but allows the **Show > Nanite Fallback** visualization in the Static Mesh Editor to render a Nanite fallback.
    

The Fallback render modes 1 and 2 are useful for scenes that have far more instances than could possibly be supported without Nanite. They allow the scene to be opened in the editor on non-Nanite-supporting platforms.

For example, in the Unreal Engine 5 Valley of the Ancients sample project, disabling Nanite would cause there to be tens of thousands of regular draw calls to happen, making it difficult to open the map on a non-supporting platform.

### Nanite Stats Command

The command **NaniteStats** adds an overlay of Nanite culling statistics to the top-right of the viewport.

[![Nanite on-screen statistical display](https://dev.epicgames.com/community/api/documentation/image/f83db49c-b029-4982-b3ea-14a08c6957f6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f83db49c-b029-4982-b3ea-14a08c6957f6?resizing_type=fit)

Command arguments are used to specify what stats Nanite displays on the screen. When no argument is provided, the primary view is used.

Use `NaniteStats List` to show all available views in the debug output:

-   Primary
    
-   VirtualShadowMaps
    

You may also see other stats available for `ShadowAtlas` and `CubemapShadows` when available. Select a view by entering the command followed by the stat list name you want to view. For example, enter `NaniteStats VirtualShadowMaps`.

For views that use two-pass occlusion culling, the statistics are split into separate buckets for Main and Post pass.

### Resizing the Nanite Streaming Pool Size

Control the amount of memory dedicated to holding Nanite streaming data with the console variable `r.Nanite.Streaming.StreamingPoolSize`. Using larger pools reduces IO and decompression work when moving around the scene but at the cost of a larger memory footprint.

If the pool is not large enough to fit all the data needed for a view, cache thrashing can occur where streaming never settles even for a static view.

To visualize Nanite streaming data, you can use the Streaming Geometry show flag, **Show > Nanite > Streaming Geometry**. When disabled, Nanite meshes are only rendered at the quality level that is always resident in memory.

### Setting Maximum Clusters in a Single Pass

You can specify the maximum number of candidate and visible clusters used in a single pass with the console variable `r.Nanite.MaxCandidateClusters` and `r.Nanite.MaxVisibleClusters`. Their values are used for sizing intermediate buffers and their default values have been chosen to work for common rendering scenarios.

There is no mechanism for dynamically resizing either of these buffers, or automatically scaling down quality on overflow, which can result in rendering artifacts from them being too small for scene complexity, and typically manifesting as missing or blinking geometry. When these types of artifacts occur, use `NaniteStats` to determine conservative bounds for candidates and visible clusters. More specifically, look at the stats for **ClustersSW** and **ClustersHW**. The memory cost of a candidate cluster is currently 12 bytes and a visible cluster is 16 bytes.

This console variable cannot be changed at runtime and must be specified in a configuration (.ini) file.