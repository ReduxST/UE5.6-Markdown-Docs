# Heterogeneous Volumes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:23

---

The Heterogeneous Volume actor is used to render volume-domain materials that sample [Sparse Volume Textures](/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine). This actor supports rendering volumes in real-time and with the [Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine). Heterogeneous Volume actors can render static or animated sparse volume texture materials.

![Heterogeneous Volume actor with static and animated SVTs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15341453-eb9f-42cf-a347-88cd2f99d956/hv-static-animated-svt.gif)

Left, static single-volume SVT; Right, an animated SVT.

## Working with Heterogeneous Volume Actors

Use the following workflow to get using Heterogeneous Volumes in your project:

-   [Import a VDB to create a Sparse Volume Texture asset in Unreal Engine.](/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine#importingvdbfiles)
-   [Set up a Volume-domain material that samples an SVT asset.](/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine#settingupasvtmaterial)
-   [Add a Heterogeneous Volume Actor to the scene and assign an SVT material to it.](/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine#settingupaheterogeneousvolume)

### Importing VDB Files

To get started, you must have a [VDB (or Voxel Data Base)](https://en.wikipedia.org/wiki/OpenVDB#What_does_VDB_stand_for) file to import into the **Content Browser**.

To import a VDB file, follow these steps:

-   Drag and drop the VDB directly into the Content Browser.
-   Use the **Import** button in the Content Browser.

VDBs have their own import window for importing **static** and **animated** VDB files.

![VDB Import Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f750875-8acc-48c8-8241-30a672bf8ed8/hv-vdb-import-options.png)

You have the option of importing a static or animated VDB file. Static VDBs only include the single file and its stored volume data whereas Animated VDBs are a set of individual files sequentially numbered. Animated VDBs only need to import any one of the sequentially numbered VDB files to import the animated VDB in its entirety.

VDBs can include different attributes stored with their data. These can be split between Attributes A and Attribute B. The general recommendation is to split the incoming data across two sampling attributes where the first attribute data is imported as 8-bit unorm and the second attribute data is 16-bit float.

For projects at Epic Games, we prefer to push density as an 8-bit unorm and pass all other data through the 16-bit float attribute list during import.

Imported transforms are applied automatically with a heterogeneous volume. If the transforms were authored with the pivot being at the origin, which is usually one of the corners of the volume, you can check the box for Pivot at Centroid to move the pivot to the center of the volume. However, be aware that forcing the pivot to the volume’s center may end up breaking transforms.

For more information specific to importing and using sparse volume textures, see [Sparse Volume Textures](/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine).

### Setting up a SVT Material

For detailed information about setting up a material with an SVT and using it within a material, see [Sparse Volume Textures](/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine).

Heterogeneous Volumes require a volume-based material that samples an sparse volume texture. These materials use the **Sparse Volume Texture Sample** node to sample an SVT, which you can use in conjunction with Heterogeneous Volumes, Volumetric Fog, and Volumetric Clouds, or any volume-based material.

Unreal Engine includes an empty sample SVT material already set up that you can apply your SVT asset to. You can find it in the Content Browser under **Engine > Engine Materials** named **SparseVolumeMaterial**. Make a copy of this material and create an instance of it.

Once you open the material instance, override the **SparseVolumeTexture** parameter and apply your own imported SVT asset to the assignment slot.

![Material Instance Editor SVT assignment slot.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/768f27c8-4646-4dec-a93c-edda6f18d5f0/hv-matinst-svt-slot.png)

### Setting Up a Heterogeneous Volume

To set up a heterogeneous volume, follow these steps:

1.  Using the **Place Actors** panel, search for and add a **Heterogeneous Volume** actor to the scene.
2.  With the actor selected, use the **Details** panel to assign an SVT material to the actor.
3.  \[Optional\] If you imported an animated VDB, you'll want to check the boxes for **Playing** and **Looping** under the **Animation** section.

## Heterogeneous Volume Actor Properties

Heterogeneous Volume actors have the following properties:

![Heterogeneous Volume Actor Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb7b5543-8d26-4226-97f2-dbcd0edf8701/hv-actor-properties.png)

| Properties | Description |
| --- | --- |
| Materials |   |
| **Element \[N\]** | Material assignment slot for a Volume-based material that samples from a sparse volume texture. |
| Volume |   |
| **Volume Resolution** | The resolution of the volume is automatically determined and cannot be modified when rendering with an SVT. |
| **Pivot at Centroid** | Moves the pivot to the center of the volume. Note that transforms were authored with the pivot being at the origin, which is usually one of the corners of the volume, depending on how it was authored. Forcing the pivot to the volume center may break transforms. |
| Animation |   |
| **Frame** | Displays the current frame of the SVT being rendered. When the **Playing** checkbox is not set, you can specify a particular frame of an animated SVT. |
| **Frame Rate** | The speed at which the frames should be played. |
| **Start Frame** | Which frame the animated SVT should start with. This is bound by the available range of the imported SVT. |
| **End Frame** | Which frame the animated SVT should end with. This is bound by the available range of the imported SVT. |
| **Playing** | When enabled, this plays through the animated SVT once. |
| **Looping** | When enabled, this repeats the animated SVT from the beginning again from the start frame to the end frame. |
| **Frame Transform** |   |
| Sparse Volume Texture Streaming |   |
| **Issue Blocking Requests** | The streaming system is notified to block when updating per-frame sparse volume texture data. This is not recommended for real-time playback but can be useful for cinematic rendering when the streaming system would otherwise page in higher MIP levels to maintain real-time frame rate. |
| **Streaming Mip Bias** | Set the texture level of the SVT being rendered. Lower values equate to higher density and quality of the volume. Higher values have less density and quality. |
| Lighting |   |
| **Step Factor** | This factor adjusts the step-size of the ray marching integrator to occur at a multiple of the volume resolution. By increasing this factor, the marcher takes longer steps and sacrifices quality for performance. |
| **Shadow Step Factor** | This factor adjusts the step-size of shadow calculations of the ray marcher. By increasing this factor, the marcher takes longer steps and sacrifices quality for performance. |
| **Shadow Bias Factor** | This factor adjusts the initial voxel bias applied when calculating shadows. Increasing this factor reduces self-shadowing but may introduce light leaking. |
| **Lighting Downsample Factor** | This factor adjusts the volume resolution of an internal lighting cache. Increasing the factor effectively lowers the operating resolution, decreasing system memory and increasing performance. This has the effect of lowering quality. While the SVT is natively sparse, the internal lighting cache is currently dense. The internal lighting cache will currently not allocate a volume resolution of greater than 1024 x 1024 x512 voxels. |

### Animation

The **Animation** properties provide custom rules for playback. By default, the **Start Frame** and **End Frame** properties are bound to the available range of the imported SVT but can be trimmed to play only part of the SVT's animation. Playback is expected to occur at a "cinematic" rate of 24 frames-per-second but can be adjusted as needed.

The SVT interactively plays in the scene when the **Playing** checkbox is set, and continuously repeats when the **Looping** checkbox is set. When the Playing checkbox is left unchecked, you can left-mouse click the **Frame** text field and drag left or right to scrub through playback of the SVT's available frames.

### Lighting

The deferred rendering model uses ray marching when rendering high-quality volumetric assets with the Heterogeneous Volume actor. Each adjustable Factor property is relative to the **Volume Resolution** property. The resolution of the imported SVT has a direct correlation to runtime performance.

### Blueprints

In Blueprints, you can use the **Play** and **Set Playing** nodes to trigger animation data start and stop.

## Using Heterogeneous Volumes with Path Tracer

You can create heterogeneous volumes with the Niagara Fluids plugin or instancing a Heterogeneous Volume actor in your scenes. These volumes begin rendering when the path tracer is enabled.

![Niagara Fluid rendered with the path tracer.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd21b570-4dfe-4b51-b9e5-f7f82b1f3f1a/hv-niagara-fluid-path-tracer.png)

Example of a Niagara Fluid heterogeneous volume rendered with the path tracer.

To render heterogeneous volumes with the path tracer, enable the following:

-   **Project Settings**
    -   Set the Default RHI to **DirectX 12**.
    -   Enable **Support Hardware Ray Tracing**.
    -   Enable **Path Tracing**
-   **Plugins**
    -   \[Optional\] Niagara Fluids

For a complete list of specifications, see [Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine).

### Heterogeneous Volumes with Niagara Fluids

The Niagara Fluids plugin must be enabled to use this feature. For more information, see [Niagara Fluids](/documentation/en-us/unreal-engine/niagara-fluids-in-unreal-engine).

To render with [Niagara Fluids](/documentation/en-us/unreal-engine/niagara-fluids-in-unreal-engine), follow these steps:

1.  Create a new Niagara Fluid in the Content Browser.
2.  In the Niagara picker window, select **New system from a template or behavior example** and click **Next**.
3.  Choose one of the examples from the **3D Gas** list in the window.
4.  Double-click the Niagara Fluid asset to open the Niagara Editor.
5.  Select the Niagara Fluid system node in the graph.
6.  In the **Details** panel, set the following:
    -   **Loop Behavior** to **Infinite**.
    -   **Loop Duration** should be shorter than 5 seconds.
7.  Compile and save the Niagara Fluid asset.
8.  Place the Niagara Fluid in your scene.
9.  Open the console window and input `r.PathTracing.HeterogeneousVolumes 1` to enable path tracer support for heterogeneous volume rendering.

### Heterogeneous Volumes with Sparse Volume Textures

To render with [Sparse Volume Textures](/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine), follow these steps:

1.  Import a VDB file and set up a sparse volume texture material to display it.
2.  In the Level editor, use the **Place Actors** panel to add a **Heterogeneous Volumes** actor to the scene.
3.  Assign the sparse volume texture material to its material slot.
4.  Open the console window and input `r.PathTracing.HeterogeneousVolumes 1` to enable path tracer support for heterogeneous volume rendering.

### Useful Console Variables

| Console Variable | Description | Default Value |
| --- | --- | --- |
| `r.PathTracing.HeterogeneousVolumes` | Enables path tracing of heterogeneous volumes. | 0 |
| `r.HeterogeneousVolumes.IndirectLighting` | Enables indirect lighting for heterogeneous volumes. This is disabled by default. | 0 |
| `r.HeterogeneousVolumes.OrthoGrid` | Enables the world-space voxel grid. | 1 |
| `r.HeterogeneousVolumes.OrthoGrid.MaxBottomLevelMemoryInMegabytes` | Determines the memory limit (in megabytes) for each bottom-level voxel grid used for voxelization (emission, extinction, and albedo). The recommended cinematic default is 512. | 128 |
| `r.HeterogeneousVolumes.OrthoGridShadingRate` | Determines the active shading rate of the world-space voxel grid, where the value roughly corresponds to pixel width. Lower shading rates creates a higher quality tessellation, but requires more memory. The recommended cinematic default is 1. | 4 |
| `r.HeterogeneousVolumes.FrustumGrid` | Enables the frustum-aligned voxel grid. | 1 |
| `r.HeterogeneousVolumes.FrustumGrid.MaxBottomLevelMemoryInMegabytes` | Determines the memory limit (in megabytes) for each bottom-level voxel grid used for voxelization (emission, extinction, and albedo). The recommended cinematic default is 512. | 128 |
| `r.HeterogeneousVolumes.FrustumGrid.ShadingRate` | Determines the active shading rate of the frustum-aligned voxel grid, where the value roughly corresponds to pixel width. Lower shading rates create a higher quality tessellation, but requires more memory. The recommended cinematic default is 1. | 4 |
| `r.HeterogeneousVolumes.FrustumGrid.DepthSliceCount` | Determines the number of depth slices of the frustum-aligned voxel grid when rendered with a shading rate of 1. Rendering with a shading rate of 2 corresponds to emitting a Depth Slice Count of 256. The recommended cinematic default is 512 or 1024. | 512 |
| `r.HeterogeneousVolumes.Tessellation.FarPlaneAutoTransition` | Truncates the far-plane of the frustum-aligned grid when the voxel size of the frustum-aligned voxel grid corresponds to the voxel size of the world-space voxel grid. | 1 |
| Scalability Variables |   |   |
| `r.HeterogeneousVolumes.DownsampleFactor` | This downsamples the rendered viewport. | 1.0 |
| `r.HeterogeneousVolumes.MaxStepCount` | The maximum ray-marching step count used to render heterogeneous volumes. | 512 |
| `r.HeterogeneousVolumes.Shadows.Resolution` | Sets the resolution when building the volumetric shadow map. | 512 |

## Heterogeneous Volumes Project Settings

Heterogeneous Volume actors have the following project settings. These are found under the **Engine > Rendering** section in the **Heterogeneous Volumes** category.

| Property | Description |
| --- | --- |
| **Heterogeneous Volumes** | Enable rendering with heterogeneous volumes subsystem. |
| **Shadow Casting** | Enable heterogeneous volumes to cast shadows onto the environment. |
| **Composite with Translucency** | Enable compositing with heterogeneous volumes when rendering translucency. |

## Additional Notes

**Real-time:**

-   **Rendering in Real-Time vs Path Tracer**
    -   More complete support for rendering volumes is now available in the Path Tracer, which can accurately simulate global illumination.
-   **Cast Shadows on the environment**
    -   This feature is experimental.
    -   You can enable heterogeneous volume shadow casting in the project settings.

**Path Tracer:**

This feature is experimental.

-   **Blocky or blurry heterogeneous volumes**
    -   The default shading rate for heterogeneous volume rendering is 4, to support interactive path tracing. Lowering the shading rate to 1 removes perceptible artifacts, but requires increased memory to correctly render. The recommended cinematic default shading rate is 1, and the recommended default memory limit is 512. We recommend setting these in the [Movie Render Queue](/documentation/404) settings when rendering.
-   **Missing voxels in renders**
    -   Lowering the shading rate of the world-space and frustum-aligned voxel grids may attempt to allocate more bottom-level voxels than allowed by the imposed memory limit. In these instances, voxels will not be allocated and portions of the volume will be missing. At this time, you must use more bottom-level memory or raise the shading rate.
-   **Overlapping heterogeneous volumes appear blocky**
    -   Bottom-level voxel data in the world-space voxel grid is aggregated if the region is determined to be homogeneous. Homogeneous detection is performed within the confines of a single volume and may be improperly aggregated in the presence of overlapping volumes within the same region. You can prevent aggregation by setting `r.HeterogeneousVolumes.Tessellation.BottomLevelGrid.HomogeneousAggregation` to `0` to disable it.
-   **Screen door effect with Niagara Fluid**
    -   Niagara systems only trigger path tracing invalidation events when the Niagara Editor is open. Having the editor open allows the animation to be viewed correctly in the path tracer. When the editor is closed, the path tracer continues to accumulate samples throughout the animation.
-   **Screen door effect with Heterogeneous Volume actor**
    -   The Heterogeneous Volume actor does not currently trigger path tracing invalidation events. Uncheck the **Animate** property on the actor to suspend the animation.

### Indirect Lighting with Heterogeneous Volumes

You can enable support for indirect lighting with heterogeneous volumes with the console variable `r.HeterogeneousVolumes.IndirectLighting 1`. This feature is best used with high-end PCs and **Cinematic** scalability settings.

|   |   |
| --- | --- |
| ![No Indirect Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b7c5d7f-2860-4aa3-8265-20808f95ebe4/hv-indirectlighting-0.png) | ![With Indirect Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b45112f-6439-4f91-9367-5dc74960a7cb/hv-indirectlighting-1.png) |
| No Indirect Lighting | With Indirect Lighting |

## Additional Resources

-   Niagara Fluids Plugin
    -   The Niagara Fluids plugin includes examples that can be used with heterogeneous volume rendering. Enable the plugin in your project and create a new Niagara system from the provided templates. For more information, see [Niagara Fluids](/documentation/en-us/unreal-engine/niagara-fluids-in-unreal-engine)
-   The VDB files used in the examples in this page are from JangaFX's free VDB set created with EmberGen.
    -   Download their free examples [here](https://jangafx.com/software/embergen/download/free-vdb-animations/).