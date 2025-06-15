# Dataprep Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:44

---

This page provides an overview of the Visual Dataprep system, and how to get started creating your own custom import recipes to prepare your 3D data for real-time visualization.

## Enabling Visual Dataprep

Enable the following plugins for your Project:

-   **DataPrep Editor**
-   **Datasmith Importer**
-   **Dataprep Geometry Operations** - This plugin is required for certain filters and operations.
-   If you want to import from other kinds of source files that Datasmith supports, you may need to enable other importer plugins for those file types. For details, see [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).

To learn how to enable plugins, refer to the [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) page.

If you started your Unreal Project from a Template in the **Architecture, Engineering, and Construction** or **Automotive, Product Design, and Manufacturing** categories, some of these Plugins may already be enabled.

## Visual Dataprep Assets

The Visual Dataprep system is based around a new kind of Asset, called a **Dataprep** Asset. This Asset is like a Blueprint in that it lays out a series of steps in a visual representation. However, the purpose of this Dataprep graph is to transform scene data read from one or more input files that you specify.

To create a new Dataprep Asset, right-click in the Content Browser and choose **Dataprep > Dataprep Asset** from the context menu.

Click image for full size.

## Dataprep Editor UI

Like Blueprint classes, Dataprep Assets have their own specialized editor window. You can open this window by double-clicking any Dataprep Asset in the **Content Browser**.

The Dataprep Editor UI is divided into several panels, which you'll use at different points in the [Dataprep workflow](/documentation/en-us/unreal-engine/dataprep-overview-in-unreal-engine#dataprepworkflow).

Click image for full size.

| Number | Name | Description |
| --- | --- | --- |
| 1 | **Toolbar** | Shortcuts for the most important user actions in the Dataprep workflow, including the **Import**, **Execute**, and **Commit** actions. |
| 2 | **Content Browser Preview** | Lists all Assets you have imported from your input files. This is a preview of the Assets that the Visual Dataprep system will create in your **Content Browser** when you **Commit** your graph. |
| 3 | **Viewport Preview** | Displays a visual preview of the 3D scenes you have imported from your input files. |
| 4 | **Outliner Preview** | Lists all Actors in the 3D scenes you have imported from your input files. This is a preview of the Actors the Visual Dataprep system will create in your Level, and the scene hierarchy that will be created in your Level's **Outliner**. |
| 5 | **Settings Panel** | 
Use this panel to specify the input files you want to import your 3D scenes from, and where you want the Assets to be created in your Project's **Content Browser**.

If you've exposed any parameters in your Dataprep graph so that they can be overridden in *instances* of your Dataprep Asset, you'll also see those parameters listed here in the **Parameterization** section. For details, see [Working With Dataprep Instances](/documentation/en-us/unreal-engine/working-with-dataprep-instances-in-unreal-engine).



 |
| 6 | **Palette** | Offers building blocks that you can drag into the Dataprep Graph Editor to build up your import recipe. |
| 7 | **Dataprep Graph Editor** | Area where you can prepare Dataprep recipes, which are left-to-right steps that you want the Dataprep system to take to prepare your input content for real-time visualization in Unreal Engine. |
| 8 | **Details Panel** | Like the **Details** panel in the main Level Editor, shows information about any Actor that you have selected in the **Outliner Preview**. Note that these settings are read-only. They are provided only for your information so you can evaluate the effects of your Dataprep Graph on your Actors. |

## Dataprep Workflow

The typical workflow for setting up a Visual Dataprep asset follows these steps:

1.  **Specify input files**: In the **Settings Panel** at the top right, create a new input producer for each file you want to import, or each folder of input files. Click the gear icon to configure additional geometry and tessellation options, such as **Chord Tolerance** and **Stitching Technique**.
    
    Click image for full size.
    
    You can also customize the following **Output** settings:
    
    -   **Folder** determines the name of the folder that will be created in your Project's **Content Browser** to hold your imported Assets. By default, your Assets are distributed by Datasmith into subfolders within this folder according to their type: one for Static Mesh Assets, one for Materials, one for Textures, and so on. (You can override this default distribution when you build your Dataprep graph, by using the **Output to Folder** operation.)
    -   **Level Name** sets the name of a new Level Asset that will be created to hold your scene. After you commit the results of the Dataprep graph, you'll be able to add the imported scene into any Level in your Project by adding that sublevel.
2.  **Preliminary import**: Press the **Import** button in the Toolbar to import your source files into a temporary world.
    
    You'll see the 3D viewport and other preview panels update with the content read from your file. This content has not yet been added to your Project. It is in a temporary world that only exists in the Dataprep Editor. This gives you an opportunity to modify the Assets and scene hierarchy read from your input files before you save the results to your Project.
    
    This step is technically optional, but it makes it easier for you to evaluate the effects of your Dataprep Graph as you build it.
    
3.  **Build the Dataprep Graph**: Drag **Select By** and **Operations** nodes from the Palette into the Dataprep Graph Editor, and connect your Action nodes in the order you want them to be carried out. See [Dataprep Graphs](/documentation/en-us/unreal-engine/dataprep-overview-in-unreal-engine#dataprepgraphs) below.
    
4.  **Test the Graph**: Press the **Execute** button in the Toolbar to run the data you've imported from your source files through the Dataprep Graph you've built. You'll see the preview panels update to show the results.
    
    Individual blocks or Action nodes can be disabled for debugging by right clicking on the name and choosing the **Disable** option. A disabled block or Action will be grayed out in the graph. They may be enabled by opening the menu again and choosing the **Enable** option.
    
5.  **Commit**: When you're happy with the effects of your graph on the 3D data imported from your input files, press the **Commit** button in the Toolbar to finalize the import process.
    
    When you commit the results, the Visual Dataprep system saves the Assets in the **Content Browser Preview** into Assets in your Project. It also modifies the Level that you currently have open to add the hierarchy of Actors shown in the **Outliner Preview**.
    
    If you prefer to import your Actor hierarchy into a new Level instead, set the name of the Level in the **Sub-Level** setting in the **Settings** panel. The Visual Dataprep system will create a new Level with this name (if it does not already exist), add your Actors to that Level, then add that Level as a sublevel within the Level that you currently have open in the main window of the Unreal Editor.
    

## Statistics Panel

Open the **Statistics** panel from the main menu of the Visual Dataprep asset editor: **Window > Statistics**. This panel shows a simple comparison of your data's metrics, such as draw calls, number of Actors, or total vertex count, before and after executing the Dataprep Graph.

Click image for full size.

## Dataprep Graphs

At the heart of every Dataprep Asset is the Dataprep Graph—the set of operations that the system will carry out on the input files you specify.

Click image for full size.

Every Dataprep Graph is made up of building blocks called **Action** nodes: vertical stacks of blocks. For example, the graph shown above contains three Action nodes. When you execute the Dataprep graph, it starts at the **Start** node on the left, then performs each Action node in order, from left to right.

You can resize Actions horizontally to read their full text by dragging their boundaries.

![Resizing an Action](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84505826-ca8e-47c0-ac7a-b6f9840e0f70/resize-dataprep-block.gif)

Unlike Blueprint graphs, where conditional branching is allowed, Dataprep graphs always progress from left to right, along a single linear execution path. In addition, there is no data flow between successive Action nodes. All Actions use the same context—a set of Assets and Actors that are imported from input files you provide.

Each Action is a stack of one or more blocks. When the Dataprep graph performs an Action, it treats each block in the Action node from top to bottom.

To start building an Action, you can drag blocks from the palette on the left into the graph editor, or right-click in the background of the graph editor and select blocks from the context palette.

You can group multiple Actions together. To do this:

1.  Click and drag to select the Actions you want to group.
2.  Right-click the group.
3.  From the context menu, select **Group Actions**.

You can disable all the Actions in an Action Group by right-clicking the group and selecting **Disable Action Group** from the context menu.

To ungroup Actions, right-click the group, then select **Ungroup Actions**.

### Operations, Filters, and Transforms

There are three basic types of blocks you can use in a Dataprep Action node:

-   **Operations** modify Assets, Actors, or Components in some predefined way. For example, the **Set Material**, **Compact Scene Graph**, and **Set Simple Collision** blocks shown above are all different types of operations.
    
    For details on all the different operations you can use in your Dataprep graphs, see [Dataprep Operation Reference](/documentation/en-us/unreal-engine/dataprep-operation-reference-in-unreal-engine).
    
-   **Filters**, also called **Select By** blocks, determine what Assets, Actors, and Components the operations under them in the current Action block should modify. By default, every Action step performs its operations on all Assets, Actors, and Components contained in the temporary world constructed from your input files. You can use these **Filter** blocks to define a subset of those objects, thereby controlling the objects your Action node will modify.
    
    For details on all the different selection filters you can use in your Dataprep graphs, see [Dataprep Selection Reference](/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine).
    
-   **Transforms** alter the current selection of Assets, Actors, and Components in potentially complex ways. In this respect, they are like filters. However, a filter block can only cut down the list of objects passed down to it. A transform block, by contrast, can add objects to the current selection.
    
    For example, you might want to select specific trees of objects from the scene hierarchy. To do this, you could use filter blocks to narrow down the full set of scene elements to a small number of specific parent elements, then use a transform block to re-expand that selection to include the children of the selected elements.
    
    For details on all the different transforms you can use to extend or modify the selected set of objects within an Action, see [Dataprep Selection Transform Reference](/documentation/en-us/unreal-engine/dataprep-selection-transform-reference-in-unreal-engine).
    

### Action Example

The Action pictured below sets a new Material on the parts of a CAD assembly. This node performs a sequence of steps, processing data through its stack of filters and operations, from top to bottom.

Click image for full size.

| Step Number | Name | Block Type | Description |
| --- | --- | --- | --- |
| 1 | **Input Pin** | N/A | Every Action gathers all data from the temporary world, including all Assets and Actors found in the imported files, and passes those objects to the block at the top of the stack. |
| 2 | **Filter by Tag** | Filter | This filter only keeps Actors that have the "Metal" tag, passing that list of Actors to the next block down. |
| 3 | **Filter by Actor Label** | Filter | This filter only keeps Actors whose names contain the word "Mechanical", passing those on to the next block down. |
| 4 | **Set Simple Collision** | Operator | This operator sets up a Box collision shape on all Static Mesh Assets that are referred to by the set of Actors passed down by the filters above. It then passes the same list of Actors on to the next block down. |
| 5 | **Set Material** | Operator | The last operator finds all Materials on all Static Mesh Components owned by the set of Actors passed down by the filters above, and replaces those Materials with the substitute specified in the **Material** setting in the block. |

After all blocks in this Action are done, the next Action in the graph begins executing. When the next Action starts, it once again gathers all data from the temporary world. All filters put in place by previous blocks are no longer considered. However, any changes made to the scene by previous Actions persist for the next Action—such as changing Materials, deleting Actors, and so on.

## Working with Filters

All filter blocks offer some additional options that make it easier for you to capture the exact list of Assets, Actors, and Components that you want to modify with your operation blocks, and to verify that your filters are having the effect you're expecting.

To access these options, right-click any filter block and look for the **Filter** section in the context menu.

Click image for full size.

If you want to affect multiple filter blocks, hold down the **Control** key and left-click all the blocks to build your selection. When all the blocks you want to affect are highlighted, right-click any highlighted block. Alternatively, click and drag to select multiple blocks.

## Creating a Filter from Selected Assets

With one or more Actors or Components selected from the Viewport, Outliner, or Asset panel, right-click anywhere in the Dataprep Graph Editor and, from the context menu, select **Create Filter From Selection**.

Click image for full size.

The new filter shows the number of Actors and Assets that will be selected, as well as the first Actors or Assets in the list.

You cannot edit this list directly, but you can create a new filter that includes this one by doing the following:

1.  Right-click the **Filter by Selection** filter in the Dataprep Recipe.
2.  From the context menu, select **Preview Filter(s)**. This will highlight the Actors and Assets in the World Outliner Preview panel that this filter selects.
3.  To add new Actors and Assets to the filter, hold the **Ctrl** key and click them in the World Outliner Preview panel.
4.  Right-click anywhere in the Dataprep Graph Editor and, from the context menu, select **Create Filter from Selection**.

### Inverting Filter Logic

Choose **Filter > Inverse Filter(s) Selection** to reverse the selection logic of any **Select By** block, turning it into an **Exclude By** block. When you do this, the operations in the same Action will apply only to the set of scene elements that do *not* match the criteria you set.

### Previewing Filter Results

Choose **Filter > Preview Filter(s)** to make the **Content Browser Preview** and the **World Outliner Preview** panels show a checkmark next to all the Assets and Actors that are selected by your filter.

Click image for full size.

You can only preview one filter, or one selected set of filters, at a time. If you start previewing a different filter or a different set of filters, your previous filters will stop previewing.