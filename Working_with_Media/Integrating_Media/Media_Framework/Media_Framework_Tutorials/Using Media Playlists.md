# Using Media Playlists

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-media-playlists-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-media-playlists-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:56

---

When working with media assets in Unreal Engine 5 (UE5), there may be times where you have a series of videos that you want to play in a specific order or you want to allow players to access videos within a specific series of videos. This can be accomplished by using a **Media Playlist** asset which points to **Media Source** assets assigned in a predefined order.

In this how-to, we create a Media Playlist and allow the player to play each asset sequentially or access a specific video inside the playlist through a key press.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19c7e419-e324-41ae-915e-2e805dfe0b20/0-hero_ue5.png)

## Steps

For this how-to we are using the **Blueprint Third Person Template** project with **Starter Content** enabled. We are also using three sample videos in our playlist which you can download by right-clicking this [Sample Videos](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/7b1b2f19-757b-4e8f-99f0-c40f98832e3a/video.zip) link and extracting the contents on your computer.

1.  In the **Content Browser** expand the **Sources Panel**, and create a folder called **Movies** then right-click on it and **Show in Explorer**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ea64351-8522-42de-83a3-0fb008f6ebdd/01-show-in-explorer_ue5.png)
    
    In order to successfully package and deploy your video files along with your project, your videos must be placed inside the **Content/Movies** folder of your project.
    
2.  Drag the Sample Video files provided into the **Content/Movies** folder of your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56d45f69-144a-4d88-9f1e-bf91c8d72d90/02-video-in-folder_ue5.png)
3.  In your project, right-click in the **Content/Movies** folder then under **Media** select **File Media Source**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f5a1ce6-1497-4823-b00b-673a6214215d/03-file-media-source_ue5.png)
4.  Create three **File Media Source** assets called **Video\_01**, **Video\_02** and **Video\_03** respectively.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ab38588-045f-44a6-9ef5-6de6e1727bb2/04-file-media-source_ue5.png)
5.  Inside **Video\_01**, point the **File Path** to the **Gideon\_720x480** file (or your desired video file) then click the **Open** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab3e7e4c-e576-44bc-8778-11eeb4963909/05-open-file_ue5.png)
6.  Repeat the previous step and assign videos for the **Video\_02** and **Video\_03** assets.
    
7.  Create a **MediaPlayer** asset called **MediaPlayer** with an associated **Media Texture**, then open the **MediaPlayer** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e567a08-f241-470d-875a-cbd0d201baf9/06-add-media-player_ue5.png)
    
    Double-clicking on a video inside the **Media Library** window will play the selected file.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58e63911-fd8f-463a-beb5-602384d54e8f/07-media-player-video-1_ue5.png)
    
    You can also set the player to **Shuffle** the playback order of videos in a playlist by enabling the option in the **Details** panel. The **Loop** option will loop the playback of entire playlist (or a single source if there is only one source in the Media Playlist). Our Media Player is also set to **Play on Open** which means, when we open this Media Source associated with this Media Player, it will automatically start playing.
    
    In the **Playlist** window, you can save out new playlist assets.
    
8.  Inside the **Content/Movies** folder of the **Content Browser**, right-click and under **Media** select **Media Playlist** and call it **MyPlaylist**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4330722f-ab49-46d5-9da7-bdf600892e52/08-add-media-playlist_ue5.png)
9.  Open the **MyPlaylist** asset, then in the **Media Library** window, double-click on a video and add each to the playlist.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d67c56c-2f44-44e0-815b-bda9a5d77e71/09-add-file_ue5.png)
    
    You can also use the **+** button to add new items to the playlist and the drop-down menu to select the type of Media Source to add. Inside the **Playlist** window you can insert, duplicate or delete items from the playlist or left-click and drag rows to reorder the playback order by clicking the tab along the left side of each row. At the top of the Media Playlist window, the **Loop** option is available if you want to loop the entire playlist.
    
10.  From the **Place Actors** panel of the Main Editor window in the **Shapes** tab, drag a **Plane** into the Level and use the **Transform Tools** to resize it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ddfc41a-6378-410f-8bec-09f35a041d72/10-shapes-plane_ue5.png)
    
    Using the [Transform Tools](/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine) you can move (**W key**), rotate (**E key**), or scale (**R key**) the plane as desired as we will play our videos on this Static Mesh.
    
11.  From the **Content Browser**, drag the **MediaPlayer\_Video** Media Texture asset onto the plane in the Level to create and apply a new Material.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5902cdf8-08b4-43e3-9fb5-b54aac8a5b0a/11-add-media-player-video_ue5.png)
    
    When dragging the **Media Texture** onto the Static Mesh in the Level, a **Material** will automatically be created and applied to the mesh, enabling us to play our videos.
    
12.  With the **Plane** selected in the Level, in the **Details** panel click the **Add Component** button and add a **Media Sound** component.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af169b44-aaed-482a-8ef8-f66505e258fc/12-add-media-sound_ue5.png)
    
    The **Media Sound** component enables us to associate audio with a Media Player and provides a way for the audio to be played along with our video.
    
13.  Select the **Media Sound** component, then under the **Media** section assign your **MediaPlayer** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1f90ecb-2b7a-47db-a32a-c2ae117ad85c/13-connect-media-player_ue5.png)
14.  From the Main Toolbar, click the **Blueprints** button and select **Open Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8202d6cc-dd43-41e8-a08c-f1a6cb3d38db/14-open-level-blueprint_ue5.png)
    
    While our video plays inside the Media Editor, in order to play during gameplay we will need to open our playlist so it can start playing.
    
15.  In the **MyBlueprint** window, create a variable called **MediaPlayer** of the **Media Player Object Reference** type and set the **Default Value** to your **Media Player** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb58662a-922f-4a18-9f9c-d037644d7bbe/15-media-player-compile_ue5.png)
    
    You may need to **Compile** your Blueprint in order to set the **Default Value**.
    
16.  In the graph, right-click and add a **1** Keyboard Event, then hold **Ctrl** and drag the **MediaPlayer** variable into the graph.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1548f14f-7062-4e54-a59c-15edeeee3e03/16-media-player-blueprint_ue5.png)
17.  Drag off the **MediaPlayer** variable and use **Open Playlist Index** (with **In Playlist** set to **MyPlaylist**) and connect to the **Pressed** of the **1** keyboard event.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/773075e5-5e35-4fef-8001-4708f4d12520/17-blueprint-open-playlist_ue5.png)
    
    Here, when the Player presses the **1** key on the keyboard, the playlist will open (and start playing) with the first video in the list. The index refers to the playlist index order specified inside your Media Playlist asset (pictured below) and is zero-based with zero being the first video in your playlist. With the **Open Playlist Index** node, you can specify which file you want to open within a playlist by entering its index value.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23995118-af38-4257-9b19-cf6387e31c86/18-array-elements_ue5.png)
18.  Right-click and add **2** and **3** keyboard events to **Open Playlist Index** for **Index 1** and **Index 2** respectively.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87f06dac-9dac-4ab7-b94f-fc242b98b435/19-index-playlist_ue5.png)
    
    With this setup, when you press 1 you will open the first file in the playlist, 2 the second and 3 the third.
    
19.  Right-click and add a **Left** and **Right** keyboard event to call **Previous** and **Next** nodes and **0** to **Open Playlist**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21e02aba-c83c-4539-83eb-3bf9b7ea8a8d/20-target-in-playlist_ue5.png)
    
    The **Previous** and **Next** nodes will jump to the previous video and next video in a playlist respectively while the **Open Playlist** node executes the same functionality as opening a playlist at index 0 (or the start of the playlist). With these nodes, we will be able to cycle through our playlist by using the **Left** and **Right** arrow keyboard keys and pressing the **0** key will open the playlist at the start of our playlist.
    
20.  Close the **Level Blueprint** then click the **Play** button to play in the Editor.
    

## End Result

When you play in the Editor pressing the **1**, **2**, **3** or **0** keys will start playback at the specified index (if applicable).

When a video ends, it will automatically jump to the next video in the playlist. If you enabled **Loop**, once the final video in the playlist plays, it will jump back to the start of the playlist. While the video is playing, you can press the **Left** or **Right** arrow keys to jump to the previous or next video in the playlist or the **1**, **2**, or **3** keys to jump directly to a video in the playlist.