# Font Materials and Outlines

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/font-materials-and-outlines-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/font-materials-and-outlines-in-unreal-engine)  
**Processed:** 2025-06-14 16:24:10

---

In addition to being able to set a **Color and Opacity** for your **Font** in UMG, you can also use Materials and font outlines for additional **Font** styling.

## Font Colors

You can set the **Vertex Color** for your **Font** by setting its **Color and Opacity**.

![Set the Font Color and Opacity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffd8649b-1851-432d-b765-2adbd07ead6d/ue5_1-01-set-color.png "Set the Font Color and Opacity")

Without a **Font Material** specified, this will apply a solid color to your text.

![Example of the Font Block without a Font Material specified](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdb47391-a20a-4fed-8fd9-8cff30768e34/ue5_1-02-example-text-block-1.png "Example of the Font Block without a Font Material specified")

## Font Materials

You can specify a **Font Material** for your **Font** in the **Details** panel.

![Set Font Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2750c90d-cc73-4762-bb50-cfaaf98f5334/ue5_1-03-set-font-material.png "Set Font Material")

If your **Font Material** doesn't have a **Vertex Color** node, the effect is like a simple multiplication.

|   |   |   |
| --- | --- | --- |
| 
 | ![Base Color material preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cfc9555-2509-4eef-9921-e6f847dde6f0/ue5_1-05-preview-1.png) | ![Example of the Font Block with a Base Color node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c61c6af6-2872-4b46-95df-064d897ce160/ue5_1-06-example-text-block-2a.png) |
| Font Material Setup | Font Material Preview | Final Font |

However, if you place a **Vertex Color** node in your **Font Material**, you can use its outputs to do math within your shader.

|   |   |   |
| --- | --- | --- |
| 
 | ![Vertex Red Color material preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7163f95a-008d-47d2-ae34-51cb8bc7ce28/ue5_1-08-preview-2.png) | ![Example of the Font Block with a Vertex Red Color node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be43b5be-aea6-4314-8e0a-c80baf062b4f/ue5_1-09-example-text-block-2b.png) |
| Font Material Setup | Font Material Preview | Final Font |

Materials used as font materials must be in the **User Interface** domain.

![Set Material Domain to UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/499215a1-3adb-4bed-9618-5bdd20d25749/ue5_1-10-set-domain.png "Set Material Domain to UI")

## Font Outlines

You can specify a different **Outline Color** as well as a different Material to use for a font outline.

![Set the Font Outline Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd8bf273-1d73-40ac-8f46-65b0480e854c/ue5_1-11-outline-settings.png "Set the Font Outline Settings")

The size of the outline is specified in Slate units, but when the font's scale is 1.0, 1 Slate unit is equivalent to 1 pixel.

![Example of the Font Block with Outline](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45fd7ffa-a12e-4891-8c18-1c1a62bb6ce9/ue5_1-12-example-text-block-3.png "Example of the Font Block with Outline")

One interesting note is that you can specify whether or not to use **Separate Fill Alpha**.

![Separate Fill Alpha option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23bb7b46-aa4e-434a-a98d-53c33600ddc0/ue5_1-13-separate-fill-alpha.png "Separate Fill Alpha option")

When this is enabled, the outline is translucent where the filled area will be, allowing you to adjust the alphas of the font and the font outline independently. When it is disabled, the font is overlaid on the outline, so the alphas are additive and the outline color and Material is visible through a font with an alpha less than 1.

![Font Color Alpha = 0.5, Separate Fill Alpha disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6ff0d9a-ce4f-48bf-9947-31a13b64acb2/ue5_1-14-separate-fill-alpha-disable.png)

![Font Color Alpha = 0.5, Separate Fill Alpha enable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a57d1d5-b9a8-4a3b-882c-b6b9f051a9d5/ue5_1-15-separate-fill-alpha-enable.png)