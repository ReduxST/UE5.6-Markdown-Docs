# Blending Gameplay and Sequencer Animation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-gameplay-animation-to-cinematic-animation-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-gameplay-animation-to-cinematic-animation-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:06

---

When creating your cinematic sequences, you may want to blend gameplay animation to or from animation inside your Level Sequence. Typically this is done to create seamless transitions into and out of a cinematic, which includes blending both the player animation and the player camera.

This document provides instructions on workflows and considerations you can use to blend player and camera animations between Sequencer and gameplay.

#### Prerequisites

-   You have a controllable player character in your project. For this document, the [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) is used as an example.
-   You have created your cinematic sequence and you are ready to blend it to gameplay.
-   You are familiar with [how to reference the player](/documentation/en-us/unreal-engine/how-to-reference-the-player-in-unreal-engine-cinematics) in Sequencer.

## Animation Blueprint Setup

Normally when animating characters in Sequencer, the Animation Mode property automatically changes to **Use Custom Mode**. Custom Mode is a special Sequencer-specific [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), different from the one used to animate the player in gameplay. In order to blend characters between Sequencer to Gameplay, you *cannot* use **Custom Mode**, and must instead use the same Animation Blueprint the character uses in gameplay.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d11ab6b-274f-4021-b940-18e81391240b/animbp1.png)

You can ensure this by [referencing the player Character Blueprint in your Sequence](/documentation/en-us/unreal-engine/how-to-reference-the-player-in-unreal-engine-cinematics), which should have Animation Mode set to the gameplay Animation Blueprint. If not, then you can manually set this property by selecting the character, navigating to the **Details** panel, and doing the following:

-   Set **Animation Mode** to **Use Animation Blueprint**.
-   Set **Anim Class** to the **Animation Blueprint** used in gameplay. In the case of the Third Person Template, it is **ABP\_Manny\_C**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a21a277-7b79-4703-bb5a-96eb6ed5875a/animbp2.png)

When an Animation Blueprint is explicitly set, Sequencer will not override this property to Use Custom Mode.

### Slot Setup

When animating characters in Sequencer using their Animation Blueprint, you must ensure that Animation Blueprint contains [Slots](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine), which provide a way to inject animation into the [Anim Graph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine). Although mainly used to play animations from [Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine), you can also use Slots to play animation from Sequencer.

To create a new Slot, open the Animation Blueprint for the character you want to blend, and do the following:

1.  Click **Window** and enable **Anim Slot Manager**, if it is not already enabled.
2.  In the Anim Slot Manager, click **Add Slot**.
3.  Type the name of your new Slot and press **Enter**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e2a94e7-f73e-470d-ae34-8c20d9e69263/animbp3.png)

Slots are stored on the [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), therefore, when you are creating or changing Slots, you are also editing the Skeleton. Clicking **Save** in the Anim Slot Manager will save the Skeleton when you make any Slot changes.

Next, reference the Slot in your Anim Graph.

1.  Right-click in the graph and add a **Slot 'DefaultSlot'** node.
2.  Select the node and in the **Details** panel, set **Slot Name** to the name of the Slot you created earlier.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e372b68b-896d-49b9-ad36-fb3d6dc8a9c1/animbp4.png)

In addition to making the slot, also consider *where* in the Anim Graph it should be inserted. For most simple blends, it is best to place it as the final node before **Output Pose**, however there may be cases where it would be better to place it earlier in the Anim Graph logic chain to take advantage of procedural effects.

For this example, connect the Slot node between the Animation Blueprint logic and Output Pose.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/860e2756-887d-4489-b20c-6056c2fcc729/animbp5.png)

## Blending to Idle

One of the most common seamless blends to create is blending a cinematic to gameplay with the player character ending in their default idle locomotion pose. As stated in the [prerequisites](/documentation/en-us/unreal-engine/blend-gameplay-animation-to-cinematic-animation-in-unreal-engine#prerequisites), this guide assumes your animation and Sequencer content already exists. This includes:

-   [Character animation](/documentation/en-us/unreal-engine/how-to-add-cinematic-animation-to-a-character-in-unreal-engine) where the character ends at the component root coordinates and matches the gameplay idle pose.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12676f3f-97fe-4a39-8bf1-c0a8e7908b0f/blendidle1.gif)
    
-   [Camera animation](/documentation/en-us/unreal-engine/how-to-animate-cinematic-cameras-in-unreal-engine) which ends in the approximate location of the gameplay camera.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b5b61b3-e5a7-4f59-b7da-93591f62a9c1/blendidle2.gif)
    

### Character Setup in Sequencer

To make the player character blend correctly, do the following operations in Sequencer:

1.  Right click the [animation](/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine) section, navigate to the **Properties** menu, and set **Slot Name** to the name of the Slot you created earlier.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad9ca3f2-c43a-407a-a431-ef7b20a14d29/blendidle3.png)
    
2.  Drag on the upper-right corner of the animation section to create a blend out region at the end of the animation. Although the ending pose of this animation might match the gameplay pose, this can still help to ensure the character does not "pop" when the Sequencer animation finishes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ba32d9d-4f24-4064-b11c-ccbf8422cea2/blendidle4.gif)
    
3.  Right click on the character's transform section, navigate to the **Properties** menu, and set **When Finished** to **Keep State**. This is required to ensure the character remains at the same position when Sequencer finishes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eba0b61b-2464-484d-b81f-68d882bf82f7/blendidle5.png)
    

### Camera Setup in Sequencer

To make the cinematic camera blend correctly to the gameplay camera, do the following operations in Sequencer:

1.  Right-click on the [Camera Cut Track](/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine) and enable **Can Blend**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d5b4b16-d9d7-4c79-ae40-1c59ec958129/blendidle6.png)
    
2.  Similar to blending the animation section, drag on the upper-right corner of the camera cut section to create a blend out region at the end of the camera animation.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c6916a8-aa19-483d-9169-c410ac1cc0e2/blendidle7.gif)
    
3.  Select the **Cine Camera Actor** and disable **Constrain Aspect Ratio** in the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a094357a-862b-4784-892b-e48aea0862ec/blendidle7a.png)
    

You may also need to select the **Level Sequence Actor** and disable **Override Aspect Ratio Axis Constraint** to prevent abrupt field of view changes, if your gameplay camera uses a different axis constraint.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4c9778c-2053-4630-a4d4-e3cdae554f74/blendidle7b.png)

### Blending Idle Results

When playing this sequence at runtime, you should see your character blend from Sequencer to gameplay. Again, this guide assumes you are familiar with [how to reference the player](/documentation/en-us/unreal-engine/how-to-reference-the-player-in-unreal-engine-cinematics) in Sequencer.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b79a297-f46b-453c-aae2-a49dc76aec63/blendidle8.gif)

## Additional Considerations

To improve the quality of your Sequencer blends, consider the following factors in your project:

### Uneven Terrain

Blending character animation on flat surfaces typically requires simple blend logic and Slot placement in your Anim Graph. However, if your gameplay Animation Blueprint contains logic for IK feet placement on uneven surfaces, then you may need to reconsider where the blending Slot is placed in the Anim Graph. Otherwise, your character may exhibit a noticeable adjustment to this terrain as the cinematic animation blends out.

For example, in the Third Person Template, the Mannequin procedurally adjusts to uneven surfaces using IK logic in the Control Rig node.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cce43881-0c4f-43bf-bd2f-5703753e9c19/terrain1.png)

If your blend occurs on an uneven surface, then you may want to move or create a new Slot that executes before the IK adjustment node in the Anim Graph. When the IK adjustment occurs afterward, it will take into account the animation from that Slot.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82103874-75a1-4207-b648-1e01ee07a639/terrain2.png)

When your animation in Sequencer uses that Slot, you should see appropriate procedural adjustments as the animation plays.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a75d18b8-ab93-4263-b82f-6c4732607ffb/terrain3.gif)

### Suppressing and Restoring Input

During most blends, you may want to suppress controller input to prevent conflicts between the controller and Sequencer as the blending sequence plays. The main way you can do this is to select the **Level Sequence Actor,** and in the **Details** panel enable the following:

-   **Disable Movement Input**, which disables gameplay movement on the character.
-   **Disable Look at Input**, which disables gameplay camera control on the character.

This suppresses all input for the duration of the sequence.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18ef7c49-1bf7-4058-b150-ef8d94e41dee/input1.png)

In cases where you want to have precise control over when player input can be restricted and released, you can also use the **Set Cinematic Mode** function to manually control input.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99389584-5daa-46d1-a4a8-fe6dc6bc42d5/input2.png)

As an example of more nuanced input management, you may want to release control of the player before the blend sequence ends. You can do this by doing the following:

1.  Right-click the character's transform [section](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#section), navigate to the **Properties** menu, and unlock **Section Range End**. Then, drag the end time of the transform section to the point where you want control released. This is necessary because the transform section continuously evaluates as the sequence plays, holding the character in place. Ending it early makes it no longer evaluate.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88569fb6-4fa1-466a-bcb0-c7b10a141a92/input3.gif)
    
2.  Create an [Event Track](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine) keyframe at the same time as the end of the transform section with the following logic:
    
    -   The event executes **Set Cinematic Mode**.
    -   **Target** is connected to **Get Player Controller**, which then connects to **Get Player State**.
    -   Disable **In Cinematic Mode**.
    -   Enable both **Affects Movement** and **Affects Turning**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8600247b-e246-4205-a09b-01699720bb4d/input4.png)
    

Now when you play your cinematic, player control should restore before the sequence ends. This can sometimes make for a smoother and more natural gameplay experience for the player.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/922b99a1-cd51-40e1-a42d-556b6fd98e31/input5.gif)

### Gameplay Camera Direction

For games with free-moving camera controls, such as the one used in the Third Person Template, the gameplay camera sometimes might not face in the direction you want when blending out.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/619dbb97-57df-419a-850a-161e1da19d14/cameraface1.gif)

You can manually set the direction of the gameplay camera by using **Get Player Controller** and **Set Control Rotation**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c6000e6-201a-452e-bcc6-0c5d7c1a6a55/cameraface2.png)

Right-click the **New Rotation** pin and select **Split Struct Pin** to view all rotation axes available and set the rotation values on the node. For this example, create the following logic:

-   Execute **Set Control Rotation** after the sequence starts to play.
-   Set **New Rotation Y** to **\-15**, to pitch the camera slightly downward.
-   Set **New Rotation Z** to **\-45**, to laterally rotate the camera and face the intended direction.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30585d3a-5e2d-4039-9200-185641ee5989/cameraface3.png)

Now when you play your cinematic, the camera blends out facing your intended direction.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82cbe772-dd32-4a90-b537-300f79aec8d6/cameraface4.gif)