# Motion Warping

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-warping-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-warping-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:02

---

**Motion Warping** is a feature where you can dynamically adjust a character's root motion to align to targets. This document will show you how to create the Motion Warping logic in your character blueprint, assign Motion Warping windows within animation montages, and link them to named positions.

#### Prerequisites

-   You must enable the **Motion Warping** plugin. For more information regarding Plugins and how to Install them, see: [Working With Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

![motion warping plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39d66fcc-bd88-4fa5-9b22-e4c39c84e28e/plugin.png)

-   Motion Warping utilizes [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) and [Animation Montage](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) workflows. Therefore you should have an understanding of these features.
    
-   You have a [Character Blueprint](/documentation/en-us/unreal-engine/setting-up-a-character-in-unreal-engine), [Input Controls](/documentation/en-us/unreal-engine/input-in-unreal-engine), and [Animations](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) in your project that you can create gameplay examples with.
    

## Motion Warping Overview

The overall feature for Motion Warping can be broken down into two main areas:

1.  **Animation Montage**, where you create motion warping windows with Anim Notify States.

![animation montage overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95b5d27b-4d9c-459d-87e5-8a22e6a9e7d1/motionwarpoverview.png)

1.  **Blueprint Logic**, where you set up the logic to assign the warp target and play the Montage.

![blueprint overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/754971c9-0c77-4638-b309-9713806964f9/blueprintconcept.png)

## Animation Montage

Animation Montages are where you specify the Motion Warping areas, customize their behavior, and name them.

### Creation

To create a new Motion Warping region, right-click on one of the **Notifies** tracks and select **Add Notify State... > Motion Warping**.

![create motion warp notify state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c509651b-5e91-4f23-9c46-5033a5151c92/createwarp.png)

These are customizable areas with start and end times that you can align to areas of the animation where warping is best applied.

For example, in this mantling montage, you likely need to ensure your starting warp region covers the area when the character places their hand on the obstacle.

![motion warp sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d11ecdd-4279-4bf3-86d0-f0afa5080a75/motionwarpingsequence.gif)

### Details

The **Anim Notify**'s **Details** panel contains properties and settings necessary for your Motion Warping to function. Select your motion warping section to reveal these details.

![motion warp details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/504d1601-f74e-4561-b0d7-b218ac3ce937/motionwarpdetails.png)

| Detail Name | Description |
| --- | --- |
| **Root Motion Modifier** | 
The Motion Warping type to specify.

**Scale**: A Motion Warp that alters an animation's scale in a uniform manner. **Skew Warp**: Warps the game object's root motion so that it matches the animation's location and rotation in the level at the end of the warping window.



 |
| **Warp Target Name** | The name used to find this warp target. Correlates to the **Add or Update Warp Target** Blueprint node. |
| **Warp Point Anim Provider** | 

Select which provider is desired for the **Warp Point**.

**None**: No Warp Point Provider is declared here. **Static**: Warp Point defined by a user-defined parameter transform, which can be declared through the warping notify itself. **Bone**: Warp Point is defined by a Bone.



 |
| **Warp Point Anim Transform** | Transform the Animation Warp Point. Only relevant when the **Warp Point Anim Provider** is set to **Static**. |
| **Warp Point Anim Bone Name** | Declare the Bone Name with which to target as a Warp Point. Only relevant when the **Warp Point Anim Provider** is set to **Bone**. |
| **Warp Translation** | Whether to warp the translation component of the root motion. |
| **Ignore ZAxis** | Whether to warp the Z component of the translation. |
| **Warp Rotation** | Whether to warp the rotation component of the root motion. |
| **Rotation Type** | 

Whether the rotation should warp to match the warp target's rotation or face the warp target.

**Default**: Character rotates to match the rotation of the warp target. **Facing**: Character rotates to face the warp target.



 |
| **Warp Rotation Time Multiplier** | Modifies how fast the rotation is warped. For example, if the Motion Warping window lasts for two seconds, and this property is 0.5, then the final rotation will be reached in one second. |
| **Notify Color** | Sets the color of the Motion Warping Notify keyframe. |

## Blueprint

Blueprints are used to add your Motion Warping component, trigger the warp to occur, and specify warp targets.

### Motion Warping Component

You must add a Motion Warping Component to your blueprint to enable Motion Warping behavior. To do this, click **(+) Add** in the **Components** panel and locate **Motion Warping** under the **Movement** category. Click it to add.

![motion warping component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83744050-ccd6-4231-bce9-065856581b8a/motionwarpingcomponent.png)

The Component can now be referenced in your blueprint graph by dragging and dropping it from the Components panel to the **Event Graph**.

![motion warping blueprint instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69119211-462a-47f2-b003-6f37a698c142/motionwarpinstance.png)

### Nodes

Dragging a link from the Motion Warping reference allows you to browse for functions and events related to it. These are located within the Motion Warping category.

![new node from motion warp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5395757d-05e2-46e8-a1ea-b4af95a0d6cd/newnode.png)

You can use the following Motion Warping nodes in your Blueprint:

| Node Name | Node Image | Description |
| --- | --- | --- |
| **Add or Update WarpTarget** | ![add or update warp target node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4370176-17ba-4d80-a304-38db0caff318/addorupdatewarptargetnode.png) | 
This node is used to link the Warp Target Name, which was defined in the Montage Asset, to a location. The **Warp Target** pin can be split into separate **Translation** and **Rotation** pins by right-clicking it and selecting **Split Struct Pin**.

Conversely, you can use the **Remove Warp Target** node to unlink the **Warp Target Name**.



 |
| **Add Root Motion Modifier Skew Warp** | ![add root motion modifier skep warp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd682490-042a-49f4-bbd3-180a5c22f8c8/addrootmotionmodifierskewwarp.png) | 

You can use this node to generate new Motion Warping Windows with Blueprints instead of adding **Skew Warp Anim Notifies** in the Montage Asset.

Settings for this Motion Warping Window can also be assigned here, such as **Start Time** and **End Time** and **Warp Target Name**.

Also available is an **Add Root Motion Modifier for Scale** node, as well as a node for disabling all Root Motion Modifiers.



 |

## Motion Warping Example

This section describes how you can set up a simple Motion Warping example of a character warping to a target to punch.

#### Warping Disabled

![warp disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2d20ece-1267-45f6-9eee-d4e1e018544c/motionwarpingdisabled.gif)

Before starting, ensure the animation you intend to use has Root Motion enabled. Do this by opening the Animation Asset and enabling **EnableRootMotion**.

![enable root motion window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73f08f47-05af-4a42-a2fb-77e547ae39a4/rootmotion.png)

### Set up Target Location

The first step is to create and position a target for you to warp to. In this example, a Cylinder is used.

In the **Place Actors** panel, click **All Classes** and locate **Target Point**. Drag and drop it into your level to add a Target Point. Ensure it is aligned and rotated to your desired warp point.

![add motion warp target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/592e52c0-3067-4130-8c14-d44ec791fc60/addtarget.png)

### Set up the Animation Montage

Next, create an Animation Montage Asset. An easy way to create one that derives from an existing animation is to right-click on your Animation Asset and select **Create** > **Create AnimMontage**. After you have created the montage, open the asset.

![create animation montage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5f80173-08d4-4fa2-a5b2-6b10542913f0/createmontage.png)

With your Montage now open, you can scrub through the sequence to preview your animation. The next step is to add a Motion Warping window under the Notifies track. Do this by right-clicking in the track area and selecting **Add Notify State…** > **Motion Warping**.

![motion warp notify state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ca17d63-371d-4b22-919b-651255835fdc/createwarp.png)

A Motion Warping window is now created, with handles where you can set the start and end ranges.

Set the range of this Motion Warping Window so that it begins near the start of the animation, and ends at the moment the character strikes. You can also hold down the **Shift** key as you move your **Notify** keyframes to preview the current animation at that time.

![motion warp notify](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ed93380-5949-4f9d-b67a-ac3151136797/motionwarpnotify.gif)

Next, select the Motion Warping keyframe and navigate to the **Details** panel. Here you will set some properties for this keyframe.

-   Set **Root Motion Modifier Config** to **Skew** **Warp**. This is done to specify the type of warp.
    
-   Set a name for **Warp Target Name**. This is done to identify this warp with a name.
    

![set details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80c384ee-a772-4809-914e-3fd3814f586d/setdetails.png)

### Get Target Location

Now open your Character Blueprint Asset. In the Event Graph, create an **Input Action** node mapped to your desired input action. Do this by right-clicking in the graph and select your input event from **Input > Action Events**.

In this example there is an Input Action Event for Punch.

![get input](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5dfcbd5-0344-40da-9ba8-787a6aa720af/input.png)

Next you will want to get the location of the Target Point you placed earlier in this example. There are a few ways you could choose to do this, but for this example create a **Get All Actors Of Class** node. Set the **Actor Class** to **Target Point**. Finally, hook the **Pressed** output pin from the Input Action node into the input execution pin for the Get All Actors of Class function.

![get actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8843f2ba-a1a2-40a6-b0c8-fb6ec7b2eb25/getactors.png)

Finally, add a **Get** (a copy) node to connect to the Out Actors array data pin. Also add a **Get Actor Location** function and connect its input **Target data** pin to the **Get** node's output data pin.

![get location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c32ec7b4-6e27-4b72-b2af-30e3715ac2d6/getlocation.png)

### Warp Target

Now you create logic for getting your Target Point's location.

To start, add a Motion Warping Component to your Character Blueprint. Do this by clicking **(+) Add** in the Components panel and locate Motion Warping under the Movement category. Click it to add the component.

![add motion warping component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddee3aaa-5d87-42d4-9f93-0489b2781cb1/motionwarpingcomponent.png)

Next, drag and drop the Motion Warping component from the Components panel to the Event Graph.

![motion warping instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/383acfe9-5346-4c22-a065-ce3807b10bca/motionwarpinstance.png)

Drag off from the Motion Warping reference pin to add an **Add or Update Warp Target from Transform** node. Once created, connect its input event pin with the **Get All Actors Of Class** node. Also, ensure you assign a Warp Target Name to the **Name** pin. This name must match the Warp Target Name you defined earlier in the Montage.

![sync point logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f8a7193-c4aa-4332-8f84-923ceddcb971/syncpointlogic.png)

You also need to link the **Add or Update Warp Target from Transform** node to the Target location. Right-click on the Warp Target pin and select **Split Struct Pin** to convert this into a dual Location/Rotation pin structure. Then connect the **Get Actor Location**'s **Return Value** pin to the **Get Actor Location**'s Return Value pin.

When connecting the **Return Value** of the Get Actor Location node, (a vector value, indicated by a yellow pin) and the Add or Update Warp Target from Transform node's Target Transform pin, (a transform value, indicated by an orange pin) a conversion node is created. In instances where different value types are present, but are compatible through a conversion, Unreal Engine automatically creates a conversion node when connecting the pins.

![sync point location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e759761-226c-407c-9090-324581adea06/synclocation.png)

### Play Montage

Now you can reference your **Skeletal Mesh** Component in the Event Graph, and play the Montage on it. Drag and drop the **Skeletal Mesh** Component into your event graph.

Right-click in the graph and select **Animation > Montage > Play Montage** to add a **Play Montage** node. Then assign your Montage Asset to the **Montage to Play** pin.

![play montage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e199ea9-1ad2-453c-9895-2fa7840ab0b6/playmontage.png)

### Results

When you play your level now, you should be able to see your character warp to the appropriate point as they play their punch animation.

![motion warping enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13369544-0d2d-4ac8-832d-f52ad4483d89/motionwarpingresult.gif)

Below you can see a full image of the Character Blueprint logic used for this page's implementation of Motion Warping to a simple warp target location.

![blueprint overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0d92808-614a-406d-a2fe-fe34f710c94d/fullblueprint.png)