# Modeling Mode Tools

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-tools-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-tools-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:36:37

---

## Modeling Mode Tools

### Modeling Tools

| **Setting** | **Description** |
| --- | --- |
| **Rendering** |   |
| **Enable Ray Tracing While Editing** | 
Enable real-time ray tracing support for Mesh Editing Tools.

This will impact performance of tools with real-time feedback like 3D sculpting.



 |
| **New Mesh Objects** |   |
| **Enable Ray Tracing** | Enable ray tracing support for new mesh objects created by Modeling Tools, if support is optional (for example, `DynamicMeshActors`). |
| **Enable Collision** | Enable collision support for new mesh objects created by Modeling Tools. |
| **Collision Mode** | 

Default collision mode set on new mesh objects created by Modeling Tools.

You can choose from the following options:

-   **Project Default:** Use project physics settings (`DefaultShapeComplexity`).
-   **Simple and Complex:** Create both simple and complex shapes. Simple shapes are used for regular scene queries and collision tests. Complex shapes (per poly) are used for complex scene queries.
-   **Use Simple Collision as Complex:** Create only simple shapes. Use simple shapes for all scene queries and collision tests.
-   **Use Complex Collision as Simple:** Create only complex shapes (per poly). Use complex shapes for all scene queries and collision tests. Can be used in simulation for static shapes only (that is, can be collided against but not moved through forces of velocity).



 |