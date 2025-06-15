# Reimporting Datasmith Content

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reimporting-datasmith-content-into-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reimporting-datasmith-content-into-unreal-engine)  
**Processed:** 2025-06-14 16:46:24

---

This page describes how to reimport Datasmith content into the Unreal Editor, and how to control what updates get synchronized to the Actors in your Levels.

For background information, including an overview of what reimporting does to the assets in your Project and the Actors in your Level, see [Datasmith Reimport Workflow](/documentation/en-us/unreal-engine/datasmith-reimport-workflow-in-unreal-engine).

## Reimporting the Datasmith Scene Asset

To reimport the Datasmith Scene Asset from a new version of a source file:

1.  Right-click the **Datasmith Scene** Asset in the Content Browser.
    
    Click image for full size.
    
    -   If you've saved the changes to your source scene into the same file on disk that you last used to create or reimport this Datasmith Scene Asset, select **Reimport** from the context menu.
        
    -   If you've saved the changes to your source scene into a different file on disk, select **Reimport With New File** from the context menu, and browse to the new file you want to use.
        
2.  You'll be prompted to specify some reimport options. These are the same ones you originally set on import, with a couple of additions.  
    The new options, under **Sync Current Level Actors**, determine whether the updates made to your Datasmith Scene Asset should also be applied to any Datasmith Scene Actors in the current Level that were created from the Asset you're updating.
    
    Click image for full size.
    
    If you don't want to synchronize your Actors now, you can do it later. See [Synchronizing a Datasmith Scene Actor with its Asset](/documentation/en-us/unreal-engine/reimporting-datasmith-content-into-unreal-engine#synchronizingadatasmithsceneactorwithitsasset) below.  
    For more information on the other import options, see [Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine).
    
3.  Set the options you want the importer to use, and click **Import**.
    

The reimport process may overwrite Static Mesh geometry, Parent Materials, and Texture Assets in your Content Browser. For details, see [Datasmith Reimport Workflow](/documentation/en-us/unreal-engine/datasmith-reimport-workflow-in-unreal-engine).

## Synchronizing a Datasmith Scene Actor with its Asset

There are two ways you can re-synchronize a Datasmith Scene Actor in a Level with its corresponding Datasmith Scene Asset:

-   [During the reimport](/documentation/en-us/unreal-engine/reimporting-datasmith-content-into-unreal-engine#duringthereimport).
    
-   [After the reimport](/documentation/en-us/unreal-engine/reimporting-datasmith-content-into-unreal-engine#afterthereimport).
    

### During the Reimport

At the time you reimport a Datasmith Scene Asset:

1.  Open the Level that contains your Datasmith Scene Actor.
    
2.  Reimport your Datasmith Scene Asset as described under [Reimporting the Datasmith Scene Asset](/documentation/en-us/unreal-engine/reimporting-datasmith-content-into-unreal-engine#reimportingthedatasmithsceneasset) above.
    
3.  In the **Import Options** dialog, find the **Sync Current Level Actors** section. Make sure to check the **Datasmith Scene Actors** box.  
    If you want to add back to your Level any Actors that you've previously deleted, also check the **Re-Spawn Deleted Actors** option.
    
    Click image for full size.
    
4.  Click **Import**.
    

### After the Reimport

At any time after you reimport a Datasmith Scene Asset:

1.  Open the Level that contains your Datasmith Scene Actor.
    
2.  Select the Datasmith Scene Actor in the **Outliner**.
    
    Click image for full size.
    
3.  In the **Details** panel, find the **Datasmith** section.
    
    Click image for full size.
    
4.  If you want to add back to your Level any Actors that you've previously deleted, check the **Respawn deleted actors** option.
    
5.  Click **Update actors from Scene**.
    

## Reimporting Individual Assets

Instead of reimporting an entire Datasmith Scene Asset, you can pick and choose individual Static Mesh, Material, and Texture Assets to update.

To re-import a single Asset:

1.  Right-click the Asset in the Content Browser, and choose **Reimport** from the context menu.
    
    Click image for full size.
    
    For a Material Asset, choose **Datasmith > Reimport Material**.
    
    Click image for full size.
    
    You'll only see the **Datasmith > Reimport** **Material** option for Material Assets that Datasmith created from scratch to match a material definition in your source file, which is typically the case only for Parent Materials imported from 3ds Max. However, this option does not appear for Material Assets that are instances of Materials built in to Datasmith, which is typically the case for Materials imported from CAD files or SketchUp.
    
2.  You'll be prompted to specify some reimport options for the Asset.  
    These are the same ones you originally set on import. For more information on all these options, see [Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine).
    

When you re-import individual Assets, you don't get the option to synchronize Level Actors. Every reference to the Asset in your Project will automatically use the updated version of your Asset. See [Datasmith Reimport Workflow](/documentation/en-us/unreal-engine/datasmith-reimport-workflow-in-unreal-engine).