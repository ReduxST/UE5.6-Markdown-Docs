# Camera Cut Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:57

---

One of the key parts of creating a cinematic in **Sequencer** is selecting which camera to be active during a sequence. You can use the **Camera Cut Track** to control this behavior, as well as providing tools to blend cameras together, or to and from gameplay.

This document provides an overview of how to create and use the Camera Cut Track in Sequencer.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).
-   You are familiar with how to [add Cameras to Sequencer](/documentation/en-us/unreal-engine/how-to-animate-cinematic-cameras-in-unreal-engine).

## Creation

There are a variety of ways to create a Camera Cut Track:

-   Click **Add Track (+) > Camera Cut Track**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e26705aa-21c8-4279-8cac-74648ddf6f44/create1.png)
    
-   Click the **Camera** button in the [Sequencer Toolbar](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine), which creates a Camera Cut Track and a [spawnable](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics) [Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine), then binds the camera to the track.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77c7c8b5-454a-4a3c-8a28-dd75fc558c6f/create2.png)
    
-   Add a currently-existing Camera Actor to the sequence by clicking **Add Track (+) > Actor To Sequencer > Camera Actor**. When you do this, you create a Camera Cut Track automatically and bind it to this camera.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c7de21e-71fe-4738-b0de-b88235801c8b/create3.png)
    

### Binding Cameras

To make Sequencer use a specific camera to look through, you must bind it to the Camera Cut Track. In most creation methods detailed above, your camera is already bound. If not, then you can bind it by clicking **Add Camera (+)** and selecting the following:

1.  If you already have Cameras added to the sequence, you can select one from the **Existing Bindings** category here.
2.  If you want to add a new camera, you can select one from the level list under **New Binding**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32af3a32-6709-4140-8c7d-b24c4b9a7bb3/create4.png)

After selecting a Camera, a Camera Cut section creates and binds to the selected camera. Enable the **Camera Lock** button on the Camera Cut Track to make the viewport look through the active camera.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b9d415e-e9c1-42f6-8418-57fff9770676/create5.png)

Viewport camera control is disabled when locking your view to the Camera Cut Track. If you want to move or keyframe the current active camera, then you need to enable that Camera Track first.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1d81835-3ef0-46e6-b67f-9a2587861a29/create6.png)

## Making Cuts

To cut between cameras, move the **Playhead** to the point in the timeline where you want the camera to cut. Next, click **Add Camera (+)** on the Camera Cut Track and select the camera you want to cut to. This creates a cut at the playhead, making a new Camera Cut section bound to the camera you selected.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdd4aa66-7f2f-46cd-ae69-55260eb3e1a9/cut1.gif)

To change the timing of your cut, click and drag on any of the touching section edges to a different time. Unlike most other [sections](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#sections), Camera Cut sections by default do not allow any gaps or overlaps between cuts.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b47b933f-21e4-427b-9707-dd56098f1bcd/cut2.gif)

In most cinematic cases we do not recommend constructing full-length cinematic sequences using multiple cameras and cuts. Instead you should construct your cinematic sequences using [shots](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine), which partition a single Camera and Camera Cut for each shot.

## Blending Cameras

Instead of hard-cutting between cameras, you can choose to blend between them, which blends the transforms and camera component properties (Depth of Field, Focal Length, and other properties). To do this, right-click the Camera Cut Track and enable **Can Blend**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2adaa72d-a1fb-43b9-a3c3-f551627f9144/blend1.png)

Once enabled, you can now [blend](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#blending) the Camera Cut sections, similarly to normal section usage. For example:

-   You can overlap two Camera Cut sections, blending from one camera in your sequence to another.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/346b0d4b-9d24-466d-9f38-5cc5fa537e00/blend2.gif)
    
-   You can drag on the upper corner of a section to blend it in and out. Blending a Camera Cut section in this way can make your sequence camera blend in or out to gameplay.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1fc7407-3dbe-4ba8-8401-c65dff5e5c92/blend3.gif)
    

Blending cameras can be useful when constructing complex shots. In this example, an unconstrained "free" camera blends to an attached camera tracking a fast-moving object. Creating and maintaining this motion with a single camera can be tedious, but with blending cameras it can be much easier.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35a8207f-625a-424d-9940-9ebe4d7f336d/blendexample.gif)

## Properties

You can find the following Camera Cut-specific properties when right-clicking a section:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/266f5469-ba8e-43a0-a12b-d5233cd43cb6/properties.png)

| Name | Description |
| --- | --- |
| **Lock Previous Camera** | Enabling this ensures that outgoing cameras do not switch if you are blending from gameplay. This can be useful to enable if your game contains possible camera switching logic that could occur during a blend. Enabling this locks the last used camera as the view to blend from. |
| **Camera Binding ID** | The camera this Camera Cut section is looking through. |

### Thumbnails

Similar to [shots](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine), Camera Cut sections display a thumbnail preview of the camera view. You can customize the thumbnail display by right-clicking the section and navigating to the **Thumbnails** menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dbd914f-95c1-4cc7-8302-9c084b4f2126/thumbnails.png)

| Name | Description |
| --- | --- |
| **Refresh** | Regenerates the thumbnails for this section. This is useful if the thumbnail images are out of date or are displaying incorrectly. |
| **Set Thumbnail Time to...** | If **Draw Single Thumbnail** is enabled, then selecting this picks a specific frame of the current sequence to use as the single thumbnail image. |
| **Refresh All** | Regenerates the thumbnails for all Camera Cut sections. This is useful if the thumbnail images are out of date or are showing incorrectly. |
| **Draw Thumbnails** | Controls the display of thumbnails for all shots. If disabled, then no thumbnails display, and the track size reduces. |
| **Draw Single Thumbnail** | Enabling this causes only a single thumbnail image to display, at the start region of the camera cut section. |
| **Thumbnail Size** | Controls the width and height of thumbnails. Adjusting the height of your thumbnail will increase or decrease the track size. |
| **Quality** | The quality used to render the thumbnail images. |

Generating thumbnails has a performance cost. If you find the Unreal Editor is running slowly while a Sequence is open, try disabling **Draw Thumbnails**.