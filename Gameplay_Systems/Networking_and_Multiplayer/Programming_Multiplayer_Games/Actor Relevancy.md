# Actor Relevancy

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-relevancy-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-relevancy-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:35

---

Unreal Engine levels can be very large. At any time, a player might only see a small fraction of the total number of actors in a level. Most of the actors are not visible or audible, nor do they have a significant effect on the current player. The set of actors the server determines are capable of affecting a client in any significant way are considered **relevant** for this client. The set of relevant actors is determined on a per-client, or, in networking terms, a per-connection basis. Unreal Engine only replicates actors to a client if they are relevant for that client.

The following image comparison showcase a contrived example that uses *distance-based* relevancy. The primary actor (in the middle of the frame) is set to have replicated actors remain relevant if they are within 300 centimeters (3 meters). In the before image, the secondary actor is within 300 cm, and is relevant. This means that the secondary actor is replicated to the primary actor’s connection and is visible. In the after image, the secondary actor has traveled beyond 300 cm from the primary actor; therefore, the actor is no longer relevant to the primary actor, is not replicated to the primary actor’s connection, and is not visible.

![Actor relevant](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ca17027-75c5-4368-8832-38afcb08ba42/actor-relevant.png)

![Actor not relevant](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31c80eb4-51f4-4698-b6e4-be584cb9266f/actor-not-relevant.png)

Dynamically spawned, replicated actors are destroyed on the client when they are no longer relevant. This is why the secondary actor is no longer visible to the primary actor in this case.

## Obtain an Actor’s Relevancy

The network driver determines whether an actor is relevant for a particular connection with a call to [`AActor::IsNetRelevantFor`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/IsNetRelevantFor). This is handled automatically by the network driver.

### Make an Actor Relevant

You can force any actor to be relevant by calling [`AActor::ForceNetRelevant`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/ForceNetRelevant) in your `AActor`\-derived class.

### Override Actor Relevancy

You can customize actor relevancy by overriding the virtual function `AActor::IsNetRelevantFor` in your `AActor`\-derived class.

Use caution when overriding `AActor::IsNetRelevantFor`. This may have unintended consequences if you are not familiar with Unreal Engine's replication system.

## How Relevancy is Determined

The virtual function `AActor::IsNetRelevantFor` implements several tests to determine the set of actors that are relevant to a connection.

### Parameters

`AActor::IsNetRelevantFor` uses three parameters to determine whether the calling actor object is relevant:

| **Parameter** | **Description** |
| --- | --- |
| `RealViewer` | Client network object controlling the current actor for which relevancy is being checked. This is usually a Player Controller. |
| `ViewTarget` | Actor currently viewed or controlled by `RealViewer`. This is usually a Pawn. |
| `SrcLocation` | Source location of the controlling network object. This is used when distance-based relevancy is enabled. |

### Relevancy Logic

For a given actor and connection, the following tests are performed:

-   If at least one of the following conditions hold, then the current actor is relevant for this connection:
    -   The current actor is always relevant.
    -   The current actor is owned by the current connection’s Pawn.
    -   The current actor is owned by the current connection’s Player Controller.
    -   The current actor is the current connection’s Pawn.
    -   The current connection’s Pawn is the instigator of some action, such as noise or damage.
-   If the following conditions hold, then the replication system uses the current actor’s owner’s relevancy to determine whether it is relevant for this connection:
    -   The current actor has an owner.
    -   The current actor is set to use its owner’s net relevancy.
-   If the following conditions hold, then the current actor is not relevant for this connection:
    -   The current actor is only relevant to its owner.
    -   The current actor does not have an owner.
    -   The current actor’s owner is not relevant.
-   If the following condition holds, then the system uses the current actor’s base relevancy to determine whether it is relevant for this connection:
    -   The current actor is attached to the skeleton of another actor.
-   If the following conditions hold, then the current actor is not relevant for this connection:
    -   The current actor is hidden.
    -   The current actor does not have a root component or the root component does not have collision enabled.
        
        If the current actor has no root component, then `AActor::IsNetRelevantFor` logs a warning and asks if the actor should be always relevant.
        
-   If the following conditions hold, then the current actor is relevant for this connection:
    -   The Game Network Manager ([`AGameNetworkManager`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AGameNetworkManager)) is set to use distance-based relevancy.
    -   The current actor is within the relevancy distance.

This relevancy logic is for the base `AActor` class. Other `AActor`\-derived classes may contain different network relevancy logic. For example, the `APawn` and `APlayerController` classes override `AActor::IsNetRelevantFor`. Therefore, they have different conditions for relevancy. See `Pawn.cpp` and `PlayerController.cpp` for more information.

## Customize Relevancy Settings

You can customize network relevancy settings for your `AActor`\-derived class in the Replication section of the Unreal Editor Details Panel or in C++.

## Relevancy Reference

The following tables provide functions and properties pertaining to actor relevancy that can be found in the `AActor` class:

### Functions

| **Name** | **Description** |
| --- | --- |
| [`ForceNetRelevant`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/ForceNetRelevant) | Force this actor to be network relevant if it is not already relevant by default. |
| [`IsNetRelevantFor`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/IsNetRelevantFor) | Check if this actor is relevant for a specific network connection. |
| [`IsRelevancyOwnerFor`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/IsRelevancyOwnerFor) | Check if this actor is the owner when performing network relevancy checks for actors marked `bOnlyRelevantToOwner`. |
| [`IsReplayRelevantFor`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/IsRelevancyOwnerFor) | Check if this actor is relevant for recorded replay. |
| [`IsWithinNetRelevancyDistance`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/IsWithinNetRelevancyDistance) | Check if the square of the distance between the given source location and this actor’s location is within `NetCullDistanceSquared`. |

### Properties

| **Name** | **Description** |
| --- | --- |
| [`bAlwaysRelevant`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor) | Always relevant for network replication. Overrides `bOnlyRelevantToOwner`. |
| [`bNetUseOwnerRelevancy`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor) | If this actor has a valid owner, call the owner's `IsNetRelevantFor` and `GetNetPriority`. |
| [`bOnlyRelevantToOwner`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor/bOnlyRelevantToOwner) | If true, this actor is only relevant to its owner. |
| [`bRelevantForNetworkReplays`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor) | If true, this actor is replicated to network replays. Default true. |
| [`NetCullDistanceSquared`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor) | Square of the maximum distance from the client’s viewport that this actor is relevant and replicates. |
| [`Owner`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/AActor) | Owner of this actor. Used for replication with `bNetUseOwnerRelevancy` and `bOnlyRelevantToOwner`. |