# Sparse Volume Textures

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:47

---

A **Sparse Volume Texture** (SVT) is a texture that stores texels (voxels) in a 3D data structure. You can index SVTs' data with three-dimensional UV coordinates, similar to 3D textures and volume textures. Unlike standard (dense) Volume Textures, SVTs only spend memory on regions of the volume with "interesting" data (those in which voxel data is present), allowing for much larger volumes, or even ones with the same extents, to use less memory when compared to the density of standard volume textures.

## Types of Sparse Volume Textures

You can use static or animated volumes to represent Sparse Volume Textures. A static SVT is a single volume, whereas an animated SVT is a sequence of volumes (or frames) that can be played back, similar to a flipbook animation.

These SVTs are rendered using Heterogeneous Volume Actors. For more information on using them, see [Heterogeneous Volumes](https://dev.epicgames.com/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine).

## Composition of Sparse Volume Textures

Sparse Volume Textures are made up of multiple textures. These include a **Page Table** texture that serves as an indirection into **Physical Tile Data** textures that make up the volume. These tile data textures store the texture data for the volume, and they can use up to two textures to store data and attributes of the volume, stored as Attributes A and B.

Attributes A and B each use the RGBA texture channels to store data, giving you up to eight channels to store data in. The data is retrieved through texture lookups — one lookup for the page table and one lookup per physical tile data for two or three lookups total, depending on the SVT. This means that SVTs share a single page table lookup for both physical tile data textures instead of having a one-to-one relation of page table to tile data texture.

The two tile data textures of SVTs (Attributes A and B) can have different pixel formats — 16bit, 32bit, and 8bit unorm. When you don't use one of the RGBA texture channels in one of the Attributes list, there is an attempt to use a pixel format with fewer channels. If you don't use any channel, the texture costs no memory.

| Texture Format | Texture | Unreal Engine Representation |
| --- | --- | --- |
| 
**Page Table**

 | 

[![Page Table](https://dev.epicgames.com/community/api/documentation/image/36eae753-7117-489f-b4c6-a13abcb82a7a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/36eae753-7117-489f-b4c6-a13abcb82a7a?resizing_type=fit)



 | 

[![Page Table UE Representation](https://dev.epicgames.com/community/api/documentation/image/fa8f1ca4-b3d5-4712-94b0-1451af936d3d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fa8f1ca4-b3d5-4712-94b0-1451af936d3d?resizing_type=fit)



 |
| 

**Physical 3D Tiles**

 | 

[![Physical 3D Tiles](https://dev.epicgames.com/community/api/documentation/image/0ab58099-a4c7-4c27-8b69-faf11a340fa5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0ab58099-a4c7-4c27-8b69-faf11a340fa5?resizing_type=fit)



 | 

[![Physical 3D Tiles UE Representation](https://dev.epicgames.com/community/api/documentation/image/bc253ff4-42b7-4fd2-b84d-db8da4d94fd5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bc253ff4-42b7-4fd2-b84d-db8da4d94fd5?resizing_type=fit)



 |

## Ways to view Sparse Volume Textures

You can work with Sparse Volume Textures in the following ways:

-   Volume-Domain Materials
    
    -   [Heterogeneous Volume actor](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine)
        
    -   [Volumetric Fog](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine)
        
    -   [Volumetric Clouds](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine#volumetric-clouds)
        
-   [Sparse Volume Texture Viewer](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine)
    

## Heterogeneous Volume Actor and Component

Heterogeneous Volumes are placeable actors that leverage SVTs by incorporating Sparse Volume Texture material nodes in their volume domain materials. This actor-type renders the SVTs and its attributes using logic setup in its material. Heterogeneous Volume actors can also play and loop animated SVTs without any additional setup required.

Heterogeneous volume rendering is partly limited by deferred rendering features for real-time. However, the [Path Tracer](https://dev.epicgames.com/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine) offers more complete support for rendering volumes, such as accurately simulating scattering, shadows and global illumination.

For more information and details on usage and setup, see [Heterogeneous Volumes](https://dev.epicgames.com/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine).

### Volumetric Fog

SVTs support [Volumetric Fog](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine), a feature of Exponential Height Fog, when its volume domain material is applied to a mesh. SVTs can have a higher amount of detail than the volumetric fog's resolution, so it's possible to see discrepancies when using this method over a Heterogeneous Volume.

[![SVT rendered as volumetric fog.](https://dev.epicgames.com/community/api/documentation/image/b70a1e38-e505-437f-9c09-b38b2809f543?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b70a1e38-e505-437f-9c09-b38b2809f543?resizing_type=fit)

Left, Heterogeneous Volume actor displaying an SVT; Right, an SVT material applied to a mesh and rendered with Volumetric Fog.

To set up volumetric fog with an SVT material, see the [Viewing Sparse Volume Textures with Volumetric Fog](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine) section of this page.

### Volumetric Clouds

SVTs support [Volumetric Clouds](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) automatically when its volume domain material is applied to a Heterogeneous Volume actor.

[![SVT cloud example rendered with Heterogeneous Volume actor.](https://dev.epicgames.com/community/api/documentation/image/155bb5ae-f9b1-4587-8b56-63839f018169?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/155bb5ae-f9b1-4587-8b56-63839f018169?resizing_type=fit)

### Sparse Volume Texture Viewer

The Sparse Volume Texture Viewer is most useful as a previewer and is not optimized, or ideal, for use with the rest of the scene. Instead, the best course of action is to create a material to properly display the SVT and apply that to a [Heterogeneous Volume](https://dev.epicgames.com/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine), or use one of the methods mentioned under [Ways to view Sparse Volume Textures](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine) section.

The **Sparse Volume Texture Viewer** provides a way to preview an SVT asset directly without needing to set up a material. With the viewer, you can preview individual attribute texture channels of the SVT and play its animation, if there is one. This makes the viewer an ideal choice for quickly debugging SVT assets without any required setup.

To use the SVT Viewer, follow these steps:

1.  Drag and drop a **Sparse Volume Texture Viewer** into the scene from the **Place Actors** panel.
    
2.  In the **Details** panel, assign an SVT Asset to the **Sparse Volume Texture Preview** assignment slot.
    

The SVT is displayed within the viewer.

[![SVT Previewer](https://dev.epicgames.com/community/api/documentation/image/344502a1-7891-4953-8df3-729ace419a6c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/344502a1-7891-4953-8df3-729ace419a6c?resizing_type=fit)

Adjust the value of the **Extinction** property to adjust how visible the volume is by setting how much it absorbs light.

For SVTs with more than one frame, use the **Playing** and **Looping** checkboxes to play a loop of the SVT's frames. The **Frame Rate** property specifies how many frames per second (fps) it should play. The previewer is set to 24fps by default. If the Animate property is left unchecked, you can use the **Frame** property value to scrub through the frames in the SVT.

In the image above, left, SVT preview without animation; right, SVT preview looping through its animated frames.

The SVT Viewer only displays a single texture channel at a time. This is useful for inspecting single channels of an SVT asset, and works more or less well depending on the data being stored in the volume texture. Any imported velocity data is displayed as density and will return undesired results.

Use the **Preview Attribute** selection box to choose the Attributes channel you want to preview. The first channel **AttributesA Red** is used by default.

The Sparse Volume Texture Viewer has the following properties:

[![SVT Previewer Settings](https://dev.epicgames.com/community/api/documentation/image/94c6c168-5ca8-42ca-aec6-3c02e32de16b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/94c6c168-5ca8-42ca-aec6-3c02e32de16b?resizing_type=fit)

| Properties | Description |
| --- | --- |
| Asset Preview |   |
| --- | --- |
| 
**Sparse Volume Texture Preview**

 | 

The SVT Asset to be used with the previewer.

 |
| 

**Blocking Streaming Requests**

 | 

Informs the SVT streaming manager to block (wait for) all streaming requests immediately after issuing them. For more information on effectively using this property, see the [Streaming Performance Notes](https://dev.epicgames.com/documentation/en-us/unreal-engine/sparse-volume-textures-in-unreal-engine) section.

 |
| 

**Apply Per Frame Transforms**

 | 

Applies the transform attached to a given Sparse Volume Texture frame. This transform is relative to the transform of the Sparse Volume Texture Viewer component.

 |
| 

**Pivot at Centroid**

 | 

Moves the pivot to the center of the volume. Note that transforms were authored with the pivot being at the origin, which is usually one of the corners of the volume, depending on how it was authored. Forcing the pivot to the volume center may break transforms.

 |
| 

**Voxel Size**

 | 

Uniform scale to apply to all the voxels. This is a quick way of scaling the whole volume to debug scaling related issues.

 |
| 

**Preview Attribute**

 | 

Choose which Attribute is being previewed. Only one can be previewed at a time, even when there are multiple contained within a single SVT.

If the Alpha channel of Attributes A or B is set to **None**, you may see black blocky visuals when previewing them in the viewer. This is because the GPU usually returns 0 for non-existing texture channels, except with Alpha channels, which returns 1 by default. This shouldn't present a problem by leaving it set to **None** because the channel is essentially undefined.



 |
| 

**Mip Level**

 | 

Sets at which mip level to view the SVT.

 |
| 

**Extinction**

 | 

Sets how opaque the volume is. Extinction is the sum of absorption (light rays hitting particles and being absorbed) and scattering (rays hitting particles and scattered/deflected into a different direction that no longer reaches the camera). Higher values appear more opaque than lower values.

 |
| Animation |   |
| --- | --- |
| 

**Frame**

 | 

Enter a value or drag the slider to scrub the frames of the animated SVT. This property is editable when **Playing** is disabled.

 |
| 

**Frame Rate**

 | 

Specify a frame rate that this SVT animation should play. For example, 24, 30, 48, 60. This property is editable when **Playing** is enabled.

 |
| 

**Playing**

 | 

Toggles whether the previewer loops through playback ofplays back the SVT Asset's frames when there are multiple present.

 |
| 

**Looping**

 | 

Loops the animation when **Playing** is enabled.

 |
| 

**Reverse Playback**

 | 

Plays the frames of an animated SVT backwards when **Playing** is enabled.

 |

## Working with Sparse Volume Textures

You can import Sparse Volume Textures from [VDB (or Voxel Data Base)](https://en.wikipedia.org/wiki/OpenVDB#What_does_VDB_stand_for) files. This format is widely used to store sparse volume data. VDB data is converted into a sparse volume representation when imported into Unreal Engine.

VDB files contain so-called "grids" — another name for volumes. These grids can have different types of components, such as density, velocity, and temperature. SVTs support importing grids with the following types: Float (float, float2, float3, float4), Double (double, double2, double3, double4), and Half (half, half2, half3, half4). The resulting SVT resolution is the union of the dimensions of all the imported grids.

While Unreal Engine supports importing VDBs of all types, SVT does not currently support double formats. The data is converted to 8/16/32bit on import.

Each grid can also have its own transform. The VDB format allows for a wide range of transform types, including perspective / frustum transitions. Unreal Engine currently supports transforms with scaling, rotation, and translation. These transforms can vary across frames, so the imported SVT can scale / rotate / translate across its animation timeline.

Although transforms can vary across multiple frames, all transforms of all grids used within a single given frame are expected to be identical.

### Importing VDB Files

You can perform one of the following actions to import a VDB file:

-   Drag and drop the VDB directly into the Content Browser.
    
-   Use the **Import** button in the Content Browser.
    

VDBs have their own import window for importing static and animated VDB files.

When importing an animated VDB file that contains the same name except for their numbered frame, you can import any one of the files from the animated sequence, the importer will recognize it as belonging to a sequence of VDBs. If you were to select all the files in an animated VDB sequence and import all at once, each file would create its own sequence, thus creating multiple identical animated SVTs.

|   |   |
| --- | --- |
| 
[![VDB Import Options Static](https://dev.epicgames.com/community/api/documentation/image/752e74ff-5992-4556-8120-038eb6f398b2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/752e74ff-5992-4556-8120-038eb6f398b2?resizing_type=fit)



 | 

[![VDB Import Options Animated](https://dev.epicgames.com/community/api/documentation/image/4464feff-abcc-4525-9fe0-69bcc4029a44?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4464feff-abcc-4525-9fe0-69bcc4029a44?resizing_type=fit)



 |
| 

SVT Import Options: Static Single Frame VDB

 | 

SVT Import Options: Animated VDB Sequence

 |

The import options include the following information and settings:

| Properties | Description |
| --- | --- |
| 
**Import Static / Animated**

 | 

Displays the type of VDB being imported, static or animated.

 |
| 

**Current Asset**

 | 

The file path of the VDB being imported.

 |
| 

**Import Sequence**

 | 

Imports multiple sequentially labeled VDB files as a single animated Sparse Volume Texture sequence.

Animated SVTs are created when importing a source file that is part of a sequentially numbered sequence VDB files (file0.vdb, file1.vdb, file2.vdb, and so on). The importer automatically detects if a file is part of a sequence and sets the **Import Sequence** checkbox.



 |
| 

**Attributes A**

 | 

Allows the user to assign individual channels from the source grids to the (RGBA) channels of the resulting SVT. Each attribute represents the tile data textures read by the Page Table Texture. The format dropdown next to this property selects which kind of format each tile data texture should use, such as 16bit float , 32bit float, and 8bit unorm. 8bit unorm is used for data or attributes that are in the 0 to 1 range.

 |
| 

**Attributes B**

 | 

Shows the grids present in the source file and allows the user to assign individual channels from the source grids to the (RGBA) channels of the resulting SVT. Each attribute represents the tile data textures read by the Page Table Texture. The format dropdown next to this property selects which kind of format each tile data texture should use, such as 16bit float , 32bit float, and 8bit unorm. 8bit unorm is used for data or attributes that are in the 0 to 1 range.

 |
| 

**Source File Grid Info**

 | 

Displays information about the grids of the VDB file to import, such as the named index, type, and dimensions.

 |

The amount of time it takes to import and create an SVT depends on the dimensions and number of frames of the source VDB file.

A **Sparse Volume Texture** asset is created during the import process. Opening the file reveals information about it, such as the resolution of its volume, number of mip levels, number of frames, and more.

[![Sparse Volume Texture Asset Editor](https://dev.epicgames.com/community/api/documentation/image/117a523b-d305-45bd-90d1-5bbd6eefa3e1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/117a523b-d305-45bd-90d1-5bbd6eefa3e1?resizing_type=fit)

Changing the sampler addressing/tiling method can take some time because it has to regenerate the runtime SVT data.

### Using Sparse Volume Textures in Materials

Materials can sample Sparse Volume Textures using the **Sparse Volume Texture Object** and **Sparse Volume Texture Sample** nodes.

[![SVT Material Nodes](https://dev.epicgames.com/community/api/documentation/image/4a478d75-c945-47f6-9657-c9bffad1b0c8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4a478d75-c945-47f6-9657-c9bffad1b0c8?resizing_type=fit)

You can use SVTs with [Heterogeneous Volumes](https://dev.epicgames.com/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine), [Volumetric Fog](building-virtual-worlds\lighting-and-shadows\environmental-lighting\volumetric-fog), and [Volumetric Clouds](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine). Their materials are set up similarly by setting their Material Domain to **Volume** and their Blend Mode to **Additive**.

The **Sparse Volume Texture Sample** node takes in some UV coordinates (must be three-dimensional) and retrieves the resulting data from Attributes A and Attributes B output pins — both of which are float4. You can use SVTs as parameters in a material graph and can sample them in any type of material. However, they are most useful when used in materials with their material domain set to Volume, such as those with heterogeneous volumes, volumetric fog, and volumetric clouds.

Below is an example of a Volume material sampling an SVT. It is computing the 3D UV coordinates based on world space position — this logic is not specific to SVTs, and is optional. If the UVs input pin is left unassigned, UVs are automatically computed with the same logic as shown in the image below. The SVT sample node has two Float4 outputs (Attribute A and Attribute B), but only the first channel is being used in this example because it contains the density of the SVT being used.

[![SVT Material Example](https://dev.epicgames.com/community/api/documentation/image/c9ac2481-d7db-46d6-9adb-3e8ff6949200?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c9ac2481-d7db-46d6-9adb-3e8ff6949200?resizing_type=fit)

This is an example of the simplest setup you can have for sampling a sparse volume texture in a material.

#### Sparse Volume Texture UV Coordinates

Sparse Volume Textures are sampled with three-dimensional UV coordinates. Like standard 2D textures, the UV space extends from 0 to 1 in all three dimensions (XYZ). The UV space spans along the Volume Resolution property which you can inspect when opening an SVT asset.

The UV space is defined as the union of the bounding boxes of the individual frames. As a consequence of this, there is no need to consider the size of the bounding box when setting up any material logic since the same UV coordinates used on different frames will index into the same world space voxel.

Additionally, you can use the **Texture Property** node to query the texture size and texel size just like you would a 2D texture. You can also query the volume of the SVT from a Blueprint.

#### Sparse Volume Texture Node Mip Values

Sparse Volume Textures Sample nodes support mip values similarly to how other texture sample nodes handle them.

[![Sparve Volume Texture Node Mip Values Settings](https://dev.epicgames.com/community/api/documentation/image/54bb348c-7f94-4e03-a582-d749755e128f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/54bb348c-7f94-4e03-a582-d749755e128f?resizing_type=fit)

#### Engine Source Sparse Volume Material Example

Unreal Engine includes an empty sample SVT material already set up for you to apply your SVT asset to. You can find it in the Content Browser under **Engine > Engine Materials** named **SparseVolumeMaterial**. Make a copy of this material and create an instance of it.

Once you open the material instance, override the **SparseVolumeTexture** parameter and apply your own imported SVT asset to the assignment slot.

### Viewing SVTs with Heterogeneous Volumes

To use SVTs with Heterogeneous Volumes, follow these steps:

1.  Add a **Heterogeneous Volume** actor to the scene.
    
2.  In the **Details** panel, navigate to the **Materials** section.
    
3.  Assign a SVT-based material to the **Element 0** slot.
    

For more information on using Heterogeneous Volumes and its properties, see [Heterogeneous Volumes](https://dev.epicgames.com/documentation/en-us/unreal-engine/heterogeneous-volumes-in-unreal-engine).

### Viewing SVTs with Volumetric Fog

To use SVTs with Volumetric Fog, follow these steps:

1.  Add an **Exponential Height Fog** to your scene.
    
2.  In the **Details** panel, enable **Volumetric Fog**.
    
3.  Apply an SVT material to a mesh.
    
    If you need a mesh, you can use the **Cube** shape in the **Place Actors** panel under the **Shape** category.
    

Because SVTs can have a higher amount of detail than the Volumetric Fog resolution, you may need to scale the mesh up to get better results. Also, you may want to use these console variables to increase the resolution of Volumetric Fog:

-   `r.VolumetricFog.GridPixelSize 4` (Default is 8)
    
-   `r.VolumetricFog.GridSizeZ 256` (Default is 128)
    

### Playing back Animated Sparse Volume Textures

Playing back animated SVTs requires using [Material Instance Dynamics](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui) (MIDs) with Blueprint. An SVTs animation is driven using the **Sparse Volume Texture Parameter** node in its material. This makes it possible to switch out the SVT parameter every tick, with the idea being that each frame of an animated SVT is itself a static SVT.

There are two parts to consider when setting up the logic to animate an SVT:

-   Event BeginPlay constructs an Animated Sparse Volume Texture Controller, which is a class that has functionality for playing back an animated SVT. To facilitate this, it can extract frames from the assigned SVT. The extracted frame also implements the SVT shader interface and can, themselves, be bound to SVT material parameters. An MID is needed in order to update the SVT parameter.
    
-   Event Tick calls for an update on the controller variable, which fetches the current frame and applies it to the Sparse Volume Texture Parameter node in the Material Instance Dynamic.
    

The example that follows demonstrates how to set up a SVT material apply it to a mesh, and rendered with Volumetric Fog. This is just one workflow example. If you want to use Volumetric Clouds or any other use case where you might want to use animated SVTs, you would need to assign the MID to whatever actor or component is used to render the material. For example, with a cloud material, you would update the cloud material of the Volumetric Cloud component.

Heterogeneous Volumes are an exception since its component implements all this logic already, you only need to create the material with an SVT parameter and assign the animated SVT to it. The heterogeneous volume component automatically creates a MID in the background in order to update the SVT parameter.

To set up the Material Instance Dynamic construction Blueprint logic for use with Volumetric Fog, follow these steps:

1.  In your SVT Material, use a **Sparse Volume Texture Sample Parameter** node in the graph.
    
2.  Create an **Actor Blueprint**.
    
3.  In the **Components** panel, click the **Add (+)** button and select a **Cube** mesh from the list.
    
4.  In the **Event Graph**, drag off the **Event BeginPlay** node and add a **Construct Object from Class** node.
    
5.  On the **Construct Object from Class**, set the Class to **Animated Sparse Volume Texture Controller**.
    
6.  On the **Construct Object from Class** node, right-click **Return Value** and choose **Promote to Variable**.
    
7.  In the **My Blueprint** panel under **Components**, rename **NewVar** to "Controller".
    
8.  Drag off the **Set Controller** node and add a **Set Sparse Volume Texture** node.
    
9.  Connect the output pin of the **Set Controller** node to the **Target** input of the **Set Sparse Volume Texture** node.
    
10.  On the **Set Sparse Volume Texture** node, right-click the **Sparse Volume Texture** pin and choose **Promote to Variable**.
    
11.  In the **My Blueprint** panel under **Components**, click on the **Sparse Volume Texture** variable. In the **Details** panel under **Default Value**, set a **Sparse Volume Texture**.
    
    Leaving the **Sparse Volume Texture** slot empty causes the SVT material not to update and play its animation.
    
12.  Drag off the **Set Sparse Volume Texture** node and add a **Play** node.
    
    The Play node causes the Controller to update an internal timer each time you call Update() on the Controller. This timer defines which frame is considered as "current" when extracting the current frame. There are also Pause and Stop nodes that can control the SVT's playback.
    
13.  On the **Set Controller** node, drag off the controller output pin and connect it to the **Target** pin on the **Play** node.
    
14.  Drag off the **Play** node and add a **Create Dynamic Material Instance** node.
    
15.  On the **Create Dynamic Material Instance** node, set the **Parent** dropdown to your **SVT Material**.
    
16.  On the **Create Dynamic Material Instance** node, right-click the **Return Value** pin and choose **Promote to Variable**.
    
17.  In the **My Blueprint** panel under **Components**, rename **NewVar** to "MID".
    
18.  Drag off the **Set MID** node return value pine and add a **Set Material (Cube)** node.
    

This part of the Blueprint logic looks like:

[![SVT Blueprint Animation Logic](https://dev.epicgames.com/community/api/documentation/image/11be0586-9846-47f6-a495-74f6627eb8cd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/11be0586-9846-47f6-a495-74f6627eb8cd?resizing_type=fit)

To set up the Blueprint logic to play each frame of the SVT, follow these steps:

1.  In the **My Blueprint** panel under the **Components**, drag a **Controller** variable into the graph and select **Get Controller**.
    
2.  Drag off the **Controller** node and add an **Update** node.
    
3.  Connect the **Event Tick** execution pin to **Update**.
    
4.  Connect the **Event Tick Delta Seconds** pin to the **Update** node's **Delta Time** pin.
    
5.  Drag off the **Update** node and add a **Get Current Frame** node.
    
6.  Drag off the **Controller** node and connect it to the **Target** pin on the **Get Current Frame** node.
    
7.  In the **My Blueprint** panel under **Components**, drag a **MID** variable into the graph and select **Get MID**.
    
8.  Drag off the **Get MID** node and add a **Set Sparse Volume Texture Parameter Value** node.
    
9.  Drag off the **Return Value** pin of the **Get Current Frame** node and connect it to the **Value** pin of the **Set Sparse Volume Texture Parameter Value** node.
    
10.  On the **Set Sparse Volume Texture Parameter Value**, set the **Parameter Name** to the name of the **Sparse Volume Texture Sample Parameter** in your SVT material.
    

This part of the Blueprint Logic looks like:

[![SVT Blueprint Animation Logic](https://dev.epicgames.com/community/api/documentation/image/2f505eb3-1d2d-483f-99f6-4ec69de4f4df?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2f505eb3-1d2d-483f-99f6-4ec69de4f4df?resizing_type=fit)

When you **Simulate** or **Play-in-Editor (PIE)**, the SVT should play its animation on a loop.

To get a good result, you may need to adjust a few things:

-   In your Blueprint, adjust the size of the mesh to get a better volume resolution when using Volumetric Fog. The example above scales the cube mesh to 20 times its original size.
    
-   In your SVT material, use a higher multiply value for the last multiply before plugging into the Extinction input. The example above uses 7.5 instead of the original value of 2.5.
    

In addition to the examples above you can also do the following:

-   Use other functions available on the controller to set the frame index or current time directly.
    
-   Playback speed is configured by adjusting the Frame Rate property of the controller. The default is 24fps.
    
-   Alternatively to getting just the current frame, you can use the **Get Current Frames For Interpolation** function to return the two closest frames and a value between 0 and 1 to interpolate between them. You can make use of this method to create two SVT parameters, a scalar parameter for the lerp alpha and then use an Interpolation node in the Material Graph.
    

#### Using an Animated Sparse Volume Texture with Sequencer

Using the animated SVT Blueprint created in the previous section, you can extend it for playback to be controlled from Sequencer. You'll create a new variable that is set as Expose to Cinematics and replace parts of the Event Tick logic. This workflow is similar to how [Skeletal Mesh Anim Blueprints are controlled with Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-animation-blueprint-parameters-from-sequencer-in-unreal-engine).

To extend the animated SVT Blueprint playback to be controlled by Sequencer:

1.  Open your animated SVT Blueprint.
    
2.  In the My Blueprint panel under Components, drag and drop a Controller variable into the graph and select Get Controller from the list.
    
3.  Drag off the Get Controller node and add a Get Duration node.
    
4.  Connect the execution pin of the Event Tick node to the Get Duration node.
    
5.  Drag off the Get Duration node and add a Set Time node (under the Animated Sparse Volume Texture Controller category).
    
6.  Connect the Get Controller node to the Target pin of the Set Time node.
    
7.  Drag off the Return Value of the Get Duration node and add a Multiply node.
    
8.  Drag off the output pin of the Multiply and connect it to the Time input pin of the Set Time node.
    
9.  Right-click in the graph and add a Fraction node.
    
10.  Right-click on the A input pin of the Fraction node and choose Promote to Variable. Name the variable "Animation Alpha".
    
11.  Drag off the Set Time node and add a Get Current Frame node.
    
12.  Drag off the Controller node and connect it to the Target pin on the Get Current Frame node.
    
13.  In the My Blueprint panel under Components, drag a MID variable into the graph and select Get MID.
    
14.  Drag off the Get MID node and add a Set Sparse Volume Texture Parameter Value node.
    
15.  Drag off the Return Value pin of the Get Current Frame node and connect it to the Value pin of the Set Sparse Texture Parameter Value node.
    
16.  On the Set Sparse Volume Texture Parameter Value node, set the Parameter Name to the name of the Sparse Volume Texture Sample Parameter used in your SVT Material.
    
17.  In the My Blueprint panel under Components, select the AnimationAlpha variable. In the Details panel, check the box for Expose to Cinematics.
    
18.  Compile and Save.
    

Your animated SVT Blueprint logic should look like this for the Event Tick path:

[![SVT Blueprint Animation Logic](https://dev.epicgames.com/community/api/documentation/image/521966f8-a8a5-4a65-9beb-d9c1d2a011a1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/521966f8-a8a5-4a65-9beb-d9c1d2a011a1?resizing_type=fit)

With this logic set up, when you add a **Track** to Sequencer for the **Animated SVT Blueprint**, when you click the **Add (+)** icon next to the track, you should see your **AnimationAlpha** variable in the list.

[![SVT Sequencer](https://dev.epicgames.com/community/api/documentation/image/efeba3a8-d9ff-48a4-921f-12b7a02b1b51?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/efeba3a8-d9ff-48a4-921f-12b7a02b1b51?resizing_type=fit)

When added, your variable can be keyed in the Sequencer panel.

[![SVT Animation](https://dev.epicgames.com/community/api/documentation/image/c323694a-66a3-4cdf-a8a6-fe95c2d76c60?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c323694a-66a3-4cdf-a8a6-fe95c2d76c60?resizing_type=fit)

## Streaming Performance Notes

-   **Real-time playback of animated SVTs**
    
    -   Real-time playback of animated SVTs depends a lot on their resolution and sparseness of the volume data. If the data takes too long to stream in, rendering falls back to coarser mip levels causing a visible drop in fidelity. You can work around this in a couple of ways:
        
        -   Using a smaller pixel format when importing a VDB, which in-turn improves streaming performance. (32-bit is usually too much for real-time use cases.)
            
        -   Lowering the animation frame rate.
            
        -   Using a lower resolution mip level.
            
    -   If using this method, the mip level needs to be set on the Animated SVT Controller or the Heterogeneous Volume component settings. Setting the MipLevel input pin on the Sparse Volume Texture Sample node attempts to sample at the given mip level (provided it has been streamed in), but streaming itself is not driven from there. **Useful console variables to adjust streaming performance**
        
    -   `r.SparseVolumeTexture.Streaming.NumPrefetchFrames` is the number of frames to prefetch when a given frame is requested on the streaming system. The default is 3 frames as it works well in most cases, but the value can depend on the SVT itself. Setting the value too high can choke the streaming system with requests. Setting it too low might cause frames to not be fully streamed in by the time they are needed for rendering.
        
    -   `r.SparseVolumeTexture.Streaming.PrefetchMipLevelBias` applies a bias to the mip level of prefetched frames.Prefetching is done at increasingly higher mip levels (lower resolution). This bias can be used to change the mip level at which the frames are prefetched. Negative values cause frames to be prefetched at higher resolution mip levels, while positive values cause frames to be prefetched at lower resolution mip levels.
        
    -   `r.SparseVolumeTexture.Streaming.PrintMemoryStats` prints memory information about all SVTs registered with the streaming system. Streaming performance usually starts to suffer for SVT frames larger than 30 - 50 megabytes (MB). When trying to play back with the default frame rate of 24. Performance largely depends on the platform and PC being used. Streaming performance also depends on the number of SVTs that are currently streaming.
        
-   **Blocking Playback**
    
    -   For certain use cases (offline productions), you might not want to compromise in the ways described above. To guarantee all the mips are streamed in when you render the current frame, the streamer supports blocking requests. With blocking requests, the IO requests for loading in a given frame are issues and immediately waited on until they are complete. Block requests are likely to impact frame rate and cause "skipping" of frames when the current game time is used to drive the animation playback. But when using Sequencer to render out frames, the skipping issue is gone because Sequencer specifies which SVT frame to render, no matter if five minutes of real-time have passed between rendering the previous and current frames. This doesn't apply to the SVT Viewer because it's mostly a way of debugging SVT assets.
        
-   **Stochastic Mip Filtering**
    
    -   This features similar optimizations as Virtual Textures where the two closest mip levels are sampled stochastically. This effectively cuts the number of texture samples in half, improving performance. Take for the example the scene below with five "Aerial Explosion" instances streaming 2GB/s IO Bandwidth. This scene would need approximately 25GB/s without the bandwidth limiter and without scaling according to projected screen space size.
        
    
    [![](https://dev.epicgames.com/community/api/documentation/image/67a255a0-5173-4da7-b1e0-8942498bda2d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/67a255a0-5173-4da7-b1e0-8942498bda2d?resizing_type=fit)
    

## Limitations

-   The Page Table texture is limited to 2 gigabytes (GB) in size and the maximum virtual SVT resolution must not exceed 32k units on the X and Y extents. The Z-axis is limited to 16k.
    
    -   For example, you could make a 32k x 100 x 100 unit volume, a 100 x 32k x 100 unit volume, or a 100 x 100 x 16k unit volume. 100 in this example is a low enough value that it should keep the page table below the 2GB limit.
        
-   Real-time playback of animated SVTs depends a lot on their resolution and sparseness of the volume data. If the data takes too long to stream in, rendering falls back to coarser mip levels causing a visible drop in fidelity. You can work around this by lowering the animation frame rate or using a lower resolution mip level. Streaming performance can also be improved by selecting a smaller pixel format when importing the VDB file.
    
-   Supported platforms:
    
    -   Currently supported on Windows with DX11, DX12 using Shader Model 5 (SM5) and Shader Model 6 (SM6).
        
    -   VDB import currently only works in Windows editor builds. Cooked builds support SVTs on any platform capable of the performance required to stream and render them.
        
    -   SVTs do not work with the Mobile Renderer.
        

## Additional Resources

-   The VDB files used in the examples in this page are from JangaFX's free VDB set created with EmberGen.
    
-   You can download their free examples [here](https://jangafx.com/software/embergen/download/free-vdb-animations/).