# Animation Notifies

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:22

---

**Animation Notifications** (Animation Notifies or just Notifies) provide a way for you to create repeatable events synchronized to **Animation Sequences**. These events can be sounds (such as footsteps for walk or run animations), spawning particles, and other types. Animation Notifies have any number of different uses, and the system can be extended with custom types.

This document provides an overview of the different types of Animation Notifies, how to create them, and how to use them in a variety of ways.

#### Prerequisites

-   Animation Notifies are created within [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine), therefore your project needs a **Skeletal Mesh** and an **Animation Sequence**.

## Getting Started

Animation Notifies are commonly accessed and created within Animation Sequences. To get started, open an **Animation Sequence Asset**, and locate the **Notifies** track in the timeline.

![notify track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ab47103-6082-4733-b574-b4ef50cc7d40/start1.png)

The Notifies track itself is a parent group for individual child tracks below, which contain the actual notify keyframes. By default, a single child track should exist (named **1**). If no child tracks exist, or if you want to add extra notify tracks, click **Add Track (+) > Add Notify Track** on the Notifies track.

![child notify tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eeda4ef2-f99d-4228-8c8e-609b92b8815f/start2.png)

You can also insert or remove notify tracks by clicking the **Add Track (+) dropdown menu** on the child track itself and selecting either **Insert Notify Track** or **Remove Notify Track**.

![insert and remove notify tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00f1ca05-8a68-4474-9815-d2b4bcf0f46e/start3.png)

To rename a Notify track, triple-click on the track text to enable text editing.

![rename notify track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48b059ad-05aa-462e-9dd9-fc989d05503d/start4.gif)

## Animation Notify Types

There are several types of Animation Notifies you can create, which are viewed when creating Notifies by right-clicking in the Notify track's timeline region.

![animation notify types](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17678c1c-323d-4100-b15b-6145a717fec7/types.png)

### Notify

The most basic kind of Animation Notify you can create is simply called a **Notify**, which causes different pre-made events to be triggered at a specified time. The following Notifies can be found when viewing the **Add Notify…** menu. Selecting one will create the Notify keyframe at your cursor position.

![notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3cead08-4907-4133-94c8-691331e5ca3a/typenotify1.png)

Notify keyframes can be edited by dragging them in the timeline. You can also hold **Shift**, which will move the **Playhead** in sync with the Notify, making it easier to align the Notify with a specific time in the animation.

![interact with notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/773cf240-72d8-46da-a01b-d5499a9d0225/typenotify2.gif)

#### Particle Effect

**Particle Effect** Notifies are used to spawn and play non-looping particle systems. You can select either:

-   **Play Niagara Particle Effect**, which spawns [Niagara particles](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine).
-   **Play Particle Effect**, which spawns [legacy Cascade particles](https://docs.unrealengine.com/4.27/RenderingAndGraphics/ParticleSystems).

This Notify is useful for creating repeatable particle effects, such as an effect when a character lands from jumping, shooting effects for a Skeletal Mesh weapon, or other similar effects.

![particle notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/216c8796-50fa-4b74-b022-3f89ad9338ab/particle1.gif)

When selecting the Particle Notify keyframe, the following relevant properties are located in the **Details** panel:

![particle notify properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df5d997d-ab5c-40eb-b4c5-32ee48630001/particle2.png)

| Name | Description |
| --- | --- |
| **Particle System / Niagara System** | The Cascade or Niagara system to spawn for this Notify. |
| **Location / Rotation / Scale Offset** | An array of location, rotation, and scale transform properties to offset the system from its spawn point. |
| **Attached** | When spawned on a [Socket](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine), enabling this causes the particle system to follow the Socket for its full duration. Disabling this still spawns the particle system at the Socket location, but the system does not continue to follow the Socket. |
| **Socket Name** | You can specify a bone or [Socket](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine) here, which spawns the particle system at its location. If nothing is specified here, then the system spawns at the root of the object. |

#### Sound

**Sound** Notifies are used to play sound effects from imported Sound Waves, [Sound Cues](/documentation/en-us/unreal-engine/sound-cues-in-unreal-engine), and [MetaSounds](/documentation/en-us/unreal-engine/metasounds-in-unreal-engine). These Notifies are useful for synchronizing foley-type sounds to animations, such as footsteps, cloth movements, and similar repeatable sounds.

When selecting the Sound Notify keyframe, the following relevant properties are located in the **Details** panel:

![sound notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b58a33ee-c207-4931-8487-f7750a17e4d2/sound1.png)

| Name | Description |
| --- | --- |
| **Sound** | 
The sound asset to play for this Notify. You can select the following assets:

-   Sound Wave
-   Sound Cue
-   MetaSound
-   Sound Bus



 |
| **Volume Multiplier** | A multiplier to increase or decrease the volume of the playing sound. |
| **Pitch Multiplier** | A multiplier to increase or decrease the pitch of the playing sound. |
| **Follow** | If enabled, the sound effect source follows the animated mesh as it moves. If disabled, the sound remains behind at the location it spawned. |
| **Preview Ignore Attenuation** | If enabled, [sound attenuation](/documentation/en-us/unreal-engine/sound-attenuation-in-unreal-engine) is disabled when playing the sound. This setting is editor-only and does not impact normal sound attenuation operation when playing or simulating the game. |
| **Attach Name** | If **Follow** is enabled, you can specify a bone or Socket to attach to. If nothing is specified here, then the sound spawns at the root of the object. |

#### Clothing Simulation

**Clothing Simulation** Notifies are used to pause, resume, and reset cloth simulations on a character. These Notifies are useful if you are teleporting the character during the animation and need to pause or reset cloth evaluation. They can also be useful if your animations are causing the cloth simulation to overreact.

![cloth notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc9bac01-9d49-4f60-a628-3bf648e3d6ab/cloth1.gif)

You can select the following Notifies:

-   **Pause Clothing Simulation**, which pauses the simulation.
-   **Resume Clothing Simulation**, which restores the simulation after having been paused.
-   **Reset Clothing Simulation**, which initializes the simulation back to its default reference pose.

#### Reset Dynamics

The **Reset Dynamics** Notify can be used to restore any [AnimDynamics](/documentation/en-us/unreal-engine/animation-blueprint-animdynamics-in-unreal-engine) used on this Skeletal Mesh back to their original state. This Notify is useful if your animations are causing the AnimDynamic simulation to overreact or enter broken-looking states.

### Skeleton Notify

**Skeleton** Notifies are custom Notifies saved on the [Skeleton Asset](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), and then used as events within your [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine). These Notifies are useful for creating any arbitrary Blueprint logic you want a Notify to execute.

To create a Skeleton Notify, right-click on a Notify track, then select **Add Notify > New Notify…**

![skeleton notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2c883d5-13e7-4afd-a598-e56bfccdfa5a/skelnot1.png)

You will be prompted to enter a name for the newly created Notify. Name it and press **Enter** to create the Skeleton Notify.

![skeleton notify creation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9abec0ed-37cb-40f7-823e-68adf2f46c37/skelnot2.png)

Skeleton Notifies are stored on the **Skeleton Asset**. Therefore, when creating them, you are also editing the [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), which requires you to save it.

You can also add currently-existing Skeleton Notifies to the timeline by right-clicking a Notify track, then selecting one from the **Add Notify > Skeleton Notifies** menu.

![add pre-exiting skeleton notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d7f5ada-edf6-4fb2-9c6c-b1ce427af085/skelnot3.png)

Skeleton Notifies are used as **Notify Events** within Animation Blueprints, either in the [Event Graph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#eventgraph) or [Transition Graph](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine). To add a **Skeleton Notify Event**, right-click in the **Event** or **Transition Graph** of your **Animation Blueprint** and select the **Notify** from the **Add Anim Notify Event** menu. This adds the event node to the Graph which is executed when the Notify is called from the animation it resides in.

![skeleton notify animation blueprint event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37cb7236-0d4a-485d-94a9-5af7864a349e/skelnot4.png)

### Notify State

**Notify States** work similar to standard Notifies, however they operate over a duration, rather than a single event. Because of this, they provide three distinct events: a **start**, an **update**, and an **end**. These events can be accessed when creating [Notify State child classes](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#customnotifyclasses).

Also like standard Notifies, they provide several different pre-made classes to choose from. You can find the following notifies when viewing the **Add Notify State…** menu. Selecting one creates the Notify keyframes at your cursor position.

![animation notify state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb21d25b-aba2-4c67-80ed-a1db72fac9bd/notifystate1.png)

Notify State keyframes are edited similar to normal Notifies by dragging them in the timeline. You can either drag the start or end to edit the range, or drag the whole Notify.

![interact with state keyframes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37efb6e7-93a2-464a-a701-e23cc6aea9c2/notifystate2.gif)

#### Timed Particle Effect

Similar to [Particle Effect](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#particleeffect) Notifies, **Timed Particle / Niagara Effects** Notifies are used to play particles during an animation. The main difference is that you can also define the duration of the particle, if the particle is set to loop. You can select the following types of Particle Notifies:

-   **Timed Particle Effect**, which spawns [legacy Cascade particles](https://docs.unrealengine.com/4.27/RenderingAndGraphics/ParticleSystems).
-   **Timed Niagara Effect**, which spawns [Niagara particles](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine).
-   **Advanced Timed Niagara Effect**, which spawns Niagara particles with extra options for driving parameters within them.

Timed Particle Notifies share the same details with normal Particle Effect Notifies, however Advanced Timed Niagara Notifies contain the following additional properties:

![timed particle notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce42c032-5187-4c5b-8634-5dbc19d00f10/timedparticle1.png)

| Name | Description |
| --- | --- |
| **Enable Normalized Notify Progress** | When enabled, causes the Notify state to output a normalized (0-1) value over the duration of the Notify to the Niagara [User Parameter](/documentation/en-us/unreal-engine/overview-of-niagara-effects-for-unreal-engine#parametersandparametertypes) specified in **User Parameter**. The parameter starts at **0** and interpolates to **1** upon the notify finishing. This property is useful if you want to link certain particle parameters to the lifetime of the notify. |
| **User Parameter** | The name of the Niagara User Parameter to drive if **Enable Normalized Notify Progress** is enabled. |
| **Anim Curve Parameters** | 
An array where you can link [Animation Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) values to Niagara User Parameters. You can add items to the array by clicking **Add (+)**, then specify the following properties:

-   **Anim Curve Name**, which is the Animation Curve that drives the Niagara parameter.
-   **Niagara User Float**, which is the Niagara User Parameter controlled by the Animation Curve.



 |

#### Trail

**Trail** Notifies are similar to Timed Particle Effects in that they spawn a particle system over the duration of the Notify. It differs because it is primarily used for [AnimTrail Cascade Particles](https://youtu.be/5HkghxEIXiU)**,** and contains additional properties for controlling trail attachment and properties.

![trail notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b3f27c0-f8d0-4500-b523-1dd8022b0694/trailnotify1.gif)

Selecting the Trail Notify reveals the following properties in the **Details** panel.

![trail notify details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d348ab4e-cd30-4936-ad64-77bd122982b2/trailnotify2.png)

| Name | Description |
| --- | --- |
| **PSTemplate** | The AnimTrail Cascade Particle system to use. |
| **First / Second Socket Name** | You can specify a separate bone or Socket here for each property, which are used to define the attach points for the AnimTrail. This also defines the trail's default width, based on the distance between these two attach points. |
| **Width Scale Mode** | 
If **Width Scale Curve** is used, this defines the relative scale point of the trail's width. You can select the following options:

-   From Centre, which scales the trail relative to the **center point** between the two sockets.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa4f86b8-a6ae-47df-998d-64e7b4dcfce9/trailnotify3.png)
    
-   From First Socket, which scales the trail relative to the location of the **first Socket**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dd3d703-5628-4480-b5d3-7fb0b2d85fbb/trailnotify4.png)
    
-   From Second Socket, which scales the trail relative to the location of the **second Socket**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/551d4531-c8ad-4742-8045-cd033e4a768b/trailnotify5.png)
    



 |
| **Width Scale Curve** | You can optionally specify an [Animation Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) here, which can be used to animate the scale width of the trail during the animation. A value of **1.0** maintains the default width, higher numbers increase the width, and lower numbers decrease the width. |
| **Render Geometry** | Enables rendering of the main trail geometry, leave this enabled. |
| **Render Spawn Points** | Enables debug rendering of the primary spawn points for the trail. |
| **Render Tangents** | Enables debug rendering of the curve tangents. |
| **Render Tessellation** | Enables debug rendering of all vertices on the curve, showing how the curve is tessellated between the spawn points. |

### Sync Marker

Sync Markers are Notifies used to inform [marker-based animation syncing](/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine#marker-basedsyncing), which is useful for blending animations together and keeping overall motion synchronized. Similar to [Skeleton Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#skeletonnotifes), Sync Markers save to the Skeleton Asset, which requires you to save the Skeleton when adding them. You can then use the same Sync Markers repeatedly in any animation you want to synchronize while blending.

![sync marker notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb9c2821-fabc-4aa1-a378-097eb759afea/markers1.png)

To learn more about using Sync Markers, refer to the [Sync Groups](/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine) page.

## Montage Notifies

When creating [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine), additional Animation Notify types are available to you to support montage-specific workflows. The following Notifies can be added in montages:

-   **Montage Notify**, which can be added by right-clicking on the Notify timeline and selecting **Add Notify > Montage Notify**.
-   **Montage Notify Window**, which can be added by right-clicking on the Notify timeline and selecting **Add Notify State > Montage Notify Window**.
-   **Disable Root Motion**, which can be added by right-clicking on the Notify timeline and selecting **Add Notify State > Disable Root Motion**.

### Montage Notify

A **Montage Notify** operates similarly to standard Notifies in that it executes an event upon reaching the Notify keyframe. When reached, the **On Notify Begin** event is executed on the [Play Montage](/documentation/en-us/unreal-engine/animation-montage-editor-in-unreal-engine#playinganimationmontages) Blueprint function. This requires playing the montage using the **Play Montage** node, instead of the **Play Anim Montage** node.

![montage notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/031243f2-6b16-4e69-a853-d635f3fb8973/montagenotify1.png)

### Montage Notify Window

A **Montage Notify Window** operates similarly to Notify States, in that the Notify operates over a duration you define. This causes both **On Notify Begin** and **On Notify End** to execute when the start and end of the Notify are reached. This requires playing the montage using the **Play Montage** node, instead of the **Play Anim Montage** node.

![montage notify window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdfb23f1-c830-4575-b7be-b37450fbc0de/montagenotify2.png)

### Disable Root Motion

A **Disable Root Motion** Notify operates similarly to Notify States, in that the Notify operates over a duration you define. This Notify suppresses root motion, allowing for user-input to control a character for its duration. This can be useful if you want to allow input control during parts of a montage, which locks out input by default.

![disable root motion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6974d01-8d36-47f9-b0e7-b8479f0791c5/montagenotify3.png)

## Managing Your Notifies

As you create and use Animation Notifies, there are several features and properties that you can use to customize your workflow and Notify behavior.

### Keyframe Editing

You can view information and commands for your Notify keyframes by right-clicking on them. The context menu shows the following:

![notify keyframe properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4b4e00c-4e03-4a46-841e-d3a7d8eaaad2/managing1.png)

| Name | Description |
| --- | --- |
| **Notify Begin Time** | The time (in seconds) that this Notify is placed in the animation. |
| **Notify Frame** | The time (in frames) that this Notify is placed in the animation. |
| **Min Trigger Weight** | Determines how much weight (between **0** and **1**) the animation needs to have to trigger the Notify. This is only relevant if the animation is being blended with another. The default value of **0.00001** means that even if this animation is barely blended in, the Notify will still execute. Setting it to higher numbers means that the animation must be blended in more fully in order for the Notify to successfully execute. |
| **Anim Notify State Duration** | The time (in seconds) of this Notify State's duration. |
| **Anim Notify State Frames** | The time (in frames) of this Notify State's duration. |
| **Copy** | Copies this Notify. |
| **Delete** | Deletes this Notify |
| **Replace with Notify…** | Replaces this Notify with another of the same type. |

To assist with keyframe alignment, you can enable snapping options by right-clicking the top of the timeline and enabling either **Frames** or **Notifies**.

![notify keyframe snapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fca92aac-f003-4c93-b3c0-a457ec5d7747/managing2.gif)

### Common Notify Properties

In addition to the properties that can be modified for each type of Notify, Notifies also contain the following common properties:

| Name | Description |
| --- | --- |
| **Notify Color** | Sets the color of the Notify keyframe. |
| **Should Fire in Editor** | Enables the Notify executing when previewing it in the Editor. This does not impact normal gameplay or simulation. |
| **Notify Trigger Chance** | Defines the chance of the Notify executing successfully. A value of **0** means the Notify never executes, and **1** means the Notify always executes. |
| **Trigger on Dedicated Server** | Enabling this causes the Notify to execute on dedicated servers. |
| **Trigger on Follower** | If enabled, this Notify also triggers when the animation is a follower, when using [Sync Groups](/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine). By default, only Sync Group leader animations execute their Notifies. |
| **Notify Filter Type** | Defines a method for filtering Notifies to control if they should execute or not. You can filter by [LOD](/documentation/en-us/unreal-engine/skeletal-mesh-lods-in-unreal-engine) and specify the maximum LOD to filter the Notify from. |
| **Trigger Weight Threshold** | Determines how much weight (between **0** and **1**) the animation needs to trigger the Notify. This is only relevant if the animation is blended with another. The default value of **0.00001** means that even if this animation is barely blended in, the Notify still executes. Setting it to higher values means the animation must be blended in more fully for the Notify to successfully execute. |
| **Montage Tick Type** | 
When using Montage Notifies, this property determines how the Notify is ticked and executed in regards to its accuracy and sequential ordering. You can select either:

-   **Queued**, which is a less precise, asynchronous, but more performant ticking method. Select this if you are okay with minor frame inaccuracy when your Notify executes.
-   **Branching Point**, is a more precise, synchronous, and higher-cost ticking method. Select this if you want to ensure your Notify executes with maximum frame accuracy, which can be useful if you are using the Notify to execute other events in a controlled sequence. For example, Branching Point is useful when making gameplay-altering decisions, such as branching a decision based on this Notify.



 |
| **Slot** | When using Montage Notifies, this property links the Notify to an animation within a specific Slot, as [some montages can have more than one Slot](/documentation/en-us/unreal-engine/animation-montage-editor-in-unreal-engine#usingmultipleslots). |
| **Link Method** | 

When using Montage Notifies, this property defines the method to link a Notify to an animation. Linking will cause the Notify keyframes to follow the montage animation section if they are adjusted. You can select from:

-   **Absolute**, which disables any automatic adjustment.
-   **Relative**, which will move the notify with the segment, but not adjust if the scale changes.
-   **Proportional**, which will both move and adjust with the segment location and scale.



 |
| **Linked Sequence** | A read-only property that displays the currently-linked Animation Sequence. This changes if you align the Notify with a different sequence in a multiple-sequence montage. |

### Animation Notify Panel

The Animation Notifies panel can be used to manage your currently existing [Skeleton Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#skeletonnotifies). You can access it by right-clicking in the Notify timeline area and selecting **Manage Notifies**.

![animation notify panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e71c83f-be55-4308-8018-0e2522998458/managing3.png)

You can right-click on a Notify and perform the following actions:

![notify panel options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42e4bc8a-9308-4f4e-b6da-d8302aa030dd/managing4.png)

| Name | Description |
| --- | --- |
| **New…** | Creates a new Skeleton Notify. |
| **Rename** | Renames the currently-selected Skeleton Notify. |
| **Delete** | Deletes the currently-selected Skeleton Notify. |
| **Find References** | Opens the [Animation Asset Browser Panel](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine#assetbrowser) and filters the list to only show animation assets that use this Notify. |

## Custom Notify Classes

If your project requires different Notify classes from those provided, you can create custom Notifies and Notify States with their own pre-defined Blueprint logic. This is a way for you to extend and create different Notify templates.

To create new Notify classes, navigate to the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) and click **Add (+) > Blueprint Class**. Navigate in the **All Classes** section and select either **AnimNotify**, to create a child class of a [Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#notify), or **AnimNotifyState**, to create a child class of a [Notify State](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#notifystate).

![create new notify class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8748e8f5-0aa6-4140-ab32-61eaed71d664/notifyclass1.png)

To start building unique functions for **AnimNotify** classes, click the **Override** function drop down menu in **My Blueprint** and select **Received Notify**. This opens the function graph where you can now script custom logic from the **Received Notify** entry node.

![override received notify function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/331f18d9-0aa6-4b7b-b462-d1f78172d5f7/notifyclass2.png)

You can override and implement the following functions in either **AnimNotify** or **AnimNotifyState** classes:

| Function | Description |
| --- | --- |
| **Get Default Trigger Weight Threshold** | This function sets the default value of **Trigger Weight Threshold** for this Notify, however it can be overridden in the [Notify keyframe details](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#commonnotifyproperties). |
| **Get Notify Name** | This function sets the name of the Notify or State keyframe in the timeline. |
| **Received Notify** | Used in standard Notifies, this function executes once when the Notify keyframe is reached. |
| **Received Notify Begin** | Used in Notify States, this function executes once when the Notify region begins. |
| **Received Notify End** | Used in Notify States, this function executes once when the Notify region ends. |
| **Received Notify Tick** | Used in Notify States, this function executes continuously throughout the duration of the Notify State. |

Once you have created your custom Notify class, you can add it to the Notify timeline from either the **Add Notify** or **Add Notify State** menu.

![notify class](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52ef961a-ce59-4cb7-b404-6266b9d7913a/notifyclass3.png)