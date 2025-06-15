# Twist Corrective

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-twist-corrective-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-twist-corrective-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:48

---

With the **Twist Corrective** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can drive [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine), like [Morph Targets](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), using the transform of a delta angle calculated using a **Base Frame** and **Twist Frame** against the direction of a **Twist Planer**.

![twist corrective animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ff9b523-9459-47c0-a14a-994017d89b96/twist.png)

## Overview

Using the Twist Corrective node, you can drive [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) values, such as [Morph Targets](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), based on the twist of one bone relative to another.

Here is an example of a character's scarph morph targets adjusting as the head bone is twisted, to create a more natural look.

|   |   |
| --- | --- |
| ![twist corrective disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbb0c307-c95b-4a0e-9611-439b7208d466/demooff.gif) | ![twist corrective enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6f5ac0a-5ab4-41bf-808c-a13ffe6d637f/demoon.gif) |
| Disabled Twist Corrective | Enabled Twist Corrective |

### Example Workflow

The Twist Corrective node operates within **Component Space**, so a [space conversion](/documentation/en-us/unreal-engine/animation-blueprint-component-space-conversion-in-unreal-engine) will need to occur to implement the node within your character's Animation Blueprint.

First, you must select a bone to act as the **Base Frame**, to calculate the twisting bone's alpha from. It is also important to define on what axis the motion the twist alpha will be in reference to. In the Axis property define which axis the motion will occur by setting the value to **1**. In the provided example the `neck_02` bone was used and the **Z**\-axis was given a value of **1**.

![base frame settings in the twist corrective animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5495c034-4206-4096-bcc5-06ba456ff8b3/baseframe.png)

Next select the bone that is undergoing the twist motion as the **Twist Frame Bone**, in the example the **head** bone is used. You must also define the axis of motion, in this case the property will replicate the **Base Frame Axis** with only a value of **1** on the **Z**\-Axis.

![twist frame settings in the twist corrective animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7502f61-5ccd-4c70-aa3f-954014433c00/twistframe.png)

You must also set the twist plane as a reference point, to calculate the alpha motion. In the example, the **Y**\-Axis was enabled by setting a value of **1** in the **Y**\-Axis field.

![twist plane normal axis settings in the twist corrective animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8edf106b-9ae4-4804-86db-5dc7d3b2b70f/twistplane.png)

Finally, you must input the name of the [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine). In the workflow example, the morph target `C_BipedHeadNeck_A_NeckMid_Jnt_n11_44_n1` is used.

![curve name settings in the twist corrective animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c8c3d7a-527c-46b6-8f28-b25368b238d2/curvename.png)

After compiling the Animation Blueprint the effects should be visible as the head bone rotates on the **Z**\-Axis in the viewport.

## Property Reference

![twist corrective animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9525967-9148-40c4-8ae6-a37af3dfc55c/details.png)

Here you can reference a list of the Twist Corrective node's properties.

| Property | Description |
| --- | --- |
| **Base Frame** | 
The Base Frame series of properties defines the reference point to calculate the motion alpha of the **Twist Frame**.

In the **Bone** property, you can select the bone to use as the Base Frame from the characters [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine).

In the **Axis** property, you can select what axes of motion to calculate motion. A value of **0** will not calculate motion, a value of **1** will calculate positive motion, and a value of **\-1** will calculate negative motion.

You can also enable the **In Local Space** property to calculate motion in local space, or disable **In Local Space** to calculate motion in world space.



 |
| **Twist Frame** | 

The Twist Frame series of properties defines the twisting bone to calculate the motion alpha from in relation to the **Base Frame** and **Twist Planer Normal Axis**.

In the **Bone** property, you can select the bone to use as the Twist Frame from the characters [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine).

In the **Axis** property, you can select what axes of motion to calculate motion. A value of **0** will not calculate motion, a value of **1** will calculate positive motion, and a value of **\-1** will calculate negative motion.

You can also enable the **In Local Space** property to calculate motion in local space, or disable **In Local Space** to calculate motion in world space.



 |
| **Twist Planer Normal Axis** | 

Here you can set the normal of the plane to calculate the angle alpha of the **Twist Frame** from the **Base Frame**.

In the **Axis** property, you can select what axes of motion to calculate motion. A value of **0** will not calculate motion, a value of **1** will calculate positive motion, and a value of **\-1** will calculate negative motion.

You can also enable the **In Local Space** property to calculate motion in local space, or disable **In Local Space** to calculate motion in world space.



 |
| **Max Angle in Degree** | Set the maximum limit of the twist that will output a value to the **Curve**. For example, the degree at which the twist should result in the maximum curve value being outputted. Values cannot exceed 180. |
| **Mapped Range Min** | Minimum value to apply to the curve. A value of 0 being the beginning of the curve and a value of **1** being the end of the curve. |
| **Mapped Range Max** | Maximum value to apply to the curve. A value of 0 being the beginning of the curve and a value of **1** being the end of the curve. |
| **Curve** | Input the name of the [Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) or [Morph Targets](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) you wish to apply the **Mapped Range Min** and **Mapped Range Max** based on the calculated twist alpha from the **Twist Frame Bone**. |