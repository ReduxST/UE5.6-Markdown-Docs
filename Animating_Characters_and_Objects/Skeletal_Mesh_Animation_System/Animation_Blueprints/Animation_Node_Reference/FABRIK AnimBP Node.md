# FABRIK AnimBP Node

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fabrik-animation-blueprint-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fabrik-animation-blueprint-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:09

---

**Forward And Backward Reaching Inverse Kinematics** (**FABRIK**) is an **IK solver** that operates on a chain of [bones](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) of arbitrary length as long as there are at least of 2 bones links in the chain.

![fabrik animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a17c53f3-d44e-4f9a-9690-a6b400c643a1/fabrik.png)

## Overview

You can add the **FABRIK** blueprint node to the **AnimGraph** of your Animation Blueprint. Once added, you can integrate the FABRIK node into your AnimBP using your objects **Component Pose**.

You can use the FABRIK node's **Effector Transform** input pin to connect a [transform variable](/documentation/en-us/unreal-engine/blueprint-variables-in-unreal-engine) to implement a **relative** or **absolute** bone transform to the chain. You can use a relative transform to reference a different bone from the same skeleton for the transform, or transform the chain without a reference using an absolute transform.

![effector transform variable input pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/212facfc-bd15-4af3-bf15-acbbbfbf193c/transformvar.png)

In order to determine the strength of the applied **Skeletal Control**, you can set an alpha value on the **Alpha** input pin, either manually on the Alpha input pin or with a dynamic variable in the AnimGraph. Larger alpha values apply more Skeletal Control, while lesser values apply less.

![alpha variable value input pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4b92b83-738b-4733-a67d-55a0c109bac5/alpha.png)

## Properties and Settings

Inside the **Details** panel for the **FABRIK** node you will find additional settings which you can be use to adjust how the solver functions:

![fabrik animation blueprint node properties details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fed69ca3-cc5d-43d6-8142-9bc97d5c30ac/fabrik_details.png)

In the **End Effector** section, you determine the target location and rotation.

The **End Effector** properties, found in the FABRIK node's details panel are very similar to the [TwoBone\_IK](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) node properties.

| Property | Description |
| --- | --- |
| **Location, Rotation, Scale** | Coordinates for target location of tip bone. If the **EffectorLocationSpace** property is set to **bone**, this is the offset from Target Bone to use as target location (can also be set as a Pin on the node). |
| **Effector Transform Space** | Set the position of the bone in SkeletalMeshComponent's reference frame. |
| **Effector Transform Bone** | If the **Effector Transform Space** property is set to **bone**, this properties defined bone will be used. |
| **Effector Rotation Source** | Control the Rotation (maintain component space, local space or match end effector target rotation). |

In the **Solver** section, you define the chain of bones to use, from the **Root** to the **Tip**. The Tip will try to reach the end effector location.

| Property | Description |
| --- | --- |
| **Tip Bone** | Define a bone as the **Tip Bone** from the **Skeleton Tree**. |
| **Root Bone** | Set a reference to the skeleton's **Root Bone** from the **Skeleton Tree**. |
| **Precision** | Here you can set a value that will operate as the **Tolerance** for final **tip bone** location delta from **Effector Location** input pin. The lower the tolerance, the more precise the tip bone's location will be in relation to the **End Effector** target, but will result in higher performance cost for the evaluation. |
| **Max Iterations** | Here you can set the maximum number of iterations allowed. You can tune this value in order to control performance cost of the evaluation to ensure high volume usage will not reduce your project's frame rate. |
| **Enable Debug Draw** | Here you can toggle drawing of axes to debug joint rotation. |

In the **Settings** section, you set the strength applied.

| Property | Description |
| --- | --- |
| **Alpha** | Current strength of the Skeletal Control (can also be set as a Pin on the node). |
| **Alpha Scale Bias** | Set the **Minimal** and **Maximal** input scale values. |
| **Node** | Can be used to reset the **Effector Rotation Source** if it is set to something other than **Local Rotation Relative to Parent**. |