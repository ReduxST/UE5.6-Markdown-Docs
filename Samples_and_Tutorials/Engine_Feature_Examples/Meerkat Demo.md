# Meerkat Demo

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/meerkat-sample-project-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/meerkat-sample-project-for-unreal-engine)  
**Processed:** 2025-06-14 16:35:36

---

Real-time rendering technology is an increasingly important tool in the filmmaking process, from previsualization to the final render, as it enables filmmakers to review and iterate on digital scenes and effects very quickly. The **Meerkat Demo** by Weta Digital is a short film rendered entirely in **Unreal Engine**, built to explore the highest level of quality possible while maintaining as fast a rendering speed as possible. With the right graphics card, the Meerkat short will run in real time. This document will guide you through the process of outputting a high-quality render of the Meerkat short yourself using the **Movie Render Queue** plugin.

This sample is available for Unreal Engine 5 and later. Be aware that it is an especially graphically intensive scene, and needs a powerful video card to run at a stable framerate.

## Required Setup

To set up a project with the Meerkat sample, follow these steps:

1.  Access the [Meerkat sample](https://fab.com/s/094cb6da0970) from **Fab** and click **Add to My Library** for the project file to show in the **Epic Games Launcher**.
    1.  Alternatively, you can search for the sample project from the Fab plugin for UE.
2.  From the **Epic Games Launcher**, go to **Unreal Engine > Library > Fab Library** to access the project.
    
    Sample projects only appear in **Fab Library** when you install the compatible engine version.
    
3.  Click **Create Project** and follow the on-screen instructions to download the sample and start a new project.
    1.  To learn more about accessing sample content and the Fab plugin for Unreal Engine, see [Samples and Tutorials](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).
4.  Open your new project in the **Unreal Editor**.
    
5.  Open the **Edit** > **Plugins** window and navigate to the **Built-In** > **Rendering** section. Make sure that the **Movie Render Queue** plugin is enabled and, if necessary, restart the editor.
    
    Enabling the Movie Render Queue plugin. Click the image to enlarge it.
    

## Viewing the Meerkat Sequence

Once you have loaded Unreal Editor and opened the Meerkat Demo project, go to the **Content Drawer** and double-click **Master\_SEQ**.

![Master_SEQ location in the content drawer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7b60fa0-0094-4e64-ad97-5840a61a34b8/master-seq-location.png)

This will open **Sequencer** and load the Master\_SEQ level sequence.

The Master\_SEQ level sequence is loaded in the Sequencer tab. Click the image to enlarge it.

You can scrub the timeline through the different shots by clicking on the timeline.

The timeline for the Master\_SEQ level sequence. Click the image to enlarge it.

If you want to be able to see the shots through the cinematic cameras set up in the scene, you can click on the **camera icon** for **Shots**. Your viewport will then look through the camera corresponding to the position of the timeline.

The toggle button for Cinematic camera mode as it appears in the Sequencer tab. Click the image to enlarge it.

You can also change your viewport mode from Perspective to **Cinematic Viewport**.

Changing to Cinematic Viewport Mode using the Viewport controls. Click the image to enlarge it.

For more information about working with Sequencer, refer to the [Sequencer Editor](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine) section.

## Optimization Settings

To improve performance, the Meerkat demo uses low-resolution settings by default. If you want the highest-quality visual, there are several optimization settings you can change.

### Toggling High-Resolution Environment Meshes

In the **Outliner**, click the **VisualSettings\_BP** Blueprint. In the **Details** tab, under **Default**, you will find the **Highres Env Meshes** setting. Your scene will have improved fidelity with it turned on, but it will run slightly faster with it turned off.

![Highres Meshes Off](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a82585c7-d939-48c4-b4d6-1d239363e682/meerkat-comparison-1.png)

![Highres Meshes On](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7ebc061-5fe7-41d2-91de-8a05fb0f1b9d/meerkat-comparison-2.png)

Move the slider to compare the scene without high-resolution environment meshes versus with them turned on.

### Changing the Eagle's Groom Resolution

The **Eagle** in the Meerkat demo uses a **Groom** hair asset to represent its feathers. By default, it uses a low-resolution groom to improve performance, but you can change this to a high-resolution asset instead.

1.  In the **Outliner**, click the **Characters** group, then select **amlEagle\_BP** and look at its **Details** tab.
    
2.  Select the **Groom** property, which is listed under **amlEagle\_BP(self)** in the **Details** tab.
    
    The Groom properties can be accessed from the Details tab. Click the image to enlarge it.
    
3.  There are both a **Groom Asset** and **Binding Asset**, and each has a dropdown menu to the right of the icon.
    
    1.  Click the **Groom Asset** menu, then change the groom from amlEagle\_groomLowRes\_r036\_GRO to **amlEagle\_highRes\_GRO**.
    2.  Click the **Binding Asset**, then change it from amlEagle\_groomLowRes\_r036\_GRB to **amlEagle\_highRes\_GRB**.

![Low-res Groom Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a150dbb3-2021-4827-9fa7-8fcd55d2cff5/eagle-comparison-1.png)

![High-res Groom Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1cd0b3b-ac49-4986-9037-d8261d92bf72/eagle-comparison-2.png)

Move the slider to compare the Eagle with low-resolution groom assets versus high-resolution assets. Note the finer detail in the feathers.

For more information about working with Groom assets, refer to the [Groom Asset Editor User Guide](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine).

## Rendering the Meerkat Demo With Movie Render Queue

To render the Meerkat Demo, you need the [Movie Render Queue](/documentation/404), which is used for outputting high-quality renders of Sequencer movies. Review the steps in [Required Setup](/documentation/en-us/unreal-engine/meerkat-sample-project-for-unreal-engine#requiredsetup) to ensure that you have the Movie Render Queue plugin enabled, then follow the steps below to set up a rendering job:

1.  Launch the Movie Render Queue by selecting **Window** > **Cinematics** > **Movie Render Queue**.
    
    ![Accessing the Movie Render Queue](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/171fdc1d-260a-4db5-99be-71e5d33c0645/movie-render-queue-location.png)
2.  In the top-left corner of the **Movie Render Queue window**, click the **\+ Render** button. Select **Master\_SEQ** from the dropdown menu.
    
    Accessing Master\_SEQ from the + Render dropdown. Click the image to enlarge it.
    
    This will add an entry to the Movie Render Queue's list of **jobs** to render.
    
3.  In the entry for Master\_SEQ, click **Unsaved Config** under the **Settings** column to open the **Settings Window**.
    
    ![Clicking Unsaved Config opens the Settings window.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5114c606-8063-4f57-993e-24e5852700a5/movie-render-queue-unsaved.png)
4.  In the Settings Window, click the **Load/Save Presets** dropdown in the top right corner and select the **MoviePipelineConfig\_Temporal** preset.
    
    Selecting the MoviePipelineConfig\_Temporal preset and applying it to the shot. Click the image to enlarge it.
    

You now have the settings needed for rendering the Meerkat demo. In the Settings window, you will see a list along the left side of the window that represents items that have been explicitly set for this project. You can edit these settings to change the output directory for the rendered images, change the type of image that will be saved, or edit post-processing settings. Click the **Accept** button on the bottom right corner to close the window.

The Settings window with the applied settings from MoviePipelineConfig\_Temporal. Click the image to enlarge it.

Note: The image above displays a warning icon in the **Settings** window. If you click it, you can see the warning details. The TAA samples in the project are set to 16, but the warning will appear anyway. You can ignore this warning.

To launch the render, click the **Render (Local)** button in the lower-right corner of the Movie Render Queue window.

Finalized settings in the Movie Render Queue window. Click the image to enlarge it.

A Render Preview window will appear, showing information related to the render.

The Movie Render Queue preview window displays information about the rendering progress. Click the image to enlarge it.

For more information about how to use Movie Render Queue, refer to the [Movie Render Queue section](/documentation/404) of the Sequencer workflow guides.

## Adding the Meerkat Control Rig to a Shot

This project includes a **control rig** for the Meerkat, which you can use to explore some keyframe animation inside Unreal Editor. To use this control rig, you need to add the **amlMeerkat\_BP** into a shot in Sequencer. The easiest way to do this is to create a new level sequence.

1.  Select **Cinematics** > **Add Level Sequence**.
    
2.  In the **Save Asset As** window, navigate to the **Levels** folder, name the level sequence **MeerkatAnim\_SEQ**, then click **Save**. The level sequence you just saved will become the active sequence in Sequencer.
    
    Saving the new sequence to use with the Meerkat control rig. Click the image to enlarge it.
    
    You can return to the original sequence by locating Master\_SEQ in the Content Drawer and double-clicking it.
    
3.  In the Content Drawer, open the **Content** > **Assets** > **meerkat** > **Blueprints** folder and locate the **amlMeerkat\_BP** asset.
    
    The Meerkat control rig asset in the Content Drawer. Click the image to enlarge it.
    
4.  Click and drag the **amlMeerkat\_BP** asset into **MeerkatAnim\_SEQ**.
    
    Clicking and dragging the Meerkat control rig Blueprint into the sequence. Click the image to enlarge it.
    

You now have a copy of the Meerkat asset with a control rig that you can use in your level sequence.

Keyframing the Meerkat control rig in the Sequencer timeline. Click the image to enlarge it.

You can edit its parameters in the timeline or manipulate the control rig directly in the viewport.

Manipulating the control rig in the level viewport. Click the image to enlarge it.

If you are trying to use the Meerkat control rig and you do not have a high-end graphics card, you can turn the visibility of the groom component off to hide the fur, which will improve performance.

To do this, click on the Meerkat in your viewport to display its information in the details panel. Under SkeletalMeshComponent click on Groom(Inherited), scroll down to Rendering, and turn off the Visible flag.

The location of the Groom component's visibility checkbox. Click the image to enlarge it.