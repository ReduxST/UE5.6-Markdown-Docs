# Importing Animations Using FBX

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-animations-using-fbx-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-animations-using-fbx-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:07

---

We can import animations into Unreal Engine from external 3D modeling applications, such as **3DS Max**, **Maya** or **Blender**. Although we're using 3DS Max and Maya to illustrate this lesson's goal, you can import animations into Unreal Engine from any 3D modeling application with a save feature.

Before getting started: Please make sure you have access to a 3D modeling application.

## Goals

The focus of this guide is to show you how to import animations from external 3D modeling programs.

## Objectives

After going through this guide, you'll know:

-   How to export animations from external 3D modeling applications.
-   How to import animations into Unreal Editor from external 3D modeling applications.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

Autodesk Maya Autodesk 3ds Max

## Exporting Animations

Animations must be exported individually with one animation per skeletal mesh in a single file.

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

Unreal's FBX animation import pipeline allows content developers to import animations with or without skeletal meshes.

### Importing Animation with Skeletal Mesh

1.  In the **Content Browser**, click the **Import** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c71ec019-fa36-47d6-b95e-6e64f66c832b/importbutton_ui.png)
2.  Locate and select the FBX file you want to import.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fadc99f6-e1a7-4cb5-9b43-881f9d7d9960/importdialogbox.png)
3.  Click **Open** to begin importing the FBX file you want to import to your project.
    
4.  Update the appropriate settings in the **FBX Import Options** dialog.
    
    Default settings should be sufficient when importing a mesh that doesn't share an existing skeleton. When importing LODs, the name of the imported mesh will follow default [Naming Conventions](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine#namingconventions). Refer to our [FBX Import Dialog](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) documentation for additional information about all of the settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3d6c2bd-a6a5-4165-9375-05bdab6a5875/fbximportoptions.png)
    
    There are two import buttons available to us in the FBX Importer. The first option we have is the Import button, allowing us to import the currently selected FBX file with our specified settings. The second option we have is the Import All button, allowing us to import all of the currently selected FBX files with our specified settings.
    
    For more information on the settings available to us in the FBX Importer, go to the [FBX Import Options Reference](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) page.
    
5.  Clicking **Import** or **Import All** adds your meshes to the project.
    
6.  The imported skeletal mesh and animations appear inside the **Content Browser** if the process succeeded.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bea21b3-5211-4b43-ad2f-5108f9d4c8ea/importedanimations.png)
    
    By default, the AnimationSequence created to hold the imported animation is named after the skeleton's root bone.
    

### Importing Animation without Skeletal Mesh

Unreal allows content creators to import multiple animations in a single FBX file; however, many DCC tools (such as 3ds Max and Maya) do no support the saving of multiple animations to a single file. If you export from supporting applications (such as Motion Builder), Unreal will import all of the animations contained in that file.

Before beginning this section, you'll need an **AnimationSequence** to import the animation into. Animation sequences can be created through the **Content Browser** or directly in the **AnimationSequence Editor**.

1.  Inside the editor, click the **Import** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5dbb9234-42f6-4c76-bfe5-a638d674eb2c/importbutton_ui.png)
2.  Locate and **select** the FBX file you want to import.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cd4d883-cb15-494a-af0d-8e2916da8008/importdialogbox.png)
3.  Click **Open** to begin importing the FBX file you want to import to your project.
    
4.  Update the appropriate settings in the **FBX Import Options** dialog.
    
    Default settings should be sufficient when importing a mesh that doesn't share an existing skeleton. When importing LODs, the name of the imported mesh will follow default naming conventions. Refer to our [FBX Import Dialog](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) documentation for additional information about all of the settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c15ef5b-b890-4f97-85ff-dcd707bd31ae/animationimportoptions.jpg)
    
    You must specify an existing skeleton when importing animations individually.
    
5.  The imported skeletal mesh and animations appear inside the **Content Browser** if the process succeeded.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4343cde9-3982-4090-b182-e2d89b2f5c1f/importedanimations.png)
    
    By default, the AnimationSequence created to hold the imported animation is named after the skeleton's root bone.
    

Now that we've reached the end of this guide, you've learned:

✓ How to export animations from external 3D modeling applications.  
✓ How to import animations into Unreal Editor from external 3D modeling applications.