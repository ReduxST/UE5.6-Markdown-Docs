# Importing Skeletal Mesh LODs Using FBX

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-skeletal-mesh-lods-using-fbx-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-skeletal-mesh-lods-using-fbx-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:26

---

Windows macOS Linux

We can import Skeletal Mesh Levels of Detail (LOD) into Unreal Engine from external 3D modeling applications, such as **3DS Max**, **Maya** or **Blender**. Although we're using 3DS Max and Maya to illustrate this lesson's goal, you can import Skeletal Mesh LODs into Unreal Engine from any 3D modeling application with a save feature.

Before getting started: Please make sure you have access to a 3D modeling application.

## Goals

The focus of this guide is to show you how to import Skeletal Mesh LODs from external 3D modeling programs.

## Objectives

After going through this guide, you'll know:

-   How to set-up Skeletal Mesh LODs from external 3D modeling applications.
-   How to export Skeletal Mesh LODs from external 3D modeling applications.
-   How to import Skeletal Mesh LODs into Unreal Editor from external 3D modeling applications.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

Autodesk Maya Autodesk 3ds Max

## Setting-up Skeletal Mesh LODs

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

Setting up LODs for **Multi-Part Skeletal Meshes** is almost identical to setting up LODs for a full mesh with the exception that each individual part containing LODs will have an LOD group created for it. The process for setting up those LOD groups is identical to the process outlined above.

## Exporting Skeletal Mesh LODs

1.  Select the LOD GRoups and the joints to be exported.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4ef524c-e5f4-4b2e-bdca-746efdea67a4/log_joint_selection.png)
    
    Follow the same export steps used for the base mesh (described in the [Export Mesh from 3D App](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#exportmeshfrom3dapp) section).
    
2.  Select the group of meshes that comprise the LOD Set and the bones to be exported.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/130aac8d-9728-49c5-8231-e5310f4d3b01/lod_meshset_bones_selection.png)
    
    Follow the same export steps used for the base mesh (described in the [Export Mesh from 3D App](/documentation/en-us/unreal-engine/fbx-skeletal-mesh-pipeline-in-unreal-engine#exportmeshfrom3dapp) section).
    

## Importing Skeletal Mesh LODs

**Skeletal Mesh LODs** can be imported through the **Mesh Details** panel in **Persona** under **LOD Settings**.

Persona is the animation editing toolset within UE4. Refer to the [Animation Editors](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) for additional information.

1.  To apply an **LOD** to a skeletal mesh, double-click the animation asset from the **Content Browser** to open **Persona** (example sequence pictured below).
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aaa94add-7a25-41ad-b097-ded0086326f7/openingpersona.png)
2.  In the **Mesh Details** panel, scroll down to find the **LOD Settings** section and click the **LOD Import** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89037c20-ca28-4dcb-b57c-e163146be224/lod_import.png)
3.  In the file browser, locate and select the FBX file you want to import.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64012360-9edc-4e08-af4e-92db770b0465/importlod1_windows.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96aba302-4659-43a3-afd7-15cefc0f66b5/importlod1_mac.png)
4.  The imported LOD is now added to the **Mesh Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d68e0399-fde1-4f89-94c0-b4e7e094c95b/lod_added.png)
5.  Under each LOD, the **Display Factor** setting indicates when to use the LOD. In the example pictured below, LOD0 is used when your position is closer to the **Skeletal Mesh**, whereas LOD1 is used when your position is further away from the **Skeletal Mesh**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd66d1e9-a22f-4a9f-8e1b-31d5f93100e7/lods_set.png)
    
    Using a small **Display Factor** tells Unreal Engine to use the LOD when your position is further away from the **Skeletal Mesh**. Larger **Display Factors** tell Unreal Engine to use the LOD when your position is closer to the **Skeletal Mesh**.
    

Now that we've reached the end of this tutorial, you've learned:

✓ How to set-up Skeletal Mesh LODs from external 3D modeling applications.  
✓ How to export Skeletal Mesh LODs from external 3D modeling applications.  
✓ How to import Skeletal Mesh LODs into Unreal Editor from external 3D modeling applications.