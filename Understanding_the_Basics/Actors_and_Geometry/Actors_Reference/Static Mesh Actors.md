# Static Mesh Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:16

---

The **Static Mesh Actor** is a simple type of Actor that displays a 3D mesh in the Level. Although the name implies that the Actor is static (or unable to move), the "static" refers to the type of mesh used rather than the Actor's ability to move. A mesh is **static** if its geometry does not change. Otherwise, the Actor itself can be moved or changed in other ways during play.

Static Mesh Actors are commonly used to create game worlds or other types of environments.

Unreal Engine includes the following default Static Mesh Actors:

-   Cube
    
-   Sphere
    
-   Cylinder
    
-   Cone
    
-   Plane
    

In addition to these, you can import your own Static Mesh Actors that were created in other 3D applications.

To learn more about how to import content into Unreal Engine, refer to the [Importing Assets Directly](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine) page.

## Placing a Static Mesh Actor

The quickest way to place a Static Mesh Actor is to drag it into the Level Viewport from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine). You can then use its Transform properties to place it where it needs to be.

![Placing a Static Mesh Actor through drag-and-drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50c292cf-9dca-412e-8bb4-e2243875dc79/placing-a-static-mesh-actor.gif)

To learn about other methods for placing Actors, refer to the [Placing Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine) page.

## Changing a Static Mesh Actor's Material

You can override the Materials applied to a Static Mesh individually for each Static Mesh Actor. This way, you can use a single Static Mesh Asset more than once in a Level while giving each a unique appearance.

The example below shows three Static Mesh Actors that use the same Static Mesh, which is a simple three-dimensional cube. Each Actor uses a different Material.

![Three Static Mesh Actors using different Materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca73186b-9c02-42a8-8207-c4d3e53b48ba/cubes.png)

To replace the Material assigned to a Static Mesh, locate the Material in the Content Browser, then drag it over the Static Mesh Actor in the Level Viewport, as shown in the example below.

![Changing the Material assigned to a Static Mesh Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eabb79cb-ffd3-4bdc-b3dc-c39bd85bb006/assigning-material-to-static-mesh.gif)

To learn about other methods for assigning a Material to a Static Mesh, refer to the [Setting Up Materials With Static Meshes](/documentation/en-us/unreal-engine/using-materials-with-static-meshes-in-unreal-engine) page.

## Moving a Static Mesh Actor During Gameplay

An Actor's **Mobility** setting controls whether an Actor can move or change in some way during gameplay.

By default, Static Mesh Actors have **Static** mobility. To move, rotate, or scale a StaticMeshActor during play, you must first make it **Movable**. To do this, in the Actor's **Details** panel, set its **Mobility** to **Movable**.

![An Actor's Movable Mobility property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0523d9e-d8df-474e-a362-f1685322a8e8/actor-mobility-movable.png)

To learn more about different Mobility settings and how they affect Static Mesh Actors, refer to the [Actor Mobility](/documentation/en-us/unreal-engine/actor-mobility-in-unreal-engine) page.

## Enabling Physics for Static Mesh Actors

If you want a Static Mesh Actor to be affected by gravity and collisions, enable the **Simulate Physics** property in the Actor's **Details** panel.

![A Static Mesh Actor's Simulate Physics property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17a80ed6-6112-4622-b0ad-2759ced1f7ab/simulate-physics-property.png)

You can read more about how physics are implemented in Unreal Engine in the [Physics](/documentation/en-us/unreal-engine/physics-in-unreal-engine) section.

In the example below, the sphere Static Mesh Actor has **Simulate Physics** enabled. When simulation starts, gravity affects the sphere and makes it fall until it collides with the ground.

![A sphere Static Mesh Actor affected by gravity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18095553-0940-444f-bf1b-a873a64cc636/sphere-falling.gif)

## Enabling Collision for Static Mesh Actors

**Collision** is an Actor's property to react to other Actors in the environment when they collide with that Actor.

By default, if a Static Mesh has **Physics Bodies**, either generated in your 3D authoring package (see [FBX Content Pipeline](/documentation/en-us/unreal-engine/fbx-content-pipeline)) or in the **Static Mesh Editor** (see [Collision Response Reference](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine)), it will have collision and it will be set to **Block All**.

Refer to the [Collision](/documentation/en-us/unreal-engine/collision-in-unreal-engine) documentation for more information on different types of collision and how they affect a Static Mesh Actor.