# Rendering Out Cinematic Movies

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-out-cinematic-movies-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-out-cinematic-movies-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:55

---

As of Unreal Engine 5.0, Renderer Movie is deprecated. Instead, please use **[](/documentation/404)**.

Once you have created your cinematic (or even during your production process as part of daily reviews), you may want to render it out as a movie file that you can share with others. The **Render Movie** option in Sequencer enables you to share your movie with others as an AVI file that will play with most media players. 

In addition to rendering as a movie file, you can render your cinematic as an Image Sequence or render out [Custom Render Passes](/documentation/404) that you can use in an external application to finalize your scene. Selecting the Render Movie button will display the [Render Movie Settings](/documentation/en-us/unreal-engine/cinematic-render-settings-and-formats-in-unreal-engine) window, which you can use to define how your scene will be rendered. 

In the following example, we render out a sample scene and present some of the options available as part of the rendering process.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8182ddd0-f5ac-488c-b855-7c86fd243f37/heroimage.png)

## Steps

For this guide, we are using the **Blueprint Third Person Template** with **Starter Content** enabled.

1.  Inside your project, from the **Main Toolbar**, click the **Cinematics** button then select **Add Level Sequence**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/711382ba-ab81-444b-a836-e2ada236690d/rendermovie_01.png)
2.  In the **Save Asset As** window, enter a name for your Sequence, then click **Save**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/252d34e8-1046-4c6e-9944-0ac3abdb2b55/rendermovie_02.png)
3.  Inside the **Sequencer Editor**, click the **Add Camera** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e87cd4b2-006c-4a21-a79c-0df56bda1c94/rendermovie_03.png)
4.  In the Viewport, position the camera anywhere in the Level facing the Character, then press the **S** key to add a keyframe.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab3940f0-21ae-48d8-9fc7-0f47a2da7bab/rendermovie_04.png)
    
    We will shoot a sample scene where the camera pushes in on our the Character in the Level for a close-up shot.
    
5.  In **Sequencer** move to frame **150**, then move the Camera in the Level to a new location and press the **S** key to add a key. The camera will now move from our first keyframe to our second keyframe, pushing in on the Character.
    
6.  In **Sequencer**, click the **Render Movie** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a307e54-9c0a-4351-8461-ca56c219e9d2/rendermovie_06.png)
    
    The **Render Movie Settings** window will open.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18ea4282-b822-4956-aaaf-633c76eba5a4/rendermoviesettings.png "RenderMovieSettings.png")
    
    Under the **Capture Settings**, click the **Output Format** option to view the options, then select **Video Sequence**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84650476-df4b-4df2-a15b-ab19a405d48a/rendermoviesettings_options.png "RenderMovieSettings_Options.png")
    
    In addition to rendering out a movie, you can render out an Image Sequence or use [Custom Render Passes](/documentation/404).
    
7.  Under **General**, choose an **Output Directory** to save your cinematic to, then click **Capture Movie**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0f9b202-c240-420d-9d30-ebedbbfd166e/rendermoviesettings_output-1.png "RenderMovieSettings_Output-1.png")
    
    A preview window will appear while the rendering process occurs.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4015ddff-7162-4fc0-afb8-1478a7684668/rendermovie_10.png)
    
    If prompted to **Save**, click **Save** or **Don't Save** to continue as selecting **Cancel** will abort the rendering process.
    

## End Result

After the capture process, you will have a video file of your cinematic sequence (below is our rendered-out cinematic).

There are additional options available when rendering out video sequences. One that may be useful during production is the ability to add [Burn Ins](/documentation/en-us/unreal-engine/applying-burn-ins-to-your-movie-in-unreal-engine) to your video. Burn ins are overlays that are embedded with your video, generally to provide internal information about the frame being shown.

You can add the default burn ins to your video, or [custom burn ins](animating-characters-and-objects/Sequencer/HowTo/BurnIns) that you create, by enabling the **Use Burn In** option.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68a2c43c-84cb-4b7e-8c59-f360170cab2d/rendermoviesettings_burnin.png "RenderMovieSettings_Burnin.png")

This can be useful if you are doing reviews of a cinematic, as it will display timecode information as well as shot names and any other custom information you want to provide.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a16a486e-1b70-4dee-9915-5de74a98b175/burninsapplied.png)