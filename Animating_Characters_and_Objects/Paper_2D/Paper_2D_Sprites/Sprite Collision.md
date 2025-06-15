# Sprite Collision

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-sprite-collision-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper-2d-sprite-collision-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:56

---

Just like other types of geometry, such as Static Meshes, Skeletal Meshes, etc., **Sprites** can define shapes that are used to calculate collisions with other geometry in the world.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7288e4a7-b080-43a8-a1b3-5fdc19c7b270/collision_shape.png)

## Collision Domain

The method used for calculating collision is defined using the **Sprite Collision Domain** property. There are three different settings:

| Collision Type | Description |
| --- | --- |
| **None** | No collision geometry is generated; use this for purely decorative sprites. |
| **Use 2D Physics** | This is an *experimental* option to generate collision geometry for use with Box2D. See [2D Collision](/documentation/en-us/unreal-engine/paper-2d-sprite-collision-in-unreal-engine#2dcollision) for more information on the current limitations. |
| **Use 3D Physics** | Collision geometry will be generated for use with PhysX. The 2D collision geometry defined in the sprite will be extruded using the Collision Thickness units deep in the perpendicular axis to make 3D collision geometry. |

## Collision Geometry

The **Geometry Type** setting on collision geometry specifies the type of calculation to use for generating the collision geometry. The following settings are available:

| Type | Description |
| --- | --- |
| **Source Bounding Box** | Uses the bounding box of the [Source Region](/documentation/en-us/unreal-engine/how-to-import-and-use-paper-2d-sprites-in-unreal-engine) for the Sprite. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92c03484-bc14-49e5-a39d-fdbe34ba799f/collision_box.png) |
| **Tight Bounding Box** | Generates a tightened bounding box that excludes any fully transparent areas of the Sprite. This results in better collision in most cases. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a740632-857e-4ca9-a565-41aa30dba57d/collision_tight.png) |
| **Shrink Wwrapped** | (*Experimental*) Generates complex geoemetry the conforms to the opaque areas of the Sprite. This results in the most realistic collision, but the added geometry could result in a performance hit. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db674eb4-1b83-43c4-a128-badbe492f320/collision_shrink.png) |
| **Fully Custom** | Enables you to specify the geometry used interactively in the viewport. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f626d657-8c17-4cec-9f9f-b311bc5c58c2/collision_custom.png) |
| **Diced** | Split up into smaller squares, including only no-empty ones in the final geometry. |

The **Edit Collision** mode displays the collision geometry and lets you adjust it in the viewport, automatically setting the mode to fully custom.

The toolbar buttons can be used to add additional polygons or snap vertices to the pixel grid. New vertices can be added by selecting an edge and **Shift+clicking** and selected vertices can be deleted by pressing **Delete**.

## 2D Collision

There is an initial **experimental** integration of Box2D 2.3.1 and various associated changes to enable 2D physics in the engine. This is a totally unsupported and undocumented prototype, exercise great caution and do not use in production. The current build only includes precompiled libraries of Box2D for Win32 and Win64, so 2D collision will not work on other platforms. Collision detection and response is automatic when the 2D domain is selected in a sprite, but queries like point traces must be separately enabled in the Physics project settings (bEnable2DPhysics option).

The integration supports collision detection and response (including Unreal collision channels/filtering), rigid body simulation, and ray casts. Non-zero extent queries, sweep tests, and overlap tests are not implemented yet. Things like CharacterMovementComponent and MoveComponent with bSweep=true rely on these sorts of queries and do not work correctly yet.

The long term integration strategy is to make it a first class citizen, where the same techniques and knowledge used in 3D scenes will directly apply to 2D scenes; for example, there'll only be one Overlap event, not a separate 2D and 3D one. 3D raycasts are already implemented for Box2D and you can both trace 'in-plane' (gameplay traces within the 2D 'world') or 'perpendicular to plane' (things like the Touch input trace to determine the object under your finger / mouse cursor), providing a proper hit result location and normal as well.