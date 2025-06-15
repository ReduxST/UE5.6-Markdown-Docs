# Cinematic Shortcuts and Tips

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-workflow-tips-for-sequencer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-workflow-tips-for-sequencer-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:27

---

To improve your cinematic animation productivity, several shortcuts have been built into the Sequencer Editor. This document provides tips for common workflows, overcoming problems, and other helpful features of Sequencer.

## Playback

### Spacebar Playback Toggle

By default, using the **Space Bar** as a hotkey to toggle playback of your sequence only works if your window focus is on Sequencer. If your focus is on the Viewport, then pressing the Space Bar will instead cycle between transform manipulation modes.

You can make the Space Bar toggle playback of Sequencer regardless of window focus by following these steps:

### Inclusive and Exclusive Frames

Animation within Unreal Engine uses the concepts of "inclusive" and "exclusive" frames, which determine if a full frame is being included or evaluated fully. Typically this matters when defining **start** and **end frames** in your sequence, such as for [animations](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine), [shots](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine), or overall Sequencer playback times.

For Sequencer, the start frame is inclusive and the end frame is exclusive, which causes all frame data up to the end frame to be evaluated. In this example, where the start time is set to **0**, and the end time is set to **10**, this means that the actual elapsed time is **9.999** (repeating) frames. In other words, it evaluates up to, but not completely to, the end time. This mimics behavior seen in most non-linear editing software such as Adobe Premiere.

[![sequencer exclusive frame](https://dev.epicgames.com/community/api/documentation/image/523967be-ebd1-441d-8404-0921f20c7e20?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/523967be-ebd1-441d-8404-0921f20c7e20?resizing_type=fit)

Because of this functionality, you can expect the following behavior:

Sequencer's treatment of inclusive and exclusive frames differs from [Animation Sequences](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine), which includes both start and end frames. When an animation FBX is imported, Unreal Engine will include a small amount of data beyond the final frame, which causes the final frame to be fully included. This can be observed in Sequencer if you zoom in far enough on the end of an unedited Animation Section.

[![animation sequence inclusive](https://dev.epicgames.com/community/api/documentation/image/e0114b06-0869-4f46-85a7-39856743dfd4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0114b06-0869-4f46-85a7-39856743dfd4?resizing_type=fit)

However, trimming, and other [section editing](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine) operations on the animation will restore Sequencer's end frame exclusive behavior.

## Workflow Shortcuts

### Middle-Mouse Scrubbing

Similar to Autodesk Maya, you can change your current time without causing updates or evaluations to occur by clicking and dragging the **middle mouse button** in the timeline. This can be useful when you want to set additional bracketing keyframes at the same value but at different times. When manipulating the playhead in this way, it will change its color to **yellow** to indicate the sequence is not evaluating.

[![middle mouse scrub](https://dev.epicgames.com/community/api/documentation/image/2e24f221-7fc1-40d6-8198-1e1b7c455a60?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2e24f221-7fc1-40d6-8198-1e1b7c455a60?resizing_type=fit)

### Adding Actors to Sequencer

When dragging new Actors into your Level from the [Content Browser](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) or by [placing Actors](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine), pressing certain keys will also add them to Sequencer. Depending on the pressed key, it will add the Actor as either a [spawnable or possessable](https://dev.epicgames.com/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics).

-   Holding **Ctrl** will add the new actor to Sequencer as a possessable.
    
-   Holding **Shift** will add the new actor to Sequencer as a spawnable.
    

### Default Tracks

### Auto Size Shots

When adjusting start and end times of shots internally, you can automatically match the parent shot section to these edits using the **Auto Size** command. To do this, right-click the shot and select **Edit > Auto Size**. This can be useful if you are retiming your shot and want the shot section to match, without needing to re-trim manually.

### Shift Snapping and Alignment

When dragging section assets onto Sequencer tracks, such as [audio](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-audio-track-in-unreal-engine), [subsequence](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine), or [animation](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine) tracks, holding **Shift** will snap the dropped section to the Playhead location.

[![shift dragging](https://dev.epicgames.com/community/api/documentation/image/cbd8f241-7c96-43d0-a0f7-b5b1010dada4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cbd8f241-7c96-43d0-a0f7-b5b1010dada4?resizing_type=fit)

If **Snap to the Pressed Key** is disabled, you can still align the Playhead to keyframes by holding **Shift** and clicking the keyframe. This makes it easy to perform subsequent actions, such as changing the value of this keyframe, or aligning other keys to it.

[![shift alignment](https://dev.epicgames.com/community/api/documentation/image/32723209-ff2a-4509-83d7-9f050696a179?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/32723209-ff2a-4509-83d7-9f050696a179?resizing_type=fit)

## Workflow Tips

### Ultrawide Monitor Framing

When making cinematics with unconstrained aspect ratios, you may encounter situations where your shot composition can change if a monitor's aspect ratio differs greatly from the aspect ratio you originally intended. For example, if you created the following shot in a cinematic:

[![](https://dev.epicgames.com/community/api/documentation/image/0a50dff9-299b-46e0-8c8d-d9ea4cb8b233?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0a50dff9-299b-46e0-8c8d-d9ea4cb8b233?resizing_type=fit)

Then, if this shot was played on an ultrawide monitor, the drastic change in aspect ratio may severely disrupt the original framing.

[![](https://dev.epicgames.com/community/api/documentation/image/6c6ff67b-22fe-40f3-804a-2e6552230371?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6c6ff67b-22fe-40f3-804a-2e6552230371?resizing_type=fit)

In this situation, where maintaining the vertical framing is important, you can resolve this by navigating to the **Level Sequence Actor's Details** and do the following:

-   Enable **Override Aspect Ratio Axis Constraint**.
    
-   Set **Aspect Ratio Axis Constraint** to **Maintain Y-Axis FOV**.
    

[![](https://dev.epicgames.com/community/api/documentation/image/a7a3efcd-9c9f-40d7-97bf-9e8a30384787?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a7a3efcd-9c9f-40d7-97bf-9e8a30384787?resizing_type=fit)

Once done, your vertical frame-space is constrained, maintaining the framing on these characters no matter the aspect ratio.

[![](https://dev.epicgames.com/community/api/documentation/image/1e2551fe-f561-4f00-8205-9c7660c3f348?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1e2551fe-f561-4f00-8205-9c7660c3f348?resizing_type=fit)

## Warm-Up Rendering

When creating pre-rendered sequences with [Movie Render Queue](animating-characters-and-objects/Sequencer/movie-render-pipeline#movierenderqueue) (MRQ), it may be necessary to "warm up" each shot in order for various aspects of your scene to render correctly. For example, some common problems can be:

-   Particles and other effects activating at the start of the shot, instead of already being active.
    
-   Cloth and other physics-driven entities exhibit a noticeable "settle" at the start of the shot.
    
-   The first rendered frame of a shot can exhibit noticeable aliasing or other temporal artifacts (sparkles).
    

You can use various warm-up properties within Movie Render Queue's [Anti-Aliasing Render Settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-rendering-image-quality-settings-in-unreal-engine) to resolve these scenarios. Depending on the scenario, there may also be different considerations to take into account that will determine which settings are best to use.

### Particles

In some cases, you may want particles and other effects to be active for a certain duration of time before a shot begins. While real-time previewing might show the correct behavior, rendering with MRQ may cause your particle system to activate at the start of the shot, which is undesirable.

|   |   |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/f59c1506-3688-4a5d-bf62-bd7795837d7a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f59c1506-3688-4a5d-bf62-bd7795837d7a?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/fce10c79-135b-493d-a6f9-ddb5518685dc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fce10c79-135b-493d-a6f9-ddb5518685dc?resizing_type=fit)



 |
| 

Particle with no warm-up

 | 

Particle with warm-up

 |

For this particle scenario, you can resolve it in either of the following ways:

If your particle is **GPU-based**, then you will also need to enable **Render Warm Up Frames**.

[![render warm up frames](https://dev.epicgames.com/community/api/documentation/image/e5891dab-d171-43df-ad85-1eb553e6647f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e5891dab-d171-43df-ad85-1eb553e6647f?resizing_type=fit)

### Cloth and Physics

For cloth and other physics objects, a common problem when rendering is that they can exhibit a noticeable settle at the start of a shot. This is due to the game simulation not starting until the rendering begins, therefore physics needs time to settle to its true simulated state.

|   |   |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/8c12181d-c270-4e05-9953-14f44593423e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8c12181d-c270-4e05-9953-14f44593423e?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/d3fbb4fa-1435-45ff-a731-17816308c2fd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d3fbb4fa-1435-45ff-a731-17816308c2fd?resizing_type=fit)



 |
| 

Cloth settles at start (no warm-up)

 | 

No cloth settling (with warm-up)

 |

#### No Starting Motion

For shots where the character or physics object is not initially moving, such as being in an idle pose, you can fix this by setting a frame value on **Engine Warm Up Count**. This value can be arbitrary depending on how many frames are needed for your physics to settle. Typically, a value greater than 30 should be used.

[![engine warm up count](https://dev.epicgames.com/community/api/documentation/image/46a22cff-5951-447c-b73b-49789190eb8a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/46a22cff-5951-447c-b73b-49789190eb8a?resizing_type=fit)

#### Starting Motion

In scenarios where shots start with the physics object in motion, such as running or jumping, then **Engine Warm Up Count** will not produce an accurate result. This is because it only "warms up" the starting frame and does not take into account motion that may be occurring beforehand. Here you can observe the cloth in the left example starting at an unnatural rest position, then correcting as the simulation reacts to the motion.

|   |   |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/b5f405a8-96a5-49cf-bfe5-f3adac8cefe5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b5f405a8-96a5-49cf-bfe5-f3adac8cefe5?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/80b54f38-7c6d-4f00-ba57-e1949b31aa26?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/80b54f38-7c6d-4f00-ba57-e1949b31aa26?resizing_type=fit)



 |
| 

Cloth starts at rest (incorrect warm-up settings)

 | 

Cloth starts correctly behind (using correct warm-up settings)

 |

In order to resolve this, you must do the following:

This technique can be used to also build a movement history for other things, such as trail particles.

### Temporal Artifacts

Aliasing and other artifacts caused by rendering features that have a temporal component, such as Temporal Anti Aliasing (TAA), Temporal Super Resolution (TSR), or raytracing denoisers, can also occur on the first few frames of your shots. Typically, this issue appears as noticeable hard edges or grainy sparkling on reflective surfaces. This is due to the lack of temporal history being accumulated at the start of a render.

|   |   |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/3cb4d108-1ae0-45a1-888f-1146dc3efef4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3cb4d108-1ae0-45a1-888f-1146dc3efef4?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/dc25c96b-5897-4d70-8259-ebca1135a4ae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dc25c96b-5897-4d70-8259-ebca1135a4ae?resizing_type=fit)



 |
| 

Sparkling and jagged edges (no warm-up)

 | 

Smooth edges and highlights (with warm-up)

 |

To resolve this issue, you can do either of the following: