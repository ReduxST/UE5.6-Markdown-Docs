# Networking Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine)  
**Processed:** 2025-06-14 16:38:37

---

In multiplayer game sessions, game state information is communicated between multiple machines over a network connection. In contrast, single-player, local games store all game state information on a single machine. Communication over a network connection makes creating multiplayer experiences inherently more complex than single-player experiences. The process of sharing information between players involves a different approach than a single-player game. **Unreal Engine (UE)** features a robust networking framework that powers some of the world's most popular online multiplayer games to help you streamline this process. This page provides an overview of the concepts that drive multiplayer programming and guides you to additional documentation about UE's tools for building multiplayer experiences.

## Plan Early for Multiplayer

If there is any possibility that your project might need multiplayer features at any time, you should build all of your gameplay with multiplayer in mind from the start of your project. If your team consistently implements the extra steps for creating multiplayer, the process of building gameplay will not consume much more time compared to a single-player game. In the long run, your project will be easier for your team to debug and service. Meanwhile, any gameplay programmed for multiplayer in UE will still work as expected in single-player, non-networked play.

If you do not design your project with multiplayer in mind from the beginning, refactoring a codebase that you have already built without networking will require you to comb through your entire project and rewrite large sections of gameplay functionality. You also might need to reconsider your design since technical obstacles in networking such as network speed and stability may force you to change your existing design.

## Unreal Engine Networking Architecture

UE uses the **client-server architecture** for networked multiplayer games. There are two types of multiplayer games: local multiplayer and networked multiplayer. In a single-player or local multiplayer game, your game runs locally on a single machine as a standalone game. In this instance, all players, assets, and functionality exists and all input is processed on a single machine. Players connect input to this machine and control everything directly in the game. There is no potential issue with communicating input from a player to the game because the player is connected directly to the game instance and the game instance can promptly process all input.

![Local Multiplayer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca5397ee-a048-4787-8ff6-2f5f75b30a30/localplayexample.png)

Single-player and local multiplayer take place on only one machine.

In a networked multiplayer game, many players on distinct machines connect to a central machine across a network. The central machine, known as the **server**, hosts the multiplayer game while all the other players on different machines connect to the server as **clients**. The server shares game state information with each connected client and provides the means for all the players on different machines to communicate with one another.

![Networked Multiplayer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3bb0f45-1aab-41d6-b726-a43a53b707f4/networkplayexample.png)

In networked multiplayer, the game takes place between a server and several connected clients. The server processes gameplay and the clients render the game to users.

As opposed to local multiplayer, this presents additional challenges. Different clients might have different network connection speeds and information must be communicated across a potentially unstable network where input might get lost. As a result, at any given time, the state of the game on one client machine is likely to be different than every other client machine. The server, as the host of the game, holds the one, true, **authoritative** game state. In other words, the server is where the multiplayer game is actually played. The clients each control remote **Pawns** that they own on the server. Clients send *remote procedure calls* from their local pawn to their server pawn to perform in-game actions. The server then *replicates* information about the game state to each client such as where **Actors** are located, how these actors should behave, and what values different variables should have. Each client then uses this information to simulate a close approximation of what is actually happening on the server.

By default, the server does not stream visuals directly to client monitors to display, the server sends state information to client game instances so the client machines can re-create the visuals inside their own game instances. Unreal Engine provides the **Pixel Streaming** system to pre-render frames and audio for display on mobile and web browsers. For more information, see the [Pixel Streaming](/documentation/en-us/unreal-engine/pixel-streaming-in-unreal-engine) documentation.

### Client-Server Gameplay Example

This section provides a side-by-side comparison of two players in a multiplayer game to illustrate the differences between local and networked multiplayer. On the left, the two players are playing local multiplayer. On the right, the two players are playing networked multiplayer.

| **Local Multiplayer** | **Networked Multiplayer** |
| --- | --- |
| 
![Local Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/169bdea2-2b05-457b-adb3-c90a49c40c9d/localmultiplayerexample.png)

 | 

![Client Server Network Play](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2b10de3-e7b9-4b3e-a877-a6c289d6ee32/clientserverexample.png)

 |
| 

**Player 1 presses an input to fire a weapon.**

-   Player 1's Pawn responds to this by firing its current weapon.
-   Player 1's weapon spawns a projectile and plays any accompanying sound or visual effects.



 | 

**Player 1 presses an input on their local machine to fire a weapon.**

-   Player 1's local Pawn relays the command to fire the weapon to its connected Pawn on the server.
-   Player 1's weapon on the server spawns a projectile.
-   The server notifies each connected client to create its own copy of Player 1's projectile.
-   Player 1's weapon on the server notifies each client to play the sound and visual effects associated with firing the weapon.



 |
| 

**Player 1's projectile moves forward from the weapon.**



 | 

**Player 1's projectile on the server moves forward from the weapon.**

-   The server notifies each client to replicate the movement of Player 1's projectile as it happens, so each client's version of Player 1's projectile also moves.



 |
| 

**Player 1's projectile collides with Player 2's pawn.**

-   The collision triggers a function that destroys Player 1's projectile, causes damage to Player 2's pawn, and plays any accompanying sound and visual effects.
-   Player 2 plays an on-screen effect as a response to being damaged.



 | 

**Player 1's projectile on the server collides with Player 2's pawn.**

-   The collision triggers a function that destroys Player 1's projectile on the server.
-   The server automatically notifies each client to destroy their copy of Player 1's projectile.
-   The collision triggers a function that notifies all clients to play the accompanying sound and visual effects for the collision.
-   Player 2's pawn on the server takes damage from the projectile collision.
-   Player 2's pawn on the server notifies Player 2's client to play an on-screen effect as a response to being damaged.



 |

In the local multiplayer game, these interactions all take place in the same world on the same machine, so they are simpler to understand and program compared to the networked multiplayer game. For example, when the game spawns an object, you can be assured that all players can see the object since they all exist in the same game world.

In the networked multiplayer game, these interactions take place in several different worlds:

-   Authoritative world on the server.
-   Player 1's client world.
-   Player 2's client world.
-   Additional worlds for any other clients connected to this server game instance.

Each world has its own player controllers, pawns, weapons, and projectiles. The server is where the game is actually played, but each client's world must accurately replicate the events happening on the server, therefore it is necessary to selectively send information to each client to create an accurate visual representation of the world on the server.

This process introduces a division between essential gameplay interactions (collisions, movement, damage), cosmetic effects (visual effects and sounds, and player information (HUD updates). Each of these is relevant to a specific machine or set of machines in the network. The process of replicating this information is not entirely automated and you must specify what information is replicated to which machines in your gameplay programming. The primary challenges involve choosing what information you should replicate to which connections to provide a consistent experience for all players, but also to minimize the amount of information that is replicated so network bandwidth is not constantly saturated.

## Fundamental Networking Concepts

This section details the concepts that drive network gameplay in UE and gives an overview of the tools UE provides to help you build your own networked multiplayer games.

### Network Modes

**Network mode** describes a machine's relationship to a networked multiplayer game session.

| **Network Mode** | `ENetMode` | **Description** |
| --- | --- | --- |
| **Standalone** | `NM_Standalone` | A game without networking with one or more local players. Still considered a server because it has all the server functionality, but does not accept connections from remote clients. This mode is used for single-player and local multiplayer games. This mode runs both server-side and client-side logic as appropriate. |
| **Dedicated Server** | `NM_DedicatedServer` | A server with no local players. Server accepts connections from remote clients only, so the server discards graphics, sound, input, and other player-oriented features to run more efficiently. This mode is often used for games that require more persistent, secure, or large-scale multiplayer. |
| **Listen Server** | `NM_ListenServer` | A server that also has a local player who is hosting the game. Available to other players on the network. This mode is often used for casual cooperative and competitive multiplayer. |
| **Client** | `NM_Client` | Client connected to a remote server. Client is connected to either a listen or dedicated server in a network multiplayer session. Client does not run any server-side logic. |

Because standalone games serve as both a server and a client, any logic created for a multiplayer game functions in single-player standalone network mode with no additional work.

To determine the network mode of your game instance, use `GetNetMode`. UE also provides preprocessor defines to help you choose which code should be compiled and which should not depending on whether you are compiling a game, server, or client target:

| **Target** | `UE_SERVER` | `WITH_SERVER_CODE` |
| --- | --- | --- |
| **Game** | 0 | 1 |
| **Server** | 1 | 1 |
| **Client** | 0 | 0 |

For more information about UE targets, see the [Targets](/documentation/en-us/unreal-engine/unreal-engine-build-tool-target-reference) documentation.

#### Server Types

##### Listen Server

**Listen servers** are designed to be simple for users to set up spontaneously since any user with a copy of the game can both start a listen server and play on the same machine. Games that support listen servers often feature an in-game user interface (UI) for starting a server or searching for existing servers to join. Listen servers are not without disadvantages. Because the player who is hosting the listen server is playing on the server directly, they have an advantage over the players who are playing as clients on the listen server. This might raise concerns about fairness of the game. On the other hand, there is also an additional processing load associated with running as a server while also supporting player-relevant systems like graphics and audio rendering. These factors make listen servers less suitable for games in highly competitive settings or games with very high network loads, but convenient for casual cooperative and competitive multiplayer among small groups of players.

##### Dedicated Server

**Dedicated servers** are more expensive and challenging to configure. They require a separate machine from all the other players participating in the game, complete with its own network connection. All players joining a dedicated server experience the game with a remote, network connection that ensures a better chance of fairness. Since a dedicated server does not render graphics or perform logic only relevant to local players, it is also able to process gameplay events and perform networking functions more efficiently. This makes dedicated servers preferable for games that require large numbers of players or high-performance, trusted servers for security, fairness, and reliability. Such games include Massively Multiplayer Online games (MMOs), competitive Multiplayer Online Battle Arena games (MOBAs), or fast-paced online shooters.

Network connection speeds and bandwidth affect a client's performance when connected to a server. There is no guarantee that all clients have the same network connection speed and it is more than likely they will not.

### Replication

**Replication** is the process of the authoritative server sending state data to connected clients. As previously mentioned, the true game state exists on the server. Connected clients *replicate* this state locally and render graphics and audio so a client can communicate with other clients and participate in the game. If replication is configured correctly, different machines' game instances synchronize and gameplay runs smoothly.

Actors and actor-derived classes are the primary classes designed for replicating their state over a network connection in UE. `AActor` is the base class for an object that can be placed or spawned in a level and is also the first class in UE's `UObject` inheritance hierarchy that is supported for networking. `UObject`\-derived classes can also replicate, but they must be attached to an actor as a replicated subobject to replicate properly.

Within the context of UE, there are two different areas that are relevant when talking about replication. First, there are the objects being replicated, flagging the properties requiring replication, and defining functions that are called over a network connection. Most of the information relevant to this can be found in the [Actor Replication](/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine#actorreplication) section. Second, there is the internal system itself that is responsible for the act of replicating objects to the correct machines. With respect to this second point, UE has a few different systems to replicate objects that can be found in the [Replication Systems](/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine#replicationsystems) section.

#### Actor Replication

Actors interact over a network using a few different mechanisms, some of these include: replicated properties, replicated using properties, and remote procedure calls. [Replicated Properties](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine#addareplicatedproperty) are actor properties that replicate their state over the network. [Replicated Using Properties](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine#addareplicatedusingproperty) are actor properties that replicate their state over the network and subsequently call a function to perform an action when their state is replicated. [Remote Procedure Calls](/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine) give actors the ability to call a function from one machine and run it on a different machine. For example, an actor can call a server remote procedure call on a client and the function will then run on the server once the server receives the network packet.

Actor replication is a highly detailed, multi-step process that involves a few primary steps:

-   Client machine determines what actors need to replicate to which connections.
    -   For more information, see the [Detailed Actor Replication Flow](/documentation/en-us/unreal-engine/detailed-actor-replication-flow-in-unreal-engine) documentation.
-   Server determines the order in which property updates and remote procedure calls are performed and executed.
    -   For more information, see the [Replicated Object Execution Order](/documentation/en-us/unreal-engine/replicated-object-execution-order-in-unreal-engine) documentation.
-   Server sends relevant information to all other connected clients.

By default, most actors do not replicate by default and instead perform their functions locally. You can enable replication for actor-derived classes by setting the `bReplicates` variable in C++ or the **Replicates** setting in Blueprint to `true`. For an overview of how to replicate actors and their properties, see the [Replicate Actor Properties](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine) documentation.

The following table provides an overview of the different replication features available:

| **Feature** | **Description** | **More Information** |
| --- | --- | --- |
| **Creation and Destruction** | When an authoritative version of a replicated actor is spawned on a server, it automatically generates remote proxies of itself on all connected clients. It will then replicate information to those remote proxies. If you destroy an authoritative actor, it will automatically destroy its remote proxies on all connected clients. | 
[Actor Owner and Owning Connection](/documentation/en-us/unreal-engine/actor-owner-and-owning-connection-in-unreal-engine) [Actor Role and Remote Role](/documentation/en-us/unreal-engine/actor-role-and-remote-role-in-unreal-engine)



 |
| **Movement** | If an authoritative actor has **Replicate Movement** enabled, or `bReplicateMovement` is set to `true` in C++, it will automatically replicate its Location, Rotation, and Velocity.. | [Networked Movement in the Character Movement Component](/documentation/en-us/unreal-engine/understanding-networked-movement-in-the-character-movement-component-for-unreal-engine) |
| **Properties** | Any properties that are designated as being replicated automatically replicate from the authoritative actor to its remote proxies whenever their values change. | [Replicate Actor Properties](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine) |
| **Components** | Actor components replicate as part of the actor that owns them if they are set to replicate. Any variables within the component that are designated as being replicated will replicate, and any RPCs called within the component will behave consistently with RPCs called in the actor class. |   |
| **Subobjects** | Any UObject-derived can be attached to an actor and replicated as a subobject. | [Replicated Subobjects](/documentation/en-us/unreal-engine/replicating-uobjects-in-unreal-engine) |
| **Remote Procedure Calls** | RPCs are special functions that are transmitted to specific machines in a network game. No matter what machine an RPC is initially called on, its implementation will run only on the machine it is intended for. These may be designated as Server (only runs on the server), Client (only runs on the Actor's owning client), or NetMulticast (runs on every machine connected to the session, including the server). | [Remote Procedure Calls](/documentation/en-us/unreal-engine/remote-procedure-calls-in-unreal-engine) |

Common use cases such as creation, destruction, and movement are handled automatically, but all other gameplay features do not replicate by default, even when you enable replication for an actor. You must manually designate:

-   Properties to replicate and any custom conditions.
-   Functions to replicate and manually call them in your code.
-   Components and subobjects to replicate and any of their associated properties and functions.

Several common features of actors, pawns, and characters do not replicate, such as:

-   Skeletal Mesh Component
-   Static Mesh Component
-   Materials
-   Animation Blueprints
-   Particle System Component
-   Sound Emitters
-   Physics Objects

Each of these run separately on all clients, however, if the variables that drive these visual elements are replicated, it ensures that all clients have the same information and each simulates these features in approximately the same manner.

### Debugging, Profiling, and Testing

The added complexity of multiple game instances, varying reliability of network connections, and differing functionality between a server and clients makes debugging, profiling, and testing networked multiplayer games an essential part of the development process. UE provides several features and specialized tools to help you debug, profile and test your project. For more information, see the [Network Debugging](/documentation/en-us/unreal-engine/network-debugging-for-unreal-engine) documentation section.

## Replication Systems

UE now provides three different systems to replicate state data over a network connection:

-   [Generic Replication System](/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine#genericreplicationsystem)
-   [Replication Graph](/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine#replicationgraph)
-   [Iris Replication System](/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine#irisreplicationsystem)

Before you start designing your networked multiplayer game, decide which replication system is best for you by reading more about each of them and what they offer.

### Generic Replication System

The generic replication system is the system that UE currently uses by default. This is the base replication system that supports replication of actors, their properties, and remote procedure calls. The majority of the documentation included in the [Networking and Multiplayer](/documentation/en-us/unreal-engine/networking-and-multiplayer-in-unreal-engine) documentation section is relevant to the generic replication system *except*:

-   [Replication Graph](/documentation/en-us/unreal-engine/replication-graph-in-unreal-engine)
-   [Iris Replication System](/documentation/en-us/unreal-engine/iris-replication-system-in-unreal-engine)

#### Key Features

| **Feature** | **Description** |
| --- | --- |
| [**Dormancy**](/documentation/en-us/unreal-engine/actor-network-dormancy-in-unreal-engine) | Control whether an actor is added to a connection's list of actors considered for replication. |
| [**Priority**](/documentation/en-us/unreal-engine/actor-priority-in-unreal-engine) | Control how important an actor is to replicate each frame if there is limited bandwidth. |
| [**Relevancy**](/documentation/en-us/unreal-engine/actor-relevancy-in-unreal-engine) | Control whether an actor is relevant to a particular connection. |

### Replication Graph

The replication graph plugin is a system for network replication designed to scale well with large numbers of replicated actors. For more information, see the [Replication Graph](/documentation/en-us/unreal-engine/replication-graph-in-unreal-engine) documentation.

### Iris Replication System

The Iris replication system is the newest addition to UE's networking features. Iris works alongside UE's generic replication system so existing actor replication and remote procedure calls work as they did before, but it also includes new features that replace some features from the generic system and aim to improve upon them.

For more information about Iris in general, see the [Iris Replication System](/documentation/en-us/unreal-engine/iris-replication-system-in-unreal-engine) documentation section. For more information about what is different between the generic replication system and Iris, see the [Migrate to Iris](/documentation/en-us/unreal-engine/migrate-to-iris-in-unreal-engine) documentation.

#### Key Features

| **Feature** | **Description** |
| --- | --- |
| [**Filtering**](/documentation/en-us/unreal-engine/iris-filtering-in-unreal-engine) | Control the connections to which an actor replicates, which replication groups an actor is a member, and dynamic replication filtering. |
| [**Prioritization**](/documentation/en-us/unreal-engine/iris-prioritization-in-unreal-engine) | Control how important an actor is to replicate each frame based on either static priority or a custom, dynamic priority. |

## Networking Tips

The following are summarized tips for networking in UE. You can find more information on the relevant documentation pages within this section.

-   Use as few RPCs and replicated Blueprint functions as possible. If you can use a Replicated Using (RepNotify) property instead, you should.
-   Use multicast functions sparingly as they create extra network traffic for each connected client.
-   Server-only logic does not necessarily have to be contained in a server RPC if you can guarantee that a non-replicated function only executes on the server.
-   Use caution when binding reliable RPCs to player input. Players can repeatedly press buttons rapidly and subsequently overflow the reliable RPC queue. If you do, you should create a mechanism for limiting how often a player can activate an RPC based on input.
-   Make RPCs unreliable if they are called especially often, such as inside an actor tick function.
-   Recycle functions as often as possible. Some functions can be recycled by calling them in response to gameplay logic and also as RepNotifies to ensure that clients and the server have parallel execution.
-   Check your actor's network role. This is useful for filtering execution in functions that activate on both server and client.
-   Check if your pawn is locally controlled using `IsLocallyControlled`. This is useful for filtering execution based on whether the pawn is relevant to the owning client.
-   Make use of network dormancy. It is one of the most significant optimizations you can make in your network gameplay.

## Tutorials

This documentation section provides some tutorials to help you get started with network programming in UE: