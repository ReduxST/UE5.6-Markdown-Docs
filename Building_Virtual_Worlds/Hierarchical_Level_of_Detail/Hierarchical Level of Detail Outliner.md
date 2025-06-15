# Hierarchical Level of Detail Outliner

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-level-of-detail-outliner-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-level-of-detail-outliner-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:26

---

There are several options that are available within the **Hierarchical LOD (Level of Detail) Outliner** that you can use to define how your HLOD meshes are set up. Once enabling the HLOD system, you can access the HLOD Outliner from the window menu option under **Level Editor**. 

Click image for full size.

Click image for full size.

This page breaks down the available properties within the **HLOD Outliner**, refer to each section for more information.

Click image for full size.

1.  **HLOD Actions:** Generates your HLOD Proxy Meshes for each of the clusters in your Level, re-generate clusters and build Proxy Meshes for each of the generated clusters in the Level, save all external HLOD data, or switch between LOD viewing options. 
    
2.  **HLOD Scene Actors:** Contains each of the clusters (or Proxy Meshes) that have been generated along with information about each Actor. You can also **Generate** or **Delete Clusters** from this panel as well as perform contextual actions by right-clicking on a Scene Actor. 
    
3.  **LODSystem:** Defines how many **HLOD Levels** you want to include along with the **Cluster** and **Mesh Generation Settings** per HLOD Level. You can also override the Material used for Proxy Materials or override the **HLODSetup Asset**. 
    

## Property and Interface Reference

Click image for full size.

## HLOD Actions

Across the top of the **HLOD Outliner**, you will find the available options: 

Click image for full size.

|   |   |
| --- | --- |
| **Generate Proxy Meshes** | 
This option becomes available after you have **Generated Clusters** that you wish to Generate Proxy Meshes from. When you generate Proxy Meshes, this will use the clustered LODs and merge these **Actors** together into a single asset. You can define how Proxy Meshes are clustered with the **Cluster Generation Settings** and ultimately how your Proxy Meshes are generated using the **Mesh Generation Settings**. This option also only affects the generated meshes, not the entire Level. 

Be aware that this process can take a very long time depending on your scene complexity and settings you've chosen for your HLOD levels.



 |
| **Build (Rebuild) All** | 

This option can be used to build both the clusters and Proxy Meshes from those clusters in one step. Typically, you will want to generate clusters and ensure that you are content with the desired results before generating the Proxy Meshes (this option will automatically build the Proxy Meshes). Once you have generated clusters, the option **Rebuild All** is available which will re-generate clusters and build Proxy Meshes from those clusters.

Unlike **Generate Proxy Meshes**, this option will dirty the Level and may take a significant amount of time depending on your scene complexity and settings.



 |
| **Save All** | This option enables you to save all external HLOD data, this includes Meshes, Materials, and Textures. |
| **LOD View** | This option enables you to choose the LOD level to view inside the Editor or to assign a **Forced Viewing Level** inside the Editor. This is helpful for debugging any LOD issues you may have. |

## HLOD Scene Actors

The **HLOD Scene Actors** panel enables you to **Generate Clusters** (but not the Proxy Meshes) for Meshes in the Level or **Delete Clusters** (which will delete all clusters in the Level). This panel also displays all the LODActors for a given LOD Level along with information about the Actor such as their original triangle count, the reduced number of triangles in an LOD mesh, the percentage of triangle reduction retained by an LOD mesh, and what Level the LOD Mesh resides in. 

Click image for full size.

Additional actions can be accessed by right-clicking on an LOD Actor or Static Mesh Actor in the panel:

### LOD Actor Context Menu

Right-click any LOD Actor listed under the **Scene Actor Name** column to bring up the menu below and available options. 

Click image for full size.

| Option | Description |
| --- | --- |
| **Select LOD Actor** | Selects the LOD Actor in the viewport (same effect as left-clicking the cluster). |
| **Select Contained Actors** | Selects all the Actors contained in the LOD Cluster. |
| **ForceView** | 
Toggles the LOD view of the HLOD Actor in the viewport. 

This option is available for LODActors that have been built into Proxy Meshes.



 |
| **Rebuild Proxy Mesh** | Forces the right-clicked cluster to rebuild its Proxy Mesh. |
| **Create Containing Hierarchical Volume** | Creates a Hierarchical Volume around the Actors contained in the Cluster that can then be modified to encompass greater or fewer Actors. |
| **Delete Cluster** | Deletes the right-clicked Cluster. |

### Actor Context Menu

Expanding an LODActor exposes the scene Actors included in the generated HLOD cluster. Right-click a Scene Actor for the following options: 

Click image for full size.

| Option | Description |
| --- | --- |
| **Remove From Cluster** | Removes the right-clicked Actor from the cluster. |
| **Exclude From Cluster Generation** | Excludes the right-clicked Actor from cluster generation. If you wish to re-add the excluded Actor click and drag it from the **World Outliner** into the cluster in the **Hierarchical LOD Outliner**. |

## Properties

Below, broken out by major section, are the properties that can be found in a **Hierarchical LODSetup** in the **LODSystem** panel located in the lower portion of the **Hierarchical LOD Outliner** interface.

### Cluster Generation Settings

The **Cluster Generation** settings enable you to control how HLOD clusters will be generated to include Actors from your levels by setting the desired bounds of your clusters, how full the cluster should be, and the minimum number of Actors that must be used to generate a cluster.

Click image for full size.

| Property | Description |
| --- | --- |
| **Allow Specific Exclusion** | This works in combination with a property on mesh components, you can add an HLOD level index for which this mesh should not be included. This allows you to only include small props for HLOD level 0, and ignore them for subsequent HLODs (as you wouldn't be able to see them from certain distances etc.) |
| **Desired Bound Radius** | The radius in which to cluster meshes together. This is not guaranteed but used to calculate filling factor for auto clustering. |
| **Desired Filling Percentage** | This is used when generating clusters, it determines how much of the cluster's bounds (sphere) is supposed to be occupied by the bounds of any actors it contains. Essentially the % of the cluster volume that has to be used by contained actors. |
| **Min Number of Actors to Build** | Min number of Actors to build LODActor. |
| **Only Generate Clusters for Volumes** | If enabled, will only generate clusters for meshes within HLOD Volumes. |

### Mesh Generation Settings

The **Mesh Generation** settings enable you to control specific properties that will be used when HLOD cluster Actors are merged, like generating lightmaps, combining Materials, transition size, and more.

Click image for full size.

| Property | Description |
| --- | --- |
| **Transition Screen Size** | This will calculate the distance to show the cluster at according to its size. It calculates the distance at which the cluster would occupy the user defined screen size, according to a fixed Field of View (FOV) / 16:9 ratio. If you would want to force all clusters to switch at a predefined distance you can do so with the **Override draw distance**. |
| **Override Draw Distance** | Forces all clusters to switch at the predefined distance specified. |
| **Simplify Mesh** | 
If enabled, the resulting mesh will be simplified. If disabled, it will just merge Actors but will not simplify using the lower LOD if it exists. For example, if you build LOD 1, it will use LOD 1 of the mesh to merge Actors if it exists. If you merge Materials, it will reduce drawcalls.



 |
| Merge Settings |   |
| **Generate Light Map UV** | When enabled, this will generate a lightmap UV for the merged mesh and assign the Lightmap Coordinate Index to 1. |
| **Target Light Map Resolution** | The lightmap resolution you'd like to use for the HLOD Actor. |
| **Computed Light Map Resolution** | Whether or not the lightmap resolution should be computed by summing the light map resolutions for the input Mesh Components. |
| **Pivot Point at Zero** | When the merged mesh should have a pivot located a the World Origin (coordinate 0,0,0), or if the pivot should be located at the first Actor listed when generating the HLOD cluster. |
| **Merge Physics Data** | When enabled, the collision primitives will be merged for the combined Actors. |
| **Merge Materials** | With this enabled the system will bake down the materials assigned to all contained meshes and combine them into a single material. This allows for reducing the draw call complexity of the merged mesh, this is only used when you merge the meshes rather than generating a proxy mesh. In case you are simplifying a mesh we will always bake the materials, and apply it to the proxy mesh. |
| **Material Settings** | See the [Material Settings](/documentation/en-us/unreal-engine/hierarchical-level-of-detail-outliner-in-unreal-engine#materialsettings) table. |
| **Gutter Size** | Sets the space, in pixels, between UV islands at the original texture resolution for the baked material. The space helps prevent the colors of your islands from overlapping. Otherwise, artifacts can appear on the mesh as downsampling of the texture occurs at render. The reduced texture sizes are known as mipmaps. |
| **Bake Vertex Data to Mesh** | When enabled, vertex data (such as vertex colors) will be baked into the resulting Proxy Mesh. |
| **Output UVs** | When enabled, any vertex colors that have been painted on the selected meshes will be incorporated into the generated HLOD Actor and Material that is created. |
| **LODSelection Type** | Enables you to define how the LOD level is determined. |
| **Specific LOD** | A given LOD level to export from the source meshes. |
| **Use Vertex Data for Baking Material** | When enabled, vertex data will be used when baking out Materials. |
| **Use Texture Binning** | This will calculate the varying output texture sizes according to their importance when packing the final atlas texture. |
| **Reuse Mesh Lightmap UVs** | Whether to attempt to re-use the source mesh's lightmap UVs when baking the Material or always generate a new set. |
| **Merge Equivalent Materials** | 

Whenever you either generate a merged mesh or a proxy mesh we need to determine which materials to bake down. Whenever this value is set, we will also merge any material instances. Say you have dynamic material instances that get generated for any of your placed props. They will essentially be the same material under the hood, but might had instance specific properties. This means when you merge them it will only use one instance for all of the meshes, this means that the final look of the HLOD mesh might be different than the original.

This can cause artifacts in the merged mesh if world position/actor position is used to determine output color.



 |
| **Use Landscape Culling** | When enabled, landscape geometry can be used to cull away (or remove) any triangle sections of the mesh that are not visible. |
| **Allow Distance Field** | 

Whether to allow distance field to be computed for this mesh. 

Disable this to save memory if the merged mesh will only be rendered in the distance.



 |

#### Material Settings

The settings here enable you to control how your Materials are packed and combined when the HLOD Actor is generated.

| Property | Description |
| --- | --- |
| **Texture Size** | Size of the generated BaseColor texture map. |
| **Texture Sizing Type** | Whether to use the specified **Texture Size** parameters for all Material properties, use automatically biased texture sizes based on **Texture Size**, or to use per property manually overridden Texture Sizes. |
| **Normal Map** | Whether to generate a Normal map. |
| **Metallic Map** | Whether to generate a Metallic map. |
| **Metallic Constant** | Enables to you set a metallic constant value in place of a texture map. |
| **Roughness Map** | Whether to generate a Roughness map. |
| **Roughness Constant** | Enables to you set a roughness constant value in place of a texture map. |
| **Specular Map** | Whether to generate a Specular map. |
| **Specular Constant** | Enables to you set a specular constant value in place of a texture map. |
| **Emissive Map** | Whether to generate an Emissive map. |
| **Opacity Map** | 
If enabled, an Opacity map will be baked out for the resulting merged Actor. This nullifies the Opacity Constant property.

Must also use the **Blend Mode** of **Translucent** to show correctly in the generated instances.



 |
| **Opacity Constant** | Only enabled if Opacity Map is disabled, this sets a constant value for the Opacity property of the resulting merged Actor's Material. |
| **Opacity Mask Map** | 

If enabled, an Opacity Mask map will be baked out for the resulting merged Actor. This nullifies the Opacity Mask Constant property.

Must also use the **Blend Mode** of **Masked** to show correctly in the generated instances.



 |
| **Opacity Mask Constant** | Only enabled if Opacity Mask Map is disabled, this sets a constant value for the Opacity Mask property of the resulting merged Actor's Material. |
| **Ambient Occlusion Map** | Whether to generate an Ambient Occlusion map. |
| **Ambient Occlusion Constant** | Enables you to set an ambient occlusion constant value in place of a texture map. |
| **Blend Mode** | Enables you to define the [Blend Mode](/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine) for Proxy Materials. |