# Physical Lighting Units

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-physical-lighting-units-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-physical-lighting-units-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:34

---

Lights in **Unreal Engine** (UE) are defined using physically based lighting units, making it possible to enter known, measurable values to achieve fully realistic lighting. In addition to light types supporting different lighting units, Post Process for [Eye Adaptation (or Auto Exposure)](/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine) now supports an extended range of values and is expressed in EV100 (ISO 100). Between the physically based units for lighting and auto exposure, creating realistic lighting is much more achievable without "magic" numbers and artists having to "eyeball" different values.

## Lighting Units for Light Intensities

Each type of light displays its physically based lighting unit next to its **Intensity** value in its **Details** panel when selected.

![Light Type Units](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ca92dc3-1a63-4793-8048-c1dd86c5ac39/01-physical-light-units-options.png)

For these types of lights, their intensity is displayed as follows:

-   **Directional Light** uses **Direct Normal Illuminance**, expressed as **Lux** which is equal to one lumen per squared meter.
-   **Sky Light** and **Emissive Materials as Static Lights** use Luminance expressed as **Candela per meter squared** (cd/m2).
-   **Point**, **Spot**, and **Rect Lights** can select between the following lighting units:
    -   **Candela** (cd) is a measure of luminous intensity emitted uniformly across a solid angle of one steradian (sr). For example, a light set to 1000 cd would measure 1000 lux at one meter.
    -   **Lumen** (lm) is a measure of the luminous flux emitted into the angle of one steradian. In photometry, luminous flux (or luminous power) is the measure of the perceived power of light. No matter its distribution (wide or narrow spot), the total amount of energy emitted will be the same.
    -   **Unitless** is an engine-specific light intensity value and maintains compatibility with engine releases prior to Unreal Engine 4.19.

### Directional Light

A **Directional Light** simulates **Direct Normal Illuminance**, which is the amount of light produced by the [**visible**](https://en.wikipedia.org/wiki/Light) part of direct solar radiation that falls on a surface perpendicular to the Sun's rays. [**Illuminance**](https://en.wikipedia.org/wiki/Illuminance) is expressed in [**Lux**](https://en.wikipedia.org/wiki/Lux) (lx).

### Emissive Surfaces

Emissive surfaces are expressed in **Candela Per Meter Squared** (cd/m2) which specifies the pixel luminance before any lighting is added.

#### Sky Light

**Sky Lights** use the pixel intensity multiplied by the light intensity result in a total luminance that is expressed in cd/m2 in HDR. For example, if the HDR pixels were thought of as a filter and those pixels ranged from 0 to 1.0 with the sky set to an intensity of 1000 cd/m2, the resulting luminance would be 1.0 \* 1000 cd/m2.

#### Emissive Materials as Static Lights

For [Emissive Materials applied to Static Meshes](/documentation/en-us/unreal-engine/using-the-emissive-material-input-in-unreal-engine) that enable the per-Actor settings **Use Emissive for Static Lighting**, the luminance of the surface is used to bake lighting into the scene.

### Point, Spot, and Rect Lights

For **Point**, **Spot**, and **Rect Lights**, you can specify the unit type of any Light that has **Inverse Squared Falloff** enabled. You can use the Details panel section Light to set the **Intensity Units** to **Candela**,**Lumen** or **Unitless**.

**Inverse Squared Falloff** is physically based distance falloff where the attenuation radius is only clamping the lights contribution supported by all three light unit types. When disabled, only **Unitless** is available. Lights with Inverse Squared Falloff disabled are useful when placing low-intensity fill lights where you don't want a bright spot near the light.

![Selecting Light Type Units](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecd1bdb0-408d-4677-8016-c5e898ef5bd0/02-physical-light-units-select-units.png)

The default unit type for Point, Spot, and Rect Lights can be set with in the **Project Settings > Rendering > Default Settings**.

The relationship between each unit is defined as follows:

-   1 cd = 625 unitless
-   1 cd = 1 lm/sr

Note that when the intensity of a light is defined in **Candelas**, it is unaffected by its cone angle. Otherwise, when the light intensity is defined in **Lumens**, its luminous power only applies to the solid angle affected by the light, in **Steradians** (sr).

For **Point Lights**, the solid angle affected by the light is 4π sr :

-   Illuminance (1 lm) ≈ 49.7 \* Illuminance (1 unitless)
-   Illuminance (1 cd) ≈ 12.6 \* Illuminance (1 lm)

For **Spot Lights**, the solid angle is defined by 2π \* (1 - cos(θ)), where θ is the light cone half angle:

-   Illuminance (1 lm) ≈ 99.5 / (1 - cos(θ)) \* Illuminance (1 unitless)

For the default cone, θ = 44° and the solid angle is about 1.76 sr :

-   Illuminance (1 lm) ≈ 354 \* Illuminance (1 unitless) for default Spot Lights.
-   Illuminance (1 cd) ≈ 1.76 \* Illuminance (1 lm) for default Spot Lights.

The smaller the cone angle, the stronger the surface illumination from the light will be when the light intensity is expressed in Lumens.

For **Rect Lights**, the solid angle is defined as 2π sr :

-   Illuminance (1 lm) ≈ 199 \* Illuminance (1 unitless)
-   Illuminance (1 cd) ≈ 3.14 \* Illuminance (1 lm)

## Tips and Suggestions

Below are some suggestions to get the most out of a physically based lighting workflow:

-   If after placing a light the image goes white, then the auto exposure range may be too limited. Consider increasing the **Auto Exposure Max EV100** (and **Histogram Max EV100**).
-   If reflective surfaces have artifacts like black patches, the SceneColor buffer might be overflowing. To fix it, either enable **Apply Pre-Exposure before writing to the scene color** in the Project Settings, or reduce the brightness of lights in the scene.
-   Don't forget that there are some default Post Process settings already applied to the scene (even when there is no Post Process Volume present). These default settings may affect the camera settings in unexpected ways. It is recommended to place a Post Process Volume in the scene so that you can change those settings as needed.
-   If you change the Project Settings to use the extended default luminance range, it will break existing exposure configurations. You will have to migrate / reconfigure manually the settings for those assets so that it's safe to do it from the start of your process.
-   Auto exposure histogram can suffer from stability issues where a small change in the scene generates a slightly different exposure value. To workaround this issue, reduce the **Histogram Min** and **Max** range around the actual usage in the scene. To see the usage, enable the **Visualize HDR** show flag.

## General Considerations

Some special care must be taken to avoid default value propagation issues between assets and instances. It's recommended that any light instanced from another light (through Blueprints or default objects) keeps the same light unit as their parent. Otherwise, ones already in use should not have their units changed. Doing this will guarantee that changing the default values will have the expected behavior and propagate to instances correctly and help prevent breaking existing instances.

The default project **Light Units** for Point, Spot, and Rect Lights can be specified in **Project Settings > Rendering > Default Settings**.

![Project Settings for Physical Lighting Units](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2db3f1f6-e5e6-4aeb-90f2-c85e12d0936e/03-physical-light-units-rendering-settings.png)