# Bloom

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/bloom-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/bloom-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:19

---

**Bloom** is a real world light phenomena that can greatly add to the perceived realism of a rendered image at a moderate render performance cost. Bloom can be seen by the naked eye when looking at very bright objects that are on a much darker background. Even brighter objects also cause other effects (streaks, lens flares), but those are not covered by the classic bloom effect. Because our displays (TV, TFT, etc.) usually do not support HDR (high dynamic range), we cannot really render very bright objects. Instead we simulate the effects that happen in the eye (retina subsurface scattering), when light hits the film (film subsurface scattering), or in front of the camera (milky glass filter). The effect might not always be physically correct but it can help to hint the relative brightness of objects or add realism to the LDR (low dynamic range) image that is shown on the screen.

![Bloom Effect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6341888d-0b4c-4761-b121-c89809b49f38/bloom.png)

Bloom can be implemented with a single Gaussian blur. For better quality, we combine multiple Gaussian blurs with different radius. For better performance, we do the very wide blurs in much lower resolution. In UE3, we had 3 Gaussian blurs in the resolution 1/4, 1/8, and 1/16. We now have multiple blurs name Blur1 to 5 in the resolution 1/2 (Blur1) to 1/32 (Blur5).

We combine the blurs differently to get more control and higher quality. For best performance, the high resolution blurs (small number) should be small and wide blurs should mostly make use of the low resolution blurs (large number).

| Property | Description |
| --- | --- |
| **Intensity** | Scales the color of the whole bloom effect (linear). Possible uses: fade in or out over time, darken. See the [examples below](/documentation/en-us/unreal-engine/bloom-in-unreal-engine#intensity). |
| **Threshold** | Defines how many luminance units a color needs to have to affect bloom. In addition to the threshold, there is a linear part (one unit wide) where the color only partly affects the bloom. To have all scene colors contributing to the bloom, a volume of -1 needs to be used. Possible uses: tweak for some not real HDR content, dream sequence. See the [examples below](/documentation/en-us/unreal-engine/bloom-in-unreal-engine#threshold). |
| **#1#2#3#4#5 Tint** | Modifies the brightness and color of each bloom. Using a black color will not make this pass faster but that can be done. |
| **#1#2#3#4#5 Size** | The size in percent of the screen width. Is clamped by some number. If you need a larger number, use the next lower resolution blur instead (higher number). See the [examples below](/documentation/en-us/unreal-engine/bloom-in-unreal-engine#size). |

#### Intensity

|   |   |   |
| --- | --- | --- |
| ![Bloom Intensity - 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74421aa6-bf33-4573-933d-d144919bab90/bloom_intensity_0_small.png) | ![Bloom Intensity - 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd5f548c-8546-42c4-8290-86d2528b28bd/bloom_intensity_1_small.png) | ![Bloom Intensity - 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b555dc1-51d7-4a7b-bb9e-f7ecc8cc3a36/bloom_intensity_5_small.png) |
| 0.0 | 1.0 | 5.0 |

#### Threshold

![Threshold - 0.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8697c12a-627c-47b5-9127-7d2b08f91edf/bloom_threshold_0_small.png)

![Threshold - 10.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fa084a3-688a-4fd6-bf17-ed6bdc211087/bloom_threshold_10_small.png)

#### Size

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
| ![Bloom Tint 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26d99971-43d5-4514-bd11-e05e39fb7b8a/bloom_tint_1_small.png) | ![Bloom Tint 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6147c8da-48f4-4ad7-8b4b-b38229bcecbe/bloom_tint_2_small.png) | ![Bloom Tint 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f82bbef0-b47b-4fd8-bbf6-6910f3352f26/bloom_tint_3_small.png) | ![Bloom Tint 4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c6e0e67-ccf9-44a8-b049-c97b51bb5b95/bloom_tint_4_small.png) | ![Bloom Tint 5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f4be4ef-f344-4f77-9829-265a4e0ad25a/bloom_tint_5_small.png) |
| #1 | #2 | #3 | #4 | #5 |

## Bloom Convolution

The Bloom **Convolution** effect enables you to add custom bloom kernel shapes with a texture that represent physically realistic bloom effects whereby the scattering and diffraction of light within the camera or eye that give rise to bloom is modeled by a mathematical convolution of a source image with a kernel image.

![Convolution for Bloom: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1507851b-c586-4c10-8f5c-fe81d233cf11/fftbloom_enabled.png)

![Convolution for Bloom: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4dd0a23c-bc00-418e-9ba7-2ddfda1abd58/fftbloom_disabled.png)

In this example, the bloom technique produces a continuum of responses ranging from star-like bursts to diffuse glowing regions.

The kernel represents the response of the optical device to a single point source in the center of the viewing field. Each pixel in the source contributes some of its brightness to neighbors as prescribed by the kernel image. The brighter the source pixel the more visible the bloom it produces. Under the hood this energy conserving scatter is formulated as a convolution operations and accelerated by use of a Fast Fourier Transform (FFT).

Bloom Convolution is designed for use with with in-game or offline cinematics or on high-end hardware, while the ***Standard* bloom should be used for most game applications**. In assessing the trade off, the *Standard* bloom has a significant performance advantage but it is not conservative (it can result in an overall brightening of the image) and it lacks the visual complexity of the Bloom Convolution.

To enable Bloom Convolution, navigate to the **Lens** section of the Post Process Volume and next to **Method** use the selection box to choose **Convolution**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df3e1788-9243-475f-8b53-46bbe4d601b5/convolution-bloom-settings.png)

| Property | Description |
| --- | --- |
| **Convolution Kernel** | Use this to select the texture that defines the kernel. |
| Advanced Properties |   |
| **Convolution Scale** | This indicates the relative size of the Convolution Kernel image in units of the viewport, defaults to 1. Primarily used to decrease the size of the bloom. |
| **Convolution Center** | In UV coordinates, defaults to (1/2, 1/2). Ideally the Convolution Kernel image is a perfectly centered response to a brighter source, but generally small tweaks will be required. Offsets here will result in full offsets of the bloom image. |
| **Convolution Boost** | Boosts the intensity of select pixels prior to applying the convolution bloom filter. This consists of a minimum value, a maximum value and a multiplier. The brightness delta above the minimum value will be amplified by the multiplier. By default this boost is disabled and should be used with caution. |
| **Convolution Buffer** | Implicit buffer region as a fraction of screen size to insure the bloom does not wrap around the image. Increasing this value has adverse performance impact. |

### Kernel Image Best Practices

The additional realism generated by the image-based convolution is the result of its ability to use a visually interesting, non-symmetric kernel images. When creating your kernel images and setting them up for use with Bloom Convolution, there are a few things that you should keep in mind.

-   The kernel image should be fully present on the GPU and available at full resolution, otherwise a low resolution version of the kernel may be used and will result in serious degradation of quality. To do this, set the following properties in the Texture Editor for the kernel image:
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e6c759b-a5ff-433a-9530-ad84f3c17e40/convolution-bloom-texture-properties.png) | 
    -   Mips Gen Setting: **No Mipmaps**
    -   Never Stream: **Enabled**
    
    
    
     |
    
-   Bloom is a whole image filter, so with Convolution Bloom the hottest part of the image should be the considerably brighter than the rest of the image (.exr format works well for this), otherwise the filter will have a strong blurring effect over the screen.
-   The system expects the hottest point to be at the center of your kernel image, however, this can be adjusted by using the **Convolution Center** controls.
-   A good bloom kernel structure should fill most of the kernel image. If you look at the default kernel image in Photoshop, you'll see that the radial lines that diverge from the center spread out for a considerable amount of the image.
    
    ![Kernel Image unaltered](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/745cdbf6-0ada-4ed4-be72-58f71406e620/kernelimage1.png)
    
    ![Kernel Image adjusted for demonstration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90606ce0-0ec3-4bf5-81ce-1baf9ba64338/kernelimage2.png)
    
-   Large changes in the Convolution behavior should be done by changing the kernel image with minor tweaks done using the Bloom Convolution Advanced properties.

## Bloom Dirt Mask

The **Bloom Dirt Mask** effect uses a texture to brighten up the bloom in some defined screen areas. This can be used to create a war camera look, more impressive HDR effect, or camera imperfections.

![Dirt Mask Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73529909-cbca-430d-8a13-8c1f0c67088a/dirtmaskenabled.png)

![Dirt Mask Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0facf1c2-4014-4328-9c28-22fa668a466a/dirtmaskdisabled.png)

To enable Bloom Dirt Mask, navigate to the **Lens** section of the Post Process Volume and enable the option for **Dirt Mask Texture**. Use the Texture selection to apply the texture for your Dirt Mask.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/775394e6-4078-40d2-a85f-e47b13ce90be/dirt-mask-properties.png)

| Property | Description |
| --- | --- |
| **Dirt Mask Texture** | Use the selection box to assign a Texture2D to be used for your Dirt Mask. Keep in mind that this property cannot be blended with other Post Process Volumes. |
| **Dirt Mask Intensity** | Scales the color of the bloom dirt mask effect (linear). This property is used to tweak dirt mask brightness. |
| **Dirt Mask Tint Color** | Used to darken or color tint the dirt mask texture. This can be used to tweak the dirt mask brightness and color. |

### Dirt Mask Image Best Practices

When creating your Dirt Mask textures and setting them up for use with Bloom Dirt Mask, there are a few things you should keep in mind.

-   The texture should be fully present on the GPU and available at the full resolution. To do this, set the following property in the Texture Editor:
    
    |   |   |
    | --- | --- |
    | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5507a06a-d061-4424-bdf3-ff6159e06aa4/dirt-mask-texture-properties.png) | 
    -   Mips Gen Setting: **No Mipmaps**
    -   Never Stream: **Enabled**
    
    
    
     |
    
-   This Post Process property cannot be blended with other Post Process Volumes in your level.
-   When constructing your Dirt Mask Texture, keep the following in mind:
    
    Example Dirt Mask Texture used in Vehicle Game.
    
    -   It is recommended to use a non-power of two image size. This avoids Mip creation and streaming, so these should be set automatically, however, if you use a power of two texture size, you'll need to set these in the Texture Editor properties.
    -   You can use a low-resolution texture as this is usually sufficient to represent dirt or scratches on the camera and these are likely to be out of focus and blurry anyway. If you're getting compression artifacts you can try a higher resolution image.
    -   You can create the texture using Photoshop (or similar image editing software) using Lens blur.
    -   Use chromatic aberration (color fringe), in the texture, to help improve the look of the dirt mask.

## Training Streams