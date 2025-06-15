# Landscape Erosion Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-erosion-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-erosion-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:09

---

The **Erosion** tool uses a thermal erosion simulation to adjust the height of the Landscape heightmap. This simulates the transfer of soil from higher elevations to lower elevations by natural forces. The larger the difference in elevation, the more erosion will occur. This tool also applies a noise effect on top of the erosion, if desired, to provide a more natural random appearance.

## Using the Erosion Tool

In this example, the Erosion tool is being used on the front and back sides of the mountain face. On the front side, the incline is not as steep, so the surface is not eroded as quickly with the settings being used. However, on the back side, the incline is much steeper and erodes much more quickly.

Use the following controls to Sculpt with Erosion for your Landscape heightmap:

| **Controls** | **Operation** |
| --- | --- |
| **Left Mouse Button** | Applies erosion values that raises, lowers, or does both to the the heightmap. |

![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d407798d-d382-4224-abd8-21a22b39def5/01-before-erosion.png "Before")

![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2338be55-1629-457a-8026-a523efd68287/02-after-erosion.png "After")

In this example, Erosion uses noise painted onto the hillside to raise or lower the surface giving it variations in different heights based on the strength and various property values used to drive the erosion being applied.

## Tool Settings

|   |   |
| --- | --- |
| ![Erosion Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cba65f1b-8339-4f36-84e8-0f3272e6673d/03-erosion-tool.png) | ![Erosion Tool Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dd91b54-ab57-41cb-a648-c7007d23221b/04-erosion-tool-properties.png) |

| **Property** | **Description** |
| --- | --- |
| **Tool Strength** | Controls how much effect each brush stroke has. |
| **Threshold** | The minimum height difference necessary for the erosion effects to be applied. Smaller values will result in more erosion being applied. |
| **Surface Thickness** | The thickness of the surface for the layer weight erosion effect. |
| **Iterations** | The number of iterations performed. Larger values result in more levels of erosion. |
| **Noise Mode** | 
Whether to apply noise to raise or lower the heightmap, or do both:

-   **Both**: Raises and lowers values for all erosion effects applied to the heightmap.
-   **Raise**: Applies erosion effects that result in raising the heightmap.
-   **Lower**: Applies erosion effects that result in lowering the heightmap.



 |
| **Noise Scale** | The size of the noise filter used. The noise filter is related to position and scale, which means if you do not change **Noise Scale**, the same filter is applied to the same position many times. |