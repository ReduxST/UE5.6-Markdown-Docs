# MegaLights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/megalights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/megalights-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:38

---

MegaLights is a whole new direct lighting path in Unreal Engine 5 enabling artists to place orders of magnitudes more dynamic and shadowed area lights than they could ever before.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/769890ef-4420-44b9-bf52-44278e676afa/ml-example-1.png)

MegaLights is designed to support current generation consoles and leverages ray tracing to enable realistic soft shadows from various types of area lights.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4dd10a1a-6d59-4a03-bc7a-04a1b052bd8c/ml-example-2.png)

MegaLights not only reduces the cost of dynamic shadowing, it also reduces the cost of unshadowed light evaluation, making it possible to use expensive light sources, such as textured area lights, on consoles.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06955022-5c7d-4480-8f7e-b923d24d5297/ml-example-3.png)

MegaLights also supports [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43187fa5-edbf-4c01-aa3e-fb551c64d9ac/ml-example-4.png)

## Using MegaLights

You can enable MegaLights for your project from the Project Settings in the **Rendering > Direct Lighting** category. This prompts you to also enable **Support Hardware Ray Tracing**, which is a recommended setting for MegaLights.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6728874-553c-413c-9034-5fea95c6b360/ml-project-settings.png)

Once enabled, all local lights are handled by the MegaLights system. MegaLights can be disabled per light using **Allow MegaLights** light component property. You can also set the **MegaLights Shadow Method** to select the source of shadowing to either be **Ray Tracing (Default)** or **Virtual Shadow Maps** (VSMs).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6cd6511a-2ac0-4039-8a94-0f4141dfd764/ml-light-settings.png)

While Virtual Shadow Maps will cast shadows directly from the non-simplified Nanite geometry, it only approximates area shadows. There is CPU, memory and GPU time overhead for VSMs on a per-light basis for preparing shadow map depths in advance.

For a more fine-grained control inside a single project, MegaLights can be enabled or disabled using Post Process Volume settings.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ebd7322-5657-43b2-b449-e6cddef04a7f/ml-postprocess-settings.png)

MegaLights can be disabled per scalability level or device profile with `r.MegaLights.Allow 0`.

## Technique Overview

MegaLights is a stochastic direct lighting technique, which solves direct lighting though importance sampling of lights. It traces a fixed number of rays per pixel towards important light sources. If a light source is hit by a ray then that light’s contribution is added to the current pixel.

This approach has a few important implications:

-   Direct lighting is handled by a single pass in an unified manner, replacing multiple existing Deferred Renderer shadowing and shading techniques.
-   MegaLights not only reduce the cost of shadowing, but also reduce the cost of the shading itself.
-   MegaLights has a constant performance overhead, but quality may decrease as lighting complexity increases at a given pixel.

Where Deferred Shading has a constant lighting quality, the GPU cost increases with the number of lights. Whereas, MegaLights have constant performance, but the quality depends on the lighting complexity at a given pixel.

MegaLights replaces the following features:

-   Shadow MapsDistance Field Shadows
-   Ray Traced Shadows
-   Deferred Shading (BRDF and light evaluation)
-   Volumetric Fog shadowing and light evaluation
-   Virtual Shadow Map projection
    -   Virtual Shadow Maps can still be used with MegaLights if selected as the shadow method on the individual light actor’s settings.

By default, MegaLights first traces a short conservative screen space ray in order to pick up tiny details, which may not be available in the simplified Ray Tracing Scene. If such ray goes offscreen, behind an object, or just reaches its max length, then MegaLights continues tracing from the last valid position using Hardware or Software Ray Tracing. MegaLights can also be configured to ray trace a virtual shadow map, but its shadows have additional upfront cost since shadow maps need to be generated per light, while the BVH (Ray Tracing Scene) is generated once for all lights in the scene.

The ray guiding in MegaLights is useful for selecting important light sources and is crucial for sending more samples to lights that are likely to have influence on a given pixel. In turn, ray guiding sends fewer samples towards lights that are to have less influence, like those that are likely occluded. This is an important part of the technique, allowing it to extract the best possible lighting quality out of the fixed per pixel light sample budget. While ray guiding reduces the number of rays sent towards occluded light sources, it still needs to periodically sample those to check whether they became visible in the current frame. With this in mind, you should avoid placing light sources with huge bounds affecting the entire scene.

Finally, all accumulated lighting goes through a denoiser that tries to reconstruct high quality direct lighting from the stochastic and possibly noisy input. As the lighting complexity increases in the scene, the denoiser needs to do more work to account for this. Increased lighting complexity can lead to blurring of the lighting or cause ghosting, which you can avoid by merging smaller light sources into large area lights and carefully narrowing down the bounds of light sources to improve the final lighting quality.

## Lighting Complexity

There’s a limitation of how many important lights can affect a single pixel before it has to rely heavily on the denoiser because there’s a fixed budget and fixed number of samples per pixel, which can cause the denoiser to produce blurry lighting and eventually noise or ghosting in the scene. It continues to be important to optimize light placement by narrowing light attenuation range, and replacing clusters of light sources with a single area light.

To keep MegaLights working well within a scene, it’s best to avoid placing lights inside scene geometry and to optimize a light’s bounds. You can use the console command `r.MegaLights.Debug 1` to visualize where rays are being sent from a selected pixel. You can freeze a selected ray using this console command `r.ShaderPrint.Lock 1`, which allows you to fly around the scene to inspect traced rays.

Additional visualization tools will be made available as MegaLights is developed into a production-ready feature of Unreal Engine.

In the example below, part of the textured rect light is inside the wall and even though it won’t be ever visible, it still needs to be sampled by MegaLights. This can be seen in the visualization, which shows some of the rays being traced into the wall. Ideally textured rect light’s **Source Width** and **Source Height** should be narrowed down, so that light source fills this arch, but doesn’t extend past it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29d9568f-4344-4e51-a9cd-1b80f13bd683/ml-light-source-width-height.png)

To minimize noise avoid placing lights inside geometry, optimize light attenuation range, spotlight cone angles, and rect light barn doors to narrow down the influence of light.

## Ray Tracing Scene

By default, MegaLights uses ray tracing, and shadow quality depends on the quality of Ray Tracing Scene representation. For performance, the Ray Tracing Scene is built using automatically simplified Nanite meshes and has more aggressive culling settings than the main view. This may cause shadow artifacts, leaking, or missing shadows.

Ray Tracing Scene visualizations are a great starting point for investigating shadowing issues. They show the actual scene representation that MegaLights ray-traces against. You can visualize the Ray Tracing Scene using:

-   One of the **Ray Tracing Debug** view modes, which is found in the Level Viewport under the View Modes menu. Ray Tracing Debug view modes are also available through console commands: `show RayTracingDebug 1` and `r.RayTracing.DebugVisualizationMode = "World Normal"`.
-   **Lumen Overview** view mode, which enables a picture-in-picture visualization where both the Ray Tracing Scene and main view can be seen at the same time. Lumen Overview view mode is also available through the console command `r.Lumen.Visualize 1`.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/504367fe-05b9-47d8-9367-35bbd51a3391/ml-sceneview.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c5c3302-abbd-46f5-aa5c-ce6eb3ec3805/ml-rts-worldnormal-vis.png) |
| Scene View | Ray Tracing World Normal Visualization View Mode |

If some shadows are missing or disappearing with distance, it may be due to Ray Tracing Scene culling. You can start adjusting culling by using the console commands under `r.RayTracing.Culling.*`. You’ll want to look at the culling mode, radius, and solid angle variables.

For culling purposes, you can merge smaller objects together using **Ray Tracing Group Id**, so that they are culled together using their merged bounds.

For more detailed information about Ray Tracing Scene culling controls, see the [Ray Tracing Performance Guide](/documentation/en-us/unreal-engine/ray-tracing-performance-guide-in-unreal-engine).

Ray Tracing Scene is based on automatically simplified Nanite Fallback Meshes. Default settings can sometimes result in fallback meshes that are too low quality for the purposes of shadowing and may require manual adjustment. Follow these steps to do this:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a836b57-d59f-4e54-967b-763166755981/ml-sme-nanite-settings.png)

1.  Open the mesh in the Static Mesh Editor.
2.  In the Details panel under **Nanite Setting**, set the **Fallback Target** to **Relative Error**.
3.  A new setting is revealed named **Fallback Relative Error**, and you can set its value. Reducing the value increases the number of triangles and fidelity of the Nanite Fallback mesh.
4.  Once you’re done, click **Apply Changes** to rebuild the Nanite Fallback Mesh.

For more information about setting up Nanite Fallback Meshes, see [Nanite Virtualized Geometry](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine).

Nanite Fallback Mesh triangle count and number of instances included in the Ray Tracing Scene will affect ray tracing BVH build times, used memory, and ray tracing performance. We recommend carefully increasing them according to the available performance and memory budget of your project.

For non real-time rendering, it’s also possible to use `r.RayTracing.Nanite.Mode 1`, which builds the Ray Tracing Scene out of full detail Nanite Meshes. This has a large performance and memory cost and can result in hitches during scene or camera animation when the Nanite LOD cut changes and its BVH needs to be rebuilt.

## Screen Space Traces

MegaLights uses the Ray Tracing Scene when casting shadows for larger geometry detail but leverages screen space traces for smaller scale geometry that may be missing from the simplified Ray Tracing Scene. Screen space traces use Scene Depth and they will hit anything that's visible on the screen. This may cause issues with certain art direction tweaks, like invisible shadow casters which don’t affect Scene Depth and only exist in the Ray Tracing Scene.

You can reduce screen space ray length using the console command `r.MegaLights.ScreenTraces.MaxDistance`. Alternatively, if the Ray Tracing Scene is already precise enough, you can disable screen traces completely, which helps minimize various screen space and view dependent artifacts.

## Shadowing Methods

MegaLights exposes two shadowing methods, which can be selected per light using light component’s properties:

-   **Ray Tracing** is the default and recommended method. It doesn't add any extra cost per light and can achieve correct area shadows. The downside is that the quality of the shadows depends on the simplified Ray Tracing Scene.
-   **Virtual Shadow Maps** traces rays against a [Virtual Shadow Map](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine). Virtual Shadow Maps are generated per light using rasterization and can capture full Nanite mesh details. The downside is that it can only approximate area shadows, and it has a significant additional per light cost in terms of memory, CPU, and GPU overhead used to generate shadow depths. This should be used sparingly.

By default, all lights, especially larger area light sources with softer shadows or less important lights, should use Ray Tracing, as softer lights don’t need precise shadow casters. It’s also worth allocating a bit more budget for the Ray Tracing Scene, as higher quality ray tracing representation allows for more lights going through the cheaper ray tracing path.

## Light Functions

Light Functions are supported as long as they are compatible with the [Light Function Atlas](/documentation/en-us/unreal-engine/using-light-functions-in-unreal-engine#lightfunctionatlas) and if the Light Function atlas is enabled in the project settings.

## Alpha Masking

By default, only Screen Space Traces can correctly handle alpha masked surfaces. It’s possible to enable Alpha Masking support for Ray Tracing using the console command `r.MegaLights.HardwareRayTracing.EvaluateMaterialMode 1`. Enabling this option has a non-trivial performance overhead, so it’s best to avoid alpha masking in content.

## Scaling Quality Up

Scaling lighting quality to that of high-end PCs or offline rendering is still under development. As of this time, you can only control the number of samples per pixel using the following console commands:

-   `r.MegaLights.NumSamplesPerPixel 16`: This provides higher lighting quality for opaque surfaces.
-   `r.MegaLights.Volume.NumSamplesPerVoxel 4`: This provides higher lighting quality for volumes like Volumetric Fog.

MegaLights doesn’t yet have dedicated support for [Movie Render Queue](/documentation/404), but good results can be achieved with either using Temporal Super Resolution (TSR) as anti-aliasing method or setting the Temporal Sample Count to around 8, which is able to resolve lighting correctly.

## Performance

When comparing performance it’s important to understand that MegaLights is solving all direct lighting and replaces a variety of Deferred Renderer passes, such as:

-   **Shadow Depths:** if using Shadow Maps or Virtual Shadow Maps
-   **RenderDeferredLighting::Lights**
-   **VolumetricFog::Shadowed Lights**
-   Removes light evaluation from **VolumetricFog::LightScattering**

Factors which impact performance:

-   Performance is mostly dependent on the internal rendering resolution.
-   Ray Tracing is the second biggest part of MegaLights cost. The cost depends on several factors: the number of instances in the Ray Tracing Scene, their complexity, amount of overlapping instances and amount of dynamic triangles which need to be updated each frame. For in-depth information about optimizing the Ray Tracing Scene, see the [Ray Tracing Performance Guide](/documentation/en-us/unreal-engine/ray-tracing-performance-guide-in-unreal-engine).
-   There’s an additional memory, CPU and GPU overhead for generating shadow map depths per each light, which uses Virtual Shadow Map for shadowing instead of Ray Tracing.
-   There’s a small cost for pixels on screen with complex BRDFs and affected by heavy light types (textured Rect Lights).

MegaLights cost is mostly constant, and there isn’t a large difference between unshadowed and shadowed lights, so all lights in the scene can have shadows enabled.

Ideally, MegaLights should be used with [Lumen HWRT](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#hardwareraytracing), which allows sharing Ray Tracing Scene overhead and optimizations between both systems.

`Stat GPU` shows GPU timing overview, including the MegaLights pass. In-depth timings can be obtained using built-in `ProfileGPU` or third party profilers.

Unreal Engine uses Async Compute to overlap multiple dispatches from various features. `Stat GPU` and `ProfileGPU` timings will be distorted until you disable Async Compute using the `r.RDG.AsyncCompute 0` console command.

Although MegaLights is fully GPU driven, there’s still some legacy CPU cost per light. If all lights are MegaLights using ray tracing, most of the per light CPU cost can be removed using the console command `r.Visibility.LocalLightPrimitiveInteraction 0`.

## Limitations

General limitations:

-   MegaLights is incompatible with the Forward Renderer

Current limitations, which we want to improve:

-   There’s a legacy per light CPU overhead tracking primitive interactions, which aren’t needed for MegaLights
-   Directional Light isn’t supported.
    -   Currently, MegaLights fallback to either Virtual Shadow Map or Ray Traced Shadows depending on the project settings
-   Subsurface scattering thickness estimation isn’t supported
-   Strand based hair isn’t supported
-   Translucency isn’t supported.
    -   MegaLights falls back to unshadowed and slower Deferred Renderer lit translucency
-   Water, Clouds, Heterogenous Volumes and Local Volumetrics aren’t supported
-   Lumen handles lots of lights with reasonable performance, but it will be greatly improved when MegaLights is fully integrated with Lumen.
-   Software Ray Tracing path is under development and has limited shadow quality.

## Platform Support

-   MegaLights are designed for current gen consoles (such as PlayStation 5, Xbox Series X | S) and PCs with ray tracing capabilities.
-   MegaLights do not support mobile, Switch, or previous-generation consoles (such as PlayStation 4 and Xbox One)