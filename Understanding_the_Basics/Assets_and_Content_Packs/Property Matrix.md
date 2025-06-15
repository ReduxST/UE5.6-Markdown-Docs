# Property Matrix

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/property-matrix-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/property-matrix-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:02

---

While working in a level with multiple actors, updating individual properties at once can become time-consuming. You can use the **Property Matrix** to complete bulk edits and compare values for large numbers of objects or actors. It displays a configurable set of properties for a collection of objects as columns in a table view. The Property Matrix also provides a standard property editor that displays all properties for the current selection set.

![Propterty Matrix in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8734893a-452a-4522-8fbc-bdea22f16f05/ue-5-3-property-matrix-gif.gif)

## Features

| Feature | Benefits |
| --- | --- |
| **Bulk Object Editing** | 
-   Easier workflow for setting a series of varying values to a bunch of objects, without sacrificing the ability to set the property on a bunch of objects to the same value.
-   Works with thousands of objects at the same time.
-   Can handle editing a wide variety of object types at the same time.



 |
| **Bulk Fine-Grain Object Comparison** | 

-   Sort the values on thousands of objects at a time.
-   Quickly find assets and Actors with incorrect settings.



 |
| **Deep Property and Array Support** | 

-   Do all of the above with the properties of arrays and struct types.
-   Can expose columns for any property.
-   Handles array indices.



 |

## Accessing the Property Matrix

You can access the Property Matrix by:

-   Select the Property Matrix button in the **Details** panel adjacent to the **Search** bar.
-   In the **Content Browser**, make a selection of assets, right-click, choose **Asset Actions**, then choose **Edit Selection in Property Matrix** from the context menu.
-   In the **Outliner**, right-click your selection, then choose **Edit Selection in Property Matrix** from the context menu.
-   In the **Outliner**, right-click your selection, then choose **Edit Components in the Property Matrix** to select any shared component types from the context menu.

## Using the Property Matrix

The Property Matrix is a table that handles data like other grid-based editors. All cells have two modes: Display and Edit. Depending on the current mode, the cells' feature set changes.

### Adding and Removing Columns

You can add and remove columns by pinning and unpinning properties in the **Pinned Columns** panel. The list of properties in the panel is referred to as the property tree.

![Adding Column](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8225b1d-aa46-40cc-a281-dbd5e2db951f/pinning-column.png)

Columns can also be removed by right-clicking the column headers or by **middle-clicking** the column header itself.

![Remove Property Matrix Column](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/add3aa72-7041-4ff8-801f-7e4f6170fc40/ue5-3-remove-column.png)

The Property Matrix attempts to auto-populate the table with valuable columns based on the types of objects bound to the table.

### Editing Properties

Most cells display their bound value as text and lets you edit the text representation, but cells are fully customizable by the programmer and can vary greatly. For example, some cells have completely custom cell implementation such as boolean and color values.

![Editing Property Matrix](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38529d85-c7b7-49dd-bdcc-968321e42d59/ue-5-3-property-edit.png)

The property tree is bound to the selected rows in the table. This bounding means the changes you make to the properties are only applied to the selected items.

![Propterty Matrix in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f4a3e59-e763-4c8b-8c8e-a0547a79e5be/ue-5-3-property-matrix-bundle-edit.gif)

While in the table, settings are applied to the last cell you select.

![Propterty Matrix in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73b496ea-09fe-453d-96a9-9a4af74eee09/ue-5-3-property-selection-edit.gif)

You can also copy selected cells and paste them to relative settings in the table.

![Propterty Matrix in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab7d9d7d-a7d0-4d3f-b455-5d4a21de2f5c/ue-5-3-property-copy-paste-data.gif)

Additional editing features include:

-   Comparing property values deep in an object.
-   The handling of array indices.

To view the path of a property in your column, hover the cursor over the header name.

Your level updates as properties are changed; however, you must click the save icon to apply the settings officially.

### Sorting

You can sort columns in ascending or descending order by clicking the column header. An arrow appears on the header to tell you how the column is sorted.

## Controls

| Control | Description |
| --- | --- |
| Keyboard Controls |   |
| **Escape** | Exits edit mode in the current cell. Some cells have complex editing widgets which have their own behavior for escape which will take priority, so the user may need to press escape multiple times. |
| **Ctrl + C** | Copies the current cell's string representation to the clipboard. |
| **Ctrl + V** | Set the current cell's value as the text in the clipboard. |
| **Ctrl + A** | Selects all cells in the table. |
| **Home** or **Ctrl + Left Arrow** | Moves the current cell to the first cell in the current row. |
| **End** or **Ctrl + Right Arrow** | Moves the current cell to the last cell in the row. |
| **Ctrl + Home** | Moves the current cell to the first cell in the table. |
| **Ctrl + End** | Moves the current cell to the last cell in the table. |
| **Left Arrow** or **Shift + Tab** | Moves the current cell to the previous cell in the current row. |
| **Right Arrow** or **Tab** | Moves the current cell to the next cell in the current row. |
| **Up Arrow** | Moves the current cell to the previous cell in the column. |
| **Down Arrow** | Moves the current cell to the next cell in the column. |
| **Ctrl + Up Arrow** | Moves the current cell to the first cell in the column. |
| **Ctrl + Down Arrow** | Moves the current cell to the last cell in the column. |
| **Shift + Up Arrow** | Moves the current cell to the previous cell in the current column and adds its row to the existing selection. |
| **Shift + Down Arrow** | Moves the current cell to the next cell in the current column and adds its row to the existing selection. |
| **Ctrl + Shift + Up Arrow** | Moves the current cell to the first cell in the current column and selects all rows between them. |
| **Ctrl + Shift + Down Arrow** | Moves the current cell to the last cell in the current column and selects all rows between them. |
| **F2** | The current cell enters edit mode. |
| Mouse Controls |   |
| **LMB Click** on Cell | Clicked cell becomes the current cell and the cell's row becomes the new selection. |
| **Ctrl + LMB Click** on Cell | If the clicked cell did not belong to an already selected row, the cell becomes the current cell and the cell's row is added to the current selection, otherwise the cell's row is removed from the selection. |
| **Shift + LMB Click** on Cell | Clicked cell becomes the current cell and all the rows between the original current cell's row and the click cell's row are added to the existing selection. |
| **LMB Click** on Current Cell | Current cell enters edit mode. |
| **LMB Double-Click** Cell | Cell becomes the current cell and enters edit mode. |
| **MMB Click** on Column Header | Removes the column from the table. |
| **MMB Click** on Property in Details Panel | Toggles pinning of the clicked property to the table. |