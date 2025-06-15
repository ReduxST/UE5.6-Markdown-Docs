# Filters and Collections

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:39

---

**Filters** and **Collections** are two different ways to sort and group Assets inside the Content Browser. There are a few key differences between them:

-   Filters **automatically** show or hide Assets in the Asset View. You can have multiple filters active at the same time, and toggle them on or off individually. Filters are saved locally and shared across projects.
    
-   Collections contain **manually** added references to Assets. You can only view the contents of one collection at a time in the Asset View. Collections can be local to your machine, or you can share them with other users.
    

Filters and Collections apply to individual Content Browsers. This means that you can have different Content Browsers displaying different types of Assets - for example, one Content Browser could display only Static Meshes belonging to a specific Collection, and another could display the 20 most recently opened Assets.

## Asset Filters

**Filters** provide a way to narrow down the Assets visible within the Asset View of the Content Browser. Filters can be based on either:

-   Asset type, such as Blueprints, Materials, Static Meshes, and so on.
    
-   Asset state, such as whether an Asset is currently checked out of source control.
    

Unlike Collections, you can have multiple filters active at the same time.

### Enabling Filters

To enable a filter, you must first add it to the **Filters** area of the **Content Browser**. To do this, from the Content Browser's **Search** bar, click the **Filters** drop-down (highlighted in the screenshot below). This opens a menu which shows all available filters you can select from, divided into specific categories.

![Filters drop-down in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12dccff0-212b-47bd-8a20-ea925cb17feb/ue5_1-filters-button.png)

Click a filter to add it to the **Filters** area. You can also add all filters under a category by clicking the category itself. The checkbox next to a filter category shows whether any filters in that category are enabled:

-   A plus sign (**+**) means all filters in that category are enabled.
-   A minus sign (**\-**) means only some filters in that category are enabled.
-   An empty checkbox means no filters in that category are enabled.

Filters are additive, which means that any new filters you add will increase the number of possible Assets that display in the Asset View. For example, if you start by selecting the **Static Mesh** filter, you will only see Static Meshes. If you then select the **Blueprint** filter, you will see Static Meshes and Blueprints.

You can also create **custom filters** from the drop-down menu. Go to **Custom Filter > Create New Filter**, then enter the following information in the window that appears:

![Creating a custom filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f9241f6-cacd-4880-bbd3-57ed67ae8fdf/ue5_1-create-custom-filter.png)

-   **Filter Label**: Give your filter a name. Filter names must be unique.
-   **Color**: Use the color wheel to select the color that this filter will use in the Filters area of the Content Browser.
-   **Filter String**: Enter the criteria for the Assets shown by this filter. You can use [advanced search operators](/documentation/en-us/unreal-engine/advanced-search-syntax-in-unreal-engine).

### Disabling Filters

There are two ways to disable filters:

-   Click the filter in the **Filters** area to toggle it on and off. Deactivated filters are grayed out and have no effect. To turn a filter back on, click it again. Disabling a filter in this manner does not remove it in the **Filters** area.
-   From the **Filters** drop-down, navigate to an enabled filter and click its name to disable it. This action also removes the filter from the **Filters** area.

![An example of enabled and disabled filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac1fd44b-60fe-4ebd-a743-592c8988ed7a/ue5_1-enabled-and-disabled-filters.png)

In this example, the Level and Material filters are enabled, and the AnimBP and devAssets filters are disabled.

### Deleting Custom Filters

Deleting a custom filter using this workflow does **not** have a confirmation dialog and cannot be undone.

To delete a custom filter, follow these steps:

1.  From the **Filters** drop-down, go to **Custom Filters**.
    
2.  Click the **Edit** button (![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ea03b2d-3fe3-4d29-bfd8-c9d7117b8b24/ue5_1-edit-icon.png)) next to the filter you want to delete.
    
3.  In the window that opens, click the **Delete** button.
    

### Bulk Filter Operations

Right-clicking a filter in the **Filters** area opens a context menu with the following available operations:

| **Operation** | **Description** |
| --- | --- |
| **Remove: \[Filter Name\]** | Removes this filter from the **Filters** area. If it is a custom filter, it will not be deleted and you can re-add it from the **Filters** drop-down. |
| **Enable Only This: \[Filter Name\]** | Disables all other filters except for the currently selected one. |
| **Enable All Filters** | Enables all filters. |
| **Disable All Filters** | Disables all filters. Note that this doesn't remove any filters from the Search and Filters bar. |
| **Remove All Filters** | 
Removes all filters from the Search and Filters bar.

This operation cannot be undone.



 |
| **Remove All But This: \[Filter Name\]** | 

Removes all filters except for the currently selected one from the Search and Filters bar.

This operation cannot be undone.



 |

### Using the Recently Opened Filter

Use the **Recently Opened** filter to view the 20 most recently opened Assets for a selected folder. You can find this filter in the **Filters** drop-down, under the **Other Filters** category.

When using the Recently Opened filter, selecting the **Content** folder will display the most recently opened Assets for the entire project folder. Selecting a sub-folder might show only a few items, or nothing at all. The list is dependent on the most recently opened Assets being contained within the folder being selected.

Note that this filter can return fewer than 20 items, or even no items, if you're working in a brand new project.

![The Recently Open filter in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10fe7582-09a1-4e57-bad0-ece937626895/ue5_1-recently-opened-filter.png)

In this example, the Recently Open filter only shows 8 items, because these are the only items that were opened since the project was created.

You can change the number of Assets listed by the Recently Opened filter. In **Editor Preferences**, under **Content Browser**, change the **Number of Assets to Keep in the Recently Opened Filter**.

## Collections

**Collections** serve as a way to organize sets of Assets into groups. Unlike folders, Collections don't contain the Assets themselves, but only references to those Assets. In practice, this means that one Asset can belong to more than one Collection.

Collections display in the **Sources** panel, under the folder tree.

### Creating Collections

To create a new Collection, follow these steps:

1.  Click the **Add** (**+**) button on the Collections panel.
    
    ![Adding a new Collection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fae4f98d-7434-43d6-9006-4ce9c9fea230/adding-collections.png)
2.  Select the Collection **type**.
    
    ![Selecting a Collection type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eaeb1f67-d7d4-4a9d-816b-21a229869e7d/collection-type.png)
    
    You can choose from one of the following options:
    
    | **Type** | **Description** |
    | --- | --- |
    | **Shared Collection** | Shared Collections are visible to other users. This option is only available if you're working in a multi-user project. |
    | **Private Collection** | Private Collections are available only to the users who have been specifically invited to view the Collection. This option is only available if you're working in a multi-user project. |
    | **Local Collection** | Local Collections are only available on your local machine. |
    
3.  Enter a name for your new Collection, then press **Enter**.
    

You can create child Collections by right-clicking a Collection, then selecting **New** from the context menu that appears and following steps 1-3 outlined above.

### Adding Assets to Collections

You can add one or more Assets to a Collection by using one of the following methods:

-   Click the Asset to select it, then drag it into a Collection.
    
-   Right-click the Asset. Then, from the context menu, select **Manage Collections**, and click the Collection you want to add the Asset to.
    
    Collections the Asset already belongs to will have a check mark next to their name.
    
-   Click the Asset to select it, then enable the check mark next to the Collection you want to add the Asset to.
    
    If the Asset is already a part of that Collection, the check mark next to the Collection will already be enabled. In this case, clearing the check mark will **remove** the Asset from that Collection.
    

If you add an Asset to a Collection that has a parent Collection, the Asset will also be added to the parent Collection.

### Removing Assets from Collections

You can remove Assets from a Collection by using one of the following methods:

-   Right-click the Asset. Then, from the context menu, select **Manage Collections**, and click the Collection you want to remove the Asset from.
    
    Collections the Asset already belongs to will have a check mark next to their name.
    
-   Click the Asset to select it, then disable the check mark next to the Collection you want to remove the Asset from.
    

If you select an Asset in a Collection and press **Delete**, you can delete the Asset entirely. You will get a prompt verifying that this is what you want to do, but keep in mind that deleting an Asset means it is **completely** removed from your project. To simply remove an Asset from a Collection, always use one of the methods described above.

### Renaming and Deleting Collections

To rename a Collection, right-click it and select **Rename** from the context menu. Then, enter a new name and press **Enter**. To cancel the rename, press **Escape**.

To delete a Collection, right-click it and select **Delete** from the context menu, then click **Delete** on the confirmation window that appears. Note that, since Collections are references to the actual Assets, deleting your Collections will not delete the Assets within the Collection.