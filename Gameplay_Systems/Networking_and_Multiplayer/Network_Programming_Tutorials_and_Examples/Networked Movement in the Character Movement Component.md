# Networked Movement in the Character Movement Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-networked-movement-in-the-character-movement-component-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-networked-movement-in-the-character-movement-component-for-unreal-engine)  
**Processed:** 2025-06-14 16:55:43

---

The **Character Movement Component** is an **Actor Component** that provides an encapsulated movement system with common modes of movement for humanoid **characters**, including walking, falling, swimming, and flying. The character movement component also features robust network gameplay integration. Its default movement modes are all built to replicate by default, and it provides a framework to help developers create custom networked movement.

## Basics of Character Movement

[`UCharacterMovementComponent`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/UCharacterMovementComponent) comes preattached to the [`ACharacter`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/ACharacter) Actor class and any **Blueprints** derived from it.

During its `TickComponent` function, `UCharacterMovementComponent` will call `PerformMovement` to calculate desired acceleration within the world based on what **movement mode** it is currently using as well as the player's input variables, commonly represented with the *control input* variables in [`APlayerController`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/APlayerController) . Once movement calculations are finalized, `UCharacterMovementComponent` applies the final movement to the owning character.

While `ACharacter` is derived from [`APawn`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/APawn), Characters are not simply Pawns that have a character movement component added to them. `UCharacterMovementComponent` and `ACharacter` are designed to be used together, as `ACharacter` overrides several replicated variables and functions specifically to facilitate replication in `UCharacterMovementComponent`.

### PerformMovement and Movement Physics

The `PerformMovement` function is responsible for physically moving the character in the game's world. In a non-networked game, `UCharacterMovementComponent` calls `PerformMovement` directly each tick. In a network game, `PerformMovement` is called by specialized functions for servers and clients to either perform the initial movement on a player's local machine or reproduce that movement on remote machines.

`PerformMovement` handles the following:

-   Applies external physics, like impulses, forces, and gravity.
-   Calculates movement from animation root motion and ***root motion sources***.
-   Calls `StartNewPhysics`, which selects a `Phys*` function based on what movement mode the character is using.

Each movement mode has its own `Phys*` function that is responsible for calculating velocity and acceleration. For example, `PhysWalking` determines the character's movement physics when moving on the ground, while `PhysFalling` determines how it behaves in the air. If you wanted to debug the specifics of these behaviors, you would look inside each of these functions.

If a movement mode changes during a tick, such as when a character starts falling or collides with an object, the `Phys*` functions call `StartNewPhysics` again to continue the character's motion in the new movement mode. `StartNewPhysics` and the `Phys*` functions each pass through the number of iterations of `StartNewPhysics` that have occurred. The parameter `MaxSimulationIterations` is the maximum number of times this recursion is allowed.

## Movement Replication Summary

`UCharacterMovementComponent` uses its owner's **network role** to determine how to replicate movement. The three network roles are as follows:

| Network Role | Description |
| --- | --- |
| **Autonomous Proxy** | The character is on its *owning client's* machine, being controlled locally by a player. |
| **Authority** | The character exists on the server hosting the game. |
| **Simulated Proxy** | The character exists on any other client that can see the remotely-controlled character, whether it's being controlled by an AI on the server or by an autonomous proxy on a different client. |

The replication process follows a cycle within the `TickComponent` function, which repeats itself on every tick. As the character performs movement, copies of it on all the different machines in the network game make ***Remote Procedure Calls (RPCs)*** to each other to synchronize movement information, with different network roles using different execution paths as appropriate.

The table below provides a step-by-step overview of what `UCharacterMovementComponent` does on each machine during this process:

| Step | Description |
| --- | --- |
| Autonomous Proxy (Owning Player's Client) |   |
| **1** | The owning client controls the autonomous proxy locally. `PerformMovement` runs the physical movement logic of the movement component. |
| **2** | The proxy builds an `FSavedMove_Character` containing data about how it just moved, then queues it in `SavedMoves`. |
| **3** | Similar `FSavedMove` entries are combined together. The autonomous proxy sends a condensed version of their data to the server with a ***ServerMove*** RPC. |
| Authoritative Actor (Server) |   |
| **4** | The server receives the ServerMove and reproduces the client's movement using `PerformMovement`. |
| **5** | The server checks to see if its position after the ServerMove matches the client's reported end location. |
| **6** | If the server and client's final positions match, it sends a signal back to the client saying the move was valid. Otherwise, it sends a correction with a ***ClientAdjustPosition*** RPC. |
| **7** | The server sends its location, rotation, and current state to the simulated proxies on the other connected clients by replicating the `ReplicatedMovement` structure. |
| Autonomous Proxy (Owning Player's Client) |   |
| **8** | If the client receives a ClientAdjustPosition, it reproduces the server's movement and uses its `SavedMoves` queue to re-trace its steps to get a new final position. When the move is successfully resolved, it removes the saved move from the queue. |
| Simulated Proxy (All Other Clients) |   |
| **9** | The simulated proxies directly apply replicated movement information. ***Network smoothing*** provides visual cleanup for the final motion. |

This process synchronizes movement between all three types of machines within a network game. The user controlling a given character should experience minimal interference from the server and maintain the illusion that they are controlling their character locally, and they should see other users' characters performing an approximation of the movement that they are all performing on their own machines.

Most of this process's complexity focuses on mediating predictions and corrections between the autonomous proxy and its counterpart on the server to make sure that players have the smoothest experience possible in controlling their own characters. Simulated proxies, by comparison, only need to stay up to date where the server says they should be.

## Replicated Character Movement In-Depth

The following sections provide a detailed step-by-step walkthrough of the process briefly outlined above. Although a majority of projects are not expected to override `UCharacterMovementComponent`'s behavior, this will serve as a reference in case you need to develop similar functionality or need to find where to make modifications.

This section focuses on replicating a character's normal movement modes. However, there are alternate execution paths for root motion and moving while based on another Actor, which follow similar steps to those listed in this section.

### Local Movement on the Owning Client

Autonomous proxies process movement locally in `TickComponent`, record it, then send it to the server to be reproduced and applied authoritatively. This section will break down the process that an autonomous proxy goes through on each tick.

#### Building Client Prediction Data

Autonomous proxies build an `FNetworkPredictionData_Client_Character` object called `ClientPredictionData` as part of their process for both recording moves and processing corrections from the server. Its parameters include:

-   Timestamps from when the client communicates with the server
-   Lists of saved or pending moves
-   Saved information from server corrections
-   Flags denoting how to apply corrections
-   Parameters determining smoothing behavior

`ClientPredictionData` also includes utility functions that interact with these parameters. You can find a full list of this object's information and functions in the [API reference for `FNetworkPredictionData_Client_Character`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/FNetworkPredictionData_Client_Ch-). Its parameters are referenced and changed frequently as the client performs local movement, prepares moves to send to the server, and processes corrections.

#### Reproducing Server Corrections

Before the player's input or forces within the world are processed, the autonomous proxy calls `ClientUpdatePositionAfterServerUpdate`. This checks to see if the server has sent any corrections to the owning player. If it has, the variable `bUpdatePosition` inside `ClientPredictionData` will be true, and the character reproduces any moves sent from the server through the client correction process. For more information about server corrections, refer to the section below on Handling Client Error and Corrections.

#### Performing and Recording Movement

Autonomous proxy characters call `ReplicateMoveToServer` during `TickComponent` instead of calling `PerformMovement` directly. This function surrounds `PerformMovement` with the necessary logic to record movement as the character performs it, then submits the move to the server. The `FSavedMove_Character` structure is a record of how the autonomous proxy started and ended its move during each tick, after which a minimum subset of its data is sent to the server through a ServerMove RPC. Its parameters include:

-   Information about the character's final position and rotation
-   What movement inputs were captured
-   What velocity and acceleration the character held
-   Root motion information captured from **AnimMontages**

You can review a full list of this structure's parameters in the [API reference for `FSavedMove_Character`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/FSavedMove_Character). This information enables the server to reproduce the movement that the player performed, then check against the final position of the client.

After processing `PerformMovement`, the `ReplicateMoveToServer` function records the results of a character's movement in the client prediction data with an `FSavedMove_Character` structure called `NewMove`, which is then added to a buffer called `SavedMoves`. This buffer is ordered from the oldest saved move to the newest and acts as a queue until a saved move can be submitted to the server. Any similar moves in the buffer are combined together into a single `FSavedMove_Character` before being submitted to ease the strain on bandwidth. The parameter `PendingMove` acts as storage for moves that are waiting to be combined with an upcoming movement.

These will be removed from the buffer when they are acknowledged, or *ACKed*. The server can ACK a move directly by confirming that the client's position is valid, or the client can ACK a move when it processes a correction from the server. The last move to be ACKed is saved in `LastAckedMove` for use in processing future corrections.

#### Submitting Moves to the Server

`ReplicateMoveToServer` finishes by running the function `CallServerMove`, which takes in the newest move and the oldest move in the queue that has not yet been ACKed by the server. This runs the final preparations for submitting a move to the server, attempts to submit the old move first (if applicable), then calls an appropriate ServerMove function to submit the finalized movement for the new move. The final ServerMove is submitted directly to the owning character of the `UCharacterMovementComponent` as an *unreliable* server RPC.

There are two reasons that ServerMove functions are unreliable:

1.  During normal gameplay, ServerMove functions are called often enough that if they were designated as reliable, they could overflow the buffer for reliable functions, forcing the owning player to disconnect.
2.  The system for buffering saved moves already ensures that movement information lost in transit will be resubmitted and evaluated. This provides a similar safety net to a reliable function, but without the risk of overflowing the reliable RPC buffer, and with added provisions to make sure movement data that is too old gets discarded.

### Evaluating Movement on the Server

The server does not regularly tick movement in sync with the game's tick cycle. Instead, it waits to receive ServerMove calls from autonomous proxies, and `ServerMove_Implementation` handles movement on the server-side, reconstructing the client's movement and checking for discrepancies. This section will provide a walkthrough of the process that a ServerMove performs in detail.

This document broadly refers to `ServerMove` and `ServerMove_Implementation`, but there are multiple types of ServerMove calls depending on what kind of information is queued.

#### Building Server Prediction Data

The authority version of a character movement component creates an `FNetworkPredictionData_Server_Character` object called `ServerPredictionData`, which exists for the lifetime of the character. During `ServerMove_Implementation` this object will store information to be used by later processes to reproduce the owning client's movement. This object is continually modified in the background as the server receives data, and its parameters include:

-   Timestamps used to calculate the server's delta time
-   Pending client adjustments
-   Flags related to resolving time discrepancies
-   Flags denoting whether the server ACKs or corrects a move

You can read its full list of parameters and functions in the [API reference guide for `FNetworkPredictionData_Server_Character`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/FNetworkPredictionData_Server_Ch-).

#### Verifying Client Timestamp

The information sent with a ServerMove RPC includes a timestamp for when the move occurred. If the server's timestamp and the client's timestamp have too large of a discrepancy, the client's timestamp is considered expired and the move is discarded. Otherwise, the discrepancy is flagged to be resolved, and `UCharacterMovementComponent` uses `ProcessClientTimeStampForTimeDiscrepancy` to create an override for the delta time in the next step.

#### Calculating Delta Time

While delta time is usually obtained by keeping track of the time that has passed between the current tick and the previous tick, characters on the server do not use `TickComponent` to calculate movement. Instead, `ServerMove_Implementation` calls `GetServerMoveDeltaTime` and calculates movement as ServerMoves are received. If the server prediction data is flagged as trying to resolve a timestamp discrepancy, it will use `TimeDiscrepancyResolutionMoveDeltaOverride`. If there is no time discrepancy, it uses the server prediction data to create a delta time using the difference between the current ServerMove RPC's timestamp and the last ServerMove RPC's timestamp. To provide an extra layer of security, the majority of these calculations are performed with the server's timestamps instead of the client's, preventing clients from hacking their speed by speeding up their local game clock.

#### Evaluating the Move

The server next uses the data from the ServerMove RPC to reconstruct the owning player controller's control rotation, then calls the function `MoveAutonomous` to process the character's acceleration, rotation, and jump inputs.

`MoveAutonomous` uses the `PerformMovement` function to simulate the character's movement physics using this reconstructed data and the delta time supplied in the previous step. Instead of simulating movement from where the client started, the server simulates from the location where its own copy of the character was when it got the ServerMove call.

If the character is performing root motion from an animation, MoveAutonomous also ticks the character's animation pose using the supplied delta time. Any animation events will trigger appropriately. Otherwise, animation ticks normally.

### Handling Client Error and Corrections

Server movement works from the assumption that the server and owning client are both starting their movement in the same locations, and that if the server performs the same moves that the client reports, the locations that they end their moves in will also be the same. If the client's moves get dropped due to connection problems or if the client submits bad data, however, the two will end in different locations, necessitating a correction. The function `ServerMoveHandleClientError` is responsible for these operations.

#### Determining if Adjustments Are Necessary

Issuing corrections frequently would strain bandwidth and cause the client to re-simulate a large number of saved moves too often, so we first check against the value returned from `WithinUpdateDelayBounds` to see if a minimum amount of time has passed between moves. If it returns `false`, then no corrections will be issued. If it returns true, then the rest of the process is permitted to run.

Next, we use `ServerCheckClientError` to see if the error between server and client is large enough to be worth correcting. If it returns true, or if something sets `bForceClientUpdate` to true to force a correction, then `ServerMoveHandleClientError` continues with the rest of the process.

The parameters for adjusting both these operations can be found in `BaseGame.ini`, and you can provide project-specific overrides in the `DefaultGame.ini` for your project. The value `ClientErrorUpdateRateLimit` determines the minimum delay in seconds for the server sending error corrections to a client. The value `MAXPOSITIONERRORSQUARED` is the square of the max position error that is accepted in network play without being corrected. Both of these can be found under the `[/Script/Engine.GameNetworkManager]` section of the config file.

If an adjustment is necessary, the server prediction data fills an **[`FClientAdjustment`](/documentation/en-us/unreal-engine/API/Runtime/Engine/GameFramework/FClientAdjustment)** structure called `PendingAdjustment` with current movement variables sampled from the server's copy of the character, including location, rotation, velocity, and any objects that might be acting as a base for the character's movement. Otherwise, we set `PendingAdjustment`'s `bAckGoodMove` value to `true` to flag the client's movement as being valid.

#### Sending Client Adjustments or ACKing Moves

The final call for acknowledging movement to the client is made with `SendClientAdjustment`. This function does not occur as part of `ServerMove_Implementation`. Rather, this is part of `UNetDriver::ServerReplicateActors`, which is called at the end of a tick on the server and is similarly responsible for calling other client adjustment RPCs. When `SendClientAdjustment` is called, it will act depending on how the prediction data we built in the previous steps is flagged.

If the server prediction data's `PendingAdjustment` is flagged with `bAckGoodMove` as `true`, it will call the `ClientAckGoodMove` RPC to ACK the move, telling the autonomous proxy on the owning client's machine that the move was valid. This will remove the original move from the `SavedMoves` buffer on the owning client's side and record it as the `LastAckedMove` for use in building future prediction data.

If the `PendingAdjustment` has `bAckGoodMove` flagged as false, it will call client adjustment functions to send the final corrections to the client.

#### Receiving Client Adjustments on Autonomous Proxies

The client adjustment RPCs include `ClientAdjustPosition`, `ClientAdjustRotation`, shortened versions of them that occur when velocity is zero, and versions of them specially used for root motion-based movement. The server may call more than one of these as part of `SendClientAdjustment`, depending on the nature and severity of what needs to be corrected. Each of these is capable of telling `ClientPredictionData` to ACK moves once the necessary corrections are applied, and each of them will flag `bUpdatePosition` to true.

The final corrections are then applied at the beginning of the client's next `TickComponent` using `ClientUpdatePosition`.

### Replicating Movement to Simulated Proxies

Characters on client machines other than their owners are simulated proxies instead of autonomous proxies. The process for replicating movement from the server to simulated proxies is highly simplified, as simulated proxies' only job is responding to the server. Instead of simulating movement physics, when they receive movement updates from the server, they set their location, rotation, and velocity to whatever the server says they should be, with a few additional processes to make their movement smoother and more believable.

#### Storing Replicated Movement Information

When Actors replicate movement, they do not replicate their transforms directly. Instead, all Actors maintain a replicated variable called `ReplicatedMovement`, which uses the structure [`FRepMovement`](/documentation/en-us/unreal-engine/API/Runtime/Engine/Engine/FRepMovement).

The boolean `bReplicateMovement`, represented by the **Replicate Movement** variable in Blueprint, flags Actors to store movement information in this structure and replicate it to clients. When a client receives updates to `ReplicatedMovement`, the **RepNotify** function `OnRep_ReplicatedMovement` unpacks the stored movement data and performs updates to the Actor's location and velocity accordingly.

Neither `ReplicatedMovement` or its OnRep are accessible inside of Blueprint, but `OnRep_ReplicatedMovement` can be overridden in C++, and `ReplicatedMovement`'s replication conditions can also be overridden in `GetLifetimeReplicatedProps`. This enables you to customize how movement replication behaves in C++ based Actor classes.

In `ACharacter`, the `ReplicatedMovement` structure is only replicated for simulated proxies. It will be ignored on autonomous proxies, who otherwise use the server move and client adjustment RPCs to process movement.

If a character is using another Actor as a base, it will use `ReplicatedBasedMovement` instead, which applies additional logic to make sure the client is based correctly according to the server. If the character uses the root motion system, all of these processes are ignored in favor of using `RepRootMotion`.

#### Ticking Movement on Simulated Proxies

When `UCharacterMovementComponent` runs `TickComponent` on a simulated proxy, it calls `SimulatedTick` to handle the logic for simulating movement. This does not perform the replicated movement outlined above. Instead, `SimulatedTick` continues moving in accordance with the most recently provided replicated movement data. When performing standard movement physics, it calls the `SimulateMovement` function, then performs final validations and network smoothing with `SmoothClientPosition`.

#### Performing Simulated Movement

The `SimulateMovement` function is responsible for moving simulated proxy characters. In addition to being called by `SimulatedTick`, it is also called by `OnRep_ReplicateMovement`. This function performs the following processes:

1.  Calls the owning character's `GetReplicatedMovement` function to obtain a reference to `ReplicatedMovement`.
2.  Performs safety checks to ensure that replicated movement data is valid and that the client's base is resolved.
3.  Checks to see if any network updates have been received.
4.  Applies the character movement mode from the server, obtained with `GetReplicatedMovementMode`.
5.  Resets all flags regarding network updates.
6.  Performs the logic for simulated moves based on the current `MovementMode` and information about the character's current state.

The logic for simulated moves is highly simplified compared with standard movement physics, such that it is mostly contained in the `SimulateMovement` function itself rather than broken into smaller functions. However, this function is still responsible for updating the character's local movement state, including what movement mode it should transition into, whether or not the character has landed on the ground, and what velocity it should have. This information ensures that the character can update its animation correctly and that its movements appear reasonably accurate.

#### Network Smoothing

If we replicated movement by simply replicating the Location and Rotation of a character, then the character would seem to teleport every few moments. This is due to the rendering rate for a local machine being faster than the rate that we would want to send data over a network. A client may be rendering to a monitor with a 240 Hz refresh rate, for instance, but the replicated movement may be sent at only 30 Hz.

Network smoothing is a process that smooths out this motion, interpolating the character gradually from the source location towards a target location instead of snapping it to the target instantly. The source location is given by the character's current position, while the target is given by the client prediction data. The interpolation itself is handled in `SmoothClientPosition`, which uses [`NetworkSmoothingMode`](/documentation/en-us/unreal-engine/API/Runtime/Engine/Engine/ENetworkSmoothingMode) to determine what kind of interpolation it should use.

## Special Movement Cases

The following sections contain information on common special movement cases, including teleportation, custom movement, and code-driven movement as you might see in special abilities.

### Teleporting a Character in Multiplayer

You can teleport a character in a network game by calling any of the **SetLocation** functions or the **Teleport** Blueprint node, provided you:

1.  Make sure they are called on the server.
2.  If using the `SetLocation` functions, set the `bTeleport` variable to true so it recognizes the move as a teleport.

![Teleporting a Character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e95d0097-45fe-4bc7-8f20-7170c0d4791e/charactermovement_teleport.png)

If these conditions are satisfied, the movement is recorded in the server's prediction data and in replicated movement as a teleport, and all clients respond accordingly by snapping the character to the desired location instead of applying smoothing.

### Using Custom Movement Modes

The movement mode `MOVE_Custom` suspends all other movement physics, enabling you to implement custom movement logic without interference from `UCharacterMovementComponent`'s normal processes.

`UCharacterMovementComponent` is not normally Blueprintable, so custom movement in Blueprint is usually implemented directly inside Character using the **UpdateCustomMovement** event. You can use the **Custom Movement Mode** byte variable to provide sub-modes, either with a switch on integer or with a conversion to a custom enum.

![Custom Movement Mode in Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69309a64-3371-4557-bada-0fc68c6d6768/charactermovement_custommovementmodebp.png)

`UpdateCustomMovement` is called by the `PhysCustom` function in `UCharacterMovementComponent`. The functions `StartNewPhysics`, `PhysCustom`, and all the other movement physics functions are virtual functions, so if you create a custom `UCharacterMovementComponent` in C++, you can override them directly.

### Replicating Special Case Movement with Root Motion

You may need to take direct control of a character's movement for brief periods, such as during abilities created with the **Gameplay Ability System** or during animation-driven actions. While this is simple to do in a local-only game, replicated special case movement requires the use of root motion, which generally refers to the application of movement from an animation. The root motion system has also been adapted to permit code-driven special case movement.

Root motion always takes precedence over standard movement physics, regardless of what movement mode the `UCharacterMovementComponent` is using. When your root motion is finished, normal movement will resume.

#### From AnimMontages

Most applications of root motion are expected to come from AnimMontages, which are used for code-triggered one-shot animations. This use of root motion suspends any other movement that your character is performing until the end of the animation. The character instead consumes movement from its skeleton's root bone and translates it into world-space movement, enabling the animation to control how the character moves. When this completes, the use of normal physics for the character is restored.

If your character is in the falling movement mode, gravity is still applied to the character's Z movement even when the character is performing root motion.

Within the replication process outlined above, root motion information is captured by the `FSavedMove_Character` structure, including the AnimMontage it comes from, the character's track position within the montage, and parameters for the character's movement itself.

The server and the autonomous proxy on the owning client do not check to see that they are playing the same animation, as this is normally considered a cosmetic feature. Therefore, you must program your gameplay logic to ensure that any AnimMontages are triggered correctly on all machines connected to a game. However, simulated proxies have parallel processes to the ones outlined above for synching root motion-based movement.

The Gameplay Ability System plugin synchronizes AnimMontages and root motion by replicating the ability that triggers them.

#### From Root Motion Sources

Sometimes you may need to control a character's location manually for special cases. For example, you might need to create a special ability where a character leaps a specific height into the air, then lands on a moving target.

Manually controlling the character with `SetLocation` and `SetRotation` is possible on standalone games, but in network games, this motion is not captured by the above replication process, so the server will see the client's final location as an error and issue a correction. Root motion from AnimMontages, meanwhile, follows only pre-computed motion from animations. This means that root motion can not normally take in real-time information from the game's world, such as the position of other characters, and it also can not be easily fine-tuned using gameplay variables.

**Root motion sources** provide a means for programmers to manually take control of a character's root motion. This enables you to control a character's movement programmatically while also taking advantage of the above system for handling root motion during networking.

Root motion sources should be applied to autonomous proxies on the owning client.

To use this system, you must create a new FRootMotionSource structure. Different FRootMotionSource variants exist for different kinds of movement. For instance, FRootMotionSource\_MoveToForce is used for a straightforward move from a starting location to a target location, while FRootMotionSource\_JumpForce follows a jump-like arc. Once you have created an appropriate root motion source, you can initialize its properties with the desired source location, target location, and parameters for how its movement should behave.

The function `UCharacterMovementComponent::ApplyRootMotionSource` will apply the root motion source to the character and return a handle that can be used to reference it later. The root motion sources themselves do not process movement. Instead, the character movement component performs movement consistent with the parameters in the provided `FRootMotionSource` in place of an animation. This is eventually added to `SavedRootMotion` within the `FSavedMove_Character` structure, capturing it in the replication cycle provided that the `FRootMotionSource` is applied to an autonomous proxy.

When the movement is completed, you must call `UCharacterMovementComponent::RemoveRootMotionSource` to remove it using the handle returned from `ApplyRootMotionSource`.

The Gameplay Ability System plugin contains several ability tasks that utilize root motion sources, enabling abilities to perform complex sequences of programmatic movement. You can refer to `AbilityTask_ApplyRootMotionMoveToForce` for a basic example.

## Customizing Networked Character Movement

Unreal Engine enables replicated Character movement support of custom function parameters. Developers who do not require this functionality and want to maintain the legacy API can define `SUPPORT_DEPRECATED_CHARACTER_MOVEMENT_RPCS` to a non-zero value in the project build files, and set the Console Variable "p.NetUsePackedMovementRPCs" to zero.

The Character Movement Component sends data across the network using an `FSavedMove_Character` struct. The system consolidates move data from one or more updates into a single variable-length bit stream for transmission across the network. By packaging old and new data together, this method avoids potential ordering issues involving `ServerMoveOld` RPCs being called after `ServerMove`, which could cause old (but still important) data to be incorrectly disregarded as obsolete. Internally, the Character Movement Component uses the new `CallServerMovePacked` function to serialize multiple `FSavedMove_Character` instances into an `FCharacterNetworkMoveDataContainer`, replacing the old usage of `CallServerMove`.

### Extending Saved Move Data

To add new data, first extend `FSavedMove_Character` to include whatever information your Character Movement Component needs. Next, extend `FCharacterNetworkMoveData` and add the custom data you want to send across the network; in most cases, this mirrors the data added to `FSavedMove_Character`. You will also need to extend `FCharacterNetworkMoveDataContainer` so that it can serialize your `FCharacterNetworkMoveData` for network transmission, and deserialize it upon receipt. When this setup is finised, configure the system as follows:

-   Modify your Character Movement Component to use the `FCharacterNetworkMoveDataContainer` subclass you created with the `SetNetworkMoveDataContainer` function. The simplest way to accomplish this is to add an instance of your `FCharacterNetworkMoveDataContainer` to your Character Movement Component child class, and call `SetNetworkMoveDataContainer` from the constructor.
    
-   Since your `FCharacterNetworkMoveDataContainer` needs its own instances of `FCharacterNetworkMoveData`, point it (typically in the constructor) to instances of your `FCharacterNetworkMoveData` subclass. See the base constructor for more details and an example.
    
-   In your extended version of `FCharacterNetworkMoveData`, override the `ClientFillNetworkMoveData` function to copy or compute data from the saved move. Override the `Serialize` function to read and write your data using an `FArchive`; this is the bit stream that RPCs require.
    

To extend the server response to clients, which can acknowledges a good move or send correction data, extend `FCharacterMoveResponseData`, `FCharacterMoveResponseDataContainer`, and override your Character Movement Component's version of the `SetMoveResponseDataContainer`.

### Accessing Extended Move Data

To maintain backwards compatibility, there have been no changes to the function stack for working with client moves on the server and replaying them on the client after receiving a correction. While this provides a stable API for the legacy functions, it also means that those function signatures do not accomodate the new movement data. You can access this data on the server while processing a move, or on a client while replaying one, by calling `GetCurrentMoveData` and casting the returned `FCharacterNetworkMoveData` to your subclass.