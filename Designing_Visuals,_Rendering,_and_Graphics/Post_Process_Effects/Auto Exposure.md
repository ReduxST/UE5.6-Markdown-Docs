# Auto Exposure

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:15

---

The **Post Process Volume** provides controls for setting up **Exposure** (more commonly called eye adaptation), which automatically adjusts how bright or darker the scene looks. This effect recreates the experience of human eyes adjusting to different lighting conditions, like when walking from a dimly lit interior to a brightly lit exterior, or the other way around.

## Exposure Metering Modes

The engine offers several types of metering modes to choose from when setting up auto exposure in your scenes. These different metering modes provide settings that accurately mimic real-world cameras, giving you control over exposure in your scenes through the post process.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c24fd1dd-902b-44ad-a775-efffd10558eb/exposuremeteringmodes.png)

-   **Auto Exposure Histogram** mode provides finer control over auto exposure with advanced settings constructed from a 64-bin histogram. This is the default exposure metering mode in Unreal Engine.
-   **Auto Exposure Basic** mode provides fewer settings, but is a faster method that computes single values by downsampling exposure.
-   **Manual** mode enables the use of **Camera** settings within the Post Process and Cameras settings to control exposure, rather than using only the settings found in the **Exposure** category.

### Histogram and Basic Algorithm

**Auto Exposure Basic** and **Auto Exposure Histogram** metering modes both calculate the overall luminance of the scene, and brighten or darken the scene to an expected value, but they differ in how they calculate scene luminance.

-   The **Auto Exposure Basic** algorithm uses the average of the log luminance of the scene to determine the target exposure value.
-   The **Auto Exposure Histogram** mode first calculates a histogram of the log luminance scene. Then, the histogram is analyzed to determine the average luminance value.

The Basic and Histogram modes use different algorithms to calculate the average luminance of the scene. However, once the average luminance value is determined, both algorithms treat that luminance as middle gray. In photography, this middle gray point is sometimes referred to as "18% gray" or "18% middle gray," referring to the amount of light that is reflected by a gray card.

### Manual Algorithm

The **Manual** metering mode allows the user to select a single, fixed exposure value that is unaffected by the luminance in the scene. If **Apply Physical Camera Exposure** is disabled in the post process settings, the exposure value will be linear brightness:

```
	`Exposure = 1/(2^(EV100 + Exposure Compensation))`

Copy full snippet
```
Exposure = 1/(2^(EV100 + Exposure Compensation))

If **Apply Physical Camera Exposure** is applied, EV100 is calculated as the following formula. Otherwise, it is 0.

```
	`EV100 = log2(Aperture^2 / Shutter Speed * 100/ISO)`

Copy full snippet
```
EV100 = log2(Aperture^2 / Shutter Speed \* 100/ISO)

Exposure in the following formula defines the relationship between the scene surface luminance (L, which is measured in cd/m2) and pixel brightness (B) before the tonemapper and exposure compensation are applied.

```
	`B = Exposure * L`

Copy full snippet
```
B = Exposure \* L

You can verify this formula's result by disabling the tonemapper through the viewport show flags (**Show > Post Processing**), and inspect the scene brightness using the Pixel Inspector. Also note that the [editor EV100 override setting](/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine#editorviewportoverride) directly sets the EV100 exposure used in this equation.

The **Exposure Compensation** (also called **ExpComp** for short) defines an additional scale of 2^ExpComp on top of the exposure computed from the current metering mode, except when using the EV100 editor override.

## Local Exposure

**Local Exposure** is a technique that automatically applies local adjustments to exposure — within artist-controlled parameters — to preserve both highlight and shadow detail on top of the existing global exposure system. This is especially useful for projects with challenging high dynamic range scenes using dynamic lighting, in which applying a single global exposure adjustment is not enough to avoid blown out highlights and completely dark shadows.

Projects using dynamic time-of-day systems can encounter scenes with both under and over exposed areas in the final image, such as indoor scenes with very bright outdoors visible through a door or window, which can be problematic for gameplay. For example, the scene below is an example where there are under and over exposed areas.

![With Exposure Only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3eeae557-8439-4e03-a710-8d8b4c029402/local-exposure-disabled.png)

![With Local Exposure](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57fe6a7b-bc9c-41e0-b71a-007c535d051f/local-exposure-enabled.png)

Local Exposure helps achieve a more consistent final image when carefully crafted lighting per scene is not feasible, and it should always be set up when using [Lumen Global Illumination](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine).

[Local Exposure settings](/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine#localexposuresettings) are found in the Post Process Volume settings under the **\*Lens > Local Exposure** category.

![Post Process Volume Local Exposure settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9afc8642-9022-4fba-ada5-0ef62fd41793/local-exposure-settings.png)

Use the **Local Exposure** visualization mode to see how it is being applied to the scene. You can enable this visualization in the Level Viewport under the **Show > Visualization** menu.

![Local Exposure visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdde5e39-8362-4e8d-b3d5-105b72fd2358/local-exposure-visualization.png)

## Key Concepts and Features

The following key concepts, features, and best practices should be taken into consideration when setting up and working with auto exposure in the levels for your project.

### Exposure Compensation Curve

The **Exposure Compensation Curve** Asset slot provides artists with finer control over exposure compensation in their scenes. The curve asset provides direct control over the X and Y axes. When using the high dynamic range visualization mode **HDR (Eye Adaptation)**, these values can be pulled from the information displayed on the screen.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d8c6039-a8e8-4c1d-adc9-83b15e5e9a2f/ppv_expcompassetcurve.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e852dd91-6545-4468-8813-38dae840d6ba/expcompcurveasset.png) |
| Post Process Settings | Curve Asset Graph |

Add your own curves by using the Content Browser to select the **Add New** button and navigating to the **Miscellaneous** category to select a **Curve** Asset type. In the Pick Curve Class window, select a **Curve Float** type.

In the Level Viewport with the "HDR (Eye Adaptation)" visualization mode enabled, the X-axis is presented by the **Average Scene EV100** value (1) and the **Actual** (purple) line (1) on the histogram chart. The Y-axis is represented by the **Exposure Compensation (Curve)** value (2).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a3856b4-5d1c-42cc-90e2-07e6050d020f/expcompcurve.png)

The example scene above shows the **Average Scene EV100** is 0.548, which translates to the plugged-in value of the X-axis of the Curve Asset (shown below). This also returns the value of 0.864 for the **Exposure Compensation (Curve)** value.

Click image for full size.

The Exposure Compensation values are split into their own *settings* and *curve* values, giving you more precise control over how you adjust them. They also provide an explanation why the exposure compensation is behaving in a specific way by separating these values.

The relevant values are:

-   **Average EV100** is the calculated target EV100 value, and is represented by the target (blue) line in the histogram.
-   **Exposure Compensation (Settings)** is the exposure compensation value set in the post process settings.
-   **Exposure Compensation (Curve)** is the resulting Y-axis value in a Curve Asset assigned to the Exposure Compensation Curve slot in the post process.
-   **Exposure Compensation (All)** is the sum of the *settings* and *curve* exposure compensation values resulting in the final exposure compensation value.

### Exposure Metering Mask

The **Exposure Metering Mask** gives artists an optional texture slot to control the influence of auto exposure for the whole screen, where each pixel is weighted in importance by the assigned texture mask. Giving importance to pixels toward the center of the screen rather than along the edges helps stabilize auto exposure (see the example below).

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dac1e268-e130-456e-90d3-89535be4b08e/ppv_expcompmeteringmask.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd8550fa-ca8b-45ab-a6c3-1a813330f8ae/expmeteringmaskexample.png) |
| Post Process Settings | Exposure Metering Mask Example Texture |

By weighting pixels in the mask toward the center of the screen, bright objects appearing along the edges of the screen have less potential to cause abrupt changes in the expected exposure.

![Without Exposure Metering Mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02f82c22-7fca-4aa6-99e2-c52f53803217/expmetmask_disabled.png)

![With an Exposure Metering Mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6da66722-733f-483b-a434-8b9be6396a2f/expmetmask_enabled.png)

The console command **r.EyeAdaptation.Focus** was removed from Unreal Engine 4.25 and newer. This command applied weighting values uniformly across the screen, providing similar functionality that is now handled by creating your own metering mask. Also, this command only supported Auto Exposure Basic metering mode, while the exposure metering mask supports both Histogram and Basic metering modes.

### Exposure Change Speed and Movement

The rate at which exposure compensation adapts to the current scene is done in logarithmic steps that perceptually move up and down the curve at the same rate of speed. The exposure compensation moves along the curve toward its Target value in f-stops per second.

To handle this perceptual movement, the adaptation algorithm traverses the curve with linear and exponential movement. Using both traversal methods improves two side effects of using only exponential movement:

-   It reduces jittery behavior from adapting quickly to small fluctuations in luminance.
-   It makes it possible to create slow transitions from dark to bright areas.

In the example below, the traversal along the curve starts out linearly (2) when far away from the Target exposure value. Once it's closer, the traversal transitions to exponential movement (1) that maintains continuity of the first derivative.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a12fde7b-4914-4e95-ae4d-73bb07b05e67/curvemovement.png)

When getting close to the Target exposure value, there is a set transition distance where the curve switches from linear to exponential movement. By default, this transition happens at 1.5 f-stops from the Target value. You can set the transition distance (in f-stops per second) using the command **r.EyeAdaptation.ExponentialTransitionDistance**.

#### Using Speed Up and Speed Down Parameters

The **Speed Up** and **Speed Down** properties in the post process controls how quickly or slowly the exposure adjusts from the Actual (purple) to the Target (blue) value. These settings let you set a time frame (in f-stops per second) for your eyes to adjust when moving between different luminance ranges, such as moving from a dark environment to a bright one.

When setting these values, consider how long it should take for your eyes to adjust to lighting changes. Use the recommendations below when setting these properties:

-   The **Speed Up** parameter should use higher values when mimicking eye adaptation behavior. This allows for quicker transitions when moving from dark areas to brightly lit ones. It also mimics natural eye behavior by *contracting* the iris, allowing less light into the pupils. Longer transition times keep exposure high, and the image is overly bright.
-   The **Speed Down** parameter should use lower values when mimicking eye adaptation behavior. This allows for slower transitions when moving from brightly lit areas to darker ones. It also mimics natural eye behavior by *expanding* the iris, allowing more light into the pupils. Longer transition times keep exposure low, and the image is overly dark.

### Extend Default Luminance Range for EV100

By default, the engine uses pixel luminance (cd/m2) for the **Max Brightness** and **Min Brightness** settings found in the Post Process Volume. When attempting to set [physically accurate lighting ranges](/documentation/en-us/unreal-engine/using-physical-lighting-units-in-unreal-engine), the default luminance range for auto exposure can be extended to express luminance in EV100 (also called ISO 100). This means that you can use correct lux values for lights in your scene and have them respected by auto exposure without causing the image to be blown out.

You can enable this option from the Project Settings in the **Rendering > Default Settings** section by placing a check next to **Extend default luminance range in Auto Exposure settings**.

Enabling this setting changes the default Post Process Volume values for the **Min Brightness** and **Max Brightness**, along with the **Histogram Log Min** and **Histogram Log Max** names to reflect EV100.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/707b6542-1583-4d00-aafa-06466543d332/ppvsettings_default.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/026e39e7-aea7-476d-9c68-a9fbe3cd3a66/ppvsettings_extendedluminance.png) |
| Engine Default Settings | With Extended Luminance Range Enabled |

### Pre-Exposure

The amount of exposure applied in the shader is called **pre-exposure**. The previous frames's scene exposure is applied within the shader before writing to the scene color. This enables the engine to remap the range of the scene color around the camera exposure to render the scene within a range similar to one of the final color (after exposure). It reduces the risk of arithmetic overflow for low-precision render target formats when using very bright lights by limiting the render target range required to support HDR lighting values. It also has the effect of increasing the quality of Auto Exposure Basic metering mode when enabled.

Pre-exposure can be enabled in the Project Settings in the **Rendering > Default Settings** section with **Apply Pre-exposure before writing to the scene color**.

## Mobile Usage

Auto Exposure on mobile devices that support feature level ES3.1 or higher share feature parity with desktop and console platforms. For mobile, memory cost is trivial, and performance cost should be minor depending on your scene.

For any Unreal Engine project which has **Mobile HDR** enabled in the project settings has Auto Exposure enabled by default. Should it not be, you can set the following:

-   Enable **Mobile HDR** in the project settings under the **Engine - Rendering -** section.
-   Set the console variable **r.Mobile.EyeAdaptation** to be **1**. This should be enabled by default.
-   Set the console variable **r.EyeAdaptationQuality** should be set to a value greater than 0.

Configure these console variables in your `BaseScalability.ini` configuration file under the **\[PostProcessQuality\]** section. When using defined profiles for specific devices, set the console variable **sg.PostProcessQuality** in the `BaseDeviceProfiles.ini`. Note that all devices are enabled by default, except **Android\_Low**.

## Game Settings

The default auto exposure post processing and Post Process Volumes control the *in-game* settings for auto exposure. The auto exposure is on by default and is available for the Level Viewport and Asset Editor viewports.

Auto Exposure settings can be accessed from the **Lens** category under the **Exposure** dropdown.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6c6e822-0e71-4cfa-b26a-3637146b280b/gamesettings_detailspanel.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f17a0266-0936-4f6d-9f5b-2058d5b3adbd/gamesettings_previewscenesettings.png) |
| Post Process Volume Settings | Asset Editor Preview Scene Settings |

The Post Process Settings available in the Level Viewport **Details** panel and the Asset Editor **Preview Scene Settings** panel contains the relevant settings needed to adjust auto exposure for your scenes. The selected **Metering Mode** gives access to different sets of properties within the post process. Each mode sets the luminance computation method to be used for auto exposure.

Choose from the following metering modes:

-   **Auto Exposure Histogram** constructs a 64-bin, histogram enabling finer control over auto exposure with advanced settings.
-   **Auto Exposure Basic** is a faster method that computes single values by down sampling.
-   **Manual** enables the use of **Camera** post process settings within to control exposure rather than using its Exposure properties.

### Auto Exposure Histogram Settings

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/016b9cdf-f343-4342-a830-69e6c53ed133/autoexp_histogram.png)

| Property | Description |
| --- | --- |
| **Exposure Compensation** | Logorithmic adjustment for exposure, and is only used if a tonemapper is specified. When set to 0, there will be no adjustment, -1 is two times darker, -2 is four times darker, 1 is two times brighter, and 2 is four times brighter. |
| **Apply Physical Camera Exposure** | This toggle only affects **Manual** metering mode. When enabled, brightness of the scene is affected by the **Camera** settings (ISO, Shutter Speed, and Aperture). When disabled, the camera uses default values of ISO 100, Aperture 1.0, and Shutter Speed 1.0. Most scenes will be significantly darker when this flag is enabled. |
| **Exposure Compensation Curve** | This slot takes a Curve Asset, which is used for finer control over exposure compensation in the scene. The X and Y-axis values in the Curve graph translate to the **Average Scene EV100** and **Exposure Compensation (Curve)** values. |
| **Exposure Metering Mask** | Use your own texture mask to meter exposure. Bright spots on the mask will have high influence on auto exposure metering, and dark spots will have low influence. |
| **Min Brightness** | The minimum brightness for auto exposure that limits the lower brightness the camera can adapt within. Value must be greater than 0 and should be less than or equal to **Max Brightness**. A good value should be a positive near 0 and should be adjusted in a dark lighting situation. If this value is too small, the viewport image appears too bright. If too large, the image appears too dark. Actual values depend on the HDR range of the content being used. If Min Brightness is equal to Max Brightness, auto exposure is disabled. |
| **Max Brightness** | The maximum brightness for auto exposure that limits the upper brightness the camera can adapt within. Value must be greater than 0 and should be greater than or equal to **Min Brightness**. A good value should be positive (2 is a good starting point), and should be adjusted in a bright lighting situation. If this value is too small, the viewport image appears too bright. If too large, the image appears too dark. Actual values depend on the HDR range of the content being used. If Max Brightness is equal to Min Brightness, auto exposure is disabled. |
| **Min EV100** | Replaces **Min Brightness** when the project setting **Extend default luminance range in Auto Exposure settings** is enabled. The minimum brightness limit for auto exposure adaptation, expressed in pixel luminance (cd/m2). Value is typically negative and should be less than or equal to Max EV100. As this value increases, the scene view gets darker. If Min EV100 is equal to Max EV100, auto exposure is disabled. |
| **Max EV100** | Replaces **Max Brightness** when the project setting **Extend default luminance range in Auto Exposure settings** is enabled. The maximum brightness limit for auto exposure adaptation, expressed in pixel luminance (cd/m2). Value should be positive and should be greater than or equal to Min EV100. As this value decreases, the scene view gets brighter. If Max EV100 is equal to Min EV100, auto exposure is disabled. |
| **Speed Up** | The speed at which the adaptation occurs from a dark environment to a bright environment. |
| **Speed Down** | The speed at which adaptation occurs from a bright environment to a dark environment. |
| Advanced |   |
| **Low Percent** | Auto exposure adapts to a value extracted from the luminance histogram of the scene color. The value is defined as having X percent below this brightness. Higher values give bright spots on the screen more priority, but can lead to less stable results. Lower values give the medium and dark values more priority, but might cause burnout of bright spots. Values should be greater than 0 and less than 100. A good starting range is 70 to 80. |
| **High Percent** | Auto exposure adapts to a value extracted from the luminance histogram of the scene color. The value is defined as having X percent below this brightness. Higher values give bright spots on the screen more priority, but can lead to less stable results. Lower values give the medium and dark values more priority, but might cause burnout of bright spots. Values should be greater than 0 and less than 100. A good starting range is 80 to 95. |
| **Histogram Log Min** | Defines the lower bounds for the brightness range of the generated histogram when using the **HDR (Eye Adaptation)** visualization mode. |
| **Histogram Log Max** | Defines the upper bounds for the brightness range of the generated histogram when using the **HDR (Eye Adaptation)** visualization mode. |
| **Histogram Min EV100** | Replaces **Min Brightness** when the project setting **Extend default luminance range in Auto Exposure settings** is enabled. Defines the lower bounds for the brightness range of the generated histogram when using the **HDR (Eye Adaptation)** visualization mode. |
| **Histogram Min EV100** | Replaces **Min Brightness** when the project setting **Extend default luminance range in Auto Exposure settings** is enabled. Defines the upper bounds for the brightness range of the generated histogram when using the **HDR (Eye Adaptation)** visualization mode. |

### Auto Exposure Basic Settings

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee6d831e-1eb9-47a1-8f83-4b55c16240fb/autoexp_basic.png)

| Property | Description |
| --- | --- |
| **Apply Physical Camera Exposure** | This toggle only affects **Manual** metering mode. When enabled, brightness of the scene is affected by the **Camera** settings (ISO, Shutter Speed, and Aperture). When disabled, the camera uses default values of ISO 100, Aperture 1.0, and Shutter Speed 1.0. Most scenes will be significantly darker when this flag is enabled. |
| **Exposure Compensation** | Logarithmic adjustment for exposure, and is only used if a tonemapper is specified. When set to 0, there will be no adjustment, -1 is two times darker, -2 is four times darker, 1 is two times brighter, and 2 is four times brighter. |
| **Exposure Compensation Curve** | This slot takes a Curve Asset which is used for finer control over exposure compensation in the scene. The X and Y-axis values in the Curve graph translate to the **Average Scene EV100** and **Exposure Compensation (Curve)** values. |
| **Exposure Metering Mask** | Use your own texture mask to meter exposure. Bright spots on the mask will have high influence on auto exposure metering, and dark spots will have low influence. |
| **Min Brightness** | The minimum brightness for auto exposure that limits the lower brightness the camera can adapt within. Value must be greater than 0 and should be less than or equal to **Max Brightness**. A good value should be a positive near 0 and should be adjusted in a dark lighting situation. If this value is too small, the viewport image appears too bright. If too large, the image appears too dark. Actual values depend on the HDR range of the content being used. If Min Brightness is equal to Max Brightness, auto exposure is disabled. |
| **Max Brightness** | The maximum brightness for auto exposure that limits the upper brightness the camera can adapt within. Value must be greater than 0 and should be greater than or equal to **Min Brightness**. A good value should be positive (2 is a good starting point), and should be adjusted in a bright lighting situation. If this value is too small, the viewport image appears too bright. If too large, the image appears too dark. Actual values depend on the HDR range of the content being used. If Max Brightness is equal to Min Brightness, auto exposure is disabled. |
| **Min EV100** | Replaces **Min Brightness** when the project setting **Extend default luminance range in Auto Exposure settings** is enabled. The minimum brightness for auto exposure adaptation, expressed in pixel luminance (cd/m2). Value is typically negative and should be less than or equal to Max EV100. As this value increases, the scene view gets darker. If Min EV100 is equal to Max EV100, auto exposure is disabled. |
| **Max EV100** | Replaces **Max Brightness** when the project setting **Extend default luminance range in Auto Exposure settings** is enabled. The maximum brightness for auto exposure adaptation, expressed in pixel luminance (cd/m2). Value is typically positive and should be greater than or equal to Min EV100. As this value decreases, the scene view gets brighter. If Max EV100 is equal to Min EV100, auto exposure is disabled. |
| **Speed Up** | The speed at which the adaptation occurs from a dark environment to a bright environment. |
| **Speed Down** | The speed at which adaptation occurs from a bright environment to a dark environment. |
| Advanced Settings |   |
| **Low Percent** | The eye adaptation will adapt to a value extracted from the luminance histogram of the scene color. This value is defined as having x percent below this brightness. Higher values give bright spots on the screen more priority but can lead to less stable results. lower values give the medium and dark values more priority but might cause burn out of bright spots. Values should be greater than 0 but less than 100. Values within the range of 70 to 80 are ideal. |
| **High Percent** | The eye adaptation will adapt to a value extracted from the luminance histogram of the scene color. This value is defined as having x percent below this brightness. Higher values give bright spots on the screen more priority but can lead to less stable results. Lower values give the medium and dark values more priority but might cause burn out of bright spots. Values shoudl be greater than 0 but less than 100. Values within the range of 80 to 95 are ideal. |
| **Histogram Min EV100** | The histograms minimum value. This is expressed in Log2(Luminance) or in EV100 when using Extend Default Luminance Range in the project settings. |
| **Histogram Max EV100** | The histograms max value. This is expressed in Log2(Luminance) or in EV100 when using Extend Default Luminance Range in the project settings. |

### Manual Settings

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f7a51a0-9ba5-461f-aa07-3bab53448f42/autoexp_manual.png)

| Property | Description |
| --- | --- |
| Exposure |   |
| **Exposure Compensation** | Logarithmic adjustment for exposure, and is only used if a tonemapper is specified. When set to 0, there will be no adjustment, -1 is two times darker, -2 is four times darker, 1 is two times brighter, and 2 is four times brighter. |
| **Apply Physical Camera Exposure** | This toggle only affects **Manual** metering mode. When enabled, brightness of the scene is affected by the **Camera** settings (ISO, Shutter Speed, and Aperture). When disabled, the camera uses default values of ISO 100, Aperture 1.0, and Shutter Speed 1.0. Most scenes will be significantly darker when this flag is enabled. |
| **Exposure Metering Mask** | Use your own texture mask to meter exposure. Bright spots on the mask will have high influence on auto exposure metering, and dark spots will have low influence. |
| Camera |   |
| **Shutter Speed (1/s)** | Defines the camera shutter speed in seconds. |
| **ISO** | This value represents the camera sensor sensitivity. |
| **Aperture (F-stop)** | Defines the size of the opening for the camera lens. Larger values reduce the depth of field (DOF) effect. |

## Local Exposure Settings

![Local Exposure Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce7eff6b-44c2-43f6-ab07-b32ad5bef0d2/local-exposure-settings.png)

| Property | Description |
| --- | --- |
| **Method** | 
Choose an algorithm to use with your local exposure settings:

-   **Bilateral:** This algorithm will decompose the image into base and detail layers using a bilateral blur. Only the base layer contrast is reduced in order to preserve detail.
-   **Fusion:** This algorithm fuses multiple exposures according to quality measures. Local exposure is calculated using the fused exposures.



 |
| **Highlight Contrast** | Controls the contrast of highlights. Local exposure decomposes luminance of the frame into a base layer and a detail layer. Contrast of the base layer is reduced based on this value. Good values are usually found between 0.6 and 1. |
| **Shadow Contrast** | Controls the contrast of shadows. Local exposure decomposes luminance of the frame into a base layer and a detail layer. Contrast of the base layer is reduced based on this value. Good values are usually found between 0.6 and 1. |
| **Highlight Contrast Curve** | This curve is used to calibrate local exposure differently depending on the average scene luminance. |
| **Shadow Contrast Curve** | This curve is used to calibrate local exposure differently depending on the average scene luminance. |
| **Highlight Threshold** | The threshold used to determine which regions of the screen are considered highlights. |
| **Shadow Threshold** | The threshold used to determine which regions of the screen are considered shadows. |
| **Detail Strength** | Controls the strength of detail applied to the scene. Local exposure decomposes luminance of the frame into a base layer and a detail layer. Values different than 1 enable local exposure. This value should be set to 1 in most cases. |
| **Blurred Luminance Blend** | Blends between bilateral filtered and blurred luminance as a base layer. Blurred luminance helps preserve image appearance and specular highlights, and reduces ringing. Good values are usually in the range of 0.4 and 0.6. |
| **Blurred Luminance Kernel Size Percent** | The percentage of the screen (or kernel size) used to blur frame luminance. |
| **Middle Grey Bias** | Logarithmic adjustment for what Local Exposure considers Middle Grey (the tone that is perceptually halfway between black and white). 0 is equal to no adjustment, -1 is twice as dark, -2 is four times as dark, 1 is twice as bright, and 2 is four times as bright. |

## Editor Viewport Override

Each editor viewport provides an option to override default auto exposure settings or ones set in your Post Process Volume.

Access the exposure override from the **View Mode** dropdown in the Level Viewport or any Asset Editor viewport and disable the checkbox next to **Game Settings** or **Auto** to use the EV100 slider.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69ebf8e2-b477-4fc1-8cc1-e1dfa97fe6d7/override_levelviewport.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8afd3c7c-ec3a-43a8-b582-be95bc6311e3/override_asseteditor.png) |
| Level Viewport Override | Asset Editor Override |

## Visualization and Debugging

The **HDR (Eye Adaptation)** visualization mode provides a histogram representation of the exposure values measured in the current scene view along with quick reference to values set in the Post Process Volume and Curve Asset.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4eadc893-0c07-453c-bdbd-bc8aca7d6956/hdr_vismode.png)

1.  A list of exposure and curve values set in the Post Process Volume and Curve Asset.
2.  The focal point meter with NIT (measured in cd/m2) and LUX values.
3.  The histogram chart with set min and max ranges.

Enable this visualization mode using the Level Viewport to select **Show** > **Visualize** > **HDR (Eye Adaptation)**.

### Histogram Chart

The histogram chart consists of a range of exposure values measured in the current view. Within the chart are colored lines that represent the target, actual, and final exposure values are always adapting to the measured exposure of the current camera view.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fc7ed7e-5268-4767-956a-fba59fa1b1b2/histogramchart.png)

-   The **blue** line represents the *target* EV100 exposure for the current view.
    -   This is where the average scene exposure is at in the histogram.
-   The **purple** line is the *actual* EV100 exposure for the current view.
    -   This is the current exposure that exists within this view. The actual exposure value will always be moving toward the target exposure value as it changes with the view.
-   The **white** line is the *final* EV100 exposure value after adjusting the exposure compensation in the post process settings.
    -   This is the actual exposure value in the current view after exposure compensation. The white and purple lines will maintain a distance set by the exposure compensation. In the example above, there is an exposure compensation of 2 where the white and purple lines keep that distance from one another.

In this example scene, if the Exposure Compensation is changed in the Post Process Volume **Exposure** settings, that value is reflected in the list of exposure settings in the Level Viewport. The difference offset for exposure compensation is reflected in the chart by the separation of the actual exposure (purple) and final exposure (white) lines.

In the chart, the far edges represents the auto exposure adaptation ranges set by **Histogram Log Min** and **Histogram Log Max** (or **Histogram Min EV100** and **Histogram Max EV100** when the project setting **Extend default luminance range in Auto Exposure settings** is enabled).

### Histogram Debug Visualization Mode

This mode provides a visualization of different pixel values to ensure that very bright pixels (like the sun) and very dark pixels (like deep shadows) are not involved in the HDR calculation that is happening for auto exposure.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0076d89-fd7f-412f-aed5-1298c4f31d1f/histogramdebugvis.png)

Red pixels represent anything *below* the auto exposure adaptation ranges set by **Histogram Log Min** (or **Histogram Min EV100**). Blue pixels represent anything *above* the auto exposure adaptation ranges set by **Histogram Log Max** (or **Histogram Max EV100**). These pixel ranges ensures that the values set for **Low Percent** and **High Percent** are removing these unwanted pixels from being calculated.

This debug visualization mode requires that the **HDR (Eye Adaptation)** visualization mode first be enabled.

Enable this visualization mode using the command **r.EyeAdaptation.VisualizeDebugType 1**.