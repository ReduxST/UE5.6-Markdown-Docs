# Groom Scalability and Performance

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-scalability-and-performance-with-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-scalability-and-performance-with-unreal-engine)  
**Processed:** 2025-06-14 16:26:55

---

This page contains information on scalability and performance options you can use with grooms.

## Geometry Scalability

Strands geometry offers natural hair motion and looks, but it needs an allocated performance budget and is not supported on all platforms. When Strands geometry is not possible, grooms can rely on Groom cards (imported or generated with the Hair Card Generator plugin) and groom meshes. A given level of detail (LOD) can be set up to have both strands and card / meshes geometry, allowing graceful switching from one or the other depending on platform support and scalability settings.

You can find more information about what platforms grooms support on the [Groom Platforms Support](/documentation/en-us/unreal-engine/groom-platform-support-in-unreal-engine) page.

For more information on generating groom cards, see the [Hair Card Generator](/documentation/en-us/unreal-engine/hair-card-generator-for-grooms-in-unreal-engine) page.

## Strands Pipeline Overview

The following is an overview of the rendering pipeline for groom strands. This can help you adapt performance of Strands based on your project's budget and use case.

The rendering pipeline is decomposed into the following stages:

-   **Simulation:** The guides' motions are simulated based on the scene environment and groom component motion.
-   **Interpolation:** The guides' motions are transferred onto the rendering strands and applied surface skinning if a groom is bound to a skeletal mesh.
-   **Voxelization:** Hair curves are voxelized to generate a density volume. This volume is used for computing shadow and hair transmittance during the lighting stage. For light using Deep Shadow, a dedicated "deep" shadow map is generated at this stage.
-   **Primary Visibility:** The hair curves are rasterized for the current camera viewport, and hair samples are allocated for use with lighting.
-   **Lighting:** All hair samples are lit with shadow and transmission using voxel or deep shadow data.
-   **Composition:** All hair samples regroup and compose the final hair pixel into the scene color buffer.

## Strands Assets

The performance in a scene is impacted by the number of grooms being rendered. The grooms complexity, such as the numebr of **curves** and **points** they contain play a big part in overall performance. The more curves a groom has, the costlier the rendering passes for Simulation, Interpolation, Voxelization, and Primary Visibility.

-   **Curves / Points** can be decimated under the strands panel in the Groom Editor (or reimported).
-   The **Auto LOD bias** can help reduce the number of curves quicker as the groom occupies less pixels on screen.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1334445-e806-47cc-84be-27a60549e3c4/strand-assets.png)

## Interpolation

The interpolation steps run for a groom if it has any of the following:

-   **Simulation** enabled.
-   An attached groom with **Skinned** Binding.
-   has **RBF / Global Interpolation** enabled.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23a4afe4-d9ad-4a4d-b62f-1aeb48027cb7/interpolation-1.png)

When the groom binding is set to **Rigid** (and has no simulation or RBF), no interpolation will run and the curves will only be linearly transformed by the bone / skeletal mesh on which tey are attached to. This saves some cost.

By default, non-visible grooms casting shadow will be updated and voxelized in order to cast "up-to-date" shadows. The interpolation and voxelization of these non-visible grooms can be disabled with `r.HairStrands.Shadow.CastShadowWhenNonVisible` which will save some interpolation cost.

Using the console command `r.HairStrands.Shadow.CastShadowWhenNonVisible` could be a sensible option if the groom's shadow is barely noticeable.

## Shadowing

By default, all shadows cast by grooms are produced by their voxelization. This is because the hair voxel is needed for other purposes, such as Lumen occlusion and ambient occlusion, and this is a simple means to avoid redrawing hair geometry for each shadowed light.

The shadow quality is related to a few parameters:

-   **Voxel Size:** This defines the finest world size a voxel that can be reached. For the same view distance, as the voxel size increases, the shadow will look coarser, but the voxelization and the lighting will be cheaper. You can set this with the console command `r.HairStrands.Voxelization.VoxelSizeInPixel`. The default is 0.3.
-   **Voxel Size in Pixel:** This defines the effective size of the voxel in pixels. This means that the actual voxel size will grow as the groom is further away from the camera. This makes voxelization and lighting cheaper. You can control this with the console command `r.HairStrands.Voxelization.VoxelSizeInPixel`. This is enabled by default.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/679b89b6-0d8d-4974-b609-c40d3c46f3b1/shadows-1.png)

When computing shadows or transmittance, the vodel structure is traversed to estimate the occlusion / trnasmittance value. This is done by raymarching the voxel in **steps**. The spacing between each step can be increased for improving speed or decreased for improving quality

The larger the steps, the faster the traversing will be but the coarser the result will be as coarser Mips will be festched. Adjusting the step scaling affects the lighting cost up to a certain limit but degrades the shadow and hair transmittance quality. This is controlled by the console command `r.HairStrands.Voxelization.RayMarching.SteppingScale`. Variants of this variable exist for different parts of the lighting integration (shadow, environment, lighting, transmission, and so on).

When using Virtual Shadow Map, the number of samples per pixel can be increased with `r.Shadow.Virtual.SMRT.SamplesPerRayHair` to improve the noise at shadow boundaries. The default is 1 sample per pixel (ssp)

If the shadow cast by a groom is not necessary for most lights, the groom's voxelization can be disabled on the asset or the instance. Important lights can then be opt-in to cast **Deep Opacity Shadow**, which creates a per-light shadow map compatible with transmittance computation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c7032eb-8990-46d8-b7a1-5677e98df785/shadows-2.png)

## Rasterization

During the rasterization the console command `r.Shadow.Virtual.SMRT.SamplesPerRayHair` can be configured to balance performance over quality.

-   When using **Multi-Sample Anti-Aliasing** (MSAA) technique (default), the number of sub-pixel samples can vary from 1 to 8 (set to 4 by default).
-   You can opt-in for a **Per-Pixel Linked List** (PPLL) technique for larger sub-pixel count (up to 32), which allows finer transparency results. This technique stores a long list of samples per pixel.
    
    This option is very expensive and should only be used for linear media, and precomputed cinematics.
    

## Environment Lighting

For environment lighting, hair can use two techniques for trading quality over speed:

-   Fast single sample environment light evaluation (`r.HairStrands.SkyLighting.IntegrationType 2`). The resulting quality varies depending on how smooth the environment lighting is.
-   High qulaity BSDF integration using multiple samples. This leads to higher quality with higher performance costs (`r.HairStrands.SkyLighting.IntegrationType 1`). The number of samples is controlled with `r.HairStrands.SkyLighting.SampleCount` for trading noise.

Small scale occlusion is enabled with `r.HairStands.SkyLighting.ScreenTraceOcclusion` for accounting fine detail occlusion. For example, having a close up on eyelashes.

Often, ambient occlusion cast by hair is really soft and barely noticeable, but can have significant cost. You can disable this ambient occlusion with `r.HairStrands.SkyAO 0`

## Ray Tracing

Ray tracing geometry for hair strands is disabled by default. You can opt-in on a per-asset and per-instance basis. Ray-tracing groom geometry is costly for memory, and its updating costs is not negligble if the groom is animated (skinned or simulated). Ray tracing geometry should be used when needed, and on small groom parts where precise shadow casting matters most. For example, having strong directional light casting thin eyelashes shadows.

You can disable the use of all ray tracing geometry with `r.HairStrands.Raytracing 0`.