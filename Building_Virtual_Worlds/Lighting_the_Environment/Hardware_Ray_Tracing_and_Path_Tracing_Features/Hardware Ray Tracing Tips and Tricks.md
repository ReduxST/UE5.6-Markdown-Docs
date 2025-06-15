# Hardware Ray Tracing Tips and Tricks

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-ray-tracing-tips-and-tricks-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hardware-ray-tracing-tips-and-tricks-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:19

---

This page contains suggestions you can use with [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) features.

## Materials 

The following suggestions work with [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials) and hardware ray tracing features.

### Ray Tracing Quality Switch Replace Node

Use this node to replace entire parts of your Material logic to lower the cost of features like ray tracing global illumination, reflections, and translucency with less complex logic. When applying these in your Material, it will affect any ray tracing with this material where it is applied in the Level.

The example below shows the **Normal** logic path with diffuse, roughness and normal map textures. The **Ray Tracing** path removes the Normal map texture and uses less complex logic for Roughness. This change makes the material cheaper to render for ray tracing effects, especially with ray tracing global illumination and reflections.

Click image for full size.

### Ray Traced Shadows Per Material

Use the **Cast Ray Traced Shadows** checkbox to set whether this Material casts ray traced shadows. This is useful for controlling specific elements of any Materials assigned to geometry that should, or should not cast a raytraced shadow.

### Testing Material Costs

Complex Materials can affect performance of hardware ray tracing features. Use the console command `r.RayTracing.EnableMaterials` to test performance impact.

### Translucency Index of Refraction (IOR)

When setting up a Material for refraction with ray tracing, the **Refraction** material input controls the index of refraction (IOR) in your translucent materials.

The amount of refraction is set up in the Material applied to an object. In the Level, the post process settings control whether refraction is ray traced and the maximum number of refraction bounces that are possible.

![Raster Translucency | with faked Refraction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8022095-b288-4ba7-b052-2c4385e6843a/1.png)

![Ray Traced Translucency | with Refraction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33629d2d-9c83-4c4e-8e9d-ac76bdd02248/3.png)

Material Setup:

-   Enable **Two Sided** in your Material.
    -   While this is not a requirement, single sided/non-manifold geometry doesn't have a good way of handling volume tracking or ray medium stacking. A two-sided material provides accurate results and is the recommended method for handling all translucent materials when using ray tracing translucency.
-   Set the **Lighting Mode** to **Surface Translucency Volume** or **Surface Forward Shading**.
-   Use the **Refraction** input to control the index of refraction.

Post Process Volume Rendering Features Setup:

-   Under the **Translucency** category, set the **Type** to **Ray Tracing**.
-   Under the **Ray Tracing Translucency** category, set the following:
    -   **Refraction:** Enabled
    -   **Max Refraction Rays:** Set the maximum number of rays to use. This should be a high enough value that it allows light to pass through to the other side.

Use a [Material Instance](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) to dynamically control the IOR of the material with instance results.

### Controlling the amount of Refraction

The amount of refraction and light transport that takes place is controlled by using the **Refraction** input in a Material. The Post Process Volume settings must have the **Refraction** check box enabled and greater than 1 **Max Refraction Rays** set.

The translucent material below is using a refraction input value of 0.04. The post process has a Max Refraction Ray count of 6 to pass light through the translucent material.

![Ray Tracing Refraction: | Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d889da7-5bba-4e19-b458-c318146741f3/5.png)

![Ray Tracing Refraction: | Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/958346c3-ed3d-4031-8b3d-2bcae1da4d39/3.png)

The examples below shows how different refraction input values in the Material affect the index of refraction.

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e802b67b-7e09-4fb2-a354-f9f5ee64ac4b/10.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d29398c1-3a90-4743-8712-bd2b10957ee7/11.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ee3ee0a-2813-42ef-b1a6-80c7c093c791/12.png)

Dragging the slider shows the amount of refraction being applied from 0.01, 0.05, and 0.1.

The examples below demonstrate how the Post Process Volume **Max Refraction Rays** value affects light transport through the translucent material. A single ray does not provide enough bounces to escape the material, leaving it appearing darkened or black. Increasing the maximum number of refraction rays gives light a greater opportunity to escape the material. Not all materials or rays will require the maximum number of refraction rays, but in cases where more are needed, this may leave some materials looking darker than needed.

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/308dc1f4-18a4-4fdb-8ced-bd6a70f39ec8/7.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3985705-d668-4790-a946-4985cd9f98d9/8.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c94a1840-307c-4139-9279-2b93781eafcb/9.png)

Dragging the slider shows the result of using 1, 3, and 5 refraction rays.

### Single Sided and Two Sided Material Refraction

Ray traced refraction works with both single sided and two sided materials to allow light transport through the object's volume. While single sided materials are supported for refraction, two side materials provide physically accurate results and is recommended for all Translucent Materials using ray tracing transparency.

![Ray Traced Translucency | Single Sided Material | with Refraction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66bfe9f9-dc17-4c0f-a563-aca8ed805b6c/4.png)

![Ray Traced Translucency | Two Sided Material | with Refraction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3a6036e-41b6-499b-afd1-12ad570536d4/3.png)

Use the Post Process Volume **Max Refraction Rays** property to set the number of refraction bounces light transport should use.

## Light Transmission for Subsurface Profile Materials

Light transmission on materials using a [Subsurface Profile](/documentation/en-us/unreal-engine/subsurface-profile-shading-model-in-unreal-engine) is possible when the light source also has the **Transmission** property enabled on the Actor placed in the Level.

![Raster Subsurface Profile | Light Transmission](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c5aae97-b124-4a36-ac11-ed5ac67a99a1/transmission_raster.png)

![Ray Tracing Subsurface Profile | Light Transmission](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa119ab4-ce52-4ff1-bc3a-78c5b17235c2/transmission_rt.png)

A small scattering simulation is run during the ray tracing shadow computation to compute the expected volumetric scattering distance through the medium to the shadow-casting light. The scatter distance is used during lighting to compute the in-scattering contribution from the light.

## Reflections

The following suggestions work with the [Reflection Environment](/documentation/en-us/unreal-engine/reflections-environment-in-unreal-engine) and hardware ray tracing features.

### Ray Tracing Reflection Capture Fallback

Ray Tracing Reflections are more expensive when rendering multiple bounces that create reflections inside of reflections. Without multiple bounces, the intra-reflected materials appear black. A lower cost solution is to use ray traced reflections for and then fall back to placed Reflection Capture Actors in the Level as the last bounce.

Enable reflection capture fallback with the console variable `r.RayTracing.Reflections.ReflectionCaptures`.

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c583a63a-f9e0-416d-9bf8-fd55545225fc/1_rtrrefcapture.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d50cd26-7d8a-4d51-9bae-54ba26848d31/2_rtrrefcapture.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1b6e7ff-3de7-4faf-9549-30861f68eb90/3_rtrrefcapture.png)

Dragging the slider shows a single bounce RTR, two bounces RTR with no reflection capture fallback, and a single bounce with reflection capture fallback.

### Including Translucent Objects in Reflections

Enable objects with translucent materials to appear in Ray Traced Reflections by enabling **Include Translucent Objects** in the Post Process Volume settings from the **Ray Tracing Reflections** category.

## Sky Lights

Capturing distance objects, like a sky dome mesh, should be disabled for Sky Light contribution, unless it is needed. This saves some performance and optimizes the scene.

The **BP\_SkySphere** sky dome mesh and Blueprint that is included with starter Levels has this sky light contribution disabled by default. It will make reflections from sky look different than expected but saves performance with hardware ray tracing.

Object contribution is enabled/disabled from the **Details** panel with the checkbox for **Visible in Ray Tracing** when the object is selected in the Level.

## Geometry Considerations with Ray Tracing

-   Geometry with small holes, or lots of little details, can significantly impact performance. For example, trees and bushes with lots of leaves, or grates and fences that have holds in them. 
    
-   Indoor environments are slower to render than outdoors ones because often light enters from the outside and is expected to bounce around well enough to light a room. Areas that are directly lit by a light are faster to render than ones indirectly lit by light. Also, consideration with other ray tracing features like reflections and translucency affect performance in these situations.
    

## General Optimizations for Hardware Ray Tracing Features

-   **Setting Reflections and Translucency Maximum Roughness**
    -   Use **Max Roughness** to set a threshold for raytraced reflections on Materials. This can be done within the Post Process Volume or using the console command r.RayTracing.Reflections.MaxRoughness. 
-   **Setting a Maximum Ray Distance for Global Illumination, Reflections, and Translucency**
    -   This sets a maximum ray distance for each of these features to lower their cost and contribution in the scene.
    -   Use the console to set the **MaxRayDistance** console variable for each of these raytraced features. You can find them under r.RayTracing.\*.
-   **Ray Traced Global Illumination Optimizations**
    
    -   Screen Percentage and Sample Per-Pixel default to **50** and **4**, respectively. If different values are needed, use the console commands `r.RayTracing.GlobalIllumination.ScreenPercentage`, and `r.RayTracing.GlobalIllumination.SamplesPerPixel`.
    -   Light contribution to global illumination can be set on each Light Actor by enabling/disabling **Affect Global Illumination**.

## Ray Tracing Solid Angle and Distance-based Culling

Scenes with ray tracing require objects outside of the camera view to be present in the scene, especially for highly reflective surfaces, which can increase cost of rendering. Culling objects that aren't visible or needed can help optimize and gain some of that performance back.

Ray tracing provides several ways of culling objects in the scene: by distance from the camera, or by projecting an area (or a angle) behind the camera and testing individual object bounds to determine whether they should be culled, not at all, or both simultaneously. The type of culling used is set by using one of the following values with the console variable `r.RayTracing.Culling`.

-   **0** culling is disabled.
-   **1** culls objects behind the camera by distance and solid angle. (Default culling method)
-   **2** culls objects in front of and behind the camera by distance and solid angle.
-   **3** culls objects in front and behind the camera by distance **or** solid angle.

Higher values cull more objects in the world.

Additionally, the ray tracing console variables (`r.RayTracing.*`) use two commands to configure Solid Angle culling: an angle and a radius.

-   **Angle** sets the projected area angle behind the camera (in degrees) that object's bounds will be tested against for whether they should be culled or not. Increasing the angle will aggressively cull a lot of objects.
-   **Radius** culls any object outside of the specified radius. By default, the radius is set to 100 meters (or 10000 cm/Unreal Units).

Two examples of ray tracing console variables using these would be `r.RayTracing.Culling.Angle`, and `r.RayTracing.StaticMeshes.WPO.CullingRadius`.

If distance-based culling is needed, any radius variables should be set to **\-1**.

## Evaluating Denoiser Quality

Hardware ray tracing features rely heavily on denoising algorithms to use as few pixels as possible and make up the different with a denoiser to intuit the rest. You can evaluate the quality of the denoiser for different ray tracing effects by following these steps:

1.  Disable **Temporal Anti-Aliasing** and **Depth of Field**
    1.  Both of these are running in linear color space in Unreal Engine's renderer. They do some HDR color weighting tricks to avoid aliasing between shadows and highlights.
2.  Compare the Denoised single sample per pixel with an Undenoised single sample per pixel. 
    1.  The result will look incorrect due to the energy difference and that the denoiser is darkening the shadows too much. However, a single sample per pixel will look brighter due to the tonemapper's non-linear operation. 
    2.  For a better comparison, the Denoised **single** sample per pixel should be tested against an Undenoised **multiple** samples per pixel.

![Denoised Single Sample Per Pixel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad657ba4-2d04-4a45-a099-0d28a1648170/rt_denoiser_singlesample.png)

![Undenoised Multiple Samples Per Pixel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/000a38a1-bb7e-4fa2-bd8f-0c00f85327c6/rt_denoiser_multisamples.png)

The denoised single sample per pixel will not be perfect due to information loss. However, when compared to undenoised multiple samples per pixel, the results are consistent. 

Keep in mind that the denoiser supports up to four samples per pixel for hardware ray tracing features. The more samples used, the closer it is to matching the undenoised multiple sampples per pixel result.