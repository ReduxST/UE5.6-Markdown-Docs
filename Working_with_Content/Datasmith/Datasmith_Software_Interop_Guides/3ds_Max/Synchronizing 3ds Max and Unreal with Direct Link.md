# Synchronizing 3ds Max and Unreal with Direct Link

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine)  
**Processed:** 2025-06-14 16:58:58

---

The Datasmith Export for 3ds Max plugin supports Datasmith Direct Link (see [Using Datasmith Direct Link](/documentation/en-us/unreal-engine/using-datasmith-direct-link-in-unreal-engine)). Direct Link works by exporting your 3ds Max scene to a local cache. When you connect 3ds Max to Unreal Engine, or another connected application such as Twinmotion, it imports the scene from the cache.

To synchronize a 3ds Max Scene with Unreal Engine, your Unreal Engine project must have the Datasmith Importer plugin enabled. If you don't enable the plugin, you won't see the Datasmith options in Unreal Engine. For more information, refer tosee Enable the Datasmith Importer Plugin.

To synchronize a 3ds Max Scene with Unreal Engine:

-   Update the Direct Link cache (see [Update the Direct Link Cache](/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine#updatethedirectlinkcache)).
-   Use Direct Link to Import the 3ds Max scene into Unreal Engine (see [Import the 3ds Max Scene with Direct Link](/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine#importthe3dsmaxscenewithdirectlink)).

If you perform a Direct Link import before you update the cache, Unreal Engine will display an error message because there is nothing in the cache to import.

## Update the Direct Link Cache

From the 3ds Max ribbon, use the synchronize options in the Direct Link panel of the Datasmith tab.

-   **Synchronize**: Performs a one-time push to the Direct Link Cache. When Unreal Engine, or another connected application, connects to 3ds Max via Direct Link, it imports the cache.
    
    Use this command if you want to control when Unreal Engine displays changes to the 3ds Max scene.
    
-   **Toggle Auto Sync**: When enabled, Datasmith pushes the 3ds Max scene to the Direct Link cache every time you make a change. Unreal engine and any other connected applications re-import the cache automatically.
    
    Use this command if you want Unreal Engine to update whenever you make a change to the 3ds Max scene.
    

## Import the 3ds Max Scene with Direct Link

1.  In 3ds Max, open the scene you want to import into Unreal Engine, and [update the Direct Link cache](/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine#updatethedirectlinkcache).
2.  In Unreal Engine, in the main toolbar, open the Create menu and select **Datasmith > Direct Link Import**.  
    ![Direct Link Import](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8abc341a-6da5-4fcf-8c2a-25f880a03eef/direct-link-import-menu.png)  
    The Direct Link Available Sources dialog opens.
    
    If you have more than one instance of 3ds Max open, each instance appears as a separate source in the Direct Link Available Sources dialog.
    
3.  Select the 3ds Max source that you want to import into Unreal Engine, and click Select. A file dialog opens.
4.  Choose a location in your project to store the imported content, and click OK. The Datasmith Import Options dialog opens.
    
    To create a new top-level folder for your Datasmith content, right-click an empty area in the file dialog. To create a subfolder of an existing folder, right-click that folder.
    
5.  Set the import options as needed, and click Import. For more information about the Datasmith Import options, see [Importing Datasmith Content Into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).

## Change the Direct Link Cache Directory

When you connect 3ds Max to Unreal Engine using Direct Link, Datasmith uses a cache directory to temporarily store the contents of your Datasmith scene. For example, sent and received `.udatasmith` scenes, meshes, textures, and so on.

You can change the cache directory from the [Connection Status window](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#thedatasmithdirectlinkconnectionstatuswindow):

1.  From the **Direct Link** panel of the **Datasmith** tab in the 3ds Max ribbon, select **Connections**. The **Connection Status** window opens.
2.  Click the more options button (**⋮**) to display the Cache Directory setting.
3.  Click the ellipsis button (**...**) to open a file dialog.
4.  Navigate to the directory you want to use, and click **Select Folder**.

The cache location updates the next time you open or create a 3ds Max file and synchronize it with Unreal Engine.

To reset the cache to the default directory, click **Reset**.