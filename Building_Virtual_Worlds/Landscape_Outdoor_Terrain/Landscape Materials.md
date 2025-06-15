# Landscape Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:17

---

Unreal Engine (UE) provides several landscape-specific [Material](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials) nodes that can help improve the textures for your Landscape. You can use the nodes alongside any other Material in UE.

You can create and modify Landscape Materials in the [Material Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide) in the same way as other materials.

## Layer Weights and Ordering

Landscape materials operate as a blend between multiple layers, where painted blend weights control the influence of each layer.

The material graph determines how the weights are interpreted to achieve the blended result. The blending method defines how the landscape uses those weights in the final result.

There are two possible blending modes: weight blending and alpha blending. You can use these methods together to create different effects, such as snow on top of your grass and dirt layers.

| Blending Mode | Description |
| --- | --- |
| 
**Weight Blending**

 | 

Assigns a value between `0` and `1.0` to each layer of the material, which indicates a corresponding percentage value. Landscape Paint tools ensure that the weight value of all weight blended layers does not exceed `1.0`. The excess value is removed and the other layers scale down appropriately, so that a total of 100% remains.

When one layer is painted to 100%, the weight values for all other layers are 0%. This means that when you use the [Paint](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine) tool to remove the layer that is at 100%, there is nothing to replace it with, because all other layers are valued at 0%. This makes it appear as if the layer hasn’t changed.



 |
| 

**Alpha Blending**

 | 

Assigns each layer an alpha percentage value between 0 and 100%. If your material graph is set up for ordered blending, this method respects the order in which the layers are applied.

The alpha layer exists separately from the other weighted layers, so when the alpha layer weight increases, other existing layer weights decrease.

 |

## Landscape Specific Material Nodes

Inside the [Material Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide), there are several specific nodes that you can use with the Landscape system. You can find these nodes by right-clicking and searching the context sensitive menu, or by searching in the **Palette** menu.

[![Material Editor Context Menu](https://dev.epicgames.com/community/api/documentation/image/08b01354-4135-4db6-8d53-d0c0afcc9aa9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/08b01354-4135-4db6-8d53-d0c0afcc9aa9?resizing_type=fit)

Click image for full size.

### Landscape Layer Blend Node

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

### Landscape Layer Coords Node

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

### Landscape Layer Switch Node

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

### Landscape Layer Weight Node

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

### Landscape Visibility Mask Node

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

You can create a separate Landscape Hole Material. You can use the same Material for your Landscape Material and your Landscape Hole Material, but Materials using opacity masks are more costly performance-wise.

## Landscape Layer Blend Types

The Landscape **Layer Blend** node has three blend modes. Each different **Layer Blend** type is used to achieve a different result.

| Blend Type | Function |
| --- | --- |
| 
**LB Weight Blend**

 | 

Implements a weighted blend between all LB Weight Blend layers. This type is not order dependent.

 |
| 

**LB Alpha Blend**

 | 

Implements an alpha-blended overlay on top of the LB Weight Blend and LB Height Blend layers. Each LB Alpha Blend layer applies in the order they appear in the list. For example, painting snow over rock and grass occludes both, but erasing snow reveals the rock and grass beneath it.

 |
| 

**LB Height Blend**

 | 

This is the same as LB Weight Blend, but also adds detail to the transition between layers based on a height map. For example, you can have dirt appear in the gaps between rocks at the layer transition point, instead of just smoothly blending between rock and dirt.

 |

Below is an example of **LB Height Blend**:

[![LB Height Blend](https://dev.epicgames.com/community/api/documentation/image/9aa770aa-16a6-4bc2-bf28-54027f85a216?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9aa770aa-16a6-4bc2-bf28-54027f85a216?resizing_type=fit)

The dirt appears in the gaps between rocks at the layer transition point, creating a smooth transition where the layers meet.

## Landscape Layer Blend Technical Information

Landscape layer nodes behave similar to a [Static Switch Parameter](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#static-switch-parameter) node. This switches between using one branch of the Material and another. Each component of the Landscape has its own **Material Instance Constant** created from the main Landscape Material, which is applied to only that component.

If a Landscape component does not use a specific layer, the subtree of nodes connected to the layer is discarded. This reduces the complexity, letting the Material applied to the Landscape contain any number of texture samples, as long as it is within the limits set by the shader model.

Using this method, you can create a master Landscape Material that contains every texture or material you need, while keeping the final result within the parameters allowed by the hardware.

Any network of material expressions can be connected to the **Layer** inputs in place of a simple **Texture Sample**. This makes it possible to do more complex effects such as transitioning from detail textures to larger macro textures depending on the distance the layer is being viewed from.

## Layer Blend Issues

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

## Mobile Landscape Materials

You can use any number of Landscape layers, as long as you have enough Texture Sampler nodes. The Landscape layer allocation uses the [Feature Level Switch material node](https://dev.epicgames.com/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine), letting a single PC or Console Landscape Material also have a Mobile version. The following image shows how the Landscape in *Fortnite* Battle Royale looks when used for mobile devices.

[![Mobile Landscape Feature Level](https://dev.epicgames.com/community/api/documentation/image/3aa88cc1-d48d-474c-b584-0cd50e5495b4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3aa88cc1-d48d-474c-b584-0cd50e5495b4?resizing_type=fit)

While you can use any number of nodes, we recommend that you only use three.

## Using Layer Blending

Blending multiple textures and material networks into paintable Landscape layers is the basis for texturing Landscape terrains. There are two methods:

1.  Use multiple **Landscape Layer Weight** nodes.
    
2.  Use up to two **Landscape Layer Blend** nodes.
    

### Landscape Layer Weight Nodes

To set up the **LandscapeLayerWeight** node:

1.  In the **Material Editor**, add a **LandscapeLayerWeight** node.
    
    [![Landscape Layer Weight Base](https://dev.epicgames.com/community/api/documentation/image/a37d6f07-367b-4cee-8130-caeb6f09f2fd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a37d6f07-367b-4cee-8130-caeb6f09f2fd?resizing_type=fit)
    
    Click image for full size.
    
2.  In the **Details** panel, change the **Parameter Name** to a descriptive name for the layer, for example, "Rock".
    
    [![Layer Name](https://dev.epicgames.com/community/api/documentation/image/dbe8b08a-f59c-4bdf-bcf1-3757e99fbe52?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dbe8b08a-f59c-4bdf-bcf1-3757e99fbe52?resizing_type=fit)
    
    Click image for full size.
    
    All layer names must be unique. It is recommended to name your layers with a descriptive name that indicates the layer’s contents.
    
3.  Add additional **Landscape Layer Weight** nodes, until you have one for each layer that you want your Material to have. This example uses two **LandscapeLayerWeight** nodes.
    
4.  Add and connect your **Texture Samples** or material network expressions to your **Landscape Layer Weight** nodes.
    
5.  Add a **LandscapeLayerCoords** node and set the UV titling. Connect it to the **Texture Sample** nodes.
    
6.  Connect each **Layer** node's output pin to the **Base** pin of the next layer node, while leaving the first layer node's **Base** pin unconnected.
    
7.  Connect the last **Layer** node's output pin to the **Base Color** input of the Material's **Base** node.
    

You should have something similar to the example below:

[![Landscape Layer Nodes](https://dev.epicgames.com/community/api/documentation/image/10c4421b-27b0-4484-bb3e-ad5389f4bb01?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/10c4421b-27b0-4484-bb3e-ad5389f4bb01?resizing_type=fit)

Click image for full size.

You can preview the effects of different weights on the Material by changing the **Preview Weight** properties of the **LandscapeLayerWeight** nodes.

### Landscape Layer Blend Nodes

As an alternative to manually blending layers using the **LandscapeLayerWeight** node, the **LandscapeLayerBlend** node automatically blends multiple layers together using either alpha blending or alpha blending with a height-based offset. The height-based offset lets a layer blend with other layers based on a heightmap input.

1.  In the **Material Editor**, add a **LandscapeLayerBlend** node.
    
2.  In the **Details** panel, next to **Layers**, click the plus icon () to add a layer.
    
    [![Layer Blend Array Elements](https://dev.epicgames.com/community/api/documentation/image/d4e68745-1cd8-4378-a7cf-235c6b3eac3d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d4e68745-1cd8-4378-a7cf-235c6b3eac3d?resizing_type=fit)
    
    Click image for full size.
    
3.  Expand the layer to view its properties.
    
4.  Change the **Layer Name** to a descriptive name for the layer, for example, "Snow".
    
    [![Layer Name](https://dev.epicgames.com/community/api/documentation/image/11b3d3a2-4f16-4be3-a4ff-d00288453323?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/11b3d3a2-4f16-4be3-a4ff-d00288453323?resizing_type=fit)
    
    Click image for full size.
    
5.  Determine whether you want the layer to be alpha blended or height blended, and set the **Blend Type** accordingly.
    
6.  Add as many additional layers as you want for your Landscape Material. Rename them, and set their **Blend Types** appropriately.
    
7.  Connect the LandscapeLayerBlend node's output to the **Base Color** input of your Material's base node.
    
8.  Add Texture Sample nodes, and connect their main outputs to the **Layer** inputs of the **LandscapeLayerBlend** nodes. Alternatively, you can create a more complex material network and connect it to the Landscape Layer Blend **Layer** input. For any height-blended layers, connect the Texture Sample's alpha output to the LandscapeLayerBlend's **Height** input.
    

When you are done, your Landscape Material network should look something like this:

[![Landscape Blend Node](https://dev.epicgames.com/community/api/documentation/image/e0f4157e-272f-4e40-b734-d9e6b8a752ae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0f4157e-272f-4e40-b734-d9e6b8a752ae?resizing_type=fit)

Click image for full size.

You can preview the effects of different weights on the Material by changing the **Preview Weight** properties of the **LandscapeLayerBlend** nodes.

## Creating Landscape Hole Materials

You can use a Landscape Hole Material to mask out the visibility and collision of specific locations to create holes in your Landscape for tunnels and caves.

1.  Open the Material Editor, and in the **Details** panel set the **Blend Mode** to **Masked**.
    
    [![Layer Visibility Mask Opacity Mask](https://dev.epicgames.com/community/api/documentation/image/a666aacf-b331-47be-ad10-60d6620bc259?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a666aacf-b331-47be-ad10-60d6620bc259?resizing_type=fit)
    
    Click image for full size.
    
2.  Add a **LandscapeVisibilityMask** node to the Material Graph, and connect its output to the **Opacity Mask** input.
    
    [![Landscape Visibility Mask Node](https://dev.epicgames.com/community/api/documentation/image/9f238056-99ae-48f7-8791-4321823abe03?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9f238056-99ae-48f7-8791-4321823abe03?resizing_type=fit)
    
    Click image for full size.
    
3.  Once the material has been compiled, assign it to the Landscape. This can be done in the **Landscape Hole Material** section in the **Details** panel.
    
    [![Landscape Hole Material](https://dev.epicgames.com/community/api/documentation/image/27f5faa3-c13e-4d2e-93c1-9563e51efa8d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/27f5faa3-c13e-4d2e-93c1-9563e51efa8d?resizing_type=fit)
    
    Click image for full size.
    
4.  Set up the rest of your Landscape Material. When completed, you should have something similar to this.
    
    [![Landscape Visibility Mask Setup In Material](https://dev.epicgames.com/community/api/documentation/image/02134a80-9296-447e-a9ce-98645ee997b5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/02134a80-9296-447e-a9ce-98645ee997b5?resizing_type=fit)
    
    Click image for full size.
    

You should now be able to mask and unmask the visibility of your terrain, like in the video below.

For information about using the painting tools to create a Landscape hole, see [Using Opacity Masking to Create a Hole](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine).

## Assigning Materials to Landscapes

After creating a Landscape Material, assign the Material to a Landscape Actor in your level.

1.  In the **Content Browser**, locate the Landscape Material that you want to use.
    
2.  Either in the viewport or using the **World Outliner**, select the Landscape.
    
3.  In the **Details** panel for the Landscape, locate the **Landscape Material** option, and click the Assign arrow () to assign the selected Material.
    
    [![Assigned Material](https://dev.epicgames.com/community/api/documentation/image/a943cdfa-913a-4efd-ac3c-5e582f8d1f89?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a943cdfa-913a-4efd-ac3c-5e582f8d1f89?resizing_type=fit)
    
    Click image for full size.
    

### Assign a Landscape Hole Material to a Landscape

You can assign different Materials to act as the **Landscape Hole Material**, which is a Material with specific opacity settings.

For general information on hole materials, see the section on Landscape Hole Materials. For information on opacity masking, see [Using Opacity Masking to Create a Hole](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine).

1.  In the **Content Browser**, find and select the Landscape Hole Material that you want to use
    
2.  Either in the viewport or in the **World Outliner**, select the Landscape.
    
3.  Navigate to **Details > Landscape > Landscape Hole Material**. To assign the selected MaterialSelect the arrow ().
    
    [![Landscape Hole Material](https://dev.epicgames.com/community/api/documentation/image/425d74cc-9b53-4c45-8eec-5718f41958c9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/425d74cc-9b53-4c45-8eec-5718f41958c9?resizing_type=fit)
    
    Click image for full size.