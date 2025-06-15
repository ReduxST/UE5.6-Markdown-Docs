# Creating a New Physics Asset

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-physics-asset-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-physics-asset-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:54

---

There are two ways to create a new **Physics Asset**: on import or by using the context menu in the **Content Drawer**. Below are the steps and interfaces for both methods.

## Steps

When a Skeletal Mesh is imported, there is an option to generate a Physics Asset for it as it is imported. Once the imported file is processed, a new Physics Asset will be generated using the default properties, which can be modified using the **Physics Asset Editor**.

![An option to generate a Physics Asset for Skeletal Mesh as it is imported](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9acf6cfc-d1e8-48b9-9688-1e6e2b89144c/import-fbx-1.png)

You can choose to use an existing Physical Asset by disabling the **Create Physics Asset** checkbox, then selecting the appropriate Physics Asset using the dropdown menu.

![You can choose to use an existing Physical Asset by disabling the Create Physics Asset checkbox and select the appropriate Physics Asset using the dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed5c5a1c-a2d1-49cc-b616-caef1b5d0044/import-fbx-2.png)

However, you can follow these steps if you need to create a Physics Asset for a Skeletal Mesh at a later time:

1.  in the **Content Drawer**, find the Skeletal Mesh asset to which you wish to add a Physics Asset.
2.  Right-click on the **Skeletal Mesh** to open the **Context Menu**, the select **Create -> Physics Asset -> Create**.
    
    ![Right-click on the Skeletal Mesh to open the Context Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d76ce923-2b2a-4a18-a4fb-49bc9af4e1dc/create-physics-asset.png)
3.  Adjust the properties to your liking.
    
    ![Adjust the properties to your liking](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab3d56da-e4e3-4fe2-8f3d-2ec108cb6a75/new-physics-asset.png)
4.  Click **Create Asset**.

## Result

Upon creating a **Physics Asset** you will find it in the same folder as the **Skeletal Mesh** it is based on.