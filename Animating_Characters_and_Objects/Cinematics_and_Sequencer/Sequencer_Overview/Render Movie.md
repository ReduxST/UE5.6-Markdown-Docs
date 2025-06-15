# Render Movie

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/old-render-movie-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/old-render-movie-in-unreal-engine)  
**Processed:** 2025-06-14 16:39:29

---

Sequencer gives you the option to render out your cinematic in either video or image format. You can render out your scene to an AVI video format to share with others, or render out images in BMP, EXR, JPG, or PNG file formats. You can also perform Custom Render Passes to render out things like Base Color, Scene Depth, Subsurface Color and more.

When rendering out your cinematic, there are several **Render Movie Settings** that you can use to define how your content is rendered. This page covers how to access the Render Movie Settings and the options that are available to you during the process.

## Render Movie Option

To access the **Render Movie Settings** and render out your cinematic, first click the **Render Movie** option within a Sequence.

[![](https://dev.epicgames.com/community/api/documentation/image/a555609d-9c4a-4d4f-b79b-4e8c0dcb503b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a555609d-9c4a-4d4f-b79b-4e8c0dcb503b?resizing_type=fit)

This will open the **Render Movie Settings** window where you can define how your cinematic is rendered.

[![](https://dev.epicgames.com/community/api/documentation/image/89875f64-ebbc-4075-91cd-d32e7e312148?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/89875f64-ebbc-4075-91cd-d32e7e312148?resizing_type=fit)

Clicking the **Capture Movie** button will start the render process with your desired **Image Output Format**.

[![](https://dev.epicgames.com/community/api/documentation/image/f3006383-96e4-4968-a74a-72b29d754c1e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f3006383-96e4-4968-a74a-72b29d754c1e?resizing_type=fit)

You will see the **Capturing** status message in the lower-right corner of the Editor, and a **Movie Render - Preview** that will scrub through your content as it renders. When the render is complete, you will see the **Capture Finished** status message in the lower-right corner of the Editor. Click the **Open Capture Folder** option in the status message to open the file location that you define as the save location for your renders.

For a step-by-step example of rendering out a movie, see [Render Movies](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-out-cinematic-movies-in-unreal-engine).

## Capture Settings

The **Capture Settings** section is where you define the Image and Audio Output Formats, Frame Rate, Resolution, and whether to apply Burn Ins.

[![](https://dev.epicgames.com/community/api/documentation/image/7e04df30-c5eb-4efe-bedd-866d9ab78dbc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7e04df30-c5eb-4efe-bedd-866d9ab78dbc?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Image Output Format**

 | 

The type of capture protocol to use for the image data.

 |
| 

**Audio Output Format**

 | 

The type of capture protocol to use for audio data.

 |
| 

**Frame Rate**

 | 

The frame rate to perform the capture at.

 |
| 

**Resolution**

 | 

The resolution to perform the capture at.

 |
| 

**Use Burn In**

 | 

Whether to [apply Burn In](https://dev.epicgames.com/documentation/en-us/unreal-engine/applying-burn-ins-to-your-movie-in-unreal-engine) content to the capture (for example, scene data, time code, and take number).

 |
| 

**Enable Texture Streaming**

 | 

Whether Texture Streaming should be enabled while capturing.

Turning off Texture Streaming may cause much more memory to be used, but also reduces the chance of blurry textures in your captured video.



 |

### Audio Output Format

Exporting audio as part of the render process is currently experimental as it relies on the experimental Audio Mixer feature.

The **Audio Output Format** uses an experimental audio capture implementation which captures the final output from the Master Submix. This requires the new Audio Mixer (launched with the command line argument `-audiomixer`) and requires that your Sequence can be played back in real-time (when rendering is disabled). If the Sequence evaluation hitches, the audio will become desynchronized due to more time passing in real-time (platform time) than in the Sequence itself.

When electing to render out a cinematic with the experimental audio bake down feature, a separate pass will be performed to specifically capture the audio. No video will appear in the preview window while the audio is being captured.

## Video Settings

The following **Video Settings** are available when choosing to render out a Video Sequence.

[![](https://dev.epicgames.com/community/api/documentation/image/136bc9f2-fe89-4851-af51-01e2854f3019?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/136bc9f2-fe89-4851-af51-01e2854f3019?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Use Compression**

 | 

Whether to render out an uncompressed video or apply compression to reduce file size.

 |
| 

**Compression Quality**

 | 

Level of Compression to apply between 1 (worst quality, best compression) and 100 (best quality, worst compression).

 |
| 

**Video Codec**

 | 

Enables you to specify a specific video codec to use when rendering out your cinematic.

 |

## Composition Graph Options

The following options are available when performing **Custom Render Passes** as the **Image Output Format**.

[![](https://dev.epicgames.com/community/api/documentation/image/54e09eca-99c3-4b97-8083-8baa78431399?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/54e09eca-99c3-4b97-8083-8baa78431399?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Include Render Passes**

 | 

A list of render passes to include in the capture. Leave this field empty to export all available passes.

 |
| 

**Capture Frames in HDR**

 | 

Whether to capture the frames as HDR textures (\*.exr format).

 |
| 

**HDRCompression Quality**

 | 

Compression Quality for HDR Frames (0 for no compression, 1 for default compression which can be slow) when **Capture Frames in HDR** is enabled.

 |
| 

**Capture Gamut**

 | 

The color gamut to use when storing HDR captured data and **Capture Frames in HDR** is enabled.

The gamut depends on whether **HDRCompression Quality** is enabled.



 |
| 

**Post Processing Material**

 | 

Whether to use a custom [Post Processing Material](https://dev.epicgames.com/documentation/en-us/unreal-engine/post-process-materials-in-unreal-engine) for rendering.

 |
| 

**Disable Screen Percentage**

 | 

Whether to disable [Screen Percentage](https://dev.epicgames.com/documentation/en-us/unreal-engine/screen-percentage-with-temporal-upscale-in-unreal-engine) during rendering.

 |

### Including Render Passes

When rendering out Custom Render Passes, you can render out all available passes or choose which passes you want to render.

[![](https://dev.epicgames.com/community/api/documentation/image/6cc3e62a-d934-4888-bf1d-caa892886379?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6cc3e62a-d934-4888-bf1d-caa892886379?resizing_type=fit)

You can add multiple passes as part of the render, each of which will be displayed in the menu.

[![](https://dev.epicgames.com/community/api/documentation/image/2f5a90e7-e6aa-478e-9c30-b2d32e5e40cb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2f5a90e7-e6aa-478e-9c30-b2d32e5e40cb?resizing_type=fit)

Click the **minus sign** to remove any Passes you previously added.

## Image Settings

When rendering out an **Image Sequence** as the **Image Output Format**, **Image Settings** may be available.

**Image Sequence (EXR)**

[![](https://dev.epicgames.com/community/api/documentation/image/a484eb5a-5b46-4b04-809c-51f44606abeb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a484eb5a-5b46-4b04-809c-51f44606abeb?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Compressed**

 | 

Whether to write out compressed or uncompressed EXRs.

 |
| 

**Capture Gamut**

 | 

The color gamut to use when storing HDR captured data.

 |

**Image Sequence** (**JPG** or **PNG**)

[![](https://dev.epicgames.com/community/api/documentation/image/ffd9a91b-9c54-47ff-953b-7bab43d9dfae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ffd9a91b-9c54-47ff-953b-7bab43d9dfae?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Compression Quality**

 | 

Level of Compression to apply to the image, between 1 (worst quality, best compression) and 100 (best quality, worst compression).

 |

## General Settings

The following options are available under the **General** section regardless of the type of rendered output.

[![](https://dev.epicgames.com/community/api/documentation/image/06aa1819-583d-47e4-abfb-22c5d4b4096b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/06aa1819-583d-47e4-abfb-22c5d4b4096b?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Output Directory**

 | 

The directory to output the captured file in.

 |
| 

**Filename Format**

 | 

The format to use for the resulting filename. Extensions will be added automatically. Any tokens of the form {token} will be replaced with the corresponding value.

 |
| 

**Game Mode Override**

 | 

Optional Game Mode to override the map's default game mode with. This is useful if the game's normal mode displays UI elements or loading screens that you don't want captured.

 |
| 

**Overwrite Existing**

 | 

Whether to overwrite existing files.

 |
| 

**Use Relative Frame Numbers**

 | 

If frame numbers in the output files should be relative to zero, rather than the actual frame numbers in the originating animation content.

 |
| 

**Zero Pad Frame Numbers**

 | 

How much to zero-pad frame numbers on filenames (4 results in 0000 followed by the file name).

 |
| 

**Use Separate Process**

 | 

Whether to capture the movie in a separate process where a standalone version of the Editor will open to process capturing.

 |
| 

**Close Editor when Capture Starts**

 | 

When enabled, the Editor will shutdown when the capture starts.

Use **Separate Process** must be enabled for this option.



 |
| 

**Additional Command Line Arguments**

 | 

Additional command line arguments to pass to the external process when capturing.

Use **Separate Process** must be enabled for this option.



 |
| 

**Inherited Command Line Arguments**

 | 

The command line arguments that are inherited from this process.

Use **Separate Process** must be enabled for this option.



 |

### Filename Format Tokens

The following Tokens can be added to the **Filename Format** option to process your file's naming convention:

| Token | Description |
| --- | --- |
| 
**{fps}**

 | 

The captured frame rate.

 |
| 

**{frame}**

 | 

The current frame number (only relevant for image sequences).

 |
| 

**{width}**

 | 

The width of the captured frames.

 |
| 

**{height}**

 | 

The height of the captured frames.

 |
| 

**{world}**

 | 

The name of the current world.

 |
| 

**{quality}**

 | 

The image compression quality setting.

 |
| 

**{material}**

 | 

The material/render pass.

 |
| 

**{shot}**

 | 

The name of the Level Sequence Asset Shot being played.

 |
| 

**{camera}**

 | 

The name of the current Camera.

 |

## Sequence Settings

The **Sequence** section provides the following options as part of the render process.

[![](https://dev.epicgames.com/community/api/documentation/image/ee574d2b-649c-4203-95bf-21e900b7ceba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ee574d2b-649c-4203-95bf-21e900b7ceba?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Write Edit Decision List**

 | 

Whether to write Edit Decision Lists (EDLs) if the Sequence contains Shots.

See the Importing & Exporting Edit Decision Lists page for more information.



 |
| 

**Write Final Cut Pro XML**

 | 

Whether to write Final Cut Pro XML files (XMLs) if the Sequence contains Shots.

 |
| 

**Handle Frames**

 | 

The number of Frame Handles to include for each Shot. These extra frames pad each Shot and are cut into and out of by the EDL (or XML) files, which can be used in your external video editing package to adjust the cuts between Shots.

 |

## Cinematic Settings

The following settings can be used to define how your cinematic plays during capture.

[![](https://dev.epicgames.com/community/api/documentation/image/8f8339d7-5900-4b4c-925c-165642889d25?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8f8339d7-5900-4b4c-925c-165642889d25?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Cinematic Engine Scalability**

 | 

Whether to enable the Cinematic Engine Scalability Settings.

 |
| 

**Cinematic Mode**

 | 

Whether to enable Cinematic Mode while capturing.

 |
| 

**Allow Movement**

 | 

Whether to allow Player movement while capturing.

Requires **Cinematic Mode** to be enabled.



 |
| 

**Allow Turning**

 | 

Whether to allow Player rotation while capturing.

Requires **Cinematic Mode** to be enabled.



 |
| 

**Show Player**

 | 

Whether to show the local Player while capturing.

Requires **Cinematic Mode** to be enabled.



 |
| 

**Show HUD**

 | 

Whether to show the in-game HUD while capturing. This setting does not apply to UMG based HUD elements and refers to the HUD class based Blueprints. 

Requires **Cinematic Mode** to be enabled.



 |

## Animation Settings

The following options define the **Animation** settings used during capture:

[![](https://dev.epicgames.com/community/api/documentation/image/fd4758fa-bffa-4d8d-8336-5fb224116dda?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fd4758fa-bffa-4d8d-8336-5fb224116dda?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Use Custom Start Frame**

 | 

When enabled, the Start Frame setting will override the default starting Frame Number.

 |
| 

**Start Frame**

 | 

Time field which takes timecode, frame and seconds formats.

This value is used when **Use Custom Start Frame** is enabled.



 |
| 

**Use Custom End Frame**

 | 

When enabled, the End Frame setting will override the default ending Frame Number.

 |
| 

**End Frame**

 | 

Time field which takes timecode, frame and seconds formats.

This value is used when **Use Custom End Frame** is enabled.



 |
| 

**Warm Up Frame Count**

 | 

The number of extra frames to play before the Sequence's Start Frame, to "warm up" the animation. This is useful if your animation contains particles or other run-time effects that are spawned into the scene earlier than your capture Start Frame.

 |
| 

**Delay Before Warm Up**

 | 

The number of seconds to wait (in real-time) before we start playing back the warm up frames.

This is useful for enabling Post Processing effects to settle down before capturing the animation.



 |
| 

**Delay Before Shot Warm Up**

 | 

The number of seconds to wait (in real-time) at Shot boundaries.

This is useful for enabling Post Processing effects to settle down before capturing the animation.



 |