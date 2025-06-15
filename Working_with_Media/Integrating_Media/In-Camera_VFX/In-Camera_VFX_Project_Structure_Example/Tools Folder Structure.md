# Tools Folder Structure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/tools-folder-structure-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/tools-folder-structure-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:44

---

![The recommended Tools folder structure in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68da9888-29c6-40da-bb78-11f796f222e9/cb_tools.png)

The **Tools** folder contains custom [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) and widgets, [Level Snapshot](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine) Filters and Presets, and [Remote Control](/documentation/en-us/unreal-engine/remote-control-for-unreal-engine) Presets. The following list describes each tool.

-   Blueprint Tool A: Separate folder per-Stage blueprint used, containing it's source:
    
    -   BP\_Tool *or* WBP\_WidgetTool — The principle Blueprint.
        
    -   Enums - Related enumerations used in the Blueprint.
        
        -   E\_(Description)
    -   Structs - Related structures used in the Blueprint.
        
        -   F\_(Description)
    -   SubBlueprints - Only present if any sub-blueprints are used.
        
        -   BP\_(Description)
    -   SubWidgets - Only present if any sub-widget blueprints are used.
        
        -   WBP\_(Description)
-   Remote Control: Remote control presets used
    
    -   RCP\_(Description)
-   Common
    

A diagram showing the recommended tools folder structure for your project in the Content Browser.