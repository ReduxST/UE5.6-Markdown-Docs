# Unreal Engine Interface and Navigation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-interface-and-navigation](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-interface-and-navigation)  
**Processed:** 2025-06-14 16:56:45

---

In this section of the guide, you’ll learn about the Unreal Engine’s editor interface and how you can use it to navigate the scene. 

## Unreal Editor Interface

This introduction to the **Unreal Engine interface** describes the most common **buttons**, **panels**, and **toolbars** you’ll interact with in the **Unreal Editor.** In this page, you’ll learn more about what they do and how you can use them. While some of these elements are generally the same across various parts of the engine, you should spend some time getting familiar with their general purpose and functionality, especially if you are new to developing projects with Unreal Engine. You can also follow links throughout this page for a deeper dive into how you can use them.

When you open the engine for the first time, the **Level Editor** opens. This provides the core creation functionality to the Unreal Editor and is used for designing and constructing levels and environments — it is where you’ll spend most of your time developing content for your project. There are different **Editors** in Unreal Engine used for different purposes. 

These are the primary parts of the level editor interface you’ll want to familiarize yourself with:

[![Unreal Editor Interface](https://dev.epicgames.com/community/api/documentation/image/2fdc451e-08f8-4532-9cf2-aaf7b88d827c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2fdc451e-08f8-4532-9cf2-aaf7b88d827c?resizing_type=fit)

| Number | Name | Description |
| --- | --- | --- |
| 
1

 | 

**Menu Bar**

 | 

Uses these menus to access common application actions, like saving, and creating new levels. You’ll also find options for opening editor windows and tools that are useful for specific functions like debugging and more. 

For more information on this panel, see the "Menu Bar" section of [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface).

 |
| 

2

 | 

**Main Toolbar**

 | 

Contains shortcuts for some of the most common tools and editors in Unreal Engine. Also includes options to enter **Play-in-Editor** mode — to run a game from the editor window — and options to deploy the project to other platforms for testing.

For more information on this panel, see the “Main Toolbar” section of [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface).

 |
| 

3

 | 

**Viewport Toolbar**

 | 

Includes common tools used to manipulate objects in the level by moving, rotating, and scaling them, as well as snapping tools for moving objects along a grid, rotation angle, or scaling amount. It also includes perspective and orthographic views along with debugging and visualization view mode and other settings you can use while working in the viewport.

For more information on the tools found in this toolbar, see [Viewport Toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar).

 |
| 

6

 | 

**Level Viewport**

 | 

A real-time editor window that displays content in your level, such as cameras, characters, game objects, lighting, and more.

For more information on this panel, see the “Level Viewport” section of [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface).

 |
| 

4

 | 

**Outliner**

 | 

Displays a hierarchical tree view of all content in the currently loaded level. Selecting objects in this list or directly in the level will display their properties in the Details panel.

For more information on this panel, see the “Outliner” section of [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface).

 |
| 

5

 | 

**Details Panel**

 | 

Displays various properties of selected actors in the scene, such as transform data for position in the level, rendering, mesh, physics options, and more. Listed properties depend on the asset selected.

For more information on this panel, see the “Details Panel” section of [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface).

 |
| 

7

 | 

**Content Drawer**

 | 

Opens a temporary Content Browser which will dismiss when it loses focus. The Content Browser is where any assets (textures, materials, skeletal and static meshes, Blueprints, and more) are stored in a folder structure.

For more information on managing and organizing content for your project, see [Content Browser](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-in-unreal-engine).

 |
| 

8

 | 

**Bottom Toolbar**

 | 

Contains shortcuts to the Command Console, Output Log, derived data cache systems, and revision control options.

For more information on this panel, see the “Bottom Toolbar” section of [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface).

 |

For a broader overview of the areas highlighted above and in the sections below, see the [Unreal Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface). 

### Level Editor Viewport Navigation and Selection

The Level Viewport is where you’ll spend most of your time working with your assets. This can include setting up a scene by dragging and dropping assets around, setting up characters for animations with Sequencer, changing lighting and post processing settings, and much more.

Navigating the viewport is similar to Maya or any other 3D application with a viewport, but there are some subtle and not so subtle differences. For a full list of navigation controls to familiarize yourself with, see the [Viewport Controls](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-controls-in-unreal-engine) page.

Below is a highlight of some of the common default controls:

| Name of Action | Control | Description |
| --- | --- | --- |
| Object Selection |  |  |
| --- | --- | --- |
| 
**Select Object**

 | 

LMB

 | 

Selects the object under the cursor, replacing currently selected objects, if there is one. 

 |
| 

**Select Multiple Objects**

 | 

Hold CTRL + LMB / Hold SHIFT + LMB

 | 

Adds the object under the cursor to selection when clicking on multiple objects. For editor lists, such as the Outliner, hold SHIFT and left mouse click to select all objects between two points in the list. 

 |
| Navigating the Viewport |  |  |
| --- | --- | --- |
| 

**Move Camera in a Direction**

 | 

Hold LMB + Drag Mouse in Direction

 | 

Moves the viewport camera forward or backward in the direction it is facing.

 |
| 

**Rotate Camera**

 | 

Hold RMB + Drag Mouse in Direction

 | 

Rotates the viewport camera to look in any direction from the current viewport camera location. 

 |
| 

**Pan Camera in a Direction**

 | 

Hold LMB + RMB + Drag Mouse in Direction

 | 

Pans the viewport camera in any direction from the current viewport camera location. 

 |
| Camera and Object Selection |  |  |
| --- | --- | --- |
| 

**Focus Object**

 | 

F

 | 

Move the camera to the selected object you want to focus attention on.

 |
| 

**Object Focus Orbit**

 | 

ALT + Hold LMB + Drag Mouse in Direction

 | 

Orbits the camera around a single pivot or point of interest, where the point of interest is the object you have selected and focused. 

 |
| 

**Dolly Camera Movement**

 | 

ALT + Hold RMB + Drag Mouse in Direction

 | 

Moves the camera towards or away from a single point of interest that is focused. 

 |
| 

**Track Camera Movement**

 | 

ALT + Hold MMB + Drag Mouse in Direction

 | 

Moves the camera in any direction from the current viewport camera location. This is similar to **Pan Camera** **in a Direction**.

 |

### Moving, Rotating, and Scaling Objects in the Viewport

Unreal Engine includes a set of **Transform Tools** to move, rotate, and scale selected objects in the level viewport. You can find these tools in the **Viewport Toolbar**. The active tool selected is highlighted in the viewport toolbar and you can look at the transform gizmo on the object to identify which transform tool is currently selected. 

[![Unreal Editor Transform Tools](https://dev.epicgames.com/community/api/documentation/image/54c85c56-dfd0-43ce-a654-94021515c845?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/54c85c56-dfd0-43ce-a654-94021515c845?resizing_type=fit)

Like other 3D applications, you can grab the axis or axes you want to move or scale. 

[![](https://dev.epicgames.com/community/api/documentation/image/adf3d5a5-d618-4c83-ae36-ff87c4c0c182?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/adf3d5a5-d618-4c83-ae36-ff87c4c0c182?resizing_type=fit)

Use the following controls to: 

| Name of Action | Control | Description |
| --- | --- | --- |
| 
**Cycle Transform Tools**

 | 

Spacebar

 | 

Cycles through move, rotate, and scale transform tools. 

 |
| 

**Move Tool**

 | 

W

 | 

Switches to the move transform tool.

 |
| 

**Rotate Tool**

 | 

E

 | 

Switches to the rotate transform tool.

 |
| 

**Scale Tool**

 | 

R

 | 

Switches to the scale transform tool.

 |

For each of the **Transform Tools**, you can change whether it uses an object’s **Local** or **World** space for movement, rotation, and scaling.

[![Unreal Editor Local or World Space](https://dev.epicgames.com/community/api/documentation/image/bf29985e-0e82-4337-8424-c67fb605ad89?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bf29985e-0e82-4337-8424-c67fb605ad89?resizing_type=fit)

Unreal Engine’s **Snapping** tools include options to toggle on and off snapping for grid, rotation angle, and scaling increments. You can also select the values next to each grid, rotation angle, and scaling increment to set their incremental values. 

[![Unreal Editor Snapping Tools](https://dev.epicgames.com/community/api/documentation/image/c232b529-d761-4f4e-9eeb-9017b126f18c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c232b529-d761-4f4e-9eeb-9017b126f18c?resizing_type=fit)

Under the Viewport Transform Tools menu, you’ll find additional **Gizmo** settings that can assist your workflows in the editor. 

[![Unreal Editor Gizmo Settings](https://dev.epicgames.com/community/api/documentation/image/a6273590-d0fd-469b-974b-e4fac4af0bd4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a6273590-d0fd-469b-974b-e4fac4af0bd4?resizing_type=fit)

For example, the **Arcball Rotation** and **Screenspace Rotation** checkboxes expand how you can rotate objects in the level. 

|  |  |
| --- | --- |
|  |  |
| 
**Arcball Rotation**

 | 

**Screenspace Rotation**

 |

### Customizing the Unreal Engine Interface

The Unreal Editor’s layout is fully customizable. You can drag and drop tabs, dock them into the main window, change the color scheme, save these layouts, and more. To learn more about how you can do all of these things, see [Customizing Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/customizing-unreal-engine).

## Level Editor Modes

The **Mode** selection dropdown for the level editor includes specific modes that change the level editor’s toolbars and panel layout. This may add or remove toolbar actions you have access to. For example, when using the Landscape mode, a new panel opens that includes options to create, manage, edit, and paint landscape terrains in the currently loaded level. Similarly, Animation mode includes tools and settings to animate directly in the level viewport. 

You can access the Mode selection in the main toolbar on the left-hand side of the level editor. Use the dropdown menu to select which editor mode you’d like to use. 

[![Unreal Editor Selection Modes](https://dev.epicgames.com/community/api/documentation/image/c9238780-5aaa-48b7-956e-7027274a29ae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c9238780-5aaa-48b7-956e-7027274a29ae?resizing_type=fit)

Below is a quick reference table of how you can use these in your real-time scenes: 

| UE Level Editor Mode | Maya Mode Equivalence | Description and Primary Uses |
| --- | --- | --- |
| 
**Selection Mode**

 | 

**Object Mode**

 | 

(Default Mode) Used to select, move, rotate, and scale objects in the viewport.

For more information, see [Select Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/select-mode-in-unreal-engine).

 |
| 

**Landscape Mode**

 | 

**Sculpt Geometry Tool**

 | 

Used to create and sculpt terrain and paint it using a material setup to paint layered materials. You can also import height maps from external tools.

For more information, see [Landscape Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine).

 |
| 

**Foliage Mode**

 | 

**MASH / Scatter Objects**

 | 

Used to paint foliage meshes, like grass, trees, rocks, or any assigned geometry, onto surfaces as instances of these objects. Supports multiple meshes, and tools for density, randomization, alignment to surfaces, and more.

For more information, see [Foliage Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine).

 |
| 

**Mesh Paint Mode**

 | 

**Vertex Painting**

 | 

Used to paint directly onto a mesh with color data painted directly into the vertices or its assigned texture. This is useful for painting blended areas on a mesh between different layers to create variety in look with dirt and wear.

For more information, see [Mesh Paint Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-paint-mode-in-unreal-engine).

 |
| 

**Modeling Mode**

 | 

**Basic Poly Modeling / Modeling Tool Kit**

 | 

Used for in-editor geometry creation and editing with a suite of tools found in common modeling applications.

For more information, see [Modeling Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

 |
| 

**Fracture Mode**

 | 

**Shatter Tool**

 | 

Used to fracture meshes for destruction effects using a suite of tools to define the look and level of fracturing that occurs, with the engine handling simulation and physics in real-time.

For more information, see [Fracture Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-destruction-in-unreal-engine).

 |

## Content Drawer and Content Browser

The **Content Browser** is the part of the Unreal Editor where you’ll create, import, view, organize, and manage the assets contained within your project. 

For a Maya user, this would be similar to an advanced Project Window and Hypershade browser combined.

[![Unreal Editor Content Browser](https://dev.epicgames.com/community/api/documentation/image/bce40e03-f625-44e0-8619-26226a39cbaf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bce40e03-f625-44e0-8619-26226a39cbaf?resizing_type=fit)

The content browser includes the following: 

-   Asset management to organize all your assets into folders.
    
-   Search, filters, and tags to find assets and asset types quickly.
    
-   Previews and thumbnails of assets.
    
-   Right-click context menus to access asset actions and asset creation.
    
-   Drag and drop workflows to import and organize assets.
    
-   Dockable panel for different workspace layouts.
    
-   Multiple browser windows.
    

For more detailed information about how you can use and navigate the Content Browser in your project, see [Content Browser](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) and [Content Browser Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-interface-in-unreal-engine).

## Next Page

[

![Importing Content into Unreal Engine from Maya](https://dev.epicgames.com/community/api/documentation/image/6af188d2-182a-420c-9da2-323bf113f719?resizing_type=fit&width=640&height=640)

Importing Content into Unreal Engine from Maya

An overview of importing content into Unreal Engine for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-content-into-unreal-engine-from-maya)