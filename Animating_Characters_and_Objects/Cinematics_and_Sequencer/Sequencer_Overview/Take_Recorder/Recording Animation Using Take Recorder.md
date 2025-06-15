# Recording Animation Using Take Recorder

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/recording-animation-using-take-recorder-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/recording-animation-using-take-recorder-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:00

---

**[Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine)** can record from various sources in both editor and gameplay contexts. The tutorials below illustrate how you can record your actions in Take Recorder.

## Record Actor Manipulation in the Viewport

You can use **Take Recorder** to record actor manipulation in the **[Viewport](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine)**.

1.  Add the object you want to record to the **[Sources](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#sources)** list.
    
    1.  Select the actor in the **Viewport**.
    2.  Click **Add Source (+) > From Actor > Add 'Sphere'**.
    
    ![Select the sphere as the source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38afbe43-893d-4b49-ae7c-faddc8ab22e9/select_sphere_source.png)
    
    Once the actor is sourced, you are ready to record your animation.
    
2.  Click **[Record](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#slate)**. A countdown and notification appears. When the countdown reaches 0, the sequence starts to record. Select your actor in the Viewport and move it around to capture its editor motion. When finished, click the **Stop** button or press the **Esc** key.
    
    ![Recording of hand animated sphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/850418ed-97fa-4c15-8388-1a04e010c1cb/hand_animation_recorded.gif)
3.  Click **Review Last Recording** to view the recording.
4.  Click **Play** in [Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) to observe your recorded actor data.
    
    ![Sequence playback](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a93ebdaf-cc96-4981-86de-8a6ea5113d6c/sequence_playback.gif)

You might see a duplicate actor performing the actions instead of the editor object. This is because the record type for the actor was set to record as a **[Spawnable Actor](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)**. You can change this on the source object or globally on the project by changing the **[Record to Possessable](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#userprojectsettings)** property in the Take Recorder details. If you record to a Possessable Actor, then you only see the original actor animate.

## Physics

You can use **Take Record** to capture physics simulations as animation data.

1.  Add a sphere to your scene.
2.  In order to break the sphere, you need to move the sphere away from the ground surface so it can gain momentum. Move the sphere up, away from the ground surface.
3.  In the Details panel, enable [Simulate Physics](/documentation/en-us/unreal-engine/playing-and-simulating-in-unreal-engine).
4.  Now, the timing to record physics to a sequence is a bit tricky. You need to start **Take Recorder** at the same time as you hit play to capture the motion you're looking to capture. In order to accomplish this, you need to remove the countdown timer for Take Recorder. Open the **Show/Hide [user/project settings](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#userprojectsettings)** (gear icon) in the Take Recorder panel.
5.  Under **User Settings**, set **[Countdown](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#usersettings)** to **0.0s**.
6.  Hover your mouse over **Record** in **Take Recorder**.
7.  Use the **hotkey Alt-P** to start playback and immediately click the **Record** in **Take Recorder**.
8.  Let the simulation play through and stop the recording (click **Stop Recording** or press **ESC**) when you are satisfied with the recording.
    
    ![Recording physics simulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3efe77cd-473b-47b5-90cc-76b61203fd4c/recording_physics_simulation.gif)

Now that you have recorded your physical simulation, you can review it.

1.  To open your take, click **Review Last Recording**.
2.  In **Sequencer**, click **Play** and watch your recording from any angle.

## Gameplay

You can use **Take Recorder** to record gameplay actions such as the player's movement and animation in a Level.

1.  From **Take Recorder**, select **Add Source (+) > Player** to add the **[Player Actor](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#sources)** to the **Sources** list
2.  Click **Play** in the Unreal Engine toolbar to start a [Play in Editor](/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine) (PIE) session.
3.  After the session has started, click **Record**. When the countdown reaches 0, the sequence starts to record. Move the character around your Level to capture its animation. When finished, click **Stop** or press **Esc**.
    
    ![Record gameplay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16c158e4-f418-4d39-88f4-1c1d8a2c78de/recording_gameplay.gif)
4.  Click **Review Last Recording** to view the recording.
5.  Click **Play** in Sequencer to preview the animation of your recorded player.
    
    ![Playback for gameplay recording](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20e0a5e4-c56a-4c34-8fd7-026b0a2a7cd8/gameplay_sequence_playback.gif)