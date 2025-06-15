# Enable Particles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-trigger-cinematic-particle-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-trigger-cinematic-particle-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:23

---

This page provides a beginner's overview of triggering effects in Sequencer and is intended for those who are new to Cinematics and Unreal.

#### Prerequisites

-   You have read through the [Sequencer Basics](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) page and have created and opened a **Level Sequence** in your level.
-   Your project contains [Niagara Systems](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine). The example below uses effects from the [Stack O Bot project](https://www.fab.com/listings/b4dfff49-0e7d-4c4b-a6c5-8a0315831c9c).

## Adding an Effect to Sequencer

Start by adding an effect to your Level. Do this by opening the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine), locate a **Niagara System** asset, and drag it into your Level.

![add particle to level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b57e9f4-5702-461a-b386-fba9f9a5bed1/addeffect.png)

You may want to disable the **Auto Activate** property in the Particle's **Details Panel**, to prevent interference with how you want to control it in Sequencer.

![disable auto activate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca0337e0-5285-4d36-b7d8-a1a24f8df58f/autoactivate.png)

Next, with your sequence open and the Niagara System selected, click **Add Track (+)** and select **Actor to Sequencer > Add 'Niagara System'**. This adds a track referencing the effect into your sequence.

![add particle to sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da08a0bf-7dd7-4069-abf9-01d5a41149d8/addeffect2.png)

Once the track is added, do the following:

1.  On the Niagara track, click **Add Track (+)** and select **NiagaraComponent0**.
2.  On the NiagaraComponent0 track, click **Add Track (+)** and select **FX System Toggle Track**.

![add component and add FX System track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cca5ac83-eed2-4c57-84e6-aa9e410e9ca7/addeffect3.png)

## Activating the Effect

Now that your effect is added to Sequencer, there are two main ways to trigger it depending on if the effect is meant to be [continuous](/documentation/en-us/unreal-engine/how-to-trigger-cinematic-particle-effects-in-unreal-engine#continuouseffects) or singularly [triggered](/documentation/en-us/unreal-engine/how-to-trigger-cinematic-particle-effects-in-unreal-engine#triggereffect).

### Continuous Effects

For effects that loop indefinitely, you need to create **Activate** and **Deactivate** keyframes.

First, select the FX System track, ensure the dropdown menu is set to **Activate**, then press **Enter**. This sets an **Activate** keyframe on the particle system track which enables the effect at this time.

![create activate keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3238e47b-fda2-4e75-baef-e83774261834/activate1.gif)

Next, move the playhead to a later point in the sequence by dragging it. Then click the dropdown menu on the FX System track and select **Deactivate**. This sets a **Deactivate** keyframe, which disables the effect at this time.

![create deactivate keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38379fb1-9e40-4ead-8cf0-80df55f2c276/deactivate.gif)

Now when you play your sequence, you should see the particle activate and deactivate at their corresponding keyframes.

![play effect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0e7d42b-f3e5-4134-ab78-007e10259aa8/regionplay.gif)

### Trigger Effect

For effects that are meant to only play once, and not loop indefinitely, you can use the **Trigger** keyframe.

To start, click the dropdown menu on the FX System track and select **Trigger**. This changes the type of keyframe to Trigger, which has no enable/disable states.

![set trigger mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa608f52-1f07-41c0-bbd4-02fb9f670445/triggerstate.png)

Next, select the **FX System** track and press **Enter** to place a keyframe. You should now see your effect play.

![create trigger keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c01b3632-c26b-434b-b0f8-bc2b53e860ab/trigger1.gif)

You can set as many **Trigger** keyframes as you want for the particle system. They will all trigger with their corresponding keyframes when the sequence is played.

![multiple trigger keyframes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdaff3c0-09c3-4772-ac6f-c747c3a5eed7/trigger2.gif)

## Animating Parameters

If your Niagara System contains [User Exposed Parameters](/documentation/en-us/unreal-engine/overview-of-niagara-effects-for-unreal-engine#parametersandparametertypes), you can animate them in Sequencer as well.

To access a parameter, click **Add Track (+)** on NiagaraComponent0 and select the **Parameter Track**. This adds a compatible [Property Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine) for the parameter.

![add niagara parameter track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6df97374-04f2-4b64-8136-4d5ad6d40ac4/param1.png)

Next, select the Parameter Track and press enter to create a keyframe, then move the playhead to a different location and change the property value on the track to set a new keyframe for that value. You can now play the sequence to see the parameter animate.

![animate niagara parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41f6caf3-74e5-466c-b93c-b2523a3dc40a/param2.gif)