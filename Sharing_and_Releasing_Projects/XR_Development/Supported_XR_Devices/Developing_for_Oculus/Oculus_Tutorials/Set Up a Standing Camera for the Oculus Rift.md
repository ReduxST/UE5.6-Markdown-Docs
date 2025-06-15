# Set Up a Standing Camera for the Oculus Rift

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-a-standing-camera-for-the-oculus-rift-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-a-standing-camera-for-the-oculus-rift-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:47

---

Skill\_family: Tutorial Level 1 Version:5.0 Parent: sharing-and-releasing-projects/xr-development/supported-xr-platforms/developing-for-oculus/OculusHowTo Order: 2 tags:Basics topic-image:HT\_Rift\_Camera\_Setup\_Topic\_Image.png

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01028070-330d-4603-8ecb-09cc461cbf54/vr_standing_experience.png)

One of the first things you will need to think about when starting to develop any Unreal Engine (UE) powered VR experience to be used with the Oculus Rift is deciding whether the experience will be a seated one or a standing one. In the following tutorial we will take a look at how to setup your UE projects VR camera for a standing Oculus Rift VR experience.

## Steps

Below you will find instructions on setting up a Pawn to work with a standing Oculus Rift experience.

1.  First, open up or create a new Pawn Blueprint and then go to the **Component** section of the **Viewport** tab. From there add the following two components with the following names, making sure that the VRCamera is a child of VRCameraRoot:
    
    | Component Name | Value |
    | --- | --- |
    | **Scene** | VRCameraRoot |
    | **Camera** | VRCamera |
    
    Click for full image.
    
    When
    
    No matter what VR HMD you are using, this is the Epic recommended way to set up a VR camera as it allows you to offset the position of the camera without having to move the actual camera.
    
2.  Next, open up the Pawn Blueprint if not already open and in the **Event Graph** drag off the **Event Begin Play** node to show the Executable Actions list. In the list search for the **Set Tracking Origin** node and click on it to add it to the Event Graph.
    
    Click for full image.
    
3.  The Set Tracking Origin node has two options, **Floor Level** and **Eye Level**. For a standing experience, you will need to keep the **Origin** of the Set Tracking Origin node to the default of **Floor Level**.
    
    Click for full image.
    
4.  Drag the Pawn Blueprint from the Content Browser to a level, making sure that it is placed at 0,0,0 in the level.
    
    Click for full image.
    
5.  Select the Pawn Blueprint that was put in the level and in the **Details** panel under the **Pawn** setting, set the **Auto Possess Player** from **Disabled** to **Player 0**.
    
    Click for full image.
    

## End Result

Finally, go to the **Main Toolbar** and change the **Play Mode** to **VR Preview** and then press the **Play** button. When you put your Oculus Rift HMD on and view the level while standing, you should see something similar to the following video.

## UE Project Downloads

Below you will find a link to where you can download the UE project that was used to create this example.

-   [**Oculus Rift Standing VR Camera Example Project**](https://epicgames.box.com/s/qgoh6uk0f8ra4rtvp0jdrxygfb2n9ykv)