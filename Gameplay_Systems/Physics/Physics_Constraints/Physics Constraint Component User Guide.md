# Physics Constraint Component User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-constraint-component-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-constraint-component-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:47

---

## Overview

Physics Constraint Components operate just like **[Physics Constraints Actors](/documentation/en-us/unreal-engine/constraints-user-guide-in-unreal-engine)**, except they are used in Blueprints or can be created in C++. Given the flexibility of Blueprints and the power of C++, you can constrain just about any Physics Body in your project using Physics Constraint Components.

This document will cover Physics Constraint Component basic creation in a Blueprint.

This document assumes that the user has some knowledge of **Blueprints** and the **Blueprint Editor**.

## Usage

1.  Create the Components that will be used to constrain. For this demonstration, two **StaticMesh** Components referencing the StaticMesh `Shape_Cube` will be used.
    
    ![Two StaticMesh Components referencing the StaticMesh ShapeCube will be used](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f5cba1a-bcc7-4487-8721-e15a81563d4d/physics-constraint-blueprint-cubes.png)
    
    You will need to position the Components that you want to be constrained. For this guide, these two cubes are used.
    
2.  Enable **Simulate Physics** for the lower of the two StaticMesh Components.
    
    ![Enable Simulate Physics](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5db37929-4af7-49e0-927f-c7cf6e135ccd/simulate-physics.png)
3.  Click **Add Component** to find **Physics Constraint**.
    
    ![Click Add Component to find Physics Constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f4cf794-14b3-4b55-aa08-591735047cab/physics-constraint-blueprint-add-constraint.png)
4.  Position the Physics Constraint Component where you wish the joint of the constraint to be.
    
    ![Position the Physics Constraint Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2849c110-a975-4171-a9c6-186a6c5af1d0/physics-constraint-blueprint-location.png)
5.  You must manually type in the names of the StaticMesh Components you wish to constrain in the **Details** panel of the Physics Constraint Component. Type in the component name you wish to constrain in the **Component Name 1** of the **Component Name** property.
    
    ![Type in the component name you wish to constrain in the Component Name 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29592d77-ebf2-4f68-9390-2a49633dc098/physics-constraint-blueprint-component-1.png)
6.  Type in the component name you wish to constrain in the **Component Name 2** of the **Component Name** property.
    
    ![Type in the component name you wish to constrain in the Component Name 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6afcbed1-9008-4d43-b550-52895052dd6b/physics-constraint-blueprint-red-blue-2.png)
7.  Select the Physics Constraint component and move its location to the bottom of the StableMesh component. This will place the anchor point at the bottom of the cube.
    
    ![Select the Physics Constraint component and move its location to the bottom of the StableMesh component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f8a4073-45e4-4ca4-89d1-6d4e8686bd61/physics-constraint-blueprint-components.png)
    
    Want to know what all the properties on a Physics Constraint Component affect? See the **[Physics Constraint Reference](/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine)** for specific details.
    
8.  Rotate the Physics Constraint Component as necessary to account for Linear and Angular Limits.
    
    ![Rotate the Physics Constraint Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c44daee5-e5d2-426c-8f07-2f865acf3e31/physics-constraint-blueprint-rotated.png)
9.  Place the **Blueprint Actor** in a level and position it where you need it.
    
    ![Place the Blueprint Actor in a level and position it where you need it](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82c3f488-617e-4f40-99dc-b1df166882be/physics-constraint-blueprint-into-world.png)
10.  Select **Blueprint Actor** and go to the **Details** panel. Select the **ConstrainedMesh** component in the hierarchy and move it as seen in the picture. In this example, the **location** was set to **X = -300** and **Z = 100**. This will allow the ConstrainedMesh to swing once you press **Simulate**.
    
    ![Select Blueprint Actor and go to the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28034571-8a9a-4c26-9eb0-bd8d41af7bbd/blueprint-actor-details.png)
11.  Test by using **Simulate in Editor** or **Play in Editor**.
    
    ![physics-constraint-blueprint-simulate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/927e9d81-5f58-4c99-9120-be6ae7b56d41/physics-constraint-blueprint-simulate.gif)