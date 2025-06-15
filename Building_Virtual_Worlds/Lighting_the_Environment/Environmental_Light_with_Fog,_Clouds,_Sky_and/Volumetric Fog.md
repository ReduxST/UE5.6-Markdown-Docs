# Volumetric Fog

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:43

---

**Volumetric Fog** is an optional part of the [Exponential Height Fog](https://dev.epicgames.com/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine) Component. Volumetric Fog computes participating media density and lighting at every point in the camera frustum to support varying densities and any number of lights that affect the fog.

[![](https://dev.epicgames.com/community/api/documentation/image/23acb13a-c367-4bec-ba0f-c3b9068eaa79?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/23acb13a-c367-4bec-ba0f-c3b9068eaa79?resizing_type=fit)

In this scene, Volumetric Fog is coming from the directional light source off screen through the arch and surrounding area to create shadowed fog.

## Volumetric Fog Controls

When setting up and adjusting Volumetric Fog, you can control it globally or locally in your scene. The global controls enable you to use the Exponential Height Fog component to control fog for the the entire scene. The local controls enable you to control fog by way of a particle system in areas where the particles can spawn.

### Global Controls

To control Volumetric Fog, you can adjust the properties in your **Exponential Height Fog** and on each **Light** to control the Light's contribution amount.

#### Exponential Height Fog

Volumetric Fog controls can be found in the **Exponential Height Fog** component under the **Volumetric Fog** section. The exponential height distribution provides a global density for Volumetric Fog.

[![Volumetric Fog controls in the Exponential Height Fog Details panel](https://dev.epicgames.com/community/api/documentation/image/873ad485-040d-41af-893b-985646d89299?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/873ad485-040d-41af-893b-985646d89299?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Scattering Distribution**

 | 

This determines how directional the volumetric scattering is; a value of 0, means light scatters equally in all directions, while a value close to 1 causes scattering, predominantly in the direction of the light (you have to be looking at the light to see its scattering).

 |
| 

**Albedo**

 | 

This is the overall reflectiveness of the participating media. Clouds, fog, and mist, which are based on water particles, have an albedo close to 1.

 |
| 

**Emissive**

 | 

This is a density of light emitted by height fog.

 |
| 

**Extinction Scale**

 | 

Controls how much the participating media blocks light.

 |
| 

**View Distance**

 | 

This is the distance from the camera over which Volumetric Fog will be computed. In the created volume texture for the fog there are a limited number of Z slices depending on this distance. Increasing the distance will result in under-sampling that can cause artifacts to appear. The number of Z slices can be adjusted by using r.VolumetricFog.GridSizeZ, where higher is better quality, but will be more expensive.

 |
| 

**Start Distance**

 | 

This is the distance (in world units) from the camera from which the volumetric fog will start.

 |
| 

**Near Fade In Distance**

 | 

This is the distance over which volumetric fog will fade in from the start distance.

 |
| 

**Static Lighting Scattering Intensity**

 | 

Scales the intensity of the volumetric fog static lighting scattering.

 |
| 

**Override Light Colors with Fog Inscattering Colors**

 | 

When enabled, uses the **Fog Inscattering Color**, **Directional Inscattering Color**, and **Inscattering Texture** properties to override the light color with Volumetric Fog.

 |

#### Lights

Each Light's contribution amount to the scene (and whether it shadows the fog) can be controlled by adjusting the following properties on each Light's Details panel under the **Light** section.

[![Volumetric Fog light properties](https://dev.epicgames.com/community/api/documentation/image/60a276d4-0082-4ce1-ae23-f914780dcba3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/60a276d4-0082-4ce1-ae23-f914780dcba3?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Volumetric Scattering Intensity**

 | 

Controls how much this light will contribute to the Volumetric Fog. When set to 0, there is no contribution.

 |
| 

**Cast Volumetric Shadow**

 | 

Toggles whether or not to cast a volumetric shadow for lights contributing to Volumetric Fog. When shadow casting is enabled, Point and Spot Lights are approximately three times more expensive because they contribute to the volume textures shadowing, where as non-shadow casting lights only contribute to the fog but do not shadow.

 |

![Volumetric Scattering Intensity: 1 (Default)](https://dev.epicgames.com/community/api/documentation/image/798a236c-26d2-4723-8f1a-e5117536a21d?resizing_type=fit&width=1920&height=1080)

![Volumetric Scattering Intensity: 0](https://dev.epicgames.com/community/api/documentation/image/ac2c4d29-131b-449b-b444-37e4373f1adc?resizing_type=fit&width=1920&height=1080)

Volumetric Scattering Intensity: 1 (Default)

Volumetric Scattering Intensity: 0

In this example, the Spot Light's contribution to the Volumetric Fog has been disabled by setting the **Volumetric Scattering Intensity** to 0.

### Local Controls

Materials using the **Volume** domain describe Albedo, Emissive, and Extinction for a given point in space. Albedo is in the range \[0-1\], while Emissive and Extinction are world space densities with any value greater than 0.

[![Volume Material example](https://dev.epicgames.com/community/api/documentation/image/7466e02f-82eb-4e21-a5bb-d1472604ffcb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7466e02f-82eb-4e21-a5bb-d1472604ffcb?resizing_type=fit)

This is an example of the simplest Volume Material for a Particle System.

Volume materials currently only work on particles and positions inside of the particle radius will be valid, which is usually handled by a SphereMask.

Placing a single Particle System with the material causes a sphere of density to be added to the Volumetric Fog. The effect is fully three dimensional (3D) with no billboards involved.

[![](https://dev.epicgames.com/community/api/documentation/image/c90db40f-b5a9-4adf-812c-d180a675e71e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c90db40f-b5a9-4adf-812c-d180a675e71e?resizing_type=fit)

Taking this approach a step further, you could use multiple spherical fog particles with noise from textures to limit fog to a certain area of your scene.

[![](https://dev.epicgames.com/community/api/documentation/image/3312dcba-d61f-45a4-a257-4b81764402b9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3312dcba-d61f-45a4-a257-4b81764402b9?resizing_type=fit)

In this scene, the fog particles have populated these low-lying areas to create a localized fog effect that is shadowed using Volumetric Fog.

## Temporal Reprojection

The volume textures (voxels) used by Volumetric Fog are relatively low-resolution and aligned to the camera frustum. Volumetric Fog uses a heavy temporal reprojection filter with a different sub-voxel jitter per frame to smooth out the aliasing. As a side-effect, fast-changing lights, like flashlights and muzzle flashes, leave lighting trails. To disable the contribution of these lights, set **Volumetric Scattering Intensity** to 0.

## Precomputed Lighting on Volumetric Fog

Volumetric Lightmaps support static lighting application for Volumetric fog by having each fog voxel interpolate precomputed lighting to its position in space.

![Spot Light with | No Indirect Light Bounce](https://dev.epicgames.com/community/api/documentation/image/32df3761-b84a-4af5-a2c1-9020a8fa8c86?resizing_type=fit&width=1920&height=1080)

![Spot Light with | Indirect Light Bounce](https://dev.epicgames.com/community/api/documentation/image/636ffe6b-8cf5-4f57-ab33-eb31c18f054e?resizing_type=fit&width=1920&height=1080)

Spot Light with | No Indirect Light Bounce

Spot Light with | Indirect Light Bounce

Stationary Lights have their indirect lighting stored in lightmaps, which now affects fog.

![Sky Light with Emissive Color](https://dev.epicgames.com/community/api/documentation/image/993eb1e8-9e0f-4f25-90c0-4e79efae35c2?resizing_type=fit&width=1920&height=1080)

![Sky Light Volumetric Lightmap](https://dev.epicgames.com/community/api/documentation/image/dd619e55-78bc-4038-b8ed-d62b2e136529?resizing_type=fit&width=1920&height=1080)

Sky Light with Emissive Color

Sky Light Volumetric Lightmap

Skylights are shadowed properly, preventing indoor areas from becoming over-fogged.

![Indirect Lighting Cache: | Static and Emissive for Static Lighting | (Old Method)](https://dev.epicgames.com/community/api/documentation/image/c5977085-71a5-4188-a43c-919c71b607d0?resizing_type=fit&width=1920&height=1080)

![Volumetric Lightmap: | Static and Emissive for Static Lighting | (New Method)](https://dev.epicgames.com/community/api/documentation/image/26cf8090-ba13-4f19-883a-be8b3038870b?resizing_type=fit&width=1920&height=1080)

Indirect Lighting Cache: | Static and Emissive for Static Lighting | (Old Method)

Volumetric Lightmap: | Static and Emissive for Static Lighting | (New Method)

Static and Emissive for Static lights affect fog without costing anything since they're all merged into the Volumetric Lightmap.

## Performance

The GPU cost of Volumetric Fog is primarily controlled by the volume texture resolution, which is set from the Shadow level of the Engine Scalability. Volumetric Fog costs 1 millisecond on PlayStation 4 at **High** settings, and 3 milliseconds on an NVIDIA 970 GTX on **Epic** settings, which has eight times more voxels to operate on.

-   Particles using **Volume** domain can add a significant GPU cost, depending on their 3D overdraw and instruction count. Use the console command `profilegpu` to inspect this cost.
    
-   Point and Spot Lights that have **Cast Volumetric Shadow** enabled, cost approximately three times more than unshadowed Point and Spot Lights.
    

Cloud rendering will use the expensive path when `r.PostProcessing.PropagateAlpha` is enabled and when any features, such as Exponential Height Fog, Volumetric Cloud, and Sky Atmosphere, have alpha holdout enabled.

## Currently Supported Features

This list comprises the currently supported features of Volumetric Fog:

-   A single Directional Light, with shadowing from Cascaded Shadow Maps or static shadowing, with a Light Function.
    
-   Any number of Point and Spot Lights, with dynamic or static shadowing (if **Cast Volumetric Shadowing** is enabled).
    
-   Shadowing of Stationary Sky Lights.
    
-   Precomputed Lighting through Volumetric Lightmaps (Direct Lighting of Static Lights, Indirect Lighting of Stationary Lights).
    
-   A single Skylight, with shadowing from Distance Field Ambient Occlusion (if enabled).
    
-   Particle Lights (if **Volumetric Scattering Intensity** is greater than 0).
    

Also, translucency is properly affected by Volumetric Fog, depending on its position in the scene. By default, translucency computes fog at vertices, so water planes with low tessellation can introduce artifacts. These materials can be set to compute fogging per-pixel to solve this with **Compute Fog Per-Pixel** enabled in the Material Details.

## Known Issues

The following features are **not yet supported** while using Volumetric Fog:

-   IES profiles and Light Functions on Point and Spot Lights.
    
-   Shadowing from Ray Traced Distance Field Shadows.
    
-   Shadowing from Volumetric Fog (itself).
    
-   Source Radius on Point and Spot Lights.
    
-   Some settings in the Exponential Height Fog, like Fog Cutoff Distance, Start Distance, and Fog Max Opacity.
    

### Common Questions

Below are some common questions or issues that may arise when using Volumetric Fog.

-   **How can one achieve stronger light shafts without heavy global fog?**
    
    -   When the global density of fog is increased, you get denser fog, so you only notice light shafts (shadows of light) if the fog is dense enough to have everything heavily fogged. There are two ways to go about having stronger light shafts without heavy fog:
        
        1.  Keep the global fog density low, but use a higher **Volumetric Scattering Intensity** for the Directional Light. Also, adjust the **Scattering Distribution** to nearly **0.9** in your Exponential Height Fog Actor.
            
        2.  Keep the global fog density low, but increase it in certain areas with Volume particles.
            
-   **Can Exponential Height Fog and Volumetric Fog be used at the same time?**
    
    -   At this time, Volumetric Fog replaces **Fog Inscattering Color** within the Volumetric Fog **View Distance**. Because Volumetric Fog is physically-based and Exponential Fog is not, it's impossible to blend the two systems in the distance for them to precisely match. This also means that some settings in the Exponential Height Fog component will have no effect on Volumetric Fog.
        
-   **Can the Volumetric Fog's center be decoupled from the camera? This would be ideal for top-down games...**
    
    -   Not currently, though, a standalone volume would be ideal for this. However, it's hard to integrate them with translucency efficiently.
        

## Training Stream

Volumetric Fog | Feature Highlight | Unreal Engine