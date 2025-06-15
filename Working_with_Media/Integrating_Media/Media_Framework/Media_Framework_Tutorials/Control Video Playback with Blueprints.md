# Control Video Playback with Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-video-playback-with-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-video-playback-with-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:52

---

Along with playing videos inside your Unreal Engine 5 based projects, you can enable players to control the playback of your videos with a series of [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) nodes.

In this how-to, we provide a way for the Player to control playback of a video by creating the ability to pause, rewind, fast-forward, and resume playback of a video in progress.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3480188e-9041-4a04-a8b6-373af1427cab/00-hero_ue5.png)

Not all player Plug-ins may support fast forward and/or reverse playback. Please refer to the [Media Framework Technical Reference](/documentation/en-us/unreal-engine/media-framework-technical-reference-for-unreal-engine) page for more information.

## Initial Setup

First, we'll locate our media and set up a folder in the Content Browser. This will lay a foundation we can later build upon in Blueprints.

For this how-to we are using the **Blueprint Third Person Template** project with **Starter Content** enabled. You will also need a video for playback, you can use your own or right-click and download this [Sample Video.](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/37336b04-cf32-4e42-af8b-2a1d6500a336/opening_demo.mp4)

1.  In the **Content Browser** expand the **Sources** panel and create a folder called **Movies.** Then, right-click on the new folder and select **Show in Explorer**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/880cecf2-faac-431d-9525-50de62c41043/01-show-in-explorer_ue5.png)
2.  Drag the Sample Video (or your supported video) into the **Content>Movies** folder of your project on your computer.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c8de927-e48d-4294-bb84-991580de4837/02-movies-folder_ue5.png)
    
    To ensure that your video content is packaged and deployed with your project, your content must reside in the **Content>Movies** folder of your project.
    
3.  Inside your project, create a **Media Player** and associated **Media Texture** asset called **MediaPlayer** and **MediaPlayer\_Video** respectively.
    
    Click image to expand.
    
4.  Create a **File Media Source** asset called **Video** and inside it, point the **File Path** to the video added in **Step 2**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c813eaaa-d3b0-408b-a32d-ee0403205767/04-media-player-video_ue5.png)
5.  Open your **Media Player** asset and disable the **Play on Open** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b18b67d-01a5-4f17-97b1-56597109f262/05-play-on-open_ue5.png)
    
    In this example, we are going to give playback control to the Player, rather than automatically start playback once we open our Media Source.
    
6.  In the **Place Actors** panel under **Shapes,** drag a **Plane** into the level and resize as desired (Place Actors can be found under the Window tab if it's not already enabled).
    
    Click image to expand.
    
7.  Drag the **MediaPlayer\_Video** texture onto the **Plane**, then in the **Details** panel for the Plane, add a **Media Sound Component** set to use your **Media Player** asset.
    
    Click image to expand.
    

## Blueprint Setup

Next, we want to set up our initial Blueprint, so later we can add functions to it.

1.  From the Main Toolbar, click the **Blueprints** button then select **Open Level Blueprint**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffbe97a4-1bf7-443d-9085-53c2800264a6/08-open-level-blueprint_ue5.png)
2.  In the **Level Blueprint**, create a variable called **MediaPlayer** (of the **Media Player Object Reference** type) and set it to point to your **MediaPlayer** asset.
    
3.  Hold **Ctrl** and drag the **MediaPlayer** variable into the graph and use **Open Source** and **Event Begin Play** to open your **Video** File Media Source asset.
    
    Click image to expand.
    
    Alternatively, you can use the Open Source Latent node (instead of the Open Source node) to open the specified media source with options and will delay the execution of the Completed output pin until after the source file has been opened.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53b78836-b26b-45bd-918c-b010b8dbce6e/10-open-source-latent_ue5.png)
    
    This can be useful when you'd like to do something like set the play rate of the source.
    

## Play/Pause - Up

1.  Add an **Up** keyboard event connected to a **Flip Flop** and off your **Media Player** variable, use **Play** and **Pause** as shown below.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e341686-4572-4613-97ff-2b59721a9823/11-add-up-key_ue5.png)
    
    When the Player presses the **Up** arrow keyboard key, the Media Source will start playing while pressing a second time will pause the video.
    
    Pausing corresponds to setting the Play Rate to 0.0, however not all Media Sources support pausing (for example, Web Cam and other video capture hardware sources. You can use the **Can Pause** Blueprint node to determine if a Media Source supports pausing.
    

## Rewind/Fast-Forward - Left/Right

1.  Add **Left** and **Right** keyboard events, then off your **Media Player** variable use **Set Rate** with the left key at **\-2** and the right key at **2**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b289e3b1-955c-460d-966e-cbd28966b77e/12-set-rate-value_ue5.png)
    
    This will enable the Player to press the left arrow keyboard key to set the Play Rate of the video to -2 (playing the video in reverse at double speed as a value of 1.0 is normal forward playback).
    
    When pressing the right arrow keyboard key, the video will fast forward at double the normal playback speed.
    
    You could add additional Blueprint logic to determine the number of times the Player presses the rewind or fast-forward keys and increase or decrease the Play Rate from 2x to 4x or 6x speeds or higher.
    
    Even if the Player Plug-in supports Play Rates other than 1.0, the actual playback rates that can be selected will depend on the Media Source in use. You can check supported rates with the **Get Supported Rates** function.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c697408c-2339-4e50-9fdb-ab2305bd1d2a/13-get-supported-rates_ue5.png)
    
    Keep in mind there is a distinction between **Thinned** and **Unthinned** rates. Thinned means that some frames will be skipped at this rate, while Unthinned means that all frames will be decoded at this rate.
    

## Close/Resume - Down

1.  Add a **Down** keyboard event connected to a **Flip Flop**, then off a **Media Player** reference, use the **Get Time** function call.
    
    Click image to expand.
    
    The **Get Time** function call will return the current playback time which we will store and use when we want to reopen and resume playback of our video.
    
2.  Right-click on the **Return Value** of the **Get Time** node and promote it to a variable called **Stop Time**, then connect all nodes to a **Close** function call as shown.
    
    Click image to expand.
    
    This will close the Media Player when pressing the down arrow keyboard key, but store the current time in which the Media Player was stopped to a variable.
    
3.  Off the **B** pin of the **Flip Flop** use the **Open Source** node and set the **Media Source** to your **Video** Media Source.
    
    Click image to expand.
    
    This will re-open your video but will open it from the beginning of the video which we will address in the next few steps.
    
4.  Drag off the **Media Player** reference and use the **Assign On Media Opened** Event Dispatcher and connect as shown.
    
    Click image to expand.
    
    This will create an [Event Dispatcher](/documentation/en-us/unreal-engine/event-dispatchers-in-unreal-engine) that will call the connected Event only when the Media Source has been fully opened. When issuing commands to a Media Player, it's a good practice to do so in this manner as it ensures that the Media Source has been opened before attempting to tell it to do something. If we were to issue a command to the Media Player directly after opening it, there is no guarantee that the Media Source has been opened fully and can receive commands which may cause the command to fail.
    
5.  Off your **Media Player** reference, call the **Seek** function followed by the **Play** function.
    
6.  Create a **Stop Time** variable and connect it to the **Time** pin on the **Seek** node. Then connect the **Seek** and **Play** nodes to the **OnMediaOpened** event as shown.
    
    Click image to expand.
    
    Now when the Player presses the down arrow key, the current time is stored before closing the Media Player. When pressing down again, the **Video** Media Source is opened and when it becomes fully opened, the video moves to the specified **Stop Time** before playing the video (resuming playback).
    
7.  Close the **Level Blueprint** and click the **Play** button from the Main Toolbar to play in the Editor.
    

## End Result

You will now be able to use the **Up**, **Down**, **Left**, and **Right** arrow keys to control the playback of the video.

Pressing **Up** will play/pause the video, pressing **Down** will close/resume the video, pressing **Left** will rewind, and pressing **Right** will fast forward.