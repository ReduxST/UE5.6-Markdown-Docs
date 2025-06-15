# Physics Volume Actor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-volume-actor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-volume-actor-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:02

---

There are some properties that are designated for this volume which can be adjusted from the **Details** panel.

| Property | Description |
| --- | --- |
| **Terminal Velocity** | Determines the Terminal Velocity of Pawns using CharacterMovement when falling. |
| **Priority** | Determines which PhysicsVolume takes precedence if they overlap. |
| **Fluid Friction** | Determines the amount of friction applied by the volume as Pawns using CharacterMovement move through it. The higher this value, the harder it will feel to move through the volume. |
| **Water Volume** | Determines if the volume contains a fluid, like water. |
| **Physics on Contact** | Determines if the Actor is affected by the volume by touching it (by Default, an Actor must be inside the volume for it to affect them). |