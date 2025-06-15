# Exporting Datasmith Content from SketchUp Pro

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-sketchup-pro-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-datasmith-content-from-sketchup-pro-to-unreal-engine)  
**Processed:** 2025-06-14 16:22:52

---

Once you've installed the Datasmith Exporter plugin for SketchUp, you'll have a new *.UDATASMITH* file type available to you when you export a scene.

Installing the Datasmith plugin for SketchUp adds a new toolbar.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/109413ac-422d-4561-8516-be3ff9488f1d/datasmith-toolbar-sketchup.png)

After you install the Datasmith Exporter Plugin for SketchUp, you will have an **Unreal Datasmith** (`.udatasmith`) filetype available to you when you save or export a scene.

Follow the steps below in SketchUp to export your scene using this new file type.

1.  Click the **Export** button on the Datasmith toolbar.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b801d07-df0d-4e3c-baa8-8b553c9a5829/datasmith-toolbar-export.png)
2.  In the **Export Model** window, name your file and verify that the file extension in the **Save as** type drop-down list is `.udatasmith`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4ffd08a-f9c4-4f9d-b9be-292c9ddc50bf/sketchup_export_model.png)
3.  Browse to the location where you want to save your new file, set its file name, and click **Export**.
    

### End Result

You should now be ready to try importing your new *.udatasmith* file into the Unreal Editor. See [Importing Datasmith Content into Unreal Engine](/documentation/en-us/unreal-engine/importing-datasmith-content-into-unreal-engine).

Along with your new `.udatasmith` file, you'll see a folder that has the same name but with the suffix `_Assets`. If you move your `.udatasmith` file to a new location, make sure that you also move this folder to the same location.