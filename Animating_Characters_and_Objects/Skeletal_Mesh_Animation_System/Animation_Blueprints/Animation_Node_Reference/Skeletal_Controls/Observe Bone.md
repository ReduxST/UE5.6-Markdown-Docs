# Observe Bone

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-observe-bone-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-observe-bone-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:36

---

With the **Observe Bone** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can watch a selected bone's translation rotation and scale motion for debug purposes.

![observe bone animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b78ea88-cefb-402e-93de-12192a286b12/observebone.png)

Here a character's `upperarm_l` is being observed during an animation.

![observe bone animation blueprint node demonstration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fdbd804-ad0a-4dcf-837e-11099282ac27/demo.gif)

The node will display debug data in the **AnimGraph** with the coordinates of the **Bone to Observe**'s motion. Each line of the debug data displays an element of motion data on each axis.

For example:

-   **TX** represents Translation on the X axis.
-   **RY** represents Rotation on the Y axis.
-   **SZ** represents Scale on the Z axis.

## Property Reference

Here you can reference the Observe Bone properties accessible in the node's **Details** panel.

| Property | Description |
| --- | --- |
| **Bone to Observe** | Here you can define a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to track position and motion data. |
| **Display Space** | 
Here you can select what space the **Bone to Observe** motion is calculated.

-   **World Space**: observes the absolute position of the **Bone to Observe**\* in world space.
-   **Component Space**: observes the position of the **Bone to Observe** within the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)'s reference frame.
-   **Parent Bone Space**: observes the position of the **Bone to Observe** relative to the parent bone.
-   **Bone Space**: observes the position of the **Bone to Observe** within its own reference frame.



 |
| **Relative to Ref Pose** | When enabled this property will track the position and motion data of the **Bone to Observe** relevant to the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)'s reference pose, based on the space defined in the **Display Space** property. |