# Play an Image Sequence

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/play-an-image-sequence-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/play-an-image-sequence-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:32

---

The **Image Media Source** asset provides a way for you play back Image Sequences inside Unreal Engine 5 (UE5) as part of the Media Framework tools. Image Media Source assets are similar to the [File Media Source](/documentation/en-us/unreal-engine/play-a-video-file-in-unreal-engine) in that you specify a path to your Image Sequence files so it can play them back instead of linking to a video. Naming conventions are important and it's recommended that you follow a sequentially based system for your images; for example, *Image\_01*, *Image\_02*, *Image\_03,* ensuring that they play back correctly in order.

In this how-to, we apply and use the Image Media Source to play an Image Sequence on a Static Mesh inside the Level.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94b0875a-14c4-406b-9ffb-b15be7c4cf20/imagemediahero_1.png)

The **Electra Media Player** does not currently support Image Sequence playback.

This tutorial covers manual workflows for image sequences. As of 5.1, you can also use the [Media Plate Actor](/documentation/en-us/unreal-engine/the-media-plate-actor-in-unreal-engine), which offers drag'n'drop addition of media sources and optimized streaming for pre-built meshes.

## Steps

For this how-to we are using the **Blueprint Third Person Template** project with **Starter Content** enabled. You will also need an Image Sequence or if you do not have one, you can right-click and download the [Sample Image Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/f4bfc412-9184-4118-82ef-a2c632eb6b95/ue5_images.zip) used with this tutorial.

1.  In the **Content Browser** expand the **Sources Panel**, then under **Content**, create a new folder called **Movies**.
    
    ![New Folder Movies](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/423880cf-e667-4e96-81ee-e1ef6d78d45c/01-new-folder-movies.png)
2.  Right-click on the **Movies** folder, then select **Show in Explorer**.
    
    ![Show in Explorer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17e27c5b-c468-4b27-9377-d5e549595960/02-show-in-explorer.png)
    
    While not required, in order to package and deploy your media with your project correctly it is recommended you place it inside **Content/Movies** folder.
    
3.  Place the images from your Image Sequence inside the **Content/Movies** folder.
    
    ![Images inside Movies Folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65beccce-f8db-42e0-9da9-51a7581c576a/03-place-the-images.png)
    
    In the image above, we have created a new folder within **Content/Movies** called **UE5\_Images** and within it, placed our JPG images. We also created another folder called **lowres** that contains lower resolution versions of the images in our sequence. The Media Framework tools provide a way for you to work with (typically) lower resolution versions of your images through media source proxies during development. This is more efficient and will help minimize any performance issues when working with larger image sequences and file sizes.
    
4.  Return to the **Editor** and click the **Don't Import** button on the **Auto-Import** dialog window inside your Unreal Engine 5 project.
    
    ![Click Don't Import Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58d270af-3936-42e3-bb79-2878254db47b/04-click-dont-import-button.png)
    
    There is no need to import the images into the project as we can point to where they are located within our project's directory.
    
5.  Right-click in your **Content/Movies** folder and under **Media**, select **Img Media Source** and call it **MyImageSequence**.
    
    ![Img Media Source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fa18b46-fa66-4d49-975e-2328071c1eed/05-select-img-media-source.png)
6.  Inside the new **MyImageSequence** asset, click the **...** button next to **Sequence Path** and point it to the first image in your image sequence.
    
    ![Sequence Path Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ade2a872-0091-4d40-a832-b841c8ae51c8/06-sequence-path-button.png)
7.  Click the **Advanced Options** rollout button to expand the **Sequence** options and under **Proxy Override**, enter **lowres**.
    
    ![Proxy Override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9de91b31-f1e4-4a0a-a085-790eac6a4a2a/07-sequence-path-advanced-options.png)
    
    Here we are pointing to a folder called **lowres** containing our lower resolution images that we will use for development. Working with the lower resolution image files will reduce the memory requirements and provide a more optimized experience than working with the full resolution files.
    
    The Proxy Override path must point to a folder of the same name, in the same directory structure as your full resolution images in order to locate it.
    
8.  Right-click in the **Content/Movies** folder and under **Media**, select **Media Player**.
    
    ![Media Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/554d5d5e-c3a3-4c16-817b-0b35d699f7d4/08-media-player.png)
    
    The Media Player asset is what we will use to play back our image sequence we have created.
    
9.  In the **Create Media Player** window, enable the **Video output Media Texture asset** option, then click the **OK** button.
    
    ![Video Output Media Texture Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efbfa083-af1a-45d4-bb39-ac6c995f9cc7/09-video-output-asset.png)
    
    This will create and automatically assign a **Media Texture** asset that is associated with this Media Player that will be used for playing our image sequence.
    
10.  Name the **Media Player** asset **MyPlayer** (which will automatically name the Media Texture) and double-click to open it.
    
    ![My Player Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29af44a4-4049-4337-8a6d-e64e89ed47b0/10-my-media-player.png)
11.  Inside the **Media Editor**, in the **Details** panel, enable the **Loop** option.
    
    ![Enable Loop Option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7917aefe-4c00-4ee3-8f5b-4578fa212894/11-enable-loop-option.png)
    
    Enabling this option will cause the Media Player to continually loop (playback) our image sequence.
    
12.  Double-click on the **MyImageSequence** asset to start playing the image sequence.
    
    ![Start Playing the Image Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00add909-218c-46da-b92f-612cc97a0a0e/12-start-playing-image-sequence.png)
    
    Your image sequence will start to play inside the Media Editor and if you click on the **Info** tab, you will see information about the image sequence that is playing. In our example, we can see that the **Dimension** for our image sequence is **640 x 360** as we are currently set to use our **lowres** images.
    
13.  In the **Content Browser**, open the **MyImageSequence** asset and clear out the **Proxy Override** section.
    
    ![Clear Out the Proxy Override Section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57bc0de2-024b-42c2-8cbd-da62c8feac0e/13-proxy-override-clear.png)
    
    This enables us to switch to our full resolution images, where if we open the Media Player asset and play our image sequence again, the **Dimension** values are different.
    
    ![Full Resolution Images](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/136c89c6-741d-478e-8daf-49b2b0df853f/14-full-resolution-image-enable.png)
    
    The **Image Cache** progress bar at the bottom of the Player window reflects the amount of content cached in memory (green means fully ready and loaded, yellow is currently being loaded, gray means it's being scheduled for loading). Based on your system hardware, the amount of caching and colors displayed may vary. See the Image Media section of the [Media Framework Overview](/documentation/en-us/unreal-engine/media-framework-overview-for-unreal-engine) for more information.
    
14.  From the Main Editor, in the **Place Actors** panel in the **Shapes** tab, drag a **Plane** into the Level and resize and position as desired.
    
    ![Plane Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0c8d9f5-8201-47b0-8a35-56bf7e6ae427/15-shapes-plane.png)
    
    You can use the [Transform Tools](/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine) to move, rotate or scale the plane as you would like.
    
15.  From the **Content Browser**, drag the **MyPlayer\_Video** Media Texture asset on top of the **Plane** in the Level.
    
    ![Add My Player Video Media Texture Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c06815c5-bc73-48fb-93d0-9c366d8809c8/16-add-my-player-video.png)
    
    This will automatically create and apply a **Material** using the Media Texture to the Plane in the Level, which our image sequence will play back on.
    
16.  From the Main Toolbar, click the **Blueprints** button then select **Open Level Blueprint**.
    
    ![Open Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74ec345a-e5c9-47bd-bda0-c2fd71e8bf23/17-open-level-blueprint.png)
    
    Before we can start testing, we will use [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) to tell our Media Player to open our Image Media Source asset at the start of gameplay so it can start playing.
    
17.  In the **MyBlueprint** panel, create a variable called **MediaPlayer** of the **Media Player Reference** type and assign **MyPlayer** as the **Media Player**.
    
    ![Variable Media Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef06fc1b-407f-4d03-a4bb-8dbf5b99e8b0/18-variable-media-player.png)
    
    You may need to click **Compile** after creating your variable in order to assign the **Default Value** for the **Media Player**.
    
18.  Hold **Ctrl** and drag the **MediaPlayer** variable into the graph, then right-click and create an **Event Begin Play** node.
    
    ![Drag the Media Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac28a941-9ace-4b52-b773-ff96ed522f78/19-media-player-blue.png)
19.  Drag off the **Media Player** variable and use the **Open Source** node and set **Media Source** to **MyImageSequence** and connect as shown.
    
    ![Set Media Source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d133a43-6a17-4b13-b33e-803a192525aa/20-media-source-image-sequence.png)
20.  **Compile** and **Save**, then from the Main Editor click the **Play** button to play inside the editor.
    

## End Result

After playing in the editor, the image sequence will start to play on the Static Mesh in the Level and loop thereafter.

This example used JPG files, however, you can use any image files that are of the [supported file type](/documentation/en-us/unreal-engine/media-framework-technical-reference-for-unreal-engine) within an Image Media Source.