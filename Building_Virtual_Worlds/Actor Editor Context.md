# Actor Editor Context

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-editor-context-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-editor-context-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:25

---

**Actor Editor Context** is an Editor feature that you can use to set a [Level](/documentation/en-us/unreal-engine/levels-in-unreal-engine), [Data Layer](/documentation/en-us/unreal-engine/world-partition---data-layers-in-unreal-engine), [Level Instance](/documentation/en-us/unreal-engine/level-instancing-in-unreal-engine), or [Outliner Actor Folder](/documentation/en-us/unreal-engine/outliner-in-unreal-engine) as the **current editor context**. When set to current, any Actors you add to the Viewport are assigned to the current context. Assigning a current Actor Editor Context helps keep your world organized when adding a large number of Actors by assigning them to a specified context automatically, such as keeping all the trees in an environment in a Trees Outliner folder and assigning them to a Trees Data Layer.

The Actor Editor Context set to the Trees Data Layer and Trees Actor Folder. Click image for full size.

A widget in the lower-right corner of the Viewport displays the currently active Level, Level Instance, Data Layer, or Actor Folder.

## Setting the Current Context

### Current Level

In worlds that don't use [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine), knowing which level you are working in is an integral part of the sublevel workflow. After adding sublevels to your Level using the Levels window, the Actor Editor Context displays the current Level:

Level window showing the Persistent Level with one sublevel named SubLevel. Click image for full size.

Actor Editor Context showing SubLevel as the current level. Click image for full size.

Using the dropdown menu in the Actor Editor Context widget, you can specify the current Level. All Actors you add to the Viewport are assigned to that Level.

Click the dropdown to change the current Level.

### Current Level Instance

Level Instancing is a Level-based workflow that creates prefabricated **Level Instances** you can place in your world more than once. When editing a Level Instance, Unreal Engine creates a new empty context and the Actor Editor Context widget displays the current Level Instance:

Actor Editor Context showing the current open Level Instance. Click image for full size.

All Actors you add to the Viewport are assigned to the currently open Level Instance. When you commit your changes to the Level Instance, the editor returns you to your previous Actor Editor Context.

### Current Data Layer

Data Layers control the loading and unloading of Actors both in the editor and at runtime. Unlike Levels, Actors can be assigned to more than one Data Layer. To set the current Data Layer (or Layers):

1.  If needed, open the **Data Layers Outliner** by selecting **Window > World Partition > Data Layer Outliner**.
2.  Right-click the Data Layer you want to make current and select **Make Current Data Layer (s)**.

Data Layer Outliner showing the Trees Data Layer set to current.

This adds the selected Data Layer to the current context. Its name and assigned debug color now display in the Actor Editor Context widget.

Actor Editor Context widget showing Trees as the current Data Layer. Click image for full size.

All Actors you add to the Viewport are assigned to the current Data Layer (or Layers). To clear the current Data Layer context, right-click in the Data Layer Outliner and select **Clear Current Data Layer(s)** or click the **X** button located in that section of the Actor Editor Context widget.

Clear the current Data Layer by clicking the X button in the Actor Editor Context widget.

### Current Actor Folder

Similar to Data Layers, you can also assign a current Actor Folder in the Outliner. To set the current Actor Folder:

1.  If needed, open the **Outliner** by selecting **Window > Outliner** and selecting one of the four Outliner instances.
2.  Right-click the folder you want to make current, then select **Make Current Folder** from the context menu.

Outliner showing Trees as the current Actor Folder.

This adds the selected folder to the current context. Its name now displays in the Actor Editor Context widget.

Actor Editor Context widget showing Trees as the current Actor Folder. Click image for full size.

All Actors you add to the Viewport are assigned to the current Actor Folder. To clear this context, right-click in the Outliner and select **Clear Current Folder** or click the **X** button located in that section of the Actor Editor Context widget.

Clear the current Actor Folder by clicking the X button in the Actor Editor Context widget.

## Toggling Actor Editor Context in the Viewport

The Actor Editor Context widget is enabled by default. To disable it, follow these steps:

1.  Click the **Viewport Options** button in the top-left corner of the Viewport, then select **Advanced Settings**. This opens the **Editor Preferences** window.
    
    Click the Viewport options button and select Advanced Settings at the bottom.
    
2.  Navigate to the **Look and Feel** section of the **Level Editor - Viewports** settings and clear the **Show Actor Editor Context** checkbox.
    
    The Level Editor - Viewports settings. Click image for full size.