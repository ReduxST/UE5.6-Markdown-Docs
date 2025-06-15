# CCDIK

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-ccdik-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-ccdik-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:18

---

The CCDIK (Cyclic Coordinate Descent Inverse Kinematics) [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node is a light-weight IK solver, that you can use to drive a chain of bones to an **Effector Location**. The CCDIK node is similar to the [FABRIK](/documentation/en-us/unreal-engine/fabrik-animation-blueprint-in-unreal-engine) node, but the CCDIK provides the ability to define angular constraints which can be useful if you want to limit rotations of any affected bones.

![ccdik animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/317a4ef2-b2e1-4e48-b7b6-5f6c4ea3fdf6/ccdik.png)

Here the CCDIK node is selected in the **AnimGraph** and the **Effector Location** is being manipulated with the debug movement tool in the viewport window.

![ccdik animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64b2646a-46e6-4ef4-8e56-5217571e9591/demo.gif)

As the **Effector Location** is changed the selected bone chain, highlighted with the **red** debug line, moves to match the **Tip Bone** to the **Effector Location**. By using a dynamic vector variable for the **Effector Location**, and applying rotation constraints, this node can be used to make dynamic adjustments to the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) to ground the character's interactions with objects in the game world.

With the **Alpha** value or pin, you can control the degree of the solved motion on the generated output pose. A value of **1** will fully use the generated output pose, while a value of **0** will output the source pose.

## Set up

In this example workflow, the CCDIK node will be used to dynamically adjust the characters finger to press a button in the game world.

The CCDIK node operates within **Component Space**, so a [space conversion](/documentation/en-us/unreal-engine/animation-blueprint-component-space-conversion-in-unreal-engine) will need to occur to implement the node within your character's Animation Blueprint.

After adding the CCDIK node to your [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), select the node in the **AnimGraph** to open the **Details** panel.

In the **Details** panel you can select the **Tip Bone**, which will be the bone at the end of your chain, and the **Root Bone**, which will ground the adjustments to a **local** root bone. In this example, the **Tip Bone** is set to the character's left index finger (`index_03_l`), and the **Root Bone** is set to the character's left clavicle (`clavical_l`).

![ccdik node details pannel select tip and root bone in the solver section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d86f6d5-d92d-492a-b956-1cf46b58ded0/solver.png)

Set the **Effector Location Space** to **World Space**, to calculate the **Effector Location** vector variable in the level.

![ccdik node details pannel effector location space property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dbc8309-3c57-4090-9280-2b8d252bec6d/effectorspace.png)

You can enable rotation limits by toggling the **Enable Rotation Limit** property and make adjustments in the **Rotation Limit Per Joints** property section. An **Index** will populate for each joint present in the [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) between the local **Root Bone** and the **Tip Bone**. You can make adjustments to these rotations to prevent unwanted geometry overlapping and over-extension of your characters joints.

![ccdik node details pannel rotation limit properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77836689-ec0f-4ee6-a64f-86055b470bc3/rotationlimts.png)

The CCDIK node will now adjust the **Tip Bone**, under the constraints of the **Root Bone** and rotation constraints, to match the location of the **Effector Location**, resulting in the character being able to dynamically interact with the button from any angle or height.

![ccdik node button demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27d47cb9-710f-40c3-91a4-71a784b9ebae/buttondemo.gif)

## Property Reference

![ccdik node details pannel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20ac89b7-2860-4ce9-b063-460a816d3f5c/details.png)

Here you can reference the CCDIK node's properties.

| Property | Description |
| --- | --- |
| **Effector Location** | By default this property appears as a pin on the node in the **AnimGraph**. This property's value is the target point to adjust the selected **Tip Bone** to when solving. |
| **Effector Location Space** | Space frame of reference used by the **Effector Location**. |
| **Effector Target** | When the **Effector Location Space** is set to **Bone**, you can define the bone to target in this property. |
| **Tip Bone** | Select the bone from the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) to adjust to meet the **Effector Location**. |
| **Root Bone** | Select the bone from the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) to end the chain, locking the chain's motion to the local root point. |
| **Precision** | Here you can set the tolerance level for the **Tip Bone** adjustment to match the **Effector Location**. A value of 1 is the default value and is most commonly the best for your project. You can increase this value for more precise adjustment or reduce it to decrease the precision. |
| **Max Iterations** | Here you can set the maximum number of solving iterations the node can perform. A higher value will decrease performance but allow for more precise values to be calculated, a lower value will increase your project's performance but not allow for as much precision. A default value of 10 is suitable for more projects. |
| **Start from Tail** | When enabled the debug drawing of the chain will begin from the **Tip Bone** and end at the **Root Bone**. |
| **Enable Rotation Limit** | When enabled, the node will limit the rotation of each joint in the chain based on the **Index** values, in the **Rotation Limit Per Joints** property. |
| **Rotation Limit Per Joints** | Here you can define the rotation limits for each joint between the **Tip Bone** and the **Root Bone** in the chain. The starting **Index** will apply to the joint directly connected to the **Tip Bone** and sequentially work up the chain until the joint that is adjacent to the **Root Bone**. |

## Button Blueprint Reference

Here you can reference the button blueprint, the character blueprint and the character's animation blueprint used to create the button demonstration.

  ![button actor blueprint logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5384efa8-1041-4c1a-be12-fa7d56ef4c87/buttonbp.png) ![character blueprint logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f15110a-a18b-4172-bb7a-192efd667feb/charbp.png) ![character animation blueprint logic](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bb56995-8740-4b46-9b66-968df5866a73/animbp.png)

*Button Actor Blueprint | Character Blueprint | Character Animation Blueprint*