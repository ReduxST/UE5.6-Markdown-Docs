# Applying Burn Ins

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/applying-burn-ins-to-your-movie-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/applying-burn-ins-to-your-movie-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:51

---

When creating and rendering out cinematic movies, you may want to include overlays with information about the scene you are viewing such as the name of the shot, the date, time or frame information. These overlays are referred to as **Burn Ins** as they are burned into the movie when it is rendered out. Often times you will see this process as part of real world movie making to provide directors, editors or anyone viewing the scene with contextual information about the scene (some will even be watermarked with copyright information).

**Sequencer** allows you to apply burn ins to your rendered out movies and provides a default burn in with general information about the shot. In this guide we take a look at how to enable the default burn in options when rendering out your cinematics.

For this how-to we are using the **Blueprint Third Person Template** project and have created a small sample cinematic.

## Steps

1.  Once you are ready to render out your **Level Sequence**, inside a **Level Sequence** click the **Render Movie** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1be5e68-dd6b-44a0-b839-07a96964e52c/overlay01.png)
2.  In the **Render Movie Settings** window, click the **Show Advanced** expand button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ca267bc-69bd-4b82-b42e-1b304b50971e/overlay02.png)
3.  Under **Burn in Options**, click the **Burn in Class** dropdown and select **DefaultBurnIn**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/501f97bf-881b-4050-b2c2-62272b1f3852/overlay03.png)
    
    This will enable the ability to define the burn in settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a144c3d-d2da-48f2-89c9-20d9fc08fa8e/overlay04.png)
4.  Leave the options as default, then click **Capture Movie**.
    

## End Result

When the capturing of your movie is complete, upon playing back your movie you will notice similar overlays applied to the cinematic. The Default Burn in applies the name of your Level Sequence across the Top Center followed by the current date. In the Bottom Left, the current Shot Name is applied (or Level Sequence name if no shots are used). The Bottom Center displays the time and frame count for the Master Sequence while the Bottom Right shows the current Shot Frame.

Each of these options can be changed to display your own text inside the **Settings** section of the **Burn in Options**. Additionally, you can apply Watermarks or make Font changes within the Default Burn In options.

You may want to view the video above in full screen or on YouTube to see the overlays more clearly.