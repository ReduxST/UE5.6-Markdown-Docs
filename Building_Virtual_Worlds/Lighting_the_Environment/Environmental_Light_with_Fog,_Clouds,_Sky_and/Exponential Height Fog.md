# Exponential Height Fog

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine)  
**Processed:** 2025-06-14 16:22:45

---

**Exponential Height Fog** creates more density in low places of a map and less density in high places. The transition is smooth, so you never get a hard cutoff as you increase altitude. Exponential Height Fog also provides two fog colors — one for the hemisphere facing the dominant directional light (or straight up if none exists), and another color for the opposite hemisphere.

## Using Exponential Height Fog

In the **Place Actors** panel, select the **Exponential Height Fog** Actor, under **Visual Effects**. Left-click and drag to place it in the world.

![Drag the Exponential Height Fog Actor into your scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2bff354-b80f-457a-88af-e34aac99afe0/01-placing-exponential-fog-in-the-world.png)

Positioning the Exponential Height Fog Actor will determind the height of the fog. Use the **Fog Height Falloff** to further adjust the height.

![Exponential Height Fog: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd1e344f-0428-49b9-9019-e7d1a9b3a78c/02-exponential-height-fog-disabled.png)

![Exponential Height Fog: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/669dc61c-9481-43a6-b117-ec6c76244ccb/03-exponential-height-fog-enabled.png)

### Exponential Height Fog Properties

In the **Exponential Height Fog Component** section, you can edit the following properties related to the component:

| **Property** | **Description** |
| --- | --- |
| Exponential Height Fog Component |   |
| **Fog Density** | This is the global density factor, which can be thought of as the fog layer's thickness. |
| **Fog Height Falloff** | Height density factor controls how the density increases as height decreases. Smaller values make the transition larger. |
| **Second Fog Data** | 
These settings control the secondary fog level. Setting the **Fog Density** of this secondary fog layer to **0** will have no influence.

-   **Fog Density:** The secondary fog layer's global density factor, which can be used to add another fog layer thickness.
-   **Fog Height Falloff:** The height density factor for the secondary fog layer that controls how the density increases as height decreases. Smaller values make the transition larger.
-   **Fog Height Offset:** The height offset relative to the Actor's Z height position in the world.



 |
| **Fog Inscattering Color** | Sets the inscattering color for the fog. Essentially, this is the fog's primary color. |
| **Sky Atmosphere Ambient Contibution Color Scale** | This color is used to modulate the Sky Atmosphere component conntribution to the non-directional component of the fog. |
| **Fog Max Opacity** | This controls the maximum opacity of the fog. A value of 1 means the fog will be completely opaque, while 0 means the fog will be essentially invisible. |
| **Start Distance** | Distance from the camera that the fog will start. |
| **Fog Cutoff Distance** | Scene elements past this distance will not have fog applied. This is useful for excluding skyboxes that already have fog baked into them. |
| Inscattering Texturing |   |
| **Inscattering Color Cubemap** | Cubemap that can be specified for fog color, which is useful to make distant, heavily fogged scene elements match the sky. When the cubemap is specified, **Fog Inscattering Color** is ignored, and Directional inscattering is disabled. |
| **Inscattering Color Cubemap Angle** | Angle to rotate the **Inscattering Color Cubemap** around the Z (height) axis. |
| **Inscattering Texture Tint** | The tint color used when **Inscattering Color Cubemap**, which is useful for making quick edits without having to reimport the cubemap specified with **Inscattering Color Cubemap**. |
| **Fully Directional Inscattering Color Distance** | Distance at which **Inscattering Color Cubemap** should be used directly for the Inscattering Color. |
| **Non-Directional Inscattering Color Distance** | Distance at which only the average color of **Inscattering Color Cubemap** should be used as Inscattering Color. |
| Directional Inscattering |   |
| **Directional Inscattering Exponent** | Controls the size of the directional inscattering cone, which is used to approximate inscattering from a directional light source. |
| **Directional Inscattering Start Distance** | Controls the start distance from the viewer of the directional inscattering, which is used to approximate inscattering from a directional light. |
| **Directional Inscattering Color** | Sets the color for directional inscattering, used to approximate inscattering from a directional light. This is similar to adjusting the simulated color of a directional light source. |
| Volumetric Fog |   |
| **Volumetric Fog** | 

Whether to enable Volumetric Fog. Scalability settings control the resolution of the fog simulation.

The Volumetric Fog currently does not support **Start Distance**, **Fog Max Opacity**, and **Fog Cutoff Distance**. In general, it cannot match Exponential Height Fog, in general, since it has non-physical behavior.



 |
| **Scattering Distribution** | Controls the scattering phase function—how much incoming light scatters in various directions. A distribution value of 0 scatters equally in all directions, while a value of 0.9 scatters predominantly in the light direction. In order to have visible volumetric fog light shafts from the side, the distribution will need to be closer to a value of 0. |
| **Albedo** | The height fog particle reflectiveness used by Volumetric Fog. Water particles in the air have an albedo near white, while dust has slightly darker value. |
| **Emissive** | Light emitted by Exponential Height Fog. This is a density, so more light is emitted the further you are looking through the fog. In most cases, Sky Light is a beter choice. However, Volumetric Fog does not support precomputed lighting right now, so Stationary Sky Light is unshadowed, and Static Sky Light doesn't affect Volumetric Fog at all. |
| **Extinction Scale** | Scales the height fog particle extinction amount used by Volumetric Fog. Values larger than 1 cause fog particles everywhere absorb more light. |
| **View Distance** | Distance over which Volumetric Fog should be computed. Larger values extend the effect into the distance but expose under-sampling artifacts in details. |
| **Start Distance** | The distance from the camera that the Volumetric Fog will start, in world units. |
| **Near Fade in Distance** | The distance over which Volumetric Fog will fade in from the start distance. |
| **Static Lighting Scattering** | Controls the intensity of scattered static lighting in the Volumetric Fog. |
| **Override Light Color with Fog Inscattering Colors** | Whether to use **Fog Inscattering Color** for the Sky Light's **Volumetric Scattering Color** and **Directional Inscattering Color** for the Directional Light's **Scattering Color**. Make sure your Directional Light has **Atmosphere Sun Light** enabled. It allows Volumetric Fog to better match Exponential Height Fog in the Distance but produces non-physical volumetric lighting that may not match surface lighting. |

## Using Exponential Height Fog Features

The sections below cover the usage of some of the features found in the Exponential Height Fog volume:

### Secondary Fog Layer

Add a second fog layer to your level using the properties found under the **Second Fog Data** category. It enables you better define and control fog at a second Z (height) level in your map with controls for density, height falloff, and height offset.

![Exponential Height Fog: | Single Fog Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00470ac1-c62c-4153-9fc3-9267956eb9d8/03-exponential-height-fog-enabled.png)

![Exponential Height Fog: | Added Second Fog Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17c564f4-9bb3-4cf4-9028-d63b12bfb758/04-second-layer-exponential-height-fog.png)

### Volumetric Fog

Control Volumetric Fog by enabling it in the Exponential Height Fog's **Details** panel under the **Volumetric Fog** category.

Unreal Engine's Volumetric Fog computes participating media density and lighting at every point in the camera frustum so that varying densities and any number of lights affecting the fog can be supported.

![Volumetric Fog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/384ec87a-79c8-47ee-9dca-c664802cc995/volumetricfog.png)

See [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine) for additional details and usage.

## Performance

The rendering cost of Exponential Height Fog is similar to two layers of constant density height fog with an additional optimization; fog **Start Distance**. The start distance is used to artificially keep some defined area in front of the viewer without fog. This also helps performance as pixels can be culled by the Z-buffer.

Below are examples of this in practice:

-   Fog Start Distance: 0
-   Fog Start Distance: 5000
-   Fog Start Distance: 5000 with high fog density

  ![Fog Start Distance: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fda1e9f-cc8d-4480-b940-28fe1e892ad7/05-fog-start-distance-0.png) ![Fog Start Distance: 5000](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29f21778-0f3d-4246-99d3-b528c6c45d6f/06-fog-start-distance-5000.png) ![Fog Start Distance: 5000 with high fog density](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30565454-7156-42a8-af8a-d7f6e58d8cbf/07-fog-start-distance-5000-high-density.png)

Fog Start Distance Preview

Depending on the scene content and when using a far fog **Start Distance**, the rendering cost can be 50% or less. This optimization is implemented by rendering a full-screen quad that has a Z-value and depth test enabled.

### The Expense of Cloud Rendering

When `r.PostProcessing.PropagateAlpha` is enabled and any feature, such as Volumetric Cloud, Sky Atmosphere, and Exponential Height Fog, with alpha holdout enabled will cause cloud rendering to use the expensive rendering path.