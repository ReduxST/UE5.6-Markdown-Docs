# Using Retarget Profiles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-ik-retarget-settings-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-ik-retarget-settings-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:02

---

In addition to **IK Retargeting** your characters during runtime, you can modify **Global**, **Root**, and **Chain** settings dynamically using **Retarget Profiles**. Retarget Profiles are an additional feature of the **Retarget Pose From Mesh** Animation Blueprint Node which you can use to change or animate these settings. This can be useful in cases where you need to change or apply different retarget settings at different points throughout an animation.

This document provides instructions on how to set up Retarget Profiles and various ways to modify them.

#### Prerequisites

-   You have set up characters to dynamically retarget at runtime using **Retarget Pose From Mesh**. Refer to the [Runtime IK Retargeting](/documentation/en-us/unreal-engine/runtime-ik-retargeting-in-unreal-engine) page for instructions on how to do this.
-   You are familiar with using [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).
-   You are familiar with creating and using [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine).

## Accessing Retarget Profiles

You can access Retarget Profiles from the **Retarget Pose From Mesh** node in the target character's Animation Blueprint you created in the [Runtime IK Retargeting](/documentation/en-us/unreal-engine/runtime-ik-retargeting-in-unreal-engine) prerequisite step. Select **Retarget Pose From Mesh** and locate the **Custom Retarget Profile** properties in the **Details** panel.

![retarget profile details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa1f3c8a-1f11-4c3c-a0a2-ce50f0201ca9/access1.png)

## Static Override

By default, the settings you set up in the assigned IK Retargeter Asset are used by the **Retarget Pose From Mesh** node. You can statically override those settings by modifying the **Custom Retarget Profile** properties on the node:

| Name | Description |
| --- | --- |
| **Apply Target Retarget Pose** | Enabling this overrides the [Retarget Pose](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#retargetpose) used for the target character. |
| **Target Retarget Pose Name** | If **Apply Target Retarget Pose** is enabled, this setting specifies the new Retarget Pose name to use instead. |
| **Apply Source Retarget Pose** | Enabling this overrides the [Retarget Pose](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#retargetpose) used for the source character. |
| **Source Retarget Pose Name** | If **Apply Source Retarget Pose** is enabled, this setting specifies the new Retarget Pose name to use instead. |
| **Apply Chain Settings** | Enabling this overrides the [Chain Settings](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#chainsettings) used in the IK Retargeter Asset with new ones specified below in **Chain Settings**. |
| **Chain Settings** | 
An array to add chains to override with new Chain Settings. Click **Add (+)** to add a new chain and set the name to match one of the retarget chains in the IK Retargeter Asset. Expand **FK**, **IK** or **Speed Planting** categories to modify the settings within.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f01d759b-dfdd-4f67-aec7-021f30b988fb/access2.png)

 |
| **Apply Root Settings** | Enabling this overrides the [Root Settings](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#rootsettings) used in the IK Retargeter Asset with new ones specified below in **Root Settings**. |
| **Root Settings** | If **Apply Root Settings** is enabled, these settings override the Root Settings used in the IK Retargeter Asset. |
| **Apply Global Settings** | Enabling this overrides the [Global Settings](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#globalsettings) used in the IK Retargeter Asset with new ones specified below in **Global Settings**. |
| **Global Settings** | If **Apply Global Settings** is enabled, these settings override the Global Settings used in the IK Retargeter Asset. |

## Dynamic Override

If you need to control when retarget settings change, then you must create additional blueprint logic. Due to the arbitrary nature of Blueprints and Animation situations, there are many ways you can create logic to edit a variety of retarget situations.

In this example, Retarget Profiles will be used to adjust the larger character's arm to correctly reach for the ground, matching the Mannequin.

![target character incorrect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/334cd9e9-a97d-44b6-8896-b63206b67ee9/animate0.gif)

### IK Rig Setup

Because of this specific retarget situation, you need to modify the target character's [IK Rig](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine) to use IK Goals and Solvers. This example uses a [Full Body IK (FBIK)](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine#fullbodyik) solver, however depending on your character, you could choose other kinds of [IK Rig Solvers](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine). This step is required to provide IK arm Chain Settings for the Retarget Profile to modify.

Open the target character's IK Rig Asset used for retargeting and do the following:

1.  Right-click one of the hand bones in the **Hierarchy** panel and select **New IK Goal**.
2.  In the next prompt, ensure **Full Body IK** is set as the solver and click **Add Solver**.
3.  Select the **Full Body IK solver** in the **Solver Stack** panel, then right-click the other hand bone and select **New IK Goal**.
4.  Lastly, select the **Full Body IK solver**, right-click the root bone (typically the **pelvis** or **hips**) in the hierarchy and select **Set Root Bone on Selected Solver**.

![create FBIK goals and solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36cfc8cd-facc-4b07-bb83-74b00a50702a/ik1.png)

#### FBIK Settings

Select **Full Body IK** in the **Solver Stack** and set **Root Behavior** to **Pin to Input** in the Details panel. This is required to prevent the lower body from moving when the IK goals move.

![pin to input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/820cc3a6-eebf-4a38-9b37-9e5580ef7e0c/ik2.png)

You may also need to create additional bone settings for bones that are controlled by the FBIK solver. This resolves stiffness or incorrect joint rotation that can result from the FBIK solve. To create a bone setting, select the **Full Body IK Solver**, then right-click a bone you want to create settings for and select **Add Settings to Selected Bone**.

In this example, to resolve rotational stiffness for the spine, shoulder, and arm bones, bone settings were created for these bones (including any symmetrical bones) with the following properties:

-   **Spine\_01**
    
    -   **Rotation and Position Stiffness**: 0.75
-   **Spine\_02**
    
    -   **Rotation and Position Stiffness**: 0.75
-   **Spine\_03**
    
    -   **Rotation and Position Stiffness**: 0.75
-   **Clavicle\_l**
    
    -   **Rotation and Position Stiffness**: 0.8
-   **Lowerarm\_l**
    
    -   **Use Preferred Angles:** Enabled
        
    -   **Preferred Angles:** 0, 0, 45
        

![fbik bone settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e3bfed8-ec8c-4f64-8c65-67ef5fb6caca/ik3.png)

### Retarget Profile Variable Setup

Returning to the target Animation Blueprint, select the **Retarget Pose From Mesh** node. In the **Details** panel click the **Custom Retarget Profile** dropdown menu and enable **Expose As Pin**, which adds a Custom Retarget Profile pin on the node.

![expose custom retarget profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18f57867-04ac-4bec-9637-41d7f781883d/dynamic1.png)

Right-click the newly created pin and select **Promote to Variable**. This creates a new [Struct Variable](/documentation/en-us/unreal-engine/blueprint-struct-variables-in-unreal-engine) of type `Retarget Profile` and connects to the pin. The variable is also visible in the **My Blueprint** panel.

![promote to variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19e0699a-a14f-422c-954e-cb8f5769da26/dynamic2.png)

### Create Event Graph Logic

Open the [Animation Blueprint Event Graph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#eventgraph) and reference the **Retarget Profile variable** here, then do the following:

1.  Drag off it and create a **Get Chain Settings from Retarget Profile** node.
2.  Set **Target Chain Name** to the retarget chain that you want to animate. In this example it is `LeftArm`.
3.  Right-click **Return Value** and select **Split Struct Pin**.

![get chain settings from retarget profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a731fe75-20fe-4b37-a1bb-7a23c42029d1/eventgraph1.png)

Next, drag off **Return Value IK** and create a **Set** **members** **in TargetChainIKSettings** node. Select it, and enable **Static Offset** in the **Details** panel, which exposes the Static Offset chain property as a pin on the node.

![set members in target chain ik settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04038dba-1fe1-4585-a426-ab520e4bd46c/eventgraph2.png)

Drag off **Struct Out** and create a **Set Chain IKSettings in Retarget Profile** node, then do the following:

1.  Set **Target Chain Name** to the same chain name used earlier: `LeftArm`,
2.  Connect the **Retarget Profile** variable to the **Retarget Profile** input.

![set chain IK settings in retarget profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c5d628e-a1f2-41f7-8c6d-3ad86cfa97f8/eventgraph3.png)

Connect **Event Blueprint Update Animation** to this execution chain, and expose **Static Offset** as a variable by right-clicking the pin and selecting **Promote to Variable**.

![update animate event and expose static offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b078faa-9503-4634-8c30-f48d64cedb28/eventgraph4.png)

Finally, in the **Details** panel for the Static Offset variable, enable **Expose to Cinematics** and **Instance Editable**, which makes the variable editable externally.

![expose variable to instance and cinematics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4252692a-3e03-4bcd-b936-07a80c0a642c/eventgraph5.png)

### Animate Retarget Setting

Because you created logic in the Target's Animation Blueprint Event Graph and linked it to **Event Blueprint Update Animation**, you can animate the exposed variable in Sequencer the same way you would [animate Anim Instances](/documentation/en-us/unreal-engine/control-animation-blueprint-parameters-from-sequencer-in-unreal-engine).

Assuming you have already [created and opened a Level Sequence](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine), add the retargeted character blueprint to it and the source Skeletal Mesh Component, then [play an animation](/documentation/en-us/unreal-engine/how-to-add-cinematic-animation-to-a-character-in-unreal-engine) on the source component to observe the retargeting effects on the target.

![runtime retargeting in sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba3171a0-6f2e-459a-9d5c-623029f9ecae/animate1.gif)

Next, add the Chain Setting variable you exposed earlier by doing the following:

1.  Add the target Skeletal Mesh Component by clicking **Add Track (+)** on the **Blueprint Track** and select the **Target** component.
2.  Click **Add Track (+)** on the target **Component Track** and select **Anim Instance**.
3.  Select **Add Track (+)** on the **Anim Instance Track** and select the variable.

![add target anim instance track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/651ae83e-fcb2-4fc4-a2d6-28b9add7bcea/animate2.gif)

You can now [keyframe](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine) this track to adjust the chain property in real-time.

![keyframe retarget profile settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da0eb75a-90c1-4e44-8326-2c9556e62848/animate3.gif)

Animating Retarget Profiles in conjunction with [Runtime Retargeting](/documentation/en-us/unreal-engine/runtime-ik-retargeting-in-unreal-engine) provides you with a way to make fine-tuning adjustments to your runtime retargeting results without creating new animations or additional assets.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80b0cf9b-ed42-44b7-9544-8477688961e7/rtp_result1.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28312ec2-ec7c-48fb-84a3-3ae1da5a9bd4/rtp_result2.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bc112d4-a33f-4b04-b7e6-2c62fb48b3dd/rtp_result3.gif) |
| Original Animation | Animating Retarget Profiles on Large Character | Animating Retarget Profiles on Small Character |