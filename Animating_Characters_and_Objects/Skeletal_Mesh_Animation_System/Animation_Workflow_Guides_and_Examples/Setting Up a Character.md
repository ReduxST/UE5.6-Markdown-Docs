# Setting Up a Character

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-character-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-character-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:57

---

![Character](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1ad8a81-1eaf-4735-a011-855e638e2763/ue5_1-character.png)

No matter your game project or genre, it is likely that at some point you are going to need some kind of animated character to move around in your environment. This may be a character that the player controls or may be some AI-driven entity that interacts with the world in some way. Regardless, you are going to need to know how to set such characters up so that they can properly animate in your world. The purpose of this document is to give you a very high-level overview of how this is done while guiding you to dedicated documents and examples for specific details. For our purposes, we will assume that you want to create a character that is controllable by the player in some way.

Throughout this document, we will make references to various scripting operations that can be done with Blueprints. Anything that can be done in Blueprints can also be done in C++, so you should not feel restricted solely to Blueprint visual scripting. The final section of this document contains references to example content showing the setup in both C++ and in Blueprints.

You can also find an example of the Playable Owen Character on the [Animation Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) page under section 1.10.

## Workflow at a Glance

The primary workflow for character setup in Unreal Engine is as follows:

1.  Create your art assets (Skeletal Meshes) and animations, using a 3rd party digital content creation (DCC) package such as 3ds Max or Maya.
2.  Import your Skeletal Meshes and animations into Unreal Engine by creating a new Skeleton asset for new Skeletal Meshes or by reusing an existing Skeleton asset for identical or similar Skeletal Meshes.
3.  Create a PlayerController script or Blueprint to handle inputs from the player.
4.  Create a Blueprint or script for a Character or Pawn to parse inputs and control the actual movement (not skeletal animation) of the character.
5.  Construct the Animation Blueprint for the character.
6.  Create a GameMode script or Blueprint that utilizes your custom PlayerController and any other custom script assets.
7.  Play your game!

Each of these steps will generally require a wide variety of further sub-steps to be completely successful. This list just gives a general idea of the flow. In the following sections, we will go into further detail on exactly what each one of these steps means and how you can apply them.

## Creating Art Assets

![Art Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e27d4486-a585-4a7d-9d39-b60838bb3454/ue5_1-art-assets.png)

In many ways, the creation of your art assets may be the most challenging part of the character development process. Generally, there is significant design, modeling, surfacing, rigging, and animation time that must take place long before you even touch the Unreal Engine. While we cannot teach you the nuances of character design and animation, we do have certain tools to help the process along.

## Importing Skeletal Meshes

![Character Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58cd9c0e-aaf1-4d57-9555-c671c4d20ad2/ue5_1-character-viewport.png)

For more information, please see the [FBX Importing](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) and [Skeletal Meshes](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) documentation.

Properly importing your Skeletal Meshes into Unreal Engine is a vital step in the process of creating your animated characters. Unreal contains a robust importing system with a variety of options to speed up your import process.

## Creating a Player Controller

![Player Controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f3ffe14-8629-41d6-bc4a-7754f3eca7a0/ue5_1-player-controller.png)

The PlayerController is a special type of script or Blueprint whose primary purpose is to parse inputs from the player into events that can drive a character. For instance, it can control how moving the analog stick on a controller upward can cause an event that will eventually be used to push the character forward on the screen.

A PlayerController is already an existing Class within Unreal. In the editor, you can create a new Blueprint with a parent class of PlayerController, and then use this to set up your events that will take place upon inputs from the player.

For an example of a custom Blueprint PlayerController, you can start a new project within the editor (**File > New Project**) and check out the **Blueprint Top Down** template. All of the Blueprint-based templates will contain a PlayerController of some sort (either the default Player Controller or a Player Controller Blueprint), though if you want to see a custom application using a Player Controller, the **Blueprint Top Down** template is the most straight forward.

Once within the new project, you can search within the **Class Viewer** for PlayerController, turning off the filters in the **Class Viewer**. Double-clicking on this asset will open it up and you can see the setup for yourself.

You can also see a PlayerController in C++ script by creating a new project (**File > New Project**) and choosing the **C++ Top Down** template.

## Creating a Pawn or Character Blueprint

![Character Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08525987-beba-4e3b-9880-c691a3a73918/ue5_1-character-blueprint.png)

Once you have set up your PlayerController, your system is now prepared to handle inputs from the player. Now, however, you have to translate those inputs into something that can in turn drive a character around on the screen. That means those inputs need to be translated (or parsed) into actions. This is where the Pawn or Character classes come into play.

### Choosing Pawn or Character

You will notice that we mention two potential classes here: Pawn and Character. Both are used for entities in the game that are either controlled by the player or by in-game AI. The key difference is that the Character class is an extension of the Pawn class, adding in player physics, support for a specific mesh, and the general types of handling needed when creating a playable in-game character. For our purposes, we will be using the Character class. For simpler elements that would just need to be driven around the scene by AI, for example, you can generally get away with using a Pawn.

### Character Class Setup

![Character Class Setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04d07fe5-7654-4e21-8bc4-1c9acbd4f93a/ue5_1-character-blueprint-graph.png)

Your Character Class is going to start with events that are triggered from the PlayerController, and use scripting (including Blueprint visual scripting) to control what to do with those inputs and how they can be used to control the character. For instance, where the PlayerController simply creates a basic event for moving the analog stick on a controller in an upward direction, the Character class is responsible for receiving that event and using it to drive the character forward.

The Character Class also holds a reference to a Skeletal Mesh, which will be the basis for what the player sees while playing the game. In the case of a first-person game, this is often just a pair of floating arms, though there may be a full body if you need that body to shadow the environment properly. For third-person games, the mesh will be the Skeletal Mesh that represents the character.

Motion on a character is generally handled by applying some motion to the physics shape (typically a capsule). This motion also coincides with a MovementMode. This is an enumeration used to keep track of what a character is doing (i.e. walking, running, falling, swimming, etc.). This information will later be used to drive what animations are being played on the Skeletal Mesh.

For an example of a custom Blueprint Character class, you should start a new project within the editor (**File > New Project**) and choose either of the Blueprint templates for First Person or Third Person. All of the Blueprint-based templates will contain a Character of some sort, though we recommend the First or Third Person templates due to their overall simplicity and the common use of those genres.

Once within the new project, you can search within the **Class Viewer** for Character, filtering by Blueprints in the Game folder. Double-clicking on this asset will open it up and you can see the setup for yourself.

You can also see a Character in C++ script by creating a new project (**File > New Project**) and choosing either the First or Third Person Code templates.

## Animation Blueprint

![Animation Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f41ea1a4-c8ff-4033-b2e0-454544c75b99/ue5_1-animation-blueprint.png)

You do most of the heavy lifting of hooking up animation to Characters in the Animation Blueprint.

After you have defined how a Skeletal Mesh Actor moves around in the world in the Character Blueprint, you can start assigning specific animations based on those movements (such as velocity) in the Animation Blueprint.

Animation Blueprints are by far the most sophisticated aspect of character setup. This is where all of your data comes together to cause your Skeletal Meshes to perform the appropriate animations. To fully understand Animation Blueprints and their power, there are many different animation assets that you should know about, including:

-   [State Machines](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine)
-   [Blend Spaces](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine)
-   [Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine)

These are just the tip of the iceberg. You would do well to look at the [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) documentation, and to also look at some of the Animation Blueprints included in some of our examples content, such as the First and Third Person Templates and those found within the Content Examples project.

Once you have created the Animation Blueprint that defines the motion of your character, you will need to make sure you assign it to the **Anim Blueprint Generated Class** property, found under the Mesh Component of the Character Blueprint. This is necessary because you may have multiple Animation Blueprints for each Skeletal Mesh, and the Character Blueprint needs to know the one into which it will be sending the necessary animation and variable data.

## GameMode Setup

![GameMode Setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41d79a3b-409a-45f9-ae2a-dbd5890e8440/ue5_1-game-mode.png)

A GameMode is a special type of class that is used to define your game. Generally speaking, is it going to be just a collection of properties used to define what the essential classes for your game are going to be. The primary properties you will set up include:

-   **Game Session Class** - This class of Game Session handles loging approval and online game interface.
-   **Game State Class** - This class controls any special rules or setup for how your game will be played, but is not covered in this document.
-   **Player Controller Class** - This will hold the custom PlayerController you set up for your in-game character.
-   **Player State Class** - This class defines any special rules for replicating relevant player information to all clients.
-   **HUD Class** - This contains any special heads-up display (HUD) classes created, which are not covered in this document.
-   **Default Pawn Class** - This will hold the Character class you set up for your in-game character.
-   **Spectator Class** - This holds any special classes used to control spectators or passive players that just watch the action. These are not covered in this document.
-   **Replay Spectator Class** - This holds any special classes used to control spectators when in a replay. These are not covered in this document.
-   **Server Stat Replicator Class** - Class used to replicate server "stat net" data over.

For testing out your character, you need to at the very least set up the Default Pawn Class and the PlayerController Class properties.

### World Settings

![World Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e276bb7f-1e41-4fee-a9c4-6e21ade219f6/ue5_1-button-toolbar-world-settings.png)

Once you have set up your GameMode, the last step to being able to play with your custom Character is to make sure that the current Level is using your GameMode. This is done using the **World Settings** tab, accessible from the **Settings** button located on the main toolbar.

Within the **World Settings**, you will want to make sure you have set the **GameMode Override** to the name of your GameMode class. Once you have done that, you are ready to save and test out your new character!

![Game Mode Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9599bddc-9fb1-4de3-ba0c-7a033ecac389/ue5_1-game-mode-settings.png)

## Summary

So, to summarize the flow of setup back up the chain:

-   Your Level's World Settings are used to set which GameMode you are using.
-   The GameMode specifies which Pawn (Character) Class and which PlayerController Class you will need to play the game.
-   The Character Class:
    -   Contains the Skeletal Mesh that you imported via FBX.
    -   Takes in data from the PlayerController Class and converts it to the movement (not animation).
    -   Stores which Animation Blueprint will be used to drive skeletal animation within its Mesh Component.
-   The Animation Blueprint:
    -   Takes data from the Character Class into its Event Graph.
    -   Uses that data to drive State Machines, Blend Spaces, and other assets.
    -   Those assets use Animation Sequences (skeletal animation data from an FBX file) to animate the character.
-   The final result of the Animation Blueprint is applied to your Skeletal Mesh so that you can see the in-game character animate.

## Included Examples

There are several examples you can check out in the engine to see how these setups are done and try them for yourself. We include both Templates, which are basic project genres you can use to make your games, and Content Examples, which are pre-constructed examples of content created by artists and technicians here at Epic.

### Templates

![Templates](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8649f03-0430-4ae7-8c44-bddcfc0ef772/ue5_1-new-project.png)

When you create a new project in Unreal Engine (**File > New Project**), you are given the option to choose a Template. Virtually all of these will use their GameModes, Character Blueprints, Animation Blueprints, and every asset mentioned in this document. For purposes of simplicity and clarity, we strongly recommend you check out the First Person or Third Person Templates.

Each of these Templates is available in a coded form or a Blueprint form so that you can choose to develop it in the way that you are most comfortable. If you are a coder, you will probably want to use a Code Template. If you are a more artistic developer, you will likely be more comfortable exploring a Blueprint Template. Be aware that the two are not mutually exclusive; you can add code classes to a Blueprint Template project, just as you can add new Blueprint classes to a Code Template project!

### Content Examples

![Content Examples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d13afe78-6dc8-42ba-b62a-06571da22573/ue5_1-animation-content-examples.png)

Content Examples are specialized versions of content designed by artists and technicians here at Epic. They are found within a project named **ContentExamples**, which can be downloaded by users via the **Marketplace**. Of particular importance would be the assets found within the **Animation** map inside the **Maps** folder, which shows a variety of uses for Skeletal Mesh animation on a character.