# Collision Response Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:00

---

There are a large number of properties and settings in the Collision Presets/Collision Response section of the Collision Properties category, so they've been separated out for clarity.

## Properties

Below are the properties for the Collision Presets, a sub-category in the Collision Properties on Physics Bodies (BodyInstances).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5f21381-a8dd-403c-9c9b-ae75f7e76e70/collprop.png)

### Collision Presets

-   [**Collision Presets Defaults**](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine#collisionpresetsdefaults)
-   [**Collision Enabled**](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine#collisionenabled)
-   [**Object Type**](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine#objecttype)
-   [**Collision Responses**](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine#collisionresponses)
-   [**Trace Responses**](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine#traceresponses)
-   [**Object Responses**](/documentation/en-us/unreal-engine/collision-response-reference-in-unreal-engine#objectresponses)

#### Collision Presets Defaults

The default collision profiles and any you have created in Project **Settings** -> **Engine** -> **Collision** -> **Preset** (see: [Add a Custom Object Type to Your Project](/documentation/en-us/unreal-engine/add-a-custom-object-type-to-your-project-in-unreal-engine) for information on creating custom collision profiles), will appear here.

| Property | Description |
| --- | --- |
| **Default** | Use the settings that were applied to the Static Mesh in the Static Mesh Editor. |
| **Custom...** | Set all custom collision settings for this instance. |
| **NoCollision** | No Collision. |
| **BlockAll** | WorldStatic object that blocks all actors by default. All new custom channels will use its own default response. |
| **OverlapAll** | WorldStatic object that overlaps all actors by default. All new custom channels will use its own default response. |
| **BlockAllDynamic** | WorldDynamic object that blocks all actors by default. All new custom channels will use its own default response. |
| **OverlapAllDynamic** | WorldDynamic object that overlaps all actors by default. All new custom channels will use its own default response. |
| **IngoreOnlyPawn** | WorldDynamic object that ignores Pawn and Vehicle. All other channels will be set to default. |
| **OverlapOnlyPawn** | WorldDynamic object that overlaps Pawn, Camera, and Vehicle. All other channels will be set to default. |
| **Pawn** | Pawn object. Can be used for capsule of any playable character or AI. |
| **Spectator** | Pawn object that ignores all other actors except WorldStatic. |
| **CharacterMesh** | Pawn object that is used for Character Mesh. All other channels will be set to default. |
| **PhysicsActor** | Simulating actors. |
| **Destructible** | Destructible actors. |
| **InvisibleWall** | WorldStatic object that is invisible. |
| **InvisibleWallDynamic** | WorldDynamic object that is invisible. |
| **Trigger** | WorldDynamic object that is used for trigger. All other channels will be set to default. |
| **Ragdoll** | Simulating Skeletal Mesh Component. All other channels will be set to default. |
| **Vehicle** | Vehicle object that blocks Vehicle, WorldStatic, and WorldDynamic. All other channels will be set to default. |
| **UI** | WorldStatic object that overlaps all actors by default. All new custom channels will use its own default response. |

#### Collision Enabled

Collision Enabled can have 4 possible states as listed below.

| Property | Description |
| --- | --- |
| **No Collision** | This body Will have no representation in the physics engine. It cannot be used for spatial queries (raycasts, sweeps, overlaps) or simulation (rigid body, constraints). This setting gives the best performance possible, especially for moving objects. |
| **Query Only** | This body is used only for spatial queries (raycasts, sweeps, and overlaps). It cannot be used for simulation (rigid body, constraints). This setting is useful for character movement and objects that do not need physical simulation. Some performance gains are made by reducing the data in the physics simulation tree. |
| **Physics Only** | This body is only for physics simulation (rigid body, constraints). It cannot be used for spatial queries (raycasts, sweeps, overlaps). This setting is useful for simulated secondary motion on characters that do not need per bone detection. Some performance gains are made by reducing the data in the query tree. |
| **Collision Enabled** | This body can be used for both spatial queries (raycasts, sweeps, overlaps) and simulation (rigid body, constraints). |

#### Object Type

| Property | Description |
| --- | --- |
| **WorldStatic** | This should be used for any Actor that doesn't move. Static Mesh Actors are a good example of an Actor that will probably have a WorldStatic type. |
| **WorldDynamic** | WorldDynamic is for Actor types that will be moving under the influence of animation or code; kinematic. Lifts and doors are good examples of WorldDynamic Actors. |
| **Pawn** | Any player controlled entity should have the Pawn type. The player's character is a good example of an Actor that should receive the Pawn Object Type. |
| **PhysicsBody** | Any Actor that will be moving due to the physics simulation. |
| **Vehicle** | Vehicles receive this type by default. |
| **Destructible** | Destructible Meshes receive this by default. |

#### Collision Responses

These define how this Physics Body should interact with all of the other types of Trace and Object Types. Remember, it's the interaction between both Physics Bodies that define the resulting action, so the Object Type and Collision Responses of both Physics Bodies matter.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca41bfdf-498e-4109-bf4c-5a445379269d/iob.png)

| Response | Description |
| --- | --- |
| **Ignore** | Regardless of the Collision Response of the other Physics Body, this Physics Body will ignore the interaction. |
| **Overlap** | If the other Physics Body is set to Overlap or Block this Physics Body's Object Type, an Overlap Event can occur. |
| **Block** | If the other Physics Body is set to Block this Physics Body's Object Type, a Hit Event can occur. |

#### Trace Responses

Trace responses are used in Traces (ray casts), such as the Blueprint Node **Line Trace by Channel**.

| Property | Description |
| --- | --- |
| **Visibility** | General visibility testing channel. |
| **Camera** | Usually used when tracing from the camera to something. |

#### Object Responses

| Property | Description |
| --- | --- |
| **WorldStatic** | How this Physics Body should react when interaction with a WorldStatic Physics Body Object Type. |
| **WorldDynamic** | How this Physics Body should react when interaction with a WorldDynamic Physics Body Object Type. |
| **Pawn** | How this Physics Body should react when interaction with a Pawn Physics Body Object Type. |
| **PhysicsBody** | How this Physics Body should react when interaction with a PhysicsBody Physics Body Object Type. |
| **Vehicle** | How this Physics Body should react when interaction with a Vehicle Physics Body Object Type. |
| **Destructible** | How this Physics Body should react when interaction with a Destructible Physics Body Object Type. |