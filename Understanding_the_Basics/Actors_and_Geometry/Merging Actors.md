# Merging Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/merging-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/merging-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:42

---

In **Unreal Engine**, you can combine two or more **Static Mesh Actors** into a single new Actor using **Actor merging**. This reduces draw calls and helps with project optimization.

## Actor Merging Workflow

To merge two or more Static Mesh Actors inside your Level, follow these steps:

1.  In the **Level Viewport** or **World Outliner**, select the Static Mesh Actors you want to merge.
    
2.  From the top menu bar, go to **Actor > Merge Actors.**
    
3.  Select the type of merge you want to perform: **Merge**, **Simplify**, **Batch**, or **Approximate**. Refer to the Merge Types section on this page for more information.
    
    The option you select will perform the merge automatically using the default or last configured settings. To configure merge options, from the top menu bar, go to **Actor > Merge Actors > Merge Actor Settings.**
    
4.  Name your new Actor and select the folder where it should be created, then click **Save**.
    

## Merge Types

Unreal Engine offers different methods to merge Static Mesh Actors, depending on what you are merging:

1.  Merge
    
2.  Simplify
    
3.  Batch
    
4.  Approximate
    

These options are described below.

### Merge

By default, this method merges all selected Static Mesh Actors, creating one mesh section for each Material. You can specify **LOD** levels to use.

The number of draw calls is equivalent to the number of **Materials**. This method preserves UVs.

You can also select to merge all Materials, which bakes a single Material for the entire mesh. This results in a single section and a single draw call, but **does not** preserve UVs. Occlusion culling is performed per section.

### Simplify

This method merges all selected Static Mesh Actors into a single mesh, called a **Proxy Mesh**. It uses the lowest-detail LOD of each selected mesh and simplifies mesh geometry based on the settings provided. Vertex count is also reduced.

This method results in one draw call. It bakes one Material for the entire mesh and **does not** preserve UVs. Occlusion culling is performed for the whole mesh.

Refer to the [Proxy Geometry Overview](/documentation/en-us/unreal-engine/proxy-geometry-tool-overview-in-unreal-engine) page for additional information.

### Batch

This method creates instanced Static Mesh components from identical Static Mesh components. It preserves UVs and does not affect occlusion culling.

### Approximate

This method is new to **Unreal Engine 5** and is similar to the Simplify merge method. The difference is that it can handle much more complex source meshes (for example, Nanite meshes), whereas the Simplify method would fail during either the simplification or the texture baking steps.

## Merge Settings

You can configure individual merge settings from the **Merge Actor Settings** panel. To access this panel, from the top menu bar, go to **Actor > Merge Actors > Merge Actor Settings**.

### Merge

When using this merge method, you can configure the options below.

#### Mesh Settings

The **Mesh Settings** section contains properties that affect the Static Meshes that will be merged.

| **Option** | **Description** |
| --- | --- |
| **Pivot Point at Zero** | 
If enabled, the pivot point of the merged Actor will be set to the Level's origin (0,0,0).

If disabled, the point of the merged Actor will be the pivot point of the first Static Mesh Actor selected for the merge.



 |
| **Merge Physics Data** | Merges all of the collision primitives into a single physics object. |
| **Bake Vertex Data to Mesh** | Bakes vertex data, including vertex color and normals, into the merged Static Mesh Actor. |
| **Output UVs** | An array that contains multiple UV channels. If the source meshes contain valid UVs for a specified channel, you can select whether or not to output the UV channel into the merged Static Mesh Actor. |
| **LOD Selection Type** | 

Control which LODs are added to the merged object. You can select one of the following options:

-   **Use all LOD levels**: Uses all available LOD levels.
-   **Use specific LOD level**: Use only the selected LOD level.
-   **Calculate correct LOD level**: Calculates the optimum LOD level for the given screen size.
-   **Always use the lowest-detail LOD (the highest LOD index)**: Uses the lowest-detail LOD available.



 |
| **Include Imposters** | If enabled, the merge will include imposter LODs that are part of the source Static Meshes. |
| **Allow Distance Field** | If enabled, a distance field will be computed for this Mesh. Disable this option to save memory if the merged mesh will only be rendered in the distance. |
| **Generate Lightmap UVs** | Creates a new lightmap UV layout for the merged Static Mesh Actor, using the existing UV islands. This new layout will be placed in the target lightmap UVChannel. |
| **Generate Nanite Enabled Mesh** | If enabled, generates a Nanite-enabled mesh. |
| **Target Light Map Resolution** | Specifies the resolution for the new lightmap UVs, which controls the distance calculated between each island within the layout. Higher resolutions will yield tighter spacing between each island. |
| **Computed Light Map Resolution** | If enabled, lightmap resolution will be computed by summing up the Lightmap resolutions for the source Static Meshes. |

#### Material Settings

The **Material Settings** section contains properties that affect the textures and Materials of the Static Meshes to be merged.

You can't merge Materials for multiple Static Meshes if the **LODSelection Type** option in the **Mesh Settings** section is set to **Use all LOD levels**.

| **Option** | **Description** |
| --- | --- |
| **Merge Materials** | 
If enabled, the Materials of all the merged assets will be combined into a single Material with a new UV layout.

The following subsettings only become available if Merge Materials is enabled.



 |
| **Texture Size** | Sets the horizontal (X) and vertical (Y) pixel dimensions, or resolution, for the final merged Material's textures. |
| **Texture Sizing Type** |   |
| **Normal Map** | If enabled, generates a Normal map for the merged Actor. |
| **Tangent Map** | If enabled, generates a Tangent map for the merged Actor. |
| **Metallic Map** | If enabled, generates a Metallic map for the merged Actor. While this option is enabled, the **Metallic Constant** property has no effect. |
| **Metallic Constant** | Sets a constant value for the Metallic property of the merged Actor's Material. Only enabled if the **Metallic Map** option is unchecked. |
| **Roughness Map** | If enabled, generates a Roughness map for the merged Actor. While this option is enabled, the **Roughness Constant** property has no effect. |
| **Roughness Constant** | Sets a constant value for the Roughness property of the merged Actor's Material. Only enabled if the **Roughness Map** option is unchecked. |
| **Anisotropy Map** | If enabled, generates an Anisotropic map for the merged Actor. Anisotropy is a Material's property to change its appearance depending on the direction it is viewed from. While this option is enabled, the **Anisotropy Constant** property has no effect. |
| **Anisotropy Constant** | Sets a constant value for the Anisotropy property of the merged Actor's Material. Only enabled if the **Anisotropy Map** option is unchecked. |
| **Specular Map** | If enabled, generates a Specular map for the merged Actor. While this option is enabled, the **Specular Constant** property has no effect. |
| **Specular Constant** | Sets a constant value for the Specular property of the merged Actor's Material. Only enabled if the **Specular Map** option is unchecked. |
| **Emissive Map** | If enabled, generates an Emissive map for the merged Actor. |
| **Opacity Map** | 

If enabled, generates an Opacity map for the merged Actor. While this option is enabled, the **Opacity Constant** property has no effect.

You must also set the **Blend Mode** to **Translucent** for opacity to work correctly in the generated instances.



 |
| **Opacity Constant** | Sets a constant value for the Opacity property of the merged Actor's Material. Only enabled if the **Opacity Map** option is unchecked. |
| **Opacity Mask Map** | 

If enabled, generates an Opacity Mask map for the merged Actor. While this option is enabled, the **Opacity Mask Constant** property has no effect.

You must also set the **Blend Mode** to **Masked** for opacity to work correctly in the generated instances.



 |
| **Opacity Mask Constant** | Sets a constant value for the Opacity Mask property of the merged Actor's Material. Only enabled if the **Opacity Mask Map** option is unchecked. |
| **Ambient Occlusion Map** | If enabled, generates an Ambient Occlusion map for the merged Actor. While this option is enabled, the **Ambient Occlusion Constant** property has no effect. |
| **Ambient Occlusion Constant** | Sets a constant value for the Ambient Occlusion property of the merged Actor's Material. Only enabled if the **Ambient Occlusion Map** option is unchecked. |
| **Tangent Texture Size** | Sets the horizontal (X) and vertical (Y) pixel dimensions, or resolution, for the merged Actor's Tangent texture. Enabled when **Texture Sizing Type** is set to **Use per property manually overridden texture sizes**. |
| **Anisotropy Texture Size** | Sets the horizontal (X) and vertical (Y) pixel dimensions, or resolution, for the merged Actor's Anisotropy texture. Enabled when **Texture Sizing Type** is set to **Use per property manually overridden texture sizes**. |
| **Blend Mode** | 

Sets how the Material's color is blended with background colors. You can choose from the following options:

-   **Opaque**: Defines a surface through which the light neither passes nor penetrates.
-   **Masked**: Defines whether the merged Material will use masking (that is, have different areas be visible or not based on a masking texture).
-   **Translucent**: Defines the visibility of a Material by using an Opacity value.
-   **Additive**: Takes the pixels of the Material and adds them to the pixels of the Background.
-   **Modulate**: Multiplies the value of the Material against the pixels of the background.
-   **AlphaComposite (Premultiplied Alpha)**: Used with textures that already have a pre-multiplied alpha.
-   **AlphaHoldout**: Creates a cutout effect by holding out the alpha in the Material and punching a hole through objects behind it.



 |
| **Allow Two Sided Material** | If enabled, the generated Material will be two-sided. |
| **Gutter Size** | Sets the space, in pixels, between UV islands at the original texture resolution for the baked material. The space helps prevent the colors of your islands from overlapping. Otherwise, artifacts can appear on the mesh as downsampling of the texture occurs at render. The reduced texture sizes are known as mipmaps. |
| **Create Merged Material** | If enabled, creates a flat Material from all Materials of the Actors to be merged, along with a new set of UVs. By default, this Material will not be applied to any section. |
| **Use Vertex Data for Baking Material** | If enabled, uses vertex data such as vertex color to bake Material results. This is useful if you have a Material that is being controlled in some way by vertex color. |
| **Use Texture Binning** | Calculate the varying output texture sizes according to their importance when packing the final atlas texture. |
| **Reuse Mesh Lightmap UVs** | If enabled, attempts to reuse the lightmap UVs of the source Static Meshes when baking the Material. If disabled, generates a new set of lightmap UVs. |
| **Merge Equivalent Materials** | 

If enabled, attempts to merge Materials that are deemed equivalent.

Enabling this option can cause artifacts in the merged Static Mesh if output color is determined by world position or Actor position.



 |

#### Landscape Culling

If the **Landscape Culling** option is enabled, Unreal Engine will use existing landscape geometry to cull fully occluded triangles when merging Actors.

For example, if you have a tree mesh that was planted such that the bottommost triangles are well below the surface of a landscape, then those occluded triangles will be removed after the merge.

### Simplify

When using the **Simplify** merge method, you can configure the options below.

#### Proxy Settings

| **Option** | **Description** |
| --- | --- |
| **Screen Size** | The screen size of the merged Static Mesh, in pixels. |
| **Calculate Correct LODModel** | If enabled, calculates the correct LOD models based on source meshes and transition size. |
| **Override Spatial Sampling Distance** | 
Overrides the spatial sampling distance when converting multiple Static Meshes for proxy LOD merging.

Large geometry with high sampling can have very high memory costs.



 |
| **Material Settings** | 

You can configure the same Material settings described in the Merge section on this page.



 |
| **Merge Distance** | Sets the distance at which meshes are merged together. For example, this can fill in gaps like doors and windows in distant geometry. |
| **Unresolved Geometry Color** | Sets the color to be assigned to LOD geometry that can't be associated with the source geometry (for example, doors and windows that were further than the Merge Distance and were filled in). You can set red, green, and blue (RGB) values, as well as an alpha (A) value that controls transparency. |
| **Transfer Distance Override** | Overrides the search distance at which Unreal Engine discovers texture values for simplified geometry. This is useful if you set a manual value greater than zero for the Merge Distance option, which generates new geometry in concave corners. |
| **Hard Edge Angle** | 

Sets the angle at which a hard edge is introduced between the faces of the merged Static Mesh.

This option increases vertex count and might introduce additional UV seams. It is only recommended if you are not using Normal maps.



 |
| **Normal Calculation Method** | 

Select the method used to control Normal calculation for the simplified geometry. You can choose from the following options:

-   **Angle Weighted**: Use the angle of a triangle at a vertex to weight how much that triangle's normal contributes to that vertex's Normal.
-   **Area Weighted**: Use triangle area to weight how much a triangle's Normal contributes its vertices' Normals.
-   **Equal Weighted**: Average the Normal of each triangle sharing a vertex.

For more information about Normal calculation, refer to the [Normal Calculation Method](/documentation/en-us/unreal-engine/normal-calculation-methods-with-the-proxy-geometry-tool-in-unreal-engine) page.



 |
| **Light Map Resolution** | Sets the lightmap resolution. |
| **Compute Light Map Resolution** | If enabled, computes lightmap resolution as a sum of the dimensions for each mesh included for merging. |
| **Enable Volume Culling** | If enabled, culling volumes can exclude geometry. |
| **Allow Adjacency** | If enabled, allows adjacency buffers for tessellation in the merged Static Mesh. |
| **Allow Distance Field** | If enabled, a distance field will be computed for this mesh. Disable this option to save memory if this mesh will only be rendered in the distance. |
| **Reuse Mesh Lightmap UVs** | If enabled, attempts to reuse the lightmap UVs of the source Static Meshes when baking the Material. If disabled, generates a new set of lightmap UVs. |
| **Group Identical Meshes for Baking** | 

If enabled, bakes identical meshes or mesh instances only once. This results in better quality baked textures and greatly reduces baking time.

This can lead to discrepancies with the source mesh visual, especially for materials that are using world position or per instance data.



 |
| **Create Collision** | If enabled, generates collision for the merged Static Mesh. |
| **Allow Vertex Colors** | If enabled, vertex colors will be saved in the merged Static Mesh. |
| **Generate Lightmap UVs** | Creates a new lightmap UV layout for the merged Static Mesh Actor, using the existing UV islands. This new layout will be placed in the target lightmap UVChannel. |
| **Generate Nanite Enabled Mesh** | If enabled, generates a Nanite-enabled mesh. |

### Batch

When using the **Batch** merge method, you can configure the options below.

| **Option** | **Description** |
| --- | --- |
| **Actor Class to Use** | Select the class to use for the instanced Static Meshes. |
| **Instance Replacement Threshold** | Sets the minimum number of Static Mesh instances needed before a Static Mesh is replaced with an instanced version. |
| **Skip Meshes with Vertex Colors** | If enabled, Static Meshes that use vertex colors will not be instanced. This prevents data loss because instanced Static Meshes do not support vertex colors per instance. |
| **Use HLOD Volumes** | If enabled, instanced Static Meshes will be split up based on their intersection with HLOD volumes. |
| **Select the type of Instanced Component** | Select the type of instanced component to use for the instanced Static Meshes. |

### Approximate

When using the **Approximate** merge method, you can configure the options below.

#### Mesh Generation Settings

| **Shape Settings** | **Description** |
| --- | --- |
| **Output Type** | 
The type of output from the mesh approximation process.

-   **Mesh and Materials**: Generates both the mesh and its material.
-   **Mesh Shape Only**: Skips the material baking step and only generates the mesh.



 |
| **Approximation Accuracy** | The approximation accuracy in meters, which will determine (for example) voxel resolution. |
| **Attempt Auto Thickening** | If enabled, attempts to auto-thicken thin parts or flat sheets. |
| **Target Min Thickness Multiplier** | A multiplier on Approximation Accuracy used for auto-thickening. |
| **Ignore Tiny Parts** | If enabled, tiny parts will be excluded from the mesh merging, which can improve performance. |
| **Tiny Part Size Multiplier** | A multiplier on Approximation Accuracy used to define tiny-part threshold, using maximum bounding-box dimension |
| **Base Capping** | 

Optionally close off the bottom of open meshes. Possible options are:

-   **No Base Capping**
-   **Convex Polygon**: Adds a downwards-facing polygon at the base of the mesh.
-   **Convex Solid**: Adds a downwards-facing polygon at the base of the mesh and thickens it into a closed solid.

These options can have very different effects on the resulting mesh depending on whether or not the other input objects are closed meshes, as well as the 'winding' threshold. For example, a large mountain scan that is uncapped should use the polygon and not the solid, but if it's many kitbashed mesh parts, the open mesh can introduce significant problems and using the solid may be more reliable.



 |
| **Fill Gaps** | If enabled, topology is expanded / contracted to fill small gaps between objects. |
| **Gap Filling Distance** | The distance in meters to expand / contract to fill gaps. |
| **Clamp Voxel Dimension** | The maximum allowable voxel count along main directions. This is a limit on **Approximation Accuracy**. |
| **Winding Threshold** | The Winding Threshold controls hole filling at open mesh borders. Smaller value means more or rounder filling. |

#### Output Mesh Filtering and Simplification Settings

| **Option** | **Description** |
| --- | --- |
| **Occlusion Method** | 
The type of hidden geometry removal to apply:

-   **No Occlusion Filtering**
-   **Visibility Based Filtering**



 |
| **Occlude from Bottom** | If enabled, then the `OcclusionMethod` computation is configured to try to consider downward-facing "bottom" geometry as occluded. |
| **Simplify Method** | 

Mesh Simplification criteria:

-   **Geometric Tolerance**: Constrain simplification to a maximum geometric deviation from the input meshes. The maximum is provided by the **Geometric Deviation** option below.
-   **Fixed Triangle Count**: Simplification will aim to reach a target count of triangles, provided by the **Target Tri Count** option below.
-   **Triangles Per Area**: Simplification will aim for a number of triangles per square meter, provided by the **Triangles per M** option below.



 |
| **Geometric Deviation** | The allowable geometric deviation, in meters, used when the Simplify Method is set to Geometric Tolerance. |
| **Target Tri Count** | The target triangle count for mesh simplification, used when the Simplify Method is set to Fixed Triangle Count. |
| **Triangles Per M** | The approximate number of triangles per square meter, used when the Simplify Method is set to Triangles Per Area. |
| **Ground Clipping** | 

Configures how the final mesh should be clipped with a ground plane, if desired. The options are:

-   **No Ground Clipping**: Does not perform ground clipping.
-   **Discard With ZPlane**: Discards triangles whose vertices are all below the clip plane.
-   **Cut With ZPlane**: Performs a mesh cut to eliminate the portion of the mesh that is below the clip plane.
-   **Cut And Fill With ZPlane**: Same as the Cut With ZPlane option above, and also closes the cut mesh by inserting new triangles where the cut was performed.

For all of these options, the height (Z) of the clip plane is provided by the **Ground Clipping ZHeight** option.



 |
| **Ground Clipping ZHeight** | The Z-Height for the ground clipping plane, if **Ground Clipping** is enabled. |

#### Mesh Normals and Tangents Settings

| **Normals Settings** | **Description** |
| --- | --- |
| **Estimate Hard Normals** | If enabled, Normal angle will be used to estimate hard Normals |
| **Hard Normal Angle** | The Normal angle to use to detect hard Normals. |

#### Mesh UV Generation Settings

| **UV Settings** | **Description** |
| --- | --- |
| **UV Generation Method** | 
The Mesh UV Generation method:

-   **Prefer UVAtlas**: Uses Microsoft's open-source [UVAtlas](https://github.com/microsoft/UVAtlas) library.
-   **Prefer XAtlas**: Uses the [XAtlas](https://github.com/jpcy/xatlas) open-source mesh parametrization / UV unwrapping library.
-   **Prefer PatchBuilder**: Uses Unreal Engine's own UV generation algorithm.



 |
| **Initial Patch Count** | The number of initial patches the mesh will be split into before computing island merging. Only relevant for the PatchBuilder UV generation method. |
| **Curvature Alignment** | Controls the alignment of the initial patches to creases in the mesh. Only relevant for the PatchBuilder UV generation method. |
| **Merging Threshold** | The distortion / stretching threshold for island merging. Larger values increase the allowable UV stretching. Only relevant for the PatchBuilder UV generation method. |
| **Max Angle Deviation** | UV islands will not be merged if their average face Normals deviate by more than this value. Only relevant for the PatchBuilder UV generation method. |

#### Output Static Mesh Settings

| **Mesh Settings** | **Description** |
| --- | --- |
| **Generate Nanite Enabled Mesh** | Whether to generate a Nanite-enabled mesh. |
| **Support Ray Tracing** | Whether ray tracing will be supported on this mesh. Disable this to save memory if the generated mesh will only be rendered in the distance. |
| **Allow Distance Field** | Whether to allow a distance field to be computed for this mesh. Disable this to save memory if the generated mesh will only be rendered in the distance. |
| **Nanite Proxy Triangle Percent** | The percentage of triangles to reduce down to when generating a coarse proxy mesh from the Nanite mesh. |

#### Material Baking Settings

| **Material Settings** | **Description** |
| --- | --- |
| **Multi Sampling AA** | If this property is greater than 1, multisample output baked textures by this amount in each direction (for example, 4 == 16x supersampling). |
| **Render Capture Resolution** | If this property is zero, use the Material Settings resolution, otherwise override the render capture resolution. |
| **Material Settings** | 
You can configure the same Material settings described in the Merge section on this page.



 |
| **Capture Field Of View** | The field of view angle to use when performing the render capture. |
| **Near Plane Dist** | The near plane distance to use when performing the render capture. |

#### Debug Output Settings

| **Debug Settings** | **Description** |
| --- | --- |
| **Print Debug Messages** | If enabled, print out debugging messages. |
| **Emit Full Debug Mesh** | 
If enabled, write the full mesh triangle set (flattened, non-instanced) used for mesh generation.

This asset may be extremely large.



 |

### Replace Source Actors

If the **Replace Source Actors** option is enabled, the Actors selected in the viewport will be removed and replaced with the new merged Actor. This will not delete their Assets from the Content Browser or from your project folders.

This option is common to all of the merge methods described on this page.