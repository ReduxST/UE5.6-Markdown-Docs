# Level Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:01

---

The **Level Editor** provides the core level creation functionality for Unreal Editor. You will use it to create, view, and modify levels .You will modify a level mainly by placing, transforming, and editing the properties of [**Actors**](/documentation/en-us/unreal-engine/actors-and-geometry-in-unreal-engine).

In Unreal Editor, the scenes in which you create your game experience are generally referred to as [Levels](/documentation/en-us/unreal-engine/levels-in-unreal-engine). You can think of a level as a 3D environment into which you place a series of objects and geometry to define the world your players will experience. Any object that is placed in your world, be it a light, a mesh, or a character, is considered to be an Actor. Technically speaking, an Actor is a programming class used within the Unreal Engine to define an object that has 3D position, rotation, and scale data. Think of an Actor as any object that can be placed in your levels.

Click image for full size.

Creating levels begins by placing items in a map inside Unreal Editor. These items may be world geometry, decorations in the form of Brushes, Static Meshes, lights, player starts, weapons, or vehicles. Which items are added when is usually defined by the particular workflow used by the level design team.

## The Default Interface

Since the interface for Unreal Editor is highly customizable, it is possible that what you see may change from one launch to the next. Below, you can see the default interface layout.

Click image for full size.

1.  [Tab Bar and Menu Bar](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#tabbar)
2.  [Toolbar](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#toolbar)
3.  [Buttom Toolbar](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#bottomtoolbar)
4.  [Place Actor / Modes](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#modes)
5.  [Viewports](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#viewport)
6.  [Content Browser / Content Drawer](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine)
7.  [Outliner](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#outliner)
8.  [Details](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#details)

### Tab Bar

The Level Editor has a tab along the top with the name of the current level. Tabs from other editor windows may be docked alongside this tab for quick and easy navigation, similar to a web browser.

Click image for full size.

The name of the tab reflects the level currently being edited. This is a pattern consistent throughout the editor—tabs will be named after the current asset being edited.

To the right of the Tab Bar is the name of the current project.

### Toolbar

Click image for full size.

The **Toolbar** panel displays a group of commands, providing quick access to commonly used tools and operations.

See the [**Toolbar**](/documentation/en-us/unreal-engine/level-editor-toolbar-in-unreal-engine) page for descriptions Toolbar items.

### Menu Bar

The **Menu Bar** in the editor should be familiar to anyone who has used Windows applications previously. It provides access to general tools and commands that are used when working with levels in the editor.

Click image for full size.

The **Console** (**\`**) is a text field that allows special console commands to be entered that are recognized by the editor. The text field has an auto-complete feature that automatically lists all commands matching the characters in the field.

If are running Source Control, the button on the far right of the menu bar is indicates its status.

| Button | Name | Description |
| --- | --- | --- |
| 
![Button Source Control On](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f19a21ed-2da3-490c-b6a3-a8dca1a90a4b/05-button-source-control-on.png "Button Source Control On") = On ![Button Source Control Off](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44ec2b76-136f-447e-89a1-060a76818885/06-button-source-control-off.png "Button Source Control Off") = Off



 | **Source Control Status** | Mouse over the button for connection details. A green icon can be clicked to log in to your connection. A red icon indicates that source control is not in use. Perforce and Subversion are supported. See [Source Control documentation](/documentation/en-us/unreal-engine/using-source-control-in-the-unreal-editor) for details. |

### Modes

The **Level Editor** can be put into different editing modes to enable specialized editing interfaces and workflows for editing particular types of Actors or geometry.

To display a selection of modes, in the Level Editor Toolbar, open the **Modes** dropdown.

Click image for full size.

| Icon | Mode | Shortcut | Description |
| --- | --- | --- | --- |
| ![LE Tools Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1d07f1a-f488-4fec-8dd4-8d18d49ca60c/02-le-tools-select.png "LE Tools Select") | **Select** | **Shift + 1** | Activate [**Select** mode](/documentation/en-us/unreal-engine/select-mode-in-unreal-engine) to select Actors in your scene. |
| ![LE Tools Landscape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55d27e6b-a02d-47f2-aa67-37814d697388/03-le-tools-landscape.png "LE Tools Landscape") | **Landscape** | **Shift + 2** | Activate [**Landscape** mode](/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) to edit Landscape terrains. |
| ![LE Tools Foliage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28f5e52b-09ed-4fd7-b2ee-5e5f0a1585be/04-le-tools-foliage.png "LE Tools Foliage") | **Foliage** | **Shift + 3** | Activate [**Foliage** Mode](/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine) to paint instanced foliage. |
| ![LE Tools Mesh Paint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df3be5c6-e252-43b8-bafa-330a018bb9d9/06-le-tools-mesh-paint.png "LE Tools Mesh Paint") | **Mesh Paint** | **Shift + 4** | Activate [**Mesh Paint** mode](/documentation/en-us/unreal-engine/mesh-paint-mode-in-unreal-engine) to paint vertex colors and textures on Static Mesh Actors directly in the viewport. |
| ![LE Tools Modeling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a647c541-00dd-45af-a283-fe902381d85b/08-le-tools-modeling.png "LE Tools Modeling") | **Modeling** | **Shift + 5** | Activate **Modeling** editing mode. |
| ![LE Tools Fracture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68cc85ff-9422-48e0-acc7-8f1ef0a5c0bf/07-le-tools-fracture.png "LE Tools Fracture") | **Fracture** | **Shift-6** | Activate [**Fracture** mode](/documentation/en-us/unreal-engine/chaos-destruction-in-unreal-engine) to create destructible objects and environments. |
| ![LE Tools Brush](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2c16b49-0e88-4d10-b5a9-2630cd735ce9/05-le-tools-brush.png "LE Tools Brush") | **Brush Editing** | **Shift + 7** | Activate [**Brush Editing** mode](/documentation/en-us/unreal-engine/geometry-brush-actors-in-unreal-engine) to modify Geometry Brushes. |
| ![LE Tools Animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b77a4d70-7d30-4199-a42b-523479b030d1/09-le-tools-animation.png "LE Tools Animation") | **Animation** | **Shift + 8** | Activate **Animation** editing mode. |

**Modes** change the primary behavior of the Level Editor for a specialized task, such as moving and transforming assets in the world, sculpting landscapes, generating foliage, creating geometry brushes and volumes, and painting on meshes. Modes panels contain a selection of tools tailored to the selected editing mode.

Click image for full size.

The Landscape panel

You can close any panel by clicking the small "X" in the upper-right corner of the tab. You can also hide any panel by right-clicking on the tab, and then clicking **Hide Tab** on the context menu that appears. To reopen a panel that you have closed, click that panel's name on the **Window** menu.

### Viewport

The **Viewport** panel is your window into the worlds you create in Unreal Engine.

Click image for full size.

This panel contains a set of viewports, each of which can be maximized to fill the entire panel and offer the ability to display the world from one of three orthographic views (Top, Side, Front) or a perspective view giving you complete control over what you see and how you see it.

See [**Viewports**](/documentation/en-us/unreal-engine/editor-viewports-in-unreal-engine) for more information on working with viewports.

### Details

Click image for full size.

The **Details** panel contains information, utilities, and functions for the current selection in the viewport. It contains transform edit boxes for moving, rotating, and scaling Actors, displays all of the editable properties for the selected Actors, and provides quick access to additional editing functionality depending on the type of Actor(s) selected in the viewport. For example, selected Actors can be exported to FBX and converted to another compatible type. Selection Details allow you to view the materials used by the selected Actors, if any, and quickly open them for editing.

See the [**Details**](/documentation/en-us/unreal-engine/level-editor-details-panel-in-unreal-engine) page for a more complete overview and guide to using the **Details** panel in the Level Editor.

### Outliner

Click image for full size.

The **Outliner** panel displays all of the Actors within the scene in a hierarchical tree view. You can select and modify Actors directly from the **Outliner**. Use the Info dropdown menu to display an additional column that shows Levels, Layers, or ID Names.

See the [**Outliner**](/documentation/en-us/unreal-engine/outliner-in-unreal-engine) page for details on using the **Outliner**.

### Bottom Toolbar

Click image for full size.

Contains shortcuts to the Command Console, Output Log, and Derived Data functionality. Also displays source control status.

See the [**Toolbar**](/documentation/en-us/unreal-engine/level-editor-toolbar-in-unreal-engine) page for descriptions Toolbar items.

### Layers

The **Layers** panel allows you to organize Actors in your Level.

Click image for full size.

Layers provide the ability to quickly select as well as control visibility of groups of related Actors. You can use your layers to quickly un-clutter a scene leaving only the geometry and Actors that you are working with. For example, you might be working on a building that has multiple levels but is comprised of many modular parts. By assigning each floor to a layer, you can hide each of the floors you are not working on making the top view much more manageable.

See the [Layers Panel](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine) page for details on using the **Layers** panel.