# Importing Static Meshes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-static-meshes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-static-meshes-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:30

---

Many tools within **Unreal Engine** can help you create assets for your **Levels**. However, there may come a time when you have to create an asset in an exterior application and import it into Unreal Engine. In this tutorial, you will learn the basics of importing a Static Mesh, made in another 3D application, into the engine for placement in your Levels.

## Set Up

To make sure the transition from your 3D modeling software, whether it be Maya, 3ds Max, or some other modeling program, is successful there are a few things to check:

-   The size of your model will scale as intended to Unreal Engine's measurement of Unreal Units, where 1 Unreal Unit equals 1 centimeter.
    
-   Your mesh is exported as an FBX, the recommended file format for 3D objects.
    
-   Any textures and materials applied to your static mesh are supported file types.
    

To learn more about supported file types, refer to [FBX Content Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-content-pipeline) and [Textures](https://dev.epicgames.com/documentation/en-us/unreal-engine/textures-in-unreal-engine) documentation.

You can skip this step if you have a project you are already working on. However, if you need a project to work with, open the launcher and create a new project. For more information on creating projects in Unreal Engine, see [Creating a New Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-a-new-project-in-unreal-engine).

The project category and template you choose and whether or not you have included **Starter Content** will not matter for this tutorial.

## Exporting

After you complete your model, the first step towards importing it into the engine is exporting it from the 3D application used to create the mesh.

This example will cover exporting this sphere model from Maya into your Level. However, feel free to use any application that can export FBX files. To get started, follow these steps:

[![Sphere Model](https://dev.epicgames.com/community/api/documentation/image/92edcba2-9f72-4a18-8fc0-be487b0a8d37?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/92edcba2-9f72-4a18-8fc0-be487b0a8d37?resizing_type=fit)

Click image for full size.

1.  Go to the file menu in your respective application and select **Export**.
    
    [![Maya File Menu](https://dev.epicgames.com/community/api/documentation/image/261283e9-92af-4fbe-8426-8c8edeb512d1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/261283e9-92af-4fbe-8426-8c8edeb512d1?resizing_type=fit)
    
    Click image for full size.
    
2.  Choose the path where you want to save your mesh. Make sure to give it a name and select the appropriate file type.
    
    [![Export All](https://dev.epicgames.com/community/api/documentation/image/3e9dac6a-9e4c-48d3-bb3c-b37449e2c35c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3e9dac6a-9e4c-48d3-bb3c-b37449e2c35c?resizing_type=fit)
    
    Click image for full size.
    

## Import

Now that you exported your mesh from the 3D application, you will need to import it into your project. Follow these steps to get started:

1.  Within your project, locate your **Content Browser**. Browse through the folders there to choose where to import your mesh.
    
    -   In this example, the sphere mesh, shown below, was imported into a folder labeled **Meshes**.
        
2.  Once you are in the folder you want to save your mesh to, import your mesh by doing one of the following:
    
    -   **Right-clicking** in an empty space within your folder and selecting **Import to...** from the context menu.
        
    -   Clicking the Import button at the top of the **Content Browser**.
        
        [![Import Content Browser](https://dev.epicgames.com/community/api/documentation/image/fbce2a99-66e4-4c58-9b19-a149f431a428?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fbce2a99-66e4-4c58-9b19-a149f431a428?resizing_type=fit)
        
        Click image for full size.
        
3.  In the pop-up Window, browse to find your exported mesh. When you find your mesh, you can import it by either **double-clicking** it or clicking **Open**.
    
    [![Open FBX](https://dev.epicgames.com/community/api/documentation/image/85cdf152-b1f1-4c41-8148-de27c3cddd9f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/85cdf152-b1f1-4c41-8148-de27c3cddd9f?resizing_type=fit)
    
    Click image for full size.
    

### FBX Import Options

After you have selected the mesh to import, the **FBX Import Options** menu will appear. By default, it will look very similar to the image below.

[![Import Options Default](https://dev.epicgames.com/community/api/documentation/image/c881d4a4-97df-4496-a02f-a61560ad7c66?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c881d4a4-97df-4496-a02f-a61560ad7c66?resizing_type=fit)

Click image for full size.

However, there are many other options that you can play with when importing your mesh. To learn more about these options, refer to [FBX Import Options Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-import-options-reference-in-unreal-engine).

[![Import Options Expanded](https://dev.epicgames.com/community/api/documentation/image/52a6cf93-4903-4284-9cd0-2281a9239a01?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/52a6cf93-4903-4284-9cd0-2281a9239a01?resizing_type=fit)

Click image for full size.

For this example, all of the defaults are fine and you can import the mesh the way it is.

The process is very similar if you have a mesh that you want to import as a **Skeletal Mesh**. You need to select the first checkbox, *Skeletal Mesh*, in the Mesh section.

To finish the process, you can do one of the following:

-   Click **Import**, allowing you to choose the Import Options for each individual mesh.
    
-   Click **Import All**, importing all the meshes with the same options.
    

If you imported more than one mesh, after you click **Import**, another **FBX Import Options** menu would appear. As you only imported one mesh in this example, clicking **Import** or **Import All** yields the same result and brings you back to your **Content Browser**.

## Saving Imported Assets

In the **FBX Import Options**, **Materials** and **Import Textures** are checked to true by default. Any materials or textures applied to your model from your 3D application will be imported into the engine.

The colored bars on the bottom of the thumbnail tell you what type of Asset it is. Your Static Mesh is the Asset with the light blue bar at the bottom.

[![After Mesh Is Imported](https://dev.epicgames.com/community/api/documentation/image/7a2bdf39-d6a6-4909-838f-be297e30e993?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7a2bdf39-d6a6-4909-838f-be297e30e993?resizing_type=fit)

Click image for full size.

After checking all your Assets have been properly imported, you need to save them. Click the **Save All** button in the **Content Browser's** menu bar to save the imported Assets.

The asterisks on your Asset icon are now gone, indicating a successful save.

Unreal Engine will save your imported Assets as .uasset in your project folder.

With your mesh imported into Unreal Engine and saved, you can now use it in your Level. To implement your mesh into your Level, refer to [Placing Actors](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine).