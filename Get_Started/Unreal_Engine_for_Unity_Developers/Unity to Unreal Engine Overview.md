# Unity to Unreal Engine Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unity-to-unreal-engine-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unity-to-unreal-engine-overview)  
**Processed:** 2025-06-14 16:55:54

---

If you are moving from Unity to Unreal Engine (UE), it can be challenging to translate familiar features that you rely on from one engine to the other. While both engines have similar functionality in many areas, UE's ecosystem and the way it is organized differ from Unity in many ways.

This guide provides a walkthrough of essential Unity editor features and concepts and their Unreal Engine equivalents. The sections below review the following topics:

-   Managing projects and installations.
-   Navigating Unreal Editor.
-   Managing level files.
-   Translating Unity GameObject terms and operations into Unreal Engine's Actor framework.

## Version Information

At the time of writing, the version of Unreal Engine and Unity engine used for screenshots and terminology are as follows:

-   Unreal Engine 5.4.3
-   Unity 6 (6000.0.2f1)

## Unity Hub / Epic Games Launcher

The Epic Games Launcher is Epic Games's equivalent to the Unity Hub application, which manages engine installations. It is also the portal and launcher for the Epic Games Store, Epic's gaming marketplace. To access Unreal Engine, follow these steps:

1.  Click the **Unreal Engine** tab on the left side of the launcher. A new series of tabs appears at the top of the screen.
    
2.  Click the **Library** tab to manage Unreal Engine installations and projects. Both projects you have created and packages you have downloaded appear in this window.
    
    ![An image showing where to install UE and manage projects in the Epic Games Launcher. UE 5.4.3 is shown as installed at the top of the screen.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f07d2e60-68d1-4c46-8c5e-419b6f7c8299/launcher.png)
    
    Alternatively, if you want an offline installation, you can [download the source code for Unreal Engine from GitHub](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).
    
    See [Installing Unreal Engine](/documentation/404) for more detailed setup information.
    

## Unity Editor / Unreal Editor

**Unreal Editor** is the application for editing UE levels and assets.

The screenshot below shows the Unity editor and Unreal Editor side by side. Different areas are color-coded to indicate common functionality. Each block is labeled to show the equivalent Unreal Engine terminology.

![An image showing the Unity editor (left) and the UE editor (right) side-by-side, with color-coded and numbered regions to show which UI elements perform similar functions.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ceee1c5-2a88-4ca5-8432-080b1d45b66e/editorcomparison.png)

| **Index** | **Unity** | **Unreal** | **Description** |
| --- | --- | --- | --- |
| 1 | Toolbar | Main Menu | Main menu with major drop-down menus, including File, Edit, Window, and Help. |
| 2 | Play/Pause/Step Controls | Play-In-Editor Controls | Controls for running play sessions in the editor. |
| 3 | Hierarchy | Outliner | List of objects in your game world. |
| 4 | Scene View/Game view | Viewport | Displays the game world. |
| 5 | Inspector | Details Panel | Displays editable parameters for selected objects. |
| 6 | Project Panel | Content Browser | Browser for exploring your project's assets, including levels, textures, materials, animations, sounds, and more. |
| 7 | Console | Output Log | Console that displays logs and provides a place to input commands. |

Unreal Editor's layout is fully customizable. You can drag and drop tabs, dock them into the main window, change the color scheme, and more. See:

-   [Customizing Unreal Engine](/documentation/en-us/unreal-engine/customizing-unreal-engine) for more information about editor customization.
-   [Unreal Editor Interface](/documentation/en-us/unreal-engine/unreal-editor-interface) for more information about navigating and using the editor.

### Tool Menus

The Main Menu bar in Unreal Editor provides different options compared with the toolbar in Unity's level editor. The following table provides a comparison of each editor's options and tips on where to find equivalent functionality where they don't match.

| **Unity** | **Unreal** | **Description** |
| --- | --- | --- |
| File | File | Used for opening and saving levels and projects. Unity places the **Build Options** menu here, whereas Unreal Engine provides a separate menu for build management. |
| Edit | Edit | Provides basic editing operations, like copy/paste, as well as options to open editor and project settings. Unity's **Edit** menu also has play mode controls, graphics settings, and selection management tools, whereas Unreal Engine breaks these out into separate menus. See the **Select** menu below for information about selection management. Unreal Engine's scalability settings are accessible through the **Settings** dropdown menu in the level editor's toolbar. |
| Assets | \- | Tools for creating and managing assets in your project. In Unreal Engine, this functionality is in the **Content Browser**. |
| GameObject | Actor | Tools for creating and managing in-game objects. Unity's menu is for creating new GameObjects, while Unreal Engine's is a context-sensitive menu for performing operations on a selected actor. In Unreal Engine, you can place actors either by clicking and dragging them from the **Content Browser** or by using the **Place Actors** panel. |
| Component | Component | Menu for creating and managing components on a selected GameObject. There is also a **Component** dropdown in Unreal Engine which appears when you select an actor's components. However, this menu is intended for editing components, not creating them. For equivalent functionality, select an actor and use the component controls in the **Details** panel, or open an actor's Blueprint and manage its components in the **Viewport** tab, under the **Components** panel. Alternatively, if you want to edit code, see the options in the **Tools** menu. |
| Services | Online Subsystems | Menu for accessing Unity's cloud services in the Package Manager. Unreal Engine's equivalent to the Package Manager is the **Plugins** window, which is located in the **Edit** menu, and many Online Subsystems are available as plugins. |
| \- | Tools | Provides access to various different toolsets and menus, including debuggers, shortcuts to creating C++ code in your IDE, Revision Control options, and more. |
| \- | Build | Provides options for running builds of different features of your game, including lighting, geometry, and landscapes. |
| \- | Select | Tools for selection management in the level editor. Unity places these in the **Edit** menu. Includes options to select different types of objects and geometry. |
| Window | Window | Shortcuts for opening commonly-used menus and panels. Also includes panel layout options. |
| Help | Help | Support and troubleshooting links, including links to community resources and documentation. |

### Scene View / Viewport

The screenshot below shows the Unity Scene View side-by-side with Unreal Editor's level editor viewport. Different areas are color-coded to indicate common functionality. Each block is labeled to show the equivalent Unreal Engine terminology.

![An image showing Unity's Scene View and UE's Viewport Panel side by side. The UI elements are color-coded and numbered to show which buttons and dropdowns have similar functionality.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e7b0778-bcd0-4a3c-81d0-93680288885a/viewportcomparison.png)

| **Index** | **Description** |
| --- | --- |
| 1 | Transform gizmo controls. |
| 2 | Local/World space controls. |
| 3 | Grid and snapping controls. |
| 4 | Lighting/shading controls. |
| 5 | Perspective/Orthographic controls |
| 6 | Object channel visibility controls. |
| 7 | Camera settings. |

### Project Panel / Content Browser

The **Content Browser** is Unreal Engine's equivalent to Unity's Project panel. You can browse and create new game assets here, as well as click and drag them into your Viewport.

![An image showing UE's Content Browser. The Character/Mannequins/Meshes folder is open, and the Content Browser displays assets for Manny and Quinn, the UE mannequins.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4c44671-7652-42ab-8e74-28392534ad13/contentbrowser.png)

See the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) documentation for more information about the Content Browser and its features.

### Inspector / Details Panel

The **Details** panel is Unreal Engine's equivalent to Unity's Inspector. Whenever you select an object in the world or edit a Blueprint, the inspector shows information about selected objects.

![A screenshot of the UE Details Panel. An instance of BP_TopDown Character is selected, and the Details Panel shows its settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5705082-d9be-4acf-8c2b-d67bf62a9e20/detailspanel.png)

The Details panel is searchable and has many filtering options for narrowing down what parameters you want to see, and also exposes an actor's components.

For more information, see:

-   [Unreal Editor Interface](/documentation/en-us/unreal-engine/unreal-editor-interface) for more information about Unreal Editor's panels and tabs, including the Details Panel.
    
-   [Details Panel Customizations](/documentation/en-us/unreal-engine/details-panel-customizations-in-unreal-engine) for information about how to customize the Details panel for specific Actors and properties.
    

### Project Settings

Click **Edit** > **Project Settings** to open the **Project Settings** window. This window contains configuration options for your project and many core UE systems, including Input, Physics, Asset Management, and Packaging options, as well as options for individual platforms and any plugins you enable.

![A screenshot of the Project Settings window.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f98ef22-6591-4345-b7db-a7c60e2f3e23/projectsettings.png)

### Plugins

Click **Edit** > **Plugins** to open the Plugins menu, where you can enable and disable many plugin packages for your project, including experimental and beta features.

If a plugin appears in the Plugins menu, it is compatible with your current version of UE by default.

![A screenshot of the Plugins window.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb37d86c-87b8-41c3-8427-a78f5c5dccdf/plugins.png)

## Scenes / Levels

**Level** files are Unreal Engine's equivalent to Unity's Scene files. Much like Unity scenes, you can load and unload these either synchronously or asynchronously. While you can hard-switch to a map using the Open Map function, Unreal Engine's [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) system can automatically stream levels based on the player's location.

### Scene Templates / World Settings

Whereas Unity uses Scene Templates to set up common objects or frameworks between multiple scenes, Unreal Engine's levels have built-in **World Settings**, which provide a place to override its game mode and change its settings. You can use [game framework](/documentation/en-us/unreal-engine/gameplay-framework-quick-reference-in-unreal-engine) classes like `AGameMode`, `UGameInstance`, and `AGameState` to create additional logic that is unique to your game's world.

### Picking Your Default Level

Unity chooses its default scene based on which scene is listed first in its Build Settings. In Unreal Engine, you choose a default map in the **Project Settings** window under **Projects > Maps & Modes**.

![The project settings window opened to the Maps and Modes section. Default maps are listed on the right.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4193546c-c268-4536-8579-b7490bbaa7e1/mapsandmodes.png)

## GameObjects / Actors

**Actors** are Unreal Engine's equivalent to GameObjects. Whereas Unity uses a composition-based framework for building GameObjects, Unreal Engine uses a combination of composition and object-oriented approaches.

### Prefabs / Blueprint and C++ Classes

In Unreal Engine, instead of creating actors in the world and then saving them as prefabs, you create a new actor class in C++ or Blueprint, then add instances of it to your world. When you create a new actor, you can choose to base it on another actor and inherit all of its components and code.

If you prefer Unity's workflow to editing GameObjects and prefabs, you can still place an empty actor in the world, then add components to it.

![An image displaying the workflow for adding components to a Blueprint Actor in the game world. The +Add dropdown displays a list of components to add. The user selects Point Light, and as a result, the Point Light component appears on the object in the world.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e35bd229-3332-4ea2-8a1e-fb0a2471a44b/componentworkflow.png)

After that, you can click the **Edit Blueprint** button to convert the object to a new Blueprint class.

### Placing and Browsing Actors

To browse UE's library of pre-made and commonly-used actors, use the **Place Actors** panel. You can use the search bar or the category filters to find triggers, lights, primitives, cinematic elements, and more. Click and drag actors from this list into your Viewport to add them to your world.

![A screenshot of the Place Actors menu.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6606a11a-fd2f-4a9e-ae84-b1372431b7d9/placeactors.png)

You can also use the **Actor** > **Place Actors** dropdown in the main menu to place commonly-used Actors. This menu is also available if you right-click in your Viewport. You can also use the Content Browser to browse for and place actors.

### Components

**Actor components** and **Scene components** are Unreal Engine's equivalent to Unity's components.

-   **Scene components** have a relative transform and appear in the actor's component hierarchy in both the Blueprint editor and the level editor's Details panel. Examples of scene components include meshes, audio sources, cameras, particle systems, lights, or anything else that benefits from having a physical presence in the game world.
    
-   **Actor components** only have code. They do not have a transform or a physical representation in the game world. Examples of actor components include movement components or components for handling AI, such as the AI Sensing component, the AI Blackboard, or the AI Behavior Tree. Many of these can interact with the world, but they don't need a local transform of their own to do it, instead relying on their parent actor to determine world location.
    

The following screenshot shows the Top-Down Character from the Top-Down game template. Scene components are parented under the actor and include the actor's mesh, camera, and collision. The **Character Movement component** is an actor component with no transform, so it appears in a separate list.

![A screenshot of the components for the Top Down Character in the Blueprint Editor. The component list shows all of its components.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2cf5250e-97c9-493e-acf7-454c789a753c/componentlist.png)

#### Adding Components

Add components to an actor in the game world by clicking the **\+ Add** button in the Details Panel.

![An image showing the workflow for adding a component to an instance of an Actor in the game world. The user clicks the +Add button next to the component list in the Details Panel, then chooses Point Light. As a result, the Point Light component is added to the Actor's component list.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cdd67b3-648a-4810-b6fd-a5bd38bb6170/addcomponentworld.png)

Add components directly to a Blueprint class by clicking the **\+ Add** button in the Blueprint editor's **Components** panel.

![An image showing where to add components in the Blueprint editor. The +Add dropdown in the Viewport shows an extensive list of components.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ab21900-aac8-4b3a-ae85-ab49505b411a/addcomponentbp.png)

In C++, add components with the `UObject::CreateDefaultSubObject` function. If the component should be attached to the actor by default, add it in the actor's **constructor** function.

### Parenting GameObjects / Sub-Objects in Unreal Engine

In Unity, to create complex objects with multiple parts that have relative transforms, you need to attach GameObjects as children to another GameObject.

In Unreal Engine, you add sub-objects by adding scene components to your actor. Scene components fulfill most jobs that child GameObjects do in Unity, such as providing colliders, particle effects, audio sources, or adjustable lights.

![A screenshot showing the Top-Down Character in the Viewport, and its Details on the right hand side of the screen. The Component list displays all of its components, and the Viewport shows how they are attached to the character.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf28713e-cd85-43d3-9f78-3cfefe2ab813/topdowncharacter.png)

You can also use the **child actor component** to attach an entire actor to another, or you can use the **Attach to Actor** function in your code to do it at runtime.

## Gameplay Framework

Unreal Engine's [Gameplay Framework](/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine) is a collection of classes that provides you with a modular foundation to build your gameplay experience on. You can pick and choose which elements are right for your game knowing that these classes are designed to work with and complement one another.

## Building and Packaging Your Project

Unreal Engine's **Platforms** dropdown serves a similar purpose as Unity's Build Settings menu.

To create a packaged build of your project, click the **Platforms** dropdown, highlight the platform you want to package for, then click **Package Project**. This will build, cook, and package all the content in your project. The **Quick Launch** options will package and deploy your build to a specific device in a single step.

![An image showing the Platforms dropdown in Unreal Editor. The Android sub-menu is open, and the button for packaging a project is highlighted.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b4f099d-1f80-497f-a7b8-09a66494b39b/packageproject.png)

Alternatively, you can use the **Project Launcher** to launch preconfigured builds, or you can use the **Unreal Automation Tool (UAT)** script to run headless command line builds.

For more information, see:

-   [Build Operations](/documentation/en-us/unreal-engine/build-operations-cooking-packaging-deploying-and-running-projects-in-unreal-engine) for information about creating builds.
-   [Cooking and Chunking](/documentation/en-us/unreal-engine/cooking-content-and-creating-chunks-in-unreal-engine) for information about how your project packages assets.