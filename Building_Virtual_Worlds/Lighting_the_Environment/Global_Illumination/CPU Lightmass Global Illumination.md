# CPU Lightmass Global Illumination

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cpu-lightmass-global-illumination-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cpu-lightmass-global-illumination-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:30

---

![Banner image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a95a8b3-08fe-4f75-966b-4ded5292c90d/lightmass-global-illum-banner.png)

**Lightmass** creates lightmaps with complex light interactions like area shadowing and diffuse interreflection. It is used to precompute portions of the lighting contribution of lights with stationary and static mobility.

Communication between the Editor and Lightmass is handled by the **Swarm Agent**, which manages the lighting build locally and can also distribute the lighting build to remote machines. The Swarm Agent, which opens minimized by default, also tracks lighting build progress and keeps you up to date with which machines are working for you, what they are working on, and how many threads each one is using.

A sample image of the Swarm Agent is pictured below (the bar near the bottom shows how much of the build is complete).

![Example of the Swarm Agent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5dcb95e-0fdd-4a6a-847f-be62e7c91324/01-lightmass-global-illum-swarm-agent.png)

## Features for Static and Stationary lights

### Diffuse Interreflection

**Diffuse Interreflection** is by far the most visually important global illumination lighting effect. Light bounces by default with Lightmass, and the BaseColor term of your material controls how much light (and what color) bounces in all directions. This effect is sometimes called Color Bleeding. Diffuse Interreflection is incoming light reflecting equally in all directions, which means that it is not affected by the viewing direction or position.

Here is a scene built by Lightmass with a single Directional Light and only direct lighting shown. The areas that are not directly visible to the light are black. This is the result without global illumination.

![The scene with the single Directional Light and only direct lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e4e2b53-955f-46e4-b88b-4d3afebdadcf/02-lightmass-global-illum-direct-light-only.png)

This is what the first diffuse global illumination bounce looks like. Notice the shadow behind the chair on the left, this is called an Indirect Shadow because it is the shadow of the indirect light. The brightness and color of the diffuse bounce depends on the incoming light and the diffuse term of the material that the light interacts with. Each bounce is darker than the previous, since some of the light gets absorbed by surfaces instead of being reflected. The pillar bases get more indirect light than other surfaces because they are closer to the areas in direct light.

![The scene with the first diffuse illumination bounce](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80839c3e-013b-4e40-98a5-4e6bf1623b2b/03-lightmass-global-illum-bounce.png)

This is the second diffuse bounce. The light has become much more attenuated and evenly distributed.

![The scene with the second diffuse illumination bounce](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b4147a0-207c-4080-9900-1b29c0201722/04-lightmass-global-illum-second-bounce.png)

And here is the scene with four diffuse bounces combined. Simulating global illumination creates much more detailed and realistic lighting than manually placing fill lights. Indirect shadows in particular are not possible with fill lights.

![The scene with four diffuse bounces combined](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b48c85f4-6011-4fb5-b3b8-6a83be25f469/05-lightmass-global-illum-four-bounces.png)

Bounced lighting picks up the diffuse color of the underlying material, as you can see below. This is where the term Color Bleeding comes from. Color Bleeding is most noticeable with highly saturated colors. You can exaggerate the effect by raising **Diffuse Boost** on the Primitive, Material, or Level.

|   |   |
| --- | --- |
| ![Diffuse bounce T](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e036aad-b23f-4a2d-a699-4cf00e0bbfd1/06-lightmass-global-illum-diffuse-bounce-t.png) | ![Diffuse bounce L](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f02c0a07-0364-472f-aad3-d33d3afd1bfe/07-lightmass-global-illum-diffuse-bounce-l.png) |

### Character lighting

Lightmass places samples in a uniform 3d grid inside the [**Lightmass Importance Volume**](/documentation/en-us/unreal-engine/cpu-lightmass-global-illumination-in-unreal-engine#lightmassimportancevolume) at a low resolution, and also on top of upward facing surfaces that characters are likely to walk on, at a higher resolution. Each lighting sample captures indirect lighting from all directions, but not direct lighting.

The first image is a debug visualization of lighting samples placed above the floor, the second image is the same scene in Lit mode. Notice how the samples above the red tapestry picked up the red bounced light. The samples are visualized as a single color, but they really capture lighting from all directions.

|   |   |
| --- | --- |
| ![Debug visualization of lighting samples placed above the floor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dabfbaba-5bae-4508-88df-c1b4549b8e31/08-lightmass-global-illum-char-lighting.png) | ![Debug visualization of lighting samples placed above the floor in Lit mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/077be0be-31a1-4e0a-b17f-adbe65e75896/09-lightmass-global-illum-char-lighting-lit.png) |

The Indirect Lighting Cache then interpolates the indirect lighting for a movable object using these lighting samples. The indirect lighting affects the color of the light environment shadow, but not the direction. Use **Show > Visualize > Volume Lighting Samples** to preview these in your Viewport.

![Enabling Volume Lightning Samples in the Viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9413919e-0a0d-49bb-98ca-d7cd4f3fde3a/10-lightmass-global-illum-enable-volume-samples.png)

For more information, see the [Indirect Lighting Cache](/documentation/en-us/unreal-engine/indirect-lighting-cache-in-unreal-engine) documentation.

#### Limitations

*The default settings for volume sample placement will result in a large number of samples in a large map. This will cause Indirect Lighting Cache interpolation times to be very large. Use Static Lighting Level Scale to reduce the sample count in large maps.* Movable objects outside the Lightmass Importance Volume will have black indirect lighting.

### Ambient Occlusion

Lightmass calculates detailed indirect shadows automatically, but it can be useful to exaggerate indirect shadows for artistic purposes or to enhance the perception of proximity in a scene.

**Ambient occlusion** is the indirect shadowing you would get from a uniformly bright upper hemisphere, like an overcast sky. Lightmass supports calculating ambient occlusion, applying it to direct and indirect illumination, and then baking it into lightmaps. Ambient occlusion is enabled by default, and can be disabled by unchecking the checkbox **Use Ambient Occlusion** in the Lightmass Settings of Lightmass under the World Settings.

In the first image is a scene with indirect lighting but no ambient occlusion. In the second image is the same scene with ambient occlusion applied to both the direct and indirect lighting, note the darkening where objects come together.

|   |   |
| --- | --- |
| ![Scene with indirect lighting and No Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd683b2e-2b65-491c-926b-aff84cddd9b1/11-lightmass-global-illum-no-ambient.png) | ![Scene with indirect lighting and Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e58c4a4-f91d-4fd0-8243-c6a5dcd59630/12-lightmass-global-illum-with-ambient.png) |
| No Ambient Occlusion | Ambient Occlusion |

#### Ambient Occlusion Settings

| Property | Description |
| --- | --- |
| **Visualize Ambient Occlusion** | Overrides lightmaps with just the occlusion factor when lighting is built. This is useful for seeing exactly what the occlusion factor is, and comparing the effects of different settings. |
| **Max Occlusion Distance** | Maximum distance for an object to cause occlusion on another object. |
| **Fully Occluded Samples Fraction** | Fraction of samples taken that must be occluded in order to reach full occlusion. Note that there is also a per-primitive FullyOccludedSamplesFraction, which allows controlling how much occlusion an object causes on other objects. |
| **Occlusion Exponent** | Higher exponents increase contrast. |

|   |   |   |   |
| --- | --- | --- | --- |
| ![Default AO settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6d0e96f-5d3f-459f-a8e5-2fe7313a85b6/13-lightmass-global-illum-default.png) | ![MaxOcclusionDistance of 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31e48daf-399f-4a1b-a0cd-05673871896c/14-lightmass-global-illum-max-occ-5.png) | ![Fully Occluded Samples Fraction of 0.8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f556e0e5-fbf6-48f3-8ae0-c7a60eb39b8d/15-lightmass-global-illum-fully-occ.png) | ![Occlusion Exponent of 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95f1746f-7d83-403f-a06b-f5629f458e75/16-lightmass-global-illum-occ-exp-2.png) |
| Default AO settings (MaxOcclusionDistance of 200, FullyOccludedSamplesFraction of 1.0, OcclusionExponent of 1.0). | MaxOcclusionDistance of 5. Low frequency occlusion is removed, only occlusion in corners is left. | FullyOccludedSamplesFraction of 0.8. Occlusion is shifted darker across all ranges, any areas that were at 80% occluded or above saturate to black. | OcclusionExponent of 2. The shadowing caused by occlusion darkens from midrange to saturated dark much more quickly, occlusion is pushed into corners. |

Ambient occlusion is nearly free as far as lighting build time goes when Num Indirect Lighting Bounces is greater than 0.

#### Limitations

*Ambient occlusion requires a fairly high lightmap resolution to look good, since it changes quickly in corners.* Preview quality builds do not do a very good job at previewing ambient occlusion, since AO requires pretty dense lighting samples (just like indirect shadows).

### Masked shadows

Lightmass takes the opacity mask of BLEND\_Masked Materials into account when calculating shadows. The part of the material that gets clipped in the editor viewports also does not cause any shadowing, which allows much more detailed shadowing from trees and foliage.

|   |   |
| --- | --- |
| ![Masked shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/642068af-3170-4556-b882-794f7c27b4ca/17-lightmass-global-illum-masked.png) | ![Masked shadows L](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c897d1ba-0ceb-422a-ad93-3ad2071a5e47/18-lightmass-global-illum-masked-l.png) |

## Features for Stationary Lights Only

### Bent Normal sky occlusion

Lightmass generates directional occlusion in the form of a bent normal whenever a [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) with Stationary Mobility is enabled.

### Distance field shadowmaps

Lightmass computes distance field shadowmaps for [Stationary Lights](/documentation/en-us/unreal-engine/stationary-light-mobility-in-unreal-engine). Distance field shadow maps maintain their curvy shape very well even under lower resolutions; however they do not support area shadowing or translucent shadows.

## Features for Static Lights Only

### Area lights and shadows

With Lightmass, all lights with Static Mobility are area lights by default. The shape used by Point and Spot Light sources is a sphere, whose radius is set by Light Source Radius under Lightmass Settings. Directional Light sources use a disk, positioned at the edge of the scene. Light source size is one of the two factors controlling shadow softness, as larger light sources will create softer shadows. The other factor is distance from the receiving location to the shadow caster. Area shadows get softer as this distance increases, just like in real life.

In the first image is a Static Directional Light with only static lighting, the penumbra size is the same everywhere. In the second image, Lightmass calculated area shadows whose sharpness is controlled by both the light source size and occluder distance. Notice how the shadow of the pillar is much sharper close to where the pillar meets the ground.

|   |   |
| --- | --- |
| ![Scene with the Static Directional Light with only static lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27578d80-7d57-42f9-a0ab-509b31c94ff0/19-lightmass-global-illum-only-static.png) | ![Sharpness of shadows is controlled by the light source size and occluder distance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf15df00-1c51-4234-9725-5f8af3685584/20-lightmass-global-illum-size-occluder.png) |

The light source radius for Point and Spot Lights is drawn in yellow wireframe, while the influence radius is drawn in teal. In most cases, you will want to make sure the light source does not intersect any shadow casting geometry, or the light will be emitting on both sides of that geometry.

![The light source areas](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fd48161-fb7a-4f8f-9c97-8fd4c21c35ad/21-lightmass-global-illum-area-light.png)

### Translucent shadows

Light passing through a translucent material that is applied to a static shadow casting mesh will lose some energy, resulting in a translucent shadow.

![Translucent shadow example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77752606-d962-4eb8-8864-872097965455/22-lightmass-global-illum-translucent-t.png)

#### Translucent shadow color

The amount of light passing through the material is called Transmission, and ranges between 0 and 1 for each color channel. A value of 0 would be fully opaque, and a value of 1 would mean that the incident light passes through unaffected. There is no material input for Transmission, so currently it is derived from the other material inputs as follows:

-   Lit materials
    -   BLEND\_Translucent and BLEND\_Additive: Transmission = Lerp(White, BaseColor, Opacity)
    -   BLEND\_Modulate: Transmission = BaseColor
-   Unlit materials
    -   BLEND\_Translucent and BLEND\_Additive: Transmission = Lerp(White, Emissive, Opacity)
    -   BLEND\_Modulate: Transmission = Emissive

This means that at an opacity of 0, the material will not filter out incident lighting and there will be no translucent shadow. At an opacity of 1, incident lighting will be filtered by the material's emissive or Base Color (depending on whether it is lit). Note that indirect lighting will sometimes wash out the translucent shadows and make them less saturated than the emissive or diffuse of the translucent material.

#### Translucent shadow sharpness

There are several factors controlling translucent shadow sharpness.

In the first image, a large light source was used (directional light with a Light Source Angle of 5) and in the second, a small light source was used (Light Source Angle of 0).

|   |   |
| --- | --- |
| ![Using of the large light source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/225099ea-3123-4509-a5fe-b76f4186229d/23-lightmass-global-illum-large-source.png) | ![Using of the small light source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c9ce587-6350-4f13-8b22-6f1a1895c055/24-lightmass-global-illum-small-source.png) |

In the first image, a small light source was used, but the lightmap resolution was too low to capture the sharp translucent shadows. In the second image, the material was exported at too low of a resolution (controlled by Export Resolution Scale in the Material Editor) to capture the sharp shadows.

|   |   |
| --- | --- |
| ![Small light source with a low resolution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50a4744e-b144-4315-8b89-1d7d2e64216d/25-lightmass-global-illum-resolution-low.png) | ![Material was exported of a resolution controlled by Export Resolution Scale feature](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14dba056-2d19-4d3a-88df-197c7a719a81/26-lightmass-global-illum-resolution-export.png) |

Indirect light is also affected by Translucent Materials. The window in this image filters incoming light based on its Transmission, and that light then bounces around the scene with its color modified.

![The window filters incoming light based on its Transmission](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d60d0b09-1037-42ce-bae0-b17a3457f823/27-lightmass-global-illum-trans-shadow-indir-light.png)

#### Limitations

***Translucent Materials** currently do not scatter light, so they will not bleed color onto objects around them.* The first diffuse bounce is currently not affected by translucent shadows. This means that first bounce indirect light passing through a translucent material will not be filtered by the material's **Transmission**. \* Refraction (caustics from transmission) is currently not supported.

## Getting the Best Quality with Lightmass

### Making lighting noticeable

#### Diffuse Textures

During rendering, lit pixel color is determined as BaseColor \* Lighting, so base color directly affects how visible the lighting will be. High contrast or dark diffuse textures make lighting difficult to notice, while low contrast, mid-range diffuse textures let the lighting details show through.

Compare the lighting clarity between the scene in the first image built with mid-range diffuse textures, to the scene in the second image also built with Lightmass but with noisy, dark diffuse textures. Only the most high-frequency changes are noticeable in the scene in the second image, like the shadow transitions.

|   |   |
| --- | --- |
| ![Scene build with mid-range diffuse textures](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17950b75-0832-4ea8-a956-423c14d9522e/28-lightmass-global-illum-mid-tone-diffuse.png) | ![Scene build with dark diffuse textures](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7628a49-85f8-4dc7-bd46-c4df10dcbebd/29-lightmass-global-illum-dark-tone-diffuse.png) |

The **Unlit** view mode is useful for viewing the Diffuse term. The scene in the first image looks flatter and more monotone in the Unlit view mode, which means the lighting is doing all the work and variations in final pixel color are mostly due to lighting differences. (To get good lighting, your scene should look flat and boring in the Unlit view mode.) Baking lighting and macro features into the diffuse textures will counteract the lighting.

|   |   |
| --- | --- |
| ![Using Unlit view mode for mid tone Diffuse term](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f669dc26-759e-4906-a999-b5a2481640fc/30-lightmass-global-illum-mid-tone-diffuse-unlit.png) | ![Using Unlit view mode for dark tone Diffuse term](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47bd3086-853b-442b-a811-6b5c42693bd5/31-lightmass-global-illum-dark-tone-diffuse-unlit.png) |

Using the editor's color picker on several parts of the unlit image, we can see that the scene in the first image has diffuse values around 0.5, while the scene in the second image has diffuse values around 0.08. Looking at the histogram of these unlit images in Photoshop gives a good idea of the distribution of the diffuse textures.

Photoshop shows you color values in gamma space, so a value of 186 (.73) is actually halfway between black and white, NOT a value of 127 (.5).\* The first image shows what the histogram should look like to get noticeable lighting.

![Histogram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34ef50f3-737f-4475-b30b-0c49813c7959/32-lightmass-global-illum-histogram-spo.png) ![Histogram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a63cddb-889d-4fba-9d68-0fca7fd94402/33-lightmass-global-illum-histogram-ut.png)

#### Lighting Setup

*Avoid ambient lighting! Ambient lighting like the Ambient cubemap adds a constant ambient term to your level, which reduces contrast in indirectly lit areas.  
*Setup lights so that there is high contrast between the directly lit areas and indirectly lit areas. The contrast will make it easier to pick out where shadow transitions are and will give your level a better sense of depth. \* Setup lights so that the bright areas are not too bright, and the dark areas are not completely black, but still have detail noticeable. It is important to check out the dark areas on the final target display.

### Improving lighting quality

#### Lightmap resolution

Using texture lightmaps with high resolution is the best way to get detailed, quality lighting. Using high lightmap resolution has the downsides of taking up more texture memory and increasing build times, so it is a tradeoff. Ideally, most of the lightmap resolution in your scene should be allocated around the high visual impact areas and in places where there are high frequency shadows.

#### Lightmass Solver quality

**Lightmass Solver** settings are automatically set based on what quality of build is requested in the Lighting Build Options dialog. Production should give good enough quality that the artifacts are not clearly noticeable with a diffuse texture applied.

## Getting the Best Lighting Build Times

There are several ways to improve your Lightmass build times:

*Only have high resolution lightmaps in areas that have high-frequency (quickly changing) lighting. Reduce the lightmap resolution for Brush surfaces and Static Meshes that are not in direct lighting or affected by sharp indirect shadows. This will give you high resolution shadows in the areas that are most noticeable.* Surfaces that are never visible to the player should be set to the lowest possible lightmap resolution. *Use a [Lightmass Importance Volume](/documentation/en-us/unreal-engine/cpu-lightmass-global-illumination-in-unreal-engine#lightmassimportancevolume) to contain the areas that are most important (just around the playable area).* Optimize the lightmap resolutions across the map so that build time for meshes is more even. The lighting build can never be faster than the slowest single object, regardless of how many machines are doing the distributed build. Avoid large continuous meshes that surround a large part of the level and with high lightmap resolution. You will get better build times if you break these up into more modular pieces, especially on machines with many cores. \* Meshes with a lot of self-occlusion will take longer to build, for example a rug with many layers parallel to each other will take much longer to build than a flat floor.

The **Lighting Build Info** dialog is a very important tool for improving lighting build times. First, build lighting in the level that you want to see stats for. Then, open the dialog under **Build > Lighting Info > Lighting StaticMesh Info**. Change the drop down to **Lighting Build Info**. This will show a sorted list of meshes and how long they took to compute lighting for.

![Lightning Static Mesh Statistic window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed1bbadc-4954-42e4-9ffd-a3020100aa84/34-lightmass-global-illum-statics-window.png)

## Lightmass Settings

### Lightmass Importance Volume

Many maps have meshes out to the edge of the grid in the editor, but the actual playable area that needs high quality lighting is much smaller. Lightmass emits photons based on the size of the level, so those background meshes will greatly increase the number of photons that need to be emitted, and lighting build times will increase. The Lightmass Importance Volume controls the area that Lightmass emits photons in, allowing you to concentrate it only on the area that needs detailed indirect lighting. Areas outside the importance volume get only one bounce of indirect lighting at a lower quality.

An overhead wireframe view of a multiplayer map is shown in the first image. The actual playable area that needs high quality lighting is the small green blob at the center.

In the second image, a close-up of the playable area of the multiplayer map is shown, with the correctly setup **Lightmass Importance Volume** selected. The Lightmass Importance Volume reduced the radius of the region to light from 80,000 units to 10,000 units, which is 64x less area to light.

|   |   |
| --- | --- |
| ![An overhead wireframe view of a multiplayer map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df7a40d1-74dc-4833-8c9e-4c6864cace50/35-lightmass-global-illum-jacinto-import-far.png) | ![A close-up of the playable area of the multiplayer map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16e2cc21-a8fe-4d4e-982c-d4d32896de33/36-lightmass-global-illum-jacinto-import-near.png) |

You can add a Lightmass Importance Volume to a level by dragging a **Lightmass Importance Volume** object from the **Volumes** tab of the **Place Actors** panel into the level then scaling it to the needed size.

![Adding a Lightmass Importance Volume to a level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6e71098-6e12-4cb3-bf8f-71c29a75de0e/37-lightmass-global-illum-add-lightmass-volume.png)

You can also convert a Brush into a Lightmass Importance Volume by clicking the **Convert Actor** drop down box inside the **Details** panel under **Actor**.

![Convert a Bush into a Lightmass Importance Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76f245eb-5cee-4af4-a511-6fd89667c11c/38-lightmass-global-illum-convert-brush-actor.png)

After clicking the drop down box, a menu will appear where you can select the type of Actor to replace the Brush with.

![The drop down box of convert settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bebe7d98-4e63-4ca0-a032-4c7e3bbbdb30/39-lightmass-global-illum-convert-dropdown.png)

If you place multiple Lightmass Importance Volumes, most of the lighting work will be done with a bounding box that contains all of them. However, Volume Lighting Samples are only placed inside the smaller volumes.

### World Settings

Lightmass settings can be adjusted inside the **World Settings** panel under the **Lightmass** section.

![Lightmass settings in the **World Settings** panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc9457d7-5462-426c-9641-27ef09d43ffd/40-lightmass-global-illum-world-settings-lightmass.png)

You can access **World Settings** by clicking the **Settings** icon from the main **Toolbar** on the right side of Editor and selecting **World Settings**.

![Enabling the **World Settings** panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df9a8a33-f97e-41df-a3fc-c8b8c2c1a96b/41-lightmass-global-illum-world-settings.png)

| Property | Description |
| --- | --- |
| **Static Lighting Level Scale** | Scale of the level relative to the scale of the engine, which is 1 Unreal Unit = 1cm. This is used to decide how much detail to calculate in the lighting and smaller scales will greatly increase build times. For a huge level, larger scales around 2 or 4 can be used to lower build times. |
| **Num Indirect Lighting Bounces** | Number of times light is allowed to bounce off surfaces, starting from the light source. **0** is direct lighting only, **1** is one bounce, etc. Bounce **1** takes the most time to calculate, followed by bounce **2**. Successive bounces are nearly free, but also do not add very much light, as light attenuates at each bounce. |
| **Indirect Lighting Quality** | Scales the sample counts used by the Lightmass GI solver. Higher settings result in fewer solver artifacts (noise, splotchiness) at much increased build times. Note that this will not affect artifacts due to using lightmaps (texture seams, compression artifacts, texel shapes). |
| **Indirect Lighting Smoothness** | Higher values cause the indirect lighting to be smoothed more, which can hide solver noise, but also causes detailed indirect shadows and Ambient Occlusion to be lost. It can be useful to lower this somewhat (.66 or .75) when increasing **Indirect Lighting Quality** for highest quality. |
| **Environment Color** | Color that rays which miss the scene will pick up. The environment can be visualized as a sphere surrounding the level, emitting this color of light in each direction. |
| **Environment Intensity** | Scales Environment Color to allow an HDR environment color. |
| **Diffuse Boost** | Scales the diffuse contribution of all materials in the scene. Increasing DiffuseBoost is an effective way to increase the intensity of the indirect lighting in a scene. The diffuse term is clamped to 1.0 in brightness after DiffuseBoost is applied, in order to keep the material energy conserving (meaning light must decrease on each bounce, not increase). If raising **Diffuse Boost** does not result in brighter indirect lighting, the diffuse term is being clamped and the Light's **Indirect Lighting Scale** should be used to increase indirect lighting instead. |
| **Volume Lighting Method** | Technique to use for providing precomputed lighting at all positions inside the Lightmass Importance Volume. |
| **Use Ambient Occlusion** | Enables static Ambient Occlusion to be calculated by Lightmass and built into your lightmaps. |
| **Generate Ambient Occlusion Material Mask** | Enables generating textures storing the AO computed by Lightmass. These can be accessed through the **Precomputed AO Mask** material node, which is usefull for blending between material layers on environment assets. Be sure to set **Direct Illumination Occlusion Fraction** and **Indirect Illumination Occlusion Fraction** to **0** if you only want the Precomputed AO Mask! |
| **Visualize Material Diffuse** | Override normal direct and indirect lighting with just the material diffuse term exported to Lightmass. This is useful when verifying that the exported material diffuse matches up with the actual diffuse. |
| **Visualize Ambient Occlusion** | Override normal direct and indirect lighting with just the AO term. This is useful when tweaking ambient occlusion settings, as it isolates the occlusion term. |
| **Compress Lightmaps** | Enables compressing lightmap textures. Disabling lightmap texture compression will reduce artifacts but increase memory and disk size by 4x. Use caution when disabling this. |
| **Volumetric Lightmap Detail Cell Size** | Size of an Volumetric Lightmap voxel at the highest density (used around geometry), in world space units. This setting has a large impact on build times and memory, use with caution. Halving the **Detail Cell Size** can increase memory by up to a factor of 8x. |
| **Volumetric Lightmap Maximum Brick Memory Mb** | Maximum amount of memory to spend on Volumetric Lightmap Brick data. High density bricks will be discarded until this limit is met, with bricks furthest from geometry discarded first. |
| **Volumetric Lightmap Spherical Harmonic Smoothing** | Controls how much smoothing should be done to Volumetric Lightmap samples during Spherical Harmonic de-ringing. Whenever highly directional lighting is stored in a Spherical Harmonic, a ringing artifact occurs which manifests as unexpected black areas on the opposite side. Smoothing can reduce this artifact. Smoothing is only applied when the ringing artifact is present. **0** = no smoothing, **1** = strong smooth (little directionality in lighting). |
| **Volume Light Sample Placement Scale** | Scales the distances at which volume lighting samples are placed. Volume lighting samples are computed by Lightmass and are used for GI on movable components. Using larger scales results in less sample memory usage and reduces Indirect Lighting Cache update times, but less accurate transitions between lighting areas. |
| **Direct Illumination Occlusion Fraction** | How much of the AO to apply to direct lighting. |
| **Indirect Illumination Occlusion Fraction** | How much of the AO to apply to indirect lighting. |
| **Occlusion Exponent** | Higher exponents increase contrast. |
| **Fully Occluded Samples Fraction** | Fraction of samples taken that must be occluded in order to reach full occlusion. |
| **Max Occlusion Distance** | Maximum distance for an object to cause occlusion on another object. |
| **Force No Precomputed Lighting** | This essentially deactivates Lightmass' ability to produce light and shadowmaps, forcing the level to only use dynamic lighting. |
| **Packed Light and Shadow Map Texture Size** | Maximum size of textures for packed light and shadow maps. |

### Light Settings

Below are Lightmass settings that can be adjusted inside the properties of a light under the **Lightmass** section.

![Lightmass settings for the Lights](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc441279-6398-4fc1-ac6d-5f55cee1b7ec/42-lightmass-global-illum-light-settings.png)

| Property | Description |
| --- | --- |
| **Light Source Angle** | For **Directional Lights Only**, determines the angle that the light's emissive surface extends relative to a receiver, affects penumbra sizes. |
| **Indirect Lighting Saturation** | **0** will result in indirect lighting being completely desaturated, **1** will be unchanged. |
| **Shadow Exponent** | Controls the falloff of shadow penumbras, or how fast areas change from fully lit to fully shadowed. |
| **Use Area Shadows for Stationary Light** | Whether to use area shadows for stationary light precomputed shadowmaps. Area shadows get softer the further they are from shadow casters, but require higher lightmap resolution to get the same quality where the shadow is sharp. |

### Primitive Component Settings

Below are Lightmass settings that can be adjusted on a **Brush** added from the **Geometry** tab of the **Place Actors** panel. These options are found under the **Details** panel of the **Brush**.

![Lightmass settings for the Primitives](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05c0e7d9-139c-4e87-89a5-90cf3f4397ee/43-lightmass-global-illum-primitive-settings.png)

| Property | Description |
| --- | --- |
| **Use Two Sided Lighting** | If checked, this object will be lit as if it receives light from both sides of its polygons. |
| **Shadow Indirect Only** | If checked, this object will only shadow indirect lighting. This is useful for grass, since the geometry that is rendered is just a representation of the actual geometry and does not necessarily cast accurately shaped shadows. It is also useful for grass because the resulting shadows would be too high frequency to be stored in precomputed lightmaps. |
| **Use Emissive for Static Lighting** | If true, allow using the emissive for static lighting. |
| **Use Vertex Normal for Hemisphere Gather** | Typically the triangle normal is used for hemisphere gathering which prevents incorrect self-shadowing from artist-tweaked vertex normals. However in the case of foliage whose vertex normal has been setup to match the underlying terrain, gathering in the direction of the vertex normal is desired. |
| **Emissive Boost** | Scales the emissive contribution of all materilas applied to this object |
| **Diffuse Boost** | Scales the diffuse contribution of all materials applied to this object. |
| **Fully Occluded Samples Fraction** | Fraction of AO samples taken from this object that must be occluded in order to reach full occlusion on other objects. This allows controlling how much occlusion an object causes on other objects. |

### Base Material Settings

Below are the Lightmass settings that can be adjusted inside a Material for the Base Node under the **Details** panel.

For more information on the Material Editor, see the [Material Editor User Guide](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide).

![Lightmass settings for the Materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9b492dd-2185-41fb-a2bd-5ed66bb4b3b8/44-lightmass-global-illum-material-settings.png)

| Property | Description |
| --- | --- |
| **Diffuse Boost** | Scales the diffuse contribution of this material to static lighting. |
| **Export Resolution Scale** | Scales the resolution that this material's attributes are exported at. This is useful for increasing material resolution when details are needed. |
| **Cast Shadow as Masked** | For translucent materials, treats the material as if it is masked for the purposes of shadow casting. |