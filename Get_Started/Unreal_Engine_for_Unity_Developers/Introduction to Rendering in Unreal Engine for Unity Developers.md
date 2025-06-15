# Introduction to Rendering in Unreal Engine for Unity Developers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-rendering-in-unreal-engine-for-unity-developers](https://dev.epicgames.com/documentation/en-us/unreal-engine/introduction-to-rendering-in-unreal-engine-for-unity-developers)  
**Processed:** 2025-06-14 16:31:42

---

## Rendering in Unreal Engine

![Rendering in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ffc40f6-d1aa-406f-bef0-29a619dd9c78/ue5-lumen.png)

## Introduction to Rendering in Game Engines

Rendering refers to the process of generating a final image (frame) on the screen from a collection of objects in a scene.

The software used to render a frame is called a **render engine**, and these engines are typically categorized as:

-   **Offline rendering**: Designed for high-quality rendering that prioritize quality over processing time. They are typically used in applications where the rendering time is not important compared to the quality of the final rendered frame.
    
-   **Real-time rendering**: Designed with performance in mind and render frames quickly. Typical real-time frame rate targets are 30 (33ms), 60 (16ms), and 120 (8ms) frames per second (FPS), but actual frame rates can vary over time depending on a number of factors. Projects developed with real-time rendering must find a balance between performance and quality to maintain consistent frame rates. Real-time rendering engines are typically used for interactive media, such as video games, simulations, and architectural visualization.
    

**Unreal Engine** is a powerful suite of tools designed for real-time rendering to meet the needs of a variety of platforms from mobile to powerful desktop computers. Unreal Engine is capable of both high-quality real-time and offline rendering. You can use it to create anything, from interactive 2D and 3D experiences on mobile, console and desktop platforms, to rendering final frames for film and television productions.

Unlike other real-time engines on the market, Unreal Engine offers many proprietary features designed specifically with real-time and performance in mind. The goal is to reduce complexity in development and to get results quicker while maintaining high quality and performance.

Features, such as [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) system, [Nanite Virtualized Geometry](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine), and [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) are important steps in achieving this goal of removing complexity during development with features that “just work” for console and desktop applications. Mobile platforms support dynamic lighting and precomputed lighting workflows that require you to bake lighting into textures.

## Introduction to Rendering in Unreal Engine

Game engines perform a series of steps, often called a **Rendering Pipeline**, to render an image (or frame) to the screen. This section describes how Unreal Engine does this using its default deferred rendering path, and compares the steps to Unity’s deferred rendering path when appropriate.

The Unity Engine comes with three distinct render pipelines: Built-In, Universal, and High Definition. Each pipeline is designed for specific use cases and is typically selected before starting a new project.

Unreal Engine comes with a **unified rendering pipeline** that scales individual features based on the target platform - from handheld and mobile devices to the current generation of consoles and PCs. This means that you can choose a rendering path and supported features that best fits your project without being locked into a singular path.

Unreal Engine’s render pipeline can be used with its default **deferred rendering** path, or it can be configured to run in a [forward rendering](/documentation/en-us/unreal-engine/forward-shading-renderer-in-unreal-engine) path. In addition, you can enable the [mobile rendering](/documentation/en-us/unreal-engine/rendering-features-for-mobile-games-in-unreal-engine) path to accommodate lower-powered devices, including the [Vulkan Mobile Renderer](/documentation/en-us/unreal-engine/using-the-android-vulkan-mobile-renderer-in-unreal-engine). You can learn more about the rendering features supported for each rendering path by reading the [Supported Features by Rendering Path](/documentation/en-us/unreal-engine/supported-features-by-rendering-path-for-desktop-with-unreal-engine) documentation.

The image below shows a high-level visualization of the steps that Unreal Engine performs each frame to render a final image using the **deferred rendering** path:

![Unreal Engine’s deferred rendering pipeline](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fe924d0-9303-4fec-8b93-af43e2a317bc/ue-deferred-pipeline.png)

The process flows from left to right, and steps 2 to 5 happen in parallel.

Below, you will learn more about each of these steps in the rendering pipeline and what it takes to render each frame.

### Scene Preparation and Occlusion

![Occlusion culling in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/602962df-1bc1-4315-ba2d-b1bce429834b/ue-rendering-occlusion.png)

Unreal Engine has three primary threads - the Game (CPU), Draw, and GPU threads.

Before starting the rendering process, the **Game (or CPU)** thread gathers the transforms of all the objects in the scene. This includes processing all animations, physics simulations, and artificial intelligence (AI) before gathering the final transform for each object.

The transform information is then passed to the **Draw** thread on the CPU. The Draw thread runs the [culling process](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine), which builds a list of visible objects in the current camera view, and removes all other objects that are not visible to the camera. These objects don’t need to be drawn, and not rendering them improves performance.

This process performs the following steps (in order):

-   **Distance Culling**: Removes all objects that are farther than a specific distance from the camera.
-   **Frustum Culling**: Removes objects that are not visible inside the frustum (view) of the camera.
-   **Occlusion Culling**: Accurately checks the visibility state of all remaining objects in the scene. This method is costly and therefore done at the end of the occlusion process, where the remaining visible objects are further tested to see if they are occluded (hidden) by other objects.

The final list of visible objects is passed to the **GPU thread** to begin the rendering process.

#### Unity Equivalent

Unity performs **frustum** and **occlusion culling** during its rendering pipeline. In addition, it can perform distance culling with its **CullingGroup** API. A combination of these techniques creates the final list of visible objects in the scene.

### Geometry Rendering

![Nanite visualization in Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d8724e0-e967-465f-b99b-3008e4b64851/ue-rendering-drawcalls.png)

In this step, Unreal Engine goes through the list of visible objects in the scene and prepares them for the next step where it converts 3D vertex data into pixel data that is displayed on the screen.

#### Vertex Shaders

A shader is a bit of code that runs directly on the GPU and is used to perform a set of calculations. They are efficient and the GPU can run many shader calculations in parallel.

The vertex shader performs the following steps:

-   **Converts local vertex positions to world position**: Object vertex data is stored in local space, but once the object is placed in the world the vertex information must be converted to world space coordinates.
-   **Handles vertex shading and coloring**: The vertex shader handles vertex smoothing as well as any vertex color data in the object itself.
-   **Can apply additional offsets to vertex positions**: The vertex shader can offset the position of any vertex on the screen to achieve specific effects. This is done through the object’s material and is called world position offset.

#### Depth Pass

Before rendering individual objects, Unreal Engine performs a **depth pass**, or early Z pass, to determine the location of objects in relation to each other. This prevents a situation where Unreal Engine is rendering the same pixels on the screen multiple times. This is called **overdraw** and can have a significant performance impact. The engine attempts to avoid this as much as possible.

#### Draw Calls

After the depth pass, the GPU renders each object by drawing all polygons that share the same properties at the same time, such as meshes and materials. This is known as a **drawcall**.

All polygons of an object that are assigned the same material are counted as the same drawcall. However, each unique material requires its own separate drawcall. For example, each object on screen requires at minimum one draw call but could have more depending on the number of materials assigned to the object.

Unreal Engine’s [Nanite Virtualized Geometry](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) renders all polygons for all objects with a given material at the same time. Frame budgets are no longer constrained by polycounts, draw calls, or mesh memory usage.

#### Unity Equivalent

Unity’s rendering pipeline performs similar steps where it does a depth pass and uses drawcalls to draw the objects in the scene.

### Rasterization and the Geometry Buffer

![Images found in Unreal Engine’s Geometry Buffer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f536fb1-c663-4bf8-a6d5-a9ef5ec30b1e/ue-rendering-gbuffer.png)

The **rasterization process** converts 3D vertex data into 2D pixel data that is displayed on your screen. This process begins after the vertex shader is done processing all of its data.

Unreal Engine’s **Geometry Buffer (GBuffer)** includes a series of images that store information about the geometry in the scene. These images typically include things like lighting information for **base color**, **world normal**, **metallic**, **roughness**, and **specular** in the scene. These images in the GBuffer are composed to make up the final image you see on screen.

The process of converting these composed images happens for every frame that is rendered, and for each draw call where vertex data is converted to pixel data and draws the correct parts of the images to the GBuffer.

#### Unity Equivalent

Unity’s deferred rendering path also uses a GBuffer to store critical information about the scene. In Unity’s case, the GBuffer stores similar information about the scene (referenced with different names): albedo, specular, normal, and emissive / lighting information for the objects.

### Rendering Textures

![A scene rendered in unlit mode to show the materials](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cea8a9f3-e38f-435b-8cf0-7fa956fab92e/ue-rendering-textures.png)

Unreal Engine renders textures using [texture streaming](/documentation/en-us/unreal-engine/texture-streaming-overview-for-unreal-engine) to optimize loading textures into the scene. The texture streaming system uses texture **mipmaps**. These are a pre-calculated sequence of images of the same texture at different resolutions. You can think of this as **levels of detail (LODs)** for textures instead of meshes. The engine automatically creates these mipmaps where each image is half the resolution of the previous one.

Unreal Engine streams the texture’s mipmap during gameplay based on the distance from the camera. This is automatically done to optimize bandwidth and memory consumption, as well as reduce noise farther from the camera.

Texture sizes must be a power of 2 to receive mipmaps. Common texture sizes include 3840 x 2160 pixels (4K) and 1920 x 1080 pixels (HD). Note that textures are not required to have a specific ratio, a 1920 x 480 pixels texture will also receive mipmaps.

#### Unity Equivalent

Unity’s **Mipmap Streaming** system uses texture mipmaps to stream its textures at runtime. Similarly to Unreal Engine, this system streams the appropriate texture mipmap automatically based on the distance and angle to the camera.

### Pixel Shaders and Materials

![A Substrate material showing layering](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a59982a2-557c-4657-afa2-1e1dc5997612/ue-rendering-materials.png)

Once the objects have been fully rendered to the GBuffer, Unreal Engine begins shading each object on the screen by using each object’s material properties with the pixel shader.

A **pixel shader** performs a series of calculations to modify the color of a pixel on the screen. Pixel shaders run on the GPU and are extremely efficient. They drive Unreal Engine’s [material system](/documentation/en-us/unreal-engine/unreal-engine-materials) and are used when calculating lighting, fog, reflections, and post-process effects.

The material system uses High-Level Shader Language (HLSL) shader templates along with the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide) to create the final materials that are applied to the objects on the screen. These materials can use parameters, such as textures, to define the look of each object.

#### Unity Equivalent

Unity comes with several pre-built shaders (equivalent to materials in Unreal Engine) along with its **Shader Graph** to author shaders for your project. Unreal Engine’s Material Editor is the equivalent to Unity’s Shader Graph.

### Reflections

![Lumen reflexions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21f7ca4b-6eb0-4ed8-9f2e-114bb1c6983f/ue-rendering-reflections.png)

After shading all objects in the scene, Unreal Engine begins rendering the object reflections based on their material properties.

Unreal Engine uses four systems to render reflections to the scene. These systems are executed in the following order:

-   [Reflection Captures](/documentation/en-us/unreal-engine/reflections-captures-in-unreal-engine): Pre-calculated and stored in a static cubemap at a specific location.
-   [Planar Reflections](/documentation/en-us/unreal-engine/planar-reflections-in-unreal-engine): Captures reflections from and to a plane.
-   [Screen Space Reflections (SSR)](/documentation/en-us/unreal-engine/screen-space-reflections-in-unreal-engine): Uses available screen information to draw accurate reflections for objects in real time.
-   [Lumen Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine): solve reflections for the full range of roughness values in the scene. These reflections include support for the skylight, clear coat materials, translucency, and even single layer water materials.

Unreal Engine blends between the three methods, giving priority to Screen Space Reflections, then falling back to Planar Reflections, and lastly, falling back to Reflection Captures. The final reflection result is combined with the roughness, specular, and metallic images in the GBuffer.

If you are using [Lumen Global Illumination](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine), Lumen reflections will be used automatically. However, you can also use Lumen reflections without Lumen GI, in which case Unreal Engine will use baked lighting with Lumen reflections.

#### Unity Equivalent

Unity’s **Reflection Probes** provide similar functionality and are used to pre-compute reflection data for your scene.

### Static Lighting and Shadows

![A scene with precomputed lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f287d9e-17d7-46b5-af2c-a33d3e9ba6e3/ue-rendering-lightmass.png)

After reflections are rendered, Unreal Engine renders the static lighting and shadows for all objects in the scene.

Unreal Engine uses its [Lightmass Global Illumination](/documentation/en-us/unreal-engine/lightmass-basics-in-unreal-engine) system to pre-compute lighting information for the scene. The lighting and shadow information is stored in a [lightmap UV texture](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine) and this texture is blended with the object’s base color when rendering the object in the scene.

This system is very fast but it requires more memory and must be pre-calculated every time there is a change to the scene.

The Lightmass Global Illumination system is a good option for projects targeting mobile and low-powered devices.

#### Unity Equivalent

Unity’s **Progressive Lightmapper** and the **Enlighten Baked Global Illumination** systems provide similar functionality when pre-computing lighting for your scene.

### Dynamic Lighting and Shadows

![A scene dynamically lit with Lumen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efebd2b6-ba7b-48f5-b09c-f53b10651b4d/ue-rendering-lumen.png)

After static lighting is rendered, Unreal Engine renders dynamic (real-time) lighting and shadows with [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine), its dynamic global illumination system.

**Lumen** is a fully **dynamic global illumination** and **reflection** system that is designed for next-generation consoles and high-end PCs. The system uses multiple ray tracing methods to solve global illumination and reflections at scale.

Lumen provides infinite diffuse bounces and works seamlessly with [Nanite Virtualized Geometry](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine). In addition, the system works in conjunction with [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) to create high-resolution, real-time soft shadows.

Lumen provides **Lumen reflections** which solve reflections for the full range of roughness values in the scene. These reflections include support for the skylight, clear coat materials, translucency, and even single layer water materials.

Lumen replaces Screen Space Reflections when used in the scene.

#### Unity Equivalent

Unity uses **Enlighten Realtime Global Illumination** to provide dynamic lighting in the scene. This system provides real-time global illumination by using precomputed visibility information along with lightmaps to calculate indirect light bounce at runtime.

This differs from Lumen, as Lumen does not require any pre-computed data to provide indirect light bounces.

### Fog and Transparency

![A scene with volumetric fog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd3a2df1-a235-41ae-b08c-b4488e4013c2/ue-rendering-fog.png)

After rendering dynamic lighting and shadows, Unreal Engine renders fog and transparency effects next.

Unreal Engine renders **fog effects** with its [Exponential Height Fog](/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine) system, which renders fog density based on height and distance from the camera. In addition, the system can generate [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine).

Transparent objects use a [translucent material](/documentation/en-us/unreal-engine/using-transparency-in-unreal-engine-materials) and are rendered at this stage in the process. When using the deferred rendering path, Unreal Engine uses information available in the GBuffer to render transparency. Alternatively, you can configure the material to use the forward rendering path to produce a more accurate transparency effect.

#### Unity Equivalent

Unity supports **Linear**, **Exponential**, and **Exponential Squared** fog in the scene.

### Post Process Effects

![A scene with depth of field applied to the final image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2323c06c-e83b-4ebb-b535-2738dda4c311/ue-rendering-post-process.png)

Once fog and transparency are rendered, Unreal can apply additional effects over the image. These effects are called [Post Process effects](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine) because they are applied after the final image has been processed. The effects rely on the pixel shader and use the information available in the GBuffer.

Some common post process effects include light bloom, depth of field, light shafts, tonemapping, and motion blur.

As part of this post process step, Unreal Engine can apply [Temporal Super Resolution (TSR)](/documentation/en-us/unreal-engine/temporal-super-resolution-in-unreal-engine). TSR is a platform-agnostic [Temporal Upscaler](/documentation/en-us/unreal-engine/temporal-upscalers-in-unreal-engine) that Unreal Engine uses to render beautiful 4K images. Images come at a fraction of the cost by amortizing some of the costly rendering calculations across many frames.

In the rendering chain, Temporal Super Resolution happens after depth of field and everything that follows is upscaled, such as motion blur, bloom, and so on.

![A graphic showing when TSR is applied to the image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f3e8a94-d24a-4f4f-82f8-066ec484528d/ue-rendering-tsr.png)

Once these effects are applied to the GBuffer, Unreal Engine renders the final image to the screen.

The steps described above generate a **single frame** to the screen. These steps are often repeated between 30 to 60 times per second depending on the target framerate of the game.

#### Unity Equivalent

Unity comes with post process solutions based on the chosen render pipeline. Many of the available effects are similar to the ones available in Unreal Engine.

In addition, Unity 6 also comes with **Spatial-Temporal Post-processing (STP)**, a native software-based scaler that uses spatial and temporal upsampling techniques to produce a high-quality, anti-aliased image.

### Overview of Rendering Features in Unreal Engine

Now that you understand the steps Unreal Engine takes to render a frame to the screen, you are ready to learn more about specific rendering features that come with the engine.

Learn more about Unreal Engine’s rendering features by reading the [Lighting the Environment](/documentation/en-us/unreal-engine/lighting-the-environment-in-unreal-engine) documentation.