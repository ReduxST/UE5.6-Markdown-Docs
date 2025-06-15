# Paint PolyGroups

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paint-polygroups-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paint-polygroups-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:30

---

The **Paint PolyGroups** tool provides the means for interactively painting PolyGroups on a mesh. A PolyGroup is a set of grouped triangles. You can use PolyGroups for various operations, such as:

-   Modeling and deformation
-   Traditional box modeling
-   UV layout
-   Material organization
-   Skin weights

To learn more, see [Understanding PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine).

## Accessing the Tool

You can access the Paint PolyGroups tool from the following:

-   The **Attributes** category in **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
-   The **Editing Tools** tab in the **Skeleton Editor**. To learn more, see [Skeleton Editing](/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).

## Using Paint PolyGroup

The Paint PolyGroups tool carries over preexisting groupings when opening the tool. Choose the PolyGroup layer you want to edit from the **Active PolyGroup** property. To create new layers, use the [Edit Attributes](/documentation/en-us/unreal-engine/edit-attributes-tool-in-unreal-engine) or [Generate PolyGroup](/documentation/en-us/unreal-engine/generate-polygroups-tool-in-unreal-engine) tools.

Use the **Action** setting to choose any of the following selection modes for painting PolyGroups:

-   **Brush:** Paints PolyGroups with a brush. **Click + Drag** across the mesh to paint.
-   **Fill:** Fills the entire component with the current group. **Click** the mesh to add the fill.
-   **Group Fill:** Fills only the hovered group(s) with the current set group ID.
-   **Poly Lasso:** Draws an area on the mesh to paint the current group ID. **Click + Drag** to highlight an area of the mesh to add PolyGroups.

To create a different PolyGroup, add a value in the **Set Group** property. The value represents the group ID. You can erase groupings by adding the group ID to the **Erase Group** property and using the **Shift + Click + Drag** hotkey. To view the current group IDs, toggle the properties in the **Visualization** section or use the **Shift + G** hotkey.

To help control group selection, use the quick action buttons in the **Freezing** and **Operations** sections.

Once you are done using the tool, accept or cancel the changes in the [Tools Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#tools,undohistory,andacceptingchanges) panel.

### Hotkeys

| **Hotkey** | **Description** |
| --- | --- |
| **Shift + Click + Drag** | Erases painted PolyGroups. |
| **\[ or S** | Decreases the brush size. Hold **Shift** for smaller steps. |
| **\] or D** | Increases the brush size. Hold **Shift** for smaller steps. |
| **Shift + Q** | Creates a new group and applies it to **Set Group**. |
| **Shift + G** | Assigns the hovered group as the **Set Group**. |
| **Shift + F** | Freezes or unfreezes the hovered group. |
| **Enter** | Accepts tool changes. |
| **ESC** | Cancels the changes and exits the tool. |