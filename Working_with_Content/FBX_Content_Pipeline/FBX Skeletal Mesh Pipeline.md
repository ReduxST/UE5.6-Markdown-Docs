# FBX Skeletal Mesh Pipeline

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:30

---

*Skeletal Mesh* support in the FBX import pipeline provides a streamlined workflow for getting animated meshes from 3D applications into Unreal for use in games. In addition to the meshes being imported, animations and morph targets can be transferred using the FBX format all within the same file if desired. Also, the textures (diffuse and normal map only) used in the materials applied to those meshes in the 3D application will be imported and materials will be automatically created and applied to the imported meshes.

Features supported for importing Skeletal Meshes using FBX:

-   [Materials including textures](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#materials)
-   [Animations](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#animations)
-   [Morph Targets](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#morphtargets)
-   Multiple UV sets
-   Smoothing groups
-   [Vertex colors](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#vertexcolors)
-   [LODs](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#skeletalmeshlods)

Currently, only a single animation for each *Skeletal Mesh* can be imported in a single file. Multiple morph targets can be transferred for a *Skeletal Mesh* in one file, though.

This page is a technical overview of using the FBX content pipeline to import Skeletal Meshes into Unreal.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

In any case below where the document tells you to use the **Import Asset** button, you can also just click and drag an FBX file in from your OS's file browser.

This page includes information on both Autodesk Maya and Autodesk 3ds Max, please choose your preferred content creation tool below and the information relevant only to the chosen tool will be displayed:

Autodesk Maya Autodesk 3ds Max

## General Setup

### Single Mesh vs Multi-Part Mesh

*Skeletal Meshes* can be comprised of a single, contiguous mesh or they can be made up of several separate meshes all skinned to the same skeleton.

![multipart.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d007f24a-cf2f-425b-beb2-d2fa9a791489/multipart.png)

Using multiple meshes makes it possible to LOD individual parts differently as well as exporting parts separately for use in modular character systems. There is no performance penalty for creating your *Skeletal Meshes* this way. The individual parts are all combined when being imported into Unreal Editor.

### Rigging

Rigging refers to the binding of a mesh to a skeletal hierarchy of bones/joints. This allows the bones/joints of the underlying skeleton to influence the vertices of the mesh, deforming it as they move.

#### Skeleton

In Maya, you will generally use the *Joint Tool* to create the skeleton for your *Skeletal Mesh*. Again, there are endless tutorials on using this tool and creating rigs in Maya. The Maya help is also a good source of information on the subject.

How you go about creating skeletal hierarchies in 3dsMax is up to you. You may use the standard *Bones Tools* as they work quite well, or create your own hierarchy of objects to allow for completely custom geometry and controls. There are many ways to skin a cat (pardon the pun) and tons of tutorials out there that show how to create animation rigs for game characters. You can also refer to the 3dsMax Help for complete details on how the tools work.

![max_rig.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ba97377-0c10-40e6-b0db-1cbacc6133b8/max_rig.png)

#### Binding

In Maya, the mesh(es) are bound to the skeleton using the *Smooth Bind* command. The process is the same whether the *Skeletal Mesh* consists of a single complete mesh or is made up of multiple mesh parts.

1.  Select the mesh(es) to be bound.
    
2.  **Shift** + Select the root joint of the skeleton.
    
3.  Select *Smooth Bind* from the *Skin > Bind Skin* menu.
    
    ![maya_skin_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01f6a4ca-1f9f-4a09-8a78-02d0d3ae8c05/maya_skin_3.jpg)
4.  Now you can adjust the weights of the vertices of the mesh for each joint to determine which vertices are influenced by which bones and to what degree. This can be done using the *Paint Skin Weights Tool* or whichever method you prefer.
    

In 3dsMax, the mesh(es) must be bound to the skeleton using the *Skin* modifier. The process is the same whether the *Skeletal Mesh* consists of a single complete mesh or is made up of multiple mesh parts.

1.  Select the mesh to be bound.
    
    ![max_skin_1.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c441e520-ec2a-4452-8723-a47f3332bc9d/max_skin_1.png)
2.  Add a *Skin* modifier from the *Modifier List*.
    
    ![max_skin_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fbecf4a-223f-4b93-99b7-c266b5b636a9/max_skin_2.jpg)
3.  In the Parameters rollout of the *Skin* modifier, click the ![skin_add_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59733006-8003-4607-a23a-1abfc95734f6/skin_add_button.jpg) button to add the bones that will influence the mesh. The **Select Bones** window will open.
    
    ![max_skin_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea044fe3-ea79-45ae-8a80-ff284c33a5e4/max_skin_3.jpg)
4.  Select the bones in the **Select Bones** window and click the **Select** button to add the bones.
    
    ![max_skin_4.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42145553-eacc-48fa-9821-a90c932c0c37/max_skin_4.jpg)
5.  The bones are now displayed in the *Bones* list of the modifier.
    
    ![max_skin_5.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e67aa392-f8ef-4e7a-8466-2975b063dd4c/max_skin_5.jpg)
6.  Now you can adjust the weights of the vertices of the mesh for each bone to determine which vertices are influenced by which bones and to what degree. This can be done using envelopes, directly entering the weights for the vertices, or whichever method you prefer.
    
    ![max_skin_6.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08eae762-09d4-44d7-a55a-89aa788c8a23/max_skin_6.png)

### Pivot Point

The pivot point of the mesh in Unreal Engine determines the point around which any transformations (translation, rotation, scale) will be performed.

![pivot.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96a72932-2232-4d6e-9586-c81aa86deeec/pivot.png)

The pivot point of a *Skeletal Mesh* is always located at the root bone/joint of the skeleton. This means it does not matter where the root of the skeleton is located within the scene. It will be as though it is at the origin (0,0,0) when exporting from a 3D modeling application.

![pivot_root.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41a460f1-7953-415e-8475-21f0b988e7e9/pivot_root.png)

### Triangulation

Meshes in Unreal Engine must be triangulated as the graphics hardware only deals with triangles.

![tris.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20df74a5-388d-40cf-aa7f-0f3cefa2691f/tris.jpg)

There are several ways you can ensure your mesh is triangulated.

-   Model the mesh with only tris - best solution, provides the most control over the end result.
-   Triangulate the mesh in the 3D app - good solution, allows cleanup and modification before export.
-   Allow the importer to triangulate the mesh - okay solution, allows no cleanup but can work for simple meshes.
-   Allow the FBX exporter to triangulate the mesh - okay solution, allows no cleanup but can work for simple meshes.

**Note:** Allowing the FBX exporter to triangulate the mesh results in completely random smoothing when Split Non-Matching Triangles is checked. Importing an FBX-triangulated mesh back into Maya and re-exporting shows proper smoothing.

It will always be best to manually triangulate the mesh in the 3D application, controlling the direction and placement of edges. Automatic triangulation can lead to undesirable results.

![tris_bad.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/592115b6-6502-440e-9539-14abcdb05abb/tris_bad.jpg)

### Creating Normal Maps

Normal maps can be created for your meshes directly inside of most modeling applications by creating both a low-res render mesh and a high-res detail mesh.

![SideBySide.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae16c9cf-e40c-474f-88c4-50e72789d348/sidebyside.jpg)

The geometry of the high-res detail mesh is used to generate the normals for the normal map. Epic uses a workflow internally that introduces XNormal into the process and generally results in much better normals when rendering inside of Unreal Engine 4. For details on this process, see [Textures](/documentation/en-us/unreal-engine/textures-in-unreal-engine).

### Materials

The materials applied to meshes modeled in external applications will be exported along with the mesh and then imported into Unreal. This streamlines the process as textures do not need to be imported separately in Unreal Ed, materials do not need to be created and applied, etc. The import process is capable of performing all of these actions when using the FBX pipeline.

These materials also need to be set up in a specific way, especially when the mesh has multiple materials or the order of the materials on the mesh is important (i.e. for character models where material 0 needs to be the body and material 1 needs to be the head).

For complete details of setting up materials for export, see the [**FBX Material Pipeline**](/documentation/en-us/unreal-engine/fbx-material-pipeline-in-unreal-engine) page.

### Vertex Colors

Vertex colors (one set only) for *Skeletal Meshes* can be transferred using the FBX pipeline. No special setup is necessary.

![vertex_color.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17360e39-7759-4104-b87d-c872d7f8f60e/vertex_color.jpg)

## Export Mesh from 3D App

*Skeletal Meshes* can be exported individually or multiple meshes can be exported to a single FBX file. The import pipeline will separate multiple *Skeletal Meshes* into multiple assets within the destination package.

1.  Select the mesh(es) and joints to be exported in the viewport.
    
    ![meshAndJointsSel.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/602453e5-bf0a-4369-9104-3af0dffec120/meshandjointssel.png)
2.  In the *File* menu choose *Export Selection* (or *Export All* if you want to export everything in the scene regardless of selection).
    
    ![maya_export_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2167b9b1-0cb7-4523-9962-d630d1886fdc/maya_export_2.jpg)
3.  Choose the location and name for the FBX file to export the mesh(es) to and set the appropriate options in the **FBX Export** dialog and then click the ![maya_export_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09d01e10-a9ee-4269-a8c1-7b5b068b741b/maya_export_button.jpg) button to create the FBX file containing the mesh(es).
    
    ![maya_export_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76afa621-6fa7-482c-893b-7cc5c5b1be92/maya_export_3.jpg)

1.  Select the mesh(es) and bones to be exported in the viewport.
    
    ![max_export_1.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bc331ff-4e3f-47c9-b635-46c24587f036/max_export_1.png)
2.  In the *File* menu, choose *Export Selected* (or *Export All* if you want to export everything in the scene regardless of selection).
    
    ![max_export_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d0b005f-a543-4d75-930e-dd74dc98da49/max_export_2.jpg)
3.  Choose the location and name for the FBX file to export the mesh(es) to and click the ![max_save_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ca264d4-7ca8-4e59-9030-025beb7229f1/max_save_button.jpg) button.
    
    ![max_export_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2d1f95a-cc0f-45a4-9692-21e00448f723/max_export_3.jpg)
4.  Set the appropriate options in the **FBX Export** dialog and then click the ![max_ok_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/382e0b58-7622-487a-a2ca-07a00d227b9d/max_ok_button.jpg) button to create the FBX file containing the mesh(es).
    
    ![max_export_4.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/207f2370-295a-4412-8a0d-8cc3de6043a8/max_export_4.jpg)

## Import Mesh

1.  Click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df4fcc05-8f59-4bbd-9b98-87e945f31121/import_button.png) button in the **Content Browser**. Navigate to and select the FBX file you want to import in the file browser that opens. **Note:** you may want to select ![import_fbxformat.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54d73166-d9a8-462c-844e-8cea23d8317e/import_fbxformat.jpg) in the dropdown to filter out unwanted files.
    
    ![import_file.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e937aa3-7874-4795-9034-f877058fa8a4/import_file.jpg)
    
    The path of the imported asset depends on the current location of the **Content Browser** while importing. Make sure to navigate to the appropriate folder prior to performing the import. You may also drag the imported assets into a new folder once import is complete.
    
2.  Choose the appropriate settings in the **FBX Import Options** dialog. The defaults should be sufficient when importing a mesh that does not share an existing Skeleton. See the [**FBX Import Dialog**](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) section for complete details of all of the settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e6bfcf8-2de0-482d-97b1-b7a8a0e8de04/skeletalmeshfbxoptions.png)
    
    If the *Skeletal Mesh* being imported shares an existing Skeleton, click the **Select Skeleton** dropdown menu and select the Skeleton asset from the list.
    
    ![FBX Skeletal Mesh Skeleton Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b81c63e4-9c37-4b93-bb34-ce2e9267bd9a/import_settings_skeletonbrowser.png)
3.  Click the ![Import Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d7ce826-7814-4b35-b40b-729e87bc2d0a/button_import.png) button to import the mesh(es). The resulting mesh (as well as materials and textures if those options were enabled) are displayed in the **Content Browser** if the process was successful.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce259758-1272-45a0-a4bb-4433a82c4e37/importedcharacter.png)
    
    By viewing the imported mesh within Persona, you can determine that the process worked as expected.
    

## Skeletal Mesh LODs

*Skeletal Meshes* can make use of levels of detail (LODs) in-game in order to limit the impact of meshes as they get farther from the camera. Generally, this means each level of detail will have a reduced number of tris, simpler skeleton, and, perhaps, a simpler material (or materials) applied to it.

The FBX pipeline can be used to export/import these LOD meshes.

### LOD Setup

In general, LODs are handled by creating models of varying complexity going from the full-detail base mesh to the lowest-detail LOD mesh. These should all be aligned and occupying the same space with the same pivot point and should all be skinned to the same skeleton. It is also possible for *Skeletal Meshes* to be made up of multiple individual meshes within the 3D application. Each of these parts can have LODs independent of the rest of the mesh. This means that some parts can have simplified versions in different LODs while other parts continue to use higher detail versions. Each LOD mesh can have completely different materials assigned, including different amounts of materials. This means the base mesh could use multiple materials to give the desired amount of detail up close, but the lower-detail meshes could use a single material since details will be less noticeable.

1.  Select all of the meshes (base plus LODs) in order from the base LOD down to the last LOD. This is important so that they are added in the correct order in terms of complexity. Then select the *Level of Detail > Group* command from the *Edit* menu.
    
    ![maya_lod_group.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7acac2a7-306e-41b5-a1ba-9f09e30c20ba/maya_lod_group.jpg)
2.  You should now have the meshes all grouped under the LOD Group.
    
    ![maya_lod_contents.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bab02f5f-8386-488f-8707-37913ae7246e/maya_lod_contents.jpg)

1.  Select all of the meshes (base plus LODs - the order is not important) and then select the *Group* command from the *Group* menu.
    
    ![max_lod_group.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bee3b9a4-9622-42d6-8697-0bbe5704f2c7/max_lod_group.jpg)
2.  Enter a name for the new group in the dialog that opens and the click the ![max_lod_ok_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89a622f1-a2c3-4698-99f8-67f2ce039476/max_lod_ok_button.jpg) button to create the group.
    
    ![max_lod_group_name.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efb9d5a1-a52b-4c5b-90d7-3a521fe82c55/max_lod_group_name.jpg)
3.  Click the ![max_utilities_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3d54375-35fc-440a-bdf7-320a9336bc92/max_utilities_button.jpg) button to view the *Utilities* panel and then choose the *Level of Detail* utility. **Note:** You may need to click ![max_utility_more_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09f1e412-11e2-4fb7-ae44-9365e5c49842/max_utility_more_button.jpg) and select it from the list.
    
    ![max_lod_utility.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96b49d42-a879-4b23-9573-dc4326a85099/max_lod_utility.jpg)
4.  With the group selected, click the ![max_lod_create_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88153aaa-cbdf-4a6b-9413-2a4ac90dd394/max_lod_create_button.jpg) button to create a new LOD Set and add the meshes in the selected group to it. The meshes will automatically be ordered according to their complexity.
    
    ![max_lod_contents.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa72d169-3a59-487b-a5a4-0ff215533023/max_lod_contents.jpg)

#### Multi-Part LODs

Setting up LODs for multi-part *Skeletal Meshes* is almost identical to setting up LODs for a full mesh with the exception that each individual part that has LODs will have an LOD group created for it. The process for setting up those individual LOD groups is identical to the process outlined above.

### Export LODs

To export the *Skeletal Mesh* LODs:

1.  Select the LOD Group(s) and the joints to be exported.
    
    ![meshAndJointsSel.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7963bc12-9332-4fb2-9e05-7b9c61b123ce/meshandjointssel.png)
2.  Follow the same export steps used for the base mesh (described above in the [Export Mesh](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#exportmesh) section).
    

1.  Select the Group(s) of meshes that comprise the LOD Set and the bones to be exported.
    
    ![max_export_1.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a49f7dd-5ac5-4e14-922b-5f6e23ed6b32/max_export_1.png)
2.  Follow the same export steps used for the base mesh (described above in the [Export Mesh](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#exportmesh) section).
    

### Import LODs

**Skeletal Mesh** LODs can be imported easily through the **Mesh Details** panel in **Persona** under **LOD Settings**.

1.  Open the **Skeletal Mesh** you wish to apply an LOD to in **Persona** and go to the **Mesh** Tab.
2.  In the **Mesh Details** panel, scroll down and find the **LOD Settings** section and click the **LOD Import** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0eb3d80-01dc-4085-b7f2-fda30dbfe3d6/lod_import.png)
3.  Navigate to and select the FBX file you want to import in the file browser that opens.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4505704-1539-465c-a6ce-4904aa419414/importfilebrowser.png)
4.  The imported LOD will be added to the **Mesh Details** panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2858dde9-1a1b-4855-b717-92a6b946806d/lod_added.png)

1.  Under each LOD, the **Screen Size** setting indicates when to use the LOD.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcaf0e7d-44b2-4fa5-ab9c-f210e57b9cad/lods_set.png)
    
    **Note:** Using a smaller number means use the LOD when further away while larger numbers mean use the LOD when closer. In the image above, LOD0 is used when closer to the **Skeletal Mesh** while LOD1 is used when further away.
    
2.  When importing or adding LODs, **Reduction Settings** can also be adjusted for the LOD.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2d1630b-6c72-43e1-bcdc-a5703cc8e903/lod_reductionsettings.png)

## Export to FBX from Unreal Editor

*Skeletal Meshes* previously imported into Unreal Editor can be exported back to an FBX file from within the **Content Browser**.

Assets in cooked packages cannot be exported as the source data which has been cooked out is required for the export process.

1.  In the **Content Browser**, select the *Skeletal Mesh* you want to export.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9990b338-17b8-47e8-b101-4c39c0fe88de/selectskeletalmesh.png)
2.  **Right-click** on the *Skeletal Mesh* and choose **Asset Actions** > **Export**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2815b4a-c0b1-4596-aa44-1cae602c9e05/exportmenu.png)
3.  Choose a location and name for the file to export in the file browser that appears. **Note:** make sure *FBX File (\*.FBX)* is selected as the file type.
    
    ![export_file.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/940912dc-32cd-459f-adec-7d4193fc030e/export_file.jpg)

## Physics Assets

For complete details on using the Physics Asset Tool (PhAT), see the [**Physics Asset Tool**](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine) user documentation.

## Animations

For complete details on using the FBX content pipeline to create and import animations, see the [**FBX Animation Pipeline**](/documentation/en-us/unreal-engine/fbx-animation-pipeline-in-unreal-engine) page.

## Morph Targets

For complete details on using the FBX content pipeline to create and import morph targets, see the [**FBX Morph Target Pipeline**](/documentation/en-us/unreal-engine/fbx-morph-target-pipeline-in-unreal-engine) page.