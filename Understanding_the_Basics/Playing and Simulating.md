# Playing and Simulating

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/playing-and-simulating-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/playing-and-simulating-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:41

---

You can instantly preview your game inside Unreal Editor at any time, without needing to build it into a standalone application first. This can help you quickly iterate on gameplay and asset tweaks and see how your game changes as a result.

There are two ways to preview your game in **Unreal Engine**:

-   **Play In Editor** (PIE), which you can access from the **Play** button on the **Main Toolbar**.
    
-   **Simulate In Editor** (SIE), which you can access from the **Play** drop-down menu or by using the **Alt + S** on Windows keyboard shortcut (or **Option + S** on macOS).
    

The key difference between playing and simulating in the Editor is that **playing** will always start the game at the Player Start location and give you control of the player character. **Simulating** doesn't move the Camera and doesn't spawn a player character.

You can toggle between Play In Editor and Simulate In Editor sessions as needed.

For this tutorial, we have created a new project using the **Blueprint Third Person** template with **Starter Content** enabled. If you have not created a project based off a template before or are not sure how to enable Starter Content, refer to the [Creating a New Project](/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine) page to learn how to do this.

## Play In Editor (PIE)

This section will show you how you can use **Play In Editor** to play your game.

1.  With the **Blueprint Third Person** Template Project open, from the **Main Toolbar**, click the **Play** button.
    
    ![Play button on the Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9069d523-89f7-41c6-84c3-5a2f497ba140/main-toolbar-play.png)
    
    After you click the **Play** button, the game should start and you should see the character in the Level Editor Viewport.
    
    ![A third-person project in Play mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23508466-6cb9-4907-a7e1-dfc4269b338b/play-mode.png)

You will also see the text "Click for Mouse Control" flash briefly in the upper-left corner of the Level Viewport. When playing inside the Level Viewport, you must click inside the viewport to assign mouse control to the playable character.

1.  Click or right-click in the Level Editor Viewport.
    
    You will see the text "Shift+F1 for Mouse Cursor" appear in the upper-left corner of the Level Editor Viewport. If you want to give mouse control back to the Editor itself, press **Shift + F1** (Windows) or **Shift + fn + F1** (macOS).
    
    While the game is running, you can use the **WASD** keys for movement, **Spacebar** to jump and **Mouse** movement to move the camera.
    
2.  During the Play session, the **Main Toolbar** will change to provide additional controls.
    
    ![Main Toolbar during PIE](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5548705-6ac4-4888-acaf-eb7586041317/main-toolbar-play-options.png)
    
    Left to right, the controls are:
    
    -   **Pause**: Pauses the game.
    -   **Frame Skip**: This will be grayed out and unavailable while your game is running in this mode.
    -   **Stop**: Ends the Play session.
    -   **Eject**: Releases control of the playable character and switches to mouse cursor controls.
    
    You can click inside the Level and use the mouse to move around, or you can use the Editor to make changes to your Level.
    
3.  While the game is still running in PIE mode, press **Shift + F1** to unlock the mouse cursor from the Level Viewport, then click **Pause** to pause the game.
    
    You will notice that the first two buttons on the **Main Toolbar** look slightly different:
    
    ![Controls available while PIE is paused](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ae7e48f-70f9-4362-8cf4-440278dc798c/main-toolbar-pause-options.png)
    
    -   The **Play** button has been replaced with a **Resume** button. Clicking the **Resume** button will resume the game simulation inside the Level Viewport.
    -   The **Frame Skip** button is now available. Clicking it will advance gameplay by 1 frame (you can see this easily if you have animated objects, such as particle emitters).
    
    The **Stop** and **Eject** buttons have the same functionality as described in step 3 above.
    
4.  While the game is still paused, **click** the **Eject** button on the **Main Toolbar**.
    
5.  **Left-click** the text in the Level Viewport to select it. Then in the **Details** panel, change its **Text** value to something else.
    
    ![Changing the value of a text Actor during PIE](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a07b7d87-0eab-4b72-ab69-9db7588fed1b/change-text.png)
    
    Press **Enter** to confirm the new text. Your changes will immediately appear in the Level Viewport.
    
6.  From the **Main Toolbar**, click the **Possess** button (1), then click the **Resume** button (2).
    
    ![Possess and Resume buttons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/143dd364-2fa9-4c64-951a-7b1fd79045fc/main-toolbar-possess-resume.png)
7.  Note that the text in the Level has changed from its default value. This method is useful for changing and testing different values for the Actors in your Level during gameplay.
    
    ![New value of the text Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4498f16-a6ea-438e-a9bc-4d779feab141/new-text-value.png)
    
    Changes you make to Actors in the Level using this method are **not** saved by default. To learn how to keep these changes, follow the steps below.
    
8.  Press **Shift + F1** to regain mouse control. Then, from the main toolbar, click the **Eject** button.
    
9.  With the game still running in the Level Viewport, **right-click** the text Actor. Then, from the pop-up menu, select **Keep Simulation Changes**.
    
    ![Keep Simulation Changes menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63336ab7-ac0a-4234-b85e-efd1085b5b04/keep-simulation-changes.png)
    
    Alternatively, **left-click** the text Actor to select it, then press **K** on your keyboard.
    
10.  Press **Esc** to stop the play session. Note that your changes have been saved.
    

### Play Modes

When you start a PIE session, you can select from several different **Play Modes**. This section describes what they are and how to access them.

1.  From the **Main Toolbar**, click the vertical ellipsis button.
    
    ![Play Options button on the Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4b32db1-96e1-4fae-954f-9b2ee753cc16/main-toolbar-play-modes-button.png)
    
    This will open the **Play Options** menu.
    
2.  Choose from one of the following options:
    
    -   **Selected Viewport**: Launches the game inside the currently selected [Viewport](/documentation/en-us/unreal-engine/editor-viewports-in-unreal-engine).
    -   **Mobile Preview ES3.1 (PIE)**: Launches the game in a standalone version outside of the Editor and provides additional tools used to mimic devices as closely as possible.
    -   **New Editor Window (PIE)**: Launches the game within the Editor; however, it creates a new standalone window, leaving the Level Viewport the same.
    -   **VR Preview**: Launches a preview of the game on a connected VR device.
    -   **Standalone Game**: Launches the game in a standalone version outside of the Editor
    
    The default setting is **Selected Viewport**.
    

### PIE Console

The **PIE Console** is an in-game console where you can enter commands to display performance data, enable and disable Unreal Engine features, and much more.

To open the PIE console, press the **tilde** (~) key while playing the game in PIE mode.

![Play In Editor Console](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3593d7d2-5bca-4702-a339-3a4889fea4de/pie-console.png)

Press the **tilde** key again to expand the console, and press **tilde** a third time to close it.

The PIE console behaves the same as the Unreal Editor's main console. When you start typing, it automatically tries to complete the console command you are trying to enter.

A great use case for the PIE Console is to profile a project's performance. To learn more, refer to the [Stat Commands](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine) page.

## Simulate In Editor (SIE)

In this section, we will take a look at **Simulate In Editor** and how to simulate your game.

1.  With your project open, inside the **Content Browser**, open the **Starter Content > Props** folder.
    
2.  Click and drag the **Material Sphere** prop into the Level, just above the stairs.
    
    ![Dragging a sphere into the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f91ffac-5c8d-4c34-9555-5a6099e3e5da/drag-sphere-into-level.png)
    
    To find the **Material Sphere** prop quickly, use the **Search Box** inside the Content Browser.
    
3.  Click the sphere to select it, then click the arrows of the [Translation widget](/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine) to move the sphere up above the stairs, as shown in the screenshot below.
    
    ![Position the sphere as shown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2b97871-6bdd-4682-99a8-46a319209044/sphere-position.png)
4.  In the **Details** panel for the sphere, scroll down to the **Physics** section and enable the **Simulate Physics** checkbox.
    
    ![The sphere's Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e292ace4-d483-4ebd-87e0-7f9de50ee928/sphere-details-panel.png)

When you start to simulate (or play), the sphere now has physics and should fall to the ground.

1.  Press **Alt + S** (Windows) or **Options + S** (macOS) to Simulate in the Editor.
    
    ![Sphere with physics enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f17b9a1-d400-43c1-9cd3-0b9406c80d7a/sphere-falling.gif)
    
    Note that, although there is no player character in the Level, the game starts and the sphere falls to the ground.
    
2.  Press **Esc** to stop the simulation. Note that the **Main Toolbar** now displays a **Simulate** button instead of the **Play** button. This button will always reflect the most recently selected **Play** or **Simulate** mode that ran for this project.
    
    ![Simulate button on the Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a440e6e8-35fd-439e-b1ea-6bb1d0e7ee86/main-toolbar-simulate-button.png)
3.  Click the **Simulate** button again, then immediately click the **Pause** button.
    
4.  From the **Main Toolbar**, click the **Frame Advance** button to step through the simulation. Every time you click the button, the sphere should move further down.
    
    ![Advancing the simulation one frame at a time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ebbfdb5-7f03-40d4-88fe-bd81f751cce9/sphere-falling-frame.gif)