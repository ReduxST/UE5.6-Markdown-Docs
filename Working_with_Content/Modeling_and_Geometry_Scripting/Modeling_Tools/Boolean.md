# Boolean

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/boolean-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/boolean-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:08

---

The **Boolean** tool subtracts or adds mesh pairs. It is helpful for quickly adding detail and displacement effects to your mesh.

## Accessing the Tool

Boolean is located in the **Model** category of **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

## Using Boolean

Two meshes are required to use the tool as the resulting mesh change revolves around the area where both meshes intersect. The order in which you select the meshes matters for the first two operations:

-   Your first selection becomes **A**.
-   Your second selection becomes **B**.

You can choose from four operations shown in the table below.

| **Operation** | **Description** |
| --- | --- |
| **Difference A - B** | Subtracts the second mesh from the first mesh. |
| **Difference B - A** | Subtracts the first mesh from the second mesh. |
| **Intersection** | Subtracts non-overlapping geometry. |
| **Union** | Combines both meshes and resolves self-intersections. |

Once both meshes are selected and the tool is activated, you can interactively manipulate one or both meshes in the Viewport, depending on the operation.

After you edit the mesh, you can decide how to handle the mesh output using the operations shown in the table below.

| **Operation** | **Description** |
| --- | --- |
| **Output Type** | Chooses the type of actor to create. Only available if **New Object** is selected in **Output Object**. |
| **Output Object** | Determines whether to create a new actor or to override one of the input meshes. |
| **On Tool Accept** | Determines what happens to the selected meshes when changes are accepted. |