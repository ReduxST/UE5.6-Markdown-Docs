# Blackmagic Video I/O Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blackmagic-video-io-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blackmagic-video-io-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 16:10:05

---

In this Quick Start guide, we walk you through the process of setting up an Unreal Engine Project to work with a professional video card from Blackmagic Design. At the end of this guide:

-   You'll have video input from your Blackmagic card playing inside your Unreal Engine Project.
    
-   You'll be able to capture camera viewpoints both from the Editor and from your runtime application, and send them out to an SDI port on your Blackmagic card.
    
-   You'll know where to go when you want to set up more advanced adjustments to your video inputs, such as correcting lens deformation and applying chroma-keying effects.
    

For a working example that shows many of the elements described below put into practice, see the **[Virtual Studio](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-studio-sample-project-in-unreal-engine)** showcase, available on the Samples tab of the Epic Games Launcher.

**Prerequisites:**

-   Make sure that you have a supported card from Blackmagic Design, and that you've installed the necessary drivers and software. For details, see the [Blackmagic Media Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/blackmagic-media-reference-for-unreal-engine) page.
    
-   Make sure that your card is working correctly, and that you have some video input feeding in to at least one of the card's SDI ports.
    
-   Open an Unreal Engine Project that you want to integrate with your video feeds. This page shows the steps in the **Third Person** Blueprint template, but the same steps will work equally well in any Project.
    

The Blackmagic Design components used in this guide are built on top of the [Media Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/media-framework-in-unreal-engine), and we'll use [Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) to script the video capturing process at runtime. Some prior knowledge of these topics is recommended but not required.

## 1 - Set Up the Project

Before you can get video input from your Blackmagic card into your Unreal Engine Level, and send output from the Unreal Engine through one of your Blackmagic card's SDI ports, you'll need to do some basic setup to enable the Blackmagic Media Player Plugin in your Project.

If you started your Unreal Engine Project from one of the Templates in the **Film, Television, and Live Events** category, the necessary plugins may already be enabled for you. If not, follow the instructions below to enable them.

### Steps

1.  Open the Project that you want to use with Blackmagic video I/O in the Unreal Editor.
    
2.  From the main menu, select **Edit > Plugins**.
    
3.  In the **Plugins** window, find the **Blackmagic Media Player** plugin under the **Media Players** category. Check its **Enabled** checkbox.
    
    [![Enable the Blackmagic Media Player Plugin](https://dev.epicgames.com/community/api/documentation/image/f7022833-9dd7-4d17-8963-bcd3f904c448?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f7022833-9dd7-4d17-8963-bcd3f904c448?resizing_type=fit)
    
    Click image to expand.
    
4.  Find the **Media Framework Utilities** Plugin under the **Media** category. Check its **Enabled** checkbox, if it's not already checked.
    
    [![Enable the Media Framework Utilities Plugin](https://dev.epicgames.com/community/api/documentation/image/f54b98fc-659f-4cfe-9f8d-e1e472f42841?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f54b98fc-659f-4cfe-9f8d-e1e472f42841?resizing_type=fit)
    
    Click image to expand.
    
5.  Click **Restart Now** to restart the Unreal Editor and reopen your Project.
    
    [![Restart Now](https://dev.epicgames.com/community/api/documentation/image/7ba742cf-87db-4b25-a961-5684db6e795a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7ba742cf-87db-4b25-a961-5684db6e795a?resizing_type=fit)
    
    Click image to expand.
    

### End Result

Your Project is now ready to accept video from the Blackmagic card, and to send rendered output to the card. In the next sections, we'll hook it up and start playing video in and out.

## 2 - Rendering Video Input in the Unreal Engine

In this process, we'll make video input from the Blackmagic card visible in the current Level in the Unreal Editor. This process uses a Media Bundle: a kind of Asset that packages together several different types of Assets involved in the Media Framework, and that offers you control over some advanced features like lens deformation, chroma-keying, color correction, and more. 

### Steps

1.  In your **Content Browser**, expand the **Sources** panel. Right-click, and choose **New Folder** from the context menu.
    
    [![New Folder](https://dev.epicgames.com/community/api/documentation/image/d77054e2-6471-41ff-a785-fa290cbe7a35?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d77054e2-6471-41ff-a785-fa290cbe7a35?resizing_type=fit)
    
    Rename your new folder **Blackmagic**.
    
2.  Open your new folder, right-click in the **Content Browser** and choose **Media > Media Bundle**.
    
3.  Your new Asset's name is automatically selected in the Content Browser, so you can give it a descriptive name: Type a new name, like **BlackmagicMediaBundle**, and press **Enter**. A new folder of Media Framework Assets is automatically created next to your Media Bundle, named with the suffix **\_InnerAssets**. We'll take a look at these Assets later.
    
4.  Save your new Assets by clicking the **Save All** button in the **Content Browser**.
    
5.  Double-click your new Media Bundle to edit its properties. The Media Bundle is capable of playing video from any kind of media source the Engine supports, so you'll need to tell it that you want to get the video from your Blackmagic card. In the **Media Source** property, select **Blackmagic Media Source** from the drop-down list:
    
    [![Set the Blackmagic Media Source](https://dev.epicgames.com/community/api/documentation/image/25f2252f-899b-4c29-a3b6-873d93be3b79?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/25f2252f-899b-4c29-a3b6-873d93be3b79?resizing_type=fit)
    
    Click image to expand.
    
6.  Once you've identified the type of Media Source you want the Media Bundle to handle, you can then set up any configuration properties offered by that type of source.  You can make Unreal Engine automatically match the format and framerate of the incoming video signal. To enable automatic format detection, click the **Configuration** dropdown, enable **Auto**, and then click **Apply**. The engine now seamlessly handles changes and restarts automatically if the signal is temporarily lost.
    
    [![Blackmagic Media Source Configuration](https://dev.epicgames.com/community/api/documentation/image/740f7e02-b79a-498d-955a-93dbfe7a6962?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/740f7e02-b79a-498d-955a-93dbfe7a6962?resizing_type=fit)
    
    Click image to expand.
    
    The options you see may vary depending on the devices you have installed. For details on all of the properties you can set for a Blackmagic Media Source, see the [Blackmagic Media Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/blackmagic-media-reference-for-unreal-engine) page.
    
7.  If you want to apply any compensation to the incoming video to account for lens distortion, you can set up the physical properties of the lens in the **Lens Parameters** section. 
    
    [![Lens undistortion parameters](https://dev.epicgames.com/community/api/documentation/image/c26a3690-df59-47b2-a2b5-ba42b7ed7e2c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c26a3690-df59-47b2-a2b5-ba42b7ed7e2c?resizing_type=fit)
    
    Click image to expand.
    
    These Lens Parameters just set up the physical properties of the lens. You'll actually activate the lens compensation later, when you edit the Material Instance used by the Media Bundle. Save and close your Media Bundle when you're done setting up its properties.
    
8.  Drag your **BlackmagicMediaBundle** Asset from the **Content Browser** into the Level Viewport. 
    
    [![Drag and drop the Media Bundle](https://dev.epicgames.com/community/api/documentation/image/980f8b9c-cdc0-415c-af0b-486097881524?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/980f8b9c-cdc0-415c-af0b-486097881524?resizing_type=fit)
    
    Click image to expand.
    
    You'll see a new plane appear, showing the video currently being played over the port configured for your Media Bundle. Use the transform tools in the Viewport toolbar to move, rotate, and resize it. If your Media Bundle doesn't start playing automatically, select it, then click the **Media Bundle > Request Play Media** button in the **Details** panel.
    
9.  Now, we'll see how to apply keying and compositing effects to the video stream. Back in the Media Bundle Editor, click the **Open Material Editor** button in the Toolbar to edit the Material Instance that this Media Bundle uses to draw its incoming video feed on to an object in the Level.
    
    [![Open Material Editor](https://dev.epicgames.com/community/api/documentation/image/143010f5-de88-45d4-869f-e646052c8495?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/143010f5-de88-45d4-869f-e646052c8495?resizing_type=fit)
    
    This Material Instance is saved inside the **BlackmagicMediaBundle\_InnerAssets** folder that was created automatically with your Media Bundle.
    
    [![Material Instance](https://dev.epicgames.com/community/api/documentation/image/8522160e-eac2-4155-9451-253e4308a714?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8522160e-eac2-4155-9451-253e4308a714?resizing_type=fit)
    
    Click image to expand.
    
10.  In the Material Instance Editor, you'll see a number of properties exposed for you to configure keying, cropping, and color correction, and to activate correcting for the lens distortion that you set up in the Media Bundle.
    
    [![Material Instance Editor](https://dev.epicgames.com/community/api/documentation/image/614a3c1b-a0f9-470a-97b3-7786397b1842?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/614a3c1b-a0f9-470a-97b3-7786397b1842?resizing_type=fit)
    
    Click image to expand.
    
    While you adjust the settings in the Material Instance Editor, you can see the effect of your changes on the video feed playing back in the main Level Viewport.
    
    You may find it more convenient to see the effects of the changes you make in the preview panel of the Material Instance Editor instead. To do this, temporarily enable the **IsValid** setting, and set its value to `1.0`.
    
    [![IsValid](https://dev.epicgames.com/community/api/documentation/image/62b94c66-261c-4a54-a673-03b5ffdc3631?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/62b94c66-261c-4a54-a673-03b5ffdc3631?resizing_type=fit)
    
    Click the arrow at the top left of the viewport toolbar, and enable the **Realtime** option in the menu.
    
    [![Realtime viewport](https://dev.epicgames.com/community/api/documentation/image/e83a94d8-f0f7-4642-a69f-3d9291ad9fa8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e83a94d8-f0f7-4642-a69f-3d9291ad9fa8?resizing_type=fit)
    
    You'll be able to judge the effect of your changes more easily by changing the preview mesh to a plane or a cube. Use the controls at the bottom of the viewport:
    
    [![Preview mesh](https://dev.epicgames.com/community/api/documentation/image/4a948937-866d-4f28-8f7b-da7ab102794e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4a948937-866d-4f28-8f7b-da7ab102794e?resizing_type=fit)
    
    When you're done, return the **IsValid** setting to its previous value.
    
11.  When you're done changing the Material Instance properties, click the **Save** button in the Toolbar.
    

### End Result

At this point, you should have video playing over an SDI port showing up inside your Unreal Engine Level, and you should understand where to set up more advanced features like lens deformation and chroma-keying.

If you're already familiar with the Media Framework, another way you could get video into your Level is to create a new **BlackmagicMediaSource** Asset in your Project, and set it up with the same source properties you set up inside the Media Bundle in the procedure above. Then, create your own **MediaPlayer** and **MediaTexture** Assets to handle the playback of that source in your Level. For details, see the [Media Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/media-framework-in-unreal-engine) documentation. However, we recommend using the Media Bundle, as shown above, to get the best balance between ease of use and professional quality video features.

## 3 - Output Captures from the Unreal Editor

In this process, you'll set up an Blackmagic Media Output object, and use the **Media Captures** panel in the Unreal Editor to output the view from selected cameras in the Level to your Blackmagic card.

### Steps

1.  Right-click in the Content Browser, and select **Media > Blackmagic Media Output**. 
    
    [![New Blackmagic Media Output](https://dev.epicgames.com/community/api/documentation/image/3d83c443-bbe9-4e18-8f36-a23283bb325f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3d83c443-bbe9-4e18-8f36-a23283bb325f?resizing_type=fit)
    
    Click image to expand.
    
    Name your new Asset **BlackmagicMediaOutput**.
    
2.  Double-click your new Asset to open it up for editing. Just like when you created your Blackmagic Media Source, you have to set up the **Configuration** property to control the properties of the video feed that the Unreal Engine sends to your Blackmagic card. Click the arrow to open the submenu, select the options that match your video setup, then click **Apply** in the submenu. 
    
    [![Blackmagic Media Output Configuration](https://dev.epicgames.com/community/api/documentation/image/60a4f0f1-3a62-43c3-8586-1b41275be3c8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/60a4f0f1-3a62-43c3-8586-1b41275be3c8?resizing_type=fit)
    
    Click image to expand.
    
    The options you see may vary depending on the devices you have installed. For details on all of the properties you can set in the Blackmagic Media Output, see the [Blackmagic Media Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/blackmagic-media-reference-for-unreal-engine) page. Save and close your Media Output when you're done.
    
3.  Now we'll place two cameras in the Level, to give us viewpoints for the output we'll send to the Blackmagic card. In the **Place Actors** panel, open the **Cinematic** tab, and drag two instances of the **Cine Camera Actor** into the viewport.
    
    [![Drag and drop Cine Camera Actors](https://dev.epicgames.com/community/api/documentation/image/2c75eab4-f940-46e7-a493-f179b4672674?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2c75eab4-f940-46e7-a493-f179b4672674?resizing_type=fit)
    
    Place the cameras where you want them in the Level, so that they're showing different viewpoints on the scene.
    
    **Piloting** the camera is a fast and easy way to set its viewpoint exactly the way you want it. See [Pilot Actors in the Viewport](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine).
    
4.  From the main menu, choose **Window > Virtual Production > Media Capture**. You'll use the **Media Capture** window to control when the Editor sends output to your Blackmagic device, and what camera it should use in the Level.
    
    [![Media Capture window](https://dev.epicgames.com/community/api/documentation/image/6a86ac89-3b13-4b48-9cd3-42706b86b0dc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6a86ac89-3b13-4b48-9cd3-42706b86b0dc?resizing_type=fit)
    
5.  Under the **Media Viewport Capture** area, find the **Viewport Captures** control. Click the **Add (+)** button to add a new capture to this list.
    
    [![Add a viewport capture](https://dev.epicgames.com/community/api/documentation/image/2f42b7d2-27f7-46de-b79f-ad181f820154?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2f42b7d2-27f7-46de-b79f-ad181f820154?resizing_type=fit)
    
6.  Expand the new entry. First, we'll add the cameras that we want to capture from. In the **Locked Camera Actors** control, click the **Add (+)** button to add a new entry.
    
    [![Add a camera actor](https://dev.epicgames.com/community/api/documentation/image/6b22f980-6b4a-4306-82fc-0a72d041ac72?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b22f980-6b4a-4306-82fc-0a72d041ac72?resizing_type=fit)
    
    Then, use the drop-down list to choose one of the cameras you placed in the Level.
    
    [![Select the camera actor](https://dev.epicgames.com/community/api/documentation/image/e92be720-84cd-4f86-81e5-05803fa83097?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e92be720-84cd-4f86-81e5-05803fa83097?resizing_type=fit)
    
    Repeat the same steps to add the other camera to the list.
    
7.  Now, set up the output that you want to capture these cameras to. Set the **Media Output** control to point to the new Blackmagic Media Output Asset that you created above. You can do this by selecting it in the drop-down list, or drag your Blackmagic Media Output Asset from the Content Browser and drop it into this slot.
    
    [![Set the Blackmagic Media Output](https://dev.epicgames.com/community/api/documentation/image/6db09756-83bd-4862-b2a7-8fa1bc9d7c67?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6db09756-83bd-4862-b2a7-8fa1bc9d7c67?resizing_type=fit)
    
8.  At the top of the window, click the **Capture** button.
    
    [![Start capturing](https://dev.epicgames.com/community/api/documentation/image/71b078e0-a6d9-411a-aed4-fcf583c87b98?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/71b078e0-a6d9-411a-aed4-fcf583c87b98?resizing_type=fit)
    
    You'll see a new frame at the bottom of the window that shows a preview of the output being sent to the Blackmagic card. If you have this port hooked up to another downstream device, you should start to see the output coming through.
    
    [![Active Media Capture](https://dev.epicgames.com/community/api/documentation/image/222e0227-bc76-42d3-ad2f-ab2318ebb0a4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/222e0227-bc76-42d3-ad2f-ab2318ebb0a4?resizing_type=fit)
    
9.  Each camera that you added to the Locked Camera Actors list for this viewport capture is represented by a corresponding button above the video preview. Click the buttons to switch the capture back and forth between the two views.
    
    [![Switch Cameras](https://dev.epicgames.com/community/api/documentation/image/9b63109a-4c6d-4b8e-8cca-762e760fc11b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b63109a-4c6d-4b8e-8cca-762e760fc11b?resizing_type=fit)
    
    Click image to expand.
    

### End Result

Now you've set up the Unreal Editor to stream output from cameras in your Level to a port on your Blackmagic card. Next, we'll see how to use Blueprint scripting to do the same thing in a running Unreal Engine Project.

## 4 - Output Captures at Runtime

The **Media Capture** window that you used in the last section is a practical and easy way to send captures to the Blackmagic card. However, it only works inside the Unreal Editor. To do the same thing when you're running your Project as a standalone application, you'll need to use the Blueprint API provided by the Media Output. In this procedure, we'll set up a simple toggle switch in the Level Blueprint that starts and stops capturing when the player presses a key on the keyboard.

The **[Virtual Studio](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-studio-sample-project-in-unreal-engine)** showcase, available on the **Samples** tab of the Epic Games Launcher, contains a UMG interface widget that demonstrates how you could control capturing from an on-screen user interface.

### Steps

1.  From the main toolbar in the Unreal Editor, choose **Blueprints > Open Level Blueprint**.
    
    [![Open Level Blueprint](https://dev.epicgames.com/community/api/documentation/image/f0db56fc-efa5-4fa7-a558-acaf907d6f26?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f0db56fc-efa5-4fa7-a558-acaf907d6f26?resizing_type=fit)
    
2.  We'll need to start from the Blackmagic Media Output Asset that you've created, where you identify the port you want to output to. In the **Variables** list in the **My Blueprint** panel, click the **Add (+)** button to add a new variable.
    
    [![New Variable](https://dev.epicgames.com/community/api/documentation/image/941a985f-d2e2-4c2a-995f-89e13efc6834?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/941a985f-d2e2-4c2a-995f-89e13efc6834?resizing_type=fit)
    
3.  In the **Details** panel, set the **Variable Name** to **BlackmagicMediaOutput**, and use the **Variable Type** drop-down list to make it a **Blackmagic Media Output Object Reference**.
    
4.  Enable the **Instance Editable** setting (1), and compile the Blueprint. Then, in the **Default Value** section, set the variable to point to the Blackmagic Media Output Asset that you created in your Content Browser (2).
    
5.  Press **Ctrl**, and drag the **BlackmagicMediaOutput** from the Variables list in the **My Blueprint** panel into the **Event Graph**.
    
    [![Control+drag the BlackmagicMediaOutput](https://dev.epicgames.com/community/api/documentation/image/901e96bc-ea00-44d1-ad7e-fcf9ae7e1925?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/901e96bc-ea00-44d1-ad7e-fcf9ae7e1925?resizing_type=fit)
    
6.  Click and drag from the output port of the **BlackmagicMediaOutput** variable node, and choose **Media > Output > Create Media Capture**. 
    
    [![Create Media Capture](https://dev.epicgames.com/community/api/documentation/image/4ec88034-fc8d-41ef-9bb0-4214c7eaee74?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4ec88034-fc8d-41ef-9bb0-4214c7eaee74?resizing_type=fit)
    
    Hook up your nodes to the **Event BeginPlay** node as shown below:
    
    [![Event Begin Play](https://dev.epicgames.com/community/api/documentation/image/942f1975-d59b-4164-a0bf-af23c4a497c4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/942f1975-d59b-4164-a0bf-af23c4a497c4?resizing_type=fit)
    
    This creates a new Media Capture object from your Blackmagic Media Output. The Media Capture offers two main Blueprint functions that we'll use to control the capturing: **Capture Active Scene Viewport** and **Stop Capture**.
    
7.  First, we'll save the new Media Capture object into its own variable, so we can get access to it again elsewhere. Click and drag from the output port of the **Create Media Capture** node, and choose **Promote to Variable**.
    
    [![Promote to variable](https://dev.epicgames.com/community/api/documentation/image/83b4e400-ae03-49e2-8d9b-9f4bb0cce454?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/83b4e400-ae03-49e2-8d9b-9f4bb0cce454?resizing_type=fit)
    
    Rename the new variable **MediaCapture** in the Variables list in the **My Blueprint** panel.
    
    It's important to save the Media Capture to a variable here. If you don't, the Unreal Engine's garbage collector may destroy it automatically before you're done with it.
    
8.  Press **Ctrl** and drag the **MediaCapture** variable into the **Event Graph**.
    
    [![Control+drag the MediaCapture](https://dev.epicgames.com/community/api/documentation/image/cee1a9d9-1bab-48b9-ae02-e0ef96fac99d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cee1a9d9-1bab-48b9-ae02-e0ef96fac99d?resizing_type=fit)
    
9.  Click and drag from the output port of the **MediaCapture** variable node, and choose **Media > Output > Capture Active Scene Viewport**. Do it again, and choose **Media > Output > Stop Capture**.
    
    [![Start and stop capture](https://dev.epicgames.com/community/api/documentation/image/cced1fcb-2c77-479f-beaa-129e8f2149c8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cced1fcb-2c77-479f-beaa-129e8f2149c8?resizing_type=fit)
    
10.  Right-click in the **Event Graph** and choose **Input > Keyboard Events > P**.   Click and drag from the **Pressed** output of the **P** node and choose **Flow Control > FlipFlop**. 
    
    [![FlipFlop](https://dev.epicgames.com/community/api/documentation/image/85081b35-fa80-49df-96fe-c08856bdd7d7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/85081b35-fa80-49df-96fe-c08856bdd7d7?resizing_type=fit)
    
11.  Connect the **A** output of the **FlipFlop** node to the input event of the **Capture Active Scene Viewport** node, and connect the **B** output of the **FlipFlop** node to the input event of the **Stop Capture** node, as shown below:
    
    [![Connect the nodes](https://dev.epicgames.com/community/api/documentation/image/56274139-92e1-4d63-ba5b-1b4d49fac098?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/56274139-92e1-4d63-ba5b-1b4d49fac098?resizing_type=fit)
    
12.  Compile and save the Blueprint, and try playing your Project. Click the arrow next to the Play button in the main Toolbar, and choose either the **New Editor Window (PIE)** or **Standalone Game** option.
    
    [![Launch the Project](https://dev.epicgames.com/community/api/documentation/image/da7f0cc8-6a79-4097-bfed-74ccd3a66e8b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/da7f0cc8-6a79-4097-bfed-74ccd3a66e8b?resizing_type=fit)
    

Video capture from the Editor will only work when you play your Project in a **New Editor Window (PIE)** or a **Standalone Game**. It won't work in the default **Selected Viewport** mode, or in **Simulate** mode. In addition, the viewport resolution of your Project (that is, the size of the rendered image the Unreal Engine generates each frame) must match the output resolution set in the active Media Profile, so that it will be the right size for the output video feed.

After your project starts up, you should be able to press the **P** button on your keyboard to toggle sending the output from the Engine to the Blackmagic card.

### End Result

At this point, you should have a basic idea of how to work with Blackmagic Media Sources, Media Bundles, and the Media Capture system, and you should understand how all of these elements work together to get professional video in and out of the Unreal Engine.

## On Your Own

Now that you've seen the basics of how to get a new Project exchanging video input and output with a Blackmagic card, you can continue learning on your own:

-   Explore the in-engine keying solution in the Material Instance created by your Media Bundle. Try passing some green-screen video into your card's input port, and use the keying controls in the Material Instance to remove the background.
    
-   Explore the **[Virtual Studio](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-studio-sample-project-in-unreal-engine)** showcase to see what it adds to this basic setup, like its on-screen UI that switches cameras and controls video capture at runtime.