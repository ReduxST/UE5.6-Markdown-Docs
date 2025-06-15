# Working with Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-assets-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:33

---

In **Unreal Engine**, you can create, delete, and manage Assets directly from the **Content Browser**. This page describes common Asset workflows, and explains what Asset references are and how to handle moving or deleting your Assets in the editor. Further, you will explore how to export some types of Assets from Unreal Engine into a format that other applications can import.

## Creating Assets

To create a new Asset, right-click inside a blank area of the **Content Browser**. Then, from the context menu that appears, choose the Asset you want to create. This creates a blank Asset of the type you specified. For some Assets, like Blueprints, you can select additional options, like the Blueprint's parent class.

The options in this menu may differ based on your version of Unreal Engine and which plugins you have enabled for your project. Click the image for full size.

Unlike [importing Assets](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine), which brings something you made in an external application into Unreal Engine, this method creates a blank Asset which you can populate with content.

## Asset Paths

Shapes assets from the Starter Content as shown in the Content Browser. Click the image for full size.

Assets in Unreal Engine are located and referenced by their **path**. When you are viewing assets in the content browser, you are actually viewing a **Package**. In the example of the image above, `Shape_Cone` is a package with path `/Game/StarterContent/Shapes/Shape_Cone` with a single asset contained in it with path `/Game/StarterContent/Shapes/Shape_Cone.Shape_Cone`. Unreal Engine generally follows the rule of one asset per package with two notable exceptions:

-   Blueprints contain two assets per-package.
    -   For example, if you have a Blueprint package with path `/Game/BP_MyBlueprint`, this package contains two assets:
        -   `/Game/BP_MyBlueprint.BP_MyBlueprint`
        -   `/Game/BP_MyBlueprint.BP_MyBlueprint_C`.
-   High Level of Detail (HLOD) can contain multiple assets per package.
    -   For example, if you have an HLOD package with path `/Game/HLOD/MyHLOD`, this package might contain:
        -   `/Game/HLOD/MyHLOD.HLOD_StaticMesh`
        -   `/Game/HLOD/MyHLOD.HLOD_Material`
        -   `/Game/HLOD/MyHLOD.HLOD_TextureBaseColor`
        -   `/Game/HLOD/MyHLOD.HLOD_TextureMRS`
        -   `/Game/HLOD/MyHLOD.HLOD_TextureNormal`

Something else worth noting is that while `/Game/StarterContent/Shapes/Shape_Cone` is considered a package, `/Game/StarterContent/Shapes` and `/Game/StarterContent` are not considered packages. Both packages and assets are considered **objects**. The **outer** of an object is the object that you belong to. For example, the outer of an asset is the package that contains that asset. The **outermost** of an object is the package the object belongs to. Specifying an asset is generally done by its **object path name**. As another example, the object path name for the **Shape\_Cube** asset is `/Game/StarterContent/Shapes/Shape_Cube.Shape_Cube`. The top-level asset in a package can also be inferred by the package's object path name, so you can alos specify `Shape_Cube` with `/Game/StarterContent/Shapes/Shape_Cube` since assets are assumed to have the same name as the leaf of their packages object path.

## Asset References

If an Asset makes use of another Asset in some way, we say that the Assets **reference** (or have a reference to) each other. For example, if a Cube Actor uses a Color Material, the Actor references that Material. This is why it is important to make sure that references are updated whenever you move or rename an Asset, and that you remove any references to an Asset before you delete it.

### Viewing Asset References

To view an Asset's references, right-click the Asset in the **Content Browser**. Then, from the context menu that appears, select **Reference Viewer**. A new window will open that displays a visual representation of the Asset's references.

Reference Viewer window for a Material Asset. Click the image for full size.

For more information about the Reference Viewer, refer to the [Reference Viewer](/documentation/en-us/unreal-engine/reference-viewer-in-unreal-engine) page.

### Copying Asset References

To copy one or more Assets' references to the clipboard, select the Asset or Assets in the **Content Browser**. Then, right-click your selection and, from the context menu that appears, select **Copy Reference**.

References contain the Asset type and the path to the `.uasset` file. They will look similar to the examples below:

```
		`Material'/Game/StarterContent/Materials/M_Metal_Brushed_Nickel.M_Metal_Brushed_Nickel' 		Material'/Game/StarterContent/Materials/M_Metal_Burnished_Steel.M_Metal_Burnished_Steel' 		Material'/Game/StarterContent/Materials/M_Metal_Chrome.M_Metal_Chrome'`
Copy full snippet
```
Material'/Game/StarterContent/Materials/M\_Metal\_Brushed\_Nickel.M\_Metal\_Brushed\_Nickel' Material'/Game/StarterContent/Materials/M\_Metal\_Burnished\_Steel.M\_Metal\_Burnished\_Steel' Material'/Game/StarterContent/Materials/M\_Metal\_Chrome.M\_Metal\_Chrome'

This is useful if you need to paste the Asset's reference in a text field, or if you need to generate an external list of Assets.

### Replace References Tool

The **Replace References Tool** provides a way to combine multiple Assets into a single one.

To learn more about this tool, refer to the [Replace References tool](/documentation/en-us/unreal-engine/consolidating-assets-in-unreal-engine) page.

## Managing Assets

To perform common Asset actions, right-click the Asset and select the desired action from the context menu that appears. These actions include:

| **Action** | **Description** |
| --- | --- |
| **Edit** | Opens the selected Asset in its Editor. For example, performing this action on a Blueprint opens it in the Blueprint Editor. |
| **Rename** | Makes the Asset's name editable. To rename the Asset, type a new name and press Enter. After you rename the Asset, Unreal Engine will update all references to the Asset to its new name. |
| **Duplicate** | Creates a copy of the selected Asset at the current location. To relocate the copy, drag it to another folder. |
| **Save** | Saves the selected Asset. |
| **Show in Folder View** | Highlights the Asset's parent folder in the folder tree. Useful for finding the actual location of Assets that are part of a collection. |
| **Show in Explorer (Windows) / Show in Finder (Mac)** | 
Opens an instance of Windows Explorer or Finder at the Asset's location on disk. This is the location of the `.uasset` file.

Never move, copy, or delete Assets directly on disk, as this might break functionality in your project and lead to data corruption or data loss. Always manage `.uasset` files through Unreal Editor.

If you need to move an Asset from one project to another, refer to the [Migrating Assets](/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine) page to learn how to do this.



 |

## Moving and Copying Assets

You can move or copy Assets and folders in your project through the **Content Browser**.

The steps to moving or copying an Asset are:

1.  Click the Asset you want to move, then drag it to another folder in the Content Browser or folder tree. As you drag the Asset, a popup window will follow your mouse cursor, indicating which Asset you are trying to move.
    
    ![Moving an Asset with drag-and-drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d12880f4-7f6a-4b18-a2b1-2ad251076724/move-asset-popup.png)
2.  When you release the mouse button, a menu will appear.
    
    ![Move Asset menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b66b35f-4b56-4b03-9784-a17940e8b92b/move-asset-menu.png)
    
    The menu confirms the folder name and contains a list of three options:
    

| **Option** | **Description** |
| --- | --- |
| **Move Here** | Moves the Asset to the new location. |
| **Copy Here** | Creates a copy of the Asset at the new location, and leaves the original Asset at its current location. |
| **Advanced Copy Here** | Creates a copy of the Asset at the new location, and attempts to automatically resolve all of that Asset's references and dependencies. This option includes an additional save dialog where you need to confirm that you want to save the Asset you copied. |

## Deleting Assets

To delete an Asset, you can either:

-   Right-click it in the **Content Browser**. Then, from the context menu that appears, select **Delete**.
    
-   Select the Asset in the **Content Browser**, **World Outliner**, or **Level Viewport**, then press **Delete** on your keyboard.
    

This action will bring up a confirmation window. If your Asset isn't being **referenced** anywhere (that is, it's not being used anywhere in your Unreal project), click the **Delete** button to confirm:

![Deletion confirmation window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a45332d7-2e46-4f7a-bb48-105874e61cf2/delete-assets-no-reference.png)

If your Asset is being referenced somewhere, the confirmation window will notify you of this and ask you what you want to do. There are two types of referencing that can happen:

-   If the Asset is referenced **by other Assets**, it means that another Asset in your project is using this one. For example, if you are trying to delete a Material, and a Static Mesh uses that Material, you will see this warning.
    
-   If the Asset is referenced **in memory**, it could be open in a separate editor window, or it might have been used recently and is still cached in memory.
    
    If you are seeing zero Asset References, but at least one Memory Reference, close all other editor windows and try again. If that doesn't work, save your work and restart Unreal Engine.
    

In this situation, you have two options:

![Deleting an Asset that still has references](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d16bf47-50d2-4cb8-a60b-bc13b43186bc/delete-assets-references.png)

-   If you select **Replace References**, you can choose another Asset to replace this one wherever it is referenced in your project. For example, if a Static Mesh uses a Material, and you want to delete that Material, you can choose a different Material that the Static Mesh will use after the deletion.
    
-   If you select **Force Delete**, the Asset will be deleted **without** any additional corrections being performed.
    
    This can cause data corruption and data loss. At a minimum, Assets that reference the deleted one will no longer work correctly, but this can break your entire project.
    

## Exporting Assets

Assets in your project are stored on disk as `.uasset` files, which is a file format specific to Unreal Engine. **Exporting** an Asset saves it to disk in a format that can then be read by other applications.

To export an Asset from your project, right-click it in the **Content Browser**. Then, from the context menu that appears, select **Asset Actions > Export**. This will open a window where you can name your exported Asset and select the location where to save it.

The file type available for export will change depending on the type of Asset you selected. For example, for a Static Mesh Asset, you will see the options to export it as an FBX, OBJ, COPY, or T3D file.

Not all Assets can be exported.