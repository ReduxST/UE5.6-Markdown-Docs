# Landscape Noise Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-noise-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-noise-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:20

---

The **Noise** tool applies a noise filter to produce variations in the surface of the Landscape heightmap.

## Using the Noise Tool

In this example, the Noise tool is used to paint on the Landscape, similarly to how Sculpt would be used, and in doing so variations are painted around this area that raise and lower the heightmap based on the tool settings. This enable you to paint grande or subtle variations into your Landscape.

Use the following controls to Sculpt with Noise for your Landscape heightmap:

| **Controls** | **Operation** |
| --- | --- |
| **Left Mouse Button** | Heightens or increases the heightmap or selected layer's weight. |

![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7909b75-2a14-4fcd-8ede-b6d042748b03/01-before-noise.png "Before")

![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7aac8b6e-f947-49d4-bcb5-e5fb24bd1ee1/02-after-noise.png "After")

In this example, Noise has been painted onto the smooth Landscape surface giving it variations in different heights based on the strength and property values used.

## Tool Settings

|   |   |
| --- | --- |
| ![Noise Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ca4f819-1fdf-4696-a8d9-49d693ea2af5/03-noise-tool.png "Noise Tool") | ![Noise Tool Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c52518bf-032c-4adc-8440-b53f02a98b23/04-noise-tool-properties.png "Noise Tool Properties") |

| **Property** | **Description** |
| --- | --- |
| **Tool Strength** | Controls how much effect each brush stroke has. |
| **Use Target Value** | If checked, blends the values of the noise being applied toward a target value. |
| **Noise Mode** | 
Determines whether to apply all noise effects, only the noise effects that result in raising the heightmap, or only the noise effects that result in lowering the heightmap.

-   **Both**: Raises and lowers values for painted values of Noise to the heightmap when the mouse click is activated.
-   **Add**: Raises values when painting Noise to the heightmap when the mouse click is activated.
-   **Sub**: Lowers values when painting Noise to the heightmap when the mouse click is activated.



 |
| **Noise Scale** | The size of the perlin noise filter used. The noise filter is related to position and scale, which means if you do not change **Noise Scale**, the same filter is applied to the same position many times. |

The brush strength determines the amount of raising or lowering that can happen when using the Noise tool.