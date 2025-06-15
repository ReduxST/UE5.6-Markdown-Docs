# Warp

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/warp-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/warp-tool-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:56

---

The **Warp** tool reshapes a mesh using non-linear transforms such as bend, flare, and twist.

## Accessing the Tool

You can access the Warp tool from the following:

-   The **Deform** category in **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
-   The **Editing Tools** tab in the **Skeleton Editor**. To learn more, see [Skeleton Editing](/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).

## Using the Tool

You can choose the following transforms from the **Operation Type** property to deform your mesh:

-   Bend
-   Flare
-   Twist

The Warp tool has a unique gizmo (additional t-shape handles) to adjust the amount of deformation. To place the gizmo in a specific mesh region, use **Ctrl + Click**. The handles are represented numerically as the following in the **Options** section:

-   Upper Bound
-   Lower Bound
-   Degree or percentage

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#tools,undohistory,andacceptingchanges) panel.

### Hotkeys

| **Key Command** | **Operation** |
| --- | --- |
| **Ctrl + Click** | Repositions the gizmo. |
| **F** | Zooms into the location of the mesh. |
| **ESC** | Cancels the changes and exits the tool. |
| **Enter** | Accepts the tool changes. |