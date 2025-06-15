# Exporting Datasmith Content from VRED

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-vred-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-vred-to-unreal-engine)  
**Processed:** 2025-06-14 16:22:54

---

## Installing the Exporter Plugin Script

Before you can get started working with your VRED content in the Unreal Engine, you need to install a plugin script for VRED.

To see what versions of VRED Professional the exporter plugin currently supports, see [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types).

Follow the steps below to install the Datasmith exporter plugin script for any supported version of VRED that you have installed on your computer.

1.  In your Unreal Engine installation folder, find the `Engine/Plugins/Enterprise/DatasmithFBXImporter/Resources/VREDPlugin` folder.
    
2.  Copy this folder, along with all of its contents, to a location that your VRED installation searches for plugins.  
    For example, on Windows platforms this may be `C:\Users[username]\Documents\Autodesk\VRED-[internalVersion]\ScriptPlugins`, where `[username]` is your Windows user ID, and `[InternalVersion]` represents the version of VRED you have installed.  
    For complete details on how to find this path, see VRED documentation on [creating, editing, and using scripts](http://help.autodesk.com/view/VREDPRODUCTS/2018/ENU/?guid=GUID-C085B3DC-A66C-48EB-8FE4-43E4383AC46E).
    
    You can also use the VRED Terminal window to help you find this path. Open the Terminal by selecting **View > Terminal** from the main menu, then look for lines that begin with the text: **Looking for script plugins in**. For example:
    
    ![VRED terminal window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2986cc29-0998-4ac1-b410-de3f1807adc8/vred-terminal.png)
3.  Restart VRED.
    

## Exporting to Datasmith

When you have your VRED scene the way you want it, and you've registered your variants, export the scene to FBX:

1.  From the main menu in VRED, choose:
    -   **File > Export > Export to Datasmith...** (for VRED 2018)
    -   **File > Export Scene Data > Export to Datasmith...** (for VRED 2019)
        
        ![Datasmith export from VRED](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d68e072-ed74-4bc1-bbfa-aeaeeaa061bb/datasmith-vred-export.png "Datasmith export from VRED")
2.  Browse to a folder and choose a file name.

The exporter creates a `.FBX` file in the location you choose.

### End Result

You should now be ready to try importing your new `.FBX` file into the Unreal Editor. See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).

The exporter also creates additional files next to the `.FBX`:

-   A `.lights` file that contains additional information about the lights in your scene.
-   A `.var` file that contains information about your registered variants.
-   A `.clips` file that contains the animations.
-   A `.mats` file that contains additional information about materials.

These files contain information required by the Datasmith importer. If you move your `.FBX` file to a new location, make sure to keep these additional files at the same relative path.