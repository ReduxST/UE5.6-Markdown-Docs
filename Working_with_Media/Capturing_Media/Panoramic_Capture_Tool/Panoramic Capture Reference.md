# Panoramic Capture Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/panoramic-capture-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/panoramic-capture-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:41:40

---

Epic Games no longer supports or maintains the Panoramic Capture Plugin, and it only exists as a reference if you want to create your own solution. The plugin may not work as-is.

## Message Log

All log information is now shown under the **Panoramic Capture Log** in the **Message Log**. If an error occurs, the **Message Log** will open automatically.

![Message Log](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/698299e6-a376-4434-9d7d-daa1faed5edb/01-message-log.png "Message Log")

## Plugin Content

![Plugin Content](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c4174e7-4445-41c5-b7cf-e283e14c299a/02-plugin-content.png "Plugin Content")

-   **Assets**: Contains one Blueprint that sets all of the parameters for a quality 6k capture.
-   **Materials**: Contains the post processes used to capture the different render passes.
-   **Viewer**: Contains Blueprints to view stereoscopic stills and videos.

The **Content Drawer** does not show plugin content by default. Select **Settings**, then enable **Show Engine Content** and **Show Plugin Content** to show plugin content.

## BP\_Capture

Under **PanoramicCapture Content > Assets**, you will find **BP\_Capture**. This Blueprint sets up all of the necessary parameters for a quality 6k capture. If you use the Blueprint in its default configuration, it will output one frame of stereoscopic output.

![BP_Capture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35755519-5208-4381-a81b-fef6da1e1bbb/03-bp-capture-blueprint.png "BP_Capture")

The output path is configurable, but defaults to **C:\\PanoramicCaptureFrames**. Below is an example of the output directory when you output all passes.

![BP_CaptureFolder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d368fdfa-128e-42e6-9155-2adb28423cef/04-output-directory.png "BP_CaptureFolder")

In the following sections, you will find a detailed description of options and controls available for the Panoramic Capture plugin and what those options do to the image that is output. The options have been broken up into groups based on what those options do. To input a command, press the backtick or tilde key (**\`**) to open up the UE5 console and then type **SP.** followed by the command you want to enter.

If you want to know more about any of the settings below, check out the **StereoPanoramaManager.cpp** file for more information.

## Render Passes

-   Ambient Occlusion
-   Base Color
-   Metallic
-   Roughness
-   Scene Depth (always 32bit)
-   World Normals

## Slice Controls

The Slice Control options are for controlling how many horizontal or vertical slices are taken for each image.

| Property | Default Value | Description |
| --- | --- | --- |
| **SP.HorizontalAngularIncrement** | 1.0f | The number of degrees per horizontal step. Must be a factor of 360. |
| **SP.VerticalAngularIncrement** | 90.0f | The number of degrees per vertical step. Must be a factor of 180. |
| **SP.CaptureHorizontalFOV** | 90.0f | Horizontal FOV for scene capture component. Must be larger than SP.HorizontalAngularIncrement. |
| **SP.EyeSeparation** | 6.4f | The separation of the stereo cameras. |

## Atlas Controls

The Atlas Controls actually control the atlas of shots collected from the slices, which are used to reconstruct the 360-degree image.

  

| Property | Default Value | Description |
| --- | --- | --- |
| **SP.StepCaptureWidth** | 4096 | The final spherical atlas width. |
| **SP.ForceAlpha** | false | Force the alpha value to completely opaque. |

## Sampling Controls

The Sampling Control options affect how the image is filtered.

| Property | Default Value | Description |
| --- | --- | --- |
| **SP.CaptureSlicePixelWidth** | 2048 | Capture Slice Pixel Dimension. |
| **SP.EnableBilerp** | true | 0 - No Filtering 1- Bilinear Filter slice samples. |
| **SP.SuperSamplingMethod** | 1 | 0 - No Supersampling, 1 - Rotated Grid SS. |

## Debug Controls

The Debug Control options allow you to see and adjust how the images are captured allowing you to easily track down any issues you might run into with the final output image.

| Property | Default Value | Description |
| --- | --- | --- |
| **SP.ConcurrentCaptures** | 30 | The number of scene captures to capture concurrently. Raising or lowering the value of **SP.ConcurrentCaptures** can greatly affect capture times. If you set this value too low, you will not be capturing the optimal number of scene captures for parallel processing. If you set this value too high, you will overwhelm the GPU. |
| **SP.GenerateDebugImages** | 0 | 0 - No Debug Images. 1 - Save out each strip as it is generated. 2 - Save each entire slice. |
| **SP.OutputDir** | This will default to your project saved folder | The location where your images will be saved. |
| **SP.ShouldOverrideInitialYaw** | true | Override Initial Camera Yaw. Set to true if you don't want to use PlayerController View-Dir. |
| **SP.ForcedInitialYaw** | 90.0f | Yaw value for initial Camera view direction. Set ShouldOverrideInitialYaw to true to use this value. |
| **SP.FadeStereoToZeroAtSides** | true | Fade stereo effect between left/right eye to zero at 90 degrees. |

Please note that raising or lowering the value of **SP.ConcurrentCaptures** can greatly affect capture times. Set this too low and you will not be using the optimal number for parallel processing. Set this too high and you will overwhelm the GPU.

## Output

Use these values to control bit depth and different render passes.

  

| Property | Default Value | Optional Value | Description |
| --- | --- | --- | --- |
| **SP.OutputBitDepth** | 8 | 32 | Sets the output bit depth. Panoramic Capture supports 8-bit(.png) and 32-bit (.exr) formats. |
| **SP.OutputFinalColor** | 0 | 1 | Enables the Final Color render pass. |
| **SP.OutputBaseColor** | 0 | 1 | Enables the Base Color render pass. |
| **SP.OutputSceneDepth** | 0 | 1 | Enables the Scene Depth render pass. Scene Depth is always 32-bit. |
| **SP.OutputWorldNormal** | 0 | 1 | Enables the Final Color render pass. |
| **SP.OutputAmbientOcclusion** | 0 | 1 | Enables the Ambient Occlusion render pass. |
| **SP.OutputMetallic** | 0 | 1 | Enables the Metallic render pass. |

## Monoscopic

This value enables you to specify whether the output should be monoscopic or stereoscopic. Stereoscopic output is the default behavior.

  

| Property | Default Value | Optional Value | Description |
| --- | --- | --- | --- |
| **SP.Monoscopic** | 0 | 1 | Use this value to specify the output as monoscopic. The default output is stereoscopic. |