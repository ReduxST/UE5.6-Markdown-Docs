# Gameplay Framework

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:59

---

**Unreal Engine's Gameplay Framework** is a collection of classes that provides you with a modular foundation upon which to build your gameplay experience. You can pick and choose which elements are right for your game knowing that these classes are designed to work with and complement one another.

## Overview

Visual representation of the gameplay framework classes and how they are associated with one another in Unreal Engine. Click image to expand.

The *game instance* is instantiated on engine launch and remains active until the engine shuts down. It is a manager class that has no physical presence in the game, but rather exists to track data and run code. The game instance is not replicated and exists independently on the server and all connected clients in network multiplayer. Anything that you want to persist between level loads should live in the game instance. For example, this makes the game instance a good place to manage your save game system. The game instance also acts as a manager for any number of *game instance subsystems* that are created and destroyed by the game instance and exist for the same lifetime as the game instance itself. An example of one of these subsystems is the Online Subsystems which you can use to manage online services functionality such as friends, game sessions, lobbies, leaderboards, and much more in your game.

The *game mode* is instantiated immediately after your level is loaded in the engine and the world is created. The game mode is a server-based manager class inherited from the actor class. Since this class is created upon level load, it is not persistent across levels. Game mode is the first actor to instantiate upon level load and can be set on map-by-map basis. Game mode exists at the heart of the gameplay framework managing the overall rules and structure of a gameplay session and instantiating the remaining framework actors upon creation. The first two are game state and player state.

*Game state* and *player state* are non-physical actors that are designed to track the state of the game and the players within it, respectively. These classes replicate their state information between the authoritative server and all connected clients in network multiplayer. Game state contains data and logic relevant to all players in a game, such as team scores, objectives, and a list of all players and their associated player states. On the other hand, the player state handles data and logic relevant to its associated player, such as health, ammo count, and inventory. A single game state is created by the game mode. A player state is created for each player when they join a game or upon entrance into the level.

The game mode spawns players when they join the game. A player primarily consists of a *controller* and a *pawn*. The controller classes handle the logic that dictates a player's actions in the game world. There are two types of controller class in UE that are widely used: *player controller* and *AI controller*. The player controller class is a manager class that can process input from a human, display heads-up information, and possess physical representations in the game. The AI controller class is a manager class that possesses physical representations in the game and dictates their actions with the help of UE's artificial intelligence, including: behavior trees, state trees, navigation, and so on.

As a non-physical actor class, the controller class and its derived classes do not have a physical manifestation in the game world. The *pawn* class consists of the physical manifestation of the player in the game world. The pawn class is as important to creating a player as the controller class. Controllers possess pawns and direct the pawn to perform actions in the game. Pawns, as actor-derived classes, consist of several actor components such as collision component, static mesh component, and movement component. The character class is a pawn-derived subclass that builds upon the default pawn class with more feature rich components, including: character movement component, skeletal mesh component, and capsule component.

The [Begin Play](https://dev.epicgames.com/community/learning/tutorials/l21z/unreal-engine-begin-play-gameplay) Epic Developer Community learning tutorial presents a video of a comprehensive overview of the gameplay framework in Unreal Engine.

## Gameplay Framework Classes

The following table provides an overview of important classes contained within the gameplay framework, a brief description of the class, and a link to each class' dedicated documentation pages:

| **Class** | **Description** | **Derived Classes** |
| --- | --- | --- |
| [Actor](/documentation/en-us/unreal-engine/actors-in-unreal-engine) | 
An Actor is any object that can be placed into a level, such as a Camera, static mesh, or player start location. Actors support transformations such as translation, rotation, and scaling. They can be spawned and destroyed through gameplay code.

Actors are also containers that hold special types of objects called actor components. Different types of components are used to control how actors move, how they are rendered, etc. The other main function of actors is the replication of properties and function calls across the network during play.



 | Pawn, Controller, Game Mode, Game State, Player State, HUD, Camera, and many more. |
| [Actor Component](/documentation/en-us/unreal-engine/components-in-unreal-engine) | Actor components are the building blocks of actors. Different actor components control different pieces of an actor, such as how the actor moves, how it is rendered, where it exists in the world, how it is viewed by the player, and so on. | Scene Component, Audio Component, Particle System Component, Primitive Component, Camera Component, Spring Arm Component, Skeletal Mesh Component, Static Mesh Component, and many more. |
| [Pawn](/documentation/en-us/unreal-engine/pawn-in-unreal-engine) | Pawn is the base class for any actor that can be controlled by a player or AI. | Default Pawn, Spectator Pawn, Character |
| [Character](/documentation/en-us/unreal-engine/characters-in-unreal-engine) | A character is a special type of pawn designed for a vertically-oriented player representation that can walk, run, jump, fly, and swim through the world. |   |
| [Controller](/documentation/en-us/unreal-engine/controllers-in-unreal-engine) | Controllers are non-physical actors that can possess a pawn to control its actions. A player controller is used by human players to control pawns, while an AI controller implements artificial intelligence to dictate a pawn's actions. | [Player Controller](/documentation/en-us/unreal-engine/player-controllers-in-unreal-engine), [AI Controller](/documentation/en-us/unreal-engine/ai-controllers-in-unreal-engine) |
| World | World is the top-level object representing a map in which Actors and Components will exist and be rendered. Contains the persistent level and many other objects like gamestate, gamemode, and lists like Pawns and Controllers currently on the map. |   |
| [Game Mode](/documentation/en-us/unreal-engine/game-mode-and-game-state-in-unreal-engine#gamemodes) | Game mode is the primary class that specifies which other classes to use in the gameplay framework and is commonly used to specify game rules for modes, such as capture the flag. |   |
| Game Instance | The game instance class persists throughout the lifetime of the game. Traveling between maps and menus maintain the same instance of this class. This class is used to manage information and systems that need to exist throughout the lifetime of the game between levels and maps. You can also use the Game Instance class to organize different game instance subsystems. |   |
| Game Instance Subsystem | Game instance subsystems are used to organize systems and functionality that should exist for the lifetime of the game. An example is subsystems that control online services functionality in games that include online experiences. |   |
| [Game State](/documentation/en-us/unreal-engine/game-mode-and-game-state-in-unreal-engine#gamestate) | Game state contains data and logic relevant to all players in a game, such as team scores, objectives, and a list of all players and their associated player states |   |
| Player State | Player state handles data and logic relevant to its associated player, such as health, ammo count, and inventory. |   |
| Gameplay Statics | Static class to handle common game-related functionality like playing sounds, spawning particle effects, spawning Actors, applying damage to Actors, getting player pawn, player controller, and so on. |   |
| [User Interface](/documentation/en-us/unreal-engine/creating-user-interfaces-with-umg-and-slate-in-unreal-engine) | User Interfaces (UI) consist of game menus, heads-up displays (HUD), and other elements drawn over the game screen. They provide users with information and help players interact with the game. |   |
| [HUD](/documentation/en-us/unreal-engine/user-interfaces-and-huds-in-unreal-engine) | The HUD is the base object for displaying elements overlaid on the screen. Every human-controlled player in the game has their own instance which draws to their individual viewport. |   |
| [Camera](/documentation/en-us/unreal-engine/cameras-in-unreal-engine) | The camera represents the player's point of view or how the player sees the world. For this reason, cameras only have relevance to human-controlled players. |   |

You can customize and use most of the classes in UE's gameplay framework in either C++, Blueprint, or, the most common, a combination of both.

## Directory