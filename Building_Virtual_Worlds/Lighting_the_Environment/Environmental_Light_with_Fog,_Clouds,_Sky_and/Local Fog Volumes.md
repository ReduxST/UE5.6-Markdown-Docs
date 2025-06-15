# Local Fog Volumes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/local-fog-volumes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/local-fog-volumes-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:09

---

Applying fog to your world is generally an all-or nothing approach using [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) or [Exponential Height Fog](/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine) unless you’re using [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine), which has the ability to create local variations using meshes and materials.

**Local Fog Volumes** are placeable actors you can use to quickly create local variations of fog in a simplistic and efficient manner. Local fog volumes, unlike volumetric fog, work across all platforms and scalability levels making them ideal to use for low-end and high-end platforms by providing consistent visuals with other fog and lighting systems.

![A scene with placed local fog volumes with | atmosphere and height fog.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/372b1d57-6a44-44d9-a1be-cdff9c18497f/lfv-withfog.png)

![A scene using only atmosphere and height fog.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e688c61-0b82-4d2e-9a43-74b468bd96f5/lfv-withoutfog.png)

The primary use case for local fog volumes is to create variations of fog without requiring separate, more costly systems — like using Exponential Height Fog with Volumetric Fog enabled. With that in mind, the order of composition when using local fog volumes with other volumetric elements is:

1.  Sky Atmosphere Aerial Perspective
2.  Exponential Height Fog
3.  Other Local Fog Volumes
4.  Volumetric Fog (when enabled)

## Using Local Fog Volumes

You can place local fog volumes anywhere in your game world. It is a sphere of participating media representing a mixture of exponential height fog combined with a radially faded out fog. Each local fog volume can be independently translated, rotated, and uniformly scaled to fit your scene.

You can add a local fog volume to your scene using the **Create** menu from the **Visual Effects** category, or you can use the **Place Actors** panel.

![Local fog volume transform demonstration.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a99b3f68-0a9a-426f-bb83-4cc5c02533d4/lfv-transform-demo.gif)

A local fog volume is added to the scene and scaled, translated, and rotated. Non-uniform scaling is not supported.

### Using Local Fog Volumes with Volumetric Fog

You can use local fog volumes with [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine), which provides volumetric shadowing and lighting within these volumes but at a higher performance cost.

To use volumetric fog with local fog volumes, check the box for the **Volumetric Fog** property in the **Exponential Height Fog** details panel. Below is an example scene with and without volumetric fog enabled.

|   |   |
| --- | --- |
| 
 | 

 |
| Local Fog Volume only | Local Fog Volume with Volumetric Fog enabled |

## Local Fog Volume Properties and Project Settings

Local Fog Volumes contain the following properties:

![Local Fog Volume Details Panel Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66e334d8-1c71-45a3-b038-0d8cd6c5fb96/lfv-properties.png)

| Property | Description |
| --- | --- |
| Radial Fog Distribution |   |
| **Radial Fog Density** | The density of the radial fog represents its coefficient at the center of the sphere. The final look of the volume is determined by combining the “Coverage = 1 - Transmittance” of both radial and height fog in order to achieve both soft edges and height fog. |
| Height Fog Distribution |   |
| **Height Fog Density** | The density of radial fog represents its extinction coefficient at height 0 in the unit sphere. The final look of the volume is determined by combining the “Coverage = 1 - Transmittance” of both radial and height fog in order to achieve both soft edges and height fog. |
| **Height Fog Falloff** | Controls how the density decreases as height increases. Smaller values make the visible transition larger. 1.0 is the lowest value before visual artifacts are visible at the horizon. |
| **Height Fog Offset** | Height offset relative to the actor’s Z position. |
| Shading |   |
| **Scattering Distribution** | Controls the phase “G” parameter, describing the scattering within this fog volume. |
| **Fog Albedo** | Sets the albedo color of this fog volume. The albedo is the base color before any lighting has been applied. |
| **Fog Emissive** | Controls the emissive color of this fog volume. |
| Sorting |   |
| **Fog Sort Priority** | 
The priority can be used as a way to override the sorting by distance. A lower value means the volume is considered further away. For example, it will draw behind volumes with higher priorities.

This setting is not used when Volumetric Fog is enabled in the Exponential Height Fog settings.



 |

The Project Settings contains the following properties for local fog volumes found in the **Engine > Rendering** section:

![Local Fog Volume project settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f09e8a3d-326d-4912-a1b9-352ac96a62fb/lfv-projectsettings.png)

| Project Setting | Description |
| --- | --- |
| Translucency |   |
| **Local Fog Volume Apply on Translucent** | Enables sampling of local fog volumes on translucent elements. |
| Optimizations |   |
| **Support Local Fog Volumes** | Local fog volumes components can be applied on translucent and opaque surfaces in Forward shading, so resources need to be bound to apply aerial perspective on transparent surfaces (and all surfaces on mobile via per vertex evaluations). Requires `r.SupportLocalFogVolumes` to be true. |

### Fog Shading

You can use the **Shading** properties to define the artistic look of fog with the albedo color, emissive color, and scattering distribution.

The **Fog Albedo** defines the color of the fog when interacting with light sources, such as the sun and sky. You can use the color picker to select a color for the fog.

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Albedo Color: White (Default) | Albedo Color: Green | Albedo Color: Brown |

The **Fog Emissive** defines the color of the light emitted by the fog. The emitted light follows the same density as the local fog volume. You can use the color picker to select an emissive color for the fog.

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Emissive Color: None (Default) | Emissive Color: Green | Emissive Color: Red |

The **Scattering Distribution** controls how much the incoming light scatters in various directions. Zero scatters light equally in all directions while something closer to a value of 1 scatters predominantly in the direction of the light.

     ![Scattering Distribution 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e74d9cc7-0d32-4f8b-9e1c-0bb9bf7f778d/lfv-scatteringdist-1.png) ![Scattering Distribution 0.25](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62b6efe3-ad7d-4b53-97cc-b47517b73adb/lfv-scatteringdist-2.png) ![Scattering Distribution 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cab50274-4747-4e98-be59-43603291b7f7/lfv-scatteringdist-3.png) ![Scattering Distribution 0.75](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36932406-1980-45fd-b9aa-81c4a2f3d42a/lfv-scatteringdist-4.png) ![Scattering Distribution 0.9](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ec4a0f2-c365-4903-b219-50942f199596/lfv-scatteringdist-5.png) ![Scattering Distribution 0.99](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7554a55-c9f0-48ff-b431-7206d541a026/lfv-scatteringdist-6.png)

**Drag the slider to see Local Fog Scattering Distribution changes from low to high starting with 0, 0.25 , 0.5, 0.75, 0.98, and 0.99**

To have volumetric fog light shafts, volumetric fog must be enabled and the scattering distribution needs to be closer to zero. The default scattering distribution of 0.2 is a good starting point.

### Fog Distribution

The distribution of fog controls how much light passes through the fog volume with properties for density, falloff, and height offset. These properties are similar to those found in the Exponential Height Fog component.

The **Radial Fog Density** and **Height Fog Density** control the look of the volume to achieve both soft edges and height fog.

![Radial Fog and Height Fog Densities](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67aa59a2-1d39-4a2b-84ec-63593cb832c0/lfv-density-examples.png)

Examples of local fog volumes. (Left to Right) Fog with radial density, fog with height density, and fog with a combination of radial and height densities.

The phase function of a local fog volume controls the uniformity of the light within the volume. Shadows and light functions are ignored because the lighting is evaluated using fast analytical integrals.

The **Height Fog Falloff** controls how the density of the fog decreases as the height increases. Smaller values make larger visible transitions, whereas larger values have smaller transitions.

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Height Fog Falloff: 500 | Height Fog Falloff: 1000 (Default) | Height Fog Falloff: 2500 |

The **Height Fog Offset** moves the center of the height fog relative to the actor’s Z (up) position within the local fog volume. Using a lower offset moves the fog down within the radial volume, whereas higher values move it vertically.

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Height Fog Offset: -0.12 | Height Fog Offset: 0 (Default) | Height Fog Offset: 0.12 |

### Fog Sort Priority

Local fog volumes are composited on screen according to the distance of their center to the camera view. This allows you to control their sort order by applying a priority for them when they happen to overlap. When volumetric fog is enabled in the exponential height fog settings, local fog volumes are voxelized into volumetric representation — local fog volumes are not sorted, instead they are voxelized as overlapping participating media. Lighting can also cause fog when shadow casting is enabled for volumetric fog.

Below are two examples showing overlapping local fog volumes without and with volumetric fog enabled.

|   |   |
| --- | --- |
| 
 | 

 |
| Two local Fog Volumes of different color composited. | Two Local Fog Volumes with different color composited with Volumetric Fog enabled. |

Because volumetric fog is voxelized as participating media, and not sorted, it can result in visuals that look different. For example if the scattering distribution (Phase function) is different from that of the volumetric fog’s, the result could look different.

When volumetric fog is enabled, fog is voxelized to sort appropriately. However, when local fog volumes are used without volumetric fog, you can use the **Fog Sort Priority** setting to override sorting by distance. Lower values means the volume is considered farther away — the volume will draw behind others. Larger values will consider the volume closer to the camera and thus should render on top of others.

Because you can have multiple overlapping local fog volumes, sorting is useful when you want larger ambient local fog to always be behind smaller, more intense volumes. In these situations, local fog will always mix well when viewed close up, even without volumetric fog enabled, like in the example scene below.

|   |   |
| --- | --- |
| 
 | 

 |
| Two overlapping local fog volumes viewed at ground level. | Two overlapping local fog volumes viewed from above. |

## Performance and Debugging

The following are some suggestions for improving performance and debugging content related to local fog volumes:

-   Local fog volumes are culled using screen tiles — where the screen is divided into small squares called tiles — making their cost similar to dynamic lights added to the scene since their cost is related to the extent of the space on screen they use.
    -   You can visualize the extent of the cost in screen space using the console command `r.LocalFogVolume.TileDebug`.
        -   **1** shows the local fog volume count as a color per tile.
        -   **2** shows the local fog volume count as a color per tile and the effect of the pixel discard/clipping.
-   On lower-end hardware, a good practice to have is to limit multiple volumes from overlapping one another. This reduces the number of volumes to process per pixel when the camera is completely inside of them.

### Local Fog Volume Tile Debug

You can visualize local fog volumes culling per screen tile using the console command `r.LocalFogVolume.TileDebug`.

Use one of the following values:

-   **1** shows the local fog volume count as a color per screen tile.
-   **2** shows the local fog volume count as a color per screen tile and the effect of the pixel discard/clipping.

The examples in the scene below demonstrate multiple local fog volumes, some close together and some overlapping.

![Local fog volume examples with overlapping for debugging purposes.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63c14e86-b9e8-4e45-915d-34fc43d1d37f/lfv-tiledebug-1.png)

Below shows what the tile debug views look like when enabled using the example scene above.

|   |   |
| --- | --- |
| 
 | 

 |
| r.LocalFogVolume.TileDebug 1 | r.LocalFogVolume.TileDebug 2 |

The tile debug views do not work when volumetric fog is enabled.

## Useful Console Variables

| Console Variable | Description | Default Value |
| --- | --- | --- |
| `r.LocalFogVolume.ApplyOnTranslucent` | Project settings enabling the sampling of local fog volumes on translucent elements. Set this to 1 in order to have local fog volumes applied on translucent meshes. | 0 |
| `r.LocalFogVolume.RenderIntoVolumetricFog` | Sets whether to voxelize local fog volumes into the volumetric fog rendering system. Otherwise, local fog volumes will remain isolated. This is enabled by default. | 1 |
| `r.LocalFogVolume.TilePixelSize` | The pixel size of tiles on screen at which point local fog volumes are culled. | 128 |
| `r.LocalFogVolume.TileMaxInstanceCount` | Maximum number of local fog volumes to account for per view (and per tile for consistency). | 32 |
| `r.LocalFogVolume.TileDebug` | Debug the tiled rendering data complexity. 0 is disabled. 1 shows per-tile LFV count as color. 2 shows the same as one but also shows the effect of pixel discard / clipping. | 0 |
| `r.LocalFogVolume.GlobalStartDistance` | Sets the start distance (in centimeters) from the camera in which local fog volumes start to appear. | 2000 |
| `r.LocalFogVolume.HalfResolution` | This renders local fog volumes at half resolution with upsampling to full resolution later on. This only works for mobile rendering paths, when enabled. | 0 |
| `r.LocalFogVolume.MaxDensityIntoVolumetricFog` | LocalFogVolume Height fog mode can become exponentially dense in the bottom part. Volumetric fog temporal reprojection then can leak due to high density. Clamping density is a way to get that visual artifact under control. | 0.01 |