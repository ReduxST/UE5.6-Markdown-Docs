# Volumetric Cloud Component Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-properties-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-properties-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:40

---

This page includes reference information for the Volumetric Cloud, Material expressions, and Light component properties.

## Volumetric Cloud Component

The following properties can be found on the **Volumetric Cloud** component through the **Details** panel when it is placed in a level. The properties found in this component enable you to define the physical attributes of the cloud placed in your Level, such as its distance from the surface of the planet, how tall the cloud volume is, the quality of the ray-marched clouds, and more.

![Volumetric Cloud Component properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43f2c9b5-3456-4bd6-872a-2fea874fbd7a/01-volumetric-cloud-component-properties.png)

| Property | Description |
| --- | --- |
| Layer |   |
| **Layer Bottom** | The altitude at which the cloud layer should start, measured in kilometers (km) above the ground. |
| **Layer Height** | The altitude at which the cloud layer should end, measured in kilometers (km) above the ground. |
| **Tracing Start Max Distance** | The maximum distance of the volumetric surface before which we will accept to start tracing, measured in kilometers (km). |
| **Tracing Max Distance Mode** | 
Select the mode to control how the tracing max distance should be interpreted. Options are:

-   **Distance from Point of View**
-   **Distance from Cloud Layer Entry Point**



 |
| **Tracing Max Distance** | The maximum distance that will be traced inside the cloud layer, measured in kilometers (km). |
| Planet |   |
| **Planet Radius** | The planet radius used when there is not a [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) component present in the scene. |
| **Ground Albedo** | The ground albedo color used to light the cloud from below with respect to the sun light and the Sky Atmosphere. This is only used by the cloud material when the **Volumetric Advanced Material Output** node has **Ground Contribution** enabled in its Details panel. (See the Material Expressions section of this page.) |
| Cloud Material |   |
| **Material** | The material assigned that describes the cloud volume. It must be a material that uses the **Volume** Material Domain. |
| Cloud Tracing |   |
| **Use Per Sample Atmospheric Light Transmittance** | Whether to apply atmosphere transmittance per sample instead of using the light global transmittance. |
| **Sky Light Cloud Bottom Occlusion** | Occlusion amount applied to the Sky Light contribution at the bottom of the cloud layer. This is a fast approximation to sky lighting being occluded by clouds without having to trace rays or sample an ambient occlusion (AO) texture. |
| **View Sample Count Scale** | The scale of the view tracing sample count. The quality level scalability console variables affect the maximum range. The sample count resolution is clamped according to the scalability setting of `r.VolumetricCloud.ViewRaySampleCountMax`. |
| **Reflection Sample Count Scale** | The scale of the reflection tracing sample count. The quality level scalability console variables affect the maximum range. The sample count resolution is clamped according to the scalability setting of `r.VolumetricCloud.ReflectionRaySampleMaxCount`. |
| **Shadow View Sample Count Scale** | The scale of the shadow view tracing sample count. The quality level scalability console variables affect the maximum range. The sample count resolution is clamped according to the scalability setting of `r.VolumetricCloud.Shadow.ViewRaySampleMaxCount`. |
| **Shadow Reflection Sample Count Scale** | The scale of the shadow reflection view tracing sample count. The quality level scalability console variables affect the maximum range. The sample count resolution is clamped according to the scalability setting of `r.VolumetricCloud.Shadow.ReflectionRaySampleMaxCount`. |
| **Shadow Tracing Distance** | The shadow tracing distance measured in kilometers (km). |
| **Stop Tracing Transmittance Threshold** | When the mean transmittance is below this threshold, we stop tracing. This is a good way to reduce the ray marched sample count, and thus increase performance. |

## Material Expressions

The following Material Expressions can be added to your Material Graph to define attributes of your volumetric clouds.

### Volumetric Advanced Material Output Expression

The **Volumetric Advanced Material Output** expression provides control over a set of cloud parameters that affect the volume material applied to the Volumetric Cloud component when added to a material graph. It also provides additional cloud properties from the Material Editor Details panel when selected (see below).

![Volumetric Advanced Material Output Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/153fc572-72c5-4362-9fff-015ec2e1177e/02-material-vol-adv-output-expression.png)

| Property | Description |
| --- | --- |
| Phase |   |
| **Phase G** | The parameter **G** input to the phase function describes how much forward (g < 0) or backward (g > 0) light scatters around. A valid range would be between -1.0 and 1.0. Defaults to 0 when no amount is specified. It is evaluated per sample if **Per Sample Phase Evaluation** is enabled. |
| **Phase G2** | The parameter **G2** input to the second phase function describes how much forward (g < 0) or backward (g > 0) light scatters around. A valid range would be between -1.0 and 1.0. Defaults to 0 when no amount is specified. It is evaluated per sample if **Per Sample Phase Evaluation** is enabled. |
| **Phase Blend** | The linear interpolation (lerp) factor is used when blending the two phase functions parameterized by **G** and **G2**. A valid range is between 0.0 and 1.0. Defaults to 0 when no amount is specified. It is evaluated per sample if **Per Sample Phase Evaluation** is enabled. |
| **Multi Scattering Contribution** | Represents how much contribution each successive octave will add to the multiple-scattering. It is evaluated per pixel, and a valid range is between 0.0 and 1.0 from low to high contribution. Defaults to 0.5 contribution if no value is specified. |
| **Multi Scattering Occlusion** | Represents how much occlusion will be reduced for each successive octave. It is evaluated per pixel, and a valid range is between 0.0 and 1.0 from low to high occlusion. Defaults to 0.5 occlusion if no value is specified. |
| **Multi Scattering Eccentricity** | Represents how much the phase will become isotropic for each successive octave. It is evaluated per pixel, and a valid range is between 0.0 and 1.0 from anisotropic to isotropic. Defaults to 0.5 scattering eccentricity if no value is specified. |
| **Conservative Density** | 
Represents a three component float vector (Vector3). The X component must represent the participating medium conservative density. If the value is greater than 0, the material will be evaluated and will evaluate the next sample directly. This optimization is used to accelerate ray marching by skipping expensive material evaluation early on. The Y and Z components (of the Vector3) are used to pass extra data with the conservative density to the material evaluation step, which avoids computing it again.

For example, a simple top down 2D density texture would be enough to help by not evaluating the material in empty regions. The Y and Z components can contain parameters that can be recovered during the material evaluation using the **Volumetric Advanced Material Input** node. This attribute is evaluated per pixel.



 |

When selected, the Material Editor **Details** provides additional properties that can be set for any cloud material using this material. It enables you to directly set **Phase** and **Multi-Scattering** values that aren't parameterized. You can control the number of octave approximations used to simulate the multiple scattering effect of light, apply contribution of ground lighting to the bottom of the cloud layer, and more.

![Volumetric advanced material output node properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/488f218a-8934-40a7-8bc1-be370c1f7667/03-material-vol-adv-output-node-properties.png)

| Property | Description |
| --- | --- |
| Phase |   |
| **Per Sample Phase Evaluation** | Enable this option to force the phase function to be evaluated per sample, instead of once per pixel (globally). Per sample evaluation is slower. |
| Multi-Scattering |   |
| **Multi Scattering Approximation Octave Count** | How many octaves to use for the multiple-scattering approximation. This increases the cost of the shader, so it's best to use a single octave. 0 means single scattering only. |
| Options |   |
| **Ground Contribution** | Sample the shadowed lighting contribution from the ground onto the medium (single scattering). This adds some costs to the tracing when enabled. |
| **Gray Scale Material** | Sets this material to only be considered for gray scale, only using the R channel of the input parameters internally. The lighting will still be colored. This is an optimization. |
| **Ray March Volume Shadow** | Disable this to use the cloud shadow map instead of secondary ray marching. This is usually enough for clouds views from the ground and it should result in a performance boost. Shadows now have infinite length but also become less accurate and gray scale. |
| **Clamp Multi Scattering Contribution** | Sets whether multiple scattering contribution entry is clamped in \[0,1\] or not. When disabled, the artist is in charge of ensuring the visual remain in a reasonable brightness range. |

## Atmosphere Lights and Sky Light

Atmospheric lights contribute to rendering of the volumetric clouds in your scene with properties that define their lighting in static and dynamic time-of-day scenes.

### Directional Light

The Volumetric Cloud component supports lighting from up to two [Directional Light](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine) sources, such as a moon and sun, or two suns. The Directional Light provides lighting and shadowing for clouds and opaque objects onto clouds. It also enables you to specify the strength, extent, and resolution of the shadows of clouds in your scene.

![Directional Light Atmosphere and Cloud properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1547fd34-8d01-452e-bc41-e0b44e13ced6/04-directional-light-cloud-atmosphere-properties.png)

| Property | Description |
| --- | --- |
| Atmosphere and Cloud |   |
| **Atmosphere Sun Light** | Whether the Directional Light can interact with the atmosphere, clouds and generate a visual sun disk, all of which compose the visual sky. |
| **Cast Shadows on Clouds** | Whether the light should cast any shadows from opaque meshes onto clouds. This is disabled for any secondary Directional Lights that have **Atmosphere Sun Light** enabled and set to **Atmosphere Sun Light Index** of 1, such as another sun or as a moon light. |
| **Cast Shadows on Atmosphere** | Whether the light should cast any shadows from opaque meshes into the atmosphere when a SkyAtmosphere is used. |
| **Cast Cloud Shadows** | Whether the light should cast any shadows from the clouds onto the atmosphere and other scene elements. |
| **Cloud Scattering Luminance Scale** | Scales the light contribution when scattered in cloud participating media. This can help counter balance the fact that our current multiple scattering solution is only an approximation. |
| Advanced Properties |   |
| **Per Pixel Atmosphere Transmittance** | Whether to apply atmosphere transmittance per pixel on opaque meshes instead of using the light's global transmittance. |
| **Cloud Shadow Strength** | The strength of the shadow. Higher values will block more light. |
| **Cloud Shadow on Atmosphere Strength** | The strength of shadows on the atmosphere. When set to 0, shadows on the atmosphere is disabled. |
| **Cloud Shadow on Surface Strength** | The strength of shadows on opaque and transparent meshes. When set to 0, shadows on opaque and translucent surfaces is disabled. |
| **Cloud Shadow Depth Bias** | Controls the bias applied to the front shadow depth of the volumetric cloud shadow map. |
| **Cloud Shadow Extent** | The world space radius of the cloud shadow map around the camera. Measured in kilometers (km). |
| **Cloud Shadow Map Resolution Scale** | Scales the cloud shadow map resolution. The resolution is clamped by `r.VolumetricCloud.ShadowMap.MaxResolution`. |
| **Cloud Shadow Ray Sample Count Scale** | Scales the number of samples used for shadow map tracing. The sample count resolution is clamped with `r.VolumetricCloud.ShadowMap.RaySampleMaxCount`. |

### Sky Light

The [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) component provides soft ambient shadowing support that can be enabled and controlled with the following properties.

![Sky Light Atmosphere and Cloud properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2be340e5-b8d9-40d2-836d-55e7a20003f4/05-sky-light-cloud-atmosphere-properties.png)

| Property | Description |
| --- | --- |
| Atmosphere and Cloud |   |
| **Cloud Ambient Occlusion** | Whether the cloud should occlude sky contribution within the atmosphere (progressively fading out multiple scattering) or not. |
| **Cloud Ambient Occlusion Strength** | The strength of the ambient occlusion. Higher values will block more light. |
| **Cloud Ambient Occlusion Extent** | The world space radius of the cloud ambient occlusion map around the camera in kilometers (km). |
| **Cloud Ambient Occlusion Map Resolution Scale** | Scales the cloud ambient occlusion map resolution. The resolution is clamped by `r.VolumetricCloud.ShadowMap.MaxResolution`. |
| **Cloud Ambient Occlusion Aperture Scale** | Controls the cone aperture angle over which the sky occlusion due to volumetric clouds is evaluated. A value of 1 takes the entire hemisphere into account, resulting in blurry occlusion. A value of 0 takes a single direction of occlusion (vertical) into account, resulting in sharp occlusion. |