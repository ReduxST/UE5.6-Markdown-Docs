# Directional Lights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:44

---

The **Directional Light** simulates light that is being emitted from a source that is infinitely far away. This means that all shadows cast by this light will be parallel, making this the ideal choice for simulating sunlight. The Directional Light when placed can be set to one of three **Mobility** settings:

-   **Static** - (pictured left) which means that the light cannot be changed in game. This is the fastest method for rendering and allows for baked lighting.
    
-   **Stationary** - (also pictured left) which means the light will only have its shadowing and bounced lighting from static geometry baked by **Lightmass**, all other lighting will be dynamic. This setting also allows for the light to change color and intensity in game, but, it does not move and allows partial baked lighting.
    
-   **Moveable** - (pictured left) which means the light is totally dynamic and allows for dynamic shadowing. This is the slowest in terms of rendering but allows for the most flexibility during gameplay.
    

Below you will see a representation of sunlight being cast through an opening in a roof.

![Directional Light](https://dev.epicgames.com/community/api/documentation/image/2b745dde-f089-4860-a528-a10a95233a4c?resizing_type=fit&width=1920&height=1080)

![Directional Light Shadow Frustum](https://dev.epicgames.com/community/api/documentation/image/ba268ad5-b333-4449-97c3-32b50b75c057?resizing_type=fit&width=1920&height=1080)

Directional Light

Directional Light Shadow Frustum

The left image shows just the light, the right image has its **Shadow Frustum** enabled in order to see that the Directional Light is casting parallel light rays.

**Light Direction** (pictured left) is indicated by an arrow that points in the direction the light will emit which is useful for placing and orientating your light as needed.

## Directional Light Properties

The properties of a Directional Light are broken up into 5 categories: Light, Light Shafts, Lightmass, Light Function and Cascaded Shadow Maps:

### Light

|  Property | Description |
| --- | --- |
| 
**Intensity**

 | 

Total energy that the light emits.

 |
| 

**Light Color**

 | 

The color that the light emits.

 |
| 

**Source Angle**

 | 

Angle subtended by a light source in degrees. Defaults to 0.5357, which is the angle for our sun.

 |
| 

**Source Soft Angle**

 | 

Angle subtended by a soft light source in degrees.

 |
| 

**Use Temperature**

 | 

When disabled, uses white as an illuminant.

 |
| 

**Temperature**

 | 

Color temperature in Kelvin of the blackbody illuminant. White is 6500K.

 |
| 

**Affects World**

 | 

Disables the light completely. Cannot be set at run time. To disable a light's effect during runtime, change its **Visibility** property.

 |
| 

**Cast Shadows**

 | 

If the light casts shadows.

 |
| 

**Indirect Lighting Intensity**

 | 

Scales the indirect lighting contribution from the light.

 |
| 

**Volumetric Scattering Intensity**

 | 

Intensity of the volumetric scattering from this light.

 |
| 

**Shadow Cascade Bias Distribution**

 | 

Controls the depth bias across cascades. Use this to mitigate the shadow acne difference on shadow cascades transition.

 |
| 

**Forward Shading Priority**

 | 

Forward lighting priority for the single directional light that will be used for forward shading, translucent, single layer water and volumetric fog. Then two lights have equal priorities, the selection will be based on their overall brightness as a fallback.

 |
| 

**Cast Modulated Shadows**

 | 

Whether to cast modulated shadows from dynamic objects (mobile only).

 |
| 

**Modulated Shadow Color**

 | 

Color to modulate against the scene color when rendering modulated shadows (mobile only).

 |
| 

**Shadow Amount**

 | 

The amount of shadow occlusion. A value of 0 means no occlusion and no shadow.

 |
| 

**Specular Scale**

 | 

The multiplier on specular highlights. Use with care. Any values besides 1 are not physical.

 |
| 

**Shadow Resolution Scale**

 | 

Scales the resolution of shadow maps used to shadow this light.

 |
| 

**Shadow Bias**

 | 

Controls how accurate the shadows from this light are.

 |
| 

**Shadow Slope Bias**

 | 

Controls how accurate the self-shadowing of whole scene shadows from this light is. This contributes to Shadow Bias by increasing the amount of bias depending on the slope of a surface.

 |
| 

**Shadow Filter Sharpen**

 | 

How much to sharpen shadow filtering for this light.

 |
| 

**Contact Shadow Length**

 | 

Length of screen space ray trace for sharp contact shadows.

 |
| 

**Contact Shadow Length in World Space Units**

 | 

Whether to use world space units for the Contact Shadow Length.

 |
| 

**Cast Translucent Shadows**

 | 

Whether to cast dynamic shadows through translucent objects.

 |
| 

**Cast Shadows from Cinematic Objects Only**

 | 

Whether the light should only cast shadows from components marked as bCastCinematicShadows. This can be useful for setting up cinematic Movable spotlights aimed at characters and avoiding the shadow depth costs of the background.

This option only works with dynamic shadow maps, not with static shadowing or Ray Traced Distance Field shadows.



 |
| 

**Dynamic Indirect Lighting**

 | 

Whether the light should be injected into the **Light Propagation Volume**.

 |
| 

**Force Cached Shadows for Movable Primitives**

 | 

Enables cached shadows for movable primitives.

 |
| 

**Lighting Channels**

 | 

Channels that this light should affect.

 |
| 

**Cast Static Shadows**

 | 

Whether this light casts static shadows.

 |
| 

**Cast Dynamic Shadows**

 | 

Whether this light casts dynamic shadows.

 |
| 

**Affect Translucent Lighting**

 | 

Whether the light affects translucency or not.

 |
| 

**Transmission**

 | 

Whether to transmit through surfaces with subsurface scattering profiles.

 |
| 

**Cast Volumetric Shadow**

 | 

Whether to shadow volumetric fog.

 |
| 

**Cast Deep Shadow**

 | 

Whether to cast high-quality hair strands self-shadowing.

 |
| 

**Cast Ray Traced Shadows**

 | 

Sets whether to enable ray traced shadows for this light. The options are:

-   Disabled
    
-   Use Project Setting
    
-   Enabled
    

 |
| 

**Affect Ray Tracing Reflections**

 | 

Whether to affect objects in reflections when ray-traced reflection is enabled.

 |
| 

**Affect Ray Tracing Global Illumination**

 | 

Whether to affect global illumination when ray-traced global illumination is enabled.

 |
| 

**Deep Shadow Layer Distribution**

 | 

Changes the deep shadow layers distribution. A value of 0 is linear distribution (uniform layer distribution), and 1 is exponential.

 |

### Light Shafts

| Property | Description |
| --- | --- |
| 
**Light Shaft Occlusion**

 | 

Whether to occlude fog and atmosphere inter scattering with the screen space blurred occlusion from this light.

 |
| 

**Occlusion Mask Darkness**

 | 

How dark the occlusion masking is, a value of 1 is no darkening.

 |
| 

**Occlusion Depth Range**

 | 

Everything close to the camera than this distance will occlude the light shafts.

 |
| 

**Light Shaft Bloom**

 | 

Whether to render light shaft bloom for this light.

 |
| 

**Bloom Scale**

 | 

Scales the additive bloom color.

 |
| 

**Bloom Threshold**

 | 

Scene color must be larger than this to create bloom in the light shafts.

 |
| 

**Bloom Max Brightness**

 | 

When exposure is applied, this value constrains scene color brightness.

 |
| 

**Bloom Tint**

 | 

Sets the color to tint the bloom coming from the light shafts.

 |
| 

**Light Shaft Override Direction**

 | 

Can be used to make the light shafts come from somewhere other than the light's actual direction.

 |

### Lightmass

| Property | Description |
| --- | --- |
| 
**Light Source Angle**

 | 

Angle that the directional light's emissive surface extends relative to a receiver, affects penumbra sizes.

 |
| 

**Indirect Lighting Saturation**

 | 

A value of 0 will completely desaturate this light in Lightmass, 1 will be unchanged.

 |
| 

**Shadow Exponent**

 | 

Controls the falloff of shadow penumbras.

 |
| 

**Use Area Shadows for Stationary Light**

 | 

Whether to use area shadows for stationary light precomputed shadow maps.

 |

### Light Function

| Property | Description |
| --- | --- |
| 
**Light Function Material**

 | 

The light function material to be applied to this light.

 |
| 

**Light Function Scale**

 | 

Scales the light function projection.

 |
| 

**Fade Distance**

 | 

The distance at which the light function should be completely faded to the value in **Disabled Brightness**.

 |
| 

**Disabled Brightness**

 | 

Brightness factor applied to the light when the light function is specified but disabled, say from the Property above: **Light Function Fade Distance**.  


 |

### Cascaded Shadow Maps

| Property | Description |
| --- | --- |
| 
**Dynamic Shadow Distance MovableLight**

 | 

How far **Cascaded Shadow Map** dynamic shadows will cover for a movable light, measured from the camera.

 |
| 

**Dynamic Shadow Distance StationaryLight**

 | 

How far **Cascaded Shadow Map** dynamic shadows will cover for a stationary light, measured from the camera.

 |
| 

**Num Dynamic Shadow Cascades**

 | 

Number of cascades to split the view frustum into for the whole scene.

 |
| 

**Distribution Exponent**

 | 

Controls whether the cascades are distributed closer to the camera (larger exponent) or further from the camera (smaller exponent).

 |
| 

**Transition Fraction**

 | 

Proportion of the fade region between cascades.

 |
| 

**Distance Fadeout Fraction**

 | 

Controls the size of the fade out region at the far extent of the dynamic shadow's influence.

 |
| 

**Inset Shadows for Movable Objects**

 | 

(Stationary lights only) Whether to use per-object inset shadows for movable components, even though cascaded shadow maps are enabled.

 |
| 

**Far Shadow Cascade Count**

 | 

A value of 0 means no Distant Shadow Cascades.

 |
| 

**Far Shadow Distance**

 | 

Distance at which the far shadow cascade should end.

 |

### Atmosphere and Cloud

Directional Lights support the [Sky Atmosphere](https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) and the [Volumetric Clouds](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) features of Unreal Engine.

Additional information and demonstration can be found in the Volumetric Clouds page under the [Directional Light Interactions and Shadowing](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) section.

|  Property | Description |
| --- | --- |
| Atmosphere and Cloud |   |
| --- | --- |
| 
**Atmosphere Sun Light**

 | 

Whether the Directional Light can interact with the atmosphere, clouds and generate a visual sun disk, all of which compose the visual sky.

 |
| 

**Cast Shadows on Clouds**

 | 

Whether the light should cast any shadows from opaque meshes onto clouds. This is disabled for any secondary Directional Lights that have **Atmosphere Sun Light** enabled and set to **Atmosphere Sun Light Index** of 1, such as another sun or as a moon light.

 |
| 

**Cast Shadows on Atmosphere**

 | 

Whether the light should cast any shadows from opaque meshes into the atmosphere when a SkyAtmosphere is used.

 |
| 

**Cast Cloud Shadows**

 | 

Whether the light should cast any shadows from the clouds onto the atmosphere and other scene elements.

 |
| 

**Cloud Scattering Luminance Scale**

 | 

Scales the light contribution when scattered in cloud participating media. This can help counter balance the fact that our current multiple scattering solution is only an approximation.

 |
| Advanced Properties |   |
| --- | --- |
| 

**Atmosphere Sun Light Index**

 | 

Two atmosphere lights are supported at any time to represent the sun and moon, or two suns. Use this index to set the primary and secondary light source. For example, the sun would be 0 and the moon would be 1.

 |
| 

**Atmosphere Sun Disk Color Scale**

 | 

A color multiplied with the sun disk luminance.

 |
| 

**Per Pixel Atmosphere Transmittance**

 | 

Whether to apply atmosphere transmittance per pixel on opaque meshes instead of using the light's global transmittance.

 |
| 

**Cloud Shadow Strength**

 | 

The strength of the shadow. Higher values will block more light.

 |
| 

**Cloud Shadow on Atmosphere Strength**

 | 

The strength of shadows on the atmosphere. When set to 0, shadows on the atmosphere is disabled.

 |
| 

**Cloud Shadow on Surface Strength**

 | 

The strength of shadows on opaque and transparent meshes. When set to 0, shadows on opaque and translucent surfaces is disabled.

 |
| 

**Cloud Shadow Depth Bias**

 | 

Controls the bias applied to the front shadow depth of the volumetric cloud shadow map.

 |
| 

**Cloud Shadow Extent**

 | 

The world space radius of the cloud shadow map around the camera. Measured in kilometers (km).

 |
| 

**Cloud Shadow Map Resolution Scale**

 | 

Scales the cloud shadow map resolution. The resolution is clamped by `r.VolumetricCloud.ShadowMap.MaxResolution`.

 |
| 

**Cloud Shadow Ray Sample Count Scale**

 | 

Scales the number of samples used for shadow map tracing. The sample count resolution is clamped with `r.VolumetricCloud.ShadowMap.RaySampleMaxCount`.

 |