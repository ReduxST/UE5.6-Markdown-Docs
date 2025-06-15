# Image Adjustment Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/image-adjustment-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/image-adjustment-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:48

---

The Image Adjustment functions exist as a way to perform basic color correction operations on textures. They are useful in that they allow corrective actions or variations on a texture without having to worry about the overhead of loading a separate version into memory.

## 3ColorBlend

The **3ColorBlend** function blends between 3 input colors based on a grayscale alpha, in the following manner:

![3 Color Blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fd3ea63-bde1-4ddf-ae51-707e2f95c536/3color-blend.png)

| Alpha Tone | Color |
| --- | --- |
| Dark Tones | Color A |
| Midtones | Color B |
| Highlights | Color C |

| Inputs | Description |
| --- | --- |
| **Color A (3Vector)** | This color will be applied wherever the alpha supplies dark tones to blacks. |
| **Color B (3Vector)** | This color will be applied wherever the alpha supplies midtones. |
| **Color C (3Vector)** | This color will be applied wherever the alpha supplies highlights to whites. |
| **Alpha (Scalar)** | This maps out where each color will be applied, as per above. |

## CheapContrast

The **CheapContrast** function boosts the contrast of an input by remapping the high end of the histogram to a lower value, and the low end of the histogram to a higher one. This is similar to applying a [Levels adjustment](http://www.cambridgeincolour.com/tutorials/levels.htm) in Photoshop, and pulling the black and white flags in a bit. The user may control the degree to which the contrast is boosted.

| Inputs | Description |
| --- | --- |
| **In (Scalar)** | The channel or black and white image having its contrast boosted. |
| **Contrast (Scalar)** | How much to boost contrast. 0 is default, or no change. |

This function takes in a scalar value rather than RGB, meaning it is particularly suited to black and white images or single channels. For contrast boost on full-color images, use *CheapContrast\_RGB*.

![Cheap Contrast](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0916637-77cb-461a-9745-634d3422aac2/cheap-contrast.png)

## CheapContrast\_RGB

The **CheapConstrast\_RGB** function boosts the contrast of an input by remapping the high end of the histogram to a lower value, and the low end of the histogram to a higher one. This is similar to applying a [Levels adjustment](http://www.cambridgeincolour.com/tutorials/levels.htm) in Photoshop, and pulling the black and white flags in a bit. The user may control the degree to which the contrast is boosted.

Unlike the regular *CheapContrast function*, this function can take in a Vector3 as the input, allowing it to perform contrast operations on a color image.

| Inputs | Description |
| --- | --- |
| **In (Scalar)** | The base image having its contrast boosted. |
| **Contrast (Scalar)** | How much to boost contrast. 0 is default, or no change. |

![Cheap Contrast RGB](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a4ec1c2-8bf6-4fdb-b6c8-51b7578e3fcd/cheap-contrast-rgb.png)

## SCurve

The **SCurve** function boosts contrast of an image by interpolating the values of each channel values of an image along an S-curve. This is similar to applying a [Curves adjustment](http://www.cambridgeincolour.com/tutorials/photoshop-curves.htm) in Photoshop and setting the RGB curve to an S-curve or using the Increase Contrast (RGB) preset.

| Inputs | Description |
| --- | --- |
| **In (Scalar)** | The base image having its contrast boosted. |
| **Power (Scalar)** | How much to boost contrast. 1 is default, or no change. |

   ![SCurve Power 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8bb6f0c-5c84-4e50-b92c-072b59496665/s-curve-0.png) ![SCurve Power 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41270b97-235a-4daf-a431-f4369e377f89/s-curve-05.png) ![SCurve Power 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb4d8941-addb-4837-9ad0-1b1c24e38ec4/s-curve-1.png) ![SCurve Power 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87633524-4559-4907-832e-17eaf2dfc5ff/s-curve-3.png)

**Examples of the SCurve Function with different Power values.**

## 3PointLevels

The **3PointLevels** function takes in an image and remaps the values of each channel across 3 points (white, black, middle). This is similar to applying a Levels adjustment in Photoshop. However, unlike the CheapContrast functions, this function provides full control in that it gives the user ability to adjust interpolation of lights, darks, and grays (gamma). By default, the three remapping points are interpolated linearly. However, you may input your own custom interpolation curve if you wish.

| Inputs | Description |
| --- | --- |
| **Texture (Scalar**) | The input texture. |
| **New Black Value (Scalar)** | Set the new value for the previous value of 0. |
| **New Middle Value (Scalar)** | Replaces the old value that matches the Middle Point input value. |
| **New White Value (Scalar)** | Set the new value for the previous value of 1. |
| **Middle Point (Scalar)** | Pick a value from the input image that will get replaced with the value from Middle Point. |
| **Define Interpolation Curve (StaticBool)** | Set to *true* if you want to define your own interpolation curve using the Interpolation Power input. |
| **Interpolation Power (Scalar)** | A power node applied to the interpolation. This controls the interpolation between the three points (black, white, and middle). |
| **Invert Interpolation Power** | Set to *true* if you want to invert the power curve (this generally lowers contrast instead of boosting it). |

![3Point Levels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24d3fa9d-fabf-454e-bf3e-ec7aec146fb0/3point-levels.png)

The "-------------" inputs of this node are merely separators in the list of inputs for sake of clarity. They are not intended to receive actual connections.

Like the CheapContrast function, this node takes in a scalar by default, meaning it is suited for single channels or black and white images.

## HueShift

The **HueShift** function offsets the current hue value of an input color by a given percentage. This percentage is 1-based and centered around the color wheel. For instance, a shift of 0.5 (50%) will shift to a complimentary hue, or the hue on the opposite side of the color wheel. A shift of 1.0 (100%) gives no change, as this is the equivalent of rotating completely around the color wheel.

| Inputs | Description |
| --- | --- |
| **Hue Shift Percentage (Scalar)** | How far around the color wheel to shift the incoming hue. |
| **Texture (Vector3)** | The incoming texture having its hue shifted. |

![Hue Shift](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb9e4152-c65f-46d0-a287-88362191f28a/hue-shift.png)

## SmoothThreshold

The **SmoothThreshold** function takes in a gradient, an interpolation rate, and a threshold value (Cutoff Value). It then applies a smooth contrast to the gradient, based on the inputs. Here is a breakdown of what each input does:

| Inputs | Description |
| --- | --- |
| **Cutoff Value** | Gradient input values that fall below the cutoff value will be affected by the operation. |
| **Lerp Value** | Add a negative or positive number to smoothly ramp to from the original values. Ramping occurs in values lower than the cutoff value. |
| **Gradient** | This value serves as the base for the contrast operation. |

![Smooth Threshold](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/481f1418-aedc-4080-aaf4-c508a7695966/smooth-threshold.png)