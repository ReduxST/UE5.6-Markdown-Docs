# Static Light Mobility

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/static-light-mobility-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/static-light-mobility-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:14

---

Lights that have their Mobility set to **Static** are lights that cannot be changed or moved in any way during runtime. They are precomputed using [Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) when a lighting built is performed. Static Lights store their data in textures called Lightmaps that are applied to geometry in the Level. Once the lighting build is complete, these lights have no further impact on performance.

Static Meshes with their Mobility set to Movable and Skeletal Meshes do not integrate (or blend) fully with Static Lighting. However, when a light build takes place, lighting data is stored in [Volumetric Lightmaps](/documentation/en-us/unreal-engine/volumetric-lightmaps-in-unreal-engine) or the [Indirect Lighting Cache](/documentation/en-us/unreal-engine/indirect-lighting-cache-in-unreal-engine) to assist in lighting and grounding these movable objects within a statically lit area.

Of the three light mobilities, Static Lights tend to have medium quality, lowest mutability, and the lowest performance cost.

## Lightmap Resolution

Static Lights generate their lighting data with [Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) and store it in lightmaps that are stored per-Level and applied to the geometry within that Level after a lighting build takes place.

Because lightmaps store their lighting data in textures applied to geometry, it's important to set a good lightmap resolution for individual actors to capture good shadow detail on its surfaces. You can use one of the following ways to set the lightmap resolution for an object in the scene:

-   Open the Static Mesh Asset in the **Static Mesh Editor** and use its **Details** panel to set the default **Light Map Resolution** used by this asset anywhere it's used.

-   In the Level Editor, select a **Static Mesh Actor** and use its **Details** panel to enable **Overridden Light Map Res** and enter a new lightmap resolution to use for this individual Actor. This option is most useful when you have scaled the object and need to make its lightmap textures consistent with the other objects around it.

The examples below compare a low lightmap resolution with a higher one. Low lightmap resolutions do not accurately capture detail compared to higher resolutions. It is worth noting that higher resolutions require additional disk space for the texture data and take longer to process when building lighting for the scene.

|   |   |   |
| --- | --- | --- |
| ![lightmap resolution 64](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10a19a66-0b48-4e39-8777-e877d7646e41/lightmap-resolution-64.png) | ![lightmap resolution 128](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2fdd242-7865-4940-a52b-ab8e648db83a/lightmap-resolution-128.png) | ![lightmap resolution 512](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0275b256-0e72-4268-a8c4-ded9a916218b/lightmap-resolution-512.png) |
| Lightmap Resolution: 64 | Lightmap Resolution: 128 | Lightmap Resolution: 512 |

Because lightmap resolution can be set per-Asset, or overridden per-Actor within a Level, it's important that shadows appear consistent between the assets that receive static shadows and that they integrate with the surrounding shadows appropriately. The Level Editor view mode for **Lightmap Density** (found under the **View Modes > Optimization Viewmodes** dropdown) shows a tiled pattern on any Static Mesh Asset with its Mobility set to Static that will generate a lightmap texture. The tiles represent the current texel density based on the lightmap resolution of the Static Mesh Asset with other Assets in the scene.

In this example, the texel density of the floor does not match much of the surrounding lightmap resolutions of the objects in the scene. Note where the block in the center meets the floor and the inconsistency of the shadow baked in across the floor compared to the block.

|   |   |
| --- | --- |
| ![lighting only view mode with built shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e4ceca9-19ce-4297-9c41-431b239d952b/lighting-only-viewmode_1.png) | ![lightmap-density-view-mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac8584fc-0820-4401-b4f8-99487f45ee36/lightmap-density-view-mode_1.png) |
| Lighting Only View Mode with built shadows | Lightmap Density View Mode — Low Floor Asset Lightmap Texel Density |

Increasing the lightmap resolution of the floor more closely aligns the texel density to the block in the center and other objects in the scene. Note how the shadows are more consistent between the floor and the block now because the texel densities are more closely aligned.

|   |   |
| --- | --- |
| ![lighting only view mode with built shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39997d5b-945e-4bbb-b41c-aff0e8a944d2/lighting-only-viewmode_2.png) | ![lightmap-density-view-mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bccdd8e7-9526-43a6-bfdc-e77dd95e972d/lightmap-density-view-mode_2.png) |
| Lighting Only View Mode with built shadows | Lightmap Density View Mode — Higher Floor Asset Lightmap Texel Density |

## Lightmass Settings

Static Lights have their own settings that located on the light and within the **World Settings** that affect their interactions within the Level.

### Per-Light Lightmass Settings

On selected **Lights** within the scene that have their Mobility set to **Static**, the following settings under the the **Lightmass** category affects the lighting build.

| Property | Description |
| --- | --- |
| **Light Source Angle** | On a Directional Light, this controls the angle that the emissive surface extends relative to a receiver and affects the penumbra sizes of shadows cast from a Directional Light. |
| **Indirect Lighting Saturation** | Controls the amount of desaturation applied to the baked bounce lighting. |
| **Shadow Exponent** | Controls the falloff of the shadow penumbras. |

### World Settings Lightmass Settings

For each **Level**, use the **World Settings > Lightmass Settings** to configure how static lighting is computed in the world. The setting here will affect any of the Static Lights in the currently loaded Level(s).

| Property | Description |
| --- | --- |
| **Static Lighting Level Scale** | Scale of the level relative to real world scale (1 Unreal Unit is equal to 1 centimeter). All scale-dependent Lightmass setting defaults have been made to work well with real world scale. Any Levels with a different scale should use this scale to compensate, such as large worlds where it can significantly reduce build times when set to a higher value, like 2 or 4. Lower values will drastically increase build times. |
| **Num Indirect Lighting Bounces** | The number of light bounces to simulate for point, spot, and directional lights, starting from the light source. 0 produces direct lighting only. The first bounce takes the most time to calculate and contributes the most to visual quality, followed by the second bounce of light. Successive bounces don't really affect light build times, but have much lower visual impact, unless the material diffuse colors are close to 1. |
| **Num Sky Light Bounces** | The number of skylight and emissive bounces of light to simulate. Lightmass uses a non-distributable radiosity method for skylight bounces whose cost is proportional to the number of bounces. |
| **Indirect Lighting Quality** | 
This setting can be used to increase the global illumination solver sample counts in order to get higher quality for Levels that need it. It can be useful to reduce **Indirect Lighting Smoothness** somewhat (approximately 0.75) when increasing quality to get defined indirect shadows.

This setting does not affect compression artifacts, UV seams or other texture based artifacts that can happen during a light build.



 |
| **Indirect Lighting Smoothness** | This setting is useful in some lighting conditions when Lightmass cannot resolve accurate indirect lighting. 1 is the default smoothness that is setup to work well for a variety of lighting situations. Higher values like 3 will smooth out the indirect lighting more but at the cost of indirect shadows losing detail. |
| **Environment Color** | Represents a constant color light surrounding the upper hemisphere of the Level, like a sky. The light source currently does not get bounced as indirect lighting and causes reflection capture brightness to be incorrect. Instead, it's recommended to use a Static Sky Light instead. |
| **Diffuse Boost** | Scales the diffuse contribution of all materials in the scene. |
| **Volume Lighting Method** | 

Technique to use for providing precomputed lighting at all positions inside the Lightmass Importance Volume.

-   **Volumetric Lightmap:** Lighting samples are computed in an adaptive grid which covers the entire Lightmass Importance Volume. Higher density grids are used near geometry. The Volumetric Lightmap is interpolated efficiently on the GPU per-pixel, allowing accurate indirect lighting for dynamic objects and volumetric fog. On mobile, interpolation is done on the VPU at the center of each object's bounds.
-   **Sparse Volume Lighting Samples:** Lighting samples are placed on top of Static surfaces at medium density, and everywhere else in the Lightmass Importance Volume at low density. Positions outside of the Importance Volume will have no indirect lighting. This method requires CPU interpolation so the Indirect Lighting Cache is used to interpolate results for each dynamic object, adding Rendering Thread overhead. Volumetric Fog cannot be affected by precomputed lighting with this method.



 |
| **Use Ambient Occlusion** | When enabled, Ambient Occlusion will be baked into the lightmaps. |
| **Generate Ambient Occlusion Material Mask** | 

Whether to generate textures toring the ambient occlusion computed by Lightmass. These can be accessed through the PrecomputedAOMask material node, which is useful for blending between different material layers on environment assets.

Be sure to set Direct Illumination Occlusion Fraction and Indirect Illumination Occlusion Fraction to 0 if you only want the PrecomputedAOMask.



 |
| **Visualize Material Diffuse** | When true, overrides the normal direct and indirect lighting with just the exported diffuse term. |
| **Visualize Ambient Occlusion** | when true, override normal direct and indirect lighting with just the ambient occlusion term. |
| **Compress Lightmaps** | Whether to compress lightmap textures. Disabling lightmap texture compression will reduce artifacts but increase memory and disk size used by a significant amount. |
| **Volumetric Lightmap Detail Cell Size** | The size of a Volumetric Lightmap voxel at the highest density (used around geometry), in world space units. This has a large impact on build times and memory and should be used with caution. Halving the Detail Cell Size can increase memory by up to a factor of 8x. |
| **Volumetric Lightmap Maximum Brick Memory Mb** | Maximum amount of memory to spend on Volumetric Lightmap Brick data. High density bricks will be discarded until this limit is met, with bricks farthest from geometry being discarded first. |
| **Volumetric Lightmap Lightmap Spherical Harmonic Smoothing** | Controls how much smoothing should be done to Volumetric Lightmap samples during Spherical Harmonic de-ringing.Whenever highly directional lighting is stored in a Spherical Harmonic, a ringing artifact occurs which manifests as unexpected black areas on the opposite side. Smoothing can reduce this artifact. Smoothing is only applied when the ringing artifact is present. 0 is equal to no smoothing, 1 to strong smoothing (with little directionality in lighting). |
| **Volume Light Sample Placement Scale** | Scales the distances at which volume lighting samples are placed. Volume lighting samples are computed by Lightmass and are used for global illumination on movable components. Using large scales results in less sample memory usage and reduces Indirect Lighting Cache update times, but less accurate transitions between lighting areas. |
| **Direct Illumination Occlusion Fraction** | How much of the ambient occlusion to apply to direct lighting. |
| **Indirect Illumination Occlusion Fraction** | How much of the ambient occlusion to apply to indirect lighting. |
| **Occlusion Exponent** | Higher exponents increase contrast. |
| **Fully Occluded Samples Fraction** | Fraction of samples taken that must be occluded in order to reach full occlusion. |
| **Max Occlusion Distance** | Maximum distance for an object to cause occlusion on another object. |
| Advanced Properties |   |
| **Lightmaps** | The computed lightmap textures save for the Level. |
| **Force No Precomputed Lighting** | 

Whether to force lightmaps and other precomputed lighting to not be created, even when the engine thinks they are needed. This is useful for improving iteration in Levels with fully dynamic lighting and shadowing.

Any lighting and shadowing interactions that are usually precomputed are lost if this setting is enabled.



 |
| **Packed Light and Shadow Map Texture Size** | The maximum size of textures for packed light and shadow maps. |