# Interchange Import Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/interchange-import-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/interchange-import-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:29

---

The **Interchange Pipeline Configuration** window opens when you import a file of a supported file type into Unreal Engine.

The Interchange Pipeline Configuration window

The options displayed in the window are dependent on two factors:

-   The file format of the imported file.
-   The Interchange Pipeline Stack you selected to process the import.

For more information on the import process using Interchange, see [Importing Assets Using Interchange](/documentation/en-us/unreal-engine/importing-assets-using-interchange-in-unreal-engine).

## Common

| **Option** | **Description** |
| --- | --- |
| **Use Source Name for Asset** | 
Names the imported asset similar to the source name when it meets the following criteria:

-   This option is set to true.
-   The **Asset Name** field is blank.
-   Only one source.
-   Only one asset.



 |
| **Asset Name** | 

Names the imported asset using this string when you meet the following criteria:

-   Only one source.
-   Only one asset.



 |
| **Offset Translation** | Applies a translation offset to meshes and animations in the specified X, Y, and Z directions. |
| **Offset Rotation** | Applies a rotation offset to meshes and animations in the specified X (Roll), Y (Pitch), and Z (Yaw) directions. |
| **Offset Uniform Scale** | Applies a uniform scale offset to meshes and animations. |

## Common Meshes

| **Option** | **Description** |
| --- | --- |
| **Force All Mesh as Type** | 
Converts the imported meshes to the specified type.

The dropdown menu contains the following options:

-   **None** (default)
-   [Static Mesh](/documentation/en-us/unreal-engine/static-meshes)
-   [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)



 |
| **Import Lods** | Imports any LODs with imported meshes found in the source. Requires you to set the **Bake Meshes** option to true in the selected pipeline. This option is true and hidden by default. |
| **Vertex Color Import Option** | 

Specifies how vertex colors are handled on import.

The dropdown menu contains the following options:

-   **Replace**: Uses the vertex colors from the imported source.
-   **Ignore**: Ignores any vertex colors from the imported source. If reimporting, keeps existing mesh vertex colors.
-   **Override**: Overrides all vertex colors with the specified color.



 |
| **Vertex Override Color** | Defines the vertex color used when the **Vertex Color Import Option** is set to **Override**. |
| **Build** | 

Defines how normals, tangents, and UVs are handled during the import process.

This menu contains the following options:

-   **Recompute Normals**: Ignores and recomputes normals for an imported mesh.
-   **Recompute Tangents**: Ignores and recomputes tangents for an imported mesh.
-   **Use MikkTSpace**: Recomputes tangents using the MikkTSpace standard.
-   **Compute Weighted Normals**: Uses the ratio between the surface area and the corner angle of triangles to compute normals.
-   **Use High Precision Tangent Basis**: Stores tangents with 16 bit precision or 8 bit precision.
-   **Use Full Precision UVs**: Stores UVs with floating point precision.
-   **Use Backwards Compatible F16Trunc UVs**: Forces use of backwards-compatible F16 conversion with truncation for legacy meshes.
-   **Remove Degenerates**: Removes degenerate triangles from imported meshes.



 |

## Common Skeletal Meshes and Animation

| **Option** | **Description** |
| --- | --- |
| **Import Only Animations** | Imports only animations. Requires a valid defined skeleton. |
| **Skeleton** | Defines the skeleton to use for imported animations. Leaving this empty creates a new skeleton. Required for **Import Only Animations**. |
| **Import Meshes in Bone Hierarchy** | Imports meshes nested in bone hierarchies, instead of converting them to bones. |
| **Use T0As Ref Pose** | Uses frame 0 of the imported animation as the reference pose. |

## Static Meshes

| **Option** | **Description** |
| --- | --- |
| **Convert Statics with Morph Targets to Skeletals** | Converts static meshes using morph targets to skeletal meshes. |
| **Import Static Meshes** | Imports static mesh assets found in the source. |
| **Combine Static Meshes** | Combines imported static meshes into a single static mesh. |
| **Lod Groups** | 
Defines which [LOD Group](/documentation/en-us/unreal-engine/creating-and-using-lods-in-unreal-engine) imported static meshes are assigned to.

The dropdown menu contains the following options:

-   **Deco**
-   **Foliage**
-   **High Detail**
-   **Large Prop**
-   **Level Architecture**
-   **None**
-   **Small Prop**
-   **Vista**



 |
| **Collision** | 

Defines how custom collision meshes are handled during import.

This menu contains the following options:

-   **Import Collision**: Imports custom collision. If no custom collision is present, one will be created.
-   **Import Collision According to Mesh Name**: Imports meshes with specific prefixes as collision meshes. Supports the following prefixes:
    -   **UBX\_**: Box Collision
    -   **UCP\_**: Capsule Collision
    -   **USP\_**: Sphere Collision
    -   **UCX\_**: Convex Collision
-   **One Convex Hull Per UCX**: Imports convex collision as a single hull. If false, Unreal Engine breaks down the collision and creates a hull for each piece.



 |
| **Build** | 

Defines how [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine), lightmaps, and [distance fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) are handled during the import process.

This menu contains the following options:

-   **Build Nanite**: Toggles [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) rendering at runtime for imported meshes.
-   **Build Reverse Index Buffer**: Builds a reverse index buffer for imported static meshes.
-   **Generate Lightmap UVs**: Generates lightmap UVS for imported static meshes.
-   **Two-Sided Distance Field Generation**: Generates the distance field while treating every triangle as a front face. This prevents the distance field from being discarded due to the mesh being open, but lowers distance field ambient occlusion quality.
-   **Enable Physical Material Mask**: Toggles a physical material mask for imported meshes.
-   **Min Lightmap Resolution**: Defines the default texture resolution for the baked light and shadow texture generated by Lightmass. For more information, see [Understanding Lightmapping in Unreal Engine](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine).
-   **Source Lightmap Index**: Defines the source UV channel to use when generating lightmaps.
-   **Destination Lightmap Index**: Defines the UV channel index where the newly generated lightmap is stored.
-   **Build Scale**: Defines the local scale applied when building the imported meshes.
-   **Distance Field Resolution Scale**: Defines the scale value applied to [distance fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) volume textures for imported meshes. The default value is 1.0 and assumes the mesh has not been scaled in the world.
-   **Distance Field Replacement Mesh**: Defines the static mesh to use when calculating ambient occlusion and shadowing using [distance fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine). When undefined, LOD 0 of the imported mesh is used.
-   **Max Lumen Mesh Cards**: Defines the max number of Lumen mesh cards generated for that mesh.



 |

## Skeletal Meshes

| **Option** | **Description** |
| --- | --- |
| **Import Skeletal Meshes** | Imports skeletal mesh assets found in the source. |
| **Import Content Type** | 
Defines whether the import process of skeletal mesh assets is partial or total.

The dropdown menu contains the following options:

-   **Geometry and Skinning Weights**: Imports all skeletal mesh content.
-   **Geometry Only**: Imports only the skeletal mesh geometry.
-   **Skinning Weights Only**: Imports only the skeletal mesh skin weights.



 |
| **Combine Skeletal Meshes** | Combines imported skeletal meshes into a single skeletal mesh. This still creates a separate skeletal mesh for each skeletal root joint. |
| **Import Morph Targets** | Imports the morph targets found in the source. |
| **Update Skeleton Reference Pose** | Updates the skeleton's reference pose on import. |
| **Create Physics Asset** | Creates a new physics asset if the source does not have one. |
| **Physics Asset** | Defines the physics asset used if **Create Physics Asset** is false. |
| **Build** | 

Defines how skin weights, animation thresholds, and morph targets are handled during the import process.

This menu contains the following options:

-   **Use High Precision Skin Weights**: Uses 16 bit precision for skin weights instead of 8 bit.
-   **Threshold Position**: Defines the distance threshold to use when determining if two vertex positions are equal.
-   **Threshold Tangent Normal**: Defines the distance threshold to use when determining if two normals, tangents, or binormals are equal.
-   **Threshold UV**: Defines the distance threshold to use when determining if two UVs are equal.
-   **Morph Threshold Position**: Defines the distance threshold to use when determining vertex position equality when computing morph target changes.
-   **Bone Influence Limit**: Defines the maximum number of bone influences each vertex in the imported mesh can use. If set higher than the value in the Project Settings, this has no effect. If set to 0, the import uses the value of **Default Bone Influence Limit** set in the Project Settings.



 |

## Animations

| **Option** | **Description** |
| --- | --- |
| **Import Animations** | Imports any animations found in the source. |
| **Import Bone Tracks** | Imports any bone transform tracks found in the source. |
| **Animation Length** | 
Defines which animation time range to import.

The dropdown menu contains the following options:

-   **Source Timeline**: Imports the range of frames based on the timeline definitions found in the source.
-   **Animation Time**: Imports the range of frames that contain animation.
-   **Set Range**: Imports the range of frames defined by the **Frame Import Range**.



 |
| **Frame Import Range** | Defines the frame range to use when you select **Set Range** for **Animation Length**. |
| **Use 30Hz to Bake Bone Animation** | Samples all animation curves at 30 frames per second. |
| **Custom Bone Animation Sample Rate** | Samples all [FBX animation data](/documentation/en-us/unreal-engine/fbx-animation-pipeline-in-unreal-engine) in the source at the specified rate. If set to 0, automatically finds the best rate. |
| **Snap to Closest Frame Boundary** | Snaps the animation to the closest frame boundary using the specified **Animation Sample Rate**. |
| **Import Attributes as Curves or Animation Attribute** | Imports node attributes as either animation curves or animation attributes. |
| **Add Curve Metadata to Skeleton** | Adds curve metadata to an animation's skeleton automatically. If false, curve metadata is added to the skeleton for morph targets, but no metadata is created for general animation curves. |
| **Set Material Curve Type** | Sets the material curve type for all custom attributes that exist. |
| **Material Curve Suffixes** | Sets the material curve type for custom attributes with suffixes defined in this array. Not applicable if **Set Material Curve Type** is true. |
| **Remove Redundant Keys** | Removes redundant keys from custom animation attributes when importing them as curves. |
| **Do not import curves with only 0 values** | Skips importing animation curves or morph target curves with a value of 0. |
| **Delete existing Animation Attributes** | Deletes previous attributes imported as animation attributes on reimport. |
| **Delete Existing Animation Curves** | Deletes previous attributes imported as animation curves on reimport. |
| **Delete Existing Morph Target Curves** | Deletes previous morph target curves on reimport. |

## Materials

| **Option** | **Description** |
| --- | --- |
| **Import Materials** | Imports any material assets found in the source. |
| **Material Import** | 
Defines what is created when a material asset is imported.

The dropdown menu contains the following options:

-   **Import as Material**: Imports material assets from the source as separate materials.
-   **Import as Material Instance**: Imports material assets from the source as material instances.



 |
| **Parent Material** | 

Defines the parent material to use when importing materials as a material instance. If you select None, one will automatically be chosen during the import process.

Unreal Engine chooses from the following shader models:

-   **Lambert and Phong**: `PhongSurfaceMaterial`
-   **Unlit**: `UnlitMaterial`
-   **Metallic/Roughness PBR**:
    -   `ClearCoatMaterial_MR`
    -   `PBRSurfaceMaterial_MR`
    -   `SheenMaterial_MR`
    -   `ThinTranslucentMaterial_MR`
-   **Specular/Glossiness PBR**:
    -   `PBRSurfaceMaterial_SG`
    -   `ClearCoatMaterial_SG`
    -   `SheenMaterial_SG`
    -   `SubsurfaceMaterial_SG`
    -   `ThinTranslucentMaterial_SG`

These Materials are found in the `/Interchange/Materials` folder.



 |

## Textures

| **Option** | **Description** |
| --- | --- |
| **Import Textures** | Imports any texture assets found in the source. |
| **Detect Normal Map Texture** | Checks to see if the imported texture is a normal map.If it is, the **SRG**, **Compression Settings** and **LOD Group** settings are adjusted automatically. |
| **Flip Normal Map Green Channel** | Inverts the green channel on imported normal maps. |
| **Import UDIMs** | Detects if a texture uses UDIM patterns and imports it as a UDIM as needed. |
| **File Extensions to Import as Long Lat Cubemap** | Defines which file types need to be imported as Long Lat cubemaps. |
| **Advanced** | 
Defines how compression and texture size are handled during the import process.

This menu contains the following options:

-   **Prefer Compressed Source Data**: Tells the translator to provide compressed source data when possible.This results in smaller asset file sizes but some operations might be slower.
-   **Allow Non Power of Two**: Defines whether textures with a non-power of two resolution are imported.



 |

## Importing Using Import Into Level

Assets can also be imported using the **File > Import Into Level** option.

The Interchange Import Into Level window

Import Into Level works with the following file formats:

-   [FBX](/documentation/en-us/unreal-engine/fbx-content-pipeline)
-   [glTF](/documentation/en-us/unreal-engine/the-gl-transmission-format-gltf-in-unreal-engine)
-   **GLB**
-   **MaterialX**

Some options are unavailable when importing using this method. The following options are available:

### Common

-   Offset Translation
-   Offset Rotation
-   Offset Uniform Scale

### Common Meshes

-   Import Lods
-   Vertex Color Import Option
-   Vertex Color Override
-   Build
    -   Recompute Tangents
    -   Use MikkTSpace
    -   Compute Weighted Normals
    -   Use High Precision Tangent Basis
    -   Use Full Precision UVs
    -   Use Backwards Compatible F16Trunc UVs
    -   Remove Degenerates

### Common Skeletal Meshes and Animation

-   Import Meshes in Bone Hierarchy
-   Use T0As Ref Pose

### Static Meshes

-   Convert Static Meshes with Morph Targets to Skeletals
-   Import Static Meshes
-   Lod Group
-   Collision
    -   Import Collision
    -   Import Collision According to Mesh Name
    -   One Convex Hull Per UCX
-   Build
    -   Build Nanite
    -   Build Reverse Index Buffer
    -   Generate Lightmap UVs
    -   Two-Sided Distance Field Generation
    -   Enable Physical Material Mask
    -   Min Lightmap Resolution
    -   Source Lightmap Index
    -   Destination Lightmap Index
    -   Build Scale
    -   Distance Field Resolution Scale
    -   Distance Field Replacement Mesh
    -   Max Lumen Mesh Cards

### Skeletal Meshes

-   Import Skeletal Meshes
-   Import Content Type
-   Import Morph Targets
-   Update Skeleton Reference Pose
-   Create Physics Asset
-   Build
    -   Use High Precision Skin Weights
    -   Threshold Position
    -   Threshold Tangent Normal
    -   Threshold UV
    -   Morph Threshold Position
    -   Bone Influence Limit

### Animations

-   Import Animations
-   Import Bone Tracks
-   Animation Length
-   Frame Import Range
-   Use 30Hz to Bake Bone Animation
-   Custom Bone Animation Sample Rate
-   Snap to Closest Frame Boundary
-   Import Attributes as Curves or Animation Attributes
-   Add Curve Metadata to Skeleton
-   Set Material Curve Type
-   Material Curve Suffixes
-   Remove Redundant
-   Do not import curves with only 0 values
-   Delete Existing Animation Attributes
-   Delete Existing Animation Curves
-   Delete Existing Morph Target Curves

### Materials

-   Parent Material

### Textures

-   Import Textures
-   Detect Normal Map Texture
-   Flip Normal Map Green Channel
-   Import UDIMs
-   File Extensions to Import as Long Lat Cubemap
-   Advance
    -   Prefer Compressed Source Data
    -   Allow Non Power of Two