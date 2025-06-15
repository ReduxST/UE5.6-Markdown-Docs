# Forward Shading Renderer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/forward-shading-renderer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/forward-shading-renderer-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:13

---

By default, Unreal Engine uses a Deferred Renderer as it provides the most versatility and grants access to more rendering features. However, there are some trade-offs in using the Deferred Renderer that might not be right for all VR experiences. **Forward Rendering** provides a faster baseline, with faster rendering passes, which may lead to better performance on VR platforms. Not only is Forward Rendering faster, it also provides better anti-aliasing options than the Deferred Renderer, which may lead to better visuals.

## Enabling Forward Shading

To enable the Forward Shading Renderer:

1.  In the **Edit** menu, open the **Project Settings**.
    
2.  Select the **Rendering** tab on the left and locate the **Forward Shading** category.
    
3.  Enable **Forward Shading**.
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eab4247a-87d1-411a-b12e-feea4a4924f7/enableforwardshading.png)

You will be prompted to restart the editor where after the restart, you can begin using the Forward Renderer options and features.

## Enabling Multisample Anti-Aliasing

To use Multisample Anti-Aliasing (MSAA):

1.  In the **Edit** menu, open the **Project Settings**.
    
2.  Select the **Rendering** tab on the left and locate the **Default Settings** category.
    
3.  Set the **Anti-Aliasing Method** property to **MSAA**.
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d7bf6f1-c962-4c2e-bcb7-87ca6a695781/enablemsaa.png)

The forward renderer supports both MSAA and Temporal Anti-Aliasing (TAA) and in most cases, TAA is preferable because it removes both geometric aliasing and specular aliasing. In VR however, the constant sub-pixel movement introduced by head tracking generates unwanted blurriness, making MSAA a better choice. Projects that choose to use MSAA will want to build content to mitigate specular aliasing. Additionally, the **Normal to Roughness** feature can help reduce specular aliasing from detailed normal maps and automatic LOD generation for static meshes can flatten features on distant meshes to help reduce aliasing from small triangles.

In our tests, using MSAA instead of TAA increases GPU frame time by about 25% (actual cost will depend on your content).

Below an example is given with Temporal AA enabled versus 4X MSAA enabled.

![With Temporal AA](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84368f4e-2515-42ce-8105-2ef1a4126a75/temporalaa.png)

![With 4X MSAA](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c417b2c-074e-411a-9de4-cbfcfcb7de54/msaa.png)

You can use the console variable `r.MSAACount` to control how many MSAA samples are computed for every pixel. `r.MSAACount 1` disables MSAA. Assigning `r.MSAACount 0` will fall back to using Temporal AA, which allows for convenient toggling between Anti-Aliasing methods.

## Performance and Features

Switching from the Deferred Renderer to the Forward Renderer may provide you with an increase in performance for your project.

The forward renderer can be faster than the deferred renderer for some content. Most of the performance improvement comes from features that can be disabled per material. By default, only the nearest reflection capture will be applied without parallax correction unless the material opts-in to High Quality Reflections, height fog is computed per-vertex, and planar reflections are only applied to materials that enable it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8cb0e8b-611b-4048-8f59-66cc7b5fb1b8/forwardshading.png)

Leveraging these options in Epic's new VR game, Robo Recall, the forward renderer is about 22% faster than the deferred renderer on an NVIDIA 970 GTX.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b4bd7f3-ec8f-4c47-8143-44e28398c7f3/exampleimage.png)

The Forward Renderer works by culling lights and Reflection Captures to a frustum-space grid. Each pixel in the forward pass then iterates over the lights and Reflection Captures affecting it, sharing the material with them. Dynamic Shadows for Stationary Lights are computed beforehand and packed into channels of a screen-space shadow mask, leveraging the existing limit of 4 overlapping Stationary Lights.

Be sure to use Unreal Engine's profilingp tools to gauge the performance of your game when switching from the Deferred Renderer to the Forward Renderer. You will want to pay special attention to profiling GPU to see where GPU cost is going, as well as using the [Stat Commands](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine) to aid with your profiling efforts.

### Supported Features

This list comprises the currently supported features of the Forward Renderer:

-   Full support for Stationary Lights, including Dynamic Shadows from Movable objects which blend together with precomputed environment shadows
-   Multiple Reflection Captures blended together with parallax correction
-   Planar Reflections of a partial scene composited into Reflection Captures
-   DBuffer Decals
-   Precomputed Lighting and Sky Lights
-   Any number of unshadowed Movable Lights
-   Capsule Shadows
-   Alpha-to-coverage for Masked Materials
-   Instanced Stereo Compatible
-   Up to 4 overlapping Shadow Casting Movable Lights
-   Light Functions on shadow casting lights

## Known Issues & Common Questions

The following features are **not supported** while using the Forward Renderer:

-   Screen Space Techniques (SSR, SSAO, Contact Shadows)
-   Dynamically Shadowed Translucency
-   Translucency receiving environment shadows from a Stationary Light
-   MSAA on D-Buffer Decals and Motion Blur

Below are some common questions/issues that may arise when using the Forward Renderer.

-   **My Material is broken when switching to the Forward Renderer, something about GBuffer scene textures?**
    -   Access to the GBuffer is not available for texture sampling in the Forward Renderer and is only available with the Deferred Renderer.
-   **Does the Forward Renderer allow fewer texture samples than the Deferred Render?**
    -   The Forward Renderer packs all features into one shader so there are fewer texture samplers available for your material.
    -   You can usually solve this by using Shared Samplers.
-   **How come I have issues with MSAA not being able to find samples against Atmospheric Fog?**
    -   Atmospheric Fog does not handle MSAA correctly yet.
    -   For Height Fog, you can get around with Vertex Fogging (which is enabled by default when enabling Forward Shading).
    -   This means it is computed in the Forward BasePass and therefore anti-aliased correctly.
    -   Atmosphere is still computed in a Deferred Pass off of resolved scene depths so it does not anti-alias correctly (which we hope to fix in future updates).