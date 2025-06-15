# Using Editor Viewports

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:06

---

Windows macOS Linux

The **Viewports** are your window into the worlds you create in Unreal. They can be navigated just as you would in a game, or can be used in a more schematic design sense as you would for an architectural Blueprint. The Unreal Editor viewports contain a variety of tools and visualizers to help you see exactly the data you need.

Click image for full size.

## Viewport Types

There are two main types of Viewports in Unreal Editor: Perspective and Orthographic. The perspective view is a 3D window into the game world. The Orthographic views - Front, Side, and Top - are 2D Viewports that each look down one of the main axes (X, Y, or Z).

    |   |   |   |   |
| --- | --- | --- | --- |
| ![View Perspective](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/613da54a-21d5-4b83-a0f8-15480e8999f6/02-view-perspective.png "View Perspective") | ![View Front](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5aec35b-aa60-4cd9-a5ed-e93bee80b27b/03-view-front.png) | ![View Side](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0053438e-db97-4f98-8364-9d7368464d75/04-view-side.png) | ![View Top](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78ceea8a-1a85-45a5-b032-6c4bbef21fe5/05-view-top.png) |
| Perspective (3D) | Front (X-Axis) | Side (Y-Axis) | Top (Z-Axis) |

You can cycle through the types of Viewports by pressing **Alt** and **G**, **H**, **J**, or **K**. These set the Viewport to be Perspective, Front, Side, or Top, respectively.

## Viewport Layout

By default, you see a single Perspective Viewport when you open Unreal Editor.

Click image for full size.

The **Viewport** panel actually contains multiple Viewports, which are laid out in a grid and any of which can be shown maximized. The default layout is a 4x4 that consists of one of each type of Viewport - Perspective, Top, Front, and Side.

Click image for full size.

The Viewports can be minimized and maximized using the ![Minimize Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6844de80-36fa-43a7-8e77-ffa48ea75b46/08-minimize-viewport.png "Minimize Viewport") and ![Maximize Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/681c7293-222f-44d4-8897-ef13d528b8e2/09-maximize-viewport.png "Maximize Viewport") buttons located in the top right corner of each Viewport.

## View Modes

The Unreal Editor viewports have a large number of visualization modes to help you see the type of data being processed in your scene, as well as to diagnose any errors or unexpected results. The more common view modes have their own hotkeys, but all can be accessed from the viewport within the **View Mode** menu.

Click image for full size.

Click image for full size.

The most commonly used view modes are shown here:

|   |   |   |
| --- | --- | --- |
| ![Viewmode Lit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/031b6a74-0a3a-41e2-b2f0-c5ab03817fa7/12-viewmode-lit.png "Viewmode Lit") | ![Viewmode Unlit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1406c8b9-f7ad-4066-acc7-38b8013d004d/13-viewmode-unlit.png "Viewmode Unlit") | ![Viewmode Wireframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2143e571-9339-403b-8e14-9599e4fc8717/14-viewmode-wireframe.png "Viewmode Wireframe") |
| Lit | Unlit | Wireframe |

See [Viewport Modes](/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine) for a listing and description of all available modes.

## Game View

**Game View** causes the Viewport to display the scene as it would appear in the game. This means that none of the editor-specific elements - such as the Actor icons - are shown. It gives you an easy way to see just how your level will look when you run it in the game.

 ![Game View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0982e26f-2aae-4962-9f70-2f4be74bd73c/15-game-view.png "Game View") ![Game View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fc938c7-e28e-40db-a829-df7beb1c6e4d/16-game-view-1.png "Game View")

**Drag the slider to toggle Game View.**

To enable Game View, simply press the **G** key (by default) with the Viewport focused or choose the **Game View** option from the Viewport Options menu:

Click image for full size.

## Immersive Mode

Viewports have another state in addition to maximized and minimized that they can be in called **Immersive Mode**. This refers to Viewport being maximized out to the full extents of the window containing the **Viewport** panel. When you have the Level editor maximized, this enables you to have your Viewport run in full-screen for a truly *immersive* editing experience!

To enable Immersive Mode, simply press the **F11** key (by default) with the Viewport focused or choose the **Immersive Mode** option from the Viewport Options menu:

Click image for full size.

You can restore the Viewport to normal using the same procedure above or by pressing the ![Restore Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c7c044c-6738-488c-9f45-683cd2a6e16a/19-restore-viewport.png "Restore Viewport") button located at the top right of the Viewport when in Immersive Mode.

     ![Immersive Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7499aef-fa79-42fd-a198-f8f9a140e6b3/20-immersive-mode.png "Immersive Mode") ![Immersive Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f1e75ad-ba3b-421e-9926-d060e9226176/21-immersive-mode-1.png "Immersive Mode") ![Immersive Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/692498f6-211f-4c67-b547-9a2a0b3fa63b/22-immersive-mode-2.png "Immersive Mode") ![Immersive Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f3aea61-8b58-435f-8bfc-35ee3e0b87e3/23-immersive-mode-3.png "Immersive Mode") ![Immersive Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06373750-a4e8-470b-9680-8cb9341ef9ed/24-immersive-mode-4.png "Immersive Mode") ![Immersive Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b59a3c92-8913-47ea-ba52-6abf0e03c937/25-immersive-mode-5.png "Immersive Mode")

**Drag the slider to see Immersive Mode in action!**    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39727c56-014c-449e-b6bd-29977164f70b/mac_immersive_1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/998cf460-964c-44c8-8faa-79b85e6cf16c/mac_immersive_2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5140fa21-2039-475d-9e32-31cdd87d363e/mac_immersive_3.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2683ae7b-2779-441e-bddb-6926d950f854/mac_immersive_4.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2260eb90-d877-4819-993c-6bbd5802dad3/mac_immersive_5.png)

**Drag the slider to see Immersive Mode in action!**