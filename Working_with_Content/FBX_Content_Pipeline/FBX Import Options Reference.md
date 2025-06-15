# FBX Import Options Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:23

---

While importing FBX files into Unreal Engine is a relatively simple procedure, there are quite a few options available for tweaking the imported asset. This document will cover those options.

When you import content through the **Content Browser** using the FBX pipeline, the **FBX Import Options** dialog appears. The importer will automatically detect what kind of file you are attempting to import and adjust its interface accordingly.

## Static Mesh Options

The options available when importing a *StaticMesh* using FBX are explained below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7382155-2997-4492-bdfa-ae51ad9896f0/staticmesh_options_4-23.png)

| Option | Description |
| --- | --- |
| Mesh |   |
| **Skeletal Mesh** | For Static Meshes: This will attempt to import the FBX file as a Skeletal Mesh. The import options will switch to handle importing the FBX file as a Skeletal Mesh. |
| **Auto Generate Collision** | This will automatically generate collision for your Static Mesh. This will not be used if custom collision is detected in the FBX file. |
| **Static Mesh LODGroup** | This dropdown allows you to choose the LOD group to which the mesh will be assigned. Mesh LOD groups define default level-of-detail settings, light map resolution, and permit global overrides (e.g. reduce all *SmallProp* LODs by 10%). Mesh LOD group settings may be overridden per-platform / device profile. You may select an LOD group at import time and change it at any time in the **Static Mesh Editor**. |
| **Vertex Color Import Option** | If enabled, vertex colors on an existing mesh are replaced with the vertex colors from the FBX file. Disable this to preserve vertex colors painted within the editor using the [Mesh Paint](/documentation/en-us/unreal-engine/mesh-paint-mode-in-unreal-engine) tool. |
| **Vertex Override Color** | This will be override color in the case that Vertex Color Import Option is set to Override. |
| **Remove Degenerates** | If enabled, degenerate triangles found during import will be removed. Disabling this option will keep degenerate triangles found. In general, this option should be enabled. |
| **Build Adjacency Buffer** | If *true*, the mesh will be optimized for PN tessellation. It is recommended to disable for larger meshes. |
| **Build Reveresed Index Buffer** | This is used to reduce the number of GPU state changes between drawcalls. This is required to optimize a mesh in mirrored transform. It will also double the index buffer size. |
| **Generate Lightmap UVs** | If enabled, the importer will generate a set of unique, non-overlapping, UVs for use with static lighting. |
| **One Convex Hull per UCX** | This option forces all UCX meshes to receive one convex hull. If disabled, then a UCX mesh could be decomposed by the engine into a series of convex hulls to get the appropriate shape. |
| **Transform Vertex to Absolute** | If *true*, the FBX file will use the transform, offset, and pivot for the world origin. If *false*, the FBX will import without any node heirarchy transform. |
| **Bake Pivot in Vertex** | If *true*, the pivot rotation will be applied to the mesh. The pivot of the FBX file will then be the origin of the mesh. Transform Vertex to Absolute must be set to *false*. |
| **Import Mesh LODs** | 
Creates LOD models for Unreal meshes from LODs defined in the file. Otherwise, only the base mesh from the LOD group is imported. For Skeletal Meshes, the LOD models can be skinned to the same skeleton, or a different skeleton. If the LOD model is skinned to a different skeleton, it must meet the Unreal LOD requirements, with the exception that the name of the root bones can be different since the FBX importer renames the root bones automatically.



 |
| **Normal Import Method** | 

This import option adjusts how Normals will be handled. The options are as follows:

-   **Compute Normals**: The engine computes normals and tangents. Smoothing group and normal info is discarded from the FBX info.
-   **Import Normals**: The normals are imported from the FBX file, tangents are computed by the engine.
-   **Import Normals and Tangents**: The normals and tangents are imported from the FBX file and nothing is computed by the engine.



 |
| **Normal Generation Method** | The option to choose between MikkTSpace or Built-in Normal generation method. |

## Skeletal Mesh Options

The options available when importing a *SkeletalMesh* using FBX are explained below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8ce8378-c24b-410c-9111-9a85a87ce6a9/skeletalmesh_options_4-23.png)

| Option | Description |
| --- | --- |
| Mesh |   |
| **Skeletal Mesh** | For Skeletal Meshes, disabling this will have the importer attempt to import the FBX file as a Static Mesh. |
| **Import Mesh** | Whether to import the mesh. This allows animation only imports when importing a Skeletal Mesh. |
| **Import Content Type** | Mesh content type you are importing. |
| **Skeleton** | The [Skeleton](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine) the SkeletalMesh should target. If no existing Skeleton is selected, a new one will be created from the SkeletalMesh being imported. The new Skeleton's name will be that of the SkeletalMesh with *Skeleton* appended. |
| **Vertex Color Import Options** | If enabled, vertex colors on an existing mesh are replaced with the vertex colors from the FBX file. Disable this to preserve vertex colors painted within the editor using the [Mesh Paint](/documentation/en-us/unreal-engine/mesh-paint-mode-in-unreal-engine) tool. |
| **Vertex Override Color** | This will be override color in the case that Vertex Color Import Option is set to Override. |
| **Update Skeleton Reference Pose** | If enabled, this will update the Reference Pose of Skeleton Asset of the Skeletal Mesh/Animation being imported, to the reference pose in the FBX file being imported. |
| **Use T0As Ref Pose** | If enabled, the first frame (frame 0) of the animation track will be used to replace the Skeletal Mesh's reference pose. |
| **Preserve Smoothing Group** | If enabled, triangles with non-matching smoothing groups will be physically split, duplicating shared vertices. |
| **Import Meshes in Bone Hierarchy** | If enabled, meshes nested in bone hierarchies will be imported instead of being converted to bones. |
| **Import Morph Targets** | If enabled, [MorphTargets](/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine) will be imported from the FBX files along with the SkeletalMesh. |
| **Import Mesh LODs** | If enabled, creates LOD models for Unreal meshes from LODs defined in the file. Otherwise, only the base mesh from the LOD group is imported. For skeletal meshes, the LOD models can be skinned to the same skeleton, or a different skeleton. If the LOD model is skinned to a different skeleton, it must meet the Unreal LOD requirements, with the exception that the name of the root bones can be different since the FBX importer renames the root bones automatically. |
| **Normal Import Method** | 
Allows for control of how Normals will be handled. The options are as follows:

-   **Compute Normals**: The engine computes normals and tangents. Smoothing group and normal info is discarded from the FBX info.
-   **Import Normals**: The normals are imported from the FBX file, tangents are computed by the engine.
-   **Import Normals and Tangents**: The normals and tangents are imported from the FBX file and nothing is computed by the engine.



 |
| **Normal Generation Method** | The option to choose between MikkTSpace or Built-in Normal generation method. |
| **Create PhysicsAsset** | If enabled, this will generate a new PhysicsAsset for the imported Skeletal Mesh. The PhysicsAsset will be composed of mostly spheres (with the exception being the root which will be a capsule/SphrL object), with the constraints being completely free on all rotational axis and completely locked on positional axis. |
| **Select PhysicsAsset** | If Create PhysicsAsset is disabled, you will be able to choose a PhysicsAsset that already exists or **none** to simply not have the Skeletal Mesh associated with a PhysicsAsset. |

## Animation Options

The options available when importing an Animation using FBX are explained below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ae81669-4af8-45dd-b2be-736d6d5ffc46/animation_options_4-23.png)

| Option | Description |
| --- | --- |
| Mesh |   |
| **Skeleton** | The [Skeleton](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine) the SkeletalMesh should target. If no existing Skeleton is selected, a new one will be created from the SkeletalMesh being imported. The new Skeleton's name will be that of the SkeletalMesh with *Skeleton* appended. |
| Animation |   |
| **Import Animations** | If enabled, [Animations](/documentation/en-us/unreal-engine/fbx-animation-pipeline-in-unreal-engine) will be imported from the FBX files along with the SkeletalMesh. A name for the Animation can be entered in the text box to override the default naming. |
| **Animation Length** | 
-   **Exported Time**: This option imports animation frames based on what is defined at the time of export.
-   **Animated Time**: Will import the range of frames that have animation. Can be useful if the exported range is longer than the actual animation in the FBX file.
-   **Set Range**: This will enable the Start Frame and End Frame properties for you to define the frames of animation to import.



 |
| **Import Meshes in Bone Hierarchy** | If checked, the meshes nested in bone hierarchies will be imported instead of being converted to bones. |
| **Frame Import Range** | 

-   **Min**: When *Set Range* is used in Animation Length, this will enable you to set the start frame of the animation you wish to import.
-   **Max**: When *Set Range* is used in Animation Length, this will enable you to set the end frame of the animation you wish to import.



 |
| **Use Default Sample Rate** | If *true*, the default sample rate of 30 frames-per-second is used for the animation. If unchecked, the system determines the sample rate from the FBX file. |
| **Custom Sample Rate** | Sample FBX animation data at the specified sample rate. When set to 0, the best sample rate is automatically determined. |
| **Import Custom Attribute** | If enabled, import a custom attribute as a curve within the animation. Requires Import Animations to be enabled. |
| **Delete Existing Custom Attribute Curves** | If true, all previous custom attribute curves will be deleted when doing a reimport. |
| **Import Bone Track** | Import bone transform tracks. If false, this will discard any bone transform tracks. (Useful for curves-only animations.) |
| **Set Material Curve Type** | If *true*, this will set the Material Curve Type for all custom attributes that exists. |
| **Material Curve Suffixes** | Specify the suffix for Material Curve Types using the custom attribute. This does not matter if Set Material Curve Type is set to *true*. |
| **Remove Redundant Keys** | Redundant keys will be removed when importing a custom attribute as a curve. |
| **Delete Existing Morph Target Curves** | If enabled, this deletes currently existing MorphTargets. This setting is only used when reimporting a mesh and can be set in the Skeletal Mesh Editors Reimport settings tab. |
| **Do not import curves with 0 values** | When importing a custom attribute or morph target as a curve, do not import if it doesn't have any value other than zero. This is to avoid adding extra curves to evaluate. |
| **Preserve Local Transform** | The way the engine calculates and accumulates transforms is different. We calculate the global transform and then calculate back to the local transform. In some cases, this can affect animations using 3DS Max or non-uniform scale. |
| **Override Animation Name** | The name to assign the animation. If nothing is entered here, the [Naming Rules](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine#namingconventions) will be used. Requires Import Animations to be enabled. |

## Transform

The options available when importing any Static or Skeletal Mesh asset using FBX are explained below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c71110ef-c75b-4d00-8126-83379482727e/transformimportoptions.png)

| Option | Description |
| --- | --- |
| **Import Translation** | This will enable the mesh to be moved along the XYZ axis when imported. This will be the location of the mesh when imported offset from the world origin. |
| **Import Rotation** | This will enable the mesh to be rotated along the XYZ axis when imported. |
| **Import Uniform Scale** | This will enable the mesh to be scaled uniformly when imported. |

## Miscellaneous

The other various options available when importing any Static or Skeletal Mesh asset using FBX are explained below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8b68b30-1d9c-48f2-8bb5-880d477affac/miscimportoptions.png)

| Option | Description |
| --- | --- |
| **Convert Scene** | This will convert the scene from the FBX coordinate system to use UE's coordinate system. |
| **Force Front XAxis** | This will convert the scene from the FBX coordinate system to UE's coordinate system with the front X axis instead of -Y axis. |
| **Convert Scene Unit** | This will convert the scene from the FBX units of measurement to UE's unit of measure, centimeters. |
| **Override Full Name** | This will use the string "Name" field as the full name of the mesh. This option only works when the scene contains one mesh. |

## Material Options

The options available when importing a Material using FBX are explained below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfdf1aa3-af61-4638-abc4-0d03d953eee9/material_options_4-23.png)

| Option | Description |
| --- | --- |
| Material |   |
| **Search Location** | 
Specify where we should search for matching materials when importing:

-   **Local**: Search for matching material in local import folder only.
-   **Under Parent**: Search for matching material recursively from parent folder.
-   **Under Root**: Search for matching material recursively from root folder.
-   **All Assets**: Search for matching material in all asset folders.



 |
| **Material Import Method** | 

Specify the import method for the following options.

-   **Create New Materials**: Automatically creates a new material asset from import.
-   **Create New Instanced Materials**: Enables selection of Base Material Name.
-   **Do Not Create Material**: Do not create a new material asset from import.



 |
| **Import Textures** | If enabled, Textures referenced in the FBX file are imported into Unreal. If **Import Materials** is *true*, textures are always imported regardless of this setting. |
| **Invert Normal Maps** | If enabled and textures are being imported, normal maps values will be inverted. |
| **Reorder Material to Fbx Order** | If enabled, the material list will be reordered to the same order as the FBX file. |

## Naming Rules

The table below shows how the various content types will be named when **Override FullName** is enabled.

The table assumes the following:

-   **%1** is the name of the asset being imported, i.e. the last part of the Import Path.
-   **%2** is the mesh node name in the FBX file. For SkeletalMesh, if it is composed of multiple FBX meshes, the first FBX mesh name is used as the part of FBX node name.

| Content Type | Naming Rules |
| --- | --- |
| **StaticMesh** | 
If **Override FullName** is:

-   **Enabled**
    -   If single mesh in file - Named as *%1*
    -   If multiple meshes in file and **Combine Meshes** is:
        -   **Enabled** - Named as *%1*
        -   **Disabled** - Named as *%1\_%2*
-   **Disabled**
    -   If single mesh in file - Named as *%1\_%2*
    -   If multiple meshes in file and **Combine Meshes** is:
        -   **Enabled** - Named as *%1*
        -   **Disabled** - Named as *%1\_%2*



 |
| **SkeletalMesh** | 

If **Override FullName** is:

-   **Enabled**
    -   If single mesh in file - Named as *%1*
    -   If multiple meshes in file - Named as *%1\_%2*
-   **Disabled** - Named as *%1\_%2*



 |
| **AnimationSequence** | 

If importing Animation with SkeletalMesh:

-   If animation name is entered (considered %1 in this case):
    -   If single sequences in file - Named as *%1*
    -   If multiple sequences in file - Named as *%1\_%2*
-   If no name entered - Named as *%1\_%2*

If importing only Animation:

-   If single sequences in file - Named as *%1*
-   If multiple sequences in file - Named as *%1\_%2*



 |
| **MorphTarget** | 

Uses the names of the MorphTarget nodes in the FBX file.



 |