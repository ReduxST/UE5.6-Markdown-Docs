# Performance Guidelines for Mobile Devices

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/performance-guidelines-for-mobile-devices-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/performance-guidelines-for-mobile-devices-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:24

---

When developing for Mobile platforms, there are some things you should keep in mind when targeting specific devices or that are general good practices depending on the list of devices you want to release your title for. This includes developing with a specific lighting tier to get the most out of performance on a device and why a particular lighting tier may work best for your target audience. You will also find some suggestions to keep in mind for any project you work on that will be developed with Mobile in mind.

## Performance Tiers

**Unreal Engine 5 (UE)** supports a variety of lighting features on mobile devices. Using these features costs performance and may cause your game to perform poorly on slower mobile devices. While it is possible to mix and match most of UE's mobile lighting features, it can be useful to categorize these features into the following tiers. When building a mobile game, you should decide which features to use based on the quality of graphics your game requires and the types of devices you need to support. Check the development requirements for [iOS Development](/documentation/404) and [Android Development](/documentation/404) for more information on what devices have been tested here at Epic and which tiers we think are most appropriate for that device.

### LDR (Low Dynamic Range)

**Low Dynamic Range** (LDR) mode is the lowest performance tier supported in UE and is recommended for games that do not require lighting or Post Processing features.

To use this mode, you must disable **Mobile HDR** for your project in the **Rendering** section of the [Project Settings](/documentation/en-us/unreal-engine/project-settings-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cda5782c-be22-490d-815d-e103dfd45ec7/01-mdv-perfom-disable-mob-hdr.png)

| Advantages | Limitations | Recommendations |
| --- | --- | --- |
| 
-   Provides the fastest and lowest overhead mode available for mobile devices, which enables your game to run well on slower mobile devices.
-   Still provides full access to the **Material Editor** for defining custom shaders and even performing simple shading that can be used to fake lighting.



 | 

-   The scene's color is written out in gamma space with each color channel clamped to the range of \[0,1\].
-   Translucent primitives are blended in gamma space. In most cases, this will require you to author your translucent textures and Materials differently than you would in HDR or for a normal PC title.
-   Post Processing features are unavailable in this mode.



 | 

-   Make sure all of your Materials have their shading model set to **Unlit** for maximum performance.
-   Placed lighting should not be used in your scene when depending on maximum performance.
-   Consider performing as many operations in the Materials **Vertex Shader** as possible. You can do this by enabling **Customized UVs**, connecting nodes to them and then in the pixel shader using a **Texture Coordinate** node to target the Customized UV.



 |

### Basic Lighting

In this tier, you will leverage **Static Lighting** and fully rough Materials to create **Levels** with interesting lighting while maximizing performance to reach a broader range of mobile devices.

To use this mode, you must enable **Mobile HDR** for your project in the **Rendering** section of the [Project Settings](/documentation/en-us/unreal-engine/project-settings-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e907ba5-08f5-4f1e-b04f-7f385125cead/02-mdv-perfom-enable-mob-hdr.png)

| Advantages | Limitations | Recommendations |
| --- | --- | --- |
| 
-   Access to Static Lighting and Global Illumination features.
-   Full HDR pipeline with access to some Post Processing features, like **Tone Mapping**.
-   Translucency is blended in linear space, enabling you to author content as your normally would for Desktop.



 | 

-   Since all Materials need to be marked as **Fully Rough**, your Materials will not have interesting specular reflection.
-   If you choose to disable **Lightmap Directionality**, **Normal Maps** will have no effect.



 | 

-   Author all of your Materials with the **Fully Rough** flag set.
-   Consider disabling the flag for **Lightmap Directionality** in your Materials for additional performance.
-   Use only Static Lights in your maps.
-   Disable some Post Processing features completely, like **Bloom**. Also, stick to the basic set of film and color controls.



 |

### Full HDR (High Dynamic Range) Lighting

In this tier, you take advantage of most of the HDR lighting features available for mobile in UE, as well as some of the Post Processing features. Using these features requires quite a bit of performance in exchange for high-quality lighting features.

To use this mode, you must enable **Mobile HDR** for your project in the **Rendering** section of the [Project Settings](/documentation/en-us/unreal-engine/project-settings-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce95a18b-3040-409d-9ca8-53e27e7a9fab/02-mdv-perfom-enable-mob-hdr.png)

| Advantages | Recommendations |
| --- | --- |
| 
-   Access to Static Lighting and **Global Illumination** features.
-   Full HDR pipeline with access to some Post Processing features.
-   Translucent is blended in linear space, enabling you to author content as you normally would for Desktop.
-   Realistic specular reflections on surfaces with support for varying roughness.



 | 

-   Consider enabling **Bloom** to take full advantage of the HDR lighting pipeline.
-   Realistic specular reflections in combination with HDR lighting can lead to specular aliasing. To reduce this effect, enable the Material property for **Normal Curvature to Roughness** to reduce specular aliasing due to high-frequency information in your normal map. You can also consider enabling anti-aliasing via the **Project Settings > Rendering** to help reduce the artifact.
-   Take time to consider the placement of **Reflection Capture Actors** to achieve the best results. See [Reflections: Placing Reflection Captures](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine#placingreflectioncaptures) for more information.
-   Use only Static Lights and Lightmaps in your scene for the best performance.



 |

### Full HDR Lighting with per-pixel lighting from the Sun

In this tier, you take advantage of all of the HDR lighting features available for mobile in UE. This tier is the same as [Full HDR Lighting](/documentation/en-us/unreal-engine/performance-guidelines-for-mobile-devices-in-unreal-engine#fullhdr_highdynamicrange_lighting) and has the same advantages and recommendations with the exception that here you can add a single **Directional Light** to your scene that automatically uses per-pixel lighting for higher quality.

To use this mode, you must enable **Mobile HDR** for your project in the **Rendering** section of the [Project Settings](/documentation/en-us/unreal-engine/project-settings-in-unreal-engine).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/426b3eee-9ef5-4531-805b-0fa5c47f125a/02-mdv-perfom-enable-mob-hdr.png)

| Advantages | Recommendations |
| --- | --- |
| 
-   All of the features and advantages listed for the [Full HDR](/documentation/en-us/unreal-engine/performance-guidelines-for-mobile-devices-in-unreal-engine#fullhdr_highdynamicrange_lighting) tier.
-   Per-pixel diffuse and specular lighting for a single Directional Light.
-   High-quality precomputed **Distance Field** shadows for a single Directional Light.



 | 

-   All of the recommendations and advantages of the [Full HDR](/documentation/en-us/unreal-engine/performance-guidelines-for-mobile-devices-in-unreal-engine#fullhdr_highdynamicrange_lighting) tier.
-   Use only Static Lights in your except for a single Directional Light, which should be set to **Stationary**.



 |

## Shader Complexity View Mode

The [Shader Complexity](/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine#shadercomplexity) view mode in the [Mobile Previewer](/documentation/en-us/unreal-engine/using-the-mobile-previewer-in-unreal-engine) to get a sense of what your Material costs will be for specific devices you are targeting. The colors indicated on screen will tell you how expensive the Material is for the device you're targeting; green means good performance, bright red means very expensive, and white or pink means that the Material is very expensive.

To use it, in the **Main Viewport** click the **View Modes** list and select **Optimization Viewmodes** and choose **Shader Complexity**, or you can use the keyboard shortcut **Alt + 8**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66979977-9c87-47e6-a334-270f3f605d96/03-mdv-perfom-enable-shader-complexity.png)

These are some examples taken from **Mobile Sun Temple** to give you an idea of Material cost when viewed using Shader Complexity:

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9a4fdef-6aa8-469f-8517-e589f949db78/04-mdv-perfom-example-1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff3c0be4-decb-4a17-a85f-1ed3dcfd80a8/05-mdv-perfom-example-2.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/538ef9ca-bf29-417d-83dc-07058fbed82d/06-mdv-perfom-example-3.png) |
| 
The pillar Materials are fairly expensive here, and the translucent volumetric sheets are **very** expensive. In this scene, I asked to have the translucent sheets should be removed, as they cost too much.



 | 

Here the pillars are quite expensive as they use all five texture lookups and do quite a bit of layering. Otherwise, this is just about efficient enough for 30fps.



 | 

Here, the tree is causing pixels to be **extremely** expensive. If the player could ever get up close or cover the screen with that Material, the cost would be enormous.



 |

## Mobile Content Scale Factor

**Mobile Content Scale Factor** is a way to scale the resolution of your project to best fit the screen resolution of the mobile device being used to view your project. You can [create and store multiple device profiles](/documentation/en-us/unreal-engine/setting-up-device-profiles-in-unreal-engine) by creating a new configuration (.ini) file called **DefaultDeviceProfiles.ini** in your project's config folder.

Inside of this file, you can specify what will happen to the resolution of your project for specific devices by entering the following command followed by one of the values from the iOS and Android sections below:

```
	`r.MobileContentScaleFactor`

Copy full snippet
```
r.MobileContentScaleFactor

In the following image, you can see an example of the Mobile Content Scale Factor being set in a configuration file:

Click for full image.

This particular configuration file is from the **Tappy Chicken** project and shows what will happen to the resolution of Tappy Chicken when it is played on various mobile devices. The top section of this file handles the resolution scaling for iOS devices and the bottom section handles resolution scaling for Android devices. Take note that each **r.MobileContentScaleFactor** has a number after it. The number is used after the command to determine if the project's resolution should be scaled up or down.

### Mobile Content Scale Factor for iOS

For iOS devices, inputting the following numbers will produce the following results:

The iOS scale factor is directly related to Apple's scale factor system and the actual resolution for any scale factor other than 0.0 will be corrected to match the aspect ratio of the screen and clamped to the native resolution of the device.

| Value | Result |
| --- | --- |
| **0.0** | This will use the native resolution of the device. |
| **1.0** | On a Retina device is the non-retina resolution. |
| **2.0** | Full native resolution on iPhone 5S, iPad Air, etc. |
| **3.0** | Full native resolution for iPhone 6+. |

### Mobile Content Scale Factor for Android

For Android devices, inputting the following numbers will produce the following results:

Please note that inputting values other than 0.0 will use this value as the scale factor for a standard 1280x720 or 720x1280 resolution depending on the orientation of the device.

| Value | Result |
| --- | --- |
| **0.0** | This will use the native resolution of the device. |
| **1.0** | This will try and give you a resolution of 1280 x 720 for Landscape and 720 x 1280 for portrait. |
| **2.0** | This will try and give you a resolution of 2560 x 1440 for Landscape and 1440 x 2560 for portrait. |

## Mobile Material Quality Settings

When building content for a UE project that will run on both low and high-end mobile devices, you will often run into issues where a feature or your artwork is working on one set of devices but not another. While there are a lot of ways to address issues like this, many of these are both time and resource intensive which can be error prone at times. To address these types of issues UE has the **Material Quality Level** system. This system enables you to build one single Material that can then be used on a wide range of devices, giving you full control over which devices use which features.

In the following sections, we'll cover these systems and how you can use them in your own UE projects:

### Previewing Material Quality Level

You can view what the different Material Quality Level settings will look like inside the Editor by going to the **Main Toolbar** and then then selecting **Settings** > **Material Quality Level** to choose the level you want to preview.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff87d657-0c64-4dd9-89bc-b51aba98a00e/08-mdv-perfom-material-preview.png)

The following images show what a Material will look like when the Material Quality Level has been set to Low, Medium, and High.

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6e86cd3-dbfb-439f-8429-1d78c46e0d90/23-mdv-perfom-mmq-1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ef7b074-3c5d-4529-91fa-019322703e21/24-mdv-perfom-mmq-2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbab93df-9fa3-4ed6-b29b-3fa3499735f6/25-mdv-perfom-mmq-3.png)

Dragging the slider will show what happens when changing the Material Quality Level from Low to Medium to High

### Setting Material Quality Level

To set the Material Quality Level for your devices, you can do so in the following ways:

##### From the Console

Bring up the console by hitting the **\`** (backtick) key and entering **r.MaterialQualityLevel** followed by one of the following values:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/787cf327-ef48-43fb-bc63-435c19cb1d59/09-mdv-perfom-command-line.png)

| Material Quality Level Number | Setting |
| --- | --- |
| **0** | Low |
| **1** | High |
| **2** | Medium |
| **3** | Epic |

Please note that 1 for high and 2 for medium is correct and not a typo.

##### From Device Profiles

Using a configuration (.ini) file, you can set the Material Quality for the devices you plan to target using the following method from within the Editor:

1.  From the **Main Toolbar** go to **Windows > Developer Tools** and then click on **Device Profiles**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a9faa9e-f902-4f3d-8133-6927949fdf68/10-mdv-perfom-device-profiles.png)
2.  In the **Device Profiles** find the **Android\_Low** profile and click on the first **Wrench** icon to open up the profile options.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8a95ccf-adff-4380-95b9-779f6e79680d/11-mdv-perfom-edit-profile.png)
3.  In the **Console Variables** section under the **Rendering** option, click on the **Plus** icon and in the input window that pops up, input **R.MaterialQualityLevel** and then press the **Enter** key to add that command to the list.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eea25720-eac4-4fd7-b8d5-47057b0f1a66/12-mdv-perfom-set-console-variables.png)
4.  Once the new entry has been added, change the value from the default value from **1** to **0** so that when this project is viewed on lower end Android devices it will use the fastest possible Material settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b858d10-b1af-433f-9361-e21f6e483aa3/13-mdv-perfom-set-quality-level.png)

### Previewing Different Quality Levels

By adjusting the **Preview Rendering Level**, you can use the Unreal Editor to see how your project will look when running on different hardware. You can adjust this by going to the **Main Toolbar** and then select **Settings > Preview Rendering Level** and select the preview level you want to use.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7371be47-9404-48ee-aeab-0ffd4e51620c/14-mdv-perfom-preview-rendering-level.png)

### Material Quality Level Switch

The **Quality Switch Material Expression** enables you to define different levels of complexity within a single Material. For example, if you have a complex math operation, or heavy texture reads that will work on higher-end mobile devices but not on lower-end ones. You can use this node to specify simplified versions to be displayed on lower-end mobile devices that do not have the power to display higher-end graphics.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c635dbc-c303-4d86-af63-a5e0bdab9b15/15-mdv-perfom-quality-switch-node.png)

To use the Quality Switch in your Materials, you will need to first add the Quality Switch Material Expression node to the **Material Graph** and then plug its output into any of the inputs on the Main Material node. In the following image, the **M\_Brick\_Clay\_Old Material** (that can be found in the Starter Content) is setup so that when the Quality Level is switched, the complexity of the Material will be reduced.

Click for full image.

### Mobile Material Options

If you open up any **Material** and click on the **Main Material Node** then look in the **Details** panel under the **Mobile** section you will find the following properties:

| Property | Setting |
| --- | --- |
| **Float Precision Mode** | How to use full **(highp)** presition in the pixel shader. **Highp** is slower than the default **(mediump)**, but can be used to work around precision-related rendering errors. Use **Full-Precision for MaterialExpressions Only** if you still want to keep the precisions of the halfs in .ush/.usf. This setting has no effect on older mobile devices that do not support high precision. |
| **Use Lightmap Directionality** | Uses lightmap directionality and per-pixel normals. If disabled, the lightmaps will be flatter looking visually but cheaper to use. |
| **Mobile High Quality BRDF** | Uses the high quality BRDF functions on mobile to get better visual effects but adds GPU cost. |
| **Use Alpha to Coverage** | Uses alpha to coverage for masked material on mobile, make sure MSAA is enabled as well. |

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f6a2e53-97b5-4e16-b6a4-9460844f2561/17-mdv-perfom-mobile-material-options.png)

Use these properties to help reduce the rendering cost of that Material when viewed on less powerful mobile devices by completely eliminating the rendering path for those features.

### Mobile Material Rendering Overrides

You can override the available rendering option a platform will use by adjusting the the Material Quality settings for different target devices located under the **Project Settings > Platforms**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b000ee40-a92f-4744-b17a-72cd150a26a5/18-mdv-perfom-materia-quality-levels.png)

You can override the available rendering option a platform will use by adjusting the **Quality Options** listed. In order to use the overrides, you must first click on the **Enable Quality Overrides** option and then select the option you want to override for a given Quality Level.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05584015-1920-43cc-8e92-6a46cf563d06/19-mdv-perfom-enable-quality-level-overrides.png)

Once all of the options you want have been selected, press the **Update Preview Shaders** button to recompile all the Materials to work with the options specified.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3de10899-cb7b-4df8-a16a-a1cee71fc380/20-mdv-perfom-quality-levels-update-shaders.png)

## Mobile Rendering Options

Inside of your **Project's Settings** menu under the **Rendering** section, you will find a number of properties that control how lighting and optimization will be handled inside of your mobile project. In the following sections we will take a look at these settings and what effect they will have on your project.

### Accessing your Project's Settings

Once the **Project Settings** menu is open, locate the **Engine** section and then click on the **Rendering** category. Use the following sections to adjust the settings below:

-   **Mobile**
-   **Misc Lightning**
-   **VR**
-   **Mobile Shader Permutation Reduction**

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/384df493-6597-418b-bb3a-a2f03cb0601b/21-mdv-perfom-project-settings-rendering.png)

### Mobile and VR Rendering Options

Under the **Mobile** and **VR** category, you can set properties that directly affect the lighting and look of your mobile project. Read on below to explore these settings for your own projects.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4df04084-e966-4eeb-b875-ad56c4e5d926/22-mdv-perfom-mob-vr-rendering-settings.png)

| Property Name | Description |
| --- | --- |
| **Mobile** | 
The listed options found under the **Mobile** section of the Project Settings that should be adjusted for mobile performance.

-   **Disable Vertex Fogging in mobile shaders**: If true, vertex fog will be omitted from all mobile shaders. If your game does not use fog, you should choose this setting to increase shading performance.
-   **Maximum number of CSM cascades to render**: The maximum number of cascades with which to render dynamic directional light shadows when using the mobile renderer.
-   **Mobile Anti-Aliasing Method**: This is the Multi-Sample Anti-Aliasing (MSAA) setting to use on mobile. If MSAA is not available, the current default AA method will be used.



 |
| **VR** | 

The listed options found under the **VR** section of the Project Settings that should be adjusted for mobile performance.

-   **Mobile HDR**: If true, mobile renders in full HDR. Disable this setting for games that do not require lighting features for better performance on slow devices.



 |

## Misc Lighting and Shader Permutation Reduction Settings for Mobile

Under the **Misc Lighting** and **Mobile Shader Permutation Reduction** section, you will find a number of different option that can be enabled or disabled to effect shaders generated for Materials, which in-turn will reduce app size, save memory and improve load times.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0cc20da-cadb-4fa4-9dea-e301d0d282ef/26-mdv-perfom-light-shader-rend-set.png)

| Property Name | Description |
| --- | --- |
| **Misc Lighting** | 
The listed options found under the **Misc Lighting** section of the Project Settings that should be adjusted for mobile performance.

-   **Allow Static Lighting**: Whether to allow any static lighting to be generated and used, like lightmaps and shadow maps. Games that only use dynamic lighting or that are unlit should set this to 0 to save some static lighting overhead.



 |
| **Mobile Shader Permutation Reduction** | 

The listed options found under **Mobile Shader Permutation Reduction** that should be adjusted for mobile performance.

-   **Support Combined Static and CSM Shadowing**: Allows primitives to receive both static and CSM shadows from a stationary light. Disabling will free a mobile texture sampler and reduce shader permutation.
-   **Support CSM on levels with Force No Precomputed Lighting enabled**: When Allow Static Lighting is enabled, shaders to support CSM without any precomputed lighting are not normally generated. This setting allows CSM for this case at the cost of extra shader permutations.
-   **Support Pre-baked Distance Field Shadow Maps**: Generates shaders for static primitives render Lightmass-baked distance field shadow maps from stationary directional lights.
-   **Support Movable Directional Light**: Generates shaders for primitives to receive movable directional lights.
-   **Max Movable Point Lights**: The number of dynamic spotlights or point lights to support on mobile devices. Setting this to 0 for games which do not require dynamic spotlights or point lights will reduce the number of shaders generated.
-   **Support Movable Spotlights**: Generates shaders for primitives to receive lighting from movable spotlights. This incurs an additional cost when processing movable lights.



 |

Changing any of these settings will require you to restart the editor before they take effect.

If you disable a shader permutation that your lighting setup requires, your lighting or shadowing will not render correctly and there will be an on-screen message indicating the setting that needs to be re-enabled for it to work properly.

## Additional Suggestions

The following suggestions will help to set up your content for optimal performance on mobile platforms. These are listed from most severe to least impactful.

-   Make sure lighting is built before running on a device.
-   Most Post Processing features are disabled for mobile platforms as they are too expensive, like vignette or screen space reflections. Some GPU intensive features like **Bloom** and **Depth of Field** are enabled by default so that PC and mobile look the same but many features can cost 60 milliseconds or more with the default settings on some devices. The console command **showflag.PostProcessing 0** can be used to turn off these features to get a general idea of their costs.
-   Make sure to use **Precomputed Visibility** and that it is set up properly. To do this, place **Precomputed Visibility Volumes** around areas where the player can walk or jump and then build lighting. You need to make sure to place these in the **Persistent Level** that is used when building lighting and when running the game, so do not build a **Sublevel** by itself. You can verify that **Precomputed Visibility** is working by entering the console command **Stat Initviews** on device or in the **Level Previewer** and making sure that **Statically Occluded Primitives** is greater than 0. Use the console command **r.ShowPrecomputedVisibilityCells 1** to visualize the cells in the Editor.
-   Use masked and transparent Materials sparingly. Only use them in places where they cover a small part of the screen. iOS devices are very optimal in shading opaque surfaces, as they will only shade each pixel once, but for masked and translucency, every single layer will have to be shaded. The total GPU time of a frame can be doubled or more by having overdraw. Use the **Shader Complexity** view mode to investigate any hot spots.
-   Draw calls of the entire scene should be <=700 for any single view. Areas with poor occlusion, like looking over a large landscape, is going to be biggest challenges for this. This can be seen with **Stat OpenGLRHI** on device or **Stat D3D11RHI** in the **Previewer** on PC.
-   Triangle count of the entire scene should be <=500k for any view. This has been determined to be the maximum poly count that can hit 30fps on both iPad4 and iPad Air. This can be seen with **Stat OpenGLRHI** on device or **Stat D3D11RHI** in the **Previewer** on PC.
-   Materials should use as few texture lookups and instructions as possible. You have five texture samplers available, but using all of those makes for a fairly expensive Materials. For now, use the PC instruction count to optimize and the **Previewer Shader Complexity** to visualize the total cost.
-   Only use independent texture fetches in Materials. This means UVs in the pixel shader (**BaseColor**, **Roughness**, and so on.) must not be manipulated in any way, such as **Scaling**. Use the **CustomizedUVs** feature instead to do the **Scaling** in the **Vertex Shader**. Some special features like environment mapping require math on the UVs and that is OK for special cases.
-   It is recommended to use square textures as they have less memory waste. Always use power of two dimensions for these (256x256, 512x512, 1024x1024). Use the console command **ListTextures** in the **Previewer** to see where all the texture memory is going.