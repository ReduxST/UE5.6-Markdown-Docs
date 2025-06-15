# XR Performance Features

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/xr-performance-features-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/xr-performance-features-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:26

---

Due to the demanding rendering requirements XR requires a number of performance optimizations and new rendering modes that are specific to XR have been introduced to Unreal Engine (UE). In the following document we will take a look at these features and how to use them in your UE XR projects.

## Variable Rate Shading and Fixed Foveated Rendering

**Variable Rate Shading (VRS)** is a feature supported on newer GPUs that provides various methods for adjusting the shading rate of pixels in a render target (or targets). The default shading rate in any setup is 1:1, where 1 pixel-shader invocation applies to 1 target pixel on the screen. With VRS, you can specify alternate shading rates, specifically 1x2, 2x1, 2x2, 2x4, 4x2, and 4x4. For example, for 2x2 shading rate, you would see a single pixel shader invocation for a group of 2x2 pixels (4 pixels), and for 4x4 you'd see a single pixel-shader invocation for a 4x4 group (16 pixels).

Shading rate can be applied either on a per-material basis, or via a shading rate image attachment (via Tier 2 VRS).

**Fixed Foveated Rendering** is a technique which can make use of image-based VRS in VR headsets to adjust the shading rate for a target, reducing the shading rate towards the periphery of the view. Due to optical distortion, the GPU ends up throwing away increasing amounts of pixel detail towards the edge of the image, so by applying a VRS image that reduces shading rate further out from the image center, you can improve performance with little perceptual degradation in image quality.

Fixed-foveation uses an attachment generated via compute shader:

[![](https://dev.epicgames.com/community/api/documentation/image/cd1a8482-4f04-4eaa-8b98-6c292bc4608e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cd1a8482-4f04-4eaa-8b98-6c292bc4608e?resizing_type=fit)

The center (black) areas on both sides correspond to the center of each stereo view; darker areas are higher shading rate, with black being full (1x1, 1 pixel-shader invocation per pixel), dark red at half-rate in both x and y (2x2, 1 pixel shader invocation per 4 pixels), and lighter red quarter rate (4x4, 1 pixel shader invocation per 16 pixels).

Initial results with VRS attachments applied to the base pass and transparency passes show significant promise. Currently this is still proof of concept, and it could be applied elsewhere other than base and transparency passes.

### Project Settings

To access VRS settings, from the main menu, go to **Edit > Project Settings**. Then, in the **Project Settings** window, go to **Engine > Rendering > VR**.

[![](https://dev.epicgames.com/community/api/documentation/image/377e4b91-84cd-42de-8c0d-53c9084c58d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/377e4b91-84cd-42de-8c0d-53c9084c58d5?resizing_type=fit)

### Console Variables

You can use the following console variables:

| Variable | Description |
| --- | --- |
| 
r.vrs.Enable

 | 

Enable or disable VRS across the engine (material-based VRS and any active image-based VRS).

 |
| 

r.VRS.EnableImage

 | 

Enable or disable image-based VRS only. Per-material VRS will still function if it is enabled and supported.

 |
| 

vr.VRS.HMDFixedFoveationLevel

 | 

HMD fixed foveated rendering quality and performance setting.

 |
| 

vr.VRS.HMDFixedFoveationDynamic

 | 

Enable or disable whether fixed-foveation level should adjust based on GPU utilization.

 |

### Known Limitations

-   Only available on Windows devices with DirectX 12 and VRS Tier 2 support, Windows devices with Vulkan and VK\_KHR\_fragment\_shading\_rate extension support, and Oculus Quest.
    
-   Not compatible with NVIDIA's DLSS.
    
-   Eye-tracked foveated rendering is currently not supported.
    

## Instanced Stereo

Instanced Stereo Rendering lessens the performance impact of XR in UE. Enable this feature by navigating to **Project Settings > Engine > Rendering > Instanced Stereo**, then check the **Instanced Stereo** option.

[![Instanced Stereo enabled in VR settings](https://dev.epicgames.com/community/api/documentation/image/ae519591-f653-4e12-a705-ce76f0536bef?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ae519591-f653-4e12-a705-ce76f0536bef?resizing_type=fit)

Click for full image.

After **Instanced Stereo** rendering has been enabled, it will require an enginpe restart, and shader recompile. The base pass, and early-z pass, works with static meshes, skeletal meshes, srite particles, and mesh particles with the feature turned on (both serial and parallel rendering paths). **Instanced Stereo** currently works on PC (DirectX) and PS4 with support for other platforms coming after the initial 4.11 release. Here is a video showing Standard Stereo Rendering in VR, versus Instanced Stereo Rendering in VR.

## Multiview Support for Mobile

Certain (supported) mobile devices can now support VR Multiview. Mobile Multiview is similar to Instanced Stereo rendering that is available to desktop PC's, and works by providing an optimized path for Stereo Rendering on the mobile device's CPU. To enable this feature, you will need to do the following:

1.  From the Main Toolbar, go to **Edit** > **Projects Settings**, to open the Editor's Project Settings.
    
2.  Then, go to **Engine** > **Rendering** > **VR**, and look for the **Mobile Multi-View** option.
    
3.  Enable the Mobile Multi-View option, and restart Unreal Engine for the changes to take effect.
    
    [![Enable mobile multi-view in the VR settings](https://dev.epicgames.com/community/api/documentation/image/c8e4e2d6-c1c9-4277-90ef-9a0ca8f4372b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c8e4e2d6-c1c9-4277-90ef-9a0ca8f4372b?resizing_type=fit)
    

-   Mobile Multiview only works with modern Mali-based GPU's.
    
-   This feature is diabled at runtime if you package this project but do not have a compatible GPU.
    

## Forward Rendering

[![](https://dev.epicgames.com/community/api/documentation/image/93e5db2d-03d3-4c12-a0fc-c426f951c1bf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/93e5db2d-03d3-4c12-a0fc-c426f951c1bf?resizing_type=fit)

Please see the [Forward Shading Renderer](https://dev.epicgames.com/documentation/en-us/unreal-engine/forward-shading-renderer-in-unreal-engine) documentation for more information on this feature.

## Performance Profiling

To track down assets that are too expensive for VR, you need to profile what your project is doing on the CPU and GPU as much as possible over the lifetime of your project.

-   **GPU Profiling** - To activate the GPU profiler, all you need to do is press **CTRL + SHIFT + ,(Comma Key)** together, while running your project. After the keys have been pressed, you will see a new window come up that should look similar to the image below.
    
    [![GPU Visualizer](https://dev.epicgames.com/community/api/documentation/image/1a48df28-d4fe-452b-8d6c-95eda2b4bf8c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1a48df28-d4fe-452b-8d6c-95eda2b4bf8c?resizing_type=fit)
    
-   **CPU Profiler** - Profiling what your project is doing on the CPU is a bit more involved than profiling for the GPU. To find out more on how to do this, please refer to the Performance Profiler documents.
    

## Post Process Settings

Due to the demanding rendering requirements of VR, many of the advanced Post Processing features that are enabled by default should be disabled, or your project could suffer from performance problems. To accomplish this in your project, you will need to do the following.

1\. Add a Post Process(PP) volume to your level if there is not one already there. 1. Select the PP volume, and in the **Post Process Volume** section, enable the **Infinite Extent (Unbound)** option so that the settings in the PP volume will be applied to the entire level.

!\[Enable unbound option for the post process volume(enable-unbound-post-process-volume.png)

1\. Expand the **Settings** of the **Post Process Volume**, and then go through each section to disable any active PP settings by enabling that property; clicking on it, and then setting the value from the default (usually 1.0) to **0**, thus disabling the feature.

[![Lens flare intensity is enabled and set to zero](https://dev.epicgames.com/community/api/documentation/image/2a78f7d7-f5f1-4674-99db-1d37c3894add?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2a78f7d7-f5f1-4674-99db-1d37c3894add?resizing_type=fit)

When doing this, you won't need to hit every section and set all of the properties to 0. Instead, first disable the really heavy hitting features like Lens Flares, Screen Space reflections, Temporal AA, SSAO, Bloom and anything else that might have an impact on performance.