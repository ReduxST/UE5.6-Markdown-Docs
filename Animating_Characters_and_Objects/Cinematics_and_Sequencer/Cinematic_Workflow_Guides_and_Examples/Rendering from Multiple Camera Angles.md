# Rendering from Multiple Camera Angles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-from-multiple-camera-angles-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-from-multiple-camera-angles-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:52

---

When rendering using [Movie Render Queue](/documentation/404), there may be a requirement to render from multiple Cinematic cameras within a single sequence or [Shot](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine#shots). For example, you could be rendering a product demonstration video or training material, which may require multiple angles. Rendering from multiple angles within a single shot can be more ideal than using [Takes](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine#takes), as Takes cause new Level Sequence assets to be created, diverging your content.

This document provides an overview of how to render multiple camera angles from a single shot using Movie Render Queue.

#### Prerequisites

-   You have a basic knowledge of how to create and open a [Level Sequence](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview)
-   Movie Render Queue is a [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) you must enable prior to use. From Unreal Engine's main menu, go to **Edit > Plugins**, locate **Movie Render Queue** in the **Rendering** section, and click the checkbox to enable it. Then, restart Unreal Engine.
    
    ![enable mrq plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d729556-8f5b-4393-bdce-89d553559a7c/plugin.png)
    

## First Camera Setup

Assuming Sequencer is already open within the Level you want to render, the first step is to start creating your [Cinematic Cameras](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine).

1.  Click **Camera** in the **Sequencer Toolbar.** This creates a [spawnable](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics) Cine Camera Actor, [Camera Cuts Track](/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine), and then binds the Cine Camera Actor to the Camera Cuts section.
    
    ![create first camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e1fe608-8f01-4faa-9eb8-d6f1760faeb4/firstcam1.png)
    
2.  Next, [move and keyframe](/documentation/en-us/unreal-engine/how-to-animate-cinematic-cameras-in-unreal-engine) the camera to your desired framing and animation for this shot.
    
    1.  Enable the **Camera icon** on the Cine Camera Actor track, which pilots the camera.
        
    2.  You can also adjust camera-specific properties, such as **Aperture**, **Focal Length**, and **Focus Distance** to help with your shot composition.
        

![create camera shot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df054805-49aa-4867-b8b6-02cbef9607a9/firstcam2.png)

## Additional Camera Setup

You can now start to add new cameras to the sequence. Do this the same way you added the first camera, by clicking **Camera** in the Sequencer Toolbar. Each click will add a new camera, so add as many as you require. Although the Camera Cuts Track still is bound to the first camera (making it appear as if this shot only has one camera), these other cameras will be correctly rendered with Movie Render Queue in the final steps of this guide.

![add more cameras](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e8f9e6c-839d-4f51-875e-8f7929b9772d/morecams1.png)

Similar to the steps taken for the first camera, enable the **Camera** icon on each new camera track to pilot it and set up your composition.

![set up all cameras](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/315b360d-c100-4ad6-9796-272e67825036/morecams2.gif)

Although not required, we recommend you rename your camera tracks to better reflect their content or usage. Right-click on a track and select **Rename**, or press **F2**. If two cameras share the same name, Movie Render Queue automatically renames them to avoid a filename conflict.

![rename cameras](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88dbe9c6-099d-4f2c-996b-f1976a31708f/morecams3.png)

## Open Movie Render Queue

Once all your cameras are composed and animated within the sequence, you can now render using Movie Render Queue (MRQ). To open MRQ, click **Render** in the Sequencer Toolbar.

![open mrq](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab72b7ab-2c85-43ab-8f45-03e0838d0950/mrq1.png)

If MRQ is not correctly opening from this button, check the dropdown menu next to **Render** and ensure it is set to **Movie Render Queue**.

![enable mrq](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5882c77d-61f5-4093-ba81-8d2580b20704/mrq2.png)

## Render Settings

With the MRQ window open, click the **Settings** entry to open the [Render Settings](/documentation/en-us/unreal-engine/cinematic-render-settings-and-formats-in-unreal-engine) window.

![mrq render settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e0d915c-221d-4015-94bf-16626142c90f/mrq3.png)

Click **Add Setting (+)** and select **Camera**, then select the newly added Camera entry and enable **Render All Cameras**.

![add camera render settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ba0246e-2bce-40e6-9850-14385ae6d792/mrq4.png)

Although optional, you may want to edit **Output Directory** or **File Name Format** in Output settings with the `{camera_name}` [Format String](/documentation/en-us/unreal-engine/cinematic-rendering-image-quality-settings-in-unreal-engine#formatstringinformation). Using this provides you extra control over how your output renders are named or categorized. For example, setting **Output Directory** to `{project_dir}/Saved/MovieRenders/{camera_name}/` outputs each camera angle to a different folder.

![set output directory](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11f925c8-ac62-445a-afe2-23859d7d646b/mrq5.png)

If you don't use `{camera_name}`, then MRQ automatically adds the camera name as a suffix to the file name when **Render All Cameras** is enabled, to prevent file name conflicts.

## Render and Results

Once your render settings are set up, click **Render (Local)** to start the MRQ render process.

![start render](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35843e28-603c-467c-ad0c-74c0942b5b77/mrq6.png)

When the render completes, click the **Output** entry to open a file explorer window to the output directory. You should see your multiple angles rendered here. In this example, the different angles were separated by folder using the steps detailed above.

![render results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6b81758-2c1b-466d-ab87-3848888a0408/mrq7.png)