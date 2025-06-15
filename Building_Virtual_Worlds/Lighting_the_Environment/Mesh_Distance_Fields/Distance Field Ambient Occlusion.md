# Distance Field Ambient Occlusion

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:49

---

Shadowing for Movable Sky Lights is provided by using Signed Distance Field Volumes precomputed around each rigid mesh to generate medium scale Ambient Occlusion. In **Unreal Engine**, this is called **Distance Field Ambient Occlusion** (DFAO). It supports dynamic scene changes; the rigid meshes can be moved or hidden, and it will affect the occlusion. Unlike [Screen Space Ambient Occlusion](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine) (SSAO), occlusion is computed from world-space occluders, so there are no artifacts from missing data off-screen.

This dynamic AO solution will not work for all projects, as it has some invasive limitations which enable it to support dynamic scene changes. In particular, only slight-non-uniform scaling (squishing) is supported. Also, large Static Meshes produce inferior quality results because a small volume texture is mapped to every object.

## Scene Setup

This feature requires that **Generate Mesh Distance Fields** be enabled in your **Project Settings** in the **Rendering** section. See the [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#enablingdistancefields) page for more information.

To enable Distance Field Ambient Occlusion, drag a **Sky Light** into the scene and set its Mobility to **Movable**

For a step-by-step guide, follow the [Distance Field Ambient Occlusion](/documentation/en-us/unreal-engine/using-distance-field-ambient-occlusion-in-unreal-engine) How-To guide to learn more.

## Sky Light

The **Sky Light** component enables you to adjust the various settings that can be found listed under **Distance Field Ambient Occlusion**.

![Distance Field Ambient Occlusion Settings of the Sky Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/250e4b6e-8f8d-4418-8926-3f034e88f57c/01-dfao-sky-light-dfs-settings.png)

These are comparisons of some of the settings you can adjust:

### Occlusion Contrast

![Occlusion | Contrast: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f9b96fd-fa31-4113-bef2-fcd8e1149aea/02-dfao-contrast-0.png)

![Occlusion | Contrast: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/418eed97-31c0-4a2e-8dbb-0f01104aa221/03-dfao-contrast-1.png)

### Minimum Occlusion

![Min Occlusion: 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66ba5d19-5063-40d5-93a1-03494a0f89f9/04-dfao-min-occlusion-0.png)

![Min Occlusion: 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b18ba19-6c4d-4347-837e-a686e24186ac/05-dfao-min-occlusion-1.png)

### Occlusion Tint

![Occlusion Tint: | Black](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed47bc29-72a9-45ac-b1dd-b5d22cf49763/06-dfao-min-occlusion-tint-0.png)

![Occlusion Tint: | Red](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6648a1e-54ea-4fa1-bd9b-422977fe4938/07-dfao-min-occlusion-tint-1.png)

For additional information about Sky Light settings and additional examples, see the [Mesh Distance Fields Reference](/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine#skylight) page.

## Scene Representation

The view mode for Distance Field AO enables you to see how DFAO looks in the level without regards to any other lighting that is happening.

You can visualize the Distance Fields that represent your scene ambient occlusion by using the Level Viewport view mode for **Distance Fields Ambient Occlusion** by selecting **Show** > **Visualize** > **Distance Fields Ambient Occlusion**.

Click image for full size.

While in this view mode, the only [Sky Light setting](/documentation/en-us/unreal-engine/mesh-distance-fields-properties-in-unreal-engine#occlusionmaxdistance) that will have any effect is **Occlusion Max Distance**.

![Example of DFAO visualization mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef3bda2d-2ade-4559-8c8e-fac526808ffb/09-dfao-example-dfao-visualization-mode.png)

### Quality

Distance Field AO quality is determined by the resolution of the Mesh Distance Field it represents. Since AO is very soft shadowing, so even if the surfaces aren't represented properly, occlusion further from the surface will be accurate. It's often not noticeable with sky occlusion. However, make sure that the larger details of the mesh are well represented in the Mesh Distance Field for good results. Use the [Mesh Distance Field Visualization](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#scenerepresentation) to inspect the quality.

For additional information about Mesh Distance Field quality, see the [Mesh Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#quality) page.

## Occlusion Results

### Diffuse

Distance Field AO produces a bent normal (the direction of least occlusion) which is used to modify the diffuse sky light calculation (along with an occlusion factor).

![No Distance Field Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/945dd583-9d96-4e61-b34c-cdf91cbe4d54/10-dfao-default-1.png)

![Distance Field Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6fbe3e6-020a-42f3-bf88-e04f630cb76d/11-dfao-enabled-dfao.png)

In this example is a Fortnite level at midday. In Fortnite, players can knock down any wall, floor or ceiling and build new ones, so the lighting must be updated accordingly. Distance Field AO supports these types of dynamic changes in the level around you.

### Specular

Distance Field AO also provides approximate specular occlusion on Sky Lights. This is computed by intersecting the directional occlusion cone with the reflection cone (whose size depends on the material roughness).

![No Specular Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/137572a6-b2de-45a0-abca-e7298bd1815f/12-dfao-default-2.png)

![Specular Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4edbf9f4-9164-40b0-8d13-b40640a9917e/13-dfao-enabled-specular-occlusion.png)

*Specular occlusion on pipes.*

By default, non-directional AO is applied to specular. You can use **r.AOSpecularOcclusionMode** to give more accurate occlusion results than the default method by intersecting the reflection cone with the unoccluded cone produced by DFAO. Note that this can introduce DFAO sampling artifacts.

### Foliage

For Actors painted with the [Foliage Tool](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#foliagetoolsettings), you must first enable the option **Affect Distance Field Lighting** in tool settings.

![Enable the Affect Distance Field Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8675d4fc-417d-4a8a-aab7-eadf256d8454/14-dfao-foliage-tool-settings.png)

Even though Distance Field AO operates on surfaces, it can still handle foliage where many small leaves are combined into sheets. The best results are obtained by enabling **Two-Sided Distance Field Generation** for foliage type assets from the **Build Settings** options in the **Static Mesh Editor**. This will soften the computed occlusion.

In the Sky Light options, increase the **Min Occlusion** to prevent the interior parts of the asset from going fully black.

![Enable Two-Sided Distance Field Generation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ac09c8e-b7b1-4a6c-b7cc-5547790c13cf/15-dfao-two-sided-distance-field.png)

This is an example where DFAO has been enabled and is using Two-Sided Distance Field Generation:

![Screen Space Ambient Occlusion only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eefb168-7ebe-4152-a446-fb82b13e622e/16-dfao-disabled-dfao.png)

![Distance Field Ambient Occlusion on foliage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d6c30b4-48a7-4045-84bf-d9670d2531bd/17-dfao-enabled-dfao.png)

For Foliage assets that use LODs (Levels of Detail), you can run into some problem with Distance Field AO produces over-occlusion. This happens when the [Mesh Distance Field](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine) is still accurate at far distances, but the LOD level is using a lower triangle count and may shrink to be inside of the generated Mesh Distance Field.

To combat this, you can use **World Position Offset** on those LODs to pull the vertices outside of the Distance Field. Typically, a small offset towards the camera is effective enough to resolve the artifact. For billboards, use the Pixel Depth Offset feature to create valid depth values which better represent the original 3D triangle mesh. This technique was used in the "A Boy and His Kite" GDC demo, which relied on Distance Fields for the long view distances.

![No Pixel Depth Offset ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a1f6ee0-7d02-4a02-8ceb-6f3af26859cd/18-dfao-bilboard-no-pixel-depth-offset.png)

![Pixel Depth Offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4d9182e-502e-448f-830a-d663aeb73298/19-dfao-bilboard-with-pixel-depth-offset.png)

*Distance tree billboards showing over-occlusion. Use Pixel Depth Offset and the Skylight Min Occlusion to reduce over-occlusion.*

### Landscapes

Landscapes use a heightfield for their representation instead of a Mesh Distance Field. This uses an approximate cone intersection, which is computed against the heightfield enabling pixels without a Distance Field representation to receive occlusion. However, there is no self-shadowing or Distance Field shadowing. Instead, landscapes should use **Far Shadows** with Cascaded Shadow Maps (CSM) shadowing for far distances.

![Landscape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/552526b2-8f79-449a-ba74-78c5f327192c/20-dfao-landscape.png)

DFAO visualization view mode showing landscape occlusion.

## Performance

The cost of Distance Field AO is primarily GPU time and video memory. DFAO has been optimized such that it can run on medium-spec PC, PlayStation 4, and Xbox One. Currently, it has a much more reliable cost so that it's mostly constant (with a slight dependency on object-density).

In cases with a static camera and mostly flat surfaces, DFAO is 1.6x faster when compared to earlier implementations. In complex scenes with foliage and a fast moving camera, the latest optimizations are 5.5x faster. The cost of Distance Field AO on PlayStation 4 for a full game scene is around 3.7ms.

### Optimizations

Below are some of the optimizations that have been added to DFAO to make it faster, more efficient, and to improve its look.

#### General Improvements

The table below shows improvements for DFAO with test results using a PlayStation 4, as a result of improvements added with Unreal Engine 4.16:

| Optimization | Orignal Cost (ms) | New Cost (ms) | Savings (ms) |
| --- | --- | --- | --- |
| The culling algorithm has changed to produce a list of intersecting screen tiles for each object, instead of the other way around. Each tile/object intersection gets its cone tracing thread group, so wavefronts are much smaller and scheduled better. | 3.63 | 3.48 | 0.15 |
| Slow instructions in the inner loop have been replaced with fast approximations | 3.25 | 3.09 | 0.16 |
| The transform was moved out of the inner loop from world to local space (sample position constructed from local space position + direction). | 3.09 | 3.04 | 0.05 |
| Compute shader for ClearUAV. | 3.04 | 2.62 | 0.42 |

#### Smooth Sampling

Before using smooth sampling for DFAO, adaptive sampling was used which meant that flat surfaces did less work compared to denser scenes with many surfaces, like foliage. It also meant that there could be a lot of splotches in clean environments.

The smooth sampling requires a longer history filter, which can contribute to "ghosting" (or a trail behind a moving object), especially when shadow casters are moved. In Unreal Engine 4.16 and later, ghosting has been improved by having the Distance Field temporal filter store a confidence value. It is used to track leaking of occlusion during the upsample and then flush those leaked values through the history faster. Overall, this should help reduce ghosting that can happen when the camera or a dynamic object is moving fast.

In the examples below, AO computations are now fast enough to get rid of the adaptive sampling, so occlusion is much smoother.

![Adaptive Sampling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e94aede-6b08-4f10-a332-4e24974af239/21-dfao-scene-old-method.png)

![Smooth Sampling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc59aaea-afcc-4ce0-99a8-7289ac168f97/22-dfao-scene-new-method.png)

*Scene View*

![Adaptive Sampling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61962c93-4c00-4a68-a1f7-be018de5ad78/23-dfao-old-method-dfao-view-mode.png)

![Smooth Sampling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7b2e886-13f0-4241-b2fb-16ae726deab2/24-dfao-new-method-dfao-view-mode.png)

*DFAO Visualization*

#### Global Distance Fields

The Global Distance Field is a low-resolution Distance Field that uses Signed Distance Fields occlusion in your levels while following the camera. It creates a cache of the per-object Mesh Distance Fields and composites them into a few volume textures centered around the camera, called clipmaps. Only newly visible areas or those affected by the scene modification need to be updated, so composition doesn't cost much.

The clipmap is separated into four slices around the camera that are only updated where needed, which can happen when camera movement reveals a new slice or an object is never moved causing its influence bounds to become dirty. The average cost of maintaining it stays close to zero, however, in a worse-case scenario, the update cost could be higher when performing something like a teleport.

![Clipmap visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7558c42f-6967-48c3-8bf1-77f09191a8ce/25-dfao-clipmap-visualization.png)

Clipmap visualization of the texel size of the clipmaps with each clipmap being represented by a different color.

The lower resolution of the object Distance Field means that it can be used for everything, but when computing cone traces for sky occlusion, they are sampled near the point of being shaded while the Global Distance Field is sampled further away.

You can visualize the Global Distance Field in the viewport by clicking **Show > Visualize > Global Distance Field**.

Click image for full size.

Below is a comparison of the per-object Mesh Distance Field visualization in comparison to the Global Distance Field visualization that combines them into clipmaps based on the camera view and distance.

![Mesh Distance Fields Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6e2df4f-2a01-49e6-b574-d31dd17b7f73/16-distance-field-mdf-visualization.png)

![Global Distance Fields Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddd6a294-ed01-4029-bdb1-bc089b49ae9d/17-distance-field-gdf-visualization.png)

The Global Distance Field is a lower resolution than its object Distance Fields counterpart, making Global Distance Fields inaccurate near surfaces. When cone traces happen, the object Distance Field is used near the start of the occlusion cone and Global Distance Field for the rest of the trace, giving better results because you get accurate self-occlusion and efficient long distance traces. Because of this, sky occlusion sees five times the performance gain because the effective max object influence distance is dramatically decreased.

## Limitations

**Limitations of the technique**

-   Only Ambient Occlusion is provided, which is different from Sky Occlusion because it has a limited blocking distance.
-   Shadows only cast from rigid meshes. For Skeletal Meshes, use [Capsule Shadows](/documentation/en-us/unreal-engine/capsule-shadows-in-unreal-engine) for indirectly lit areas.

**Limitations of the current implementation (can be improved in the future)**

-   Updates to the AO from dynamic scene changes lag a bit as the work is spread across multiple frames causing occlusion to shift around a bit as new samples are generated. This has been improved in Unreal Engine 4.16 and later by having the Distance Field temporal filter store a confidence value which is used to track leaking of occlusion during the upsample and then flush those leaked values through the history faster. This helps reduce the ghosting that happens when the camera is moving.
-   Large objects will have diminished Distance Field resolution and cause inferior AO quality since a volume texture is mapped to each mesh.

For additional limitation of Distance Fields, see the [Distance Fields](/documentation/en-us/unreal-engine/mesh-distance-fields-in-unreal-engine#limitations) page.

## Tips and Tricks

### Cheap Bounce Light

By unchecking **Lower Hemisphere is Solid Color** on the Sky Light and painting in some ground color into the cubemap, you can get what looks like Sun bounce lighting for no further cost. This will cause light leaking indoors as it does not respect shadowing of the directional light, but can be effective for outdoor scenes.