# Dataprep Operation Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-operation-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-operation-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:43

---

This page describes each of the **Operations** blocks that you can use in the Visual Dataprep system to modify your Assets and scene elements.

Each type of **Operations** block encapsulates a specific kind of modification that the Unreal Editor can make to 3D data. When the Visual Dataprep system carries out each action in your Dataprep graph, it performs each operation you've defined in that action on all the Assets or Actors that match the criteria set by the **Select By** blocks above it. For more background information, see [Dataprep Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-overview-in-unreal-engine).

## On Actor

**On Actor** operations apply only to Actors that match the **Select By** criteria you set for their steps. That means only items that you see listed in the **Outliner Preview** panel on the right of the Dataprep preview UI. If your **Select By** criteria match other scene elements, like the Texture, Material, and Static Mesh Assets that are listed in the **Content Browser Preview** panel on the left of the Dataprep preview UI, the **On Actor** operation will have no effect on those elements.

### Add Tags

This operation adds the array of tags you specify to each Actor or Component that matches the **Select By** criteria you set for this step.

[![Add Tags](https://dev.epicgames.com/community/api/documentation/image/5c1caeb4-5355-4b48-8695-f529a7c1009c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5c1caeb4-5355-4b48-8695-f529a7c1009c?resizing_type=fit)

Click image for full size.

After this block has completed, you can find the list of tags by selecting your Actor in the **Outliner Preview** and looking in the **Details** panel. Under the **Actor** category, expand the advanced options and look for the **Tags** setting.

[![Actor Tags after addition](https://dev.epicgames.com/community/api/documentation/image/8849d0b5-ff1b-427c-a0cb-425f4e79b515?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8849d0b5-ff1b-427c-a0cb-425f4e79b515?resizing_type=fit)

Click image for full size.

### Add To Layer

This operation takes each Static Mesh Actor that matches the **Select By** criteria you set for this step and adds it to the Layer you specify.

[![Add To Layer](https://dev.epicgames.com/community/api/documentation/image/7e5f21aa-4b04-4428-9e7c-d2ab30ecc92d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7e5f21aa-4b04-4428-9e7c-d2ab30ecc92d?resizing_type=fit)

Click image for full size.

### Compact Scene Graph

For each Static Mesh Actor that matches the **Select By** criteria you set for this step, this operation deletes the Actor if it doesn't have any visual result on the scene, and if none of its descendants in the scene hierarchy have visual results on the scene. The effect is to tidy unnecessary elements from the scene hierarchy without compromising the visual objects in the scene.

[![Compact Scene Graph](https://dev.epicgames.com/community/api/documentation/image/1c6cc18d-5a65-4375-bf4a-d3f7cea12256?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1c6cc18d-5a65-4375-bf4a-d3f7cea12256?resizing_type=fit)

Click image for full size.

### Create Proxy Mesh

This operation collects the geometry from all Static Mesh Actors and Components that match the **Select By** criteria you set for this step, and merges the geometry into a single new mesh using the [Proxy Geometry Tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/proxy-geometry-tool-in-unreal-engine).

[![Create Proxy Mesh](https://dev.epicgames.com/community/api/documentation/image/eca1bca1-7c12-4775-93dd-3a326a1f837e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eca1bca1-7c12-4775-93dd-3a326a1f837e?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**New Actor Label**

 | 

Specifies the name of the new Actor created from the merged geometry.

 |
| 

**Quality**

 | 

The level of quality for the geometry of the generated proxy mesh. Lower values are less detailed but may render more efficiently. Higher values are more detailed and faithful to the original geometry but may not be as efficient to render.

 |

### Merge

This operation collects the geometry from all Static Mesh Actors and Components that match the **Select By** criteria you set and merges the geometry into a single new mesh.

[![Merge](https://dev.epicgames.com/community/api/documentation/image/dc574b37-2123-4d79-91c5-dee6ebf22e76?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dc574b37-2123-4d79-91c5-dee6ebf22e76?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**New Actor Label**

 | 

Specifies the name of the new Actor created from the merged geometry.

 |
| 

**Pivot Point at Zero**

 | 

Enable this setting if you want the merged mesh to have its pivot point set at the world origin. If left disabled, the pivot will be located at the first merged component.

 |

### Random Offset Transform

For each Actor that matches the **Select By** criteria you set for this step, this operation applies a random offset to the 3D position, rotation, or scale of the Actor. If you have placeholder elements in your scene, you can use this operation to scatter those elements around, or to give them varied sizes and rotations.

For example, an external architectural scene may contain placeholder objects for scene entourage like trees or bushes. In your Dataprep graph, you may want to replace all of those placeholders with other custom 3D Assets that you've already imported into your Project. However, this might result in a line of trees that are unnaturally identical. By applying random offsets to the position, rotation, and scale of the trees, you can quickly create a more varied and lifelike result without having to adjust the objects manually.

[![Random Offset Transform](https://dev.epicgames.com/community/api/documentation/image/38060c5c-ef05-4de0-934f-8335900d9794?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/38060c5c-ef05-4de0-934f-8335900d9794?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Transform Type**

 | 

Each **Random Offset Transform** block can apply offsets to only one of the following:

-   **Location**, which adjusts the placement of the objects in 3D space.
    
-   **Rotation**, which adjusts the facing direction of the objects.
    
-   **Scale**, which adjusts the size of the objects.
    

 |
| 

**Reference Frame**

 | 

Determines what frame of reference is used to interpret the axes in the **Min** and **Max** settings:

-   **Global** interprets the **Min** and **Max** values in world space, relative to the global 3D axes.
    
-   **Relative** interprets the **Min** and **Max** values in the object's local space, relative to the object's pivot point.
    

 |
| 

**Min** and **Max**

 | 

Sets a range for the random offsets along each of the three axes of 3D space. For each Actor this block treats, it generates a different random number in between the **Min** and **Max** values.

 |

### Set Mesh

For each Static Mesh Actor or Component that matches the **Select By** criteria you set for this step, this operation changes all Static Mesh Assets referred to by the Actor or Component to a different Static Mesh Asset that you specify in the settings.

[![Set Mesh](https://dev.epicgames.com/community/api/documentation/image/bd77d2d2-71fc-4e48-a676-2a4d29426e06?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bd77d2d2-71fc-4e48-a676-2a4d29426e06?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Static Mesh**

 | 

The Static Mesh Asset that you want the Actor to instance in place of its existing Static Mesh. This replacement may be any Static Mesh in the **Content Browser Preview** panel of the Dataprep Editor, or any Static Mesh Asset that already exists in your project.

 |

This operation has no effect on Actors that don't already refer to a Static Mesh Asset. For example, if you have an empty Actor in the scene hierarchy that doesn't already have a Static Mesh, you won't be able to use this operation to add a new Static Mesh to that Actor.

### Set Metadata

This operation adds an array of keys and values to the Datasmith Metadata maintained by each Actor and Component that matches the **Select By** criteria you set for this step.

[![Set Metadata](https://dev.epicgames.com/community/api/documentation/image/6bc006a5-e228-491a-93e2-5bde85f423e4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6bc006a5-e228-491a-93e2-5bde85f423e4?resizing_type=fit)

Click image for full size.

After this block has completed, you can find the list of metadata by selecting your Actor or Component in the **Outliner Preview** and looking in the **Details** panel under the **Asset User Data** category.

For more information, see [Using Datasmith Metadata](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-datasmith-metadata-in-unreal-engine).

### Set Mobility

For each Actor or Component that matches the **Select By** criteria you set for this step, this operation sets the value of the Actor's **Mobility** setting.

The **Mobility** setting has slightly different implications for Light Actors than it does for Static Mesh Actors. For details on how it is interpreted, see [Actor Mobility](https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-mobility-in-unreal-engine).

[![Set Mobility](https://dev.epicgames.com/community/api/documentation/image/20439347-e96f-4c30-9263-28a89a68d6c9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/20439347-e96f-4c30-9263-28a89a68d6c9?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Mobility Type**

 | 

The value you want to set for the Actor's **Mobility** setting.

 |

Find the **Mobility** setting in the **Details** panel:

[![Actor Mobility](https://dev.epicgames.com/community/api/documentation/image/56b63670-0f18-4666-8ac3-95ea0d8e0cf3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/56b63670-0f18-4666-8ac3-95ea0d8e0cf3?resizing_type=fit)

Click image for full size.

### Spawn Actors at Location

For each Actor that matches the **Select By** criteria you set for this step, this operation spawns a new Actor at the same 3D coordinates. The newly spawned Actor is an instance of the Asset you specify in the **Selected Asset** setting.

[![Spawn Actors at Location](https://dev.epicgames.com/community/api/documentation/image/2c8f2c7c-4cc5-43b3-92d5-5d7e30c94a90?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2c8f2c7c-4cc5-43b3-92d5-5d7e30c94a90?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Selected Asset**

 | 

The Asset in your Project that you want to spawn new instances of.

 |

## On Asset

**On Asset** operations apply only to Assets that match the **Select By** criteria you set for their steps. That means only items that you see listed in the **Content Browser Preview** panel on the left of the Dataprep preview UI. If your **Select By** criteria match other scene elements, like the Actors that are listed in the **Outliner Preview** panel on the right of the Dataprep preview UI, the **On Asset** operation will have no effect on those elements.

### Output to Folder

This operation moves each Asset that matches the **Select By** criteria you set for this step into a subfolder with the name that you specify. You can use this block to customize the way the imported Assets are organized in your Project's Content Browser after you commit the results of your Dataprep graph.

The results of the **Output to Folder** block are not shown in the **Content Browser Preview** panel of the Dataprep Editor when you execute your Dataprep graph. You'll only see the results in your Project's **Content Browser** after you commit the Dataprep graph.

[![Output to Folder](https://dev.epicgames.com/community/api/documentation/image/b0b27dce-c48c-48f9-9e61-2211d6b443ee?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b0b27dce-c48c-48f9-9e61-2211d6b443ee?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Folder Name**

 | 

The name of the subfolder that you want the selected Assets to be placed in when you commit your Dataprep graph.

 |

You can use as many **Output to Folder** blocks as you want in your Dataprep graph. If you use the same **Folder Name** setting for different blocks, the Assets treated by those different blocks will be gathered together into a single folder. This allows you to redirect the Assets that result from several different filters in different Actions to the same folder in the Content Browser. By pairing multiple **Output to Folder** blocks with different filters, you can distribute your Assets into whatever organization you want to end up with in your **Content Browser**.

For example, in this case the main folder set in the settings panel at the top right of the Dataprep Editor is **/Content/Motorbike**. The first Action in this graph takes all Static Mesh Assets that have fewer than 1000 triangles and moves them to a subfolder named **LowPoly**. The second Action takes all other Static Meshes with more than 1000 triangles and moves them to a subfolder named **HighPoly**. Finally, the last two Actions take all Materials and all Material Instances and move them to a subfolder named **Surfaces**.

[![Output to Folder example graph](https://dev.epicgames.com/community/api/documentation/image/8dbc3d6f-887b-41e1-9f23-b8db713b0e1f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8dbc3d6f-887b-41e1-9f23-b8db713b0e1f?resizing_type=fit)

Click image for full size.

After you commit the Dataprep graph, the Content Browser has the following folder structure:

[![Output to Folder example result](https://dev.epicgames.com/community/api/documentation/image/20250b46-5de6-4fc9-b821-f37876605cf8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/20250b46-5de6-4fc9-b821-f37876605cf8?resizing_type=fit)

Click image for full size.

The **Geometries** and **Materials** subfolders normally created by the default Datasmith import process are still created, but in this case they are empty. All Assets have been redistributed to the new **HighPoly**, **LowPoly**, and **Surfaces** subfolders.

### Replace Asset References

This block identifies the *first* Asset in the list of objects passed in. It then attempts to replace all references to the *other* Assets in the input list with references to the first Asset instead.

For example, suppose that the first object in the input list is a Static Mesh Asset named **Chair**. This block will look through all other objects in the input list to find other Static Mesh Assets — say, **Table**, **Bench**, and **Dresser**. It will then replace all references to **Table**, **Bench**, and **Dresser** with references to **Chair** anywhere they are found in the imported scene, *and* it will delete the **Table**, **Bench**, and **Dresser** Assets entirely.

[![Replace Asset References](https://dev.epicgames.com/community/api/documentation/image/7aeb2032-522f-417a-ad53-9f489f24b6bb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7aeb2032-522f-417a-ad53-9f489f24b6bb?resizing_type=fit)

Click image for full size.

### Set Max Texture Size

By default, Datasmith scales imported textures to power-of-2 sizes. This operator sets a value that restricts the maximum in-game variable on a texture, but does not impact the import size of the texture.

The **Max Texture Size** field behaves like the **Maximum Texture Size** field on any Texture, rounding the value you entered to the nearest power-of-2 value.

[![Set Max Texture Size](https://dev.epicgames.com/community/api/documentation/image/05356cd2-dd72-48e1-8099-baefa34be817?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/05356cd2-dd72-48e1-8099-baefa34be817?resizing_type=fit)

Click image for full size.

## On Mesh

**On Mesh** operations apply only to Static Mesh Assets.

-   If your **Select By** criteria match any Static Mesh Assets that you see listed under the **Geometries** folder in the **Content Browser Preview** panel, the operation will apply to those Assets.
    
-   If your **Select By** criteria match any Actors in the **Outliner Preview** that refer to Static Mesh Assets, the operation will also apply to those Static Mesh Assets.
    
-   If your **Select By** criteria match any other kinds of scene elements, like Actors, Textures, or Materials, the **On Mesh** operation will have no effect on those elements.
    

### Bake Transform

For each Static Mesh Actor that matches the **Select By** criteria you set for this step, this operation creates a new mesh by baking the transform of the Static Mesh Actor directly into the mesh it refers to and replaces the Static Mesh Actor's mesh with this new mesh. This operation comes with several options:

[![Bake Transform](https://dev.epicgames.com/community/api/documentation/image/88c152a0-314c-40d8-8ebc-7c0ef7e11faa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/88c152a0-314c-40d8-8ebc-7c0ef7e11faa?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Bake Rotation**

 | 

Bakes the current rotation as part of the operation. Enabled by default.

 |
| 

**Bake Scale**

 | 

Determines how the operation handles baking scale and includes the following options:

-   **Bake Full Scale**: Bakes all scale information, so the mesh has a scale of 1 on all axes
    
-   **Bake Non Uniform Scale**: Bakes the non-uniform scale information, so that the mesh has a uniform scale.
    
-   **Do Not Bake Scale**: Will not bake the scale as part of the operation.
    

 |
| 

**Recenter Pivot**

 | 

Translates the geometry of the new mesh so that the Static Mesh Actor's translation is positioned at its center.

 |

### Flip Faces

For each Static Mesh that matches the **Select By** criteria you set up for this step, this operation flips the facing direction of all triangles in the mesh.

[![Flip Faces](https://dev.epicgames.com/community/api/documentation/image/8815e36a-d7a1-43c4-9ecf-fc1b1aa3fdaa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8815e36a-d7a1-43c4-9ecf-fc1b1aa3fdaa?resizing_type=fit)

Click image for full size.

This block can be helpful to reverse the orientation of meshes that were originally modeled in source applications that have different conventions for the visibility of backward-facing triangles. However, note that it is not selective: it reverses the facing direction of *all* triangles. If the facing direction of the triangles in your Static Mesh is mixed, so that some are visible and some are not, you may still need to make additional changes such as flipping faces by hand in the Static Mesh Editor, or using a Material with the **Two Sided** option enabled.

### Generate Unwrapped UVs

For each Static Mesh that matches the **Select By** criteria you set up for this step, this operation unwraps the mesh geometry into a 2D UV map and saves the mapping in the specified UV channel on the Static Mesh Asset.

[![Generate Unwrapped UVs](https://dev.epicgames.com/community/api/documentation/image/2ac1cb66-8adc-4fbc-b438-8d86f75808fd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2ac1cb66-8adc-4fbc-b438-8d86f75808fd?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Channel Selection**

 | 

Determines what UV channel the generated UV mapping is saved to. **First Empty Channel** saves the unwrapped UV in the first empty UV channel. **Specify Channel** saves the unwrapped UV in the channel identified by the **UV Channel** setting.

 |
| 

**UV Channel**

 | 

When **Channel Selection** is set to **Specify Channel**, use this setting to determine the index of the UV channel that the unwrapped UV is saved to.

 |
| 

**Angle Threshold**

 | 

Determines the maximum angle between two adjacent faces for those faces to remain connected after unwrapping. Raising this value minimizes the number of separate UV "islands", keeping more triangles connected to their neighbors and reducing the number of seams that may cause breaks in texture mapping. However, this may also introduce more distortion in the wrapped textures, as triangles may need to be more aggressively resized in 2D space to remain connected to their neighbors.

 |

### Remesh

For each Static Mesh that matches the **Select By** criteria you set for this step, this operation uses isotropic remeshing to reach a triangle count matching the target value you specify. This operation comes with several options:

[![Remesh](https://dev.epicgames.com/community/api/documentation/image/6ae5067e-cc3c-418e-8c25-b8fd94d0daa2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6ae5067e-cc3c-418e-8c25-b8fd94d0daa2?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Target Triangle Count**

 | 

Specifies the target triangle count of the new mesh.

 |
| 

**Smoothing Rate**

 | 

Applies the specified amount of Vertex Smoothing during the remeshing process. Range from 0-1.

 |
| 

**Discard Attributes**

 | 

If set to True, discards existing UVs and Normals.

 |
| 

**Remesh Type**

 | 

Determines how many passes are applied during the remesh process:

-   **Standard**: Applies one pass over the entire mesh, then remeshes only changed edges.
    
-   **Full Pass**: Applies multiple full passes over the entire mesh. This enables the Remesh Iterations option where you can specify the number of incremental passes the tool makes.
    
-   **Normal Flow**: Applies one pass over the entire mesh, then remeshes only changed edges. Uses Normal flow to align triangles with the original input mesh.
    

 |
| 

**Mesh Boundary**

 | 

Determines how the boundary edges of an open mesh are preserved:

-   **Fixed**: Boundary edges are not split or collapsed.
    
-   **Refine**: Boundary edges are split and/or collapsed as needed.
    
-   **Free**: Boundary edges are split, but not collapsed.
    

 |
| 

**Group Boundary**

 | 

Determines how the boundary edges of a polygroup are preserved:

-   **Fixed**: Boundary edges are not split or collapsed.
    
-   **Refine**: Boundary edges are split and/or collapsed as needed.
    
-   **Free**: Boundary edges are split, but not collapsed.
    

 |
| 

**Material Boundary**

 | 

Determines how the boundary edges of a material region are preserved:

-   **Fixed**: Boundary edges are not split or collapsed.
    
-   **Refine**: Boundary edges are split and/or collapsed as needed.
    
-   **Free**: Boundary edges are split, but not collapsed.
    

 |

### Set Convex Collision

For each Static Mesh that matches the **Select By** criteria you set up for this step, this operation replaces the Static Mesh's collision with a new convex decomposition made up of multiple volumes, or *hulls*.

[![Set Convex Collision](https://dev.epicgames.com/community/api/documentation/image/285df069-2a8a-42b1-87cc-1174d5f967c5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/285df069-2a8a-42b1-87cc-1174d5f967c5?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Hull Count**

 | 

The maximum number of convex volumes to create.

 |
| 

**Max Hull Verts**

 | 

The maximum number of vertices that are allowed for any generated convex hull.

 |
| 

**Hull Precision**

 | 

The number of voxels to use when generating the collision volumes.

 |

### Set LOD Group

For each Static Mesh that matches the **Select By** criteria you set up for this step, this operation replaces the existing LODs for the Static Mesh with new ones that are based on the settings for the group you specify.

These LOD groups are the same ones you can set when you enable automatic LOD generation in the Static Mesh Editor UI. For more information, see [Setting Up Automatic LOD Generation](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-automatic-lod-generation-in-unreal-engine).

[![Set LOD Group](https://dev.epicgames.com/community/api/documentation/image/97bb3de9-6714-4c71-93b0-8a696feacc87?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/97bb3de9-6714-4c71-93b0-8a696feacc87?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**LOGGroupName**

 | 

The name of the LOD group that defines the settings you want to use for this Static Mesh.

 |

### Set LODs

For each Static Mesh that matches the **Select By** criteria you set up for this step, this operation replaces the existing LODs for the Static Mesh with new ones that are based on the reduction settings you specify.

These reduction settings are the same ones you can set when you enable automatic LOD generation in the Static Mesh Editor UI. For more information, see [Setting Up Automatic LOD Generation](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-mesh-automatic-lod-generation-in-unreal-engine).

[![Set LODs](https://dev.epicgames.com/community/api/documentation/image/f0c84a93-b152-4876-8c38-eeb57c27b255?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f0c84a93-b152-4876-8c38-eeb57c27b255?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Auto Screen Size**

 | 

When enabled, the screen sizes at which LODs swap are automatically computed.

 |
| 

**Reduction Settings**

 | 

An array of reduction settings that defines how many Levels of Detail to create, and the percentage of triangles each should contain.

 |

### Set Simple Collision

For each Static Mesh that matches the **Select By** criteria you set up for this step, this operation replaces the existing collisions for the Static Mesh with a simple collision volume of the shape you specify.

[![Set Simple Collision](https://dev.epicgames.com/community/api/documentation/image/594e0eee-d445-4a6b-9b54-aa30da120ce4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/594e0eee-d445-4a6b-9b54-aa30da120ce4?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Shape Type**

 | 

Defines the shape of the collision volume that you want to set for the Static Mesh.

 |

### Setup Static Lighting

For each Static Mesh that matches the **Select By** criteria you set up for this step, this operation sets up options that control how the Static Mesh interacts with baked lighting.

[![Setup Static Lighting](https://dev.epicgames.com/community/api/documentation/image/ef51845f-2820-4159-b750-1057d2c09fa7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ef51845f-2820-4159-b750-1057d2c09fa7?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Enable Lightmap UV Generation**

 | 

When enabled, the operation generates lightmap UVs for the Static Mesh.

 |
| 

**Resolution Ideal Ratio**

 | 

A ratio between the scale of the Static Mesh geometry and the lightmap resolution to use for the Static Mesh. Raise this value to make your objects use higher resolution lightmaps. This may increase the quality of baked lighting, but also increases memory requirements.

 |

### Simplify Mesh

For each Static Mesh that matches the **Select By** criteria you set for this step, this operation simplifies the static mesh to a set percentage of its original triangle count. This operation comes with several options:

| Setting | Description |
| --- | --- |
| 
**Target Percentage**

 | 

Target percentage of original triangle count

 |
| 

**Discard Attributes**

 | 

If set to True, discards existing UVs and Normals.

 |
| 

**Mesh Boundary**

 | 

Determines how the boundary edges of an open mesh are preserved:

-   **Fixed**: Boundary edges are not split or collapsed.
    
-   **Refine**: Boundary edges are split and/or collapsed as needed.
    
-   **Free**: Boundary edges are split, but not collapsed.
    

 |
| 

**Group Boundary**

 | 

Determines how the boundary edges of a polygroup are preserved:

-   **Fixed**: Boundary edges are not split or collapsed.
    
-   **Refine**: Boundary edges are split and/or collapsed as needed.
    
-   **Free**: Boundary edges are split, but not collapsed.
    

 |
| 

**Material Boundary**

 | 

Determines how the boundary edges of a material region are preserved:

-   **Fixed**: Boundary edges are not split or collapsed.
    
-   **Refine**: Boundary edges are split and/or collapsed as needed.
    
-   **Free**: Boundary edges are split, but not collapsed.
    

 |

### Weld Edges

For each Static Mesh that matches the **Select By** criteria you set for this step, this operation welds vertex pairs within a specified tolerance. **If Only Unique** is enabled, this operation only merges pairs of equivalent edges.

[![Weld Edges](https://dev.epicgames.com/community/api/documentation/image/00f09c22-f7c3-4ec8-bcbc-5e3a04e5757d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/00f09c22-f7c3-4ec8-bcbc-5e3a04e5757d?resizing_type=fit)

Click image for full size.

### Set Collision Complexity

For each Static Mesh that matches the **Select By** criteria that you set for this step, this operation sets collision complexity on that mesh to the one you specify.

[![Set Collision Complexity](https://dev.epicgames.com/community/api/documentation/image/1bc1a928-9880-4d85-a0da-420269ae5f6f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1bc1a928-9880-4d85-a0da-420269ae5f6f?resizing_type=fit)

Click image for full size.

You can select from these four options:

-   Project Default, as defined in the Project Settings
    
-   Simple and Complex
    
-   Use Simple Collision as Complex
    
-   Use Complex Collision as Simple
    

### Plane Cut

This operation requires you to enable the **Dataprep Geometry Operations** plugin.

For each Static Mesh that matches the **Select By** criteria that you set for this step, this operation cuts and removes geometry, such as performing boxing.

For instanced geometry, one of these two scenarios will happen:

-   If the full mesh is cut, it will no longer be instanced.
    
-   If the mesh is partially cut, this will produce a separate Actor for each former instance of the cut mesh.
    

[![Plane Cut](https://dev.epicgames.com/community/api/documentation/image/79e38036-717b-4460-b82d-4917674a2ef1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/79e38036-717b-4460-b82d-4917674a2ef1?resizing_type=fit)

Click image for full size.

This operation can use both local and world coordinates:

-   On Static Meshes, this operator will cut in their local referential coordinates.
    
-   On Static Mesh Actors, this operator will cut in world coordinates.
    

For example, consider the following scene:

| Setting | Description |
| --- | --- |
| 
**Plane's Origin**

 | 

Defines the origin of the plane to be cut, expressed in local coordinates for Static Meshes, or world coordinates for Static Mesh Actors.

 |
| 

**Plane's Orientation**

 | 

Defines plane rotation in Euler angles, expressed in degrees. The default plane to be cut is XY.

 |
| 

**Side(s) To Keep**

 | 

Selects which side of the cutting plane to keep: Positive, Negative, or Both.

 |
| 

**Spacing Between Halves**

 | 

If you select to keep both sides, this defines the gap between the two sides.

 |
| 

**Fill Holes**

 | 

Enable this option to generate geometry that will fill the cut section.

 |
| 

**Export Separated**

 | 

Enable this option to save cut meshes as separate Assets.

 |

## On Object

**On Object** operations apply to potentially any kind of scene element matched by your **Select By** criteria.

### Delete Objects

This operation deletes all objects that match the **Select By** criteria you set up for this step.

[![Delete Objects](https://dev.epicgames.com/community/api/documentation/image/a4916f38-346f-4ed3-913f-1a2d1edf8fca?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a4916f38-346f-4ed3-913f-1a2d1edf8fca?resizing_type=fit)

Click image for full size.

### Delete Unused Assets

This operation deletes all Assets that match the **Select By** criteria you set up for this step and that aren't referenced by any other Assets or Actors.

[![Delete Unused Assets](https://dev.epicgames.com/community/api/documentation/image/6404b94c-c7a7-4eaa-9fc5-8cd9beca7a01?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6404b94c-c7a7-4eaa-9fc5-8cd9beca7a01?resizing_type=fit)

Click image for full size.

### Set Material

For each Static Mesh, Static Mesh Actor, or Component that matches the **Select By** criteria you set up for this step, this operation replaces all existing Materials with the Material you specify.

[![Set Material](https://dev.epicgames.com/community/api/documentation/image/216f8df5-9e6d-4a3d-bc1f-68ea8a1b8790?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/216f8df5-9e6d-4a3d-bc1f-68ea8a1b8790?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Material**

 | 

The Material you want to use as a substitute for all existing Materials.

 |

### Substitute Material

For each Static Mesh, Static Mesh Actor, or Component that matches the **Select By** criteria you set up for this step, this operation replaces any Material that matches the criteria with the substitute Material you specify.

[![Substitute Material](https://dev.epicgames.com/community/api/documentation/image/c26c094e-ac81-468f-9d63-41cd5cf69c67?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c26c094e-ac81-468f-9d63-41cd5cf69c67?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Material Search**

 | 

The name or partial name of the Material or Materials you want to replace.

 |
| 

**String Match**

 | 

Defines the type of matching that you want to perform on the **Material Search** string. These options are interpreted the same way as when you use a string filter in a **Select By** block. For details, see [Visual Dataprep Selection Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine).

 |
| 

**Material Substitute**

 | 

The Material you want to use as a substitute for the Materials that match the criteria above.

 |

### Substitute Material By Table

For each Static Mesh, Static Mesh Actor, or Component that matches the **Select By** criteria you set up for this step, this operation replaces Materials according to a substitution table that you provide in a DataTable Asset.

[![Substitute Material By Table](https://dev.epicgames.com/community/api/documentation/image/521b6d69-1af0-45c8-abaf-19d9463553d1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/521b6d69-1af0-45c8-abaf-19d9463553d1?resizing_type=fit)

Click image for full size.

| Setting | Description |
| --- | --- |
| 
**Material Data Table**

 | 

The Data Table Asset that determines what Materials are replaced by what other Materials.

 |

The Data Table that you provide in the **Material Data Table** setting must use the **MaterialSubstitutionDataTable** row structure. You typically set this row format in the **Pick Row Structure** dialog box at the time you create your Data Table Asset. For example:

[![Select the MaterialSubstitutionDataTable Row Structure](https://dev.epicgames.com/community/api/documentation/image/cecb9ebb-c97a-4bce-a779-eea9c9ebfca5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cecb9ebb-c97a-4bce-a779-eea9c9ebfca5?resizing_type=fit)

Click image for full size.

With this row structure, each row in the Data Table defines one Material substitution operation that will be executed on each of the Static Mesh Actors and Assets.

-   The first value in the row, **Row Name**, provides a name for the substitution. You can set this value freely.
    
-   The second value, **Search String**, is the name or partial name of the Material or Materials you want to replace in this operation.
    
-   The third value, **String Match**, is the type of string comparison you want to make between the Materials in the Static Mesh Assets and Actors and the search string you set in the second value of this row. You can use any of the values accepted by the **Substitute Material** operation: **Exact Match**, **Contains**, or **Matches Wildcard**. These options are interpreted the same way as when you use a string filter in a **Select By** block. For details, see [Visual Dataprep Selection Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-selection-reference-in-unreal-engine).
    
-   The fourth value, **Material Replacement**, is the full name of the Material Asset you want to use to replace any Materials that match the search string.
    
    You can get this value by right-clicking a Material in the **Content Browser** and selecting **Copy Reference** from the context menu.
    

For example:

[![Material substitution table](https://dev.epicgames.com/community/api/documentation/image/3bfb9465-51ff-4fad-bb05-33dee68f670c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3bfb9465-51ff-4fad-bb05-33dee68f670c?resizing_type=fit)

Click image for full size.