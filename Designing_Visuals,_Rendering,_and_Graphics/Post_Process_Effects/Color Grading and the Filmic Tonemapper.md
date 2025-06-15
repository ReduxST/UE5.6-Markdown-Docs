# Color Grading and the Filmic Tonemapper

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:08

---

Within the Unreal Engine, the term **Color Grading** covers the Tone Mapping function (HDR to LDR transformation) that is used with [High Dynamic Range (HDR) display output](/documentation/en-us/unreal-engine/high-dynamic-range-display-output-in-unreal-engine) and further the color correction (LDR color to screen color transformation) processing of the image.

## Tone Mapping

The purpose of the **Tone Mapping** function is to map the wide range of high dynamic range (HDR) colors into low dynamic range (LDR) that a display can output. This is the last stage of post processing that is done after the normal rendering during post processing. The process of tone mapping can be thought of as a way to simulate the response that film has to light.

### Academy Color Encoding System (ACES) Filmic Tonemapper

The Filmic tonemapper that is used with Unreal Engine matches the industry standard set by the [Academy Color Encoding System (ACES)](http://www.oscars.org/science-technology/sci-tech-projects/aces) for television and film. This ensures that consistent color is preserved across multiple formats and displays while also as a way to future proof the source material since it will not have to be adjusted for each medium that comes along. The filmic tonemapper also uses the same global tonemapper that was previously used in Unreal Engine, with the exception that there is now a filmic response meaning that the S-curve shape now better simulates film stock for a better overall look.

Two places you'll immediately notice a difference is with Bloom and Exposure Levels.

#### Physically Correct Emissive and Bloom

Emissive values are now physically correct so that as the emissive power increases the color will become lighter, similarly to how colored lights work in the real world. As color gets tone mapped, if the final color is bright enough to start saturating the film / sensor, it will become white.

![Filmic Tonemapper | Emissive](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b79639b6-1088-4c5c-af35-f7a04317cef4/bloom_filmictonemapper.png)

![Legacy Tonemapper | Emissive](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5066d3bd-f742-47bb-bdc1-4f29e1302099/bloom_oldtonemapper.png)

In this example, the legacy tonemapper is compared to the new filmic tonemapper. With a high enough emissive power, the color will start to become white, unlike the legacy tonemapper where values would just become overly saturated causing areas of the material to lose its detail. With the filmic tonemapper, you can even see that the Bloom in this scene retains its physical correctness as well as it is never overly saturated, thus retaining it's reflective primary color value.

#### Exposure Levels

Exposure levels are physically correct so that colors will continue to have shape to them rather than lose detail.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd398058-3152-4150-9312-b2e474cf06d6/exposure_default.png)

In this example, there are a variety of colors and material types with varying roughness and metalness. The Exposure Bias is also set to 0.

![Filmic Tonemapper | Exposure Bias: 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27d38f5c-acb0-4af1-8d8a-c847034a3ffb/exposure_filmictonemapper.png)

![Legacy Tonemapper | Exposure Bias: 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bd015de-95f8-488c-be01-461a957a024f/exposure_oldtonemapper.png)

In this comparison, the Exposure Bias has been increased to a value of 3 so really show the response of the Filmic tonemapper compared to the legacy tonemapper implementation. Also, a value of three means that the processed image will be eight times brighter than the default value of 0 shown in the previous example above.

As the exposure level is increased, the difference between the filmic and the legacy tonemapper will become more apparent. The spheres in the filmic example will continue to have shape to their color and shading, even as they appear to look brighter. The sphere using the legacy tonemapper will start to have their colors blend with the shading. The spheres become really bright as a solid color, but you can't necessarily tell that they have a high exposure value, whereas the filmic tonemapper takes this into account. The filmic response looks like a natural camera effect if you were to increase its exposure.

### Film Settings

In the **Film** section of the Post Process Volume enables you to tonemap your scene using properties that match the ACES standardized film stock. You can adjust these controls to emulate other types of film stock for your project.

It is recommended that changes to these properties be used project-wide for a specific look and not changed dynamically or on a shot-by-shot basis. Instead, you should use the [Color Grading](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorcorrectionproperties) properties for any artistic adjustments.

![Filmic tonemapper properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/912196c2-fcce-488c-9d83-6371cd99f237/5_1_tone-mappper-properties.png)

-   **Slope:** This will adjust the steepness of the S-curve used for the tonemapper, where larger values will make the slope steeper (darker) and lower values will make the slope less steep (lighter). Value is in the range of \[0.0, 1.0\]. \[0.0, 1.0\].\*
    
    ![Slope: 0.88 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a73e6d6e-0e8f-48cf-a6c5-6f00fb908c37/defaultsettings_filmictonemapper.png)
    
    ![Slope: 0.6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3a8a2ca-c830-4146-a595-42ed6a9f7cc6/slope_0_6.png)
    
    ![Slope: 0.88 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca693ebf-d43b-48fc-8a71-abcfddfa603f/defaulttonemapper.png)
    
    ![Slope: 0.6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f260469b-e6d4-42e0-9ae1-49fd14e15696/slopetonemap.png)
    
-   **Toe:** This will adjust the dark color in the tonemapper. Value is in the range of \[0.0, 1.0\]. \[0.0, 1.0\].
    
    ![Toe: 0.55 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e1a9cb8-dccf-440e-93ba-39489aaa3855/defaultsettings_filmictonemapper.png)
    
    ![Toe: 0.8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b97463d-96f7-4811-895b-dba00e9043d4/toe_0_8.png)
    
    ![Toe: 0.55 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0a37ce0-9cac-4a48-8040-a650d77c793f/defaulttonemapper.png)
    
    ![Toe: 0.8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/304f1f46-985e-4d70-9b88-1b658a78d215/toetonemap.png)
    
-   **Shoulder:** This will adjust the bright color in the tonemapper. Value is in the range of \[0.0, 1.0\]
    
    ![Shoulder: 0.26 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8f579e0-dc87-4fa4-a6b7-21452a264f56/defaultsettings_filmictonemapper.png)
    
    ![Shoulder: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/329d1ee3-9982-4c46-835b-c933aa25be98/shoulder_1.png)
    
    ![Shoulder: 0.26 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7359234-716f-464d-afc3-dbc42f2b1c38/defaulttonemapper.png)
    
    ![Shoulder: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68e14341-78aa-4505-b977-bd97375b2dbe/shouldertonemap.png)
    
-   **Black Clip:** This will set where the crossover happens where black's start to cut off their value. In general, this value should **not** be adjusted. Value is in the range of \[0.0, 1.0\]
    
    ![Black Clip: 0 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/218b9ca4-ad8c-4558-9ad0-1f4b7c408db4/defaultsettings_filmictonemapper.png)
    
    ![Black Clip: 0.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56090857-3c8d-4d79-a2b9-7b4db625c629/blackclip_0_1.png)
    
    ![Black Clip: 0 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6b6e2ea-7dff-4233-9476-d407b1845061/defaulttonemapper.png)
    
    ![Black Clip: 0.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd26d1c6-dac9-4951-9712-7aad4e944837/blackcliptonemap.png)
    
-   **White Clip:** This will set where the crossover happens where white's start to cut off their values. This will appear as a subtle change in most cases. Value is in the range of \[0.0, 1.0\]
    
    ![White Clip: 0.04 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9893dc67-f392-4d88-97a0-eaf1b371baa2/defaultsettings_filmictonemapper.png)
    
    ![White Clip: 0.2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4eb46219-4624-4071-aaf6-a0bf35fa988d/whiteclip_0_2.png)
    
    ![White Clip: 0.04 (Default)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b57a4e8-794f-41ee-8a3b-0148c20d9cda/defaulttonemapper.png)
    
    ![White Clip: 0.2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c8d988b-0be0-46bc-8cd4-b8e2923f3ffd/whitecliptonemap.png)
    

If you'd like to test different tonemapper values in a real-time graph like the ones above, you can use the default [UE4 Tonemapper example](https://www.desmos.com/calculator/h8rbdpawxj) here.

## Color Correction

Color correction, or color grading, is used to alter or enhance the overall color of light in your scene. With the advent of HDR displays, the need to preserve color before it's processed is very important. It ensures that the color will be properly displayed.

In the past, the color correction would have been implemented through [Lookup Tables (LUTs)](/documentation/en-us/unreal-engine/using-lookup-tables-for-color-grading-in-unreal-engine), which happens in LDR and on the final color that was output to the monitor in sRGB color space. This presents a problem when working with HDR displays because the LUT is just a snapshot in time of the currently supported display it is being adjusted for and cannot be used to the same effect on an HDR display. To solve these types of issues, the [color correction controls](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorcorrectionproperties) do their work in Scene Referred Linear Space, which means all colors are captured before they are tone mapped. This makes it possible to only adjust your colors on one HDR display for any color correction to look correct on all displays the image is being outputted to, whether they are HDR or LDR.

You can learn more about the HDR pipeline and how this works for the benefit of your content in the [High Dynamic Range Display Output](/documentation/en-us/unreal-engine/high-dynamic-range-display-output-in-unreal-engine) page.

### Color Correction Properties

In the **Color Grading** section of the Post Process Volume, you'll find the properties that enable you to have the most artistic control over the scene.

#### Settings

|   |   |
| --- | --- |
| ![RGB color wheel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46a0eaf9-e812-4766-8294-23a26f8e09a2/5_1_rgb-color-wheel.png) | ![HSV color wheel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c32ab56-9a28-4eca-8455-b4fafb4ede83/5_1_hsv-color-wheel.png) |
| RGB | HSV |

Under each section, you can use the color wheel to select and drag the color values around. You also can choose between the following modes:

-   RGB - This will adjust the Red, Green, Blue values.
-   HSV - This will adjust the Hue and Saturation values.

For more precise control over the slider values, you can hold the **Shift** key while dragging them.

![Color Grading properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fd5d27f-c8a4-417e-8813-60c78f2719f8/5_1_color-grading-properties.png)

| Property | Description |
| --- | --- |
| Temperature | The properties in this section are used to adjust the colors in the scene so that whites appear truly white. This allows for other colors in the scene to be correctly lit under the given lighting in the scene. |
| **Temperature Type** | 
Select a type of temperature calculation to use.

-   **White Balance**: Uses the Temperature value to control the virtual camera's White Balance. This is set by default.
-   **Color Temperature**: Uses the Temperature value to adjust the color temperature of the scene, which is the inverse of the White Balance operation.



 |
| **Temp** | This will adjust the white balance in relation to the temperature of the light in the scene. When the light temperature and this one match the light will appear white. When a value is used that is higher than the light in the scene it will yield a "warm" or yellow color, and, conversely, if the value is lower, it would yield a "cool" or blue color. |
| **Tint** | This will adjust the white balance temperature tint for the scene by adjusting the cyan and magenta color ranges. Ideally, this setting should be used once you've adjusted the white balance **Temp** property to get accurate colors. Under some light temperatures, the colors may appear to be more yellow or blue. This can be used to balance the resulting color to look more natural. |
| Global | The properties in this section are a global set of color corrections you can use for your scene. |
| **Saturation** | This will adjust the intensity (purity) of the colors (hue) that are being represented. A higher saturation intensity will result in colors appearing more like their purest forms (red, green, blue) and when saturation is lowered colors will appear more gray or washed-out. |
| **Contrast** | This will adjust the tonal range of light and dark color values in your scene. Lowering the intensity will remove highlights and lighten the image resulting in a washed-out appearance, whereas a higher intensity will tighten the highlights and darken the overall image. |
| **Gamma** | This will adjust the luminance intensity of the image's mid-tones to accurately reproduce colors. Lowering or raising this value will result in the image being washed-out or too dark. |
| **Gain** | This will adjust the luminance intensity of the image's whites (highlights) to accurately reproduce colors. Raising or lowering this value will result in the image highlights being washed-out or too dark. |
| **Offset** | This will adjust the luminance intensity of the image's blacks (shadows) to accurately reproduce colors. Raising or lowering this value will result in the image shadows being washed-out or too dark. |
| Shadows | The properties in this section are used to adjust the color correction values for shadows in the scene. |
| **Saturation** | This will adjust the intensity (purity) of the colors (hue) that are being represented. A higher saturation intensity will result in colors appearing more like their purest forms (red, green, blue) and when saturation is lowered colors will appear more gray or washed-out. |
| **Contrast** | This will adjust the tonal range of light and dark color values in your scene. Lowering the intensity will remove highlights and lighten the image resulting in a washed-out appearance, whereas a higher intensity will tighten the highlights and darken the overall image. |
| **Gamma** | This will adjust the luminance intensity of the image to accurately reproduce colors. Raising or lowering this value will result in the image mid-tones being washed-out or too dark. |
| **Gain** | This will adjust the luminance intensity of the image's whites (highlights) to accurately reproduce colors. Raising or lowering this value will result in the image highlights being washed-out or too dark. |
| **Offset** | This will adjust the luminance intensity of the image's blacks (shadows) to accurately reproduce colors. Raising or lowering this value will result in the image shadows being washed-out or too dark. |
| **Shadows Max** | This is a multiplier of the properties that affect the color correction properties that have been adjusted in the **Shadows** section. |
| Mid-tones | The properties in this section are used to adjust the color correction values for mid-tones in the scene. |
| **Saturation** | This will adjust the intensity (purity) of the colors (hue) that are being represented. A higher saturation intensity will result in colors appearing more like their purest forms (red, green, blue) and when saturation is lowered colors will appear more gray or washed-out. |
| **Contrast** | This will adjust the tonal range of light and dark color values in your scene. Lowering the intensity will remove highlights and lighten the image resulting in a washed-out appearance, whereas a higher intensity will tighten the highlights and darken the overall image. |
| **Gamma** | This will adjust the luminance intensity of the image to accurately reproduce colors. Raising or lowering this value will result in the image mid-tones being washed-out or too dark. |
| **Gain** | This will adjust the luminance intensity of the image's whites (highlights) to accurately reproduce colors. Raising or lowering this value will result in the image highlights being washed-out or too dark. |
| **Offset** | This will adjust the luminance intensity of the image's blacks (shadows) to accurately reproduce colors. Raising or lowering this value will result in the image shadows being washed-out or too dark. |
| Highlights | The properties in this section are used to adjust the color correction values for Highlights in the scene. |
| **Saturation** | This will adjust the intensity (purity) of the colors (hue) that are being represented. A higher saturation intensity will result in colors appearing more like their purest forms (red, green, blue) and when saturation is lowered colors will appear more gray or washed-out. |
| **Contrast** | This will adjust the tonal range of light and dark color values in your scene. Lowering the intensity will remove highlights and lighten the image resulting in a washed-out appearance, whereas a higher intensity will tighten the highlights and darken the overall image. |
| **Gamma** | This will adjust the luminance intensity of the image to accurately reproduce colors. Raising or lowering this value will result in the image mid-tones being washed-out or too dark. |
| **Gain** | This will adjust the luminance intensity of the image's whites (highlights) to accurately reproduce colors. Raising or lowering this value will result in the image highlights being washed-out or too dark. |
| **Offset** | This will adjust the luminance intensity of the image's blacks (shadows) to accurately reproduce colors. Raising or lowering this value will result in the image shadows being washed-out or too dark. |
| **HighLights Min** | This is a multiplier of the properties that affect the color correction properties that have been adjusted in the **Highlights** section. |
| Misc |   |
| **Blue Correction** | Correction for artefacts with "electric" blues due to the ACES color space. Bright blue desaturates instead of going violet. |
| **Expand Gamut** | Expand bright saturated colors outside the sRGB gamut to fake wide gamut rendering. |
| **Tone Curve Amount** | Allows effects of Tone Curve to be reduced. Set Tone Curve Amount and Expand Gamut to 0 to full disable tone curve. |
| **Scene Color Tint** | This is a multiplier for color that is a filter color applied to the HDR scene color. |
| **Color Grading LUT Intensity** | A scaling factor that controls the effect of the color correction. |
| **Color Grading LUT** | The LUT texture to use as a lookup table for color correction. [See below for examples.](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorgradinglut) |

##### Color Grading LUT

   |   |   |   |
| --- | --- | --- |
| 
Click image for full size.



 | 

Click image for full size.



 | 

Click image for full size.



 |
| ![Neutral LUT](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/007141bb-70e2-48e8-85e8-eb1eab89fc5c/rgbtable16x1.png) | ![Greenish LUT](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aaf9999b-ff56-4688-a5da-c24968e805ae/lut_greenish.png) | ![Reddish LUT](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7c6e9d4-9799-4172-a25d-fb7c9ea9f78a/lut_reddish.png) |

### Workflow for Good Color Correction

These are some good habits that should be used when working with the color grading tools in your Post Process Volume.

-   The **Film** controls should be set for a project-wide look. Ideally, these properties should not be adjusted and certainly should not be adjusted dynamically or on a shot-by-shot basis. Use the [Color Grading](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorcorrectionproperties) properties for this.
    
-   Start by using the **Global** color correction properties and doing an initial pass on your scene before touching any of the other properties. The majority of your color grading changes should be done with these properties.
    
-   You should not try to use the **Gain** property to adjust exposure for your scene. This should be used for fine tweaks for different colors. Instead use the **Exposure Bias** in the **Lens** > **Auto-Exposure** section.
    
-   Use **Offset** in minor amounts to make your shadowed or darkened areas a little lighter. If you want things to look a little hazy or have more bloom, then you can set a higher value, conversely if your scene is overly hazy or has too much bloom you can lower the value to subtract color from the scene.
    
-   Instead of using a [Lookup Table (LUT)](/documentation/en-us/unreal-engine/using-lookup-tables-for-color-grading-in-unreal-engine) for coloring the scene, since that happens after tone mapping, you should use the Color Grading properties to get the look you want so that it's consistent on all displays you output to (LDR and HDR). However, it can be a good practice to quickly get a look to set the tone with a LUT and then adjust the color correction to get a similar look.
    

## Training Streams