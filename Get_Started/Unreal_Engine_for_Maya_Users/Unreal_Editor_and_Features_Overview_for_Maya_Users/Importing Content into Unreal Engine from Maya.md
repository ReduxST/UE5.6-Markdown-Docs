# Importing Content into Unreal Engine from Maya

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-content-into-unreal-engine-from-maya](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-content-into-unreal-engine-from-maya)  
**Processed:** 2025-06-14 16:30:15

---

Importing contents, such as textures, meshes, animations or anything supported by Unreal Engine, is a fairly straightforward process. However, there are critical details and best practices you should know to ensure smooth workflows and assets that are optimized for a real-time engine, like Unreal Engine.

There are several direct ways to you can import content into Unreal Engine: 

-   **Drag and Drop** the assets directly into the Content Browser folder.
    
-   Using the Content Browser’s **Import** button.
    
    [![Unreal Editor Content Browser Import](https://dev.epicgames.com/community/api/documentation/image/9fe0aac5-ec23-4236-bf36-c416c9638531?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9fe0aac5-ec23-4236-bf36-c416c9638531?resizing_type=fit)
    
-   Using the right-click context menu and choosing the **Import to Current Folder** option.
    
    [![Unreal Editor Import To Current Folder](https://dev.epicgames.com/community/api/documentation/image/d2c3ea61-0a2e-4542-9c8e-7673489e726a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d2c3ea61-0a2e-4542-9c8e-7673489e726a?resizing_type=fit)
    

When supported content is imported, the **Import Content** dialog appears. Use this dialog to apply any general settings or specific ones to the type of content you’re importing. 

[![Unreal Editor Import Content Dialog](https://dev.epicgames.com/community/api/documentation/image/3b298314-750c-48e0-8019-c75bf5f222a3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3b298314-750c-48e0-8019-c75bf5f222a3?resizing_type=fit)

Import Content Dialog

For more information on general content import workflows into Unreal Engine, see [Importing Assets Directly](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine).

## Preparing your Content for Unreal Engine

When it comes to preparing your content to import into Unreal Engine, there are a few things to keep in mind with how the engine handles things. There are also some considerations you need to make depending on where you’re exporting your content from. 

For Maya users starting to integrate their content workflow into one with Unreal Engine, you should keep the following things in mind: 

-   Clean Geometry Practices
    
-   Scaling and Units
    
-   Pivots and Scene Origin
    
-   Textures Preparation
    
-   FBX Export Settings
    
-   Naming conventions
    

Use the sections below to familiarize yourself with how Unreal Engine looks at imported content with additional context. 

### Supported File Formats for Unreal Engine

Unreal Engine supports a broad range of file formats, supporting most content you would want to import into your project. Below are the most common formats used for different types of files and purposes:

Some file types require a plugin for their importer to be enabled in Unreal Engine. For example, Universal Scene Description (USD) for large collaborative scenes and Alembic files for hair grooms.

You enable these file type importers in the **Plugins** browser found under the main menu in the **Edit** menu.

| File Type | File Extension | Recommended Uses |
| --- | --- | --- |
| Geometry - Static Mesh |  |  |
| --- | --- | --- |
| 
**FBX** 

 | 

`.fbx`

 | 

The recommended format for geometry, animations, and skeletal meshes.

 |
| 

**OBJ**

 | 

`.obj`

 | 

Works best for static geometry but doesn’t handle animations.

 |
| 

**Universal Scene Description (USD)**

 | 

`.usd`

 | 

Useful for large complex scenes and for collaboration with teams. Requires the **USD Importer** plugin to be enabled. For more information on using them, see [Universal Scene Description](https://dev.epicgames.com/documentation/en-us/unreal-engine/universal-scene-description-usd-in-unreal-engine).

 |
| Geometry - Skinned Mesh, Skeleton, and Animations |  |  |
| --- | --- | --- |
| 

**FBX**

 | 

`.fbx`

 | 

The recommended format for geometry, animations, and skeletal meshes.

 |
| 

**OBJ**

 | 

`.obj`

 | 

Works best for static geometry but doesn’t handle animations.

 |
| 

**Alembic**

 | 

`.abc`

 | 

Works for complex animation caches, hair, cloth, or vertex animations. Requires the **Alembic Groom Importer** plugin to be enabled. For more information, see [Alembic File Importer](https://dev.epicgames.com/documentation/en-us/unreal-engine/alembic-file-importer-in-unreal-engine).

 |
| 

**Universal Scene Description (USD)**

 | 

`.usd`

 | 

Useful for large complex scenes and for collaboration with teams. Requires the **USD Importer** plugin to be enabled. For more information on using them, see [Universal Scene Description](https://dev.epicgames.com/documentation/en-us/unreal-engine/universal-scene-description-usd-in-unreal-engine).

 |
| Images - Texture, Cubemap, and Light Profiles |  |  |
| --- | --- | --- |
| 

**PNG**

 | 

`.png`

 | 

This is a lossless format that preserves transparency that can be highly compressed. This is used for textured surfaces and for channel packing with grayscale different image data stored in RGB channels. 

 |
| 

**Targa**

 | 

`.tga`

 | 

This is a lossless format that preserves transparency while avoiding potential issues of PNG. It is uncompressed, which can also speed up loading and editing. 

 |
| 

**JPG**

 | 

`.jpg` and `.jpeg`

 | 

This is a lossy format that can be highly compressed. Because of this, it should not be used when creating your source assets. 

 |
| 

**Photoshop**

 | 

`.psd`

 | 

This is a lossless, uncompressed format that retains the source files layers and data. 

 |
| 

**Cubemap**

 | 

`.dds`

 | 

These are compressed or uncompressed files that contain multiple images with various layouts in 2D layouts, 3D volume textures, and cubemaps. These are most commonly used for skyboxes and distance backgrounds.

 |
| 

**HDR Image**

 | 

`.exr`

 | 

This is a high dynamic range (HDR) image format that preserves more color data and brightness variations than other formats like PNG and JPG. This makes it ideal for using these with sky spheres and sky lights.

 |
| 

**Illuminating Engineering Society Light Source Profile**

 | 

`.ies`

 | 

These are defined profiles of lights that describe their distribution from a light source using real-world measured data. For more information on using them, see [IES Light Profiles](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-ies-light-profiles-in-unreal-engine).

 |

### General Maya File Export Considerations

Below is a general list of things you should keep in mind when setting up files in Maya that you’ll later import into Unreal Engine.

| Unreal Engine’s Coordinate System, Scaling, and Units of Measure |
| --- |
| 
-   Unreal Engine uses Centimeters as its default unit of measurement.
    
-   Unreal Engine’s coordinate system is left-handed and uses a Z-up axis
    
    -   The X-axis is Red and faces forward.
        
    -   The Y-axis is Green and faces right.
        
    -   The Z-axis is Blue and faces upwards
        
-   For more information on Unreal Engine’s coordinate system, see [Coordinate System and Spaces](https://dev.epicgames.com/documentation/en-us/unreal-engine/coordinate-system-and-spaces-in-unreal-engine).
    

 |
| Unreal Engine’s Materials, Textures, and UVs |
| --- |
| 

-   **Materials**
    
    -   Maya’s materials must be rebuilt with Unreal Engine’s material system.
        
    -   You can include media, such as textures, with an exported file that can be optionally imported and create a basic material to apply to geometry with diffuse maps, normal maps, and so on mapping to ones in Unreal Engine.
        
-   **Textures**
    
    -   It’s recommended to create and import your textures separately into Unreal Engine.
        
    -   For source files, choose a lossless format to preserve quality during development. For instance, consider the differences of using PNG, TGA, or JPG for textures as an output versus development resource.
        
    -   For texture compression, know that the engine handles compression automatically. However, you can customize compression settings for individual textures using the Texture Asset Editor.
        
    -   For alpha channels, consider how you work with transparency for a material in Unreal Engine and what type of image format you choose. For instance, TGA may handle alpha channels better than PNG in some cases.
        
    -   Consider disk space versus memory usage. Disk space is less critical than memory usage (VRAM) for performance. The engine compresses textures to optimize memory usage.
        
-   **UVs**
    
    -   Ensure all UVs for geometry are laid out in such a way that makes them ideal for applying textures and materials to them. For example, modular geometry may rely heavily on tiled textures and materials whereby you’d overlay the UVs to get higher texel density with a lower resolution texture. For things like characters or unique geometry, you’d want to have unique UVs for most things with no overlapping.
        
        -   If your project is using precomputed (“baked”) lighting, geometry should have no overlapping UVs, otherwise you’ll have visible artifacts on the mesh. To learn more about lightmapping and their UV layouts, see [Understanding Lightmapping in Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine).
            
    -   UDIM workflows are supported with Virtual Texturing features. To learn more about UDIM support in the engine, see [Virtual Texturing](https://dev.epicgames.com/documentation/en-us/unreal-engine/streaming-virtual-texturing-in-unreal-engine#udim-support).
        

 |
| Skinned Meshes, Skeletons, and Animations |
| --- |
| 

-   **Skinned Meshes**
    
    -   Ensure bones and joints are properly skinned and named clearly. Unreal Engine imports skeletal structures for animation.
        
    -   Clean Skeleton with one root and no scaling on joints.
        
-   **Animations**
    
    -   Export animations separately or bundled together in the same FBX file.
        
    -   Blend Shapes (Morph Targets) should be exported with Deformed Models checked to include this morph data.
        
    -   Unreal Engine uses root motion, make sure your rig and animation support this, if needed.
        

 |
| General |
| --- |
| 

-   **Export Clean Up Practices**
    
    -   Center an object’s pivot point to the world origin (0,0,0) on export from Maya. Unreal Engine uses this as the pivot point location on the mesh during import. Geometry offset from the world origin will have an offset pivot point from its geometry. This can make working with assets in Unreal Engine more difficult.
        
    -   Freeze transformations and delete history.
        
    -   Ensure proper naming conventions for meshes, joints, and materials.
        
    -   Remove unused nodes or hidden objects.
        
-   **Level of Detail (LODs)**
    
    -   You can manually set up LODs for geometry in Maya, but there are auto-generation tools you can use for static and skeletal meshes in Unreal Engine to do this for you. 
        
-   **Nanite**
    
    -   Nanite supports high polygon meshes without requiring decimation. It supports both static and skeletal meshes.
        
        -   For more information on using Nanite with meshes, see [Nanite Virtualized Geometry](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine). 
            

 |

### Maya Static Mesh Export Considerations

When exporting a Static Mesh as FBX from Maya, set the following options in the export dialog:

-   Geometry Only
    
-   Smoothing Groups: Enabled
    
-   Tangents and Binormals: Enabled
    
-   Triangualate: Enabled
    
-   Animation: Disabled
    
-   Embed Media: Optional
    

When importing a Static Mesh as FBX into Unreal Engine, set the following options in the import dialog:

-   \[Optional\] Generate Lightmap UVs: Checked
    
    -   Ideal if using baked precomputed lighting.
        
-   Import Materials: checked
    
-   Apply Collision
    

For more information on importing Static Meshes into Unreal Engine, see the following: 

-   [Importing Static Meshes using FBX](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-static-meshes-using-fbx-in-unreal-engine)
    
-   [Importing Static Meshes](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-static-meshes-in-unreal-engine)
    
-   [FBX Material Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-material-pipeline-in-unreal-engine)
    

### General Maya Skinned Mesh Export Considerations

When exporting a Skeletal Mesh as FBX from Maya, set the following options in the export dialog:

-   Include the following with the export:
    
    -   Geometry
        
    -   Animation
        
    -   Skeleton Definitions
        
-   Smoothing Groups: Enabled
    
-   Tangents and Binormals: Enabled
    
-   Triangualate: Enabled
    
-   Animation: Enabled
    
-   Embed Media: Optional
    
-   Deformed Models: Enabled
    
    -   Skins: Enabled
        
    -   Blend Shapes: Enabled
        

When importing a Skeletal Mesh as FBX into Unreal Engine, set the following options in the import dialog:

-   Import the Skeleton FBX first with no animation.
    
    -   Enable Import Mesh
        
    -   Enable Import Skeleton
        
-   Import the Animation(s) separately and choose their skeleton when prompted.
    
-   Import the Morph Targets (Blend Shapes).
    
-   Check Import materials to create the basic material if media is included in the FBX import.
    

For more information on importing Skeletal Meshes into Unreal Engine, see the following: 

-   [Skeletal Meshes Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)
    
-   [Importing Skeletal Meshes Using FBX](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-skeletal-meshes-using-fbx-in-unreal-engine)
    
-   [FBX Material Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-material-pipeline-in-unreal-engine)
    
-   [Alembic File Importer](https://dev.epicgames.com/documentation/en-us/unreal-engine/alembic-file-importer-in-unreal-engine)
    
-   [Importing Grooms](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-grooms-into-unreal-engine)
    

## Next Page

[

![Using Materials and Textures in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/709cd0c1-cc2e-43c7-bc6e-6789097e0210?resizing_type=fit&width=640&height=640)

Using Materials and Textures in Unreal Engine for Maya Users

An overview of Unreal Engine's Material System and Textures for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-materials-and-textures-in-unreal-engine-for-maya-users)