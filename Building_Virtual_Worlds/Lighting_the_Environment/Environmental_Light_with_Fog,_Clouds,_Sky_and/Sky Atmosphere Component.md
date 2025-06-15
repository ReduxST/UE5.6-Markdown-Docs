# Sky Atmosphere Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:56

---

The **Sky Atmosphere** component in Unreal Engine is a physically-based sky and atmosphere-rendering technique. It's flexible enough to create an Earth-like atmosphere with time-of-day featuring sunrise and sunset, or to create extraterrestrial atmospheres of an exotic nature. It also provides an aerial perspective to which you can simulate transitions from ground to sky to outer space with proper planetary curvature.

![Sky Atmosphere with time-of-day featuring sunrise and sunset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2b618f2-43c4-4e14-a044-1c9e627742b9/01-sky-atmosphere-day-dusk.png)

The Sky Atmosphere gives an approximation of light scattering through a planetary atmosphere's participating media, giving outdoor levels a more realistic or exotic look by including the following:

-   You can have two atmospheric Directional Lights that receive sun disk representation in the atmosphere with sky color that depends on the sunlight and atmosphere properties.
-   A sky color that will vary, depending on the altitude of the sun, or in other terms, how close the dominant Directional Light's vector gets to being parallel with the ground.
-   Control over scattering and fuzzy settings, allowing for full control of your atmospheric density.
-   Aerial perspective that simulates the curvature of the world when transitioning from ground to sky to space views.

## Enabling the Sky Atmosphere Component

Enable the Sky Atmosphere component by following these steps using the **Place Actors** panel in the Level Editor:

1.  Place a **Sky Atmosphere** component in the scene.
    
    ![Drag a Sky Atmosphere into your scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d6ca1e7-0172-4c74-bf5f-97bb19c2adda/02-placing-sky-atmosphere.png)
2.  Place a **Directional Light** in the scene.
    
    ![Drag a Directional Light into your scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61fa493b-d8e5-4b4b-9a4c-808a410f8b65/03-placing-directional-light.png)
3.  From its **Details** panel, enable **Atmosphere Sun Light**.
    
    ![Select Directional Light and enable Atmosphere Sun Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1124206-508e-4f83-81a5-6e28bb7cdda0/04-enabling-atmosphere-sun-light.png)
    1.  If using multiple **Directional Lights**, set the **Atmosphere Sun Light Index** for each; for instance, 0 for the Sun and 1 for the Moon.
4.  Place a **Sky Light** in the scene to capture Sky Atmosphere and have it contribute to the scene lighting.
    
    ![Drag a Sky Light into your scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5b12bd3-a2fc-4df4-97ae-31bd3e984ab3/05-placing-sky-light.png)

### Adjusting Atmospheric Directional Lights

When you've enabled **Atmosphere Sun Light** on your **Directional Light(s)** and set the **Atmosphere Sun Light Index** for each, you can quickly adjust each light's position using the following keyboard shortcuts:

-   **Right Ctrl + L** with mouse movement will adjust the Directional Light set to index 0. Typically this would be the Sun.
-   **Right Ctrl + L + Shift** with mouse movement will adjust the Directional Light set to index 1. Typically this would be the Moon.

Moving these light sources will affect the atmosphere based on properties set in the Sky Atmosphere component for each Directional Light.

## Sky Atmosphere Model

Simulating the sky and atmosphere requires several properties that mimic the look and feel of a real-world atmosphere. These properties can be used to define the look of the sky and atmosphere by scattering light in an appropriate and accurate manner. By default, the Sky Atmosphere component represents the Earth.

For an Earth-like planet, the atmosphere is made up of multiple layers of gasses. They themselves are made up of particles and molecules that have their own shape, size and density. When photons (or light energy) enter the atmosphere and collide with the particles and molecules there, they are either scattered (reflected) or absorbed (see below).

![Particle Light Interaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47c9ee59-842d-429c-9267-7950fd238e09/06-particle-light-interaction.png)

(1) Incident Light from the Sun; (2) Particles in the Atmosphere; (3) Redirected Light Energy.

The Sky Atmosphere system simulates absorption with Mie scattering and Rayleigh scattering. These scattering effects enable the sky to appropriately change colors during time-of-day transitions by simulating how the incident light interacts with particles and molecules in the atmosphere.

The sky color changes depending on the time-of-day simulation when using the Sky Atmosphere component.

### Rayleigh Scattering

The interaction of light with smaller particles (such as air molecules) results in **Rayleigh scattering**. This type of scattering is highly dependent on the light wavelength. For instance, in the Earth's sky, blue scatters more than other colors, giving the sky its blue color during the daytime. However, at sunset, it appears red because light rays need to travel further in the atmosphere. After long distances, all blue light is scattered away before other colors, resulting in colorful sunsets full of yellow, orange, and red colors.

![Rayleigh Scattering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbdbc6db-5e21-4093-8aa1-36d090895b09/07-rayleigh-particle-shape.png)

(1) Incident light; (2) Small particles in the atmosphere; (3) Rayleigh scattered light energy.

In an Earth-like atmosphere, when sunlight interacts with small particles (1) in the atmosphere (2), Rayleigh scattering happens throughout the atmosphere. The upper atmosphere is less dense compared to the lower atmosphere near the Earth's surface (3).

![Rayleigh Atmosphere Interaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e77b518-1aab-4fa7-8b62-c1b35267e6ad/08-rayleigh-atmosphere-interaction.png)

Increasing or decreasing the density of particles in the atmosphere causes light to scatter more or less.

  ![Decreased Rayleigh Scattering Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe38a8f6-bd8d-4263-aac4-e2a4f31b5aea/09-ray-leigh.png) ![Default Rayleigh Scattering Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c70c46d4-9682-4a4e-9264-bb0f7a98d7df/10-ray-leigh2.png) ![Increased Rayleigh Scattering Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a16d195-5794-4812-a57c-f8e40662647c/11-ray-leigh3.png)

**Drag the slider to see the effects of decreasing and increasing the Rayleigh Scattering Scale. (Left to right, 1–3)**

1.  **Decreased** scattering causes light to scatter less through the atmosphere. This is 10x less dense than Earth's atmosphere.
2.  This is representative of an Earth-like atmospheric density.
3.  **Increased** scattering allows light to scatter more through the atmosphere. This is 10x more dense than Earth's atmosphere.

### Mie Scattering

The interaction of light with larger particles—such as those from dust, pollen, or air pollution—suspended in the atmosphere results in **Mie scattering**. These particles are referred to as aerosols and can be caused naturally or by human activity. Incident light that follows the Mie scattering theory usually absorbs light, causing the clarity of the sky to appear hazy by occluding light. Light also usually scatters more forward, resulting in bright halos around the light's source, such as around the sun disk in the sky.

![Mie Scattering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44a418d5-427a-465c-92b3-3d3ef20a3f88/12-mie-particle-shape.png)

(1) Incident light; (2) Large particles in the atmosphere; (3) Mie-scattered light energy.

Increasing or decreasing the aerosol density causes more or less clarity in the sky, contributing to how hazy it looks.

  ![Decreased Mie Scattering Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d09e971d-ae4d-4c7c-802b-b7684baae8bd/13-mie.png) ![Default Mie Scattering Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/675d51ea-17a7-4dc5-90f9-33edde180bb5/14-mie2.png) ![Increased Mie Scattering Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c0e7e87-fb0f-4610-ab78-943d4b1f2f2c/15-mie3.png)

**Drag the slider to see the effects of decreasing and increasing the Mie Scattering Scale. (Left to right, 1–3)**

1.  **Decreased** particle density allows the sky to appear more clearly. It has less haze and light is scattered less directionally.
2.  Default Mie scattering scale.
3.  **Increased** particle density causes the sky to become occluded. It also causes the sky to appear hazy with the strong forward scattering lob around the incident light direction.

### Mie Phase

The *Mie Phase* controls how uniformly light scatters when interacting with larger aerosol particles in the atmosphere. With Mie scattering, light usually scatters more forward, resulting in bright halos around the light's source, such as around the sun disk in the sky.

![Mie Phase](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c91da6e7-9a12-42d2-bdd7-1dc14864d463/16-mie-phase-function-shape.png)

(1) Incident Light; (2) Larger particles in the atmosphere; (3) Stronger Mie-scattered light energy.

Use the **Mie Anisotropy** property to control how uniformly Mie scattering happens across the atmosphere.

  ![Decreased Mie Anisotropy Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3d29e6b-4d15-4fc8-82fd-4e736088f472/17-mie-phase.png) ![Default Mie Anisotropy Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c48be76-c53e-4a97-9380-cbd1e4fc1032/18-mie-phase2.png) ![Increased Mie Anisotropy Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e871ed34-2d23-4f85-8467-2d2d696eee51/19-mie-phase3.png)

**Drag the slider to see the effects of decreasing and increasing the Mie Anisotropy of the atmosphere. (Left to right, 1–3)**

1.  **Decreasing** the Mie Anisotropy scatters light more uniformly across the atmosphere. This example is using a value of 0.
2.  Default settings mimic an Earth-like atmosphere. This example is using a value of 0.8.
3.  **Increasing** the Mie Anisotropy scatters light more directionally causing it to tighten around the light source. This example is using a value of 0.9.

### Atmospheric Absorption

The amount and colors absorbed are controlled using the **Absorption Scale** and **Absorption** color picker properties. The examples below demonstrate removing a single RGB color through the increased Absorption Scale.

  ![No atmospheric absorption](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8914598-476a-46f0-96c5-e95523b14f2e/20-absorption.png) ![Default Earth Ozone Absorption Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de3d5835-e1f0-429e-a47f-fbd93bae5d14/21-absorption2.png) ![Increased Ozone Absorption Scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d71ae372-2408-473a-8325-0ecf8e193fc1/22-absorption3.png)

**Drag the slider to see the effects of decreasing and increasing the Absorption Scale of the atmosphere. (Left to right, 1-3)**

1.  **No** atmospheric absorption.
2.  Default Earth Ozone absorption scale.
3.  **Increased** Ozone absorption scale.

The amount and colors absorbed are controlled using the **Absorption Scale** and **Absorption** color picker properties. The examples below demonstrate removal of a single RGB color through an atmosphere with increased absorption.

|   |   |   |
| --- | --- | --- |
| ![Green Absorbed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ec9c309-c84b-4fc1-a5c7-1c2889a8d412/23-absorption-green-removed.png) | ![Red Absorbed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb2b2be7-449e-4959-9939-a09dbb260437/24-absorption-red-removed.png) | ![Blue Absorbed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f4d15b8-ac38-4a38-b198-b5c82c398506/25-absorption-blue-removed.png) |
| Green Absorbed | Red Absorbed | Blue Absorbed |

Absorption of some colors may not be as noticeable during different times of day due to the way light scatters through the atmosphere.

### Altitude Distribution

The Sky Atmosphere component enables you to control the atmosphere from not only a ground perspective but also from an aerial and space one. This means that you can effectively define the curvature of your world so that transitioning from ground to sky to space feels and looks like a real-world atmosphere.

Use the following properties to achieve this use:

-   **Ground Radius** to define the planet's size.
    
-   **Atmospheric Height** to define the height of the atmosphere above which we stop evaluating light interactions with the atmosphere.
    
-   **Rayleigh Exponential Distribution** to define the altitude (in kilometers) at which Rayleigh scattering effect is reduced to 40% due to reduced density.
    
-   **Mie Exponential Distribution** to define the altitude (in kilometers) at which Mie scattering effect is reduced to 40% due to reduced density.
    

  ![Decreased Rayleigh Atmosphere Height](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e836b0b4-46be-430d-abcf-6ca5285576ff/26-alt-dist.png) ![Deafult Rayleigh Atmosphere Height](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fcef5fa-d007-4941-9434-eb31086f9448/27-alt-dist2.png) ![Increased Rayleigh Atmosphere Height](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5b9aab3-afea-4ffe-8018-e66be8ee83cf/28-alt-dist3.png)

**Drag the slider to see the effects of decreasing and increasing Rayleigh height of the atmosphere. (Left to right, 1–3)**

1.  Rayleigh Atmosphere Height is **0.8** kilometers.
2.  Default Rayleigh Atmosphere Height of **8** kilometers.
3.  Rayleigh Atmosphere Height is **80** kilometers.

### Artistic Direction

Additionally, the Sky Atmosphere component supports artistic control when designing the *look* of your project.

#### Aerial Perspective Scale

The **Aerial Perspective View Distance Scale** property scales distances from the view to surfaces to make them look thicker when viewed from a high enough distance above the ground surface.

  ![Aerial Perspective View Distance Scale setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e7942b0-2188-4235-ada8-5641c375b621/29-aerial-perspective.png) ![Aerial Perspective View Distance Scale increased](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1c8d417-85eb-41f0-a56b-1d48b86b4837/30-aerial-perspective-increased.png) ![Aerial Perspective View Distance Scale doubled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5355bffb-ab27-4012-8c50-261a8727b25d/30-aerial-perspective-increased.png)

**Drag the slider to change the Aerial Perspective View Distance Scale property. (Left to right, 1-3)**

1.  Some atmospheric properties were set up for this scene.
2.  The same scene with the Aerial Perspective View Distance Scale increased slightly.
3.  The same scene with Aerial Perspective View Distance Scale doubled.

#### Exponential Height Fog

Mie scattering is a component of the atmosphere and is a height fog simulation in itself, meaning you can already use it to create height fog in your scene without using the Exponential Height Fog component (see below).

![Sky Atmosphere's Height Fog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e01c467f-aad3-40ee-919d-6a62bb777cd1/32-sky-atmosphere-height-fog.png)

![Sky Atmosphere | with Exponential Height Fog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80bf73eb-0e3b-446b-89cf-5f6070ce41e6/33-sky-atmosphere-with-expo-height-fog.png)

Height fog produced from the Sky Atmosphere component without Exponential Height Fog component.

Should your project require **Exponential Height Fog**, it can be enabled in the Project Settings under the Rendering category by setting **Support Sky Atmosphere Affecting Height Fog**. Contribution from height fog is additive; it applies sky atmosphere height fog on top of the existing faked colors provided by the Exponential Height Fog component. To have Sky Atmosphere component affect and influence Exponential Height Fog, you'll need to set Fog Inscattering Color and Directional Inscattering Color to Black using their respective color pickers.

![Set Fog Inscattering Color and Directional Inscattering Color to Black using their respective color pickers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f408191-48da-4691-b032-8ecf55954800/34-set-inscattering-colors-to-black.png)

With these set, you can use the Sky Atmosphere's **Height Fog Contribution** setting under the **Art Direction** category to apply artistic control over how much light coming through the atmosphere affects the height fog. Below is an example of height fog contribution being adjusted.

  ![Default height fog contribution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7109008-b65b-4c19-bc26-07192c73eda5/35-default-height-fog-contribution.png) ![Half height fog contribution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fed3af95-fe86-4306-b1fb-a26e0de115b8/36-half-height-fog-contribution.png) ![Double height fog contribution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c4330d9-1839-4314-b4b7-04d818ab61ba/37-double-height-fog-contribution.png)

**Drag the slider to see the height fog contribution increase and decrease its contribution to the Sky Atmosphere component. (Left to right, 1-3)**

1.  Default height fog contribution from the Sky Atmosphere component.
2.  Half height fog contribution (0.5) from the Sky Atmosphere component.
3.  Double height fog contribution (2.0) from the Sky Atmosphere Component.

## Sky Rendering Options

The sky and aerial perspective is rendered on screen using ray marching. However, doing so for each pixel can be expensive, especially with today's standard pushing towards 4K or 8K resolution. That is why the sky is evaluated in a few lookup tables (LUTs) at low resolution. Those LUTs are:

By default, all of these LUTs are all evaluated, but using the examples below you can determine the needs for your own projects.

| Type of LUT Used | Description |
| --- | --- |
| **FastSkyViewLUT** | Stores a latitude/longitude texture of the ray ray marched sky luminance around a point of view. It is applied on the sky pixels only. |
| **AerialPerspectiveLUT** | Stores the transmittance and scattered luminance into froxel (camera frustum voxel). This is used to apply **aerial perspective** on opaque and transparent meshes\*\*. |
| **MultipleScatteringLUT** | During ray marching, used to evaluate the multiple scattering contributions. |
| **TransmittanceLUT** | During ray marching, used to evaluate the remaining illuminance from the sun light for any position within the atmosphere and on the planet. |
| **DistanceSkyLightLUT** | Stores non-occluded luminance after a scatter event with a uniform phase function. |

Many of these settings allow you to control the LUT's performance and visual quality for your project. For additional details about them, see the [Sky Atmosphere Properties](/documentation/en-us/unreal-engine/sky-atmosphere-component-properties-in-unreal-engine) page.

## Rendering the Sky using a Skydome Mesh

For some projects, you will want to position the skydome mesh around the world, enabling artists to control the way the sky is composited with clouds, stars, sun and any other celestial bodies.

To set up a skydome mesh to work with the Sky Atmosphere component, you'll need to set the following in its Material:

-   **Blend Mode:** Opaque
-   **Shading Model:** Unlit

The *sky* material is rendered as the last opaque mesh during the base pass, meaning that aerial perspective will not be applied on it to avoid double contribution. However, height fog and volumetric fog will continue to be applied, if used.

In this material, you will have the freedom to compose the sky, sun disk, clouds and aerial perspective. Also, you will have to compute lighting on the clouds and other elements in the sky. Several Material Expressions can be used to achieve this in your materials. You can find them by searching the term "SkyAtmosphere" in the Material Editor.

#### Customized Sky Material

When creating your own *sky* material, which has customized clouds, planets, sun, or other object, you should enable the **Is Sky** flag in the **Material** advanced properties. However, keep in mind that it disables contribution from aerial perspective (atmospheric fog) of the Sky Atmosphere component, but does apply height and volumetric fog to the scene from the Exponential Height Fog component.

For additional information about these Material Expressions, see the [Sky Atmosphere Properties](/documentation/en-us/unreal-engine/sky-atmosphere-component-properties-in-unreal-engine) page.

The shape of the skydome mesh is important when using some of these expressions since they will drive evaluation of those values. For example, if you use the functions to evaluate lighting on clouds, you can assume the skydome pixel world position represents the cloud world position in the atmosphere.

### Time of Day Example Level

A working example template map demonstrating a skydome mesh with a material using the Sky Atmosphere Material Expressions is available within Unreal Engine.

![Time of Day Example Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75c4373a-fe9d-445f-b204-8ef098abae62/38-sky-atmos-time-of-day-map.png)

This Level is located in the Engine Content folder under `Engine/Content/Maps/Templates`, or you can use the main menu to create a new level and select the TimeOfDay\_Default Level.

## Planetary Atmospheres Viewed from Space

In addition to creating beautiful atmospheres from a planet's surface, the Sky Atmosphere system is capable of creating a planetary atmosphere viewed from space. Without any special setup, you can even move seamlessly from the planet's surface through the atmosphere to outer space.

This video uses assets and materials that are not part of the Sky Atsmosphere system, such as the star field and meshes that represent the planet surface.

The following properties are useful when setting up a planet to be viewed from outer space (or even just a very high altitude):

-   **Ground Radius** define the size of your planet (measured in kilometers).
-   **Atmosphere Height** defines the height of the atmosphere above the planet's surface (measured in kilometers).
-   **Rayleigh Exponential Distribution** defines the altitude at which the Rayleigh effect is reduced to 40%.

Below are some examples using demonstrating different planetary atmospheres using variations of these three properties:

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
| **Ground Radius:** 6360 km | **Ground Radius:** 300 km | **Ground Radius:** 300 km | **Ground Radius:** 300 km | **Ground Radius:** 300 km |
| **Atmosphere Height:** 100 km | **Atmosphere Height:** 100km | **Atmosphere Height:** 100 km | **Atmosphere Height:** 100 km | **Atmosphere Height:** 300kn |
| **Rayleigh Distribution:** 8 km | **Rayleigh Distribution:** 8 km | **Rayleigh Distribution:** 2 km | **Rayleigh Distribution:** 32 km | **Rayleigh Distribution:** 32 km |

Click images for full size.

### Moving the Atmosphere

The Sky Atmosphere component is freely movable within Level using the selectable **Transform Mode**. Choose from the following options:

-   **Planet Top at Absolute World Position** places the top ground level of the atmosphere at the world origin coordinates (0,0,0) in the scene. The Sky Atmosphere is not movable when this option is selected.
-   **Planet Top at Component Transform** places the top ground level of the atmosphere relative to the component's transform origin. Moving the transform of the Sky Atmosphere component, or one that it is a child of, moves the atmosphere within the level.
-   **Planet Center at Component Transform** places the atmosphere centered to the component's transform origin. Moving the transform of the Sky Atmosphere component, or one that it is a child of, moves the atmosphere within the level.

The Sky Atmosphere component can be parented to objects in the scene, such as a *planet* mesh.

### Atmosphere Transmittance

Light transmittance through the atmosphere is optimized for ground-level views; a single transmittance is evaluated for the top of the planet, but for a planetary view, the transmittance should be evaluated per pixel for the atmosphere terminator to look correct. This also enables the atmosphere to cast shadows on nearby moons, or other celestial objects.

![Transmittance: | Look-up Table (LUT)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfd03deb-5e9d-41fd-9776-8bab988b3585/44-transmittance-lut.png)

![Transmittance: | Per Pixel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d2e11ad-16c3-4fd7-a316-807494e20f8a/45-transmittance-per-pixel.png)

Per pixel transmittance also enables shadowing of objects in outer space, such as nearby moons and other celestial objects, according to properties set on the Sky Atmosphere component.

![Transmittance Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33f59625-668f-4a79-b203-8d6719c8f4e5/46-transmittance-off.png)

![Transmittance Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0298cbf6-0954-401f-b06a-46cad77ed1f9/47-transmittance-on.png)

Enable per pixel transmittance on your **Directional Light** by ticking the checkbox for **Per Pixel Atmosphere Transmittance**.

### Moving from Ground to Outer Space

The Sky Atmosphere system is optimized for scenes that are on ground level. However, there is nothing preventing you from traveling from the ground to a high aerial view, or even outer space. While the transition through the atmosphere should be seamless—without a noticeable transition—from the look-up tables (LUTs) to per pixel tracing, you may sometimes experience a hitch or when this happens.

This optimization can be disabled by setting the following console command values to **0**:

-   r.SkyAtmosphere.FastSkyLUT
-   r.SkyAtmosphere.AerialPerspectiveLUT.FastApplyOnOpaque

Once disabled, it is worth noting that you may encounter the following issues. These are some suggestions to help you work around them for your project to find a balance that best fits your project.

-   A high-frequency pattern can become visible when it should be absorbed by temporal anti-aliasing (TAA). However, when moving the camera very fast, there is a camera cut that happens—restarting TAA—so it is visible in space views.
    
-   Due to the way samples count is based on distance, samples become visibly large (as circles) in the atmosphere. Visibility of the samples is a side-effect of the density of medium in the atmosphere being higher, and very concentrated, close to the ground, which is a typical ray marching issue. You can solve this in a couple of ways:
    
    -   Trade performance for quality increase by increasing the number of samples with **r.SkyAtmosphere.SampleCountMax** or **r.SkyAtmosphere.DistanceToCountMax**.
    -   Set up logic to adjust and tweak atmospheric properties when in outer space to have less particles near the ground, making them more uniform and height distributed.

## Atmosphere Sunlight Shafts and Quality

Shadowing from a **Directional Light** source is used to create sunlight shafts within the atmosphere for ground-level and space views.

**Ground view atmosphere sunlight shafts:**

![Opaque Objects Shadowing | on the Atmosphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/743038bd-402d-4111-997d-4e20f899905c/48-atmosphere-shadowing-opaque-only.png)

![Opaque Objects and Cloud Shadowing | on the Atmosphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5cb6e5b-bd02-44e9-ab5e-45414a7359ba/49-atmosphere-shadowing-with-clouds.png)

**Space view atmosphere sunlight shafts:**

![Opaque Objects Shadowing | on the Atmosphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a202e8fd-4d65-4863-806f-a69e2b658ee8/50-space-shadowing-opaque-only.png)

![Opaque Objects and Cloud Shadowing | on the Atmosphere](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ae4205c-5d70-4af3-ba69-7f12f8a81def/51-space-shadowing-with-clouds.png)

Use the following properties to enable and control sunlight shafts:

-   Enable **Cast Shadow on Atmosphere** to cast shadows from opaque objects. Also, enable **Cast Cloud Shadows** to enable shadow casting from cloud materials when using the [Volumetric Cloud](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) system.
-   Set a high value for the **Dynamic Shadow Distance**. For instance, the examples below used a shadow distance of 100000000 units (or 1000 kilometers).
-   For outer space views, enable **Per Pixel Atmosphere Transmittance** to apply accurate planetary shadowing that also casts shadows on nearby celestial objects, such as a moon.

You can further improve the quality of sunlight shafts using the following:

-   The tracing quality of the atmosphere is scalable using the Sky Atmosphere component's **Trace Sample Count Scale** property. This property is important when generating LUTS, or when using per pixel tracing. The maximum number of samples is clamped but can be increased by using the console command `r.SkyAtmosphere.SampleCountMax`. Also, keep in mind that the number of samples only reach the specified kilometers set by `r.SkyAtmosphere.DistanceToSamplesCountMax`.
    
-   Improving the overall quality of sunlight shafts within the atmosphere is handled by increasing the `r.SkyAtmosphere.FastSkyLUT.Width` and `r.SkyAtmosphere.FastSkyLUT.Height` values. Quality can further be improved for fog on opaque and translucent surfaces by increasing the width of `r.SkyAtmosphere.AerialPerspectiveLUT.Width`.
    
    To use the fast sky LUT commands, `r.SkyAtmosphere.FastSkyLUT` must not be disabled.
    
    Use caution when increasing the Aerial Perspective LUT. It uses a 3D volume texture. Increasing its size can significantly increase memory usage.
    
-   Achieving cinematic quality of atmosphere rendering is done by disabling the Sky View and Aerial Perspective LUTs optimizations, which use a lower resolution to be performant. They can be disabled by setting `r.SkyAtmosphere.FastSkyLUT` and `r.SkyAtmosphere.AerialPerspectiveLUT.FastApplyOnOpaque` to **0**. Atmosphere will become slower to render but produces fewer visual artefacts with high-frequency detail that appear in some areas, such as a planet's shadow or its scattering lobe. You'll also want to increase the tracing quality on the Sky Atmosphere component (see above).
    

## Volumetric Cloud Shadow Quality with a Directional Light

When adjusting the quality of volumetric cloud shadows on a directional light, there are a few things to keep in mind with settings that need to be adjusted.

-   The Volumetric Cloud property **Trace Sample Count Scale** needs to be increased.
-   The Directional Light property **Cloud Shadow Ray Sample Count Scale** must be increased.
-   The console variables `r.SkyAtmosphere.FastSkyLUT.Width` and `r.SkyAtmosphere.FastSkyLUT.Height` need to be compensated to adjust for the low default resolution of the cloud's shadow quality to provide more defined shadows.
    -   We recommend using a value of 256 for the width and height as a starting point.

## Visualization and Debugging

The Sky Atmosphere visualization and debugging view enables you to see—in real time—the changes you make to the atmosphere settings.

![The Sky Atmosphere visualization and debugging view is enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a88f3032-5934-491a-84c4-a866a602b03b/52-sky-atmosphere-visualization.png)

1.  The **Hemisphere View** shows a visual representation of your atmosphere, taking into account Rayleigh and Mie scattering along with Absorption.
2.  The **Time-of-Day Preview** displays different times of day based on the settings that are applied to the Sky Atmosphere component.
3.  The **Graph View** shows a representation of Rayleigh, Mie, and Absorption values within the Sky Atmosphere component's set Ground Level and Atmosphere Height.

Enable the Sky Atmosphere visualization to be drawn on screen using the command:

```
	`ShowFlag.VisualizeSkyAtmosphere 1`
Copy full snippet
```
ShowFlag.VisualizeSkyAtmosphere 1

## Supported Platforms

The Sky Atmosphere component supports the following platforms to provide a scalable atmosphere system:

| Feature | Mobile | XB1 / PS4 | XBX / PS5 | Low-end / High-end PC |
| --- | --- | --- | --- | --- |
| **Sky Atmosphere** | YES\* | YES | YES | YES |

\* Requires a skydome mesh with a material that has **Is Sky** enabled.

## Additional Notes

-   **Setting up Physically-Based Sky Lighting**
    -   When the sun is at its zenith, it should be set to 120000 lux (or cd:sr\*m^2) for an angular diameter of 0.545 degrees.
    -   The total Lux on a white diffuse surface with a perpendicular sun at its zenith should be around 150000 Lux.
        -   Sky contribution would be 20% of that total.
        -   Disable Ambient Occlusion when measuring this value in the Engine using the luminance/illuminance meter that is available in the HDR (Eye Adaptation) Visualization tool (Show > Visualize).
        -   **Multiscattering** in the Sky Atmosphere component should be equal to 1 and Earth Albedo is 0.4 (linear) by default.
    -   When the moon is at its zenith, it should be set to 0.26 Lux for an angular diameter of 0.568 degrees.
-   **Why does the ground/lower hemisphere appear dark?**
    
    When you are close to the ground, there isn't any fog, so you don't get the scattering effect nor any fog color. This means for the lower hemisphere of a virtual planet, it is black. To address this, try the following:
    
    -   Populate the scene with a terrain or mesh to represent the planet surface.
    -   Use an Exponential Height Fog component as a lower hemisphere color filler.
    -   Place your terrain or mesh surface at a higher altitude.
-   **Why does the second Directional Light source have a lower impact on the sky?**
    
    Currently, multi-scattering is not evaluated for the second light source.
    
-   **Why are texels visible on the skydome?**
    
    Try increasing the resolution of the FastSkyViewLUT (`r.SkyAtmosphere.FastSkyViewLUT.SampleCountMax`) if texels appear on the sky. If texels appear on fogged elements, increase the resolution of the AerialPerspectiveCameraVolumeLUT (`r.SkyAtmosphere.AerialPerspectiveLUT.DepthResolution`).
    
-   **Do atmospheric lights work when the camera is not close to the +Z North Pole of the planet?**
    
    As an optimization, sun light transmittance effect on surface lighting is only evaluated as if the camera is at the top of the planet (over +Z position). This will be improved in a future release based on feedback.
    
-   **Can you render multiple planetary atmospheres on screen at once?**
    
    This is not currently supported with this version of the Sky Atmosphere system.
    
-   **Noise, aliasing, and some rings of different colors are visible**
    
    When you have high-frequency elements or values that generate high spikes in the atmosphere close to the ground that are hard to catch, resolve this using one of two ways:
    
    -   Increase the Sky Atmosphere sample count using `r.SkyAtmosphere.SampleCountMax`.
    -   If you're using the FastSky LUT instead of per-pixel ray marching, use `r.SkyAtmosphere.FastSkyLUT.SampleCountMax`. Additional details can be found in the [Sky Rendering Options](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine#skyrenderingoptions) section above.
-   **Cloud Rendering Expense**
    
    Cloud rendering will use the expensive path when `r.PostProcessing.PropagateAlpha` is enabled and when any features, such as Exponential Height Fog, Volumetric Cloud, and Sky Atmosphere, have alpha holdout enabled.