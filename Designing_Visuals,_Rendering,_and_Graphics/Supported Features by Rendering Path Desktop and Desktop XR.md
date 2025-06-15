# Supported Features by Rendering Path: Desktop and Desktop XR

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/supported-features-by-rendering-path-for-desktop-with-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/supported-features-by-rendering-path-for-desktop-with-unreal-engine)  
**Processed:** 2025-06-14 16:53:05

---

The tables found in this page lists features of Unreal Engine 5 and the rendering paths they support.

The features listed in this page are intended to give you a general idea of what features are supported by the different rendering paths available in Unreal Engine 5. Some features may not fully support a rendering path, even if it indicates it does. It's recommended to check the documentation for each feature in cases where it may not be clear. For example, in the case of Lumen, Nanite, Virtual Shadow Maps, and Ray Tracing.

## Top Rendering Features of UE5 Quick Reference

The following table is a quick reference of selected new Unreal Engine 5 features and their supported rendering paths.

Some features of Unreal Engine 5 require DirectX 12 with Shader Model 6 (SM6) to work, such as [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) and [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine). Refer to [Hardware and Software Specifications](/documentation/404) more specific requirements.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Lumen Global Illumination: Software Ray Tracing** | Y | Y | N | Y | N |
| **Lumen Global Illumination: Hardware Ray Tracing** | Y | N | N | Y | N |
| **Nanite Virtualized Geometry** | Y | N | N | Y | N |
| **Virtual Shadow Maps** | Y | N | N | Y | N |
| **Temporal Super Resolution** | Y | Y | N | Y | Y |
| **Path Tracer** | Y | N | N | N | N |

## Post Processing

Post Processing enables artists to control the overall look and feel of their scene using placed volumes. Each volume contains lighting and rendering features that affect the look of the scene for things such as type of global illumination and reflections that are used, color grading, amongst other lighting effects.

See [Post Process Effects](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine) to learn more about the available post-processing options.

### Lens

The **Lens** category contains properties that affect the look of the scene that can be created by a camera lens. For example, things like lens flare, depth of field, exposure, and other similar types of effects.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Mobile Depth of Field Properties** | N | N | N | N | N |
| **Mobile Depth of Field: High Quality Gaussian** | N | N | N | N | N |
| **Bloom: Standard** | Y | Y | Y | Y | Y |
| **Bloom: Convolution** | Y | Y | Y | Y | Y |
| **Exposure** | Y | Y | Y | Y | Y |
| **Chromatic Aberration Properties** | Y | Y | Y | Y | Y |
| **Dirt Mask Properties** | Y | Y | Y | Y | Y |
| **Camera Properties** | Y | Y | Y | Y | Y |
| **Local Exposure** | Y | Y | Y | Y | Y |
| **Lens Flare Properties** | Y | Y | Y | Y | Y |
| **Image Effects: Vignette** | Y | Y | Y | Y | Y |
| **Depth of Field Properties** | Y | Y | Y | Y | Y |

### Color Grading

The **Color Grading** category enables color styling and color palettes to be applied on top of the rendered scene without making direct changes to the content in the scene itself. Artistic choices can be made to adjust things such as color temperature, saturation, contrast, and more. Color grading can also be used to adjust those highlights, midtones, or even shadows without being destructive to the content in the scene.

See [Color Grading](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine) to learn more.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Color Grading Properties** | Y | Y | Y | Y | Y |

### Film

The **Film** category enables artistic choices to map the scene colors to match those of the Academy Color Encoding System (or ACES) standard.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Film Properties** | Y | Y | Y | Y | Y |

### Post Process Global Illumination

The **Global Illumination** category primarily contains properties for selecting the type of global illumination to use for the Post Process Volume.

For general support of Global Illumination features, see the [General Engine Features](/documentation/en-us/unreal-engine/supported-features-by-rendering-path-for-desktop-with-unreal-engine#generalenginefeatures) section of this page.

### Post Process Reflections

The **Reflections** category primarily contains properties for selecting the type of reflections to use for the Post Process Volume.

For general support of Reflections features, see the [General Engine Features](/documentation/en-us/unreal-engine/supported-features-by-rendering-path-for-desktop-with-unreal-engine#generalenginefeatures) section of this page.

### Rendering Features

The **Rendering Features** category contains features that are specific to the Post Process Volume, such as controlling motion blur, screen space reflection, and ambient occlusion. It also provides configurable settings for features such as [Hardware Ray Tracing and the Path Tracer](/documentation/en-us/unreal-engine/ray-tracing-and-path-tracing-features-in-unreal-engine).

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Post Process Material Properties** | Y | Y | Y | Y | Y |
| **Ambient Cubemap Properties** | Y | Y | N | Y | N |
| **Ambient Occlusion Properties** | Y | Y | Y | Y | Y |
| **Global Illumination Properties** | Y | Y | Y | Y | Y |
| **Reflections Properties** | Y | Y | Y | Y | Y |
| **Motion Blur Properties** | Y | Y | Y | \- | \- |
| **Translucency Type: Raster** | Y | Y | Y | Y | Y |
| **Translucency Type: Ray Tracing** | Y | N | N | N | N |
| **Ray Tracing Translucency Properties** | Y | N | N | N | N |
| **Path Tracing Properties** | Y | N | N | N | N |

For Ray Tracing and Path Tracer features that have additional requirements, see [Hardware Ray Tracing and Path Tracing](/documentation/en-us/unreal-engine/ray-tracing-and-path-tracing-features-in-unreal-engine) for complete specifications.

### Film Grain

The **Film Grain** category contains properties that give an intentionally film-like appearance to the scene. Film grain can be a purely visual choice that adds realism to your project with a cinematic look.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Film Properties** | Y | Y | Y | Y | Y |

## General Engine Features

The following are listings of features supported across the various rendering paths available in Unreal Engine.

### Anti-Aliasing

**Anti-Aliasing** techniques are used to smooth or remove the jagged edges in a rendered image. There are multiple anti-aliasing techniques to choose from, with some being better suited for specific hardware and platforms.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Temporal Super Resolution** | Y | Y | Y | Y | Y |
| **Fast Approximation Anti-Aliasing (FXAA)** | Y | N | Y | N | Y |
| **Multi-Sample Anti-Aliasing (MSAA)** | N | N | Y | N | N |
| **Temporal Anti-Aliasing (TAA)** | Y | Y | Y | Y | Y |

### Systems and Tools Features

The following are general features of Unreal Engine 5 that work in conjunction with other parts of the engine, for example materials and lighting.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Nanite Virtualized Geometry** | Y | N | N | N | N |
| **Hardware Ray Tracing Features** | Y | N | N | Y | N |
| **Path Tracer** | Y | N | N | N | N |
| **Texture Streaming** | Y | Y | Y | Y | Y |
| **Virtual Textures: Streaming** | Y | Y | Y | Y | Y |
| **Virtual Textures: Runtime** | Y | Y | Y | Y | Y |
| **Mesh Decals** | Y | Y | Y | Y | Y |
| **Mesh Distance Fields** | Y | Y | Y | Y | Y |
| **Water System** | Y | Y | Y | Y | Y |
| **Hair and Fur Grooms** | Y | Y | Y | Y | Y |

### Level of Detail

**Level of Detail** (or LOD) is an optimization whereby lowering geometric detail of objects at specified distances from the camera has the potential to improve performance. This includes material-based transitions that can reduce the visual switching (or popping that occurs) when swapping between the levels of detail.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Level of Detail** | Y | Y | Y | Y | Y |
| **Hierarchical Level of Detail** | Y | Y | Y | Y | Y |
| **Dither LOD Transition** | Y | Y | Y | Y | Y |

### Visibility and Occlusion Culling

Different **Visibility and Occlusion Culling** methods are used to reduce the number of rendered objects in the scene to improve performance. Culling is handled in a few different ways depending on the chosen method: size and distance, and visibility from the player camera. Some methods are only available — even, better suited — for some platforms over others. Some culling methods can be used in conjunction with another method.

See [Visibility and Occlusion Culling](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine) to learn more about them.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Cull Distance Volumes** | Y | Y | Y | Y | Y |
| **Precomputed Visibility Volumes** | Y | Y | Y | Y | Y |
| **Hardware (GPU) Occlusion Queries** | Y | Y | Y | Y | Y |

## Lighting Features

The following lighting features are supported across Unreal Engine's rendering paths.

To learn more about all of Unreal Engine's lighting features, see [Lighting the Environment](/documentation/en-us/unreal-engine/lighting-the-environment-in-unreal-engine).

### Environmental Lighting and Effects

Lighting for large open worlds requires features that seamlessly work together to create a unified experience. These include components for creating atmosphere, clouds, fog, and fully supported dynamic lighting from the sun and moon.

See [Environmental Lighting](/documentation/en-us/unreal-engine/environmental-light-with-fog-clouds-sky-and-atmosphere-in-unreal-engine) to learn more about them.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Sky Atmosphere** | Y | Y | Y | Y | Y |
| **Volumetric Clouds** | Y | Y | Y | Y | Y |
| **Exponential Height Fog** | Y | Y | Y | Y | Y |
| **Volumetric Fog** | Y | Y | Y | Y | Y |

### Global Illumination

**Global Illumination** simulates lighting interactions with geometry and material surfaces to add accurate-looking lighting to a scene. Unreal Engine provides precomputed and dynamic global illumination methods. See [Global Illumination](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) to learn more about them.

See [Global Illumination](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) to learn more about them.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Lumen Global Illumination: Software Ray Tracing** | Y | Y | N | N | N |
| **Lumen Global Illumination: Hardware Ray Tracing** | Y | N | N | N | N |
| **Precomputed Global Illumination with Lightmass** | Y | Y | Y | Y | Y |
| **Screen Space Global Illumination** | Y | Y | N | Y | N |
| **Ray Tracing Global Illumination (Deprecated)** | Y | N | N | Y | N |

Some features of Hardware Ray Tracing have been deprecated and may be removed in later versions of the engine. Lumen Global Illumination is the replacement for these features.

### Shadowing

**Shadows** enables objects to feel grounded in the world, while providing a sense of depth and space. Unreal Engine provides different methods for shadowing objects in your projects, with some shadowing methods being better suited specific platforms and hardware.

See [Shadowing](/documentation/en-us/unreal-engine/shadowing-in-unreal-engine) to learn more about them.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Standalone Hardware Ray Traced Shadows** | Y | N | N | Y | N |
| **Virtual Shadow Maps** | Y | N | N | Y | N |
| **Modulated Shadows** | Y | Y | Y | Y | Y |
| **Capsule Shadows** | Y | Y | N | Y | N |
| **Contact Shadows** | Y | Y | N | Y | N |
| **Precomputed Translucent Shadows** | Y | Y | Y | Y | Y |
| **Dynamic Translucent Shadows** | Y | Y | N | Y | N |

### Reflections

**Reflections** are another way to ground objects in the world and add a sense of realism. Reflections start with rough or smooth the materials applied to surfaces are. The smoother a material, the more a surface can reflect light that hits it.

Unreal Engine provides different methods of reflections for materials that include precomputed static reflections and fully dynamic reflections to choose from for your project. Not all reflection systems are exclusive to itself and some can be used together with one another.

See [Reflections Environment](/documentation/en-us/unreal-engine/reflections-environment-in-unreal-engine) to learn more about them.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Reflection Captures (Box/Sphere)** | Y | Y | Y | Y | Y |
| **Scene Capture Cubemap** | Y | Y | Y | Y | Y |
| **Scene Capture 2D** | Y | Y | Y | Y | Y |
| **Planar Reflections** | Y | Y | Y | Y | Y |
| **Screen Space Reflections** | Y | Y | N | Y | N |
| **Standalone Hardware Ray Traced Reflections (Deprecated)** | Y | N | N | N | N |
| **High Precision Normals** | Y | Y | Y | Y | Y |
| **Reflection Capture Resolution** | Y | Y | Y | Y | Y |
| **HDR Cubemaps** | Y | Y | Y | Y | Y |

Some features of Hardware Ray Tracing have been deprecated and may be removed in later versions of the engine. Lumen Global Illumination is the replacement for these features.

## Light Type and Mobility Features

When thinking about how to light your project, you want to consider all the various types of lights you may need and whether they need to be fully, partially static and dynamic, or fully dynamic. When deciding the type of light to use, it is just as important to think about how that light will be used and if it needs to dynamically change or not, which can have an impact on how your project looks and interacts with objects being lit, and with performance.

See [Light Types and Their Mobility](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) for more information on using the different types of lights and how their mobility affects them.

### Static Lighting

This section includes a breakdown of what types of lights and their common features are supported when using precomputed **Static** Light Mobility.

For more details, see [Static Light Mobility](/documentation/en-us/unreal-engine/static-light-mobility-in-unreal-engine).

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| Static Mobility: Light Types |   |   |   |   |   |
| **Directional Light** | Y | Y | Y | Y | Y |
| **Sky Light** | Y | Y | Y | Y | Y |
| **Point Light** | Y | Y | Y | Y | Y |
| **Spot Light** | Y | Y | Y | Y | Y |
| **Rect Light** | Y | Y | Y | Y | Y |
| Static Mobility: General Lighting Features |   |   |   |   |   |
| **Indirect Lighting Intensity** | Y | Y | Y | Y | Y |
| **Lighting Channels** | Y | Y | Y | Y | Y |
| **Light Transmission** | Y | Y | N | Y | N |
| **Light Functions** | Y | Y | N | Y | N |
| Static Mobility: Directional Light Features |   |   |   |   |   |
| **Source Angle** | Y | Y | Y | Y | Y |
| **Light Shafts** | Y | Y | N | Y | N |
| **Modulated Shadows** | N | N | N | N | N |
| Static Mobility: Sky Light Features |   |   |   |   |   |
| **SLS Captured Scene** | Y | Y | Y | Y | Y |
| **SLS Specified Cubemap** | Y | Y | Y | Y | Y |
| **Specified Cubemap Resolution** | Y | Y | Y | Y | Y |
| Static Mobility: Point, Spot, Rect Light Features |   |   |   |   |   |
| **IES Textures** | Y | Y | Y | Y | Y |
| **Rect Light: Source Texture** | Y | Y | Y | Y | Y |

### Stationary Lighting

This section includes a breakdown of what types of lights and their common features are supported when using **Stationary** Light Mobility.

For more details, see [Stationary Light Mobility](/documentation/en-us/unreal-engine/stationary-light-mobility-in-unreal-engine).

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| Stationary Mobility: Light Types |   |   |   |   |   |
| **Directional Light** | Y | Y | Y | Y | Y |
| **Sky Light** | Y | Y | Y | Y | Y |
| **Point Light** | Y | Y | Y | Y | Y |
| **Spot Light** | Y | Y | Y | Y | Y |
| **Rect Light** | Y | Y | Y | Y | Y |
| Stationary Mobility: General Lighting Features |   |   |   |   |   |
| **Indirect Lighting Intensity** | Y | Y | Y | Y | Y |
| **Lighting Channels** | Y | Y | Y | Y | Y |
| **Light Transmission** | Y | Y | N | Y | N |
| **Light Functions** | Y | Y | N | Y | N |
| Stationary Mobility: Directional Light Features |   |   |   |   |   |
| **Source Angle** | Y | Y | Y | Y | Y |
| **Cascaded Shadow Maps** | Y | Y | Y | Y | Y |
| **Light Shafts** | Y | Y | N | Y | N |
| **Modulated Shadows** | N | N | N | N | N |
| Stationary Mobility: Sky Light Features |   |   |   |   |   |
| **SLS Captured Scene** | Y | Y | Y | Y | Y |
| **SLS Specified Cubemap** | Y | Y | Y | Y | Y |
| **Specified Cubemap Resolution** | Y | Y | Y | Y | Y |
| Stationary Mobility: Point, Spot, Rect Light Features |   |   |   |   |   |
| **IES Textures** | Y | Y | Y | Y | Y |
| **Rect Light: Source Texture** | Y | Y | Y | Y | Y |

### Movable Lighting

This section includes a breakdown of what types of lights and their common features are supported when using **Movable** Light Mobility.

For more details, see [Movable Light Mobility](/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine).

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| Movable Mobility: Light Types |   |   |   |   |   |
| **Directional Light** | Y | Y | Y | Y | Y |
| **Sky Light** | Y | Y | Y | Y | Y |
| **Point Light** | Y | Y | Y | Y | Y |
| **Spot Light** | Y | Y | Y | Y | Y |
| **Rect Light** | Y | Y | Y | Y | Y |
| Movable Mobility: General Lighting Features |   |   |   |   |   |
| **Indirect Lighting Intensity** | Y | Y | Y | Y | Y |
| **Lighting Channels** | Y | Y | Y | Y | Y |
| **Light Transmission** | Y | Y | N | Y | N |
| **Light Functions** | Y | Y | N | Y | N |
| Movable Mobility: Directional Light Features |   |   |   |   |   |
| **Source Angle** | Y | Y | N | Y | N |
| **Cascaded Shadow Maps** | Y | Y | Y | Y | Y |
| **Light Shafts** | Y | Y | N | Y | N |
| **Modulated Shadows** | N | N | N | N | N |
| **Distance Field Shadows** | Y | Y | Y | Y | Y |
| Movable Mobility: Sky Light Features |   |   |   |   |   |
| **SLS Captured Scene** | Y | Y | Y | Y | Y |
| **SLS Specified Cubemap** | Y | Y | Y | Y | Y |
| **Specified Cubemap Resolution** | Y | Y | Y | Y | Y |
| Movable Mobility: Point, Spot, Rect Light Features |   |   |   |   |   |
| **IES Textures** | Y | Y | Y | Y | Y |
| **Rect Light: Source Texture** | Y | Y | N | Y | N |

## Materials and Textures

Materials and Textures are applied to surfaces to control the visual representation of a surface and typically how it interacts with lighting. There are a variety of material and texture types that can be used in your projects.

See [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials) and [Textures](/documentation/en-us/unreal-engine/textures-in-unreal-engine) to learn about them.

### Material Domain

The **Material Domain** defines what the material will be used for in your project.

See [Material Properties](/documentation/en-us/unreal-engine/unreal-engine-material-properties) for more information.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Surface** | Y | Y | Y | Y | Y |
| **Deferred Decal** | Y | Y | Y | Y | Y |
| **Light Function** | Y | Y | N | Y | N |
| **Volume** | Y | Y | Y | Y | Y |
| **Post Process** | Y | Y | Y | Y | Y |
| **User Interface** | Y | Y | Y | Y | Y |

### Material Blend Mode

The **Blend Mode** describes how the output of the current material will blend over what is already being drawn in the background. It allows you to control how the engine will combine this material (source color) with what is already in the frame buffer (destination color) when rendered.

See [Material Properties](/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine) for more information.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Opaque** | Y | Y | Y | Y | Y |
| **Masked** | Y | Y | Y | Y | Y |
| **Translucent** | Y | Y | Y | Y | Y |
| **Additive** | Y | Y | Y | Y | Y |
| **Modulate** | Y | Y | Y | Y | Y |
| **Alpha Composite (Premultiplied Alpha)** | Y | Y | Y | Y | Y |
| **Alpha Holdout** | Y | Y | Y | Y | Y |

### Material Shading Model

The **Shading Model** determines how material inputs are combined to make the final color.

See [Shading Models](/documentation/en-us/unreal-engine/shading-models-in-unreal-engine) for more information.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Unlit** | Y | Y | Y | Y | Y |
| **Default Lit** | Y | Y | Y | Y | Y |
| **Subsurface** | Y | Y | Y | Y | Y |
| **Preintegrated Skin** | Y | Y | Y | Y | Y |
| **Clear Coat** | Y | Y | Y | Y | Y |
| **Subsurface Profile** | Y | Y | Y | Y | Y |
| **Two Sided Foliage** | Y | Y | Y | Y | Y |
| **Hair** | Y | Y | Y | Y | Y |
| **Cloth** | Y | Y | Y | Y | Y |
| **Eye** | Y | Y | Y | Y | Y |
| **Single Layer Water** | Y | Y | Y | Y | Y |
| **Thin Translucent** | Y | Y | Y | Y | Y |
| **From Material Expression** | Y | Y | Y | Y | Y |

### Material Inputs

**Material Inputs** are the inputs being fed data through the Main Material node to define surface properties and how they interact with light. The types of inputs available are determined by the materials set domain, blend mode, and shading model.

See [Material Inputs](/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine) to learn more about them.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Base Color** | Y | Y | Y | Y | Y |
| **Metallic** | Y | Y | Y | Y | Y |
| **Specular** | Y | Y | Y | Y | Y |
| **Roughness** | Y | Y | Y | Y | Y |
| **Anisotropy** | Y | Y | Y | Y | Y |
| **Emissive Color** | Y | Y | Y | Y | Y |
| **Opacity** | Y | Y | Y | Y | Y |
| **Normal** | Y | Y | Y | Y | Y |
| **Tangent** | Y | Y | Y | Y | Y |
| **World Position Offset** | Y | Y | Y | Y | Y |
| **Cloth** | Y | Y | Y | Y | Y |
| **Fuzz Color** | Y | Y | Y | Y | Y |
| **Iris Mask** | Y | Y | Y | Y | Y |
| **Iris Distance** | Y | Y | Y | Y | Y |
| **Subsurface Color** | Y | Y | Y | Y | Y |
| **Custom Data 0 – 7** | Y | Y | Y | Y | Y |
| **Ambient Occlusion** | Y | Y | Y | Y | Y |
| **Refraction** | Y | Y | Y | Y | Y |
| **Pixel Depth Offset** | Y | Y | Y | Y | Y |
| **Shading Model** | Y | Y | Y | Y | Y |
| **Clear Coat** | Y | Y | Y | Y | Y |
| **Clear Coat Roughness** | Y | Y | Y | Y | Y |
| **Backlit (for Hair)** | Y | Y | Y | Y | Y |

### Textures

**Textures** are image assets that are primarily used in [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials) but can also be directly applied to components in some situations. For Materials, textures are mapped to surfaces which the material is applied to. Textures can be used for a variety of calculations within a Material, such as a base color, normal map, and mask.

See [Textures](/documentation/en-us/unreal-engine/textures-in-unreal-engine) for more information on using them.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Default (DXT 1/5, BC ⅓ on DX11)** | Y | Y | Y | Y | Y |
| **Normal Map (DXT 5, BC5 on DX11)** | Y | Y | Y | Y | Y |
| **Masks (no sRGB)** | Y | Y | Y | Y | Y |
| **Grayscale (R8, RGB8, sRGB)** | Y | Y | Y | Y | Y |
| **Displacement Map (8/16-bit)** | Y | Y | Y | Y | Y |
| **Vector Displacement Map (RGBA8)** | Y | Y | Y | Y | Y |
| **HDR (RGB, no sRGB)** | Y | Y | Y | Y | Y |
| **User Interface 2D (RGBA)** | Y | Y | Y | Y | Y |
| **Alpha (no sRGB, BC4 on DX11)** | Y | Y | Y | Y | Y |
| **Distance Field Font (R8)** | Y | Y | Y | Y | Y |
| **HDR Compressed (RGB, BC6H, DX11)** | Y | Y | Y | Y | Y |
| **BC7 (DX11, optional A)** | Y | Y | Y | Y | Y |
| **Half Float (R16F)** | Y | Y | Y | Y | Y |

### Decals

**Decals** are [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials) that are projected surfaces in your Level. Decals can even be applied to some geometry as a placed mesh decal.

| Property | Desktop Deferred (SM5/SM6: DirectX 12, macOS, Vulkan Desktop) | Desktop Deferred (SM5: DirectX 11, macOS Metal, Vulkan Desktop) | Desktop Forward | Desktop XR Deferred | Desktop XR Forward |
| --- | --- | --- | --- | --- | --- |
| **Mesh Decals** | Y | Y | Y | Y | Y |
| **Material Decal Response (DBuffer): Color Normal Roughness** | Y | Y | Y | Y | Y |
| **Material Decal Response (DBuffer): Color** | Y | Y | Y | Y | Y |
| **Material Decal Response (DBuffer): Color Normal** | Y | Y | Y | Y | Y |
| **Material Decal Response (DBuffer): Color Roughness** | Y | Y | Y | Y | Y |
| **Material Decal Response (DBuffer): Normal** | Y | Y | Y | Y | Y |
| **Material Decal Response (DBuffer): Normal Roughness** | Y | Y | Y | Y | Y |
| **Material Decal Response (DBuffer): Roughness** | Y | Y | Y | Y | Y |