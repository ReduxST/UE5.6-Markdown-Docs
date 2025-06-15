# Lumen Global Illumination and Reflections

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:26

---

Lumen is Unreal Engine 5's fully dynamic global illumination and reflections system that is designed for next-generation consoles, and it is the default global illumination and reflections system. Lumen renders diffuse interreflection with infinite bounces and indirect specular reflections in large, detailed environments at scales ranging from millimeters to kilometers.

[![Example scene with Lumen global illumination and reflections.](https://dev.epicgames.com/community/api/documentation/image/c343fedc-597b-46a2-b2e5-7d2766c1f322?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c343fedc-597b-46a2-b2e5-7d2766c1f322?resizing_type=fit)

## Getting Started with Lumen

Newly-created projects have Lumen Global Illumination and Reflections enabled by default, as well as their dependencies like [Generate Mesh Distance Fields](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine). Existing projects converted from Unreal Engine 4 to Unreal Engine 5 will **not** automatically enable Lumen features. This prevents breaking or changing any lighting paths within those projects.

Lumen is enabled from the Project Settings under the **Rendering > Dynamic Global Illumination** and **Reflections** categories.

[![](https://dev.epicgames.com/community/api/documentation/image/8950505d-649f-488f-b454-9a9d1b951298?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8950505d-649f-488f-b454-9a9d1b951298?resizing_type=fit)

Global Illumination and Reflections can be set independently. In each category, set the following to enable Lumen:

-   Dynamic Global Illumination: **Lumen**
    
-   Reflection Method: **Lumen**
    
    When enabled, the property **Generate Mesh Distance Fields** will be enabled, if it is not already. It is required for Lumen's [Software Ray Tracing](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#software-ray-tracing) mode. Requires the engine to be restarted.
    

Lumen Global Illumination replaces [Screen Space Global Illumination (SSGI)](https://dev.epicgames.com/documentation/en-us/unreal-engine/screen-space-global-illumination-in-unreal-engine) and [Distance Field Ambient Occlusion (DFAO)](https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine). Lumen Reflections replace Screen Space Reflections.

When Lumen is enabled for a project, precomputed static lighting contributions are disabled and all lightmaps are hidden.

## Lumen Lighting Features

Lumen brings robust dynamic global illumination to Unreal Engine and integrates well with other supporting systems in Unreal Engine 5, such as Nanite, World Partition, and Virtual Shadow Maps.

Unreal Engine 4 features, like [Screen Space Global Illumination](https://dev.epicgames.com/documentation/en-us/unreal-engine/screen-space-global-illumination-in-unreal-engine) and [Ray Tracing Global Illumination](https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) (RTGI) were not reliable or performant for projects that relied on real-time with a high enough quality. Also, these features did not fully integrate with other important systems to widely support most features of the engine.

### Lumen Global Illumination

Lumen Global Illumination solves diffuse indirect lighting. For example, light bouncing diffusely off a surface picks up the color of that surface and reflects the colored light onto other nearby surfaces — creating an effect called color bleed. Meshes in the scene also block indirect lighting, which also produces indirect shadowing.

[![](https://dev.epicgames.com/community/api/documentation/image/c951b919-6ce3-4608-80f0-cd4a26ac846d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c951b919-6ce3-4608-80f0-cd4a26ac846d?resizing_type=fit)

Lumen provides infinite diffuse bounces, which are important in scenes with bright diffuse materials like the white paint in the apartment below.

[![](https://dev.epicgames.com/community/api/documentation/image/f0f65ae1-acf9-4d6b-a2c6-e0ec5c5169bd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f0f65ae1-acf9-4d6b-a2c6-e0ec5c5169bd?resizing_type=fit)

Unreal Engine 5's [Nanite Virtualized Geometry](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/Nanite) allows for geometry to be much more detailed than ever before. Lumen achieves full-resolution shading, while computing indirect lighting at a much lower resolution for real-time performance.

[![](https://dev.epicgames.com/community/api/documentation/image/41637eab-4d30-4c4c-9dd9-d03de6a684ce?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/41637eab-4d30-4c4c-9dd9-d03de6a684ce?resizing_type=fit)

### Lumen with Sky Lighting

Sky lighting is solved as part of Lumen's **Final Gather** process. It includes sky shadowing, allowing indoor space to be much darker than outdoor lighting, providing a much more natural effect.

[![](https://dev.epicgames.com/community/api/documentation/image/81920a0f-9219-479d-ab30-127986c79a51?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/81920a0f-9219-479d-ab30-127986c79a51?resizing_type=fit)

Lumen also provides lower-quality global illumination for [Lit Translucency](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-transparency-in-unreal-engine-materials) and [Volumetric Fog](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/Rendering/VolumetricFog).

[![](https://dev.epicgames.com/community/api/documentation/image/56adc133-f29a-42c8-a907-6aa4f404daec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/56adc133-f29a-42c8-a907-6aa4f404daec?resizing_type=fit)

### Lumen and Emissive Materials

Emissive materials propagate light through Lumen's Final Gather with no additional performance cost. However, there's a limit to how small and bright emissive areas can be before they begin to cause noise artifacts to appear. It is inherently much more difficult to solve than manually placed light sources.

[![](https://dev.epicgames.com/community/api/documentation/image/c251d8d3-9512-4919-bce1-97be6109d7ab?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c251d8d3-9512-4919-bce1-97be6109d7ab?resizing_type=fit)

### Lumen Reflections

Lumen solves indirect specular, or reflections, for the full range of material roughness values.

[![](https://dev.epicgames.com/community/api/documentation/image/a0f32280-9c41-4a32-ae12-3f03e0d215ce?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a0f32280-9c41-4a32-ae12-3f03e0d215ce?resizing_type=fit)

Diffuse global illumination and shadowed skylight can be seen in all reflections. Lumen Reflections also support Clear Coat materials, like the car example below.

[![](https://dev.epicgames.com/community/api/documentation/image/4f381e92-b2bf-4265-8d30-1faab41f6410?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4f381e92-b2bf-4265-8d30-1faab41f6410?resizing_type=fit)

Lumen provides glossy reflections on translucency, like the car windows in the example below.

[![](https://dev.epicgames.com/community/api/documentation/image/e08aa3e8-37a6-4e3b-b127-fb98f89b2402?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e08aa3e8-37a6-4e3b-b127-fb98f89b2402?resizing_type=fit)

When the project has **High Quality Translucency Reflections** enabled, Lumen Reflections provide mirror reflections on the frontmost layer of translucent surface materials.

[![Mirror reflections using High Quality Translucent Reflectoions for the project.](https://dev.epicgames.com/community/api/documentation/image/e8dcdaba-65c4-4146-850d-7954111fd733?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e8dcdaba-65c4-4146-850d-7954111fd733?resizing_type=fit)

Lumen Reflections support **Single Layer Water** materials, with reflections forced to mirror.

[![Water material using Single Layer Water with Lumen Reflections.](https://dev.epicgames.com/community/api/documentation/image/80d366cc-4f7d-4e2d-8ac7-f0ab6e3b6550?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/80d366cc-4f7d-4e2d-8ac7-f0ab6e3b6550?resizing_type=fit)

### Lumen Two-Sided Foliage

The **Two-Sided Foliage** shading model is solved by gathering lighting from the backface and scattering it through the leaf, attenuated by the material's **Subsurface Color**.

[![Comparison example of two-sided foliage lit by Lumen.](https://dev.epicgames.com/community/api/documentation/image/73be2f9d-d236-453d-80eb-59635747f0c5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/73be2f9d-d236-453d-80eb-59635747f0c5?resizing_type=fit)

[![Example scene with tree canopy's lit by Lumen.](https://dev.epicgames.com/community/api/documentation/image/74eb427c-9e10-4c25-9fe1-51cea38425f2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/74eb427c-9e10-4c25-9fe1-51cea38425f2?resizing_type=fit)

### Supported Light Types and Other Features

At a high level, Lumen supports the following:

-   All [Light Types](https://dev.epicgames.com/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) are supported, which includes Directional, Sky, Point, Spot, and Rect Lights.
    
-   [Light Functions](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-light-functions-in-unreal-engine) are supported on all types of lights.
    
-   Lights with their [Mobility](https://dev.epicgames.com/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) set to **Static** are not supported because Static Lights are stored completely in lightmaps and their contribution is disabled when Lumen is enabled.
    

## Lumen Settings

Settings for Lumen are found in two places: **Project Settings** and the **Post Process Volume**.

### Lumen Project Settings

All Project Settings that are for, or affect, Lumen are found in the **Engine > Rendering** section. Project Settings contains all the default settings for Lumen for the project.

[![](https://dev.epicgames.com/community/api/documentation/image/60999bf7-cad6-42c2-ae91-4c10333f56f0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/60999bf7-cad6-42c2-ae91-4c10333f56f0?resizing_type=fit)

Below is a listing of all settings that are needed by, or affect, Lumen:

| Property Name | Description |
| --- | --- |
| Global Illumination |   |
| --- | --- |
| 
**Dynamic Global Illumination Method**

 | 

Choose the type of dynamic global illumination you want to use in your project.

 |
| Reflections |   |
| --- | --- |
| 

**Reflection Method**

 | 

Choose the type of dynamic reflections you want to use in your project.

 |
| Lumen |   |
| --- | --- |
| 

**Use Hardware Ray Tracing when available**

 | 

Uses Hardware Ray Tracing for Lumen features when supported by the video card, RHI, and operating system. Lumen will fall back to Software Ray Tracing otherwise. Hardware Ray Tracing has significant scene update costs for scenes with more than 100,000 instances. See [Ray Tracing Performance Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/ray-tracing-performance-guide-in-unreal-engine) for information.

 |
| 

**Ray Lighting Mode**

 | 

Controls how Lumen Reflection rays are lit when Lumen is using Hardware Ray Tracing. By default, Lumen uses **Surface Cache** for best performance, but can be set to **Hit Lighting for Reflections** for higher quality.

 |
| 

**High Quality Translucency Reflections**

 | 

Whether to use high quality mirror reflections on the front layer of translucent surfaces. Other layers will use the lower quality Radiance Cache method that can only produce glossy reflections. This increases GPU cost when enabled from the Post Process Volume settings.

 |
| 

**Software Ray Tracing Mode**

 | 

Controls which tracing method Lumen uses when ray tracing the scene. **Detail Tracing** traces against individual mesh's Distance Fields for the highest quality. **Global Tracing** traces against the lower detail Global Distance Field for fastest traces.

 |
| Hardware Ray Tracing |   |
| --- | --- |
| 

**Support Hardware Ray Tracing**

 | 

Enables ray tracing from supported operating systems, RHI, and video cards for higher quality results.

 |
| Software Ray Tracing |   |
| --- | --- |
| 

**Generate Mesh Distance Fields**

 | 

Whether to build distance fields of Static Meshes. This is needed for Software Ray Tracing with Lumen and Distance Field Ambient Occlusion which is used to implement Movable Sky Light shadows and ray-traced distance field shadows on Directional Lights. Enabling this increases build times, memory usage and disk size of Static Meshes.

 |
| 

**Distance Field Voxel Density**

 | 

Determines how the default scale of a mesh converts into Distance Field Voxel dimensions. Changing this causes all distance fields to be rebuilt. Large values consume memory very quickly.

 |

### Post Process Settings

Post Process Volumes contain overrides and artist-controlled properties for Lumen. The settings are found in the **Global Illumination** and **Reflections** categories.

[![](https://dev.epicgames.com/community/api/documentation/image/768c7a90-6c0c-427f-8a4c-370dede9a69e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/768c7a90-6c0c-427f-8a4c-370dede9a69e?resizing_type=fit)

Below is a listing of all settings for Lumen found in the Post Process Volume:

| Property Name | Description |
| --- | --- |
| Global Illumination: Lumen Global Illumination |   |
| --- | --- |
| 
**Lumen Scene Lighting Quality**

 | 

Larger scales cause Lumen Scene to be calculated with a higher fidelity, which can be visible in reflections, but at a higher GPU cost.

 |
| 

**Lumen Scene Detail**

 | 

Controls the size of instances that can be represented in Lumen Scene. Larger values ensure small objects are represented, but increase GPU cost.

 |
| 

**Lumen Scene View Distance**

 | 

Sets the maximum view distance of the scene that Lumen maintains for ray tracing against. Larger values increase the effective range of sky shadowing and global illumination, but increase GPU cost.

 |
| 

**Final Gather Quality**

 | 

Increases the quality of Lumen Global Illumination and reduces noise being rendered, but increases the GPU cost of rendering it.

 |
| 

**Screen Traces**

 | 

Whether to use screen space traces for Lumen Global Illumination. Screen space traces bypoass Lumen Scene and insteaad sample Scene Depth and Color. This improves quality, but at the same time prevents from Lumen Scene only changes, like adding emissive objects that are only visible in global illumination.

 |
| 

**Max Trace Distance**

 | 

Controls the maximum distance that Lumen should trace while solving lighting. Values that are too small cause lighting to leak into large areas, such as caves. Large values increase the GPU cost to render the scene.

 |
| 

**Scene Capture Cache Resolution**

 | 

Scale factor for Lumen Surface Cache resolution. Smaller values save GPU memory, at a cost in quality. Defaults to 0.5 if not overridden. This should be set on the Scene Capture component in its Post Process Settings.

 |
| Global Illumination: Lumen Global Illumination: Advanced Properties |   |
| --- | --- |
| 

**Lumen Scene Lighting Update Speed**

 | 

Controls how much Lumen Scene is allowed to cache lighting results to improve performance. Larger scales cause lighting changes to propagate faster, but increase GPU cost.

 |
| 

**Final Gather Lighting Update Speed**

 | 

Controls how much Lumen Final Gather is allowed to cache lighting results to improve performance. Larger scales cause lighting changes to propagate faster, but increase GPU cost.

 |
| 

**Diffuse Color Boost**

 | 

Allows brightening indirect lighting by calculating material diffuse color as pow(DiffuseColor, 1/DiffuseColorBoost). Values above 1 (original diffuse color) are not physically correct, but they can be useful as an art direction knob to increase the amount of bounced light in the scene. It works best to keep the value below 2 as it also causes reflections to be brighter than the scene.

 |
| 

**Skylight Leaking**

 | 

Controls what fraction of the Sky Light intensity should be allowed to leak. This is useful as an art direction knob (non-physically based) to keep indoor areas from going fully black.

 |
| 

**Full Skylight Leaking Distance**

 | 

Controls the distance from a receiving surface where skylight leaking reaches its full intensity. Smaller values make the skylight leaking flatter, while larger values create an Ambient Occlusion effect.

 |
| Reflections: Lumen Reflections |   |
| --- | --- |
| 

**Quality**

 | 

Increases the quality of Lumen Reflections on surfaces, and reduces noise being rendered, but increases the GPU cost of rendering them.

 |
| 

**Ray Lighting Mode**

 | 

When using [Hardware Ray Tracing with Lumen](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#hardware-ray-tracing), this setting controls whether reflections will reuse the Surface Cache for cheap lighting, or calculate lighting at the hit point for higher quality.

 |
| 

**Screen Traces**

 | 

Whether to use screen space traces for Lumen Global Illumination. Screen space traces bypoass Lumen Scene and insteaad sample Scene Depth and Color. This improves quality, but at the same time prevents from Lumen Scene only changes, like adding emissive objects that are only visible in global illumination.

 |
| 

**High Quality Translucency Reflections**

 | 

Whether to use high quality mirror reflections on the front layer of translucent surfaces. Other layers will use the lower quality Radiance Cache method that can only produce glossy reflections. This increases GPU cost when enabled. Requires that the Project Setting **High Quality Translucency Reflections** be enabled first.

 |
| 

**Max Roughness To Trace**

 | 

Sets the maximum roughness value for which Lumen still traces dedicated reflection rays. Higher values improve reflection quality but greatly increase GPU cost.

 |
| 

**Max Reflection Bounces**

 | 

Sets the maximum number of recursive reflection bounces. The default is 1, which means a single reflection ray with no secondary reflections in mirror-like surfaces. 2 or more bounces can prevent black areas in reflections when there is enough performance budget to allow it. This post process setting can be up to 8 bounces. You can use the `r.Lumen.Reflections.MaxBounces` to override the post process settings to allow up to 64 reflection bounces. Requires [Hardware Ray Tracing with Hit Lighting for reflections](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) to be enabled in the project settings.

 |
| 

**Max Refraction Bounces**

 | 

The maximum count of refraction events to trace. When hit lighting is used, Translucent meshes are traced when Lumen Max Refraction Bounces are greater than 0, making the reflection tracing more expensive.

 |

## Additional Notes

The following are some additional considerations to keep in mind while working with Lumen features in your projects.

### Lumen Lighting Update Speed

Lumen uses a number of caches to achieve real-time performance. While local lighting changes propagate quickly, global lighting changes, like disabling the Sun, can take multiple seconds to propagate. Projects can use the **Lumen Scene Lighting Update Speed** and **Final Gather Lighting Update Speed** [controls in the Post Process Volume](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) to work around this delay at the cost of increased GPU cost.

### Disabling Static Lighting for the Project

Precomputed lighting from Static lighting is removed when Lumen is enabled. You can disable precomputed lighting entirely for your project from the Project Setting under the **Engine > Rendering** section by disabling **Allow Static Lighting**.

Disabling Static lighting also saves some static lighting overhead with shader permutations. It also allows [Material Ambient Occlusion](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine) to work with Lumen Global Illumination.

Projects that already use Static Lighting will have their lightmaps loaded into memory and on disk until **Force No Precomputed Lighting** is enabled in the **World Settings** of an already loaded Level. You then need to rebuild the lighting and save the Level to remove lightmap data.

### Using Lumen Reflections with Baked Static Lighting

Lumen Reflections can be used without Lumen Global Illumination. This is most beneficial for games and projects which use static lighting but want to scale up in reflection quality beyond the capabilities of placed reflection captures. Standalone Lumen Reflections require [Lumen Hardware Ray Tracing mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#hardware-ray-tracing) to be enabled, which enables hit lighting for reflections automatically.

### Clear Coat Materials

Lumen supports clear coat materials (with dual normals), but with some limitations. These are:

-   Only the top layer can have low roughness values. The bottom layer is assumed to have a rough value, leading to glossy results. This limitations comes from the fact that a single reflection ray is cast per pixel, preventing both the top and bottom layers from casting sharp reflections.
    
-   When the clear coat amount reaches 0, the above limitation still applies. This means that despite having a single (bottom) layer, the reflection continues to look glossy/rough even with low roughness values.
    

### Material Ambient Occlusion

Lumen Global Illumination supports [Material Ambient Occlusion](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine), which provides reliable self-occlusion on Skeletal Meshes.

To use Material Ambient Occlusion with Lumen:

-   Disable **Allow Static Lighting** in the Project Setting to create space in the GBuffer.
    
-   Set the Material to output to **Ambient Occlusion**.
    

[![Lumen Material Ambient Occlusion](https://dev.epicgames.com/community/api/documentation/image/510bca44-e80f-42f2-9140-d5a2b2cc0e04?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/510bca44-e80f-42f2-9140-d5a2b2cc0e04?resizing_type=fit)

Left, Lumen GI on a Skeletal Mesh with only Screen Traces (Software Ray Tracing); Right, Material Ambient Occlusion.

Material Ambient Occlusion is not visible when using the Buffer Visualization **Ambient Occlusion** view mode.

Lumen Global Illumination supports Material [Bent Normal Maps](https://dev.epicgames.com/documentation/en-us/unreal-engine/bent-normal-maps-in-unreal-engine). However, these are significantly more expensive than Material Ambient Occlusion with little visual improvement.

To use Bent Normal Maps with Lumen:

-   Set `r.GBufferDiffuseSampleOcclusion=1` in the `[SystemSettings]` section of your project's DefaultEngine.ini configuration file and restart the editor.
    
-   Set up the Material to output to the **Bent Normal** custom output node.