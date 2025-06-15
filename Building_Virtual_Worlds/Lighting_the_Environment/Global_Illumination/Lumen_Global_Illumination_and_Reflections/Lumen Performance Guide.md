# Lumen Performance Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-performance-guide-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-performance-guide-for-unreal-engine)  
**Processed:** 2025-06-14 16:34:28

---

Lumen targets 30 and 60 frames per second (fps) on consoles with 8ms and 4ms frame budgets at 1080p for global illumination and reflections on opaque and translucent materials, and volumetric fog. The engine uses preconfigured Scalability settings to control Lumen's target FPS. The **Epic** scalability level targets 30 fps. The **High** scalability level targets 60 fps.

Lumen relies on [Temporal Upsampling](/documentation/en-us/unreal-engine/dynamic-resolution-in-unreal-engine) with Unreal Engine 5's [Temporal Super Resolution](/documentation/en-us/unreal-engine/temporal-super-resolution-in-unreal-engine) (TSR) for 4k output. Lumen and other features use a lower internal resolution (1080p), which gives TSR the best final image quality. Otherwise, rendering these features at 4K natively would need lower quality settings to achieve 30 or 60 fps.

## Scalability Settings

You can find the Scalability settings in the Level Editor under the Viewport **Settings > Engine Scalability Settings**. In-game, control the Scalability settings with GameUserSettings and the graphics settings menus (see the [Lyra](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine) project for an example). Lumen quality is set by the **Global Illumination** and **Reflections** quality groups:

-   **Cinematic** scalability level targets [Movie Render Queue](/documentation/404).
    
-   **Epic** scalability level targets a 30 fps console budget.
    
-   **High** scalability level targets a 60 fps console budget.
    
-   **Low** and **Medium** scalability levels disable Lumen features.
    

![Engine Scalability Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccea2e96-5d24-4fef-bb99-5d6c7c3fcb8b/engine-scalability-settings.png)

By default, Unreal Engine targets 30 fps on consoles. To target 60 fps, set the **Global Illumination** and **Reflections** quality groups to **High** in the console Device Profiles. These profiles can be found in `[Your Project Name]\Platforms[Console]\Config\` folder. For example, `[Your Project Name]\Platforms\PS5\Config\PS5DeviceProfiles.ini`.

A PlayStation 5 Device Profile targeting 60 fps would look like:

```
    `[PS5 DeviceProfile]     ; Set Lumen GI and reflection quality to High, targeting 60 fps     +CVars=sg.GlobalIlluminationQuality=2     +CVars=sg.ReflectionQuality=2`
Copy full snippet
```
\[PS5 DeviceProfile\] ; Set Lumen GI and reflection quality to High, targeting 60 fps +CVars=sg.GlobalIlluminationQuality=2 +CVars=sg.ReflectionQuality=2

## Scaling Down Beyond Lumen

The default **Global Illumination** and **Reflections** quality groups are in `\Engine\Config\BaseScalability.ini`. These settings attempt to keep indirect lighting looking similar between quality levels. This has the added benefit of not needing to redo your lighting per platform while scaling down costs of Lumen.

Medium Quality Level

-   For large-scale ambient occlusion, **Distance Field Ambient Occlusion** replaces **Lumen Global Illumination**.
-   For small-scale ambient occlusion, **Screen Space Ambient Occlusion** is enabled.

Low Quality Level

-   Uses only unshadowed skylight.
-   Reduces skylight intensity (`r.SkylightIntensityMultiplier=0.7`) to better match **Medium** quality level since there's no form of skylight shadowing.

### Software Ray Tracing

[Software Ray Tracing](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#softwareraytracing) is the fastest tracing method in Lumen and we recommend it for games which cannot afford Hardware Ray Tracing or as a fallback for GPUs which don't support Hardware Ray Tracing.

**Epic** scalability level enables **Detail Traces**. These traces provide higher quality but incur a large performance overhead. Traces happen for individual Mesh Distance Fields. This makes performance sensitive to the number of instances and number of overlapping instances. Detail Traces will have a high cost when using excessive amounts of kit-bashing with many layers of intersecting meshes. Disable **Affects Distance Field Lighting** to remove individual distance field instances from rendering in the distance field scene. Removing less important instances that don't have a major impact on global illumination or reflections can help save Detail Traces performance.

For Detail Traces, [Hardware Ray Tracing](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#hardwareraytracing) provides improved quality at similar performance costs compared to Software Ray Tracing.

**High** scalability level disables Detail Traces, and Lumen traces a single merged Global Distance Field instead of individual Mesh Distance Fields. Tracing the global distance field makes tracing independent from the number of instances and their overlap with other instances. It's also a great fit for content with a large amount of overlapping instances.

### Hardware Ray Tracing

Hardware Ray Tracing provides Lumen with improved quality and we recommend it as a default option on consoles for both 30 fps and 60 fps. It is more expensive than Software Ray Tracing and requires careful scene optimization as it is quite sensitive to large amounts of instance overlaps.

Hardware Ray Tracing requires rebuilding the **Top Level Acceleration Structure** (TLAS) every frame. This cost is proportional to the number of instances you need to include in this acceleration structure. Achieving good performance on next-generation consoles generally means having fewer than 100,000 instances in the **Ray Tracing Scene** after culling. On Microsoft Windows, the number of instances can vary.

Use `Stat SceneRendering` to check how many instances are visible in the ray tracing scene. Look at the **Ray tracing active instances** stat.

![Stat SceneRendering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82dcb6ff-c19b-4413-a767-40d162003ffd/stat-scenerendering.png)

The ray tracing scene culling settings are the most powerful tool for controlling how many ray tracing instances are in the scene. Ray tracing culling is enabled by default to simplify its setup, but additional changes can be made to the **DefaultEngine.ini** configuration file found in the `[Your Project Name]\Config\` folder.

```
    `[SystemSettings]     r.RayTracing.Culling=3     r.RayTracing.Culling.Radius=15000     r.RayTracing.Culling.Angle=0.5`
Copy full snippet
```
\[SystemSettings\] r.RayTracing.Culling=3 r.RayTracing.Culling.Radius=15000 r.RayTracing.Culling.Angle=0.5

You can remove Individual instances from the ray tracing scene by disabling **Visible In Ray Tracing** on the actor in the level.

See the [Ray Tracing Performance Guide](/documentation/en-us/unreal-engine/ray-tracing-performance-guide-in-unreal-engine) for detailed information on Hardware Ray Tracing performance, including performance counters and debug views.

**Far Field** provides aggressive culling without compromising global illumination and reflection distance. After the ray tracing scene radius, all rays use the far field traces to extend global illumination and reflections at a cheaper cost. [Lumen Technical Details](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine) provides information on how to set up Far Field.

Increasing ray tracing scene culling coupled with Far Field helps you to optimize and scale down Lumen Hardware Ray Tracing performance.

Hardware Ray Tracing performance depends on how much the meshes in the scene overlap. Large meshes that overlap the entire scene are a performance issue, such as a skybox. These meshes should have **Visible In Ray Tracing** disabled. You can also save tracing costs on grass meshes, and kit-bashed meshes with multiple layers of intersecting combined meshes.

To keep scenes performant with Hardware Ray Tracing, you must keep overlapping meshes to a reasonable level.

**Hit Lighting for Reflections** provides improved reflection quality. It evaluates materials and lighting at every hit point, but is expensive for games. We don't recommend using it for games unless materials are trivial and optimized with **Ray Tracing Quality Switch** nodes. On consoles, you can limit the number of BVH traversal iterations and terminate long and expensive rays early using `r.Lumen.HardwareRayTracing.MaxIterations`. Terminated rays are treated as fully occluded with zero radiance causing over-occlusion. This setting is useful to finetune performance and avoid performance issues caused by parts of the scene with lots of overlapping geometry.

## Tips

The cost of **Lumen Reflections** can vary depending on how much of the screen has smooth, or low-roughness, materials. These materials need dedicated reflection rays. By default, all pixels with roughness below 0.4 will trace a reflection ray. Pixels with roughness above that get free reflection approximation based on Lumen Global illumination.

### Lumen Reflection Roughness Threshold

You can control the roughness threshold using **Max Roughness To Trace** setting in the **Post Process Volume**. It can be additionally clamped from scalability settings using `r.Lumen.Reflections.MaxRoughnessToTraceClamp`. Pixels with roughness below the set threshold will trace dedicated **Lumen Reflection** rays, and pixels with roughness above this threshold fall back to free rough specular approximation.

Foliage has an independent roughness threshold. Any pixel with materials **Two Sided Foliage** or **Subsurface** shading models are treated as foliage. You can control foliage roughness with `r.Lumen.Reflections.MaxRoughnessToTraceForFoliage`. Pixels requiring dedicated reflection rays can be visualized using **Performance Overview** view mode, which is found in the Level Viewport under the View Modes menu.

![Lumen Performance View Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac0862d3-8661-4e50-a0b1-fc65555edcc7/lumen-performance-view-mode.png)

Reflections on foliage are often hard to see. Without compromising quality, it's possible to achieve some significant performance wins by setting the foliage max roughness threshold to 0.

### Replacing Lumen Reflections with Screen Space Reflections

Reflection costs can be more aggressively scaled down by replacing Lumen Reflections with **Screen Space Reflections** (SSR). You can do this by setting `r.Lumen.Reflections.Allow=0`. For example, you can save 1 ms on Xbox Series S by adding the following to the `XSXDeviceProfiles.ini` file.

```
    `[XSX_Lockhart DeviceProfile]     ; Use SSR in lieu of Lumen reflections for perf     +CVars=r.Lumen.Reflections.Allow=0`
Copy full snippet
```
\[XSX\_Lockhart DeviceProfile\] ; Use SSR in lieu of Lumen reflections for perf +CVars=r.Lumen.Reflections.Allow=0

The example below demonstrates how Lumen Global Illumination provides rough specular even when Lumen Reflections is disabled.

![Example of Lumen GI Specular with Lumen Reflections disabled.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a31db2c-a492-4c4f-9908-d9b1eef75192/lumen-gi-lumen-reflections-disabled.png)

Some performance increase from Lumen Reflections is gained by reusing rays traced for diffuse global illumination. This only provides a speed increase for scenes with many pixels whose roughness is in the range of 0.2–0.4. You can enable this using `r.Lumen.Reflections.RadianceCache=1`.

### Surface Cache Tile Updates

**Lumen Scene Lighting** updates the surface cache's direct and indirect lighting. Performance depends on the fraction of surface cache updated every frame. You can tweak per frame update speed separately for direct and indirect lighting, using `r.LumenScene.DirectLighting.MaxLightsPerTile` and `r.LumenScene.Radiosity.UpdateFactor`.

Lumen Scene Lighting selects a small subset of the most important lights per surface cache tile, which makes its performance less sensitive to the total number of lights in the scene. Number of lights per tile can be controlled by `r.LumenScene.DirectLighting.MaxLightsPerTile`.

### Profiling Lumen

Lumen is divided into three passes:

-   **Lumen Scene Lighting** for evaluating surface cache lighting.
-   **Lumen Screen Probe Gather** for evaluating diffuse global illumination and rough reflections, and translucency global illumination.
-   **Lumen Reflections** for evaluating dedicated reflection rays on smooth surfaces.

`Stat GPU` displays GPU pass timings, including individual Lumen passes.

![Stat GPU](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8e4349d-d616-4de9-acde-cd9716162192/stat-gpu.png)

For a more detailed performance breakdown, use the `ProfileGPU` command. You can also use third-party profiling tools like RenderDoc.

Lumen is using Async Compute on consoles. These timings will be zero until you disable it with the console command `r.Lumen.AsyncCompute 0`. See the next section for more details about Async Compute.

## Async Compute

Lumen uses **Async Compute** on consoles. This allows the GPU to overlap Lumen's work with the non-Nanite geometry pass and direct lighting pass. Additionally, Lumen can overlap with the **Lumen Screen Probe Gather** and **Lumen Reflections** passes.

![Async compute graphics passes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a431718-3441-41b3-abdc-e4396a981e8c/async-compute.png)

Async Compute is pre-configured for common workloads, but in some cases non-default settings can be faster. One of these cases which we encountered is when the **Lumen Screen Probe Gather** pass can't overlap with the **Lumen Reflections** pass due to large amounts of direct lighting or shadow map work on the graphics queue. In this case, it may be beneficial to run the Lumen entirely as an async compute pass. You can do this by setting the following:

```
    `r.LumenScene.Lighting.AsyncCompute=1     r.Lumen.DiffuseIndirect.AsyncCompute=1     r.Lumen.Reflections.AsyncCompute=1`
Copy full snippet
```
r.LumenScene.Lighting.AsyncCompute=1 r.Lumen.DiffuseIndirect.AsyncCompute=1 r.Lumen.Reflections.AsyncCompute=1

Async Compute makes Lumen overlap with other rendering passes. This makes profiling harder since timings can't be properly tracked by `Stat GPU` or `ProfileGPU`. When profiling and comparing full render frame times or using external GPU profiling tools, disable Async Compute.

## Scalability Reference

The default engine scalability and per-platform device profiles contain individual Lumen settings. These are useful as a reference for important and up-to-date renderer performance scalability settings. Also, they are a good starting point for custom scalability settings. We recommend using the default scalability levels to achieve 30 fps or 60 fps, but also for a consistent look between levels. You can take a look at these scalability settings in either of these files:

```
    `[Engine Root]\Engine\Config\BaseScalability.ini     [Engine Root]\Platforms[Console Name]\Base[ConsoleName]DeviceProfile.ini`
Copy full snippet
```
\[Engine Root\]\\Engine\\Config\\BaseScalability.ini \[Engine Root\]\\Platforms\[Console Name\]\\Base\[ConsoleName\]DeviceProfile.ini

The reference table below contains descriptions of individual settings and their set state used by the scalability levels.

### General

| Setting Name | High | Epic | Cinematic | Description |
| --- | --- | --- | --- | --- |
| `r.Lumen.TraceMeshSDFs.Allow` | 0 | 1 | 1 | Enables **Detail Traces** for **Software Ray Tracing**. Detail traces incur a large performance penalty by tracing individual mesh distance fields, but improve quality, especially surface cache direct lighting quality. |

### Lumen Scene Lighting

Lumen Scene Lighting performance depends on the fraction of surface cache updated every frame. It also depends on the resolution of the Translucency Global Illumination volume.

| Setting Name | High | Epic | Cinematic | Description |
| --- | --- | --- | --- | --- |
| `r.LumenScene.DirectLighting.UpdateFactor` | 32 | 32 | 32 | A fraction of the surface cache area for which direct lighting should be updated every frame. Higher values improve performance, but make lighting changes less responsive. |
| `r.LumenScene.Radiosity.UpdateFactor` | 64 | 64 | 64 | A fraction of surface cache area for which indirect lighting should be updated every frame. Higher values improve performance, but makes lighting changes less responsive. |
| `r.LumenScene.Radiosity.ProbeSpacing` | 8 | 4 | 4 | The spacing between surface cache indirect lighting probes. Lower values improve spatial resolution of indirect lighting in surface cache at a cost of lower performance. |
| `r.LumenScene.Radiosity.HemisphereProbeResolution` | 3 | 4 | 4 | The resolution of the surface cache indirect lighting probe. |
| `r.Lumen.TranslucencyVolume.GridPixelSize` | 64 | 32 | 32 | Controls the resolution of the translucency global illumination volume. |

### Screen Probe Gather

Global illumination performance depends on the internal render resolution and screen probe trace resolution.

| Setting Name | High | Epic | Cinematic | Description |
| --- | --- | --- | --- | --- |
| `r.Lumen.ScreenProbeGather.RadianceCache.ProbeResolution` | 16 | 32 | 32 | Controls the number of traces per radiance cache probe. Higher values improve quality at the cost of performance. |
| `r.Lumen.ScreenProbeGather.RadianceCache.NumProbesToTraceBudget` | 300 | 300 | 1000 | The number of radiance cache probes to be updated per frame. Higher values improve quality at the cost of performance. |
| `r.Lumen.ScreenProbeGather.DownsampleFactor` | 32 | 16 | 8 | Allows global illumination to be downsampled independently from the internal render resolution. |
| `r.Lumen.ScreenProbeGather.TracingOctahedronResolution` | 8 | 8 | 16 | Determines how many traces are done per probe. Higher values make tracing slower but improves global illumination quality. |
| `r.Lumen.ScreenProbeGather.TwoSidedFoliageBackfaceDiffuse` | 0 | 1 | 1 | Whether to gather lighting along the backface for the **Two Sided Foliage** and **Subsurface** shading models. |
| `r.Lumen.ScreenProbeGather.ScreenTraces.HZBTraversal.FullResDepth` | 0 | 1 | 1 | Whether the screen space traces should sample the full resolution depth. Enabling it makes screen space traces more accurate but costs some performance. |
| `r.Lumen.ScreenProbeGather.ShortRangeAO` | 1 | 1 | 1 | Controls small-scale ambient occlusion added on top of global illumination. You can disable it for extra performance at a visual loss of detail in contact shadows. |

### Reflections

**Lumen Reflections** performance depends on the number of dedicated reflection rays. Rays are traced from pixels with roughness values below the set threshold. Another important factor for performance is the internal render resolution and reflection resolution.

| Setting Name | High | Epic | Cinematic | Description |
| --- | --- | --- | --- | --- |
| `r.Lumen.Reflections.DownsampleFactor` | 2 | 1 | 1 | Whether to downsample reflections independently from the internal render resolution. |
| `r.Lumen.Reflections.MaxRoughnessToTraceClamp` | 1.0 | 1.0 | 1.0 | Project and Post Process Volume max roughness settings are clamped to this value. This allows control of the number of dedicated reflection rays from the scalability the settings. |
| `r.Lumen.Reflections.MaxRoughnessToTraceForFoliage` | 0.2 | 0.4 | 0.4 | The max roughness value for which dedicated reflection rays on foliage should be traced. |
| `r.Lumen.TranslucencyReflections.FrontLayer.Allow` | 0 | 1 | 1 | Whether to allow high quality reflections on translucency to be enabled from a Post Process Volume. |
| `r.Lumen.TranslucencyReflections.FrontLayer.Enable` | 0 | 0 | 1 | Whether to enable high quality reflections on translucency by default. |