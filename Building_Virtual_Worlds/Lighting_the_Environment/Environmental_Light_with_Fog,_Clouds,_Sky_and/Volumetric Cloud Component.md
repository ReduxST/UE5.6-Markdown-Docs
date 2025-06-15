# Volumetric Cloud Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:39

---

The Volumetric Cloud component is a physically-based cloud rendering system that uses a material-driven approach to give artists and designers the freedom to create any type of clouds they need for their projects. The cloud system handles dynamic time-of-day setups that is complemented by the [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) and [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) using the real time capture mode. The system provides scalable, artist-defined clouds that can adapt to projects using ground views, flying, and ground to outer space transitions.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a75c0db7-50bb-4aab-a6e3-ea7a91d0cc2c/vt_cloudexamples.png)

## How are clouds rendered?

Previously, rendering clouds in real-time for games and cinematics have primarily been achieved through static materials applied to a sky dome mesh or a similar approach. Now, the volumetric cloud system uses a three-dimensional volume texture that is ray-marched to represent cloud layers in real-time. The material-driven approach provides the most flexibility for artists and designers to create clouds that can move across the sky, of any type, and can handle different times of day.

The sections that follow explore and break down the cloud system's elements that contribute to rendering them for real-time rendering.

### Ray Marching the Cloud Volume

The participating media that makes up clouds require complex lighting simulations that either aren't possible, or are too expensive, for real time simulation on consumer-grade hardware. The Volumetric Cloud system employs ray- marching and approximation to simulate cloud rendering for scalable real-time performance across many supported platforms and devices. This makes it possible to support real time time-of-day simulations that support the multiple light scattering effect of lighting, shadowing from clouds and onto clouds, light contribution from the ground onto the bottom layer of clouds, and much more.

### Light Multiple Scattering

Light rays that travel through a volume have the potential to scatter on particles within the volume before reaching your eye, or a camera sensor. This effect of light is called multiple scattering, and it is what defines the distinct appearance of clouds. In a cloud, the droplets that make up the cloud usually lead to an albedo that is close to a value of 1, meaning that light is almost never absorbed within the volume. Light that is not absorbed passes through the volume making the scattering effect very complex in the process. The multiple scattering effect of the participating media affects light travel through the cloud volume; it's what makes them look bright while also appearing very thick.

The complexity of multiple scattering in real-time rendering is solved by using an approximation of realistic scattering by tracing multiple octaves (or steps) of light transmittance in the volume material. The **Volumetric Advanced Material Output** expression enables you to set the number of octaves used along with the amount of multiple scattering contribution, occlusion, and eccentricity that happens.

The example below shows the difference between no octaves used (single scattering), one octave, and two octaves of multiple scattering approximation. High octaves apply additional scattering approximations to your cloud material but make the shader more expensive in the process.

For games projects, it is recommended to only use a single octave of light multiple scattering for performance considerations. However, you can use high Contribution and low Occlusion values on the **Volumetric Advanced Material** expression in your cloud material to similar effect without impact to performance. See the Volumetric Material section below.

**Ground View:**

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea32a389-202c-4268-8536-59ab759fb449/octaves_groundview_0.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8305906b-e061-4e52-9705-de14f457265a/octaves_groundview_1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f09cedd-4c0c-48de-ae19-bb215ce8170c/octaves_groundview_2.png)

Drag the slider to change the number of Multiple Scattering Approximation Octaves used from 0 - 2.

**Higher Altitude View:**

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5ad0755-cb2a-410e-b9ec-0346215fb7ff/octaves_cloudview_0.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3f283ad-8784-42d8-a654-f09a6d0f2876/octaves_cloudview_1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5c263f3-6795-41d9-bdb1-66dfde255dd2/octaves_cloudview_2.png)

Drag the slider to change the number of Multiple Scattering Approximation Octaves used from 0 - 2.

### Cloud Occlusion and Shadowing

An important aspect of clouds is due to how they occlude light and cast shadow on surfaces. Cloud occlusion and shadowing is primarily handled by atmosphere lights and the volume material used to represent the cloud. These components enable you to control different aspects that define the look of your clouds, such as having sunlight shafts, or cloud self shadowing.

#### Volume Ray Marching and Shadow Maps

There are two modes for cloud shadowing available which can be toggled in the cloud material used; the default **Ray Marched** and **Beer Shadow Maps** (BSM).

![Ray Marched](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5674a151-a062-4658-8a96-6a1a56132e63/shadows_raymarched.png)

![Beer Shadow Maps](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c9ba6e8-7f50-4562-8483-77b747ddcd42/shadows_beershadowmaps.png)

-   **Ray marching the volume shadow** uses secondary ray marching to get sharp, colored shadows but is limited in distance that shadows can be traced due to the limited number of samples that can be used. Ray-marched shadows are good for ground to sky to space transitions even though they are more expensive.
-   **Beer shadow maps** use cascaded shadow maps to support far shadow distances for clouds and casting shadows on the ground. They are also faster to render, but are less accurate and lack volumetric self shadow color. Beer shadow maps are usually enough for clouds viewed from the ground.

For console platforms, such as Xbox One and PlayStation 4 or other systems using similar specifications, Beer shadow maps are recommended for cloud shadowing.

Toggle between these modes inside of your cloud volume material by adding a **Volumetric Advanced Material Output** expression to your material graph. With the node selected, toggle the **Ray March Volume Shadow** checkbox from the Details panel to switch between two types of shadowing.

![Cloud shadowing mode selection from Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32d076a5-6649-4d61-94ec-bf867ee2bcc0/material-shadows-type-selection.png)

#### Directional Light Interactions and Shadowing

Atmosphere lights, such as ones for the sun and moon, provide control for cloud and atmospheric shadowing. With them, you can control the strength of shadows, the distance that cloud shadowing happens from the current camera position (in kilometers), and whether clouds can self-shadow and cast shadows into the atmosphere, to name a few.

![Directional light cloud properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/baaf045f-4ff6-4fa3-828d-5824d0859b77/directional-light-cloud-properties.png)

Enabling **Cast Cloud Shadows** on an atmospheric light allows for the cloud volume to shadow scene elements and to cast sunlight shafts (also called God Rays) within the atmosphere, whereby sunlight shafts are defined by the Sky Atmosphere component.

![Cloud Shadows: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6dca1682-7402-43cb-b28b-8f5c5c7567fd/shadows_cloudshadows_off.png)

![Cloud Shadows: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb7821ac-d05d-4c76-9432-1ac1370dae51/shadows_cloudshadows_on.png)

The **Cloud Shadow Map Resolution Scale** drives the resolution and performance cost of the sunlight shafts. Reducing the radius of the cloud shadow map around the camera with the **Cloud Shadow Extent** property can help focus the shadow map resolution for sharper, better results.

Casting shadows onto the atmosphere and clouds from opaque objects is enabled with **Cast Shadows on Atmosphere** and **Cast Shadows on Clouds**. Shadowing for large objects is achieved using a large enough **Dynamic Shadow Distance** or using **Far Shadow Distance** on the Directional Light to shadow objects that enable the **Far Shadow** flag in their details.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed0c4cd9-951d-4763-aad5-f52798d791d9/directionallight_opaqueshadowsonclouds.png)

Simulating light multiple scattering within participating media using the octave approximation can result in some energy being lost. The atmosphere light property **Cloud Scattering Luminance Scale** provides a nice counterbalance that enables you to scale the light contribution using a color picker, making it possible to have more interesting and natural light scattering without the added expense.

These are some examples with different Cloud Scattering Luminance Scales.

Click image for full size.

#### Real Time Sky Light Capture

The Sky Light component provides a Real Time Capture mode that handles interactions with atmosphere, clouds, height fog, and opaque meshes using an Unlit material that is tagged Is Sky. This mode makes it possible to create natural-looking and dynamic time-of-day simulations without sacrificing performance.

Learn more about the Real Time Capture mode and other optimizations in the Sky Light page.

#### Sky Lighting Cloud Ambient Occlusion

Soft ambient shadowing is an important part of defining the natural look of clouds. The [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) component uses the **Cloud Ambient Occlusion** properties to control how much light clouds can block coming from contribution of the sky and atmosphere lights. These properties can be found under the **Atmosphere and Cloud** section in the Details panel of the Sky Light.

The comparison below shows ambient occlusion enabled with increased strength, which controls how much light contribution sky and atmosphere lights have by progressively reducing the amount of light multiple scattering that happens.

![Cloud Ambient Occlusion Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26f53cb8-89ee-410f-bfb9-9466f8b5a89f/skylight_cloudao_off.png)

![Cloud Ambient Occlusion Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1393192-b2ad-4010-a581-09c63ab09f63/skylight_cloudao_on.png)

Skylight AO contribution on the atmosphere and clouds can be described as:

-   Shadow Tracing Costs:
    -   When using secondary marching per sample, the cost is driven by values setup on the Volumetric Cloud component with **Shadow View Sample Count Scale**.
    -   When the cloud samples the Directional Light Beer Shadow Map (which is also used to cast shadow on meshes), then a single evaluation of the shadow map is done at each ray marched position. The Beer Shadow Map generation is driven by information coming from the setup on the Directional Light component with **Cloud Shadow Ray Sample Count Scale**.

## Setting Up and Using Volumetric Clouds

The volumetric clouds system is a core part of the available atmospheric components that make up the sky and planet's atmosphere. The following sections will help you get started in setting up and using these components together with the cloud system.

### Initial Level Setup

Create a new level (or use an existing one) that contains the following components:

-   A **Directional Light** with **Atmosphere Sun Light** enabled to represent the sun or moon.
-   A **Sky Atmosphere** component to represent the planet's atmosphere.
-   A **Sky Light** with **Real Time Capture** optionally enabled if you want to have dynamic time-of-day simulation.
-   A **Volumetric Cloud** component with a volume material assigned to represent the clouds in the sky.

Simplify creation and editing of atmospheric components within your level by using the Environment Light Mixer. It provides relevant settings for each component within a single panel.

For more information, see [Environment Light Mixer](/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine).

### Sky Light Cloud Reflections Quality

The [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) component provides scene reflections for volumetric clouds. The Volumetric Cloud component enables you to control the number of samples used to ray march reflection surfaces in the scene from the Details panel under the **Cloud Tracing** section. You can scale the number of samples used for reflections of clouds and for the shadowed reflections of clouds.

      ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a0359aa-811b-41be-b956-c130f8190f15/skylightreflectionquality_0_25.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84b0cd0c-c1f6-421a-8003-1c85c0ec361e/skylightreflectionquality_0_50.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab46cf33-5d1a-40ee-86d8-e7ae88a2d91e/skylightreflectionquality_0_75.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc1dd71a-844a-43f5-801f-75cf687e6995/skylightreflectionquality_1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53f39806-4df6-4a8e-a0c2-7d052335cd69/skylightreflectionquality_2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ec426bb-2adf-45ed-ba2f-46706c663b3c/skylightreflectionquality_4.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42447737-5a88-4936-8ae6-fc6f4cbd6d85/skylightreflectionquality_8.png)

Drag the slider to see progressive increase of samples used when tracing the cloud's reflection ray sample counts: 0.25, 0.5, 0.75, 1 (Default), 2, 4, and 8.

The properties **Reflection Sample Count Scale** and **Shadow Reflection Sample Count Scale** are clamped. The following commands can be used to increase scale and sample counts:

-   `r.VolumetricCloud.ReflectionRaySampleMaxCount`
-   `r.VolumetricCloud.Shadow.ReflectionRaySampleMaxCount`
-   `r.VolumetricCloud.ViewRaySampleMaxCount`
-   `r.VolumetricCloud.SampleMinCount`
-   `r.VolumetricCloud.DistanceToSampleMaxCount`

See [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) for more information on its real time capture mode and reflection quality properties.

### Ray Marching Quality Modes

The cloud system provides scalable quality modes that fit many gameplay types from standard to fast-paced gameplay that requires ground-to-space movement. It also supports cinematic quality for projects that are less concerned with running in real time.

The quality modes are defined by the command **r.VolumetricRenderTarget**:

-   Reactive modes supporting cloud intersections with opaque surfaces but with traces completed at a lower resolution: **\* r.VolumetricRenderTarget.Mode 0** is the recommended option for quality. It supports fast-paced gameplay that may have ground-to-space transitions, or flying through clouds. Clouds are fast to trace but can appear to have low resolution. Traces happen at quarter resolution, reconstruction at half resolution, and upsample on screen at full resolution.
    -   **r.VolumetricRenderTarget.Mode 1** balances quality with performance to fit a lot of types of gameplay that are good for ground views. This mode is more expensive but looks higher quality. Traces happen at half resolution, reconstruction and upsample on screen at full resolution.
-   A less reactive mode but looks full resolution:
    -   **r.VolumetricRenderTarget.Mode 2** focuses on higher quality while still supporting ground views for real-time gameplay. This mode is fast to trace and looks high resolution, but it does not support cloud intersection with opaque meshes.
-   Cinematic mode is achieved by starting with **r.VolumetricRenderTarget 0** and following the suggestions in the Achieving Cinematic Quality workflow (see below).

Quality can further be improved, or lowered, for the platforms you're intending to deploy to through console commands following r.SkyAtmosphere. *and r.VolumetricClouds.*. Also, user-facing properties can be found in the Volume Material, and on the Volumetric Cloud and Directional Light components.

## Volumetric Cloud Shadow Quality with a Directional Light

When adjusting the quality of volumetric cloud shadows on a directional light, there are a few things to keep in mind with settings that need to be adjusted.

-   The Volumetric Cloud property **Trace Sample Count Scale** needs to be increased.
-   The Directional Light property **Cloud Shadow Ray Sample Count Scale** must be increased.
-   The console variables `r.SkyAtmosphere.FastSkyLUT.Width` and `r.SkyAtmosphere.FastSkyLUT.Height` need to be compensated to adjust for the low default resolution of the cloud's shadow quality to provide more defined shadows.
    -   We recommend using a value of 256 for the width and height as a starting point.

### Achieving Cinematic Quality

This is an advanced workflow that bypasses optimizations used by the engine for real time rendering of clouds and sky and can significantly impact performance.

Achieving cinematic (or per pixel) quality for the Sky Atmosphere and Volumetric Clouds components is handled through some commands, setting attributes in your cloud material, and by increasing the number of samples used to trace the atmosphere and cloud volume.

![With real time quality settings applied](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0123c23-0960-420d-a713-52ba52412262/modes_defaultquality.png)

![With cinematic quality settings applied](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e37307a6-0f02-4cfa-b0ce-6cee32fca755/modes_cinematicquality.png)

The steps below are the primary starting points to achieving the highest quality clouds and atmosphere in your project.

1.  Set **r.VolumetricRenderTarget** to **0** to start enabling cinematic quality results.
2.  Set **r.VolumetricCloud.HighQualityAerialPerspective** to **1** to enable cinematic aerial perspective for clouds to use high quality ray tracing instead of low resolution LUTs.
3.  Set the following on the Volumetric Cloud component:
    -   Under the **Cloud Tracing** section, increase the sample count scale for **View, Reflections,** and **Shadows**. Sample counts can be increased for each of these scales using commands found in their tool tips.
    -   Enable the **Use per Sample Atmospheric Light Transmittance** property to apply atmosphere transmittance per sample instead of using the Directional Light's global transmittance.
4.  Set the following in your Volume Cloud Material using the **Volumetric Advanced Material Output** expression:
    -   Apply ground lighting to the bottom of cloud layers, giving more shape and color to clouds in the scene.
        -   Enable **Ground Contribution** from the Details panel. On the Volumetric Cloud component, use the **Ground Albedo** to specify the ground color used to light the cloud from below with respect to the sunlight and atmosphere.
    -   Set the number of approximations used to simulate the multiple scattering of light through the cloud volume:
        -   You can better simulate multiple scattering effects of light through the cloud volume by increasing the number of **Multi Scattering Approximation Octaves** used, up to a value of **2**.
        -   Light will scatter more through the cloud volume when applying additional octaves meaning that you'll want to adjust the **Multi Scattering Contribution** and **Multi Scattering Occlusion** values on the Volumetric Advanced Output expression to compensate.
5.  Enable the following shadowing properties of Atmospheric Lights:
    -   Set **Cast Cloud Shadow** to cast shadows from clouds onto scene elements and into the atmosphere.
    -   Set **Cast Shadows on Clouds** to cast shadows from opaque objects onto cloud layers.
        
        The Directional Light must have a large enough **Shadow Dynamic Distance** to effectively shadow large objects onto clouds.
        
        \* Choose between the following quality improvements for Sky Atmosphere based on your project needs:
6.  Choose between the following quality improvements for [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) based on your project needs:
    -   **Improve the overall quality of atmosphere rendering.**
        -   Set **r.SkyAtmosphere.FastSkyLUT** to **0**. Disabling this optimization is slower to render, but produces fewer visual artefacts with high-frequency detail that can appear in places like the earth's shadow or scattering lobe.
    -   **Increase tracing quality of the atmosphere and sunlight shafts within the atmosphere.**
        
        Requires `r.SkyAtmosphere.FastSkyLUT` to be enabled.
        
        -   Set **r.SkyAtmosphere.AerialPerspectiveLUT.FastApplyOnOpaque** to **0**.
        -   On the Sky Atmosphere component, use the quality slider **Trace Sample Count Scale** to adjust the number of samples used. If the max range isn't enough, use the command `r.SkyAtmosphere.SampleCountMax` to choose a higher limit and manually enter a value in the property field.
        -   Improve the quality of sunlight shafts by increasing the LUT sizes set with the commands **r.SkyAtmosphere.FastSkyLUT.Width** and **r.SkyAtmosphere.FastSkyLUT.Height**.
        -   Improve the quality of fog on opaque and transparent surfaces by increasing the size of **r.SkyAtmosphere.AerialPerspectiveLUT.Width**.
        
        Exercise caution when increasing this value because it is a 3D volume texture that increases memory consumption.
        

### Volumetric Material

A material using the **Volume** material domain drives the look of clouds using volume textures. A volume texture is a 3D texture that is sliced into a series of 2D textures aligned to a grid. These types of textures within a material are used for different volumetric effects, like smoke and clouds, because they work well for things like light traveling through a volume.

The volume texture below represents a series of two-dimensional images in a grid (left) that when stacked, they make a three-dimensional volume representation (right).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59b40a86-ed82-49aa-b18d-a29d300875d7/volumetexture.png)

Open and view a volume texture with the Texture Editor to display its two-dimensional image view (left), or its three-dimensional volume view (right).

Along with the attributes controllable in the Volumetric Cloud Component and Material, the volume texture is the basis that provides the initial look of your cloud and helps define what is possible. Volume textures open up the possibilities through your cloud material to create many different types of clouds and effects.

The examples below demonstrate several varieties of clouds that can be created using a single volume material with some adjustable parameters through instancing.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a73f9016-68c6-4936-86f9-594956409f96/vt_cloudexamples.png)

Your volume material has material expression input and output nodes that provide editable attributes forming the basis of your cloud material. Some of these settings have performance implications that increase or reduce the cost of the shader.

It's recommended when using these expressions to parameterize the values of these expressions to quickly and easily adjust their values in a [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine).

### Volumetric Cloud Material

The `Engine/Content` folder includes the default volume material used with the Volumetric Clounds component. This material includes parameters to create different cloud types, cloud shapes, and additional effects, such as storm clouds.

![Example Volumetric Cloud](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c225a358-647d-4b8a-beeb-422bf2d0699a/vcm-materialinstancesettings.png)

For more information on using this material and its controls to create various types of clouds, see [Volumetric Cloud Material](/documentation/en-us/unreal-engine/volumetric-cloud-material-in-unreal-engine).

### Blueprint Placed Clouds

Place individual clouds Blueprint Actors in your scene using the example set up in this plugin folder. The individually placed Blueprints in the scene can be scaled, rotated, and moved along the X and Y-axes. The Volumetric Cloud component is required to be in the scene as well along with an assigned cloud material to be used. The Blueprint Cloud Actor enables additional customization and placement of clouds within your scene.

You'll find an example setup in the `/Tools/CloudCompositing/Maps` folder in the **Composite\_Cloud\_Object Level**. Take a look at the **BP\_CloudMask\_Object** and the **BP\_CloudMask\_Generator** to see how this scene is set up and the available properties you can adjust on this Actor.

### Blueprint Painted Clouds

Start painting clouds onto your skies using this example set up to add sparse or densely-packed clouds to your scene. This example uses a play-in-editor game mode with a simple user interface to paint clouds using your mouse cursor that can scale the brush, its intensity, and more.

You'll find an example setup in the `/Tools/CloudCompositing/Maps` folder in the **Paint\_Clouds** Level. Select the **BP\_PaintClouds** Actor to explore some of the properties you can change for how your cloud is painted.

To start painting clouds, press **Play** in the main toolbar to play-in-editor. Use the following to start painting clouds in the scene:

-   **Left Mouse Button** paints the cloud volume
-   **Mouse Wheel** scales the size of the paint brush.
-   **Shift + Mouse Wheel** changes the strength of the brush strokes being painted.
-   **Shift** while painting removes painted areas.
-   **Right Mouse Button + Mouse Wheel** scales the velocity speed painted into the cloud when **Velocity** is chosen from the **Paint Mode** dropdown in the **BP\_PaintCloud** properties.

## Performance and Scalability

Managing performance and scalability across multiple platforms is important when developing your projects. The sections below contain information on scaling the quality of clouds and other features relevant to capturing and lighting clouds in your projects.

### Supported Platforms

The Volumetric Cloud and Sky Atmosphere components support the following platforms to provide a scalable atmosphere system:

| Feature | Mobile | XB1 / PS4 | XBX / PS5 | Low-end / High-end PC |
| --- | --- | --- | --- | --- |
| **SkyAtmosphere** | YES\* | YES | YES | YES |
| **Volumetric Clouds** | NO | YES\*\* | YES | YES |

\* Requires a skydome mesh with a material that has **Is Sky** enabled. \*\* To achieve acceptable performance on these platforms, it is recommended to evaluate cloud self shadowing using the shadow map approach instead of secondary tracing mentioned in the [Volume Ray Marching and Shadows Maps](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine#volumeraymarchingandshadowmaps) section.

### Controlling Cloud Tracing Quality

The cloud system performs a number of traces through the volume material. The quality of the traced result is dependent on the number of samples used. The more samples used, the higher the quality will be. The opposite is true as well, the fewer samples used, the lower the quality will be.

![Default Sample Counts (1.0)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f3b5c35-0944-468f-9573-cda80f69edfd/performance_tracingquality_default.png)

![Lowered Sample Counts (0.25)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78afe46a-916d-4360-ae2a-267b011838ce/performance_tracingquality_lowered.png)

For different platforms, it's important to strike a balance between performance and quality. The **Cloud Tracing** properties enable you to scale the tracing quality of key cloud attributes, like clouds in reflections, shadowing samples for clouds and clouds in reflections, and the distance from the camera that cloud shadowing should stop.

![The Cloud Tracing properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6eb3d9ee-7d8e-4361-b88d-7abe93f70745/performance-tracing-quality-properties.png)

Each of these properties has its own console command that can be set individually per-platform using the Device Profiles configuration (\*.ini) file. This provides a broad level of flexibility when setting target scalability across different platforms.

### Optimizing your Volume Cloud Material

The basis of rendering clouds starts with your volume material and the **Volumetric Advanced Output** and **Volumetric Advanced Input** expressions that are used in the Material Graph. While you can parameterize a lot of aspects of your cloud material to control some of its attributes through material instancing, some can only be set on this node from the base material.

The following suggestions are set on the **Volumetric Advanced Output** expression and can be used independently of each other when deciding how to optimize your project's cloud material:

-   Use **Gray Scale Material** to only consider the **R** (red) channel of the material's input parameters during evaluation. In your scene, the material response of the cloud will be grayscale but lighting of the material will still be colored.
-   Enable **Ground Contribution** if your frame budget allows. It adds some costs to tracing to sample the shadowed lighting contribution from the ground on to the bottom layer of the clouds.
-   Limit the number of **Multi Scattering Approximation Octave Counts** used to save some performance in the shader. By default, it uses single scattering (0) but can use a max of two approximation octaves to simulate the multiple scattering of light effect in the cloud volume.
-   Use the **Ray March Volume Shadow** checkbox to toggle between secondary ray marching the cloud volume or using cascaded shadow maps. Enabling cascaded shadow maps (unchecking the box) provides a performance boost and gives infinite length for shadowing even though they become less accurate and grayscale in color.
-   The **Conservative Density** attribute is used to accelerate the ray marching by skipping expensive material evaluation early on. The **X** component of the float vector (Vector3) represents the participating medium conservative density. When the value is greater than **0**, the material is evaluated, otherwise, it evaluates the next sample directly. For additional details, see Volumetric Cloud Reference.
-   Cloud rendering will use the expensive path when `r.PostProcessing.PropagateAlpha` is enabled and when any features, such as Exponential Height Fog, Volumetric Cloud, and Sky Atmosphere, have alpha holdout enabled.

### Budgeting with the Sky Light Real Time Capture Mode

The Sky Light's **Real Time Capture** mode enables 9-frames time slicing to distribute a single frame's capture over multiple frames. This optimization improves performance for achieving time-of-day simulations, making it much less costly because time slicing is only as expensive as its most costly frame. It provides you the opportunity to push quality in other areas of your frame budget without additional costs.

For example, if you were to break down the captured scene elements and their frame cost and see that Specular Convolution is taking 0.8 milliseconds (ms) per frame, but Sky and Cloud are only taking 0.6 ms, you still have room in the frame budget to increase sky and cloud quality marginally without paying additional cost.

### Conservative Density Evaluation

**Conservative Density** has been added as a way to optimize the ray marching process. Evaluating the entirety of the cloud material graph for each sample that is ray marched in the atmosphere would quickly become too expensive. To make it more cost-efficient, a user-specified conservative density is inexpensively reasonable to evaluate. For example, the material evaluation could be a top-down two-dimensional texture describing the cloud density whereby the only rule is that the conservative density must be greater than 0 where there is cloud in the atmosphere when evaluating using the **Volumetric Advanced Input** expression.

While ray marching the atmosphere, a cloud material sample is taken in two steps if the conservative density input is used:

1.  On the **Volumetric Advanced Output** node, the conservative density input (Vector 3) graph is evaluated.
2.  If the Conservative Density of X (in the Vector3) is greater than 0:
    1.  A decision to evaluate the more expensive material graph plugged into the **Main Material** node (evaluating Albedo, Emissive Color, and Extinction) is used.
    2.  The values can be accessed using the **Volumetric Advanced Input** node, which avoids computing the conservative density values that have already been evaluated in Step 1.
3.  Otherwise, if the Conservative Density of X is equal to or less than 0, the more expensive material evaluation is skipped and goes to the next sample.

Unreal Engine doesn't support dynamic branching in its material graph. The ConservativeDensity input enables dynamic branching to skip the more expensive material evaluation that can happen. When Unreal Engine natively supports dynamic branching in materials, inputs like this will be obsolete and let technical artists make decisions for what can be dynamically skipped.

### Ray Tracing and Volumetric Clouds

The cloud system doesn't support [Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) features and only takes into account the clouds as rendered into the Sky Light. Tracing volumetric clouds for reflections would be significantly costly to performance.

In instances where you want reflections on an object in the sky, placing the Sky Light Actor closer to it (in the sky) would help.