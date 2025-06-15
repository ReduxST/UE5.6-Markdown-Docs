# Sky Lights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:59

---

The Sky Light captures the distant parts of your level and applies that to the scene as a light. That means the sky's appearance and its lighting/reflections will match, even if your sky is coming from atmosphere, or layered clouds on top of a skybox, or distant mountains. You can also manually specify a cubemap to use.

## Scene Capture

The Sky Light will only capture the scene under certain circumstances:

-   For **Static Sky Lights**, updates automatically happen when building lighting.
-   For **Stationary** or **Movable Sky Lights**, updates happen once on load and only updates further when **Recapture** is called unless the [**Real Time Capture**](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine#realtimecapture) feature is enabled. Both are accessible via the **Details** panel, and Recapture can also be called via Blueprint in-game.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d37247b4-e157-4721-b2ae-540f68bbae7d/skylight_recapture.png)
    
    Details panel Sky Light Recapture button
    

If you change the texture that the skybox is using, it will not automatically know to update. You'll be required to use one of the methods above for it to update.

A Sky Light should be used instead of the Ambient Cubemap to represent the sky's light because Sky Lights support local shadowing, which prevents indoor areas from getting lit by the sky.

## Mobility

Similarly to other [Light Types](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine), the Sky Light can be set to one of the following **Mobilities**:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e9c79ae-2334-4289-98d0-11dfc42b9934/skylighticon.png)

| Mobility | Description |
| --- | --- |
| **Static** | Lighting cannot be changed while in game. This is the fastest method for rendering and allows for baked lighting. |
| **Stationary** | When lighting is built, shadowing and light bounces will only be captured from static geometry. All other lighting will be dynamic. This setting also allows for the light to change color, intensity, and the cubemap in-game, but it does not move and allows for partially baked lighting. |
| **Movable** | Lighting can be moved and changed in-game as needed. |

## Static Sky Light

A Sky Light set to **Static** will be baked completely into the lightmap for static objects in the level and therefore costs nothing. When edits are made to the light's properties, the changes will not be visible until lighting has been rebuilt for the level.

When using a Static Sky Light, only Actors and Lights in the level that have their mobility set to **Static** or **Stationary** will be captured and used for lighting. Furthermore, only the emissive contribution of Materials can be captured with a Static Sky Light in order to avoid a feedback loop. For this reason, make sure any skybox has a Material that is set to **Unlit**.

### Stationary Skylight

A Sky Light with **Stationary Mobility** gets baked shadowing from **Lightmass**. Once you place a Stationary Sky Light in your level, you have to rebuild lighting once to get the baked shadowing. You can then change the sky light as much as you want without rebuilding. The Sky Light shadowing that **Lightmass** bakes stores directional occlusion information in what is called a [**Bent Normal**](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine#bentnormalforstationaryskylights).

Only components and lights with **Static** or **Stationary Mobility** will be captured and used for lighting with a Stationary Sky Light.

Like all types of **Stationary Lights**, the color of the direct lighting can be changed at runtime through **Blueprint** or **Sequencer**. However the indirect lighting is baked into the lightmap and cannot be modified at runtime. The amount of indirect lighting can be controlled by `IndirectLightingIntensity`.

![Direct Lighting Only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bd5fffc-2406-49c7-9d43-be57eef67eb3/0original.jpg)

![Direct Lighting and Diffuse GI computed for a Stationary Sky Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f4d39d9-0cdd-47cd-b9e5-7bc1eb7ad3e4/0skylightgi.jpg)

### Movable Sky Light

A Sky Light set to **Movable** does not use any form of precomputation. It captures components and lights of any mobility when setup to capture the scene.

#### Distance Field Ambient Occlusion

This property requires that [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) be enabled in the project settings.

Shadowing for a Movable Sky Light is provided by [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine) from Signed Distance Field Volumes that are generated around each rigid object. Distance Field Ambient Occlusion supports dynamic scene changes where the rigid meshes can be moved or hidden, and it will affect the occlusion.

Click image for full size.

Check out the [How to use Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/using-distance-field-ambient-occlusion-in-unreal-engine) page for more information and examples.

## Precomputed (Static or Stationary) Sky Light

When using baked lighting with a Static or Stationary Sky Light, the lighting and shadowing data will be stored in lightmaps. The sections below discuss some of these features supported by [Lightmass](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine).

### Improved Static Sky Light Directionality

Prior to Unreal Engine 4.18, Static Sky Lights used to be represented by Lightmass with a 3rd Order Spherical Harmonic which didn't capture the detail that could be present in a sunrise or sunset. A filtered cubemap is used now which results in a higher resolution by default. Lightmass will also select the appropriate mip of the cubemap texture based on the size of the Final Gather rays to avoid any aliasing.

To see an example of this type of interaction, go to **Engine Content** > **MapTemplates** > **Sky** and select **SunsetAmbientCubemap** as it will show a great example.

![Third Order Spherical Harmonic | (Before) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75584aa9-eeff-4d6c-94f2-f8d462ce7e52/skylight_2.png)

![Filtered Cubemap | (After)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ae17229-7918-4bce-bba8-8ffec7d8f7ea/skylight_1.png)

The biggest difference can be seen in heavily occluded scenes with a Sky Light cubemap that has a lot of brightness and color variations.

#### Camera Obscura

With the improved directionality of Static Sky Lights, it is now possible to recreate a pinhole camera effect ([Camera Obscura](https://en.wikipedia.org/wiki/Camera_obscura)) with a small enough opening. The smaller the opening, the more directional sky lighting will become.

|   |   |
| --- | --- |
|  |  |
| Sky Light Source Cubemap | Resulting Light Build |
| *Click image for full size.* | *Click image for full size.* |

### Bent Normal for Stationary Sky Lights

For Stationary Sky Lights, static and stationary lighting is baked separately from movable using Lightmass to store directional information in what is called a **Bent Normal**. This is the direction from the texel to the most un-occluded source of ambient light. Areas that are mostly occluded use this direction for sky lighting instead of the surface normal, which improves quality in cracks.

![Static Sky Light Ambient Occlusion Only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0675f32a-2b84-41c0-9fce-9129d8df0666/1skylightaoonly.png)

![Stationary Sky Light with Bent Normal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5662c253-678a-43fa-b72d-d605df6c7554/1skylightbentnormal.png)

The first image shows Sky Light with Ambient Occlusion only. The second image shows Sky Light with Bent Normal occlusion. Notice how surfaces in cracks 'agree' on where the lighting is coming from.

For additional information visit the [Bent Normal Map](/documentation/en-us/unreal-engine/bent-normal-maps-in-unreal-engine) page.

### Multiple Light Bounces

Multiple bounces of indirect light from Sky Lights is supported by adjusting the **Num Sky Lighting Bounces** setting in **World Settings** > **Lightmass**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef1c9911-d50b-4b5c-9e34-0941be34ce3a/lightmasssettings.png)

Setting for the number of sky light bounces to use.

![Number of Bounces: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b196db50-6645-4753-8113-0a86b9e203ad/skylight_4.png)

![Number of Bounces: 10](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b6fa5b6-98d4-4666-b727-46c1d217e059/skylight_3.png)

For multiple Sky Light bounces to be noticeable, your Materials need to have a high diffuse value in most cases. For example, with a diffuse value of .18 (18% grey), the second sky light bounce will only contribute 18^3 = 0.006 of the light's emitted energy, which is very subtle. With a diffuse value of 0.5, the second skylight bounce will contribute 0.125 of the light's emitted energy and be noticeable.

Each added bounce increases non-distributed build times, so use with care when not using [Swarm distribution](/documentation/en-us/unreal-engine/unreal-swarm-in-unreal-engine).

## Real Time Capture

The **Real Time Capture** mode provides dynamic and specular environment lighting, making possible dynamic time-of-day simulations with real-time reflections on scene elements.

This mode is available when the Sky Light's mobility is set to Stationary and Dynamic and when **Real Time Capture** is enabled from the Sky Light component **Details** panel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ba53884-b64b-42d6-8500-101a5d4e980a/skylight_rtcmode.png)

This mode supports the following components for captured reflections and shadowing:

-   [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine)
-   [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine)
-   [Exponential Height Fog](/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine)
-   Sky Dome Meshes with an unlit material tagged as **IsSky**

These are some additional things to keep in mind when using this mode:

-   Volumetric Fog is not supported.
-   Requires a [Sky Atmosphere](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine) component to be present in the scene for real time capture to work. In a future release, real time capture will be supported without this requirement.
-   It's possible to render meshes only in real time capture mode by disabling them from rendering in the main view.
-   It's possible to have a different sky dome mesh for the main view as compared to the reflection of the real time capture when enabling **Visible in Real Time Sky Captures** on individual actors.
-   Real Time Capture mode allows for ambient shadowing from Volumetric Clouds to be cast onto the world when **Cloud Ambient Occlusion** is enabled.
-   Real Time Capture mode is faster and more efficient than the **RecaptureSky** Blueprint node because all the computations stay on the GPU without any use of CPU processing that can cause pauses, or slowdowns in gameplay.
-   If you are using the volumetric clouds, performance can vary a lot depending on the complexity of the cloud material you're using. You can control the performance tradeoff—while respecting visuals in your scene—by adjusting the Volumetric Cloud component's **Reflection Sample Count Scale** and **Shadow Reflection Sample Count Scale** values.

### Reflection Quality

The quality of reflections captured by the Sky Light is set by the property **Cubemap Resolution**. It uses power of two values (such as, 64, 128, 256, and so on) to specify a texture resolution for the captured scene.

Keep in mind that higher resolution values increase quality at the cost of performance. The specified value is applied to the highest cubemap mip (a texture's level of detail).

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9ed3de1-42dc-4556-ae4f-a888c48d42e6/sl_cuebmapquality_64.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8c91739-391f-499e-bb36-520b360e0f45/sl_cuebmapquality_128.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b110554-7225-4103-a9e6-02e491f7e928/sl_cuebmapquality_256.png)

Drag the slider to see decreased (64), default (128), and increased (256) skylight cubemap resolutions being used.

Note that [Screen Space Reflections](/documentation/en-us/unreal-engine/screen-space-reflections-in-unreal-engine) (SSR) has been disabled in these shots. Reflections are only the result of the Sky Light.

### Time Slicing Optimization

Real Time Capture mode utilizes a performance optimization called **Time Slicing** to distribute the captured scene over several frames rather than performing a full scene process every frame. This optimization reduces the per frame cost that would make a full process real time capture every frame too expensive for use on some platforms.

For example, a capture performed on the PlayStation 4 using a 128x128x6 HDR cubemap with sky and volumetric clouds would look something like (measured in milliseconds):

-   A **Full** process per frame for a 128x128 cubemap would cost around 1.465ms (divided up as the following):
    -   Sky and Cloud costs 0.60 ms
    -   Cubemap Mip Generation costs 0.05 ms
    -   Specular Convolution costs 0.80 ms
    -   Diffuse Irradiance costs 0.015 ms
-   The same process but time sliced over **9-Frames Time Slice** would cost, at most, 0.20 ms for the most expensive step.

Distributing a single frame's capture over multiple frames has the benefit of keeping real time skylight capture within an affordable budget for your project, because time slicing is only as expensive as its most costly frame. It also means you can look for opportunities to push quality in other areas, such as the quality of the sky or clouds, because you have a little bit of room in the frame budget.

Time slicing is enabled by default, but can be set using the console command `r.SkyLight.RealTimeReflectionCapture.TimeSlice.`

## Shadowing from Movable Objects

Soft shadowing from movable objects onto the environment can be achieved using [Capsule Shadows](/documentation/en-us/unreal-engine/capsule-shadows-in-unreal-engine) for Skeletal Meshes or [Distance Field Indirect Shadowing](/documentation/en-us/unreal-engine/using-distance-field-indirect-shadows-in-unreal-engine) for rigid meshes. These require a separate setup to work properly.

## Properties

There are two categories of Sky Light component properties, Sky Light and Light, although they are not differentiated in the UI. These can be accessed from the Actor **Details** panel. Sky Light properties are specific to Sky Light Actors, while Light properties are common to all Light Actors. Certain properties are only accesible by expanding the Advanced section, indicated in the table below.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c8d2809-28d3-4f87-b669-8c18021b9618/skylightsettings.png)

| Property | Description |
| --- | --- |
| Sky Light |   |
| **Real Time Capture** | When enabled, the sky will be captured and convolved to achieve dynamic diffuse and specular lighting. SkyAtmosphere, VolumetricCloud Components as well as sky domes with Sky materials are taken into account. |
| **Source Type** | 
Whether to capture the distant scene and use it as the light source or to use the specified cubemap. When capturing the scene, anything further than SkyDistanceThreshold from the Sky Light position will be included:

-   **SLS Captured Scene**: Construct the sky light from the captured scene. Anything further than Sky Distance Threshold from the sky light position will be included.
-   **SLS Specified Cubemap**: Construct the sky light from the specified cubemap.



 |
| **Cubemap** | Specify the Cubemap to use for sky lighting if Source Type is set to SLS\_SpecifiedCubemap. |
| **Source Cubemap Angle** | The angle to rotate the source cubemap when Source Type is set to SLS Specified Cubemap. |
| **Cubemap Resolution** | Maximum resolution for the very top processed cubemap MIP. It also must be a power of 2 texture. |
| **Sky Distance Threshold** | Distance from the Sky Light at which any geometry should be treated as part of the sky (also used by Reflection Captures). |
| **Capture Emissive Only** | Only capture emissive Materials. Skips all lighting making the capture cheaper. This is recommended when using Capture Every Frame. Advanced. |
| **Lower Hemisphere is Solid Color** | Whether all lighting from the lower hemisphere should be set to zero. This is useful to prevent leaking from the lower hemisphere. Advanced. |
| **Lower Hemisphere Color** | Use the color picker to select the color for the lower hemisphere. Advanced. |
| Light |   |
| **Intensity Scale** | The total energy that the light emits. |
| **Affects World** | Whether the light can affect the world, or whether it is disabled. |
| **Cast Shadows** | Whether the light should cast any shadows. |
| **Indirect Lighting Intensity** | Scales the indirect lighting contribution from this light. A value of 0 disables any global illumination (GI) from this light. |
| **Volumetric Scattering Intensity** | Intensity of the volumetric scattering from this light. This scales Intensity and Light Color. |
| **Casts Static Shadows** | Whether the light should cast shadows from static objects. Also, requires Cast Shadows to be set to True. Advanced. |
| **Casts Dynamic Shadows** | Whether the light should cast shadows from dynamic objects. Also, requires Cast Shadows to be set to True. Advanced. |
| **Affect Translucent Lighting** | Whether the light affects translucency or not. Disabling this can save GPU time when there are many small lights. Advanced. |
| **Transmission** | Whether light from the skylight transmits through surfaces with subsurface scattering profiles. Requires the light to be movable. Advanced. |
| **Cast Volumetric Shadow** | Whether the light shadows Volumetric Fog. Advanced. |
| **Cast Deep Shadow** | Whether the light should cast high quality hair-strands self shadowing. When this option is enabled, an extra GPU costs is applied to this light. Advanced. |
| **Cast Ray Traced Shadows** | Whether the light shadows are computed with shadow mapping or ray tracing (when available). Advanced. |
| **Affect Ray Tracing Reflections** | Whether the light affects objects in reflections when ray traced reflection is enabled. Advanced. |
| **Affect Ray Traced Global Illumination** | Whether the light affects global illumination when ray traced global illumination is enabled. Advanced. |
| **Deep Shadow Layer Distribution** | Change the deep shadows layer distribution. 0: linear (uniform layer distribution), 1: exponential (more details on near small shadows). Requires Cast Deep Shadow to be enabled. Advanced. |
| Atmosphere and Cloud |   |
| **Cloud Ambient Occlusion** | Whether the cloud should occlude sky contribution within the atmosphere (progressively fading out multiple scattering) or not. |
| **Cloud Ambient Occlusion Strength** | The strength of the ambient occlusion. Higher values will block more light. |
| **Cloud Ambient Occlusion Extent** | The world space radius of the cloud ambient occlusion map around the camera in kilometers (km). |
| **Cloud Ambient Occlusion Map Resolution Scale** | Scales the cloud ambient occlusion map resolution. The resolution is clamped by `r.VolumetricCloud.ShadowMap.MaxResolution`. |
| **Cloud Ambient Occlusion Aperture Scale** | Controls the cone aperture angle over which the sky occlusion due to volumetric clouds is evaluated. A value of 1 takes the entire hemisphere into account, resulting in blurry occlusion. A value of 0 takes a single direction of occlusion (vertical) into account, resulting in sharp occlusion. |

## Limitations

These features would be useful with SkyLights but are not yet implemented:

-   Soft shadowing from movable objects (characters) onto the environment is not integrated with Sky Light and currently requires implementing separate features at additional rendering cost.
-   The SkyLightComponent Blueprint function RecaptureSky() can be used, however it has a high processing cost and requires at least 120 ms, leading to a pause or slowdown in gameplay.