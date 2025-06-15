# Sky Atmosphere Component Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-atmosphere-component-properties-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-atmosphere-component-properties-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:58

---

This page includes reference information for the Sky Atmosphere system. It includes information about Project Settings, component properties, console commands and the SkyAtmosphere Material Expressions.

## Project Settings

The following Project Settings are used to affect the Sky Atmosphere component in your project.

![Sky Atmosphere in Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/953fcd7c-10b7-4eea-adb3-f194ebd48f43/01-sky-atmosphere-project-settings.png)

| Property | Description |
| --- | --- |
| **Support Sky Atmosphere** | The Sky Atmosphere component requires extra samplers/textures in order to be bound to apply aerial perspective on transparent surfaces (and all surfaces on mobile via per-vertex evaluation). |
| **Support Sky Atmosphere Affecting Height Fog** | The Sky Atmosphere component can light up the height fog but it requires extra samplers/textures to be bound to apply aerial perspective on transparent surfaces (and all surfaces on mobile via per-vertex evaluation). It reuires that **Support Sky Atmosphere** be enabled. |

## Sky Atmosphere Properties

The following settings can be found on the Sky Atmosphere component in the Level Details panel.

![Sky Atmosphere Properties in the Level Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7ba2d83-580d-4419-a776-38804e64618e/02-sky-atmosphere-component-settings.png)

| Property | Description |
| --- | --- |
| Planet |   |
| **Transform Mode** | 
Choose how the Sky Atmosphere component's transform placement and movement in the level. Choose one of the following from the dropdown menu:

-   **Planet Top at Absolute World Origin:** Places the top ground level of the atmosphere at the world origin coordinates (0,0,0) in the scene. The Sky Atmosphere is not movable when this option is selected.
-   **Planet Top at Component Transform:** Places the top ground level of the atmosphere relative to the component's transform origin. Moving the transform of the Sky Atmosphere component, or one that it is a child of, moves the atmosphere within the level.
-   **Planet Center at Component Transform:** Places the atmosphere centered to the component's transform origin. Moving the transform of the Sky Atmosphere component, or one that it is a child of, moves the atmosphere within the level.



 |
| **Ground Radius** | The planet radius measured in kilometers from the center to the ground level. |
| **Ground Albedo** | The ground albedo that tints the atmosphere when the sun light bounces on it. This is only taken into account when **MultiScattering** is greater than 0. |
| Atmosphere |   |
| **Atmosphere Height** | The height of the atmosphere above the ground surface, measured in kilometers. |
| **MultiScattering** | Render multi-scattering as if sun light bounces around in the atmosphere. It is achieved using dual scattering approach. |
| **Trace Sample Count Scale** | The scale of the Atmosphere tracing sample count. |
| Atmosphere — Rayleigh |   |
| **Rayleigh Scattering Scale** | Rayleigh scattering coefficient angle. |
| **Rayleigh Scattering** | The Rayleigh scattering coeffecients resulting from molecules in the air at an altitude of 0 kilometers. |
| **Rayleigh Exponential Distribution** | The altitude in kilometers at which Rayleigh scattering effect is reduced to 40%. |
| Atmosphere — Mie |   |
| **Mie Scattering Scale** | Mie scattering coefficient scale. |
| **Mie Scattering** | The Mie scattering coefficients resulting from particles in the air at an altitude of 0 kilometers. Light is scattered more as it increases. |
| **Mie Scattering Absorption** | Mie absorption coefficient scale. |
| **Mie Absorption** | The Mie absorption coefficients resulting from particles in the air at an altitude of 0 kilometers. Light is absorbed more as it increases. |
| **Mie Anisotropy** | A value of 0 means light is uniformly scattered. A value closer to 1 means light will scatter more forward, resulting in halos around light sources. |
| **Mie Exponential Distribution** | The altitude in kilometers at which Mie effects are reduced to 40%. |
| Atmosphere — Absorption |   |
| **Absorption Scale** | Absorption coefficients for another atmosphere layer. Density increase from 0 to 1 between 10 to 25 kilometers and decreases from 1 to 0 between 25 to 40 kilometers. This approximates ozone molecule distribution in the Earth atmosphere. |
| **Absorption** | Absorption coefficients for another atmosphere layer. Density increases from 0 to 1 between 10 to 25 kilometers and decreases from 1 to 0 between 25 to 40 kilometers. The default values represent ozone molecules absorption in the Earth atmosphere. |
| **Tent** | 

Represents the altitude-based tent distribution of absorption particles in the atmosphere.

-   **Tip Altitude:** The altitude at which the tent function reaches its peak.
-   **Tip Value:** The density at the tent tip altitude.
-   **Width:** The width, or variation of altitude, over which the tent function linearly decreases to reach 0.



 |
| Art Direction |   |
| **Sky Luminance Factor** | Scales the luminance of pixels representing the sky. For example, not belonging to any surface. |
| **Aerial Perspective Distance Scale** | Makes the aerial perspective look thicker by scaling distances from view to surfaces (opaque and translucent). |
| **Height Fog Contribution** | Scale the sky and atmosphere lights contribution to the height fog when **Support Sky Atmosphere Affects Height Fog** is enabled in the Project Settings. |
| **Transmittance Min Light Elevation Angle** | The minimum elevation angle in degrees that should be used to evaluate the sun transmittance to the ground. Useful to maintain a visible sun light and show on meshes even when the sun has started going below the horizon. This does not affect the aerial perspective. |
| **Aerial Perspective Start Depth** | The distance in kilometers at which to start evaluating the aerial perspective. By default is set to 100 meters. |

## Sky Atmosphere Material Expressions

The following Material Expressions are used when creating a sky material where you want to compose the sky, sun disk, clouds, and aerial perspective. Computing the lighting on the clouds and other elements in the sky is assisted with these expressions.

To explore a working example using these expressions within a material that are applied to a skydome mesh, see the **TimeOfDay\_default** map found in the `Engine/Content/Maps/Templates` folder.

Click image for full size.

Also, for additional details, see the "Rendering a Skydome Mesh" section of the [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) page.

The shape of the skydome mesh is important when using some of these expressions since they will drive evaluation of those values. For example, if you use the functions to evaluate lighting on clouds, you can assume the skydome pixel world position represents the cloud world position in the atmosphere.

### SkyAtmosphereViewLuminance

Th **SkyAtmosphereViewLuminance** expression outputs the sky luminance resulting from the interaction with atmospheric lights in the atmosphere.

![The SkyAtmosphereViewLuminance expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ade40f4c-1ef2-4cb1-b6f9-f2822868e833/04-sky-atmosphere-view-luminance.png)

### SkyAtmosphereAerialPerspective

The **SkyAtmosphereAerialPerspective** expression outputs RGBA-colored in-scattered luminance in RGB and grayscale transmittance over the skydome world position in A.

![The SkyAtmosphereAerialPerspective expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3a154f9-d627-4198-9249-fbba42723dc7/05-sky-atmosphere-aerial-perspective.png)

The shape of the skydome mesh is important because it drives the evaluation of these values. For instance, if you use these functions to evaluate the lighting on clouds, you can assume that the skydome pixel world position represents the cloud world position in the atmosphere. However, there is an override to provide the sampled position.

### SkyAtmosphereLightDirection

The **SkyAtmosphereLightDirection** expression takes in the Atmospheric Light Index for a Directional Light and outputs the light direction from the light.

![The SkyAtmosphereLightDirection expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a98768c-30e3-4b04-8a4e-984a28623d80/06-sky-atmosphere-light-direction.png)

In the **Details** panel, set the **Light Index** for the Directional Light being referenced. This should match the Directional Light's **Atmosphere Sun Light Index** property.

### SkyAtmosphereLightIlluminance

The **SkyAtmosphereLightIlluminance** expression takes in the Atmospheric Light Index for a Directional Light and outputs illuminance reaching the skydome world position (see note below). This is illuminance, so it needs to be integrated against a BxD/phase function to get luminance to accumulate. A multiplication with a uniform phase function of 1/(4π) is a good starting point.

![The SkyAtmosphereLightIlluminance expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/013c2416-1257-4379-8e02-63c16c504ee2/07-sky-atmosphere-light-illuminance.png)

In the **Details** panel, set the **Light Index** for the Directional Light being referenced. This should match the Directional Light's **Atmosphere Sun Light Index** property.

The shape of the skydome mesh is important because it drives the evaluation of these values. For instance, if you use these functions to evaluate the lighting on clouds, you can assume that the skydome pixel world position represents the cloud world position in the atmosphere. However, there is an override to provide the sampled position.

### SkyAtmosphereDistantLightScatteredLuminance

The SkyAtmosphereDistanceLightScatteredLuminance expression outputs the sky scattered luminance integrated over the unit sphere, assuming a uniform phase function. The sample is taken at the specified altitude of the DistanceSkyLight LUT (r.SkyAtmosphere.DistanceSkyLightLUT.Altitude).

![The SkyAtmosphereDistanceLightScatteredLuminance expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc3ef608-75e7-43a0-b1fe-eb2d3ce52f66/08-sky-atmosphere-distance-light-scattered-luminance.png)

### SkyAtmosphereLightDiskLuminance

The SkyAtmosphereLightDiskLuminance expression takes in the Atmospheric Light index for a Directional Light and outputs the light sun disk luminance with atmosphere transmittance applied.

![The SkyAtmosphereLightDiskLuminance expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35d2508d-2898-45e8-96c3-8cf49dba7f37/09-sky-atmosphere-light-disk-luminance.png)

In the **Details** panel, set the **Light Index** for the Directional Light being referenced. This should match the Directional Light's **Atmosphere Sun Light Index** property.

## Console Commands

The following console commands enable you to control the performance and visual quality of your atmosphere.

For additional details, see the "Sky Rendering Options" section of the [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) page.

| Console Variable | Description |
| --- | --- |
| System |   |
| `r.SkyAtmosphere` | Sky Atmosphere components are rendered when this is not 0, otherwise ignored. |
| `r.SupportSkyAtmosphere` | Enables Sky Atmosphere rendering and shader code. |
| `r.SupportSkyAtmosphereAffectsHeightFog` | Enables Sky Atmosphere affecting height fog. It requires r.SupportSkyAtmosphere to be true. |
| `r.SkyAtmosphere.LUT32` | Uses the full 32-bit per-channel precision for all sky look-up tables (LUT). |
| `r.SkyAtmosphere.EditorNotifications` | Enables the rendering of in-editor notification to warn the user about missing sky dome pixels on screen. It is better to keep it enabled and will be removed when shipping. |
| `r.SkyAtmosphereASyncCompute` | SkyAtmosphere on async compute. Default is false. |
| Fast Sky View LUT |   |
| `r.SkyAtmosphere.FastSkyLUT` | When enabled, a lookup texture is used to render the sky. It is faster, but can result in visual artifacts if there are some high-frequency details in the sky such as Earth shadow or scattering lob. |
| `r.SkyAtmosphere.FastSkyLUT.SampleCountMin` | Fast sky minimum sample count used to compute sky/atmosphere scattering and transmittance. The minimal value is clamped to 1. |
| `r.SkyAtmosphere.FastSkyLUT.SampleCountMax` | Fast sky maximum sample count used to compute sky/atmosphere scattering and transmittance. The minimal value is clamped to r.SkyAtmosphere.FastSkyLUT.SampleCountMin +1. |
| `r.SkyAtmosphere.FastSkyLUT.DistanceToSampleCountMax` | Fast sky distance in kilometers after which at which SampleCountMax samples is used to ray march the atmosphere. |
| `r.SkyAtmosphere.FastSkyLUT.Width` | The width of the FastSky LUT. |
| `r.SkyAtmosphere.FastSkyLUT.Height` | The height of the FastSky LUT. |
| Aerial Perspective |   |
| `r.SkyAtmosphere.AerialPerspective.StartDepth` | The distance at which we start evaluate the aerial perspective. Default is set to 100 meters. |
| `r.SkyAtmosphere.AerialPerspective.DepthTest` | When enabled, a depth test is used to not write pixel closer to the camera than StartDepth, effectively improving performance. |
| Aerial Perspective LUT |   |
| `r.SkyAtmosphere.AerialPerspectiveLUT.DepthResolution` | The number of depth slices to use for the aerial perspective volume texture. |
| `r.SkyAtmosphere.AerialPerspectiveLUT.Depth` | The length of the LUT in kilometers (default is 96 kilometers to get nice cloud/atmosphere interactions in the distance for the default sky). Further than this distance, the last slice is used. |
| `r.SkyAtmosphere.AerialPerspectiveLUT.SampleCountPerSlice` | The sample count used per slice to evaluate aerial perspective scattering and transmittance in camera frustum space froxel. |
| `r.SkyAtmosphere.AerialPerspectiveLUT.SampleCountMaxPerSlice` | The sample count used per slice to evaluate aerial perspective. The effective sample count is usually lower and depends on SampleCountScale on the component as well as `.ini` files, scattering and transmittance in camera frustum space froxel. |
| `r.SkyAtmosphere.AerialPersepctiveLUT.Width` | The width and height on screen of the AerialPerspective LUT. |
| `r.SkyAtmosphere.AerialPerspectiveLUT.FastApplyOnOpaque` | When enabled, the low resolution camera frustom/froxel volume containing the atmospheric fog, which is usually used for fog on translucent, is used to render fog on opaque. It is faster but can result in visual artefacts if there are some high frequency details, such as earth shadow or scattering lob. |
| Raymarching Sky |   |
| `r.SkyAtmosphere.SampleCountMin` | The minimum sample count used to compute sky/atmosphere scattering and transmittance. The minimal value will be clamped to 1. |
| `r.SkyAtmosphere.SampleCountMax` | The maximum sample count used to compute sky/atmosphere scattering and transmittance. The minimal value will be clamped to r.SkyAtmosphere.SampleCountMin +1. |
| `r.SkyAtmosphere.SampleLightShadowmap` | Enables the sampling of atmospheric lights shadow map in order to produce volumetric shadows. |
| `r.SkyAtmosphere.DistanceToSampleCountMax` | The distance in kilometers after which at which SampleCountMax samples is used to ray march the atmosphere. |
| Transmittance LUT |   |
| `r.SkyAtmosphere.TransmittanceLUT` | Enables the generation of the sky transmittance. |
| `r.SkyAtmosphere.TransmittanceLUT.SampleCount` | The sample count used to evaluate transmittance. |
| `r.SkyAtmosphere.TransmittanceLUT.UseSmallFormat` | If true, the transmittance LUT uses a small R8BG8B8A8 format to store data at lower quality. |
| `r.SkyAtmosphere.TransmittanceLUT.LightPerPixelTransmittance` | Enables Sky Atmosphere light per pixel transmittance, but only for opaque objects in the deferred renderer. It is more expensive but space/planetary views will be more accurate with it enabled. |
| `r.SkyAtmosphere.TransmittanceLUT.Width` | The width of the Transmittance LUT. |
| `r.SkyAtmosphere.TransmittanceLUT.Height` | The height of the Transmittance LUT. |
| Multi-Scattering LUT |   |
| `r.SkyAtmosphere.MultiScatteringLUT.SampleCount` | The sample count used to evaluate multi-scattering. |
| `r.SkyAtmosphere.MultiScatteringLUT.HighQuality` | When enabled, 64 samples are used instead of 2, resulting in a more accurate multi-scattering approximation (but also a bit more expensive.) |
| `r.SkyAtmosphere.MultiScatteringLUT.Width` | The width of the MultiScattering LUT. |
| `r.SkyAtmosphere.MultiScatteringLUT.Height` | The height of the MultiScattering LUT. |
| Distance Sky Light LUT |   |
| `r.SkyAtmosphere.DistantSkyLightLUT` | Enable the generation of the sky ambient lighting value. |
| `r.SkyAtmosphere.DistantSkyLightLUT.Altitude` | The altitude at which the sky samples are taken to integrate the sky lighting. Defaults to 6 kilometers, typicall cirrus clouds altitude. |