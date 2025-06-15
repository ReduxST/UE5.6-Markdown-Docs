# Pivot Painter Tool 2.0

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pivot-painter-tool-2.0-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pivot-painter-tool-2.0-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:07

---

The **Pivot Painter 2.0** MAXScript stores the pivot and rotational information in the model's textures. Those textures can then be referenced inside of Unreal's shader system to create interactive effects.

The motion shown in the sample video is procedurally generated in real-time using vertex shaders. The Pivot Painter material function forms motion inheritance information for each of the model's leaves and branches. Each element is animated using its individual pivot point, direction vector, bounds size and inherited motion. The results are fluid and realistic.

Creating these types of materials has been made much simpler with the addition of the [Pivot Painter 2's Material Functions](/documentation/en-us/unreal-engine/pivot-painter-tool-1.0-in-unreal-engine). Sample content, [like that provided in Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) also helps by showing how an animation, like the one featured above, can be generated. Retrieving sub-object pivot points is now simply a matter of processing a mesh in 3D Studio Max with the Pivot Painter script, importing the files and creating a material using the available Pivot Painter functions. The sample foliage motion material function provides support for hierarchies up to 4 levels deep and 30,000 model elements.

Creating motion this way has its benefits. A model processed using this technique uses only one additional UV channel more than a standard Static Mesh, but its animations are far less expensive than skeletal animations because they are calculated in real time. Vertex shader instruction counts are generally less of a performance concern on the graphical side than pixel instruction counts, due to the number of vertices on a model generally being significantly lower than the number of pixels that the model draws.

If you'd like to explore some of the examples demonstrated in this page, you can download the [Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) project from the Epic Games Launcher and open the **PivotPainter2** map.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d186812-6645-4b74-a661-a17ffd8f6595/ce_pivotpainter2map.png)

## What's New for Pivot Painter 2.0

With Pivot Painter 2.0's release, you'll notice that there have been some improvements and changes to the MAXScript. While some options have been removed (Hierarchy Painter) or renamed (Per Object Painter to Vertex Alpha Painter), this is an improvement to the overall workflow to simplify the process of creating these types of detailed assets. This is all in service of expanding the capabilities of Pivot Painter 2 to get even better results than before, ultimately giving you the widest range of options when developing your own content! Read on below to read about the additional improvements that have been added.

### Workflow Improvements

The rigging pre-processing step is now done through the standard **Link** tool in Autodesk 3ds Max. Simply model your tree as separate, logical elements like leaves and branches. Ensure that their pivots are ideally located and oriented (X-axis down the object's length) and then link them together as one would in a traditional rig.

Ultimately, this makes producing complex foliage far simpler. You can rig one branch, duplicate it, and then place it. A re-parented branch will retain its children's hierarchical arrangement as well.

Once your tree is rigged and modeled, simply select any element within the tree and under the Render Options sections, press the **Process The Selected Object Hierarchy** button. The script will automatically traverse the selected element's hierarchy to find its root and then go back up the chain to collect and process all of its children, finally, rendering the textures using whatever data was chosen from the available Render Options.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f81cd8ba-2b62-4ded-b42c-b9cf051afb69/scriptmotion_ui.png)

This method supports both individual and linked elements at the same time. In the case of combined grass and tree models, you would select every blade at once and then an element from the tree before pressing the Process Selected Object Hierarchy button.

### Texture Coordinate Control

You now have control over which UV set is written to, enabling you to combine this system with others like the [Vertex Animation tools](/documentation/en-us/unreal-engine/vertex-animation-tool-in-unreal-engine). Also, the preferences chosen in Pivot Painter 2.0 are noted in the final output texture name as a helpful reminder.

The automated naming convention is as follows:

```
	`[MeshName]_rgb_[Current Texture RGB Choice]_a_[Alpha Choice]_[UV Channel]`
Copy full snippet
```
\[MeshName\]\_rgb\_\[Current Texture RGB Choice\]\_a\_\[Alpha Choice\]\_\[UV Channel\]

An example final output would look something like this.

```
	`ExampleMesh_rgb_PivotPos_a_ParentIndex_UV_2`
Copy full snippet
```
ExampleMesh\_rgb\_PivotPos\_a\_ParentIndex\_UV\_2

### Extensibility

The processing and rendering code has been thoroughly abstracted, resulting in a minimal amount of effort needed to add new rendering options in the future.

### New Rendering Options

As part of the improvements with the MAXScript, there is a new bit-shifting algorithm used behind the scenes that stores integers as float data. This enables the hierarchy depth and max object count to increase from 3,000 to 30,000, which is vital for representing complex foliage.

This particular tree asset contains 14,431 sub-models.

-   **16-bit RGB:**
    -   Pivot Point Location
    -   Origin Positon
    -   Origin Extents
-   **8-bit RGB:**
    -   Object Basis Vectors (one vector at a time)
-   **16-bit Alpha:**
    -   Parent Index (Int as float)
    -   Number of Steps From Root
    -   Random 0-1 Value Per Element
    -   Bounding Box Diameter
    -   Selection Order (Int as float)
    -   Normalized 0-1 Hierarchy Position
    -   Object X,Y, Z Bound Lengths From Pivot Location
    -   Parent Index (Float - Up to 2048)
-   **8-bit Alpha:**
    -   Normalized 0-1 Position in the Hierarchy
    -   Random 0-1 Value Per Element
    -   Object X,Y, Z Bounds Length (Up To 2048)

### Recreating Bounding Boxes

When using 3ds Max, the model's bounding boxes are expanded as its sub-object geometry shifts during the modeling process. The object's bounding box is left no longer being oriented or aligned to the mesh during this process. The same thing can happen when you alter the meshes' pivot transform. To counteract this, the **Recreate Bounding Boxes** section will replace the bounding box of the selected meshes with one that is properly aligned and oriented to the meshes pivot point, which is very useful for the scripts other data gathering features (Vertex Alpha Painter and Bound information).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffc88ff0-4bce-459b-80e3-abd9d80dc87e/boundingbox.png)

On the left, the model's pivot transform has been altered but the bounding box is not aligned and oriented properly. After using the Process Selected Objects button under the Recreate Bounding Boxes section, the rightmost model's bounding box has been properly aligned and oriented.

### Merge Selected Model's Normals

The Merge Selected Model's Normals feature averages out normals on multiple models where open edge vertices happen to lay on top of each other. This option will fix the normal seam issues that occur when a single model is broken into multiple pieces specifically for use with Pivot Painter.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f518f46-9b4d-4b29-b265-40cc2ecf51b2/mergemeshnormalsbutton.png) | 
![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a69977a-c445-4299-bec4-43fdecee1941/mergemeshnormals1.png)

![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b3d66a8-b387-4f19-a721-ffe5fc9f1c02/mergemeshnormals2.png)



 |
| Press the Merge Mesh Normals button to adjust the normal of any open faces that meet. | Before the Normals are merged they are aligned to each face. After they are merged the they are more closely aligned so that the edges blend together more naturally. |

## 3ds Max Version and Script Information

This tool has been tested with **3ds Max 2015** and **2016** currently. Other versions of 3ds Max have not been specifically tested, so be aware that you may run into issues when using these versions of 3ds Max.

To install the MAXScript, just drag-and-drop it from its location in **\[UE5Directory\]/Engine/Extras/3dsMaxScripts/PivotPainter2.ms** right into the 3ds Max viewport and the script will launch itself.

If you find that you are using this script a lot, you can always add it to one of the tool bars or quad menus. If you are unfamiliar how to do this the *Autodesk* site has [a very detailed walk through](http://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/3DSMax/files/GUID-A2CF8BAA-7B52-40A8-8C40-803B1AB5FC05-htm.html) that will explain the process.

### 3ds Max Unit Setup

Before you begin to use the tool you will need to first ensure that the units of measurement 3ds Max uses is set up to correctly match the units of measurement that Unreal Engine uses. This way, you can ensure that the data the tool exports from 3ds Max will work in the same manner inside the editor. Since the editor uses centimeters as its default unit of measurement, you will need to ensure that 3ds Max uses this as well. To change this setting in 3ds Max, do the following:

1.  Open up 3ds Max and from the Main Toolbar select **Customize** > **Unit Setup**.
2.  Next, click on the **System Unit Setup** button and under the **System Unit Scale** section. Use the drop-down, changing the setting from **inches** to **centimeters**. Then click the **OK** button.
3.  Finally, change the **Display Unit Scale** to **Generic Units** and then press the **OK** button.
    

## Importing Assets

When importing your assets, there are a few things you should be aware of to get the best results. Follow the setups for your **Static Meshes** and **textures** below.

### Static Meshes

In the **Import Options** window, make sure to uncheck **Skeletal Mesh** and to enable the option for **Combined Meshes**.

<table class="table" style="--columns-count: 2;"><tbody><tr><td>Static Mesh Import Options</td><td>&nbsp;</td></tr><tr><td><div><block-lightbox-md alt="" loading="lazy" src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/decafbfe-8810-48fe-9b8d-66de727ed80a/importoptions.png" width="200"></block-lightbox-md><p class="figure-caption is-separated">Click image for full size view</p></div></td><td><div><ul><li><strong>Skeletal Mesh:</strong> unchecked</li><li><strong>Combine Meshes:</strong> Enabled</li></ul></div></td></tr><tr><td>[OPTIONAL] Static Mesh Build Settings</td><td>&nbsp;</td></tr><tr><td><div><block-lightbox-md alt="SMBuildSettings" loading="lazy" src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea3d6426-b23e-4e56-a843-aab4e5b4a250/smbuildsettings.png" width="200"></block-lightbox-md><p class="figure-caption is-separated">Click image for full size view</p></div></td><td><div><ul><li><p>If you've enabled Mesh Distance Fields for your project, you may want to enable <strong>Generate Distance Field as if Two-Sided</strong> from the Static Mesh Editor Build Settings. Depending on the content, you may not want distance fields enabled at all. If that's the case you should set the <strong>Distance Field Resolution Scale</strong> to 0 or from the <strong>Level Details</strong> panel you can uncheck the option for <strong>Affect Distance Field Lighting</strong>.</p></li><li><p>For some content, you may need to enable <strong>Full Precision UVs</strong> if you notice leaves are straying from their location.</p></li></ul></div></td></tr></tbody></table>

It is recommended to do a "full" reimport (overwrite the previous model) whenever updating, instead of using the **Reimport** option. This is the safest method to prevent any material issues.

### Textures

Once you import your generated textures created with Pivot Painter 2.0, make sure to open the Texture asset and set the following:

<table class="table" style="--columns-count: 2;"><tbody><tr><td>8-bit BMP Texture Settings</td><td>&nbsp;</td></tr><tr><td><div><block-lightbox-md alt="" loading="lazy" src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdd76bee-060d-4977-b27b-670edab3dcb3/texture8bitsettings.png" width="400"></block-lightbox-md><p class="figure-caption is-separated">Click image for full size view</p></div></td><td><div><ul><li><strong>Mip Gen Settings:</strong> NoMipMaps</li><li><strong>Compression Settings:</strong> VectorDisplacementMap(RGBA8)</li><li><strong>sRGB:</strong> Unchecked</li><li><strong>Filter:</strong> Nearest</li></ul></div></td></tr><tr><td>16-bit EXR Texture Settings</td><td>&nbsp;</td></tr><tr><td><div><block-lightbox-md alt="" loading="lazy" src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d0cbe53-ae53-4a42-bb49-1bce4ff74ed5/texture16bitsettings.png" width="400"></block-lightbox-md><p class="figure-caption is-separated">Click image for full size view</p></div></td><td><div><ul><li><strong>Mip Gen Settings:</strong> NoMipMaps</li><li><strong>Compression Settings:</strong> HDR (RGB, no sRGB)</li><li><strong>sRGB:</strong> Unchecked</li><li><strong>Filter:</strong> Nearest</li></ul></div></td></tr></tbody></table>

## Writing Shaders

All of the textures rendered from Pivot Painter provide us with the tools to create simple mathematical representations of our trees' sub-object (branches and leaves). With that information, we can then start to approximate each sub-asset's reaction to a wind source enabling us to create very detailed elemental hierarchies to produce naturalistic motion.

If you desire to write your own shader, you will need to know that some of the data types need to be unpacked. These unpacking functions use the following naming convention:

```
	`ms_PivotPainter2_*`
Copy full snippet
```
ms\_PivotPainter2\_\*

The PivotPainter2FolaigeShader Material Function, as it stands, can operate as a useful Material in itself, if it fits your needs, or it can act as the scaffolding for your own version of a foliage shader. For additional information about the Material Functions available for Pivot Painter, visit the Pivot Painter Material Functions reference page.

### Pivot Painter 2 Foliage Shader

To implement Pivot Painter 2.0 animation within a Material is now fairly simple, with a lot of the back-end work already set up for you! Simply insert the **PivotPainter2FoliageShader** into your Material's code before making the final connection to the Material Attributes input pin. You'll also want to make sure to disable **Tangent Space Normals** in the Material Details panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53a08791-eac7-4bd1-929f-40b19bea8e7f/pivotpainter2foliageshader.png)

This Material Function assumes that you've processed the asset with Pivot Painter's default UV and texture settings.

Once you create a Material Instance, you will have access to the available Wind Settings that enable you to control the sub-object hierarchy. In order to make use of these, you will first need to enable the **Wind Setting** for the level(s) that you want to affect.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/456d640c-0fcf-4ae0-9a1e-62a0f7c289ac/enablewindsettings.png)

When a Wind Setting is enabled, the available options for that hierarchy depth will be visible and editable.

You'll now have access to the **Shared Wind Settings** that allows you to assign the rendered textures from Pivot Painter.

<table class="table" style="--columns-count: 2;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba52a120-d139-4b6c-be3f-e62ca56c6dab/sharedwindsettings.png" alt="" loading="lazy" width="450"></td><td><div><ul><li><strong>Position and Index Texture:</strong> Assign your rendered Pivot Positional texture to this slot.</li><li><strong>X-Vector and X-Extent Texture:</strong> Assign your rendered X-Vector and X-Extent texture to this slot.</li></ul></div></td></tr></tbody></table>

With the correct textures assigned, you can now open the **Wind Settings** groups and enable the desired features. Each Wind Setting group controls the meshes at a specific hierarchical depth. In the example of a tree, Wind Setting 1 would control the trunk, the next group, the branches and so on.

### Wind Turbulence and Gusts

This should enable you to produce fairly nice foliage animations. If they aren't tailored to your liking, you can create a new wind turbulence and gust magnitude texture. To do this, the RGB values of a vector are used to offset the wind vector and the alpha is then used to control the strength of the wind. These two channel sets are each sampled separately in the shader.

Use a texture to control vector offsets and strength of the wind for variety.

### Optimizations

It is helpful to understand how the material works when attempting to optimize the results. The PivotPainter2FoliageShader Material Function has been designed in a generic fashion. It executes the same wind reaction code 4 times. Each time another set of settings is used it is done so on a hierarchy level that is one step deeper. You can see how this works by opening the PivotPainter2FoliageShader Material Function.

Should you open the PivotPainter2FolaigeShader Material Function, you will find this network of shader functionality for the Wind Hierarchy Depths that is exposed when you create a Material Instance.

Now, you can use the sections below to understand optimizations techniques you can use.

#### Material Instances

When all the shader features are enabled you can produce a fairly expensive Material. The shader can be optimized by disabling the Wind Settings groups (or hierarchy levels of a tree) that do not need to animate. For instance, you could simply enable Wind Setting 4 to animate the model's leaves on their own. Grouping wind reaction settings by hierarchy depth mean that the model's elements should be grouped in the same fashion. All leaves should be "X" number of steps away from the root object. All branches that behave similarly should be grouped together as well. For this reason, it is recommended to set up a "parent" or "master" Material Instance for assets like trees, where you can easily have multiple hierarchies.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75af20d3-291d-4a7a-bd20-62ace374cea4/instanceparents.png)

The base Material is instanced to create your "master" Material Instance, which is used to define all of your wind settings all in one place. Then use additional Material Instances to define the pixel shader components of your hierarchy, like the base color textures for trunk, branches, and leaves. This way, you can also disable and optimize any properties not needed for that hierarchy depth.

As an example, the leaf Material Instance needs to simulate the trunk, both sets of branches, and the leaves themselves so that they properly move with the rest of the tree. The trunk, on the other hand, only needs to simulate the trunk animation, which means that you can disable the other hierarchies for the leaves and branches because they are not needed.

#### Bend Normals

Another optimization to consider, especially if you're writing your own shader or plan to edit this one is, the method that we use to bend normals. The **PivotPainter2FoliageShader** Material Function performs actual rotations to the surface Normals when the user chooses to update the normals within the shader. This could be done more cheaply (with the risk of artifacts) using custom UVs and the **BlendAngleCorrectedNormals** Material Function.

### Additional Use Example

Using the positional information and the hierarchical depth, you can create your own procedural growth or building animations like the ones below. You can also take a look at the Content Examples map **PivotPainter2** for an example of how to set these types of examples up.

|   |   |
| --- | --- |
| 
 | 

 |

These examples can be found in the **Content Examples** project available from the **Learn** tab of the Epic Games Launcher. Open up the **PivotPainter2.umap** to explore these and other examples.

## Troubleshooting

If the models seem to be animating poorly, attempt the following solutions:

-   Reimport the assets.
-   Check the model and texture settings.
-   Make sure that the Materials have **Tangent Space Normals** disabled.
-   Non-uniformly scaled meshes within 3ds Max will return incorrect transform values and will result in broken results. If this appears to be the case attempt a "Reset XForm" operation. It's always safer to non-uniformly scaled meshes via the sub-objects rather than at the object-level. It's recommended to do this before you start duplicating, parenting and placing model elements.
-   Some mesh warping appears due to optimizations are done within the shader. To properly calculate wind's effect on a branch, we would need to calculate the wind's effect on each leaf's pivot and its vector before executing each mesh rotation. Every rotation and offset operation is expensive, so we perform the mesh rotation for each element within its local space (before the other rotations are factored in). The resulting mesh offset from the rotation is then added to the other transformations. The result is less accurate but far cheaper. Sometimes the reduced accuracy will cause the foliage scale to alter a little based on the combination of offsets. So if this occurs you can try the following:
    -   Reduce the intensity of the wind simulation.
    -   Animate fewer hierarchical levels.
    -   Rotate the mesh so that the coincidence occurs less frequently.