# FBX Import Errors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-import-errors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-import-errors-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:22

---

This is a list of error or warning messages you may encounter during importing FBX files.

## Generic

Importing failed to create new asset. In this case, you are likely to have other warning messages that indicate the cause of the failures.

---

Loading FBX Scene has failed. Either the file is corrupted or it is not the correct file type.

---

An asset already exists with the given name. Make sure to use a different name to import or import into a different folder.

---

Currently importing asset is going to replace currently existing asset of the same name.

---

When overriding existing assets, the importer needs to delete the old asset first, however the importer cannot delete it because of references.

Try using a different name or importing into a different folder.

---

Opening file and importing has failed. Either the file is corrupted or it is not the correct file type.

---

No Mesh was found in the file. Make sure the FBX contains a mesh object.

---

## Mesh

Mesh object does not contain geometry.

---

Mesh is composed of polygons other than triangles, so the importer attempted to triangulate, but failed. Check the source content and triangulate it in your DCC tool.

---

The importer only supports smoothing on a polygon level, and when smoothing was done by edge, the importer will attempt to convert edge smoothing to polygon smoothing, but that has failed.

(FBX API ComputePolygonSmoothingFromEdgeSmoothing.)

---

The importer only supports smoothing on a polygon level, and when smoothing was done by vertex, the importer will attempt to convert vertex smoothing to polygon smoothing, but that has failed.

---

Face Material index is not valid. Either it is mapped to the wrong index or the material is not available. The importer forces the index to 0 when this happens.

---

FBXMesh object is not found in the node given. Make sure the mesh exists in the scene.

---

No smoothing group information was found in this FBX scene. Please make sure to enable the "Export Smoothing Groups" option in the FBX Exporter plug-in before exporting the file.

Even for tools that do not support smoothing groups, the FBX Exporter will generate appropriate smoothing data at export-time so that correct vertex normals can be inferred while importing.

---

Invalid Mesh LOD index. In order to add LOD(N), the current mesh should contain all of LOD from \[0-(N-1)\].

---

You should select a file for the LOD. No file was selected.

---

You may only select one file for the LOD.

---

### StaticMesh

Currently the importer supports up to MAX\_MESH\_MATERIAL\_INDEX(64) materials. Break your mesh into multiple pieces to fix this.

---

The light map UV set for Static Mesh appears to have layout problems. Either the triangle UVs are overlapping one another or the UVs are out of bounds (0.0 - 1.0 range.)

---

### SkeletalMesh

This error is thrown when importing an LOD (or importing a Skeletal Mesh with LODs) and the requested mesh for the LOD does not have the same root bone as the original mesh. They should have same root bone.

---

The importer cannot have bones with the same name in the Skeletal Mesh hierarchy. Make sure each bone name is unique.

---

The importer did not find any vertices weighted to the skeleton. Skeletal Meshes are required to have at least one vertex weighted to the skeleton.

---

While restoring the sort order for the section, strips could not be matched to the new data.

---

Unable to restore triangle sort setting for the section number in the old mesh, as a matching section could not be found in the new mesh. The custom sorting information has been lost.

---

Unable to restore triangle sort setting for the section as the new mesh does not contain that many sections. Please find the matching section and apply manually.

---

Could not find any valid mesh on the root hierarchy. If you have mesh in the sub hierarchy, please enable option of \[Import Meshes In Bone Hierarchy\] when importing.

---

Could not find a valid root node.

---

(#SkeletalMesh\_InvalidBone

Failed to find any bone hierarchies. Try to import with the Rigid Mesh option enabled.

---

Could not find any valid Nodes.

---

Ignoring this deformer because it did not find any the weighting information.

---

Scene does not contain a Bind Pose. Make sure you have a Bind Pose in the scene. If you do not, import with \[Use Time 0 as Reference Pose\] enabled.

---

No cluster is found.

---

Could not find any bone nodes. If it is rigid, please use the \[Import Rigid Body\] option.

---

Could not find any valid bind poses. A bind pose can exist but be invalid. Often this can be fixed by recreating bind pose in the DCC tool.

---

Found multiple roots. The importer only supports one root per mesh.

---

Some bones are missing from the bind pose data. If you would like to avoid this, you can import with \[Use Time 0 as Reference Pose\] enabled or fix the bind pose in your DCC tool.

---

There are vertices in the Skeletal Mesh that are not weighted to a bone. These vertices will be fully weighted to the root bone.

---

Input mesh has a section with no triangles. This mesh may not render properly.

---

Input mesh has too many vertices. The generated mesh will be corrupt!

Consider adding extra materials to split up the source mesh into smaller chunks.

---

If you have \[Create Physics Asset\] on, it will try to create physics asset.

It can fail if:

1.  The importer failed to create the Skeletal Mesh (and thusly has no bones to build the Physics Asset)
    
2.  The mesh is too small and the Physics Asset creation default setting will not work with it.
    

If this fails, you can create physics asset after imported.

Bring up the Right-Click Context menu on the Skeletal Mesh -> Create... -> Create Physics Asset. You can then adjust the settings for creating a Physics Asset to work with the size of your Skeletal Mesh.

---

The importer is trying to recreate skeleton, but it failed because an asset exists with the same name, but it is of a different type of asset (eg: Static Mesh). Try to import in a different folder or with a different name.

---

Your Skeletal Mesh has too many bones, Unreal Engine's current max bone count is 65536.

---

Skeletal Mesh does not have any UVSets. Creating a default set.

---

New mesh is missing bones that are required by the LOD(s). Make sure these bones exist in the new mesh.

---

Failed to import LOD. Please check other warning/error messages that came up.

---

Root bone name in the LOD does not match with original mesh root bone name. Make sure both root bone names match.

---

New mesh for LOD bones should exist in the original mesh. If it has extra bones, the importer cannot match.

---

New mesh for LOD bone hierarchy should match with the original bone hierarchy. The parent does not match for the specified bone.

---

The mesh LOD you are importing has some vertices with more than one influence. If you would like to have soft vertex deformation, please set CheckSingleInfluenceLOD to False in the Editor INI file.

---

The mesh LOD is missing a bone that is required by a socket. This can cause game play artifacts when the Actor switches to the LOD.

---

Could not find morphtarget for the LOD.

---

### Animation

Mesh contains the root bone in the description, but animation does not contain that bone track. The animation data should contain at least root bone track.

-   Make sure if this animation FBX is supposed to be for the given skeleton.
-   Make sure the original mesh contains same bone hierarchy as the animation.

---

Failed to build skeleton to create animation track.

---

Could not find an animation track.

---

Animation track length is zero. You can try different options of time options.

1.  Exported Time: Find scene's local start and end time
2.  Animated Time: Find root's animated time
3.  Set Range: Set range of the frame

---

Root bone of animation does not match with the root bone of the skeleton it is importing for. Is the animation file intended for this skeleton?

---

Animation contains duplicated bones.

---

Animation contains bones that are not found in skeleton.

---

Animation does not contain any valid animation tracks, takes, or blendshapes.

---

This can be caused by using shearing or other forms of transforms the importer does not support. Or this can possibly happen due to a math error. If the animation looks fine in Persona, you can ignore this warning.