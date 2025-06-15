# Bone Driven Controller

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-bone-driven-controller-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-bone-driven-controller-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:17

---

With the **Bone Driven Controller** [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node, you can dynamically affect the motion of a **Target Object**, such as another [Bone](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), **Morph Target** or **Material Parameter**.

## Overview

With this node, you can apply motion data from the **Source Bone** to dynamically adjust another object on the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine), such as a character's accessory object, to avoid geometry intersections during an animation.

![bone driven controller animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1f6d7cd-0b5d-49b8-add0-379e75484c8d/bonedrivencontroller.png)

Here the character's arm bone has been selected as the **Source Bone**, and the shoulder pad bone has been selected as the destination **Target Bone**. As the arm rotates, the Bone Driven Controller node uses the arm bone motion to drive a similar rotation of the shoulder pad bone, to avoid the geometry intersection when no motion occurs on the shoulder pad bone.

|   |   |
| --- | --- |
| ![bone driven controller node disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9211b5c-299e-4e62-b995-52f59319c915/orcdemooff.gif) | ![bone driven controller node enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6e6b3ff-bc2e-4974-b6d5-4d0626a2bc5e/orcdemoon.gif) |
| **Disabled** Bone Driven Controller | **Enabled** Bone Driven Controller |

## Set Up

The Bone Driven Controller node operates within **Component Space**, so a [space conversion](/documentation/en-us/unreal-engine/animation-blueprint-component-space-conversion-in-unreal-engine) will need to occur to implement the node within your character's Animation Blueprint.

With the **Alpha** property or pin, you can control the degree of the applied driven motion on the generated output pose. A value of **1** will fully use the generated output pose, while a value of **0** will output the source pose.

In the **Detail** panel of the Bone Driven Controller node, you first declare the **Source Bone**. Then in the **Source Component Property**, you can select the kind of motion (**Translation**, **Rotation** or **Scale**), and on what axis (**X**, **Y** or **Z**) you want to use from the **Source Bone** as the motion to drive the target object's motion.

![source bone properties in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8201e07e-d272-4e3a-b81a-54201744d954/sourcebone.png)

With the **Multiplier** property you can declare a set value with which to multiply the **Source Bone** motion as it drives the target object.

![miltiplier properties in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f32e584-344d-40aa-9ee4-d3c85773c6d3/multi.png)

If the **Multiplier** property is a value of 0, no motion will occur. The **Multiplier** property is ignored when a **Driving Curve** is selected.

You can assign a curve to modify the **Source Bone** motion within the **Driving Curve** property. Curves can provide more precise control over how the **Source Bone**'s motion data is used to drive the target object.

![curve maping properties in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/682c16cc-3005-4303-8557-41aa6c331fb3/curve.png)

If the **Destination Mode** property is set to **Bone**, an applied motion type must be defined. You can define how the **Source Bone** motion drives the **Target Bone**, by toggling the different axis of motion in the **Translation**, **Rotation** and **Scale** properties. You can enable any combination of these properties, and the source bone motion data will be applied to each additively.

![motion properties attributes values axis axes translation rotation scale in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73bf6c22-17cd-4a99-a74a-03a40d187d21/matrix.png)

If there are no applied motion types selected, no motion will occur.

### Debug

When a Bone Driven Controller node is selected in the **AnimGraph**, a debug object will be drawn in the Viewport window to indicate the associated objects. A **blue line** will be drawn connecting the **Source Bone** to the target object, and a **green cone** will be drawn on the blue line pointed in the direction of the target object.

![bone driven controller displays a blue line conecting source and target bones with a green cone pointing twords the target bone when the node is selected in the animgraph for debug](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/736cbde2-edbf-48aa-a25d-b0d99a673917/debug.png)

## Property Reference

![details panel bone driven controller node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ce433ba-ac5a-4e36-b4c2-d60a8bfb2280/details.png)

Here you can reference a list of the Bone Driven Controller node's properties.

| Property | Description |
| --- | --- |
| **Source Bone** | Select the bone that will be used as the controller to drive the target object. |
| **Source Component** | 
Select which motion component from the **Source Bone** will be used to drive the target object.

You can select any axis (**X**, **Y**, **Z**) from the source object's **Transform**, **Rotation** and **Scale** components.



 |
| **Driving Curve** | Here you can select a curve to map the **Source Bone** attribute to the target object attributes. If no curve is selected, the Bone Driven Controller node will default to using the **Multiplier** property to determine the degree of effect the **Source Bone** attribute has on the target object attributes. |
| **Remap Source** | If enabled, the Bone Drive Controller node will clamp the **Source Bone** attribute and remap them to the curve **before** scaling the values. |
| **Multiplier** | Applies the assigned value as a multiplier to the **Source Bone** attribute to drive the target object. |
| **Destination Mode** | Select the type of object the **Source Bone** motion will drive. You can choose another another [Bone](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine), **Morph Target** or **Material Parameter**. |
| **Target Bone** | When **Bone** is selected in the **Destination Mode** property, you can select a bone to drive with the **Source Bone**. |
| **Target Component Space** | Here you can reference the **Target Bone**'s component space. |
| **Modification Mode** | Toggle any of the **Translation** axes (**X**, **Y**, **Z**) you want driven by the **Source Bone**. |
| **Translation** | Toggle any of the **Translation** axes (**X**, **Y**, **Z**) you want driven by the **Source Bone**. |
| **Rotation** | Toggle any of the **Rotation** axes (**X**, **Y**, **Z**) you want driven by the **Source Bone**. |
| **Scale** | Toggle any of the **Scale** axes (**X**, **Y**, **Z**) you want driven by the **Source Bone**. |
| **Modification Mode** | 

Here you can select the method in which the Bone Driven Controller node will drive the **Target Bone**.

-   **Add to Input**: Will add the driven attribute values to the existing input attribute values.
-   **Replace Component**: Replaces the input attribute values with the driven attribute values.
-   **Add to Reference Pose**: Adds the driven attribute values to the character's reference pose.



 |
| **Parameter Name** | When the **Destination Mode** property is set to **Morph Target** or a **Material Parameter**, you can specify which object you want to drive with the **Source Bone**, by typing the name of the object in the property's field. |