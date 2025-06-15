# Collision Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-in-unreal-engine---overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-in-unreal-engine---overview)  
**Processed:** 2025-06-14 16:13:59

---

**Collision Responses** and **Trace Responses** form the basis for how Unreal Engine 4 handles collision and ray casting during run time. Every object that can collide gets an **Object Type** and a series of responses that define how it interacts with all other object types. When a collision or overlap event occurs, both (or all) objects involved can be set to affect or be affected by blocking, overlapping, or ignoring each other.

**Trace Responses** work basically the same way, except the trace (ray cast) itself can be defined as one of the Trace Response types, thusly allowing Actors to either block it or ignore it based on *their* Trace Responses.

## Interactions

There are a few rules to keep in mind with how collisions are handled:

-   **Blocking** will naturally occur between two (or more) Actors set to Block. However, **Simulation Generates Hit Events** needs to be enabled to execute **Event Hit**, which is used in Blueprints, Destructible Actors, Triggers, etc...
-   Setting Actors to **Overlap** will often look like they **Ignore** each other, and without **Generate Overlap Events**, they are essentially the same.
-   For two or more simulating objects to block each other, they both need to be set to block their respective object types.
-   For two or more simulating objects: if one is set to overlap an object, and the second object is set to block the other, the overlap will occur but not the block.
-   Overlap events **can** be generated even if an object **Blocks** another, especially if traveling at high speeds.
    -   It is not recommended for an object to have both collision and overlap events. Though possible, there is much that needs manual handling.
-   If one object is set to ignore and the other is set to overlap, no overlap events will be fired.

For purposes of testing levels and looking around your worlds:

-   The default **Play In Editor** camera is a pawn. Thusly can be blocked by anything set to block pawns.
-   The **Simulate in Editor** camera, before possessing anything, is **not** a pawn. It can freely clip through everything and will not create any collision or overlap events.

## Common Collision Interaction Examples

These interactions assume that all the objects have **Collision Enabled** set to **Collision Enabled** so they are set to fully collide with everything. If collision is disabled, it is as if **ignore** has been set for all **Collision Responses**.

For the following section, this will be the setup used to explain what is happening:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c7f22c6-c2ca-4d30-9a56-eefeb61f1219/col_setup.png)

The sphere is a **PhysicsBody** and the box is **WorldDynamic**, and by changing their collision settings we can get a number of behaviors.

### Collision

By setting both of their collision settings to block each other, you get a collision, great for having objects interact with each other:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c194183-3ea3-480d-9c45-87b0c7f9aa7a/col_collidenoevent.png)

| Sphere Collision Setup | Wall Collision Setup |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10c10808-3c0e-4637-bfee-e931a8b5e308/col_collidenoevent_sphere.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cd0f624-d01c-4ab3-bf8d-9ed784c11252/col_collidenoevent_box.png) |
| In this case, the sphere is a **PhysicsBody** and it is set to `block` **WorldDynamic** (which is what the wall is). | The wall is a **WorldDynamic** and is set to `block` **PhysicsBody** Actors (which is what the sphere is). |

In this case, the sphere and the wall will simply collide; no further notifications of the collision will take place.

### Collision and Simulation Generates Hit Events

Just collision is useful and in general, the bare minimum for physics interactions, but if you want something to **report** it has collided so a Blueprint or section of code can be triggered:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a708e18-e166-4d3d-9f2c-3a14b5c2f8d1/col_collideevent.png)

| Sphere Collision Setup | Wall Collision Setup |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef4be1fc-2e5f-4e72-9d42-3da3f380de22/col_collideevent_sphere.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dbb79af-e28f-429c-8319-3caeb50a4014/col_collidenoevent_box.png) |
| As in the example above, the sphere is a **PhysicsBody** and it is set to `block` **WorldDynamic** (which is what the wall is). However, the sphere has also enabled **Simulation Generates Hit Events** so it will trigger an event for itself whenever it collides with something. | The wall is a **WorldDynamic** and is set to `block` **PhysicsBody** Actors (which is what the sphere is). Since the wall is not set to **Simulation Generates Hit Events**, it will not generate an event for itself. |

With the sphere set to **Simulation Generates Hit Events**, the sphere will tell itself that it has had a collision. It will fire off events such as **ReceiveHit** or **OnComponentHit** in the sphere's Blueprint. Now if the box had an event for collision, it would not fire because it will never notify itself it has happened.

Further, an object that is reporting rigid collisions will report them all and spam reports when it is just sitting on something, so it is best to be careful to filter what it is colliding within its Blueprint or in code.

### Overlap and Ignore

For all intents and purposes, **Overlap** and **Ignore** work exactly the same **assuming Generate Overlap Events** is disabled. In this case, the sphere is set to overlap or ignore the box:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c26a177-6f71-46d1-ac2f-b21e01cb66f2/col_ignore.png)

| Sphere Collision Setup | Wall Collision Setup |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dba5fbe-071f-496a-a81b-5b8f67213710/col_overlapnoevent_sphere.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/990c2537-8de0-4407-a840-7306f132a6ac/col_collidenoevent_box.png) |
| Here the sphere is set to `overlap` **WorldDynamic** Actors (like our wall), but it does not have **Generate Overlap Events** enabled. As far as the sphere is concerned, it has not collided or overlapped anything, effectively it has ignored the wall. | The wall is a **WorldDynamic** and is set to `block` **PhysicsBody** Actors (which is what the sphere is). As stated above, both Actors need to be set to block each other's respective object types. If they do not, they will not collide. |

Or:

| Sphere Collision Setup | Wall Collision Setup |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e28c57a-cc35-4810-9b1d-a72415c8a3c5/col_ignore_sphere.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11cc85b4-6fa6-42da-a392-01f0c173c6ac/col_collidenoevent_box.png) |
| Here the sphere is set to `ignore` **WorldDynamic** Actors (like our wall), and it will pass through the wall. | The wall is a **WorldDynamic** and is set to `block` **PhysicsBody** Actors (which is what the sphere is). As stated above, both Actors need to be set to block each other's respective object types. If they do not, they will not collide. |

### Overlap and Generate Overlap Events

Unlike collisions that can fire every frame, the overlap events are **ReceiveBeginOverlap** and **ReceiveEndOverlap**, which only fire in those specific cases.

For an overlap to occur, both Actors need to enable **Generate Overlap Events**. This is for performance. In the case where both the Sphere and the Box want overlaps when we move either the Sphere or the Box, we do an overlap query to see if we need to fire any events.

If the Box doesn't want overlaps then when it moves we will not do an overlap query. But now we could be overlapping with the Sphere, and so the Sphere would need to tick and check for overlaps each frame in case someone moved into them.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad3d2476-2cb5-48d9-a548-2380df6f7e78/col_overlapevent.png)

| Sphere Collision Setup | Wall Collision Setup |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a5b75a5-d73a-4b71-b8eb-3ca63c92f8b8/col_overlapevent_sphere.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5260c5a-6e9e-4dfa-b532-d997f3c7ed11/col_collideoverlapevent_box.png) |
| Here the sphere is set to `overlap` **WorldDynamic** Actors (like our wall), and it will generate an event for itself when it does overlap something. | The wall is a **WorldDynamic** and is set to `block` **PhysicsBody** Actors (which is what the sphere is). As stated above, both Actors need to be set to block each other's respective object types. If they do not, they will not collide. But, an **Overlap** does occur here, and events for the sphere and box are fired. |