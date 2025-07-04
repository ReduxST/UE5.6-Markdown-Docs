# Spot Lights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/spot-lights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/spot-lights-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:57

---

A **Spot Light** emits light from a single point in a cone shape. Users are given two cones to shape the light - the **Inner Cone Angle** and **Outer Cone Angle**. Within the Inner Cone Angle, the light achieves full brightness. As you go from the extent of the inner radius to the extents of the Outer Cone Angle, a falloff takes place, creating a penumbra, or softening around the Spot Light's disc of illumination. The Radius of the light defines the length of the cones. More simply, this will work like a flash light or stage can light.

Like other lights, a Spot Light can be set to one of three Mobility settings:

-   **Static** - (pictured left) which means that the light cannot be changed in game. This is the fastest method for rendering and allows for baked lighting.
    
-   **Stationary** - (also pictured left) which means the light will only have its shadowing and bounced lighting from static geometry baked by Lightmass, all other lighting will be dynamic. This setting also allows for the light to change color and intensity in game, but, it does not move and allows partial baked lighting.
    
-   **Moveable** - (pictured left) which means the light is totally dynamic and allows for dynamic shadowing. This is the slowest in terms of rendering but allows for the most flexibility during gameplay.
    

Two examples of a **Spot Light** placed inside a level are shown below demonstrating how to determine the light radius and cone effectors:

![Spot Light without its Cone showing](https://dev.epicgames.com/community/api/documentation/image/8bd0c8eb-ec01-48cc-91ca-f953557dbd4a?resizing_type=fit&width=1920&height=1080)

![Spot Light with Cone showing](https://dev.epicgames.com/community/api/documentation/image/625e5ecf-5fad-4c89-8d31-81dfc16ca1c4?resizing_type=fit&width=1920&height=1080)

Spot Light without its Cone showing

Spot Light with Cone showing

On the left a Spot Light without its cones showing light radius, on the right the same Spot Light with its cone effectors showing.

## Spot Light Properties

The properties of a Spot Light are broken up into 4 categories: Light, Light Profiles, Lightmass, and Light Function.

### Light

| Property | Description |
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

**Inner Cone Angle**

 | 

Sets the inner cone angle of the Spot Light, in degrees.

 |
| 

**Outer Cone Angle**

 | 

Sets the outer cone angle of the Spot Light, in degrees.

 |
| 

**Attenuation Radius**

 | 

Bounds the light's visible influence.

 |
| 

**Source Radius**

 | 

Radius of light source shape.

 |
| 

**Source Length**

 | 

Length of light source shape.

 |
| 

**Affects World**

 | 

Disables the light completely. Cannot be set at run time. To disable a light's effect during runtime, change its Visibility property.

 |
| 

**Casts Shadows**

 | 

If the light casts shadows.

 |
| 

**Indirect Lighting Intensity**

 | 

Scales the indirect lighting contribution from the light.

 |
| 

**Use Inverse Squared Falloff**

 | 

Whether to use physically based inverse squared distance falloff, where AttenuationRadius is only clamping the light's contribution.

 |
| 

**Light Falloff Exponent**

 | 

Controls the radial falloff of light when UseInverseSquaredFalloff is disabled.

 |
| 

**Min Roughness**

 | 

Min roughness effective for this light, used for softening specular highlights.

 |
| 

**Shadow Bias**

 | 

Controls how accurate the shadows from this light are.

 |
| 

**Shadow Filter Sharpen**

 | 

How much to sharpen shadow filtering for this light.

 |
| 

**Cast Translucent Shadows**

 | 

Whether this light is allowed to cast dynamic shadows through translucent objects.

 |
| 

**Affect Dynamic Indirect Lighting**

 | 

Whether the light should be injected into the Light Propagation Volume.

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

### Light Profiles

| Property | Description |
| --- | --- |
| 
**IES Texture**

 | 

The IES "Texture" used for the light profile. IES files are ASCII though Unreal represents them as textures, they are not image files.

 |
| 

**Use IES Brightness**

 | 

If *false*, it will use the Brightness of the light to determine how much light to produce. If *true*, it will use the IES files brightness in Lumens (usually much larger than default values on lights in Unreal).

 |
| 

**IES Brightness Scale**

 | 

Scale for IES brightness contribution, as they can seriously blow out a scene.

 |

### Lightmass

| Property | Description |
| --- | --- |
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

**Light Function Fade Distance**

 | 

The distance at which the light function should be completely faded to the value in Disabled Brightness.

 |
| 

**Disabled Brightness**

 | 

Brightness factor applied to the light when the light function is specified but disabled, say from the property above: Light Function Fade Distance.

 |