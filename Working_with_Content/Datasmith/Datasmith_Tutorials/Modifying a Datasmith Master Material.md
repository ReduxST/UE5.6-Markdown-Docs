# Modifying a Datasmith Master Material

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/modifying-a-datasmith-master-material-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/modifying-a-datasmith-master-material-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:40

---

As described in [Datasmith Overview](/documentation/en-us/unreal-engine/datasmith-plugins-overview) and [Datasmith Import Process](/documentation/en-us/unreal-engine/datasmith-import-process-in-unreal-engine), Datasmith creates a Material Instance in your Project to represent each different type of surface that it detects in your source scene. Each of these Material Instances exposes a pre-set list of properties, which you can modify freely in your Unreal Engine Project.

However, if you want to modify the Master Material that any of your Datasmith Material Instances are based on, always create a duplicate of the original Master Material, save that duplicate in your Project content, make your changes in the duplicate, then set the Material Instance to point to your duplicate Master Material.

The instructions below on this page provide step-by-step instructions for doing so.

-   The pre-set Parent Material Assets used by Datasmith — such as the **Datasmith\_Color**, **SketchUpMaster**, and **RevitMaster** Materials — are included in the Datasmith Plugin content. If you make any changes to these Parent Materials, you'll be changing them for all your Projects, not just for your current Project. And your changes won't be saved in your Project, so if you have to distribute your Project to someone else, or upgrade to a new version of Unreal Engine, you'll lose those changes. Always make a duplicate inside your Project's content folder.
    
-   Even when you're working with a Parent Material created by Datasmith inside your Project's content folder — typically, a Parent Material created for a custom-designed Material imported from 3ds Max or Rhino — you should always follow this same procedure to create a duplicate of the original Parent Material instead of modifying the original Parent Material directly. Changes to Parent Material graphs are not preserved as Datasmith overrides, so your changes would be lost the next time you reimport your Datasmith Scene Asset.
    

## Steps

To duplicate and modify the Parent Material for any Material Instance created by Datasmith:

1.  Double-click the Material Instance whose Parent Material you want to modify. This opens the Material Instance in the Material Instance Editor.
    
2.  In the **Details** panel, find the **General > Parent** setting. This identifies the Parent Material that provides the Material Graph that this Material Instance is based on.
    
    Click image for full size.
    
3.  Double-click the thumbnail image for the **Parent**.
    
    Click image for full size.
    
    This opens the Parent Material in the Material Editor, where you can see its Material graph.
    
    You can also use the **Hierarchy** button in the Toolbar to choose and open the Parent Material.
    
    Click image for full size.
    
4.  From the main menu of the Parent's Material Editor, select **File > Save As**, and save a copy of the Parent Material anywhere in your Project's content folder.
    
    Click image for full size.
    
5.  Go back to your Material Instance, and change the **General > Parent** setting to point to your newly created Master Material.
    
    Click image for full size.
    
6.  **Save** the Material Instance.
    

## End Result

You've created a new Parent Material that duplicates the default Parent Material assigned by Datasmith, and you've assigned that new Parent Material to your Material Instance. Now, any changes you make to the graph and settings in your duplicated Master Material will immediately apply to your Material Instance. And, the next time you reimport your Datasmith Scene Asset, you won't lose any of the changes you made in your duplicated Parent Material.