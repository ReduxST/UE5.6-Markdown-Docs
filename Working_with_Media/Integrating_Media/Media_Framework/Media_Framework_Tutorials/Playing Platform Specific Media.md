# Playing Platform Specific Media

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/playing-platform-specific-media-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/playing-platform-specific-media-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:44

---

If you are working on a multi-platform project, there may be instances where you want to play platform specific media. For example, you may want a specific movie to play when playing on PlayStation 4 (PS4) and a different movie to play when playing on the Xbox One. Or you may be using the same type of media, but it is encoded differently for performance reasons and want those different formats to play on different platforms.

With the **Platform Media Source** asset, you can determine which Media Source assets should play based on the platform it is running on. When you open/play the Platform Media Source, it will look at which platform you are currently on and play the assigned Media Source automatically.

In this how-to, we create a Platform Media Source and assign two different Media Sources for Android and Windows platforms.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d96e2b4-0a95-4efc-870a-8f9b8b4dd154/00-hero-image_ue5.png)

## Steps

For this how-to we are using the **Blueprint Third Person Template** project with **Starter Content** enabled. We are also using two sample videos which you can download by right-clicking this [Platform Videos](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/505ae3df-755b-4cc5-8531-bf70165544a0/platform_video.zip) link and extract the contents on your computer.

1.  In the **Content Browser** expand the **Sources Panel** and add a new folder called **Movies** then right-click on it and **Show in Explorer**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e1c4174-3a41-4672-8ec0-4a3c4c6a7b15/01-show-in-explorer_ue5.png)
2.  Drag the sample videos or your desired media files into the **Content/Movies** folder of your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89311237-b3dc-4c24-81ad-304529ef2c61/02-video-in-folder_ue5.png)
    
    If you want to package and deploy your project along with any media files, you will need to place them inside the **Content/Movies** folder of your project.
    
3.  In your project under the **Content/Movies** folder of the **Content Browser**, right-click and under **Media** select **File Media Source** and name it **Android\_Movie**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f900ac06-774d-4324-86f2-266b45b00288/03-file-media-source_ue5.png)
    
    Here we are creating a Media Source asset that the **Platform Media Source** asset can point to and use if it is running on an Android device.
    
4.  Create another **File Media Source** asset and call it **Windows\_Movie**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/defc11a0-b261-4a7c-ad48-d29cd04fbc37/04-file-media-android-windows_ue5.png)
5.  Open the **Android\_Movie** Media Source, then for the **File Path** use the **Gideon\_720x480** (or your desired video) and select **Open**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff63adc3-5b6d-436c-904d-b33aa9601671/05-open-gideon-video_ue5.png)
    
    For our Android movie, we are using a **.3GP** video file which is better suited for playback on Android devices while our Windows movie is an **.MP4** file.
    
6.  Open the **Windows\_Movie** Media Source, then point the **File Path** to the **Infiltrator Demo** (or your desired video) and select **Open**.
    
7.  Right-click in the **Content/Movies** folder then under **Media**, select **Platform Media Source** and call it **Platform\_Source**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbf122ea-d7e3-4c40-9ed2-af2390cdfea0/06-platform-media-source_ue5.png)
    
    Now that we have multiple Media Source assets, we can define which Media Source is to be played on which Platform with the **Platform Media Source** asset.
    
8.  Open the **Platform\_Source**, then under **Android** select the **Android\_Movie** and under **Windows** select the **Windows\_Movie**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/338faf02-29f0-4d46-a0a3-0e0ea94ff447/07-media-sources-android_ue5.png)
    
    In our example we are using two different videos. However, you can use the same video that is encoded differently or in a different format for use with different devices. You may also use different Media Source types, for example, on Windows you may elect to use a [Media Stream](/documentation/en-us/unreal-engine/play-a-video-stream-in-unreal-engine) to pull content from a website instead of using a file on disk.
    
9.  Right-click in the **Content/Movies** folder then under **Media**, select **Media Player**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b72c9fc-52fe-4d14-8c26-70e4190a6034/08-media-player_ue5.png)
    
    We still need to use a **Media Player** to open and play our **Platform Media Source** asset.
    
10.  In the **Create Media Player** window, enable the **Video output Media Texture asset** option then click **OK** and call the asset **Media Player**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b400554-a290-49d9-93cc-f4806c101b2c/09-video-output-asset_ue5.png)
    
    This will automatically create a **Media Texture** associated with this Media Player that we can use inside a [Material](/documentation/en-us/unreal-engine/unreal-engine-materials). We can then take that Material and apply it to a mesh in our Level to play our content on.
    
11.  Inside the **Media Player** asset, double-click on the **Platform\_Media** asset in the **Media Library** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9a1bb4e-cacb-4046-ad18-57cc5a0b33a7/10-video-media-player_ue5.png)
    
    Double-clicking on the **Platform\_Source** asset will start playback of only the **Windows** assigned Platform Media Source (since we are running on the Windows platform). Through Blueprint or C++, we could open the **Android\_Movie** Media Source for playback however when we open the Platform\_Source, only the Media Source assigned to Windows will play. Also, the **Play on Open** option is enabled by default which will allow the Media Player to start playback of whatever Media Source is opened.
    
12.  In the Main Editor window, from the **Modes** panel under **Basic**, drag a **Plane** into the Level and resize as desired then drag the **MediaPlayer\_Video** texture onto it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/110dd1e0-2c0b-4e7e-b0c7-593ddb568f5b/11-add-media-player_ue5.png)
    
    By dragging the **Media Texture** asset onto the Static Mesh in the Level, a Material is created and applied and will playback our media.
    
    If you are using a Texture Sample or Texture Object with the **Electra Media Player**, set the **Sampler Type** to **Color**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e64aa7e8-86d4-4ca2-8756-bbf1e5291c99/12-samler-type-color_ue5.png)
13.  With the **Plane** selected, in the **Details** panel add a **Media Sound** component with the **Media Player** option set to use your **MediaPlayer** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e2408c5-c6a6-41fa-a7ac-44cb1af31882/13-connect-media-player_ue5.png)
14.  From the Main Toolbar, click the **Blueprints** option then select **Open Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4dc2495-6c0b-4feb-91d9-740441b17dba/14-open-level-blueprint_ue5.png)
15.  In the **MyBlueprint** panel create a variable called **MediaPlayer** of the **Media Player Object Reference** type then assign your **MediaPlayer** as the **Media Player** to use.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efa982ab-79ab-487c-90ee-02a3bbc7c80f/15-media-player-compile_ue5.png)
    
    This creates a reference to your Media Player asset which you can then use within Blueprint and call actions on.
    
    In order to set the **Default Value** for the variable, you may need to first click **Compile** to compile the Blueprint.
    
16.  Hold **Ctrl** and drag the **MediaPlayer** variable into the graph, right-click and add a **1** keyboard event and connect to an **Open Source** node pointing to the **Platform\_Source**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b2e43ed-436a-43f5-b731-6dafc053f391/16-blueprint-keybord_ue5.png)
    
    Here we are telling our Media Player to open the **Platform Media Source** asset which is set to open other Media Source assets based on which platform it is being run on.
    
17.  Close the **Level Blueprint** then click the **Play** button to play in the Editor.
    

## End Result

When you play in the Editor, pressing the **1** key will open the Windows-defined Media Source inside the Platform Media Source.

If you were to deploy this project to an Android Device, the Android assigned Media Source asset would play.