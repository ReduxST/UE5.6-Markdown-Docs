# Shadowing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/shadowing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/shadowing-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:21

---

Shadows make objects feel grounded in the world. They give the viewer a sense of depth and space. Shadowing is supported by all available [types of lights](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) and determined by a light's mobility.

## Supported Shadowing Methods

The type of shadowing used by a light is determined by what its Mobility is set to: **Static**, **Stationary**, or **Movable**. Mobility is the primary guiding factor in whether a light should cast a precomputed shadow baked into a texture called a lightmap, a dynamic shadow generated in real-time, or one that uses a combination of precomputed and dynamic shadowing.

A Light's Mobility can be set independently of other lights in the Level, meaning that you can use any combination of mobilities to light the scene.

The following shadowing methods are available to use:

Some require Project Settings to be enabled, or additional properties to be enabled on the Light to work.

-   Shadow Mapping
    -   The default shadowing method that renders geometry into shadow depth maps. This shadowing method works for all platforms that support dynamic shadowing, but it requires manual setup of shadowing distances and only culls per-component, causing poor performance with high polygon scenes. Also, it does not support [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) geometry.
-   [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine)
    -   This shadowing method renders geometry into virtualized shadow depth maps. It provides high quality shadows for next-gen projects with simplified setup. It has high efficiency culling when used with [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) geometry.
-   [Ray-traced Shadows](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine)
    -   This method traces a set number of samples per pixel using [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) with denoising algorithms to render high quality ray-traced shadows in real-time.
-   [Distance Field Shadows](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine)
    -   This method uses signed distance fields per Static Mesh and is used by [Lumen Software Ray Tracing](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) for dynamic soft area shadows.
-   [Precomputed Shadows with Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine)
    -   This method uses lighting data from the scene to generate lightmap textures that are applied to Static geometry in the Level. Geometry requires additional setup with proper lightmap UVs. Precomputing lighting for the scene can vary depending on machine specifications, scene complexity, and other factors when determining how long a light build will take.

## Static and Stationary Light Preview Shadowing

When editing a Light with its Mobility set to **Stationary** or **Static** the light is considered *un-built*. **Preview Shadowing** is enabled to give you an idea of what the shadows will look like when lighting is rebuilt, but they are not representative of the final, baked result.

To indicate what are actually preview shadows, shadows from these lights are shown in the Level Editor with the text **Preview**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbdfaa3b-5ea1-48a0-a043-7c4d4f680ea1/unbuiltshadows.png)

Preview text over shadows is visible only while working in the Level Editor. If you launch your project in Play-In-Editor (PIE) or Standalone Game modes, no text will appear over unbuilt shadows.

To resolve any preview shadows, you will need to build lighting. Use the Main Menu to select **Build > Build All Levels** to kick off a lighting build.

|   |   |
| --- | --- |
| ![built scene shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13e0ae59-4ece-4e44-8247-9b3f149a7ea6/scene-shadows.png) | ![preview shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22df884b-4910-4962-b4bd-3be200fbde4e/preview-shadows.png) |
| Built Scene Shadows | Preview Shadows |

Preview shadows can be disabled while working in the Editor by unchecking the **Preview Shadows Indicator** under the Level Viewport **Show > Visualize** menu.

## Configuring Shadowing Properties of Lights

The following properties can be found on the available [Types of Lights](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine).

The properties are accessible through the Level's **Details** panel when a Light is selected.

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
| 
![directional light properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33e5d9df-e7a1-450b-9bae-4c5cb8073301/directional-light-properties.png)

 | 

![sky light properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/346a02e6-d91f-44db-afd6-ffd8be0fdf46/sky-light-properties.png)

 | 

![point light properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77a99a1d-5037-42a2-a3c6-f63fcafead80/point-light-properties.png)

 | 

![spot light properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97222e2a-008f-4177-bec3-b2d0b01f83b6/spot-light-properties.png)

 | 

![rect light properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12989309-d38e-4f7e-9d85-a0b9082a0ecb/rect-light-properties.png)

 |
| Directional Light | Sky Light | Point Light | Spot Light | Rect Light |

Click images for full size.

### Source Angle, Radius, Height and Width

Each type of light has an option to set the angle, radius, or height and width of its light source to control the size and shape of the shadows it casts. Larger angles, radii, heights, and widths soften shadows for objects the light affects.

In the examples below, the left Spot Light has no source radius specified and produces sharp shadows. The right Spot Light has a moderate source radius specified, which softens the shadows of that light depending on the distance of the objects from it.

![source radius example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c33814fa-f722-4633-8610-df4226f64bb7/source-radius-example.png)

When looking at the Spot Lights in the Level Editor viewport, you can see the Source Radius of the light is represented by the yellow sphere on the Spot Light on the right side.

![source radius editor example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b81d3c49-158f-4f45-b90c-0e47f2b5cac9/source-radius-editor-example.png)

Point, Spot, and Rect Lights all have a visible source size that updates in real-time while being edited.

![point, spot, rect light source sizes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/854a0553-3bae-4e16-83f9-50cbdee83a1f/point-spot-rect-light-sources.png)

Point Lights and Spot Lights have an additional option to control length of the Source Radius with the **Source Length** property, making it possible to create cylindrical light shapes like a tube light.

![point and spot light source length](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38cbdfec-f43e-4519-849f-b2c831f9312d/point-spot-source-length.png)

### Attenuation Radius

The **Attenuation Radius** of Point, Spot, and Rect Lights enable you to set a bounding area that this light will affect. While this is not physically accurate, it is important to clamp the bounds of dynamic shadowing-casting lights for performance.

In the examples below, the left Spot Light has a smaller attenuation radius than the one one on the right. Notice how the light only affects the area within the farthest point of its radius.

![light attenuation radius example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c1e8b2c-8ad3-4377-a62d-9eebc00abe2f/light-attenuation-radius.png)

When the lights are selected, you can see how the distance of the attenuation radius affects the objects within its area and doesn't shadow objects outside of its reach.

![light attenuation radius editor view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6734c88c-4125-4926-81b7-46574bc62c6d/light-attenuation-radius-editor.png)

### Casting Shadows

**Cast Shadow** controls whether the selected light should contribute shadows to the scene.

![shadow casting on and off](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc8aedc1-6769-4076-b6aa-e206bee11ce7/shadow-casting-on-off.png)

Left, shadow casting enabled; Right, shadow casting disabled.

### Volumetric Shadowing

The **Volumetric Scattering Intensity** scales the fog intensity and light color when enabled. It enables a light to contribute more to fog without having to directly increase its intensity.

Lights contribute to [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine) when enabled for the scene.

You can control the contribution of individual lights to Volumetric Fog with **Volumetric Scattering Intensity**. By default, volumetric shadows are disabled for lights but can be enabled with **Cast Volumetric Fog**.

![Volumetric Shadow: Disabled (default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdf48752-9eb7-40f7-9512-b3c93e040529/volumetric-shadow-off.png)

![Volumetric Shadow: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6dcdd13a-e31e-4009-a839-697b0eb3aa15/volumetric-shadow-on.png)

### Global Illumination Indirect Lighting

[Global Illumination](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) provides indirect lighting for a scene from light that hits a surface and bounces within a space. It provides fill lighting and soft area shadowing for surfaces to ground objects within the space. Unreal Engine supports indirect lighting with precomputed baked global illumination from Lightmass, and dynamically with [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) and [Screen Space Global Illumimation](/documentation/en-us/unreal-engine/screen-space-global-illumination-in-unreal-engine).

The Mobility of a light determines which method a light should contribute to (in some cases).

![lumen-global-illumination example scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09c4c30a-3ef6-4223-be35-7368b37e076a/lumen-global-illumination.png)

Scene showing real-time indirect lighting with Lumen dynamic global illumination.

Some dynamic global illumination methods are not able to be combined with precomputed ones, such as Lumen with baked global illumination. However can work together, such as using [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) with baked global illumination.

### Shadow Bias

When using the default shadow mapping method, the shadow map generated to shadow assets in the Level are set per-light to maintain a balance between performance and shadowing quality. Shadow maps have some limitations, such as faceting on curved geometric surfaces or self-shadowing artifacts, that can be adjusted using **Shadow Biasing** properties found on lights.

Shadow bias is a per-light set of properties that help improve accuracy of self-shadowing and contact hardening from a light source. Biasing settings are useful for finding a trade-off between accuracy in one area while reducing self-shadowing artifacts in another.

![Default Shadow Bias Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20984b0a-3d82-47e4-bb31-e6072b995983/shadow-bias-default.png)

![Adjusted Shadow Bias Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b3863e0-8bf4-463c-9a47-dfb065e7b6de/shadow-bias-adjusted.png)

For more information, see [Movable Lights](/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine).

### Contact Shadows

[Contact Shadows](/documentation/en-us/unreal-engine/contact-shadows-in-unreal-engine) are a per-light additive feature to use on top of other shadowing methods employed by lights. It is a screen space effect that draws rays from a pixel's position toward the light source through the scene's depth buffer. Thus, it helps improve contact hardening and accuracy of shadows in some cases, but is limited by what is visible within the current camera view.

Use **Contact Shadows Length** property to define their length whereby a value of 1 is equal to the entire screen, 0.5 is half the screen, and 0 is disabled. Lower values produce less noise and may appear more accurate depending on the scene.

![Contact Shadows Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04c8f18e-81b8-46b2-b054-9a182620fbec/contact-shadows-off.png)

![Contact Shadows Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c35df2bf-8664-4830-ba71-cbc2904e157a/contact-shadows-on.png)

### Lightmass Settings

The **Lightmass** settings on a light affect precomputed lighting when the [Light Mobility](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) is set to **Static** or **Stationary** and a lighting build has been completed.

These settings control the baked softness of the shadow with [Source Angle](/documentation/en-us/unreal-engine/shadowing-in-unreal-engine#source-angle-radius-height-and-width) for Directional Lights, how much this light's saturation affects indirect lighting, and the fall off of shadow penumbras with a shadow exponent.

### Shadowing with Materials and Textures

Lights can use [Light Functions](/documentation/en-us/unreal-engine/using-light-functions-in-unreal-engine) and [IES Light Profiles](/documentation/en-us/unreal-engine/using-ies-light-profiles-in-unreal-engine) to further define aspects of lights and their shadows.

**Light Functions** are a Material type that can be applied to non-lightmapped lights, like **Movable Lights** and the direct lighting of **Stationary Lights** to filter a light's intensity, but not its color. It can also be used to apply an animated texture to the light source. For example, simulating moving cloud shadows from a Directional Light.

![light function on a spot light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ab3e849-4df8-48d9-b6f3-26b19196c5d5/light-functions.png)

**IES Light Profiles** are textures which describe a light's distribution from a light source using real-world measured data. They are a lighting industry standard method of diagramming the brightness and fall off of lights as it exists in a particular light fixture.

![ies profile examples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe7ba5f4-5ad9-4d7d-8b97-e5a7ac41147f/01-ies-light-profiles-examples.png)

### Distance Field Shadowing

[Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) have a variety of uses from shadowing to creating interactive materials and dynamic indirect lighting and reflections with [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine).

A mesh distance field representation of a Static Mesh is used to produce soft shadowing from a **Movable** light sources when the **Distance Field Shadows** property is enabled.

This method of shadowing is similar to other methods, like [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) and [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) where the [Source Angle, Radius, or Size](/documentation/en-us/unreal-engine/shadowing-in-unreal-engine#source-angle-radius-height-and-width) control penumbra of shadow.

![shadow maps versus distance field shadows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6a3f8a4-adf2-4a08-919d-6313df532fce/distance-field-shadows.png)

Left, shadows maps; Right, shadows from mesh distance fields.

### Directional Light

[Directional Lights](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine) contains unique settings relevant to this light source to simulate large world lighting.

#### Cloud and Atmosphere Shadowing

In the Light's **Atmosphere and Clouds** section, there are settings and properties that affect how this light source will interact with [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) and [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine), such as having the sun affect the atmosphere and clouds, casting shadows from or onto clouds, and shadow quality, to name a few.

![cloud and atomosphere shadowing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c5aa7a1-9e0a-4f94-a5d1-1a4af6bd4547/vt_cloudexamples.png)

#### Cascaded Shadow Maps

Cascaded Shadow Maps split the camera view frustum into different cascades (or shadow levels of detail) for whole scene dynamic shadowing. This optimizes shadows over larger distances to provide quality where it's needed: higher quality closer to the camera position, lower quality farther away from the camera position.

The settings found under the **Cascaded Shadow Maps** section specify the number of cascades to use, their maximum distance, where to distribute quality, and where the transition between each cascade should be.

![cascaded shadow maps from a directional light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9c85002-5d73-47f3-bafd-7ff2fd78626e/csm-shadows.gif)

Cascaded shadow maps have a maximum distance you specify. But when you need shadowing on larger objects beyond this, you can use the **Far Shadow Cascades** to enable shadowing art farther distances. However, the one difference here is that you have to enable specified assets that you want to have shadowing at this distance. You can do this with this by selecting an Actor in the Level and enabling **Far Shadow** on that asset.

![directional light far shadow](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/821d4416-e064-4b39-adda-f73d646516c8/csm-far-shadow.png)

## Shadow Performance and Optimization Options

Performance of shadows can largely depend on the [shadowing method being employed](/documentation/en-us/unreal-engine/shadowing-in-unreal-engine#supported-shadowing-methods) for your project.

The properties mentioned in this section are starting points for optimizing lighting within a scene, especially for dynamic lights where some methods of shadowing are more expensive, like the default shadow mapping.

-   **Attenuation Radius** for Point, Spot, and Rect Lights is important to control not only where light is within the scene but to limit the number of objects that have to be shadowed, which can make them expensive for some shadowing methods, especially the default shadow mapping method.
-   Disabling **Cast Shadows** on dynamic lights can improve performance if the shadows are not contributing a lot to the scene, the light affects a lot of objects with a large attenuation radius, or assets have a lot of geometric detail. This mostly affects methods lit using traditional shadow mapping, but it's important to consider for any dynamic light to reduce frame cost.
-   Setting a **Max Draw Distance** on a light will limit its dynamic shadowing contribution up to that point. For scenes where you have a lot of small to medium-sized lights affecting an area, this can help reduce frame cost. Using **Max Fade Range** in addition to the max draw distance will fade that light out over time so that it doesn't abruptly appear and disappear.
-   The Shadow Map shadowing method is a product of balancing quality with performance. Sometimes, you want to trade performance for a bit of quality. The **Shadow Map Resolution** property enables you to increase the shadow map of the selected light to trade quality for performance.
-   When using [Hardware Ray Tracing Shadows](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) you can adjust the **Samples Per Pixel** property under the **Ray Tracing** section to apply more samples to the light's ray-traced shadows. Fewer samples reduce quality and improve performance, while more samples improve quality (to a point with the denoising algorithm) but cost more.