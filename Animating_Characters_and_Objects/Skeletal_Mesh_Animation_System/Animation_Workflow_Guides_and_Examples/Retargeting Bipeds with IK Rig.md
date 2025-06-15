# Retargeting Bipeds with IK Rig

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/retargeting-bipeds-with-ik-rig-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/retargeting-bipeds-with-ik-rig-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:17

---

Unreal Engine provides flexible tools for retargeting animation from one character to another. One of the ways you can do this is by using [IK Rigs](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine) in conjunction with the [IK Retargeter](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine), which make it possible to retarget characters with vastly different skeleton hierarchies and proportions. Retargeting animations is a way to share animation data between multiple different skeletons without needing to create and manage new animations outside of Unreal Engine.

This document provides an overview of how to use these tools to retarget animation between two different bipedal characters.

#### Prerequisites

-   Your project contains at least two different bipedal characters. This example uses the Unreal Engine Mannequin available from the [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) and the [Stack O Bot](https://www.fab.com/listings/b4dfff49-0e7d-4c4b-a6c5-8a0315831c9c).
-   Both characters should have different Skeleton Assets and bone hierarchies so you can maximize the rationale for retargeting this way. Otherwise, it may be better to use [Compatible Skeletons](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine#compatibleskeletons) if your characters have similar proportions and hierarchies.

## Source and Target IK Rig Setup

Retargeting with IK Rig requires a **source** and **target** Skeletal Mesh, which are defined by an **IK Rig Asset** for each of those meshes. Therefore, you must first create an **IK Rig** for each of the characters being used in the retargeting process.

1.  Open the Content Browser and click **Add (+) > Animation > IK Rig > IK Rig**.
2.  Select the Skeletal Mesh you wish to add the rig to.
3.  Do this for both characters, then open each IK Rig Asset.

![create ik rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d64983e-c9b9-4faa-aaf8-15703bfb76b4/iksetup1.png)

### Retarget Root

Within both IK Rig Assets, you must define the **root** for each character, which is typically the **pelvis** or **hip** bone. This is done in order for the character's root motion to be defined and transferred in a proportional way.

In the **Hierarchy** panel, right-click the bone and select **Set Retarget Root**. Do this in both IK Rig Assets.

![set retarget root](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/241a18d2-2f6b-4262-87b7-0a0db785944d/iksetup2.png)

Once done, the chosen bone shows an indication that it is the **Retarget Root** in the **Hierarchy** and the **IK Retargeting** panels.

![retarget root indication](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6516e9e1-acb8-496e-9ca8-eac705eb4f19/iksetup3.png)

### Retarget Chains

You must also define limbs and other appendages that you want to transfer in the retarget process on both the source and target IK Rigs. This is a process similar to *characterizing* your rig in other applications like Autodesk MotionBuilder or Maya. The main difference is that you define it by **joint chains**, rather than by individual bones. This provides flexibility in retargeting characters with vastly different bone structures.

You must create chains for all major limbs that you want to retarget. You can optionally create chains for minor limbs such as fingers, too. In this example, you will create the following chains in both IK Rigs:

-   Spine
-   Left Arm
-   Right Arm
-   Neck
-   Head
-   Left Leg
-   Right Leg

![retarget chains](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d565b2f-2c48-4411-b9c0-d283cd044270/iksetup4.png)

To create a chain, follow these steps:

1.  Select the first bone of the chain in the **Hierarchy** panel, then select all bones down the hierarchy until you reach the last bone of the chain.
2.  Right-click these bones and select **New Retarget Chain from Selected Bones**.
3.  In the **Add New Retarget Chain** dialog window, make sure the **Chain Name** is set correctly, then click **OK**. In most cases, IK Rig will automatically assign this value from its list of [common chain names](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#chainpropertiesandnames).
4.  In the **Add Goal to New Chain** dialog window, select **No Goal**. Typically, you do not need to add [IK Goals](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) unless your retargeting requires additional IK adjustments, such as [Speed Planting](/documentation/en-us/unreal-engine/fix-foot-sliding-with-ik-retargeter-in-unreal-engine), [Stride Warping](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#globalsettings), or **Blend to Source**.

![create chain](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/785fabc1-462d-4662-859d-0db04197b6ee/iksetup5.gif)

Repeat this step for all major chains in both IK Rig Assets. Once completed, the **IK Retargeting** panel should be populated with several chains.

![create chains](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0154ead-913e-45d6-84bf-7ccd843c9262/iksetup6.png)

It is valid for a chain to consist of a single bone. This can happen in some cases, such as for shoulders, neck, or head bones. In those cases, you can still right-click a single bone in the **Hierarchy** panel and select **New Retarget Chain from Selected Bones**. The chain entry will have the same bone defined in the **Start Bone** and **End Bone** fields.

## IK Retargeting

After you create the necessary bone chains, you can begin the retargeting process in the **IK Retargeter**. The IK Retargeter is an Asset that references both source and target IK Rigs. In the IK Retargeter Editor, you can customize how to transfer animation between the source and the target.

### Create and Set Up IK Retargeter

To create an IK Retargeter, do the following steps:

1.  Click **Add (+)** in the Content Browser, then select **Animation > IK Retargeter**.
2.  In the dialog window that appears, select the IK Rig that you want to retarget animation from.
3.  After you select a rig, name the new IK Retargeter Asset, then double-click it to open it in the IK Retargeter Editor.

![create ik retargeter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46b2fc49-58a4-48f6-aa09-8554841d84b7/retargeting1.png)

The IK Retargeter Editor only shows the source Skeletal Mesh in the viewport and in the **Source IKRig Asset** property. To add the target character, click the **Target IKRig Asset** dropdown menu and select the target IK Rig.

![add target ik rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6e9ff28-b6fc-409d-9a83-2196aa8b773f/retargeting2.png)

### Checklist Before Retargeting

Before continuing, there are a few things you should check to ensure the retargeting process is correct and accurate.

-   In the **Chain Mapping** panel, make sure the **Target** and **Source Chains** are matching. In most cases, the names should correctly auto-match. If not, then you can click the **Source Chain** dropdown menu and change the chain assignment to match with the **Target Chain**.
    
    ![matching chains](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f287a82-13b0-40a4-894f-d4c015df8271/retargeting3.png)
    
-   Make sure both characters have matching reference poses. If these reference poses differ, such as if one character is T-posed and another is A-posed, then you will need to adjust one of their [retarget poses](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine#retargetpose) so they match.
    
    ![matching retarget pose](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1b909b5-7ba9-4694-b5e2-425d58b945f4/retargeting4.png)
    
-   You can optionally adjust offset and scale settings in the **Details** panel to more easily see both source and target skeletons.
    
    ![offset target character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2d07b69-d227-4044-b0f2-5accae818f7f/retargeting5.png)
    

### Preview Retargeting

In the **Asset Browser** panel, double-click different animations to preview the retargeting effect on different Animation Sequences.

![preview retargeting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64af97fa-1a0f-4af3-9fd3-5fad5b3cfa71/retargeting6.gif)

### Export Retargeting Results

Once you are satisfied with your retargeting results on the target character, you can export the animations to [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) that are compatible with that character's Skeleton. To do this, select the animations you want to export in the **Asset Browser** panel, then click **Export Selected Animations**.

![export selected animations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0eedbe80-99f1-4f4e-97f5-c08d2dec63fc/retargeting7.png)

Specify your export path in the dialog window and click **OK** to export the animations. The retargeted animations will now be available in the output folder with the postfix `_Retargeted`.

![export naming](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01e08a2d-9257-474a-bf02-8ccdcb679df0/retargeting8.png)

## Embellishing Motion

If you are retargeting realistic motion-capture animation to a non-realistic character, the resulting animation may appear incorrect or strange looking. This can be somewhat subjective, but in these cases it may be helpful to perform extra steps to embellish or diminish certain character motions to achieve a more fitting appearance.

For example, when previewing a run animation on the retargeted robot character, you might want the character to have more bounce. The following steps detail how you can achieve this.

|   |   |
| --- | --- |
| ![running with no bounce](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bea26ce3-52e3-4110-a8f7-59b72ab02c96/embellishoff.gif) | ![running with bounce](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f85a8fe-1d10-4170-9995-46240213d2fa/embellishon.gif) |
| Original retargeting results | Retargeting with adjusted settings |

### Create IK Goals

The first step is to create IK Goals to ensure the feet stay planted on the ground when adding the extra bouncing.

Assuming no IK Goals are already created, open the IK Rig Asset for the target character. In the **Hierarchy** panel, right-click one of the feet bones and select **New IK Goal**.

![create new ik goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2981976e-3522-468b-ad69-e9b129d0657e/embellish1.png)

In the following prompts, ensure **Limb IK** is set as the solver and click **Add Solver**, then click **Assign Goal**.

![add solver and assign goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/127f89f8-8654-4879-8400-3b201fe6d795/embellish2.png)

Next, ensure that the newly created Limb IK solver is selected in the **Solver Stack** panel, then right-click the thigh bone and select **Set Root Bone on Selected Solver**.

![set root bone on selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f47d5159-f929-44c1-b02c-93100f21d1ad/embellish3.png)

Perform the same steps above for the other leg until you have two IK Goals and Limb IK solvers.

![limb ik set up](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2eaf346-dd7b-4051-997b-44c2cb328312/embellish4.png)

### IK Retargeter Root Settings

Next, return to the IK Retargeter Asset and open the root settings by either selecting the root debug visualizer in the viewport or clicking **Root Settings** in the **Chain Mapping** panel.

![root settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fabe7d0-9a5e-4abe-9eed-23ff89fddd89/embellish5.png)

The two properties you need to edit are **Scale Horizontal** and **Translate Offset Z**.

-   **Scale Horizontal** increases the overall scale of the animation curve on the retarget root, which in most cases is the pelvis or hip bone. This increases the overall vertical motion of the character, but also causes the character to rise higher away from the floor.
    
-   **Translation Offset Z** compensates for this. When decreasing it, it lowers the retarget root, but does not affect its overall scale.
    

Using both these properties together makes it so that you can increase the up and down bounce of a retargeted character. The amount to increase or decrease the properties depends on your character and the animation.

![adjust vertical scale and offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19a441bf-6edd-4437-8898-7c0df746c825/embellish6.gif)

In this example, to achieve a desirable bounce, **Translation Offset Z** is set to **\-173**, and **Scale Vertical** is set to **6**.

![embellishment results](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1423d9db-4f74-4034-aa9d-57b0956fbc97/embellish7.gif)