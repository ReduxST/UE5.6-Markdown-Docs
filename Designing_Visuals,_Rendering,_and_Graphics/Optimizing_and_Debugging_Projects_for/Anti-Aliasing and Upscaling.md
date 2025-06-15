# Anti-Aliasing and Upscaling

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/anti-aliasing-and-upscaling-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/anti-aliasing-and-upscaling-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:44

---

**Anti-Aliasing** is the process of removing jagged, or stair-stepped, lines on edges and objects that should otherwise be smooth. There are different methods of anti-aliasing used to reduce these types of visual artifacts. Some are developed for use with specific renderers and platforms, while others are ideal for improving performance and fidelity.

![No anti-aliasing applied to the scene.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ad00fcd-f7c3-45e9-ae48-a0b73f164508/1-no-aa.png)

![With anti-aliasing applied to the scene.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f20cbb48-4966-49c4-9676-d9110e0ff005/2-with-aa.png)

## Anti-Aliasing Methods

Many different methods of anti-aliasing have been developed. Unreal Engine provides several methods to choose from depending on the needs and requirements of your project. You can choose between anti-aliasing methods for desktop / console and mobile platforms.

Unreal Engine provides the following methods of anti-aliasing for your projects.

| Anti-Aliasing Method | Desktop / Console: Deferred Renderer | Desktop / Console: Forward Renderer | Mobile: Deferred Renderer | Mobile: Forward Renderer |
| --- | --- | --- | --- | --- |
| [Temporal Super Resolution (TSR)](/documentation/en-us/unreal-engine/anti-aliasing-and-upscaling-in-unreal-engine#temporalsuperresolution) | Y | Y | N | N |
| [Temporal Anti-Aliasing Upsampling (TAAU)](/documentation/en-us/unreal-engine/anti-aliasing-and-upscaling-in-unreal-engine#temporalantialiasingupsampling) | Y | Y | Y | N |
| [Fast Approximate Anti-Aliasing (FXAA)](/documentation/en-us/unreal-engine/anti-aliasing-and-upscaling-in-unreal-engine#fastapproximateantialiasing) | Y | Y | Y | N |
| [Multi-Sample Anti-Aliasing (MSAA)](/documentation/en-us/unreal-engine/anti-aliasing-and-upscaling-in-unreal-engine#multisampleantialiasing) | N | Y | N | Y |

Use the image slider below to switch between no anti-aliasing and the available anti-aliasing methods to compare their result. These are single frame captures that show a static scene. To see the clearest results of anti-aliasing, you should test in a scene where you have different types of assets and materials and where you can freely move around.

IMAGE SEQUENCE NO AA, TSR, TAA, FAA, MSAA

    ![Without any Anti-Aliasing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0ca1b23-d9b1-43ad-aa77-2fe3441d980b/3-no-aa.png) ![Temporal Super Resolution | Deferred Renderer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adec40c5-df65-46c0-9d5c-f787a75b9381/3-tsr.png) ![Temporal Anti-Aliasing Upsampling | Deferred Renderer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1841ab8a-a791-43ad-8240-331c454dfa48/3-taau.png) ![Fast Approximate Anti-Aliasing | Deferred Renderer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/141f1d78-0a08-4119-affe-a2da9bde682d/3-fxaa.png) ![Multi-Sample Anti-Aliasing | Forward Renderer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5df64c5d-614d-46bb-8145-741fe64f18c6/3-msaa.png)

**Drag the slider to see the scene when using no anti-aliasing, TSR, TAA, FAA, or MSAA (Forward Renderer).**

## Anti-Aliasing Scalability Settings

Anti-aliasing settings have their own scalability group in the **Engine Scalability Settings** to scale GPU costs directly related to the anti-aliasing quality for each of the methods. The scalability group controls the console variables for each of the respective anti-aliasing methods.

You can access the **Anti-Aliasing** scalability settings from the **Settings** dropdown menu under **Engine Scalability Settings**.

![Opening the Engine Scalability Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d098b4b-0327-45af-9e13-664aa9dd1f4f/4-engine-scalability-settings.png)

You can control the quality by choosing an option between **Low**to **Cinematic**, or use **Auto** if you want the editor to test your system and choose the best options. Alternatively, you can adjust the quality of specific features, such as anti-aliasing or shadows.

![Engine Scalability Settings Quality Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6990ceb-b350-49d9-a51e-0fedb858795f/5-engine-scalability-quality-options.png)

Each of the Engine Scalability Settings entries corresponds to a set of configurable console variables found in the **DefaultScalability.ini** file. You can edit these to better fit your project based on the quality settings you want.

Refer to Scalability Settings for more information on setting up and configuring console variables. This is an advanced workflow.

## Choose an Anti-Aliasing Method

Open the **Project Settings** from the main menu under **Window**. In the Project Settings, anti-aliasing settings are found in the **Engine > Rendering** settings.

For **Desktop / Console** platforms, anti-aliasing settings are located under the **Default Settings** section.

![Rendering Project Settings Anti-Aliasing settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c185b33a-1ef6-4ee8-af10-1de539e814ce/6-project-settings-aa-options.png)

For **Mobile** platforms, anti-aliasing settings are located under the **Mobile** section.

![Rendering Project Settings Mobile Anti-Aliasing Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d964bef3-8b98-454e-b48e-dac246b665f7/6-project-settings-mobile-aa-options.png)

## Temporal Super Resolution

**Temporal Super Resolution** (or TSR) is a platform-agnostic temporal upscaler using an algorithm that focuses primarily on investing more GPU cycles of a frame into temporal upscaling quality to save total GPU frame cost. It does this by rendering a significantly lower internal resolution than what Temporal Anti-Aliasing Upsampling in Unreal Engine 4 could do.

TSR provides a native high-quality upsampling technique that meets the demand of next-generation games through the amount of detail and fidelity possible with [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) micropolygon geometry.

The comparison below demonstrates the quality and performance difference of captured frames rendered at native 4K resolution with 1080p resolution upscale to 4K. TSR makes it possible to achieve image quality near 4K resolution while also reducing GPU frame time by half.

![4k frames rendered at native 4K resolution | Frame time: 57.50ms](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/947bf0da-eaff-4d6f-82a0-933a16327159/7-tsr-1.png)

![4k frames rendered at 1080p resolution (r.ScreenPercentage=50) | Frame Time 33.37ms](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9d3b051-62c0-4bbe-ad13-bf5e8f8367b4/7-tsr-2.png)

Each of the images in the comparison above are 4K images that are limited to the width of this page. To see their fully uncompressed resolution, right-click on either and save them to your computer, or open them in a new browser window.

Temporal Super Resolution has the following properties:

-   Rendered frames approach the quality of native 4K with input resolutions as low as 1080p.
-   Less "ghosting" artifacts against high-frequency backgrounds than were visible with Unreal Engine 4's default Temporal Anti-Aliasing method.
-   Reduced flickering on geometry with high complexity.
-   Supports [Dynamic Resolution](/documentation/en-us/unreal-engine/dynamic-resolution-in-unreal-engine) scaling on console platforms.
-   Runs on any hardware that supports D3D11, D3D12, Vulkan, Metal, PlayStation 5, and Xbox Series S | X.
-   Shaders are optimized specifically for PlayStation 5 and Xbox Series S | X GPU architectures.

For more information, see [Temporal Super Resolution](/documentation/en-us/unreal-engine/temporal-super-resolution-in-unreal-engine).

## Temporal Anti-Aliasing Upsampling

**Temporal Anti-Aliasing Upsampling** (or TAAU) samples different locations within each frame and uses past frames to blend samples together to remove and smooth jagged edges.

![Without any anti-aliasing.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6de6db11-3f4b-4bea-8bd5-dbcde538fcb3/12-no-aa.png)

![With Temporal Anti-Aliasing Upsampling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ef0c327-5662-420f-b2d9-aa3b047988f6/12-with-taau.png)

The quality of TAAU is controlled using the console variable `r.TemporalAA.Quality`. You can choose from the following values:

-   **0:** Disables input filtering.
-   **1:** Enables input filtering.
-   **2:** Enables input filtering with mobility-based anti-ghosting (default)

You can use the **Engine Scalability Settings** to change the quality of anti-aliasing.

In the rendering chain, TAAU uses the Temporal Upscaler configuration with Screen Percentage by default.

![Temporal Anti-Aliasing Upsampling with Primary Screen Percentage less than 100%. ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55212d97-a825-4c0a-b358-fac0018a340a/13-pipeline-taau.png)

### Disabling Temporal Upsampling

To simplify the process of migrating projects from Unreal Engine 4 to Unreal Engine 5, Temporal Upsampling can be disabled to use the Spatial Upscaler for primary Screen Percentage.

To do so, in the UE5 Project Settings under **Engine > Rendering > Default Settings**, disable the **Temporal Upsampling** setting.

![Rendering Project Settings Temporal Upsampling checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0efd5689-532d-4968-afae-1447802b68f3/14-project-settings-temporal-upsampling-checkbox.png)

When disabling the setting, the rendering chain for Temporal Anti-Aliasing will look like this:

![Spatial and Temporal Upsample with primary screen percentage less than 100%](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15728c58-d0bb-4f51-a68e-1a79ca8a0604/14-pipeline-taa.png)

### TAAU-Specific Shader Permutations for Screen Percentage

TAAU includes its own shader permutation for primary Screen Percentage ranges:

-   **50 - 70** renders faster because it uses a smaller LDS tile in memory.
-   **71 - 100** is useful for "normal" DPI rendering on desktop and base consoles.

You can set the primary **Screen Percentage** in the Level Editor **Viewport Options** dropdown menu.

![Level viewport Options setting the Primary Screen Percentage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/324f46db-488d-4ce4-a290-fca836be6dfe/15-setting-primary-screen-percentage.png)

## Fast Approximate Anti-Aliasing

**Fast Approximate Anti-Aliasing** (or FXAA) is a spatial-only anti-aliasing technique that is a post-processing effect that uses a high contrast filter to find edges and smooth them by blending (dithering) between the pixel edges. As the name suggests for this technique, it is fast to render and well-suited for low-end devices and desktops.

While this technique is fast to render, the final image can lose fidelity when compared to other anti-aliasing techniques.

![Without Anti-Aliasing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94b16772-346b-4879-82df-b4af613bb7da/16-no-aa.png)

![With Fast Approximate Anti-Aliasing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/056d6c9b-883c-4733-a793-6d8d32098cf3/16-with-fxaa.png)

The dithering quality of FXAA is controlled using the console variable `r.FXAA.Quality`. You can set how many samples are used for dithering to remove jagged edges. More samples equals higher fidelity but at increased GPU cost.

Choose from the following:

-   **0:** Console
-   **1:** PC Medium dithering using 3 samples
-   **2:** PC Medium dithering using 5 samples
-   **3:** PC Medium dithering using 8 samples
-   **4:** PC Low dithering using 12 samples (Default)
-   **5:** PC Extreme dithering using 12 samples.

You can also use the **Engine Scalability Settings** to change the quality of anti-aliasing.

In the spatial and temporal upsampling chain, the Spatial Upscaler happens at the end of the post processing chain for the primary Screen Percentage.

![Spatial and Temporal Upsample with primary screen percentage less than 100% for FXAA](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fbeaa10-1005-471c-ad4f-87fd92238f97/16-pipeline-fxaa.png)

## Multi-Sample Anti-Aliasing

This anti-aliasing technique is only available on Mobile and Desktop / Console when using the [Forward Renderer](/documentation/en-us/unreal-engine/forward-shading-renderer-in-unreal-engine).

**Multi-Sample Anti-Aliasing** (or MSAA) is a technique that only smooths parts of the frame. MSAA primarily looks at areas that are issue-prone, like the edges of geometry. Where aliasing problems can occur on edges, MSAA manipulates their color to be between the color of the two pixels that make up the edge. The dithering effect gives the illusion of smoother edges.

![Without Anti-Aliasing | Forward Renderer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e688f57-d41a-410e-8c36-83242c830f7c/17-no-aa.png)

![With Multi-Sampling Anti-Aliasing | Forward Renderer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6349ab8c-97f1-40de-b0c6-04e3dcf96396/17-with-msaa.png)

The quality of MSAA is dependent on the number of samples it uses to blend colors along edges that it determines to have aliasing. More samples equal better visual quality, but at the cost of higher GPU processing.

You can set the number of samples MSAA uses in the Project Settings under the **Engine > Rendering > Default Settings** with the **MSAA Sample Count** setting. This setting controls the sample count for desktop / console and mobile. Alternatively, you can use the console variable `r.MSAA.Quality` to set the quality.

![Rendering Project Setting Multi-Sample Anti-Aliasing options.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16b7d670-c965-4ea4-964d-a334bc8ebb5d/17-project-settings-msaa-options.png)

Choose between **2**, **4**, and **8** samples.

   ![MSAA disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f4b1e90-54ea-49b8-93f1-14703e0a669e/18-msaa-disabled.png) ![MSAA Sample Count: 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e078553f-87e9-444f-abad-9513ca449fde/18-msaa-2.png) ![MSAA Sample Count: 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed66a510-f51a-4812-8a3e-7b682ad68b3e/18-msaa-4.png) ![MSAA Sample Count: 8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f23f90b-785e-47ff-995a-1657f41815ee/18-msaa-8.png)

**Drag the slider to increase the number of samples that Multi-Sample Anti-Aliasing uses.**

Unlike other anti-aliasing techniques, MSAA is **not** controlled by the Engine Scalability Settings and must be set using the console variable or its project setting.

In the rendering chain, MSAA primarily resolves geometry aliasing along edges before the Spatial Upscaler. Aliasing from materials, textures, and transparent surfaces are not affected by MSAA.

![MSAA plus Spatial Upscaler with primary screen percentage less than 100%.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27c20e72-eff2-40af-87c9-b3429ba39825/18-pipeline-msaa.png)

## Temporal Upscalers

**Temporal Upscalers** use data from the current and previous frames to produce a high-quality upscaled result. Temporal upscalers all work the same with Unreal Engine, whether they are Unreal Engine 4's Temporal Anti-Aliasing Upscaling (TAAU), Unreal Engine 5's [Temporal Super Resolution](/documentation/en-us/unreal-engine/temporal-super-resolution-in-unreal-engine), or a third-party plugin such as NVIDIA's DLSS 2+ Super Resolution, AMD's FSR 2.0+, and Intel's XeSS.

For more information, see [Temporal Upscalers](/documentation/en-us/unreal-engine/temporal-upscalers-in-unreal-engine).