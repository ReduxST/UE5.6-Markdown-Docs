# Preparing Assets for Chunking

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/preparing-assets-for-chunking-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/preparing-assets-for-chunking-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:10

---

**Unreal Engine (UE)** can deliver assets outside of the main executable of your applications in the form of packaging files. To do this, you need to organize your assets into chunks, groups of asset files that are recognized by the cooking process. This tutorial shows you how to organize assets into chunks in the **Unreal Editor**. When you have finished, you will have a sample project that will produce packaging files you can deliver with a patching system.

## Recommended Assets

For this guide, the following assets are used: **Crunch**, **Boris**, and **Khaimera** from **Paragon**, which you can download from the **Unreal Marketplace** for free. As long as you have assets that you can safely group into separate folders, you do not need to use these specific assets. The **Paragon Character Assets** make a convenient test case since UE already organizes them this way.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8d86e65-890f-483d-a0a8-6bb45f171083/01_paragonassets.png)

## Required Setup

Before proceeding any further, you should review the [Setting Up the ChunkDownloader Plugin](/documentation/en-us/unreal-engine/setting-up-the-chunkdownloader-plugin-in-unreal-engine).

As described in reference quide, you need:

1.  Create **C++ project** based on a **Blank template**. Name this project **PatchingDemo**.
    
2.  Enable **ChunkDownloader** plugin in the **Plugins** menu.
    
3.  Enable **Use Pak File** and **Generate Chunks** in **Project Settings > Project > Packaging**.
    
4.  Edit your project's `ProjectName]Build.cs` file in **Visual Studio**.
    
5.  Generate Visual Studio project files.
    
6.  Build your project in Visual Studio.
    

## Organizing Your Chunking Scheme

Now that you have enabled chunking and set up your plugins, you need to organize your assets and package them into chunks.

For more information about the chunking process, refer to [Cooking and Chunking](/documentation/en-us/unreal-engine/cooking-content-and-creating-chunks-in-unreal-engine).

1.  Right-click inside the **ParagonBoris** folder, navigate to **Create Advanced Asset > Miscellaneous**, then create a new **Data Asset**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e3da6ad-d29a-45c3-abc9-bbee02b16a68/02_createdataasset.png)
2.  Choose **PrimaryAssetLabel** as the base class for the new Data Asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5455d3a-8246-41d9-9851-dfe2ea115f02/03_primaryassetlabel.png)
    
    You can create subclasses of PrimaryAssetLabel in C++ to add extra metadata. If you create subclasses for PrimaryAssetLabel in Blueprint, they will not work for chunking purposes.
    
3.  Name the new Primary Asset Label **Label\_Boris**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fa496e6-e409-4425-8d78-58d8fc25f980/04_labelborisasset.png)
4.  Open **Label\_Boris** and fill in the following properties:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e4ff291-4827-4226-a2c5-c1224f3c4545/05_labelborissettings.png)
    
    | Property | Value |
    | --- | --- |
    | **Chunk ID** | This should be a unique value for each folder. Here we use **1001** for Boris. |
    | **Priority** | This should be a value greater than 0. Here we set them all to **1**. |
    | **Cook Rule** | Set to **Always Cook**. |
    | **Label Assets in My Directory** | Set to **Enabled**. |
    | **Is Runtime Label** | Set to **Enable** |
    
5.  Repeat steps 1 through 4 for **ParagonCrunch** and **ParagonKhaimera**. In this example we set the **ChunkID** to **1002** for Crunch and **1003** for Khaimera.
    
6.  Package or cook content for your project.
    

## Final Result

If everything is set up correctly, you will see the packaging files in your build directory, under `/Windows/PatchingDemo/Content/Paks`, when UE has finished packaging them. UE will name each of them for the Chunk ID that you designated, and they each will contain the assets for your three characters.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/053b0b70-f6d4-45b3-8398-32ad3e45cab0/06_finalpakfiles.png)

You can also navigate click **Tools > Audit > Asset Audit** to view your chunks in the Asset Audit Window.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d52fb60d-7750-478b-8e7c-b7f5333f7021/07_openassetaudit.png)

You can find more information about Asset Audit in [Cooking and Chunking](/documentation/en-us/unreal-engine/cooking-content-and-creating-chunks-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86db8dc5-b10f-4322-afa2-b80c65a6e389/08_pakfileassetaudit.png)