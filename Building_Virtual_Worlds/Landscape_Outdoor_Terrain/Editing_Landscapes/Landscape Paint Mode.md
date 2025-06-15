# Landscape Paint Mode

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:25

---

The Landscape Paint mode tools adjust layer weights to selectively apply materials and modify the appearance of your landscape.

Grassy field created by artists at Quixel.

For more information about Landscape Materials, see [Landscape Material Layer Blending](/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine).

## Layers

Layers are a part of the assigned Landscape Material that define which material you are painting on your Landscape.

Landscape layers determine how the material is applied. A landscape can use multiple layers with different textures, scaling, rotation, and panning blended together to create the final textured terrain.

Each layer that is defined in the Landscape Material automatically populates the list of **Target Layers** found in the Landscape Mode panel and displays with its name and thumbnail image.

Select your active layer from the Target Layers list in the Landscape Mode panel.

The highlighted layer is applied to the landscape according to the tool’s options and [brush](/documentation/en-us/unreal-engine/landscape-brushes-in-unreal-engine) settings.

A mountain landscape painted with multiple layers.

The Paint tools manipulate the weightmap of the landscape similar to how the Sculpting tools manipulate heightmaps.

Layers are created in the Landscape Material. For more information about layers and Landscape Materials, see [Landscape Material Layer Blending](/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine).

### Layer Info Objects

A Layer Info Object is an asset that contains the weightmap and other information about a particular Landscape layer. Every Landscape layer must have a layer info object assigned to it You can create layer info objects in the Landscape Mode panel.

There are two kinds of layer info object, Weight-Blended and Non Weight-Blended:

-   **Weight-Blended** - Painting a weight-blended layer will decrease the weight of all other weight-blended layers. For example, painting mud will remove grass, and painting grass will remove mud. This is the most commonly used type of layer info object.
-   **Non Weight-Blended** - Layers that are independent of each other. Painting a non weight-blended layer does not affect the weights of the other layers. These are used for more advanced effects, such as blending snow onto other layers: instead of having grass, mud, rock *or* snow, you would use a non weight-blended snow layer to blend between "grass, mud, or rock" and "snowy grass, snowy mud, or snowy rock."

You can either create a layer info object from the layer itself, or reuse an existing layer info object from another Landscape.

**To create a layer info object:**

1.  Click the **Plus** icon to the right of the Layer name.
2.  Select **Weight-Blended Layer (normal)** or **Non Weight-Blended Layer**.
    
    ![Weight Blended Non Weight Blended](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab4eb362-e4fa-43ac-abeb-4f451ef2d75e/09-weight-blended-non-weight-blended.png "Weight Blended Non Weight Blended")
3.  Choose the save location for the new layer info object.

Layer info objects exist as assets in the **Content Browser** after creation and can be reused with other landscapes. Each layer of your landscape must use a different layer info object.

![Layer Info Object](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bdd6d7e-af82-4dcf-bd8e-39ab2b435ba5/10-layer-info-object.png "Layer Info Object")

**To reuse an existing layer info object from another Landscape:**

1.  Find and select the layer info object in the **Content Browser**.
    
2.  In the **Target Layers** section, click the Assign icon (![Assign](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92cc2f6a-752a-42ff-b815-a88dcc61ad77/11-assign.png "Assign")) to the right of the layer you want to use the layer info object.
    

Layer info objects can only be used if their layer name matches the layer they were originally created for.

The primary purpose of layer info objects is to store the weightmap data for a painted layer They also contain the following properties:

| Option | Description |
| --- | --- |
| **Layer Name** | Displays the name of the layer. |
| **Phys Material** | The [Physical Material](/documentation/en-us/unreal-engine/physical-materials-in-unreal-engine) (if any) assigned to areas of Landscape where this layer is dominant. |
| **Hardness** | The value used by the [Erosion](/documentation/en-us/unreal-engine/landscape-erosion-tool-in-unreal-engine) tool. |
| **Minimum Collision Relevance Weight** | Determines the minimum required weight needed to be considered the dominant layer. |
| **No Weight Blend** | Toggles weight blending. |
| **Layer Usage Debug Color** | Determines the color used when debugging layers. |
| **Spline Falloff Modulation** | Settings for controlling Spline Falloff Modulation. |

#### Orphaned Layers

If a layer is removed from the landscape material after it has been populated in the **Target Layers** list and it has painted data on the Landscape, it will be displayed in the list with a **?** icon. This denotes an orphaned layer.

Interface showing a missing Grass layer.

Areas previously painted with this layer likely appear black, though the exact behavior depends on your landscape material.

#### Deleting Orphaned Layers

You can delete orphaned layers from the Landscape. It is recommended that you first paint over any areas where the layer was used. Painted layer data is preserved until the layer is deleted, so no information is lost if you make a mistake in the landscape material.

To remove a layer from your Landscape, click the **X** icon to the right of the layer's name.

Click the X to delete the orphaned layer.

### Weight Editing

At each vertex in your landscape, each layer has a weight specifying how much influence that layer has on the Landscape. Layers have no particular blending order. Instead, each layer's weight is stored separately and the results added. In the case of weight-blended layers, the weight values add up to 255.

Non weight-blended layers are independent of other layers and can have any weight value.

The Paint tool increases or decreases the weight of the selected layer. For weight-blended layers, as you increase the weight of one layer, the weight of the other layers uniformly decreases. Fully painting one layer will result in no weight value on any other layer.

You can reduce the value of a weight-blended layer by holding **Ctrl + Shift** while painting. This causes the weight value of other layers to uniformly increase. Because of this, it is not possible to paint layers completely away. Instead, it is recommended to choose the layer you want to paint in its place and paint that additively.

## Using the Painting Tools

Painting tools modify the appearance of your landscape by selectively applying layers of specially designed [Landscape Materials](/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine) to portions of the landscape components.

The tools use the following controls:

| **Controls** | **Description** |
| --- | --- |
| **LMB** | Performs a stroke that applies the selected tool's effects to the selected layer. |
| **Ctrl+Shift+LMB** | Performs a stroke that applies the opposite of the selected tool's effects to the selected layer. |
| **Ctrl+Z** | Undo last stroke. |
| **Ctrl+Y** | Redo last undone stroke. |

Though each tool has specific options, they all share the following:

| **Common Option** | **Description** |
| --- | --- |
| **Tool Strength** | Determines how much effect each brush stroke has. |

### Paint

The Paint tool increases or decreases the weight of the material layer being applied to the Landscape using the currently selected brush and falloff.

| **Option** | **Description** |
| --- | --- |
| **Use Target Value** | Blends the values of the noise being applied toward a target value. |

### Smooth

The Smooth tool averages the layer weights across the area on which the tool is used. The strength determines the amount of smoothing.

**Layer Smoothing**

![Landscape Smooth Layer Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a80c8eaf-6242-473c-bfcd-b45b33c1fcd3/03-layer-smoothing-before.png "Landscape Smooth Layer Before")

![Landscape Smooth Layer After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/794e7b6e-0fa4-4a17-a040-8c0f71116ecf/04-layer-smoothing-after.png "Landscape Smooth Layer After")

| **Option** | **Description** |
| --- | --- |
| **Filter Kernal Scale** | Sets the scale multiplier for the smoothing filter kernel. |
| **Detail Smooth** | Performs a detail preserving smooth using the specified detail smoothing value. Larger detail smoothing values remove more details, while smaller values preserve more details. |

### Flatten

The Flatten tool directly sets the selected layer's weight to the value of the **Tool Strength** slider.

| **Option** | **Description** |
| --- | --- |
| **Flatten Mode** | Determines whether the tool will increase or decrease the application of the selected layer's weight, or do both. |

### Noise

This tool applies a noise filter to the layer weight. The strength determines the amount of noise.

| **Option** | **Description** |
| --- | --- |
| **Use Target Value** | Blends the values of the noise being applied toward a target value. |
| **Noise Mode** | Determines whether to apply all noise effects, only the noise effects that result in increasing the application of the layer, or only the noise effects that result in reducing the application of the layer. |
| **Noise Scale** | Determines the size of the perlin noise filter used. The noise filter is related to position and scale. If the Noise Scale does not change, the same filter is applied to the same position many times. |

### Blueprint

Landscape Blueprint Brush tool provides user-defined sculpting brushes that are used as part of a non-destructive landscape workflow. Requires the Landmass plugin to use. This tool is found under the Sculpt mode tools once the plugin is enabled.

For more information on Landscape Blueprint Brushes, see [Landscape Blueprint Brushes](/documentation/en-us/unreal-engine/landscape-blueprint-brushes-in-unreal-engine).