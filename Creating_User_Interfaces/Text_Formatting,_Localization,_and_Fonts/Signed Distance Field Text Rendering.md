# Signed Distance Field Text Rendering

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-signed-distance-field-text-rendering-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-signed-distance-field-text-rendering-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:52

---

In Unreal Engine (UE) 5.5 and newer, you can use **signed distance field-based text rendering** for any UI (user interface) text. This includes **conventional signed distance fields** and **multi-channel signed distance fields (MSDF)**, which preserve sharp corners.

A signed distance field is a resolution-independent approximate representation of individual font glyphs stored in texture memory, which can be shaded to output the anti-aliased alpha mask of a glyph. Additionally, it can provide the signed distance to a material shader, which it can use for graphical effects. A signed distance is the distance to the closest edge point, with the sign specifying whether the origin point is inside (positive) or outside (negative).

![Signed Distance Field-based Text Render](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58d08abf-0c1e-4ea3-88ef-43c2678597fd/sdf-text-render.png)

A signed distance field-based text render on the left, and the actual texture with the signed distance field on the right.

The distance field mode does not replace the previous text rendering pipeline but is offered as an alternative since it has pros and cons.

## Pros

-   Resolution independence means that a separate texture representation won't be needed for each glyph size (and also skew, outline size), potentially saving texture memory and performance.
-   Very large text can be rendered from a low resolution distance field at good quality, saving texture memory.
-   Using text outlines is significantly more efficient with distance fields, and doesn't require additional texture memory.
-   Enables distance-based material effects, such as outlines, glows, growth animations, and more.

## Cons

-   Computing distance fields is more computationally intensive than direct rasterization.
-   As a resolution-independent technique, it does not support hinting. This can negatively affect quality at small font sizes.
-   Distance fields are an approximation. Depending on their resolution, they may only be able to reproduce some glyph features with sufficient fidelity. Thin font faces and thin, delicate features, in general, are the most problematic. Consider if the font face you use suits distance field rendering.
-   The initial version does not support font faces with non-standard geometry.

We recommend you enable the distance field mode for very large or dynamically scaled text when using the same font face at a large number of different sizes or to take advantage of the signed distance in a material effect.

## Setup and Use

To get setup, follow these steps:

1.  Open **Project Settings > Engine > User Interface > UMG Fonts**.
    
2.  Enable the **Enable Distance Field Font Rasterization** setting.
    
    ![ Enable Distance Field Font Rasterization setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70752605-f4f8-4eb6-a1a8-a4708f632928/enable-distance-field-font-rasterization.png)
3.  Open the font face asset you want to use distance field text rendering for.
    
4.  In the **Details** panel, locate the **Distance Field Mode** category, then enable the **Enable Distance Field Rendering** setting. When you enable the setting you can configure the quality levels for the single and multi-channel distance field resolution.
    
    ![Enable Distance Field Rendering setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7ab6bf5-2aa4-49f5-a604-2f5e3b5183ed/enable-distance-field-rendering-setting.png)

## Configuration

When you enable this rendering mode, you can set the single-channel and multi-channel distance field resolutions for low, medium, and high quality levels. These resolutions are expressed in distance field pixels per "em" (em is a font face metric approximately representing the width of the letter "M").

You are able to preview the rendering output for all of the resolutions and both distance field types, as well as the "reference" appearance rasterized directly from vector geometry. Make sure that all quality levels are of acceptable quality for all relevant glyphs. Make sure to check potentially problematic glyphs which may contain thin or small features. As a rule of thumb, the distance field resolution should be high enough that at least one whole distance field pixel fits into each such small feature.

The distance field type (multi-channel, single-channel, and approximate) and used quality level is dictated by [device profiles](/documentation/en-us/unreal-engine/setting-up-device-profiles-in-unreal-engine), where it can be specified per-device. Set the following CVars in the device profile to customize which rasterization mode and quality level is used.

| **CVar** | **Description** |
| --- | --- |
| `UI.SlateSDFText.RasterizationMode` | Rasterization mode or distance field type. |
| `UI.SlateSDFText.ResolutionLevel` | Distance field resolution quality level. Values are 1 (low), 2 (medium), and 3 (high-quality). |

The following are valid values for `UI.SlateSDFText.RasterizationMode`.

| **Value** | **Description** |
| --- | --- |
| **Bitmap** | Direct rasterization. This disables distance field rendering for the given device. |
| **Msdf** | Multi-channel signed distance field rendering. Uses one of the multi-channel resolutions. |
| **Sdf** | Conventional single-channel signed distance field rendering. Corners may appear rounded or chipped, mitered outlines won't be available. |
| **SdfApproximation** | A less precise version of Sdf. This provides similar quality but at a significantly lower performance cost. Recommended for less powerful devices, such as mobile phones. |

You may also override the rasterization modes for a specific font face in that font asset's settings in the Unreal Editor.

## Material effects

For utilizing font signed distance in a material effect, you can use the new **Font Signed Distance** material node.

![Material Effect Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5661230-e795-444a-ad83-3c50de81f45e/material-effects.png)

Currently, the node has no inputs, and samples the text's signed distance at the current pixel. It provides the following outputs.

| **Output** | **Description** |
| --- | --- |
| **Signed Distance** | The primary signed distance, expressed in "em"s. It is negative outside the glyphs and positive inside. When using a multi-channel signed distance field, this will be the perpendicular distance, which forms sharp rather than rounded miters around corners. |
| **Smooth Signed Distance** | The Euclidean signed distance, expressed in "em"s. Where negative represents the outside and positive inside. If a single-channel distance field is used, this value is the same as the primary Signed Distance. |
| **Pixel Distance Factor** | Value that can be used to convert the above signed distances from "em"s to screen pixels by multiplying them together. This can be typically used for anti-aliasing, by smoothly transitioning between two colors between `threshold distance - 0.5 px` and `threshold distance + 0.5 px`. |
| **Implicit Opacity** | The implicit opacity of the text when the signed distance is interpreted the same way as when rendering without a material. This can be used as a basis before additional effects are added. |

The distance fields only provide a limited range of signed distances in and around the font glyphs. If your material effect requires distances further away from the glyph, you can force a distance field with a wider distance range by setting an outline for the text with a width similar to that of your effect.

By default, only the interior area of text is filled by the material. If your effect needs to draw around the text (for example, a glow effect), you should enable the new option **Material Is Stencil** in the text. When you enable the option, entire glyph quads are filled with the material, and your material needs to correctly set the opacity to stencil the glyph shapes. You can use the **Implicit Opacity** as described above, or you can do it in a custom way using the signed distances.

![Font Matrial](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f0b24a4-309a-43b0-b9d2-ef20a04d973d/font-matrial.png)