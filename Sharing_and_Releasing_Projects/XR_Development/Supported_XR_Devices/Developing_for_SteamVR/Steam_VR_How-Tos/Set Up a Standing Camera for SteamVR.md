# Set Up a Standing Camera for SteamVR

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-a-standing-camera-for-steamvr-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-a-standing-camera-for-steamvr-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:46

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03443176-b234-41de-98d4-55d1793153a0/vr_standing_experience.png)

One of the first things you will need to think about when starting to develop any Unreal Engine powered VR experience to be used with SteamVR is deciding whether the experience will be a seated one or a standing one. In the following How - To we will take a look at how to setup your UE projects VR camera for a standing SteamVR experience.

## Steps

Below you will find instructions setting up a Pawn to work with a standing SteamVR experience.

1.  First, open up or create a new Pawn Blueprint and then go to the **Component** section of the **Viewport** tab. From there add the following two components with the following names, making sure that the VRCamera is a child of VRCameraRoot:
    
    | Component Name | Value |
    | --- | --- |
    | **Scene** | VRCameraRoot |
    | **Camera** | VRCamera |
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/322ac808-5b0e-4423-9c67-acb10a124477/ht_steamvr_camera_setup_00.png)
    
    No matter what VR HMD you are using, this is the Epic recommended way to set up a VR camera as it allows you to offset the position of the camera without having to move the actual camera.
    
2.  Next, open up the Pawn Blueprint if not already open and in the **Event Graph** drag off the **Event Begin Play** node to show the Executable Actions list. In the list search for the **Set Tracking Origin** node and click on it to add it to the Event Graph.
    
    Click for full image.
    
3.  The Set Tracking Origin node has two options, **Floor Level** and **Eye Level**. For a standing experience, you will need to leave the **Origin** of the Set Tracking Origin node to the default of **Floor Level**.
    
    Click for full image.
    
4.  Drag the Pawn Blueprint from the Content Browser to a level, making sure that it is placed at 0,0,0 in the level.
    
    Click for full image.
    
5.  Select the Pawn Blueprint that was placed in the level and in the **Details** panel under the **Pawn** setting, set the **Auto Possess Player** from **Disabled** to **Player 0**.
    
    Click for full image.
    

## End Result

Finally, go to the **Main Toolbar** and change the **Play Mode** to **VR Preview** and then press the **Play** button. When you put your HTC Vive HMD on and view the level while sitting down, you should see something similar to the following video:

## Project Downloads

Below you will find a link to where you can download the project that was used to create this example.

-   [**SteamVR Standing VR Camera Example Project**](https://epicgames.box.com/s/8n6rtur0q01jrmgbdacog986tuzfx7js)