# Level Visibility Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-level-visibility-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-level-visibility-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:10

---

There may be times when you want to toggle the visibility of entire [**Levels**](/documentation/en-us/unreal-engine/levels-in-unreal-engine) during your sequences. You can do so with the **Level Visibility Track** by setting Levels to either **Visible** or **Hidden** within Sequencer. This does not stream in/out the level but sets all the content within the level to either Visible or Hidden.

In this example we create two very small levels with unique content and toggle the visibility of those levels during our cinematic.

## Steps

For this how-to, we are using the **Blueprint Third Person Template** with **Starter Content** enabled.

1.  Inside your project in the **Content Browser**, **Right-click** and create two **Levels** named **Level01** and **Level02**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffb8bada-774e-4ae7-acc7-2c2229a34375/visibility01.png)
2.  Open **Level01**, then in the viewport click the **ViewMode** drop-down and select **Unlit**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/224c49c2-9014-4e33-b7a2-de774851e1b3/visibility02.png)
    
    This will make it easier to see the items that we place in the level since there are no lights.
    
3.  From the **Content Browser** under **Content/StarterContent/Architecture** drag the **SM\_AssetPlatform** into the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fe18590-423a-4ab3-a3ba-36f8308488b6/visibility03.png)
4.  From the **Content Browser** under **Content/StarterContent/Props** drag the **SM\_Chair** into the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/033186fc-d9b3-42ff-b250-afd9c5adab54/visibility04.png)
5.  **Save** the level, then open the **Level02** level and drag a **Wall\_Door\_400x300** into the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc33ef0f-d8ba-42af-a0b4-e78cd2313356/visibility05.png)
6.  Drag the **Floor\_400x400** (or any other assets) into the level as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aca42021-7fd4-46bc-8fe1-73c8df649667/visibility07.png)
    
    The content we are added are for example purposes to distinguish Level 01 from Level 02. Feel free to add your own content!
    
7.  In the **Content Browser** under **Content/ThirdPersonBP/Maps** open the **ThirdPersonExampleMap** and set the viewport to **Lit**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37b4b0e9-f7f8-48f6-b962-08292ad92b6b/visibility08.png)
8.  From the Menu Bar, select **Window** then select **Levels**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f96a3fb8-81ec-48f1-bae4-1eda944edbd3/visibility09.png)
9.  Click the **Levels** drop-down menu then select **Add Exisiting...**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc476d51-0083-4561-b1a8-12035d5c3431/visibility10.png)
    
    We need to add which levels we want to affect with the Level Visibility Track.
    
10.  In the **Open Level** window point to your **Level01** then repeat the process and add **Level02**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/624ae7d8-8973-41eb-8984-81984e4578e0/visibility11.png)
11.  Hold **Shift** and click on each level, then **Right-click** and change the **Streaming Method** to **Always Loaded**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aae4d36b-2105-4421-af55-0b7a66eee52a/visibility12.png)
    
    This will allow us to selectively turn on/off each level with Sequencer's Visibility Track.
    
12.  **Right-click** on the **Persistent Level** and select **Make Current**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0bfc2981-877b-45db-889e-cb5b936b45f5/visibility13.png)
    
    Our Levels are now set and we can jump into Sequencer and use our Level Visibility Track to affect them.
    
    Please see the [Level Streaming](/documentation/en-us/unreal-engine/level-streaming-in-unreal-engine) for more information on Level Streaming.
    
13.  From the Toolbar, click **Cinematics** and **Add Level Sequence**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/274d5581-7abb-44b1-82bd-b56b5c24a3fc/visibility14.png)
14.  In Sequencer, click the **Add** button and add the **Level Visibility Track**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8af5d83-a31e-4748-a30c-084364d0f8ff/visibility15.png)
15.  On the Level Visibility Track, click the **Visibility Trigger** button and add two **Visible** and two **Hidden** tracks.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acc5ba40-d655-4f28-934c-06be4144d83d/visibility16.png)
16.  **Right-click** on the top-most Visible track, then under **Properties** click the **+** for **Level Names** and enter **Level01**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/765a38fb-e795-4742-b1ce-54abe389c2a0/visibility17.png)
    
    The **Level Names** field is where we define what level we want to affect, which we set to **Level01** for this track.
    
17.  Repeat the previous step for the second **Visible** track, but use **Level02** instead.
    
18.  For the two **Hidden** tracks, set one of the **Level Names** to **Level01** and the other to **Level 02** then arrange as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e80a437-3ad9-4e09-9440-85c57da2d9ec/visibility18.png)
    
    Above, the top-most tracks are pertaining to **Level01** where we move from Visible to Hidden. The bottom two tracks pertain to **Level02** where we start out **Hidden** then move to **Visible**.
    
    You may not see your items in the level, used the **WASD** keys and check under the level.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23795e7f-7434-4b1c-b48e-dca30609aa62/visibility19.png)
    
    The location where they appear when streamed in is based on the location they are placed in their corresponding levels. You can select the level streamed in Actors like you can any other Actor and manipulate them with the [**Transform Tools**](/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine).
    
19.  Use the preview **Play** button for the Sequencer Editor to play the Level Sequence.
    

## End Result

The items placed in Level 01 will appear in the Persistent Level before disappearing at which point the items placed in Level 02 appear.

We also dragged the Level Sequence asset into the Level and enabled the **Auto Play** option so that we could use the **Play in Editor** option.

One thing to keep in mind with using the Level Visibility Track is that while you can toggle whether or not a level and its assets are hidden or visible, it does not unload or load levels as each level still sits in memory and is either rendered or not rendered based on the setting you choose.