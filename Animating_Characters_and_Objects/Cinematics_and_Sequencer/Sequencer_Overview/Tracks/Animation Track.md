# Animation Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:54

---

The Animation track applies animation to your Skeletal Mesh Actors using Animation Sequence assets in Sequencer. This guide provides an overview of the usage of this track and its properties.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).
-   Your project has a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) actor and can play [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) in it.

## Creation

By default, the Animation track is [automatically created](/documentation/en-us/unreal-engine/cinematic-editor-and-project-settings-in-unreal-engine#projectsettings) under your Actor's track when a Skeletal Mesh Actor class is added to Sequencer. If you have added a different Actor class that supports animation, or have deleted the track, then you can add the track manually by clicking **Add Track (+) > Animation** on the Actor's track, and selecting an **Animation Sequence**.

![add animation track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69844670-3162-49d7-8619-1cc405ef4e05/add1.png)

Doing this creates the Animation track with an Animation Sequence section at the playhead.

![sequencer animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfadc78d-26c0-446c-8604-46c732df5e37/createseq.png)

### Adding Animations

Once an Animation track is created, you can add animations to it. You can do this in the following ways:

Click **Add Animation (+)** on the Animation track and select an Animation Sequence. The animations listed here are filtered to only display [compatible](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine#compatibleskeletons) animations for the Skeletal Mesh.

![add animation sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/860dacef-29f3-4dbd-acb1-69adde8d3569/addanim.png)

You can also drag Animation Sequences from the **[Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine)** into the timeline area of Sequencer. This operation will preview the clip's length and drop points as you drag along the Animation track.

![drag drop add animation sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e87b6df9-56c7-41db-94d9-123b4c315187/dragdropanimcb.gif)

Dragging onto another clip will create a separate track for the animation.

## Usage

### Animation Mode

When a Skeletal Mesh is animated in Sequencer, its **Animation Mode** property will switch to **Use Custom Mode**. This is done to ensure Sequencer drives the Actor's animation using a special [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).

![animation custom mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b20a6a4-1277-4351-9e73-70aa04dbaca0/custommode.png)

Animation Mode will not switch to **Use Custom Mode** if an Animation Blueprint is already assigned. In that case, you should ensure the Animation Blueprint contains a [Slot](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine) to receive animation from Sequencer.

### Layers and Blending

The Animation track supports multiple track layers, animations, and allows animations to be blended together in various ways.

![sequencer animation layers blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1954ec63-1b39-4bf9-9577-6ff690783725/animlayers1.gif)

You can add a second animation by clicking **Add Animation (+)** and selecting another Animation Sequence. This will add the new sequence to your current playhead time. If your playhead is placed over an animation, then it will create a new track layer for the animation.

![sequencer animation layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5e0447f-c42c-41da-b8db-2eef53203253/animlayers2.png)

Expanding the Animation track reveals the Weight attribute for the section, which has a value range of 0-1. Weights can be keyframed to allow for dynamic weighting and blending of animation sections.

![sequencer animation weight](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e94c0e3-21a9-4155-a84b-32d7bea0367c/weight.png)

Animations can be moved between tracks by dragging them up and down.

![sequencer animation layer stack move up down](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15e7e028-d56f-49a5-a710-d1d8092560d3/animlayers3.gif)

Intersecting two animation sections creates an automatic blend curve between them, and the animations blend over the duration of the intersection.

![sequencer blend clips together](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8930f4ba-9a5e-4fdb-9ce6-372231b9ae73/animblending1.gif)

You can adjust the **Start** and **End** blend curves by selecting and moving the blend curve handle located on the upper portion of the animation section's edge. A curve symbol will appear above the cursor to aid your selection accuracy.

![sequencer start end blend curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f8882d8-3a33-4a34-9fc3-2ece68835780/animblending2.png)

Right-clicking a blend curve reveals blend-specific context menu commands.

![blend curve menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e939a01-4ae3-4f8e-95c9-a54fc480332d/blendcurvemenu.png)

| Name | Description |
| --- | --- |
| **Easing Length** | 
The length of the blend curve. Enabling **Auto** causes the blend curve to return to the default behavior and support automatic length calculation when sections are intersecting.

![blend curve length](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93263b7a-7b2e-4b5e-90fd-9629e9956c2f/easinglength.gif)

 |
| **Method** | **Method** controls the type of curves to apply to the blend, and enables custom external blends based on functions. |
| **Options** | 

The Options menu will display a list of curve shapes that you can apply to your blend curve. Selecting one of these will replace your current curve shape with the selected curve.

![blend curve shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f0f6871-d321-4b80-8335-a332b885309b/curveshapes.png)

 |

### Trim, Loop, and Play Rate

There are various ways you can edit your clips by looping, trimming, and time-scaling them.

Selecting either edge of the section and dragging inward will trim the section.

![sequencer trim animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/327ff64a-026d-48d7-b83e-8cdbcd98ae78/trim1.gif)

You can also split a selected animation section at the current playhead time by pressing **Ctrl + /**.

![sequencer split cut animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d148956-4776-47db-9678-e01876159c0e/split.gif)

Trim and split commands are also located in the **Edit** menu when right-clicking a section.

Sections can be looped by dragging the right-side edge outward. Loop segments are indicated by notches in the section.

![sequencer loop animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3485800-4dd3-4a9e-96e7-c328004e8711/loop.gif)

Holding **Ctrl** when hovering on a section edge will engage the **Play Rate** modifier.

![sequencer scale animation time play rate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12853750-8cf8-41fa-9d22-cd6bfa8fc507/scalemodifier.png)

Once the **Play Rate** modifier is engaged, dragging the clip edge will scale the clip's playback rate instead of looping or trimming.

![sequencer play rate animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/835350c5-a284-496a-b561-9b0c49e3f71c/ctrlscale.gif)

If you have trimmed or looped an animation and want to restore it to its original length, you can right-click it and select **Edit > Auto Size**.

## Properties

Animation tracks display the following properties when right-clicking them and navigating to the **Properties** menu.

![sequencer animation properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46007ad7-f0fd-4da2-b25a-4e2c98b80f2b/properties.png)

| Name | Description |
| --- | --- |
| **Section Range Start** | The start time of the animation section. |
| **Section Range End** | The end time of the animation section. |
| **When Finished** | 
Determines what the Actor should do when the animation section finishes.

-   **Keep State** will keep the Actor in Sequencer's animation mode. This will not cause the Actor to snap back to its previous state and will instead hold on its last animation frame.
-   **Restore State** will return the Actor back to its state before Sequencer animated them.
-   **Project Default** is the default behaviour, and will use the settings defined in your **DefaultEngine.ini** project file. Adding the following lines to the .ini file will set the project default.
    
    `[/Script/LevelSequence.LevelSequence]`
    
    `DefaultCompletionMode=KeepState`
    
    or
    
    `DefaultCompletionMode=RestoreState`
    



 |
| **Timecode Source** | The timecode information for the clip, if timecode is being used. You can also specify delta frames here to control offset information. |
| **Is Active** | Activates the selected section. This is similar to [**Muting Tracks**](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#mute), but is used for sections instead of tracks. |
| **Is Locked** | Locks the selected section. This is similar to [**Locking Tracks**](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine#lock), but for sections instead of tracks. |
| **Pre/Post Roll Frames** | 

Specifies the extra padding to apply to the start and end regions of your animation track. This padding causes the first and last frame of the animation to be held for the specified duration. The roll visual can be enabled or disabled in **[Sequencer's Editor Preferences](/documentation/en-us/unreal-engine/cinematic-editor-and-project-settings-in-unreal-engine#editorpreferences)** to preview this padding in the timeline.

![pre post roll hold start end frame](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3165409-bec6-410d-aaf9-9a6ce45c390d/prepostroll.png)

 |
| **Animation** | The **[Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine)** asset being referenced. |
| **First Loop Start Frame Offset** | 

When the sequence is being looped, this property controls the amount of start trim to apply to the first loop of the sequence. Subsequent loops will be full length.

When holding **Shift**, you can also change this value directly by dragging your mouse left and right.

![first loop start frame offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99e9e31e-4336-493c-8148-1e6fce0de7fe/shiftfirstloopoffset.gif)

 |
| **Start/End Frame Offsets** | The frame offset properties control the amount of offset to apply to the start and end of a section. The result is an effect similar to trimming, but looping will now respect these trimmed regions as the new loop segments. |
| **Play Rate** | The playback speed of the section. A value of **1.0** will result in normal-speed playback, lower values will playback more slowly, and higher numbers will playback more quickly. |
| **Reverse** | Enabling this will cause the sequence to play backwards, reversing the animation. |
| **Slot Name** | 

Specifies the [Animation Slot](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine) to play animation from. In order to use **Slot Name** you must also set the **Animation Mode** of your Skeletal Mesh to use the appropriate Animation Blueprint.

![sequencer animation slot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f983d00-4e7b-4280-9159-a2653de4d18f/slots.png)

 |
| **Mirror Data Table** | [Mirrors](/documentation/en-us/unreal-engine/mirroring-animation-in-unreal-engine) this animation according to the assigned Mirror Data Table Asset. |
| **Skip Anim Notifiers** | When enabled, any **[Animation Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine)** for this animation are ignored. |
| **Force Custom Mode** | When enabled, the Skeletal Mesh's **Animation Mode** will be forced into using **Custom Mode** for the duration of this animation. |
| **Swap Root Bone** | 

Options for making the root bone of the Skeletal Mesh swap with the following:

-   **Component**, which causes the Skeletal Mesh Component to follow the root bone.
-   **Actor**, which causes the Actor to follow the root bone.
-   **None**, which does not swap the root bone.



 |
| **Start Location Offset** | Specifies the location offset to apply to the Actor at the beginning of its animation when using root motion. |
| **Start Rotation Offset** | Specifies the rotation offset to apply to the Actor at the beginning of its animation when using root motion. |
| **Show Skeleton** | 

Draws a skeleton in the viewport for this animation sequence. Multiple animation sequence skeletons can also be enabled at once, allowing for the display of multiple skeletons per animation on the same character. This is useful when using Sequencer's **[Motion Blending](/documentation/en-us/unreal-engine/motion-blending-tools-in-unreal-engine)**.

![sequencer show skeleton animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73bafe0e-b96e-4468-9a39-51b8a0ed788e/skeletonview.png)

 |

## Blending Tools

The Animation Track also supports aligning bones in order to better support dynamic blending. Visit the **[Motion Blending](/documentation/en-us/unreal-engine/motion-blending-tools-in-unreal-engine)** page to learn more about this feature.