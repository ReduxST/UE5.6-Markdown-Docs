# Landscape Material Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-material-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-material-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:16

---

## LandscapeLayerBlend

The **Landscape Layer Blend** node blends together multiple per-layer values, such as texture samples or materials. Layers with higher blend weights have more influence on the blended result.

To add a new layer, click the plus (**+**) icon.

[![Layer Blend Array Elements](https://dev.epicgames.com/community/api/documentation/image/7c900f29-ca7f-4df3-b1fd-4150fdac90b8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7c900f29-ca7f-4df3-b1fd-4150fdac90b8?resizing_type=fit)

Click image for full size.

After you’ve added layers to the node, the Layer Names appear in the LandscapeLayerBlend node. The node has the following inputs:

[![Landscape Layer Blend Mode](https://dev.epicgames.com/community/api/documentation/image/b632b57f-f61b-4cda-a171-e47f8e98a995?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b632b57f-f61b-4cda-a171-e47f8e98a995?resizing_type=fit)

Click image for full size.

| Number | Property | Description |
| --- | --- | --- |
| 
**1**

 | 

**Layers**

 | 

Lists layers contained in the array. Add new layers by clicking the plus icon ().

 |
| 

**2**

 | 

**Additional Layers**

 | 

Shows any additional collapsed layers.

 |
| 

**3**

 | 

**Layer Name**

 | 

Displays the unique name of the layer. The **Layer Name** corresponds to the layer name used in [Paint mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine) in the Landscape tool window.

 |
| 

**4**

 | 

**Blend Type**

 | 

Defines the blend mode used by this layer. It contains the following options: **LB Alpha Blend**, **LB Height Blend**, or **LB Weight Blend.** For more information, see [Landscape Layer Blend Types](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine#landscape-layer-blend-types).

 |
| 

**5**

 | 

**Preview Weight**

 | 

Displays the weight value to use when previewing the blending in the Material Editor.

 |
| 

**6**

 | 

**Const Layer Input**

 | 

Defines an RGB value to use when you do not want to use a texture. This is used for debugging a layer.

 |
| 

**7**

 | 

**Const Height Input**

 | 

Defines a height value to use when you do not want to use a texture.

 |

The **Landscape Layer Blend** node has the following inputs and outputs:

[![Layer Blend Node](https://dev.epicgames.com/community/api/documentation/image/202f23be-ca5b-466c-964f-20bde280e751?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/202f23be-ca5b-466c-964f-20bde280e751?resizing_type=fit)

Click image for full size.

| Number | Item | Description |
| --- | --- | --- |
| 
**1**

 | 

**Layer *Layer Name***

 | 

Displays the unique name of the layer. This input is only available after you have added and names layers in the **Details** panel.

 |
| 

**2**

 | 

**Height *Layer Name***

 | 

Defines a height map to blend with the named layer. This input is only visible on layers where the **Blend Type** property is set to **LB Height Blend**.

 |
| 

**3**

 | 

**Output**

 | 

Outputs the blended result.

 |

All layer names must be unique. It is recommended to name your layers with a descriptive name that indicates the layer’s contents.

When you use the LB Height Blend mode for multiple Landscape layers, you may find black spots on your Landscape where different layers meet. LB Height Blend works by managing the blend factor, or weight, for the layer, using the specified height value. When multiple layers are painted on an area and are set to LB Height Blend, the layers painted in a particular area can simultaneously have a 0 height value, so the desired blend factor for each layer becomes `0`.

Because there is no specific ordering, black spots can appear because no layers have any contributions in that area. When you blend a Normal map, even more black spots can appear, because this blending results in a Normal value of (0,0,0), which is invalid and causes lighting issues. If this happens, paint the area with a material with a non-zero weight.

In the left image, all layers are LB Height Blend, causing some areas to be black. On the right, the red "1" layer has been changed to use LB Alpha Blend.

[![LB Height Blend Problem](https://dev.epicgames.com/community/api/documentation/image/e4f2b94a-1c22-49f2-971a-b398833bb166?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e4f2b94a-1c22-49f2-971a-b398833bb166?resizing_type=fit)

Click image for full size.

Below is an example of the properties of the **Landscape Layer Blend** node for all the layers being blended together. The **Soil** layer has its blend mode set to LB Alpha Blend, while the other layers have theirs set to LB Height Blend. This is to stop the issue mentioned above from happening.

[![Layer Blend Properties](https://dev.epicgames.com/community/api/documentation/image/ec4d7ab9-a269-431e-b705-45ad4a6b28df?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ec4d7ab9-a269-431e-b705-45ad4a6b28df?resizing_type=fit)

Click image for full size.

To delete a layer, click the dropdown arrow to the right of the layer's element number, and select **Delete**.

[![Delete Layer](https://dev.epicgames.com/community/api/documentation/image/f638880b-3dc4-44c7-b2fa-b462629fe914?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f638880b-3dc4-44c7-b2fa-b462629fe914?resizing_type=fit)

Click image for full size.

## LandscapeLayerCoords

The **Landscape Layer Coords** node generates UV coordinates used for mapping the Landscape Material onto Landscapes.

[![Landscape Layer Coords Node](https://dev.epicgames.com/community/api/documentation/image/a237623c-ffdf-4378-ba52-66d9474893fa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a237623c-ffdf-4378-ba52-66d9474893fa?resizing_type=fit)

Click image for full size.

This node has the following options:

| Number | Property | Description |
| --- | --- | --- |
| 
1

 | 

**Mapping Type**

 | 

Specifies the orientation to use when mapping the Material or network to the Landscape. It contains the following options:

-   **TCMT Auto**: Uses landscape vertex coordinates, in the range \[0, OverallLandscapeResolution\]
    
-   **TCMT XY**: Uses object space XY mapping. This is equivalent to TCMT Auto.
    
-   **TCMT XZ**: Uses object space XZ mapping. Recommended for side-projected textures.
    
-   **TCMT YZ**: Uses object space YZ mapping. Recommended for side-projected textures.
    

 |
| 

2

 | 

**Custom UVType**

 | 

Outputs the UV coordinates to map the Material to the Landscape based on the type. It contains the following options:

-   **LCCT None**: Do not use custom UVs.
    
-   **LCCT Custom UV0**: Use custom UVs in channel 0.
    
-   **LCCT Custom UV1**: Use custom UVs in channel 1.
    
-   **LCCT Custom UV2**: Use custom UVs in channel 2.
    
-   **LCCT Weight Map UV**: Use original Weightmap UVs.
    

 |
| 

3

 | 

**Mapping Scale**

 | 

Applies uniform scaling to the UV coordinates.

 |
| 

4

 | 

**Mapping Rotation**

 | 

Applies the rotation, in degrees, to the UV coordinates.

 |
| 

5

 | 

**Mapping Pan \[U\]**

 | 

Applies the offset in the \[U\] direction to the UV coordinates.

 |
| 

6

 | 

**Mapping Pan \[V\]**

 | 

Applies the offset in the \[V\] direction to the UV coordinates.

 |
| 

7

 | 

**Unlabeled Output**

 | 

Outputs the UV coordinates to map the material to the Landscape based on the given property values.

 |

## LandscapeLayerSwitch

You can use the **Landscape Layer Switch** node to exclude some Material operations when a specific layer is not contributing to a region of the Landscape. You can use this to optimize your Material by removing calculations that are not necessary when a layer's weight is zero.

[![Landscape Layer Switch Node](https://dev.epicgames.com/community/api/documentation/image/d0d94b25-1733-4738-a0b8-3bbf5be80f7d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d0d94b25-1733-4738-a0b8-3bbf5be80f7d?resizing_type=fit)

Click image for full size.

This node has the following options:

| Number | Property | Description |
| --- | --- | --- |
| 
1

 | 

**Parameter Name**

 | 

Displays the unique name of the parameter.

 |
| 

2

 | 

**Preview Used**

 | 

If checked, uses a preview.

 |
| 

3

 | 

**Layer Used**

 | 

Indicates the material network to use if the specific layer is in use by the current region of the Landscape.

 |
| 

4

 | 

**Layer Not Used**

 | 

Indicates the material network to use if the specific layer is not used by the current region of the Landscape.

 |
| 

5

 | 

**Output**

 | 

Either the **Layer Used** or **Layer Not Used** inputs, depending on whether the layer contributes to the particular region of the Landscape.

 |

## LandscapeLayerWeight

You can use the **Landscape Layer Weight** node to access layer weights and implement your own custom blending solution in the material graph. The output returns (Base + Layer \* LayerWeight). By chaining multiple Landscape Layer Weight nodes together, you can produce a weighted sum that blends between the specified layers.

You can directly access the LayerWeight value without modification by setting the Base value to 0 and the Layer value to `1.0`.

[![Landscape Layer Weight Node](https://dev.epicgames.com/community/api/documentation/image/1cfa415f-6781-4e97-9155-476772833f95?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1cfa415f-6781-4e97-9155-476772833f95?resizing_type=fit)

Click image for full size.

This node has the following options:

| Number | Property | Description |
| --- | --- | --- |
| 
1

 | 

**Parameter Name**

 | 

Displays the name of the layer whose weight you want to read.

 |
| 

2

 | 

**Preview Weight**

 | 

Defines the weight to use for preview purposes in the Material Editor.

 |
| 

3

 | 

**Const Base**

 | 

Defines a specific RGB constant value to use when Base is not connected.

 |
| 

4

 | 

**Base**

 | 

The node network to blend with this layer. This includes the value of the previous layers and any other underlying data. This gives the layer value multiplied by the painted layer weight.

 |
| 

5

 | 

**Layer**

 | 

The value for the specified layer. This input value is multiplied by the layer weight and accumulated onto Base to produce the Output value.

 |
| 

6

 | 

**Output**

 | 

Outputs the result of the blending between the **Base** and **Layer** inputs, based on the layer weights of the inputs.

 |

## LandscapeVisibilityMask

The **Landscape Visibility Mask** node outputs the visibility value of the landscape.

[![Landscape Visibility Mask Node](https://dev.epicgames.com/community/api/documentation/image/1ee8b585-5c84-4421-a0cc-dbc07f86f965?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1ee8b585-5c84-4421-a0cc-dbc07f86f965?resizing_type=fit)

Click image for full size.

This node has the following options:

| Number | Property | Description |
| --- | --- | --- |
| 
1

 | 

**Output**

 | 

Outputs the visibility mask value. The value is `0.0` where the landscape is transparent and `1.0` where the landscape is visible.

 |

[![Layer Visibility Mask Opacity Mask](https://dev.epicgames.com/community/api/documentation/image/05e8047d-fadc-4290-9a01-56d2c20dcf2f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/05e8047d-fadc-4290-9a01-56d2c20dcf2f?resizing_type=fit)

Click image for full size.