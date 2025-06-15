# Setting Up a Game Mode

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-game-mode-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-game-mode-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:59

---

The **GameMode** defines the game's set of rules. The rules can include how players join the game, game pausing, and level transition, as well as any game-specific behavior such as win conditions. The GameMode is set for each level, and GameModes can be reused in multiple levels.

## Implementation Guide

This guide covers how to create a GameMode Blueprint and set default values for it, how to assign a Default GameMode for your game, and how to override the Default GameMode through the World Settings and GameMode Override option.

### Creating a Game Mode Blueprint

The steps below will guide you in creating and setting up defaults for a **Game Mode** Blueprint.

For this example, we are using the **Blueprint Third Person Template**; however you can use any project you wish.

1.  In the **Content Browser**, click the **Add New** button.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/08732cc7-a2d3-4e5f-8313-0796637dbd41?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/08732cc7-a2d3-4e5f-8313-0796637dbd41?resizing_type=fit)
    
2.  Select **Blueprint Class** from the **Create Basic Asset** section of the dropdown menu.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/e93cfb34-4d9c-4c09-ba5c-4c2084c751d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e93cfb34-4d9c-4c09-ba5c-4c2084c751d5?resizing_type=fit)
    
    You can create several different [types of Blueprint Assets](programming-and-scripting/blueprints-visual-scripting/UserGuide/Types) from the **Blueprints** option under **Create Advanced Asset**.
    
3.  Choose a **Parent Class** for your Blueprint Asset. See [Parent Classes](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine) for more information.
    
    [![Choose a Parent Class](https://dev.epicgames.com/community/api/documentation/image/dbc1917c-a4a6-4986-a658-4179c2ccc8d0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dbc1917c-a4a6-4986-a658-4179c2ccc8d0?resizing_type=fit)
    

In the **Pick Parent Class** window, select the **Game Mode Base** Class. This is the parent class for all Game Modes.

### Editing the Game Mode Defaults

1.  **Double-click** on the Blueprint to open it, click the **Class Defaults** button to open the Blueprint Defaults in the **Details** panel.
    
2.  Under the **Game Mode** are several options that you can set as the game's default settings (default character, HUD, etc.).
    
    [![](https://dev.epicgames.com/community/api/documentation/image/6159dbd0-d0ea-4090-a442-04bffb11555a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6159dbd0-d0ea-4090-a442-04bffb11555a?resizing_type=fit)
    
    Here we are assigning the Character Blueprint called ThirdPersonCharacter as the Default Pawn Class for players to use in the game.
    
    The **Game Mode** Blueprint points to existing Blueprints of the Character, HUD, PlayerController, Spectator, and Game State Classes. You will need to create these separately then specify them for use in the Game Mode Blueprint in order to actually use them in your game.
    

### Assigning a Default Game Mode

In the previous section, we created a Game Mode Blueprint. Once you have a Game Mode Blueprint, you can assign it as the Default Game Mode to use in your game. The steps below will guide you through assigning the Default Game Mode through the Project Settings option.

1.  From the Main Editor Window, click the **Edit** button from the Menu Bar, then select **Project Settings**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2bb6c3ae-3d14-466b-b079-111f850587ff?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bb6c3ae-3d14-466b-b079-111f850587ff?resizing_type=fit)
    
2.  In the **Project Settings** window, click the **Maps & Modes** option.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/c4b7e9f8-9cfa-4704-8bb6-7ff5179b9815?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c4b7e9f8-9cfa-4704-8bb6-7ff5179b9815?resizing_type=fit)
    
3.  In **Maps & Modes** under **Default Modes**, click the **Default GameMode** drop-down box and assign the **GameMode** you wish to use.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/9481267e-284d-498b-bbd4-84fba7a1302a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9481267e-284d-498b-bbd4-84fba7a1302a?resizing_type=fit)
    
    This will assign the **GameMode** you select as the **Default Game Mode** whenever the project is loaded.
    
4.  If you click the arrow next to **Selected GameMode**, you will see the current settings used by the assigned **GameMode**.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/93fc7305-9c28-4536-9d2f-cbabeebbb39f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/93fc7305-9c28-4536-9d2f-cbabeebbb39f?resizing_type=fit)
    
    Here we can see that **ThirdPersonCharacter** is being used as the **Default Pawn Class**.
    

### Overriding the Default Game Mode

When you have a Default Game Mode assigned, you can overwrite it on a per level basis through the World Settings menu under the GameMode Override section. The steps below will show you how to override the default Game Mode.

1.  From the Main Editor Window, click the **World Settings** button from the Main Toolbar.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/42d59bac-6915-4a86-a60d-789fdb9680d0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/42d59bac-6915-4a86-a60d-789fdb9680d0?resizing_type=fit)
    
2.  This will open the **World Settings** option which will appear in the bottom right window where the **Details** tab is located.
    
3.  Inside the **World Settings**, under **Game Mode**, you can click the **GameMode Override** drop-down box to change the **GameMode** used.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/dbaca3e3-bf80-44f0-a454-191f3ebbca80?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dbaca3e3-bf80-44f0-a454-191f3ebbca80?resizing_type=fit)