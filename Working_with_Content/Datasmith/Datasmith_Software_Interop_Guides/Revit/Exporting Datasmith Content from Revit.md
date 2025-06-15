# Exporting Datasmith Content from Revit

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-revit-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-revit-to-unreal-engine)  
**Processed:** 2025-06-14 16:22:49

---

Once you've installed the Datasmith Exporter plugin for Revit, you'll have a **Datasmith** ribbon that you can use to export a selected 3D view to a `.udatasmith` file.

![Datasmith ribbon in Revit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75b6237e-ace9-431f-88d9-6192be4efe00/datasmith-ribbon-revit.png)

Follow the steps below in Revit to export your scene using this file type.

1.  In the **Project Browser**, select and open the 3D View that you want to export.
    
    ![Select a 3D View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36e56e6a-6fea-4949-8410-754a2c3cd4cb/revit-select-3d-view.png "Select a 3D View")
    
    The Datasmith Exporter plugin uses the visibility settings defined for the current 3D View to determine what parts of the scene it should export. For details, see [Revit](/documentation/en-us/unreal-engine/using-datasmith-with-revit-in-unreal-engine).
    
2.  Open the **Datasmith** ribbon, then click **Export 3D View**.
    
    ![Export 3D View button on the Datasmith toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/573488f9-d2cc-4c4b-8eaf-5301eee13bda/revit-toolbar.png "Export 3D View button on the Datasmith toolbar")
3.  In the **Export 3D View to Unreal Datasmith** window, browse to the location you want to save your .udatasmith file, and use the **File Name box** to give your new file a name.
    
    ![Set the location and file name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fbb9a13-4b2e-4809-9249-f7acb2ef0cb2/revit-ds-export-location.png "Set the location and file name")
4.  Click **Save**.
    

### End Result

You should now be ready to try importing your new `.udatasmith` file into the Unreal Editor. See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine) and [Reimporting Datasmith Content](/documentation/en-us/unreal-engine/reimporting-datasmith-content-into-unreal-engine).

Along with your new `.udatasmith` file, you'll see a folder that has the same name but with the suffix `_Assets`. If you move your `.udatasmith` file to a new location, make sure that you also move this folder to the same location.