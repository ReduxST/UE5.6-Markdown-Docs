# AJA Video I/O Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/aja-video-io-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/aja-video-io-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 16:05:25

---

In this Quick Start guide, we walk through the process of setting up an Unreal Engine Project to work with a professional video card from AJA Video Systems. At the end of this guide:

-   you'll have video input from your AJA card playing inside your Unreal Engine Project.
-   you'll be able to capture camera viewpoints both from the Editor and from your runtime application, and send them out to an SDI port on your AJA card.
-   you'll know where to go when you want to set up more advanced adjustments to your video inputs, such as correcting lens deformation and applying chroma-keying effects.

For a working example that shows many of the elements described below put into practice, see the **[Virtual Studio](/documentation/en-us/unreal-engine/virtual-studio-sample-project-in-unreal-engine)** showcase, available on the Samples tab of the Epic Games Launcher.

**Prerequisites:**

-   Make sure that you have a supported card from AJA Video Systems, and that you've installed the necessary drivers and software. For details, see the [AJA Media Reference](/documentation/en-us/unreal-engine/aja-media-reference-for-unreal-engine) page.
-   Make sure that your card is working correctly, and that you have some video input feeding in to at least one of the card's SDI ports.
-   Open an Unreal Engine Project that you want to integrate with your video feeds. This page shows the steps in the **Third Person** Blueprint template, but the same steps will work equally well in any Project.

The AJA Media components used in this guide are built on top of the [Media Framework](/documentation/en-us/unreal-engine/media-framework-in-unreal-engine), and we'll use [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) to script the video capturing process at runtime. Some prior knowledge of these topics is recommended but not required.

## 1 - Set Up the Project

Before you can get video input from your AJA card into your Unreal Engine Level, and send output from the Unreal Engine through one of your AJA card's SDI ports, you'll need to do some basic setup to enable the AJA Media Player Plugin in your Project.

If you started your Unreal Engine Project from one of the Templates in the **Film, Television, and Live Events** category, the necessary plugins may already be enabled for you. If not, follow the instructions below to enable them.

### Steps

1.  Open the Project that you want to use with AJA video I/O in the Unreal Editor.
    
2.  From the main menu, select **Edit > Plugins**.
    
3.  In the **Plugins** window, find the **AJA Media Player** plugin under the **Media Players** category. Check its **Enabled** checkbox.
    
    Click image to expand.
    
4.  Find the **Media Framework Utilities** Plugin under the **Media Players** category. Check its **Enabled** checkbox, if it's not already checked.
    
    Click image to expand.
    
5.  Click **Restart Now** to restart the Unreal Editor and reopen your Project.
    
    Click image to expand.
    

### End Result

Your Project is now ready to accept video from the AJA card, and to send rendered output to the card. In the next sections, we'll hook it up and start playing video in and out.

## 2 - Rendering Video Input in the Unreal Engine

In this process, we'll make video input from the AJA card visible in the current Level in the Unreal Editor. This process uses a Media Bundle: a kind of Asset that packages together several different types of Assets involved in the Media Framework, and that offers you control over some advanced features like lens deformation, chroma-keying, color correction, and more. 

### Steps

1.  In your **Content Browser**, expand the **Sources** panel. Right-click, and choose **New Folder** from the context menu.
    
    ![New Folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbc67195-961b-4e52-ad31-649a9561dfe3/04-new-folder_ue5.png "New Folder") Rename your new folder **AJA**.
    
2.  Open your new folder, right-click in the **Content Browser** and choose **Media > Media Bundle**.
    
    ![New Media Bundle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a6c05ec-62bf-4463-aff9-e9a134d13726/05-media-bundle_ue5.png "New Media Bundle")
3.  Your new Asset's name is automatically selected in the Content Browser, so you can give it a descriptive name:
    
    ![Name the Media Bundle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d9fb626-69ac-4214-b7ae-2278a517255e/06-rename-media-bundle_ue5.png "Name the Media Bundle")
    
    Type a new name, like **AjaMediaBundle**, and press **Enter**. A new folder of Media Framework Assets is automatically created next to your Media Bundle, named with the suffix **\_InnerAssets**. 
    
4.  Save your new Assets by clicking the **Save All** button in the **Content Browser**.
    
    ![Save All Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20f537a6-c561-4beb-bf61-5c99a244875b/07-save-all_ue5.png "Save All Assets")
5.  Double-click your new Media Bundle to edit its properties. The Media Bundle is capable of playing video from any kind of media source the Engine supports, so you'll need to tell it that you want to get the video from your AJA card.
    
    In the **Media Source** property, select **Aja Media Source** from the drop-down list:
    
    Click image to expand.
    
6.  Once you've identified the type of Media Source you want the Media Bundle to handle, you can then set up any configuration properties offered by that type of source.
    
    You can make Unreal Engine automatically match the format and framerate of the incoming video signal. To enable automatic format detection, click the **Configuration** dropdown, enable **Auto**, and then click **Apply**. The engine now seamlessly handles changes and restarts automatically if the signal is temporarily lost.
    
    Click image to expand.
    
    The options you see may vary depending on the devices you have installed. For details on all of the properties you can set for an AJA Media Source, see the [AJA Media Reference](/documentation/en-us/unreal-engine/aja-media-reference-for-unreal-engine) page.
    
7.  If you want to apply any compensation to the incoming video to account for lens distortion, you can set up the physical properties of the lens in the **Lens Parameters** section. 
    
    Click image to expand.
    
    These **Lens Parameters** just set up the physical properties of the lens. You'll actually activate the lens compensation later, when you edit the Material Instance used by the Media Bundle. Save your Media Bundle when you're done setting up its properties, and return to the **AJA** folder in the Content Browser.
    
8.  Drag your **AjaMediaBundle** Asset from the Content Browser into the Level Viewport.
    
    Click image to expand.
    
    You'll see a new plane appear, showing the video currently being played over the port configured for your Media Bundle. Use the transform tools in the Viewport toolbar to move, rotate, and resize it. If your Media Bundle doesn't start playing automatically, select it, then click the **Media Bundle > Request Play Media** button in the **Details** panel.
    
    ![Request Play Media](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88c3548a-97e3-46bb-ac90-db99d9435b38/12-request-play-media_ue5.png "Request Play Media")
9.  Now, we'll see how to apply keying and compositing effects to the video stream. Back in the Media Bundle Editor, click the **Open Material Editor** button in the Toolbar to edit the Material Instance that this Media Bundle uses to draw its incoming video feed on to an object in the Level.
    
    ![Open Material Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49370eba-6b7b-4850-98eb-5c1dee318847/13-open-material-editor_ue5.png "Open Material Editor")
    
    This Material Instance is saved inside the **AjaMediaBundle\_InnerAssets** folder that was created automatically with your Media Bundle.
    
    Click image to expand.
    
10.  In the Material Instance Editor, you'll see a number of properties exposed for you to configure keying, cropping, and color correction, and to activate the correction for the lens distortion that you set up in the Media Bundle.
    

Click image to expand.

While you adjust the settings in the Material Instance Editor, you can see the effect of your changes on the video feed playing back in the main Level Viewport.

You may find it more convenient to see the effects of the changes you make in the preview panel of the Material Instance Editor instead. To do this, temporarily enable the **IsValid** setting, and set its value to `1.0`.

![IsValid](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a03780d0-fb4c-4b85-ba01-c3addf5deade/16-global-scalar-parametr_ue5.png)

Click the arrow at the top left of the viewport toolbar, and enable the **Realtime** option in the menu.

![Realtime viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e535bf2-abec-4bc9-aaf4-ecd3c16dba54/17-expose-realtime_ue5.png "Realtime viewport")

You'll be able to judge the effect of your changes more easily by changing the preview mesh to a plane or a cube. Use the controls at the bottom of the viewport:

![Preview mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e11ecf13-6707-436c-b1cb-aa4b62280606/18-change-shape-form_ue5.png "Preview mesh")

When you're done, return the **IsValid** setting to its previous value.

1.  When you're done changing the Material Instance properties, click the **Save** button in the Toolbar.

### End Result

At this point, you should have video playing over an SDI port showing up inside your Unreal Engine Level, and you should understand where to set up more advanced features like lens deformation and chroma-keying.

If you're already familiar with the Media Framework, another way you could get video into your Level is to create a new **AjaMediaSource** Asset in your Project, and set it up with the same source properties you set up inside the Media Bundle in the procedure above. Then, create your own **MediaPlayer** and **MediaTexture** Assets to handle the playback of that source in your Level. For details, see the [Media Framework](/documentation/en-us/unreal-engine/media-framework-in-unreal-engine) documentation. However, we recommend using the Media Bundle, as shown above, to get the best balance between ease of use and professional quality video features.

## 3 - Output Captures from the Unreal Editor

In this process, you'll set up an AJA Media Output object, and use the **Media Captures** panel in the Unreal Editor to output the view from selected cameras in the Level to your AJA card.

### Steps

1.  Right-click in the Content Browser, and select **Media > Aja Media Output**. 
    
    Click image to expand.
    
    Name your new Asset **AjaMediaOutput**.
    
2.  Double-click your new Asset to open it up for editing. Just like when you created your Aja Media Source, you have to set up the **Configuration** property to control the properties of the video feed that the Unreal Engine sends to your AJA card. Click the arrow to open the submenu, select the options that match your video setup, then click **Apply** in the submenu.
    
    Click image to expand.
    
    For details on all of the properties you can set in the AJA Media Output, see the [AJA Media Reference](/documentation/en-us/unreal-engine/aja-media-reference-for-unreal-engine) page.Save and close your Media Output when you're done.
    
3.  Now we'll place two cameras in the Level, to give us viewpoints for the output we'll send to the AJA card. In the **Place Actors** panel, open the **Cinematic** tab, and drag two instances of the **Cine Camera Actor** into the viewport.
    
    ![Drag and drop Cine Camera Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06e2ee5f-3fb0-4171-804f-dc2d8e8df09d/21-add-cinema-camera-actor_ue5.png "Drag and drop Cine Camera Actors")
    
    Place the cameras where you want them in the Level, so that they're showing different viewpoints on the scene.
    
    **Piloting** the camera is a fast and easy way to set its viewpoint exactly the way you want it. See [Pilot Actors in the Viewport](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine).
    
4.  From the main menu, choose **Window > Virtual Production > Media Capture**. You'll use the **Media Capture** window to control when the Editor sends output to your AJA port, and what camera it should use in the Level.
    
    ![Media Capture window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a4a890f-93b2-4001-b3da-b5bcb1dc61ff/22-media-capture_ue5.png "Media Capture window")
5.  Under the **Media Viewport Capture** area, find the **Viewport Captures** control. Click the **Add (+)** button to add a new capture to this list.
    
    ![Add a viewport capture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8269956e-e1e5-43ef-b0f2-b401739a9cd5/23-add-viewport-capture_ue5.png "Add a viewport capture")
6.  Expand the new entry. First, we'll add the cameras that we want to capture from. In the **Locked Camera Actors** control, click the **Add (+)** button to add a new entry.
    
    ![Add a camera actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47932b51-0ad3-4c52-870e-32356e664222/24-add-cameras_ue5.png "Add a camera actor")
    
    Then, use the drop-down list to choose one of the cameras you placed in the Level.
    
    ![Select the camera actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d57b1ef6-e2c5-449e-a307-6f502cb6a083/25-select-cinema-actor_ue5.png "Select the camera actor")
    
    Repeat the same steps to add the other camera to the list.
    
7.  Now, set up the output that you want to capture these cameras to. Set the **Media Output** control to point to the new AJA Media Output Asset that you created above. You can do this by selecting it in the drop-down list, or drag your AJA Media Output Asset from the Content Browser and drop it into this slot.
    
    ![Set the AJA Media Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b23b96f-86e0-4467-b9a5-daf0d1fd2dad/26-select-aja-output_ue5.png "Set the AJA Media Output")
8.  At the top of the window, click the **Capture** button.
    
    ![Start capturing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d606165-8931-43e2-866f-cd7eea3c0ae9/27-capture-button_ue5.png "Start capturing")
    
    You'll see a new frame at the bottom of the window that shows a preview of the output being sent to the AJA card. If you have this port hooked up to another downstream device, you should start to see the output coming through.
    
    ![Active Media Capture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0157ac2-e2ec-4215-a173-0f30b9391796/28-viewport-cinema-actor_ue5.png "Active Media Capture")
9.  Each camera that you added to the Locked Camera Actors list for this viewport capture is represented by a corresponding button above the video preview. Click the buttons to switch the capture back and forth between the two views.
    
    Click image to expand.
    

### End Result

Now you've set up the Unreal Editor to stream output from cameras in your Level to a port on your AJA card. Next, we'll see how to use Blueprint scripting to do the same thing in a running Unreal Engine Project.

## 4 - Output Captures at Runtime

The **Media Capture** window that you used in the last section is a practical and easy way to send captures to the AJA card. However, it only works inside the Unreal Editor. To do the same thing when you're running your Project as a standalone application, you'll need to use the Blueprint API provided by the Media Output. In this procedure, we'll set up a simple toggle switch in the Level Blueprint that starts and stops capturing when the player presses a key on the keyboard.

The **[Virtual Studio](/documentation/en-us/unreal-engine/virtual-studio-sample-project-in-unreal-engine)** showcase, available on the **Samples** tab of the Epic Games Launcher, contains a UMG interface widget that demonstrates how you could control capturing from an on-screen user interface.

### Steps

1.  From the main toolbar in the Unreal Editor, choose **Blueprints > Open Level Blueprint**.
    
    ![Open Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/855ebcf3-cea0-4050-8e6e-4db74634457c/30-open-level-blueprint_ue5.png "Open Level Blueprint")
2.  We'll need to start from the AJA Media Output Asset that you've created, where you identify the port you want to output to. In the **Variables** list in the **My Blueprint** panel, click the **Add (+)** button to add a new variable.
    
    ![New Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6949f019-fe28-448c-9973-e59e708a24da/31-add-variables_ue5.png "New Variable")
3.  In the **Details** panel, set the **Variable Name** to **AjaMediaOutput**, and use the **Variable Type** drop-down list to make it an **Aja Media Output Object Reference**.
    
    ![Aja Media Output Object Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3571a57-c898-45fb-8667-a211f3daec51/32-select-variable-type_ue5.png "Aja Media Output Object Reference")
4.  Enable the **Instance Editable** setting (1), and compile the Blueprint. Then, in the **Default Value** section, set the variable to point to the AJA Media Output Asset that you created in your Content Browser (2).
    
    ![Set the default value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a723762b-7a80-4bec-b9a0-8246fc4ac0d8/33-details-panel-properties_ue5.png "Set the default value")
5.  Press **Ctrl**, and drag the **AjaMediaOutput** from the Variables list in the **My Blueprint** panel into the **Event Graph**.
    
    ![Control+drag the AjaMediaOutput](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58e50105-89a5-430f-aa42-25bacab6deb6/34-add-aja-output-blueprint_ue5.png "Control+drag the AjaMediaOutput")
6.  Click and drag from the output port of the **AjaMediaOutput** variable node, and choose **Media > Output > Create Media Capture**. 
    
    ![Create Media Capture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36d0d168-2c11-4962-bfa8-4bc179808a88/35-create-media-capture_ue5.png "Create Media Capture")
    
    Hook up your nodes to the **Event BeginPlay** node as shown below:
    
    ![Event Begin Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba00328f-147b-4948-8fec-66c156ec88c3/36-add-event-begin-play_ue5.png "Event Begin Play")
    
    This creates a new Media Capture object from your Aja Media Output. The Media Capture offers two main Blueprint functions that we'll use to control the capturing: **Capture Active Scene Viewport** and **Stop Capture**.
    
7.  First, we'll save the new Media Capture object into its own variable, so we can get access to it again elsewhere. Click and drag from the output port of the **Create Media Capture** node, and choose **Promote to Variable**.
    
    ![Promote to variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/414fb092-618e-42b6-80a0-1c40942f177f/37-promote-to-variable_ue5.png "Promote to variable")
    
    Rename the new variable **MediaCapture** in the Variables list in the **My Blueprint** panel.
    
    It's important to save the Media Capture to a variable here. If you don't, the Unreal Engine's garbage collector may destroy it automatically before you're done with it.
    
8.  Press **Ctrl** and drag the **MediaCapture** variable into the **Event Graph**.
    
    ![Control+drag the MediaCapture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4772947e-0a11-4978-813c-192d83410a98/38-add-media-capture_ue5.png "Control+drag the MediaCapture")
9.  Click and drag from the output port of the **MediaCapture** variable node, and choose **Media > Output > Capture Active Scene Viewport**. Do it again, and choose **Media > Output > Stop Capture**.
    
    ![Start and stop the capture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c4da200-2e24-40ad-b836-fb78df90ac0b/39-add-stop-capture_ue5.png "Start and stop the capture")
10.  Right-click in the **Event Graph** and choose **Input > Keyboard Events > P**.   Click and drag from the **Pressed** output of the **P** node and choose **Flow Control > FlipFlop**. 
    

![FlipFlop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c079738-7764-4449-86c0-8413f7bf2faf/40-add-flipflop_ue5.png "FlipFlop")

1.  Connect the **A** output of the **FlipFlop** node to the input event of the **Capture Active Scene Viewport** node, and connect the **B** output of the **FlipFlop** node to the input event of the **Stop Capture** node, as shown below:

![Connect the nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a549f71-560a-47fb-9c02-8b9077c31d4a/41-add-p-button_ue5.png "Connect the nodes")

1.  Compile and save the Blueprint, and try playing your Project. Click the arrow next to the Play button in the main Toolbar, and choose either the **New Editor Window (PIE)** or **Standalone Game** option.

![Launch the Project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bb11a10-0eac-4fa4-b276-4aadbfedc99b/42-new-editor-window_ue5.png "Launch the Project")

Video capture from the Editor will only work when you play your Project in a **New Editor Window (PIE)** or a **Standalone Game**. It won't work in the default **Selected Viewport** mode, or in **Simulate** mode. In addition, the viewport resolution of your Project (that is, the size of the rendered image the Unreal Engine generates each frame) must match the output resolution set in the active Media Profile, so that it will be the right size for the output video feed.

After your project starts up, you should be able to press the **P** button on your keyboard to toggle sending the output from the Engine to the AJA card.

### End Result

At this point, you should have a basic idea of how to work with Aja Media Sources, Media Bundles, and the Media Capture system, and you should understand how all of these elements work together to get professional video in and out of the Unreal Engine.

## On Your Own

Now that you've seen the basics of how to get a new Project exchanging video input and output with an AJA card, you can continue learning on your own:

-   Explore the in-engine keying solution in the Material Instance created by your Media Bundle. Try passing some green-screen video into your card's input port, and use the keying controls in the Material Instance to remove the background.
-   Explore the **[Virtual Studio](/documentation/en-us/unreal-engine/virtual-studio-sample-project-in-unreal-engine)** showcase to see what it adds to this basic setup, like its on-screen UI that switches cameras and controls video capture at runtime.