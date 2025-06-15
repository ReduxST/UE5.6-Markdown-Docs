# Material Editor UI

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-ui](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-ui)  
**Processed:** 2025-06-14 16:56:48

---

The Material Editor UI consists of a menu bar, a toolbar, and the five main regions shown below.

| **Number** | **Description** |
| --- | --- |
| 1 | Menu Bar |
| 2 | Toolbar |
| 3 | Viewport Panel |
| 4 | Details Panel |
| 5 | Material Graph Panel |
| 6 | Stats Panel |
| 7 | Palette Panel |

-   You can close any panel by clicking the small "X" in the upper-right corner of the tab. You can also hide any panel by right-clicking on the tab, and then clicking **Hide Tab** in the context menu that appears. To once again display a panel that you have closed, click that panel's name in the **Window** menu.
-   Pressing **F1** displays the Unreal Engine Materials documentation.

## Menu Bar

![Material Editor menu bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8732640-714e-4a2e-8db9-3adb8d181c89/menu-bar.png)

### File

-   **Open Asset** - Opens the Global Asset Picker to quickly find an asset and open the appropriate editor.
-   **Save All** - Saves all unsaved levels and assets for your project.
-   **Choose Files to Save** - Brings up a dialog box that allows you to choose which levels and assets you want to save for your project.
-   **Save** - Saves the asset you are currently working on.
-   **Save As** - Saves this asset under a different name.

### Edit

-   **Undo** - Undoes the most recent action.
-   **Redo** - If it was the last action taken, this option redoes the most recent Undo.
-   **Undo History** - Shows the history of the Undo actions.
-   **Editor Preferences** - Gives you a list of options, any of which open that part of the **Editor Preferences** window, where you can modify your Unreal Editor preferences.
-   **Project Settings** - Gives you a list of options, any of which open that part of the **Project Settings** window, where you can modify various settings for your Unreal Engine project.
-   **Plugins** - Opens the Plugins Browser tab.

### Asset

-   **Find in Content Browser** - Locates and selects the current asset in the **Content Browser**.
-   **Reference Viewer** - Launches the reference viewer showing the selected assets' references.
-   **Size Map** - Displays an interactive map showing the approximate size of this asset and everything it references.
-   **Audit Assets** - Opens the Asset Audio UI and displays information about the selected assets.
-   **Shader Cook Statistics** - Opens the Shader Cook statistics UI.

### Window

-   **Graph** - Toggles the **Graph** panel display.
-   **Viewport** - Toggles the **Viewport** panel display.
-   **Details** - Toggles the **Details** panel display.
-   **Palette** - Toggles the **Palette** panel display.
-   **Find Results**\- Allows you to search for items in the Material Graph.
-   **Preview Scene Settings** - Opens a tab that allows you to change the **Material preview** viewport options.
-   **Parameters**\- Toggles displaying the **Materials** global parameters.
-   **Custom Primitive Data**\- Opens a tab that displays all parameters in the current Material with Custom Primitive Data enabled.
-   **Layer Parameters**\- Displays all Material Layers added to the current Material.
-   **Platform Stats** - Toggles displaying the **Material** cost per platform.
-   **Stats** \- Toggles the **Material** cost.
-   **Shader Code -** Toggles displaying the **Material HLSL** code for the selected platform.
    -   **HLSL Code** - Toggles displaying the **HLSL** code.
        -   **Desktop** - Toggles displaying the **HLSL** code for the various desktop renders.
            -   **DirectX SM5** - Toggles displaying the **HLSL** code for **Windows SM5**.
            -   **DirectX SM6** - Toggles displaying the **HLSL** code for **Windows SM6**.
            -   **DirectX ES 3.1** - Toggles displaying the **HLSL** code for **ES 3.1**.
            -   **Vulkan SM5** - Toggles displaying the **HLSL** code for **Vulkan SM5**.
            -   **Metal SM5** - Toggles displaying the **HLSL** code for **Metal SM5**.
            -   **OpenGL SM4** - Toggles displaying the **HLSL** code for **OpenGL** **SM4**.
        -   **Android** \- Toggles displaying the **HLSL** code for the various **Android** renders.
            -   **Android GLES 3.1** - Toggles displaying the **HLSL** code for **Android GLES 3.1**.
            -   **Android Vulkan** - Toggles displaying the **HLSL** code for **Android** **Vulkan**.
            -   **Android Vulkan SM5** - Toggles displaying the **HLSL** code for **Android Vulkan SM5**.
        -   **iOS** - Toggles displaying the **HLSL** code for the various **iOS** renders.
            -   **Metal SM5** - Toggles displaying the **HLSL** code for **Metal**.
            -   **Metal MRT** - Toggles displaying the **HLSL** code for **Metal MRT**.
-   **Cinematics** - Open the Cinematics Sequence Recorder, Takes Recorder, or Takes Browser in a new window.
-   **Content Browser** - Opens the **Content Browser** in a separate window.
-   **Virtual Production** - Open the LIve Link streaming manger tab.
-   **Reset Layout** - Resets your layout to a default arrangement. Requires the editor to restart after saving your changes and creating a backup of your settings.
-   **Save Layout** - Saves the current layout of the panels as the new default layout.
-   **Remove Layout** - Removes the current layout.
-   **Enable Fullscreen** - Enables fullscreen mode for the application, expanding across the entire monitor.

### Tools

-   **New C++ Class** - Adds C++ code to the project. This code can only be compiled if you have Visual Studio installed.
-   **Generate Visual Studio Project** - Generates your C++ code project in Visual Studio.
-   **Find in Blueprints** - Find references to functions, events and variables in all Blueprints.
-   **Cache Statistics** - Displays statistics about the Derived Data Cache.
-   **Class Viewer** - Displays all classes that exist in this project.
-   **CSV to SVG** - Opens a tool for generating vector line graphs from comma-separated value files generated from CSV profiles.
-   **Localization Dashboard** - Opens the localization dashboard for this project.
-   **Merge Actors** - Opens the Merge Actors dialog.
-   **Project Launcher** - Opens the Project Launcher tab.
-   **Resource Usage** - Displays derived data resource usage breakdown.
-   **Session Frontend** - Opens the session frontend tab.
-   **Struct Viewer** - Displays all structures that exist in this project.
-   **Virtual Assets** - Displays statistics about any virtual assets within this project.
-   **Debug** - Debugging tools for Blueprints, collisions, Niagara and more.
-   **Profile** - Open the Profile Data Visualizer or the Trace Data Filtering tab.
-   **Audit** - Open the Asset Audit window or the Material Analyzer.
-   **Platforms** - Open the Device Manager or Device Profiles UI.
-   **Source Control** - Connect to Source Control, view changelists, or submit content.
-   **Run Unreal Insights** - Run the Unreal Insights standalone application.

### Help

-   **Material Editor Documentation** - Opens a browser window and navigates to the documentation about this tool.
-   **Documentation Home** - Opens a browser window and navigates to the documentation home page.
-   **Online Learning** - Opens a browser window and navigates to the [Unreal Online Learning](https://www.unrealengine.com/en-US/onlinelearning-courses) home page.
-   **Forums** - Go to the Unreal Engine forums to view announcements and engage in discussions with other developers.
-   **Answer HUB** - Go to the AnswerHub to ask questions, search existing answers, and share your knowledge with other Unreal Engine developers.
-   **Support** - Opens a browser window to the Epic Pro Support forum page where you can ask a question about Unreal Engine.
-   **Report a Bug** \- Opens a browser window and navigates to the Unreal Engine Bug submission form.
-   **Issue Tracker** \- Opens a browser window and navigates to a searchable database of Unreal Engine issues and fixes.
-   **About Unreal Editor** - Displays application credits, copyright information, and build information.
-   **Credits** - Displays application credits.
-   **Visit UnrealEngine.com** - Navigates to UnrealEngine.com where you can learn more about Unreal Technology.

## Toolbar

The following table lists the options in the Toolbar and what they do.

| **Icon** | **Description** |
| --- | --- |
| ![Save icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e349fca-ee51-4ca4-98fc-710abc2bfafb/save-icon.png) | Saves the current asset. |
| ![Browse icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a44bb306-4d4c-42c5-b68a-8b91e818df9f/browse-icon.png) | Finds and selects the current asset in the Content Browser. |
| ![Apply Icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61cbc3f0-6828-42ee-a4fd-1e48dae1b2c0/apply-material.png) | Applies any changes made in the Material Editor to the original Material and any uses of that Material in the world. |
| ![Search icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acf39c44-b1f5-4832-8f83-b2374f2ade6d/search-icon.png) | Finds expressions and comments in the current Material. |
| ![Home Icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49bce6b1-a724-4999-a312-89704f3765fc/home-icon.png) | Centers the [Main Material node](/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine) in the **Material Graph** panel. |
| ![Hierarchy icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ec084ce-c581-4d3b-b6c4-9d168f31c09a/hierarchy.png) | Displays a list of all Material Instances using the current Material as a parent. |
| ![Live Update options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86cf9cd9-cf6f-4565-a923-df84322e03d3/live-update.png) | Toggle which elements in the Material Editor UI will update in realtime. |
| ![Clean Graph icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9a9bdc1-5039-44f2-9db9-4cbfb5d24b2c/clean-graph.png) | Deletes any Material nodes that are not connected to the Material. |
| ![Preview State toggle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b35c9bfe-f946-4e1b-ac1b-cd869684416f/preview-state.png) | Preview the graph state for a given feature level, Material quality, or static switch value. |
| ![Hide unrelated nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5776137-9e05-4097-8cb0-0cf882ae1bd1/hide-unrelated.png) | Hides all nodes that are not related to the selected nodes. |
| ![Material stats toggle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5b7c8a8-8725-4847-af5f-72eed387860a/stats-icon.png) | Shows or hides Material statistics in the **Stats** panel. |
| ![Platform Stats toggle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/040ffaf5-a0a9-436b-84ea-e5208a79c2de/platform-stats-icon.png) | Toggles the window that shows Material stats and compilation errors for multiple platforms. |

## Viewport Panel

![Material Editor Viewport panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c670eb5-06a1-4be7-a37e-c4651aa7195c/material-editor-viewport.png)

The **Viewport** panel displays the Material that you are currently editing.

You can navigate in the **Viewport** panel by using the options in the following table.

| Action | Description |
| --- | --- |
| Drag with the left mouse button | Rotate the mesh. |
| Drag with the middle mouse button | Pan |
| Drag with the right mouse button | Zoom |
| Hold down **L** and drag with the left mouse button | Rotate the light direction. |

You can change the viewport preview mesh using the associated toolbar controls (the five shape buttons in the bottom-right corner of the viewport). To use a custom preview mesh, select a **Static Mesh actor** in the Content Browser and click the **brick** icon in the viewport. The viewport mesh is saved with the Material so that the next time the Material is opened in a Material Editor, it will display the same mesh.

This table details the options available in the Material Editor preview viewport:

| **Icon** | **Description** |
| --- | --- |
| ![Preview meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/274e9d93-6de9-457c-b487-72625ad3dbf8/preview-meshes.png) | Shows the result of your current Material on the respective primitive shape in the **Preview** panel. |
| ![Viewport options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bfbdc682-5909-4751-8173-9580e5c018a9/viewport-options.png) | Toggles the Material **Viewport Options** |
| ![Viewport type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a1d2435-4c83-4647-a312-0c9cde34f578/viewport-perspective.png) | Changes the type of **Viewport** that is used. |
| ![Viewport lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/936bc004-a25c-433e-9494-a9b801ea2c61/viewport-lit.png) | Changes the type of lighting the **Viewport** is using. |
| ![Viewport show options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f90f79c7-3e7c-4c78-bc3e-07e7ec0ae516/viewport-show.png) | Enables additional options to the Material Viewport. |

## Details Panel

![Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fb1ae35-8605-4b4a-913f-6970b2d1284d/details-panel.png)

This panel contains a property window for all currently selected Material expression and function nodes. If no nodes are selected, the base properties of the Material are displayed.

See [Material Properties](/documentation/en-us/unreal-engine/unreal-engine-material-properties) for descriptions of all Material properties.

## Material Graph Panel

![Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd311cc9-3e8a-411d-9bd5-3787c78bacd8/graph-panel.png)

This panel contains a graph of all Material expressions that belong to this Material. By default, each Material contains a single base Material node. This node has a series of inputs, each associated with a different aspect of the Material that other Material nodes can connect to.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2b0b66c-ecb6-4b1e-8aaf-c625df3681de/materialeditor_materialnode.png "MaterialEditor_MaterialNode.png")

See [Material Inputs](/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine) for descriptions of the various inputs on the Main Material node.

## Palette Panel

![Material Editor palette](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51daa952-611d-4bf5-ab2c-0416d140a644/palette-panel.png)

The **Palette** panel contains a categorized list of all the Material nodes you can drag into your Material. To place a new Material node, drag it from the Palette into the **Material Graph** panel.

The Palette is hidden by default. Click the **Palette** tab in the upper-right corner of the Material Editor to display the Palette. Click the **Pin** icon if you want the Palette to remain visible while you work.

![Open Material Palette](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af7d4aab-f5e4-487d-9184-8a64d6686232/palette-open.png)

You can filter the Material nodes listed in the **Palette** panel by choosing either **Expressions** or **Functions** in the **Category** drop-down list.

For more information about Material functions, see [Material Functions](/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview).

### Stats Panel

![Stats panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9741216f-38dd-41e9-90bf-d2d86e88b35d/stats-panel.png)

The number of shader instructions used in the Material as well as any Compiler Errors are displayed in this panel. The fewer the number of instructions, the less costly the Material. Material expression nodes that are not connected to the base Material node do not contribute to the instruction count (cost) of the Material.

### HLSL Code Panel

![HLSL Code panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/257a4fbc-63a7-48a9-bfd9-dee16f6b637a/hlsl-panel.png)

This panel shows the **High Level Shader Language** (HLSL) code that is generated by the current Material. Be aware that this is not an editor; you will not be able to change the HLSL code. Rather, this is merely a viewer to allow you to visualize the code defined by your Material network.

By default the **Code View** panel is not visible. To display the **Code View** panel, open the **Window** menu and click on **HLSL Code**.

### Platform Stats

You can view the cost of your Material on various platforms by clicking on the **Platform Stats** icon.

![Platform Stats](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dedff3bc-8524-4cf2-a5d0-3c2fddd9be9b/platform-stats-01.png)

You can view stats for each rendering API Unreal Engine suports by clicking on the **Settings** option and then selecting the renderer you want to see stats for.

![Platform Stats settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0223279-59d4-4729-9500-ef5bdc04fc75/platform-stats.png)

In order to see stats for **Android** you will need to first install **Mali Offline Compiler** by doing the following:

1.  Download and install the [Mali Offline Compiler](https://developer.arm.com/products/software-development-tools/graphics-development-tools/mali-offline-compiler/downloads).
    
2.  After installing the Mali Offline Compiler go to **Edit** \\> **Editor Preferences** in the menu bar.
    
    ![Editor Preferences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/738ab9a1-9068-4689-b125-b59bf0ce6d4e/editor-preferences.png)
3.  Under **Content Editors** select **Material Editor**
    
    ![Material Editor preferences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57b48d68-38db-4da1-af8a-dd7892157d78/editor-preferences-material-editor.png)
4.  Click the **three dots** to the right of the **Mali Offline Compiler** option, and then locate the **malisc.exe** file that was installed with the Mali Offline Compiler. The default file path is shown below.
    
    ![Mali Compiler](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2677b41a-9a73-4704-834b-2c81e24463e0/mali-compiler.png)
5.  After the previous steps are complete, you can see stats for the various Android renderers supported by Unreal Engine.
    
    ![Android platform stats](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1d511e0-2221-4ba9-a0b2-f15692210bb7/platform-stats-android.png)

You cannot see the Android Platform stats without installing the Mali Offline Compiler.

## Graph Controls

Controls in the Material Editor generally match the controls of other tools in the Unreal Editor. For example, you can navigate the Material Expression graph as with other node-based object editors (Blueprints). You can orient the Material preview mesh as per other mesh tools.

### Mouse Controls

| **Control** | **Action** |
| --- | --- |
| **RMB drag on background** | Pan Material expression graph |
| **LMB drag on background** | Box select |
| **Rotate Mouse Wheel** | Zoom in and out |
| **LMB + RMB drag** | Zoom in and out |
| **LMB click on object** | Select expression/comment |
| **Ctrl + LMB on object** | Toggle selection of expression/comment |
| **LMB click + drag** | Move current selection/comment |
| **Ctrl + LMB drag** | Box select (add to current selection) |
| **LMB drag on connector** | Create connection (release on connector) |
| **Ctrl + LMB drag from connection** | Move connection (release on same type connector) |
| **Shift + single-click LMB on connector** | Marks the connector. Performing the action again with a connector marked will create connection between the two connectors. This is a quick way of making connections over large distances. |
| **RMB on background** | Bring up **New Expression** menu |
| **RMB on object** | Bring up **Object** menu |
| **RMB on connector** | Bring up **Object** menu |
| **Alt + LMB on connector** | Break all connections to connector |
| **Ctrl + LMB on connector** | Add a new node along connector |

### Keyboard Controls

| **Control** | **Action** |
| --- | --- |
| **Ctrl + B** | Find in Content Browser |
| **Ctrl + C** | Copy selected expressions |
| **Ctrl + S** | Save Material |
| **Ctrl + V** | Paste |
| **Ctrl + D** | Duplicate selected objects |
| **Ctrl + Y** | Redo |
| **Ctrl + Z** | Undo |
| **Delete** | Delete selected objects |
| **Spacebar** | Force update all Material expression previews |
| **Enter** | (same as clicking apply) |

### Hotkeys

You can use hotkeys to place commonly used Material expression types. Hold down the hotkey and **left-click** to drop in the node. The hotkeys are as follows:

| **Hotkey** | **Expression** |
| --- | --- |
| **A** | Add |
| **B** | BumpOffset |
| **C** | Comment |
| **D** | Divide |
| **E** | Power |
| **F** | MaterialFunctionCall |
| **I** | If |
| **L** | LinearInterpolate |
| **M** | Multiply |
| **N** | Normalize |
| **O** | OneMinus |
| **P** | Panner |
| **R** | ReflectionVector |
| **S** | ScalarParameter |
| **T** | TextureSample |
| **U** | TexCoord |
| **V** | VectorParameter |
| **1** | Constant |
| **2** | Constant2Vector |
| **3** | Constant3Vector |
| **4** | Constant4Vector |
| **Shift + C** | ComponentMask |