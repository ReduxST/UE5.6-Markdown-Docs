# Edit Pivot

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/edit-pivot-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/edit-pivot-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:33

---

The **Edit Pivot** tool changes a mesh's pivot location. The pivot is a fixed point in the scene that defines the center of a mesh for which rotation and scaling occur. The pivot also represents the location of your mesh.

You can use the Edit Pivot tool to change the pivot:

-   Manually with your cursor.
-   Automatically with preset buttons.

Edit Pivot is helpful in many areas of your modeling and non-modeling workflows. After editing or importing a mesh, you may have to adjust the pivot to an ideal location. Setting the pivot to a specific location on the mesh can help various processes, such as:

-   How a mesh snaps to an area of another mesh.
-   The direction in which a mesh bends and rotates.

## Accessing the Tool

You can access the Edit Pivot tool from the **XForm** (transform) category in **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

## Using Edit Pivot

When you open the Edit Pivot tool, the mesh's pivot location becomes visible (represented as a gizmo) in the level.

If the pivot does not appear on the mesh, it may be located outside of the mesh due to various reasons. Zoom out of the level to find the pivot or select the center preset in **Box Positions** to reposition the location automatically.

When you accept the new position, the location is baked into the mesh, meaning it's applied to the static mesh asset and any instances in the scene. To avoid changing the asset and position of any static mesh instance, you can copy the mesh to create a new actor with the [Duplicate](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#xform) tool.

### Adjusting Location

You can manually transform the pivot location by dragging the gizmo. To interactively snap the pivot to an area on the mesh, and decide if LODs (Level of Details) are affected, use the **Options** section.

| **Options** | **Description** |
| --- | --- |
| **Apply to All LODs** | Bakes the pivot transform to all available LODs. The setting has no effects on selections without LODs. |
| **Enable Snap Dragging** | Activates a freehand mode for transforming the pivot. You can click and drag on the mesh to snap the pivot's location. You can use **Rotation Mode** to adjust the rotation automatically. |
| **Rotation Mode** | 
Determines how to rotate the pivot during snap dragging. You can choose from the following:

-   **Ignore:** Only translates the pivot.
-   **Align:** Lines up the pivot's Z-axis and normals of the mesh to point in the same direction.
-   **Align Flipped:** Lines up the pivot's Z-axis to the opposite normals of the mesh.



 |

To numerically change the pivot's location and rotation, use the **Transform Panel**. To learn more about the modeling gizmo and how to access the Transform Panel, see the [Gizmo](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#gizmo) section of the overview documentation.

You can automatically snap the pivot to a location using the presets in the **Box Positions** section. The positions are based on the axes of the bounding box you choose in the **Use World Box** property.

To help determine the direction of the pivot, compare the gizmo's color to the [Level Editor's](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine) axes widget.

| **Box Positions** | **Description** |
| --- | --- |
| **Center** | Positions the pivot to the center-mass of the bounding box. |
| **Bottom** | Positions the pivot to the lowest point on the Z-axis of the bounding box. |
| **Top** | Positions the pivot to the highest point on the Z-axis of the bounding box. |
| **Left** | Positions the pivot to the lowest point on the Y-axis of the bounding box. |
| **Right** | Positions the pivot to the highest point on the Y-axis of the bounding box. |
| **Back** | Positions the pivot to the highest point on the X-axis of the bounding box. |
| **Front** | Positions the pivot to the lowest point on the X-axis of the bounding box. |
| **World Origin** | Positions the pivot to the world origin (0,0,0). |
| **Use Word Box** | Uses the world-space bounding box of the mesh instead of the mesh-space bounding box when enabled. |

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#toolsundohistoryandacceptingchanges) panel.

## Hotkeys

| **Hotkey** | **Description** |
| --- | --- |
| **F** | Zooms into the location of the mesh. |
| **CTRL + Drag** | Aligns the gizmo to the scene. |
| **Enter** | Accepts the tool changes. |
| **ESC** | Cancels the changes and exits the tool. |