# Fix Foot Sliding with IK Retargeter

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fix-foot-sliding-with-ik-retargeter-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fix-foot-sliding-with-ik-retargeter-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:50

---

When using the [IK Retargeter](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine) to retarget animation between different characters, the target character may exhibit noticeable feet sliding. This can occur if leg lengths and stances between the source and target characters are very different, causing leg retargeting to be imperfect. To resolve this, you can use **Speed Planting** workflows which pin [IK Goals](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) in place when they should not be moving.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43290d73-96dc-498e-9d89-770d886a20e5/speedplantoff.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27a57a15-90d2-4ba7-b1ce-3708e42a99dc/speedplanton.gif) |
| Original retargeting results | Modified retargeted results using Speed Planting |

This document provides instructions on how to use Speed Planting to resolve foot sliding in your retargeted animations.

#### Prerequisites

-   You have retargeted animations from one character to another using the IK Retargeter. Refer to the [Retargeting Bipeds with IK Rig](/documentation/en-us/unreal-engine/retargeting-bipeds-with-ik-rig-in-unreal-engine) page for how to do this.
-   You are familiar with creating [Full Body IK](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine#fullbodyik) solvers in IK Rig.

## Source Animation Setup

The first step for setting up Speed Planting is to create [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) in the source animation that will define the speed of each foot bone throughout the animation. You can do this using [Animation Data Modifiers](/documentation/en-us/unreal-engine/animation-modifiers-in-unreal-engine) to generate the curve so that it produces accurate motion data quickly. The intent of this step is to use Animation Curve data to determine at what point during the animation the feet should be planted.

### Animation Data Modifier

In your source [Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine), from the main menu, go to **Window > Animation Data Modifiers**.

![open animation data modifiers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e17fbb54-cf73-4ee1-91f2-076feeda440a/setup1.png)

Next, add a Motion Extractor Modifier by clicking **Add Modifier > MotionExtractorModifier**. Do this for each foot bone within the source animation. In this example, two Motion Extractor Modifiers are added.

![add motion extractor modifier](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f39b0400-50f1-4016-8733-b49a5d0628f3/setup2.png)

Within both Motion Extractor Modifiers, set the following properties:

-   **Bone Name**: The name of the foot bone to watch for its speed. This example uses the `ball_r` and `ball_l` bones.
-   **Motion Type**: Translation Speed.
-   **Axis**: XYZ.

![motion extractor modifier properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df52c96c-d24a-4b91-887d-e2b8998415ad/setup3.png)

### Generate Speed Curve

Once your Animation Data Modifiers are set up, click **Apply All Modifiers** to generate speed curves for the specified bones.

![apply all modifiers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c05260e3-6e2e-4ecb-ac81-d7baec3d0bbb/setup4.png)

Double-click the curve track to open the [Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine) where you can see more detailed information about it. Select or hover your cursor over the keyframes to see the values. This information can be used to determine the threshold of speed at which the foot should be planted. In most cases, this means that the lower flat parts of the curve are where the foot is stationary, whereas the peaks are where it is in motion.

![check curve editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fcbea49-4c4c-440a-9d6b-dcff00ffeb78/setup5.png)

Because you modified this Animation Sequence and the [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) (due to creating a new curve), make sure you save both Assets now.

## IK Rig Setup

Continuing the setup process, you must now create IK Goals and Solvers for the leg chains on the target character. This example uses a [Full Body IK (FBIK)](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine#fullbodyik) solver, however depending on your character, you could choose other kinds of [IK Rig Solvers](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine). This step is required in order to pin the legs using IK when they become stationary during the animation.

### Create FBIK

Open the target character's **IK Rig Asset** used for retargeting, navigate to the **Hierarchy** panel, right-click the end bone in one of the leg retarget chains, and select **New IK Goal**.

![new ik goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f92b2e8-23b5-49b1-8b64-cd652285e5d4/fbik1.png)

In the following prompts, ensure **Full Body IK** is set as the solver and click **Add Solver**, then click **Assign Goal**.

![add solver and assign goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9efd0847-6878-4b91-9c09-2208a0491abf/fbik2.png)

Next, ensure that the newly created Full Body IK solver is selected in the **Solver Stack** panel, right-click the other foot bone, select **New IK Goal**, then click **Assign Goal**.

![new ik goal and assign](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a0999db-d7f8-4825-bdb6-930bfe6838de/fbik3.png)

Finally, select the **Full Body IK** solver, then right-click the root bone in the hierarchy and select **Set Root Bone on Selected Solver**. Typically, the root bone for an FBIK solver is the pelvis or hips.

![set root bone on selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88b9b6f0-e8b0-4763-a6df-b94736880bf2/fbik4.png)

### FBIK Settings

Depending on the bone structure of your character's legs, you may also need to create additional bone settings for bones that are controlled by the FBIK solver. This resolves stiffness or incorrect joint rotation that can result from the FBIK solve. To create a Bone setting, select the **Full Body IK Solver**, then right-click a bone you want to create settings for and select **Add Settings to Selected Bone**.

![fbik settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7a78c64-a3e5-44ca-9379-7abd20ea611d/fbiksettings1.gif)

In this example, to resolve rotational stiffness for some leg bones, bone settings were created for these bones with the following properties:

-   **thigh\_l**
    -   **Use Preferred Angles**: Enabled
    -   **Preferred Angles**: 0, 0, -45
-   **calf\_l**
    -   **Use Preferred Angles**: Enabled
    -   **Preferred Angles**: 0, 0, 45
-   **thigh\_r**
    -   **Use Preferred Angles**: Enabled
    -   **Preferred Angles**: 0, 0, -45
-   **calf\_r**
    -   **Use Preferred Angles**: Enabled
    -   **Preferred Angles**: 0, 0, 45

![fbik preferred angles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc459191-985d-4ff2-b74c-b0bd2319501d/fbiksettings2.png)

Depending on your character's needs, there may be other bone settings required to ensure your FBIK solver functions correctly, such as **Stiffness**, **Limits**, and **Mass Multiplier**. Refer to the **Full Body IK** section of the [Solvers](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine) page for more information.

## Speed Planting in IK Retargeter

Next, open the **IK Retargeter Asset** for your characters. In the viewport select either the IK Goal or the chain, and in the **Details** panel enable **Speed Planting**.

![enable speed planting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/397d7d9f-135b-4847-9bde-11492ef37495/speed1.png)

Set the following properties in the **Speed Planting** section:

-   Set **Speed Curve Name** to the name of the corresponding leg curve that was generated earlier on the source character. In this example it is set to `ball_l_translation_speed_XYZ`.
-   Depending on the generated curve values, you may need to adjust **Speed Threshold** to a number that is slightly higher than where the curve stays flat. If you notice that your character's feet are still unplanting inappropriately, then increase this number. In this example, it is set to **30**.

Do this for all necessary leg chains on your target character.

![speed planting properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4868f0b-e551-4c36-971b-05dc166b297b/speed2.png)

## Final Result

Now when you play animations in the retargeter, you should see better feet planting for your target character. You can now [export](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#previewanimationandexport) the retargeted animation to a new Animation Sequence.

![final result](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d00b8717-cfa8-4b86-816d-db1b58498ef8/speed3.gif)