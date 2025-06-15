# Modeling Tools

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:38

---

**Modeling Mode** provides various tools for creating and editing geometry. These tools are organized into specific categories to help guide you through your modeling process.

The [Create](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#create) category can get you started with building a new mesh. To edit and inspect properties of your mesh you can use the following categories:

-   [Select](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#select): Edit element selections.
-   [Transform](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#xform): Adjust the placement or representation of a mesh.
-   [Deform](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#deform): Sculpt or distort a mesh as a whole or in specific areas.
-   [Model](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#model): Perform granular mesh editing.
-   [Mesh](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#mesh): Mesh processing for inspecting, optimizing, and editing a mesh's geometry.
-   [Voxel](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#voxel): Convert a mesh into voxels to perform volumetric operations before converting it back into a mesh.
-   [Bake](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#bake): Generate textures and vertex color data for meshes.
-   [UVs](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#uvs): Edit the UV coordinates of a mesh.
-   [Attribs](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#attribs): Inspect and adjust the secondary properties of a mesh.
-   [Misc](/documentation/en-us/unreal-engine/modeling-tools-in-unreal-engine#misc): Additional utility tools such as managing LODs and volume conversion.

Each tool per category opens a specific toolset and settings in the [Tool Properties](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#accessingmodelingmode) panel. Refer to the categories below to learn how to implement them in your workflow.

The modeling tools are usable when working on various types of actors in Unreal Engine, for example, a static mesh, dynamic mesh, or volume. These are collectively referred to as "a mesh" or "meshes", except when a tool is only usable for a specific actor type.

## Create

Build new meshes from predefined primitives, paths, or splines. The following predefined primitives are available:

*Box* Sphere *Cylinder* Cone *Torus* Arrow *Rectangle* Disc *Stairs* Capsule

To learn more about these primitives, see [Predefined Shapes](/documentation/en-us/unreal-engine/predefined-shapes-in-unreal-engine).

Several tools, such as **Extrude Polygon** and **Extrude Path**, use a grid to draw shapes. To control the position of the grid, **Ctrl + Click** your desired location.

| Tool | Description |
| --- | --- |
| **CubeGrid** | Creates blockout meshes using a repositionable grid. To learn more about this tool, see the [CubeGrid](/documentation/en-us/unreal-engine/cubegrid-tool-in-unreal-engine) overview. |
| **Extrude Polygon** | Draws and extrudes polygons freehand or from a selection of predefined shapes. |
| **Extrude Path** | Draws and extrudes **PolyPaths** to create new meshes such as walls and ramps. |
| **Revolve Path** | Draws and revolves pathways around an axis to create a symmetrical mesh. |
| **Revolve Path** | Draws and revolvse 2D paths to create a new mesh. |
| **Revolve Spline** | Revolves a spline to create a new mesh. |
| **Draw Spline** | Draws a spline in the level. To learn more about this tool, see [Draw Spline](/documentation/en-us/unreal-engine/draw-spline-tool-in-unreal-engine). |
| **Mesh Spline** | Triangulates the spline components of the selected actors to create new meshes. |

## Select

Edit element selections.

**Mesh Element Select** must be enabled in the **Modeling Mode Quick Settings**.

| Tool | Description |
| --- | --- |
| **Delete** | Removes the current mesh selection. |
| **Extrude** | Protrudes geometry from the set of selected faces by moving and stitching them. |
| **Offset** | Protrudes selected faces similar to the Extrude operation, but defaults to moving faces along vertex normals instead of a single direction. Mouse movement controls the offset distance. Click in the viewport to complete the offset. |
| **Push Pull** | Faces can cut away the mesh or bridge mesh parts. To learn more, see [Push Pull](/documentation/en-us/unreal-engine/push-pull-tool-in-unreal-engine). |
| **Inset** | Insets the current set of selected faces. Mouse movement controls the inset distance. Click in the viewport to complete the inset. |
| **Outset** | Expands the set of selected faces out. Mouse movement controls the outset distance. Click in the viewport to confirm the outset distance. |
| **Cut** | Divides the selected PolyGroup faces at the drawn line, as if cutting them with a plane through that line. Click the face to draw the cutting line. New PolyGroups are formed at the border of the cut. |
| **Bevel** | Slants the edge loops around the selected faces. |
| **Insert Loop** | Inserts a chain of edges across quads in a mesh. You can not insert edges on non-quad faces. |
| **Clean** | Retriangulate the current mesh or mesh selection. |

## Xform

Adjust the placement or representation of a mesh.

| Tool | Description |
| --- | --- |
| **Transform** | Transform different aspects of the selected mesh. |
| **Align** | Repositions the selected meshes in relation to one another. |
| **Merge** | Combines multiple meshes into one, keeping intersecting geometry. |
| **Duplicate** | Duplicates a single mesh, creating a new actor. |
| **Edit Pivot** | Edit the pivot point placement on the selected mesh. To learn more about this tool, see the [Edit Pivot](/documentation/en-us/unreal-engine/edit-pivot-tool-in-unreal-engine) overview. |
| **Bake Transform** | Bakes the scale and rotation values into the mesh. By default, scale is uniformly set to 1, while rotation is uniformly set to 0. |
| **Transfer** | Transfers the data of one mesh to a target mesh or a specific LOD used by the target mesh. |
| **Convert** | Change the Output Type of a mesh between a Static Mesh, Dynamic Mesh, or Volume. |
| **Split** | Takes a mesh with disconnected geometry and splits them into separate mesh. |
| **Pattern** | Tile one or more selected meshes along a **Line**, **Grid**, or **Circle** oriented on a movable 3D plane. |
| **ISMEd** | Edit instances in Instance Static Mesh Components. |

## Deform

Sculpt or distort a mesh as a whole or in specific areas.

| Tool | Description |
| --- | --- |
| **Vertex Sculpt** | Sculpts the selected mesh (adjusting its vertices) using various brushes. To learn more, see the [Vertex Sculpt Tool](/documentation/en-us/unreal-engine/vertex-sculpt-tool-in-unreal-engine) overview. |
| **Dynamic Sculpt** | Sculpts the selected mesh using various brushes and dynamically adds new geometry to the mesh through remeshing. To learn more, see the [Dynamic Sculpt Tool](/documentation/en-us/unreal-engine/dynamic-sculpt-tool-in-unreal-engine) overview. |
| **Smooth** | Even out the surface of the mesh, helping remove jagged artifacts. To learn more, see the [Smooth Tool](/documentation/en-us/unreal-engine/smooth-tool-in-unreal-engine) overview. |
| **Offset** | Adjust the positioning of the mesh's vertices by a specified amount along their normal. To learn more, see the [Offset Tool](/documentation/en-us/unreal-engine/offset-tool-in-unreal-engine) overview. |
| **Warp** | Reshape a mesh using non-linear transforms such as **Blend**, **Flare**, and **Twist**. To learn more, see the [Warp Tool](/documentation/en-us/unreal-engine/warp-tool-in-unreal-engine) overview. |
| **Lattice** | Edit a mesh via its vertices using a structure of points. To learn more, see the [Lattice Tool](/documentation/en-us/unreal-engine/lattice-tool-in-unreal-engine) overview. |
| **Displace** | Distort the vertices of a mesh based on preset algorithms, user-generated weight maps, or texture maps. To learn more, see the [Displace Tool](/documentation/en-us/unreal-engine/displace-tool-in-unreal-engine) overview. |
| **Deform PolyGroups** | Opens tools to deform meshes via their PolyGroups. To learn more about this tool, see the [Deform PolyGroups Tool](/documentation/en-us/unreal-engine/deform-polygroups-tool-in-unreal-engine) overview. |

## Model

Perform granular mesh editing.

| Tool | Description |
| --- | --- |
| **PolyGroup Edit** | Opens tools, such as **Extrude**, **Bevel**, and **Edge Loop**, to edit meshes via PolyGroups. To learn more about this tool, see the [PolyGroup Edit](/documentation/en-us/unreal-engine/polygroup-edit-tool-in-unreal-engine) overview. |
| **Subdivide** | Increases the resolution of a mesh by PolyGroups or triangles. To learn more about this tool, see the [Subdivide](/documentation/en-us/unreal-engine/subdivide-tool-in-unreal-engine) overview. |
| **Boolean** | Subtracts or adds mesh pairs. To learn more about this tool, see the [Boolean](/documentation/en-us/unreal-engine/boolean-tool-in-unreal-engine) overview. |
| **PolyCut** | Cuts the selected mesh with extrude polygon and open tools to define the new mesh. |
| **Plane Cut** | Cuts the selected mesh on a plane. |
| **Mirror** | Reflects a mesh along a given plane to create new geometry. |
| **Mesh Cut** | Splits one mesh into parts using a second mesh. To learn more about this tool, see the [Mesh Cut](/documentation/en-us/unreal-engine/mesh-cut-tool-in-unreal-engine) overview. |
| **Trim** | Trims or cuts selected meshes with a second mesh. |

## Mesh

Mesh processing for optimizing and editing a mesh's geometry.

When using the following tools for optimization, it is helpful to change the [View Mode](/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine) and enable **Mesh Edges** under [Show](/documentation/en-us/unreal-engine/viewport-show-flags-in-unreal-engine) > **Advance**.

| Tool | Description |
| --- | --- |
| **Tri Select** | Selects triangles to edit a mesh and adjust secondary properties. |
| **Triangle Edit** | Opens tools to edit the mesh via triangles. |
| **Fill Holes** | Fills any holes in your mesh. |
| **Weld** | Automatically combines disconnected edges of the selected mesh within a given tolerance. |
| **Union** | Combines multiple meshes into one, resolving self-intersections. |
| **Jacket** | Removes hidden triangles from the selected meshes. |
| **Simplify** | Attempts to reduce the triangle density of the selected mesh. |
| **Remesh** | Retriangulate and increase triangle density on the selected mesh. |
| **Project** | Map or re-mesh one mesh onto the targeted mesh (the second selected mesh). |

## Voxel

Convert a mesh into voxels to perform volumetric operations before converting it back into a mesh.

| Tool | Description |
| --- | --- |
| **Voxel Wrap** | Wraps a selected mesh using voxels—helping remove holes as well as removing self-intersections and hidden triangles. |
| **Voxel Blend** | Blends selected meshes using voxels. |
| **Voxel Offset** | Offsets or inset the surface of the selected meshes using voxels. |
| **Voxel Boolean** | Performs boolean operations on selected meshes and then wrap the result with voxels. |
| **Voxel Merge** | Merges selected meshes and then voxelates the result. |

## Bake

Generate textures and vertex color data for meshes.

The source mesh(es) and target mesh must overlap for proper baking.

| Tool | Description |
| --- | --- |
| **Bake Textures** | Bake the source mesh's details to a target mesh as textures. |
| **Bake All** | Bake textures for a single mesh from multiple source meshes. |
| **Bake Vertex Colors** | Bake a source mesh's details to a target mesh as vertex colors. |
| **Bake RC** | Bakes textures for a target mesh from multiple source meshes via a virtual photo or render capture. |

## UVs

Edit the UV coordinates of a mesh, changing how textures are mapped to the surface. To learn more about this category, see [UVs Category](/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine).

| Tool | Description |
| --- | --- |
| **AutoUV** | Automatically unwrap and pack UVs for the selected mesh. |
| **UV Unwrap** | Recompute UVs for existing UV islands or PolyGroups, helping minimize stretched and squashed areas. |
| **Project UVs** | Creates UVs from casting a predefined shape or point onto your mesh. |
| **Edit UV Seams** | Interactively separate edges in the Viewport to create seams. |
| **Transform UVs** | Interactively scale, rotate, and translate UV islands in the Viewport. |
| **Layout UVs** | Transform, stack, or repack existing UVs. |
| **UV Editor** | Launch a dedicated Editor for creating and editing UVs. |

## Attribs

Inspect and adjust a mesh's secondary properties, such as normals and PolyGroups.

| Tool | Description |
| --- | --- |
| **Inspect** | Inspect mesh attributes. |
| **LOD Manager** | Opens the LOD Manager to define and create LODs for the selected static mesh asset. |
| **Normals** | Recomputes the normals and opens tools to set Normals calculations by toggling options on and off and setting the Normals Topography. |
| **Tangents** | Edit the mesh's lines and tangents. |
| **Generate PolyGroups** | Generates PolyGroups for your mesh. |
| **Paint PolyGroups** | Paint PolyGroups onto a mesh using brushstrokes. |
| **Edit Attributes** | Edit the mesh's different attributes, including UVs, and add new attributes. |
| **Edit Materials** | Assign multiple materials and new material elements to triangles selected via brushstrokes. |
| **Paint Vertex Colors** | Adds color values to the vertices of a mesh (including nanite meshes). To learn more about this tool, see [Paint Vertex Colors](/documentation/404). |
| **Paint Maps** | Paint on specific Weight Map Layers, which you first must generate with the Edit Attribute tool. To learn more about this tool, see [Paint Maps](/documentation/en-us/unreal-engine/paint-maps-tool-in-unreal-engine). |
| **Inspect Collision** | Inspect physics geometry for the selected mesh. |
| **Simple Collision Editor** | Edit the simple collision shape of the selected mesh. |
| **Mesh To Collision** | Convert the selected mesh to Simple Collision Geometry for the last selected mesh. |
| **Collision To Mesh** | Converts Simple Collision Geometry to a new mesh actor. |

## Misc

Additional utility tools such as managing LODs and volume conversion.

| Tool | Description |
| --- | --- |
| **AutoLOD** | Opens a toolset to generate and define static mesh LOD Assets. |
| **Pivot Actor** | Add an actor to act as a pivot for the child components. |
| **Revolve Boundary** | Revolves the mesh boundary loops to create a new shape. |
| **Volume To Mesh** | Define and convert a volume actor to a static or dynamic mesh actor. |
| **Mesh To Volume** | Defines the conversion of a mesh to a new volume. |
| **Convert BSPs** | Convert Binary Space Partitioning geometry to a mesh. |