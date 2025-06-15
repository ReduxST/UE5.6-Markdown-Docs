# Mobile Rendering Features

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-features-for-mobile-games-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-features-for-mobile-games-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:50

---

Many mobile devices have significant hardware limitations compared with desktop hardware and game consoles, especially in terms of compatibility with graphics features. To address this, **Unreal Engine** has an alternate rendering path for mobile devices. This rendering path uses simplified or performance-oriented models for many of Unreal's rendering features, such as shadows and textures, and it removes many unsupported post-processes. The guides in this section provide details about configuration options and features in the mobile renderer.

The following links contain specialized topics in Mobile rendering.

## Feature Levels

The basic **Feature Levels** for Mobile are as follows:

| Feature Level | Description |
| --- | --- |
| OpenGL ES 3.2 | The default feature level for Android devices. You can configure the material settings for this feature level in **Project Settings** > **Platforms** > **Android Material Quality - ES32**. |
| Android Vulkan | A high-end renderer available for some specific Android devices. For more information on how to use Vulkan in your projects and what GPUs support it, see our guide on the [Android Vulkan Mobile Renderer](/documentation/en-us/unreal-engine/using-the-android-vulkan-mobile-renderer-in-unreal-engine). |
| Metal 2.0 | The feature level used for iOS devices. You can configure material settings for this feature level in **Project Settings** > **Platforms** > **iOS Material Quality**. |

## Supported Rendering Features

Each column in the tables below lists whether or not a feature is supported. The possible values are as follows:

| Value | Description |
| --- | --- |
| Yes | The feature is supported on the hardware for this column. |
| No | The feature is not supported on the hardware for this column. |
| Yes \* | The feature is supported, but may require some prerequisites or additional setup to be used. |

### Post Process Volume

| Feature | Mobile Forward (Open GL ES 3.2, Metal, Vulkan, Switch) | Mobile Deferred (Metal, Vulkan, Switch) | Mobile Forward w/ HDR Disabled (Head-mounted Mobile XR) |
| --- | --- | --- | --- |
| Lens |   |   |   |
| Mobile Depth of Field Properties | **Yes** | **Yes** | No |
| Mobile DoF - High Quality Gaussian DoF | **Yes** | **Yes** | No |
| Bloom - Standard | **Yes** | **Yes** | No |
| Bloom - Convolution | No | No | No |
| Chromatic Abberation Properties | **Yes** | **Yes** | No |
| Dirt Mask Properties | **Yes** | **Yes** | No |
| Camera Properties | No | No | No |
| Lens Flare Properties | **Yes** | **Yes** | No |
| Image Effects Properties | **Yes** | **Yes** | No |
| Cinematic Depth of Field Properties | No | No | No |
| Exposure |   |   |   |
| Metering Mode - Auto Exposure Histogram | **Yes** | **Yes** | No |
| Metering Mode - Auto Exposure Basic | **Yes** | **Yes** | No |
| Metering Mode - Manual | **Yes** | **Yes** | **Yes** |
| Local Exposure | No | No | No |
| Color Grading |   |   |   |
| Color Grading Properties | **Yes** | **Yes** | No |
| Film |   |   |   |
| Film Properties | **Yes** | **Yes** | No |
| Rendering Features |   |   |   |
| Post Process Material Properties | **Yes** | **Yes** | No |
| Ambient Cubemap Properties | No | No | No |
| Ambient Occlusion Properties | **Yes** | **Yes** | No |
| Global Illumination Properties | No | No | No |
| Reflections Properties | No | No | No |
| Motion Blur Properties | No | No | No |
| Translucency Type: Raster | **Yes** | **Yes** | **Yes** |
| Translucency Type: Ray Tracing | No | No | No |
| Ray Tracing Transluency Properties | No | No | No |
| Path Tracer Properties | No | No | No |
| Film Grain |   |   |   |
| Film Grain Properties | No | No | No |

### General Rendering Features

| Feature | Mobile Forward (Open GL ES 3.2, Metal, Vulkan, Switch) | Mobile Deferred (Metal, Vulkan, Switch) | Mobile Forward w/ HDR Disabled (Head-mounted Mobile XR) |
| --- | --- | --- | --- |
| Anti-Aliasing |   |   |   |
| Temporal Super Resolution (TSR) | No | No | No |
| Fast Approximation Anti-Aliasing (FXAA) | **Yes** | **Yes** | No |
| Multi-Sample Anti-Aliasing (MSAA) | **Yes** | No | **Yes** |
| Temporal Anti-Aliasing (TAA) | **Yes** | **Yes** | No |
| Systems/Tools Features |   |   |   |
| Nanite Virtualize Geometry | No | No | No |
| Hardware Ray Tracing Features | No | No | No |
| Path Tracer | No | No | No |
| Texture Streaming | **Yes** | **Yes** | **Yes** |
| Virtual Textures: Streaming | **Yes** | **Yes** | **Yes** |
| Virtual Textures: Runtime | **Yes** | **Yes** | **Yes** |
| Mesh Distance Fields | **Yes \*** | **Yes \*** | No |
| Water System | **Yes** | **Yes** | **Yes** |
| Hair and Fur Grooms | **Yes** | **Yes** | **Yes** |
| Level of Detail (LOD) |   |   |   |
| Level of Detail (LOD) | **Yes** | **Yes** | **Yes** |
| Hierarchical Level of Detail (HLOD) | **Yes** | **Yes** | **Yes** |
| Dither Fading | **Yes** | **Yes** | **Yes** |
| Visibility and Occlusion Culling |   |   |   |
| Cull Distance Volumes | **Yes** | **Yes** | **Yes** |
| Precomputed Visibility Volumes | **Yes** | **Yes** | **Yes** |
| Hardware (GPU) Occlusion Queries | **Yes** | **Yes** | **Yes** |

### Lighting Features

| Feature | Mobile Forward (Open GL ES 3.2, Metal, Vulkan, Switch) | Mobile Deferred (Metal, Vulkan, Switch) | Mobile Forward w/ HDR Disabled (Head-mounted Mobile XR) |
| --- | --- | --- | --- |
| Atmosphere and Fog |   |   |   |
| Sky Atmosphere | **Yes** | **Yes** | **Yes** |
| Volumetric Clouds | No | No | No |
| Exponential Height Fog | **Yes** | **Yes** | **Yes** |
| Volumetric Fog | No | No | No |
| Lighting and Shadowing |   |   |   |
| Dynamic Lighting | **Yes** | **Yes** | **Yes** |
| Precomputed/Baked Lighting | **Yes** | **Yes** | **Yes** |
| Image Based Lighting | **Yes** | **Yes** | **Yes** |
| Standalone Ray Traced Shadows | No | No | No |
| Virtual Shadow Maps | No | No | No |
| Modulated Shadows | **Yes** | **Yes** | **Yes** |
| Capsule Shadows | **Yes** | **Yes** | **Yes** |
| Contact Shadows | No | No | No |
| Precomputed Translucent Shadows | No | No | No |
| Dynamic Translucency Shadows | No | No | No |
| Point Light Shadows | **Yes** | **Yes** | **Yes** |
| Global Illumination |   |   |   |
| Lumen GI and Reflections: Software Ray Tracing | No | No | No |
| Lumen GI and Reflections: Hardware Ray Tracing | No | No | No |
| Precomputed / Baked Global Illumination | **Yes** | **Yes** | **Yes** |
| Screen Space Global Illumination | No | No | No |
| Standalone Ray Traced Global Illumination (Deprecated) | No | No | No |
| Reflections |   |   |   |
| Reflection Captures (Box/Sphere) | **Yes** | **Yes** | **Yes** |
| Scene Capture Cubemap | **Yes** | **Yes** | **Yes** |
| Scene Capture 2D | **Yes** | **Yes** | **Yes** |
| Planar Reflections | **Yes** | **Yes** | **Yes** |
| Screen Space Reflections | **Yes** | **Yes** | **Yes** |
| Standalone Hardware Ray Traced Reflections (Deprecated) | No | No | No |
| High Precision Normals | No | No | No |
| Reflection Capture Resolution | **Yes** | **Yes** | **Yes** |
| HDR Cubemap | **Yes** | **Yes** | **Yes** |
| Direct Specular | **Yes** | **Yes** | **Yes** |
| GGX Specular | **Yes** | **Yes** | **Yes** |

### Light Type and Mobility Features

| Feature | Mobile Forward (Open GL ES 3.2, Metal, Vulkan, Switch) | Mobile Deferred (Metal, Vulkan, Switch) | Mobile Forward w/ HDR Disabled (Head-mounted Mobile XR) |
| --- | --- | --- | --- |
| Static Mobility - Light Type |   |   |   |
| Directional Light | 1 directional light of any type | 1 directional light of any type | 1 directional light of any type |
| Sky Light | **Yes** | **Yes** | **Yes** |
| Point Light | **Yes** | **Yes** | **Yes** |
| Spot Light | **Yes** | **Yes** | **Yes** |
| Rect Light | **Yes** | **Yes** | **Yes** |
| Static Mobility - General Features |   |   |   |
| Indirect Lighting Intensity | **Yes** | **Yes** | **Yes** |
| Lighting Channels | **Yes** | **Yes** | **Yes** |
| Light Transmission | No | No | No |
| Light Functions | No | **Yes** | No |
| Static Mobility - Directional Light Features |   |   |   |
| Source Angle | **Yes** | **Yes** | **Yes** |
| Light Shafts | **Yes** | **Yes** | No |
| Modulated Shadows | No | No | No |
| Static Mobility - Sky Light Features |   |   |   |
| SLS Captured Scene | **Yes** | **Yes** | **Yes** |
| SLS Specified Cubemap | **Yes** | **Yes** | **Yes** |
| Specified Cubemap Resolution | **Yes** | **Yes** | **Yes** |
| Static Mobility - Point/Spot/Rect Light Features |   |   |   |
| IES Texture | **Yes** | **Yes** | **Yes** |
| Rect Light - Source Texture | No | No | No |
| Stationary Mobility - Light Type |   |   |   |
| Directional Light | 1 directional light of any type | 1 directional light of any type | 1 directional light of any type |
| Sky Light | **Yes** | **Yes** | **Yes** |
| Point Light | **Yes** | **Yes** | **Yes** |
| Spot Light | **Yes** | **Yes** | **Yes** |
| Rect Light | No | No | No |
| (MOBILE) Stationary Mobility - Dynamic Shadow Casting |   |   |   |
| Directional Light | **Yes** | **Yes** | **Yes** |
| Sky Light | No | No | No |
| Point Light | No | No | No |
| Spot Light | **Yes** | **Yes** | No |
| Rect Light | No | No | No |
| Stationary Mobility - General Features |   |   |   |
| Indirect Lighting Intensity | **Yes** | **Yes** | **Yes** |
| Lighting Channels | **Yes** | **Yes** | **Yes** |
| Light Transmission | No | No | No |
| Light Function | No | **Yes** | No |
| Stationary Mobility - Directional Light Features |   |   |   |
| Source Angle | No | No | No |
| Cascade Shadow Maps | **Yes** | **Yes** | **Yes** |
| Light Shafts | **Yes** | **Yes** | **Yes** |
| Modulated Shadows | **Yes** | **Yes** | **Yes** |
| Stationary Mobility - Sky Light Features |   |   |   |
| SLS Captured Scene | **Yes** | **Yes** | **Yes** |
| SLS Specified Cubemap | **Yes** | **Yes** | **Yes** |
| Specified Cubemap Resolution | **Yes** | **Yes** | **Yes** |
| Stationary Mobility - Point/Spot/Rect Light Features |   |   |   |
| IES Texture | **Yes** | **Yes** | **Yes** |
| Rect Light - Source Texture | No | No | No |
| Movable Mobility - Light Type |   |   |   |
| Directional Light | 1 directional light of any type | 1 directional light of any type | 1 directional light of any type |
| Sky Light | **Yes** | **Yes** | **Yes** |
| Point Light | **Yes** | **Yes** | **Yes** |
| Spot Light | **Yes** | **Yes** | **Yes** |
| Rect Light | No | No | No |
| (MOBILE) Movable Mobility - Dynamic Shadow Casting |   |   |   |
| Directional Light | **Yes** | **Yes** | **Yes** |
| Sky Light | No | No | No |
| Point Light | No | No | No |
| Spot Light | **Yes** | **Yes** | **Yes** |
| Rect Light | No | No | No |
| Movable Mobility - General Features |   |   |   |
| Indirect Lighting Intensity | No | No | No |
| Lighting Channels | **Yes** | **Yes** | **Yes** |
| Light Transmission | No | No | No |
| Light Function | No | **Yes** | No |
| Movable Mobility - Directional Light Features |   |   |   |
| Source Angle | No | No | No |
| Cascade Shadow Maps | **Yes** | **Yes** | **Yes** |
| Light Shafts | **Yes** | **Yes** | **Yes** |
| Modulated Shadows | No | No | No |
| Distance Field Shadows | **Yes** | **Yes** | **Yes** |
| Movable Mobility - Sky Light Features |   |   |   |
| SLS Captured Scene | **Yes** | **Yes** | **Yes** |
| SLS Specified Cubemap | **Yes** | **Yes** | **Yes** |
| Specified Cubemap Resolution | **Yes** | **Yes** | **Yes** |
| Movable Mobility - Point/Spot/Rect Light Features |   |   |   |
| IES Texture | No | **Yes** | No |
| Rect Light - Source Texture | No | No | No |

### Material Features

| Feature | Mobile Forward (Open GL ES 3.2, Metal, Vulkan, Switch) | Mobile Deferred (Metal, Vulkan, Switch) | Mobile Forward w/ HDR Disabled (Head-mounted Mobile XR) |
| --- | --- | --- | --- |
| Material Inputs |   |   |   |
| Surface | **Yes** | **Yes** | **Yes** |
| Deferred Decal | **Yes** | **Yes** | No |
| Light Function | No | **Yes** | No |
| Volume | No | No | No |
| Post Process | **Yes** | **Yes** | No |
| User Interface | **Yes** | **Yes** | **Yes** |
| Material Blend Mode |   |   |   |
| Opaque | **Yes** | **Yes** | **Yes** |
| Masked | **Yes** | **Yes** | **Yes** |
| Translucent | **Yes** | **Yes** | **Yes** |
| Additive | **Yes** | **Yes** | **Yes** |
| Modulate | **Yes** | **Yes** | **Yes** |
| Alpha Composite (Premultiplied Alpha) | **Yes** | **Yes** | **Yes** |
| Alpha Holdout | **Yes** | **Yes** | **Yes** |
| Shading Model |   |   |   |
| Unlit | **Yes** | **Yes** | **Yes** |
| Default Lit | **Yes** | **Yes \*** | **Yes** |
| Subsurface | **Yes** | **Yes \*** | **Yes** |
| Preintegrated Skin | **Yes** | **Yes \*** | **Yes** |
| Clear Coat | **Yes** | **Yes \*** | **Yes** |
| Subsurface Profile | **Yes** | **Yes \*** | **Yes** |
| Two Sided Foliage | No | No | No |
| Hair | No | No | No |
| Cloth | No | No | No |
| Eye | No | No | No |
| Single Layer Water | **Yes** | **Yes** | **Yes** |
| Thin Translucent | No | No | No |
| From Material Expression | **Yes** | **Yes** | **Yes** |
| Material Inputs |   |   |   |
| Base Color | **Yes** | **Yes** | **Yes** |
| Metallic | **Yes** | **Yes** | **Yes** |
| Specular | **Yes** | **Yes** | **Yes** |
| Roughness | **Yes** | **Yes** | **Yes** |
| Anisotropy | No | No | No |
| Emissive Color | **Yes** | **Yes** | **Yes** |
| Opacity | **Yes** | **Yes** | **Yes** |
| Opacity Mask | **Yes** | **Yes** | **Yes** |
| Normal | **Yes** | **Yes** | **Yes** |
| Tangent | No | No | No |
| World Position Offset | **Yes** | **Yes** | **Yes** |
| Cloth | No | No | No |
| Fuzz Color | No | No | No |
| Iris mask | No | No | No |
| Iris Distance | No | No | No |
| Subsurface Color | **Yes** | **Yes** | **Yes** |
| Custom Data 0—7 | **Yes** | **Yes** | **Yes** |
| Ambient Occlusion | **Yes** | **Yes** | **Yes** |
| Refraction | **Yes** | **Yes** | No |
| Pixel Depth Offset | **Yes** | **Yes** | **Yes** |
| Shading Model | **Yes** | **Yes** | **Yes** |
| Clear Coat | **Yes** | **Yes** | **Yes** |
| Backlit (for Hair) | No | No | No |
| Decals |   |   |   |
| Decal Response (DBuffer): Color, Normal, Roughness | No | **Yes** | **Yes** |
| Decal Response (DBuffer): Color | No | **Yes** | No |
| Decal Response (DBuffer): Color, Normal | No | **Yes** | **Yes** |
| Decal Response (DBuffer): Color, Roughness | No | **Yes** | **Yes** |
| Decal Response (DBuffer): Normal | No | **Yes** | **Yes** |
| Decal Response (DBuffer): Normal, Roughness | No | **Yes** | **Yes** |
| Decal Response (DBuffer): Roughness | No | **Yes** | **Yes** |
| Mesh Decals | **Yes** | **Yes** | **Yes** |

### Textures

| Feature | Mobile Forward (Open GL ES 3.2, Metal, Vulkan, Switch) | Mobile Deferred (Metal, Vulkan, Switch) | Mobile Forward w/ HDR Disabled (Head-mounted Mobile XR) |
| --- | --- | --- | --- |
| Compression Settings |   |   |   |
| Default (DXT1/5, BC1/3 on DX11) | **Yes** | **Yes** | **Yes** |
| Normal Map (DXT 5, BC5 on DX11) | **Yes** | **Yes** | **Yes** |
| Masks (no sRGB) | **Yes** | **Yes** | **Yes** |
| Grayscale (R8, RGB8, sRGB) | **Yes** | **Yes** | **Yes** |
| Displacement Map (8/16-bit) | **Yes** | **Yes** | **Yes** |
| Vector Displacement Map (RGBA8) | **Yes** | **Yes** | **Yes** |
| HDR (RGB, no sRGB) | **Yes** | **Yes** | **Yes** |
| User Interface 2D (RGBA) | **Yes** | **Yes** | **Yes** |
| Alpha (no sRGB, BC4 on DX11) | **Yes** | **Yes** | **Yes** |
| Distance Field Font (R8) | **Yes** | **Yes** | **Yes** |
| HDR Compressed (RGB, BC6H, DX11) | No | No | No |
| BC7 (DX11, optional A) | **Yes \*** | **Yes \*** | **Yes \*** |
| Half Float (R16F) | **Yes** | **Yes** | **Yes** |

### Particle Effects

| Feature | Mobile Forward (Open GL ES 3.2, Metal, Vulkan, Switch) | Mobile Deferred (Metal, Vulkan, Switch) | Mobile Forward w/ HDR Disabled (Head-mounted Mobile XR) |
| --- | --- | --- | --- |
| Niagara Particle System |   |   |   |
| CPU Particles | **Yes** | **Yes** | **Yes** |
| CPU Particle Collision | **Yes** | **Yes** | **Yes** |
| GPU Particles | **Yes** | **Yes** | **Yes** |
| GPU Depth Collision | No | No | No |
| Mesh Particles | **Yes** | **Yes** | **Yes** |
| Beam Emitter | **Yes** | **Yes** | **Yes** |
| Ribbon Emitter | **Yes** | **Yes** | **Yes** |
| Anim Trail | **Yes** | **Yes** | **Yes** |
| Vector Field | **Yes** | **Yes** | **Yes** |
| Particle Lights | No | **Yes** | No |
| GPU Distance Field Collision | No | No | No |
| GPU Raytracing Collision (Experimental) | No | No | No |
| Fluid Simulation | No | No | No |