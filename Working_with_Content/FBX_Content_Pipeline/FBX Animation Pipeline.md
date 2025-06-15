# FBX Animation Pipeline

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-animation-pipeline-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-animation-pipeline-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:16

---

Animation support in the FBX import pipeline provides a simple workflow for getting animations for *Skeletal Meshes* from 3D applications into Unreal for use in games. Currently, only a single animation for each *Skeletal Mesh* can be exported/imported in a single file.

This page is a technical overview of using the FBX content pipeline to import animations into Unreal.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

This page includes information on both Autodesk Maya and Autodesk 3ds Max, please choose your preferred content creation tool below and the information relevant only to the chosen tool will be displayed:

Autodesk Maya Autodesk 3ds Max

## Naming

When importing animations into Unreal using the FBX format, the AnimationSequence will be named the same as the name of the file. When importing animations along with a Skeletal Mesh, the AnimationSequence that is created will be taken from the name of the root bone in the animation sequence. This can easily be renamed after the import process is complete through the **Content Browser**.

## Creating Animations

Animations can be unique to a single *Skeletal Mesh* or they can be reused for any number of Skeletal Meshes as long as each *Skeletal Mesh* uses the same skeleton. All you really need to create an animation and export it into Unreal using the FBX pipeline is a skeleton that has been animated. Having a mesh bound to the skeleton is completely optional, though it makes the process of creating the animation much easier as you can see how the mesh is deforming during the animation. At export time, only the skeleton is required though.

## Exporting Animations from 3D Apps

Animations must be exported individually; one animation per *Skeletal Mesh* to a single file. The steps below are for exporting a single animation into a file by itself. The mesh bound to this skeleton has been hidden as it is not absolutely necessary for exporting animations by themselves.

1.  Select the joints to be exported in the viewport.
    
    ![maya_export_1.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e60d6bef-d0a5-455b-86f7-5040cb09bc4a/maya_export_1.jpg)
2.  In the **File** menu, choose **Export Selection** (or **Export All** if you want to export everything in the scene regardless of selection).
    
    ![maya_export_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aebe5466-199c-4fbe-a75a-fbc44960f01e/maya_export_2.jpg)
3.  Choose the location and name for the FBX file to export the animation to and set the appropriate options in the **FBX Export** dialog. For the purposes of exporting animations, you must enable the **Animations** checkbox.
    
    ![maya_export_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2a4afc1-34cd-4b46-a104-2526d691c548/maya_export_3.jpg)
4.  Click the ![maya_export_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edd9a19f-d441-47e1-85d3-fb054dafb0e9/maya_export_button.jpg) button to create the FBX file containing the mesh(es).
    

1.  Select the bones corresponding to the animation to be exported in the viewport.
    
    ![max_export_1.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9ce2415-6dc9-42a4-967e-ea6b46f32204/max_export_1.jpg)
2.  In the **File** menu, choose **Export Selected** (or **Export All** if you want to export everything in the scene regardless of selection).
    
    ![max_export_2.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d73072e-b9b5-4f8c-b25a-e6df033e8c6e/max_export_2.jpg)
3.  Choose the location and name for the FBX file to export the animation to and click the ![max_save_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e405eae-57a6-45e7-abb7-30a953992a43/max_save_button.jpg) button.
    
    ![max_export_3.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81c6ea38-24ae-4f61-b7d2-c6a5a750666a/max_export_3.jpg)
4.  Set the appropriate options in the **FBX Export** dialog. For the purposes of exporting animations, you must enable the **Animations** checkbox.
    
    ![max_export_4.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17f57ee5-1f42-49b4-84b8-643b80580095/max_export_4.jpg)
5.  Click the ![max_ok_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30802496-8629-4042-b86b-89aad14585d4/max_ok_button.jpg) button to create the FBX file containing the mesh(es).
    

## Importing Animations

The FBX animation import pipeline allows for importing both a *Skeletal Mesh* and animation all at once, or importing one or the other individually.

**Skeletal Mesh with Animation**

1.  Click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8174f2b2-af0a-4c0f-81d7-35ea1b6b1e47/import_button.png) button in the **Content Browser**. Navigate to and select the FBX file you want to import in the file browser that opens. **Note:** you may want to select ![import_fbxformat.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a37a7f24-1eb2-4213-842b-ea95b897ca44/import_fbxformat.jpg) in the dropdown to filter out unwanted files.
    
    ![import_file.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9781989f-f66d-41f1-860f-df947357f6e1/import_file.jpg)
    
    The imported path of the imported asset depends on the current location of the **Content Browser** while importing. Make sure to navigate to the appropriate folder prior to performing the import. You may also drag the imported assets into a new folder once import is complete.
    
2.  Choose the appropriate settings in the **FBX Import Options** dialog. The name of the imported mesh will follow the default naming rules See the [**FBX Import Dialog**](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) section for complete details of all of the settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73766943-cfcf-4053-ae41-10e73fd11e1f/skeletalmeshfbxoptions.png)
3.  Click the ![button_import.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb917c39-26a1-420d-ad31-db22029e952a/button_import.png) button to import the mesh and LODs. The resulting mesh, animation (AnimationSequence), material(s), and texture(s) will be displayed in the **Content Browser** if the process was successful. You can see the AnimationSequence that was created to hold the animation was named after the root bone of the skeleton by default.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4012294-20c9-4d06-a3eb-ef09f24de9b3/importedcharacter.png)

**Individual Animations**

To import animations, you first need an AnimationSequence to import the animation into. This can be created through the **Content Browser** or directly in the AnimationSequence Editor.

Unreal Editor supports importing multiple animations contained in a single FBX file; however, many DCC tools such as 3ds Max and Maya do not currently support saving multiple animations to a single file. If you export from a supporting application such as Motion Builder, Unreal will import all the animations in that file.

1.  Click the ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f269a05-6c4e-4c0e-a826-21e14015224a/import_button.png) button in the **Content Browser**. Navigate to and select the FBX file you want to import in the file browser that opens. **Note:** you may want to select ![import_fbxformat.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e532054-82ce-40ee-84f5-298ee0900aae/import_fbxformat.jpg) in the dropdown to filter out unwanted files.
    
    ![import_file.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dedc4cd-8934-44f9-8675-f08419060a39/import_file.jpg)
    
    The imported path of the imported asset depends on the current location of the **Content Browser** while importing. Make sure to navigate to the appropriate folder prior to performing the import. You may also drag the imported assets into a new folder once import is complete.
    
2.  Choose the appropriate settings in the **FBX Import Options** dialog. The name of the imported mesh will follow the default naming rules. See the [**FBX Import Dialog**](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) section for complete details of all of the settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58aac872-15bf-4060-89f7-9c4f38f87a06/animationimportoptions.png)
    
    When importing animation on its own, you must specify an existing skeleton!
    
3.  Click the ![button_import.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b18a1af-b09f-457e-a9b9-681d03d2e0a8/button_import.png) button to import the mesh and LODs. The resulting mesh, animation (AnimationSequence), material(s), and texture(s) will be displayed in the **Content Browser** if the process was successful. You can see the AnimationSequence that was created to hold the animation was named after the root bone of the skeleton by default.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adbc9572-b6f2-4ca1-8105-eec33ce272d6/animsequenceimported.png)

Unreal Editor supports non-uniform scale animations. When importing an animation, if scale exists, it will also import without the need for setting additional options. For memory reasons, the engine does not save scale for all animations and only saves it if it has scale that is not 1.

Refer to the [**Skeletal Mesh Animation**](/documentation/en-us/unreal-engine/skeletal-mesh-animation-system-in-unreal-engine) page for more information and video samples.