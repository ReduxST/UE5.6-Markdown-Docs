# CubeGrid

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cubegrid-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cubegrid-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:59

---

The **CubeGrid** tool creates blockout meshes using a repositionable grid. You can use CubeGrid to create a new mesh or edit the selected mesh.

The **Push** and **Pull** actions are helpful in quickly building level prototypes.

## Accessing the Tool

CubeGrid is located in the **Create** category of **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

## Using CubeGrid

What makes CubeGrid an efficient tool for blocking out a level are the tool's operations coupled with hotkey commands. Below are hotkeys for building out your grid and adjusting its size.

| **Hotkey** | **Description** |
| --- | --- |
| **Click** | Makes a grid selection. |
| **Click + Drag** | Dynamically creates an array of rows and columns. |
| **Shift + Click** | Creates an array of rows and columns between the initial and second positions clicked. |
| **Ctrl + E** | Increases the grid size. |
| **Ctrl + Q** | Decreases the grid size. |
| **Shift + E** | Shifts your selection forward one grid cell. |
| **Shift + Q** | Shifts your selection backward one grid cell. |

Once your grid is selected, you can use the **Actions** buttons or the following hotkeys to build your mesh.

| **Hotkey** | **Description** |
| --- | --- |
| **Ctrl + Drag** | Push or pull geometry from the selected grid. |
| **E** | Pull geometry from the selected grid. |
| **Q** | Push from the selected grid. |
| **Z** | Enters **Corner Mode**, where you can select corners of your selected grid that are pushed or pulled by **Ctrl + Drag** or **E/Q**. Press **Z** again to apply the change. |

You can reposition the grid using the grid gizmo (toggled with the **R** key) or by **Ctrl + Middle-Click**, which will move the gizmo to the corner of the nearest cell. You can also set specific position and orientation in the **[Tool Properties](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#accessingmodelingmode)** panel or reinitialize from the transform of a created mesh.

See **Shortcut Info** in the **Tool Properties** panel to learn more about the various hotkeys for the tool.

## Output

After you finish editing the mesh, you can choose the following **Output Types**:

-   Static mesh
-   Dynamic mesh
-   Volume

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#toolsundohistoryandacceptingchanges) panel.

To learn more about the Output Types and their use cases, see [Working with Meshes](/documentation/en-us/unreal-engine/working-with-meshes-in-unreal-engine). For a concept breakdown of blockouts and when to use it, see [Blockouts and Stand-in Meshes](https://dev.epicgames.com/community/learning/tutorials/bXd/unreal-engine-blockouts-and-stand-in-meshes).