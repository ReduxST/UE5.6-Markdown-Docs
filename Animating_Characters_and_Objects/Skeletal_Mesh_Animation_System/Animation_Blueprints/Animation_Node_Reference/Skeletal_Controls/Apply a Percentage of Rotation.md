# Apply a Percentage of Rotation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-apply-percent-of-rotation-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-apply-percent-of-rotation-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:14

---

With the **Apply a Percentage of Rotation** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can apply a **Source Bone**'s rotation motion to a **Target Bone**.

Here, the robot's antena are matching the X-axis rotation its head.

|   |   |
| --- | --- |
| ![apply a percentage of rotation disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7ec11d0-8ada-40c1-9577-555e2048af02/botdemooff.gif) | ![apply a percentage of rotation enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/841db8d4-7f94-4804-9968-ad5e6ab9df22/botdemoon.gif) |
| Disabled Apply a Percentage of Rotation | Enabled Apply a Percentage of Rotation |

## Overview

The Apply a Percentage of Rotation node operates within **Component Space**, so a [space conversion](/documentation/en-us/unreal-engine/animation-blueprint-component-space-conversion-in-unreal-engine) will need to occur to implement the node within your character's Animation Blueprint.

![Apply a Percentage of Rotation animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a59b7b5-6e70-4205-9ff6-49a9f4ef5ca1/applypercentage.png)

With the **Alpha** property or pin, you can control the degree of the applied rotation on the generated output pose. A value of **1** will fully use the generated output pose, while a value of **0** will output the source pose.

The **Multiplier** property or pin allows you to multiply the degree of the rotation beyond the **Source Bones** rotation.

A **Multiplyer** value of 0 will not apply any rotation to the Target Bone.

In the Apply a Percentage of Rotation node's **Details** panel you can select a **Source Bone**, to copy the rotational movement from, as well as a **Target Bone** in which to apply the copied rotation motion.

![apply a percentage of rotation animation blueprint node with target bone and soruce bone properties highlighted in details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f957c00-ffc5-4ac4-a90d-4cd1a3c5f2b7/detailspanelhighlight.png)

See the [Property Reference](/documentation/en-us/unreal-engine/animation-blueprint-apply-percent-of-rotation-in-unreal-engine#propertyreference) table for more information about the Apply a Percentage of Rotation node's properties.

### Stacking Nodes

Multiple Axis rotation can be used by stacking addition Apply a Percentage of Rotation nodes together, and assigning unique axis of rotation to each.

![combined apply a percentage of rotation animation blueprint nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1cdd2d1-ddb9-42f8-8fce-eb7528fefa11/stack.png)

When stacking Apply a Percentage of Rotation nodes, ensure the **Is Additive** property is enabled in the **Details** panel for any additive or stacked nodes applying rotation to the same bone. This property is also important to enable when using the Apply a Percentage of Rotation node in conjunction with any other animation or node making adjustments to the same bone.

## Property Reference

![apply a percentage of rotation animation blueprint node with details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cef077a2-763b-47b5-a71f-e97edc54cd8b/detailspanel.png)

Here you can reference a list of the Apply a Percentage of Rotation node's properties.

| Property | Description |
| --- | --- |
| **Target Bone** | Select a bone from the character's [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) in which to apply the rotation from the **Source Bone**. Any child bones of the Target Bone will also be moved relevant to the parent bone motion. |
| **Source Bone** | Select a bone in which to copy the rotational motion from, on the axis defined in the **Rotation Axis to Refer** property. This rotation motion will then be applied to the **Target Bone**. |
| **Multiplyer** | 
Set a multiplier to apply to the rotation motion from the **Source Bone** as it is applied to the **Target Bone**. A value of 1 will copy the rotation motion exactly.

By default this property is accessible in the **AnimGraph** on the selected node.



 |
| **Rotation Axis To Refer** | Here you can select which axis of rotation motion will be copied from the **Source Bone**, and applied to the **Target Bone**. |
| **Is Additive** | Enable this property to enable the rotation motion to be applied to the bone as additive. Disabling this property will overwrite any previous motion on the **Target Bone**. |