# Point Lights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/point-lights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/point-lights-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:50

---

**Point Lights** work much like a real world light bulb, emitting light in all directions from the light bulb's tungsten filament. However, for the sake of performance, Point Lights are simplified down emitting light equally in all directions from just a single point in space. The Point Light when placed can be set to one of three Mobility settings:

-   **Static** - (pictured left) which means that the light cannot be changed in game. This is the fastest method for rendering and allows for baked lighting.
-   **Stationary** - (also pictured left) which means the light will only have its shadowing and bounced lighting from static geometry baked by **Lightmass**, all other lighting will be dynamic. This setting also allows for the light to change color and intensity in game, but, it does not move and allows partial baked lighting.
-   **Moveable** - (pictured left) which means the light is totally dynamic and allows for dynamic shadowing. This is the slowest in terms of rendering but allows for the most flexibility during gameplay.

Two examples of a Point Light placed inside a level are shown below.

![Point Light Without Radius Showing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/287e43b7-2236-4c7a-92a8-2d893dc31c91/pointlight_004.png)

![Point Light With Radius Showing.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36039826-8aeb-4536-9640-60a6ef67f73f/pointlight_005.png)

The image on the left is a Point Light without its radius showing, and the same light with it enabled is shown in the right image, giving a good impression of where the light will affect the world.

While the light from a Point Light only emits from that point in space, having no shape, Unreal Engine can give a point light a radius and a length for use within reflections and specular highlights to give the point light more of a physical feel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2516e75f-bc76-4f30-ba82-ef19294fa77a/pointlight_001.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7469cec-1259-47e0-9e30-827c4d0f80ee/pointlight_002.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1c49072-a634-4c49-8f4d-15255675ccbc/pointlight_003.png)

## Point Light Properties

The properties of a **Point Light** are broken up into 4 categories: Light, Light Profiles, Lightmass, and Light Function.

### Light

| Property | Description |
| --- | --- |
| **Intensity** | Total energy that the light emits. |
| **Light Color** | The color that the light emits. |
| **Attenuation Radius** | Bounds the light's visible influence. |
| **Source Radius** | Radius of light source shape. |
| **Source Length** | Length of light source shape. |
| **Affects World** | Disables the light completely. Cannot be set at run time. To disable a light's effect during runtime, change its Visibility property. |
| **Casts Shadows** | If the light casts shadows. |
| **Indirect Lighting Intensity** | Scales the indirect lighting contribution from the light. |
| **Use Inverse Squared Falloff** | Whether to use physically based inverse squared distance falloff, where AttenuationRadius is only clamping the light's contribution. |
| **Light Falloff Exponent** | Controls the radial falloff of light when UseInverseSquaredFalloff is disabled. |
| **Specular Scale** | Multiplier on Specular Highlights. Use only with great care! Any value besides 1 is not physical! Can be used to artistically remove highlights mimicking polarizing filters or photos touch up. |
| **Shadow Bias** | Controls how accurate the shadows from this light are. |
| **Shadow Filter Sharpen** | How much to sharpen shadow filtering for this light. |
| **Contact Shadow Length** | The length of screen space to ray trace for sharp contact shadows. A value of zero disables this option. |
| **Cast Translucent Shadows** | Whether this light is allowed to cast dynamic shadows through translucent objects. |
| **Affect Dynamic Indirect Lighting** | Whether the light should be injected into the Light Propagation Volume. |
| **Cast Static Shadows** | Whether this light casts static shadows. |
| **Cast Dynamic Shadows** | Whether this light casts dynamic shadows. |
| **Affect Translucent Lighting** | Whether the light affects translucency or not. |

### Light Profiles

| Property | Description |
| --- | --- |
| **IES Texture** | The IES "Texture" used for the light profile. IES files are ASCII though Unreal represents them as textures, they are not image files. |
| **Use IES Brightness** | If *false*, it will use the Brightness of the light to determine how much light to produce. If *true*, it will use the IES files brightness in Lumens (usually much larger than default values on lights in Unreal). |
| **IES Brightness Scale** | Scale for IES brightness contribution, as they can seriously blow out a scene. |

### Lightmass

| Property | Description |
| --- | --- |
| **Indirect Lighting Saturation** | A value of 0 will completely desaturate this light in Lightmass, 1 will be unchanged. |
| **Shadow Exponent** | Controls the falloff of shadow penumbras. |

### Light Function

| Property | Description |
| --- | --- |
| **Light Function Material** | The light function material to be applied to this light. |
| **Light Function Scale** | Scales the light function projection. |
| **Light Function Fade Distance** | The distance at which the light function should be completely faded to the value in Disabled Brightness. |
| **Disabled Brightness** | Brightness factor applied to the light when the light function is specified but disabled, say from the property above: Light Function Fade Distance. |