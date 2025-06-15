# Volumetric Lightmaps

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-lightmaps-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-lightmaps-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:45

---

Volumetric Lightmaps replace the [Indirect Lighting Cache](/documentation/en-us/unreal-engine/indirect-lighting-cache-in-unreal-engine) and Volume Lighting Samples going forward.

The Indirect Lighting Cache can be re-enabled by opening the **World Settings > Lightmass Settings** and setting the **Volume Lighting Method** to **Sparse Volume Lighting Samples**.

Lightmass generates [surface lightmaps](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine) for indirect lighting on static objects. However, dynamic objects (like characters) need a method of receiving indirect lighting as well. This is done by storing precomputed lighting in all points in space called a **Volumetric Lightmap** at build-time and then used for interpolation at runtime for indirect lighting of dynamic objects.

![Sparse Volume Lighting Samples | (Old Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e9807f0-3403-4ea1-88b8-16027f7ba5b8/01-volumetric-lightmaps-lit-movable-character-ilc.png)

![Volumetric Lightmaps | (New Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e05a249e-4d88-48bb-b852-40f9f3a77370/02-volumetric-lightmaps-lit-movable-character-vlm.png)

Sparse Volume Lighting Samples determined leaking amounts and lighting accuracy. Volumetric Lightmaps improve upon this.

## How It Works

From a high-level, the Volumetric Lightmaps system works in the following manner:

-   Lightmass places lighting samples throughout the level and computes indirect lighting for them during the lighting build.
-   When it comes time to render a dynamic object, the Volumetric Lightmap is interpolated to each pixel being shaded, providing precomputed indirect lighting.
-   If no built lighting is available (meaning the object is new or has moved too much), lighting is interpolated to each pixel from the Volumetric Lightmap for **Static** objects until lighting is rebuilt.

When a Lightmass Importance Volume is placed, the Volumetric Lightmap builds bricks that are made up of 4x4x4 cells (lighting samples). When lightmass is run, the cells are placed over the whole Lightmass Importance Volume and then it uses more cells around static geometry in the scene to capture better indirect lighting results.

![Example of visualization the Volumetric Lightmap](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0960fe12-7dd6-4fc0-98ac-cd8367bb41f8/03-volumetric-lightmaps-cube-vlm.png)

Each of these points (or spheres) is a Volumetric Lightmap lighting sample, which uses a Third Order Spherical Harmonic to store the incoming lighting in all directions.

![Example of visualization the Volumetric Lightmap](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3884693d-e27c-4b0c-b2d0-a40750989a4e/04-volumetric-lightmaps-sphere.png)

Near objects, any static geometry that is within one of the bricks will use more cells where indirect lighting changes the most. This data structure enables interpolation of indirect lighting to any point in space on the GPU.

![The example of the static geometry density representation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/206c630a-b852-42f9-b71e-dd215f195464/05-volumetric-lightmaps-vlm-density.png)

(From left to right) A Lightmass Importance Volume with a single Static Mesh placed within the volume. Cells around the static geometry are higher-density; An example representation of a single side of a brick showing the placement of 4x4x4 cells; The same example representation of cells with higher-density when static geometry is present during a lighting build.

### Enabling Volumetric Lightmap Visualization

Use the view mode for **Volumetric Lightmap** to visualize the lighting samples in the level viewport by clicking **Show > Visualize > Volumetric Lightmap**.

|   |   |
| --- | --- |
| 
 | 

 |
| Enable Volumetric Lightmap view mode | Visualization Volumetric Lightmap lighting samples |
| *Click image for full size.* | *Click image for full size.* |

When visualizing the Volumetric Lightmap after a lighting build, you can see the density of the lighting samples that gathers around static geometry based on the cells within the Lightmass Importance Volume that is affected. Lighting Samples farther away from the static geometry are less dense since they do not have any geometry near them.

![Sparse Volume Lighting Samples | (Old Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15641cd8-fb44-42b5-9ae9-926ae593fc01/08-volumetric-lightmaps-ilc-placement.png)

![Volumetric Lightmaps | (New Method) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dcfa1a4-5576-41a2-96a0-47559a645ae1/09-volumetric-lightmaps-vlm-placement.png)

The [Indirect Lighting Cache](/documentation/en-us/unreal-engine/indirect-lighting-cache-in-unreal-engine) only placed lighting samples above the surface of static geometry. The Volumetric Lightmap places samples in high-densities around static geometry for more detail where indirect lighting changes the most.

### Previewing Unbuilt Lighting

The Volumetric Lightmap allows previewing of objects with unbuilt lighting. When you move a Static Mesh that had lighting previously built for it, it will automatically switch to the Volumetric Lightmaps until the next lighting build.

![Indirect Lighting Cache | (Old Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f9353ab-4a09-44b1-bfe2-07cf23d2e439/10-volumetric-lightmaps-unbuild-ilc.png)

![Volumetric Lightmap | (New Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da6034ce-8e2b-4a44-9511-016e9f77c6f6/11-volumetric-lightmaps-unbuild-vlm.png)

The column in the center has been copied and is now lit by the Volumetric Lightmap until lighting is built again.

### Precomputed Lighting on Movable Objects

Unlike the [Indirect Lighting Cache](/documentation/en-us/unreal-engine/indirect-lighting-cache-in-unreal-engine) where interpolation between a lighting sample happens once for the whole component, the Volumetric Lightmap allows for more detail by interpolating to each pixel instead. This leads to a reliable distribution of detail that results in fewer cases of light leaking.

![Indirect Lighting Cache  | (Old Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bd7c7ab-d730-4684-9148-baffd4f13c70/12-volumetric-lightmaps-movable-character-ilc.png)

![Volumetric Lightmap  | (New Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09e82599-e435-464a-ac60-b15977864d5a/13-volumetric-lightmaps-movable-character-vlm.png)

The added detail of Volumetric Lightmaps blends the character better with the environment.

![Indirect Lighting Cache | (Old Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/559440e9-9360-4654-b77c-5430f5e096d9/14-volumetric-lightmaps-movable-object-ilc.png)

![Volumetric Lightmap | (New Method)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98fb8206-d657-4686-8e1e-d0994d40cfbc/15-volumetric-lightmaps-movable-object-vlm.png)

For movable objects that are embedded in any static geometry, it now provides a better match for the static object lighting compared to the Indirect Lighting Cache.

### Precomputed Lighting on Volumetric Fog

Volumetric Lightmaps support static lighting application for Volumetric fog by having each fog voxel interpolate precomputed lighting to its position in space.

![Spot Light with | No Indirect Light Bounce](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16473961-d58b-4777-84ea-583b2a0fcb04/16-volumetric-lightmaps-sl-no-bounce.png)

![Spot Light with | Indirect Light Bounce](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18e147c2-07f1-472d-a207-c22ef077bb97/17-volumetric-lightmaps-sl-indirect-bounce.png)

Stationary Lights have their indirect lighting stored in lightmaps, which now affects fog.

![Sky Light with Emissive Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48352bfc-9732-4e68-b963-f10f0e76a0e7/18-volumetric-lightmaps-skylight-emissive.png)

![Sky Light Volumetric Lightmap](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67b4e27a-e438-4f11-a365-12b98a4f7ed8/19-volumetric-lightmaps-skylight-vlm.png)

Skylights are shadowed properly, preventing indoor areas from becoming over-fogged.

![Indirect Lighting Cache: | Static and Emissive for Static Lighting | (Old Method) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92341b0f-a51e-4155-942e-c566cb4dbf09/20-volumetric-lightmaps-static-ilc.png)

![Volumetric Lightmap: | Static and Emissive for Static Lighting | (New Method) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd3181ca-76a2-48d0-8ede-78c83de7333b/21-volumetric-lightmaps-static-vlm.png)

Static and Emissive for Static lights affect fog without costing anything since they're all merged into the Volumetric Lightmap.

## Settings

The Volumetric Lightmap settings can be accessed from the **World Settings** located under the **Lightmass Settings**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa86aec3-a20e-457c-8dff-3e35161b0502/22-volumetric-lightmaps-vlm-settings.png)

| Setting | Description |
| --- | --- |
| **Volumetric Lighting Method** | 
Technique used for providing precomputed lighting at all positions inside the Lightmass Importance Volume.

-   **Volumetric Lightmap**: Lighting samples are computed in an advanced grid which covers the entire Lightmass Importance Volume. Higher-density grids are used near geometry. The Volumetric Lightmap is interpolated efficiently on the GPU per-pixel allowing accurate indirect lighting for dynamic objects and volumetric fog. Positions outside of the Importance Volume reuse the border texels of the Volumetric Lightmap (clamp addressing). On mobile, interpolation is done on the CPU at the center of each object's bounds.
-   **Sparse Volume Lighting Samples**: Volume lighting samples are placed on top of static surfaces at medium-density and everywhere else in the Lightmass Importance Volume at low-density. Positions outside of the Importance Volume will have no indirect lighting. This method requires CPU interpolation, so the Indirect Lighting Cache is used to interpolate results for each dynamic object, adding Rendering Thread overhead. Volumetric Fog cannot be affected by precomputed lighting with this method.



 |
| **Volumetric Lightmap Detail Cell Size** | Size of a Volumetric Lightmap voxel at the highest density (used around geometry), in world space units. This setting has a large impact on build times and memory and should be used with caution. |
| **Volumetric Lightmap Maximum Brick Memory Mb** | The maximum amount of memory to spend on Volumetric Lightmap Brick data. High-density bricks will be discarded until this limit is met with bricks furthest from geometry discarded first. Trimming memory too heavily will result in inconsistent resolution and it would be better to increase **Volumetric Lightmap Detail Cell Size** instead. |
| **Volumetric Lightmap Spherical Harmonic Smoothing** | Controls how much smoothing should be done to Volumetric Lightmap samples during Spherical Harmonic de-ringing. Whenever highly directional lighting is stored in a Spherical Harmonic, a ringing artifact occurs which manifests as unexpected black areas on the opposite side. Smoothing can reduce this artifact. Smoothing is only applied when the ringing artifact is present. **0** = no smoothing, **1** = strong smooth (little directionality in lighting). |
| **Volume Light Sample Placement Scale** | Scales the distances at which volume lighting samples are placed. Volume lighting samples are computed by Lightmass and are used for GI on movable components. Using larger scales results in less sample memory usage and reduces Indirect Lighting Cache update times, but less accurate transitions between lighting areas. |

## Performance

The following considerations should be taken into account when considering performance and memory usage with Volumetric Lightmaps.

-   Volumetric Lightmaps on a third person character cost .02ms of GPU time on the PlayStation 4. All Indirect Lighting Cache Rendering Thread cost is removed.
-   In Epic's Paragon map Monolith, memory usage increased from 5Mb with the Indirect Lighting Cache to 30Mb with Volumetric Lightmaps at default **Detail Cell Size** settings. Memory usage can be seen under the **Stat MapBuildData** command in the Editor with **Volumetric Lightmap Memory**
    
    Click image for full size.
    

### Volumetric Lightmap versus Indirect Lighting Cache

Below are the details of the comparisons that can be made between the Indirect Lighting Cache and Volumetric Lightmaps:

| **Precomputed Light Volumes/Indirect Lighting Cache** | **Volumetric Lightmaps** |
| --- | --- |
| Costly interpolation on the CPU | Efficient interpolation on the GPU |
| Per-object interpolation, even on instanced components | Per-pixel interpolation |
| Cannot affect Volumetric Fog | Works with Volumetric Fog |
| Placed with high-density only on top of static surfaces resulting in leaking from low-density samples | Placed with high-density all all around static surfaces |
| Black samples outside of the Lightmass Importance Volume | Border voxels are stretched to cover areas outside of the Lightmass Importance Volume |
| Supports Level Streaming | Level Streaming is supported but requires that all levels (including those streamed in) must be built at the same time. For more details, see the "Additional Notes" section below. |

Level Streaming is supported but requires that all levels (including those streamed in) must be built at the same time. For more details, see the "Additional Notes" section below.

## Additional Notes

-   If you reduce the **Volumetric Lightmap Detail Cell Size** in a large level to get more accuracy, you need to raise the **Volumetric Lightmap Maximum Brick Memory Mb** as well. Otherwise, the detail cells will get culled causing dynamic object indirect lighting to be less accurate.
-   Level Streaming requires that all levels (the Persistent and any sub-levels) all be built at the same time, otherwise streamed in levels will not be registered correctly. Streaming levels are primarily a memory optimization where the most detailed bricks volumes are merged into a bigger volume that is a cube (equal dimensional sides) instead of a box (different dimensional sides). The most detailed bricks are streamed with the closest sub-level and higher level bricks are always persistent. In levels that contain actual geometry, the majority of data goes into the most detailed level bricks. There should be little concern given to parts of the volume that appear to be empty (or "wasted") space if the level is filled with geometry. The current system uses a single volume texture, meaning that we can't do much about empty space since we don't support multiple volume textures that has overlap and blending.
-   Use **Volumetric Lightmap Density Volumes** to provide local control over the density of samples within areas of the scene. These volumes only supports convex shapes. Add one to your scene from the **Place Actors** panel in the Level Editor.

## Troubleshooting

-   The **Detail Cell Size** has been lowered for more samples, but the sample density is lower than requested near static geometry.
    -   Detail bricks can be culled if the **Maximum Brick Memory** is too low, or if all lighting in the area is nearly equal.
-   There is light leaking through a wall on characters but no on the Static Meshes nearby.
    -   The only current solutions to leaking are to decrease **Detail Cell Size** (allowing more memory) or increase the thickness of the wall.