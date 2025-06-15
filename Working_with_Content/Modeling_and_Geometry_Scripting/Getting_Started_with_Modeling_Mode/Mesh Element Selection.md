# Mesh Element Selection

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-element-selection-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-element-selection-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:50

---

**Modeling Mode** provides the option for direct mesh element (topology) selection in Unreal Engine for a more consistent and optimized modeling workflow. Artists can use the **Mesh Element Selection** toolbar to select a mesh or mesh element and then invoke an operation without using an intermediate tool such as **PolyGroup Edit** or **Triangle Edit**.

Mesh elements consist of the following:

-   Triangle
    
-   Triangle vertex
    
-   Triangle edge
    
-   PolyGroup
    
-   PolyGroup edge
    
-   PolyGroup vertex
    

These elements represent the granular geometry that makes up your mesh. This workflow of selecting and editing elements can help you create a clean mesh topology.

PolyGroups are a set of grouped triangles that help your modeling workflow. For example, you can construct quad-like groups for box modeling. To learn more about PolyGroups and how they differ from triangles, see [Understanding PolyGroups](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine).

## Accessing the Toolbar

The Mesh Element Selection toolbar is disabled by default in Modeling Mode. For more information about Modeling Mode and how to access it, see [Modeling Mode Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

To enable the toolbar, follow these steps:

1.  In **Modeling Mode Quick Settings**, click the **gear** icon
    
2.  Click **Mesh Element Selection**.
    
3.  Exit and re-enter Modeling Mode.
    

The toolbar should appear in the **Viewport**. Additionally, when you re-enter Modeling Mode, the **Select** category becomes available with tools for editing your element selections.

## Using Mesh Element Selection

You can transform element selections with the modeling gizmo and use the **Select** category tools for additional edits. When you open an available tool, your selected elements are carried over.

The element selection is not editable when you open a tool. To update the selected elements, you must exit the tool, adjust the selection, and then re-enter the tool.

Selection commands, such as **Select All** and **Invert Selection**, help you quickly select your desired elements. You can adjust the method for highlighting elements by toggling **Drag Mode**. The Drag Mode options are clicking individual elements or dragging to select multiple elements with your mouse. To learn more about these properties, see the **Toolbar Properties** section on this page.

The mesh element section is locked by default for imported static meshes. This setting ensures you don't accidentally edit the mesh's geometry. To enable element selection, you can toggle the **lock** icon in the toolbar.

### Gizmo and Numerical Control

You can transform each element selection with the modeling gizmo or use the **Transformation** panel for numerical input. To adjust the gizmo's orientation from local space to normal selection, use the additional settings section of the toolbar (see table below).

To learn more about the modeling gizmo and Transformation panel, see the [Gizmo](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine) section of the Modeling Mode overview.

### Toolbar Properties

| Icon | Description |
| --- | --- |
| 
[![Element Selection](https://dev.epicgames.com/community/api/documentation/image/e92dc330-fbd9-4a45-8950-ae941d9a48f2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e92dc330-fbd9-4a45-8950-ae941d9a48f2?resizing_type=fit)



 | 

Disables element selection. Returns to mesh selection.

 |
| 

[![Triangles](https://dev.epicgames.com/community/api/documentation/image/4db0e7b9-1379-45e4-9496-652ad3f8d106?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4db0e7b9-1379-45e4-9496-652ad3f8d106?resizing_type=fit)



 | 

Selects triangles (faces).

 |
| 

[![Triangle Edges](https://dev.epicgames.com/community/api/documentation/image/c6699d47-3927-4e74-a498-e3c6365ab99b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c6699d47-3927-4e74-a498-e3c6365ab99b?resizing_type=fit)



 | 

Selects triangle edges.

 |
| 

[![Triangle Vertices](https://dev.epicgames.com/community/api/documentation/image/7527abf9-c0e3-4822-b75d-7c8168dc4dbf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7527abf9-c0e3-4822-b75d-7c8168dc4dbf?resizing_type=fit)



 | 

Selects triangle vertices.

 |
| 

[![PolyGroup](https://dev.epicgames.com/community/api/documentation/image/3d6a21b7-04a8-4bd0-bef2-53aa8819c882?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3d6a21b7-04a8-4bd0-bef2-53aa8819c882?resizing_type=fit)



 | 

Selects PolyGroups (faces).

 |
| 

[![PolyGroup Edges](https://dev.epicgames.com/community/api/documentation/image/63dfedb9-f665-4f41-9de2-b2b2db3940cf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/63dfedb9-f665-4f41-9de2-b2b2db3940cf?resizing_type=fit)



 | 

Selects PolyGroup edges, also known as borders.

 |
| 

[![PolyGroup Vertices](https://dev.epicgames.com/community/api/documentation/image/e45e1f78-2df5-4cd1-bb4b-6f9bc9675e38?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e45e1f78-2df5-4cd1-bb4b-6f9bc9675e38?resizing_type=fit)



 | 

Selects PolyGroup vertices, also known as corners.

 |
| 

[![Additional Selection](https://dev.epicgames.com/community/api/documentation/image/df6a5b31-48f2-449b-81ae-3bb16e0b2d38?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/df6a5b31-48f2-449b-81ae-3bb16e0b2d38?resizing_type=fit)



 | 

Additional selection functionality.

-   Select All
    
-   Expand to Connected
    
-   Invert Selection
    
-   Invert Connected
    
-   Expand Selection
    
-   Contract Selection
    

 |
| 

[![Additional Settings](https://dev.epicgames.com/community/api/documentation/image/2137e374-f156-4fdc-87d0-ad977533f16e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2137e374-f156-4fdc-87d0-ad977533f16e?resizing_type=fit)



 | 

Additional settings.

-   **Drag Mode:** Method for mouse selection.
    
    -   **None:** Click individual elements.
        
    -   **Path:** Click an element, and then drag to highlight more.
        
-   **Selectable Mesh Types:**
    
    -   Volumes
        
    -   Static Mesh
        
-   **Local Frame Mode:** Adjusts the gizmo's orientation.
    
    -   **From Geometry** (selection normal)
        
    -   **From Object** (local space)
        

 |
| 

[![Lock](https://dev.epicgames.com/community/api/documentation/image/44a17c7b-b989-429c-81b4-642f6fb2b10b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/44a17c7b-b989-429c-81b4-642f6fb2b10b?resizing_type=fit)



 | 

Locks and unlocks the selected mesh from element selection. Available when you choose an element type.

 |

PolyGroup elements are based on the grouping of triangles. To obtain a specific selection, try adjusting your PolyGroups. To learn more, see [Understanding PolyGroups](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine).

### HotKeys

| Command | Description |
| --- | --- |
| 
**Shift + Click (Mesh)**

 | 

Adds elements to selection. Use **Ctrl + Drag** when **Path Drag Mode** is enabled.

 |
| 

**Ctrl + Click (Mesh)**

 | 

Removes elements from selection. Use **Ctrl + Drag** when **Path Drag Mode** is enabled.

 |
| 

**Ctrl + Z**

 | 

Undo action.

 |
| 

**Middle Mouse + Translate (Gizmo)**

 | 

Repositions the gizmo temporarily.

 |
| 

**Shift + Ctrl + Click (Gizmo)**

 | 

Repositions the gizmo grid to the hit normal.

 |

## Select Category Tools

Many of the tools in the **Select** category open a panel with additional operations. However, the **Clean** and **Delete** options are one-click operations.

-   **Delete:** Removes the selection.
    
-   **Clean:** Retriangulates the selection. Works on PolyGroup selections only.
    

You can find more information on the remaining tools in the table below.

Some tools are only available for specific elements or located in another category.

| Tool | Description |
| --- | --- |
| 
**Extrude**

 | 

Protrudes geometry from the set of selected faces by moving and stitching them.

 |
| 

**Extrude Edge**

 | 

Protrudes geometry from the set of selected edges by moving and stitching them.

 |
| 

**Offset**

 | 

Protrudes selected faces similar to the Extrude operation, but defaults to moving faces along vertex normals instead of a single direction. Mouse movement controls the offset distance. Click in the viewport to complete the offset.

 |
| 

**Push Pull**

 | 

Faces can cut away the mesh or bridge mesh parts. To learn more, see [Push Pull](https://dev.epicgames.com/documentation/en-us/unreal-engine/push-pull-tool-in-unreal-engine).

 |
| 

**Inset**

 | 

Insets the current set of selected faces. Mouse movement controls the inset distance. Click in the viewport to complete the inset.

 |
| 

**Outset**

 | 

Expands the set of selected faces out. Mouse movement controls the outset distance. Click in the viewport to confirm the outset distance.

 |
| 

**Cut**

 | 

Divides the selected PolyGroup faces at the drawn line, as if cutting them with a plane through that line. Click the face to draw the cutting line. New PolyGroups are formed at the border of the cut.

 |
| 

**Bevel**

 | 

Slants the edge loops around the selected faces.

 |
| 

**Insert Loop**

 | 

Adds a chain of edges across quads in a mesh. You can not insert edges on non-quad faces.

 |
| 

**Weld**

 | 

Merges the selected element to its matching disconnected element within a distance tolerance. The tool is available in the **Mesh** category.

 |
| 

**Split**

 | 

Disconnects the elements you select from the non-selected elements to create a second mesh. The tool is available in the **XForm** category.

 |
| 

**Smooth**

 | 

Softens the edges of surfaces by moving vertices towards the averaged location of their neighbors. Available in the **Deform** category. To learn more, see [Smooth](https://dev.epicgames.com/documentation/en-us/unreal-engine/smooth-tool-in-unreal-engine).

 |
| 

**Lattice**

 | 

Edits a mesh's vertices through a 3D grid of points. The tool is available in the **Deform** category. To learn more, see [Lattice](https://dev.epicgames.com/documentation/en-us/unreal-engine/lattice-tool-in-unreal-engine).

 |
| 

**Displace**

 | 

Adds tessellation and distortion to a mesh. The tool is available in the **Deform** category and when using the **Flat** subdivsion type. To learn more, see [Displace](https://dev.epicgames.com/documentation/en-us/unreal-engine/displace-tool-in-unreal-engine).

 |