# Media Framework Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/media-framework-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/media-framework-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 16:35:32

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72b5f8f0-6449-443c-b027-8f12fb884c95/00-final-result.png)

*At the end of this guide, you will have a TV playing content in your level that you can turn on or off when standing next to them and pressing a key.*

### Goals

In the Media Framework Quick Start guide, we walk through setting up a television (TV) that can play videos inside your level. We also set the TV up with Blueprints so the content on the TV can be turned on with the press of a button. We also expose the Media Framework variables so that we can quicly change the content that is played on the TV through the **Details** panel. If you are new to the Media Framework tools, or want to know how to play videos on Static Meshes inside your levels, this guide is for you.

This guide includes some setup using [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials) and [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) to achieve the effect of a video playing on a TV. Some prior knowledge of these topics is recommended but not required.

### Objectives

After going through this tutorial, developers will know the following:

-   How to import Media and use different Media Sources.
-   How to create a Material incorporating a Media Texture used to play media files.
-   How to start and stop playback of media using Blueprint.
-   How to create a TV Blueprint where you can specify what Media Source to use.

## 1 - Project and Material Setup

## 1 - Project and Material Setup

1.  Create a New Project using from the Games category using the **ThirdPerson** Blueprint template and give it any name.
    
2.  Extract this [Sample Content](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/c117b6e9-99e5-42df-8ea1-872cdf66ffb4/sample_content.zip) to your machine, then import all content into the Engine.
    
    ![Import all content](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e84f4c0-2d15-4d98-be05-60433280c57a/01-sample-content_ue5.png "Import all content")
    
    Optionally, you can create a new folder to hold all the sample content. A **Material** will automatically be created based on the Texture asset.
    
3.  In the **M\_TV\_Inst** Material, delete the **Vector Parameter** node, and add a **Texture Sample** with the **Sample Type** set to **External**.
    
    ![Add a Texture Sample](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3f65358-e843-4643-9580-be98cfd6d521/02-texture-sample-external_ue5.png "Add a Texture Sample")
4.  Add a **Texture Object Parameter** and name it **TV\_Texture**, then connect to the **Texture Sample** through the **Tex** pin.
    
5.  For the **TV\_Texture** Param Tex Object, change the **Texture** to a new **Media Texture** and call it **MediaPlayer\_01\_Video**.
    
    Click image to expand.
    
6.  Click the magnifying glass icon to browse to and open the **MediaPlayer\_01\_Video** asset.
    
    ![Open Media Player asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a456c63-b2c7-4b36-a8ff-547f7d7591e6/04-media-player-01-video_ue5.png "Open Media Player asset")
    
    If you are using a Texture Sample or Texture Object with the **Electra Media Player**, set the **Sampler Type** to **Color**.
    
    ![Set the Sampler Type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1552cbd1-b618-4b9f-aa96-b95c3e6701c4/05-samler-type-color_ue5.png "Set the Sampler Type")
7.  Click the **Media Player** drop-down menu and create a **Media Player** asset called **MyMediaPlayer**.
    
    Click image to expand.
    
    When the **Create Media Player** pop-up menu appears, just click **Ok** as you do not need to create another **Media Texture** as you did this in Step 5 above.
    
    ![Click OK](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8421f7f-ec0d-470e-b40e-cf009768a664/07-media-texture-asset_ue5.png)
8.  Open your **MyMediaPlayer** asset, then double-click the **Sample Video** file and the video will start playing.
    
    Click image to expand.
    
9.  In the **M\_TV\_Inst** Material, add a **TexCoord** with **VTiling** set to **2.0** and connected to the **UVs** pin of the **Texture Sample**.
    
    Click image to expand.
    
10.  Add another **TextureSample** with the **Texture** set to the **T\_TV\_M2** asset.
    
    Click image to expand.
    
11.  Add a **LinearInterpolate** node with the **Texture** from the previous step connect to the **Alpha** through the **Green** channel.
    
    ![Add a LinearInterpolate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67a294b0-33b7-4325-bafa-f65e104b9751/11-texture-sample-lerp_ue5.png "Add a LinearInterpolate")
12.  Connect the remaining pins as shown below.
    
    Click image to expand.
    

### Section Result

We've set up the Material that will play back our Media using a **Media Player** and associated **Media Texture** asset. If we open the TV mesh in the **Content Browser**, you may notice that the screen appears black (or white in some instances).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3c676f7-1192-40df-961e-e58858448c9c/13-tv-settings_ue5.png)

To preivew, you can open the Media Player asset and double-click the Media Source, at which point, the media will play on the Static Mesh TV in the Viewport.

Click image to expand.

## 2 - TV Blueprint - Component Setup

In this step, we create a Blueprint that uses the TV Static Mesh and the remaining components needed make our TV work in the Level.

1.  In the **Content Browser** click the **Add New** button and select **Blueprint Class**.
    
    ![Add new Blueprint Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f168dfe-6820-4030-b442-cd23acd37d41/15-add-blueprint-class_ue5.png "Add a new Blueprint Class")
2.  In the **Pick Parent Class** menu, select **Actor** and name the Blueprint **TV\_BP**.
    
    ![Pick Parent Class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7289509-c29a-4e28-8725-2ca6c47b80e9/16-actor-class_ue5.png "Pick Parent Class")
3.  In the **TV\_BP** asset, click the **Add Component** button and select **Static Mesh**.
    
    ![Add Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbc10f0f-3e75-4778-9ca0-b2b31e4c7cc7/17-add-static-mesh_ue5.png "Add Component")
4.  In the **Details** panel for the **Static Mesh**, assign the **SM\_TV** as the **Static Mesh** to use.
    
    Click image to expand.
    
5.  Add a **Box Collision** component, then resize and move the box infront of the TV as shown below.
    
    Click image to expand.
    
    We are going to use the Box Collision to indicate when the player is infront of the TV and can turn it on (we don't want to be able to turn on the TV while standing behind it).
    
6.  Add a **MediaSound** component and assign the **MyMediaPlayer** asset in the **Details** panel for the **Media Player** property.
    
    Click image to expand.
    
    This will be used to play back the audio associated with the defined **Media Source** inside the **Media Player**.
    
7.  In the **Details** panel for the **Box Collision**, add both the **On Component Begin Overlap** and **On Component End Overlap** events.
    
    ![Add Events](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce9ea3a6-7b06-478e-9024-d8e866cc7db2/21-add-component-overlap_ue5.png "Add Events")

### Section Result

Our TV Blueprint is set up, next we will add the scripted functionality to be able to turn the TV on when standing next to it by pressing a key.

## 3 - TV Blueprint - Scripted Setup

In this final step, we add the scripted functionality that enables the player to press a button to turn the TV on or off.

1.  On the **Event Graph** of the TV Blueprint, use a **Get Player Controller**, **Enable Input** and **Disable Input** connected as shown below.
    
    Click image to expand.
    
2.  Right-click in the graph and add a **P** Keyboard Event (or your desired key press) and connect **Pressed** to a **FlipFlop** node.
    
    ![Add P Keyboard Event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0edd63a-a367-4d63-a8f7-df6cac58b5b2/23-p-keyboard_ue5.png "Add P Keyboard Event")
3.  Right-click in the graph and disable **Context Sensitive**, then add an **Open Source** node.
    
    ![Add an Open Source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed6ee88e-1a6f-47ac-a8bd-3f0c9136da89/24-open-source_ue5.png "Add an Open Source")
4.  On the **Open Source** node, right-click the **Target** pin and select **Promote to Variable** and call it **MediaPlayerforVideo**.
    
    ![Promote to Variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20cd20fb-b7f6-4eeb-bd24-873b0f6ea3f1/25-promote-to-variable_ue5.png "Promote to Variable")
    
    By default, Media Players are set to **Play on Open** which will play the media whenever it is opened.
    
    For Media Players that have **Play on Open** disabled, you can use a **Play** node followed by an **Open Source** call.
    
5.  Promote **Media Source** to a variable and call it **SourceToOpen**.
    
6.  In the **Variables** list, click the eye icon on both variables to make them **Instance Editable** and connect as shown below.
    
    ![Click the eye icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88ac8d01-0771-49c4-b8bd-62167748cbdd/26-open-icons_ue5.png "Click the eye icon")
7.  Add a **Close** node connected to the **B** pin of the **FlipFlop** and **Target** set to **MediaPlayerforVideo**.
    
    ![Add a Close node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c757772-3fb8-4191-8adb-be7cf3ff637a/27-close-target_ue5.png "Add a Close node")
8.  Drag the **TV\_BP** into the Level, then in the **Details** panel, assign the **MyMediaPlayer** and **Opening Demo** assets.
    
    Click image to expand.
    
    You are going to use the Box Collision to indicate when the player is infront of the TV and can turn it on (we don't want to be able to turn on the TV while standing behind it).
    
9.  Inside the **MyMediaPlayer** asset, enable the **Loop** option.
    
    ![Enable the Loop option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98359887-8caa-4131-ae15-a89c9fa37e17/29-loop-enable_ue5.png "Enable the Loop option")
    
    This will automatically loop the video once it starts playing unless instructed to close.
    
10.  Click the **Play** button to play in the Level.
    

### End Result

When playing in the Level and approaching the TV, pressing the P button will start playing the assigned media. Pressing P again will stop playback.

## 4 - On Your Own!

Here are some additional things to try with your project using the Media Framework tools:

-   Enable the player to [control playback](/documentation/en-us/unreal-engine/control-video-playback-with-blueprints-in-unreal-engine) of the TV.
-   Use a [Media Playlist](/documentation/en-us/unreal-engine/using-media-playlists-in-unreal-engine) as a Media Source and allow the player to "change the channels" for the TV.
-   Add a second TV Blueprint to the level with its own Media Player, Media Sound, and Media Source Assets.