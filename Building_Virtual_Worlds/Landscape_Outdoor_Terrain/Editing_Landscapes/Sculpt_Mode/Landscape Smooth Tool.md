# Landscape Smooth Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-smooth-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-smooth-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:36

---

The **Smooth** tool will soften the heightmaps painted values to give your Landscape a smoother flow and appearance by getting rid of jagged artifacts that can sometimes happen after using the Sculpting or Erosion tools.

## Using the Smooth Tool

In this example, the Smooth tool is used to soften some of the harder edge artifacts that can happen when using the various Landscape tools.

Use the following controls to sculpt your Landscape heightmap:

| **Controls** | **Operation** |
| --- | --- |
| **Left Mouse Button** | Smoothens and softens the heightmap or selected layer's weight. |

![Before Smoothing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41c71c1a-58e9-4288-94c9-d248b88b3109/01-before-smoothing.png "Before Smoothing")

![After Smoothing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58b09cba-9614-4542-8994-8923f8d2d68a/02-after-smoothing.png "After Smoothing")

The Brush Strength determines the amount of smoothing that can happen when using the Smooth tool.

## Tool Settings

|   |   |
| --- | --- |
| ![Landscape Smooth Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93efcb82-d8ac-4d15-bc51-a1cfee0c3449/03-landscape-smooth-button.png "Landscape Smooth Button") | ![Smooth Tool Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b4f3130-4f08-4833-8f63-aae8cf3c3316/04-smooth-tool-properties.png "Smooth Tool Properties") |

| **Property** | **Description** |
| --- | --- |
| **Tool Strength** | Controls how much smoothing occurs with each brush stroke. |
| **Filter Kernel Scale** | Sets the scale multiplier for the smoothing filter kernel for the radius that smoothing will be performed over. Higher values smooth out bigger details, while lower values only smooth out smaller details. |
| **Detail Smooth** | If checked, performs a detail-preserving smoothing using the specified detail-smoothing value. Larger-detail smoothing values remove more details, while smaller values preserve more details. |