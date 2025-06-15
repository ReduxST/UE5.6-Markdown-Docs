# Experimental Pixel Streaming Features

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/experimental-pixel-streaming-features](https://dev.epicgames.com/documentation/en-us/unreal-engine/experimental-pixel-streaming-features)  
**Processed:** 2025-06-14 16:22:44

---

The below features are exciting new tools we've implemented into Pixel Streaming. Though they provide new possibilities, it's important to note that these are unstable and should be used with caution. We recommend you do not build critical components of your product on them as they may change or be removed in subsequent releases of Unreal Engine.

## VCam

VCam is a new feature that allows you to use the new VCam actor to stream the video content of the Level Viewport to an output provider.

At this stage, VCam is mostly intended for virtual production use cases. It can be paired with the Live Link VCam iOS application and used for ARKit tracking. This is useful for piloting virtual cameras in Unreal Engine, with Pixel Streaming handling touch events and streaming the Level Viewport as real-time video feedback to the iOS device. For more information on Live Link VCam, please head to this site here: [iOS Live Link VCam](https://apps.apple.com/us/app/live-link-vcam/id1547309663)

### How to use VCam

1.  Ensure you have the Virtual Camera plugin enabled.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa388b4b-5b50-4b75-88ff-8ef27f509926/vcamplugin.jpg)
2.  Add the VCam actor, found under Virtual Production.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ffeee70-c710-48e1-9d3a-69993f88018a/vcamactor.png)
3.  As soon as you add the actor, you'll be presented with the view of the VCam as shown below:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86a482b1-0041-40ae-ae55-9cccfaf06eb3/vcamadded.png)
4.  As soon as the actor is added, it will start streaming. You can start and stop this via the Pixel Streaming Toolbar.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16b9b2b1-626e-4271-b71c-13e4685f63e2/streamingvcam.png)
5.  Once started, open a local browser and navigate to 127.0.0.1 to see your streamed display, or open the Live Link iOS application and navigate to your computer's IP address and hit connect.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93e0ed2c-c595-4d15-8480-b071d3830602/vcambrowser.png)

If you want to interact with the stream through the browser, open the control panel in-browser and change the Control Scheme to Hovering.

## Use Microphone

With Pixel Streaming, you can now allow in-engine playback of a particular peer / player microphone using WebRTC audio through the web browser.

### Setting up Use Microphone in Project

Making your project microphone compatible is extremely simple and only requires a single addition to your project.

1.  Enable the Pixel Streaming Plugin.
    
2.  On any Actor in scene, add the `PixelStreamingAudio` component. You can leave its settings as the default.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/030289ae-92f9-4c11-9119-08801378059b/psaudiocomponent.jpg)

Each audio component associates itself with a particular Pixel Streaming player/peer (using the the Pixel Streaming Player ID)

### Using Microphone in Stream

1.  Once your project is set up with the `PixelStreamingAudio` component, run your application as per usual for Pixel Streaming (packaged or standalone with Pixel Streaming launch args) and launch your signalling server.
    
2.  Connect to your signalling server via web browser.
    
3.  Open the frontend settings panel and set `Use Mic` to `true`. Click **Restart** at the bottom to reconnect.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e52e3fd-0fd3-4db9-b49e-51b18a4b0b7d/usemic.jpg) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b262ada9-b191-4ffd-abfd-819052e8ebc1/restartstream.jpg)
4.  Your browser may ask permission to use your microphone, ensure you allow access.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d81a9d26-8ae7-4f2e-b4b7-7471041a958e/micperm.jpg)
5.  Speak into your microphone, you should hear your voice played back through the stream!
    

For cloud streaming you’ll need HTTPS set up for this to work, see steps to create a HTTPS certificate in the VR guide below. Additionally, Firefox requires HTTPS for successful microphone capture in both local and cloud deployments.

## Pixel Streaming in Virtual Reality

Virtual Reality (VR) Pixel Streaming is a new feature that provides users with the means to connect to a VR-compatible application using Pixel Streaming. This allows users to enjoy a VR experience with their own headsets, without running a local application.

### Setting Up the Project

For this example, we'll use the Virtual Reality template project.

1.  Create a new project using the Virtual Reality template.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a4c1564-675f-49d8-806b-bd9ca7403cce/vrproject.jpg)
2.  Enable the Pixel Streaming plugin and disable the OpenXR plugin. Restart the editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dcc3ac5-00b6-4cbb-a874-711e62789d6f/openxrplugin.jpg)  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5c6cf11-1d57-4bf3-9b77-c6ab77e720cc/pixelstreamingplugin.jpg)
    
3.  In the Content Browser, search for "Asset\_Guideline" and delete "B\_AssetGuideline\_VRTemplate". When prompted, click **Force Delete**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b9668ed-44f1-46b8-bf45-fc5a2da1420e/assetguideline.jpg) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f771447-5518-40ae-ad88-b9abfe80fa5c/assetforcedelete.jpg)
4.  Now search for "VRPawn" in the Content Browser. Double-click the VRPawn to open it, then compile the Blueprint. If working properly it should compile successfully. Save and close this Blueprint.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75181e44-42b0-46e6-8acf-d3f03a3dbdcc/vrpawn.jpg)
5.  Open **Editor Preferences > Level Editor > Play** and add `-PixelStreamingURL=ws://127.0.0.1:8888 -PixelStreamingEnableHMD -ResY=1080`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52de34b0-fc8a-4efb-988d-5b8eee6e7849/launchargsvr.jpg)

You only need to specify the vertical resolution, as the horizontal resolution automatically adjusts to suit the device's aspect ratio. Set the best resolution for your performance-to-quality ratio.

### Creating the Required Certificates

You need a HTTPS certificate to use VR with Pixel Streaming. This is due to the fact that the standard for WebXR requires that the API is only available to sites loaded over a secure connection (HTTPS). For production use, you will need to use a secure origin to support WebXR. You can find extra information on these requirements here: [https://developer.oculus.com/documentation/web/port-vr-xr/#https-is-required](https://developer.oculus.com/documentation/web/port-vr-xr/#https-is-required).

For this example, we'll be setting up a basic certificate via Gitbash. If you don't have Gitbash installed prior, head to this page here for steps on how to install Gitbash: [https://www.atlassian.com/git/tutorials/git-bash](https://www.atlassian.com/git/tutorials/git-bash).

1.  Create a `certificates` folder inside the `SignallingWebServer` directory, as shown below:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48ec513f-e4c6-4954-ada4-b89beaf48ebd/certificatesfolder.jpg)
2.  Right click inside the `certificates` directory and open Gitbash. Type in `openssl req -x509 -newkey rsa:4096 -keyout client-key.pem -out client-cert.pem -sha256 -nodes`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5f7a746-4579-4b4e-8058-cb981b3f47c5/gitbashcert.jpg)
3.  Press Enter multiple times, until the command is complete. You'll know it's done when done as it will have created 2 `.pem` files in the certificates folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/545ecc98-589a-4cad-a3c0-a7d50e64823f/pemfiles.jpg)
4.  Open the `config.json` file found in the `SignallingWebServer` folder, set the `https` value to `true`. If the `config.json` file is missing, runt he signalling server once.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dad6b141-bbc5-4739-a30d-193a75f59623/httptrue.jpg)

You should now be ready to run and test your VR application!

The certificate created above is only for testing purposes. For full cloud deployment, you will need to organize a proper certificate.

### Joining the VR Stream

For this example, we'll be using the Meta Quest 2.

1.  Start the `start_with_stun.bat` script found in `\SignallingWebServer\platform_scripts\cmd`
    
2.  Going back to the editor, run the application standalone. As you added the launch args in previous steps, it should connect to the signalling server once it's fully started up.
    
3.  Now using your VR headset, open the web browser and enter your computer's IP address. You'll be presented with a "Connection not secure" page, open the "Advanced" tab and click "Proceed to IP"
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8203c456-b0be-4630-813e-2b248be67a3e/notsafecert.jpg)
4.  You should see the application streamed to two views in the browser window. Click the XR button on the left to switch to VR.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94e8125b-98d1-4026-bd49-5111580b5e2e/xrbutton.jpg)
5.  Done! You should now be in your Pixel Streamed VR project!
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/236278df-a5a7-4cc7-82a4-61c851ced46c/invr.jpg)

## Pixel Streaming Player

The Pixel Streaming Player allows you to display active Pixel Streams within your Unreal Engine project on a display within 3D space. With this, you can display cloud-hosted content as a media source within local applications.

The Pixel Streaming Player is an experimental feature with an API currently under development. As of 5.4, the Pixel Streaming Player is compatible with H264, VPX, and AV1 encoders.

Setting up the Pixel Streaming Player has changed in Pixel Streaming 2. For more information, please refer to [Pixel Streaming 2 Overview](/documentation/en-us/unreal-engine/pixel-streaming-2-overview-in-unreal-engine).

### Setting up your Pixel Streaming Player

1.  Enable the Pixel Streaming and Pixel Streaming Player plugins.
    
2.  Create a new **Blueprint** class (Actor). Save and name this anything you like.
    
3.  Open the new Blueprint class and add two components, **PixelStreamingSignalling** and **PixelStreamingPeer**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7044f7d0-b7aa-446c-9753-2e94dd02e707/addcomponentpsplay.jpg)
4.  Drag the **PixelStreamingSignalling** component into the event graph. Drag off from this node and create a **Connect** node. Connect **BeginPlay** to the input of the new node and enter "ws://127.0.0.1:80" into the URL value. Adding the port to the URL field is importing, as the Pixel Streaming Player may not automatically connect to the right port. For Windows, the port is 80, but for Linux, use port 8080.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77fd4a3b-dae6-497f-8100-175e4959a538/beginconnectnode.jpg)
5.  Select the PixelStreamingSignalling component and add: **On Connected**, **On Config**, **On Offer**, and **On Ice Candidate** events from the **Details** window. Add the **On Ice Candidate** event from the PixelStreamingPeer node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4dc118a9-b8ff-417d-99b8-daffe3a6f5bd/addeventsps.jpg)
6.  From **On Connected**, drag and create a **Get Streamer ID List** node, then drag again from its output and create a **Subscribe** node. Ensure you attach **Pixel Streaming Signalling** to the **Signalling Component** and **Target** inputs as shown below. Drag from the **Streamer List** output, and create a **Get (a ref)** node and connect it to the **Streamer ID** input.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fa2eeff-5540-4387-ae16-6068b96abfc6/onconnected.png)
7.  From **On Config (PixelStreamingSignalling)** node, drag and create **Set Config (Pixel Streaming Peer)**. Ensure the config values are connected between **Set Config** and **On Config**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bebd4e7a-bd9d-444f-a906-38cd995a7db2/onconfigss.jpg)
8.  From **On Offer (PixelStreamingSignalling)**, drag and create **Create Answer**. Ensure the offer values are connected between **Offer** and **Create Answer**. From the out node of **Create Answer**, drag and create **Send Answer** node. Ensure the **Return Value** of **Create Answer** connects to the answer value of **Send Answer**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25d74c2d-1d85-40a3-94fb-2fd141936afa/sendanswerps.jpg)
9.  From **On Ice Candidate (PixelStreamingSignalling)**, Drag and create **Receive Ice Candidate** and connect the candidate values.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b916357b-4277-4ef4-ba5e-95f512f26e18/icecandss.jpg)
10.  From **On Ice Candidate (PixelStreamingPeer)**, drag and create a **Send Ice Candidate** node. Connect the candidate values.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7cd1c0d-1fd8-4204-a88d-999868a53d5a/sendicecand.jpg)
11.  If the above is done correctly, your finished blueprint should look like this:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eca893a9-0e05-4788-990d-96f4c3169031/psplayerbp.jpg)
12.  Select the **PixelStreamingPeer** component in the **Components** window on the left. In the **Details** window under **Properties**, you should see **Pixel Streaming Video Sink**. Select the dropdown and choose **Pixel Streaming Media Texture**. Name and save accordingly.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dc86bf6-9933-425d-bd55-c8c57582927d/mediatexture.jpg)
13.  Drag your blueprint actor into the scene. Create a simple plane object and then resize and shape it into a suitable display.
    
14.  Drag your saved Pixel Streaming media texture directly from the **Content Browser** onto the plane in the scene. This will automatically create a material and apply it to the object.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d672d908-4e8e-41ee-9834-d3893f302112/mediavideotexture.jpg)
15.  Play your scene. You should now see your external Pixel Stream displayed on the plane in your scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b0ebfa6-16c1-4e30-95d8-662b6bb083e5/psplayer.jpg)