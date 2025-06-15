# Working with Meshes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-meshes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-meshes-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:48

---

**Modeling Mode** is an editor mode that provides you with the tools to create and edit your own 3D mesh directly in Unreal Engine. Although Modeling Mode works similarly to other modeling software, there are a few key differences in how the editor mode creates new meshes and handles editing that you should know before you begin working with it.

#### Prerequisite Topics

To better understand and use the content of this page, familiarize yourself with Modeling Mode by reading the [Modeling Mode Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine) documentation.

## Output Type

You can create a new mesh using the tools found in the **Shapes** or **Create** categories of the Modeling Tools palette:

[![Create a new mesh in modeling mode](https://dev.epicgames.com/community/api/documentation/image/7dd3a356-0fa4-4d20-a55d-b91a6a97d8a9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7dd3a356-0fa4-4d20-a55d-b91a6a97d8a9?resizing_type=fit)

Unreal Engine uses the **Output Type** specified in the **Modeling** panel when creating a new mesh. Output types that are not supported by the selected tool are grayed out.

[![Change Output Type in Modeling Mode](https://dev.epicgames.com/community/api/documentation/image/b616f399-4022-46a6-bdce-61ce94e67674?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b616f399-4022-46a6-bdce-61ce94e67674?resizing_type=fit)

### Static Mesh

A [Static Mesh](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-actors-in-unreal-engine) is a type of **Actor** that represents 3D geometry. When you select Static Mesh as the type, the Actor is saved in your **Content Browser** as an **Asset**, and an Actor instance is placed in the Level.

[![Static Mesh Instance in Modeling Mode](https://dev.epicgames.com/community/api/documentation/image/a784c7d7-4362-42f2-8e0b-4344f5fa3d50?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a784c7d7-4362-42f2-8e0b-4344f5fa3d50?resizing_type=fit)

When you accept new edits, the original Static Mesh is updated. These updates apply to any duplicates made in the **Viewport**, as they are an instance of the same mesh.

To properly create a copy saved separately in the Content Browser, you can use the **MshDup** (Mesh Duplicate) tool. Using this tool to clone your Static Mesh before you start modeling will ensure that the original Asset remains intact and make it possible to change only individual Static Meshes in your world as needed.

Modeling Mode saves new Static Mesh based on the settings in the Modeling Mode section of the [Project Settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-meshes-in-unreal-engine#modeling-mode-project-settings). You can quickly customize settings using the [New Asset Location](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-meshes-in-unreal-engine#modeling-mode-quick-settings) property in the Modeling Mode Quick Settings.

### Dynamic Mesh

A [Dynamic Mesh](https://dev.epicgames.com/documentation/en-us/unreal-engine/geometry-scripting-users-guide-in-unreal-engine) is an Actor that visually represents a Static Mesh; however, their functions differ. Dynamic Meshes are saved in the **Level** instead of the Content Browser since it is not an [Asset](https://dev.epicgames.com/documentation/en-us/unreal-engine/assets-and-content-packs-in-unreal-engine).

Dynamic Meshes can help you create an efficient workflow by saving time on editing because:

-   No **Build** step is required
    
-   No Asset is created
    
-   You can edit duplicates without updating the original mesh
    

There are a few caveats to know when using Dynamic Meshes:

-   It is not efficient for rendering and memory.
    
-   It is not compatible with **Lumen** or **Nanite**.
    

You can use the **Convert** tool to change a Dynamic Mesh to a Static Mesh or Volume, and vice versa. This conversion option is beneficial when you are editing a high-resolution mesh with a long Build time after a tool operation.

### Volume

A **Volume** is a type of Actor you can use to alter the behavior of areas in your Level. When selected, the standard **Volume Types** become available.

To learn about the Volume Types, refer to the [Volume Actors in Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/volume-actors-in-unreal-engine) documentation.

When creating a new Volume using either the Shapes or Create category, the mesh appears similar to a Static or Dynamic Mesh. Once you select Accept, the mesh is represented as a traditional Volume (a 3D outline).

## Preview Mesh

After you create a mesh and accept it, your shape is ready for editing. When you edit a mesh using Modeling Mode, the original mesh is hidden and replaced with a preview mesh (Dynamic Mesh Actor). The Dynamic Mesh Actor becomes a container that holds the changes to your mesh until you click the **Accept** button. Once you accept the changes, Modeling Mode applies the changes and overwrites the existing target output mesh.

While the tool is active, the original mesh can be unhidden by toggling the **Visible** property under the **Rendering** category in the **Details** panel. Once the changes are accepted, they are applied to the existing target output mesh. The preview mesh is destroyed, and the original mesh Actor is unhidden.

### Exceptions

Some tools give you the option to overwrite the existing mesh or create new meshes directly. Here are some examples:

-   Mesh Merge (MshMrg)
    
-   Mesh Bool (MshBool)
    
-   Trim
    
-   Merge
    
-   Vox Wrap
    
-   Vox Blend (VoxBlnd)
    
-   Vox Morph (VoxMrph)
    

[![Write to settings drop down](https://dev.epicgames.com/community/api/documentation/image/365d500b-13c5-4fef-828a-9bdb1b61956f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/365d500b-13c5-4fef-828a-9bdb1b61956f?resizing_type=fit)

Click image for full size.

These tools give you the option to create a **New Object** using the result of your edit or to overwrite the **First Input Object** or **Last Input Object**.

There are also tools that create non-mesh Assets. The **Baking** tools create Texture Assets and saves them in the selected location.

## Modeling Mode Project Settings

There are several options for Modeling Mode in the Project Settings you can use to configure the creation and selection of meshes, as well as the saving of Assets. They are found in the **Plugins > Modeling Mode** and **Plugins > Modeling Mode Tools** sections.

[![Modeling Mode Project Settings](https://dev.epicgames.com/community/api/documentation/image/cd42be00-5246-4ad8-827f-04a0415bf0e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cd42be00-5246-4ad8-827f-04a0415bf0e0?resizing_type=fit)

Click image for full size.

| Property | Description |
| --- | --- |
| 
**Default Mesh Object Type**

 | 

Determines the default mesh type for Modeling Mode tools. Requires an Editor restart to take effect. The following options are available:

-   **Static Mesh Asset**
    
-   **Volume Actor**
    
-   **Dynamic Mesh Actor**
    

 |
| 

**Asset Generation Location**

 | 

Determines where assets generated by Modeling Mode tools are stored by default.The following options are available:

-   **Auto Generated World Relative Asset Path**: Stores assets in an auto-generated folder relative to the level they are being saved in.
    
-   **Auto Generated Global Asset Path**: Stores assets in an auto-generated folder located in the Content folder of your project.
    
-   **Current Asset Browser Path if Available**: Stores assets in the folder currently selected in the Content Browser, if available. If not, assets are saved in the auto-generated asset path.
    

 |
| 

**Asset Generation Mode**

 | 

Determines how assets generated by the Modeling Mode tools are handled. The following options are available:

-   **Auto Generate and Autosave**: Generates and automatically saves new assets on creation.
    
-   **Auto Generate But Do Not Autosave**: Generates new assets and marks them as modified.
    
-   **Interactive Prompt to Save**: Generates new assets and prompts you to save them.
    

 |
| 

**Asset Generation Asset Path**

 | 

Defines the file path where auto-generated assets are saved. This is relative to the parent path defined in the **Asset Generation Location**. Leaving this blank disables this option.

 |
| 

**Store Unsaved Level Assets in Top Level Game Folder**

 | 

If enabled, determines whether auto-generated assets in an unsaved level are stored relative to the top level **Game** folder or are stored in the **Temp** folder. You cannot save assets stored in the **Temp** folder until they are moved to a permanent location.

 |
| 

**Use Per User Autogen Subfolder**

 | 

If enabled, determines if auto-generated assets are stored in specific user folders within the auto-generated folder.

 |
| 

**Autogen Subfolder User Name Override**

 | 

Overrides the user name used for per-user folders within the auto-generated folder.

 |
| 

**Append Random String to Name**

 | 

Appends a short, random string to the name of auto-generated assets.

 |
| 

**Enable Persistent Selections**

 | 

If enabled, maintains your selection when changing between tools. This feature is Experimental and is disabled by default.

 |

[![Modeling Mode Tools Project Settings](https://dev.epicgames.com/community/api/documentation/image/28c8507b-b6eb-4fa0-a61b-a60765655da2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/28c8507b-b6eb-4fa0-a61b-a60765655da2?resizing_type=fit)

Click image for full size.

| Property | Description |
| --- | --- |
| 
**Enable Ray Tracing While Editing**

 | 

Enables Ray Tracing when using Modeling Mode tools. This affects the performance of tools with real time feedback, such as 3D Sculpting.

 |
| 

**Enable Ray Tracing**

 | 

Enables Ray Tracing for new assets created using the Modeling Mode tools, if support is optional.

 |
| 

**Enable Collision**

 | 

Enables collision for new meshes created using the Modeling Mode tools.

 |
| 

**Collision Mode**

 | 

Determines the default Collision Mode for new meshes created using the Modeling Mode tools. The following options are available:

-   Project Default
    
-   Simple and Complex
    
-   Use Simple as Complex
    
-   Use Complex as Simple
    

For more information on these settings, refer to [Simple versus Complex Collision](https://dev.epicgames.com/documentation/en-us/unreal-engine/simple-versus-complex-collision-in-unreal-engine).

 |

## Modeling Mode Quick Settings

The **Modeling Mode Quick Settings** are located at the bottom of the Modeling Tools Details panel and contain options for specifying the LOD to display during editing and the location to save new Assets.

[![Modeling Mode Quick Settings](https://dev.epicgames.com/community/api/documentation/image/3728e969-e40f-4690-bc5e-18dbcadeffa7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3728e969-e40f-4690-bc5e-18dbcadeffa7?resizing_type=fit)

Click image for full size.

| Property | Description |
| --- | --- |
| 
**Editing LOD**

 | 

Determines which LOD mesh you are currently editing.

 |
| 

**New Asset Location**

 | 

Determines where the new Asset you are currently creating will be saved. This overrides the current project setting for this Asset.

 |