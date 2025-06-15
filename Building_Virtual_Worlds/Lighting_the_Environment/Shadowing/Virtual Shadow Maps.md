# Virtual Shadow Maps

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:19

---

**Virtual Shadow Maps** (VSMs) is the new shadow mapping method used to deliver consistent, high-resolution shadowing that works with film-quality assets and large, dynamically lit open worlds using Unreal Engine 5's [Nanite Virtualized Geometry](designing-visuals-rendering-and-graphics\rendering-optimization\nanite), [Lumen Global Illumination and Reflections](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine), and [World Partition](building-virtual-worlds/world-partition) features.

## Goals of Virtual Shadow Maps

Virtual Shadow Maps have been developed with the following goals:

-   Significantly increase shadow resolution to match highly detailed [Nanite](designing-visuals-rendering-and-graphics\rendering-optimization\nanite) geometry
    
-   Plausible soft shadows with reasonable, controllable performance costs
    
-   Provide a simple solution that works by default with limited amounts of adjustment needed
    
-   Replace the many Stationary Light shadowing techniques with a single, unified path
    

Conceptually, virtual shadow maps are just very high-resolution shadow maps. In their current implementation, they have a virtual resolution of 16k x 16k pixels. Clipmaps are used to increase resolution further for Directional Lights. To keep performance high at reasonable memory cost, VSMs split the shadow map into tiles (or Pages) that are 128x128 each. Pages are allocated and rendered only as needed to shade on-screen pixels based on an analysis of the depth buffer. The pages are cached between frames unless they are invalidated by moving objects or light, which further improves performance.

Nanite does not support many of the Stationary Light shadowing techniques, such as pre-shadows and per-object (or Inset) shadows. While some of the more dynamic parts of Stationary Light shadowing may work — such as the Cascaded Shadow Maps near the camera viewer — Nanite and Stationary Lights with conventional shadow maps are not supported. If you are using Nanite in your project, you must either use Movable Lights or use Virtual Shadow Maps.

## Enabling Virtual Shadow Maps

In the Project Settings under **Engine > Rendering** in the **Shadows** section, you can set what **Shadow Map Method** your project supports, whether **Virtual Shadow Maps** or the conventional **Shadow Maps** that have been used in previous Unreal Engine releases.

Existing projects will need to opt-in using the project setting, or console variable `r.Shadow.Virtual.Enable`. New projects use Virtual Shadow Maps by default.

[![](https://dev.epicgames.com/community/api/documentation/image/812df697-f19f-4405-be19-d59ecbbde8e2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/812df697-f19f-4405-be19-d59ecbbde8e2?resizing_type=fit)

### What happens with existing shadow methods when VSMs are enabled?

When VSMs are enabled, they replace a variety of existing shadow methods in Unreal Engine:

-   Stationary precomputed shadows, including 2D Distance Field and shadow factor "shadow maps"
    
-   Pre-shadows
    
-   Per-object / inset shadows
    
-   Cascaded Shadow Maps (CSMs)
    
-   Movable dynamic shadows for local lights
    

Fully baked shadows from Static Lights will still work as before (when not using Lumen). Their contributions are entirely represented in the baked lightmaps and there is no runtime lighting evaluated at all. Stationary lights will use the indirect diffuse contribution from any baked lightmaps, but their direct lighting and shadows are evaluated dynamically (the same as Movable lights) when VSMs are enabled.

[Distance Field Shadows](https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine) are not replaced, and can be used in tandem with Virtual Shadow Maps for Directional Lights. Distance Field Shadows take over for non-Nanite geometry beyond the dynamic shadowing distance of Movable Lights — set on a Directional Light using the Cascaded Shadow Maps property **Dynamic Shadow Distance Movable Light**. Using Distance Field Shadows provides a useful tool to reduce runtime costs in complex scenes, such as those with lots of [non-Nanite foliage](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine).

Nanite geometry always renders to the Virtual Shadow Map regardless of distance, since this is the most performant option and provides the highest quality. It is possible to make non-Nanite geometry behave the same way as Nanite by the console variable `r.Shadow.Virtual.UseFarShadowCulling 0`.

Local lights (Point and Spot Lights) are not affected, and selecting Distance Field shadows for these continues to override the active shadow map method.

Due to VSM's high resolution and accuracy, the screen space Contact Shadow feature controlled with the Contact Shadow Length property is no longer necessary to achieve sharp contact shadows. It still may have value when used to pick up cheaper shadows from objects set to not render into shadow maps but is not recommended otherwise as it will be less accurate than the shadows VSMs will create.

Ray-traced shadows still take precedence over VSMs as they generally provide the highest quality solution.

## Soft Shadows with Shadow Map Ray Tracing

**Shadow Map Ray Tracing** (SMRT) is a sampling algorithm used with virtual shadow maps to produce more plausible soft shadows and contact hardening. Objects that cast shadows farther will have softer shadows than objects casting shadows closer to a shadow-receiving surface. For example, the mesh pictured below is tall and casts its shadow over a long distance. Shadows near the base are sharper than those farther away.

[![](https://dev.epicgames.com/community/api/documentation/image/f003d54f-b2d0-4610-a99a-99bc70fea354?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f003d54f-b2d0-4610-a99a-99bc70fea354?resizing_type=fit)

Example with a Point Light casting soft shadows and contact hardened shadows using Shadow Map Ray Tracing.

Past methods based on Percentage-Closer Filtering (PCF) would over-blur and reduce the visual impact of high-resolution geometry and shadows.

![Percentage-Closer Filtering blurs uniformly, | removing important detail](https://dev.epicgames.com/community/api/documentation/image/ffaf25eb-d107-4323-8612-5c98a24e50fc?resizing_type=fit&width=1920&height=1080)

![Shadow Map Ray Tracing produces plausible | soft shadows with contact hardening](https://dev.epicgames.com/community/api/documentation/image/a4a6b4d9-18ed-49f2-91b4-6cb2766e255a?resizing_type=fit&width=1920&height=1080)

Percentage-Closer Filtering blurs uniformly, | removing important detail

Shadow Map Ray Tracing produces plausible | soft shadows with contact hardening

The SMRT algorithm works by shooting a number of rays towards the light source, but instead of evaluating intersections with geometry — like conventional raytracing does — a number of samples along the ray are projected and tested against the virtual shadow map to achieve soft shadowing and contact hardening. Shadow rays are distributed based on the light using **Source Radius** on local lights or **Source Angle** on Directional Lights.

|  |  |
| --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/62c94e0b-820f-45d3-93f3-1e4471fceb22?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/62c94e0b-820f-45d3-93f3-1e4471fceb22?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/1008aa28-0701-4ca7-b9af-01f1d62d77da?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1008aa28-0701-4ca7-b9af-01f1d62d77da?resizing_type=fit)



 |
| 

Local Light Source Radius

 | 

Directional Light Source Angle

 |

Local lights have no Source Radius by default, compared to Directional Lights which start with a low Source Angle. When either are set with an appropriate value, SMRT produces real-time soft shadowing with contact hardening, like the example below using a Point Light with a Source Radius of 10.

![Point Light with Source Radius 0](https://dev.epicgames.com/community/api/documentation/image/9cdd75cf-573f-422b-bfcb-a35e538a9e79?resizing_type=fit&width=1920&height=1080)

![Point Light with Source Radius 10](https://dev.epicgames.com/community/api/documentation/image/1247b8df-f994-465a-81d9-95b8942927eb?resizing_type=fit&width=1920&height=1080)

Point Light with Source Radius 0

Point Light with Source Radius 10

### Controlling Penumbra Shadow Quality

The penumbra shadow's softness and quality is set by console variables for both local and Directional Lights. They include their own scalability settings that are generally good for most scenes.

Noise in the penumbra is influenced by the number of rays being used, and both local and Directional Lights use eight rays by default when scalability for **Shadows** is set to **Epic**.

Use the console variables `r.Shadow.Virtual.SMRT.RayCountLocal` and `r.Shadow.Virtual.SMRT.RayCountDirectional` to adjust the number of rays. Fewer rays show visible noise in the penumbra. Setting the associated console variable to 0 disables SMRT and reverts to single-sample hard shadows.

![Directional Light Source Angle: 5.0 | SMRT Ray Count: 1](https://dev.epicgames.com/community/api/documentation/image/ad78d819-a722-4444-ae8c-7d0a65fe4468?resizing_type=fit&width=1920&height=1080)

![Directional Light Source Angle: 5.0 | SMRT Ray Count: 7 (Default)](https://dev.epicgames.com/community/api/documentation/image/b791fb7b-32b5-4d07-9e46-b9a7045b6015?resizing_type=fit&width=1920&height=1080)

Directional Light Source Angle: 5.0 | SMRT Ray Count: 1

Directional Light Source Angle: 5.0 | SMRT Ray Count: 7 (Default)

Furthermore, the number of shadow samples taken along each ray's path can be set for both local and Directional Lights to control the maximum softness. Fewer shadow map samples are cheaper to render, but limit the amount of penumbra softness that can be achieved by the light's shadows. For finer control than the **Shadow** scalability settings, and the console variables `r.Shadow.Virtual.SMRT.SamplesPerRayLocal` and `r.Shadow.Virtual.SMRT.SamplesPerRayDirectional` to adjust the number of samples used. Using values between 4 and 8 samples works well.

![Dragging the slider will show what happens when a Directional Light with a Source Angle of 5.0 uses Shadow Map Samples that number 0, 2, and 8 (default).](https://dev.epicgames.com/community/api/documentation/image/53b8d53d-270c-4965-9b80-7de458837166?resizing_type=fit&width=1920&height=1080)![Dragging the slider will show what happens when a Directional Light with a Source Angle of 5.0 uses Shadow Map Samples that number 0, 2, and 8 (default).](https://dev.epicgames.com/community/api/documentation/image/4c405ebc-f928-4ded-b5cf-4c70561b0335?resizing_type=fit&width=1920&height=1080)![Dragging the slider will show what happens when a Directional Light with a Source Angle of 5.0 uses Shadow Map Samples that number 0, 2, and 8 (default).](https://dev.epicgames.com/community/api/documentation/image/a3f8acea-de35-4099-8a14-a7c19343c3c4?resizing_type=fit&width=1920&height=1080)

**Dragging the slider will show what happens when a Directional Light with a Source Angle of 5.0 uses Shadow Map Samples that number 0, 2, and 8 (default).**

### Limitations of Shadow Map Ray Tracing

Quality of SMRT is generally good with the default setting, but there are limitations inherent to using the data from a single shadow map projection rather than testing against true geometry.

### Penumbra Size Limits

The shadow's penumbra is clamped for local and Directional Lights to avoid sample divergence from the ray origin that can become increasingly "bent" compared to the ideal test along the ray itself. Using reasonable values for Source Radius on local lights and Source Angle on Directional Lights will avoid results that are too extreme, limiting the extent that the ray can diverge in various ways. Values that are too large can both impact performance and cause shadow penumbrae to visually warp as the camera gets near to them.

Local and Directional Lights can use the console variables `r.Shadow.Virtual.SMRT.MaxRayAngleFromLight` and `r.Shadow.Virtual.SMRT.RayLengthScaleDirectional` to loosen or tighten the clamped extents.

### Inconsistent Penumbra

Since the Virtual Shadow Map only stores the first depth layer where naive iteration misses intersections with any occluders behind the first one, a variety of light leaking artifacts can happen where the occluders overlap. These types of light leaks are resolved using a gap-filling heuristic that extrapolates depths behind the first occluder based on depths seen before the point of occlusion.

This works well in resolving lighting leaks, but causes penumbrae on surfaces parallel to the light to shrink in size. There is currently no direct way to counteract this effect other than to keep penumbra sizes reasonable.

[![](https://dev.epicgames.com/community/api/documentation/image/bc0d8042-05f0-4912-ad2f-8a3e5721f23a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bc0d8042-05f0-4912-ad2f-8a3e5721f23a?resizing_type=fit)

Examples of inconsistent penumbra shadows.

### Penumbra Artifacts

By default, Virtual Shadow Maps only guarantees that the samples around the ray origin (the receiver pixel) will be present. As the algorithm traverses the ray, it can encounter unmapped pages where no shadow data exists. A variety of techniques are used to reduce the impact of this, including dilating the page mappings slightly and having various fallbacks in place during iteration. Even still, occasional artifacts stemming from missing pages can happen, especially around edges of the screen when zoomed in on soft penumbra. These artifacts will manifest as noisy light leaks in shadowed areas. Like other limitations with VSMs, issues can mostly be avoided by keeping shadow penumbra sizes reasonable and avoiding zooming in to the point where they cover large portions of the screen.

## Clipmaps for Directional Light

A single virtual shadow map does not provide enough resolution to cover large areas. Directional Lights use a clipmap structure of expanding ranges around the camera, with each clipmap level having its own 16K VSM. Each clipmap level is the same resolution but covers twice the radius of the previous one.

|  |  |
| --- | --- |
| 
[![Directional Light Clipmap Visualization](https://dev.epicgames.com/community/api/documentation/image/d16e8752-2327-44e3-88de-1ea3fd7d77be?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d16e8752-2327-44e3-88de-1ea3fd7d77be?resizing_type=fit)



 | 

[![Virtual Shadow Map Pages Visualization](https://dev.epicgames.com/community/api/documentation/image/3064da6d-74b0-418c-8262-55fc76037db0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3064da6d-74b0-418c-8262-55fc76037db0?resizing_type=fit)



 |
| 

Directional Light Clipmap Visualization

 | 

Virtual Shadow Map Pages Visualization

 |

By default, clipmap levels 6 through 22 are allocated virtual shadow map page tables. This means that the default settings have the most detailed clipmap covering 64 cm (2^6 cm) from the camera position, and the broadest clipmap covering about 40 kilometers (2^22 cm). The cost of virtual clipmap levels is insignificant if nothing is present in them, so these defaults work well to cover very large scenes with fairly high resolution near the camera.

The first and last levels can be adjusted using the console variables r.Shadow.Virtual.Clipmap.FirstLevel and `r.Shadow.Virtual.Clipmap.LastLevel`.

The resolution allocated to a given pixel is a function of the distance away from the clipmap origin — the camera. This is set by Shadow scalability with the console variable `r.Shadow.Virtual.ResolutionLodBiasDirectional`. A value of 0 picks the resolution required based on the perspective projection of the camera. Projective aliasing — when a shadow is cast on a surface almost parallel to the light direction — is still possible, even at high resolutions, but it can be reduced partly by biasing the resolution. Like Mip biasing in textures, lowering the value by -1 doubles the resolution of shadows with the associated performance tradeoffs. The default value of -1.5 on Epic Shadow scalability provides a reasonable balance for many scenes.

## Local Lights

Spot Lights use a single 16k VSM with a mip chain rather than clipmaps to handle shadow level of detail. Similarly, Point Lights use a cube map of 16k VSMs, one for each face.

Local lights provide a significant increase in resolution compared to traditional shadow maps. It is possible to run out of virtual resolution with very large local lights, and care should be taken to use Directional Lights where possible in these cases.

![Scene lit by a Spot Light](https://dev.epicgames.com/community/api/documentation/image/e77a3647-e525-4dbf-9462-da03bdc23848?resizing_type=fit&width=1920&height=1080)

![Virtual Shadow Map Pages for a Spot Light](https://dev.epicgames.com/community/api/documentation/image/51404ad9-8e1f-45c0-8ef6-52627d654ce2?resizing_type=fit&width=1920&height=1080)

Scene lit by a Spot Light

Virtual Shadow Map Pages for a Spot Light

Appropriate mip levels are picked by projecting the size of the screen pixels into shadow map space. Like Directional Lights, it's possible to bias the resolution with the Shadow scalability settings, or using the console variable `r.Shadow.Virtual.ResolutionLodBiasLocal`.

Per-light resolution controls are not available but may be added in a future release.

## Moving Lights

Stationary lights are largely cached and, as a result, can use a much higher resolution than moving lights. To account for this difference between stationary and moving lights, movable lights should have a different LOD bias than stationary lights. When a light stops moving, it does a gradual transition to the original bias. You can control the LOD bias for moving lights with the following scalability console variables:

-   `r.Shadow.Virtual.ResolutionLodBiasLocalMoving`
    
-   `r.Shadow.Virtual.ResolutionLodBiasDirectionalMoving`
    

## Translucent surfaces

Virtual Shadow Maps support high quality shadow filtering for translucent surfaces with Substrate and legacy paths. This is a global opt-in feature that you can enable with the console variables `r.Shadow.Virtual.TranslucentQuality`. This console variable controls the quality of shadows for lit, translucent surfaces. This is applied on all translucent surfaces and has a high performance impact. Settings for `r.Shadow.Virtual.TranslucentQuality`:

-   Any value greater than 1: High quality shadows for lit translucent surfaces.
    
-   0: (Default) Normal quality shadows for lit translucent surfaces.
    

## Coarse Pages

Depth buffer analysis is used as the primary method of marking pages that are needed to render. There are some systems that need to sample shadows at more arbitrary locations though, such as [Volumetric Fog](building-virtual-worlds\lighting-and-shadows\environmental-lighting\volumetric-fog) and forward-rendered translucency. Most systems only need low-resolution shadow data that gets filtered and blurred through other data structures.

To accommodate shadowing in these situations, **Coarse Pages** are marked to ensure that at least low-resolution shadow data is available across the whole domain for sampling. Local lights simply mark the root mip page while Directional Lights can mark a series of pages at various low detail levels to form some coarse clipmaps. Depending on the scene, coarse pages can create performance issues. This is particularly true for non-Nanite dynamic geometry since they are effectively rendering low-resolution shadows over large regions of space, which can result in draw-call bottlenecks.

It is recommended to experiment with disabling non-Nanite objects rendering into the coarse pages using the console variable `r.Shadow.Virtual.NonNanite.IncludeInCoarsePages 0`.

Many scenes — especially ones consisting primarily of Nanite geometry — do not need non-Nanite objects casting shadows onto Volumetric Fog and similar things. Disabling this can provide a significant performance improvement.

Local light coarse pages can be toggled off with `r.Shadow.Virtual.MarkCoarsePagesLocal`, if not needed. Directional Light coarse pages can be toggled off with `r.Shadow.Virtual.MarkCoarsePagesDirectional`, or the range of clipmap levels that coarse pages are marked in can be modified with `r.Shadow.Virtual.FirstCoarseLevel` and `r.Shadow.Virtual.LastCoarseLevel`.

In a future release, a more elegant solution would be where some of these effects can be marked for localized pages directly in advance rather than the current, overly conservative coarse pages being used.

## Visualization

Visualization options for Virtual Shadow Maps are accessible from the Level Viewport using the **View Modes** drop-down menu and selecting **Virtual Shadow Map**.

[![Level Viewport Virtual Shadow Maps View Mode Options](https://dev.epicgames.com/community/api/documentation/image/0201bf8b-2a29-4deb-8d71-abada728a0d1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0201bf8b-2a29-4deb-8d71-abada728a0d1?resizing_type=fit)

Visualization options include:

| Visualization Name | Description |
| --- | --- |
| 
**Shadow Mask**

 | 

The final shadow mask that is used by shading.

 |
| 

**Clipmap/Mip Level**

 | 

The chosen clipmap (for Directional Lights) or mip (for Local Lights) level.

 |
| 

**Virtual Page**

 | 

Visualization of the virtual page address.

 |
| 

**Cached Page**

 | 

Cached pages are tinted green, uncached pages are red. Pages where only the static page is cached (dynamic uncached) are blue.

 |

By default, the Virtual Shadow Map visualizations display results for the Directional Light. By selecting a light in the **Outliner**, you can view visualizations for that light.

You can also enable visualization using the console (except in Shipping builds), which is useful for profiling and debugging a live game. If any of these are set in the editor, they override any mode selection made through the editor's user interface.

| Visualization Name | Description |
| --- | --- |
| 
`r.Shadow.Virtual.Visualize [mode]`

 | 

When the view mode visualization is set to Virtual Shadow Map through the Level Viewport or the console command, this command specifies which of the channels to display. Use the names below in place of "\[mode\]" to enable that visualization. **Cache** and **vpage** are two common ones used for visualization and **none** disables vsm visualization.

-   mask
    
-   mip
    
-   vpage
    
-   cache
    
-   raycount
    
-   clipmapvirtual
    

 |
| 

`ShowFlag.VisualizeVirtualShadowMap`

 | 

Enables the Virtual Shadow Map visualization when a visualization mode is specified.

 |
| 

`r.Shadow.Virtual.Visualize.Layout`

 | 

Choose a layout for the Virtual Shadow Map visualization.

-   **0** is full screen
    
-   **1** is a thumbnail
    
-   **2** is split-screen
    

 |
| 

`r.Shadow.Virtual.Visualize.DumpLightNames`

 | 

Outputs a list of the current lights with Virtual Shadow Maps to the console.

In some build / runtime configurations, the names of the lights may be different from their names in the editor.



 |
| 

`r.Shadow.Virtual.Visualize.LightName [light name]`

 | 

Specify a light by name, partial or full matches are accepted.

To clear a light from being selected using this console variable, specify a light name that won't match any names. Using two quotation marks (") is an acceptable way of resetting it back to no specified light.



 |

Enabling visualization modes has a small but measurable effect on the performance of Virtual Shadow Maps. Be sure to disable the visualization before performance profiling.

## Caching

Reusing shadow map pages from previous frames is key to maintaining high performance with Virtual Shadow Maps, especially in complex scenes. Caching is enabled by default, but can disabled for debugging purposes using the console variable `r.Shadow.Virtual.Cache 0`. Virtual Shadow Maps respect the Nanite cull distance when caching is enabled.

Since pages are only rendered for on-screen pixels, changing camera visibility due to movement of disocclusion can reveal new pages that need to be rendered. Generally, as long as camera movement is relatively smooth, it is not a major source of new pages. On the other hand, you should watch out for very fast movement near objects, large disocclusions, and camera cuts.

In most scenes, the largest source of work comes from shadow map pages that need to be redrawn due to changes in scene geometry. Common sources of cache page invalidations include:

-   Any light movement or rotation will invalidate all cached pages for that light
    
-   Geometry that casts shadows moving, or being added or removed from the scene will invalidate any pages that overlap its bounding box from the light's perspective.
    
-   This can include objects such as Blueprints setting properties on primitive components that trigger render state invalidation even though it does not actually move.
    
-   Geometry using materials that may modify mesh positions, such as World Position Offset (WPO) or Pixel Depth Offset (PDO)
    

In instances where you have a slowly moving light, or a shifting Directional Light changing the time of day, VSM pages will effectively not be cached at all. In situations like time-of-day changes, it is recommended to quantize the changes by some small amount to allow cached pages to live for some number of frames since the tiny differences in direction will not be noticeable.

In a future release, caching should improve by adding a priority system and per-frame update budgets to allow finer control over the cost of rendering shadows. For example, allowing shadow resolution to temporarily lower in cases where too many pages need updates.

### Managing Cache Invalidations

Decreasing cache invalidations is best done by first visualizing the invalidations, then finding and reducing the things causing them. The [Cached Page visualization](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine#visualization) is a good place to start.

[![Virtual Shadow Map Cached Page Visualization](https://dev.epicgames.com/community/api/documentation/image/909d90e1-2bb3-4424-8e52-6c48a4e8b54b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/909d90e1-2bb3-4424-8e52-6c48a4e8b54b?resizing_type=fit)

Cached Page Visualization

In this visualization, pages that are fully cached are shaded **green**. Pages that are new or invalidated are shaded **red**. As you move the camera you should expect to see small rings of red near screen edges, clipmap boundaries and disoccluded geometry. With a static camera, most of the new pages will come from cache invalidations.

If separate static caching is enabled (see below), pages that are partially cached (where only the static portion is valid) will show up as **blue**.

Once problem areas have been found, it is often additionally useful to turn on a visualization of the object bounds that are driving the invalidations using the console variable `r.Shadow.Virtual.Cache.DrawInvalidatingBounds 1`. Inspect these objects and bounds to ensure that they are indeed objects that are expected to invalidate shadows, and that their bounds are as tight as possible. Since all pages that an invalidating object could potentially overlap within its bounds must be invalidated, even moderately inflated bounds combined with low light angles can cause many unnecessary invalidations.

[![Virtual Shadow Map Cached Page Invalidated Bounds Visualization](https://dev.epicgames.com/community/api/documentation/image/b0745cba-4d1a-45fb-ae61-bce665298f9e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b0745cba-4d1a-45fb-ae61-bce665298f9e?resizing_type=fit)

Cached Pages and Invalidating Bounds Visualization

Invalidations that are entirely in the shadow of Nanite objects can be skipped, but this is not true for non-Nanite objects. For this reason it is particularly important to ensure that large shadow-casting objects — such as buildings — use [Nanite](designing-visuals-rendering-and-graphics\rendering-optimization\nanite).

You can trigger Virtual Shadow Map invalidation on Nanite LOD streaming changes with the console variable `r.Nanite.VSMInvalidateOnLODDelta`. Clusters that are not streamed into LOD matching the computed Nanite LOD estimate trigger VSM invalidation such that they are re-rendered when streaming completes. This functionality is experimental. We do not recommend shipping projects with Experimental features and this feature is subject to change.

In complex scenes, it can sometimes be difficult to pinpoint what is causing invalidations even with these visualizations. Another tool that can help is the **Draw only Geometry Causing VSM Invalidation** visualization mode found in the Level viewport under **Show > Visualize**.

[![Virtual Shadow Maps Draw Only Geometry Causing VSM Invalidation Visualization](https://dev.epicgames.com/community/api/documentation/image/ab7fce8b-087a-41b7-89b2-7720faddfdff?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ab7fce8b-087a-41b7-89b2-7720faddfdff?resizing_type=fit)

When enabled, any geometry that is not causing cache invalidations is hidden.

Due to implementation details, the **Draw Only Geometry Causing VSM Invalidation** mode occasionally shows objects that are unrelated to shadowing (such as particle and visual effects) that go through a separate rendering pass and are drawn on top.

Stats are not reliable while using this visualization because rendering the main scene differently affects which pages are mapped and invalidated. It is better to start with other [visualization modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine#visualization) and use this one to double-check.

There is a known issue with [Scene Capture Components](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) that can cause the entire cache to be invalidated.

You can override default engine behavior for shadow invalidations with the per-primitive enumeration class Shadow Cache Invalidation Behavior. This is useful to prevent invalidations from static World Position Offset (WPO). The options include:

-   **Auto**: (Default) Invalidates based on World Position Offset material and transform changes.
    
-   **Always**: Always invalidate shadows, can be used to flag a primitive that is using some method of animating that is not known to the system.
    
-   **Rigid**: Suppress invalidations that would otherwise be generated by, for example, World Position Offset.
    
-   **Static**: In addition to the **Rigid** behavior, also suppress invalidations due to transform changes. Add/Remove still triggers invalidations. If the primitive is moved or animated, the visual result is undefined.
    

### Non-Nanite Deformation and Foliage

Geometry that can be deformed using Skeletal animation, or materials using World Position Offset or Pixel Depth Offset always invalidates cached pages every frame. By definition, these cases must also be non-Nanite — which is more expensive — and therefore it is extremely important to ensure that these features are used carefully and bounds are kept under control.

In some cases, such as grass and sometimes foliage, using only [Contact Shadows](https://dev.epicgames.com/documentation/en-us/unreal-engine/contact-shadows-in-unreal-engine) is a sufficient substitute for high resolution shadow maps. In cases where high detail shadows are necessary in the foreground, consider the following to help mitigate the performance cost:

-   Non-Nanite objects still respect the regular shadow CPU culling settings, such as `r.Shadow.RadiusThreshold`. Use these to help control the cost of rendering these objects into Virtual Shadow Maps.
    
-   In scenes with lots of foliage, it is highly recommended to disable non-Nanite objects in coarse pages with `r.Shadow.Virtual.NonNanite.IncludeInCoarsePages 0`. Or, consider [disabling coarse pages entirely](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) if they are not needed.
    
-   Use Mesh LODs to switch to materials that do not use WPO/PDO at distances where the effect is no longer obvious. In some cases, it may be possible to switch off dynamic shadow casting for these objects in the distance and rely entirely on screen space Contact Shadows.
    

For Directional Lights, there are additional options available:

-   Distance Field Shadows take over for non-Nanite geometry beyond the **Dynamic Shadow Distance Movable Light** distance set by the Cascaded Shadow Maps section of the Light. Switching to Distance Field Shadows for non-Nanite in the distance can be a large performance improvement since this geometry does not have the fine-grained LOD scaling that Nanite provides.
    

### Separate Static Caching

This feature is considered **experimental**.

Many scenes consist of a large amount of static geometry that never moves, together with significantly smaller amounts of dynamic (or movable) geometry. By default, this means that the relatively cheap dynamic geometry invalidates pages that then cause the expensive static geometry to be re-rendered, just to update the dynamic portion.

To better optimize in these cases, an optional **Separate Static Caching** mode can be enabled using `r.Shadow.Virtual.Cache.StaticSeparate 1`. This mode doubles the size of the physical page pool so that the static geometry in a given page can be cached separately from the dynamic geometry. Even when the dynamic geometry moves, there is no need to redraw the static geometry. Instead, the cached static page can be cheaply composited on top. In cases, such as the [Valley of the Ancients](https://dev.epicgames.com/documentation/en-us/unreal-engine/valley-of-the-ancient-sample-game-for-unreal-engine) sample project, it can be a significant performance optimization as the static terrain is very expensive while the dynamic elements are relatively cheap.

While using this mode, it's important to accurately set the [Mobility of Actors](https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-mobility-in-unreal-engine) in the scene. In particular, if an Actor that is set to Static Mobility moves — or even uses a material with World Position Offset or similarly unsupported materials — it invalidates both the dynamic and static cached pages, resulting in pure overhead for no gain. Conversely, if too much of the expensive geometry is set to Movable Mobility, then there may be little benefit from caching it separately.

The Virtual Shadow Map statistics are a good way to get a high level overview of how well static caching is working. In particular, the number of "invalidated" static pages should be near 0. Finding instances that are invalidating the static cache frequently and switching them to Movable is an important way to ensure the static cache remains valid.

Nanite includes an advanced visualization mode to help determine object mobility in the world, which is also useful for Virtual Shadow Maps.

[![Virtual Shadow Maps Nanite VSM Static Visualization](https://dev.epicgames.com/community/api/documentation/image/954caa65-1c65-4502-88cc-0dcb8256877b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/954caa65-1c65-4502-88cc-0dcb8256877b?resizing_type=fit)

Nanite's Advanced Virtual Shadow Map Static visualization mode

This visualization mode can be enabled in one of two ways:

-   Enable Nanite's advanced visualization options with `r.Nanite.Visualize.Advanced 1` and then use the Level Viewport to select the **View Mode > Nanite Visualization** and choose **Virtual Shadow Map Static** from the list of visualization options.
    
    [![Advanced Nanite View Mode Options](https://dev.epicgames.com/community/api/documentation/image/34718668-99df-4fff-85c1-7eb585faac1f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/34718668-99df-4fff-85c1-7eb585faac1f?resizing_type=fit)
    
    Click image for full size.
    
-   Alternatively, you can enable the Virtual Shadow Map Static visualization with the command `r.Nanite.Visualize vsmstatic`.
    

## GPU Profiling and Optimization

Unreal Engine provides tools that help you check performance in your projects, and the [GPU Profiler](https://docs.unrealengine.com/4.27/TestingAndOptimization/PerformanceAndProfiling/GPU) (or platform-specific tool) is a good starting place to troubleshoot and debug performance issues.

There are two main performance buckets where VSM costs will show up: Shadow Depths and Shadow Projection (under Lights). The tradeoffs in each of their categories are relatively independent from one another.

Be aware that commands used to list statistics, such as stat gpu and associated counters, can provide unreliable timings, especially if your project's performance is CPU-bound.

### Shadow Depths

The **Shadow Depths** category refers to the cost of rendering geometry into shadow maps.

[![GPU Profile Shadow Depths](https://dev.epicgames.com/community/api/documentation/image/bf6b2a52-cf1c-47b7-9c86-1db8b16c3441?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bf6b2a52-cf1c-47b7-9c86-1db8b16c3441?resizing_type=fit)

-   **RenderVirtualShadowMaps(Nanite)** contains all rendering of Nanite geometry into VSMs. All Directional Lights are rendered in a single Nanite pass, and all local lights are done in a second pass.
    
-   **RenderVirtualShadowMaps(Non-Nanite)** handles the rendering of non-Nanite geometry. Each visible light has a separate pass with individual draw calls for various objects and instances, the same as conventional shadow maps rendering.
    
-   **Atlas** and **Cubemap**, along with other similar passes, following the VSM passes are rendering conventional shadow maps. There are still a small number of geometry types that are not yet supported in the Virtual Shadow Maps path, and those follow the old path. If there is no unsupported geometry casting shadows, these passes will not run or allocate shadow map storage. These passes and associated overhead can be disabled entirely with the console variable `r.Shadow.Virtual.ForceOnlyVirtualShadowMaps 1`, in which case any unsupported geometry types will simply not cast shadows.
    

The cost of the Shadow Depths pass with VSMs is directly related to how many shadow pages need to be rendered, and how much geometry needs to be rendered into them. Non-Nanite geometry is much more expensive to render into VSMs than Nanite geometry. For this reason, **it is recommended to enable Nanite on all supported geometry, including low-poly meshes.** The only exception is for features not yet supported by [Nanite Virtualized Geometry](designing-visuals-rendering-and-graphics\rendering-optimization\nanite).

#### Understanding the Number of Pages Being Drawn

The on-screen stats for VSM pages used can give an idea of how many pages are being used, and where to look to resolve potential problems.

Use the following console variables in succession to enable stats:

-   `r.ShaderPrintEnable 1`
    
-   `r.Shadow.Virtual.ShowStats 1` (or 2 to show only the page statistics)
    

[![Virtual Shadow Maps Pages Stats](https://dev.epicgames.com/community/api/documentation/image/eb09544c-c96a-4d82-819f-50181bbd54a8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eb09544c-c96a-4d82-819f-50181bbd54a8?resizing_type=fit)

| Stat Name | Description |
| --- | --- |
| 
**Physical Pages**

 | 

The maximum number of physical pages that virtual shadow maps can use.

 |
| 

**Allocated**

 | 

The total number of requested shadow map pages by the current view. It should always be less than Max pages, otherwise corruption can occur. (See the [Issues and Limitations](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) section below.)

 |
| 

**Cleared**

 | 

The number of new pages that were cleared in the current frame.

 |
| 

**Cached**

 | 

The number of pages that are already in the virtual shadow map page cache, and that do not need to be rendered in the current frame. Cached pages are very low cost and will have almost no impact on performance. When separate static caching is enabled, this is further split by cached Static Pages and Cached Dynamic Pages.

 |
| 

**Invalidated**

 | 

The number of otherwise-cached pages that were invalidated by dynamic geometry in the previous frame. These pages need to be rendered again because something moved that covers them. When using separate static caching the number of invalidations of static pages should ideally be zero or very close to it. If large numbers of static pages are being invalidated the actor(s) causing the invalidations should be switched to Movable.

 |
| 

**Merged**

 | 

When separate static caching is enabled, this is the number of pages where the dynamic and static pages were merged (due to one or the other not being cached).

 |

The total page counts are a function of the average number of lights that affect each pixel on screen. They can be lowered by reducing screen resolution, shadow resolution (using the console variables for resolution LOD bias), light extents, or the number of shadow casting lights.

Poor performance in shadow depths is typically associated with a high number of pages being used and lots of dynamic invalidation happening, which leads to poor caching of VSMs. See the [Caching](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine#caching) section for more details on diagnosing and reducing cache invalidations.

#### Improving Non-Nanite Performance

Beyond improving caching, there are a number of ways to improve the performance of non-Nanite shadow rendering.

Consider the following to improve non-Nanite object performance:

-   Enable Nanite on as much geometry as possible for your project.
    
    -   Nanite geometry renders far more efficiently into Virtual Shadow Maps and should be preferred in every applicable case, regardless of polygon counts.
        
    -   Nanite geometry can occlude non-Nanite geometry and avoid spurious cache invalidations. Thus, the only non-Nanite objects should be those that are not supported by Nanite itself, such as deforming objects (skinned meshes), or materials using World Position Offset (WPO) and Pixel Depth Offset (PDO).
        
-   Non-Nanite objects should have full Mesh LOD hierarchies setup.
    
    -   It is important that non-Nanite meshes have LODs setup or else they become extremely expensive to render into small pages.
        
    -   Where possible, it is advisable to switch to non-deforming meshes (no WPO/PDO materials) beyond a distance where the effect is obvious.
        
-   CPU culling console variable are still useful for Non-Nanite meshes rendering into Virtual Shadow Maps
    
    -   Adjust values of CPU culling on non-Nanite objects rendering into Virtual Shadow Maps with the console variable `r.Shadow.RadiusThreshold`. It can help control the cost of small objects in the distance.
        
-   Using [Distance Field Shadows](https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine) for distant shadowing of Non-Nanite Objects
    
    -   For Directional Lights, it is often necessary to switch to Distance Field Shadows beyond some range, same as Cascaded Shadow Maps. With Virtual Shadow Maps, only non-Nanite geometry will switch to using the Distance Field Shadows while Nanite geometry continues to have full-detail shadows.
        
-   Disabling non-Nanite geometry in Coarse Pages can increase performance
    
    -   Disabling non-Nanite geometry in coarse pages can often net a large performance gain, since non-Nanite geometry is generally inefficient to render into large pages.
        

The Virtual Shadow Maps statistics can give some insight into non-Nanite instance counts:

[![Virtual Shadow Maps Pages Stats](https://dev.epicgames.com/community/api/documentation/image/a3897086-b940-46bd-ad86-64f46cfb17a2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a3897086-b940-46bd-ad86-64f46cfb17a2?resizing_type=fit)

| Stat Name | Description |
| --- | --- |
| 
**Total**

 | 

Total number of non-Nanite instances input to the GPU culling. Instances are culled separately for each virtual shadow map mip/clipmap level. For example, a single Static Mesh instance can result in 48 instances (8 mip levels \* 6 cubemap faces) for each point light that it intersects, 17 instances for each Directional Light (in default configuration there are 17 clipmap levels) and so on.

 |
| 

**Drawn**

 | 

Number of instances actually drawn into all virtual shadow maps after culling.

 |
| 

**HZB Culled**

 | 

Number of instances removed due to being occluded (by Nanite geometry) from the light's perspective.

 |
| 

**Page Mask Culled**

 | 

Number of instances removed due to not overlapping any required pages. This, for example, represents Static Meshes that are discarded when drawing into already cached areas.

 |
| 

**Empty Rect Culled**

 | 

Number of instances removed due to not overlapping any required pages. For example, this represents Static Meshes that are discarded when drawing into already cached areas.

 |
| 

**Frustum Culled**

 | 

Number of instances that were outside the view frustum.

 |

### Shadow Projection

The **Shadow Projection** category is the cost of sampling shadow maps using Shadow Map Ray Tracing. These passes are located under the **Lights | DirectLighting | UnbatchedLights** and there will typically be one VSM projection pass per associated light. The most expensive pass is usually the main SMRT loop in **VirtualShadowMapProjection**. The rest should be relatively low cost.

If the projection pass is labeled as **RayCount:Static** instead of **RayCount:Adaptive**, a slow path is being taken.

The VSM projection pass described in this section is different from the experimental One Pass Projection described in the next section.

[![GPU Profile Shadow Projection](https://dev.epicgames.com/community/api/documentation/image/35526f40-92a1-4926-997e-52dc21616833?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/35526f40-92a1-4926-997e-52dc21616833?resizing_type=fit)

Shadow projection is purely a function of the total number of shadow map samples that are taken across the screen, and performance doesn't depend on the number of pages or caching.

When SMRT is being used, it comes down to:

-   **Average lights per pixel**
    
    -   The more lights touching large portions of the screen, the more expensive rendering will be. Lights covering small numbers of on-screen pixels are cheaper, although there are still some fixed costs per light.
        
    -   Care should be taken to avoid having the majority of pixels on screen taken up by several large lights.
        
-   **Rays per pixel**
    
    -   Visible softness of shadows affects performance due to the adaptive ray count. Try reducing the Source Radius of local lights or Source Angle of Directional Lights before lowering any of the ray and sample counts.
        
-   **Samples per ray**
    

These settings are set by the **Shadow** scalability setting, but can be further adjusted if needed. See the Shadow Map Ray Tracing section of this page for more details.

Generally, shadow projection costs are much easier to control (trade off with quality and noise) than shadow depth costs.

#### One Pass Projection

This feature is considered experimental. The console variable names in this section are likely to change.

Even though smaller lights have a lower cost, they still have some fixed pass overheads. This is being addressed by developing a single-pass shadow projection solution where the majority of local lights in a scene can efficiently evaluate their shadowing in one pass. The shadowed contribution from these lights can then be applied all at once using clustered shading.

This path is enabled using the console variables `r.UseClusteredDeferredShading 1` and `r.Shadow.Virtual.OnePassProjection 1`. For scenes with a lot of small local lights, this can result in significant improvements to performance.

The use of certain light features will prevent a light from being batched even when One Pass Projection is enabled:

-   Texture Profiles
    
-   Light Functions
    
-   Lighting Channels
    
-   Rect Lights
    
-   Directional Lights (there is no benefit to these being batched since they cover the full screen)
    

In the captures below, the left shows a shadow projection pass happening per-light compared to the right side's one pass projection.

[![GPU Profile Comparison One Pass Projection](https://dev.epicgames.com/community/api/documentation/image/72f34462-8fbe-4a7a-83d6-3e415332e4ba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/72f34462-8fbe-4a7a-83d6-3e415332e4ba?resizing_type=fit)

*Click image for full size.*

In the default path on the left, each local light is accumulated one by one with several passes per light. This is inefficient for small lights that cover a small screen area.

In the new path on the right, all of the shadowed local lights are batched together in the single clustered shading pass (**BatchedLights**). The Directional Light is still done in a separate pass; it covers the whole screen and thus is not a benefit to batch it.

Each local light still injects into the translucency volume separately. This is less of an issue for performance than the projection, but will likely also be batched together in the future.

When One Pass Projection is enabled it is possible to limit the number of shadowed lights that are fully filtered per-pixel by adjusting `r.Shadow.Virtual.OnePassProjection.MaxLightsPerPixel` from the default of 16. This is useful both for controlling performance and can save a small amount of transient graphics memory.

If there are more shadowed lights than the maximum in a given pixel (or in practice, a clustered deferred shading tile), additional lights will be shadowed using an inexpensive single hard shadow lookup. This can cause visual discontinuities if the value is set too aggressively, but is generally more forgiving than entirely disabling shadows for lights beyond the count.

This pass is still in development and not enabled by default. The primary caveat is in cases that a local light would have both a virtual shadow map and a classic shadow map (due to some unsupported geometry type in the scene), the One Pass Projections path ignores the latter, causing those shadows to disappear.

If you are using `r.Shadow.Virtual.ForceOnlyVirtualShadowMaps` already, it should be safe to also enable One Pass Projection. Once current limitations have been addressed, it will likely become the default path used.

## Supported Platforms

Virtual Shadow Maps are currently supported on PlayStation 5, Xbox Series S|X, and PCs with graphics cards meeting these specifications, using the latest drivers with DirectX 12:

-   NVIDIA: Maxwell-generation cards or newer
    
-   AMD: GCN-generation cards or newer
    
-   All newer versions of Windows 10 (newer than version 1909.1350) and Windows 11 with support for [DirectX 12 Agility SDK](https://devblogs.microsoft.com/directx/gettingstarted-dx12agility) are supported.
    
    -   Windows 10 version 1909 — The revision number should exceed or be equal to .1350.
        
    -   Windows 10 version 2004 and 20H2 — The revision number should exceed or be equal to .789.
        
    -   DirectX 12 (with Shader Model 6.6 atomics), or Vulkan (VK\_KHR\_shader\_atomic\_int64)
        
-   Apple Silicon M2 or newer.
    
-   Linux with a NVIDIA GeForce 2080 or newer.
    
-   Latest Graphics Drivers
    

For additional information about hardware and software specifications recommended by Epic Games, see [Hardware and Software Specifications](understanding-the-basics\installing-unreal-engine\hardware-software-specifications).

## Issues and Limitations

Virtual Shadow Maps are still actively being developed. There are a number of known issues and limitations to using them currently, and they are currently targeted at high-end desktops and next-generation consoles.

### Multiple Lights Performance

Performance in scenes with many small local lights is still a work in progress. For the time being, the best strategy is to [enable one pass projection](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) and be very careful with invalidations to keep as many of the pages cached as possible. Multiple local lights will perform far better with Nanite geometry than non-Nanite geometry, so aggressively culling or disabling shadow casting on non-Nanite geometry in the distance can help a lot. In some cases it may be desirable to disable dynamic shadow casting on distant lights entirely and rely solely on screen space [Contact Shadows](https://dev.epicgames.com/documentation/en-us/unreal-engine/contact-shadows-in-unreal-engine).

In the future, better controls will be available for making algorithmic and quality tradeoffs, as well as throttling updates in these situations.

### Low Poly Geometry

Low poly geometry with high curvature and smooth normals can exhibit artifacts. This is known as the "shadow terminator problem." It also occurs in ray tracing and other highly accurate visibility queries. The issue stems from the mismatch between the real low poly geometry and the "smooth" shading normals: in the area near the terminator some of these faces are geometrically in shadow, but the non-geometric shading normals are slightly facing the light. It is common to work around this artifact with a normal-based bias to the shadow lookup. This particular artifact can be more noticeable with Virtual Shadow Maps because by default they are set up to deliver highly detailed shadows from Nanite geometry.

The best way to address this is to increase the polygon count in these objects/regions. Limiting the divergence between the geometric and shading normals reduces or eliminates these artifacts without negatively impacting shadow quality elsewhere. With Nanite adding more polygons is straightforward and generally inexpensive. If the offending objects cannot use Nanite, adding a higher detail level of detail (LOD) often works well too, as these artifacts are mostly visible when objects are near the camera.

If it is not possible to add more geometry, the Virtual Shadow Map normal bias can be increased using `r.Shadow.Virtual.NormalBias` (default 0.5). Note that this should only be considered when content adjustments are not possible as it will negatively impact the quality of shadows throughout the scene, but particularly in areas of fine detail.

In the examples below, artifacts are visible on a low polygon sphere near the camera with high detail geometry in the background. Adding polygons to the sphere improves the artifacts without negatively affecting the detailed landscape in the background.

![Low Polygon Geometry with | default normal bias (0.5)](https://dev.epicgames.com/community/api/documentation/image/b8d43fa0-f69d-401d-9c18-1fb50c3bb108?resizing_type=fit&width=1920&height=1080)

![Higher Polygon Geometry with | default normal bias (0.5)](https://dev.epicgames.com/community/api/documentation/image/5b1f6d7f-c43c-4b0b-862c-d982253030f5?resizing_type=fit&width=1920&height=1080)

Low Polygon Geometry with | default normal bias (0.5)

Higher Polygon Geometry with | default normal bias (0.5)

Adjusting the bias also improves the artifacts, but fine detail is visibly lost in the background geometry.

![Low Polygon Geometry with | default normal bias (0.5)](https://dev.epicgames.com/community/api/documentation/image/6b258794-b99c-45c8-83a2-4d7843c20a3b?resizing_type=fit&width=1920&height=1080)

![Low Polygon Geometry with | increased normal bias (1.0)](https://dev.epicgames.com/community/api/documentation/image/7ac4716a-3aac-467c-9bc3-36d47b547d90?resizing_type=fit&width=1920&height=1080)

Low Polygon Geometry with | default normal bias (0.5)

Low Polygon Geometry with | increased normal bias (1.0)

### Virtual Reality

Virtual reality is not yet fully supported by Virtual Shadow Maps. There are likely to be artifacts with Directional Lights in the right eye.

### Split-screen

Split screen has received minimal testing and may have poor performance.

### Overflow of Physical Page Pool

With Virtual Shadow Maps, all of the shadow data in the scene for all lights is stored in a single large texture pool. The default pool size is affected by the **Shadow** Scalability setting, but it may need to be adjusted in scenes with many lights using high resolution shadows.

Alternatively it may need to be adjusted on lower-end hardware to save video memory.

The page pool size can be adjusted using `r.Shadow.Virtual.MaxPhysicalPages`. Enabling Virtual Shadow Map stats with `r.ShaderPrintEnable 1` and `r.Shadow.Virtual.ShowStats 2`, in succession, will display statistics about the current page pool use.

[![VSM physical pages stat](https://dev.epicgames.com/community/api/documentation/image/dde6c92d-b7e5-43e6-93de-ff96029704b3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dde6c92d-b7e5-43e6-93de-ff96029704b3?resizing_type=fit)

Example of current page pool use from Virtual Shadow Map on-screen stats.

If the number of **Pages** exceeds **Max Pages** corruption will occur, which sometimes manifests visually as a checkerboard pattern, or corrupt or missing shadows. If the shadow page pool overflows, a warning is displayed on screen and in the log.

[![max pages exceeded artifact](https://dev.epicgames.com/community/api/documentation/image/561bb943-b76c-4ef2-b1d9-a14c43535399?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/561bb943-b76c-4ef2-b1d9-a14c43535399?resizing_type=fit)

Example of corrupted virtual shadow maps from an exceeded number of pages in the page pool.

If this occurs, increase the size of the page pool or decrease the shadow resolution or number of virtual shadow map casting lights.

### Scene Capture

In some cases, Scene Capture components can cause the entire Virtual Shadow Map cache to be invalidated. The symptoms of this usually manifest as the *Invalidations* being low in the Virtual Shadow Map statistics, but the cached pages being also low (or sometimes even zero) and the Cached Page visualization being uniformly red.

If this happens, try hiding/removing any Scene Capture actors in the scene to verify if they are causing the issue.

There is currently no workaround other than disabling the Scene Capture when this occurs.

### Materials

Only simple subsurface materials are supported. Subsurface Profile and transmission are not yet implemented. If a material is using them, that material will be shadowed as though it is opaque.

### Shadow Resolution

Virtual Shadow Maps provide significantly increased resolution compared to conventional shadow maps, but shallow light angles (or projective aliasing) and very large local lights can exhaust the available virtual resolution. This may present itself as box-like shadows and bias issues depending on the geometry's surface.

Directional Light clipmaps are much less susceptible to running out of resolution, but very narrow camera fields-of-view can eventually exhaust those as well.

There is no simple solution to solving projective aliasing with shadow maps. Even with virtual shadow maps, some care must be taken to avoid the worst cases and balance resolution with performance.

### Map Check Warnings

Virtual Shadow Maps cause some inaccurate map check warnings to happen:

-   The **Lighting needs to be rebuilt** message does not appear when Virtual Shadow Maps is enabled, even though lighting may in fact need to be rebuilt when not using [Lumen Global Illumination and Reflections](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) features. While Stationary direct lighting is dynamic with Virtual Shadow Maps enabled, Stationary indirect lighting is still baked.
    
-   Warnings regarding **preshadows** can be ignored as they are not relevant when using Virtual Shadow Maps.