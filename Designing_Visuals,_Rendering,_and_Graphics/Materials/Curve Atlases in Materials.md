# Curve Atlases in Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/curve-atlases-in-unreal-engine-materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/curve-atlases-in-unreal-engine-materials)  
**Processed:** 2025-06-14 16:18:02

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/957c2bef-d4d4-4dd7-9ad6-cb3f091412ad/materialgradientcurvesbanner.png "MaterialGradientCurvesBanner.png")

Curve Atlases store a combination of [Curve](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine) assets which enable you to access Curve Linear Color data through your Materials. The Curve Atlas stores any number of Curves in a texture that can be used with [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials). When creating [Material Instances](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) and changing [Material Instance Dynamics](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialinstancedynamic) (MIDs) through Blueprint, you are able to set a curve as an override, enabling you to quickly iterate and change RGBA curve values without changing your base Material.

## Curve Linear Color Asset

A **Curve Linear Color** asset is used to store the interpolated RGBA points that are evaluated over a given range, producing a color gradient that can be used with Materials.

![Curve Gradient example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ca46c5e-52df-41d2-9abc-2a17bd1de3af/curvegradient.png)

Example of a Curve Gradient created with a Curve Linear Color asset

**Right-click** in the **Content Browser**, and select **Miscellaneous > Curve** to create a new Curve Asset.

![Create Curve Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/069228c9-6fb1-4303-b7b1-532964642414/create-curve-asset.png)

In the **Pick Curve Class** dialog, select **CurveLinearColor**.

![Pick Curve Class dialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/847d2719-dc1a-4819-b152-0e05d50719e1/pick-curve-class.png)

A new Curve Linear Color asset is added to the Content Browser displaying a preview of its current gradient. Double-click the thumbnail to open the **Curve Asset Editor**, where you can add, subtract, and adjust keys for the individual RGBA curves in the graph.

![Curve Asset in Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fde724b-5e3e-4560-a986-c178d4049b03/curve-in-content-browser.png)

When you open the Curve in its Asset Editor, you'll be able to set the individual RGBA curves, adjust color values for the Curve, and preview the Curve Gradient Result.

Click image for full size.

1.  The **Curve Gradient Result** shows you the resulting gradient.
2.  The **Curve Graph** is where you add, adjust, and subtract any keys for the individual RGBA curves.
3.  The **Color** panel is where you adjust color values that affect all keys.

To add a key to an individual curve, click the curve with the **Middle Mouse Button**. A key is inserted at the mouse pointer. If you **right-click** in the empty graph and choose **Add Key** from the context menu, you can add a key on all curves at the point on the x-axis where you clicked.

## Curve Atlas Asset

A **Curve Atlas** asset is used to store and access multiple Curve assets, enabling management of gradient lookup tables (LUT). The **Curve Atlas Asset Editor** is similar to the Texture Editor, enabling you to make adjustments for Brightness, Vibrance, Hue, and more.  
![Curve Atlas Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/754c525e-44fe-45d2-aba0-b24e7e5bad3d/curve-atlas-example.png)

Example of the Curve Atlas LUT

The curves assigned to the Curve Atlas as **Gradient Curves** make up the atlas. The Material Graph uses the texture created to perform the lookup for Materials applied to Actors.

You can create a new Curve Atlas by right-clicking in the **Content Browser** and selecting **Miscellaneous > Curve Atlas**.

![Create Curve Atlas Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a446e087-042a-4ea0-8df2-f41b0d6dc1c7/create-curve-atlas.png)

When you open the Curve Atlas in its Asset Editor, you can set the number of curves it can store, assign your curves, and adjust color values for all assigned curves. This is similar to the functionality of the Texture Editor.

Click image for full size.

1.  The main viewport displays the **Curve Atlas** lookup table, which displays all assigned **Gradient Curves** for the **Texture Size** that is applied.
2.  The **Curves** panel is where you sets the **Texture Size** for the number of **Gradient Curves** you need. The default is 256. The **Gradient Curves** subcategory is where you can add Gradient Curve assets to your asset.
3.  The **Adjustments** panel makes texture adjustments to all **Gradient Curves** assigned to the Curve Atlas.

For maximum texture efficiency, it's best to use a **power of 2** value (such as 32, 64, 128). You can uncheck **Square Resolution** and change the **Texture Height** to eliminate vertical white space.

The **Texture Size** used can have an impact on the fidelity of your gradients, so it's best not to use a small atlas size for a complex curve. However, you can save texture size by using a small atlas for a set of simple curves.

To add a new Gradient Curve to the Curve Atlas, click the **Plus** (**+**) icon to add array elements. You can use the **Trash Can** icon to remove all elements from from the array.

![Add Curve Element](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d54da52-ab01-4535-bb2c-8eccc3526784/add-curve-element.png)

Use the drop-down menu next to the new array element, and in the context menu select the Curve Asset you want to add to the Curve Atlas.

![Reference curve asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16498172-7b51-4098-a9f7-a3dfeb6792f2/reference-curve-asset.png)

Each Gradient Curve you add to your Curve Atlas is displayed as a row in the Curve Atlas lookup table.

![Gradients in Curve Atlas](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1580a24f-7444-4188-80f9-c0faf3aa86b5/curve-atlas-gradient-detail.png)

## Using a Curve Atlas with Materials

After creating your Curves and applying them to a Curve Atlas, you can create a Material that references the Curve Atlas and retrieves one of the curves assigned to the atlas.

To sample one of the curves in the atlas, create a new Material and in the graph, right-click and add a **Curve Atlas Row Parameter** node.

![Curve Atlas Row Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bbab36f-0194-4835-8c90-867fca3cb83a/curve-atlas-row-parameter.png)

This node is similar to a Scalar Parameter in that it enables you to work with [Material Instance Dynamics](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine#materialinstancedynamic) (MIDs). These can then be used through Blueprint for the V-axis of the atlas UVs, but the node will do the sampling for you and return a Vector 3, along with R, G, B, and A, masks.

Select the Curve Atlas Row Parameter expression to display its **Details Panel** properties. Here you can assign the **Atlas** and select a **Curve** from that atlas to use with this Material by default.

![Curve Atlas Row Parameter properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc09a930-9e3a-465b-8f28-1878d68d8e56/curve-atlas-properties.png)

The Curve Atlas bakes down when it is compiled, which means there is currently no runtime support for changing what is in the atlas or the curve data that is stored in the atlas at runtime. However, you can store a large amount of data in a single Curve Atlas, and use Blueprint to override the curve being sampled from a Material Instance.

As an example, here is a "Rock" Material that samples one of the curves assigned to a Curve Atlas.

Click image for full size.

When you create any **Material Instances**, you can override the **Curve** Scalar Parameter to reference a different Curve in the **Curve Atlas** that is applied to your mesh.

The examples here show a Material Instance applied and the Curve that is being referenced from the Curve Atlas.

| ![Curve Base](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e798717f-cbb9-4600-85a7-59bdacac43e8/curve_base.png) | ![Curve 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d40f114-f9f5-4a5f-85ea-d84d38c0fbd5/curve_1.png) | ![Curve 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5b0ac29-e610-43f1-addf-3a94e960a4fb/curve_2.png) | ![Curve 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78a70ee2-08c8-473d-a219-30761372a30e/curve_3.png) |
| --- | --- | --- | --- |
| Base | Curve 1 | Curve 2 | Curve 3 |

### Accessing Curve Atlases through Blueprint

In Blueprint, you can set the Scalar Parameter value on a Dynamic Material Instance using the **Get Curve Position** node. Get Curve Position takes the Curve Atlas as an input, passes the scalar value to the **Set Scalar Parameter Value**, and returns a Boolean indicating whether the curve was found in the atlas.

Click image for full size.