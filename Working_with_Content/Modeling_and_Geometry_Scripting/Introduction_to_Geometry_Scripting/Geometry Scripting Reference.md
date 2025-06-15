# Geometry Scripting Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:35

---

The Geometry Scripting library contains a very broad range of functionality, from low-level mesh construction and queries, such as building a mesh triangle-by-triangle or counting its vertices, to high-level operations like mesh booleans and intersection tests.

For more information on using the Geometry Scripting library, see [Geometry Scripting Users Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-users-guide-in-unreal-engine).

Most functions are available while working in the editor and at runtime. However, some are only available while working in the editor and have been noted in the tables below.

For more information on the various functions, see the [Blueprint](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/GeometryScript) and [Python](https://docs.unrealengine.com/en-US/PythonAPI/) APIs.

## Asset and Component Read/Write

You can use these functions to read and write dynamic mesh instances, such as reading and writing to or from an existing or new asset or component.

| Node Name | Description |
| --- | --- |
| 
**Copy Mesh From Static Mesh**

 | 

Extracts a Dynamic Mesh from a Static Mesh Asset.

 |
| 

**Copy Mesh To Static Mesh**

 | 

Updates a Static Mesh Asset with new geometry converted from a Dynamic Mesh.

 |
| 

**Copy Mesh From Component**

 | 

Extracts a Dynamic Mesh Actor from any supported Component type, in World or Local space.

 |
| 

**Create New Volume From Mesh**

 | 

Creates a new Volume Actor, such as a Blocking Volume, from a Dynamic Mesh Actor.

This node only works in the Editor.



 |
| 

**Create New Static Mesh Asset From Mesh**

 | 

Creates a new Static Mesh Asset from a Dynamic Mesh Actor.

This node only works in the Editor.



 |
| 

**Set Static Mesh Collision From Mesh**

 | 

Generates Simple Collision shapes for a Static Mesh Asset based on the input Mesh.

 |
| 

**Set Dynamic Mesh Collision From Mesh**

 | 

Generate Simple Collision shapes for a Dynamic Mesh Component based on the input Mesh.

 |
| 

**Copy Collision Meshes From Object**

 | 

Extracts the Collision Geometry from From Object and copies it with meshes stored in To Dynamic Mesh.

-   For Simple Collision, From Object can be a Static Mesh Asset or any Primitive Component.
    
-   For Complex Collision, From Object can be a Static Mesh Asset, Static Mesh Component, or Dynamic Mesh Component.
    

 |
| 

**Reset Dynamic Mesh Collision**

 | 

Clears Simple Collisions from the Dynamic Mesh Component.

 |
| 

**Copy Mesh From Skeletal Mesh**

 | 

Copies the Skeletal Mesh into the target Dynamic Mesh.

 |
| 

**Copy Mesh To Skeletal Mesh**

 | 

Copies the given Dynamic Mesh to the Skeletal Mesh.

 |
| 

**Create New Skeletal Mesh Asset From Mesh**

 | 

Create a new Skeletal Mesh Asset from the Target Mesh.

This node only works in the Editor.



 |
| 

**Check Static Mesh Has Available LOD**

 | 

Checks if a Static Mesh Asset has the RequestedLOD available. That is if Copy Mesh From Static Mesh will be able to succeed for the given LODType and LODIndex.

 |
| 

**Get Num Static Mesh LODs Of Type**

 | 

Determines the number of available LODs of the requested LODType in a static mesh asset.

 |
| 

**Determine Mesh Occlusion**

 | 

Determines which meshes are entirely hidden by other meshes in the set, when viewed from outside.

 |
| 

**Get LOD Material List From Skeletal Mesh**

 | 

Extracts the Material List and corresponding Material Indices from the specified LOD of the skeletal mesh asset.

 |
| 

**Get Material List From Static Mesh**

 | 

Gets the asset materials from the static mesh asset.

 |
| 

**Get Material List From Skeletal Mesh**

 | 

Get the asset materials from the skeletal mesh asset.

 |
| 

**Convert Material Map To Material List**

 | 

Converts material map to a material list and a slot names list. Null materials will be kept in the list, and the list will have the same number of elements as the map.

 |
| 

**Convert Material List To Material Map**

 | 

Converts material list and slot names list to material map, which is the format expected by CreateNewSkeletalMeshAssetFromMesh.

 |
| 

**Copy Morph Target To Skeletal Mesh**

 | 

Add a Dynamic Mesh morph target to a skeletal mesh asset.

 |
| 

**Copy Skin Weight Profile To Skeletal Mesh**

 | 

Add a Dynamic Mesh skin weight profile to a Skeletal Mesh Asset.

 |

## Primitive Generation

You can use these functions to generate and append a primitive mesh to the input Dynamic Mesh.

| Node Name | Description |
| --- | --- |
| 
**Append Box**

 | 

Adds a 3D box to a specified Dynamic Mesh.

 |
| 

**Append Sphere Lat Long**

 | 

Adds a 3D Sphere triangulated using latitude/longitude topology to a Dynamic Mesh.

 |
| 

**Append Sphere Box**

 | 

Adds a 3D sphere triangulated using box topology to a Dynamic Mesh.

 |
| 

**Append Capsule**

 | 

Adds a 3D Capsule to a Dynamic Mesh.

 |
| 

**Append Cylinder**

 | 

Adds a 3D Cylinder (with optional end caps) to a Dynamic Mesh.

 |
| 

**Append Cone**

 | 

Adds a 3D cone to a Dynamic Mesh.

 |
| 

**Append Torus**

 | 

Adds a 3D torus (donut) or partial torus to a Dynamic Mesh.

 |
| 

**Append Rectangle XY**

 | 

Adds a planar Rectangle to a Dynamic Mesh.

 |
| 

**Append Round Rectangle XY**

 | 

Adds a planar Rectangle with Rounded Corners (RoundRect) to a Dynamic Mesh.

 |
| 

**Append Disc**

 | 

Adds a planar disc to a Dynamic Mesh.

 |
| 

**Append Triangulated Polygon**

 | 

Adds a [Delaunay triangulation](https://en.wikipedia.org/wiki/Delaunay_triangulation) of a planar 2D polygon to a Dynamic Mesh.

 |
| 

**Append Revolve Polygon**

 | 

Adds the surface-of-revolution of a 2D polygon, full or optionally-capped partial revolution to a Dynamic Mesh.

 |
| 

**Append Spiral Revolve Polygon**

 | 

Revolves a 2D polygon on a helical path, like one used to create a vertical spiral.

 |
| 

**Append Revolve Path**

 | 

Revolves an open 2D path, with optional top and bottom end caps.

 |
| 

**Append Simple Extrude Polygon**

 | 

Extrudes a 2D polygon along a vertical path using a selected Dynamic Mesh.

 |
| 

**Append Simple Swept Polygon**

 | 

Sweeps a 2D polygon along an arbitrary 3D path using a selected Dynamic Mesh.

 |
| 

**Append Linear Stairs**

 | 

Adds a linear staircase using a selected Dynamic Mesh.

 |
| 

**Append Curved Stairs**

 | 

Adds a rising circular staircase using a selected Dynamic Mesh.

 |
| 

**Append Mesh Transformed**

 | 

Applies each transform to Append Mesh, then adds its geometry to the Target Mesh.

 |
| 

**Append Sweep Polygon**

 | 

Sweeps and rotates a 2D polygon along the Sweep Path to create a 3D mesh that appends to the provided mesh.

 |
| 

**Append Voronoi Diagram 2D**

 | 

Generates triangulated Voronoi Cells from the provided Voronoi Sites, identifying each with PolyGroups, and appends to the provided mesh.

 |
| 

**Append Sweep Polyline**

 | 

Sweep the given 2D Polyline Vertices along the Sweep Path specified as a set of FTransforms. If the 2D vertices are (U,V), then in the coordinate space of the FTransform, X points "along" the path, Y points "right" (U), and Z points "up" (V).

 |
| 

**Append Bounding Box**

 | 

Adds a 3D box to the Target Mesh with dimensions and origin taken from the input Box.

 |
| 

**Append Delaunay Triangulation 2D**

 | 

Generates a Delaunay Triangulation of the provided vertices, and appends it to the Target Mesh.

 |
| 

**Append Polygon List Triangulation**

 | 

Generates a Delaunay Triangulation of the provided Polygon List, and appends it to the Target Mesh.

 |
| 

**Append Triangulated Polygon 3D**

 | 

Appends a Triangulated Polygon (with vertices specified in 3D) to the Target Mesh. Uses Ear Clipping-based triangulation. Output vertices will always be 1:1 with input vertices. Polygon endpoint is not repeated.

 |
| 

**Append Simple Collision Shapes**

 | 

Appends Simple Collision shapes to the Target Mesh, triangulated as specified by Triangulation Options.

 |
| 

**Append Sphere Covering**

 | 

Appends the spheres in the Sphere Covering to the Target Mesh.

 |
| 

**Append Box With Collision**

 | 

Appends a 3D box to the Target Mesh and creates matching simple collision.

 |
| 

**Append Bounding Box With Collision**

 | 

Appends a 3D box to the Target Mesh with dimensions and origin taken from the input Box. Also creates matching simple collision.

 |
| 

**Append Sphere Lat Long With Collision**

 | 

Appends a 3D Sphere triangulated using latitude/longitude topology to the Target Mesh. Also creates matching simple collision.

 |
| 

**Append Sphere Box With Collision**

 | 

Appends a 3D sphere triangulated using box topology to the Target Mesh. Also creates matching simple collision.

 |
| 

**Append Capsule With Collision**

 | 

Appends a 3D Capsule to the Target Mesh. Also creates matching simple collision.

 |
| 

**Create Constrained Edges Loop**

 | 

Intended for use with Append Delaunay Triangulation 2D. Create a loop of edges through sequential vertices. For example, a Loop (3,0) constructs edges (2,0), (0,1) and (1,2).

 |
| 

**Create Constrained Edges Chain**

 | 

Intended for use with Append Delaunay Triangulation 2D. Create a chain of edges through sequential vertices. For example, a Chain (3,0) will construct edges (0,1) and (1,2).

 |

## Transform and Deformation

You can use these functions to manipulate the vertex positions of a Dynamic Mesh. These manipulations do not change the mesh topology or connectivity.

| Node Name | Description |
| --- | --- |
| 
**Translate Mesh**

 | 

Applies a translation to the vertices of a Mesh.

 |
| 

**Scale Mesh**

 | 

Applies a scale transformation to the vertices of a Mesh.

 |
| 

**Transform Mesh**

 | 

Applies an arbitrary FTransform to the vertices of a Mesh.

 |
| 

**Apply Bend Warp To Mesh**

 | 

Applies a bend warp around an axis defined by a Transform.

 |
| 

**Apply Twist Warp To Mesh**

 | 

Applies a twist warp around an axis defined by a Transform.

 |
| 

**Apply Flare Warp To Mesh**

 | 

Applies a Flare or Bulge warp.

 |
| 

**Apply Math Warp To Mesh**

 | 

Applies various simple math-function-based warps, currently a 1D or 2D sine-wave with arbitrary orientation.

 |
| 

**Apply Perlin Noise To Mesh**

 | 

Applies a 3D Perlin noise displacement to the entire mesh or regions of the mesh defined by optional Selection.

 |
| 

**Apply Iterative Smoothing To Mesh**

 | 

Applies several mesh smoothing iterations to the entire mesh or a subset defined by the optional Selection

 |
| 

**Apply Displace From Texture Map**

 | 

Applies a displacement to a Dynamic Mesh based on a Texture2D and a UV channel.

 |
| 

**Rotate Mesh**

 | 

Rotates the mesh relative to the specified origin.

 |
| 

**Translate Pivot To Location**

 | 

Set the Pivot Location for the Mesh. Since the Pivot of a Mesh object is always the point at (0,0,0), this function simply translates the mesh by -PivotLocation.

 |
| 

**Make Transform From Z Axis**

 | 

Create a transform at the given location, with the ZAxis vector as the Z-axsis of the transform, and the X or Y axis oriented to the tangent vector, based on the `bTangentIsX` parameter.

 |
| 

**Make Transform From Axes**

 | 

Create a transform at the given location, with the ZAxis vector as the Z-axsis of the transform, and the X or Y axis oriented to the Tangent vector, based on the `bTangentISX` parameter.

 |
| 

**Get Transform Axis Vector**

 | 

Get the vector for the direction of the X, Y, and Z axis of the transform.

 |
| 

**Get Transform Axis Ray**

 | 

Get the ray at the transform location aligned with the direction of the X,Y, and Z-axis of the transform.

 |
| 

**Get Transform Axis Plane**

 | 

Get the plane at the transform location with the plane normal aligned with the direction of the X,Y, and Z-axis of the transform.

 |

## Composition and Decomposition

You can use these functions to combine meshes together, or split them apart.

| Node Name | Description |
| --- | --- |
| 
**Copy Mesh To Mesh**

 | 

Copies the mesh from one Dynamic Mesh into another.

 |
| 

**Get Sub Mesh From Mesh**

 | 

Copies a list of triangles from one Dynamic Mesh to another.

 |
| 

**Split Mesh By Components**

 | 

Separates a mesh into parts, one for each connected component, drawn from a Dynamic Mesh Pool.

 |
| 

**Split Mesh By Material IDs**

 | 

Separates a mesh into parts, one for each Material ID, drawn from a Dynamic Mesh Pool.

 |
| 

**Append Mesh**

 | 

Adds the geometry from one mesh to another, with optional Transform.

 |
| 

**Append Mesh Repeated**

 | 

Adds the geometry from one mesh to another based on the number of times it should repeat, accumulating a transform each time. This operation is useful for making patterns.

 |
| 

**Split Mesh By Vertex Overlap**

 | 

Creates a new mesh for each vertex-connected or vertex-overlapping part of Target Mesh.

 |
| 

**Sort Meshes By Volume**

 | 

Sorts meshes by their volume.

For meshes with open boundary, volume is computed with respect to the average vertex position.



 |
| 

**Sort Meshes By Area**

 | 

Sorts meshes by their surface area.

 |
| 

**Sort Meshes By Bounds Volume**

 | 

Sorts meshes by their axis-aligned bounding box volume.

 |
| 

**Sort Meshes By Custom Values**

 | 

Sorts meshes according to the values in a second array, which must have the same length as the Meshes array.

For example, if the values array is \[3, 2, 1\], with Ascending Sort Order, the Meshes array would be reversed.

 |

## Mesh Modeling

These functions provide standard high-level modeling operations, but are generally calling the low-level mesh processing code that the similarly-named Tool in Modeling Mode would call.

| Node Name | Description |
| --- | --- |
| 
**Apply Mesh Boolean**

 | 

Applies a Boolean operation (such as, Union, Intersect, and Subtract) to a Dynamic Mesh based on a second mesh.

 |
| 

**Apply Mesh Plane Cut**

 | 

Applies a plane cut to a mesh, optionally filling any holes created.

 |
| 

**Apply Mesh Plane Slice**

 | 

Slices a mesh into two halves, with optional hole filling.

 |
| 

**Apply Mesh Mirror**

 | 

Mirrors a mesh across a plane, with optional cutting and welding of triangles.

 |
| 

**Apply Mesh Offset**

 | 

Moves the vertices of a mesh to an offset surface.

 |
| 

**Apply Mesh Shell**

 | 

Moves a copy of the mesh's triangles to an offset surface, and stitches them to the original triangles. For example, to create a thickened shell.

 |
| 

**Apply Mesh Extrude**

 | 

Extrudes the triangles of a mesh along a constant direction. For example, it creates a solid from an open triangulated polygon.

 |
| 

**Apply Mesh Solidify**

 | 

Replaces the mesh with a voxelized-and-meshed approximation (VoxWrap operation).

 |
| 

**Apply Mesh Morphology**

 | 

Replaces the mesh with an SDF-based offset mesh approximation.

 |
| 

**Apply Mesh Self Union**

 | 

An object performs a Boolean Union operation with itself, computing actions such as repairing self-intersections and removing floating geometry.

 |
| 

**Apply Mesh PolyGroup Bevel**

 | 

Applies Mesh Bevel operation to all PolyGroup Edges.

 |
| 

**Apply Mesh Disconnect Faces Along Edges**

 | 

Disconnects triangles of Target Mesh along the edges of the Selection. The input Selection still identifies the same geometric elements after disconnecting.

 |
| 

**Apply Mesh Bevel Edge Selection**

 | 

Applies a Mesh Bevel operation to parts of Target Mesh using the Bevel Options settings.

 |
| 

  **Apply Mesh Iso Curves**

 | 

Inserts edges along the curve where the interpolated per-vertex values match a given iso value.

 |

## Mesh Selections

These functions identify regions of a mesh to different tools so they can operate locally. Several functions can work on the entire mesh or a subset defined by a Selection. Selection Types include: Triangle, Vertices, and PolyGroups.

| Node Name | Description |
| --- | --- |
| 
**Invert Mesh Selection**

 | 

Invert the selection on the Target Mesh.

 |
| 

**Create Select All Mesh Selection**

 | 

Creates a selection of the given selection type containing all the elements of the Target Mesh

 |
| 

**Convert Mesh Selection**

 | 

Converts a mesh selection to a different type.

By default, vertices map to triangles within a [one-ring](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-reference-in-unreal-engine?application_version=5.5#glossary) neighborhood, and triangles to all contained vertices.

 |
| 

**Combine Mesh Selections**

 | 

Combines two mesh selections into a new mesh selection. The two inputs, Selection A and Selection B must have the same type.

 |
| 

**Convert Index Array To Mesh Selection**

 | 

Creates a mesh selection from the Index Array.

 |
| 

**Convert Index Set To Mesh Selection**

 | 

Creates a mesh selection from the Index Set.

 |
| 

**Convert Mesh Selection To Index Array**

 | 

Converts a mesh selection to an Index Array.

 |
| 

**Convert Index List To Mesh Selection**

 | 

Creates a mesh selection from the Index List. For cases where the Index List Type does not match the Selection Type, Convert mesh selection with `bAllowPartialInclusion=true` is used to convert.

 |
| 

**Convert Mesh Selection To Index List**

 | 

Converts a mesh selection to an Index List.

 |
| 

**Select Mesh Elements In Box**

 | 

Creates a new mesh selection of the Selection Type for the Target Mesh by finding all elements contained in the Box.

 |
| 

**Select Mesh Elements In Box With BVH**

 | 

Create a new Mesh Selection of the Selection Type for the Target Mesh by finding all elements contained in the Box. Similar to **Select Mesh Elements In Box** but takes a BVH to make it work faster.

 |
| 

**Select Mesh Elements In Sphere**

 | 

Creates a new mesh selection of the Selection Type for the Target Mesh by finding all elements contained in the Sphere.

 |
| 

**Select Mesh Elements With Plane**

 | 

Creates a new mesh selection of the Selection Type for the Target Mesh by finding all elements on one side of the plane, particularly the side that the surface normal of a Plane points towards.

 |
| 

**Select Mesh Elements By Normal Angle**

 | 

Creates a new mesh selection of the Selection Type for the Target Mesh by finding all elements that have a normal vector that is within an angular deviation threshold from the given Normal.

For Triangle and PolyGroup selections the triangle facet normal is used, for Vertex selections the per-vertex averaged normal is used.

 |
| 

**Select Mesh Elements Inside Mesh**

 | 

Creates a new mesh selection of the Selection Type for the Target Mesh by finding all elements inside a second Selection Mesh.

 |
| 

**Expand Mesh Selection To Connected**

 | 

Expands the Selection on the Target Mesh to connected regions and returns the New Selection.

 |
| 

**Get Mesh Selection Bounding Box**

 | 

Gets the 3D Bounding Box of a mesh selection.

 |
| 

**Get Mesh Selection Boundary Loops**

 | 

Computes the set of Vertex Loops bordering a mesh selection. Both the 3D polylines and lists of vertex indices are returned for each Loop.

For a Vertex selection, this function returns the border loops around the one-ring neighborhood of the vertex selection.



 |
| 

**Get Mesh Selection Info**

 | 

Queries information about a mesh selection.

 |
| 

**Debug Print Mesh Selection**

 | 

Prints information about the mesh selection to the Output Log.

 |
| 

**Expand Contract Mesh Selection**

 | 

Grow or shrink the Selection on the Target Mesh to connected neighbors.

*For vertex selections, Expand includes vertices in one-ring of selected vertices, and Contract removes any vertices with a one-ring neighbor that is not selected.* For triangle selections, add or remove triangles connected to selected triangles. \* For PolyGroup selections, add or remove PolyGroups connected to selected PolyGroups.



 |
| 

**Get Mesh Unique Selection Info**

 | 

Queries information about a Mesh Selection, and get a count of unique selected elements

 |
| 

**Select Mesh Elements By Material ID**

 | 

Creates a Selection of the Selection Type that contains all mesh elements referencing triangles with the given Material ID.

 |
| 

**Select Mesh Elements By Polygroup**

 | 

Creates a Selection of the SelectionType that contains all mesh elements referencing triangles with the given PolyGroup ID in the given GroupLayer.

 |
| 

**Select Mesh Sharp Edges**

 | 

Creates a new Selection, for the Target Mesh, of all sharp edges where the edge's adjacent triangle normals differ by at least MinAngleDeg.

 |
| 

**Select Mesh Boundary Edges**

 | 

Create a new Selection, for the TargetMesh, of all mesh boundary edges.

 |
| 

**Select Selection Boundary Edges**

 | 

Create a new BoundarySelection, for the TargetMesh, of the edges on the boundary of another Selection.

 |
| 

Select Mesh Split Normal Edges

 | 

Creates a new Selection, for the Target Mesh, of all edges seams in the mesh normal topology. That is, where normals can be different across the edge.

 |
| 

Select Mesh UV Seam Edges

 | 

Creates a new Mesh Selection of UV seam edges for the Target Mesh.

 |
| 

  Select Mesh PolyGroup Boundary Edges

 | 

Creates a new Mesh Selection of PolyGroup boundary edges for the Target Mesh. 

 |

## Modify Mesh by Selection

Functions for editing geometry from a given selection.

### Transform Mesh

| Node Name | Description |
| --- | --- |
| 
**Transform Mesh Selection**

 | 

Applies the given transform to the selected part of the mesh.

 |
| 

**Translate Mesh Selection**

 | 

Applies the given translation to the selected part of the mesh.

 |
| 

**Rotate Mesh Selection**

 | 

Rotates the selected part of the mesh relative to the specified origin.

 |
| 

**Scale Mesh Selection**

 | 

Applies the given scale to the selected part of the mesh.

 |
| 

**Inverse Transform Mesh**

 | 

Applies the inverse of the provided transform to the Target Mesh.

 |
| 

**Inverse Transform Mesh Selection**

 | 

Applies the inverse of the given transform to the vertices identified by the Selection of the Target Mesh.

 |

### Materials and PolyGroups

| Node Name | Description |
| --- | --- |
| 
**Set Material ID For Mesh Selection**

 | 

Sets a new Material ID on all the triangles of the given Selection.

 |
| 

**Set PolyGroup For Mesh Selection**

 | 

Sets a new PolyGroup on all the triangles of the given Selection, for the given Group Layer.

 |

### Mesh Modeling

| Node Name | Description |
| --- | --- |
| 
**Apply Mesh Disconnect Faces**

 | 

Disconnects the triangles of the Target Mesh identified by the Selection.

 |
| 

**Apply Mesh Duplicate Faces**

 | 

Duplicates the triangles of the Target Mesh identified by the Selection input.

 |
| 

**Apply Mesh Linear Extrude Faces**

 | 

Applies Linear Extrusion to the triangles of Target Mesh identified by the Selection.

 |
| 

**Apply Mesh Offset Faces**

 | 

Applies an Offset to the faces of the Target Mesh identified by the Selection, or all faces if Selection is empty.

 |
| 

**Apply Mesh Inset Outset Faces**

 | 

Applies an Inset or Outset to the faces of Target Mesh identified by the Selection, or all faces if the Selection is empty.

 |
| 

**Apply Mesh Bevel Selection**

 | 

Applies a Mesh Bevel operation to parts of Target Mesh using the Bevel Options settings.

 |

## Subdivision

These functions apply various mesh subdivision strategies to a Dynamic Mesh.

| Node Name | Description |
| --- | --- |
| 
**Apply PolyGroup Catmull Clark SubD**

 | 

Apply Catmull Clark Subdivision to the PolyGroup Topology of the mesh (discards input triangulation).

This node only works in the Editor.



 |
| 

**Apply Triangle Loop SubD**

 | 

Apply Loop Subdivision to the input mesh.

This node only works in the Editor.



 |
| 

**Apply Selective Tessellation**

 | 

Tessellate the specified mesh selection using the indicated Pattern Type.

 |
| 

**Apply PN Tessellation**

 | 

Apply point-normal tessellation to the input mesh.

 |
| 

**Apply Uniform Tessellation**

 | 

Apply a uniform tessellation to the input mesh.

 |

## Simplification

These functions simplify a mesh using various strategies.

| Node Name | Description |
| --- | --- |
| 
**Apply Simplify To Triangle Count**

 | 

Simplifies the mesh until a target triangle count is reached.

 |
| 

**Apply Simplify To Vertex Count**

 | 

Simplifies the mesh until a target vertex count is reached.

 |
| 

**Apply Simplify To Tolerance**

 | 

Simplifies the mesh to a target geometric tolerance. For example, any further simplification would result in a deviation from the input mesh larger than the tolerance.

 |
| 

**Apply Simplify To Planar**

 | 

Simplifies planar areas of the mesh that have more triangles than necessary.

This does not change the 3D shape of the mesh.



 |
| 

**Apply Simplify To PolyGroup Topology**

 | 

Simplifies the mesh down to the PolyGroup Topology. For example, the high-level faces of the mesh PolyGroups. Another example would be on a default Box-Sphere where simplifying to PolyGroup topology produces a box.

 |
| 

  Apply Editor Simplify To Triangle Count

 | 

Simplifies the mesh until a target triangle count is reached, using the UE Editor's standard mesh simplifier. Editor only.

 |
| 

  Apply Editor Simplify To Vertex Count

 | 

Simplifies the mesh until a target vertex count is reached, using the UE Editor's standard mesh simplifier. Editor only.

 |

## Box

Utility functions for computing basic math functions for box objects.

| Node | Description |
| --- | --- |
| 
**Make Box From Center Size**

 | 

Create a box from a center point, and X, Y, and Z dimensions.

 |
| 

**Make Box From Center Extents**

 | 

Create a box from a center point and X, Y, and Z [extents](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-reference-in-unreal-engine?application_version=5.5#glossary). Extents are half-dimensions.

 |
| 

**Get Box Center Size**

 | 

Get the center point, and X, Y, and Z dimensions of a box.

 |
| 

**Get Box Corner**

 | 

Get the position of a corner of the box. Corners are indexed from 0 to 7, using an ordering where:

-   0 is the Min corner
    
-   1/2/3 are +Z/+Y/+X from the Min corner
    
-   7 is the Max corner
    
-   4/5/6 are -Z/-Y/-X from the Max corner
    

 |
| 

**Get Box Face Center**

 | 

Get the position of the center of a face of a box. Faces are indexed from 0 to 5, using an ordering where:

-   0 and 1 are the MinZ and MaxZ faces
    
-   2 and 3 are MinY and MaxY
    
-   4 and 5 are MinX and MaxX
    

 |
| 

**Get Box Volume Area**

 | 

Get the volume and surface area of a box.

 |
| 

**Get Expanded Box**

 | 

Get the input box expanded by adding the Expand By parameter to both the Min and Max. Dimensions will be clamped to the center point if any of the Expand By parameters are larger than half the box size.

 |
| 

**Get Transformed Box**

 | 

Apply the input transform to the corners of the input box, and return the new box containing those points.

 |
| 

**Test Box Box Intersection**

 | 

Test if box 1 and box 2 intersect.

 |
| 

**Find Box Box Intersection**

 | 

Find the box formed by the intersection of box 1 and box 2.

 |
| 

**Get Box Box Distance**

 | 

Calculate the minimum distance between box 1 and box 2.

 |
| 

**Test Point Inside Box**

 | 

Test if a point is inside the box; returning true if so, otherwise false.

 |
| 

**Find Closest Point On Box**

 | 

Find the point on the faces of the box that is closest to the input point. If the point is inside the Box, it is returned.

 |
| 

**Get Box Point Distance**

 | 

Calculate the minimum distance between the box and the point.

 |
| 

**Test Box Sphere Intersection**

 | 

Check if the box intersects a sphere defined by the Sphere Center and Sphere Radius.

 |

## Normals

These functions recompute the normals of a mesh.

| Node Name | Description |
| --- | --- |
| 
**Flip Normals**

 | 

Flips the mesh normals by reversing the orientation of each face.

 |
| 

**Set Per Vertex Normals**

 | 

Sets the mesh normals to per-vertex normals. For example, no split normals at any vertex.

 |
| 

**Set Mesh To Facet Normals**

 | 

Sets the mesh normals to per-face/triangle normals. For example, split normals along every edge of the mesh.

 |
| 

**Compute Split Normals**

 | 

Computes split-normals for the mesh based on an angle tolerance and/or other factors such as PolyGroup topology.

 |
| 

**Recompute Normals**

 | 

Recomputes the existing mesh normals. Preserves existing split normals. For use after mesh deformations, for example.

 |
| 

**Compute Tangents**

 | 

Recomputes tangents for the mesh (various methods).

 |
| 

**Set Mesh Per Vertex Normals**

 | 

Set all normals in the Target Mesh Normals Overlay to the specified per-vertex normals.

 |
| 

**Get Mesh Has Tangents**

 | 

Check if the target mesh has a Tangents Attribute Layer enabled.

 |
| 

**Discard Tangents**

 | 

Remove any existing Tangents Attribute Layer from the Target Mesh.

 |
| 

**Compute Tangents**

 | 

Recompute tangents for the Target Mesh, using the method specified by

 |
| 

**Set Mesh Per Vertex Tangents**

 | 

Set all tangents in the Target Mesh Tangents Overlays to the specified per-vertex tangents.

 |
| 

**Get Mesh Per Vertex Tangents**

 | 

Compute the interpolated Position, `A * Vertex1 + B * Vertex2 + C * Vertex3`, where (A,B,C) = BarycentricCoords and the Vertex positions are taken from the specified TriangleID of the target mesh.

 |
| 

**Update Vertex Normal**

 | 

Update the Normals and Tangents at VertexD of the Target Mesh.

 |
| 

**Recompute Normals For Mesh Selection**

 | 

Recompute the normals of Target Mesh on all the triangles/vertices of the given Selection using the given Calculate Options. This method will preserve any existing hard edges, that is each shared triangle-vertex normal is recomputed by averaging the face normals of triangles that reference that shared triangle-vertex normal.

 |
| 

**Set Split Normals Along Selected Edges**

 | 

Set or remove split normals (aka sharp normals) for all edges in the Selection.

 |
| 

**Flip Triangle Selection Normals**

 | 

Inverts the normal vectors of the triangles in a given selection of Target Mesh. For edge or vertex selections, normals for the triangles touching the selected edges or vertices will be flipped.

 |

## Cleanup and Repair

You can use these functions to fix issues in a mesh, or to apply other standard repairs.

| Node Name | Description |
| --- | --- |
| 
**Compact Mesh**

 | 

Compacts the mesh's vertices and triangles to remove any "holes" in the Vertex ID or Triangle ID lists (see discussion in Low-Level Mesh Queries section).

 |
| 

**Discard Mesh Attributes**

 | 

Removes the Attribute Set from a Dynamic Mesh, such as all UVs, Normals, Material IDs, Vertex Colors, and extended PolyGroup Layers. Note that this may prevent many functions from working.

 |
| 

**Auto Repair Normals**

 | 

This function tries to automatically reorient the Normals of a mesh so that they are consistent, such as fixing flipped normals.

 |
| 

**Weld Mesh Edges**

 | 

Welds any open boundary edges of the mesh together if possible in order to remove "cracks."

 |
| 

**Fill All Mesh Holes**

 | 

Tries to fill all open boundary loops (such as holes in the geometry surface) of a mesh.

 |
| 

**Remove Small Components**

 | 

Removes connected components of the mesh that have a volume, area, or triangle count below a threshold.

 |
| 

**Remove Hidden Triangles**

 | 

Removes any triangles in the mesh that are not visible from the exterior view, under various definitions of "visible" and "outside."

 |
| 

**Resolve Mesh TJunctions**

 | 

Attempts to resolve t-junction in the Target Mesh.

 |
| 

**Split Mesh Bowties**

 | 

Splits vertices in the Target Mesh that otherwise produce a bowtie where only a single vertex connects regions of the mesh.

 |
| 

**Repair Mesh Degenerate Geometry**

 | 

Modifies the Target Mesh by deleting small triangles or merging triangles until all edges are greater than a specified minimum length.

 |
| 

**Remove Unused Vertices**

 | 

Remove vertices that are not used by any triangles.

Does not update the IDs of any remaining vertices. Use Compact Mesh to do so.



 |
| 

**Snap Mesh Open Boundaries**

 | 

Snap vertices on open edges to the closest compatible open boundary, if found within the tolerance distance.

 |

## Low-Level Mesh Queries

These functions provide low-level information about the elements of a mesh. In this context, **VertexID** and **TriangleID** are integers.

In a Dynamic Mesh, there may be gaps in VertexID or TriangleID range — after vertices/triangles are deleted — and some operations (like Simplification) may return a mesh with gaps present. Gaps in the ID ranges are cleaned up using the Compact Mesh function.

| Node Name | Description |
| --- | --- |
| 
**Get Vertex Count**

 | 

Gets the number of vertices in the mesh.

 |
| 

**Get Num Vertex IDs**

 | 

Gets the number of Vertex IDs in the mesh, which may be larger than the Vertex Count, if the mesh is not dense. For example, after deleting vertices.

 |
| 

**Is Valid Vertex ID**

 | 

Returns true if a Vertex ID refers to a valid vertex.

 |
| 

**Get All Vertex IDs**

 | 

Returns an IndexList of all Vertex IDs in mesh.

 |
| 

**Get Vertex Position**

 | 

Gets the 3D position of a mesh vertex, by Vertex ID.

 |
| 

**Get All Vertex Positions**

 | 

Returns a Vector List of all the mesh vertex positions. This list may be extensive.

 |
| 

**Get Triangle Count**

 | 

Returns the number of triangles in the mesh. Note that this is a function on the Dynamic Mesh directly.

 |
| 

**Get Num Triangle IDs**

 | 

Gets the number of Triangle IDs in the mesh. The number may be larger than the Triangle Count if the mesh is not dense, even after deleting triangles.

 |
| 

**Is Valid Triangle ID**

 | 

Returns true if a TriangleID refers to a valid Triangle.

 |
| 

**Get All Triangle IDs**

 | 

Returns an Index List of all Triangle IDs in a mesh.

 |
| 

**Get Triangle Indices**

 | 

Returns the vertex indices triplet for a Triangle.

 |
| 

**Get All Triangle Indices**

 | 

Returns a TriangleList of all Triangle indices triplets in a mesh.

 |
| 

**Get Triangle Positions**

 | 

Returns the three corner positions for a Triangle.

 |
| 

**Get Triangle Face Normal**

 | 

Returns the face/facet normal of a Triangle.

 |
| 

**Get Triangle UVs**

 | 

Returns the three corner UVs for a Triangle.

 |
| 

**Get Triangle Material ID**

 | 

Returns the current Material ID for a Triangle.

 |
| 

**Get All Triangle Material IDs**

 | 

Returns an Index List of all triangle Material IDs.

 |
| 

**Get Triangle PolyGroup ID**

 | 

Returns the current PolyGroup ID for a Triangle, in a given PolyGroup layer.

 |
| 

**Get Has Vertex ID Gaps**

 | 

Returns true if there are gaps in the Vertex ID list. For example, Get Number of Vertex IDs is greater than Get Vertex Count.

 |
| 

**Get Has Triangle ID Gaps**

 | 

Returns true if there are gaps in the Triangle ID list, such that Get Num Triangle IDs is greater than Get Triangle Count.

 |
| 

**Get Is Dense Mesh**

 | 

Returns true if the mesh is dense. For example, no gaps in Vertex IDs or Triangle IDs.

 |
| 

**Get Mesh Has Attribute Set**

 | 

Returns true if the mesh has an Attribute Set enabled to store UVs, Normals, Material IDs, and Vertex Colors. This is generally enabled by default.

 |
| 

**Get Interpolated Triangle Position**

 | 

Compute the interpolated Position, `A * Vertex1 + B * Vertex2 + C * Vertex3`, where (A,B,C) = BarycentricCoords and the Vertex positions are taken from the specified TriangleID of the target mesh.

 |
| 

**Compute Triangle Barycentric Coords**

 | 

Compute the barycentric coordinates (A,B,C) of the Points relative to the specified TriangleID of the Target Mesh.

 |
| 

**Get Interpolated Triangle UV**

 | 

Compute the interpolated UV, `A * UV1 + B * UV2 + C * UV3`, where (A,B,C) = BarycentricCoords and the UV positions are taken from the specified TriangleID in the specified UV Channel of the Target Mesh.

 |
| 

**Get Triangle Normals**

 | 

For the specified TriangleID of the Target Mesh, get the Normal and Tangent vectors at each vertex of the Triangle. These Normals and Tangents will be taken from the Normal and Tangents Overlays.

 |
| 

**Get Interpolated Triangle Normal**

 | 

Compute the interpolated Normal, `A * Normal1 + B * Normal2 + C * Normal3`, where (A,B,C) = BarycentricCoords and the Normals are taken from the specified TriangleID in the Normal layer of the Target Mesh.

 |
| 

**Get Triangle Normal Tangents**

 | 

For the specified TriangleID of the Target Mesh, get the Normal and Tangent vectors at each vertex of the Triangle. These Normals and Tangents will be taken from the Normal and Tangents Overlays.

 |
| 

**Get Interpolated Triangle Normal Tangents**

 | 

Compute the interpolated Normal and Tangents for the specified TriangleID in the Normal and Tangent attributes of the Target Mesh.

 |
| 

**Get Has Vertex Colors**

 | 

Return true if the Target Mesh has the Vertex Colors attribute enabled.

 |
| 

**Get Triangle Vertex Colors**

 | 

For the specified TriangleID of the Target Mesh, get the Vertex Colors at each vertex of the Triangle. These Colors will be taken from the Vertex Color Attribute.

 |
| 

**Get Interpolated Triangle Vertex Color**

 | 

Compute the interpolated Vertex Color, `A * Color1 + B * Color2 + C * Color3`, where (A,B,C) = BarycentricCoords and the Colors are taken from the specified TriangleID in the Vertex Color layer of the Target Mesh.

 |
| 

**Get All Vertex Positions At Edges**

 | 

Returns the vertex positions for each edge in the given index list.

 |
| 

**Get Mesh UV Area**

 | 

Gets the area of triangles in UV space for the given UV Channel.

 |
| 

**Get All UV Seam Edges**

 | 

Returns all edge element IDs that are UV seam edges for a given UV channel.

 |
| 

**Get Num UV Islands**

 | 

Returns the number of UV islands in a given UV channel.

 |

## Low-Level Mesh Building

These functions construct a mesh triangle-by-triangle and perform other low-level mesh editing operations.

Using these functions in situations that involve looping over the elements of meshes with many thousands of triangles can be quite slow in Blueprint or Python scripting.

| Node Name | Description |
| --- | --- |
| 
**Set Vertex Position**

 | 

Sets the 3D position of a mesh vertex.

 |
| 

**Add Vertex To Mesh**

 | 

Adds a new vertex to the mesh and returns a new Vertex ID.

 |
| 

**Add Vertices To Mesh**

 | 

Adds a list of vertices to the mesh.

 |
| 

**Delete Vertex From Mesh**

 | 

Removes a vertex from the mesh.

 |
| 

**Delete Vertices From Mesh**

 | 

Removes a list of vertices from the mesh.

 |
| 

**Add Triangle To Mesh**

 | 

Adds a triangle (3-element Vertex ID tuple) to the mesh.

 |
| 

**Add Triangles To Mesh**

 | 

Adds a list of triangles to the mesh.

 |
| 

**Delete Triangle From Mesh**

 | 

Removes a triangle from the mesh.

 |
| 

**Delete Triangles From Mesh**

 | 

Removes a list of triangles from the mesh.

 |
| 

**Delete Triangles In PolyGroup**

 | 

Deletes all triangles from the mesh that have a particular PolyGroup, in a specific PolyGroup layer.

 |
| 

**Append Buffers To Mesh**

 | 

Adds a set of vertices/triangles to the mesh, with attributes such as Normals and UVs. Similar to Create Mesh Section in Proc Mesh Component.

 |
| 

**Set Mesh Triangle Normals**

 | 

Sets the Normals of a mesh triangle.

 |
| 

**Set Mesh Triangle UVs**

 | 

Sets the UVs of a mesh triangle.

 |
| 

**Set Triangle Material ID**

 | 

Sets the Material ID of a mesh triangle.

 |
| 

**Set All Mesh Vertex Positions**

 | 

Set all vertex positions in the Target Mesh to the specified positions.

 |
| 

**Append Mesh With Materials**

 | 

Apply Append Transform to Append Mesh and then add its geometry to the Target Mesh. Also combines materials lists of the Target and Append meshes, and updates the output mesh materials to reference the combined list.

 |
| 

**Append Mesh Transformed With Materials**

 | 

For each transform in AppendTransforms, apply the transform to AppendMesh and then add its geometry to the TargetMesh Also combines materials lists of the Target and Append meshes, and updates the output mesh materials to reference the combined list.

 |
| 

**Append Mesh Repeated With Materials**

 | 

Repeatedly apply AppendTransform to the AppendMesh, each time adding the geometry to TargetMesh. Also combines materials lists of the Target and Append meshes, and updates the output mesh materials to reference the combined list.

 |
| 

**Merge Mesh Vertex Pair**

 | 

Attempts to merge together two vertices, and report whether they were merged.  

Some merges may be prevented because they would create non-manifold edges in the mesh, which are not supported.



 |
| 

**Merge Mesh Vertices In Selections**

 | 

Attempts to merge together vertices in one selection to their closest vertices in the second selection, within a distance threshold.

Merges may be prevented because they would create non-manifold edges in the mesh, which are not supported.



 |

## Low-Level List Management

These functions cover list management for: Index List, Scalar List, Vector List, UV List, and Color List.

| Node Name | Description |
| --- | --- |
| 
**Get Index List Length**

 | 

Returns the number of items in the Index List.

 |
| 

**Get Index List Last Index**

 | 

Returns the index of the last item in the Index List.

 |
| 

**Get Index List Item**

 | 

Returns the item stored in the Index List at the specified location.

 |
| 

**Set Index List Item**

 | 

Updates the value of the item stored in the Index List at the specified location.

 |
| 

**Convert Index List To Array**

 | 

Converts an Index List to an array of integers.

 |
| 

**Convert Array To Index List**

 | 

Converts an array of integers to an Index List.

 |
| 

**Duplicate Index List**

 | 

Duplicates the contents Index List into Duplicate List.

 |
| 

**Clear Index List**

 | 

Resets all the items in the Index List to the Clear Value.

 |
| 

**Get Scalar List Length**

 | 

Returns the number of items in the Scalar List.

 |
| 

**Get Scalar List Last Index**

 | 

Returns the index of the last item in the Scalar List.

 |
| 

**Get Scalar List Item**

 | 

Returns the Scalar (double) stored in the Scalar List at the specified location.

 |
| 

**Set Scalar List Item**

 | 

Updates the value of the Scalar stored in the Scalar List at the specified location.

 |
| 

**Convert Scalar List To Array**

 | 

Converts a Scalar List to an array of doubles.

 |
| 

**Convert Array To Scalar List**

 | 

Converts an array of doubles to a Scalar List.

 |
| 

**Duplicate Scalar List**

 | 

Copies the contents of Scalar List into Duplicate List.

 |
| 

**Clear Scalar List**

 | 

Reset all the items in the Scalar List to the Clear Value.

 |
| 

**Get Vector List Length**

 | 

Returns the number of items in the Vector List.

 |
| 

**Get Vector List Last Index**

 | 

Return the index of the last item in the Vector List.

 |
| 

**Get Vector List Item**

 | 

Return the FVector stored in the VectorList at the specified location.

 |
| 

**Set Vector List Item**

 | 

Updates the value of the FVector stored in the Vector List at the specified location.

 |
| 

**Convert Vector List To Array**

 | 

Converts a Vector List to an array of FVectors.

 |
| 

**Convert Array To Vector List**

 | 

Converts an Array of FVectors to a Vector List.

 |
| 

**Duplicate Vector List**

 | 

Copies the contents of Vector List into Duplicate Vector List.

 |
| 

**Clear Vector List**

 | 

Resets all the items in the Vector List to the Clear Value.

 |
| 

**Get UV List Length**

 | 

Returns the number of items in the UV List.

 |
| 

**Get UV List Last Index**

 | 

Returns the index of the last item in the UV List.

 |
| 

**Get UV List Item**

 | 

Returns the [FVector2D](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Core/Math/FVector2D?application_version=5.5) stored in the UV List at the specified location.

 |
| 

**Set UV List Item**

 | 

Updates the value of the FVector2D stored in the UV List at the specified location.

 |
| 

**Convert UV List To Array**

 | 

Converts a UV List to an array of FVector2Ds.

 |
| 

**Convert Array To UV List**

 | 

Converts an array of FVector2D to UVList.

 |
| 

**Duplicate UV List**

 | 

Duplicates the contents of UV List into Duplicate List.

 |
| 

**Get Color List Length**

 | 

Returns the number of items in the Color List.

 |
| 

**Get Color List Last Index**

 | 

Returns the index of the last item in the Color List.

 |
| 

**Get Color List Item**

 | 

Returns the [FLinearColor](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Core/Math/FLinearColor?application_version=5.5) stored in the Color List at the specified location.

 |
| 

**Set Color List Item**

 | 

Updates the value of the FLinearColor stored in the Color List at the specified location.

 |
| 

**Convert Color List To Array**

 | 

Converts the Color List to an array of FLinearColor.

 |
| 

**Convert Array To Color List**

 | 

Converts an array of FLinearColor to a Color List.

 |
| 

**Extract Color List Channel**

 | 

Creates a Scalar List that corresponds to the 0,1, or 2 channel of a Color List.

 |
| 

**Extract Color List Channels**

 | 

Creates a Vector List from a Color List. The channels in the Color List are mapped to vector components by means of X Channel Index, Y Channel Index, and Z Channel Index.

 |

## Low-Level Math

Functions that operate on the Vector Lists and Scalar Lists in a component wise fashion. The functions that take multiple lists, such as Vector Dot, require the lists to have the same number of elements.

| Node Name | Description |
| --- | --- |
| 
**Vector Length**

 | 

Computes the length of each vector in Vector List A and returns the value in the Scalar List.

 |
| 

**Vector Dot**

 | 

Computes the dot-product between each pair of vectors in Vector List A and Vector List B, and returns the value in the new Scalar List.

 |
| 

**Vector Cross**

 | 

Computes the cross-product between each pair of vectors in Vector List A and Vector List B and returns the value in the new Vector List.

 |
| 

**Vector Normalize In Place**

 | 

Normalizes each vector in Vector List, and stores the value in a Vector List. If a vector is degenerate, set the normal to the Set On Failure vector.

 |
| 

**Vector Blend**

 | 

Computes `ConstantA * A + ConstantB * B` for each pair of vectors in Vector List A and Vector List B, and returns the value in the new Vector List.

By default this (constants = 1) adds the two vectors. Set `ConstantB = -1` to subtract B from A.

You can also use the function to Linear Interpolate, by setting `ConstantB = 1 - ConstantA`.

 |
| 

**Vector Blend In Place**

 | 

Computes `ConstantA * A + ConstantB * B` for each pair of vectors in Vector List A and Vector List B, and stores the value in Vector List B.

By default this (constants = 1) adds the two vectors. Set `ConstantB = -1` to subtract B from A.

You can also use the function to Linear Interpolate, by setting `ConstantB = 1 - ConstantA`.

 |
| 

**Scalar Vector Multiply**

 | 

Computes `Scalar Multiplier * Scalar * Vector` for each scalar/vector pair in the two input lists, and returns the value in a new Vector List.

 |
| 

**Scalar Vector Multiply In Place**

 | 

Computes `Scalar Multiplier * Scalar * Vector` for each scalar/vector pair in the two input lists, and stores the value in the input Vector List.

 |
| 

**Constant Vector Multiply**

 | 

Computes `Constant * Vector` for each element in the Vector List and returns the value in a new list.

 |
| 

**Constant Vector Multiply In Place**

 | 

Computes `Constant * Vector` for each element in Vector List, and stores the value in Vector List.

 |
| 

**Vector To Scalar**

 | 

Converts each Vector in Vector List to a Scalar by computing `ConstantX * Vector.X + ConstantY * Vector.Y + ConstantZ * Vector.Z` , and returns the value in a new Scalar List.

You can use it to extract the X, Y, and Z values from a Vector, or other component-wise math.

 |
| 

**Scalar Invert**

 | 

Computes `Numerator / Scalar` for each element of the Scalar List and returns the value in a new Scalar List.

If Abs(Scalar) < Epsilon, set to Set On Failure value.

 |
| 

**Scalar Invert In Place**

 | 

Computes `Numerator / Scalar` for each element of the Scalar List and stores the value in input Scalar List.

If Abs(Scalar) < Epsilon, set to Set On Failure value.

 |
| 

**Scalar Blend**

 | 

Computes `ConstantA * A + ConstantB * B` for each pair of values in Scalar List A and Scalar List B and returns the value in the new Scalar List.

By default this (constants = 1) just adds the two values. Set `ConstantB = -1` to subtract B from A.

The function can also be used to Linear Interpolate, by setting `ConstantB = 1 - ConstantA`.

 |
| 

**Scalar Blend In Place**

 | 

Computes `ConstantA * A + ConstantB * B` for each pair of values in ScalarListA and ScalarListB and return in ScalarListB.

By default this (constants = 1) just adds the two values. Set `ConstantB = -1` to subtract B from A.

Can also be used to Linear Interpolate, by setting `ConstantB = ( 1 - ConstantA )`.

 |
| 

**Scalar Multiply**

 | 

Computes `Scalar Multiplier * A * B` for each pair of values in Scalar List A and Scalar List B, and returns the values in the new Scalar List.

 |
| 

**Scalar Multiply In Place**

 | 

Computes `Scalar Multiplier * A * B` for each pair of values in Scalar List A and Scalar List B, and returns the values in Scalar List B.

 |
| 

**Constant Scalar Multiply**

 | 

Computes `Constant * Scalar` for each value in Scalar List, and returns the values in the new Scalar List.

 |
| 

**Constant Scalar Multiply In Place**

 | 

Computes `Scalar Multiplier A * B` for each pair of values in Scalar List A and Scalar List B, and returns the values in the current Scalar List.

 |
| 

**Transform In Place**

 | 

Transform each vector in VectorList, and store in VectorList

 |
| 

**Vector Inverse Transform In Place**

 | 

Inverse transform each vector in VectorList, and store in VectorList.

 |
| 

**Vector Plane Project In Place**

 | 

Project each vector in VectorList to the given Plane, and store in VectorList.

 |

## Mesh Sampling

These functions calculate and place points along the surface of a mesh.

| Node | Description |
| --- | --- |
| 
**Compute Point Sampling**

 | 

Compute a set of sample points lying on the surface of Target Mesh based on the provided sampling Options. Samples are approximately uniformly distributed, and non-overlapping relative to the provided Options.

 |
| 

**Compute NonUniform Point Sampling**

 | 

Compute a set of sample points lying on the surface of Target Mesh based on the provided sampling Options and NonUniform Options.

 |
| 

**Compute Vertex Weighted Point Sampling**

 | 

Compute a set of sample points lying on the surface of TargetMesh based on the provided sampling Options and NonUniform Options.

 |
| 

**Compute Render Capture Cameras For Box**

 | 

Compute a set of Render Capture Cameras to capture a scene within the given Box.

 |
| 

**Compute Render Capture Point Sampling**

 | 

Compute oriented sample points on the visible surfaces of the given Actors. The Samples are computed using Render Capture from the given virtual cameras.

 |
| 

**Compute Uniform Random Point Sampling**

 | 

Computes a uniform random (not uniform spacing) point sampling over the mesh surface.

 |

## Mesh Sculpt Layers New!

These functions manage additional vertex offsets stored on the mesh. They can be blended together using prescribed weights.

| Node | Description |
| --- | --- |
| 
**Set Active Sculpt Layer**

 | 

Sets the requested Layer Index as the current active sculpt layer, if possible.

 |
| 

**Set Sculpt Layer Weight**

 | 

Sets the weight of the layer at Layer Index to the requested Weight.

 |
| 

**Set Sculpt Layer Weights Array**

 | 

Sets the weights of multiple layers to match the given Weights array.Note: If the Weights array length is larger than the number of layers, will just set the weights of the existing layers. Will not add or remove layers.

 |
| 

**Get Sculpt Layer Weights Array**

 | 

Gets the weights of all sculpt layers on the mesh.

 |
| 

**Get Num Sculpt Layers**

 | 

Gets the number of sculpting layers active on the mesh.

 |
| 

**Get Active Sculpt Layer**

 | 

Gets the current sculpting layers active on the mesh, or -1 if the mesh does not have sculpting layers.

 |
| 

**Discard Sculpt Layers**

 | 

Discards all sculpt layer data, leaving current vertex positions unchanged.

 |
| 

**Merge Sculpt Layers**

 | 

Merges a range of sculpt layers together. May change the Active Sculpt Layer.

 |

## Ray

Utility functions for creating and querying rays. A ray is a line which can be used to determine intersections of objects. These are particularly useful for building interactive user interfaces in Blueprints.

| Node | Description |
| --- | --- |
| 
**Make Ray From Points**

 | 

Create a ray from two points, placing the origin at A and the direction as Normalize (B-A).

 |
| 

**Make Ray From Point Direction**

 | 

Create a ray from an origin and direction, with optionally non-normalized direction.

 |
| 

**Get Transformed Ray**

 | 

Apply the given transform to the given ray, or optionally the Transform Inverse, and return the new transformed ray.

 |
| 

**Get Ray Point**

 | 

Get a point at the given distance along the Ray, `Origin + Distance * Direction`.

 |
| 

**Get Ray Start End**

 | 

Get two points along the ray.

 |
| 

**Get Ray Parameter**

 | 

Project the given point onto the closest point along the ray, and return the ray parameter and distance at that point.

 |
| 

**Get Ray Point Distance**

 | 

Get the distance from the given point to the closest point on the ray.

 |
| 

**Get Ray Closest Point**

 | 

Get the closest point on the Ray to the given point.

 |
| 

**Get Ray Sphere Intersection**

 | 

Check if the ray intersects a sphere defined by the Sphere Center and Sphere Radius. This function returns two intersection distances (ray parameters). If the ray grazes the sphere, both distances will be the same. If it misses, they will be MAX\_FLOAT. Use the function Get Ray Point to convert the distances to points on the ray and sphere.

 |
| 

**Get Ray Box Intersection**

 | 

Check if the ray intersects a sphere defined by the Sphere Center and Sphere Radius.

 |
| 

**Get Ray Plane Intersection**

 | 

Find the intersection of a ray and a plane.

 |
| 

**Get Ray Line Closest Point**

 | 

Compute the pair of closest points on a 3D ray and line. The line is defined by an origin and direction, but extends infinitely in both directions.

 |
| 

**Get Ray Segment Closest Point**

 | 

Compute the pair of closest points on a 3D ray and line segment. The line segment is defined by its two endpoints.

 |

## Point Set

Functions for working with point sets.

| Node | Description |
| --- | --- |
| 
**KMeans Cluster To IDs**

 | 

Use K-Means clustering to cluster the given points into a target number of clusters, and return an array with a cluster index per point.

 |
| 

**KMeans Cluster To Arrays**

 | 

Use K-Means clustering to cluster the given points into a target number of clusters, and return the clusters as an array of lists of point indices.

 |
| 

**Downsample Points**

 | 

Find a subset of the given Points of a specified size. You can optionally specify a priority weighting and/or request uniform spacing for the downsampled points.

 |
| 

**Transforms To Points**

 | 

Create an array of the positions of the input Transforms.

 |
| 

**Offset Transforms**

 | 

Offset the location of all Transforms by Offset in the given Direction, either locally in the space of the transform or in world space. For example, this can offset mesh surface samples along the surface normal direction.

 |
| 

**Flatten Points**

 | 

Convert an array of points from 3D to 2D, by transforming into the given ReferenceFrame and taking the X,Y coordinates Note that to transform into the ReferenceFrame, we apply the inverse of the ReferenceFrame's transform.

 |
| 

**Unflatten Points**

 | 

Convert an array of points from 2D to 3D, by transforming out of the given ReferenceFrame, with the given Height for the non-flat axis (default Z).

 |
| 

**Make Bounding Box From Points**

 | 

Make a Axis Aligned Bounding Box that bounds the given Points, optionally expanded by some additional amount on each side.

 |
| 

**Get Points From Index List**

 | 

Create an array of the subset of AllPoints indicated by the Indices list.

 |

## Materials

Functions for manipulating Material IDs of a mesh. A Material ID is a per-triangle integer and is not directly connected to any specific Material. Each Material ID is associated with a **Mesh Section** when converting to or from a Static Mesh.

| Node Name | Description |
| --- | --- |
| 
**Get Has Material IDs**

 | 

Returns true if the mesh has Material IDs available/enabled.

 |
| 

**Enable Material IDs**

 | 

Enables Material IDs on a mesh, initialize to 0.

 |
| 

**Clear Material IDs**

 | 

Resets all Material IDs on a mesh to 0.

 |
| 

**Get Max Material ID**

 | 

Returns the maximum Material ID currently set on a mesh.

 |
| 

**Remap Material IDs**

 | 

For all triangles with a Material ID matching a given value, and sets the Material ID to a new value.

 |
| 

**Set All Triangle Material IDs**

 | 

Sets the Material ID of all triangles in a mesh to the values in an input Index List.

 |
| 

**Set PolyGroup Material ID**

 | 

Sets the Material ID of all triangles in a mesh that have a specified PolyGroup ID (in a given PolyGroup layer) to the specified Material ID.

 |
| 

**Remap To New Material IDs By Material**

 | 

Remap the Material IDs of the Target Mesh to a new set of Material IDs based on a From/Current Material List, and a New Material List. For each triangle, the current Material is determined as FromMaterialList\[MaterialID\], and then the first index of this Material is found in the ToMaterialList, and this index is used as the new MaterialID. If a Material cannot be found in ToMaterialList, a warning will be printed and the MaterialID left unmodified, unless MissingMaterialID is set to a value >= 0, in which case MissingMaterialID will be assigned.

 |
| 

**Remap And Combine Materials**

 | 

Remap material IDs to be consistent with a Required Materials list. The Target Mesh material IDs will be remapped to reference the Combined Materials list, which will always start with the Required Materials.

 |

## Collision

Functions for creating, editing, and maniputing collision shapes.

| Node Name | Description |
| --- | --- |
| 
**Static Mesh Has Customized Collision**

 | 

Returns true if the static mesh has customized collision. If no editor data is available, returns false.

 |
| 

**Get Simple Collision From Component**

 | 

Get the simple collision from a Primitive Component.

 |
| 

**Set Simple Collision Of Dynamic Mesh Component**

 | 

Set the simple collision on a Dynamic Mesh Component.

 |
| 

**Get Simple Collision From Static Mesh**

 | 

Get the simple collision from a Static Mesh.

 |
| 

**Set Simple Collision Of Static Mesh**

 | 

Set the simple collision on a Static Mesh.

 |
| 

**Get Simple Collision Shape Count**

 | 

Count of number of simple collision shapes.

 |
| 

**Transform Simple Collision Shapes**

 | 

Transform simple collision shapes.

 |
| 

**Combine Simple Collision**

 | 

Add simple collision shapes from Append Collision to Collision To Update.

 |
| 

**Simplify Convex Hulls**

 | 

Simplify any convex hulls in the given simple collision representation. Updates the passed-in Simple Collision.

 |
| 

**Approximate Convex Hulls With Simpler Collision Shapes**

 | 

Attempt to approximate any convex hulls in the given simple collision representation. Updates the passed-in Simple Collision. Convex hulls that aren't well approximated (to tolerances set in ApproximateOptions) will remain as convex hulls.

 |
| 

**Merge Simple Collision Shapes**

 | 

Attempt to merge collision shapes to create a representation with fewer overall shapes.

 |
| 

**Compute Negative Space**

 | 

Compute the negative space of an input mesh surface that should be protected when merging simple collision shapes.

 |
| 

**Sphere Covering To Array Of Spheres**

 | 

Return an array of the spheres in the given Sphere Covering.

 |
| 

**Array Of Spheres To Sphere Covering**

 | 

Return a sphere covering containing the spheres in the given Spheres array.

 |
| 

**Set Static Mesh Custom Complex Collision**

 | 

Sets a static mesh as the custom collision for another static mesh to use.

Note: Only works if editor-only data is available.



 |
| 

**Reset Simple Collision**

 | 

Clears the Simple Collision shapes.

 |
| 

**Generate Collision From Mesh**

 | 

Generates Simple Collision shapes for an input Dynamic Mesh shape.

 |
| 

**Combine Simple Collision Array**

 | 

Combines the SimpleCollisionArray collision shapes into a single SimpleCollision.

 |
| 

**Compute Navigable Convex Decomposition**

 | 

Computes the 'navigable' convex decomposition of an input mesh surface. That is a convex decomposition appropriate for a character of (or larger than) a given size.

 |

## Containment

Functions to approximate a mesh with convex hull.

| Node Name | Description |
| --- | --- |
| 
**Compute Mesh Convex Hull**

 | 

Computes the Convex Hull of a given Target Mesh, or part of the mesh if an optional Selection is provided, and puts the result in Hull Mesh.

 |
| 

**Compute Mesh Swept Hull**

 | 

Computes the Swept Hull of a given Target Mesh for a given 3D Plane defined by ProjectionFrame, and puts the result in Hull Mesh. The Swept Hull is a linear sweep of the 2D convex hull of the mesh vertices projected onto the plane (the sweep precisely contains the mesh extents along the plane normal)

 |
| 

**Compute Mesh Convex Decomposition**

 | 

Compute a Convex Hull Decomposition of the given TargetMesh. Assuming more than one hull is requested, multiple hulls will be returned that attempt to approximate the mesh.

If simplification settings are enabled,there is no guarantee that the entire mesh is contained in the hulls.



 |

## Vertex Values

You use these functions to get and manipulate mesh values stored at vertices, including **Vertex Colors**

Multiple values, such as Normals, can be stored at a given vertex but these methods will only return one.

| Node Name | Description |
| --- | --- |
| 
**Set Mesh Constant Vertex Color**

 | 

Sets all vertex colors to a specific color.

 |
| 

**Set Mesh Per Vertex Colors**

 | 

Sets the color for every vertex using a Color List.

 |
| 

**Get Mesh Per Vertex Colors**

 | 

Gets a list of single vertex colors for each mesh vertex in the Target Mesh, derived from the Vertex Color [Overlay](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-reference-in-unreal-engine?application_version=5.5#glossary).

 |
| 

**Set Mesh Selection Vertex Color**

 | 

Sets the colors in the Target Mesh's Vertex Color Overlay, identified by the Selection, to a constant value.

-   For a Vertex Selection, each existing Vertex Color Overlay Element for the vertex is updated.
    
-   For a Triangle or PolyGroup Selection, all Overlay elements in the identified Triangles are updated.
    

 |
| 

**Convert Mesh Vertex Colors SRGB To Linear**

 | 

Apply an SRGB to Linear color transformation on all vertex colors.

 |
| 

**Convert Mesh Vertex Colors Linear To SRGB**

 | 

Apply a Linear to SRGB color transformation on all vertex colors.

 |
| 

**Get Mesh Per Vertex Normals**

 | 

Get a list of single normal vectors for each mesh vertex in the Target Mesh, derived from the Normals Overlay.

 |
| 

**Get Mesh Per Vertex UVs**

 | 

Get a list of single vertex UVs for each mesh vertex in the Target Mesh, derived from the specified UV Overlay.

 |
| 

**Blur Mesh Vertex Colors**

 | 

Blur the color attribute of the mesh. If the mesh has no color attribute, the function returns the mesh unchanged.

 |
| 

**Transfer Vertex Colors From Mesh**

 | 

Transfers the vertex colors from the Source Mesh to the Target Mesh.

 Assumes that the meshes are aligned. Otherwise, use the Transform Mesh geometry script function to align them.

 |

## Texture Sampling and Creation

Functions for reading and creating texture data.

| Node Name | Description |
| --- | --- |
| 
**Sample Texture 2D At UV Positions**

 | 

Sample the given Texture Map at the list of UV positions and return the color at each position in the Color List output.

 |
| 

**Create New Texture 2D Asset**

 | 

Create a serialized Texture 2D Asset from a temporary [UTexture2D](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Engine/UTexture2D?application_version=5.5).

 |
| 

**Sample Texture Render Target 2D At UV Positions**

 | 

Sample the given Texture Map at the list of UV positions and return the color at each position in Color List output. This function fetches GPU data before sampling, so, depending on your application, it can be inefficient and slow.

 |

## Baking

These functions bake data between a source and target mesh into texture or vertex color data. You can bake various mesh data such as normals, curvature, ambient occlusion, opacity map, and subsurface color map. There is also the ability to specify type of filtering to apply.

| Node Name | Description |
| --- | --- |
| 
**Bake Texture**

 | 

Creates textures for the Target Mesh from data sampled in the Source Mesh.

 |
| 

**Bake Vertex**

 | 

Populates the vertex colors in the Target Mesh with the results of the baking properties of the given Source Mesh.

 |
| 

**Bake Texture From Render Captures**

 | 

Bakes textures for a target mesh from render captures.

 |
| 

**Make Bake Type UV Shell**

 | 

Generate the bake options for UV Shell.

 |
| 

**Bake Signed Distance To Volume Texture**

 | 

Write a distance field to the given existing volume texture.

 |
| 

**Make Bake Type Height**

 | 

Generates the bake options for Height data.

 |

## UV

You use these functions to manipulate the [UVs](working-with-content/modeling-and-geometry-scripting/modeling-tools/uvs-category) of a mesh.

| Node Name | Description |
| --- | --- |
| 
**Get Num UV Channels**

 | 

Gets the number of UV [Channels](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-reference-in-unreal-engine?application_version=5.5#glossary) on a mesh.

 |
| 

**Set Num UV Channels**

 | 

Sets the number of UV Channels on a mesh.

 |
| 

**Get UV Set Bounding Box**

 | 

Gets the 2D bounding box of all UVs in a UV Channel.

 |
| 

**Copy UV Channel**

 | 

Replaces target UV Channel with values from source UV Channel.

 |
| 

**Translate Mesh UVs**

 | 

Applies 2D Translation to all UVs, or a subset of UVs if you provide a Selection, in the UVSet Index.

 |
| 

**Scale Mesh UVs**

 | 

Applies 2D Scale to all UVs, or a subset of UVs if you provide a Selection, in the UVSet Index.

 |
| 

**Rotate Mesh UVs**

 | 

Apples 2D Rotation to all UVs, or a subset of UVs if you provide a Selection, in the UVSet Index.

 |
| 

**Recompute Mesh UVs**

 | 

Recomputes UVs for a Mesh based on different types of well-defined UV islands, such as existing UV islands, PolyGroups, or the Selection input.

 |
| 

**Repack Mesh UVs**

 | 

Packs the existing UV islands into standard UV space.

 |
| 

**Set Mesh UVs From Planar Projection**

 | 

Using Planar projection, set UVs for an entire mesh or a subset you define by the Selection input.

 |
| 

**Set Mesh UVs From Box Projection**

 | 

Using Box Projection, set UVs for an entire mesh or a subset you define by the Selection input.

 |
| 

**Set Mesh UVs From Cylinder Projection**

 | 

Using Cylinder Projection, set UVs for an entire mesh or a subset you define by the Selection input.

 |
| 

**Auto Generate Patch Builder Mesh UVs**

 | 

Computes new UVs using PatchBuilder method, and optionally pack.

 |
| 

**Auto Generate X Atlas Mesh UVs**

 | 

Computes new UVs using XAtlas, and optionally packs.

 |
| 

**Get Mesh UVSize Info**

 | 

Computes information about dimensions and areas for a UV Channel of a Mesh, with an optional mesh selection.

 |
| 

**Get Mesh Per Vertex UVs**

 | 

Gets a list of single vertex UVs for each mesh vertex in the Target Mesh, derived from the specified UV Overlay.

 |
| 

**Copy Mesh UV Channel To Mesh**

 | 

Copies the 2D UVs from the given UV Channel Index in Copy From Mesh to the 3D vertex positions in Copy To UV Mesh. PolyGroup IDs and Material IDs are preserved in the UV Mesh.

 |
| 

**Copy Mesh To Mesh UV Channel**

 | 

Transfers the 3D vertex positions and triangles of Copy From UVMesh to the given UV Channel identified by To UV Channel Index of Copy To Mesh. The 3D positions (X,Y,Z) will be copied as UV positions (X,Y).

 |
| 

**Compute Mesh Local UV Param**

 | 

Compute local UV parameterization on Target Mesh vertices around the given CenterPoint / Triangle. This method uses a Discrete Exponential Map parameterization, which unwraps the mesh locally based on geodesic distances and angles. The Center Point will have a UV value (0,0), and the computed vertex UVs will be such that \` Length(UV) == geodesic distance\`.

 |
| 

**Add UV Element To Mesh**

 | 

Adds a new UV Element to the specified UV Channel of the Mesh and returns a new UV Element ID.

 |
| 

**Set Mesh Triangle UV Element IDs**

 | 

Sets the UV Element IDs for a given Triangle in the specified UV Channel, that is the UV Triangle indices. This function does not create new UVs. The UV Triangle can only be set if the resulting topology would be valid. That is the elements cannot be shared between different base Mesh Vertices, so they must either be unused by any other triangles, or already associated with the same mesh vertex in other UV triangles. If any conditions are not met, bIsValidTriangle will be returned as false.

 |
| 

**Get Mesh Triangle UV Element IDs**

 | 

Returns the UV Element IDs associated with the three vertices of the triangle in the specified UV Channel. If the Triangle does not exist in the mesh or if no UVs are set in the specified UV Channel for the triangle, bHaveValidUVs will be returned as false.

 |
| 

**Get Mesh UV Element Position**

 | 

Returns the UV Position for a given UV Element ID in the specified UV Channel. If the UV Channel or Element ID does not exist, bIsValidElementID will be returned as false.

 |
| 

**Set Mesh UV Element Position**

 | 

Sets the UV position of a specific ElementID in the given UV Channel. If the UV Channel or Element ID does not exist, bIsValidElementID will be returned as false.

 |
| 

**Set UV Seams Along Selected Edges**

 | 

Converts Selection to an Edge selection, and set or remove UV seams along all of the selected edges.

 |
| 

**Apply Texel Density UV Scaling**

 | 

Rescales UVs in the UV Channel for a Mesh to match a specified texel density, described by the options passed in. Supports processing on a subset of UVs via a non-empty Selection.

 |
| 

**Layout Mesh UVs**

 | 

Packs the existing UV islands in the specified UV Channel into standard UV space based on the Repack Options.

 |
| 

**Transfer Mesh UVs By Projection**

 | 

Copies UVs from one mesh to another, by projecting along the requested direction.

This does not transfer UV seams, it assigns a single UV coordinate per vertex in the target mesh selection.



 |
| 

**Intersects UV Box 2D**

 | 

Tests two Box2D bounds for intersection, with optional support for working in a wrapped space.

 |

## PolyGroup

Functions for manipulating PolyGroups of a mesh. PolyGroups are per-triangle integers that implicitly define regions and patches of triangles in the modeling tools and some Geometry Script operations. However, a PolyGroup layer is ultimately a per-triangle number, and you can use it for any other purpose. To learn more about PolyGroups see, [Understanding PolyGroups](working-with-content/modeling-and-geometry-scripting/modeling-mode/understanding-polygroups).

| Node Name | Description |
| --- | --- |
| 
**Get Has PolyGroups**

 | 

Returns true if the mesh has a standard PolyGroup Layer.

 |
| 

**Enable PolyGroups**

 | 

Enables standard PolyGroup Layer on a Mesh.

 |
| 

**Get Num Extended PolyGroup Layers**

 | 

Returns the count of extended PolyGroup Layers.

Extended PolyGroup Layers are not yet fully supported by all operations or modeling tools.



 |
| 

**Set Num Extended PolyGroup Layers**

 | 

Sets the number of extended PolyGroup Layers on a Mesh.

 |
| 

**Clear PolyGroups**

 | 

Resets the triangle PolyGroup assignments to a constant value for a given PolyGroup Layer.

 |
| 

**Copy PolyGroups Layer**

 | 

Copies PolyGroups from one layer to another.

 |
| 

**Convert UV Islands To PolyGroups**

 | 

Creates and assigns a new PolyGroup for each disconnected UV island of a Mesh.

 |
| 

**Convert Components To PolyGroups**

 | 

Creates and assigns a new PolyGroup for each disconnected component of a Mesh.

 |
| 

**Compute PolyGroups From Angle Threshold**

 | 

Sets PolyGroups by partitioning the mesh based on an edge crease/opening-angle.

 |
| 

**Compute PolyGroups From Polygon Detection**

 | 

Identifies polygons and assigns PolyGroup IDs.

 |
| 

**Add Named Polygroup Layer**

 | 

Adds an extended PolyGroup layer with the given name. If a layer with that name is already on the mesh, that existing layer will be returned and no new layer will be added.

 |
| 

 **Find** **Extended Polygroup Layer By Name**

 | 

Finds an extended PolyGroup layer by its name. If there are multiple layers with the same name, returns the first such layer.

 |
| 

**Get PolyGroup Bounding Box**

 | 

Computes the bounds of a PolyGroup.

 |
| 

**GetPoly Group UV Bounding Box**

 | 

Computes the UV bounds of a PolyGroup.

 |
| 

**Get PolyGroup UV Centroid**

 | 

Computes the UV centroid of a PolyGroup.

 |

## Bone Weight

These functions calculate and manipulate bone weights, also known as skin weights. Bone weights determine a bone's transformation influence on a set of vertices. You can also get information about the skeleton stored in the dynamic mesh. This information is one-to-one with the Skeletal Mesh skeleton after you convert to dynamic mesh through the **Copy Mesh From Skeletal Mesh** node.

| Node | Description |
| --- | --- |
| 
**Mesh Has Bone Weights**

 | 

Check whether the Target Tesh has a per-vertex Bone Weight attribute set.

 |
| 

**Mesh Create Bone Weights**

 | 

Create a new Bone Weights attribute on the Target Mesh, if it does not already exist. If it does exist, and `bReplaceExistingProfile` is passed as true, the attribute will be removed and re-added, to reset it.

 |
| 

**Get Max Bone Weight Index**

 | 

Determine the largest Bone Weight index that exists on the mesh.

 |
| 

**Get Vertex Bone Weights**

 | 

Return an array of Bone Weight at a given vertex of the Target Mesh.

 |
| 

**Get Largest Vertex Bone Weight**

 | 

Return the Bone Weight of the maximum weight at a given vertex of the Target Mesh.

 |
| 

**Set Vertex Bone Weights**

 | 

Set the Bone Weight at a given vertex of the Target Mesh.

 |
| 

**Set All Vertex Bone Weights**

 | 

Set all vertices of the Target Mesh to the given Bone Weights.

 |
| 

**Compute Smooth Bone Weights**

 | 

Computes a smooth skin binding for the given mesh to the skeleton provided.

 |
| 

**Transfer Bone Weights From Mesh**

 | 

Transfer the bone weights from the SourceMesh to the TargetMesh. Assumes that the meshes are aligned. Otherwise, use the Transform Mesh geometry script function to align them.

 |
| 

**Copy Bones From Mesh**

 | 

Copy the bone attributes (skeleton) from the Source Mesh to the Target Mesh.

 |
| 

**Discard Bones From Mesh**

 | 

Discard the bone attributes (skeleton) from the Target Mesh.

 |
| 

**Get Bone Index**

 | 

Get the index of the bone with the given name.

 |
| 

**Get Root Bone Name**

 | 

Get the name of the root bone.

 |
| 

**Get Bone Children**

 | 

Get the information about the children of the bone.

 |
| 

**Get All Bones Info**

 | 

Get an array of bones representing the skeleton. Each entry contains information about the bone.

 |
| 

**Get Bone Info**

 | 

Get the index of the bone with the given name.

 |
| 

**Mesh Copy Bone Weights**

 | 

Copies all bone weights from a source profile onto a target profile, on the same mesh, replacing all.

 |
| 

**Blend Bone Weights**

 | 

Blends two bone weights using an Alpha value that ranges from 0 to 1, inclusive.

 |
| 

**Prune Bone Weights**

 | 

Prunes the given bones from any bone weight assignment on the given profile.

 |

## Mesh Geometric Queries

Functions for high-level geometric queries of a mesh.

| Node Name | Description |
| --- | --- |
| 
**Get Mesh Bounding Box**

 | 

Computes the bounding box of the mesh vertices.

 |
| 

**Get Mesh Volume Area**

 | 

Computes the volume and area of the mesh.

 |
| 

**Get Is Closed Mesh**

 | 

Returns true if the mesh is closed, such as no topological boundary edges.

 |
| 

**Get Num Open Border Loops**

 | 

Returns the number of open border loops, such as "holes" in the mesh.

 |
| 

**Get Num Open Border Edges**

 | 

Returns the number of topological boundary edges in the mesh.

 |
| 

**Get Num Connected Components**

 | 

Returns the number of separate connected-components in the mesh, such as "triangle patches" connected by shared edges.

 |
| 

**Compute Mesh Convex Hull**

 | 

Computes the Convex Hull of a given Mesh, or part of the mesh you define by the Selection input, and returns in a separate mesh.

 |
| 

**Compute Mesh Swept Hull**

 | 

Computes a 2D swept-hull of the input mesh and returns in a separate mesh.

 |
| 

**Compute Mesh Convex Decomposition**

 | 

Computes a Convex Hull Decomposition of the given Target Mesh. Assuming more than one hull is requested, multiple hulls will be returned that attempt to approximate the mesh. There is no guarantee that the entire mesh is contained in the hulls.

 |
| 

**Get Mesh Volume Area Center**

 | 

Computes the volume, area, and center-of-mass of the mesh.

 |

## Mesh Geodesic

These functions compute the shortest given path on a mesh surface.

| Node | Description |
| --- | --- |
| 
**Get Shortest Vertex Path**

 | 

Computes a vertex list that represents the shortest path constrained to travel along mesh triangle edges between the prescribed start and end vertex. This can fail if the Start and End points are within separate connected components of the mesh.

 |
| 

**Get Shortest Surface Path**

 | 

Computes a polypath that represents the shortest mesh surface path between two prescribed points on the provided mesh.This can fail if the Start and End points are within separate connected components of the mesh.

-   Barycentric coordinates are of the form (a,b,c) where each entry is positive and `a + b + c = 1`.
    
-   If the provided coordinates are invalid, the value (1/3, 1/3, 1/3) is used.
    



 |
| 

**Create Surface Path**

 | 

Computes a polypath that represents a "straight" surface path starting at the prescribed point on the mesh, and continuing in the indicated direction until reaching the requested path length or encountering a mesh boundary, whichever comes first.

-   Barycentric coordinates are of the form (a,b,c) where each entry is positive and `a + b + c = 1`.
    
-   If the provided coordinate is invalid, the value (1/3, 1/3, 1/3) is used.
    
-   Also, if the direction vector is nearly zero, the up-vector is used.
    



 |

## Mesh Pool

Functions to call and release compute mesh pool.

| Node Name | Description |
| --- | --- |
| 
**Get Global Mesh Pool**

 | 

Accesses a global compute mesh pool (created on first access).

 |
| 

**Discard Global Mesh Pool**

 | 

Fully clears or destroys the current global mesh pool, allowing it and all its meshes to be garbage collected.

 |
| 

**Request And Release Compute Mesh**

 | 

Macro to request a compute mesh which can be used via the With Mesh execute pin, and then automatically released before the After Release execute pin.

 |
| 

**Request And Release Compute Mesh From Global Pool**

 | 

Macro to request and release a compute mesh using the global compute mesh pool.

 |

## Simple Polygon

A simple 2D polygon is a closed polygon with no holes. You can use these functions to call and manipulate simple polygons.

| Node | Description |
| --- | --- |
| 
**Get Polygon Vertex Count**

 | 

Returns the number of vertices in a simple polygon.

 |
| 

**Get Polygon Vertex**

 | 

Returns the specified vertex of a simple polygon. Vertex Index loops around, that is, -1 gives the last vertex in the polygon. If the polygon has no vertices, it returns the zero vector.

 |
| 

**Set Polygon Vertex**

 | 

Set the specified vertex of a simple polygon. Vertex Index loops around, that is, -1 gives the last vertex in the polygon. Does nothing if the polygon has no vertices.

 |
| 

**Add Polygon Vertex**

 | 

Set the specified vertex of a simple polygon. Returns the index of the added vertex.

 |
| 

**Get Polygon Tangent**

 | 

Returns a vertex's tangent of a simple polygon. Vertex Index loops around, that is, -1 gives the tangent of the last vertex in the polygon. If the polygon has no vertices, it returns the zero vector.

 |
| 

**Get Polygon Arc Length**

 | 

Returns the arc length of a simple polygon.

 |
| 

**Get Polygon Area**

 | 

Returns the area enclosed by a simple polygon.

 |
| 

**Get Polygon Bounds**

 | 

Returns the bounding box of a simple polygon.

 |
| 

**Convert Spline To Polygon**

 | 

Sample positions from a `USplineComponent`. into a simple polygon, based on the given Sampling Options.

 |
| 

**Simple Polygon To Array Of Vector**

 | 

Returns an array of 3D vectors with the polygon vertex locations, with Z coordinate set to zero.

 |
| 

**Simple Polygon To Array Of Vector2D**

 | 

Returns an array of 2D vectors with the polygon vertex locations.

 |
| 

**Array Of Vector To Simple Polygon**

 | 

Returns a polygon created from an array of 3D position vectors, ignoring the Z coordinate.

 |
| 

**Array Of Vector2D To Simple Polygon**

 | 

Returns a polygon created from an array of 2D position vectors.

 |

## Polygon List

A polygon list includes a list of general polygons, which may have holes. You can use these functions to call and edit polygons in a polygon list.

| Node | Description |
| --- | --- |
| 
**Get Polygon Vertex Count**

 | 

Returns the number of vertices in a polygon's outer shape, if Hole Index is -1, or in the specified inner hole. Returns 0 for invalid polygon or hole indices.

 |
| 

**Get Polygon Vertex**

 | 

Returns the specified vertex of a polygon — either of the outer polygon, if Hole Index is -1, or specified inner hole.Vertex are the zero vector for invalid polygon or hole indices, or if the polygon is empty. Vertex Index will loop.

 |
| 

**Get Polygon Count**

 | 

Returns the number of polygons in the Polygon List.

 |
| 

**Get Polygon Hole Count**

 | 

Returns the number of holes in a polygon. Returns zero for an invalid Polygon Index.

 |
| 

**Get Polygon Vertices**

 | 

Returns the vertices of a polygon — either of the outer polygon, if Hole Index is -1, or specified inner hole. Out Vertices are empty for invalid polygon or hole indices.

 |
| 

**Get Polygon Area**

 | 

Returns the area enclosed by a polygon. Returns zero for an invalid Polygon Index.

 |
| 

**Get Polygon Bounds**

 | 

Returns the bounding box of a polygon. Returns an empty, invalid box for an invalid Polygon Index.

 |
| 

**Get Simple Polygon**

 | 

Returns a specified simple polygon from a polygon list — either the outer polygon, if Hole Index is -1, or specified inner hole. Polygon are empty for invalid polygon or hole indices.

 |
| 

**Get Polygon List Area**

 | 

Returns the area enclosed by a polygon.

 |
| 

**Get Polygon List Bounds**

 | 

Returns the bounding box of a polygon.

 |
| 

**Create Polygon List From Single Polygon**

 | 

Create a polygon list of a single polygon, with optional holes.

 |
| 

**Add Polygon To List**

 | 

Add Polygon to a polygon list, with optional holes. Returns index of the added polygon.

 |
| 

**Create Polygon List From Simple Polygons**

 | 

Create a Polygon List from an array of Simple Polygons.

 |
| 

**Append Polygon List**

 | 

Add the polygons in Polygons to Append to Polygon List.

 |
| 

**Polygons Union**

 | 

Compute union of all polygons in Polygon List. Also resolves self-intersections within each polygon.

 |
| 

**Polygons Difference**

 | 

Compute difference of Polygon List and Polygons to Subtract.

 |
| 

**Polygons Intersection**

 | 

Compute intersection of Polygon List and Polygons to Intersect.

 |
| 

**Polygons Exclusive Or**

 | 

Compute exclusive or of Polygon List and Polygons to Exclusive Or.

 |
| 

**Polygons Offset**

 | 

Apply a single offset to a list of closed polygons.

 |
| 

**Polygons Offsets**

 | 

Apply two offsets in sequence to a list of closed polygons.

 |
| 

**Polygons Morphology Open**

 | 

Apply a morphological open operator to a list of closed polygons — first offsetting by -Offset, then by +Offset. If Offset is negative, this instead functions as a close operation.

 |
| 

**Polygons Morphology Close**

 | 

Apply a morphological close operator to a list of closed polygons — first offsetting by +Offset, then by -Offset. If Offset is negative, this instead functions as an open operation.

 |
| 

**Create Polygons From Path Offset**

 | 

Apply an offset to a single open 2D path, generating closed polygons as a result.

 |

## Poly Path

These functions perform poly path manipulations. A poly path is a path defined by an ordering of vertices.

| Node Name | Description |
| --- | --- |
| 
**Get Poly Path Num Vertices**

 | 

Returns the number of vertices in the poly path.

 |
| 

**Get Poly Path Last Index**

 | 

Returns the index of the last vertex in the poly path.

 |
| 

**Get Poly Path Vertex**

 | 

Returns the 3D location of the specified vertex.

 |
| 

**Get Poly Path Tangent**

 | 

Returns the local tangent vector of the poly path at the specified vertex index.

 |
| 

**Get Poly Path Arc Length**

 | 

Returns the length of the poly path.

 |
| 

**Get Nearest Vertex Index**

 | 

Returns the index of the nearest poly path vertex to the specified point in 3D.

 |
| 

**Flatten To 2D On Axis**

 | 

Creates a 2D flatten copy of the path, by dropping the given axis and using the other two coordinates as the new X, Y coordinates.

 |
| 

**Convert Spline To Poly Path**

 | 

Samples the positions from a [USplineComponent](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Components/USplineComponent?application_version=5.5) into a Poly Path, based on the given Sampling Options.

 |
| 

**Convert Poly Path To Array**

 | 

Populates an array of 3D vectors with the poly path vertex locations.

 |
| 

**Convert Array To Poly Path**

 | 

Creates a poly path from an array of 3D position vectors.

 |
| 

**Convert Poly Path To Array Of Vector 2D**

 | 

Creates an array of 2D Vectors with the poly path vertex locations projected onto the XY plane.

 |
| 

**Convert Array Of Vector 2D To Poly Path**

 | 

Creates a poly path from an array of 2D position vectors. The Z-coordinate of the corresponding Poly Path vertices is zero.

 |
| 

**Create Circle Path 3D**

 | 

Creates a closed circle around the origin on the XY plane, then is repositioned by the Transform input.

 |
| 

**Create Circle Path 2D**

 | 

Creates a closed circle on the XY plane around the given Center.

For closed paths, the end vertex is not a duplicate of the start vertex.



 |
| 

**Create Arc Path 3D**

 | 

Creates an open arc around the origin on the XY plane, then is repositioned by the Transform input.

 |
| 

**Create Arc Path 2D**

 | 

Creates an open arc on the XY plane around the given Center.

 |

## Mesh Comparisons

Functions for comparing two meshes. These nodes do not modify either mesh through their usage.

| Node Name | Description |
| --- | --- |
| 
**Is Same Mesh As**

 | 

Returns true if the two input meshes are equivalent under the comparisons defined by the input options.

 |
| 

**Measure Distances Between Meshes**

 | 

Measures the min/max and average closest-point distances between two meshes.

 |
| 

**Is Intersecting Mesh**

 | 

Returns true if the two input meshes (with optional transforms) are geometrically intersecting.

 |

## BVH & Spatial Queries

These functions create and query a Bounding Volume Hierarchy (BVH) object for a mesh.

| Node Name | Description |
| --- | --- |
| 
**Build BVH For Mesh**

 | 

Builds a BVH object for a mesh that can be used by **Is BVH Valid For Mesh**, **Rebuild BVH for Mesh**, **Find Nearest Point On Mesh**, **Find Nearest Ray Intersection With Mesh**, and **Is Point Inside Mesh** nodes. The function returns a Geometry Script dynamic mesh BVH struct.

 |
| 

**Is BVH Valid For Mesh**

 | 

Checks if the BVH object can still be used with the Mesh — it generally returns false if the mesh has been changed.

 |
| 

**Rebuild BVH For Mesh**

 | 

Rebuilds the BVH object for the mesh in-place, which can reduce memory allocations, compared to building a new BVH.

 |
| 

**Find Nearest Point On Mesh**

 | 

Finds the nearest point on the mesh/BVH to a given 3D point.

 |
| 

**Find Nearest Ray Intersection With Mesh**

 | 

Finds the nearest intersection of a 3D ray with the mesh or BVH.

 |
| 

**Is Point Inside Mesh**

 | 

Tests if a point is inside the mesh/BVH using the Fast Winding Number query.

 |

## Utilities

These helper functions are useful in Geometry Script mesh processing and procedural generators.

| Node Name | Description |
| --- | --- |
| 
**Create Dynamic Mesh Pool**

 | 

Creates a new dynamic mesh pool object.

 |
| 

**Create Unique New Asset Path Name**

 | 

Create a new unique asset name given a base path and base asset name, which is useful with functions such as **Create New Static Mesh Asset From Mesh**.

This node only works in the Editor.



 |
| 

**Get Mesh Info String**

 | 

Returns a debug string that contains mesh statistics and other information.

 |
| 

**Sample Spline To Transforms**

 | 

Sample a [USplineComponent](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/Engine/Components/USplineComponent?application_version=5.5) into a list of [FTransforms](https://docs.unrealengine.com/en-US/API/Runtime/Core/Math/FTransform/), based on the given Sampling Options.

 |

## Glossary

| Term | Definition |
| --- | --- |
| 
**Overlay**

 | 

A data structure representing a type of vertex data applied to a mesh.These types include: vertex color, normal, tangent, and UV.

Multiple values of the specified type can be stored at a single vertex. In such cases, depending on the type, one of the following occurs: the last value is used, the values are averaged, or an arbitrary value is used.

 |
| 

**One-ring**

 | 

The neighboring vertices of the selected vertex, connected by an edge.

[![One-ring Triangles](https://dev.epicgames.com/community/api/documentation/image/9f5ba8db-9284-42db-807d-41cd7f2b2834?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9f5ba8db-9284-42db-807d-41cd7f2b2834?resizing_type=fit)

*The one-ring of vertex M.*

 |
| 

**UV Set**

 | 

Contains the UV coordinates of a mesh, also referred to as the [UV Channel](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine). You can use multiple UV Channels to represent different [UV maps](working-with-content/modeling-and-geometry-scripting/modeling-tools/uvs-category#UVMap).

 |
| 

**Extents**

 | 

The half-dimensions of a box, measured along the three axes. They are used to determine how much to extend from a center point.

A center point, C, and Extent, E, results in a box with a bottom-left-near corner at `C - E` and a top-right-far corner at `C + E`.

 |

**h PolyGroup Boundary Edges**