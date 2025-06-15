# Push Pull

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/push-pull-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/push-pull-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:12

---

The **Push Pull** tool extrudes PolyGroup faces that cut or merge mesh parts. You can think of this as performing a boolean operation (like those done by the [Boolean tool](/documentation/en-us/unreal-engine/boolean-tool-in-unreal-engine)) between the original mesh and an extruded selection.

Left is the face selection; middle is the Push Pull operation; right is the Extrude operation.

Before you start using the Push Pull tool, we recommend reviewing the [Understanding PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine) documentation to learn more about PolyGroups and how to create them.

## Accessing the Tool

You can access the Push Pull tool from the following:

-   As a standalone tool in the **Select** category when selecting PolyGroup faces. To learn more about this category, see [Mesh Element Selection](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#meshelementselection).
-   As an operation in the **PolyGroup Edit** tool. To learn more, see [PolyGroup Edit Reference](/documentation/en-us/unreal-engine/polygroup-edit-tool-in-unreal-engine)

## Using Push Pull

| **Current Operation** | **Description** |
| --- | --- |
| **Apply** | Bakes extrusion changes into the mesh. |
| **Cancel (Esc)** | Negates changes. |

| **Extrusion Options** | **Description** |
| --- | --- |
| **Distance Mode** | 
Determines how the extrusion distance is set. You can use the following methods:

-   **Click in Viewport:** Mouse movement controls extrusion height and depth. Click in the viewport to complete the extrusion and exit the operation. Using the cursor, you can align the extrusion distance to objects in the level. An additional line from the center of the selection indicates the direction of measurement for the extrusion.
-   **Fixed:** Set extrusion height or depth from a numerical input (**Distance**).



 |
| **Direction Mode** | 

Determines the direction vertices move during extrusion before the boolean operation. You can use the following methods:

-   **Vertex Normals:** Follow the vertex normals regardless of selection.
-   **Single Direction:** Move all triangles in the same direction regardless of their normals.
-   **Selected Triangle Normals:** Take the angle-weighted average of the selected triangles around each extruded vertex to determine vertex movement direction.
-   **Selected Triangle Normals Even:** Similar to Selected Triangle Normals, but also adjust the distance moved in an attempt to keep triangles parallel to their original facing.
    -   **Max Distance Scale Factor:** Controls the maximum distance vertices can move from the target distance in order to stay parallel with their source triangles.

[See below for examples.](/documentation/en-us/unreal-engine/push-pull-tool-in-unreal-engine#pushdirectionmodeexamples)



 |
| **Shells to Solids** | 

Controls whether extruding an entire open-border patch should create a solid or open shell.

-   True (enable): Open-border faces are extruded as a solid shell (no holes in the mesh).
-   False (disable): Open-border faces are extruded with an open shell.



 |

#### Push Direction Mode Examples

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83716e83-ab1c-466d-b901-7ab79eb5c7df/selection.png) | ![Vertex Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcb8f214-e227-4d11-aede-b3d779145f8f/vertex-normals.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e1518e1-83fe-4f94-a008-9470dbc50b77/push-pull-single-direction.png) | ![Selected Triangle Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5221b737-e539-4096-bc15-91a016b04772/triangle-normals.png) | ![Triangle Normal Even](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78df8e86-3c9c-43dc-b293-31b70f34e780/triangle-normal-even.png) |
| No Extrusion | Vertex Normal | Single Direction | Selected Triangle Normals | Selected Triangle Normals Even |

| **Advanced** | **Description** |
| --- | --- |
| **Measure Direction** | 
The direction to measure the distance of extrusion when Selected Triangle Normals, Vertex Normals, or Selected Triangle Normals Even is active. The extrusion height is set based on the mouse location on the respective axis. When Single Direction is active, the direction of the extrusion is based on Measure Direction. The setting is only available when Distance Mode is set to Click in Viewport. You can choose from the following directions:

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

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#tools,undohistory,andacceptingchanges) panel.