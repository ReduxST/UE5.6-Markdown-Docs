# UVs Category

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:34

---

A valuable step after modeling is creating UVs for accurate Texture placement on your mesh. The **UVs** category in **Modeling Mode** provides tools for **Level** based UV editing. UV editing in your Level helps contextualize your model's UVs in comparison to its environment.

[![Tools in the Uvs of Modeling Mode](https://dev.epicgames.com/community/api/documentation/image/670ba0ae-8450-410f-9901-8c9d6fe67b93?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/670ba0ae-8450-410f-9901-8c9d6fe67b93?resizing_type=fit)

Click image to expand.

There are limits to this workflow, and you may find using the [UV Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine#uv-editor) more appropriate to achieve your desired UV map.

## Understanding Key Concepts

Before learning about the tools, we recommend you familiarize yourself with common terminology.

### UV

UVs are a parameterization (U,V) of a 3D surface mesh into a normalized (0-1) 2D space. In other words, they represent coordinates in 2D space that translate to vertices on your 3D model.

[![UV Coordinates Translate to Vertices on 3D Model](https://dev.epicgames.com/community/api/documentation/image/7a380a5d-49e0-41b7-90c7-ab127625ce70?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7a380a5d-49e0-41b7-90c7-ab127625ce70?resizing_type=fit)

The 2D space is represented horizontally as U and vertically as V, thus the name UV coordinates (also referred to as 2D or texture coordinates).

[![UV Space](https://dev.epicgames.com/community/api/documentation/image/9bbda4cf-f315-4be6-a4f7-89fc3305da93?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9bbda4cf-f315-4be6-a4f7-89fc3305da93?resizing_type=fit)

*Click image to expand.*

### UV Map

The collection of UV islands and their layout is called a UV map. The UV map determines how a Texture will be wrapped around your 3D geometry when rendered—this process of texture wrapping is known as UV mapping.

[![UV Map in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/7ada95fa-affe-49d4-9cf0-84777bc15c65?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7ada95fa-affe-49d4-9cf0-84777bc15c65?resizing_type=fit)

Click image to expand.

A Material uses the mapping between 2D coordinates and 3D vertex positions to determine which areas of the Texture are used to shade what triangles in your 3D model.

### UV Islands

UV islands, also called charts, are a collective of connected triangles within a given boundary of edges. However, one triangle can represent an island.

[![UV Islands in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/d029b4df-9178-41f7-9558-b2f643a32f9f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d029b4df-9178-41f7-9558-b2f643a32f9f?resizing_type=fit)

Click image to expand.

### UDIM

A traditional UV map is created in the 0-1 [unit square](https://dev.epicgames.com/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine). This limitation in texture space can make creating efficient textures difficult.

[![UV Unit Square in 2D Space](https://dev.epicgames.com/community/api/documentation/image/4cbc67f5-4280-4b8d-a270-92a8fe4f298d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4cbc67f5-4280-4b8d-a270-92a8fe4f298d?resizing_type=fit)

Click image to expand.

UDIMs make it possible to manage multiple resolutions for a single model by using additional unit squares. You may need certain parts of your model to have a 1k texture, while others use a 4k texture. In addition, you can choose multiple lower-resolution textures for differing parts to accumulate to a high-resolution image. Using different texture regions at different resolutions helps achieve the appropriate texel density for your model.

UDIMs is short for U-Dimension – the direction in which a set number of unit squares (or UDIM tiles) are used for textures before moving up in the V direction and repeating the process. UDIMs is a process practiced heavily in the VFX industry compared to traditional video game development.

[![UDIMs in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/a01ace12-a602-40b7-9af8-a8fdfa595946?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a01ace12-a602-40b7-9af8-a8fdfa595946?resizing_type=fit)

Click image to expand.

For UDIM creation and management you need to use the UV Editor.

## Common Functionality

Some tools have shared settings that we explain here.

### UV Channel

A **UV Channel** contains your UV map. You can create multiple UV maps for one model using UV Channels.

UV Channels provide the ability to layer Textures on your mesh and store data such as baked lights. You can create and manage channels using the following:

-   The UV Editor's **Channel** tool
    
-   The **Static Mesh Editor**
    
-   **AttrEd** tool under the **Attributes** category while in Modeling Mode
    

The UV Editor provides functionality to add, delete, and copy channels.

To learn more about UV Channels, refer to the [Using UV Channels With Static Meshes](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine) documentation.

### Poly Group Layer

You can decide to constrain the arrangement of UVs based on your geometry's **PolyGroups**.

You can create and manage PolyGroups through tools such as [GrpGen](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine) and [GrpPnt](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine). To learn more about PolyGroups, refer to the [Understanding PolyGroups](https://dev.epicgames.com/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine) documentation.

### Preview Material

You use the **Preview Material** to help visualize your UVs. You can switch between the following Material:

| Material | Description |
| --- | --- |
| 
**Original**

 | 

Displaying the current Material applied in the Details panel.

 |
| 

**Checkerboard**

 | 

Applies a temporary checkerboard Material.

 |
| 

**Override**

 | 

Applies a temporary Material located in your Content Browser.

 |

Using the checkerboard material, you can adjust the density and preview the look of additional channels that are set to the mesh.

### Preview UV Layout

For some tools, you can preview your UV map in 2D Space.

[![Preview UV Space in Level Editor](https://dev.epicgames.com/community/api/documentation/image/cc50ffe8-38a4-40ff-8ad8-c7a66ec12a78?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cc50ffe8-38a4-40ff-8ad8-c7a66ec12a78?resizing_type=fit)

Click image to expand.

The preview panel will match the movement of the camera for visibility. In addition, you can:

-   Control which side it appears on
    
-   Scale the panel
    
-   Manually adjust the position using **Offset**
    
-   Enable wireframe
    

The preview panel will show all your UVs with a square border depicting the 0-1 unit square. However, the panel can become challenging to read for models with UDIMs or UVs far away from 0-1.

[![Preview UV Space in Level Editor](https://dev.epicgames.com/community/api/documentation/image/b55de438-1bd1-4044-84d4-5650bfaec558?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b55de438-1bd1-4044-84d4-5650bfaec558?resizing_type=fit)

Click image to expand.

## UV Tools

When creating new UVs, you can use the AutoUV or [Project](https://dev.epicgames.com/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine#project) tool to get started. You can use the remaining tools after to work out the details. Use the [SeamEd](https://dev.epicgames.com/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine#seam-ed) tool for a manual start.

You can adjust Texture resolution using the **Layout**, **AutoUV**, and **Unwrap** tools.

### AutoUV

You can automatically unwrap and pack your UVs using **AutoUV**. This automation is helpful as a starting point for custom UV mapping or background assets needing a quick UV map.

There are three methods for control: **UVAtlas**, **XAtlas**, and **PatchBuilder**.

| Method | Description |
| --- | --- |
| 
**Patch Builder**

 | 

Supports large models, such as Nanite. Default option built in-engine.

 |
| 

**UV Atlas**

 | 

More valuable for organic objects, minimizing stretching. To learn more on UV Atlas, refer to [Using UVAtlas](https://learn.microsoft.com/en-us/windows/win32/direct3d9/using-uvatlas).

Does not work on Linux.



 |
| 

**XAtlas**

 | 

Designed for light maps and mechanical meshes. To learn more about XAtlas, refer to [XAtlas Github](https://github.com/jpcy/xatlas).

 |

In Patch Builder mode you can layout UVs based on predefined PolyGroups.

### Unwrap

The **Unwrap** tool flattens your 3D object out into 2D space to compute UV coordinates, helping minimize stretched and squashed areas (distortion)

In the video, using the Unwrap tool to recompute the UVs removes the high-distortion area around the seam, resulting in more proportional UVs.

You can use the UV Editor to perform the operation on a selected UV island(s).

You can decide if you want to UV unwrap based on **Existing UVs** or **PolyGroups**. How your UVs automatically unwrap is determined by the **Unwrap Type**.

| Unwrap Type | Description |
| --- | --- |
| 
**ExpMap**

 | 

Performs a fast unwrap but is limited in reducing distortion.

 |
| 

**Conformal**

 | 

Reduces distortion compared to ExpMap, but is increasingly expensive on large islands.

 |
| 

**SpectralConformal**

 | 

Compared to the Conformal method reduces the distortion further but is more expensive to compute. Additionally has the option Preserve Irregularity to remove unnatural distortion due to mesh irregularity.

 |
| 

**Island Merging**

 | 

UV islands are merged into larger islands if it does not increase distortion beyond defined limits.

 |

If you are texturing a simple geometry such as a flat plane, then all unwrap types will give you approximately the same result. If you are working with a mesh that is not uniformly tessellated and has a complex shape, Spectral Conformal is the best option. It provides the least distortion; however, it computes slower.

You also have the option to choose a [Layout Type](https://dev.epicgames.com/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine#layout) and preserve UDIMs.

### Project

One way to create a UV map is by projecting it from a selected shape or point onto your geometry. The **Project** tool is an alternative to **AutoUV** for initializing your UV maps quickly.

Project works well on geometry with a similar silhouette to the selected **Projection Type**. The tool may not be the best option for complex geometry as it can cause distortion and unwanted seams. However, it can serve as a starting point before using the UV Editor.

You can choose from the different Projection Types illustrated in the table below.

|   |   |   |   |
| --- | --- | --- | --- |
| 
[![UV Box Projection](https://dev.epicgames.com/community/api/documentation/image/c483633f-424e-4b5a-8d5f-361cd234d93d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c483633f-424e-4b5a-8d5f-361cd234d93d?resizing_type=fit)



 | 

[![UV Cylinder Projection](https://dev.epicgames.com/community/api/documentation/image/5a0e4049-b5cc-44e7-8d05-c1eafe3c1994?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5a0e4049-b5cc-44e7-8d05-c1eafe3c1994?resizing_type=fit)



 | 

[![UV Plane Projection](https://dev.epicgames.com/community/api/documentation/image/3b0bdd40-17bd-40bf-986f-8546f500c4ed?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3b0bdd40-17bd-40bf-986f-8546f500c4ed?resizing_type=fit)



 | 

[![UV ExpMap Projection](https://dev.epicgames.com/community/api/documentation/image/72db9c54-39f2-426b-8987-1e77b6529917?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/72db9c54-39f2-426b-8987-1e77b6529917?resizing_type=fit)



 |
| 

**Box**

 | 

**Cylinder**

 | 

**Plane**

 | 

**ExMap**

 |
| 

Useful for assets with sharp edges, such as a crate or book.

 | 

Useful for assets with round edges, such as an arm or tree trunk.

 | 

Useful for flat assets, such as a mirror or wall.

 | 

Useful for decals in a separate UV Channel.

 |

You may notice **ExpMap** has an identical shape to the **Plane** projection; however their operation is different. Instead of projecting based on a shape, ExpMap projects based on a point.

To learn more about the ExpMap projection, refer to the paper [Interactive Decal Compositing with Discrete Exponential Maps](https://prism.ucalgary.ca/bitstream/handle/1880/46212/2006-824-17.pdf;jsessionid=EA77D1B305EA6B2A72425CAF119503CE?sequence=2).

#### Making Adjustments

You can adjust the dimension of each shape for a better fit around your mesh. To uniformly define the size, enable **Uniform Dimensions** and adjust only the X value. You can then use the transform widget for further adjustments.

**Initialization** determines the way the projection shape automatically fits your model when activating the Project tool. You have four options described in the table below.

| Initialization Type | Description |
| --- | --- |
| 
**Default**

 | 

Projection to bounding box center.

 |
| 

**Use Previous**

 | 

Projection based on previous usage of the Projection tool.

 |
| 

**Auto Fit**

 | 

Automatically fits the UV Projection Dimensions to your geometry based on the current projection orientation.

This method will appear the same as Default unless the orientation of the projection shape is altered.



 |
| 

**Autofit Align**

 | 

Automatically orients the projection, then automatically fits the UV Projection Dimension to your model.

 |

You can change the Initialization type after opening the **Project** tool. However, as soon as you alter the projection type, dimension, or position, Initialization deactivates.

To reactivate Initialization, set the desired type and then either:

-   Reselect the Project tool.
    
-   Press the **Reset** button under **Actions**.
    

The Actions options also let you initiate Auto Fit and Auto Fit Align at any point needed.

If Uniform Dimension is enabled, you may not see the projection shape change when using Initialization or Actions.

Finally, using the **UV Transformation** settings, you can adjust the rotation, scale, and translation of the projected UVs.

### SeamEd

You can interactively separate edges to create seams in the Viewport. Click a vertex and drag to a neighboring vertex to create a seam. You can make multiple seams before clicking Accept or pressing the **Enter** key.

It is not necessary to select directly onto a vertex to highlight it; clicking near the vertex on the geometry will do. This selection option will help you avoid choosing other Actors in the scene.

You typically want seams invisible to your audience unless it is the desired aesthetic. Knowing what parts of your asset are visible in the experience is essential in understanding where to create seams.

To merge seams together, you will need to use the [Sew tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine) in the UV Editor. In addition, the tool doesn't support multiple UV Channels.

### XFormUV

The **XFormUV** tool also provides interactive control in the Viewport. You can scale, rotate, and translate UVs per island. To adjust multiple islands at once, hold the **Shift** key.

The XFormUV tool helps adjust distortion in individual islands after using the other UV tools.

### Layout

The **Layout** tool helps organize your UV islands into the 0-1 unit square.

The process of laying out UVs into a UV space is called UV packing. There are three Layout Types to help pack your UVs:

| Layout Type | Description |
| --- | --- |
| 
**Transform**

 | 

Transform applies scaling and translation to all your UVs, regardless if particular islands are selected. Keeps the current layout of the UVs. These scale and translation controls are available in Stack and Repack.

 |
| 

**Stack**

 | 

Uniformly scale and translate each UV island individually to pack in a unit square with overlap. Stacking can be useful when two UV islands share the same texturing design, removing the need for replication.

 |
| 

**Repack**

 | 

Uniformly scale and translate UV islands collectively to pack in a unit square with no overlap. Unique to Repack is the Allow Flips setting. Enabling this feature can save space when packing UVs but can lead to issues for downstream operations.

 |

Using the UV Editor, you can organize your UV islands within their originating UDIM when **Preserve UDIMs** is enabled.

### UV Editor

Although the UV tools provide editing capabilities, there are limits such as:

-   Merging edges
    
-   UDIM management
    
-   Multi-asset workflow
    
-   Manual precision control of islands, vertices, and triangles
    

The UV Editor picks up these limitations by providing a toolset and Viewports for such capabilities. Refer to the [UV Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine) documentation to learn how to use this Editor.

[![UV Editor in Unreal Engine](https://dev.epicgames.com/community/api/documentation/image/cceb398b-9491-4e78-8eba-94c3a5bc48c7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cceb398b-9491-4e78-8eba-94c3a5bc48c7?resizing_type=fit)

Click image to expand.