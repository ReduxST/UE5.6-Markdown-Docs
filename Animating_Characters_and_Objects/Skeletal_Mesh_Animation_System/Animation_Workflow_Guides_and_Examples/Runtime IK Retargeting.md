# Runtime IK Retargeting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/runtime-ik-retargeting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/runtime-ik-retargeting-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:36

---

One of the options available to you when retargeting characters using [IK Retargeting](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine) is to retarget during runtime sessions. Doing this means you can retarget to other characters without generating new [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine), or during [Live Link](/documentation/en-us/unreal-engine/live-link-in-unreal-engine) sessions.

This document provides instructions on how to set up a character to retarget to another during runtime sessions using **IK Retargeting** and **Retarget Pose From Mesh**.

#### Prerequisites

-   You have created an **IK Retargeter Asset** retargeting from one character to another. Refer to the [Retargeting Bipeds with IK Rig](/documentation/en-us/unreal-engine/retargeting-bipeds-with-ik-rig-in-unreal-engine) page for how to do this.
-   Although not absolutely required, your source character should be gameplay controllable to better preview the retargeting effects at runtime. You can use the [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine), which contains a controllable Mannequin.

## Animation Blueprint Setup

The first main step is to create an [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) for the target character. In this example, the Mannequin is retargeting to the Stack-O-Bot, therefore, create a new **Animation Blueprint** for the Stack-O-Bot and a **Retarget Pose From Mesh Node**.

In the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine), click **Add (+)**, then select **Animation > Animation Blueprint**. In the next window, select the target **Skeletal Mesh** and click **Create**. Name your Animation Blueprint Asset and double-click it to open it.

![create animation blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/142b167e-04c2-459f-bff3-b62fe2853ce5/animbp1.png)

Next, right-click in the [Anim Graph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine) and select **Misc. > Retarget Pose From Mesh** to create this node, then connect it to **Output Pose**.

![add retarget pose from mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c197960e-3911-4a14-ab91-9e405896a701/animbp2.png)

Select the **Retarget Pose From Mesh** node and ensure the following properties are set:

-   Enable **Use Attached Parent**. Doing this simplifies content set-up, without needing you to find and assign the **Source Mesh Component** manually.
    
-   Set **IKRetargeter Asset** to your IK Retargeter Asset created as a [prerequisite](/documentation/en-us/unreal-engine/runtime-ik-retargeting-in-unreal-engine#prerequisites) for this tutorial.
    

![retarget pose from mesh properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f58365ef-e4b1-4a27-a105-d81bc6dfceb4/animbp3.png)

## Blueprint Setup

In this next step, you will need to set up both source and target characters in a single Blueprint and assign the Animation Blueprint created in the previous step to the Target character.

First, create a new **Actor Blueprint** by clicking **Add (+)** in the **Content Browser**, then select **Blueprint Class** and click **Actor**. Name your Blueprint Asset and double-click it to open it.

![create blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30559450-c74f-477b-a518-79b92b00b10f/bp1.png)

In the **Components** panel of the **Blueprint**, click **Add (+)** and add two **Skeletal Mesh Components**, one for the source, and the other for the target. Assign the **Skeletal Mesh Asset** property in the **Details** panel to the appropriate Skeletal Mesh Asset for each Component.

![add skeletal mesh components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ad17a70-9130-474e-9f92-3d3df06b6916/bp2.png)

If **Use Attached Parent** is enabled in your target Animation Blueprint, then the target Skeletal Mesh must be parented to the source Component so that the retargeting will work correctly. As this setting is based on using the parent Component as the source.

![parent components and use attached parent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3f06d0f-7e1d-4006-9a84-22cc6d49371f/bp3.png)

Select your source character and set **Animation Mode** to **Use Animation Asset**, then assign an animation to **Anim to Play**. Next, select your target character and assign the Animation Blueprint created earlier to **Anim Class**.

![assign animation blueprints to skeletal mesh components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87097987-0d65-466a-8469-2f87e35d4028/bp4.png)

You should now see the target character retargeting to the source character in the Blueprint Viewport.

![retargeting results in blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/592f6549-6219-4dc2-a7f5-48da77860bda/bp5.gif)

## Character Blueprint Example

Depending on your project's needs, runtime retargeting can be useful for prototyping gameplay animation on different characters. In this example, the **Third Person Template** Character Blueprint has been modified with the Stack-O-Bot added to the Blueprint.

![character blueprint setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e274378f-b98d-45d2-9aed-feedf85743c0/charbp1.png)

You can then create logic to switch **Visibility** between the different characters to preview the retargeting results in a gameplay scenario.

![gameplay example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1062a12-b7ab-43d7-8128-f10aeae8f77a/charbp2.gif)

In situations where you are hiding the source character, you must set **Visibility Based Anim Tick Option** to **Always Tick Pose and Refresh Bones** under the **Optimizations** category.

![always tick pose and refresh bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/846a1158-d934-4b9a-a698-5c95d63aedee/charbp3.png)