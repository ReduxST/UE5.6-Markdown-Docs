# Play a Video Stream

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/play-a-video-stream-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/play-a-video-stream-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:31

---

A **Stream Media Source** is an asset that enables you to stream a video in the [supported URL](/documentation/en-us/unreal-engine/media-framework-technical-reference-for-unreal-engine) format inside Unreal Engine 5 (UE5). With the stream defined, you can load it up and play it inside UE5 with a **Media Player** asset and (with an associated **Media Texture**) can assign it to various aspects of your level.

The stream can be loaded and played as part of a UI element, played fullscreen or even applied to a Static Mesh (such as a TV) and played inside your level.

For this how-to, we use [Unreal Motion Graphics](/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine) (UMG) to create a UI element that will play a streamed video fullscreen.

You don't need to use C++ for this how-to.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1a13df8-5e1e-44e2-b406-49aae023270c/00-hero-stream_ue5.png)

## Recommended Setup

For this how-to we are using the **Blueprint Third Person Template** project with **Starter Content** enabled.

## 1\. Creating the Streaming Media Source and Texture

1.  In the **Content Browser** expand the **Sources Panel** and create a new folder called **Media** inside the **Content** folder.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd3fb9cf-3537-46d0-87a5-03e87e8d219b/01-media-folder_ue5.png)
2.  Right-click inside the empty Media folder, then under **Media**, select **Stream Media Source** and name the asset **MediaStream**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0ec8796-26f4-46b2-ae39-7ecc382a2fa5/02-stream-media-source_ue5.png)
3.  Open **MediaStream** then enter your desired **Stream URL**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0b8e26b-3a17-4da6-8c01-e60599989778/03-stream-url_ue5.png)
    
    If you do not have a URL file to link to, right-click this [Sample Video](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/c62af338-08e2-4f09-a9e7-4193c623f42b/samplevideo.mp4) and copy the link address and paste it in the Stream URL field.
    
    Your Stream URL must link directly to a supported format in order to play the video. For example, PS4Media (PS4) only supports MP4 through HLS in the latest engine version, while WmfMedia (Windows) can support a number of other stream sources. For further information on supported formats per platform/player plug-in, see the [Media Framework Technical Reference](/documentation/en-us/unreal-engine/media-framework-technical-reference-for-unreal-engine) page.
    
4.  Right-click inside the Media folder, then under **Media**, select the **Media Player** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d99f31cb-f2a6-4e09-ba90-67565cd88ee3/04-add-media-player_ue5.png)
5.  In the **Create Media Player** window, enable **Video output Media Texture asset** then click **Ok**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d34ae4c-1e99-4fca-a66a-88e1c5f1a049/05-video-output-asset_ue5.png)
    
    This will automatically create and associate a Media Texture asset linked to this **Media Player** asset which is needed for playback.
    
6.  Name the new Media Player Asset **MyPlayer** which will automatically be applied to the created **Media Texture** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/608ca6a4-8e31-461b-89f2-25a8e92d4121/06-media-player_ue5.png)
    
    If you are using the **Electra Media Player**, open the newly created Media Texture asset in the Editor. In the Details panel:
    
    -   Enable **Enable new style output**.
    -   Set **Output format (new style)** to **Default (sRGB)**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7375918-0e75-4c69-ba25-d1410e1775da/07-enable-new-style-output_ue5.png)

## 2\. Associating the Media Source With a Material

1.  In the Media folder, create a new **Material** and call it **MyPlayer\_Material**.
    
    ![New material that will be used for the streaming media source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9e4d6ed-68ab-4e0c-b9c9-1c59223dcc34/07-my-player-material_ue5.png)
2.  Open **MyPlayer\_Material** and change its **Material Domain** to **User Interface**. This will change the Result node so that it has user interface outputs.
    
    ![Material domain set to User Interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a894bbb2-4f21-45c2-94e2-cb960577d343/08-material-domain_ue5.png)
3.  Click and drag **MyPlayer\_Video** from the Content Browser into the graph for **MyPlayer\_Material**. This will create a **Texture Sample** node with MyPlayer\_Video as the source.
    
4.  Connect the **RGB** pin to the **Final Color** input for your material.
    
    ![Final material using streaming media source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2974fb65-362b-427d-8317-bbde82de9feb/09-add-texture-sample_ue5.png)
    
    If you are using a Texture Sample or Texture Object with the Electra Media Player, you will need to set the **Sampler Type** to **Color**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8b2fa97-5607-4a8f-b947-276a58d86559/10-sampler-type-color_ue5.png)

## 3\. Adding the Media Source to a User Interface Widget

1.  Right-click in the Media folder, then under **User Interface** select **Widget Blueprint** and call it **HUD**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/226880b9-45a4-45f3-8581-f05813f4e3b2/11-widget-blueprint_ue5.png)
    
    A **Widget Blueprint** is an asset that is used with [UMG](/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine) to create UI elements within Unreal Engine which we will apply our streaming video to.
    
2.  Inside the **HUD** Widget Blueprint, from the **Palette** window drag an **Canvas Panel** into the graph and stretch it to fill the grid's aspect ratio.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af292ae0-be9a-4d3e-a5a0-9f7c2f963c13/12-add-canvas-panel_ue5.png)
3.  From the **Palette** window drag an **Image** into the graph inside **Canvas Panel** and stretch it to fit.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4f8eda8-a373-4e44-ad6b-90c67a149013/13-add-image-canvas_ue5.png)
    
    We are going to apply our Media Texture to this image, and the image will fill the player's viewport when playing the game (creating a video that will play fullscreen).
    
4.  In the **Details** panel for the **Image** under **Appearance** expand **Brush** then set the **Image** to **MyPlayer\_Material**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4059b86-d128-4100-9cd3-510712b5be1a/14-image-my-player-material_ue5.png)
5.  In the **Details** panel for the **Image** under **Slot**, click the **Anchors** dropdown and select the anchor middle option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cda9e06-ebdf-48b6-a3dc-abaef76d8014/15-add-anchors_ue5.png)
    
    This will ensure that the image stays fixed in the center of the viewport regardless of viewport size.
    

## 4\. Playing the Media Source

1.  Close the **HUD** Widget Blueprint, then from the Level Editor Toolbar, select **Blueprints** and **Open Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75c882f3-e91c-4a4e-8fef-6f9df624aca8/16-open-level-blueprint_ue5.png)
2.  Create a new variable called **MediaPlayer** of the **Media Player Reference** type and set the **Default Value** to your **MyPlayer** Media Player asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d91de7db-0f7b-457d-81d0-709294d0c40d/17-variables-media-player_ue5.png)
    
    You may need to click **Compile** in order to see the Default Value of your **MediaPlayer** variable.
    
3.  Hold **Ctrl** and drag the **MediaPlayer** variable into the graph to create a **Get** node for this variable, then right-click and add an **Event Begin Play** node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17022cab-7e03-4acc-ae9e-70b234351751/18-add-media-player-blueprint_ue5.png)
    
    When our game starts, we will go through the process of creating and displaying our **HUD**, set up sound for our stream, then open our stream so that it plays.
    
4.  Right-click and add a **Create Widget** node and set **Class** to **HUD**, then off the **Return Value** use **Add to Viewport** and connect as shown.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/549e838e-b909-497b-ac6b-b8154da4d9ba/19-create-hud-widget_ue5.png)
5.  Following the **Add to Viewport** node, right-click and use **Add Media Sound Component** and set the **Media Player** to **MyPlayer** in the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/204c6aa7-c0e6-480c-acd8-231b4b0a752c/20-add-media-sound-component_ue5.png)
    
    In order to hear audio along with your video, you will need to use a Media Sound Component which points to your Media Player asset. Here we are dynamically creating and adding one at runtime. However, you can also add this component to an Actor that exists in the level or as part of a Blueprint from the **Components** panel.
    
6.  Following the **Add Media Sound Component** node off the **Media Player** reference node, use **Open Source** and set **Media Source** to your **MediaStream** asset.
    
    Click image for full view.
    
    With our node network complete, when the game starts our **HUD** will be created and displayed, and sound will play along with our Media Stream we open it for play.
    
7.  Close out the Level Blueprint, then click the **Play** button to play in the Level.
    

## End Result

After playing in the Editor, the video will start playing back in full screen as part of our **HUD** Widget Blueprint.

Similar to using a [File Media Source](/documentation/en-us/unreal-engine/play-a-video-file-in-unreal-engine) which plays a video file from disk, Stream Media Sources will automatically play when calling **Open Source** if their associated **Media Player** asset are set to **Play on Open** which by default is enabled. There are additional commands you can issue to the Media Player asset such as pausing, rewinding or stopping the video once it has begun playing which can be found under the **Media Player** section when dragging off the Media Player Reference.