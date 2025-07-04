# Rectangular Area Lights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:05

---

The **Rect Light** emits light into the scene from a rectangular plane with a defined width and height. You can use them to simulate any kind of light sources that have rectangular areas, such as televisions or monitor screens, overhead lighting fixtures, or wall sconces.

RectLights do not behave like true area lights in all situations. See the discussion on mobility settings below.

Each Rect Light has two key settings, **Source Width** and **Source Height**, which determine the size of its rectangle along its local Y and Z axes:

![Source Width and Source Height](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d0a706e-6411-4530-b1b8-a5759f97fd20/rectlight-widthheight-1.png "Source Width and Source Height")

The Rect Light has a spherical attenuation radius, like a Point Light or a Spot Light. As shown in the image above, the Rect Light emits light within its sphere of attenuation only in the positive direction of its local X axis, similar to a Spot Light with its cone set to 180 degrees. However, specular highlights for Rect Lights show the width and height of the light's rectangular area.

Like other types of light sources, Rect Lights have three Mobility settings:

-   **Static:** With this setting, the light's direct and indirect illumination are both baked to lightmaps when you build lighting for your level. This is the fastest method for rendering, but it means that the light cannot be changed in the game at runtime.
-   **Stationary:** With this setting, only the indirect illumination from the light is baked into lightmaps when you build lighting for your level. The direct lighting cast by the light is calculated dynamically every frame in the game. This setting preserves the high-quality soft shadowing and global illumination pre-computed by Lightmass, but it also permits you to change the color and intensity of the light in the game at runtime.
-   **Movable:** With this setting, the light is totally dynamic. None of its direct or indirect illumination is baked by Lightmass at all. This allows your light to cast correct shadows from moving objects in the game at runtime every frame. However, this setting is typically the slowest to render.

![Rect Light Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/effaa880-072d-4102-a465-c78c1fd622fd/rect-light.png)

The mobility setting you choose also has a significant effect on the way the Rect Light casts light into the scene:

-   If your Rect Light is set to **Static** or **Stationary**, Lightmass takes the width and height of the light into account when it computes the illumination cast from the light source. For example, in the image on the left above, the light from the left and right extents of the rectangle reaches under the model and illuminates most of the floor.  
    In this case, the light emitted from the RectLight is sampled from multiple points across its rectangular surface. Each sampled light emits a fraction of the overall light intensity, so you can think of the RectLight as a simulation of many weak point lights distributed across the rectangular surface. The number of samples increases with the quality of your light build. Preview builds use few samples, so their shadows can look quite blocky. However, raising the quality setting eventually converges toward smoother results, as shown above.
    
    If you set your Rect Light to **Stationary** Mobility, you may be able to achieve better quality shadows by also enabling the **Use Area Shadows for Stationary Light** setting.
    
-   If your Rect Light is set to **Movable**, the width and height of the rectangle are only used for specular reflections. The actual light is emitted outward from the center of the Rect Light, similar to a Point Light. For example, in the image on the right above, the sharp shadow cast on the floor indicates that the light is emitted from the center of the rectangle.
    

Rect Lights that are set to **Stationary** or **Movable** are typically much more expensive to render than a Point Light or Spot Light with the same mobility. The exact cost scaling depends on the platform, but in general, Movable lights cost more than Stationary lights. The cost is also due in part to shadow casting, so you may be able to minimize the extra cost by turning off the **Casts Shadows** option. Alternatively, you could opt to set the mobility of the light to **Static**, which has no effect on runtime rendering performance at all.

The forward renderer does not currently support Rect Lights. If you need to use forward rendering in your Project, use a Spot Light or Point Light instead.

## Rect Light Properties

The properties of a **Rect Light** are broken up into 4 categories: [Light](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine#light), [Lightmass](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine#lightmass), [Light Function](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine#lightfunctions) and [Light Profiles](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine#lightprofiles).

### Light

| Property | Description |
| --- | --- |
| **Intensity** | The total energy that the light emits. Note that for Rect Lights, this value is averaged over the surface area of the light. As you increase the Source Width and Source Height of the light, you will need to increase the Intensity in order to maintain the same apparent brightness. |
| **Light Color** | The color that the light emits. |
| **Attenuation Radius** | Bounds the light's visible influence. Like a Point Light or a Spot Light, a Rect Light has a spherical attenuation radius. |
| **Source Width** | The extent of the Rect Light along its local Y axis. |
| **Source Height** | The extent of the Rect Light along its local Z axis. |
| **Barn Door Angle** | The angle of the barn door attached to the Rect Light. |
| **Barn Door Length** | The length of the barn door attached to the Rect Light. |
| **Source Texture** | 
Specifies a Texture that will be applied on the emitting rectangle. This Texture affects the color of the light emitted by the Rect Light, and is visible in specular reflections. Note, however, that this is only an approximation. It does not affect shadows cast by the Rect Light. Use an HDR image if possible, to avoid banding artifacts. In addition, make sure that the **Level of Detail > Mip Gen Settings** option for your Texture is set to **Blur5**.



 |
| **Temperature** | The color temperature of the light, measured in Kelvin. |
| **Use Temperature** | Determines whether or not the Temperature setting should apply to this light. |
| **Affects World** | Enables and disables the light completely. Cannot be set at run time. To disable a light's effect during runtime, change its Visibility property. |
| **Cast Shadows** | Determines whether or not the light casts shadows from objects in the Level. |
| **Indirect Lighting Intensity** | Scales the indirect lighting contribution from the light. |
| **Volumetric Scattering Intensity** | Scales the intensity and color of the volumetric scattering from this light. |
| **Advanced Settings** |   |
| **Intensity Units** | Determines how the light's Intensity setting should be interpreted. |
| **Specular Scale** | Multiplier on Specular Highlights. Use only with great care! Any value besides 1 is not physical! Can be used to artistically remove highlights mimicking polarizing filters or photos touch up. |
| **Shadow Resolution Scale** | Scales the resolution of the shadowmaps used to calculate dynamic shadows cast by this light. By default, this value is computed based on the screen size of the shadow caster. Note that this value is capped by the value of the global r.Shadow.MaxResolution setting. |
| **Shadow Bias** | Controls how accurate the shadows from this light are. |
| **Shadow Filter Sharpen** | How much to sharpen shadow filtering for this light. |
| **Contact Shadow Length** | The length of screen space to ray trace for sharp contact shadows. A value of zero disables this option. |
| **Contact Shadow Length in World Space Units** | Determines whether the Contact Shadow Length setting is interpreted in world space units, or in screen space units. |
| **Cast Translucent Shadows** | Determines whether this light is allowed to cast dynamic shadows through translucent objects. |
| **Cast Shadows from Cinematic Objects Only** | Determines whether this light should cast shadows only from Components that have the Cast Cinematic Shadows option enabled. |
| **Dynamic Indirect Lighting** | Determines whether this light should be included in Light Propagation Volumes. |
| **Force Cached Shadows for Movable Primitives** | When enabled, this light will generate cached shadows for movable primitives even when the global r.shadow.cachedshadowscastfrommovableprimitives setting is disabled. |
| **Lighting Channels** | Determines the lighting channels that this light should affect. |
| **Cast Static Shadows** | Determines whether this light should cast shadows from static objects. |
| **Cast Dynamic Shadows** | Determines whether this light should cast shadows from movable objects. |
| **Affect Translucent Lighting** | Determines whether this light should affect translucency. Disabling this setting may save some GPU time when your scene has many small lights. |
| **Transmission** | Determines whether the light cast by this light source transmits through surfaces with subsurface scattering profiles. |
| **Cast Volumetric Shadow** | Determines whether this light source casts shadows from volumetric fog. |

### Lightmass

The settings in this section are specific to the way this light is treated by the [Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine) global illumination system.

| Property | Description |
| --- | --- |
| **Indirect Lighting Saturation** | Determines the saturation of this light in baked lightmaps. A value of 0 completely desaturates this light; 1 leaves it unchanged. |
| **Shadow Exponent** | Controls the falloff of shadow penumbras. |
| **Use Area Shadows for Stationary Light** | Determines whether to use area shadows for stationary lights. This causes the shadows to get softer as the distance from the caster increases, but can require higher lightmap resolutions to get equally good results in places where the shadows are sharp |

### Light Functions

Use the settings in this section to set up a [Light Function](/documentation/en-us/unreal-engine/using-light-functions-in-unreal-engine) for this light.

| Property | Description |
| --- | --- |
| **Light Function Material** | The light function material to be applied to this light. |
| **Light Function Scale** | Scales the light function projection. |
| **Fade Distance** | The distance at which the light function should be completely faded to the value in Disabled Brightness. |
| **Disabled Brightness** | Brightness factor applied to the light when the light function is specified but disabled — for example, when outside the maximum distance set by the Fade Distance setting above. |

### Light Profiles

Use the settings in this section to set up an [IES profile](/documentation/en-us/unreal-engine/using-ies-light-profiles-in-unreal-engine) for this light.

Note that Rect Lights project their IES profiles from the center of the light, not along the edges of the light's rectanglular area. This may produce unexpected results.

| Property | Description |
| --- | --- |
| **IES Texture** | The IES Texture Asset assigned to the light's profile. Note that IES files are ASCII files, not image files, even though Unreal represents them as textures. |
| **Use IES Brightness** | Determines the source of the light's brightness. When this option is enabled, the light uses brightness set in the IES profile, in Lumens. When this option is disabled, the light uses its Intensity setting. |
| **IES Brightness Scale** | Scales the brightness contribution when Use IES Brightness is enabled, to avoid the light overwhelming the scene. |