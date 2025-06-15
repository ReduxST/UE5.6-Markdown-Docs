# Offset

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/offset-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/offset-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:39:27

---

The **Offset** tool adjusts the position of a mesh's vertices by a specified amount along its normal, such as creating additional details, like a cobblestone pattern, in highly tessellated geometry.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/483fea38-ef3d-435c-b644-1e22c9f9952d/flat-rec.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a62d547-1fcb-4898-8867-0f3cbe06304b/jagged-cobble.png) |
| Flat Rectangle | Cobblestone |

The tool is additionally helpful for:

-   Adding thickness to a mesh, such as a wall.
-   Growing or shrinking a solid object.
-   Creating custom [Volume Actors](/documentation/en-us/unreal-engine/volume-actors-in-unreal-engine) and [Cutting Actors for fracturing](https://dev.epicgames.com/community/learning/tutorials/k84m/unreal-engine-chaos-destruction-fracture-and-clustering#:~:text=Play%20Video-,MESH%20CUT,-The%20Mesh%20fracture).

## Accessing the Tool

You can access the Offset tool from the following:

-   The **Deform** category in **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
-   The **Editing Tools** tab in the **Skeleton Editor**. To learn more, see [Skeleton Editing](/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).

## Using Offset

Offset has the following operation types:

-   **Iterative**: Offsets with N iterations.
-   **Implicit**: Offsets in a way that produces smoother output and does a better job at preserving UVs but can be slow on large meshes.

When you offset a mesh, you can toggle **Create Shell** to add a thickened shell instead of only moving the input vertices.

To help visualize the effect of the brush on your mesh, you can toggle **Show Wireframe** and **Flat Shading** and change the material mode in the **Rending** section.

![Weight Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5075d603-1ca3-44e4-8d9a-c5d66741bc5c/map-paint-tool.png)

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#toolsundohistoryandacceptingchanges) panel.

| **Key Command** | **Operation** |
| --- | --- |
| **F** | Zooms into the location of the mesh. |
| **ESC** | Cancels the changes and exits the tool. |
| **Enter** | Accepts the tool changes. |