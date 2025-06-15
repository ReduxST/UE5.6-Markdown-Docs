# Using the Virtual Scouting Tools

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-virtual-scouting-tools-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-virtual-scouting-tools-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:16

---

The Virtual Scouting tools are similar to editor modes in the [Level Editor](/documentation/en-us/unreal-engine/level-editor-modes-in-unreal-engine). You can only select one tool at a time, except for the Navigation tool, which is always available.\`

## Main Menu Palette

Use the Main Menu Palette to select tools, adjust the settings of each tool, and undo and redo your actions.

### Controls

To view the Main Menu Palette, pull and hold the trigger on your left motion controller (or right motion controller if you have set handedness to **Left**). The Main Menu stays visible as long as you keep the left trigger pulled.

![Viewing the Main Menu Palette](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b09e7594-8488-41e6-a6fe-d2c8279c4efe/main-menu-view.gif)

To interact with the Main Menu, use your right motion controller to point with the green cursor and the right motion controller trigger to click and/or drag on the Main Menu UI elements.

![Interacting with the Main Menu Palette](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/263707d5-27a1-436f-aea3-4ed89f256f09/main-menu-interact.gif)

### Settings

The Main Menu has the following sections:

-   Section 1: Icons for each tool. Clicking these will switch to the selected tool.
-   Section 2: Each tool's specific settings.
-   Section 3: Undo/Redo and the settings menu.

![Main Menu Palette settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a40bfc12-990a-4d1f-85f4-ee0af8ff69d0/main-menu-settings.png)

## Navigation Toolbar

Use the **Navigation** tool to move around your level. You can adjust settings for movement speed and rotation in the Main Menu Palette.

Navigation is always available while you use other tools. Navigation uses the left controller and sometimes the right controller, depending on whether the selected tool overrides the navigation input controls.

### Controls

The table below lists the controls for navigation.

| Control | Action | Preview |
| --- | --- | --- |
| **Right Thumbstick, all directions (pink)** | Fly-in stick direction. | ![VR preview of Fly-in](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50057705-fb62-42c6-bb22-385a3999f245/fly-in.gif) |
| **Left Thumbstick, on Y-axis (pink)** | Fly-in stick direction. You can use both left and right thumbsticks to fly faster. |   |
| **Left Thumbstick (pink)** | Snap rotate, or smooth rotate if **Use Smooth Rotation** is selected. | 
![VR preview of snap rotate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ddd72a5-0417-43e5-80c4-559f31976ecf/snap-rotate.gif)

Snap rotate



 |
| **Left or Right side grip (Yellow button)** | Drag. Press and hold to drag in the direction of your hand movement. | ![VR preview of drag](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/227b9481-52b1-48ea-a28a-cecbd2c13ee5/drag.gif) |
| **Left and Right side grips (both yellow buttons together)** | 

Move the controllers together or apart to modify your size in the size in the scene.

Move the controllers like you're holding a wheel to rotate yourself in the scene.



 | 

![VR preview of scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e39fda2-77d2-4f93-b92b-b3c41f833cf7/scale.gif)

Change size

![VR preview of rotate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a14ef42-3790-4d76-a5cb-358a9fa004c8/smooth-rotate.gif)

Rotate



 |
| **Blue Button** | 

Press and hold to summon the teleporter. Release to teleport to the end of your laser pointer.

If **Use Teleport Rotation** is enabled you will be able to roll your wrist and adjust the direction you will be facing when you finish teleporting.



 | 

![VR preview of teleport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2af03a46-2629-42c2-b40c-e56fa122eb0b/teleport.gif)

Teleport

![VR preview of teleport with rotation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b615661e-8814-4ca0-817d-60dd80c9e2a5/teleport-rotate.gif)

Teleport with rotation



 |

### Settings

In the Main Menu Palette, you can change the fly and drag speed, whether to use snap-rotate or smooth rotation on the left thumbstick, and whether to use rotation from your wrist's roll axis (forward axis) when teleporting. You can also see a history of times that you've teleported in the scene.

![The Navigation tool settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00828958-62aa-43d8-9607-bec19988d258/navigation-settings.png)

## Draw Tool

Use the **Draw** tool to draw on your scene (Laser Draw), draw in space (Free Draw), and delete your drawings.

### Controls

To draw on the scene, select the draw tool and pull the right trigger. Move the right controller to create a line, and release the trigger to stop drawing.

![VR preview of drawing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56556176-a964-4ff3-a320-b7ff287152c2/draw.gif)

### Settings

In the Main Menu Palette, you can switch between the three modes: **Laser Draw**, **Free Draw**, and **Delete**. You can also control the color, width, and spacing of the lines.

![The Draw tool settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bb4ddf3-eb29-4b53-a826-ae9eac10823f/draw-settings.png)

## Measurement

Use the **Measurement** tool to measure the distance between two points.

### Controls

To create measurements point the laser pointer, pull and hold the trigger and drag from the start position to the end point. The measurement updates as you drag.

![VR preview of measurement](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25cab771-dec4-4443-b168-fdffe230340b/measurement.gif)

### Settings

In the Main Menu Palette, you can modify the color of your measurements or swap the tool type. Use the **Persistent** type to create measurements that are visible to all users in a multi-user session and remain in the environment after you stop using the measurement tool. Use the **Temporary** type to make measurements that are only visible to you, and are removed as soon as you swap to another tool.

![The Controls tab in the Measurement settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ac654ee-79d7-467e-941a-2d5a18abeb96/measurement-controls.png)

The Measurement tool **List** tab displays all the measurements currently in the level. For each measurement, you can toggle its visibility, see a line from your location to the measurement, teleport to the measurement, and delete the measurement.

![The List tab in the Measurement settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1169f844-3ff3-4a50-9d04-115dab15b1ad/measurement-list.png)

## Environment Light

Use the Environment (**Env**) tool to control the placement of the **Sun** and **Moon** light in your level.

For this placement to work you must have two directional lights in your level and your Sun and Moon must have the following properties set:

-   `Atmosphere Sun Light` = `True`
-   `Atmosphere Sun Light Index` = `0` (for the Sun)
-   `Atmosphere Sun Light Index` = `1` (for the Moon)
-   `Forward Shading Priority` = `0` (for the Sun)
-   `Forward Shading Priority` = `1` (for the Moon)

### Controls

By default, the tool starts with the sun selected. To move the sun, point your laser pointer and pull the right-hand motion controller trigger. Hold the trigger and move your laser pointer, and the sun follows the direction of your pointer.

![VR preview of the Env tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/834e01b4-b239-405f-a723-e1275520bd25/sun.gif)

### Settings

In the Main Menu Palette, you can control the properties of the Sun and Moon lights, such as **Intensity**, **Temperature**, **Color**, and **Source Angle**, and also reset the properties to default values.

![The Env tool settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b958895-6c4d-46f6-b96c-d5b57a77116d/env-settings.png)

## Viewfinder

Use the **Viewfinder** tool to take screenshots of the environment with an on-screen camera. You can control various properties of the shot, such as aperture and focus.

### Controls

You can modify properties, take screenshots, and create camera objects using the controls in the following table.

| Control | Action |
| --- | --- |
| **Green Button** | Summons on-screen lens controls. |
| **Trumbstick (left/right)** | Swaps the controlled property (Lens, Aperture, Focus). |
| **Thumbstick (up/down)** | Modifies the controlled property. |
| **Blue Button** | Captures a screenshot. |
| **Trigger + Blue Button** | Creates a camera object. |
| **Trigger (hold)** | Picks up a camera when overlapping it with the laser pointer. Camera must be near the motion controller. |

![Using the on-screen lens controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/653a59b7-b614-4083-9238-d30cb2a98e8c/viewfinder.gif)

### Settings

In the Main Menu Palette, use the **Lens** tab to change settings for the lens, such as **Exposure**, the type of **Lens**, and **Iris**.

![The Lens tab in the Viewfinder settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/492d8360-e047-41df-8d6f-3f9a9715c3f3/lens-tab.png)

Use the **Monitor** tab to pick up and drop the monitor, as well as change monitor settings like **Filmback** and **Mask**.

![The Monitor tab in the Viewfinder settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77314f7d-c6f6-4422-89a6-af49da237819/monitor-tab.png)

Use the **Camera** tab to view a list of created camera objects and delete them.

![The Camera tab in the Viewfinder settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a570d00d-9ea2-4b0e-91b1-6706109aa6c2/camera-tab.png)

Screenshots are saved to your `/[ProjectName]/Saved/Screenshots/` directory.

## Sequencer

Use the Sequencer tool to load a level sequence and control playback.

### Controls

To open a sequence, click the **Open** button next to its thumbnail in the Main Menu Palette.

![The Open button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a55702a9-ec0c-43b7-80ff-1e5d9553b13f/sequencer.png)

The level sequence opens in the editor and a small console widget appears above your right motion controller.

In a multi-user session, to make the level sequence open for the other users, enable the `Concert.EnableOpenRemoteSequencer` variable.

To close the sequence, click the **Close** button with your laser pointer.

When a sequence is open, you can use the controls in the following table.

| Control | Action |
| --- | --- |
| **Green Button** | Stop/start playback |
| **Right Thumbstick (left/right)** | Scrub backward/forward |
| **Right Trigger + Move (left/right)** | Scrub backward/forward |
| **Right Thumbstick Button** | Drop/Pickup Sequence console |

### Settings

In the Main Menu Palette, the Sequencer tool has **Use Collection Filter** set to true by default. Use the setting to curate which Level Sequences are available in Virtual Scouting. If **Use Collection Filter** is set to false, then all Level Sequences in the project are visible to the Sequencer tool.

To create a collection of sequences for Virtual Scouting, follow these steps:

1.  In the Content Browser, go to **Collections** and click the **Add (+)** button.
2.  Name the collection.
3.  Drag some Level Sequences into the collection.
    
    ![Level sequences in a collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca5cb4bb-c031-4abf-9543-e5419fbb73e2/level-sequences.png)
4.  In **Project Settings** > **Virtual Scouting Settings**, input the name of your collection into the **Sequence Tool Collection** field.
    
    ![The Sequence Tool Collection field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b369855-b3b2-433c-a29c-5369e939a9b5/sequence-tool-collection.png)

## Gaffer

Use the **Gaffer** tool to create spot and area (or "rect") lights.

### Controls

| Control | Action | Preview |
| --- | --- | --- |
| **Right Trigger** | 
1.  Creates a new light (if no light is created yet).
2.  Moves the light (if you hit a light's sphere collider with the laser pointer).
3.  Moves the selected light's point of interest (if your laser pointer hits any other location that is not the light's collider sphere).



 | 

![Creating and placing a light in VR](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3bb52a5-2c2b-4c13-b221-72497a3f06bc/create-light.gif)

Creating and placing a light

![Moving a light in VR](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d3c98c1-32d6-4ef8-a77a-35111fb561e8/move-light.gif)

Moving a light

![Moving a light's point of interest in VR](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/732e1095-68ab-4650-b737-7511cf2ab888/move-light.gif)

Moving a light's point of interest



 |
| **Thumbstick (up/down) + Right Trigger Held** | Pulls or pushes the light along your laser pointer. |   |
| **Thumbstick Button** | Swaps from 3D control of the light position to the light sticking to any collision geometry. |   |

### Settings

In the Main Menu Palette, you can select whether to create a **Spot Light** or an **Area Light**.

![The New Light tab in the Gaffer settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8cc7b029-0f56-4efd-802d-8e1c7c893843/new-light-tab.png)

The **All Lights** tab has buttons to toggle visibility, solo, delete, and select a light. If you hover over a light's name, a line appears in the environment pointing to the light you're highlighting.

![The All Lights tab in the Gaffer settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b408f56-a5be-475b-bad9-0c4f2dfc838d/all-lights-tab.png)

When you select a light you can modify its properties using the sliders. You can control the following properties:

-   **Intensity**
-   **Attenuation**
-   **Cone Angle**
-   **Source Size**
-   **Width**
-   **Height**
-   **Barndoor angle**
-   **Color Temperature**
-   **Color**

![The settings for an individual light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/769ac2e2-6c91-4050-9c61-61f8089a8cbd/light-settings.png)

## Grab Tool

Use the **Grab** tool to manipulate the selected actors in the environment with a transform Gizmo.

![Using the Grab tool in VR](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d9b0877-ff92-4445-81d7-7231905bbf09/grab.gif)

### Controls

To manipulate actors and gizmos, use the controls in the following table.

| Control | Action |
| --- | --- |
| **Right Trigger** | Selects an Actor. |
| **Right Trigger** | Moves the selected Gizmo handle. |
| **Green Button** | 
Swaps the Gizmo mode between the following modes:

-   Move
-   Rotate
-   Scale
-   Combined
-   Hidden



 |
| **Blue Button** | Swaps the Axis between Local and World alignment. |

### Settings

Use the Main Menu Palette to change the Gizmo between local and world space, swap between modes, duplicate or delete a selected actor, or reset the selected actor's rotation or scale back to default.

![The Grab tool settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a650f826-3b02-4464-b8ab-b28415fbb27d/grab-settings.png)

## Content Placement Tool

Use the **Content** (or **Placement**) tool to place static and skeletal meshes and Blueprints in your level. Select an asset from the Palette menu. This will spawn a preview copy of the asset attached to your laser pointer. Pull the trigger again to drop the asset into the level.

![Using the Placement tool in VR](content.gif)(convert:false)

### Controls

| Control | Action |
| --- | --- |
| **Right Trigger** | Selects an asset from the Main Menu Palette. |
| **Right Trigger** | Spawns the placed asset in your level. |
| **Right Thumbstick (left/right)** | Rotate the object while placing. |
| **Right Thumbstick (up/down)** | Move the object away or towards your controller when in free placement mode. |
| **Right Thumbstick Button** | Swap between surface snapping mode and free placement mode. |

### Content Browser

In the Main Menu Palette, under **Content**, you can use the **SM** (static meshes), **SKM** (skeletal meshes), and **BP** (Blueprints) buttons to browse assets of those types in the environment.

![List of static meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b8cec5e-8a99-4e73-9da5-5c4230032c86/sm-button.png) ![List of skeletal meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c280559-b93e-4901-a8f3-40ed7838b3a1/skm-button.png) ![List of Blueprints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a27101f2-7f06-4539-ad6c-1e692e77dd56/bp-button.png)

### Settings

In the Main Menu Palette, under **Content**, click **Options** to toggle the following settings:

-   **Collection Filter** - Whether the assets listed come from the Placement Tool collection or all of your project content.
-   **Use Smooth Rotation** - Whether to rotate smoothly the yaw axis of assets while you place them.
-   **Rotate to Surface Normal** - Whether the roll and pitch rotations snap to the surface of level objects.
-   **Use Grab Tool on Spawn** - Whether to automatically swap to the Grab tool after placing an asset. This lets you immediately use a transform gizmo on the asset.

![Settings for the Content Placement tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41627b02-e82d-49fc-95a1-ab17a7796f51/placement-settings.png)

#### Create a Placement Tool Collection

The Placement tool has **Collection Filter** set to **True** by default. Use a named collection to curate what assets are available for placement. If **Collection Filter** is set to **False**, then all mesh assets in the project are visible to the Placement tool.

To create a Placement Tool collection, follow these steps:

1.  In the **Content Browser**, go to **Collections** and click the **Add (+)** button.
2.  Name the collection.
3.  Drag some assets into the collection.
    
    ![A Placement tool collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efe82ee0-7b15-46b4-94fb-e447fcda8701/create-placement-collection.png)
    
    To learn more about content browser collections, see [Creating Collections](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine#creatingcollections).
    
4.  In **Project Settings** > **Virtual Scouting Settings**, input the name of your collection into the **Placement Tool Collection** field.
    
    ![The Placement Tool Collection field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f17e3169-bc6e-403d-b3e3-9327e5b267ad/placement-collection-setting.png)