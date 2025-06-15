# Physics Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:46

---

The Physics Components are used to affect any objects that are utilizing physics at your level in varying ways.

## Physical Animation Component

The **Physical Animation Component** applies a **physics simulation** on top of the animation of a **Skeletal Mesh**. By using this component you can apply realistic physical simulations to specific groups of bones in the Skeletal Mesh, while still playing an animation.

![Physical Animation Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/093917e2-1bb0-417d-a8c5-cefbf75178e6/ue5_1-physical-animation.png)

## Physics Constraint Component

A **PhysicsConstraintComponent** is a joint that allows you to connect two rigid bodies. You can create different types of joints using the various parameters of this Component.

By using a **Physics Constraint Component** and two **Static Mesh Components**, you can create dangling type objects such as a tire swing, heavy bag, or sign that reacts to physics in the world allowing players to interact with the Component (see **[Constraints Blueprints](/documentation/en-us/unreal-engine/physics-constraint-component-user-guide-in-unreal-engine)** for an example in **Blueprints**).

![Physics Constraint Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca3cc9c9-74ec-4e5c-8983-9d78de1d34db/ue5_1-constraint.png)

## Physics Handle Component

The **Physics Handle Component** is an object for "grabbing" and moving physics objects around while allowing the object you are grabbing to continue to use physics. An example of this could be in the form of a "gravity gun" where you can pick up and drop physics objects (see the [**Physics Content Examples**](/documentation/en-us/unreal-engine/physics-in-unreal-engine) for more information).

![Physics Handle Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14a81db0-f995-4c89-8c51-741568010aa3/ue5_1-handle.png)

## Physics Thruster Component

A **Physics Thruster Component** is used with objects that have physics to apply a specified force down the negative-X direction (i.e. point X in the direction you want to thrust in). The thruster uses continuous force and can be auto-activated, activated ,or deactivated through the script.

An example of using a thruster is in the form of a rocket (pictured below) which continuously applies force propelling the rocket upward (since the thruster is positioned under the rocket). You can contain the movement of the Component that is influenced by a thruster by using **Blocking Volumes**.

![Physics Thruster Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/debed437-c50c-4e7d-89c9-052c8af96a74/ue5_1-thruster.png)

## Radial Force Component

The **Radial Force Component** is used to emit a radial force or impulse that can affect physics objects and or destructible objects. Unlike a **Physics Thruster Component**, this type of Component applies a "fire-and-forget" type of force and is not continuous.

You can use this type of Component to push the fractured pieces of a destroyed object, for example, an explosion. Using a **Radial Force Component** to specify the force and direction, when an object is destroyed you can "push" the pieces outwards in a particular direction as seen in the example image below (see the [**Destructibles Content Examples**](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) for more information).

![Radial Force Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b80d388-3ddf-4659-8a8d-e0f01db1cb34/ue5_1-radial_force.png)