# Setting Up the ChunkDownloader Plugin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-the-chunkdownloader-plugin-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-the-chunkdownloader-plugin-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:51

---

The **ChunkDownloader** patching system is a built-in plugin for **Unreal Engine** that provides patching functionality. This page shows how to set up **Project Settings** and **Plugins** of your Unreal Engine project for using ChunkDowloader.

This example uses **C++ project** based on **Blank template**. This project has name **PatchingDemo**.

Click image to enlarge.

This example uses **C++ project** based on **Blank template**. The project has name **PatchingDemo**.

## Steps

1.  Open your **Project Settings**, navigate to **Project > Packaging**, then make sure that **Use Pak File** and **Generate Chunks** are both enabled.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35ff3075-8f3c-460d-9756-458aeeb3fe10/02_projsetenablechunking.png)
2.  Open the **Plugins** window and enable the **Chunk Downloader** plugin. Restart the **Unreal Editor** for your changes to take effect.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/734580b7-b9a6-4d73-9582-54d856aedec2/03_chunkdownloaderplugin.png)
3.  Open your project's `[ProjectName]Build.cs` file in **Visual Studio**. This file locates under `[ProjectName]/Source/[ProjectName]`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ee769d1-27d6-46ee-b279-d8c6efb7c55b/04_buildfileloc.png)
4.  Edit file by adding **ChunkDownloader** to your `ModuleRules` as `PrivateDependencyModuleNames`. For this add the following section to the `ModuleRules` in the file.
    
    ```
             `PrivateDependencyModuleNames.AddRange(new string[] { "ChunkDownloader" } );`
    		
    Copy full snippet
    ```
    PrivateDependencyModuleNames.AddRange(new string\[\] { "ChunkDownloader" } );
5.  **Save** your changes to this file.
    
6.  Right-click on your **\[ProjectName\].uproject** file and click **Generate Visual Studio project files**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df31c821-d060-4acb-a671-e87b320f2c60/05_genvsprojfiles.png)
7.  Return to your project's solution in **Visual Studio**, then **Build** the project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf2249f2-97ac-4373-a7dc-0ce7105bc02c/06_vsbuildproject.png)

## Final Result

Now, ChunkDownloader is available to use in your project. You can proceed with implementing this in your game's code to download and mount packaging files (see [Preparing Assets for Chunking](/documentation/en-us/unreal-engine/preparing-assets-for-chunking-in-unreal-engine)).