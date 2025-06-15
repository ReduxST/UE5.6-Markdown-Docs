# Static Mesh Editor UI

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:19

---

The **Static Mesh Editor** consists of four areas:

Click image for full size.

1.  [Menu Bar](/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine#menubar)
2.  [Toolbar](/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine#toolbar)
3.  [Viewport Panel](/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine#viewportpanel)
4.  [Details Panel](/documentation/en-us/unreal-engine/static-mesh-editor-ui-in-unreal-engine#detailspanel)
5.  \[Bottom Toolbar\] (#BottomToolbar)

-   You can close any panel by clicking the small **X** in the upper-right corner of the tab. You can also hide any panel by right-clicking on the tab, and then clicking **Hide Tab** on the context menu that appears. To once again display a panel that you have closed, click that panel's name on the **Window** menu.
    
-   Pressing **F1** displays the Unreal Engine Static Mesh Editor UI documentation.
    

## Menu Bar

Click image for full size.

### File

Click image for full size.

| Command | Description |
| --- | --- |
| **Open Asset** | Opens the **Global Asset Picker** to quickly find an asset and open the appropriate editor. (**CTRL + P**) |
| **Save All** | Saves all unsaved levels and assets for your project. (**CTRL + SHIFT + S**) |
| **Choose Files to Save** | Brings up a dialog box that allows you to choose which levels and assets you want to save for your project. |
| **Save** | Saves the asset you are currently working on. (**CTRL + S**) |
| **Save As** | Saves the asset you are currently working on under a new name. (**CTRL + ALT + S**) |

### Edit

Click image for full size.

#### History

| Command | Description |
| --- | --- |
| **Undo** | Undoes the most recent action. (**CTRL + Z**) |
| **Redo** | Redoes the most recent Undo, if it was the last action taken. (**CTRL + Y**) |
| **Undo History** | Brings up the **Undo History** panel in a separate window. |

#### Sockets

| Command | Description |
| --- | --- |
| **Delete Socket** | Deletes the selected socket from the mesh. (**DELETE**) |
| **Duplicate Socket** | Duplicates the selected socket. (**CTRL + D**) |

#### Configuration

| Command | Description |
| --- | --- |
| **Editor Preferences** | Gives you a list of options, any of which open that part of the **Editor Preferences** window, where you can modify your Unreal Editor preferences. |
| **Project Settings** | Gives you a list of options, any of which open that part of the **Project Settings** window, where you can modify various settings for your Unreal Engine project. |
| **Plugins** | Brings up the **Plugins** window. |

### Asset

Click image for full size.

| Command | Description |
| --- | --- |
| **Find in Content Browser** | Locates and selects the current asset in the **Content Browser**. (**CTRL + B**) |
| **Reference Viewer** | Launches the **Reference Viewer** showing the selected assets' references. (**ALT + SHIFT + R**) |
| **Size Map** | Displays an interactive map showing the approximate size of this asset and everything it references. (**ALT + SHIFT + M**) |
| **Audit Assets** | Opens the **Audit Assets UI** and displays information about the selected assets. (**ALT + SHIFT + A**) |
| **Shader Cook Statistics** | Shows the **Shader Cook** statistics. (**CTRL + ALT + SHIFT + S**) |
| **Reimport filename** | Reimports the current asset from its original location on disk. |
| **Find Source** | Opens the explorer to the location of the selected asset. |
| **Additional Data** | Toggles whether or not to draw additional user data associated with the asset. |
| **Bake Out Materials** | Bake out **Materials** for given LODs. |

### Collision

Click image for full size.

| Command | Description |
| --- | --- |
| **Add Sphere Simplified Collision** | Generates a new sphere collision mesh encompassing the Static Mesh. |
| **Add Capsule Simplified Collision** | Generates a new capsule collision mesh encompassing the Static Mesh. |
| **Add Box Simplified Collision** | Generates a new box collision mesh encompassing the Static Mesh. |
| **10DOP-X Simplified Collision** | Generates a new axis-aligned box collision mesh with the 4 X-axis aligned edges beveled (10 total sides) encompassing the Static Mesh. |
| **10DOP-Y Simplified Collision** | Generates a new axis-aligned box collision mesh with the 4 Y-axis aligned edges beveled (10 total sides) encompassing the Static Mesh. |
| **10DOP-Z Simplified Collision** | Generates a new axis-aligned box collision mesh with the 4 Z-axis aligned edges beveled (10 total sides) encompassing the Static Mesh. |
| **18DOP Simplified Collision** | Generates a new axis-aligned box collision mesh with all edges beveled (18 total sides) encompassing the Static Mesh. |
| **26DOP Simplified Collision** | Generates a new axis-aligned box collision mesh with all edges and corners beveled (26 total sides) encompassing the Static Mesh. |
| **Convert Boxes to Convex** | Converts any simple box collision meshes to convex collision meshes. |
| **Remove Collision** | Removes any simplified collision assigned to the Static Mesh. |
| **Delete Selected Collision** | Deletes the selected collision from the mesh. (**DELETE**) |
| **Duplicate Selected Collision** | Duplicates the selected collision. (**CTRL + D**) |
| **Auto Convex Collision** | Generates a new convex collision mesh based on the shape of the Static Mesh asset. |
| **Copy Collision from Selected Static Mesh** | Copies any collision meshes that were created in the native 3D application and saved with the Static Mesh. |
| **Find Source**\* | Locates the folder location of the current asset . |

For more information about collision for Static Meshes in Unreal Engine, refer to the [Setting Up Collisions With Static Meshes](/documentation/en-us/unreal-engine/setting-up-collisions-with-static-meshes-in-unreal-engine) page.

### Window

Click image for full size.

#### Static Mesh Editor

| Command | Description |
| --- | --- |
| **Viewport** | Toggles the display of the **Viewport** panel. |
| **Details** | Toggles the display of the **Details** panel. |
| **Socket Manager** | Displays the **Socket Manager** panel, which is not displayed by default. |
| **Convex Decomposition** | Displays the **Convex Decomposition** panel, which is not displayed by default. |
| **Preview Scene Settings** | Toggles the display of the **Preview Scene Settings** panel. |

#### Level Editor

| Command | Description |
| --- | --- |
| **Cinematics** | **Sequence Recorder:** Opens a Sequence Recorder tab. |
| **Content Browser** | Brings up the **Content Browser** tool in a separate window. Enables opening multiple Content Browser windows. |

#### Log

| Command | Description |
| --- | --- |
| **Device Output Log** | Brings up the **Device Output Log** in a separate window. |
| **Interchange Results Browser** | Brings up the **Interchange Results Browser**. |
| **Message Log** | Brings up the **Message Log** in a separate window. |
| **Output Log** | Brings up the **Output Log** in a separate window. |

#### Get Content

| Command | Description |
| --- | --- |
| **Open Marketplace** | Brings up the **Marketplace** window to shop for Assets. |
| **Quixel Bridge** | Brings up a **Quixel Bridge** tab for importing Assets. |

#### Layout

| Command | Description |
| --- | --- |
| **Load Layout** | 
-   **Default Editor Layout:** Loads the default layout that the Unreal Editor automatically generates.
-   **UE4 Classic Layout:** Loads the default editor layout of Unreal Engine 4.
-   **Import Layout:** Import a custom layout (or a set of layouts) from a different directory and load it into your current instance of the Unreal Editor UI.



 |
| **Save Layout** | 

-   **Save Layout As:** Save the current layout customization on disk so it can be loaded later.
-   **Export Layout:** Export the current layout customization to a different directory.



 |
| **Remove Layout** | 

-   **Remove All User Layouts:** Remove all the layout customizations created by the user.



 |
| **Enable Fullscreen** | Enables fullscreen mode for the application, expanding across the entire monitor. (**SHIFT + F11**) |

### Tools

Click image for full size.

#### Programming

| Command | Description |
| --- | --- |
| **New C++ Class** | Brings up a window to add C++ code. The code can only be compiled if **Visual Studio** is installed. |
| **Generate Visual Studio Project** | Generates your C++ code in Visual Studio. |

#### Tools

| Command | Description |
| --- | --- |
| **Find in Blueprints** | Brings up the **Find in Blueprints** tool in a separate window. Enables opening multiple Find in Blueprints windows. |
| **Cache Statistics** | Displays cache statistics. |
| **Class Viewer** | Displays all existing classes within the current project. |
| **CSV to SVG** | A table of tools for generating vector line graphs. |
| **Localization Dashboard** | Brings up the **Localiztion Dashboard** for your project in a separate window. |
| **Merge Actors** | Brings up the **Merge Actors** tool in a separate window. |
| **Natine Tools** | Tools for auditing and optimizing **Nanite** assets. |
| **Project Launcher** | The **Project Launcher** provides advanced workflows for packaging, deploying, and launching your projects. |
| **Resource Usage** | A table displaying data usage of each asset type. |
| **Session Frontend** | Brings up the **Session Frontend** in a separate window. |
| **Struct Viewer** | Brings up the **Struct Viewer** in a separate window, which displays all structs that exist within the project. |
| **Virtual Assets** | Statistics for **Virtual Assets**. |

#### Instrumentation

| Command | Description |
| --- | --- |
| **Debug** | 
Brings up the **Debug Tool** in a separate window.

-   **Blueprint Debugger:** Brings up the **Blueprint Debugger** in a separate window.
-   **Collision Analyzer:** Brings up the **Collision Analyzer** in a separate window.
-   **Debug Tools:** Brings up the **Debug Tools** in a separate window.
-   **Modules:** Brings up the **Modules** tab in a separate window.
-   **Niagara Debugger:** Brings up the **Niagara Debugger** in a separate window.
-   **Pixel Inspector:** Brings up the viewport **Pixel Inspector** tool in a separate window
-   **Stylus Input Debug:** Displays current values of stylus inputs.
-   **Visual Logger:** Brings up the **Visual Logger** tool in a separate window.
-   **Widget Reflector:** Brings up the **Widget Reflector** tool in a separate window.



 |
| **Profile** | 

-   **Profile Data Visualizer:** Brings up the **Profile Data Visualizer** tool in a separate window.
-   **Trace Data Filtering:** Bring up the Visual Logger tool in a separate window, allows for setting **Trace Channel** states.



 |
| **Audit** | 

-   **Asset Audit:** Brings up the **Asset Audit** window, which enables viewing detailed information about assets.
-   **Material Analyzer:** Brings up the **Material Analyzer** tool in a separate window



 |
| **Platforms** | 

-   **Device Manager:** Brings up the **Device Manager** in a separate window.
-   **Device Profiles:** Brings up the **Device Profiles** in a separate window



 |

#### Source Control

| Command | Description |
| --- | --- |
| **View Changelists** | Brings up a dialog displaying current changelists. |
| **Submit Content** | Brings up a dialog with check-on options for content and levels. |
| **Connect to Source Control** | Brings up a dialog box that allows you to choose or interact with a source-control system Unreal Editor can integrate with. |

#### Unreal Insights

| Command | Description |
| --- | --- |
| **Run Unreal Insights** | Brings up the **Unreal Insights Session Browser**. |

### Help

Click image for full size.

#### StaticMesh Editor Resources

| Command | Description |
| --- | --- |
| **StaticMesh Editor Documentation** | Opens a browser window and navigates to the documentation about this tool. *( **F1**)* |

#### Reference

| Command | Description |
| --- | --- |
| **Documentation Home** | Brings up an internet browser to technical resources for utilizing the engine. |
| **C++ API Reference** | Classes, functions, and other elements that make up the C++ API. |
| **Console Variables** | Reference companion for console variables and commands. |

#### Community

| Command | Description |
| --- | --- |
| **Online Learning** | Learn Unreal Engine for free with easy-to-follow video courses and guided learning paths. |
| **Forums** | Navigate to the Unreal Engine forums to view announcements and engage in discussions with other developers. |
| **Q&A** | Navigates to the Question and Answer section of the Forum. |

#### Support

| Command | Description |
| --- | --- |
| **Support** | Navigates to the Unreal Engine support website's main page. |
| **Report a Bug** | Navigates to an online portal for reporting bugs in the Unreal Editor. |
| **Issue Tracker** | Navigates to the Unreal Engine issue tracker page |

#### Application

| Command | Description |
| --- | --- |
| **About Unreal Editor** | Displays application credits, copyright information, and build information. |
| **Credits** | Display application credits. |
| **Visit UnrealEngine.com** | Navigates to UnrealEngine.com where you can learn more about Unreal technology. |

## Toolbar

Click image for full size.

| Command | Description |
| --- | --- |
| **Save** | Saves the current asset. |
| **Browse** | Browses to the associated asset and selects it in the most recenty-used Content Browser (summoning one if necessary). |
| **Reimport Base Mesh** | 
-   **Reimport Base Mesh:** Reimports the base mesh.
-   **Reimport Base Mesh + LODs:** Reimports the base mesh and all the custom LODs.



 |
| **Collision** | Quick access to display the same **Collision** options as the menu bar. |
| **UV** | 

-   **None**: Toggles display of the static mesh's UVs.
-   **UV Channel #:** Toggles display of the Static Mesh's UVs for the selected channel(s) for the static mesh asset in the Preview Panel.
-   **Remove Selected**: Removes the currently selected UV from the static mesh.



 |

## Viewport Panel

The **Viewport** panel shows a rendered (or optionally wireframe) view of the Static Mesh asset. This allows you to examine the Static Mesh as it would be rendered in-game. Simultaneously, the Viewport contains tools and visualizers to see specific data such as:

-   The bounds of the Static Mesh asset.
-   Any Collision Mesh assigned to the Static Mesh.
-   The UVs of the Static Mesh.

Overlaid onto the **Viewport** panel is a set of statistics or information about the Static Mesh asset.

Click image for full size.

In this information you will find the following:

-   **LOD**: Displays the number of LOD (Levels of Detail) for the Static Mesh.
-   **Current Screen Size**: The vertical height of the mesh displayed on screen as a proportion of the height of the viewport.
-   **Triangles**: Displays the number of triangles in the Static Mesh.
-   **Vertices**: Displays the number of vertices in the Static Mesh.
-   **UV channels**: Number of UV channels. Unique, non-overlapping UVs are required for shadow mapping.
-   **Distance Field**: The resolution and memory footprint of the distance field for this mesh.
-   **Approx Size**: Displays the approximate size (Length x Width x Height) of the Static Mesh in Unreal units with a scale of 1 in all axes.
-   **Num Collision Primitives**: Number of collisions primitives.

The tables below cover the basics of the Viewport. For more information about using this panel, refer to the [Using Editor Viewports](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine) documentation.

### Viewport Options

Click image for full size.

| Command | Description |
| --- | --- |
| **Realtime** | Toggles whether the viewport updates in realtime, or only when clicked on / moused over. By default, it is turned off, and you may need to click in the viewport once after the mesh is loaded in order to get streamed textures displaying at high resolution. (**CTRL + R**) |
| **Show Status** | Toggles showing stats in the viewport. If **Realtime** is not enabled, **Show Stats** automatically enables it. (**SHIFT + L**) |
| **Show FPS** | Toggles showing the frames per second in the viewport. If **Show Stats** is not enabled, **Show FPS** automatically enables it. (**CTRL + SHIFT + D**) |
| **Field of View (H)** | Controls the Horizontal Field of View — how much of the left and right of the frame is visible. |
| **Far View Plane** | Choose the distance to use as your far view plane. Setting this to zero acts as an infinite far view plane. |
| **Screen Percentage** | Sets the percentage of the screen your **Preview** panel uses. |
| **Layouts** | Provides the option to arrange the viewport between one to four panes. |

### Viewpoint Type

Click image for full size.

| Command | Description |
| --- | --- |
| **Perspective** | The default viewpoint used in the viewport, providing a 3D view of your Asset. |
| **Top** | Switches the viewport to the top view in 2D. **(ALT+J)** |
| **Bottom** | Switches the viewport to the bottom view in 2D. **(ALT+SHIFT+J)** |
| **Left** | Switches the viewport to the left view in 2D. **(ALT+K)** |
| **Right** | Switches the viewport to the right view in 2D. **(ALT+SHIFT+K)** |
| **Front** | Switches the viewport to the front view in 2D. **(ALT+H)** |
| **Back** | Switches the viewport to the back view. **(ALT+SHIFT+H)** |

### Lit

Click image for full size.

#### View Mode

| Command | Description |
| --- | --- |
| **Lit** | Shows the final result of your scene once all of the Materials and lighting have been applied. (**ALT + 4**) |
| **Unlit** | Removes all lighting from the scene, showing you Base Color only. (**ALT + 3**) |
| **Wireframe** | Toggles the viewmode of the Preview panel between a lit view and a wireframe view. (**ALT + 2**) |
| **Detail Lighting** | Activates a neutral Material across the entire scene, using the normal maps of the original materials. (**ALT + 5**) |
| **Lighting Only** | Shows a neutral Material that is only affected by lighting. (**ALT + 6**) |
| **Reflections** | Overrides all materials with a flat normal and a roughness of 0, which is a mirror. |
| **Player Collision** | Renders a color-coded view of what a Player or Pawn can collide with. Static Mesh collision displays as green, Volumes as pink, and Brushes as a grayish-violet. |
| **Visibility Collision** | This setting will render a color-coded view of what Actors in the scene will block visibility traces. Static mesh collision displays as green, volumes as pink, and brushes as a grayish-violet. |
| **Optimization Viewmodes** | 
Select from the following options:

-   **Light Complexity:** Renders a view showing where raw light overlaps.
-   **Lightmap Density:** Renders a view of lightmap density in the scene, with blue being the least dense and red being the most dense.
-   **Stationary Light Overlap:** Renders a view of where stationary lights overlap.
-   **Shader Complexity:** Renders a view of the shader complexity in a scene. Light green is the least complex, moving to darker greens as complexity increases, and the most complex areas are in red.
-   **Shader Complexity and Quads:** Renders a view with both shader complexity and quad overdraw displayed.
-   **Quad Overdraw:** Renders a view with just quad overdraw complexity displayed.
-   **Material Texture Scales:** Visualize the accuracy of the material texture scales used for texture streaming.
-   **Required Texture Resolution:** Visualize the ratio between the currently streamed texture resolution and the resolution wanted by the GPU.



 |
| **Level of Detail Coloration** | 

Select from the following options:

-   **Mesh LOD Coloration:** Renders the scene using LOD color visualization.
-   **Hierarchical LOD Coloration:** Renders the scene using HLOD color visualization.



 |

#### Collision

| Command | Description |
| --- | --- |
| **Player Collision** | Renders a color-coded view of what a Player or Pawn can collide with. Static Mesh collision displays as green, Volumes as pink, and Brushes as a grayish-violet. |
| **Visibility Collision** | This setting will render a color-coded view of what Actors in the scene will block visibility traces. Static mesh collision displays as green, volumes as pink, and brushes as a grayish-violet. |

#### Exposure

| Command | Description |
| --- | --- |
| **Auto** | Enable or disable automatic exposure. |
| **EV100** | Allows you to set the exposure value when Auto exposure is disabled. |

### Show

Click image for full size.

| Command | Description |
| --- | --- |
| **Sockets** | Displays any sockets that have been applied to this mesh. For more information about sockets, refer to [Skeletal Mesh Sockets](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine) (**ALT + S**) |
| **Vertices** | Toggles display of vertices in the Preview panel. (**ALT + V**) |
| **Vert Colors** | Toggles visibility of vertex colors. |
| **Normals** | Toggles display of vertex normals in the Preview panel. (**ALT + N**) |
| **Tangents** | Toggles display of vertex tangents in the Preview panel. (**ALT + T**) |
| **Binormals** | Toggles display of vertex binormals (orthogonal vector to normal and tangent) in the Preview panel. (**ALT + B**) |
| **Show Pivot** | Toggles visibility of the mesh's pivot point. (**ALT + P**) |
| **Grid** | Toggles visibility of the grid in the Preview panel. |
| **Bounds** | Toggles display of the bounds of the Static Mesh. |
| **Simple Collision** | Toggles display of the simplified collision mesh of the Static Mesh, if present. |
| **Complex Collision** | Toggles display of the complex collision for this Static Mesh. |
| **Physical Material Masks** | Toggles physical material masks. |

### LOD

Click image for full size.

| Command | Description |
| --- | --- |
| **LOD Auto** | Automatically sets Level of Detail (LOD). |
| **LOD 0** | Forces LOD 0. |

## Details Panel

Click image for full size.

The **Details** panel shows specific properties pertaining to the Static Mesh Actor, such as the Materials applied to the surface, LOD options, and mesh reduction options.

For information about the basics of using this panel, refer to the [Level Editor Details Panel](/documentation/en-us/unreal-engine/level-editor-details-panel-in-unreal-engine) documentation.

## Bottom Toolbar

Click image for full size.

| Command | Description |
| --- | --- |
| **Content Drawer** | Opens a temporary Content Browser **(Ctrl+Spacebar)**. |
| **Output Log** | Debugging tool that prints out useful information while your application is running. |
| **CMD** | 
Executes the following command options:

-   **CMD**: Executes Unreal Console commands
-   **Python:** Executes Python scripts, including files.
-   **Python (REPL)**: Executes a single Python statement and shows its results.



 |
| **Source Control Off** | 

Signals if Source Control is disabled or active. Provides the followiing options once active:

-   **View Changelist:** Opens a dialog displaying the current changelist.
-   **Submit Content:** Opens a dialog with check in options of content and levels.
-   **Checkout Modified Files:** Opens a dialog to checkout any assets which have been modified.
-   **Connect to Source Control:** Opens a dialog to perform source control operations on content and levels.



 |

## Controls

### Mouse Controls

**Viewport Panel**

-   **LMB + Drag** - If the camera is locked, rotates the mesh around its Z-axis and moves towards or away from the origin. Otherwise, rotates the camera around its Z-axis and moves the camera along its local X-axis.
-   **RMB + Drag** - If the camera is locked, rotates the mesh. Otherwise, rotates the camera.
-   **LMB + RMB + Drag** - If the camera is not locked, moves the camera along its local YZ plane.

### Keyboard Controls

-   **Ctrl + R** - Toggles realtime in the **Preview** panel.
-   **L + Mouse Move** - Rotates the preview light in the **Preview** panel.

**Camera Hotkeys**

-   **Alt+H** - Position camera to the Front Orthographic view.
-   **Alt+J** - Position camera to the Top Orthographic view.
-   **Alt+K** - Position camera to the Side Orthographic view.
-   **Alt+G** - Position camera to the Perspective view.