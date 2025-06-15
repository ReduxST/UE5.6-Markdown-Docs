# Skeletal Mesh Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:37

---

The **Skeletal Mesh Actor** displays an animated mesh whose geometry can be deformed, typically through the use of control points during animation sequences. These can either be created and exported from external 3D animation applications, or programmed directly in Unreal Engine.

To learn more about how to import content into Unreal Engine, refer to the [Importing Assets Directly](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine) page.

Like the name suggests, Skeletal Meshes have a **skeleton** that consists of a number of **bones**. These are used in the animation process.

Skeletal Mesh Actors are commonly used to represent player characters, NPCs, other animated creatures, and complex machinery. The Unreal Engine Mannequin that appears in the [Third Person template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) is an example of a Skeletal Mesh Actor.

## Placing a Skeletal Mesh Actor

The quickest way to place a Skeletal Mesh Actor is to drag it into the Level Viewport from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine). You can then use its Transform properties to place it where it needs to be.

![Placing a Skeletal Mesh Actor from the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc760f3e-3c9f-4f4e-b472-2421f9b64575/placing-skeletal-mesh.gif)

To learn about other methods for placing Actors, refer to the [Placing Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine) page.

## Animating a Skeletal Mesh Actor

There are two basic ways to animate a Skeletal Mesh Actor in Unreal Engine:

-   Using an [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) to play and blend multiple animations together.
    
-   Using an Animation Asset to play a single [Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) one time or in a loop.
    

To learn more about animating Skeletal Meshes, refer to the [Skeletal Mesh Animation System](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine) page.

## Changing a Skeletal Mesh Actor's Material

You can override the material of a Skeletal Mesh Actor individually to change its appearance. This is useful if you want to use the same Static Mesh in the Level multiple times, but want to have some variation between them.

The example below shows three Skeletal Mesh Actors that use the Unreal Mannequin Skeletal Mesh. Each Actor uses a different Material.

![Unreal Mannequins using different Materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/822ff27d-06c3-4303-904b-39cb33207d1f/mannequins-different-materials.png)

To replace the Material assigned to a Skeletal Mesh, locate the Material in the Content Browser, then drag it over the Skeletal Mesh Actor in the Level Viewport, as shown in the example below.

![Changing a Skeletal Mesh Actor's Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9068e6e-08a4-4dfc-9baf-d705c013991e/changing-skeletal-mesh-material.gif)

To use a Material with a Skeletal Mesh Actor, you need to enable the **Used with Skeletal Mesh** option. To do this:

1.  In the **Content Browser**, double click the **Material** to open it in the **Material Editor**.
    
2.  In the **Details** panel, enable the **Used with Skeletal Mesh** option.
    

The Used with Skeletal Mesh option in the Material Editor. Click for full size.

## Skeletal Mesh Actor Collision

Normal collision creation and detection does not work with Skeletal Mesh Actors. To have your Skeletal Meshes collide with objects in the Level, your Skeletal Mesh Actors need to have a **Physics Asset** that is specifically created for them.

To learn more about Physics Assets and their use, refer to the [Physics Asset Editor](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine) documentation.

To create and assign a Physics Asset to a Skeletal Mesh Actor, follow these steps:

1.  Find the **Skeletal Mesh** in the **Content Browser** and right-click it.
    
2.  In the **context menu**, select **Create > Physics Asset > Create and Assign**.
    

![Creating and assigning a Physics Asset to a Skeletal Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ead05087-401e-4060-9ee5-567a94e5cf47/creating-physics-asset.png)

Creating and assigning a Physics Asset to a Skeletal Mesh.