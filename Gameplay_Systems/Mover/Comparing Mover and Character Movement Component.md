# Comparing Mover and Character Movement Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/comparing-mover-and-character-movement-component-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/comparing-mover-and-character-movement-component-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:29

---

We intend for the **Mover** plugin to succeed the **Character Movement Component (CMC)** system. This document aims to help you better understand the two systems' differences.

## High-Level Comparison

| **Mover** | **CMC** |
| --- | --- |
| 
-   Modular
-   Actor-type agnostic
-   Broader shape support
-   Unified rollbacks
-   Client-side corrections
-   Guarded state
-   Move cadence driven by server (unified)
-   Yet untested
-   Networked Physics support



 | 

-   Monolithic
-   Requires ACharacter actor
-   Limited to capsule shape
-   Isolated rollbacks
-   Server-side corrections
-   Open access to state
-   Move cadence driven by client RPCs
-   Battle-hardened with many shipped projects
-   Limited physics interactions



 |

## Replication Model Differences

With CMC, the owning client sends a combination of inputs and state as a "move" at the client's frame rate. The server receives them and performs the same move immediately. The server then compares the state to decide if a correction is needed and replies with either an acknowledgment of the move or a block of corrective state data.

With Mover and Network Prediction, the server and clients simulate on a shared timeline, with clients running predictively ahead of the server by a small amount of time. Clients author inputs for a specific simulation timeframe, and that is all they send to the server. The server buffers these inputs until their simulation time comes. After performing all movement updates, the server broadcasts the state to all clients. The clients decide whether a correction via rollback and resimulation is needed.

Unlike CMC, the state of the Mover actor is not directly modifiable externally at any time. For example, there is no velocity property to manipulate directly. Instead, developers must use modes, instant effects, and other mechanisms to affect change during the next available simulation tick. Additionally, player-provided inputs, such as move input and button presses, must be combined into a single input command for the movement simulation tick rather than immediately affecting the Mover actor's state.

Depending on your project settings, you may have player input from several game world frames contributing to a single movement simulation tick.

![Replication Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/163d6dcf-adbd-488f-bba8-3188178a6548/replication-model.png)

This diagram only shows the Network Prediction model, but Chaos’ Network Physics replication flows similarly.

## Other Notable Comparisons

-   [Movement modes](/documentation/en-us/unreal-engine/mover-features-and-concepts-in-unreal-engine#movementmodes) are similar in both systems but are modular in Mover.
-   [Layered moves](/documentation/en-us/unreal-engine/mover-features-and-concepts-in-unreal-engine#layeredmoves) found in Mover are similar to CMC's Root Motion Sources (RMS).
-   [Transitions](/documentation/en-us/unreal-engine/mover-features-and-concepts-in-unreal-engine#transitions), [Instant Effects](/documentation/en-us/unreal-engine/mover-features-and-concepts-in-unreal-engine#instanteffects), and [Movement Modifiers](/documentation/en-us/unreal-engine/mover-features-and-concepts-in-unreal-engine#movementmodifiers) are new concepts implemented in Mover.
-   In CMC, the Controller and Pawn handle the basic move inputs. Mover does not make assumptions about input, leaving additional work to the project to translate inputs into the movement simulation.
-   In Mover, you can mix movement from modes and layered moves together.
-   Mover makes it easier to add custom movement modes, even from plugins and at runtime.
-   [MoverComponent](/documentation/en-us/unreal-engine/mover-features-and-concepts-in-unreal-engine#movercomponent) does not require or assume a skeletal mesh as the visual representation.
-   MoverComponent requires a root SceneComponent, but it does not have to be a singular vertically-oriented capsule or even a PrimitiveComponent. This is particularly useful for creating non-humanoid characters like dogs or horses.
-   You are free to create Mover actors without collision primitives with Mover.
-   With Mover, the positive Z-axis does not have to be up.