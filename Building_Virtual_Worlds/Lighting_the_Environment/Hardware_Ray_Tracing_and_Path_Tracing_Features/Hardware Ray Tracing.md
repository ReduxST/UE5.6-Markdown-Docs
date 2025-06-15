# Hardware Ray Tracing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:17

---

Ray tracing is a technique that has primarily been used in offline rendering for film, television, and visualization because it’s capable of producing high-quality, natural-looking images with physically accurate shadowing, ambient occlusion, reflections, and global illumination. Rendering individual frames of a scene can take longer periods of time and often require power computers in a render farm to do so.

Unreal Engine has ray tracing capabilities for real-time and offline through the use of supported hardware. The engine supports standalone ray tracing for some features, like ray-traced shadows. However, most of the core ray tracing functionality is built into the [Lumen global illumination and reflections system](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine). Hardware ray tracing can also be used in conjunction with [Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine) and [Movie Render Queue](/documentation/404) to render high-quality results.

The hardware ray tracing capabilities of the engine are coupled with those of traditional raster techniques — meaning fewer rays for sampling per pixel are needed each frame. When combined with denoising algorithms, the results are perceptually close to those of an offline renderer.

![Example Scene using Ray Tracing features](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c838025-9ef5-48b6-9ec0-bd1ed7bc056d/hwrt-examplescene.png)

Example scene using Ray Tracing features, such as ray-traced shadows and ray-traced reflections.

## Enabling Hardware Ray Tracing

You can enable hardware ray tracing for your project in the Project Settings under **Engine > Rendering > Hardware Ray Tracing**. Check the box for **Support Hardware Ray Tracing**.

![Hardware Ray Tracing Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9b9b870-e862-4aa8-a2f7-480cb6d5d868/hardware-rt-projectsettings.png)

Things to know:

-   When \*\*Support Hardware Ray Tracing is enabled, you may be prompted to enable Support Compute Skin Cache from a pop-up message if it’s not already enabled. Hardware ray tracing requires this to be enabled.
-   Lumen uses hardware ray tracing when **Use Hardware Ray Tracing when available** is checked and when **Ray Lighting Mode** is set to **Hit Lighting for Reflections**. For more information on Lumen’s hardware ray tracing mode, see [Lumen Technical Details](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine).

### Ray Tracing Project Settings

The following project settings are relevant to Hardware Ray Tracing:

| Property | Description |
| --- | --- |
| Lumen |   |
| **Use Hardware Ray Tracing when available** | Uses Hardware Ray Tracing for Lumen features when supported by the video card, RHI, and operating system. Lumen falls back to Software Ray Tracing mode otherwise. Note that Hardware Ray Tracing has significant scene update costs for scenes with more than 100k instances. |
| **Ray Lighting Mode** | 
Controls how Lumen Reflection rays are lit when Lumen is using Hardware Ray Tracing. By default, Lumen uses the Surface Cache for best performance but can be set to Hit Lighting for higher quality.

-   **Surface Cache:** Lighting is calculated for each mesh using Lumen’s generated cards to quickly look up lighting at ray hit points in the scene. This method gives the best reflection performance.
-   **Hit Lighting for Reflections:** Lighting is calculated at a ray’s hit point. This method gives the highest reflection quality but greatly increases GPU cost since the material needs to be evaluated and shadow rays traced. The Surface Cache is still used for diffuse indirect lighting (the global illumination seen in reflections).



 |
| Hardware Ray Tracing |   |
| **Support Hardware Ray Tracing** | Enables support of hardware ray tracing features. Requires **Support Compute Skin Cache**. |
| **Ray Traced Shadows** | Controls whether ray traced shadows are used as the default shadowing method for lights in the project. Lights can override and force ray traced shadows on and off. This option requires that **Support Hardware Ray Tracing** be enabled. |
| **Texture LOD** | Enables automatic texture mip level selection in ray tracing material shaders. When unchecked, the highest resolution mip level is used for all textures. When checked, texture LOD is approximated based on total ray length, output resolution and texel density at the hit point. |

## Features of Hardware Ray Tracing

Hardware ray tracing features of Unreal Engine includes some features that are standalone and some that are integrated with the [Lumen global illumination and reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) system.

### Hardware Ray Traced Shadows

**Ray Traced Shadows** is a standalone feature of hardware ray tracing that simulates soft area shadowing for objects in the environment. These shadows can be more accurate than traditional shadow maps or [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) because they can have hard contact shadows with softer shadows the farther the shadow caster is from the receiving surface.

Virtual shadow maps are the default shadowing method in Unreal Engine and provide plausible soft shadows that support increased shadow resolution to match the highly detailed geometry of Nanite with controllable performance costs. Ray traced shadowing trades this control for more accurate shadow definition.

In the examples, the light pole is tall and its light fixture sits high above the ground. With the directional light high in the sky, you can see how this affects the shadows with each method. The ray-traced shadow in this example has sharper contact shadows on the ground the closer it is to the pole. The farther an object is from the receiving surface, the softer the shadow becomes. With virtual shadow maps, the harder contact shadow and area shadows are more subtle. And, traditional shadow maps are consistent throughout with their hard and soft details, the distance a shadow caster is from the receiving surface has no effect.

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Ray Traced Shadows | Virtual Shadow Maps | Traditional Shadow Maps |

A light’s **Source Size** (Point, Spot, and Rect) or **Source Angle** (Directional) also affects how sharp or soft the shadow is. Larger sizes and angles soften the shadows more, whereas smaller values sharpen the shadows.

The examples below show you the differences between default, larger, and smaller source angles with a directional light. Notice how the changes affect either shadow method’s overall sharpness and softness with the tree’s shadow. Traditional shadow maps are not affected by the size or angle of the light source in this way.

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Directional Source Angle: 0.5357 (Default) | Directional Source Angle: 1.25 | Directional Source Angle: 0.1 |

If Nanite is enabled for an object, ray tracing features uses the Nanite Fallback Target (or fallback mesh) to cast shadows for standalone ray traced shadows. Because the fallback target is often fewer triangles than the Nanite mesh, this can cause visual artifacts since rays are traced against the triangles of the mesh. You can disable Nanite for this object, or increase the Fallback Target value to reduce any artifacts.

### Ray Traced Ambient Occlusion

This standalone ray tracing feature is available when Lumen Global Illumination is disabled. Lumen has its own ambient occlusion.

**Ray Traced Ambient Occlusion** (RTAO) accurately shadows areas blocking ambient lighting in turn grounding objects in the environment more naturally. For example, shadowing in corners and edges where walls meet, and adding depth to the things like crevices and wrinkles in skin.

The example below compares ray traced ambient occlusion with screen space ambient occlusion (SSAO). When visualizing ambient occlusion, the difference becomes clearer since SSAO can only apply ambient shadows for areas it can see on the screen. For example, the area under cars is noticeably brighter than that of ray traced ambient occlusion.

|   |   |
| --- | --- |
| 
 | 

 |
| Ray Traced Ambient Occlusion (RTAO) | Screen Space Ambient Occlusion (SSAO) |

### Hardware Ray Traced Reflections with Lumen

Ray-traced reflections are built into Lumen’s reflection system and are used when enabled in the project settings. Ray-traced reflections support a larger range of geometry types than Lumen’s software ray tracing mode. In particular, it supports tracing against skinned meshes. It also scales better to higher qualities since the rays intersect the triangles of the mesh, having the option to evaluate lighting at the ray hit instead of the lower quality surface cached used with Lumen’s software ray tracing.

To use hardware ray tracing reflections with Lumen, set the **Ray Lighting Mode** to **High Lighting for Reflections** in the Project Settings under **Engine > Rendering** in the **Lumen** category.

|   |   |
| --- | --- |
| 
 | 

 |
| Lumen Reflections with Hardware Ray Tracing | Lumen Reflections with Software Ray Tracing |

Lumen’s reflection system combines screen space traces with both hardware and software ray tracing modes to provide a more reliable method of reflection. It is useful for covering up reflection mismatches between the Lumen scene and the triangle scene.

To inspect the differences between Lumen’s hardware and software ray tracing modes without screen traces, you can remove the check next to **Screen Traces** in the post process volume settings to disable them.

For additional details on Lumen’s reflection system, see [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) and [Lumen Technical Details](/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine).

## Using Ray Tracing Features

Use the sections below to learn about ways you can use and configure ray tracing features in your own projects. Ray Tracing settings primarily exist on individual actors, such as lights, static meshes, and skeletal meshes, and within post process volumes.

### Post Process Volume

Post process volumes contain the majority of settings to configure hardware ray tracing features. These placed volumes are useful for configuring global usage of ray tracing in a level or having them configure specific areas of your level. For example, you could set a large area to use lower quality settings to save on performance cost, but have a smaller volume in an interior have higher quality settings with increased reflection quality, or multiple light bounces for reflections.

With a post process volume, you can control the following ray tracing features:

Post Process Volumes provide controls for the following standalone ray tracing features:

-   Ambient Occlusion (standalone feature)
-   Lumen Reflections with Hit Lighting
-   Translucency (standalone feature)

For additional information about the available post process settings, see Ray Tracing and Path Tracer Properties.

### Lights

By default, lights will use the default shadowing method assigned in the project settings. However, when ray tracing is enabled for the project, lights can optionally use what’s specified in the project settings or force enable or force disable the use of ray tracing.

In the **Details** panel, you can use the **Cast Ray Traced Shadows** dropdown box to select **Use Project Setting** (default), **Enable**, or **Disabled**.

Thes size or angle of the light source also plays a role in defining the look of an object’s shadows. These factors can harden or soften shadowing for any object the light affects. For example, you can see what effect increasing the directional light’s source angle has on the water tower’s shadow. Shadows appear softer with fewer hard shadows compared to the default value.

|   |   |
| --- | --- |
| 
 | 

 |
| Directional Light Source Angle: 0.5357 (Default) | Directional Light Source Angle: 1.5 |

Point and spot lights will have a similar effect on softening shadows of an object based on their size, larger sizes will have softer shadows than smaller ones.

Rect Lights, on the other hand, can be large or small with their light not coming from a single point. This shaped light can create shadows with defined [umbra, penumbra, and antumbra](https://wikipedia.org/wiki/Umbra,_penumbra_and_antumbra) — the inner and outer parts of shadows created from opaque objects. Larger area lights will demonstrate this effect more so than smaller ones.

In the video below, you can see how changing the width and height of the rect light affects the shadows being cast from these objects.

To learn more about these types of lights and their properties, see [Light Types and Their Mobility](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine).

## Performance and Debugging

For details and strategies on optimizing your projects and debugging content that is using ray tracing features, see the [Ray Tracing Performance Guide](/documentation/en-us/unreal-engine/ray-tracing-performance-guide-in-unreal-engine).

## Additional Notes

Below are some additional considerations for hardware ray tracing features.

### Using Hardware Ray Tracing with Vulkan

This feature is experimental.

Ray tracing features are supported on Vulkan, including feature parity with DirectX 12 and Shader Model 6. This allows the full suite of ray tracing features to be used, including Hit Lighting mode with Lumen and the path tracer.

Vulkan ray tracing supports both Linux and Windows platforms.

To enable Vulkan ray tracing in your project, add the following lines to these configuration (\*ini) files:

Add the following lines to the **DataDrivenPlatformInfo.ini** file under the `[ShaderPlatform VULKAN_SM6]` section located in your **Engine/Config/VulkanPC** folder:

```
`bSupportsRayTracingShaders = true bSupportsPathTracing = true bSupportsRayTracingCallableShaders = true bSupportsRayTracingProceduralPrimitive = true BindlessSupport=RayTracingOnly`
Copy full snippet
```
bSupportsRayTracingShaders = true bSupportsPathTracing = true bSupportsRayTracingCallableShaders = true bSupportsRayTracingProceduralPrimitive = true BindlessSupport=RayTracingOnly

Depending on whether your adding Vulkan ray tracing to Windows or Linux, you’ll need to update the **BaseLinuxEngine.ini** or **BaseWindowEngine.ini** files located in their respective folder, **Engine/Config/Linux** or **Engine/Config/Windows**.

```
`[SF_VULKAN_SM6] BindlessResources=Enabled BindlessSamplers=Enabled`
Copy full snippet
```
\[SF\_VULKAN\_SM6\] BindlessResources=Enabled BindlessSamplers=Enabled

### Toggle Ray Tracing at Runtime

This feature is experimental.

Hardware ray tracing can be dynamically switched on and off for your desktop game projects without needing to restart the game. This is useful when you want to give players the option to turn off features like this for performance reasons. You can enable this feature by adding the following commands to your **WindowsEngine.ini** configuration file:

-   `r.RayTracing.EnableOnDemand=1`
-   `r.RayTracing.Enable=1`
    -   1 starts with hardware ray tracing enabled by default. 0 starts with it disabled.

Once these are set in your project configuration file, you can toggle hardware ray tracing using the following the `r.RayTracing.Enable` command. It has the following options:

-   **0** disables ray tracing.
-   **1** enables ray tracing all the time.

## Supported Ray Tracing Features

The following list of features is intended to give you an idea of what is supported by our core hardware ray tracing features in Unreal Engine. This is not meant to be a comprehensive list of supported features.

| Feature | Supported (Y/N/Partially) | Additional Notes |
| --- | --- | --- |
| Rendering Path |   |   |
| **Deferred** | Y |   |
| **Forward** | N |   |
| Geometry Types |   |   |
| **Nanite** | N | The fallabck target (also called the Fallback Mesh) is used for Nanite-enabled meshes. Lower the fallback relative error setting in the Static Mesh Editor to use more of the mesh's triangles for representation in the ray tracing scene. Nanite is enabled with `r.RayTracing.Nanite.Mode`. 0 (default) supports Nanite's fallback mesh. 1 supports the streamed out mesh. |
| **Skinned Mesh** | Y |   |
| **Static Mesh** | Y |   |
| **Geometry Cache (Alembic)** | Y |   |
| **Landscape** | Y |   |
| **Hierarchical Instanced Static Mesh (HISM)** | Y |   |
| **Instanced Static Mesh (ISM)** | Y |   |
| **Splines** | Y |   |
| **Procedural Mesh** | Y | This type of geometry can be expensive to render in Ray Tracing. |
| **Levels of Detail (LOD)** | Y | Dithered LOD transitions are not yet supported. |
| **World Position Offset-driven Animation** | Y | Check the **Evaluate World Position Offset** property on individual scene actors to opt in to using WPO with ray tracing. |
| **Hair Strands** | Y | Support for Hair strands is considered experimental as it can require many resources to build efficient acceleration structures. You can use the console variable `r.HairStrands.RayTracingProceduralSplits` to balance between rendering performance and acceleration structure build performance (memory usage). The default value (4) emphasizes rendering performance but heavy groovers can lead to instability. If you experience GPU timeouts, try lowering this value to reduce the number of hair segments in the groom. |
| **Water Geometry** | Y | Supported when `r.RayTracing.Geometry.Water` is set to 1. |
| Visual Effects (VFX) |   |   |
| **Niagara** | Partially | Currently supports Sprites, Ribbons, and Mesh emitters. |
| Types of Lights |   |   |
| **Directional Light** | Y |   |
| **Sky Light** | Y |   |
| **Point Light** | Y |   |
| **Spot Light** | Y |   |
| **Rect Light** | Y |   |
| Features of Lights |   |   |
| **Emissive Surfaces** | Y | This is supported with the Lumen Global Illumination and Reflections system with Software and Hardware Ray Tracing modes. |
| **Sky Atmosphere** | Y |   |
| **Volumetric Clouds** | Y |   |
| **Height Fog** | Y |   |
| **Volumetric Fog** | Y | 
Enabled with the console variable `r.VolumetricFog.InjectRayTracedLights`:

-   0: disabled (default due to performance cost)
-   1: lights with Ray Traced shadows are injected into the Volumetric Fog



 |
| **IES Profiles** | Y |   |
| **Light Functions** | Y |   |
| **Image Based Lighting (IBL)** | Y | Support for HDRI with Sky Light. |
| **Light Transmission** | N | The translucent shadow is treated as opaque, meaning no colored shadows or light transmission through the material. |
| Materials: Shading Model |   |   |
| **Default Lit** | Y |   |
| **Unlit** | Partially |   |
| **Masked** | Partially | Supports casting of masked shadows. |
| **SubSurface and SubSurface Profile** | Y |   |
| **Preintegrated Skin** | Partially | Works but the result isn't correctly raytraced. It uses the raster pipeline. |
| **Clear Coat** | Y |   |
| **TwoSided Foliage** | Y |   |
| **Hair** | Partially | Works but the result isn't correctly raytraced. It uses the raster pipeline. |
| **Cloth** | Partially | Works but the result isn't correctly raytraced. It uses the raster pipeline. |
| **Eye** | Y |   |
| **Single Layer Water** | Y |   |
| **Thin Translucent** | Y | Does not support colored light transmission. |
| **From Material Expression** | Y |   |
| Materials Features |   |   |
| **Substrate** | Y | Experimental support is implemented. |
| **Colored Shadows** | N |   |
| **Translucent Shadows** | Y |   |
| **Refraction** | Y |   |
| **Decals** | Y |   |
| **Anisotropy** | Y |   |
| System Support |   |   |
| **Sequencer Movie Render Queue** | Y |   |
| **Orthographic Camera Projection** | Y |   |
| **Multi-View (VR and Split-screen)** | Y |   |