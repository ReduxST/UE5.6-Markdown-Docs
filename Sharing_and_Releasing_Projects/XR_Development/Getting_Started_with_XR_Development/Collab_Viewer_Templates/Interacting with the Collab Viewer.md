# Interacting with the Collab Viewer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:23

---

This page describes the different ways you can control the camera and interact with content at runtime in the Collab Viewer Templates, in both [desktop](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#desktopcontrols) and [VR](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#vrcontrols) modes.

## Desktop Controls

### Toolbar

You can use the toolbars at the top of the window to teleport, switch navigation modes, and save the current session.

| Icon | Description |
| --- | --- |
| ![Voice Over IP](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9febaf98-ac2e-44e0-9575-352a2f943995/voip.png "Voice Over IP") | Voice Over IP is enabled by default in the project. Toggle it on or off by clicking this icon. |
| ![Activate Fly mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34f4b771-0f8a-403a-a5d6-bfdff9e0a9cc/flymode.png "Activate Fly mode") | 
Activates Fly mode. In Fly mode, you can fly freely around the scene in all directions. In this mode, you pass through all geometry regardless of collision settings on the Actors. See [Fly Mode Controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#flymodecontrols).

Returning to Walk mode after being in Fly mode re-enables gravity. Depending on your location, you will either free-fall until you reach the ground, or you will snap to the closest ground surface.



 |
| ![Activate Walk mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e064669-538d-4cbf-bcc0-cd250388b422/walkmode.png "Activate Walk mode") | Activates Walk mode. In Walk mode, you're held down to the ground by gravity. As you walk around the scene, you collide with any objects in the Level that are set up with collision volumes. See [Walk Mode Controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#walkmodecontrols). |
| ![Activate Orbit mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc1d0de7-6fc8-45f7-a8ab-856d35c93222/orbitmode.png "Activate Orbit mode") | Activates Orbit mode. In Orbit mode, you select a point of interest in the Level. Then, as you rotate the camera, you move around that point of interest, keeping it in the center of the screen. See [Orbit Mode Controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#orbitmodecontrols). |
| ![Activate VR mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1082d6b1-3e78-4b5a-abf9-fa57d719d755/vrmode.png "Activate VR mode") | Activates VR mode, if you have a supported VR headset installed and working. See [VR controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#vrcontrols). |
| ![Save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/675f352b-79c8-4d3f-a476-2f0cd2895379/savestate.png "Save") | Saves the current state of the viewer, including annotations and measurements. See [Saving and Loading a Session](/documentation/en-us/unreal-engine/saving-and-loading-a-session-in-unreal-engine) |

Switch between modes quickly with the following hotkeys:

-   Activate Fly mode by pressing **U** on your keyboard.
-   Activate Walk mode by pressing **I** on your keyboard.
-   Activate Orbit mode by pressing **O** on your keyboard.
-   Activate VR mode by pressing **P** on your keyboard.

### Common Desktop Controls

The following controls work the same way in all desktop movement modes: Fly mode, Walk mode, and Orbit mode.

| To... | Do... |
| --- | --- |
| Activate the laser pointer | Move the mouse cursor to the object you want to highlight, then left-click. |
| Open the Interaction Menu | Press **Spacebar**. For details on using the items in this menu, see [The Interaction Menu](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#theinteractionmenu). |
| Move to a preset bookmark location | Press any number key from 0-9 that has been mapped to a specific bookmark location. See [Working with Bookmarks in the Collab Viewer Template](/documentation/en-us/unreal-engine/working-with-bookmark-in-the-collab-viewer-template-in-unreal-engine). |
| Exit the application | Press **Esc**. |

### Fly Mode Controls

In addition to the [Common Desktop Controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#commondesktopcontrols), the following controls work in Fly mode.

| To... | Do... |
| --- | --- |
| Look around the world from your current position | Right-click and drag. |
| Move forward, to the left, backward, or to the right from your current position | Hold the right mouse button and press **W**, **A**, **S** and **D**. |
| Move straight up or down (along the world's global Z axis) | Hold the right mouse button and press **Q** and **E**. |

### Walk Mode Controls

In addition to the [Common Desktop Controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#commondesktopcontrols), the following controls work in Walk mode.

| To... | Do... |
| --- | --- |
| Look around the world from your current position | Right-click and drag. |
| Move forward, to the left, backward, or to the right from your current position | Hold the right mouse button and press **W**, **A**, **S** and **D**. |

### Orbit Mode Controls

In addition to the [Common Desktop Controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#commondesktopcontrols), the following controls work in Orbit mode.

| To... | Do... |
| --- | --- |
| Orbit the camera around the point of interest | Right-click and drag. |
| Change the camera's point of interest to a new location, remaining at the current zoom level | Middle-click. |
| Choose a new point of interest, and zoom to fit the selected object in the viewport | Double middle-click. |
| Zoom in or out on the current point of interest | Turn the mouse wheel. |
| Pan the camera left, right, up, or down | Middle-click and drag. |

## VR Controls

| To... | Do... |
| --- | --- |
| Teleport to a new location | 
-   **Oculus Touch:** Press and hold the B button on the right controller or the Y button on the left.
-   **Valve Index Controller:** Press and hold the B button on either controller.
-   **HTC Vive Controller:** Press and hold the Grip button on either controller.

You'll see an arc emitted from your controller, and a target marker superimposed on the ground. The target marker represents your Teleport location. Move your controller in real world space to place the marker as close as possible to the place you want to move.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/726fcd71-7ba3-4ffa-85c0-b8b8bd1e9f7b/vr_teleport.gif)

The pointer of the marker represents your facing direction after the teleport. You can control this facing direction by rotating your wrist. Release the button you're holding to complete the teleport.



 |
| Activate the laser pointer | Press the main trigger button on either controller, and move the controller around in real world space. |
| Open the Interaction Menu | Push the right-hand controller thumbstick forward or back. Use the thumbstick to highlight the option you want to activate, then press the thumbstick button to confirm your choice. For details on using the items in this menu, see [The Interaction Menu](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#theinteractionmenu). |
| Exit the application | Press **Esc** on your computer keyboard. |

## The Interaction Menu

The Interaction Menu offers you several commands and modes for interacting with the content in your scene at runtime.

![The Interaction Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3c766c6-cc70-4123-839f-7074425fbe96/collabviewer-server-interactionmenu.png "The Interaction Menu")

To open the Interaction Menu, press **Spacebar** in any desktop mode. See [VR Controls](/documentation/en-us/unreal-engine/interacting-with-the-collab-viewer-in-unreal-engine#vrcontrols) for how to open the menu on your VR controller.

| Command | Description |
| --- | --- |
| **Transform** | Use the options in the **Transform** sub-menu to move selected objects around in the scene. |
| **Transform > Move** | Activates the **Transform Move** mode. When you select an object in the scene with your laser pointer, you can drag the laser pointer to move the selected object around in 3D space. |
| **Transform > Reset** | Activates the **Transform Reset** mode. When you select an object in the scene with your laser pointer, you instantly reset the selected object to its original position and rotation. |
| **Transform > Reset All** | Instantly returns all objects in the scene to their original positions and rotations. |
| **Annotation** | Use the options in the **Annotation** sub-menu to add and remove annotations. See [Annotating in the Collab Viewer](/documentation/en-us/unreal-engine/annotating-in-the-collab-viewer-in-unreal-engine). |
| **Annotation > Paint** | Activates the **Annotation Paint** mode. While this mode is active, you can paint on a grid. |
| **Annotation > Delete Stroke** | Activates the **Annotation Delete Stroke** mode. While this mode is active, you can select a paint stroke with your laser pointer to delete it. |
| **Annotation > Annotate Text** | Activates the **Annotate Text** mode. While this mode is active, you can place, edit, and delete 2D text labels. |
| **Snapshot > Take** | Select to take a snapshot. Snapshots are saved as .PNG files in the `YourProjectName/Saved/Snapshot` sub-folder of the collaborative view package. |
| **Xray** | Use the options in the **Xray** sub-menu to apply and remove a see-through Material to selected objects in the scene. |
| **Xray > Apply** | Activates the **Xray Apply** mode. While this mode is active, any object you select in the scene with your laser pointer gets the see-through Material applied to it. |
| **Xray > Isolate** | Activates the **Xray Isolate** mode. While this mode is active, and you select an item in the scene with your laser pointer, the see-through Material is applied to all *other* Actors in the same hierarchy as the one you select. |
| **Xray > Reset All** | Instantly removes the see-through Material from all objects in the Level, returning them to their original Materials. |
| **Measurement** | Use the options in the **Measurement** sub-menu to add and remove measurements. See [Measuring in the Collab Viewer](/documentation/en-us/unreal-engine/measuring-in-the-collab-viewer-in-unreal-engine). |
| **Measurement > Add** | Activates the **Measurement Add** mode. While this mode is active, a measurement is drawn between each pair of points that you select. |
| **Measurement > Delete** | Activates the **Measurement Delete** mode. While this mode is active, you can select a measurement with your laser pointer to delete it. |
| **Measurement > To Centimeter** | Use this option to set your unit of measure to centimeters. |
| **Measurement > To Meter** | Use this option to set your unit of measure to meters. |
| **Scale** | Use the **Scaling** mode to change your world scaling. Default is 1:1 |
| **Bookmark** | Opens a list of all Bookmarks in the current Level. Select any Bookmark in the sub-menu to teleport to its viewpoint. See also [Working with Bookmarks](/documentation/en-us/unreal-engine/working-with-bookmark-in-the-collab-viewer-template-in-unreal-engine). |
| **Bookmark > Create Bookmark** | Use this option to create a new Bookmark during runtime. |
| **3D Cut Plane** | Use the options in the **3D Cut Plane** sub-menu to select a section of geometry to remove. |
| **3D Cut Plane > Add/Edit** | Use this option to place or transform the 3D Cut volume. |
| **3D Cut Plane > Remove** | Use this option to remove the 3D Cut volume. |
| **3D Cut Plane > Include / Exclude** | Use this option to toggle between removing the geometry inside or outside the 3D Cut volume. |

When an interaction mode is active, such as **Xray Apply**, the name of the mode appears in the lower right of the viewport.

## 3D Cut Operation

You can cut geometry based on a 3D cube volume, selecting whether to preserve the geometry inside or outside of the volume. The 3D cube can be translated, rotated, and scaled. It also functions with geometry loaded at runtime, the material of geometry intersecting the volume will be switched temporarily to a custom grey material which supports the operation.

![3D cut removing inside](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ba762a5-8002-4a09-b6c5-7da9015c043d/3d-cut-internal.png)

A cutting volume that removes the inside of the volume.

![3D cut removing outside](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6530efa9-32f8-4ef8-abf1-46ac6af811d6/3d-cut-external.png)

A cutting volume showing only what is inside of the volume.

## World Scaling

Each participant can now choose their own scale for the world. They can scale up to view and interact with a real scale model as if it was a mockup, or scale down for more precise movement to observe details. The scale affects the participants' displacement as well as their visual representation. The scaling function can be accessed directly from the HUD or from the Menu.

Click image to expand. The scale can be tuned with a slide bar in the menu and through direct keyboard input on the top HUD.

Click image to expand. The bottom left participant (blue) has a scale 10 times bigger than the world and other participants.

## Testing in VR in the Unreal Editor

When you launch a packaged or standalone version of the Collab Template with VR set up on your computer, you'll be able to switch to VR mode using the icon in the Toolbar.

However, if you want to use VR controls while testing your Project in the Unreal Editor, you'll need to follow these steps:

1.  Find the **BP\_CollaborativeViewer\_GameInstance** Asset in the Content Browser under *CollaborativeViewer/Blueprints/GameInstance*.
    
    ![BP_CollaborativeViewer_GameInstance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cd0b264-ae84-42a1-8bac-291933d4efdc/collabviewer-gameinstance.png "BP_CollaborativeViewer_GameInstance")
2.  Double-click the Asset to open it in the Blueprint Editor.
    
3.  In the **My Blueprint** panel, select the **NavigationMode** variable.
    
    ![NavigationMode variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6147af59-c6c7-402f-96a7-3ce9c4da406b/collabviewer-gameinstance-navigationmode.png "NavigationMode variable")
4.  In the **Details** panel, under the **Default Value** section, select **VR** for the **Navigation Mode** option.
    
    ![Game Instance Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5bb60dde-71eb-48e3-a183-6a402afe3e2d/collabviewer-gameinstance-vrmode.png "Game Instance Details panel")
5.  **Compile** and **Save** the Blueprint.
    
6.  To launch the preview, use the drop-down arrow next to the Play button in the Toolbar to select **VR Preview**.
    
    ![VR Preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/424a3581-7c07-4be2-b9fd-2a0fcdd9fcca/collabviewer-gameinstance-preview.png "VR Preview")

Remember to turn this setting back off before you package your application! If you don't, the resulting package will not work as you expect.