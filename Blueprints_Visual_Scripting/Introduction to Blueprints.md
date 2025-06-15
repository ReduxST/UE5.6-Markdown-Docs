# Introduction to Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-blueprints-visual-scripting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-blueprints-visual-scripting-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:36

---

The **Blueprint Visual Scripting** system in Unreal Engine is a visual programming language that uses a node-based interface to create gameplay elements. The node-based workflow provides designers with a wide range of scripting concepts and tools that are generally only available to programmers. In addition, Blueprint-specific markup available in Unreal Engine's C++ implementation provides programmers with a way to create baseline systems that designers can extend.

As with many common scripting languages, you can use the system to define object-oriented (OO) classes or objects in the engine. The system, along with the objects you define, are often referred to as just "Blueprints".

### Prerequisite Knowledge

We recommend understanding the following topics before continuing with the page:

-   [Unreal Engine Terminology](/documentation/en-us/unreal-engine/unreal-engine-terminology)
-   [Levels in Unreal Engine](/documentation/en-us/unreal-engine/levels-in-unreal-engine)

## How Do Blueprints Work?

Blueprints work by using graphs of nodes for various purposes, such as object construction, individual functions, and general gameplay events. You can create gameplay elements by connecting nodes of events, functions, and variables with wires.

## Commonly Used Blueprint Types

The most common Blueprint types are **Level Blueprints** and **Blueprint Classes**.

For a full list of types, see [Types of Blueprints](/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine).

## Level Blueprint

A Level Blueprint contains logic for level-specific events within maps. Each level has a Level Blueprint, which can:

-   Reference and manipulate actors within the level
-   Control cinematics using [level sequence actors](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview)
-   Manage level streaming

A Level Blueprint can also interact with Blueprint Classes placed in the level, such as reading variables and triggering custom events. To learn more, see [Level Blueprints](/documentation/en-us/unreal-engine/level-blueprint-in-unreal-engine).

## Blueprint Class

A Blueprint Class defines a new class or type of actor that you can place into maps as instances. Editing a Blueprint Class used throughout a project will update every instance of it.

Blueprint Classes are ideal for making interactive assets such as doors, switches, collectible items, and destructible scenery. To learn more, see [Blueprint Class](/documentation/en-us/unreal-engine/blueprint-class-assets-in-unreal-engine).

## What Else Can Blueprints Do?

The following topics are a few examples you can accomplish with the Blueprint system.

## Create Customizable Prefabs with Construction Scripts

![Construction Script](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51bdfc25-2f94-42a2-9e56-7009f08cd0ff/construction-script-ue5.png)

The [Construction Script](/documentation/en-us/unreal-engine/construction-script-in-unreal-engine) is a type of graph within a Blueprint Class that executes when an actor is placed or updated in the editor, but not during gameplay. It helps create customizable props that improve environment artists' workflows. For example, a light fixture that automatically updates its material to match the color and brightness of its point light component or a Blueprint that randomly scatters foliage meshes over an area.

In the [Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) maps, the demo rooms that contain each example (pictured above) are a single Blueprint made up of many components. The Blueprint's Construction Script creates and arranges the various static meshes and lights according to parameters exposed in the Blueprint's **Details** panel. With each Content Example map, we can drop in the demo room Blueprint, set values for the length, height, and number of rooms to generate, and have a complete set of rooms ready in moments.

## Create A Playable Game Character

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf68e43f-d2ba-4aee-b1e4-8da70d33e2d0/game_characters.png)

[Pawns](/documentation/en-us/unreal-engine/pawn-in-unreal-engine), a type of Blueprint Class, are the physical representation of actors players can control. With a pawn class, you can assemble every element you need to create a playable [Character](/documentation/en-us/unreal-engine/characters-in-unreal-engine). You can manipulate [camera](/documentation/en-us/unreal-engine/cameras-in-unreal-engine) behavior, set up input events for mouse, controller, and touch screens, and create an animation Blueprint asset for handling skeletal mesh animations.

A character Blueprint contains a character component that has much of the behavior needed for moving around, jumping, swimming, and falling built-in. To finalize the setup, you must add some input events in accordance with how you want players to control your character.

To learn more, see [Setting Up Character Movement](/documentation/en-us/unreal-engine/setting-up-character-movement).

## Create A HUD

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcd31caa-085f-46e0-803d-3f56b9e2552b/create_huds.png)

You can use Blueprints to create a game's HUD (heads-up display). The setup is similar to Blueprint Classes in that it can contain event sequences and variables but is assigned to your project's GameMode asset instead of directly to a level.

You can set up a HUD to read variables from other Blueprints, display a health bar, update a score value, display objective markers, and more. It is also possible to use the HUD to add hit-boxes for elements like buttons you can click on.

While possible with Blueprint, the [Unreal Motion Graphics](/documentation/en-us/unreal-engine/umg-editor-reference-for-unreal-engine) system is a more designer-friendly way of laying out a UI. The system is based on Blueprint Visual Scripting.

## Blueprint Editors and Graphs

The **Blueprint Editor** is the user interface you use to construct Blueprint elements to build your visual script.

![Blueprint Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cf4ae24-21fb-4dbc-a520-8827758e52f7/blueprint-editor-ue5.png)

The Blueprint Editor's UI changes based on the type of Blueprint chosen. The core feature of most **Blueprint Editors** is the **Event Graph** tab for laying out the network of your Blueprint.

To learn more about the interface, see [Blueprint Editor](/documentation/en-us/unreal-engine/user-interface-reference-for-the-blueprints-visual-scripting-editor-in-unreal-engine).

## Getting Started

You can continue to learn the basics of visual scripting in Unreal Engine with the following pages.

## Blueprint Samples and Tutorials

Additional hands-on resources you can use to learn more about the Blueprint system.

-   [Sample Projects](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine)
-   [Blueprint Tutorials](/documentation/en-us/unreal-engine/blueprint-workflows-in-unreal-engine)