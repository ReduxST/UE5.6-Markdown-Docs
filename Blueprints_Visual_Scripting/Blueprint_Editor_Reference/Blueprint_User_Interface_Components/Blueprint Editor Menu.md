# Blueprint Editor Menu

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/menu-for-the-blueprints-visual-scripting-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/menu-for-the-blueprints-visual-scripting-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:41

---

The **Menu** is displayed at the top of the Blueprint Editor by default.

### File

| Command | Description |
| --- | --- |
| **Load and Save** |   |
| **Save** | Saves the Blueprint. |
| **Open Asset...** | Summons the asset picker window. |
| **Save All** | Saves all unsaved levels and assets. |
| **Choose Files to Save...** | Opens a dialog with save options for content and levels. |
| **Connect to Source Control...** | If Source Control is enabled, opens a dialog with check-in options for content and levels. |
| **Blueprint** |   |
| **Compile** | Compiles the Blueprint. |
| **Refresh All Nodes** | Refreshes all nodes in the graph to account for external changes. |
| **Reparent Blueprint** | Change the parent of the open Blueprint. |
| **Diff** | Diff against previous revisions. Requires source control to be active. |
| **Developer** | Open the Developer Menu, where you can change compiler settings and recompile modules like the Graph Editor. |

### Edit

| Command | Description |
| --- | --- |
| **History** |   |
| **Undo** | Undo the last action. |
| **Redo** | Redo the last undone action. |
| **Undo History** | Displays the entire Undo History. |
| **Search** |   |
| **Search** | Find references to functions, events, variables, and pins in the current Blueprint. |
| **Find in Blueprints** | Find references to functions, events, variables, and pins in ALL Blueprints. |
| **Delete Unused Variables** | Deletes any variables that are never used. |
| **Configuration** |   |
| **Editor Preferences** | Opens the settings for the Editor. |
| **Project Settings** | Opens the settings for the current project. |
| **Plugins** | Opens the Plugin Browser tab. |

### Asset

<table class="table" style="--columns-count: 2;"><tbody><tr><td><strong>Find in Content Browser...</strong></td><td>Summons the <strong>Content Browser</strong> and navigates to this asset.</td></tr><tr><td><strong>Reference Viewer...</strong></td><td>Launches the reference viewer to show what the current asset references and what references the current asset.</td></tr><tr><td><strong>Size Map...</strong></td><td>Displays an interactive map showing the approximate size of this asset and everything it references.</td></tr></tbody></table>

### View

| Command | Description |
| --- | --- |
| **Pin Visibility** |   |
| **Show All Pins** | Shows all pins on all nodes. |
| **Hide Unused Pins** | Hides all pins with no connections and no default values. |
| **Hide Unconnected Pins** | Hides all pins with no connections. This option will hide input pins for inputs that have been set directly on the node. |
| **Zoom** |   |
| **Zoom to Graph Extents** | Fits the current view to the entire graph. |
| **Zoom to Selection** | Fits the current view to the selection. |

### Debug

| Command | Description |
| --- | --- |
| **Breakpoints** |   |
| **Disable All Breakpoints** | Disables all breakpoints in all graphs of the current Blueprint or Level Blueprint. |
| **Enable All Breakpoints** | Enables all breakpoints in all graphs of the current Blueprint or Level Blueprint. |
| **Delete All Breakpoints** | Removes all breakpoints in all graphs of the current Blueprint or Level Blueprint. |
| **Watches** |   |
| **Delete All Watches** | Removes all watch values in all graphs of the current Blueprint or Level Blueprint. |

### Window

The **Window** menu in the **Blueprint Editor** has a specific subsection for displaying Blueprint Editor-specific tabs. Not all tabs will be present in the menu while the Blueprint Editor is in the **Defaults** and **Components** modes.

| Command | Description |
| --- | --- |
| **Toolbar** | Shows the Toolbar if it is currently not visible. |
| **Details** | Shows the [Details](/documentation/en-us/unreal-engine/details-panel-in-the-blueprints-visual-scriting-editor-for-unreal-engine) pane if it is currently not visible. |
| **Debug** | Shows the **Debug** pane if it currently not visible. |
| **Palette** | Shows the [Blueprint Editor Palette](/documentation/en-us/unreal-engine/palette-in-the-bleprints-visual-scripting-editor-for-unreal-engine) pane if it is not currently visible. |
| **My Blueprint** | Shows the [Blueprint Editor My Blueprint Panel](/documentation/en-us/unreal-engine/my-blueprint-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine) pane if it is not currently visible. |
| **Compiler Results** | Shows the **Compiler Results** pane if it is not currently visible. |
| **Find Results** | Shows the **Find Results** pane if it is not currently visible. |
| **Components** | Shows the **Components panel** if it is not currently visible. |
| **Viewport** | Shows the **Preview Viewport** pane if it is not currently visible. |
| **Content Browser** | Opens a sub-menu with access to all four **Content Browsers**. |
| **Developer Tools** | 
-   **Blueprint Debugger**: Opens the Blueprint Debugger, which shows you the current "stack" of commands that is being run in a Blueprint along with all watched values.
-   **Collision Analyzer**: Shows the Collision Analyzer.
-   **Debug Tools**: Show the Debug Tools panel, which contains an assortment of functions for common debug tasks (reloading textures, showing texture atlases, gamma correction, etc...)
-   **Message Log**: Opens the Message Log. This is where errors or warnings from the Editor will go.
-   **Output Log**: Opens the Output Log. If you are debugging something using Print it will appear here.
-   **Visual Logger**: Opens the Visual Logger.
-   **Class Viewer**: Opens the Class Viewer.
-   **Device Manager**: Opens the Device Manager.
-   **Device Profiles**: Opens the Device Profiles Tab.
-   **Session Frontend**: Shows the Session Frontend. Please see the [Unreal Frontend](/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool) documentation for more information.
-   **Widget Reflector**: Opens the Widget Reflector. This enables you to see the various Slate elements that make up the interfaces within the Editor interface.



 |
| **Project Launcher** | Shows the Project Launcher which enables you to run your project on any appropriately setup and connected devices. |
| **Plugins** | Shows the Plugin Tab where you can load/unload plugins. |
| **Reset Layout...** | Restores the default layout for the entire Unreal Engine 4 Editor. This requires the Editor to restart, but it will re-open the current project. |
| **Save Layout** | Saves the current interface layout. |
| **Enable Fullscreen** | Enables fullscreen mode for the Main Editor window. |