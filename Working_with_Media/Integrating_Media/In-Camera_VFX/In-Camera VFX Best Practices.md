# In-Camera VFX Best Practices

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-best-practices-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-best-practices-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:38

---

There are a number of challenges associated with building an environment that will be used for an in-camera VFX shoot. The two main concerns are:

-   Building assets that appear realistic on an LED wall.
    
-   Optimizing the environment for performance so it runs in real time.
    

Mitigating these issues requires close collaboration between the Art team and the Stage team. Many effects that may appear to be performant and practical when running Unreal Engine in a workstation environment will not be effective for an LED wall, and proper communication between teams can avert many issues that result from that difference.

Use this page as a reference for these topics as you develop your projects for In-Camera VFX. This page is not exhaustive, nor is it intended to act as a strict set of rules. You should always carefully consider the requirements and limitations of your project when trying to determine how to best improve performance.

## Project Set Up

-   Ensure your project is set up properly for efficient workflows. Refer to the [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine) documentation for an example of our recommended project set up, then customize it as necessary for your project's requirements.
    
-   We recommend disabling the **Virtual Reality** and **Mixed Reality** plugins. This will reduce the resources required to run Unreal Engine, and, other than for [Virtual Scouting](/documentation/en-us/unreal-engine/virtual-scouting-in-unreal-engine) and [Live Link XR](/documentation/en-us/unreal-engine/livelinkxr-in-unreal-engine), they are of limited use for virtual production.
    
-   Ensure you define your **Project Structure** in the **Content Browser**. When producing multiple levels and environments it is strongly recommended you define a structure for Artists to use from the outset.
    
-   One suggested structure as used in the ICVFX Production Test is documented here:
    
    [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine)
    

## Performance Targets & Profiling

For real time applications of Unreal Engine, it's often the case that the in-editor performance is worse than in the shipping environment. However, for ICVFX purposes, your in-editor performance should be considerably better than your target framerate on stage.

nDisplay comes with additional performance costs due to the multiple views rendered in an ICVFX environment, and the additional steps taken during rendering to ensure sync. Likewise, hardware can vary from one stage to the next and on individual workstations building content, therefore these differences should be considered along with your performance target when authoring content.

For the [ICVFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine), assets were created on a Dual NVIDIA RTX 8000 and 128GB DDR5 RAM machine for an intended stage render node using Dual NVIDIA A6000s and 128GB DDR5 RAM.

To ensure sufficient performance, we targeted a frame rate between 48-72 frames-per-second (FPS) on Artist workstations when viewed in 4K full screen with the resolution scale in Windows set to 100%. This was used as a benchmark guideline. However, further testing was required on a target device off-stage. This device was running scenes in nDisplay with a viewport configuration that simulated the heaviest load anticipated for any on-stage device. Additionally, closer to production, the scenes were regularly tested on-stage using the anticipated hardware.

While the content of this page is focused on performance and profiling specifically for In-Camera VFX workflows, we recommend that you review the documentation for [Testing and Optimization](/documentation/en-us/unreal-engine/testing-and-optimizing-your-content) and specifically [Unreal Insights](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) for additional resources on improving performance in your project.

When preparing your scenes for the stage, consider the following:

-   While a 2-3x target frame rate approach can provide a rough guideline for Artists, do not assume it will be sufficient in all cases, as not all scenes scale the same. We strongly recommend you run performance tests on a regular basis and document the results. Performance is everyone's responsibility, and testing early and often means you're not surprised by bad performance when you're on set.
    
-   Always work towards a **target FPS** on content workstations that are comparable to the ICVFX stage render nodes.
    
    -   It may not always be possible for all Artist workstations to be comparable, however it is essential to have access to at least one workstation that is readily available for profiling.
        
    -   Scalability settings can be used to closely emulate the performance of the target hardware, however this is less accurate and should only be used as a rough guideline.
        
-   Conduct regular **performance profiling** on machines with the same specifications as those found on-stage, by running the scene in the same configuration as the most heavily tasked render node. This means a proper inner and outer frustum setup for a single node with the maximum resolution used on-stage.
    
-   When possible, work with the stage team to run performance tests on the stage itself. Don't leave testing until the last minute on a production or assume the stage team will optimize for performance.
    
-   Windows scaling can affect Engine performance:
    
    ![Windows scaling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61a10e2e-6fdd-4872-a036-9ad144f18d09/icvfx-windows-scaling.png)
-   Use [Unreal Insights](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) to generate nDisplay traces. Refer to this [live stream](https://www.youtube.com/watch?v=TygjPe9XHTw) for a full explanation of how to do so. GPU Profiling and CPU Profiling will also be helpful.
    

## Asset Creation and LODs

-   [Level of Detail](/documentation/en-us/unreal-engine/creating-and-using-lods-in-unreal-engine): Use different levels of polygon counts for when a Mesh is rendered larger or smaller on the screen. LODs are based on the screen size.
    
-   **Representations**:
    
    -   Use Hero representation for when an asset is extremely close to the camera.
        
    -   Use Proxy representation for when an asset is further from the screen and the texture and poly detail isn't needed. One method is to build the hero geometry with complex shading and high-resolution textures, and then use a DCC app or the Proxy Mesh tool to create lower-resolution geometry and bake down the textures using a simplified shader.
        
    -   If an asset needs to be both near and far from the camera at different points during the shoot, then use Levels of Detail (LODs) for flexibility.
        
    -   Proxy meshes can be generated in-Editor for individual or clusters of background assets. Refer to the [Proxy Geometry Overview](/documentation/en-us/unreal-engine/proxy-geometry-tool-overview-in-unreal-engine) documentation for more information.
        
    -   Local clusters of the same Actor that share materials can be merged together with **Merge Actors**.
        
        -   If a local cluster of Actors use different meshes and materials, you can use Merge Actors to merge the materials into a shared material asset that atlases the various textures to reduce draw calls. This is most useful for optimizing medium-distance assets as the atlasing can reduce the quality resulting in potentially smaller texture sizes. They can be used closer to the camera on a case-by-case basis when the drop in quality is not too noticeable.
            
        -   You can use LODs and other performance-improving techniques with merged Actors.
            
-   Object culling can be an issue for performance. Large objects won't cull as easily, resulting in an impact on performance. This is less notable for static scenes, but if the LED volume moves throughout the environment then the culling of Large objects will be more important to consider. Due to this behavior, when merging meshes, don't merge too many Actors together, as creating large meshes will impact the ability to cull the merged mesh.
    
-   [Automatic LODs](/documentation/en-us/unreal-engine/static-mesh-automatic-lod-generation-in-unreal-engine) can produce assets with a softer, indistinct look. We recommend you budget resources for some hand-crafted LODs.
    
    You only need hand-authored LODs for level 1 and possibly level 2, as anything beyond that will be rendered too small on the screen for the details to be noticeable.
    
-   When possible, aim to get optimized versions approved by the Art Director, the Production Designer, or whoever else is signing off on the look, otherwise optimization may introduce noticeable visual differences and increase the budget and schedule of your project.
    
-   Optimize as you work, don't leave this process until the end, it will help receive and maintain Art Director approval if the project is always optimized, and will free additional system resources that can be used elsewhere for higher-quality or dynamic effects, such as volumetric fog or dynamic lighting.
    
    -   Additionally, we recommend to always turn on all the high-quality and dynamic features you intend to use from the beginning, so you will have a consistent idea of what the performance costs are, how much remaining capacity you have to work with, and if you will need to adjust their quality using cvars.
-   Quad Overdraw can greatly increase performance cost. To minimize this impact, consider the following issues and optimizations:
    
    -   Avoid using too much translucency, especially large translucent areas. Instead, we recommend using a Masked Material, due to the lower performance cost.
        
    -   Avoid dense meshes. Models should be built for their appropriate screen size. Solid meshes in wire frame mode, or nearing a solid color might result in poor performance.
        
    -   Normal maps should only be used for details. Do not use Normal maps for geometry.
        
    -   Use the **Quad Overdraw** viewport mode to profile the scene. Any meshes rendered Green or worse should be avoided to keep Quad Overdraw costs down. The majority of the screen should be rendered a shade of blue.
        
    -   It's important to understand how much of your mesh will render visible on the screen. In our experience, many teams don't properly consider how geometry will be used. For example, If a mountain only fills 100px x 100px on an LED wall, then that mountain doesn't need to consist of 2 million triangles.
        
    -   The same optimization practices apply for textures. The GPU might not load an 8k texture until it's in the camera's direct view.
        
-   Reuse assets so the engine can instance them. Avoid using too many unique meshes, as this is less performant. Use the **Statistics** window to identify how many unique or rarely reused assets are in the scene. If you see a lot of 1's or 2's in the **HWInstance** column, then this should be addressed. There are some exceptions to this, as merging Actors or creating a proxy mesh will create a new unique Actor.
    
-   Reduce the number of Material IDs on a mesh as much as possible. Try to keep it at 1 material per asset. You can use the Merge Actors tool for this purpose. Each material ID adds draw calls, so to lower the cost of performance you want to keep draw calls to a minimum. Ideally, assets are prepped with the correct number of Material IDs on import.
    
-   Use [Material Functions](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine) to group common features together to have maintainable materials without bloating.
    
-   Use [Material Parameter Collections](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine) to simplify setting up materials.
    
-   Use master Materials when possible for easier mass changes. However, remember that master Materials with many switches will increase shader permutations, which will increase shader compile times. There's a balance between maintainability and compile times. Be mindful of any last-minute master material changes while on set, as a lot of materials may need to be recompiled.
    
-   Use more complex shading for assets closer to the camera. Use simpler shading for assets further away from the camera. Use static switches to avoid multiple master materials for different quality levels, and implement them using LODs. Then, instead of using a lot of complex nodes to compute an effect in a material when it is far away (being rendered small on the screen), we recommend you bake the output down to a texture to reduce the shader complexity, that is, the instruction count. You can refer to this live stream video on [Baking Materials to Textures](https://youtu.be/WaM_owaUpbE&sa=D&source=editors&ust=1633124927652000&usg=AOvVaw2VeZdLzVhs5UKFm6dUKB1L) for more information.
    
-   High-resolution assets of 4k or 8k are almost always going to be a poor choice for both visuals and performance. When working with assets in real-time production, more is not always better. In most scenarios it will not be needed, and it consumes memory that can be used by other scene elements. Refer to the documentation on [Level of Detail Texture Properties](/documentation/en-us/unreal-engine/replicate-actor-properties-in-unreal-engine) and how to use [mipmapping with image sequences](/documentation/en-us/unreal-engine/image-sequence-mipmapping-in-unreal-engine) for more information.
    
-   For mipmapping and streaming reasons, textures need to be a power of 2 in both dimensions, however, they don't have to be perfect squares. They can be rectangular as long as both vertical and horizontal resolutions are a power of 2 respectively. For example, textures of 128x256 and 256x256 will function as intended, 8080x8080 will not.
    
-   Are you using decals? If not, disable **Deferred Decals** in the **Project Settings**.
    
-   Don't use video elements, use [Flipbooks](/documentation/en-us/unreal-engine/paper-2d-flipbooks-in-unreal-engine) instead.
    
    -   With ICVFX, you want to ensure that all the nodes rendering on the wall are synced. Due to how video elements are encoded, there is no method to properly synchronize them, to ensure that each machine is pointing to the same 'frame' of the video.
        
    -   Using a texture Flipbook animated through a material parameter, or an EXR sequence being driven by a level sequence that is being played at the same time, are both good methods to have a synchronized animated sequence.
        

## Lighting and Rendering

-   **Efficient lighting:** Avoid ray tracing or over-use of dynamic lights, as these forms of [Lighting](/documentation/en-us/unreal-engine/lighting-the-environment-in-unreal-engine) are expensive. Use more efficient alternatives such as light baking and other lower-performance-cost tools. When used with caution, dynamic lighting is a useful tool, but it should be applied sparingly.
    
    -   If dynamic lighting is needed, consider disabling **Cast Shadows** to reduce performance impact.
        
    -   Try to avoid relying on [Light Functions](/documentation/en-us/unreal-engine/using-light-functions-in-unreal-engine) and [Rect Lights](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine), both of which are expensive compared to cheaper techniques such as [IES profiles](/documentation/en-us/unreal-engine/using-ies-light-profiles-in-unreal-engine) and [Spot Lights](/documentation/en-us/unreal-engine/spot-lights-in-unreal-engine).
        
    -   Consider setting up [Precomputed Lighting Scenarios](/documentation/en-us/unreal-engine/using-precomputed-lighting-scenarios-in-unreal-engine) to allow for quick switching between different settings while on-set.
        
-   **nDisplay costs:** When setting up a complex scene, always keep in mind that using nDisplay adds an additional performance cost that exceeds the baseline costs for the scene itself. This can be a source of performance differences between a scene rendered in Unreal Engine on a workstation and a scene rendered on the LED walls for in-camera VFX shoots.
    
-   [Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) is not [Path Tracing](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine). We sometimes encounter confusion about what ray tracing means in the context of real-time rendering in Unreal Engine. Because ray tracing is expensive in terms of performance, you can achieve better-looking and more stable image quality using baked lighting with volumetric light maps and reflection probes.
    
    -   While ray tracing is required for GPU Lightmass to work, it does not require the additional ray tracing features that are enabled by default, such as ray-traced shadows, ambient occlusion, global illumination, and reflections. Instead, it's best to disable all of these features using the following console command:
        
        ```
              `r.RayTracing.ForceAllRayTracingEffects 0`
        Copy full snippet
        ```
        r.RayTracing.ForceAllRayTracingEffects 0
        
        Refer to the main [GPU Lightmass Global Illumination](/documentation/en-us/unreal-engine/gpu-lightmass-global-illumination-in-unreal-engine) documentation for more information.
        
    -   It is possible to use other ray-tracing effects carefully, if your set up is powerful enough to handle them. For example, the [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine) made use of ray-traced shadows and ray-traced reflections.
        
    -   When ray tracing is a requirement for your project, we recommend going through all master materials and optimizing them for the ray-traced scene using the `RayTracingQualitySwitch`. Additionally, we recommend reviewing all the ray tracing settings, such as samples, ray distance, bounces, and so on. Refer to the general [Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) documentation for more information.
        
-   The **Cinematic** **Engine Scalability** quality setting is usually not needed, instead we recommend lowering all the quality settings so they are almost visually identical to cinematic, as this can save a significant amount of performance in your scenes.
    
    Cinematic Engine Scalability automatically determines the values of a number of other settings, so you will have to set some of those manually when you use a lower setting.
    
-   At the start of a new project, go through all the [Rendering](/documentation/en-us/unreal-engine/designing-visuals-rendering-and-graphics-with-unreal-engine) settings in the **Project Settings** and enable or disable anything you require for the project. This will recompile all shaders, however, after setting up the [Derived Data Cache](/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine) you will not experience many issues with recompiling shaders.
    
-   Sometimes customers have raised concerns about baked lighting because they want to be able to change things quickly, so it is important to highlight the value of how to properly use both baked *and* dynamic lighting.
    
    -   When using baked lighting, we recommend you keep your lightmap resolutions sensible. They don't need to be set to a 4096p resolution.
-   If you're not using baked lighting, then disable **Allow Static Lighting** in the **Project Settings**.
    
-   [Volumetric Clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine) and lighting effects are expensive. Be careful when relying on them. Consider baking volumetric clouds after the desired look is achieved.
    
-   [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine) is expensive for performance, therefore, we recommend you consider regular fog or shader tricks instead. If Volumetric Fog is needed, we recommend adjusting the quality. To optimize Volumetric Fog use the following CVars:
    
    | CVar Command | Description |
    | --- | --- |
    | r.VolumetricFog.GridPixelSize 8 | 8 is the default value, increase this for better performance, for example to 16. Be careful changing these values, as it can cause artifacts. |
    | r.VolumetricFog.GridSizeZ 128 | 128 is the default value, decrease this for better performance, for example to 64. Be careful changing these values, as it can cause artifacts. |
    
-   **Lightmaps (CPU & GPU)**: Set up proper lightmaps. Refer to the [Unwrapping UVs for Lightmaps](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine) documentation for more information.
    
    -   Use caution when using lightmaps with large meshes, as the lightmap density will be diluted.
        
    -   Complex meshes are difficult for the lightmap auto-generation algorithm to evaluate efficiently. Your resulting lightmap might have tiny UV triangles that don't receive any baked lighting info. Consider using manually generated lightmaps in such instances.
        
-   [Overlapping Dynamic Lights](/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine): Be mindful of your light's radius and fall off, tweak these settings to reduce overlap and consider disabling **Cast Shadows** for small meshes. Overlaps can be previewed with the **Light Complexity** viewmode.
    
-   [Dynamic Shadows](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine): If dynamic shadows are required for your project, then ensure a balance between performance and visual quality. There are several methods to improve performance with only a minimal visual impact on quality.
    
    -   Simplify shadows for complex meshes using [Proxy Geometry Shadows](/documentation/en-us/unreal-engine/proxy-geometry-shadows-in-unreal-engine).
        
    -   When using **Cascade Shadow Maps (CSM)**, you can reduce the **Dynamic Shadow Distance** and **Num Dynamic Cascade Shadows** settings for better performance.
        
    -   Consider switching to **Distance Field** (DF) shadows or **Far Shadow Cascade** shadows. Because DF shadows are static, and Far Cascade shadows are only used for specific Actors, both are more performant than dynamic shadows.
        
    -   You can tweak the settings of several additional console commands to improve performance.
        
        -   `r.ShadowQuality`
        -   `r.Shadow.MaxResolution`
        -   `r.Shadow.RadiusThreshold`
        -   `r.Shadow.DistanceScale`
        -   `r.Shadow.CSM.TransitionScale` Refer to the [Scalability Reference](/documentation/en-us/unreal-engine/scalability-reference-for-unreal-engine) documentation for more information on how to use these commands.

## On Stage

-   Have a 3D representation of the stage in the level, and ensure it is an empty flat ground plane. The stage area needs to be void of any CG assets, this includes grass or foliage, and be mindful of moving assets through the scene or particle emitters entering the volume. Having the stage is useful for development and level design so you can accurately build around the stage area. .
    
    -   In theory, the LED wall volume shouldn't have any 3D assets for the shoot. In practice, you can have 3D assets inside the LED wall volume when shooting, but if that is the case then the practical floor or ceiling can't be in the frame as this will reveal that elements are at different depths. Carefully consider if you can make 3D assets on the stage work for your shoot.
-   Build dynamic controls using the [Web Remote Control](/documentation/en-us/unreal-engine/remote-control-for-unreal-engine) feature or into a Blueprint that can be controlled using a device such as an iPad or Tablet while on set.
    
-   Direct sun lighting is difficult to emulate on a stage, therefore we recommend you consider placing the stage in some kind of shaded space if outdoors.
    
-   Take into account the camera location and distance on stage. You don't need to render everything at cinematic quality, just what the camera view can see.
    
-   Consider whether the scene is a static set extension, or if you plan to include dynamic content for movement or animation in the background. A dynamic background is more expensive to render in high quality in real time.