# FBX Scene Import

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine)  
**Processed:** 2025-06-14 16:23:28

---

The Import Into Level command enables users to import full FBX scenes into their levels instead of importing assets individually. Users are given full control of exactly which assets will be imported, as well as per-asset control over import settings. The workflow also allows for selective reimporting for individual assets that receive further edits outside of Unreal.

At this time, FBX full scene import supports the following asset types:

-   Static Meshes
-   Skeletal Meshes
-   Animations
-   Materials *(Basic support; may not match original material in your content creation app)*
-   Textures
-   Rigid Mesh
-   Morph Targets
-   Cameras *(no animation)*
-   Lights

In order to reimport your scene later, you must import your scenes as a single Blueprint containing components for each asset in the scene.

## FBX Full Scene Workflow

1.  From the Main Menu bar, choose **File > Import Into Level**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16593e51-cc7c-4ed6-b490-0ba947133ef7/importintolevelmenu.png)
2.  Select the FBX file containing the scene you wish to import.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7695ac1-2c8e-42ea-aa39-f6bcf93f610c/fbxfileimport.png)
3.  Choose the destination folder in your Unreal project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c4e2e17-0b12-4dac-84af-ef76384a3214/folderlocation.png)
4.  Using the FBX Scene Import Dialog, select the assets (static meshes, skeletal meshes, and materials) from your scene you would like to import.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4adc35d-8b9c-4616-bc63-197b4244c388/fbxsceneimportoptions.png)

You may also select the final output of the import process, importing all selected FBX scene assets as:

-   **Individual level Actors**
-   **Components of a single Actor**
-   **Components of a single Blueprint Actor Class** (this is the only method that supports full scene reimporting)

Once you have imported your FBX scene, all of the assets will be imported into your project, along with an FBX Scene Data asset. This asset contains all of the linking information between the original FBX scene and all of the assets that were just imported into your project.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83bd3f8f-3726-4e93-a8ee-f987ed163938/scenedata.png)

## FBX Scene Import Options Dialog

The FBX Scene Import Options Dialog gives you complete control over which assets will be imported into your scene and which will be included in the final output asset(s). You can also establish named groups of specific import settings, and quickly assign them to objects in your scene.

### Scene Tab

The Scene tab is where you can control how each asset from your FBX scene will be imported. The left side includes a tree view of the scene hierarchy. The right includes general import options for the entire scene.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3dae6a4-12db-4b8d-853d-4d48aca2f516/fbxsceneimportoptions.png)

It is important to note that unchecking an asset in the tree view of the Scene Tab will *not* prevent that asset from being imported. It only prevents the asset from being included in the final output (level actors, single actor components, or Blueprint). In order to completely prevent an asset from being imported, you must uncheck it in both the Scene Tab and the Static Meshes or Skeletal Meshes tab, respectively. This workflow enables you to import assets from the scene that you may use eventually.

#### Available Options

| Option | Description |
| --- | --- |
| **Create Content Folder Hierarchy** | This will automatically create a folder representing each tier in the hierarchy. The folder will be named after the first item found at that hierarchy level. |
| **Import as Dynamic** | If checked, the mobility of all actors or components will be dynamic. If unchecked, they will be static. |
| **Hierarchy Type** | 
This is where you choose the final output of the import process:

-   **Blueprint Asset**: This creates a single Blueprint Actor. All the assets selected in the tree view will become components of this Blueprint Actor. This is the *only* hierarchy type that supports full scene reimporting.
-   **Actor Component**: This will create a single Actor, with each of the selected assets from the tree view imported as its components. This type does not support reimporting.
-   **Actors**: This option will import each of the assets in the tree view as individual Actors. This type does not support reimporting.



 |

### Static Meshes Tab

The Static Meshes tab contains all options for importing the various Static Meshes found in your FBX scene file. On the left is a list of all of the included meshes, where you can uncheck meshes you do not want imported. On the right are the Static Mesh import options. This tab includes the ability to create presets of import options that can be quickly applied to groups of Static Meshes in the list view. The options found are similar to those in the standard [Static Mesh import options](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine).

The Static Meshes tab also includes the ability to create sets of override options, which will be covered in the [Option Overrides](/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine#optionoverrides) section.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f17b8b92-ad26-492a-bb4f-a47d8f2ad58f/staticmeshestab.png)

### Skeletal Meshes Tab

The Skeletal Meshes tab will show all of the Skeletal Meshes being imported into the scene from your FBX file. On the left is a list of all the included Skeletal Meshes. As with the Static Meshes tab, you can uncheck any meshes you do not want to import. The right side contains a list of options for each of the Skeletal Meshes being imported, and is very similar to the standard [Skeletal Mesh import options](/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine).

The Skeletal Meshes tab also includes the ability to create sets of override options, which will be covered in the [Option Overrides](/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine#optionoverrides) section.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be172ceb-12b6-4cd7-985f-19cef4c92e03/skeletalmeshestab.png)

### Materials Tab

The Materials tab enables control over the materials that are being imported into your scene along with your FBX file. You can also **Right-click** on an existing material from the FBX file and replace it with an existing one in your project.

Keep in mind that the FBX importer never allows you to override materials that already exist in the project. You can only assign existing materials to replace those in the FBX, or it will create new materials with basic texture hookups.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76cf7e8c-d2b4-489e-8175-7a462ad1f054/materialstab.png)

Also on the Materials Tab you can override the location of where to save all Materials. Click the **Browse** option and define where in your project you would like to import your Materials to.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95f2005d-4c3c-41b4-9d0c-2981ed6a6ecf/materialbasepath.png)

### Option Overrides

Option overrides can be used to group sets of import options into a named set, which can then be applied to multiple assets simultaneously. This allows users to quickly create sets of common options for groups of meshes, rather than having to set them all one at a time.

To create and apply an option override:

1.  Click the Create Override button found in either the Static Meshes or Skeletal Meshes tab.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0380b64-5ba8-4bce-86c4-90e31cacf124/overridebutton.png)
2.  Enter a name for the new override.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e37e280-c23e-484f-81a6-9604d9bbde61/namedoverride.png)
3.  With the new override selected from the dropdown at the top of the options list, set your desired options.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0eda55fb-4726-485a-8e68-705b2cd11cd6/settingoptions.png)
4.  Select any number of meshes from the list on the left of the tab, then **Right-click** and choose your new override from the context menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8facf2f1-d55d-4c1f-b2a6-10e11a0f6796/selectoverride.png)

You may also remove any selected override by clicking the Delete button, located above the options list.

## Full Scene Reimporting

If you have imported your scene as a Blueprint object, you also have the ability to do a full scene reimport. This works very similarly to the full scene import functionality, but also tells you what components of your FBX scene have been added, removed, or edited. Using full scene reimport, it is easy to return to your DCC app, make any desired changes, and then bring your complete scene back into Unreal, selectively applying only the changes you wish to update.

### Scene Reimport Workflow

To reimport your scene **Right-click** on the **FBX Scene Import Data** asset (or any assets imported by a previous scene import) and choose **Reimport** from the context menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/847db9fa-fd9b-4dc9-a084-0fede9055377/reimportmenu.png)

This will open the FBX Scene Reimport Options dialog. This dialog is similar to the FBX Scene Import options, but will also show any assets that have been removed (their icons will have a minus sign) and assets which have been added (their icons will have a plus sign). The scene asset tree view can also be filtered to show you which assets in your FBX scenes have been added, removed, or changed.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/848e5606-d301-4ec5-aaca-a8e09aa8408c/reimportaddremove.png)

The dialog consists of the same four tabs as before:

-   Scene
-   Static Meshes
-   Skeletal Meshes
-   Materials

### Reimport List Filter Buttons

All of the tabs of the FBX Scene Reimport Options dialog contain a series of filters for quick access to changed assets. These filters include:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9aa20a58-65ef-4df8-98d8-279348b8a0ea/filters.png)

| Option | Description |
| --- | --- |
| **Add** | This will automatically create a folder representing each tier in the hierarchy. The folder will be named after the first item found at that hierarchy level. |
| **Delete** | This only shows those assets in the FBX scene that have been removed since the last import. |
| **Overwrite** | This shows only assets that will be overwritten from the last import. |
| **Diff** | This shows only assets that are different (added or deleted) from the last import. |

### Reimport Scene Tab

The Reimport Scene tab is essentially the same as the Scene tab from the original Import Into Level operation. However, a key difference is the ability to reimport the hierachy. When the Reimport Hierarchy checkbox (found at the top of the Options group) is checked, this re-imports the Blueprint's hierarchy, causing you to lose any changes you've made to the Components list of the Blueprint. Any node graph changes you make to the Blueprint will be maintained.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/665431e7-2a15-4cb8-a519-5afe31a328d5/reimportscene.png)

### Reimport Static Meshes Tab

The Reimport Static Meshes Tab shows offers the same functionality as the standard [Static Meshes Tab](/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine#staticmeshestab) found in the FBX Scene Import Dialog, now applied to meshes being reimported. You can also filter the results using the [Filter Options](/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine#reimportlistfilterbuttons).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04d9f020-49d4-4d35-9f6f-760edffbb906/reimportsm.png)

### Reimport Skeletal Meshes Tab

The Reimport Skeletal Meshes Tab shows offers the same functionality as the standard [Skeletal Meshes Tab](/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine#skeletalmeshestab) found in the FBX Scene Import Dialog, now applied to meshes being reimported. You can also filter the results using the [Filter Options](/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine#reimportlistfilterbuttons).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea817b51-df68-4294-bdc9-634823f68f46/reimportsk.png)

### Reimport Materials Tab

The Reimport Materials Meshes Tab shows offers the same functionality as the standard [Materials Tab](/documentation/en-us/unreal-engine/fbx-scene-import-in-unreal-engine#materialstab) found in the FBX Scene Import Dialog, now applied to materials that are a part of the FBX scene being reimported.

Remember that the importer will never overwrite existing Materials!

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14e997f6-4487-44f4-b058-2278b63d6c54/reimportmats.png)