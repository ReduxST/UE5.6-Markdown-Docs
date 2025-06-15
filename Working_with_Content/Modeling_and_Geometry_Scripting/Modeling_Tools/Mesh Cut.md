# Mesh Cut

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-cut-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-cut-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:43

---

The **Mesh Cut** tool splits one mesh into parts using a second mesh. You can use the tool to break up meshes into smaller components and add detail, reducing the manual process of adding edges and deleting faces when modeling.

## Accessing the Tool

Mesh Cut is located in the **Model** category of **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

## Using Mesh Cut

Gizmos for each mesh appear in the Viewport to dynamically change the cut.

Similar to the [Boolean](/documentation/en-us/unreal-engine/boolean-tool-in-unreal-engine) tool, the selection order matters as follows:

-   The first selected mesh becomes the one you cut.
-   The second selection becomes the cutting boundary.

Mesh Cut is a single-cut tool, meaning you must start a new session for each cut you want to make on the mesh.

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#toolsundohistoryandacceptingchanges) panel.

## Settings

| **Setting** | **Description** |
| --- | --- |
| **Try Fix Holes** | When true, Mesh Cut automatically attempts to fill holes created by numerical errors. |
| **Try Collapse Edges** | When true, any extra edges created by the boolean operation are collapsed. |
| **Winding Threshold** | Determines whether a triangle in one mesh is inside or outside of the other. |
| **Show New Boundaries** | When true, shows boundary edges created by the boolean operation caused by numerical errors. |
| **Use First Mesh Materials** | When True, only the first mesh keeps its material assignments. All other triangles are assigned material 0. |
| **Show Gizmo** | Toggles the transform gizmo's visibility. |