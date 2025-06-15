# Pose Blender

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pose-blender-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pose-blender-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:56

---

After creating an [Animation Pose Asset](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine), you can use the [Pose Blender](/documentation/en-us/unreal-engine/pose-blender-in-unreal-engine#poseblender) and [Pose by Name](/documentation/en-us/unreal-engine/pose-blender-in-unreal-engine#posebyname) [animation blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) nodes to animate characters with pose assets.

## Pose Blender

**Pose Blender** nodes are [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) nodes that are automatically created by dragging a **pose asset** into the **AnimGraph**.

![pose blender node animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dec5e365-046c-4756-aaef-3fb1339bd824/posenode.png)

Pose Blender nodes are used to play the associated **pose asset** on the [skeletal mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) at runtime.

Pose Blender nodes will not display an **output pose** without any method of driving the contained **animation curves**. You will need to use an Animation Blueprint node to drive the curve data of the pose node to generate an output pose.

![source pose was visible but ignored no pose output without animation curve driving method](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b4eafcd-b5bc-4cd3-9c18-62c53391585d/error.png)

Here is an example of an [animation sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine), that contains authored animation curves, driving the pose assets curves, to animate the face.

|   |   |
| --- | --- |
| ![animation curves in animation sequence asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecafc138-31a8-4a23-b424-5547477e12a1/animcurve.png) | ![pose blender demo using animation sequence curves to drive anim curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75b0a1df-355b-4cd1-9fe5-0f7b35cdf4ff/poseassetdemo.gif) |
| Animation Sequence Curves | Pose Asset playback using animation sequence curves and Pose Blender node |

While nodes like the animation sequence players, can be used to drive animation curves found within the pose asset, you can also drive these curves with an [curve asset](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine). You can set a custom curve, to drive the pose asset, in the **Custom Curve** property, in the **Pose Blender** node's **Details** panel.

![custom curve property in the pose blender nodes detail panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acdaa1d1-c30e-4ea1-9a21-f3139e4656f5/customcurve.png)

## Pose by Name

When working with a pose asset that contains multiple [skeletal mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) poses, stored as unique animation curves, you can use the Pose by Name [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node to selectively playback poses by using their name.

![pose by name animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a124c275-01c2-4fdf-880e-842abc290f57/posebynamenode.png)

To create a Pose by Name node, you must right click a Pose Blender node in the AnimGraph and select, **Create Pose by Name Node** from the context menu.

![convert a pose blender node to a pose by name animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a262276d-22c7-436c-b8f2-224936420d0f/convert.png)

Here a Pose by Name node is outputting a single pose from within a pose asset that was generated using a run animation, with each frame of animation having its own animation curve assigned, `Frame 25` being the desired pose's name.

![pose by name animation blueprint node demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a5fed4d-42d6-46f6-9b31-6f5dbe8f4b30/posebynamedemo.png)

When using the Pose by Name node, you can control the weight of the specified pose using the **Alpha Property**. Here a simple wave value is adjusting the alpha value to drive the weight of the pose.

|   |   |
| --- | --- |
| ![aniamtion blueprint driving pose alpha](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6eb3d2a-a2f1-4e2c-bb77-0d7e5862909a/poseweight.png) | ![alpha value demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90fa1670-7107-4cd9-a4c7-73059fd1c910/alphademo.gif) |
| Animation Blueprint | Result |

If you are using a Pose Asset that has been enabled as **Additive**, you will need to use the **Apply Additive** node to correctly display your desired pose.

![apply additive node when pose asset is additive](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05362e45-eb63-4b29-9a3e-fcc22dcea4b3/additive.png)