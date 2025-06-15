# Movable Light Mobility

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:04

---

Lights that have their Mobility set to **Movable** are lights that can be or be changed dynamically in any way during runtime — these are sometimes called dynamic lights. Their performance cost is higher than those lights that are Static or Stationary, and depend on the number of meshes affected by the light along with the triangle count of those meshes. For example, a shadow-casting dynamic light with a large radius has a higher performance cost than one with a smaller radius.

Movable light's support dynamic indirect lighting when used with [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine).

Of the three light mobilities to choose from, Movable lights have varying quality (depending on the type of dynamic shadows being used), highest mutability, and highest performance cost.

## Supported Shadow Types

Movable lights support a lot more dynamic lighting and shadowing methods than Static and Stationary Lights do. The following types of shadowing are supported for lights that are Movable:

-   **Shadow Maps** provide whole scene dynamic shadows. It is the standard shadowing method for all dynamic shadowing in the engine, and they work across most platforms for all light types. Shadow maps do not provide soft area shadowing, like many of the other shadowing methods in this list.
-   [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) provide consistent, high resolution shadow maps that works well with film-quality assets and large dynamically lit open worlds. They provide soft area shadowing and work well with [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine), [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine), and [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) to deliver the highest quality at a reasonable performance cost. Virtual Shadow Maps are supported on the latest console and PC platforms that support DirectX 11 or DirectX 12.
-   [Ray Tracing Shadows](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) simulate soft area lighting effects for the highest shadowing quality at reasonable performance. They use the ray tracing architecture supported by NVIDIA GPU hardware running on Windows 10 (or later) with DirectX 12.
-   Mesh Distance Field Shadows provide lighting effects and soft area shadowing from meshes based on a distance field representation of the mesh. This method requires the distance field meshes for the project, which is needed for software ray tracing in [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine), and [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine).

## Shadow Biasing

The default shadow mapping techniques in Unreal Engine work across all platforms for Movable lights to provide dynamic shadowing. Shdaow mapping comes with some limitations that produce artifacts, such as faceted shadows on curved surfaces and shadow contact hardening at surface intersections that can make objects look like they are floating or not grounded in the scene.

Shadow biasing is a per-light set of properties that help reduce these types of artifacts while improving accuracy of self-shadowing and contact hardening from these light sources. These biasing settings work by finding a trade-off between balancing accuracy in one areas while reduing self-shadowing artifacts in another.

![Shadow Bias (Constant and Slope): Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6fde9843-aeec-4e5c-8171-66fc81ec8b73/shadowbias_actor_0.png)

![Shadow Bias (Constant and Slope): Adjusted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77bd703a-105a-4416-852c-54654787fe53/shadowbias_actor_1.png)

Adjusting the **Shadow Slope Bias** reduces self-shadowing artifacts at the loss of shadow accuracy, which can cause a peter-panning (or floating) effect for grounded objects in the scene. Slope bias adjustments won't solve *all* your self-shadowing issues with dynamic lighting, but it can solve most of them. It's up to you to decide the *right* balance for your project.

Directional Lights have an extra depth bias property that controls the bias strength across the Cascaded Shadow Maps (CSM). It reduces dicontinuities of shadow artifacts at cascade transition points.

![Shadow Bias (Constant and Slope): Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfa1192c-4ba3-44e3-a16b-1e3586472f25/shadowbias_landscape_0.png)

![Shadow Bias (Constant and Slope): Adjusted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad381db5-d6ab-4f5c-855e-e348a85a94b0/shadowbias_landscape_1.png)

The following properties are available on Lights to adjust shadow biasing:

| Property | Description |
| --- | --- |
| **Shadow Cascade Bias Distribution** | (Directional Lights Only) Controls the depth bias scaling across Cascaded Shadow Maps. It mitigates the difference in shadow artifacts between different cascade transitions. Values of 1 scales shadow bias based on each cascade's size. 0 scales shadow bias uniformly across all cascades. |
| **Shadow Bias** | Controls how accurate self shadowing of whole scene shadows are from this light source. At 0, shadows start at their shadow caster surface but there will be many artifacts. Larger values have shadows start farther from their caster and there won't be any self-shadowing artifacts, but the object may appear to float above a surface. Values around the mid-point of 0.5 is a good trade-off balance between accuracy and reduction in self-shadowing artifacts. |
| **Shadow Slope Bias** | This works in additions to Shadow Bias to control the accuracy of self-shadowing of whole scene shadows from the selected light. This property increases the amount of bias depending on the slope of a given surface. At 0, shadows start at their caster surface but will have many self-shadowing artifacts. Larger values will start shadows farther from their caster and there won't be any self-shadowing artifacts but objects might appear to float above a surface. |
| **Shadow Filter Sharpen** | Adjusts the sharpness of direct shadowing from Stationary or Movable lights. It can reduce the soft shadowing effect of shadow mapping. |

## Shadow Map Caching

Shadow map caching is a feature of Movable lights that makes shadow casting from Point and Spot Lights much more affordable in games. In Levels where you have assets that don't need to move, their shadow calculation is costing performance each frame. Shadow map caching looks at these assets that have their Mobility set to **Static** or **Stationary** and doesn't need to recalculate them each frame unless something changes with them or the light.

Shadow map caching has a significant impact on performance, especially in levels where there are a lot of assets affected by a lights.

For instance, in a moderately sized scene with three shadow-casting Movable Point lights, they could take upwards of 14 milliseconds to render shadow depths. With cached shadows enabled, those same three lights may take around 1 millisecond to render shadow depths.

Shadow map caching require memory to store the cached shadows, and for large enough scenes, you may need to adjust the amount of memory alloted to them with the console command `r.Shadow.WholeSceneShadowCacheMb`.

### Shadow Map Caching Performance

Check the performance cost of shadow map caching by enabling/disabling caching with the console command `r.Shadow.WholeSceneShadows`. Be sure to first have

You can check the performance of cached shadows by opening the stat window for shadow rendering with `Stat ShadowRendering`. Then enable/disable cached shadows with the console command `r.Shadow.WholeSceneShadows`.

|   |   |
| --- | --- |
| 
 | 

![shadow map caching disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5453f76-e88b-42f4-8670-635ad9d1cb60/smc_off.png)

 |
| Shadow Map Cashing: Enabled | Shadow Map Caching: Disabled |

### Shadow Map Caching Limitations

Shadow map caching can significantly decrease the cost of using dynamic shadowing in your Levels, but there are some limitations that must be considered when using with unsupported features of the engine.

By default, caching can only happen when the following assets meets these criteria:

-   Primitives in the Level must have their Mobility set to **Static** or **Stationary**.
-   Materials that use **World Position Offset** will not be cached.
-   **Point Lights** and **Spot Lights** are supported and must have their Mobility set to **Movable** while casting shadows.
-   Lights that move around **will not** have their shadows cached.
-   Materials that use animated **Tessellation** or **Pixel Depth Offset** can cause artifacts because their shadows will be cached but look incorrect with the asset.