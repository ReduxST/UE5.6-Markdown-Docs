# Deform PolyGroups

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/deform-polygroups-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/deform-polygroups-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:19:39

---

The **Deform PolyGroups** modeling tool dynamically alters the shape of a mesh through its [PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine). Deformation is an efficient way to reshape a mesh quickly and create organic geometry.

You can select vertices, edges, or faces and drag them along the world grid axes to deform the overall profile of a mesh. You can also apply multiple deformations in a single tool session.

If your mesh does not deform as expected, your resolution (triangle count) may be too low. You can use the **[Remesh](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#mesh)** tool to re-triangulate.

## Accessing the Tool

You can access the Deform PolyGroups tool from the following:

-   The **Deform** category in Modeling Mode. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
-   The **Editing Tools** tab in the **Skeleton Editor**. To learn more, see [Skeleton Editing](/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).

## Settings

### Options

The two core options for using the tool are **Deformation** and **Transformation**.

You can choose between **Linear** and **Smooth** for the type of deformation to occur.

| **Deformation** | **Description** |
| --- | --- |
| **Linear** | PolyGroup edges connected to the selected component remain straight. |
| **Smooth** | PolyGroup edges connected to the selected component are smoothly interpolated into a curve. |

The Transformation option determines the type of movement that occurs when selecting a component.

| **Transformation** | **Description** |
| --- | --- |
| **Translate** | Move the selected components linearly on the X, Y, and Z axes. |
| **Rotation** | Move the selected component around the X, Y, and Z axes. |

### Selection

**Selection** determines which element types (edge, face, or vertice) are selectable. You can toggle multiple options at the same time.

If you cannot select elements as expected, confirm you set your PolyGroups correctly. For more information, see [Understanding PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine).

### Show Wireframe

When you enable **Show Wireframe**, a 2D lining overlays on the mesh, depicting underlying triangles.

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#tools,undohistory,andacceptingchanges) panel.