# User Interfaces and HUDs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/user-interfaces-and-huds-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/user-interfaces-and-huds-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:03

---

The way in which the game communicates and interacts with the player is extremely important. **User Interfaces** (UIs) and **Heads-up Displays** (HUDs) are the games' way of providing information about the game to the player and in some cases allowing the player to interact with the game.

Unreal Engine provides multiple means of creating UIs and HUDs. The `Canvas` class can be used to draw directly to the screen at a low level, overlaid onto the world.

The game's Interface is used to convey information to the player and provide a means of prompting the user for directed input. A game interface generally consists of two main elements: the heads-up display (HUD) and menus or user interfaces (UIs).

The HUD refers to the status and information overlaid on the screen during gameplay. The purpose of the HUD is to inform the player of the current state of the game, i.e. the score, their health, the amount of time remaining, etc. The HUD is usually non-interactive, meaning the player does not click on elements of the HUD, though this becomes a gray area in certain types of games where the HUD and user interfaces are hard to separate.

**User Interfaces** refer to menus and other interactive elements. These elements are usually drawn overlaid on the screen much like the HUD, but in certain circumstances they could be part of the game world itself rendered onto a surface in the world. The most obvious examples of UIs are the main menu displayed when the game starts up or the pause menu shown when the player has paused the game. However, other UIs may be displayed during play. These could be used to show dialog between characters in the game or in more complex situations, such as in an RTS or RPG, they may be integral to the game play itself allowing the player to choose weapons, armor, units to build, etc.

## HUD

The **HUD** is the base object for displaying elements overlaid on the screen. Every human-controlled player in the game has their own instance of the `AHUD` class which draws to their individual Viewport. In the case of splitscreen multiplayer games, multiple Viewports share the same screen, but each HUD still draws to its own Viewport. The type, or class, of HUD to use is specified by the gametype being used.

## Canvas

The **Canvas** is an object that can be used during the render loop of the HUD to draw elements - text, texture and material tiles, arbitrary triangles, and simple primitive shapes - to the screen. Unless you are making use of some specialized alternative, drawing with the Canvas is the method used to create HUDs and UIs in games made with Unreal Engine.

## Slate

**Slate** is a custom and platform agnostic user interface framework that is designed to make building the user interfaces for tools and applications such as Unreal Editor, or in-game user interfaces, fun and efficient. It combines a declarative syntax with the ability to easily design, lay out, and style components that provides a method for creating and iterating on UIs.

[Refer to Slate UI Framework](/documentation/en-us/unreal-engine/slate-user-interface-programming-framework-for-unreal-engine) for additional documentation.