# Volumetric Cloud Material

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-material-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-material-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:42

---

The [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) component is driven by a volume material. This volumetric cloud material includes parameters in named categories that are simple, clear, and easy to understand when defining the types and shapes of clouds you want, and making them look like storm clouds.

## Recommended Workflow with the Volumetric Cloud Material

The material used for rendering clouds with the volumetric cloud component is located in the Engine Content folder under `Engine/EngineSky/VolumetricClouds`. The material is named `m_SimpleVolumetricCloud_Inst` and is derived from `m_SimpleVolumetricClouds`.

Making changes to any content in the Engine Content folder directly has an effect on any projects and components that references this material. For this reason, we strongly recommend you make material instances of this material in your project’s Content folder. This way, you can make many variations to support different cloud types and shapes without overwriting the original material that is used by default.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8893728c-e766-40e0-9e72-89382b556a76/vcm-scene.png)

Default look and location of Volumetric Cloud Shader in Blank Game Template.

## Cloud Material Instance Settings

When you open the Volumetric Cloud material instance or create one of your own from the original, you will find the parameters are grouped into categories that define the look, shape, and effects of different clouds.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/552eacd1-5631-4fc1-9bac-eef8982ca2c8/vcm-materialinstanceparameters.png)

Volumetric cloud parameter groups in a material instance.

### Cloud Layout

The **Cloud Layouts** parameters are broken into textures and cloud types. The textures define the shapes, location, and mask for the cloud material and parameters to control the different types of clouds.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83ec7821-ec20-415f-b797-784c4ae5eab6/vcm-cloudlayout.gif)

Volumetric Cloud Shader Layout Parameters.

The cloud type parameters use color channels to align with different types of cloud formations. There are four types of cloud types aligned with the red, green, blue, and alpha channels of the cloud textures. These cloud types are:

|   |   |   |   |
| --- | --- | --- | --- |
| 
 | 

 | 

 | 

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23ad26ad-311c-4c98-916c-e3ed186f9f91/example-nimbo-half.gif)

 |
| Stratocumulus | Altostratus | Cirrostratus | Nimbostratus (Storm) |

The Cloud Type section has the following settings:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35fa69ed-1ba8-4e03-9252-9bfedaf1b520/vcm-cloudlayout-parameters.png)

| Property | Description |
| --- | --- |
| Cloud Type Textures |   |
| **Layout\_CloudHeightProfile** | This texture describes the shape of the clouds as the altitude changes. Each channel of this texture describes the profile shape and relative altitude of a different cloud type, where R (red) is Stratocumulus, G (green) is Altostratus, B (blue) is Cirrostratus, and A (alpha) is Nimbostratus. |
| **Layout\_CloudGlobalPattern** | This texture defines the world location for each type of cloud where each channel describes a different cloud type. The channels represent the following: R (red) is Stratocumulus, G (green) is Altostratus, B (blue) is Cirrostratus, and A (alpha) is Nimbostratus. |
| **Layout\_GlobalCloudMask** | This texture is used to add clouds to or remove clouds from the global pattern texture (Layout\_CloudGlobalPattern) in the masked region. Each channel of this texture applies to a different cloud type where R (red) is Stratocumulus, G (green) is Altostratus, B (blue) is Cirrostratus, and A (alpha) is Nimbostratus. |
| Cloud Type Parameters |   |
| **Layout\_CloudType** | These parameters control the visibility for each different cloud type individually, where R (red) is Stratocumulus, G (green) is Altostratus, B (blue) is Cirrostratus, and A (alpha) is Nimbostratus. |
| **Layout\_CloudGlobalScale** | These parameters control the distance over which the layout region textures (Layout\_GlobalCloudMask and Layout\_CloudGlobalPattern) repeat. This is measured in kilometers (km). |
| **Layout\_CloudPerTypeScale** | These parameters control the scale of the cloud global pattern (Layout\_CloudGlobalPattern) texture for each of the cloud types, where R (red) is Stratocumulus, G (green) is Altostratus, B (blue) is Cirrostratus, and A (alpha) is Nimbostratus. |
| **Layout\_GlobalTexturePlacement** | This vector controls the offset and rotation (around the world Z axis) of the layout region textures (Layout\_GlobalCloudMask and Layout\_GlobalCloudPattern). |
| **Layout\_WindControls** | This vector controls the strength of the wind along each world axis (x, y, or z), where the value for each can be positive or negative. The Alpha channel can be used to uniformly increase or decrease the strength of the wind. |
| **Layout\_CloudTypeMask** | These parameters specify how strongly the global cloud mask (Layout\_GlobalCloudMask) texture affects each of the cloud types, where R (red) is Stratocumulus, G (green) is Altostratus, and B (blue) is Cirrostratus. The MaskContribution (or alpha channel) sets the overall strength of the effect. |
| **Layout\_GlobalCoverage** | These parameters determine the overall amount of cloud cover to apply, where positive values increase cloud cover and negative values decrease the amount of cloud cover. |

### Cloud Shape

The **Cloud Shape** parameters are useful for defining a general cloud shape and color using a noise volume texture. In this section, there are three separate noise samplers available, each with their own controls.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90cd0329-9e8b-4ace-893d-bcaadc936b25/vcm-cloudshape.gif)

Volumetric Cloud Shader Shape Parameters.

The Cloud Shape section has the following settings:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/873d3a43-013f-4241-86e6-8615de593c57/vcm-cloudshape-parameters.png)

| Property | Description |
| --- | --- |
| **Noise\_Texture3D** | This texture is used to break up the shapes of the clouds for authoring their general form. Each color channel of the texture describes a different noise pattern where the influence of each is determined by the Noise controls. The alpha channel of this texture is unused. |
| **UseNoise3** | This toggle enables the use of a third sample of the Noise\_Texture3D in order to break up the cloud shapes with an additional level of detail (or a different method of break up). This adds Noise3\_Coordinates and Noise3\_MultiChannel parameters. |
| **Noise\_Bias** | Each parameter in this set is subtracted from the respective NoiseTexture sample, which can have positive or negative values. This determines how the noise texture dilates or erodes the Cloud Layout without increasing the overall contrast of the noise. |
| **Noise\_Strength** | Each parameter in this set is multiplied against the respective result of the biased Noise Texture sample, which can be positive or negative values. This increases or decreases the contrast of the noise and thus increases the apparent strength of the noise effect on the Cloud Layout. |
| **Noise1\_Coordinates** | This parameter controls both the scale of the green channel of the Noise Texture as well as how strong an effect Wind Velocity has on this noise sample. Noise1 controls the primary breakup noise for the clouds. |
| **Noise2\_Coordinates** | This parameter controls both the scale of the red channel of the Noise Texture as well as how strong an effect Wind Velocity has on this noise sample. Noise2 controls the amount and scale of distortion for Noise1. |
| **Noise3\_Coordinates** | When UseNoise3 is enabled, this parameter controls both the scale of the blue channel of the Noise Texture as well as how strong an effect Wind Velocity has on this noise sample. Noise3 is added to Noise1 as an additional level of detail. Noise3 includes an additional control (Multichannel) which is used to modulate the existing noise by any combination of Noise Texture channels. |
| **Noise2\_MultiChannel** | When UseNoise3 is enabled, this parameter controls the multiplicative contribution to the overall cloud noise of each of the channels, as well as the total magnitude of the multiplicative effect (using the alpha channel). This means the cloud noise is multiplied by a factor determined by this formula. MultiChannel A *(Noise R + MultiChannel R + Noise G* MultiChannel G + Noise B \* MultiChannel B). |
| **Cloud\_AlbedoColor** | This is the color of the clouds when they are not considered storm clouds. The Ambient Occlusion (alpha channel) of this parameter determines the strength of light occlusion for the material (and consequently how dense the shadows appear). |
| **Cloud\_GlobalDensity** | This parameter controls the overall density of the cloud material, rendering them more opaque at higher values or hazier at lower values. |

### Storm

The **Storm** parameters are necessary settings useful for making a cloud system look like a storm in formation and color. Enabling this section of settings uses the Nimbostratus layer of the material.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10f12bee-7aeb-444e-aac4-26736a0a087c/vcm-storm.gif)

Volumetric Cloud Shader Storm Parameters.

The Storm section has the following settings:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd6941fa-625c-41e0-b152-070dcf24844d/vcm-storm-parameters.png)

| Property | Description |
| --- | --- |
| **Storm\_Clouds** | This value controls the strength of the blend from normal clouds to storm clouds, which have additional controls for albedo, occlusion, distortion, and optional lightning effects. |
| **Storm\_LightningTexScale** | This value controls the relative scale of the lightning texture. This texture is used to determine the location of lightning flashes in the material. |
| **Storm\_LightningAnim** | These parameters control the animation of the lightning in the material. The lighting flicker adds a secondary animation to the flashes. Dynamic lightning animation is used to determine the frequency of lightning flashes, such that the higher the value, the more frequently the flashes occur. Manual lightning is intended to be used when Dynamic Lighting is set to 0. This will let you decide the state of the flashes independently of time (which is mostly useful when rendering still images or when manually updating time in a Sequence). |
| **Storm\_LightningClouds** | 
These parameters control the effect of lightning on the clouds.

-   **Source Power** controls the intensity of the core of the lightning strike.
-   **Fill Scatter** controls the distance the lightning scatters in the clouds.
-   **Fill Scatter Intensity** controls the brightness of the scattered light in the clouds.
-   **Second Mip Level** controls the sharpness of the details contributed by the second lightning texture sample (where higher values are sharper).



 |
| **Storm\_LightningColor** | These parameters control the color (RGB values) and brightness (alpha value) of the lightning flashes. |
| **Storm\_LightningMask** | 

These parameters control how the lightning texture is masked in the material.

-   **Lightning Mask Bias** determines at what positions in the cloud layout texture alpha channel lightning can appear.
-   **Lighting Mask Strength** is multiplied against the bias result to compensate for lightning masks which are either too opaque or too transparent.
-   **Cloud Texture Weight** determines the influence of the noise texture results on the lighting mask, where higher values increase the influence of the texture.



 |
| **Storm\_AlbedoColor** | Sets the color of clouds when they are considered storm clouds. The alpha channel determines the multiplicative factor for the shadow density, with lower values resulting in darker shadows. |

### Multiscatter

The **Multiscatter** parameters are a set of controls for how light scatters in the cloud material.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d088436-6359-4272-a087-30d34a11e0e9/vcm-multiscatter.gif)

Volumetric Cloud Multiscatter Parameters.

The Multiscatter section has the following settings:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27951879-f329-4954-bd36-7cb7fd62e9e0/vcm-multiscatter-parameters.png)

| Property | Description |
| --- | --- |
| **Phase\_Controls** | 
The cloud scattering uses a combination of two phase functions to determine how light bounces in the material.

-   **Phase A** and **Phase B** determine the directionality of light scattering in the clouds. Positive values scatter forward, away from the source. Negative values scatter backward, towards the source. These can be defined in the range of -1 to 1.
-   **Phase Blend** determines how strong the contribution of each phase is, where 0 is entirely Phase A and 1 is entirely Phase B.



 |
| **Multiscatter\_Controls** | 

These parameters control the multiscattering approximations in the cloud material. Each value below has a valid range from 0 to 1.

-   **Intensity** controls the overall strength of the effect.
-   **Occlusion** determines how strongly light is attenuated.
-   **Eccentricity** determines how uniform the scattering is.



 |

## Additional Notes

### Upgrade Notes from Unreal Engine 5.4 and earlier to 5.5 and later

With Unreal Engine 5.5, the volumetric cloud material that is assigned by default to Volumetric Cloud components and used with plugins, like the Sun Position Calculator, has been updated with a new material. Because this material replaces the original one entirely, all template projects and projects that used it are updated automatically when opened in Unreal Engine 5.5 or later versions of the engine.

It is expected that some projects may look different or have trouble locating this resource when updated. If your project depends on the original material, the simplest solution is to migrate the original material to your current version of the engine.

#### Migrating and Redirecting Materials

You can move the original material from Unreal Engine 5.4 to any later version of the engine by following the steps for [Migrating Assets](/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine).

For content like the [Sun Position Calculator](/documentation/en-us/unreal-engine/geographically-accurate-sun-positioning-tool-in-unreal-engine) plugin, you only need to redirect the material to its location in the engine content folder, which can be found here: **Engine > Content > EngineSky > VolumetricClouds**.

#### Engine Content Original Volumetric Clouds Textures

The Engine Content folder where the volumetric cloud material is saved also includes all the assets needed to make the material. In this folder, you’ll find new textures and assets that work with the updated volumetric cloud material. You will also find the original textures and volume textures in order to permit their reuse with the original material if you were to migrate it from Unreal Engine 5.4.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b745d662-38c4-45b5-956e-0dabcc068363/vcm-enginecontent.png)