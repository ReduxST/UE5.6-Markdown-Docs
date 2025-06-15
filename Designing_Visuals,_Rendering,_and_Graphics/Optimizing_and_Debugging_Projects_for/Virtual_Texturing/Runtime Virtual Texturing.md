# Runtime Virtual Texturing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/runtime-virtual-texturing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/runtime-virtual-texturing-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:38

---

A **Runtime Virtual Texture** (RVT) creates its texel data on demand using the GPU at runtime, and works similarly to traditional texture mapping. The RVT caches shading data over large areas, making them a good fit for Landscape shading that uses decal-like materials and splines that are well suited to conform to the terrain.

## Workflow

Use the following high-level steps to set up and use runtime virtual texturing in your project:

1.  Create a **Runtime Virtual Texture** Asset(s) in the Content Browser. It is used to link all the components (including RVT Volume Actors, and RVT Materials) together to render the runtime virtual texture.
2.  Add a **Runtime Virtual Texture Volume** to the scene from the **Modes** panel. This is used to place the RVT Asset in the scene.
3.  Configure your Materials to **write to** the RVT Asset.
4.  Configure Materials to **sample from** the RVT Asset.
5.  Set up one or more Primitive Components or Landscape Actors to render to the RVT Asset.

For a step-by-step guide to setting up RVT, see the [Runtime Virtual Texturing Quick Start](/documentation/en-us/unreal-engine/runtimevirtual-texturing-quick-start-in-unreal-engine). In this guide, you'll set up a Landscape material and additional scene components to work with runtime virtual texturing.

## Runtime Virtual Texturing Components

Use the following components to setup and work with runtime virtual textures in your Unreal Engine projects.

### Runtime Virtual Texture Asset

The **Runtime Virtual Texture** Asset contains the configuration details that will be used when creating the RVT in the scene. Think of this as the linchpin in the RVT system that connects your Materials and components in the scene that are rendered to the RVT.

The RVT Asset is referenced by the following components:

1.  Each **Runtime Virtual Texture Volume** placed in the scene is assigned a single RVT Asset.
2.  Individual scene components are assigned any number of RVT Assets. When they are within the bounds of a volume that uses one of their assigned RVT Assets, they are rendered to the runtime virtual texture.
3.  Before a component is rendered to the RVT through the RVT Volume, its Materials must use the **Virtual Texture** Material Domain or use properly setup RVT Material Expressions.

Create a new RVT Asset from the Content Browser using the right-click context menu or the **Add New** button. Under the **Materials & Textures** category, select a **Runtime Virtual Texture**.

Click image for full size.

Double-click the Asset to open and configure its settings in its own Editor window:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4b7a9f3-834a-4bc2-b2ec-ccc71d6886b7/rvt_asset_window.png)

Use this window to define the size, tile size, and type of Material Attributes supported by the runtime virtual texture.

For details and usage of these settings, see [Virtual Texture Settings](/documentation/en-us/unreal-engine/virtual-texturing-settings-and-properties-in-unreal-engine#runtimevirtualtextureasset) page.

#### Asset Actions

From the right-click context menu, you have a couple of actions that can help you manage your RVT Assets in Materials:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f55ca40-b13c-4486-8860-57656ae552b5/rvtcontextmenuactions.png)

-   **Find Materials Using This** will find and highlight in the Content Browser all the Materials that reference this RVT Asset.
-   **Fix Material Usage** provides an automated way to fix all Materials after changing an RVT Asset Material Type. It finds all Materials and Material Functions that contain a Runtime Virtual Texture Sample node which references this RVT Asset. If the **Virtual Texture Material Type** in the node does not match the Material Type in the RVT Asset, then the Material Type in the node is fixed to match the RVT Asset.

### Runtime Virtual Texture Material Types

When setting up your RVT Material, there are several options to choose from:

| Material Type | Description | Compressed Format |
| --- | --- | --- |
| **Base Color** | Stores only the base color. | BC1 |
| **Base Color, Normal, Roughness, Specular** | Stores the base color, normal, roughness, and specular. When compression is enabled, two BC3 textures are used to hold the data. One texture contains base color and the normal X. The other contains roughness, specular, normal Z direction, and normal Y. | BC3 + BC3 |
| **YCoCg Base Color, Normal, Specular** | Stores base color, normal, roughness, and specular. When compression is enabled, three textures are used; a BC3 texture holds the base color encoded in YCoCg format, a BC5 texture holds the normal X and Y, and a BC1 texture holds roughness, specular, and normal Z direction. | BC3 + BC5 + BC1 |
| **YCoCg Base Color, Normal, Specular, Mask** | This is the same as YCoCg Base Color, Normal, Specular but with an additional 8 bit "mask" channel intended for general use. When compression is enabled the mask is packed into the alpha channel of a BC3 format. | BC3 + BC5 + BC3 |
| **World Height** | Stores a height value. The value is stored normalized in the range of the minimum and maximum z coordinate from the RVT volume. | R16\_UNORM |
| **Displacement** | Stores a displacement value between 0 and 1. When compression is enabled the value is stored in a BC4 texture. | BC4 |
| **Mask4** | Stores a 4 channel mask with each channel holding a value between 0 and 1. When compression is enabled the value is stored in a BC3 texture. | BC3 |

The **Base Color, Normal** material type available in Unreal Engine 4.23 has been removed. Assets using it are automatically converted to use the **Base Color, Normal, Roughness, Specular** material type in 4.24.

#### Runtime Virtual Texture Base Color Storage

The **YCoCg Base Color, Normal, Roughness, Specular** material type enables a different encoding of the Base Color in the RVT.

By default, the Base Color is stored as RGB and compressed to BC1. This type of encoding can lead to color shifts and banding in the stored data. This is most apparent with Base Color data that has smooth gradients. The YCoCg material type helps reduce these types of artifacts. However, using it comes at the cost of 25% extra memory and some additional performance sampling and decoding of the virtual texture data.

![Default Base Color Encoding](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3d8f55a-7ec1-4be9-b394-da84c0430a22/basecolorstorage_0.png)

![YCoCg Base Color Encoding](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b1770fe-4b31-4f3f-8bc5-5769671acfa1/basecolorstorage_1.png)

#### Runtime Virtual Texture Normal Storage

Normals are stored with X and Y values in a BC5 texture, or in the alpha channels of two BC3 textures, giving them the same precision as BC5. The Z direction of the normal is also used to store world space normals.

When the material writes from a Runtime Virtual Texture Output node, there are no hidden transforms applied to the output. Whatever is input into the node is written to the RVT (with some encoding to store in the texture).

The recommended way to store normals in an RVT is in world space. The use of this common space should allow for better blending behavior when multiple primitives are writing and reading from the RVT.

### Runtime Virtual Texture Volume

The **Runtime Virtual Texture Volume** is used to place the RVT Asset in the scene. This volume should encompass the Actor that it will render to when the Material is set up. Generally, this should be a Landscape or surface terrain-like primitive.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3fc5a10-9781-43fb-821a-d6182253696e/modes_rvtvolume.png)

Any primitives sampling from, or writing to, the runtime virtual texture should be inside the bounds of the volume. When placing the RVT Volume, use the **Transform from Bounds** parameters in the Level **Details** panel to quickly position and scale the volume to a selected Actor. Typically, this would be something like a Landscape in your scene.

1.  From the **Place Actors** panel, drag in a **Runtime Virtual Texture Volume** to the scene.
2.  With the volume selected, use the level **Details** panel to locate the **Transform from Bounds** category and use the **Source Actor** asset selection (or the eyedropper) to select an Actor in the scene.
3.  Use the **Set Bounds** button to quickly position, scale, and rotate the volume.
4.  Later when other components have been set to write to this RVT, **Set Bounds** will also scale the volume so that the volume bounds include all the relevant component bounds.

Objects that render to the RVT are rendered using an Orthographic projection in the Negative-Z direction of the RVT Volume.

### Runtime Virtual Texture Material Expressions

Scene components that have an assigned Runtime Virtual Texture Asset must use the following Material Expressions to enable the components to be composited into the generated runtime virtual texture in the scene.

#### Writing to and Sampling from the Runtime Virtual Texture

To write to and sample from an RVT in your scene, you must first setup some RVT expressions to handle this for your material:

-   The **Runtime Virtual Texture Output** expression is used to define a single material that both writes to and samples the virtual texture. Existing material logic should be plugged into this node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe3a030e-58dd-412b-9eb7-8c43a068c25f/mat_rvtoutput.png)
-   The **Runtime Virtual Texture Sample** expression takes in the assigned RVT Asset to sample and outputs that for this material.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a0fc934-1ab8-4f67-8e84-dc54dcf7ca38/mat_rvtsample.png)
-   The **Runtime Virtual Texture Sample Parameter** expression works like the Runtime Virtual Texture Sample node but exposes the RVT Asset being sampled as a parameter for Material Instances to override.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b3fd9a5-cfec-428d-9efa-383f8ca5b4b3/rvtsampleparam.png)
    
    Like other parameters, you can create this node directly or by right-clicking a Runtime Virtual Texture Sample node and selecting **Convert to Parameter** from the context menu.
    
    When using a Material Instance to override the RVT Asset, the RVT Asset assigned must match the Material Type set in the Runtime Virtual Texture Sample Param expression's Details panel.
    

This is an example Landscape material that writes to and samples the bound RVT Asset. It also uses logic to fall back to traditional landscape rendering when a platform doesn't support Virtual Texturing:

Click image for full size.

#### Additional Material Expressions

Materials are compiled in one of two contexts for use with RVT:

-   To render to the RVT
-   To render to other passes

The **Runtime Virtual Texture Replace** expression is ideal when wanting part of your material logic to render to the RVT.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/362c19e3-7a37-4070-98e9-296afce9103c/mat_rvtreplace.png)

The **View Property** expression also has a couple of RVT-specific options:

-   The **Virtual Texture Output Level** node outputs the RVT mip level currently being rendered.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b953360-26f8-41d1-b1da-73cecf432b6f/mat_viewpropertyvtoutputlevel.png)
-   The **Virtual Texture Output Derivative** node outputs the X and Y size of world space covered by a single texel of the current virtual texture output.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e649139a-967e-4af0-ba89-27ab0b1442b6/mat_viewpropertyvtoutputderivative.png)
-   The **Virtual Texture Max Level** node outputs the number of mip levels in the RVT currently being rendered.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de7107d3-3924-4aaf-b406-27c8e5dd3020/mat_virtualtexturemaxlevel.png)

An example use case of these expressions would be to mimic the use of some distance-based shading in the RVT. Because RVT shading is camera-independent, this type of shading cannot be expressed directly. However, something similar is achievable by making the shading mip level-dependent. The **Runtime Virtual Texture Replace** node can be used to implement a mip level-dependent shading path only for the **Runtime Virtual Texture Output** node.

-   The **Virtual Texture Feature Switch** is useful when setting up material logic to fallback to an alternative path when virtual texturing is not supported.

## Scene Component Output Properties

Any component placed in the scene can render to an RVT. The following component types are good candidates:

| Ideal Component Candidates | Non-Ideal Component Candidates |
| --- | --- |
| 
-   Landscape and Landscape Splines
-   Static Meshes and Instanced Static Meshes
-   Foliage Instances (for decal scattering)\*



 | 

-   Skeletal Meshes
-   Movable Static Meshes
-   Animated Meshes



 |

Because RVT content is effectively a shading cache, it isn't fully updated on every frame, meaning that the objects rendered to it are expected to have their mobility be **Static**. Skinned and animated primitives are not good candidates for rendering to an RVT.

Use the **Render to Virtual Textures** array in the component **Details** panel to specify which RVT Assets it can render to in the scene. A component can be assigned to multiple RVTs. Rendering to an RVT only happens when the RVT Asset has been assigned to a placed RVT Volume in the scene and once the component's Materials have been set up correctly.

See the [Runtime Virtual Texture Quick Start](/documentation/en-us/unreal-engine/runtimevirtual-texturing-quick-start-in-unreal-engine) for an example. Also see the [Virtual Texture Setting Reference](/documentation/en-us/unreal-engine/virtual-texturing-settings-and-properties-in-unreal-engine)

Use the sections that follow to further component behavior when rendering to an RVT in the scene.

### Virtual Texture Pass Type

The **Draw in Main Pass** options enable you to control the main pass rendering for objects that are set to render to an RVT:

These options enable you to control object rendering to an RVT:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3aab996-c26a-4e1a-9cdd-48f8a7f85f03/rvt_actor_rvtasset_passtype.png)

| Selection | Description |
| --- | --- |
| **Never** | Never render this component in the Main Pass. If there is no RVT in the scene, it will not render at all. This option should be used for items that aren't necessary (such as decal-type materials) when there is no virtual texture support. For example, using a Static Mesh plane with a material outputting to an RVT will write the material like a decal to the RVT landscape material. If a platform or feature level doesn't support virtual texturing, the Static Mesh plane would not render to the Main Pass. |
| **From Virtual Texture** | 
Renders the component to either the RVT or the Main Pass, depending on virtual texture support and settings. The component will not render to the main pass if all of the following are true:

-   The support for virtual texturing is enabled.
-   One of the RVT assets referenced by the component is placed in the scene with an RVT volume.
-   One of the relevant RVT volumes are set to "Hide Primitives."

For example, a Landscape spline rendering a road mesh and material should write to the RVT to apply its material along the spline. However, if there is no valid RVT in the scene or there is no feature level support for virtual texturing, the spline road mesh will still be visible on the Landscape.



 |
| **Always** | Renders the component to the RVT and in the Main Pass regardless of virtual texture support. This is ideal for objects (such as a Landscape) that need to both write to and sample from the RVT. For example, a Landscape material that is set up to both write data to the RVT and render the final RVT should always be visible. |

It's recommended to disable collision for primitives that are only being rendered to an RVT. This is not automatically disabled.

### Setting LOD and Mips

Use the Virtual Texture Advanced rollout properties to control how components render to the RVT by setting level of detail (LOD) and culling behavior. Access these parameters from the component's level **Details** panel:

For Primitives in the scene, adjust the following properties:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc539879-e740-4c51-b761-2872de938f7d/rvt_actor_lodsettings.png)

| Property | Description |
| --- | --- |
| **Virtual Texture LOD Bias** | This sets the LOD to render into the RVT. It is selected automatically based on how much of the virtual texture page the rendered primitive covers. A further bias can be applied using this option. Higher values will force a lower detailed LOD to be used. |
| **Virtual Texture Skip Mips** | This is the number of lowest mips in the RVT to skip rendering this primitive. This option removes the cost of rendering into the RVT if it is known that a primitive doesn't need to be rendered beyond some set draw distance. |
| **Virtual Texture Min Coverage** | If this value is set, the **Virtual Texture Skip Mips** parameter is ignored and instead cull (or remove) the primitive from an RVT mip based on its estimated projected size in the mip. This value is in units of pixels but in log space. For example, setting a value of 3 will cull (or remove) a primitive if its projected size is less than 8 pixels. |

For Landscapes in your scene, adjust the following properties:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d379366-d0f1-4043-8357-1e8e770cfff7/rvt_actor_landscape_lodsettings.png)

| Property | Description |
| --- | --- |
| **Virtual Texture Num LODs** | The number of LODs used to render Landscape components into the RVT. A setting of 0 means that each Landscape component is rendered into the RVT as a single quad. A setting of 0 is optimal for the GPU. Higher values are required if the Landscape Material requires high frequency vertex interpolated data. |
| **Virtual Texture LOD Bias** | A bias applied to the selected LOD for rendering to the RVT. |

### Object Sort Priority

Rendering multiple primitives to the RVT in the scene presents a potential problem for object layer sorting. Since Z-buffering isn't used and the component's material can have alpha blending, it means that the sort order may need to be defined.

Use the level **Details** panel for any selected component in the scene to set its **Translucency Sort Priority**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6b9b237-88d8-440d-8127-941560d6a0cb/rvt_actor_translucenysortpriority.png)

All components have a default value of **0**. Smaller values always render first (or on the bottom layer) and larger ones render last (or on top).

![Translucency Sort Priority | Spline: 1 | Decal: 0 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6d243ae-9f4f-45e8-a75f-c28e05dff5d4/rvt_actor_translucencysortpriority_0.png)

![Translucency Sort Priority | Spline: 1 | Decal: 2 ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6e4731d-4428-43fa-a4ac-c5978d3ba82f/rvt_actor_translucencysortpriority_1.png)

The render order of components with the same value is *undefined*. If a component r is missing from the RVT in your scene, check the **Translucency Sort Priority** first.

## Streaming Virtual Texture Build

When an RVT covers a large world with many components, rendering to the low resolution mips of the RVT can be a slow operation. Also, in this scenario, world Actors need to be permanently resident to be available to render to low mips that represent distant parts of the world. Just keep in mind that this can be expensive for memory.

In this situation, it's more efficient to bake and stream the low resolution mips of an RVT. The higher resolution mips can still be rendered at runtime. In this way, a single virtual texture can make the best use of both [Streaming Virtual Texturing](/documentation/en-us/unreal-engine/streaming-virtual-texturing-in-unreal-engine) and Runtime Virtual Texturing approaches.

### Enabling SVT with RVT

1.  To add streaming virtual texture support to an RVT, set the number of low mips that you would like to stream.
    
2.  In the RVT Volume set the number of Streaming Levels that you would like to stream.
    
    Click image for full size.
    
    A higher number low mip value generates a larger streaming virtual texture that will be used at a closer distance to the camera.
    
3.  Next you will need to create the streaming virtual texture asset. In the RVT Volume component click the **Build** below the **Streaming Levels** property. On first use this will create a new **Virtual Texture Builder** asset which holds the streaming virtual texture.
    
    Click image for full size.
    
4.  After editing you'll need to update the streaming virtual texture. This can be achieved in two ways:
    
    -   Using the **Build** menu in the Editor Toolbar and selecting the **Build Virtual Textures**. This option builds all virtual textures in the currently opened Level.
        
        Click image for full size.
        
    -   Using the RVT Volume component and clicking the **Build** next to the **Use Streaming Low Mips in Editor** property. This option builds only the streaming virtual texture assigned to the selected RVT Volume. This option builds only the streaming virtual texture assigned to the selected RVT Volume.
        

By default, the Editor always renders with runtime generated RVT data and doesn't render with the streaming virtual texture data. This avoids the need to update the streaming virtual texture after each relevant edit.

To render with the streaming virtual texture in the RVT low mips, select the **Use Streaming Low Mips in Editor** property in the RVT Volume **Details** panel.

When some RVT asset settings change then any associated SVT asset will no longer match and will be disabled. This could lead to performance problems in game. The RVT volume UI shows when this is the case with a warning icon next to the Build button. The condition is also flagged during Map Check.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4b86ebd-64ae-4c03-a102-cd7e2e9b705a/rvt_actor_streaminglevelsnote.png)

## Optimizations, Statistics, and Debugging

Use the following sections to explore ways to optimize and debug runtime virtual texturing in your projects.

### Stats

Open the console using the backtick (\`) key and enter the following commands to enable their stats information:

Use `stat virtualtexturing` to give you feedback about the virtual texturing scene for cost in milliseconds (ms) and counters for page tables.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34ed5435-28a5-4ee4-a648-c15dd7216e4d/stat_virtualtexturing.png)

Use `stat virtualtexturememory` to display relevant memory counters related to the use of virtual texturing in the current scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00f80a4e-3cad-407c-b45a-5b406d85298d/stat_virtualtexturememory.png)

### Streaming Virtual Texture Low Mips Debugging

To help visualize the distance at which the streaming virtual texture is being used, use the **Build Debug** checkbox in the RVT Volume **Details** panel. This can be found next to the **Use Streaming Low Mips in Editor** property.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6580e5c8-0136-4125-bef5-3808775d16e5/build_builddebugvtvolume.png)

When this option is set the streaming virtual texture rebuilds data with a tint so that it's easy to see where the streaming virtual texture mips are being used.

### Memory Pools

The Memory Pool Sizes for virtual texturing are set up in the `BaseEngine.ini` configuration file. The pools are set up per-texture format group and tile size. Configuration of the pool size is driven by specifying the maximum memory budget for your project. You'll find these settings under the `[/Script/Engine.VirtualTexturePoolConfig]`.

A ScalabilityGroup option has been added to specify which r.VT.PoolSizeScale scalability setting applies to a memory pool.

### Debugging

Use the following console variables for debugging virtual texturing in your project:

| Console Variable | Description |
| --- | --- |
| `r.VT.Flush` | Use this command to flush all the physical caches in the Virtual Texturing system. It can be useful when you suspect an issue that could be caused by a bad cache invalidation. |
| `r.VT.MaxUploadsPerFrame` | Use this command to set the maximum number of page uploads per-frame (default is 64 in Editor and 8 in game). It can be useful when you want to throttle the number of Runtime Virtual Texture Tiles being updated in a frame to prevent performance spikes. |

### Console Variables and Scalability

The following console variables can be tuned per-project and per-platform or scalability level.

| Console Variable | Description |
| --- | --- |
| `r.VT.MaxUploadsPerFrame` | The maximum number of virtual texture page uploads per frame. Reducing this can improve performance at the expense of slower visual updates. |
| `r.VT.MaxUploadsPerFrameInEditor` | The maximum number of page uploads per frame when in Editor mode. This is independent of the command `r.VT.MaxUploadsPerFrame` because in the Editor it's better to trade some runtime performance for a cleaner visualization while working. |
| `r.VT.MaxContinuousUpdatesPerFrame` | The maximum number of continuous page uploads per frame. Each of these uploads refreshes a single random page that is already mapped. This only occurs for RVT assets set for continuous upload and when we haven't used the MaxUploadsPerFrame budget with other page updates. |
| `r.VT.MaxContinuousUpdatesPerFrameInEditor` | The maximum number of continuous page uploads per frame when in Editor mode. |
| `r.VT.RVT.TileCountBias` | This is a bias to apply to the RVT Asset **Size in Tiles** property. A value of -1 will halve the RVT resolution. A value of 1 will double the RVT resolution. |
| `r.VT.RVT.TileCountBias.Group<x>` | This applies the tile count bias only to RVT volumes that have been set to Scalability Group . Note that the variation of the CVar without a Group specified maps to Scalability Group 0.. |
| `r.VT.PoolSizeScale` | The scale factor to apply to the virtual texture physical pool sizes. A value of less than 1 will reduce the texture pool sizes. This may be necessary on platforms that are more memory constrained. |
| `r.VT.PoolSizeScale.Group<x>` | This applies the scale factor only to virtual texture physical memory pools that have been set to Scalability Group . Note that the variation of the CVar without a Group specified maps to Scalability Group 0. |
| `r.VT.MaxAnisotropy` | This is the specific MaxAnisotropy setting for Virtual Texture sampling. |

## Additional Notes and Limitations

-   Sampling a virtual texture from the Vertex Shader stage is possible. However, use this with extreme caution since no virtual texture GPU feedback will be generated by the vertex shader.
-   There is no support for using virtual textures in materials that fill runtime virtual textures. This is because there would need to be ensurance that any source virtual textures were fully streamed to the correct level before filling any runtime virtual texture page. This would add complexity and performance cost to the runtime virtual texture rendering.
    -   You should also be careful when using regular streaming textures to fill runtime virtual textures, since these can cause issues when they write to a runtime virtual texture page before being fully streamed in. However, regular streaming can rely on the camera location metrics, which are more predictable, where the virtual texture streaming depends fully on the GPU feedback.