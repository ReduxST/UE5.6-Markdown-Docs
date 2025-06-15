# Static Mesh Morph Targets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-morph-targets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-morph-targets-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:20

---

**Morph Targets** provide a way to deform a mesh from its base form towards a *target* form. Generally, these are used with SkeletalMeshes as part of the Animation system; however, using the `StaticMeshMorpher.ms` maxscript and the **StaticMeshMorphTarget** [Material Function](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine), StaticMeshes also have the ability to be setup for deformation using morph targets.

This method performs the deformation by using multiple UV channels, vertex colors, and the WorldPositionOffset. The offsets of the vertices for each morph target are stored as vertex colors in a UV channel. The StaticMeshMorphTarget Material Function then extracts these and makes them available within the Material. By passing them to the WorldPositionOffset input of the material, the vertices of the mesh can be transformed to the positions of the vertices in the morph target.

## Script Setup and Installation

The `StaticMeshMorpher.ms` maxscript is located in your build at `UE/Engine/Extras/FX_tools/3DSMax2012_x64/`.

**To run the** `StaticMeshMorpher.ms` **maxscript:**

1.  In 3dsMax, in the **MAXScript** menu choose **Run Script...**.
    
2.  Navigate to the location of the `StaticMeshMorpher.ms` maxscript in your build and open it.
    
3.  The script's interface is displayed and ready to be used.
    

The script can also be bound to a key combination or added to a custom menu to make running it faster and easier.

## Creating Morph Targets

Morph targets require multiple instances of the same mesh with their vertices transformed. For example, a melting ball of ice could have three forms:

|   |   |   |
| --- | --- | --- |
| ![Game Model](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56a18e9d-4e16-4d6c-9487-61f57f2e8220/game_model_table.png) | ![Morph target 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c133d0e-e5a0-4b0f-8308-07b09bebe88e/morph_1_table.png) | ![Morph target 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26e008b6-c86f-4aad-af45-7750f937c37c/morph_2_table.png) |
| Game Model | Morph Target 1 | Morph Target 2 |

The morph targets are packed into UV channels 2 and 3 (assuming two morph targets are being packed), and the normals for morph target 1 can also be stored in the mesh's vertex colors if desired.

**To pack morph targets:**

1.  Press the ![Pick Game Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4663e09f-a4db-49be-a6a4-dd2a1010709f/button_pick_gamemesh.png) button and then select the game model mesh in the scene.
    
    ![Game Mesh Selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9af3156a-9677-487b-93da-81cf1d1ede92/game_mesh_selected.png)
2.  Press the ![Pick Morph Target 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fa63785-e05a-4e88-b45d-c2ad3f680059/button_pick_morph1.png) button and then select the mesh for the first morph target in the scene.
    
    ![Morph Target 2 Selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68daa295-7338-4f5c-a731-e09e0ada95a1/morph_1_selected.png)
3.  Repeat the process above for the second morph target in the scene, if one exists.
    
    ![Morph Target 2 Selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/378e911c-6bfd-4acf-9ae9-e9c17cc57a41/morph_2_selected.png)
4.  Check the **Store Morph 1 Normals** checkbox if desired.
    
5.  Press the ![Pack Morph Targets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/525903f8-4c77-41d2-9972-e58b2ff53ea6/button_pack_morphs.png) button to begin the process of packing the morph targets into the UV channels.
    
    ![Morph Packing Progress](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e13ce350-56c2-47f0-ae5b-1b07ae3310f4/processing_progress.png)
6.  The mesh can be exported from 3dsMax and imported into Unreal normally. See **[FBX Static Mesh Pipeline](/documentation/en-us/unreal-engine/fbx-static-mesh-pipeline-in-unreal-engine)** for details on this process.
    

## Material Setup

The *StaticMeshMorphTargets* function provides access to the morph targets and normals inside the *Material* applied to the *StaticMesh*. This function has two outputs corresponding to the two morph targets and one output for the normals. The morph target outputs provide values that can be plugged into the WorldPositionOffset input channel of the *Material* node, while the normal output, as you might expect, can be connected to the *Normal* input channel of the *Material* node.

In order to allow for *morphing* between the base mesh and the morph targets, one or more *LinearInterpolate* expressions are used with a single *ScalarParameter* driving the Alpha input. This allows the morph targets to be driven at runtime by gameplay code or Sequencer.

An example setup (only the morph network) is shown here:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9997b5b-7a9d-447b-96e7-a8e17ca3a5aa/morph_material_setup.png)

The result as the *Time* parameter in the network above goes from 0 to 1 is shown below:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02ae37d0-cbf0-4c1c-926e-4d86942fd5a5/morph_result.png)