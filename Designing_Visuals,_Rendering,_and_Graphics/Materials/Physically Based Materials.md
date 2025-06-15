# Physically Based Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:32

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c327e06a-0458-4fab-b450-5a0a8f027786/physmatheader.png)

This document is designed to provide guidelines and best practices for working within Unreal Engine's **physically based Materials** system. It assumes that you have some familiarity with the Material creation process in Unreal. If you are completely new to Materials in Unreal, you may prefer to start with the [Essential Material Concepts](/documentation/en-us/unreal-engine/essential-unreal-engine-material-concepts) page.

This page focuses only on the Material attributes that are directly related to the physically based shading workflow. For a complete breakdown of all inputs on the Main Material node, see the [Material Inputs](/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine) page.

## What Does Physically Based Mean?

**Physically based rendering** (PBR) means that surfaces approximate the way light behaves in the real world, as opposed to the way we intuitively think it should. Materials that adhere to PBR principles are more accurate and typically more natural looking than a shading workflow that relies fully on artist intuition to set parameters.

Physically based Materials work equally well in all lighting environments. In addition, Material values can be less complex and interdependent, resulting in a more user-friendly Material creation workflow. These benefits are applicable even for non-photorealistic rendering, as evident in films from Pixar [\[4\]](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#smits) and Disney [\[3\]](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#burley).

For an in depth technical look at Unreal Engine's physically based Material and shading model, refer to this SIGGRAPH presentation [2](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#karis).

## PBR Material Attributes

These are the Material attributes that are directly related to the physically based aspect of Unreal Materials.

-   [Base Color](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#basecolor)
-   [Roughness](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#roughness)
-   [Metallic](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#metallic)
-   [Specular](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#specular)

All of these inputs are designed to accept values between 0 and 1. In the case of Base Color this means a color or texture sample with RGB values that fall between 0 and 1.

Physically based values can be measured from real world Materials. Some examples are given below.

### Base Color

Base Color defines the overall color of the Material. The Base Color input accepts a **Vector3 (RGB)** value where each channel is automatically clamped between 0 and 1.

![Base Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c4dc23f-b578-4eec-9060-1cfb75fbf2c4/base-color.png)

If taken from the real world, this is the color when photographed using a polarizing filter (polarization removes the specular of nonmetals when aligned).

**Measured BaseColor values for nonmetals (intensity only):**

| Material | BaseColor Intensity |
| --- | --- |
| Charcoal | 0.02 |
| Fresh asphalt | 0.02 |
| Worn asphalt | 0.08 |
| Bare soil | 0.13 |
| Green grass | 0.21 |
| Desert sand | 0.36 |
| Fresh concrete | 0.51 |
| Ocean Ice | 0.56 |
| Fresh snow | 0.81 |

**Measured BaseColors for metals:**

| Material | BaseColor (R, G, B) |
| --- | --- |
| Iron | (0.560, 0.570, 0.580) |
| Silver | (0.972, 0.960, 0.915) |
| Aluminum | (0.913, 0.921, 0.925) |
| Gold | (1.000, 0.766, 0.336) |
| Copper | (0.955, 0.637, 0.538) |
| Chromium | (0.550, 0.556, 0.554) |
| Nickel | (0.660, 0.609, 0.526) |
| Titanium | (0.542, 0.497, 0.449) |
| Cobalt | (0.662, 0.655, 0.634) |
| Platinum | (0.672, 0.637, 0.585) |

### Roughness

The Roughness input controls how rough or smooth a Material's surface is. In the Material this manifests as how sharp or blurry reflections appear on the Material.

Rough Materials scatter reflected light in more directions than smooth Materials, which results in diffuse, sometimes subtle reflections. Smooth surfaces reflect light more uniformly, resulting in clear, focused reflections or specular highlights.

-   A Roughness of 0 (smooth) results in a mirror reflection.
-   A Roughness of 1 (rough) results in a diffuse or matte surface.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/214b071e-334f-4d92-99f3-bead35cc2ef1/roughness_nonmetal.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83e75954-9364-4c72-a2de-7c872ab5d431/roughness_metal.png)

Roughness values from 0 to 1. Nonmetal top, metal bottom.

                    ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a26b60de-6af0-421b-a243-8c1915a3b08f/roughness-slider-00.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/beb9fcfd-945d-4e3e-8d90-eda1f376ed1b/roughness-slider-01.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/128aaa0c-8f8e-4585-aa08-c465eeee0cd5/roughness-slider-02.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec1f5040-515d-4e29-a711-7d113b2eae10/roughness-slider-03.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d2f4c13-9884-4f1c-9da6-39785a3eabc5/roughness-slider-04.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73df6818-770b-434d-912b-91478d10beba/roughness-slider-05.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1956dab5-8343-4e61-b6df-a6fc98d89752/roughness-slider-06.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/269dc105-ffeb-4160-8960-18969d1b5ec3/roughness-slider-07.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8088029-f72e-43a3-9a19-668f28c2212c/roughness-slider-08.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d0bb797-4c40-46ec-b9f8-7d2552ed4dc7/roughness-slider-09.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b34497f-1966-43a6-9e45-017cbcbfd5fa/roughness-slider-10.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/360754bd-878f-4ac4-9453-04d4aa9e7a6a/roughness-slider-11.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25b84917-afa1-41b0-87f3-4ae862fd4c04/roughness-slider-12.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c498b499-40f8-4a51-b0a8-e2842df208c9/roughness-slider-13.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79a7f477-3e47-4114-9a6a-7962154bddaf/roughness-slider-14.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/055e0ac1-edef-4b20-93e9-6fc2aa956d1a/roughness-slider-15.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e9389d3-6286-449b-bcd0-e8cd5a42adf4/roughness-slider-16.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ab69bd7-1f6a-4344-9af2-0150b5740f53/roughness-slider-17.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76375c7c-aa25-47a0-ab1c-dab965bbfbec/roughness-slider-18.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93f6cc74-3f88-4f11-9bc2-e92f9cc11653/roughness-slider-19.png) ![Roughness value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1432aebc-b944-4f4a-8518-29a32a85b5ea/roughness-slider-20.png)

**Roughness values from 0 to 1.**

#### Mapping Roughness

Roughness is frequently mapped on objects using a grayscale texture to add physical variation to a surface. Dark areas on a roughness map appear mirrorlike on the Material, while light areas are rough and appear less reflective.

The video below shows the Roughness value increasing from 0 to 1, with a perlin texture controlling the distribution of **light (rough)** and **dark (smooth)** values. At 0, the Material preview is completely mirrorlike. At 1, the Material is perfectly matte. In-between values are more interesting, as parts of the surface appear smooth and parts appear rough.

Roughness maps are frequently used to add scruffs, smudges, or other imperfections to Materials like plastic and metal.

#### Roughness vs. Specular

The interplay between roughness and specular is an important point to understand, particularly if you were working in Unreal Engine before the PBR workflow was adopted.

**Specularity** refers to the amount of [specular light](https://en.wikipedia.org/wiki/Specular_reflection) reflected by a surface. This value is inherent to the Material type, and usually the default value of 0.5 is accurate. The Specular input is **not used for reflection/specularity maps** or to add surface variation. These should be handled in the Roughness map.

### Metallic

The Metallic input accepts a value between 0 and 1, and defines whether your Material behaves as a metal or nonmetal.

In most cases, you should treat Metallic as a binary property in Unreal Engine. For pure surfaces, such as pure metal, pure stone, pure plastic, and so on, you should set Metallic to **either 0 or 1**, not anything in between. When creating hybrid surfaces like corroded, dusty, or rusty metals, you may find that you need some value between 0 and 1.

-   **Nonmetals** have a Metallic value of 0. This is the default value.
-   **Metals** have a Metallic value of 1.

![Metallic values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c9ce65a-a57b-4d94-869a-a7ce986e0a80/metallic.png)

Metallic values 0 to 1.

You may be reluctant at first to make any Material completely metallic. Resist the impulse to use partial values unless you have a good reason.

This example shows how a surface changes when Metallic is increased from 0 to 1 on a Material with relatively low Roughness.

          ![Metallic value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/daa404d9-6fce-4ed1-a225-b814d118f8ea/metallic-slider-00.png) ![Metallic value .1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3685ab77-d15b-4e6f-9c01-ccd1947d8017/metallic-slider-01.png) ![Metallic value .2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1328181e-27e9-4a48-9191-a6dc0fa9b644/metallic-slider-02.png) ![Metallic value .3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/524f6c68-5d79-4bae-b5a4-41d5d18aea16/metallic-slider-03.png) ![Metallic value .4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e37c9c43-c5d6-4b15-8921-1544550a4e19/metallic-slider-04.png) ![Metallic value .5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bcc9d8c-03a0-4d83-a683-34a3df6ba423/metallic-slider-05.png) ![Metallic value .6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfafb4da-85dd-4dd9-8538-71f8ddd6b399/metallic-slider-06.png) ![Metallic value .7](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3941756a-8889-47df-bf39-ef5f567d03ad/metallic-slider-07.png) ![Metallic value .8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2620161c-c3e8-40f1-87bf-2ff4c498b678/metallic-slider-08.png) ![Metallic value .9](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31f07482-ef43-42ca-8a6e-c29a1ddfe0b7/metallic-slider-09.png) ![Metallic value 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7398d2a-9051-4be5-b0a0-54ca3a10cb7a/metallic-slider-10.png)

**Metallic values from 0 to 1.**

#### Mapping Metallic

Metals and nonmetals are often present in the same Material. Consider a metal panel, with a coat of paint covering some or all of the metal.

Paint is a nonmetal, so the Metallic value should be 0 in any regions covered by paint. Anywhere the metal panel is visible, the Metalic value should be 1.

This should be handled with a black and white mask passed into the Metallic input. Paint does not blend with metal, it sits on top of it. Your Metallic map should not contain intermediate grayscale values, only black and white. You could also use Material Layers to achieve similar results.

### Specular

The Specular input takes a value between 0 and 1, and controls how much specular light the surface reflects.

-   A Specular value of 0 is fully non-reflective.
-   A Specular value of 1 is fully reflective.

Unreal Engine uses a **default Specular of 0.5**, which represents approximately 4% specular reflection. This value is accurate for a vast majority of materials.

For very diffuse Materials, you may be inclined to set this to zero. Resist! All Materials have specular, see this post for examples [\[5\]](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine#hable).. The correct way to make very diffuse Materials is to use a high Roughness value.

### Cavity Maps

One reason to modify Specular is to add micro occlusion or small scale shadowing, say from cracks represented in the normal map. These are sometimes referred to as cavities. Small scale geometry, especially details only present in the high poly and baked into the normal map, will not be picked up by the renderer's real-time shadows.

To capture this shadowing, you can generate a cavity map, which is typically an AO map with very short trace distance. This is multiplied by the final BaseColor before output and multiplied with 0.5 (Specular default) as the Specular output.

To be clear this is BaseColor = Cavity*OldBaseColor, Specular = Cavity*0.5.

For advanced use, this can be used to control the index of refraction (IOR). We have not found this to be necessary for 99% of Materials. Below are Specular values based off of measured IOR.

**Measured Specular Values:**

| Material | Specular |
| --- | --- |
| Glass | 0.5 |
| Plastic | 0.5 |
| Quartz | 0.570 |
| Ice | 0.224 |
| Water | 0.255 |
| Milk | 0.277 |
| Skin | 0.35 |

          ![Specular value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2a47053-1c26-425e-9cfc-906c948b6756/spec-slider-00.png) ![Specular value .1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe83b14e-3ee1-45c6-ad03-8ce0789b8552/spec-slider-01.png) ![Specular value .2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd912a0b-e801-4c93-905d-d18e338a857d/spec-slider-02.png) ![Specular value .3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71d8fdde-6f9c-4ac9-b99a-6a5ebd368695/spec-slider-03.png) ![Specular value .4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d3ecd19-ce2d-4862-886e-ae707641e80c/spec-slider-04.png) ![Specular value .5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2cd14e0b-1642-4664-acd3-52bccf5b23f0/spec-slider-05.png) ![Specular value .6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4777a6e1-3564-4670-a5b4-22c5e060f429/spec-slider-06.png) ![Specular value .7](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f08c3be-d444-4e8c-80cd-a568b2e1e75d/spec-slider-07.png) ![Specular value .8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2023bc51-a9b7-4ed8-b08e-26cc01241774/spec-slider-08.png) ![Specular value .9](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/221379f8-65a2-4305-924d-f1f0ec98faed/spec-slider-09.png) ![Specular value 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbcecdb6-bd08-47cb-919e-e1abeab827d3/spec-slider-10.png)

**Specular values from 0 to 1**![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58ca76ab-10cd-410f-8b05-aeb754c190a3/measured_materials.png)

Example measured Materials. Top: Charcoal, fresh concrete, worn asphalt. Bottom: Copper, iron, gold, aluminum, silver, nickel, titanium

## References

**1**. Lagarde, [Feeding a physically based shading model](http://seblagarde.wordpress.com/2011/08/17/feeding-a-physical-based-lighting-mode/)

**2**. Karis, [Real Shading in Unreal Engine 4](https://de45xmedrsdbp.cloudfront.net/Resources/files/2013SiggraphPresentationsNotes-26915738.pdf)

**3**. Burley, [Physically-Based Shading at Disney](http://blog.selfshadow.com/publications/s2012-shading-course/burley/s2012_pbs_disney_brdf_slides_v2.pdf)

**4**. Smits, [Reflection Model Design for WALL-E and Up](http://blog.selfshadow.com/publications/s2012-shading-course/smits/s2012_pbs_pixar_model_slides_v2.pdf)

**5**. Hable, [Everything is Shiny](http://filmicworlds.com/blog/everything-is-shiny/)