# Rendering and Shading Modes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mobile-rendering-and-shading-modes-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mobile-rendering-and-shading-modes-for-unreal-engine)  
**Processed:** 2025-06-14 16:36:29

---

UE provides both **forward** and **deferred** shading modes tailored for use on mobile devices, as well as experimental support for the **desktop renderer**. Each shading mode has different trade-offs for both performance and fidelity. This page provides an overview of the forward and desktop shading modes for Mobile, while the desktop renderer is covered in a [separate guide](/documentation/en-us/unreal-engine/using-the-desktop-renderer-on-mobile-in-unreal-engine).

## How to Set Your Shading Mode

You can set which mobile shading model you want to use in your `Engine.ini` file with the CVar `r.Mobile.ShadingPath`. The values you can use are as follows:

| **Value** | **Shading Mode** | **Description** |
| --- | --- | --- |
| 0 | Mobile Forward Shading | Processes lighting and shadows at runtime. Preferred for projects that use precomputed lighting. |
| 1 | Mobile Deferred Shading | Processes lighting and shadows |

Alternatively, you can use the desktop renderer on high-end mobile devices, but bear in mind that this comes with significant performance costs. For more information about it, see the [Desktop Renderer for Mobile](/documentation/en-us/unreal-engine/using-the-desktop-renderer-on-mobile-in-unreal-engine).

See the sections below for more detailed information about these rendering modes.

## Which Shading Mode Should I Use?

![Reflections with mobile forward (old)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c12c6cc9-df4f-4fcc-8fd4-732eae76e483/mobilerenderingold.png)

![Reflections with mobile deferred (new)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f0d1df0-4dc2-4b57-829b-52925d7ca13d/mobilerenderingnew.png)

Most devices that Unreal Engine supports will fulfill the hardware requirements for using Mobile Deferred shading, and it usually provides superior performance due to decreased material complexity, as well as superior lighting features.

For projects that use precomputed lighting, we strongly recommend using Mobile Forward shading.

## Mobile Forward Shading

**Forward shading** processes material interactions with lights and shadows at draw time, and it is the default shading mode for Mobile.

### Benefits

-   Fastest baseline performance and compatibility with the largest variety of hardware.
    
-   Faster rendering with precomputed lighting.
    
-   Best variety and quality of anti-aliasing options.
    
-   Better performance when using a large number of reflection captures.
    

### Drawbacks

-   Limited support for dynamic lighting, shadows, and reflections.
    
-   Materials have to include light and shadow code alongside all other parameters.
    
    -   This increases:
        
        -   The number of instructions materials use.
            
        -   The number of samplers materials use.
            
        -   The length of compile times when compiling materials/shaders.
            
    -   This can result in more hitches and memory consumption compared with Deferred shading.
        

### When to Use Forward Shading

Forward Shading is preferable for:

-   Projects that use precomputed lighting.
    
-   Projects that use local lights or a large number of reflection captures.
    
-   Projects targeting devices that do not use tile-based GPUs.
    

## Mobile Deferred Shading

**Deferred shading** processes geometry and lighting/shading as separate passes instead of handling both of them at runtime. This provides support for high-quality reflections, multiple dynamic lights, lit decals, and other advanced lighting features that are not normally available in the default forward rendering mode for Mobile. See [Mobile Deferred Shading](/documentation/en-us/unreal-engine/using-the-mobile-deferred-shading-mode-in-unreal-engine) for more details about both its fidelity and performance improvements.

### Benefits

-   Better performance on Mobile devices that use tile-based GPUs.
    
-   Better performance and memory use on projects using complex lighting.
    
-   Advanced lighting features not offered by forward shading.
    

### Drawbacks

-   Requires relatively higher-end Mobile hardware.
    
-   Only provides DefaultLit and Unlit shading models for precomputed lighting.
    
-   More limited anti-aliasing options.
    

### When to Use Deferred Shading

Deferred Shading is preferable for:

-   Projects that use dynamic lighting.
    
-   Projects with extensive outdoor environments.
    

### Lighting Features

The Mobile Deferred shading mode provides the following lighting features:

-   Light Functions
    
-   Light Profiles
    
-   IES Light Profiles
    
-   Lit Decals
    
-   Increased local light rendering efficiency.
    

For more details, see [Mobile Deferred Shading](/documentation/en-us/unreal-engine/using-the-mobile-deferred-shading-mode-in-unreal-engine).

### Rendering Limitations

-   **Pre-computed lighting and shading model limitations:** If your project uses precomputed lighting, deferred shading only provides DefaultLit and Unlit shading models. If your project uses precomputed lighting, we strongly advise that you use forward shading instead of deferred shading.
    
-   **Translucency Passes:** Translucency is available in Deferred Shading mode, but translucency passes always use Forward shading. Make sure translucent materials such as glass or water have their **Lighting Mode** set to **Surface ForwardShading**.
    
-   **Multi-Sample Anti-Aliasing (MSAA)**: Deferred rendering can not support MSAA due to the amount of space it would need in GBuffer. It would also have a more resource-intensive shading pass due to the need to shade each sample rather than each pixel.
    
-   **Lit Decal Limitations:** Lit decals are not supported with static lighting in Deferred mode, as it would require an additional buffer for decals. This is not feasible on Mobile devices ude to memory constraints. However, **emissive** decals work fine with static lighting.
    
-   **Other Decal Limitations:** Because of space limitations in GBuffer, decals use octahedron encoding for normals to reduce their size. This encoding makes it impossible to blend or modify normals in GBuffer. However, you can fully overwrite them instead.
    
-   **Shading Model Limitations:** Supporting multiple shading models at the same time is very expensive with Mobile Deferred shading. Therefore, you should limit your use of complex shading models only to objects that need them.
    

### Tile Memory Usage

Each mobile platform has different ways to perform shading in tile memory.

-   **iOS** uses a functionality similar to `framebuffer_fetch` to access GBuffer on tile memory.
    
-   **Android Vulkan** uses Vulkan's sub-passes.
    
-   **Android GLES** requires extensions, and there is no universal method for all GPUs.
    
-   **Mali** and **PowerVR** use PLS extensions.
    
-   **Adreno** GPUs use the `framebuffer_fetch` extension.
    

Other GPUs use an immediate-mode renderer, so these tile memory techniques do not apply. In these cases, GBuffer is allocated as a regular texture in system memory and may not provide memory benefits.

### Hardware Limitations

Most of the mobile hardware that UE supports meets the requirements for using the Mobile Deferred shading model. However, Mali devices running Android Vulkan have strict limitations on color and input attachments:

-   16 bytes or 128-bit per-pixel in GBuffer.
    
-   Can only use up to 4 input attachments.
    
-   Can only fetch up to 3 color attachments and 1 depth attachment during the lighting pass.
    

The Mobile Deferred shading mode adopts these limitations by default to ensure consistency across all devices. To remove these limitations, set the `MobileUsesExtendedGBuffer` parameter in your `Engine.ini` file to `true`. The Mobile Deferred shading mode will then expand GBuffer to use the full capabilities of the user's device.