# PolyGroup Edit Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:53

---

This document is a reference guide for the properties of the PolyGroup Edit tool, which provides a suite of operations for editing a mesh with PolyGroups. For an overview of the tool and how to access it, see [PolyGroup Edit](/documentation/en-us/unreal-engine/polygroup-edit-tool-in-unreal-engine).

Before you start using the PolyGroup Edit tool, we recommend reviewing the [Understanding PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine) documentation to learn more about PolyGroups and how to create them.

The PolyGroup Edit tool consists of the following key sections:

-   [Face Edits](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#faceedits): Operations for editing the PolyGroup faces of a mesh.
-   [Shape Edits](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#shapeedits): Operations for editing the mesh as a whole.
-   [Edge Edits](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#edgeedits): Operations for editing the PolyGroup edge of a mesh.
-   [UVs](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#uvs): Operations for creating UVs.
-   [Selection](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#selectionactions): Operations for highlighting mesh elements (PolyGroup vertices, edges, and faces). You must select an element to use many of the operations in the editing sections.

Associated [hotkeys](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#hotkeys) are listed at the end of this document.

If you click **Accept** or **Cancel** in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#toolsundohistoryandacceptingchanges) panel, the PolyGroup Edit tool closes.

## Face Edits

The **Face Edits** section includes operations for editing the PolyGroup faces of a mesh. A single triangle can be a PolyGroup face. Before using the operations, you must first select a face. For more information, see the [Selection Filter](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#selectionfilter) section.

### Extrude

The **Extrude** operation protrudes geometry in a positive or negative direction from the set of selected faces and connects them to the mesh with new faces around the selection boundary. New faces inherit the PolyGroup divisions of the adjacent faces. If the selection lies on a mesh boundary (no adjacent faces exist), you can adjust the PolyGroup division of the new faces using the **Use Colinearity for Setting Border Groups** setting in the table below.

Click image to expand.

When you click the Extrude operation, the Tool Properties panel displays the operation's properties. The Extrude operation is also available as a standalone tool in the **Select** category when selecting faces. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | **Description** |
| --- | --- |
| **Apply** | Bakes extrusion changes into the mesh. |
| **Cancel (Esc)** | Negates changes. |

| **Extrude** | **Description** |
| --- | --- |
| **Distance Mode** | 
Determines how the extrusion distance is set. You can use the following methods:

-   **Click in Viewport:** Mouse movement controls extrusion height and depth. Click in the viewport to complete the extrusion and exit the operation. Using the cursor, you can align the extrusion distance to objects in the level. An additional line from the center of the selection indicates the direction of measurement for the extrusion.
-   **Fixed:** Set extrusion height or depth from a numerical input (**Distance**).



 |
| **Shells to Solids** | 

Controls whether extruding an entire open-border patch should create a solid or open shell.

-   True (enable): Open-border faces are extruded as a solid shell (no holes in the mesh).
-   False (disable): Open-border faces are extruded with an open shell.



 |
| **Direction Mode** | 

Determines the direction vertices move during extrusion. You can use the following methods:

-   **Single Direction:** Extrude all triangles in the same direction regardless of their normals.
-   **Selected Triangle Normals:** Take the angle-weighted average of the selected triangles around each extruded vertex to determine vertex movement direction.
-   **Selected Triangle Normals Even:** Similar to Selected Triangle Normals, but also adjust the distance moved in an attempt to keep triangles parallel to their original facing.
    -   **Max Distance Scale Factor:** Controls the maximum distance vertices can move from the target distance in order to stay parallel with their source triangles.

[See below for examples.](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#extrudedirectionmodeexamples)



 |
| **Direction** | 

The direction of extrusion when Single Direction in the Direction Mode section is active. You can choose from the following:

-   **Selection Normal**
-   **World X**
-   **World Y**
-   **World Z**
-   **Local X**
-   **Local Y**
-   **Local Z**



 |

| **Advanced** | **Description** |
| --- | --- |
| **Measure Direction** | 
The direction to measure the distance of extrusion when Selected Triangle Normals or Selected Triangle Normals Even and Click In Viewport is active. The extrusion height is set based on the mouse location on the respective axis. You can choose from the following:

-   **Selection Normal**
-   **World X**
-   **World Y**
-   **World Z**
-   **Local X**
-   **Local Y**
-   **Local Z**



 |
| **Use Colinearity for Setting Border Groups** | 

Considers edge colinearity for determining how side triangles connecting the extruded face are grouped when extruded faces touch the mesh border.

-   If true, side triangles touching the mesh border are grouped per colinear section of boundary.
-   If false, all side triangles touching the mesh border are grouped as one.

For example, when true, extruding a flat rectangle gives four different PolyGroups on its side rather than one connected PolyGroup.



 |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

#### Extrude Direction Mode Examples

|   |   |   |   |
| --- | --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4865dbb-d09f-460f-9a59-893d41b30fed/no-extrusion.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1588db9d-f111-41ba-82ba-9678580ea812/single-direction.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11014a60-7013-4202-99b0-ae56262e10a6/extrude-triangle-normal.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40af291d-46cf-44cd-9182-dab4eabd7bd8/extrude-triangle-normal-even.png) |
| No Extrusion | Single Direction | Selected Triangle Normals | Selected Triangle Normals Even |

### Offset

The **Offset** operation protrudes selected faces similar to the Extrude operation, but defaults to moving faces along vertex normals instead of a single direction.

Click image to expand.

When you click the Offset operation, the Tool Properties panel displays the operation's properties. The Offset operation is also available as a standalone tool in the **Select** category when selecting faces. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | **Description** |
| --- | --- |
| **Apply** | Bakes extrusion changes into the mesh. |
| **Cancel (Esc)** | Negates changes. |

| **Extrude** | **Description** |
| --- | --- |
| **Distance Mode** | 
Determines how the extrusion distance is set. You can use the following methods:

-   **Click in Viewport:** Mouse movement controls extrusion height and depth. Click in the viewport to complete the extrusion and exit the operation. Using the cursor, you can align the extrusion distance to objects in the level. An additional line from the center of the selection indicates the direction of measurement for the extrusion.
-   **Fixed:** Set extrusion height or depth from a numerical input (**Distance**).



 |

| **Offset** | **Description** |
| --- | --- |
| **Shells to Solids** | 
Controls whether extruding an entire open-border patch should create a solid or open shell.

-   True (enable): Open-border faces are extruded as a solid shell (no holes in the mesh).
-   False (disable): Open-border faces are extruded with an open shell.



 |
| **Direction Mode** | 

Determines the direction vertices move during extrusion. You can use the following methods:

-   **Vertex Normals:** Follow the vertex normals regardless of selection.
-   **Selected Triangle Normals:** Take the angle-weighted average of the selected triangles around each extruded vertex to determine vertex movement direction.
-   **Selected Triangle Normals Even:** Similar to Selected Triangle Normals, but also adjust the distance moved in an attempt to keep triangles parallel to their original facing.
    -   **Max Distance Scale Factor:** Controls the maximum distance vertices can move from the target distance in order to stay parallel with their source triangles.

[See below for examples.](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#offsetdirectionmodeexamples)



 |

| **Advanced** | **Description** |
| --- | --- |
| **Measure Direction** | 
The direction to measure the distance of extrusion when Click In Viewport is active. The extrusion height is set based on the mouse location on the respective axis. You can choose from the following directions:

-   **Selection Normal**
-   **World X**
-   **World Y**
-   **World Z**
-   **Local X**
-   **Local Y**
-   **Local Z**



 |
| **Use Colinearity for Setting Border Groups** | 

Considers edge colinearity for determining how side triangles connecting the extruded face are grouped when extruded faces touch the mesh border.

-   If true, side triangles touching the mesh border are grouped per colinear section of boundary.
-   If false, all side triangles touching the mesh border are grouped as one.

For example, when true, extruding a flat rectangle gives four different PolyGroups on its side rather than one connected PolyGroup.



 |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

#### Offset Direction Mode Examples

|   |   |   |   |
| --- | --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b08dce61-eaec-4c7e-b7f1-288efdd75fa7/selection.png) | ![Vertex Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10c744a6-7abc-4a34-9570-0a0e001efc58/vertex-normals.png) | ![Selected Triangle Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/254a7481-6da6-4a09-86da-8687717c3df1/triangle-normals.png) | ![Triangle Normal Even](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e63cc61-83b6-436e-a0ee-7d1bfd1e0f0a/triangle-normal-even.png) |
| No Extrusion | Vertex Normal | Selected Triangle Normals | Selected Triangle Normals Even |

### Push Pull

The **Push Pull** operation extrudes faces that cut or merge mesh parts. You can think of this as performing a boolean operation (like those done by the [Boolean tool](/documentation/en-us/unreal-engine/boolean-tool-in-unreal-engine) between the original mesh and an extruded selection.

Left is the face selection; middle is the Push Pull operation; right is the Extrude operation.

When you click the Push Pull operation, the Tool Properties panel displays the operation's properties. The Push Pull operation is also available as a standalone tool in the **Select** category when selecting faces. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | **Description** |
| --- | --- |
| **Apply** | Bakes extrusion changes into the mesh. |
| **Cancel (Esc)** | Negates changes. |

| **Extrude** | **Description** |
| --- | --- |
| **Distance Mode** | 
Determines how the extrusion distance is set. You can use the following methods:

-   **Click in Viewport:** Mouse movement controls extrusion height and depth. Click in the viewport to complete the extrusion and exit the operation. Using the cursor, you can align the extrusion distance to objects in the level. An additional line from the center of the selection indicates the direction of measurement for the extrusion.
-   **Fixed:** Set extrusion height or depth from a numerical input (**Distance**).



 |

| **Extrusion Options** | **Description** |
| --- | --- |
| **Direction Mode** | 
Determines the direction vertices move during extrusion before the boolean operation. You can use the following methods:

-   **Vertex Normals:** Follow the vertex normals regardless of selection.
-   **Single Direction:** Move all triangles in the same direction regardless of their normals.
-   **Selected Triangle Normals:** Take the angle-weighted average of the selected triangles around each extruded vertex to determine vertex movement direction.
-   **Selected Triangle Normals Even:** Similar to Selected Triangle Normals, but also adjust the distance moved in an attempt to keep triangles parallel to their original facing.
    -   **Max Distance Scale Factor:** Controls the maximum distance vertices can move from the target distance in order to stay parallel with their source triangles.

[See below for examples.](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#pushpulldirectionmodeexamples)



 |
| **Shells to Solids** | 

Controls whether extruding an entire open-border patch should create a solid or open shell.

-   True (enable): Open-border faces are extruded as a solid shell (no holes in the mesh).
-   False (disable): Open-border faces are extruded with an open shell.



 |

| **Advanced** | **Description** |
| --- | --- |
| **Measure Direction** | 
The Measure Direction setting is the direction to measure the distance of extrusion when Selected Triangle Normals, Vertex Normals, or Selected Triangle Normals Even is active. The extrusion height is set based on the mouse location on the respective axis. When Single Direction is active, the direction of the extrusion is based on Measure Direction. The setting is only available when Distance Mode is set to Click in Viewport. You can choose from the following directions:

-   **Selection Normal**
-   **World X**
-   **World Y**
-   **World Z**
-   **Local X**
-   **Local Y**
-   **Local Z**



 |
| **Use Colinearity for Setting Border Groups** | 

Considers edge colinearity for determining how side triangles connecting the extruded face are grouped when extruded faces touch the mesh border.

-   If true, side triangles touching the mesh border are grouped per colinear section of boundary.
-   If false, all side triangles touching the mesh border are grouped as one.

For example, when true, extruding a flat rectangle gives four different PolyGroups on its side rather than one connected PolyGroup.



 |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

#### Push Pull Direction Mode Examples

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd0b88d9-7b85-4ffd-a944-4130a3b770b6/selection.png) | ![Vertex Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d573b3ef-42a5-4c61-a5cc-82d6154589db/vertex-normals.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/511d9716-0ae3-4a0a-a1b0-692ea0dff6b1/push-pull-single-direction.png) | ![Selected Triangle Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33a39fb7-0385-46d1-b210-1844d1ec4f0f/triangle-normals.png) | ![Triangle Normal Even](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a53453a-15c9-41f7-9301-d0e60a48044b/triangle-normal-even.png) |
| No Extrusion | Vertex Normal | Single Direction | Selected Triangle Normals | Selected Triangle Normals Even |

### Inset

The **Inset** operation contracts a set of selected faces to create new faces. Mouse movement controls the inset distance. Click in the viewport to complete the inset.

When you click the Inset operation, the Tool Properties panel displays the operation's properties.The Inset operation is also available as a standalone tool in the **Select** category. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | **Description** |
| --- | --- |
| **Done** | Click to exit the operation if you decide no changes are needed. You can also use **Ctrl** \+ **Z** to cancel the operation. |

| **Inset/Outset** | **Description** |
| --- | --- |
| **Softness** | Amount of smoothing applied to the inset boundary. When low, faces may begin to overlap at bends in the selection boundary. |
| **Reproject** | Determines whether vertices in the inset region should be projected back onto the input surface. |
| **Boundary Only** | Controls whether the operation moves interior vertices as well, or only the boundary vertices. |
| **Area Scale** | Adjusts area scaling when solving for interior vertices. |

These settings are most noticeable on high-resolution and curved surfaces.

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

### Outset

The **Outset** operation expands the set of selected faces out to create new faces. Mouse movement controls the outset distance. Click in the viewport to confirm the outset distance.

When you click the Outset operation, the Tool Properties panel displays the operation's properties. The Outset operation is also available as a standalone tool in the **Select** category. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | Description |
| --- | --- |
| **Done** | Click to exit the operation if you decide no changes are needed. You can also use **Ctrl** \+ **Z** to cancel the operation. |

| **Inset/Outset** | Description |
| --- | --- |
| **Softness** | Amount of smoothing applied to the inset boundary. When low, faces may begin to overlap at bends in the selection boundary. |
| **Boundary Only** | Controls whether outset operation moves interior vertices as well as border vertices. |
| **Area Scale** | Adjusts area scaling when solving for interior vertices. |

These settings are most noticeable on high-resolution and curved surfaces.

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

### Bevel

The **Bevel** operation slants the edge loops around the selected faces, creating edge-aligned faces.

When you click the Bevel operation, the Tool Properties panel displays the operation's properties. The Bevel operation is also available as a standalone tool in the **Select** category. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | Description |
| --- | --- |
| **Apply** | Bakes changes into the mesh. |
| **Cancel (Esc)** | Negates changes. |

| **Bevel** | Description |
| --- | --- |
| **Bevel Distance** | 
Adjusts the length of the bevel.

Setting the length too high can cause faces to overlap.



 |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

### Delete

The **Delete** operation removes selected faces. You can also use the hotkeys **Backspace** and **Delete**.

### Merge

The **Merge** operation combines the set of selected faces into one, creating a new PolyGroup.

### Cut Faces

The **Cut Faces** operation divides the selected faces at the drawn line, as if cutting them with a plane through that line. New PolyGroups are formed at the border of the cut.

To draw a line, follow these steps:

1.  Click any point on the selected faces or snap to a vertex.
2.  Move your cursor to set the line direction and distance.
3.  Click to set the cut line.

The cut occurs only on selected faces, including occluded faces, where the drawn line intersects.

When you click the Cut Faces operation, the Tool Properties panel displays the operation's properties. The Cut Faces operation is also available as a standalone tool in the **Select** category. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | **Description** |
| --- | --- |
| **Done** | Click to exit the operation if you decide no changes are needed. You can also use **Ctrl** \+ **Z** to cancel the operation. |

| **Cut** | **Description** |
| --- | --- |
| **Orientation** | 
Determines how the cutting plane is oriented when splitting the faces. The difference is easier to see when cutting a curved face. You can choose from the following:

-   **Face Normals:** The cutting plane is oriented using the normals at the endpoints of the drawn line.
-   **View Direction:** The cutting plane is oriented to align with the view direction.



 |
| **Snap Vertices** | Determines if the cursor should snap to vertices. |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

### Recalc Normals

The **Recalc Normals** operation recalculates normals for the current set of selected faces.

![Normals After Editing a Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a844158-f294-4d21-8d5c-b034e1f3a666/original-normals.png)

![Normals Recalucated](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc3ba724-6921-4d6c-9828-3a9a3ab01201/recalculated-normals.png)

### Flip

The **Flip** operation inverts normals and face orientation for the current set of selected faces.

Click image to expand.

### Retriangulate

The **Retriangulate** operation removes all interior vertices in the selection and attempts to retriangulate it using only its boundary.

![Interior Vertices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19598bea-c16a-4bbe-972e-25abf70d6267/interior-vertices.png)

![Minimized Triangulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dba761c-709e-4bc8-bb1e-6e7191939a6d/retriangulate.png)

### Decompose

The **Decompose** operation splits each of the selected faces into a separate PolyGroup per triangle.

### Disconnect

The **Disconnect** operation separates the selected faces at their borders, disconnecting them from the mesh.

Click image to expand.

### Duplicate

The **Duplicate** operation copies the selected faces at their border. Duplicated faces are disconnected from the mesh.

Click image to expand.

## Shape Edits

The **Shape Edits** section contains operations for editing the mesh as a whole.

### Insert Edge Loop

Use the **Insert Edge Loop** operation to insert a chain of edges across quad-like PolyGroups in a mesh. You can only add edges to quad-like faces, which have exactly four corners. You can set multiple insertions while the operation is active.

When you click the Insert Edge Loop operation, the Tool Properties panel displays the operation's properties. The Insert Edge Loop operation is also available as a standalone tool in the **Select** category. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).

| **Current Operation** | Description |
| --- | --- |
| **Done** | Click to exit the operation if you decide no changes are needed. You can also use **Ctrl** \+ **Z** to cancel the operation. |

| **Insert Edge Loop** | Description |
| --- | --- |
| **Position Mode** | 
Determines how edge loops position themselves vertically relative to loop direction. You can choose from the following methods:

-   **Even:** Inserts edges by evenly dividing the start and destination edges of each face. For example, when inserting a single loop at a time, the new edges cross existing edges exactly at their halfway point. When Even is active, **Number of Loops** is available.
    -   **Number of Loops:** Determines how many loops to insert at a time.
-   **Proportion Offset:** Edge loops fall at the same length proportion at each edge they intersect.
-   **Distance Offset:** Edge loops fall at a constant distance from the start of each edge they intersect. This clamps to the end if the edge is too short. When Distance Offset is active, Flip Offset Direction is available.
    -   **Flip Offset Direction:** Measure the distance offset from the opposite side of the edges.



 |
| **Insertion Mode** | 

Determines how edge loops are added to the mesh. You can choose from the following methods:

-   **Retriangulate:** Deletes existing groups, and new triangles are created for the new groups. This process keeps topology simple but breaks non-planer groups.
-   **Plane Cut:** Keeps existing triangles and cuts them to create a new path. This process preserves the shape of non-planar groups, but may result in fragmented triangles over time.



 |
| **Highlight Problem Groups** | When true, non-quad-like PolyGroups that stop the loop are highlighted with X’s marking the corners. |

| **Advanced** | Description |
| --- | --- |
| **Interactive** | Decides if the offset amount of the edge is set by the cursor or numerical value. When false, the offset is numerically specified by Distance or Proportion Offset, and mouse clicks only choose the edge. Not available for the Even position mode. |
| **Distance Offset** | Numerically sets the offset amount.Only available when Interactive is false and Position Mode is set to Distance Offset. |
| **Proportion Offset** | Numerically sets the offset amount. Only available when Interactive is false, and Position Mode is set to Proportion Offset. |
| **Vertex Tolerance** | Determines how close a new loop edge needs to pass next to an existing vertex when crossing an edge to use that vertex rather than creating a new one. |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

### Insert Edge

Use **Insert Edge** to add an edge to existing edges or vertices across a single face. You can set multiple insertions while the operation is active.

To insert an edge, follow these steps:

1.  Click along an edge of the mesh or snap to a vertex.
2.  Move your cursor to set the edge direction and distance.
3.  Click a neighboring edge or snap to a vertex to add the new edge.

Insert Edge cannot add an edge in cases where doing so would not be enough to divide the given face into separate parts.

For example, it is unable to connect the inner and outer edges of an O-shaped face because the triangles of the face would stay connected in a C-shape, meaning there is no PolyGroup boundary at the new edge. Inserting edges in such situations requires using the Cut Faces tool (which cuts through the entire face, not just between the endpoints) or breaking up the face into new PolyGroups.

When you click the Insert Edge operation, the Tool Properties panel displays the operation's properties.

| **Current Operation** | **Description** |
| --- | --- |
| **Done** | Click to exit the operation if you decide no changes are needed. You can also use **Ctrl** \+ **Z** to cancel the operation. |

| **Insert Edge** | **Description** |
| --- | --- |
| **Insertion Mode** | 
Determines how edge loops are added to the mesh. You can choose from the following methods:

-   **Retriangulate:** Deletes existing groups, and new triangles are created for the new groups. This process keeps topology simple but breaks non-planer groups.
-   **Plane Cut:** Keeps existing triangles and cuts them to create a new path. This process preserves the shape of non-planar groups, but may result in fragmented triangles over time.



 |
| **Continuous Insertion** | When true, edge insertions are chained together so that each endpoint becomes the new start point. |

| **Advanced** | **Description** |
| --- | --- |
| **Vertex Tolerance** | Determines how close a new edge needs to pass next to an existing vertex when crossing an edge to use that vertex rather than creating a new one. Particularly relevant when using Plane Cut mode when there are interior vertices present. |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

### Simplify by Groups

**Simplify by Groups** simplifies every PolyGroup by removing vertices on shared straight edges, removing all interior vertices, and retriangulating.

This process is helpful in cleaning up mesh topology when PolyGroups are simple and there are unneeded interior or colinear vertices. However, avoid using the operation for PolyGroup topologies that involve non-planar faces, as it loses their shape and destroys any faces that could not be retriangulated (a warning is shown in this case after completion). For instance this currently fails to retriangulate the side of a cylinder when it is a single PolyGroup.

![Interior Vertices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61f5e42c-7c91-42f3-ab8b-378d2b39f87a/simplify-by-groups-2.png)

![Simplified](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1a571eb-7309-443c-9096-aa9f485ba33e/simplify-by-groups.png)

## Edge Edits

The **Edge Edits** section contains operations for editing the PolyGroup edges of a mesh. Before using the operations, you must select an edge. For more information, see the [Selection Filter](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#selectionfilter) section.

### Weld

The Weld operation merges two selected edges, moving the first selected edge to the second.

### Straighten

The **Straighten** operation makes each selected edge follow a straight path between its endpoints.

### Fill Hole

The **Fill Hole** operation fills the adjacent hole for any selected boundary edges.

### Bevel

The **Bevel** operation slants the selected edges, replacing them with angled faces.

![No Bevel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c8be65e-eb66-4608-bcf1-45582ca5320c/no-bevel.png)

![Bevel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/393bafd8-e853-4ccf-ae92-518a6af7c567/bevel.png)

### Bridge

The **Bridge** operation creates a new face that connects the selected edges.

### Simplify

The **Simplify** operation attempts to remove colinear vertices along the edge when doing so does not change the UVs or make low-quality triangles.

## UVs

The **UVs** section contains operations for editing the UVs of a mesh.

### Planar Projection

The **Planar Projection** operation interactively sets UVs on selected faces.

To set UVs, follow these steps:

1.  Click the face.
2.  Drag the cursor in or out.
3.  Click to set the UV.

The drawn line can snap to vertices, helping control orientation. To learn more about creating and editing UVs, see [UV Editor](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine). When you click the Planar Projection operation, the Tool Properties panel displays the operation's properties.

|   | **Current Operation** | **Description** |
| --- | --- | --- |
| **Done** | Click to exit the operation if you decide no changes are needed. You can also use **Ctrl** \+ **Z** to cancel the operation. |   |

| **Planar Project UV** | **Description** |
| --- | --- |
| **Show Material** | Determines the type of material to set, default or checkerboard. When false, the checkerboard material becomes active. |

Properties for [Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#options) and [Gizmo](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#gizmo) are also available.

## Selection Actions

You can manually select elements (PolyGroup vertices, edges, and faces) of a mesh using the **Selection Filter** or perform quick selections using **Selection Actions**.

| **Selection Action** | **Description** |
| --- | --- |
| **Invert Selection** | Selects all of the specified element that you did not select and deselect any elements that were selected. The selected element type depends on the Selection Filter. If multiple element icons are selected, the first active element in the Selection Filter (furthest to the left) is selected. |
| **Select All** | Selects all of the specified element. The selected element type depends on the selection filter. If multiple element icons are selected, the first active element in the Selection Filter (furthest to the left) is selected. |

## Selection Filter

The **Selection Filter** controls which element (PolyGroup vertices, edges, and faces) of your mesh can be selected. All elements can be set to true at once. Click the icons to enable and disable the selection of the element.

![Selection Filter Icons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f46739a-03ce-40b8-adb0-31277a335258/selection-filter.png)

For marquee selection, click and drag in the viewport to select multiple components of an element at once. Use the properties in **Additional Selection Options** for further control. If multiple elements are enabled when marquee selecting, then the first active element (furthest to the left) is selected.

| **Element Icon** | **Description** |
| --- | --- |
| ![Select Verticies PolyGroups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e29b3d8-3c21-4145-8e54-a4f56ae03c23/select-vertices.png) | Select vertices of a PolyGroup. |
| ![Select PolyGroup Edges](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7bd2e5c-2d69-46f4-a929-c88410d42a01/select-edges.png) | Select edges of a PolyGroup. |
| ![Select PolyGroup Faces](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02a62d4d-7f11-4e7f-be9f-5f714edca102/select-faces.png) | Select PolyGroup faces |
| ![Select PolyGroup Edge Loops](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aa04eab-2e46-4801-86c1-6e0f2f77ceff/select-edge-loops.png) | Select PolyGroup edge loops. Edge loops are paths through vertices with four attached edges. |
| ![Select PolyGroup Ring E](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/958f6a97-aba9-4db4-97d9-94a24b46fe0a/select-ring-edges.png) | Select ring of PolyGroup edges. Rings are sequences of edges that lie across from each other over a face that has four PolyGroup edges. |

If you cannot select elements as expected, confirm you set your PolyGroups correctly.

## Additional Selection Options

| **Additional Selection Options** | **Description** |
| --- | --- |
| **Marquee Ignore Occlusion** | When true, the marquee selection includes all valid geometric components. When false, the marquee selection only includes elements that are visible from the current camera. |

| **Ortho Viewport Behavior** | **Description** |
| --- | --- |
| **Prefer Projected Element** | Selects an edge projected to a point rather than the vertex at that point, or a face projected to an edge rather than that edge. |
| **Select Down Ray** | If the closest element is valid, selects other elements behind it that are aligned with it. |
| **Ignore Occlusion** | Does not check whether the closet element is occluded from the current view in a lit version of the scene. |
| **Hit Back Faces** | Selects the back side of a face. It can be helpful to turn this off when working with an "inside-out" mesh, such as a cube representing the inside of a room where the sides face inward, to avoid selecting the closer back faces. |
| **Enable Marquee** | Activates marquee selection. |

## Options

Additional options for visualization.

| **Visualization Option** | Description |
| --- | --- |
| **Show Wireframe** | Creates an outline of your mesh's topology at the triangle level. |
| **Show Selectable Corners** | Toggle visibility of generated corners. For more information, see the **[Topology Options](/documentation/en-us/unreal-engine/polygroup-edit-tool-reference-in-unreal-engine#topologyoptions)** section below. |
| **Gizmo Visible** | Toggle visibility of the transform gizmo. |

## Gizmo

Additional gizmo control when you set the gizmo's coordinate system to local space is active. The settings are deactivated when you enable world transform.

| **Gizmo Opton** | **Description** |
| --- | --- |
| **Local Frame Mode** | Determines if the gizmo's rotation is taken from the selected element (**From Geometry**) or from the transform of the mesh as a whole (**From Object**). |
| **Lock Rotation** | When true, keep the gizmo orientation of the last selection. Toggle with **Q0** hotkey. |

## Topology Options

As you group triangles to create a PolyGroup, a boundary edge will form, encompassing the triangles. Depending on the topology of your mesh and generated PolyGroups, editing the edges of your mesh may not work as you expect compared to other modeling Digital Content Creation (DCC) software.

In the image below, the mesh includes two PolyGroups, represented by the highlighted boundary edge. Although the boundary of the PolyGroups appears to have multiple edges due to its bending shape, it does not consist of any PolyGroup vertices, meaning there is only one PolyGroup edge.

![PolyGroup Boundary Edge](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1c19529-abdf-49e6-b4c9-291e686f0c16/polygroup-boundary-edge.png)

PolyGroup edges and vertices are generated under the following conditions:

-   Two or more connecting PolyGroup faces (or a mesh boundary) create a PolyGroup edge.
-   Three or more connecting PolyGroup edges create a PolyGroup vertex.

To help generate extra edges and vertices along a PolyGroup boundary where there are one or no neighboring faces, the following topology options are available.

| **Topology Options** | **Description** |
| --- | --- |
| **Add Extra Corners** | 
Adds corners at sharp group edge bends to generate PolyGroup vertices. This generation is in addition to the normal corners that are placed at junctions of three or more PolyGroup edges



 |
| **Extra Corner Angle Threshold Degrees** | 

Determines how sharp the angle must be to warrant an extra corner. Lower values require sharper corners, making it more tolerant of curved group edges. The setting is applied either when Regenerate Extra Corners is clicked or after any operation that modifies topology.

If you have unexpected corners (extra vertices and edges) either adjust the angle threshold or disable Add Extra Corners, then click Regenerate Extra Corners.



 |
| **Regenerate Extra Corners** | Regenerates extra corners. Must be clicked after toggling Add Extra Corners or adjusting the angle threshold. |

## Hotkeys

| **Hotkey** | **Description** |
| --- | --- |
| **F** | Zooms into the location of the selection. |
| **Shift + Click/Drag** | Adds elements to the current selection. |
| **Ctrl + Click/Drag** | Removes elements from the current selection. |
| **Ctrl + Shift + Click/Drag** | Toggles the elements in the selection. |
| **Enter** | Accepts tool changes. |
| **ESC** | Cancels the changes and exit the tool. |
| **Middle-Drag Gizmo** | Transforms mesh pivot. Hold Ctrl to enable snapping. |
| **Ctrl + Drag Gizmo** | Snaps transform of selected element. |
| **Q** | Locks the gizmo rotation. |