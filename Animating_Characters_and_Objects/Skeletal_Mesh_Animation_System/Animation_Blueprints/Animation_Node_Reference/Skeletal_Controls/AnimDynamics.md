# AnimDynamics

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-animdynamics-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-animdynamics-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:12

---

The AnimDynamics [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) node is a light-weight physics simulation solution, that you can use to apply physics-based, secondary animation to parts of a character's [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) at runtime. Unlike the [RigidBody](/documentation/en-us/unreal-engine/animation-blueprint-rigid-body-in-unreal-engine) node that uses the character's [Physics asset](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine), the AnimDynamics node simulates its own physics bodies, to increase your projects performance.

![anim dynamics skeletal control animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf9fcfff-7915-4d62-a242-694bcd797886/animdynamics.png)

With the AnimDynamics node, you can apply simulated-physics motion to parts of your character's skeletal mesh, such as, necklaces, bracelets, wires, or other items, in conjunction with character motion.

Here, the AnimDynamics node is used to dynamically drive the motion of the character's antenna, to react to the motion of the character's head during animation playback.

|   |   |
| --- | --- |
| ![anim dynamics animation blueprint bot demo disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6be81795-b37d-451f-9c07-fd2ca504368a/botdemooff.gif) | ![anim dynamics animation blueprint node bot demo enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37357972-deec-423f-bff0-447c592b9ff9/botdemoon.gif) |
| AnimDynamics Disabled | AnimDynamics Enabled |

## Overview

The AnimDynamics node is a low-performance cost physics-solver that is processed on the AnimGraph at runtime. In order to achieve a low performance cost, the AnimDynamics node makes a few approximations that are important to consider:

-   Simulated **boxes** are used instead of the character's bones or physics bodies, to calculate inertia for each segment.
    
-   Collision is **not** calculated; instead, **constraints** can be used to restrict movement.
    

The AnimDynamics node supports **Linear**, **Angular** and **Planar** constraints to simulate physically-influenced motion. **Linear** and **Angular** constraints can be driven by **springs** to provide a more bouncy feel, while **Planar** constraints can be used to create a plane that the object will not cross. You can toggle each of these constraints, and adjust their associated properties in the AnimDynamics node's **Details** panel.

![anim dynamics skeletal control animation blueprint node constraints settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8216a450-291b-4d69-b092-63e2c1a35ef4/constraints.png)

## Single-Body Simulation

Using the AnimDynamics node you can apply simulated-physics motion to any object on your character using a bone as a reference point. Here is an example of the AnimDyamics node being used to add dynamic motion to a drum that is reacting to the motion of the character's running animation.

|   |   |
| --- | --- |
| ![anim dynamics animation blueprint node drum demo disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5104bd26-8cef-4400-9e4f-1a848f93f405/drumdemooff.gif) | ![anim dynamics animation blueprint node drum demo enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/620f3fba-2dc0-4d42-9fd9-92dc604871d6/drumdemoonclean.gif) |
| AnimDynamics Disabled | AnimDynamics Enabled |

By selecting the drum's bone as the **Bound Bone**, you can control the physics-driven motion by defining a bounding box with the **Box Constraints** property. The **Local Joint Offset** is an offset from the **Bound Bone**'s joint, that you can use to determine the reference point of the constraints.

By leaving the **Box Constraints** and the **Local Joint Offset** properties as their default values, you may not see any movement. This is because the constraints are preventing any motion on the object. By reducing the bounding box's dimensions, you will see motion.

Here, the AnimDynamics's **Debug** properties are enabled. You can use these debug drawings to visually see the **Bounding Box** and **Local Joint Offset** properties as they influence the mesh.

![anim dynamics animation blueprint node debug draw enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37db96bb-58f1-49d7-89d2-8241023d5055/drumdemoondraw.gif)

In this example, **Rotation Constraints** are also set, so the drum can only move along a set axis, within a specified range. The applied Rotation Constraint along the **Y** axis is represented by the green angle overlay, and is useful to prevent the mesh from overlapping on itself.

![anim dynamincs animation blueprint node constraints example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/026a48ac-8efc-4a80-ad6a-3b5013475b85/constraintex.png)

For more information about creating single-body physics simulations using the AnimDynamics node, see the [Creating Dynamic Animations](/documentation/en-us/unreal-engine/creating-dynamic-animations-in-unreal-engine) workflow guide.

### External Force

You can also set an **External Force** to the physics-simulate motion, to weight the object being simulated, or apply more inertia for more reactive motion. By default, an **External Force** vector can be applied using the pin in the AnimGraph.

![anim dynamics external forces input pin property animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9a268c9-043c-44a6-9153-81231462d0b4/externalforces.png)

For more information about using an **External Force** to create physics simulations using the AnimDynamics node, see the [Creating Dynamic Animations](/documentation/en-us/unreal-engine/creating-dynamic-animations-in-unreal-engine) workflow guide.

## Chains

By enabling the **Chain** property in the **Details** panel, you can use the AnimDynamics node is to simulate the motion and collision of a chain of objects.

![anim dynamics animation blueprint node chain demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c8e59ee-0311-4219-a6ce-95d357103e34/chaindemo.gif)

Chain simulation is a much more resource intensive simulation, than a single-body simulation. With chain simulation, linked constraints now need to be solved, which requires many more iterations to correctly converge. Iteration counts are also configurable per-node using the **Num Solver Iterations Pre Update** and the **Num Solver Iterations Post Update** properties in the **Details** panel.

By enabling the **Chain** property and selecting a **Bound Bone** and **Chain End**, the AnimDynamics will generate a chain using any bones in between. Each bone within the chain, **excluding** the **Bound Bone**, will have a constraint box generated around it, to simulate motion and collision with the other bones in the chain. These constraint boxes will need to be tweaked manually to achieve good results.

![anim dynamics animation blueprint chain settings details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19826174-4bff-40ba-9245-468b90e23315/chainsettings.png)

Overlapping constraints can cause undesirable results, like flailing bones and uncontrolled motion. If you are experiencing these kinds of results, ensure the chain constraints are not overlapping.

## Collision Simulation

Using **Planer** and **Spherical** limits, you can enable simple collision simulation with the AnimDyanmic node's simulated physics structures.

### Planer Limits

With planar limits, you can set flat boundaries the physically-simulated structures are unable to cross. You can use these planer constraints to prevent the simulated structures from overlapping with other parts of the character's [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) or the ground.

![anim dynamics planer consrtaints demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c784db7-a8c1-48d1-84bc-b3f74b704d3f/planer.png)

In the AnimDynamics **Details** panel, you can enable planer limits with the **Use Planer Limits** property. Then, using **Add (+)** to create an **Index**, you can set individual planer limits to control the simulated structure's behavior. With each index, you can set a **Driving Bone** as a reference point for the location of the planer limit. Then, using the **Plane Transform** properties, you can set the planer limit's **Location**, **Rotation**, and **Scale** properties to establish planer boundaries that the simulated structure is unable to cross.

For example, adding a planer limit to the character's **root bone**, can create a boundary that represents the ground, that simulated objects are not able to cross.

![anim dynamics planer constraint settings for floor boundary](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be788c6e-c43e-47c6-857d-67995a564c01/planersettings.png)

### Spherical Limits

With spherical limits, you can create sphere boundaries, that surround points on the AnimDynamics physics-simulated structures, to act as a simple collision prevention.

![anim dynamics sphere constraints demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e778409c-d4ba-439e-9fe0-f52467adf477/sphere.png)

After enabling the **Use Spherical Limits** property in the AnimDynamics **Details** panel, you can use **Add (+)** to create an **Index** where you can set up sphere limits. Within each Index you can set a **Driving Bone** to act as a reference point for the location of the sphere and the **offset** its location on the **X**, **Y**, and **Z** axes, with the **Sphere Local Offset** property. You can also set the sphere's **Limit Radius** to determine how large the sphere is, and set the **Limit Type** to decide how the sphere interacts with the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine).

![anim dynamics sphere constraints tail settings demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca84fbc9-2204-40d0-b8ee-8784d1dfe618/spheresettings.png)

By setting the **Limit Type** on a sphere limit to **Outer**, you can use sphere limits to prevent structures from colliding, by not allowing objects to pass through the sphere. You can also use sphere limits to contain structures, by setting the **Limit Type** to **Inner**.

## Property Reference

![anim dynamics animation blueprint node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e080c7e2-2056-4eb2-aa24-d9a19d8abda5/details.png)

Here, you can reference a list of the AnimDynamics properties and a description of their functions:

| Property | Description |
| --- | --- |
| **Preview Live** | When enabled a preview of the live physics object will be drawn on the mesh in the viewport. |
| **Show Linear Limits** | When enabled a preview of the **Linear Limits** (prismatic) will be drawn on the mesh in the viewport. |
| **Show Angular Limits** | When enabled a preview of the **Angular Limit** ranges will be drawn on the mesh in the viewport. |
| **Show Planer Limit** | When enabled a preview of the **Planer Limit** information (actual plane, plane normal) will be drawn on the mesh in the viewport. |
| **Show Spherical Limit** | When enabled a preview of the **Spherical Limits** will be drawn on the mesh in the viewport. |
| **Show Collision Spheres** | If **Planer Limits** are enabled and the **Collision Mode** is set to **Custom Sphere**, **Inner Sphere** or **Outer Sphere** a preview sphere, representing the collson sphere, will be drawn on the mesh in the viewport. |
| **Reset Simulation** | Reset the simulation for this node. |
| **Simulation Space** | 
The space used to run the simulation. The options available for selection are as follows:

-   **Component**: Simulation origin will be calculated using the location and orientation of the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) component.
-   **Actor**: Simulation origin will be calculated using the location and orientation of the [actor](/documentation/en-us/unreal-engine/actors-and-geometry-in-unreal-engine) containing the [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) component.
-   **World**: Simulation origin will be calculated using the world origin.
    
    It is not recommended to use the **World** simulation mode with Teleporting characters.
    
-   **Root Relative**: Simulation origin will be calculated using the location and orientation of the [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine)'s root bone.
-   **Bone Relative**: Simulation origin will be calculated using the location and orientation of the bone specified in the **Relative Space Bone** property.



 |
| **Relative Space Bone** | When the **Simulation Space** is set to **Bone Relative**, the simulation will use the selected bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) as the origin reference. |
| **Chain** | When enabled, the node will use the solver to simulate a connected chain. |
| **Bound Bone** | Select a bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) to attach the physics body to. If the **Chain** property is enabled, the selected bone will become the top, or first, bone of the defined chain. |
| **Chain End** | When the **Chain** property is enabled, the selected bone from the character's [skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) will become bottom, or end, of the defined chain. When the **Chain** property is disabled, this property is ignored. |
| **Box Extents** | Set the extents of the box on the **X**, **Y**, and **Z**, to use for physics simulation. The coordinates within the context of the **Simulation Space** and are in reference to the **Local Joint Offset** location. |
| **Local Joint Offset** | Set the position offset of the **Box Extent**, from the nearest joint to the **Bounding Bone**. |
| **Angular Spring Constraints** | 

Set a Spring constant to use when the **Angular Spring** property is enabled. Higher values mean a stronger spring.

To see results, ensure the **Angular Target Axis** and **Angular Target** properties have been defined.



 |
| **Use Gravity Override** | When enabled the **Gravity Override** property values will be used instead of the **Gravity Scale** for simulation. |
| **Gravity Override** | Set the vector value to override the **Gravity Scale** when **Use Gravity Override** is enabled. |
| **Gravity Override in Sim Space** | When enabled, the **Gravity Override** is defined in simulation space. When disabled, the **Gravity Override** is defined in world space. |
| **Gravity Scale** | Set the scale for gravity use in the simulation. A value of 1 is a full gravity weight while values higher than 1 increase forces due to gravity. |
| **Linear Spring** | When enabled the body will attempt to spring back to its initial position using the **Linear Spring Constraint** property value as a scale. |
| **Angular Spring** | When enabled the body will attempt to align itself with the specified angular target using the **Angular Spring Constraint** property value as a scale. |
| **Linear Spring Constraint** | Set the spring constant to use when calculating linear springs. Higher values mean a stronger spring. |
| **Num Solver Iterations Post Update** | 

Set the number of updates passed on the **Linear** and **Angular** limits, found in the **Constraint** property section of the Details panel. **Post Update** indicates the set number of update passes occurs after the solver has the position of the bodies.

It is recommended that the set value should be around a quarter of the set **Number Solver Iterations Pre Update** property.



 |
| **Do Eval** | When enabled, the node will perform bone transform evaluations. You can disabled this property to see a visualization of the default animation state, to quickly compare the physics simulation to the default animation state. |
| **Num Solver Iterations Pre Update** | 

Set the number of updates passed on the **Linear** and **Angular** limits, found in the **Constraint** property section of the Details panel. **Pre Update** indicates the set number of update passes occurs after the solver has the position of the bodies.

It is recommended that the set value should be about four times the value of the set **NumSolverIterationsPostUpdate** property.



 |
| **Linear Damping Override** | 

Set a value to be used when the **Override Linear Damping** property is enabled.

The default is 0.7. Values below 0.7 won't have an effect.



 |
| **Angular Damping Override** | 

Set the value to be used when the **Override Angular Damping** property is enabled.

The default is 0.7. Values below 0.7 won't have an effect.



 |
| **Angular Bias Override** | 

Set the value to be used when the **Override Angular Bias** property is enabled.

Angular bias performs a twist reduction for chain forces and defaults to a value to keep chain stability in check. When simulating, a single-body angular force can appear delayed from the position of the mesh. If you encounter this issue you can tweak the value of the **Angular Bias Override** towards 1.0f until it settles correctly.



 |
| **Do Update** | When enabled the node will perform physics simulation updates. When disabled will show the base animation pose. This property can be helpful to toggle the node's effects. |
| **Override Linear Damping** | When enabled, the **Linear Damping Override** value will be used to apply linear damping. |
| **Override Angular Bias** | 

When enabled, the **Angular Bias Override** value will be used to apply an angular bias for bodies in this node.

Angular bias is a twist reduction for chain forces and defaults to a value to keep chain stability in check. When using single-body systems sometimes angular forces will look like they are delayed from the mesh's motion, if that's the case enable **Override Angular Bias** and tweak the **Angular Bias Override** value towards 1.0f until it settles correctly.



 |
| **Override Angular Damping** | When enabled the **Angular Damping Override** value will be used to apply angular damping. |
| **Component Linear Acc Scale** | When using non-world space simulation, this property controls how much of the component's world-space acceleration is passed on to the local-space simulation. Vector values can be used on the **X**, **Y**, and **Z** axes. |
| **Component Linear Vel Scale** | When using non-world space simulation, this applies a drag to the bodies in the local space simulation, based on the component's world space velocity. Vector values can be used on the **X**, **Y**, and **Z** axes. |
| **Component Applied Linear Acc Clamp** | When using non-world space simulation, this is an overall clamp on acceleration derived from the **Component Linear Acc Scale** and **Component Linear Vel Scale** properties. |
| **Linear XLimit Type** | Limit the linear X-Axis motion by selecting **Limit**. Select **Free** to disable any limits. |
| **Linear YLimit Type** | Limit the linear Y-Axis motion by selecting **Limit**. Select **Free** to disable any limits. |
| **Linear ZLimit Type** | Limit the linear Z-Axis motion by selecting **Limit**. Select **Free** to disable any limits. |
| **Linear Axes Min** | 

Set the minimum values to allow linear movement per-axis, **X**, **Y**, and **Z**.

To lock linear motion on a specific axis, set the value to 0 on the desired axis in the **Linear Axes Min** and **Linear Axis Max** properties.



 |
| **Linear Axes Max** | 

Set the maximum values to allow linear movement per-axis, **X**, **Y**, and **Z**.

To lock linear motion on a specific axis, set the value to 0 on the desired axis in the **Linear Axes Min** and **Linear Axis Max** properties.



 |
| **Angular Constraint Types** | Select the method to use when constraining angular motion. **Angular** will limit the motion, based on the parameters set in the **Angular Limits Min**, **Angular Limits Max**, **Angular Target Axis**, and **Angular Target** properties. **Cone** will limit the motion within a cone, whose origin point is vectored from the **Bound Bone**'s joint, and angle is set in the **Cone Angle** property. |
| **Twist Axis** | Select which axis, **X**, **Y**, and **Z**, the twist will be occurring along when constraining angular motion. |
| **Cone Angle** | Set the cone angle to use when **Angular Constraint Types** is set to **Cone**. |
| **Angular Limits Min** | Set the minimum angle limits on each axis, **X** **Y**, and **Z**, to use when **Angular Constraint Types** is set to angle. |
| **Angular Limits Max** | Set the maximum angle limits on each axis, **X** **Y**, and **Z**, to use when **Angular Constraint Types** is set to angle. |
| **Angular Target Axis** | 

Set the axis, **X** **Y**, and **Z**, the angle will be used to align to the **Angular Target**. Typically, this is the axis pointing along the **Bound Bone**.

This is affected by the Angular Spring Constraints.



 |
| **Angular Target** | 

Set the axis to align the **Angular Spring Constraint** to. A value of 0 will disable the axis while a value of 1 will enable the axis when factoring the alignment.

The properties values are typically set to point down the bone. For example, the property might be set to (1.0, 0.0, 0.0), but you can pick other values to align the spring to a different direction.



 |
| **External Forces** | When set, an external force can be applied to all bodies in the simulation, specified in world space. By default this property appears as a Pin on the node in the AnimGraph. Also see the [External Force Section](/documentation/en-us/unreal-engine/animation-blueprint-animdynamics-in-unreal-engine#externalforce) of this page. |
| **Collision Type** | 

Set the resolution method to use when **Planer Limits** are enabled. Options include: **CoM** (**Center of Mass**): Only limits the center of mass from crossing planes. **Custom Sphere**: Use the specified sphere radius to collide with planes. **Inner Sphere**: Use the largest sphere that fits entirely within the body extents to collide with planes. **Outer Sphere**: Use the smallest sphere that fully contains the body extents to collide with planes.



 |
| **Sphere Collision Radius** | Set the radius to calculate a sphere when **Collision Type** is set to **Custom Sphere**. |
| **Use Spherical Limits** | When enabled, spherical limits will be evaluated. |
| **Spherical Limits** | 

When **Use Spherical Limits** is enabled, you can add spherical limits to the array. After adding an element, it's properties include:

**Driving Bone**: Bone to attach the sphere to. **Sphere Local Offset**: Local offset for the sphere, if no driving bone is set the is in node space, otherwise bone space. **Limit Radius**: Set the radius of the sphere. **Limit Type**: Whether to lock bodies inside (**Inner**) or outside (**Outer**) the sphere.



 |
| **Use Planer Limits** | When enabled, planer limits will be evaluated. |
| **Planer Limits** | 

When **Use Planer Limits** is enabled, you can add planer limits to the array. After adding an element, it's properties include:

**Driving Bone**: When using a driving bone, the plane transform will be relative to the bone transform. **Planer Transform**: Set the transform of the plane. This is either in component space if no **Driving Bone** is specified, or in bone space if a driving bone is present. Set the **X**, **Y**, and **Z** values for the planes **location**, **rotation**, and **scale** properties.



 |
| **Enable Wind** | When enabled wind is factored for the bodies in this simulation. |
| **Wind Scale** | Set the scale to apply calculated wind velocities in the solver. |