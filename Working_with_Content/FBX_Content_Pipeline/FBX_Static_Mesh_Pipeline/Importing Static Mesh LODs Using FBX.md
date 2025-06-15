# Importing Static Mesh LODs Using FBX

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-static-mesh-lods-using-fbx-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-static-mesh-lods-using-fbx-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:28

---

You can import Static Mesh Levels of Detail (LOD) into **Unreal Engine** from external 3D modeling applications, such as **3DS Max**, **Maya**, or **Blender**. Although 3DS Max and Maya are used to illustrate this lesson's goal, you can import Static Mesh LODs into Unreal Engine from any 3D modeling application with a save feature.

### Prerequisites

-   You have access to a 3D modeling application.
-   You have a model with LODs created.

### Objectives

After going through this guide, you'll know:

-   How to set up Static Mesh LODs from external 3D modeling applications.
-   How to export Static Mesh LODs from external 3D modeling applications.
-   How to import Static Mesh LODs into Unreal Editor from external 3D modeling applications.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

Autodesk Maya Autodesk 3ds Max

## Setting-up Static Mesh LODs

1\. Select all meshes, from the base LOD down to the last LOD. The selection order is essential for ensuring the LODs are added in the correct order of complexity. Then select the *Level of Detail* > Group command from the *Edit* menu.

Click image for full size.

1\. All meshes are now grouped under the LOD Group.

Click image for full size.

1\. Select all of the LOD meshes (the order is not important) and then select the *Group* command from the *Group* menu.

Click image for full size.

1\. Enter a name for the new group in the dialog that opens and the click the ![3ds LOD Ok Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba20ff03-bb94-479b-a4bb-5da31ace38c0/max_lod_ok_button.jpg) button to create the group.

Click image for full size.

1\. Click the ![3ds Max Utility Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c773fd94-3461-42b1-a885-2c7caa91a877/3ds-utilities-button.png) button to view the *Utilities* panel and then choose the *Level of Detail* utility. **Note:** You may need to click ![max_utility_more_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28f45657-44bb-4d9b-8fdb-24b458d39844/max_utility_more_button.jpg) and select it from the list.

Click image for full size.

1\. With the group selected, click the ![max_lod_create_button.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d62ec8ed-a258-43b5-8310-379ca34295f9/max_lod_create_button.jpg) button to create a new LOD Set and add the meshes in the selected group to it. The meshes are automatically ordered according to their complexity.

Click image for full size.

## Exporting Static Mesh LODs

1.  In Maya, select the LOD Group and any collision geometry.
    
    Click image for full size.
    
2.  Go to the file menu and select Export Selection.
    
    Click image for full size.
    
3.  Choose the path where you want to save your mesh. Make sure to give it a name, choose FBX as the file format, and enable the export of animations in the FBX exporter properties. Enabling animation is required for LODs to be exported.
    
    Click image for full size.
    
    1.  In 3ds Max select the Group of meshes that comprise the LOD Set and any collision geometry.
        
        Click image for full size.
        
    2.  Go to the file menu and select *Export* > *Export Selected*.
        
        Click image for full size.
        
    3.  Choose the path where you want to save your mesh. Make sure to give it a name, choose FBX as the file format, and then save.
        
        Click image for full size.
        
    4.  In the FBX Export window enable animation under the Animation properties. This is required for LODs to be exported.
        
        Click image for full size.
        
        ## Importing Static Mesh LODs
        
        Importing Static Mesh LODs is done a few ways. One option uses the *Content Browser*, as shown below, and the other is from within the *Details* panel in the *Static Mesh Editor*. To learn how to import LOD from the Static Mesh Editor, refer to the [Creating and Using LODs](/documentation/en-us/unreal-engine/creating-and-using-lods-in-unreal-engine) documentation.
        
        1.  In the **Content Browser**, click the **Import** button.
            
            Click image for full size.
            
        2.  Locate and select the FBX file you want to import.
            
            Click image for full size.
            
        3.  Click **Open** to begin importing the mesh file to your project.
            
        4.  In the **FBX Import Options** dialog box, choose the appropriate settings, making sure the **Import LODs** option, under **Mesh** > **Advanced**, is enabled.
            
            Click image for full size.
            
        
        There are two import buttons available to us in the FBX Importer. The first option is the Import button, making it possible to import the currently selected FBX file with your specified settings. The second option is the Import All button; this imports all of the currently selected FBX files with our specified settings.
        
        For more information on the settings in the FBX Importer, refer to the [FBX Import Options Reference](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) documentation.
        
        1.  Click **Import** or **Import All** to import the mesh to your project.
            
            Click image for full size.
            
            When importing LODs, the name of the imported mesh will follow default [Naming Conventions](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine#namingconventions). Refer to our [FBX Import Dialog](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine) documentation for additional information about all of the settings.
            
        2.  Your imported mesh will show in the **Content Browser**, along with any Textures and Materials applied.
            
            Click image for full size.
            
        3.  Double-click the Static Mesh to open the **Static Mesh Editor**. By viewing the imported mesh in the **Static Mesh Editor**, you can cycle through its LODs using the **Auto LOD** dropdown.
            
            ![Cycle through LODs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e36ee49e-db97-4ad7-9cdc-898b30078306/cycle-lods.gif)
        
        Now that you have reached the end of this guide, you've learned:
        
        ✓ How to set up Static Mesh LODs from external 3D modeling applications.  
        ✓ How to export Static Mesh LODs from external 3D modeling applications.  
        ✓ How to import Static Mesh LODs into Unreal Editor from external 3D modeling applications.