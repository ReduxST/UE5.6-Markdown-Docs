# Blend Masks and Blend Profiles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:08

---

As you create complex animation logic, it may be necessary to have more refined control over the way your animation blends, instead of just blending all bones at once. **Blend Masks** can be used to exclude bones from a blend, and **Blend Profiles** provide control over the rate at which different bones blend. These additional blending controls can improve the fidelity and compatibility of your gameplay animation.

This page provides an overview of how to create and use Blend Masks and Blend Profiles.

#### Prerequisites

-   Your project contains a [Skeletal Mesh Actor](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine), along with [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine).
    
-   You have a basic knowledge of how to create and use [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).
    

## Blend Masks

**Blend Masks** are definitions you can add to your skeleton where you can define weight influences, disabling animation from playing partially or fully on specific bones. You can then use this pre-set definition on the [Layered Blend Per Bone](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#layeredblendperbone) to play animation on certain bones.

A common use-case for using Blend Masks is to exclude lower-body bones so that animation plays only on the upper-body, regardless of the full-body state. This is useful for weapon-based animations that require the upper-body bones to ignore the rest of the body, such as reloading, equipping, or shooting.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb1eb13d-c485-4ed0-b322-3b0f9fcb906e/blendmaskon.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd05128e-b1f5-4c8a-9c3d-33e015149df9/blendmaskoff.gif) |
| Using Blend Masks | No Blend Masks |

### Creating Blend Masks

You create Blend Masks within the [Skeleton Tree](/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine#headername) of your Skeletal Mesh. Click the **Options** dropdown menu in the Skeleton Tree and select **Add Blend Mask**. Give it a name and press **Enter**.

![add blend mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4ae61b2-7abb-4c79-985f-8d9dadc243d2/blendmask1.png)

Once created, a **Blend column** appears within the Skeleton Tree listing your Blend Mask. If you have multiple Blend Masks, you can switch between them by clicking them in the **Options** menu.

![blend mask view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a93aa4fc-2e39-4ee8-9a49-a05d70f58f6e/blendmask2.png)

To delete the currently-viewed Blend Mask, click the **Options** dropdown menu in the Skeleton Tree and select **Remove**.

![delete blend mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5dc51d9-7dfe-4a78-936f-6a3cdf9a77a7/blendmask3.png)

Both Blend Masks and Blend Profiles are stored in the [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) asset. Therefore, when creating or editing Blend Masks, you are editing the Skeleton asset.

### Editing Blend Mask Values

The Blend column shows the current values of each bone within your Blend Mask. Each bone can have an assigned value between **0 - 1**. A value of **0** will cause no animation to play on that bone, and a value of **1** will cause animation to play at 100% value.

You can edit these values by either dragging on the value to enable the slider control, or by selecting and typing in a value directly.

![edit blend mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e471a2f5-8efd-492f-90dd-ff94531ac3e1/blendmask4.gif)

You can also set the same value to all children by right-clicking on a bone and selecting **Recursively Set Blend Scales**, which applies this blend value across several bones at once.

![Recursively Set Blend Scales](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92b36ecb-69a3-49e7-9ca8-815e5865c15c/blendmask5.gif)

If you do not see the column for editing Blend Mask values, you may need to right-click on the property header and enable **Blend Profile**.

![blend profile column](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1afa5834-7e7f-4f04-81fe-3c9f3be0e34c/blendmask8.png)

### Using Blend Masks

Once you have created and set appropriate values for your Blend Mask, you can use it in your [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine). This is done by setting your Blend Mask on the [Layered Blend Per Bone](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#layeredblendperbone) node within the Anim Graph.

In your Animation Blueprint Anim Graph, right click and create a **Layered blend per bone** node, then set the following properties in the **Details** panel:

-   Set **Blend Mode** to **Blend Mask**.
-   Set **Blend Masks** to your Blend Mask.

![layered blend per bone node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8d8999e-a34e-4dbf-bd5e-5afab8d9876c/blendmask6.png)

Connect your incoming source base and blend poses and you can now observe that the Blend Mask is working. In this example, we used an upper-body Blend Mask.

![blend mask final](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/976310cc-1fec-4fff-a339-e16219ff44c4/blendmask7.gif)

Although this behavior is possible by using the default **Branch Filter** Blend Mode on the Layered Blend per bone node, Blend Masks let you reuse these blend amounts on your bones more easily.

## Blend Profiles

**Blend Profiles** are definitions you can add to your skeleton where you can define per-bone blend speeds, causing some bones to blend faster than others. Blend Profiles can be used when blending using the following methods:

-   [Blend Poses by bool](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#blendposesbybool).
-   [Blend Poses by int](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#blendposesbyint).
-   [Blend Poses by enum](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#blendposesbyenum).
-   [State Machine Transitions](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine).
-   [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine).

A use case for using Blend Profiles might be to blend the lower-body faster than the upper-body, which can be useful when transitioning between idle and locomotion states. This can make the feet appear to plant firmly on the ground when stopping, and start more naturally before the upper body when starting to move.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bd7e0da-d2ac-4fff-9a01-b57676cd29a4/blendprofileon.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5de53942-ab9a-467c-a359-2a3a47a86ffc/blendprofileoff.gif) |
| Using Blend Profile (Legs are blending faster) | No Blend Profile |

Similar to Blend Masks, Blend Profiles are [created](/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine#creatingblendmasks), managed, and [edited](/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine#editingblendmaskvalues) in the Skeleton Tree. Click the **Options** dropdown menu in the Skeleton Tree and select either **Add Time Blend Profile** or **Add Weight Blend Profile**.

![create blend profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a56c8fb-0ad7-4688-bc3d-f3a248d28f00/blendprofile1.png)

Because the list of Blend Masks and Blend Profiles occupy the same column and option menu region, you should ensure that they are clearly named to avoid confusion.

![blend names](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1316eeac-f780-46b0-b610-82129ed93204/blendnames.png)

### Time Blend Profile

**Time Blend Profiles** are Blend Profiles that blend using a normalized (0 - 1) multiplier against the base blend value. A value of **1.0** blends at normal speed, and lower numbers blend faster. A value of **0.0** causes the blend to be instantaneous.

For example, if you set the following:

-   Pelvis and all upper-body bones set to **1.0**.
-   Legs and all lower-body bones set to **0.5**.

This causes the legs to blend twice as fast, according to the base blend time wherever you use this Blend Profile. If it is used on a **Blend** **Poses** **by bool** node, with the base blend time set to **2.0** seconds, then the legs blend over only **1.0** seconds. All other bones set to **1.0** still blend over the base **2.0** seconds.

![time blend profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc509d91-0390-4e7b-b57c-a096092dbb45/timeblend1.png)

### Weight Blend Profile

**Weight Blend Profiles** are Blend Profiles that blend using a weight factor against the base blend value. A value of **1.0** will blend at normal speed, and higher numbers will blend faster.

For example, if you set the following:

-   Pelvis and all upper-body bones set to **1.0**.
-   Legs and all lower-body bones set to **2.0**.

This causes the legs to blend twice as fast, according to the base blend time wherever you use this Blend Profile. A value of **2.0** means the blend will be **2x** faster, **3.0** will mean **3x** faster, and so on.

![weight blend profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b8da87e-b01c-4e16-aad8-227fa23d1554/weightblendprofile1.png)

### Using Blend Profiles

Once you have created and set appropriate values for your Blend Profile, you can apply it in the following ways:

1.  On [Blend Pose](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#blendposesbyint) nodes in the **Animation Blueprint Anim Graph**, select the node and locate the **Blend Profile** property in the **Details** panel.
    
    ![blend profile blend pose nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5378d70-f4ef-4736-94ff-4d5dbd55dff3/usingblendprofile1.png)
    
2.  On [State Machine transition rules](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine), select the **transition rule** and locate the **Blend Profile** property in the **Details** panel.
    
    ![blend profile state machine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb4b5f2d-0282-4b7c-a3c8-7ffa3c0256c4/usingblendprofile2.png)
    
3.  In the [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) editor, you can set a different Blend Profile for blending in and out of the Montage using the **Blend Profile In** and **Blend Profile Out** properties in the **Asset Details** panel.
    
    ![blend profile montage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e56aa5a-b07d-464c-816d-cd868fab85d9/usingblendprofile3.png)