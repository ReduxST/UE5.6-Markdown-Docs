# Reflections Environment

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reflections-environment-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reflections-environment-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:16

---

Reflections are an important aspect of bringing environments to life by allowing light to ground objects in the scene. In real-time 3D, reflections start with how the [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials) are set up. Materials with low roughness values make surfaces more or less reflective. This can be the difference between creating a mirror-like surface or like brushed metal.

Unreal Engine provides several dedicated reflection systems to use for your projects. Some of these can be used in conjunction with one another or on their own, deprioritizing any other reflection methods. Choosing what types of reflections you enable for your project primarily comes down to the quality you want to achieve and the platforms you're targeting to release on. Some reflection systems may be too costly to performance, only supported on certain platforms, or may have hardware restrictions.

## Types of Reflections

When developing your project, you'll want to consider whether your project needs dynamic reflections, the level of quality it should achieve, and if the target platform you want to release on supports them or not.

For example, using a combination of static Reflection Captures with a dynamic Screen Space Reflections post process effect works well for most platforms and is fast to render but has rendering artifacts due to their nature. However, using Lumen Global Illumination and Reflections or Ray Tracing Reflections emulate light and reflections more accurately to ground objects in the scene, but comes at a higher rendering cost and is not supported on all platforms.

The available reflection systems support the following types of reflections and platforms:

| Reflection System | Type of Reflections | Supported Platforms |
| --- | --- | --- |
| **Lumen Reflections** | Dynamic | High-end Desktop PCs and Next-Gen Consoles |
| **Ray Tracing Reflections** | Dynamic | Desktop PC systems with Windows 10, DirectX 12, and a supported NVIDIA GPU |
| **Screen Space Reflections** | Dynamic | Desktop and Consoles |
| **Reflection Captures** | Static | All Platforms |
| **Planar Reflections** | Dynamic | All Platforms |

### Lumen Reflections

**Lumen Reflections** are part of the Lumen Global Illumination and Reflection system which uses either software or hardware-based ray tracing to generate reflections for the scene. Lumen uses a combination of methods to accurately represent the scene through screen traces when using software ray tracing mode. When hardware ray tracing mode is enabled, it will leverage the existing ray tracing architecture for reflections but requires a supported NVIDIA GPU to operate.

![Lumen Global Illumination and Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e759ff3-dbe8-4c89-8d94-4b3ed9f8dd5f/1-lumen-reflections.png)

![Screen Space Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72bca445-cc54-4210-96bf-30dabd2a7028/1-ssr.png)

For more information, see [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine).

### Ray Tracing Reflections

This feature of ray tracing is deprecated and may be removed in a future release.

Hardware **Ray Tracing Reflections** use ray-tracing techniques to emulate the way light works for accurate environment representation and supports multiple reflection bounces. Ray Tracing in Unreal Engine requires a supported NVIDIA GPU and Windows OS that supports DirectX 12.

![Screen Space Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3e21bba-0e7c-4746-91c9-d37d0c4c7d8f/rtr_ssronly.png)

![Ray Traced Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5af1c53a-caa1-4e14-92fa-80d0d710dab4/rtr_multiplebounces.png)

For more information, see [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine).

### Screen Space Reflections

**Screen Space Reflections** (SSR) are a dynamic post process effect that is limited to only reflecting what is visible on the screen. Objects off screen or occluded by objects on screen are not able to be represented in screen space reflections, which can cause rendering artifacts in the reflections.

![screen space reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec99daf4-9b6d-44bd-a2e2-4784d3b7431f/screen-space-reflections.png)

For more information, see [Screen Space Reflections](/documentation/en-us/unreal-engine/screen-space-reflections-in-unreal-engine).

### Reflection Capture Actors

**Reflection Capture** Actors are a low-cost, static capture of the area the reflection probe is placed. Many of these can be placed around the Level with no performance impact since they are calculated before runtime.

![sphere reflection capture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/653f452e-ba33-4cd4-b50b-07ef09c9d335/sphereshape.png)

There are two types of Reflection Captures to choose from: a **Box** and a **Sphere** shape. They work by capturing an image of the surrounding environment from their center and then mapping that to the reflection capture shape. Reflection Captures can overlap and blend with one another and are often placed with a large one to encompass an area and smaller ones for more defined static reflections on surfaces.

For more information, see [Reflection Capture Actors](/documentation/en-us/unreal-engine/reflections-captures-in-unreal-engine).

### Planar Reflections

**Planar Reflections** is an Actor that can be placed along surfaces to create accurate, dynamic reflections of the scene whereby it renders the level again from the direction of the reflection. This method of reflection can be costly, but provides accurate reflections and is supported on all platforms.

![Screen Space Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/911748b7-6651-4933-9556-cdf17608e936/planarreflections_disabled.png)

![Planar Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0cf2d5f-325b-4e1c-8550-bd4cee5e990a/planarreflections_enabled.png)

For more information, see [Planar Reflection](/documentation/en-us/unreal-engine/planar-reflections-in-unreal-engine).

## High Quality Reflections

Default reflection quality settings strike a good balance between performance and visual quality. However, for projects that are less concerned about performance and want to push quality of reflections even higher, you can use the **High Precision Normals** GBuffer to do so.

An important factor in achieving high quality reflections is how accurately the vertex normal and tangent can be represented. High density meshes may lead to adjacent vertices quantizing to the same vertex normal and tangent values, which leads to blocky jumps in normal orientation. Encoding the normals and tangents as 16 bits per channel enables developers to make the trade off between higher quality and how much additional memory is used encoding vertex buffers.

![GBuffer: Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80bfcc26-000d-434c-8666-13ae3ca7b717/sm_hp_vertex_normals_off.png)

![GBuffer: High Precision Normal On](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/452fabbb-4f22-48fd-b984-a8aabfe0d389/sm_hp_vertex_normals_on.png)

The following settings are required to enable High Precision Normals for reflections:

-   In the Project Settings under **Engine > Rendering > Optimizations** change the **GBuffer Format** to **High Precision Normals**.
    
    ![project setting high precision normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a30c3c1-d424-48e0-986c-10c2ec4c3b7e/project-settings-gbuffer-high-precision-normals.png)
-   Open any Static Mesh Asset and using the **Details** panel in the Static Mesh Editor, under **LOD 0 > Build Settings** enable **Use High Precision Tangent Basis**.
    
    ![static mesh high precision tangent basis setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0400d9fe-b149-451f-b5b3-e7ef0c36b8e6/static-mesh-high-precision-normals.png)