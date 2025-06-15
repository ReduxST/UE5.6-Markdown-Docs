# Unreal Editor Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-interface)  
**Processed:** 2025-06-14 16:56:06

---

This introduction to the **Unreal Engine** **interface** describes the most common **buttons**, **panels**, and **toolbars** you’ll interact with in the **Unreal** **Editor**. In this page, you’ll learn more about what they do and how you can use them. While some of these elements are generally the same across various parts of the engine, you should spend some time getting familiar with their general purpose and functionality, especially if you are new to developing projects with Unreal Engine. You can also follow links throughout this page for a deeper dive into how you can use them.

When you open the engine for the first time, the **Level Editor** opens. This provides the core creation functionality to the Unreal Editor and is used for designing and constructing levels and environments. It is where you’ll spend most of your time developing content for your project. There are different editors in Unreal Engine used for different purposes. 

Once your project opens, you will see the following layout, keeping in mind that what’s in the level will differ depending on the project you open. For this example, we are using the First Person template.

[![](https://dev.epicgames.com/community/api/documentation/image/669481b3-c96f-4e63-9c89-2f8025e8210f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/669481b3-c96f-4e63-9c89-2f8025e8210f?resizing_type=fit)

| Number | Name | Description |
| --- | --- | --- |
| 
1

 | 

Menu Bar

 | 

Uses these menus to access common application actions, like saving, and creating new levels. You’ll also find options for opening editor windows and tools that are useful for specific functions like debugging and more. 

 |
| 

2

 | 

Main Toolbar

 | 

Contains shortcuts for some of the most common tools and editors in Unreal Engine, as well as shortcuts to enter Play mode (run your game inside Unreal Editor) and to deploy your project to other platforms.  

 |
| 

3

 | 

Viewport Toolbar

 | 

Includes common tools used to manipulate objects in the level by moving, rotating, and scaling them, as well as snapping tools for moving objects along a grid, rotation angle, or scaling amount. It also includes perspective and orthographic views along with debugging and visualization view mode and other settings you can use while working in the viewport.

 |
| 

4

 | 

Level Viewport

 | 

Displays the contents of your Level, such as Cameras, Actors, Static Meshes, and so on.

 |
| 

5

 | 

Outliner

 | 

Displays a hierarchical tree view of all content in your Level.

 |
| 

6

 | 

Details panel

 | 

Appears when you select an Actor. Displays various properties for that Actor, such as its **Transform** (position in the Level), Static Mesh, Material, and physics settings. This panel displays different settings depending on what you select in the Level Viewport.

 |
| 

7

 | 

Content Drawer

 | 

Opens the Content Drawer, a temporary Content Browser window, from which you can access all of the Assets in your Project.

 |
| 

8

 | 

Bottom Toolbar

 | 

Contains shortcuts to the Command Console, Output Log, and Derived Data functionality. Also displays source control status.

 |

## Menu Bar

Each editor in Unreal Engine has a **menu bar** that is located in the top-left of the editor window (Windows), or at the top-left of the display (macOS). Some of the menus, such as **File**, **Window**, and **Help**, are present in all editor windows, not just the Level Editor. Some other menus are specific to their own editors.

[![](https://dev.epicgames.com/community/api/documentation/image/f4b51aec-4b51-478e-8ca8-a5bb81c8d3bc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f4b51aec-4b51-478e-8ca8-a5bb81c8d3bc?resizing_type=fit)

## Main Toolbar

The **Main Toolbar** contains shortcuts to some of the most used tools and commands in Unreal Editor. It is divided into the following areas:

[![](https://dev.epicgames.com/community/api/documentation/image/96d4b7e3-0822-4752-b8e4-1eedf68053a1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/96d4b7e3-0822-4752-b8e4-1eedf68053a1?resizing_type=fit)

| Number | Name | Description |
| --- | --- | --- |
| 
1

 | 

Save button

 | 

Click this button to save the level that is currently open.

 |
| 

2

 | 

Select the open level

 | 

Click this button to show the currently loaded level in the Content Browser. This will open the most recently used Content Browser, which can be the docked Content Drawer or standalone Content Browser panel.

 |
| 

3

 | 

Mode selection

 | 

Contains shortcuts for quickly switching between different modes to edit content within your level. These modes also change the primary behavior of the Level Editor, which can include toolbar options designed for each mode specifically. You can click the links to go to their respective pages to learn more about a mode.

-   [Selection](https://dev.epicgames.com/documentation/en-us/unreal-engine/select-mode-in-unreal-engine)
    
-   [Landscape](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-quick-start-guide-in-unreal-engine)
    
-   [Foliage](https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine)
    
-   [Mesh Paint](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-paint-mode-in-unreal-engine)
    
-   [Modeling](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-quick-start-in-unreal-engine)
    
-   [Fracture](https://dev.epicgames.com/documentation/en-us/unreal-engine/fracture-mode-selection-tools-user-guide)
    
-   [Brush](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-brush-actors-in-unreal-engine)
    
-   [Animation](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine)
    

 |
| 

4

 | 

Content shortcuts

 | 

Contains shortcuts for adding and opening common types of content within the Level Editor.

1.  The **Create** button can be used to choose from a list of common **Actor Types** and **Recently Used** assets from the Content Browser to quickly add to your level.
    
2.  The **Blueprints** button can be used to create and access blueprints. 
    
3.  The **Cinematics** button can be used to create and access a **Level Sequence** or **Master Sequence** cinematic.
    

 |
| 

5

 | 

Play mode controls

 | 

Contains the shortcut buttons Play, Skip, Stop, and Eject for running your game in the editor.  

 |
| 

6

 | 

Platforms menu

 | 

Contains a series of options you can use to configure, prepare, and deploy your project to different platforms, such as desktop platforms such as Windows, macOS and Linux, mobile, and consoles.

Some platforms, such as mobile and console, require additional setup and configuration of your project. These can include their own software development kit (SDK) installations or non-disclosure agreements (NDAs) to access them.



 |

## Viewport Toolbar

The Viewport Toolbar can be used to accomplish a number of tasks when building levels. It is located at the top of the Level Viewport, and its settings and tools are grouped into the following categories:

[![](https://dev.epicgames.com/community/api/documentation/image/55cc5842-0874-4d8d-84fc-0f3fc2988797?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/55cc5842-0874-4d8d-84fc-0f3fc2988797?resizing_type=fit)

| Number | Name | Description |
| --- | --- | --- |
| 
1

 | 

Transform and Snapping tools

 | 

These are the options to swap between different Transform tools and change the snapping options.

 |
| 

2

 | 

Camera tools

 | 

These are the options to switch between Perspective and Orthographic views and change camera movement speed.

 |
| 

3

 | 

View Mode and Show Flag options

 | 

These are the options to pick between different view modes like Lit, Unlit, and Wireframe, and show flags related to the current viewport to hide and reveal types of content in the Level Viewport.

 |
| 

4

 | 

Performance and Scalability tools

 | 

This dropdown can be used to reveal settings like Viewport Scalability and Material Quality Level.

 |
| 

5

 | 

Viewport options

 | 

These options can be used to change viewport related settings, like mouse sensitivity in the Level Viewport.

 |

To learn more about this toolbar, read the [Viewport Toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar) documentation.

## Level Viewport

The **Level** **Viewport** displays the contents of the level that is currently loaded. When opening a project in Unreal Engine, the project's default level is loaded For example, if you open the First or Third Person Template project, you’ll see a gray box area (like the one pictured below) with some physics objects, floors, walls, and ramps.

The Level Viewport is where you can view and edit the contents of your Level, whether it's a game environment, a product visualization, or something else.

The Level Viewport can generally display the contents of the Level in two different ways:

-   Perspective is a 3D view you can navigate to see the contents of the viewport from different angles.
    
-   Orthographic is a 2D view that looks towards a specific direction (top, down, left, right, front, back). This creates a view where the distance from the object doesn’t affect size or provide a sense of depth.
    

| Perspective view | Top view | Right side view |
| --- | --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/eafa8ca5-da06-4c39-8914-6e81cc0573f1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eafa8ca5-da06-4c39-8914-6e81cc0573f1?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/8ab4d964-b22f-42f6-8829-b9ea33ab99a3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8ab4d964-b22f-42f6-8829-b9ea33ab99a3?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/7b4be143-d77b-4612-8292-0b2e87ddf8e3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7b4be143-d77b-4612-8292-0b2e87ddf8e3?resizing_type=fit)



 |

The **Viewport Type** can be changed between **Default** **Viewport** and **Cinematic Viewport**. Default Viewport displays gizmos and icons in the level like Camera actors, Collision Components, and the World Grid.

Additionally, you can change the **View Mode** of your viewport by pressing the Lit button in the top-right corner of the viewport. Lit is the default view mode used for real-time applications in the Perspective view, where you can preview your scene with normally rendered lighting. If you select another View Mode, this button will be titled after that. So, if you have already selected one of the Orthographic views (Top, Front, Left, and so on), the button might say **Wireframe** in your viewport as that is the default View Mode for the Orthographic view. If you press it, and select Lit, you will see your environment fully lit again in any view mode.

You can use the **Scalability** options to change the visual fidelity of which your level is being previewed. By clicking the **Performance and Scalability** button and clicking **Viewport Scalability**, you can change to a different scalability group. 

| Low option | High option | Cinematic option |
| --- | --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/ef04c505-63e7-4174-b53b-1fbde47be74b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ef04c505-63e7-4174-b53b-1fbde47be74b?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/e5deea9c-e839-4b0b-8228-3f910ba3b14a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e5deea9c-e839-4b0b-8228-3f910ba3b14a?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/c7187af5-c647-44f2-be29-5780927c44a6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c7187af5-c647-44f2-be29-5780927c44a6?resizing_type=fit)



 |

To learn more about the scalability options, see the [Scalability Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-reference-for-unreal-engine) page.  

## Navigating the Viewport

Let’s explore your Level! To control the viewport camera, the perspective through which you view the Level, press and hold the Right Mouse Button (RMB) anywhere in the viewport. While holding down RMB, you can use the **W**, **A**, **S**, and **D** keys to fly through the scene. You can fly up and down with the **E** and **Q** keys.

Releasing RMB and holding down the Left Mouse Button (LMB) can be used along with dragging the mouse to move the camera forward, backward, and rotate it left or right. This provides an alternative method for navigating the environment with greater precision.

| Navigating with LMB | Navigating with RMB |
| --- | --- |
|  |  |

Clicking on an object in the Level with the LMB **selects** the object. Selected objects can be manipulated using the **Transform Tool gizmos** in the viewport. Gizmos are a set of on-screen handles used to move, rotate, or scale the object along specific axes, activated based on the transform tool you select. You can activate the **Translate** tool by pressing **W**, the **Rotation** tool by pressing **E**, and the **Scale** tool by pressing **R**. Alternatively, you can use the Toolbar located at the top-right of the Viewport to switch between Transform tools.

Once you have selected a tool, you can manipulate the object using the gizmo’s axes. With the Translate or Scale tools, you can also drag from the center of the gizmo to adjust all axes simultaneously. This is particularly useful for uniformly scaling an object without disproportionately affecting any single axis.

The viewport will have snapping enabled by default for every way of transforming your object. You can turn these off or change their snapping values by using the individual settings on the top-left side of the viewport.

[![](https://dev.epicgames.com/community/api/documentation/image/a3453a28-9e0f-4e40-af53-501650f07c5e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a3453a28-9e0f-4e40-af53-501650f07c5e?resizing_type=fit)

For more information on how to navigate a level, see the [Viewport Controls](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-controls-in-unreal-engine) page.

## Content Drawer and Content Browser

The **Content Browser** is a file explorer for your project where you can organize all the assets that make up your project. These assets can include Blueprints, Geometry (static and skeletal), textures, materials, and so on.

The **Content Drawer**, located in the bottom-left corner of the Unreal Editor, opens a special instance of the Content Browser that automatically minimizes when it loses focus (that is, when you click away from it). To keep it open, click the **Dock in Layout** button in the top-right corner of the Content Drawer. This creates a new instance of the Content Browser, but you can still open a new Content Drawer. You can also open a Content Drawer by holding down **CTRL** key and pressing the **Space** key.

## Bottom Toolbar

The **Bottom Toolbar** contains shortcuts and settings to various elements of the Unreal Editor. Depending on the Editor you are in (like the Viewport Editor), some of these options might not be available.

[![](https://dev.epicgames.com/community/api/documentation/image/bda8f673-5f85-48e1-b434-527727894e44?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bda8f673-5f85-48e1-b434-527727894e44?resizing_type=fit)

| Number | Name | Description |
| --- | --- | --- |
| 
1

 | 

Content Drawer

 | 

Temporary content browser window which gets dismissed as it loses focus, used for quick access.

 |
| 

2

 | 

OutputLog Drawer and Command Prompt

 | 

Opening the Output Log and entering Console Commands, including changing between executing Unreal Commands and Python scripts.

 |
| 

3

 | 

  Tracing

 | 

Start tracing, save a Snapshot of the Current Trace Buffer, and change Trace settings.

 |
| 

4

 | 

Stall Log

 | 

Opens the Stall Log.

 |
| 

5

 | 

Derived Data

 | 

Provides [Derived Data](https://dev.epicgames.com/documentation/en-us/unreal-engine/derived-data-settings-in-the-unreal-engine-project-settings) functionality.

 |
| 

6

 | 

Live Coding Compiler

 | 

Recompile and reload C++ code on the fly using Live Coding.

This option is only available in C++ projects, not Blueprint projects.



 |
| 

7

 | 

Save Status

 | 

View the number of Levels with changes not yet saved. You can click on this option to view unsaved Levels.

 |
| 

8

 | 

Revision Control

 | 

Connect to Revision Control and View Changes, Submit Content, or Check Out Modified Files.

 |

## Outliner

The **Outliner** panel displays a hierarchical view of all content in your level. It is located in the upper-right corner of the Unreal Editor window. You can have up to four different Outliners, each with its own column layout and filter configuration.

[![](https://dev.epicgames.com/community/api/documentation/image/46e3571a-9cb5-423f-84a6-6a904a743209?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/46e3571a-9cb5-423f-84a6-6a904a743209?resizing_type=fit)

You can hide or reveal objects by clicking their associated **Eye** button. Accessing an object’s **context menu** can be done by right-clicking that object in the Outliner. You can then perform additional, actor-specific operations from that menu.

To keep your levels organized, you can create, move, and delete content folders. Folders can be used to group objects in your level together. 

## Details Panel

When you select an actor in the Level Viewport or the Outliner, the **Details** panel will show the settings and properties that affect the actor you selected. By default, it is located on the right side of the Unreal Editor window, under the Outliner panel.

[![](https://dev.epicgames.com/community/api/documentation/image/491f8e6d-38cd-4973-8661-13dd3d5fe7bf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/491f8e6d-38cd-4973-8661-13dd3d5fe7bf?resizing_type=fit)

As shown in the image above:

| Number | Description |
| --- | --- |
| 
1

 | 

The ramp object in the Level is highlighted after being selected (clicked on).

 |
| 

2

 | 

The ramp object is also highlighted in the **Outliner** panel automatically. Selecting an object through the Level Viewport or the Outliner Panel highlights it the same.

 |
| 

3

 | 

The **Details** panel shows the components and properties of the ramp object. You can modify the properties of an object through the Details panel. To learn more about components, see the [Components Window](https://dev.epicgames.com/documentation/en-us/unreal-engine/components-window-in-unreal-engine) page.

 |

You can filter the actor’s properties to view and change by selecting a specific Component at the top of the Details panel. You can lock the current selection into the Details panel, which you can use to highlight other objects while keeping the Details panel locked on the first object.