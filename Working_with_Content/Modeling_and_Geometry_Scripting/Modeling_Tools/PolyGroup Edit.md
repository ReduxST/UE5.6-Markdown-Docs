# PolyGroup Edit

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/polygroup-edit-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/polygroup-edit-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:51

---

The **PolyGroup Edit** tool includes a suite of operations for editing a mesh with PolyGroups. Common operations such as **Extrude**, **Bevel**, **Weld**, and **Bridge** are available. Also included are operations that only work with structured PolyGroups, such as **Insert Edge Loop** and edge loop selection.

Combining all these tools with PolyGroup-specific operations like **Merge** (groups) or **Simplify By Groups** creates a low polygon workflow commonly associated with Digital Content Creation (DCC) software such as 3ds Max, Blender, and Maya.

PolyGroup Edit is not available for meshes with no PolyGroup information.

## Understanding PolyGroups

PolyGroups are a set of grouped triangles. You can use the groups for:

-   Modeling and deformation
-   Traditional box modeling
-   UV layout
-   Material organization

PolyGroups are automatically generated on [predefined shapes](/documentation/en-us/unreal-engine/predefined-shapes-in-unreal-engine) in the **Create** category. You can also create them using the **Paint PolyGroups**, **Generate PolyGroups**, and **Tri Select** tools.

Before you start using PolyGroup Edit, we recommend reviewing the [Understanding PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine) documentation to learn more about PolyGroups and how to create them.

## Accessing the Tool

You can access the PolyGroup Edit tool from the following:

-   The **Model** category in **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
-   The **Editing Tools** tab in the **Skeleton Editor**. To learn more, see [Skeleton Editing](/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).

## Using PolyGroup Edit

PolyGroup Edit's editing operations are grouped into three categories:

-   **Face Edits:** Operations for editing the PolyGroup faces of a mesh.
-   **Shape Edits:** Operations for editing the mesh as a whole.
-   **Edge Edits:** Operations for editing the PolyGroup edge of a mesh.

Many operations have a panel of settings that open upon selection. These panels have an accept and cancel option separate from PolyGroup Edit's [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#toolsundohistoryandacceptingchanges) panel.

### Element Selection

You can control which element of your mesh you want to select by using the **Selection Filter**.

| **Element Icon** | **Description** |
| --- | --- |
| ![Select vertices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c36d75a8-73d1-43db-b0f0-f781d75578ff/select-vertices.png) | Selects vertices of a PolyGroup. |
| ![Select edges](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/654229c5-132d-4d9b-ad43-2ea2f8546a41/select-edges.png) | Selects edges of a PolyGroup. |
| ![Select faces.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7a07248-f0b9-4243-a8d2-cb88048c3fe1/select-faces.png) | Selects PolyGroup faces. |
| ![Select edge loops.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/211dc1a6-bcf5-440d-9c93-19df4fdff926/select-edge-loops.png) | Selects PolyGroup edge loops. Edge loops are paths through vertices with four attached edges. |
| ![Select a ring of edges](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/235d2e6d-ea5b-497b-aaf3-053e848895c5/select-ring-edges.png) | Selects ring of PolyGroup edges. Rings are sequences of edges that lie across from each other over a face with four PolyGroup edges. |

If you cannot select elements as expected, confirm you set your PolyGroups correctly or try regenerating extra corners in the [Topolgy Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#topologyoptions) section of the reference guide.

Marquee selection is available for quickly selecting the enabled element. All elements in the selection area are toggled by default, including ones you can't see. To ensure you are not selecting elements you can't see, uncheck **Marquee Ignore Occlusion**.

You can also use the following hotkeys to adjust your selection:

-   **Shift + Click** to add to the current selection.
-   **Ctrl + Click** to remove from the current selection.

While using **PolyGroup Edit**, you can interactively set UVs using **Planar Projection**. To scale the UV island, drag the cursor in and out. To learn more about creating and editing UVs, see [UV Category](/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine).

To continue learning about the PolyGroup Edit properties, see the [PolyGroup Edit Reference](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine) documentation and [PolyGroup Edit video series](https://youtu.be/JgPU9A4nJWY?feature=shared).