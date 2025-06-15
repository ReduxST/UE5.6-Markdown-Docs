# Playing Live Video Captures

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/playing-live-video-captures-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/playing-live-video-captures-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:43

---

Media Framework in Unreal Engine (UE) supports video and audio capture devices as a form of media that can be played inside the Engine. For example, you can take a live video feed from your webcam and play it directly inside UE on a Static Mesh or as part of a HUD. Or, you can deploy your project to a mobile device and retrieve the front or rear camera video feed and play that back inside your application.

In this example, you take the video capture feed from a webcam and display it as part of a HUD during gameplay.

![Final Result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bad58d6-fad1-4581-8f3d-ab181d176bc3/01-final-result.png)

The Electra Media Player does not currently support Live Video Capture playback.

## Steps

This tutorial is using the **Blueprint Third Person Template** project with **Starter Content** enabled. You must also have a webcam attached to your computer.

1.  Expand the **Sources** panel and create a folder called **Movies**, then inside it, create a **Media Player** and linked **Media Texture** asset called **MediaPlayer**.
    
    ![Create a New Folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/296bb12c-97d7-412a-9d76-360f5660bb52/02-select-media-player.png "Create a New Folder")
2.  Open the **MediaPlayer** asset, then next to the **Media URL** field, click and expand the **Capture Devices** and find your camera under **Video**.
    
    ![Find Your Camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b450372-2bc8-4626-9379-1f37099feeff/03-select-camera-path.png "Find Your Camera")
    
    The number of capture devices and names displayed may differ from the screenshot based on your computer setup.
    
    When selecting your video capture device, video from the camera will be displayed inside the Media Editor Player.
    
3.  Highlight and right-click copy the **Media URL** string displayed in the Media URL field.
    
    Click image to expand.
    
    The URL string displayed may differ from the screenshot based on your computer setup.
    
4.  Inside the **Content Browser**, right-click and under **User Interface** select **Widget Blueprint** and call it **HUD**.
    
    ![Create Widget Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1442d587-5304-4727-84d1-9b384c02a278/05-create-widget-blueprint.png "Create Widget Blueprint")
    
    You are going to use your **Media Texture** inside your User Interface to display a picture-in-picture style HUD taking in and using your webcam video.
    
5.  Open the **HUD** Widget Blueprint, then from the **Content Drawer**, drag-and-drop the **MediaPlayer\_Video** texture into the HUD graph. You will see the video populate the **Image** field under **Appearance**.
    
    ![Drop the Media Texture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99d0a6cc-6888-40bb-91d6-ddb3951931c7/06-add-media-texture.png "Drop the Media Texture")
6.  Close the **HUD** Widget Blueprint, then from the Main Editor Toolbar, click **Blueprints** then select **Open Level Blueprint**.
    
    ![Open Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbf13272-5540-48f9-b344-ddd7cd02c4b1/07-open-level-blueprint.png "Open Level Blueprint")
    
    While you are not directly opening a Media Source and instead have copied the Media URL, you still need to open it in order for it to play at runtime.
    
7.  In the **My Blueprint** panel, create a variable called **Media Player** of the **Media Player Object Reference** type and assign your **Media Player**.
    
    Click image to expand.
    
    You may need to click **Compile** to compile the Blueprint before assigning the **Default Value** of the Media Player variable.
    
8.  Hold **Ctrl** and drag the **MediaPlayer** variable into the graph, then right-click and add an **Event BeginPlay** node.
    
    ![Drag the Media Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4dea255-76d8-4f10-be5e-310c5a6c0649/09-add-player-to-graph.png "Drag the Media Player")
    
    You have created a reference to your Media Player that you want to perform actions on, and an [Event](/documentation/en-us/unreal-engine/events-in-unreal-engine) to signify the start of gameplay.
    
9.  Right-click and add a **Create Widget** node (with **HUD** as the **Class**), then off the **Return Value** use **Add to Viewport** and connect as shown.
    
    ![Create the Widget Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/684a6c02-7d2c-4b4d-a9e4-4dadf9a5f70b/10-create-hud-wiget.png "Create the Widget Node")
    
    Here you are saying when the game begins, create the HUD Widget Blueprint and add it to the player's viewport.
    
10.  Off the **Media Player** node in the graph, use **Open URL** and paste the URL copied from **Step 3** and connect as shown.
    
    Click image to expand.
    
    If you play in the Editor now, video from your webcam will appear on the HUD image you placed in your desired location.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93d8d581-bc49-4d69-844f-e00ea39bed9e/12-final-result.png)
    
    In this example the Media URL is specified to open, however, knowing what this is may not always be the case. You may package and distribute your project to others with this functionality and want to get what capture devices the end users have connected and use one of those. Or you may want to deploy your project to a mobile device and want to get the front or rear camera video feed and use that as the media source. You can use the **Enumerate Capture Devices** function to return all of the attached capture devices and get information about those devices.
    
11.  Right-click in the graph and search for and add the **Enumerate Video Capture Devices** function.
    
    ![Enumerate Video Capture Devices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb43868c-7c30-44f1-878c-447ae877821f/13-add-enumerate-video-capture-function.png "Enumerate Video Capture Devices")
    
    There are enumerators for Audio, Video and webcam capture devices (where webcam is used for Mobile devices as you can get the Front or Rear cameras).
    
12.  Drag off the **Filter** pin and use the **Make Bitmask** node.
    
    ![Add Make Bitmask Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/831c66ba-dcf5-4768-9a93-0f8ff2f1b4e9/14-use-make-bitmask.png "Add Make Bitmask Node")
    
    Using the Make Bitmask node will enable you to filter for a specific subset of devices.
    
13.  With the **Make Bitmask** node selected, in the **Details** panel, change the **Bitmask Enum** to **EMediaVideoCaptureDeviceFilter** then enable each in the filter.
    
    ![Enable Each Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/134059b5-83db-4126-b636-17c82fbe414c/15-enable-each-filter.png "Enable Each Filter")
    
    Here you are filtering for each of the enabled options to return the capture devices (you could exclude the ones you want to omit to narrow the list of returned devices).
    
14.  From the **Out Devices** use the **Get Copy** node and off its out pin, use the **Break MediaCpatureDevice** node and connect to an **Open URL** as shown below.
    
    Click image to expand.
    
    This process will find the first available capture device and return its URL that is then used with Open URL to open the source for playback.
    
15.  **Compile** and close the Level Blueprint then click the **Play** button from the Main Toolbar to play in the Editor.
    

## End Result

When you play in the Editor, the video feed from your camera will get pushed through to the Engine and appear on your HUD.

To get the Front or Rear camera on a mobile device:

-   Use the **Enumerate Video Capture Devices** node and set the **Bitmask Enum** to **EMediaWebcamCaptureDeviceFilter** option.
-   On the **Make Bitmask** node, flag which camera you want to get.

![Flag Camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99b68afc-769c-4566-8df5-c13471e3d1a7/17-flag-needed-camera.png "Flag Camera")