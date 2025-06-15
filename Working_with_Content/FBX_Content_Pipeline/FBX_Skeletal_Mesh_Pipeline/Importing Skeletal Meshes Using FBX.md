# Importing Skeletal Meshes Using FBX

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-skeletal-meshes-using-fbx-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-skeletal-meshes-using-fbx-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:27

---

Windows macOS Linux

We can import static meshes into Unreal Engine from external 3D modeling applications, such as **3DS Max**, **Maya** or **Blender**. Although we're using 3DS Max and Maya to illustrate this lesson's goal, you can import **skeletal meshes** into Unreal Engine from any 3D modeling application with a save feature.

Before getting started: Please make sure you have access to a 3D modeling application.

## Goals

The focus of this guide is to you how to import skeletal meshes from external 3D modeling applications.

## Objectives

After going through this guide, you'll know:

-   How to export skeletal meshes from external 3D modeling applications.
-   How to import skeletal meshes into Unreal Editor.
-   How to verify that skeletal meshes were imported properly.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

Autodesk Maya Autodesk 3ds Max

## Exporting Skeletal Meshes from External 3D Modeling Applications

Skeletal meshes can be exported individually or multiple meshes can be exported to a single FBX file. The import pipeline will separate multiple Skeletal Meshes into multiple assets within the destination package.

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

## Importing Skeletal Meshes

1.  In the **Content Browser**, click the **Import** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f816d9bc-ce16-47e9-87a8-739f18bddef9/importbutton_ui.png)
2.  Locate and select the FBX file you want to import.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f08e804d-49fd-4c13-82cf-299c50d88a9c/importskeletalmesh_windows.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f20ef604-4d03-4991-aeed-11c32d59ee08/importskeletalmesh_mac.png)
3.  Click **Open** to begin importing the FBX file you want to import to your project.
    
4.  Update the appropriate settings in the **FBX Import Options** dialog.
    
    Default settings should be sufficient when importing a mesh that doesn't share an existing skeleton. Refer to our [FBX Import Options Reference](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) for detailed information on all of the settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29aeca3e-1402-46d1-81cd-74ee5a2cba9d/fbxskeletalmeshdialog_windows.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffcb2cbd-b178-49c3-b1b7-2aed1df71eb8/fbxskeletalmeshdialog_mac.png)
    
    There are two import buttons available to us in the FBX Importer. The first option we have is the Import button, allowing us to import the currently selected FBX file with our specified settings. The second option we have is the Import All button, allowing us to import all of the currently selected FBX files with our specified settings.
    
    For more information on the settings available to us in the FBX Importer, go to the [FBX Import Options Reference](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) page.
    
5.  Clicking **Import** or **Import All** adds your meshes to the project.
    
    1.  If the **Skeletal Mesh** being imported shares an existing skeleton, click the **Select Skeleton** dropdown menu and select the skeleton asset from the list.
        
        ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9cd203f-6904-4529-bfd4-2d951f9037fc/import_settings_skeletonbrowser.png)
6.  The imported mesh appears inside the **Content Browser** if the process succeeded.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c3df734-2a94-4bde-8c15-52464c16424f/importedskmesh.png)

## Verifying Imported Skeletal Meshes

Double-click the imported mesh to view it in **Persona**.

*Verify that the asset imported properly by viewing it in **Persona**.*

Now that we've reached the end of this guide, you've learned:

✓ How to export skeletal meshed from external 3D modeling applications.  
✓ How to import skeletal meshes into Unreal Editor.  
✓ How to verify that skeletal meshes were imported properly.