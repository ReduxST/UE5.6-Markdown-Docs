# Reference Viewer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reference-viewer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reference-viewer-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:11

---

This page defines Asset references and how to view them in Unreal Engine. It also gives an overview of the Unreal Engine tools for identifying Asset references, as well as their settings and other functionality.

## What Are Asset References?

If an Asset makes use of another Asset in some way, we say that the first Asset **references** the second one.

For example, if a **Cube Actor** uses a **Color Material**, the Actor references that Material. We can also say that the Actor has a **dependency** on that Material. Think of it this way: the Actor needs the Material to look as it should.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/187b2b57-12e8-4ae3-976d-bc3bf0985558/ue5_1-referenced-asset.png)

In the example above, the **DistanceToNearest\_Mat\_Gradient** Material references the **OceanNoise** Texture2D Asset.

References are one-way (unidirectional). The referenced Asset has no reference back to its referrer.

## Reference Viewer Tool

The **Reference Viewer** displays a graph of Assets that reference or are referenced by one or more Assets.

To open the Reference Viewer:

1.  In the **Content Browser**, select one or more Assets.
    
2.  Right-click the selected Asset(s). Then, from the **context menu**, select **Reference Viewer**.
    

If you selected:

-   One Asset, the **Reference Viewer** displays that Asset's references.
    
-   Multiple Assets, you only see the references that your selected Assets have in common.
    
-   A folder, you see a graph of references for all Assets in that folder.
    

Click the image for full size.

The screenshot above illustrates the main elements of the Reference Viewer:

1.  Other Assets that reference the selected Assets.
    
2.  The selected Assets.
    
3.  Other assets that are referenced by the selected Assets.
    
4.  The Reference Viewer toolbar.
    
5.  The Search panel with several active Asset Filters.
    

These elements are described in detail below.

### Asset References

The Reference Viewer tool displays a graph of Assets that reference or are referenced by the selected Asset. The referencing relationship is shown by an arrow pointing towards the referenced Asset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59362525-373d-46d4-8226-9da9fbf57d82/ue5_1-reference-example.png)

In this example, the relationship between the M\_Tree\_FallTreeMerged\_01 Material and the other three Assets is made clear by the three arrows connecting them.

Right-click any Asset in the graph to open a context menu with the following options:

| **Option** | **Description** |
| --- | --- |
| **Browse to Asset** | Opens a **Content Browser** window with the Asset selected. |
| **Edit** | Opens the Asset in its Editor. For example, a **World Asset** will open in the **Level Viewport**. |
| **Zoom to Fit** | Resizes the reference tree so that it fits inside the window. |
| **Re-Center Graph** | Generates a **new** reference tree for the selected Asset. |
| **Make Collection With** | Create a new **Collection** with the selected Asset's referencers or dependencies. |
| **Copy Referenced Objects List, Copy Referencing Objects List** | 
Copies a list of referenced or referencing Assets for the selected Assets to the clipboard, in text format. The list uses relative Asset paths.

Example:

```
	`[/Game/Foliage/Foliage_TallGrass - Dependencies] 	[HARD] 		/Game/Foliage/M_Lit_Foliage.M_Lit_Foliage`

Copy full snippet
```
\[/Game/Foliage/Foliage\_TallGrass - Dependencies\] \[HARD\] /Game/Foliage/M\_Lit\_Foliage.M\_Lit\_Foliage

 |
| **Show Referenced Objects List, Show Referencing Objects List** | 

Shows a list of referenced or referencing Assets for the selected Assets, in text format. The list uses relative Asset paths.

Example:

```
	`[/Game/Foliage/Foliage_TallGrass - Dependencies] 	[HARD] 		/Game/Foliage/M_Lit_Foliage.M_Lit_Foliage`

Copy full snippet
```
\[/Game/Foliage/Foliage\_TallGrass - Dependencies\] \[HARD\] /Game/Foliage/M\_Lit\_Foliage.M\_Lit\_Foliage

 |
| **Show Reference Tree** | 

Opens the **Reference Tree** tool.

The Reference Tree lists reference chains for a specific Asset. A reference chain is a list of references in which each object in the list references the objects below it in the list.

Right-click any Asset in the Reference Tree, then click **Select Actor** to select that Asset's Actor in the Level Viewport (if it exists).

To display script objects that reference the selected Asset, from the Reference Tree menu, enable the **Options > Show Script Objects** option. These references are not displayed by default.



 |
| **Size Map** | 

Shows a **size map** representing a visual breakdown of Asset and dependencies size (on disk or in memory). This helps with performance profiling.

You can also open a size map for an Asset and its references from the Content Browser by right-clicking the Asset and selecting **Size Map** from the content menu.



 |
| **Audit Assets** | Opens the **Asset Audit** tool, which shows detailed information about the selected Assets. You can export this information to a `.csv`file from the **Settings** menu (gear icon) in the upper right corner of the Asset Audit window. |

### Reference Viewer Toolbar

Located at the top of the Reference Viewer window, the **Reference Viewer toolbar** provides the following options:

![Reference Viewer toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b707daf7-8f42-462b-88a9-8b324afc901e/ue5_1-reference-viewer-main-toolbar.png)

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | **Refresh**, **Back**, and **Forward** buttons | These buttons behave in the same way as the Refresh, Back, and Forward buttons in a web browser. Use them to refresh the view and navigate to a previous view. |
| 2 | **View** menu | Contains options that offer granular control over what information displays in the Reference Viewer graph and how that information displays. |
| 3 | **Toggle Duplicate References** button | Toggles the display of duplicate references in the visual graph. |
| 4 | **Asset Filters** controls | 
The **Asset Type Filters** button (left) toggles filtering the Reference Viewer by the Asset type filters set in the **Search Panel** (see the next section).

The **Auto-Populate Asset Type Filters** button (right) automatically selects filters that correspond to all Assets visible in the reference graph. While this button is active, every time you select a new root Asset or change the graph parameters, the filters list in the Search Panel automatically populates with all of the Asset types that are in your graph

Use the **A** keyboard shortcut to toggle between filtered and unfiltered versions of the graph.



 |
| 5 | n/a | Relative path of the Asset whose dependencies are displayed in the graph. |

### Search Panel

In the upper-left corner of the Reference Viewer, use the **Search** panel to:

-   Find a reference or dependency by name.
-   Filter references by Asset type.
-   Configure the depth to which Unreal Engine searches for references and dependencies.
-   Restrict the search to a specific Asset Collection.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9f6f7c3-d24f-4d91-bd17-f98fc0a01a6a/ue5_1-reference-viewer-search-options.png)

The screenshot above illustrates the main areas of the Search Panel.

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | Search box | Search for references by Asset name. |
| 2 | Filters | Filter references by Asset type. These filters behave in the same way as [filters in the Content Browser](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine). |
| 3 | Search options | 
Use the following options to further configure which Assets appear in the Reference Viewer graph:

**Search References Depth:** The depth to which the engine searches for Assets that reference your selected Asset. For example, a value of 2 means that the graph displays not only the assets related to the selected asset, but also the assets that are related to those related assets. **Search Dependencies Depth:** The depth to which the engine searches for dependencies (Assets that your selected Asset(s) reference). For example, a value of 2 means that the graph displays not only the assets related to the selected asset, but also the assets that are related to those related assets. **Search Breadth Limit:** The number of references listed in a given column (reference or referenced by). For example, if an asset references 20 assets, but the value of the Search Breadth Limit is set to 10, only 10 assets display in that column. **Collection Filter:** Restrict your search to a single [Collection](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine).



 |

### Asset Nodes in the Reference Viewer

Each Asset in the Reference Viewer is represented by a **node** in the visual graph. Nodes are color-coded by Asset type and contain more information about the Asset, such as its name, type, thumbnail, and so on.

Nodes can be regular (fully displayed) or compact. Toggle between these two modes from the **View** menu in the Reference Viewer Toolbar (refer to the Reference Viewer Toolbar section above), or by using the **V** keyboard shortcut.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14602144-7c82-4dff-bec6-390ced8f95f6/ue5_1-regular-node.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab9cac83-ce0e-4759-bca8-e9d351c7db52/ue5_1-compact-node.png) |
| Regular node | Compact node |

#### Inactive Nodes

If you use filters, you might see some nodes that are inactive (they are semi-transparent and always in compact mode). These nodes are excluded by your current filters, but they exist between two Assets that are not excluded. Inactive nodes are still displayed so the chain of references remains clear.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a083a6ba-c75b-4587-9b0b-61850f931fbe/ue5_1-ghosted-nodes.png)

In this example, Material Assets are filtered out. The two Material nodes (M\_Tree\_FallBark\_01 and M\_Tree\_FallTreeMerged\_01) are still shown as inactive nodes to keep the reference chain intact.

#### Overflow Nodes

For large values of the **Search Breadth Limit** value in the Search Panel, the Reference Viewer won't display all Asset references at once. Instead, you will see an **Overflow** node. Double-click this node to view the remaining references.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e824a377-8140-49ee-8bb7-4d8fe7b1f09e/ue5_1-overflow-node.png)

The GIF below illustrates the use of overflow nodes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71d5e03d-9c7e-4ba1-896d-ad7ec0aed1ee/ue5_1-overflow-nodes-animated.gif)

### Reference Viewer Keyboard Shortcuts

| Function | Keyboard Shortcut |
| --- | --- |
| Referencers |   |
| Increase Referencer Search Depth | **R** |
| Decrease Referencer Search Depth | **SHIFT + R** |
| Set Referencer Search Depth | **CTRL + R** |
| Dependencies |   |
| Increase Dependency Search Depth | **D** |
| Decrease Dependency Search Depth | **SHIFT + D** |
| Set Dependency Search Depth | **CTRL + D** |
| Breadth Limit |   |
| Increase Breadth Limit | **L** |
| Decrease Breadth Limit | **SHIFT + L** |
| Set Breadth Limit | **CTRL + L** |
| Reference Types |   |
| Show/Hide **Soft** References | **S** |
| Show/Hide **Hard** References | **H** |
| Show/Hide **Editor Only** References | **E** |
| Show/Hide **Management** References *(Primary Asset IDs)* | **M** |
| Show/Hide **Name** References *(Searchable Names)* | **N** |
| Show/Hide **C++** Packages References | **C** |
| View |   |
| Show/Hide **Duplicate** References | **U** |
| Toggle Compact **View** | **V** |
| Toggle Asset **Path** as a Comment | **P** |
| Zoom to **Fit** | **F** |
| Toggle **Asset** Filters On/Off | **A** |
| Search | **CTRL + F** |
| Asset |   |
| Edit Asset | **CTRL + E** |
| Browse to Asset | **CTRL + B** |
| Copy Selected Asset Paths to the Clipboard | **N** |