# Root Motion

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/root-motion-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/root-motion-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:27

---

With Root Motion animations, you can drive character movement with animation data to create more grounded movement within levels.

This document provides an overview of Root Motion, and a quick explanation of how to enable Root Motion in compatible animations.

#### Prerequisites

-   Your project contains a [character](/documentation/en-us/unreal-engine/setting-up-a-character-in-unreal-engine) with a [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) that has a [Root Bone](/documentation/en-us/unreal-engine/root-motion-in-unreal-engine#root%20bone).
    
-   Your project contains an [Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) or a [Montage](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) with motion data assigned to the Skeleton's Root Bone.
    

## Overview

Within a level, a character is composed of many [Components](/documentation/en-us/unreal-engine/basic-components-in-unreal-engine). A character's movement is often driven by the character's [Movement Component](/documentation/en-us/unreal-engine/movement-components-in-unreal-engine), with animation playback layered on top to communicate the visual feedback of motion.

Below is an example of a character rendered with a [Skeletal Mesh Component](/documentation/en-us/unreal-engine/basic-components-in-unreal-engine) and a [Capsule Component](/documentation/en-us/unreal-engine/components-in-unreal-engine#primitivecomponents) in the [Blueprint Viewport Editor](/documentation/en-us/unreal-engine/components-mode-viewport-in-the-blueprints-visual-scripting-editor-for-unreal-engine).

![character mesh and capsule component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2ac6fbe-9c3c-4dbd-ab87-6193694eb9c7/charactercapsule.png)

### Root Bone

Animations are driven by the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine)'s [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), which is composed of bones. The **Root Bone** is the Skeleton's foundational bone; unlike other bones, the Root Bone is not built to represent an element of the Skeletal Mesh, like a leg or arm, but rather, is a reference point for the entire skeletal structure. Some animations do not have any animation data on the Root Bone, it remains stationary and grounds the skeleton and the animation to a single point, while others animate the Root Bone to follow the animation's displacement in 3D space.

Below is an example of a Skeletal Mesh with its Root Bone highlighted.

![skeleton root bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a5e7f89-1581-4584-84ec-8dd34036df33/rootbone.png)

### Root Motion

In the absence of any character movement, animations with a stationary Root Bone will play in place with no actual movement or displacement.

![no root motion enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e78f801-cd2e-437d-b979-408400c3bf8b/rootmotionlock.gif)

While some animations, like the animation above, have a stationary Root Bone, others have movement assigned to the Root Bone.

Below is a demonstration of an animation with movement data on the Root Bone. The **red line** represents the tracked displacement of the Root Bone, from its starting position to its current location.

![root bone displacement](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16fc89a2-6e92-4968-9b2a-c4ec3e32a673/rootbonedisplacement.gif)

However, an animation containing animation data on the Root Bone does not affect the character movement by default, it must first be enabled with the **Root Motion** property.

|   |   |
| --- | --- |
| ![no root motion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1e8e4e5-76fc-4c34-962e-5e21b43d9fb1/norootmotion.gif) | ![root motion enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ffc0e39-80ee-4b54-a44c-dc4fb5a217b1/hasrootmotion.gif) |
| No Root Motion | Using Root Motion |

Without Root Motion enabled, the animation is animating the Skeletal Mesh off the Root Bone and away from the character (represented with the wireframe capsule). The Skeletal Mesh disconnects from the character, before snapping back to the starting position at the end of the animation cycle. By enabling an animation's Root Motion, the Root Bone motion data can drive the character's movement, which drags the character along with the Root Bone's movement.

By driving character movement with Root Motion, animations are able to recursively loop, beginning from the character's last position from the previous animation loop. Below is an example of recursive animation cycles.

![recursive root motion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bbfc13e-fd39-44ed-bb6c-0766edee3fcd/recursiverootmotion.gif)

## Enabling Root Motion

In order to enable and use Root Motion features, you must first have a Skeleton that has a root bone, and an animation with an animated root bone.

### Animation Sequence

Each individual Animation Sequence or Montage must be toggled to **Enable** Root Motion. This property is found and modified within the **Asset Details** panel in the [Animation Sequence Editor](/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine).

![root motion properties asset details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/635fdd94-c256-4460-b471-2c60101a36f8/rootmotiondetails.png)

Below is a listing and explanation of the properties relating to Root Motion found when editing an Animation Sequence Asset.

| Property | Description |
| --- | --- |
| **Enable Root Motion** | When enabled, Root Motion data is extracted. Uses the Animation Blueprint's Class Defaults property **Root Motion Mode** to define how Root Motion is extracted. |
| **Root Motion Root Lock** | 
Locks the Root Bone to the defined position when extracting the Root Motion.

The options for the position with which to lock the Root Bone are as follows: **Ref Pose**: Locks the Root Bone to the location it presides in the **Reference Pose** for the Skeletal Mesh. **Anim First Frame**: Locks the Root Bone to its location in the **first frame** of the selected animation. **Zero**: Locks the Root Bone position to a 0,0,0 coordinate point, relative to the mesh.



 |
| **Force Root Lock** | When enabled, forces the Root Bone to Lock, even if **Root Motion** is not enabled. |
| **Use Normalized Root motion Scale** | When enabled, applies a normalized scale to the extracted Root Motion. FVector(1.0, 1.0, 1.0). |

### Animation Blueprint

After enabling Root Motion within an individual Animation Sequence's parameters, you need to determine how that sequence is handled inside of the [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) driving your object's animations. There are several different ways you can handle Root Motion within Animation Blueprints. To access these options, click **Class Defaults** in the [Animation Blueprint Editor](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine)'s **Toolbar**. This opens a **Details** panel that contains a **Root Motion Mode** property with a drop down menu.

![open class defults](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c70dcbc-b404-4eaf-afad-cd4d2c3675d5/classdefaults.png)

The options are as follows:

| Name | Description |
| --- | --- |
| **No Root Motion Extraction** | Root Motion remains unchanged (applied to the root bone). |
| **Ignore Root Motion** | Root Motion is extracted (and removed from the root bone), but not applied to the character. |
| **Root Motion from everything** | Each Root Motion enabled animation asset that contributes to the final character pose has its Root Motion extracted. The extracted Root Motion is blended based on the weight of the source assets contributing to the pose. |
| **Root Motion from Montages Only** | Root Motion is only extracted from Root Motion enabled [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine). |

There is a performance cost to enabling Root Motion.

When either **Root Motion from everything** or **Root Motion from Montages** is enabled, the Animation Graph is updated on the Game Thread instead of a Worker Thread. More work on the Game [Thread](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#cputhreadusageandperformance) can cause performance issues.

### Results

Once Root Motion is enabled in your animation and the application method of Root Motion extraction is defined in the Animation Blueprint, the animation drives the Movement Component during playback.

The physics state of the character is taken into account during Root Motion. For example, if a character is **Walking** or **Falling,** along an X and Y axis, then the Z-axis of Root Motion is ignored, and gravity is applied. This character will fall, go down slopes, or up stairs. If the character is **Flying,** in an unbound state, then the full Root Motion is applied and gravity is ignored.

This is defined and adjusted within the character Blueprint with a **Movement Mode Node**.

## Debugging Root Motion

Below are relevant debugging properties for working with Root Motion animations.

### Animation Sequence Editor

While working with animation sequences in the editor's Viewport, there are many helpful features at your disposal for debugging purposes.

To render the character's Skeleton as an overlay over the Skeletal Mesh, navigate to the **Character** tab and open the **Bones** breakout menu. Within the **Bone Drawing** header, select **All Hierarchy**. This option renders the entire Skeleton, including the Root Bone rendered in red. Since the Root Bone is undergoing a transform, a red line is rendered between the Root Bone origin point and the current location.

Below is a demonstration of enabling the **All Hierarchy** Bone Drawing Mode.

![show bones all hierarchy bone drawing mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91dc4854-f152-4c70-acba-83f250b7f5f1/showbones.gif)

The **Red Line** represents the Root Bone displacement due to enabling Root Motion. You can see the amount of displacement, and track the movement of the Root Bone during animations with Root Motion enabled.

To alter the playback settings of the Root Motion animation, navigate to the **Character** tab and open the **Animation** breakout menu. Under the **Root Motion** header you can toggle the preview playback options as shown and described below.

| Option | Image | Description |
| --- | --- | --- |
| **Ignore** | ![ignore root motion mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8298b27-f41e-4158-84b2-f5faf3581ce4/ignorerootmotion.gif) | Ignores any present Root Motion and plays back the animation in a static setting. |
| **Loop** | ![loop root motion mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/831f3346-d0c1-40f6-9573-a3b15da50b73/looprootmotion.gif) | Enables the Root Motion playback, and continually loops the animation beginning from the endpoint of the previous loop. |
| **Loop and Reset** | ![loop and repeat root motion mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fde3c413-917e-42c1-bbe9-6488e0627730/looprepeatrootmotion.gif) | Enables the Root Motion playback, and continually loops the animation beginning from the Root Bone origin point for every loop. |

### Console Command

You can enable a character's Capsule Component to display during run time with a **Console Command**.

Although the Collision Component is not the character object, the Collision Component can be a quick and easy way to visualize the character object separately from the Mesh.

While a game is running in the editor, press the **Backtick** (**\`**) key, to enable the console command window.

Enter the console command: `show collision`, and press the **Enter** key.