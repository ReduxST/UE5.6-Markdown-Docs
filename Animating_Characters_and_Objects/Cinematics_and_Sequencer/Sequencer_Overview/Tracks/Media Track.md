# Media Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-movie-media-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-movie-media-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:11

---

Sequencer can control the playback of any Media Source by using a **Media Track** and assigned **Media Source** and **Media Texture** assets. Sequencer will also create internal Media Players when playing back your media source so you do not need to create a Media Player asset. 

In this How-to, we create a new Level Sequence, assign a Media Track and point it to our EXR image sequence which plays back when we play in our Level. 

![UsingMediaHero.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e9bce28-1af9-47f7-be53-2f49189d55be/usingmediahero-resize839x385.png "UsingMediaHero.png")

## Steps

For this How-to, we are using a new **Blank Blueprint Project**. You will also need a series of EXR or PNG  images to use for your Media Source. If you do not have a set of images to use, you can download this [UE4 Logo](https://epicgames.box.com/s/fsxw4c9llathxzk8dwof302d1tba4ow1) set of images for use in this guide.

1.  Inside your project, right-click in the **Content Browser** and under **Media**, select **Img Media Source** and give it any name. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90458b48-82a8-45da-8d97-1c1e2d080a8f/mediatrack_02.png "MediaTrack_02.png")
2.  Open the **Img Media Source** asset, then point the **Sequence Path** to the sample EXR images and open the first image.  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20e9b500-be34-4971-8b5f-cd3490e32a5b/mediatrack_03.png "MediaTrack_03.png")
    
3.  In the **Content Browser**, right-click then under **Media**, create a **Media Texture** asset. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/938bacc9-546d-490f-8761-6cb1270da4fc/mediatrack_04-1.png "MediaTrack_04-1.png")
    
    Typically you would create a **Media Player** asset and an associated **Media Texture**. When we use the **Media Track** in **Sequencer**, each Media Track will automatically create an internal Media Player to handle playback on-demand.
    
4.  From the Main Toolbar, click **Cinematics** then select **Add Level Sequence** and choose any name and save location.  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0e4c1af-bd49-4c0f-9d0f-c860fda02587/mediatrack_06.png "MediaTrack_06.png")
    
5.  Open the Level Sequence, then click the **Track** button and select the **Media Track** option.  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d5d5f5d-b69c-4503-9272-4d6a6f22865d/mediatrack_07.png "MediaTrack_07.png") Alternatively, you can drag a **Media Source** asset from the **Content Browser** into **Sequencer** to create a **Media Track**.
    
    ![MediaTrack_08-2.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9012db12-ecf1-4f17-be82-123bb92b30a3/mediatrack_08-resize1047x434.png "MediaTrack_08-2.png")
6.  On the **Media Track**, click the **\+ Media** button and select your **Img Media Source** asset.  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df56362e-4ebb-4089-9c1c-8c37ee6e90d5/mediatrack_09.png "MediaTrack_09.png")
7.  Stretch the Media to frame **520** and move the end marker to the end of the sequence.  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e1fb61f-1346-46eb-b660-7fe00ab415ab/mediatrack_10.png "MediaTrack_10.png")
    
    Currently, the Media section does not automatically size itself to the length of the Media which is why we are stretching it to fill the section.  In a future release, we hope to have it automatically resize itself.
    
8.  Right-click on the Media, then under **Properties**, set the **Media Texture** to your **Media Player** asset.  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9df49272-c060-4778-94dd-2ed23bd9cc4f/mediatrack_11-1.png "MediaTrack_11-1.png") Whenever you add a Media Track, you will need to go into the  **Properties** and define the **Media Texture** to associate the Media Track with. This Media Texture will receive the video output of the video that is being played. 
    
    You can reuse the same Media Texture from multiple sections, but you will need to make sure that no two sections write to the same Media Texture at the same time.
    
9.  Select your Level Sequence in the Level, then in the **Details** panel, enable **Auto Play**. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e0faef2-091d-4628-b986-2d4f91dc23a7/mediatrack_12.png "MediaTrack_12.png")
10.  From the **Modes** panel under **Basic**, drag a **Plane** into the Level and resize and rotate as desired. 
    
11.  Drag your **Media Texture** asset from the **Content Browser** onto the **Plane** in the Level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e89c125d-1a97-46d3-ac9a-7015ef58c850/mediatrack_13-1.png)
    
    This will automatically create and assign a new **Material** that uses the **Media Texture**.
    
12.  Click the **Play** button to play in the Editor. 

## End Result

When you play in the Editor, the video will start playing back as indicated by the Level Sequence which is set to auto play. You can also scrub through the Media inside the Sequencer Editor which will scrub the video playback. 

## Additional Information

The **Media Track** currently works best with **Img Media Source** objects for images sequences, particularly EXR sequences.

MP4 movies and other movie formats are supported but are experimental, as is rendering out Media Tracks.

When optimizing playback of Media Tracks, there are a few things to configure.

First, there is a global setting in the **Project Settings > Plugins > IMG Media**. The **Cache Size GB** is the number of gigabytes that each active Media Player will cache. You need to set this to a reasonable number, depending on how many Media Players you have active at a time, and what the memory footprint of video frames is. As a recommendation, 0.5 or 1.0 is usually a good number, but your requirements may differ.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb008f8a-a810-412b-91ba-a46e7156cef4/mediatracks_projectsettings.png "MediaTracks_ProjectSettings.png")

The **Cache Behind Percentage** is the percentage of the cache that will be used to cache frames behind the current play position. For real-time playback you want to set this to 0 as you are only interested in caching frames forward.

Second, each Media Track Section needs to have its **Pre-roll** time configured for the frames to be preloaded in time. Again, the correct amount depends on a number of factors, such as how many videos you're playing, how big the frames are or how fast your machine is.

In general, you want to make sure that video frames are pre-rolled early enough so they are available by the time they are needed, but you also don't want to pre-roll too soon as that may interfere with the performance of other sections that are still playing and loading video frames. You should adjust the Cache Size and Pre-roll settings in such a way that the least number of video frames are pre-rolled at any given point in time while still guaranteeing that all frames are ready when needed.