# Rendering

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:46:58

---

## Rendering

### Mobile

| **Section** | **Description** |
| --- | --- |
| **Disable Vertex Fogging in Mobile Shaders** | 
If enabled, vertex fog will be omitted from most of the mobile base pass shaders.

Instead, fog will be applied in a separate pass and only when the scene has a fog component.



 |
| **Maximum Number of CSM Cascades to Render** | The maximum number of cascades with which to render dynamic directional light shadows when using the mobile renderer. |
| **Mobile Anti-Aliasing Method** | 

The mobile default anti-aliasing method.

You can choose from the following options:

-   **None**
-   **Fast Approximate Anti-Aliasing (FXAA)**
-   **Temporal Anti-Aliasing (TAA)**
-   **Multisample Anti-Aliasing (MSAA)**



 |
| **Mobile Float Precision Mode** | 

Project-wide mobile float precision mode for shaders and materials.

Changing this setting requires restarting the editor.

You can choose from the following options:

-   **Use Half-Precision:** Half-precision, except explicit float in `.ush` / `.usf`.
-   **Use Full-Precision for MaterialExpressions Only:** Half-precision, except full-precision for material floats and explicit floats in `.ush` / `.usf`.
-   **Use Full-Precision for Every Float:** All the floats are full-precision.



 |
| **Allow Dithered LOD Transition** | 

Defines whether to support **Dithered LOD Transition** material option on mobile platforms.

Enabling this may degrade performance because rendering will not benefit from Early Z optimization.



 |
| **Enable Virtual Texture Support on Mobile** | 

Defines whether to support virtual textures on mobile.

Requires general virtual texturing to be enabled as well.

Changing this setting requires restarting the editor.



 |
| **Mobile Reflection Capture Compression** | 

Defines whether to use the Reflection Capture Compression for mobile.

It will use ETC2 format to do the compression.



 |
| **Support Movable Light CSM Shader Culling** | 

Primitives lit by a movable directional light will render with the CSM shader only when determined to be within CSM range.

Changing this setting requires restarting the editor.



 |
| **Mobile Ambient Occlusion** | 

Enabling the mobile ambient occlusion.

An extra sampler will be occupied in the mobile Base Pass pixel shader after enabling the mobile ambient occlusion.

Changing this setting requires restarting the editor.



 |
| **Planar Reflection Mode** | 

Planar Reflections on Mobile work differently depending on the selected mode. Choose a mode that best fits your mobile project.

Changing this setting requires restarting the editor.

You can choose from the following options:

-   **Usual:** The Planar Reflection Actor works as usual on all platforms.
-   **MobilePPR Exclusive:** The Planar Reflection Actor is only used for mobile pixel projection reflections, it will not affect PC and Console platforms. MobileMSAA will be disabled when using this mode.
-   **MobilePPR:** The Planar Reflection Actor works as usual on PC and Console platforms and is used for mobile pixel projected reflection on Mobile platforms. MobileMSAA will be disabled when using this mode.



 |
| **Supports Desktop Gen4 TAA on Mobile** | 

Defines whether to support desktop Gen4 TAA with mobile rendering.

Changing this setting requires restarting the editor.



 |

### Materials

| **Section** | **Description** |
| --- | --- |
| **Game Discards Unused Material Quality Levels** | 
When running in game mode, defines whether to keep shaders for all quality levels in memory, or only those needed for the current quality level.

If this option is disabled, the engine will keep all the quality levels in memory, allowing a runtime quality level change. This is the default behavior.

If this option is enabled, the engine will discard unused quality levels when loading content for the game, saving some memory.



 |
| **Shader Compression Format** | 

Select how the shaders are compressed for storage.

You can choose from the following options:

-   **Do not compress**
-   **LZ4**
-   **Oodle**
-   **ZLib**



 |
| **Clear Coat Enable Second Normal** | 

Use a separate normal map for the bottom layer of a clear coat material.

This is a higher quality feature that is expensive in terms of performance.



 |
| **Enable Rough Diffuse Material** | Enables the Material's diffuse component to be affected according to the roughness input set on the Material's root node. |
| **Enable Energy Conservation on Material** | 

When enabled, materials reduce the loss of energy (light) in the specular lobe of metals and glass materials. This feature is only implemented with the Path Tracer.

Changing this property requires restarting the editor.



 |

### Culling

| **Section** | **Description** |
| --- | --- |
| **Occlusion Culling** | If this option is enabled, occluded meshes will be culled and not rendered. |
| **Min Screen Radius for Lights** | 
The minimum screen radius (in centimeters) of a light that will cause lights to be culled from rendering.

Using larger radius sizes will improve performance by culling more lights but causes them to quickly disappear when they only affect a small area of the screen.



 |
| **Min Screen Radius for Early Z Pass** | 

The minimum screen radius (in centimeters) that will cause Actors to be culled from rendering using a depth check.

Using larger values can improve performance by culling objects occluded by larger objects. However, using values which are too large will also remove large objects that were occluding ones behind it, in turn causing more objects to be rendered than expected.



 |
| **Min Screen Radius for Cascaded Shadow Maps** | 

The minimum screen radius (in centimeters) that objects are culled from being rendered in Cascaded Shadow Map Depth Passes.

Using larger values improves performance by rendering fewer Actors into the Shadow Map but causes Actors that meet the minimum screen radius to stop casting shadows.



 |
| **Warn About No Precomputed Visibility** | 

Displays a warning when no precomputed visibility data is available for the current camera location.

This can be helpful if you are making a game that relies on precomputed visibility (for example, a first-person mobile game).



 |

### Textures

| **Section** | **Description** |
| --- | --- |
| **Texture Streaming** | 
When enabled, textures will stream in based on what is visible on screen.

The texture streamer increases and decreases the resolution of visible textures, allowing for visual quality where it matters while managing available memory more efficiently.



 |
| **Use DXT5 Normal Maps** | 

Defines whether to use DXT5 for normal maps. If disabled, BC5 will be used, which is not supported on all hardware.

Changing this setting requires restarting the editor.



 |

### Virtual Textures

| **Section** | **Description** |
| --- | --- |
| **Enable Virtual Texture Support** | 
When enabled, textures can be streamed using the virtual texture system.

Changing this setting requires restarting the editor.



 |
| **Enable Virtual Texture on Texture Import** | 

Set the **Virtual Texture Streaming** setting for imported textures based on "Auto Virtual Texturing Size" in the texture import settings.



 |
| **Enable Virtual Texture Lightmaps** | 

When enabled, Lightmaps will be streamed using the virtual texture system.

Changing this setting requires restarting the editor.



 |
| **Enable Virtual Texture Anisotropic Filtering** | 

When enabled, virtual textures will use anisotropic filtering.

This adds a cost to all shaders using virtual textures.

Changing this setting requires restarting the editor.



 |
| **Tile Size** | 

Size in pixels for virtual texture tiles, will be rounded to the next power-of-2.

Changing this setting requires restarting the editor.



 |
| **Tile Border Size** | 

Size in pixels for virtual texture tile borders, will be rounded to the next power-of-2.

Larger borders allow higher degree of anisotropic filtering, but use more disk / cache memory.

Changing this setting requires restarting the editor.



 |
| **Feedback Resolution Factor** | Lower factor will increase virtual texture feedback resolution which increases CPU / GPU overhead, but may decrease streaming latency, especially if materials use many virtual textures. |

### Working Color Space

| **Section** | **Description** |
| --- | --- |
| **Working Color Space** | 
Choose from a list of provided working color spaces, or **Custom** to provide user-defined space:

-   **sRGB / Rec709**
-   **Rec2020**
-   **ACES AP0**
-   **ACES AP1 / ACEScg**
-   **P3DCI**
-   **P3D65**
-   **Custom**



 |
| **Red Chromaticity Coordinate** | Working color space red chromaticity coordinates. |
| **Green Chromaticity Coordinate** | Working color space green chromaticity coordinates. |
| **Blue Chromaticity Coordinate** | Working color space blue chromaticity coordinates. |
| **White Chromaticity Coordinate** | Working color space white chromaticity coordinates. |

### Global Illumination

| **Section** | **Description** |
| --- | --- |
| **Dynamic Global Illumination Method** | 
Sets the method for dynamic Global Illumination.

You can choose from the following options:

-   **None:** No dynamic Global Illumination method will be used. Global Illumination can still be baked into Lightmaps.
-   **Lumen:** Use Lumen Global Illumination for all lights, emissive materials casting light and SkyLight Occlusion. Requires the **Generate Mesh Distance Fields** to be enabled for Software Ray Tracing, and the **Support Hardware Ray Tracing** to be enabled for Hardware Ray Tracing.
-   **Screen Space (Beta):** Standalone Screen Space Global Illumination. Low cost, but limited by screen space information.
-   **Standalone Ray Traced (Deprecated):** Standalone Ray Traced Global Illumination technique. Deprecated, use Lumen Global Illumination instead.
-   **Plugin:** Use a plugin for Global Illumination.



 |

### Reflections

| **Section** | **Description** |
| --- | --- |
| **Reflection Method** | 
Reflection method.

You can choose from the following options:

-   **None:** No global reflection method will be used. Reflections can still come from Reflection Captures, Planar Reflections or a Skylight placed in the level.
-   **Lumen:** Use Lumen Reflections, which supports Screen / Software / Hardware Ray Tracing together and integrates with Lumen Global Illumination for rough reflections and Global Illumination seen in reflections.
-   **Screen Space:** Standalone Screen Space Reflections. Low cost, but limited by screen space information.
-   **Standalone Ray Traced (Deprecated):** Standalone Ray Traced Reflections technique. Deprecated, use Lumen Reflections instead.
-   **Plugin:** Use a plugin for Global Illumination.



 |
| **Reflection Capture Resolution** | 

The cubemap resolution for all reflection capture probes.

Must be a power of 2 number.

Very high values might have a severe impact on memory and performance.



 |
| **Reduce Lightmap Mixing on Smooth Surfaces** | 

Defines whether to reduce Lightmap mixing with reflection captures for very smooth surfaces.

This is useful to make sure reflection captures match Screen Space Reflections (SSR) or Planar Reflections in brightness.



 |
| **Support Global Clip Plane for Planar Reflections** | 

Defines whether to support the global clip plane needed for planar reflections.

Enabling this increases Base Pass triangle cost by ~12% regardless of whether planar reflections are active.

Changing this setting requires restarting the editor.



 |

### Lumen

| **Section** | **Description** |
| --- | --- |
| **Use Hardware Ray Tracing When Available** | 
Uses Hardware Ray Tracing for Lumen features, when supported by the video card, RHI, and Operating System.

Lumen will fall back to Software Ray Tracing otherwise.

Hardware Ray Tracing has significant scene update costs for scenes with more than 100,000 instances.



 |
| **Ray Lighting Mode** | 

Controls how Lumen Reflections rays are lit when Lumen is using Hardware Ray Tracing.

By default, Lumen uses the Surface Cache for best performance, but this can be set to **Hit Lighting** for higher quality.



 |
| **Software Ray Tracing Mode** | 

Controls which tracing method Lumen uses when using Software Ray Tracing.

You can choose from the following options:

-   **Detail Tracing:** When using Software Ray Tracing, Lumen will trace against individual meshes' Distance Fields for highest quality. Cost can be high in scenes with many overlapping instances.
-   **Global Tracing:** When using Software Ray Tracing, Lumen will trace against the Global Distance Field for fastest traces.



 |

### Shadows

| **Section** | **Description** |
| --- | --- |
| **Shadow Map Method** | 
Selects the primary shadow mapping method. Automatically uses **Shadow Maps** when Forward Shading is enabled for the project as Virtual Shadow Maps are not supported.

You can choose from the following options:

-   **Shadow Maps:** Renders geometry into Shadow Depth Maps for shadowing. Requires manual setup of shadowing distances and only culls per-component, causing poor performance with high-poly scenes. Bake shadowing for Stationary Lights requires this method. However, Stationary lighting is incompatible with Nanite-enabled meshes that are movable, so they will not cast any dynamic shadows.
-   **Virtual Shadow Maps (Beta):** Renders geometry into virtualized Shadow Depth Maps for shadowing. Provides high-quality shadows for next-gen projects with simplified setup. High-efficiency culling when used with Nanite.
    
    This system is in development and thus has a number of performance pitfalls.
    



 |

### Hardware Ray Tracing

| **Section** | **Description** |
| --- | --- |
| **Support Hardware Ray Tracing** | 
Sets the support of Hardware Ray Tracing features.

Requires **Support Compute Skincache** before the project is allowed to set this.



 |
| **Ray Traced Shadows** | 

Controls whether Ray Traced Shadows are used by default.

Lights can still override and force Ray Traced Shadows on or off.

Requires Hardware Ray Tracing to be enabled.



 |
| **Ray Traced Skylight** | 

Controls whether Ray Traced Skylight is used by default.

Skylights can still override and force Ray Traced Skylight on or off.

Requires Hardware Ray Tracing to be enabled.

Has no effect when the Dynamic Global Illumination Method is set to Lumen.



 |
| **Texture LOD** | 

Enables automatic texture Mip level selection in ray tracing material shaders.

If disabled, the highest resolution Mip level is used for all textures (default).

If enabled, texture LOD is approximated based on total ray length, output resolution and texel density at hit point (ray cone method).



 |
| **Path Tracing** | 

Enables the Path Tracing renderer.

This enables additional Material permutations.

Requires Hardware Ray Tracing to be enabled.



 |

### Software Ray Tracing

| **Section** | **Description** |
| --- | --- |
| **Generate Mesh Distance Fields** | 
Defines whether to build distance fields of Static Meshes, needed for Software Ray Tracing in Lumen, and distance field AO, which is used to implement Movable SkyLight Shadows, and Ray Traced Distance Field Shadows on directional lights.

Enabling this will increase the build times, memory usage and disk size of Static Meshes.

Changing this setting requires restarting the editor.



 |
| **Distance Field Voxel Density** | 

Determines how the default scale of a mesh converts into distance field voxel dimensions.

Changing this will cause all distance fields to be rebuilt.

Large values can consume memory very quickly!

Changing this setting requires restarting the editor.



 |

### Misc Lighting

| **Section** | **Description** |
| --- | --- |
| **Allow Static Lighting** | 
Defines whether to allow any static lighting to be generated and used, like Lightmaps and Shadow Maps.

Games that only use dynamic lighting should set this to 0 to save some static lighting overhead.

Disabling this allows Material AO and Material BentNormal to work with Lumen Global Illumination.

Changing this setting requires restarting the editor.



 |
| **Use Normal Maps for Static Lighting** | Defines whether to allow any static lighting to use normal maps for lighting computations. |
| **DBuffer Decals** | 

Defines whether to accumulate decal properties to a buffer before the Base Pass.

DBuffer decals correctly affect Lightmap and sky lighting, unlike regular deferred decals.

DBuffer enabled forces a full Pre-Pass.

Changing this setting requires restarting the editor.



 |

### Forward Renderer

| **Section** | **Description** |
| --- | --- |
| **Forward Shading** | 
Defines whether to use forward shading on desktop platforms. Requires Shader Model 5 hardware.

Forward shading supports MSAA and has lower default cost, but fewer features supported overall.

Materials have to opt in to more expensive features like high quality reflections.

Changing this setting requires restarting the editor.



 |
| **Vertex Fogging for Opaque** | 

Causes opaque materials to use per-vertex fogging, which costs slightly less.

Only supported with forward shading.

Changing this setting requires restarting the editor.



 |

### Translucency

| **Section** | **Description** |
| --- | --- |
| **Separate Translucency** | 
Allows translucency to be rendered to a separate render targeted and composited after depth of field.

Prevents translucency from appearing out of focus.



 |
| **Translucent Sort Policy** | 

The sort mode for translucent primitives, affecting how they are ordered and how they change order as the camera moves.

Requires that Separate Translucency (found in the **Viewport Options** under **Show > Advanced**) is enabled.

You can choose from the following options:

-   **Sort by Distance:** Sort based on distance from camera center point to bounding sphere center point (default, best for 3D games).
-   **Sort by Projected Z:** Sort based on the post-projection Z distance to the camera.
-   **Sort Along Axis:** Sort based on the projection onto a fixed axis (best for 2D games).



 |
| **Translucent Sort Axis** | The axis that sorting will occur along when Translucent Sort Policy is set to `SortAlongAxis`. |

### VR

| **Section** | **Description** |
| --- | --- |
| **HMD Fixed Foveation Level (Experimental)** | 
Set the level of fixed-foveation to apply when generating the Variable Rate Shading attachment.

This feature is currently experimental.

This can yield some fairly significant performance benefits on GPUs that support Tier 2 VRS.

Lower settings will result in almost no discernible artifacting on most head-mounted devices (HMDs); higher settings will show some artifacts towards the edges of the view.

You can choose from the following options:

-   **Disabled**
-   **Low**
-   **Medium**
-   **High**
-   **High Top**



 |
| **Dynamic Fixed Foveation (Experimental)** | 

Allows fixed foveation level to adjust dynamically based on GPU utilization.

Level will range between none at the minimum, and the currently selected foveation level at the maximum.



 |
| **Instanced Stereo** | Enables single-pass stereoscopic rendering through view instancing or draw call instancing. |
| **Mobile HDR** | 

If enabled, mobile pipelines include a full post-processing pass with tonemapping.

Disable this setting for a performance boost and to enable stereoscopic rendering optimizations.

Changing this setting requires restarting the editor.



 |
| **Mobile Multi-View** | Enables single-pass stereoscopic rendering on mobile platforms. |
| **Round-Robin Occlusion Queries** | Enables round-robin scheduling of occlusion queries for VR. |

### Post-Processing

| **Section** | **Description** |
| --- | --- |
| **Custom Depth-Stencil Pass** | 
Defines whether the Custom Depth Pass for tagging primitives for post-processing passes is enabled.

Enabling it on demand can save memory but may cause a hitch the first time the feature is used.

You can choose from the following options:

-   **Disabled**
-   **Enabled:** Depth buffer is created immediately, Stencil is disabled.
-   **Enabled on Demand:** Depth buffer created on first use; this option can save memory but cause stalls. Stencil is disabled.
-   **Enabled with Stencil:** Depth buffer is created immediately, Stencil is available for read / write.



 |
| **Custom Depth with TemporalAA Jitter** | 

Defines whether the Custom Depth Pass has the TemporalAA jitter enabled.

Disabling this can be useful when the result of the CustomDepth Pass is used after TAA (for example, after Tonemapping).



 |
| **Enable Alpha Channel Support in Post-Processing (Experimental)** | 

Configures alpha channel support in renderer's post-processing chain.

Still experimental: works only with Temporal AA, Motion Blur, and Circle Depth of Field.

This option also force-disables the separate translucency.

You can choose from the following options:

-   **Disabled:** Reduces GPU cost to the minimum. This is the default option.
-   **Linear Color Space Only:** Maintains alpha channel only within linear color space. Tonemapper won't output alpha channel.
-   **Allow Through Tonemapper:** Maintains alpha channel within linear color space, but also passes it through the tonemapper.

Passing the alpha channel through the tonemapper can inevitably lead to pretty poor compositing quality as opposed to linear color space compositing, especially on purely additive pixels bloom can generate.

This setting is exclusively targeting the broadcast industry in case the hardware is unable to do linear color space compositing and tonemapping.



 |

### Default Settings

| **Section** | **Description** |
| --- | --- |
| **Bloom** | Defines whether the default for Bloom is enabled or not (post-process volume / camera / game settings can still override and enable or disable it independently). |
| **Ambient Occlusion** | Defines whether the default for AmbientOcclusion is enabled or not (post-process volume / camera / game settings can still override and enable or disable it independently). |
| **Ambient Occlusion Static Fraction (AO for Baked Lighting)** | Defines whether the default for `AmbientOcclusionStaticFraction` is enabled or not. This is only useful for baked lighting and if AO is on, and allows SSAO to affect baked lighting as well at the cost of lowering performance (post-process volume / camera / game settings can still override and enable or disable it independently). |
| **Auto-Exposure** | Defines whether the default for Auto-Exposure is enabled or not (post-process volume / camera / game settings can still override and enable or disable it independently). |
| **Auto-Exposure Method** | 
The default method for Auto-Exposure (post-process volume / camera / game settings can still override and enable or disable it independently).

You can choose from the following options:

-   **Auto-Exposure Histogram:** This method constructs a 64-bin histogram, giving finer control over Auto-Exposure with some advanced settings.
-   **Auto-Exposure Basic:** Faster method that computes single values by downsampling.
-   **Manual:** This method uses camera settings.



 |
| **Auto-Exposure Bias** | Default value for Auto-Exposure bias. |
| **Motion Blur** | Defines whether the default for MotionBlur is enabled or not (post-process volume / camera / game settings can still override and enable or disable it independently). |
| **Lens Flares (Image-Based)** | Defines whether the default for LensFlare is enabled or not (post-process volume / camera / game settings can still override and enable or disable it independently). |
| **Temporal Upsampling** | Defines whether to do primary screen percentage upscale with Temporal AA pass or not. |
| **Anti-Aliasing Method** | 

Selects the anti-aliasing method to use.

You can choose from the following options:

-   **None**
-   **Fast Approximate Anti-Aliasing (FXAA)**
-   **Temporal Anti-Aliasing (TAA)**
-   **Multisample Anti-Aliasing (MSAA)**
-   **Temporal Super-Resolution (TSR)**



 |
| **MSAA Sample Count** | 

Default number of samples for MSAA.

You can choose from the following options:

-   **No MSAA**
-   **2x MSAA**
-   **4x MSAA**
-   **8x MSAA**



 |
| **Light Units** | 

Which units to use for newly placed point, spot and rect lights.

You can choose from the following options:

-   **Unitless**
-   **Candelas**
-   **Lumens**



 |
| **Frame Buffer Pixel Format** | 

Pixel format used for back buffer, when not specified.

You can choose from the following options:

-   **8-bit RGBA**
-   **Float RGBA**
-   **10-bit RGB, 2-bit Alpha**



 |

### Optimizations

| **Section** | **Description** |
| --- | --- |
| **Render Unbuilt Preview Shadows in Game** | 
Defines whether to render unbuilt preview shadows in-game.

When enabled, any shadows from unbuilt static lighting will be rendered in the game using dynamic movable lighting.

When disabled, any static lighting which has not been previously built will not have shadows rendered.

Disabling this setting means that lighting between working in the Level Editor and launching the game won't match because unbuilt static shadows are not being replaced by dynamic preview shadows.



 |
| **Use Stencil for LOD Dither Fading** | 

Defines whether to use stencil for LOD dither fading.

This saves GPU time in the Base Pass for materials with dither fading enabled, but forces a Full Pre-Pass.

Changing this setting requires restarting the editor.



 |
| **Early Z Pass** | 

Defines whether to use a Depth Only Pass to initiate Z culling for the Base Pass.

You can choose from the following options:

-   **None**
-   **Opaque Meshes Only**
-   **Opaque and Masked Meshes**
-   **Decide Automatically:** Let the engine decide what to render in the Early Z Pass based on the features being used.



 |
| **Mask Material Only in Early Z Pass** | 

Defines whether to compute Materials' mask opacity only in Early Z Pass.

Changing this setting requires restarting the editor.



 |
| **Enable CSM Caching** | Enable caching CSM (Cascaded Shadow Maps) to reduce draw calls for casting CSM and potentially improve performance. |
| **Clear Scene** | 

Defines how the GBuffer is cleared in game mode (only affects deferred shading).

You can choose from the following options:

-   **Do Not Clear:** This option is the fastest but can cause artifacts unless you render to every pixel. Make sure to use a skybox with this option!
-   **Hardware Clear:** This option performs a full clear before rendering. Most projects should use this option.
-   **Clear at Far Plane:** This option draws a quad to perform the clear at the far plane. This is faster than a hardware clear on some GPUs.



 |
| **Velocity Pass** | 

Defines when to write to the velocity buffer.

Changing this setting requires restarting the editor.

You can choose from the following options:

-   **Write During Depth Pass**
-   **Write During Base Pass**
-   **Write After Base Pass**



 |
| **Output Velocities Due to Vertex Deformation** | 

Enables materials with World Position Offset and / or World Displacement to output velocities during the Velocity Pass even when the Actor has not moved.

If the `VelocityPass` is set to "Write After Base Pass", this can incur a performance cost due to additional draw calls.

That performance cost is higher if many objects are using World Position Offset (for example, a forest of trees).

You can choose from the following options:

-   **Off:** Always off
-   **On:** Always on
-   **Auto:** On when the performance cost is low (velocity in Depth or Base Pass).



 |
| **Selective GBuffer Render Targets Output** | 

When this setting is enabled, GBuffer render targets that are not relevant are not exported.

Changing this setting requires restarting the editor.



 |
| **Enable Particle Cutouts by Default** | 

When this setting is enabled, Particle Cutouts automatically cuts the square shape of the particle down to its masked area.

This process trades overdrawing for slightly increased vertex counts.

A Particle Cutout texture is chosen automatically using the Opacity Mask texture (if one exists in the Particle's Material). If an Opacity Mask texture doesn't exist, the Opacity texture will be used (if it exists).



 |
| **GPU Particle Simulation Texture Size - X** | 

The X size of the GPU simulation texture size.

`SizeX * SizeY` determines the maximum number of GPU-simulated particles in an emitter.

Potentially overridden by CVar settings in `BaseDeviceProfile.ini`.



 |
| **GPU Particle Simulation Texture Size - Y** | 

The Y size of the GPU simulation texture size.

`SizeX * SizeY` determines the maximum number of GPU-simulated particles in an emitter.

Potentially overridden by CVar settings in `BaseDeviceProfile.ini`.



 |
| **GBuffer Format** | 

Selects which GBuffer format should be used.

Affects performance primarily via how much GPU memory bandwidth is used.

You can choose from the following options:

-   **Force 8 Bits Per Channel:** Forces all GBuffers to 8 bits per channel. Intended as profiling for best performance.
-   **Default:** See GBuffer allocation function for layout details.
-   **High Precision Normals:** Same as Default, except normals are encoded at 16 bits per channel.
-   **Force 16 Bits Per Channel:** Forces all GBuffers to 16 bits per channel. Intended as profiling for best quality.



 |
| **Use GPU for Computing Morph Targets** | Whether to use the original CPU method (loop per morph, then by vertex) or use a GPU-based method on Shader Model 5 hardware. |
| **Support Compute Skin Cache** | 

Enables the Skin Cache system to skin positions and normals / tangents using a Compute Shader where the results are cached in vertex buffers before being passed for rendering.

Note that this cannot be disabled while Hardware Ray Tracing is enabled.



 |
| **Default Skin Cache Behavior** | 

Sets the default behavior of which rendering path Skeletal Meshes use and whether they will automatically use the Skin Cache or `GPUSkinVertexFactory` render path.

If the project setting for **Support Ray Tracing** is enabled and the Skeletal Mesh has **Support Ray Tracing** in its properties, it will be included into Skin Cache (inclusive behavior).

You can choose from the following options:

-   **Exclusive:** All Skeletal Meshes are excluded from the skin cache. Each must opt in individually. If Support Ray Tracing is enabled on a mesh, will force inclusive behavior on that mesh.
-   **Inclusive:** All Skeletal Meshes are included into the skin cache. Each must opt out individually.



 |
| **Maximum Memory for Compute Skin Cache Per World (MB)** | Maximum amount of memory (in MB) per world / scene allowed for the Compute Skin Cache to generate output vertex data and recompute tangents. |
| **Support Depth-Only Index Buffers** | Support depth-only index buffers, which provide a minor rendering speed-up at the expense of using twice the index buffer memory. |
| **Support Reversed Index Buffers** | Support reversed index buffers, which provide a minor rendering speed-up at the expense of using twice the index buffer memory. |

### Debugging

| **Section** | **Description** |
| --- | --- |
| **Enable Vendor-Specific GPU Crash Analysis Tools** | Enables vendor-specific GPU crash analysis tools. |

### Experimental

| **Section** | **Description** |
| --- | --- |
| **Omni-Directional Stereo Capture** | Enables capture of 360-degree stereo images using a Scene Capture Cube and Texture Targets for the left, right, and omni-directional stereo capture. |
| **Mesh Streaming** | When enabled, meshed will stream in based on what is visible on the screen. |

### Editor

| **Section** | **Description** |
| --- | --- |
| **Wireframe Cull Threshold** | The screen radius of the object's bounding box (in centimeters) at which objects in Wireframe view mode are culled. |

### Shader Permutation Reduction

| **Section** | **Description** |
| --- | --- |
| **Support Stationary Skylight** | 
Stationary skylight requires permutations of the Base Pass shaders.

Disabling this setting will reduce the number of shader permutations required per material.

Changing this setting requires restarting the editor.



 |
| **Support Low-Quality Lightmap Shader Permutations** | 

Low-quality Lightmap requires permutations of the Lightmap rendering shaders.

Disabling this setting will reduce the number of shader permutations required per material.

The mobile renderer requires low-quality Lightmaps, so disabling this setting is not recommended for mobile titles using static lighting.

Changing this setting requires restarting the editor.



 |
| **Support PointLight WholeSceneShadows** | 

PointLight WholeSceneShadows requires many vertex and geometry shader permutations for cubemap rendering.

Disabling this setting will reduce the number of shader permutations required per Material.

Changing this setting requires restarting the editor.



 |
| **Support Sky Atmosphere** | The Sky Atmosphere component requires extra samplers / textures to be bound to apply aerial perspective on transparent surfaces (and all surfaces on mobile via per-vertex evaluation). |
| **Support Sky Atmosphere Affecting Height Fog** | 

The Sky Atmosphere component can light up the height for, but it requires extra samplers / texture to be bound to apply aerial perspective on transparent surfaces (and all surfaces on mobile via per-vertex evaluation).

It requires `r.SupportSkyAtmosphere` to be `true`.



 |
| **Support Cloud Shadow on Forward Lit Translucent** | 

Enable cloud shadow on translucent surface not relying on the translucent lighting volume, like using Forward lighting.

This is evaluated per-vertex to reduce GPU cost and requires extra samplers / textures to be bound to vertex shaders.

This is not implemented on Mobile platforms because VolumetricClouds are not available on these platforms.



 |

### Mobile Shader Permutation Reduction

| **Section** | **Description** |
| --- | --- |
| **Support Combined Static and CSM Shadowing** | 
Allow primitives to receive both static and CSM (Cascaded Shadow Maps) shadows from a stationary light.

Disabling this setting will free a mobile texture sampler and reduce shader permutations.

Changing this setting requires restarting the editor.



 |
| **Support CSM on Levels with Force No Precomputed Lighting Enabled** | 

When **Allow Static Lighting** is enabled, shaders to support CSM without any precomputed lighting are not normally generated.

This setting allows CSM for this case at the cost of extra shader permutations.

Changing this setting requires restarting the editor.



 |
| **Support Pre-Baked Distance Field Shadow Maps** | 

Generate shaders for Static Mesh primitives to render distance field shadow maps with soft shadowing from Lightmass for Stationary Directional Lights.

Changing this setting requires restarting the editor.



 |
| **Support Movable Directional Lights** | 

Generate shaders for primitives to receive movable directional lights.

Changing this setting requires restarting the editor.



 |
| **Max Movable Spotlights / Point Lights** | 

The number of dynamic spotlights or point lights to support on mobile devices.

Setting this to 0 for games which do not require dynamic spotlights or point lights will reduce the number of shaders generated.

Changing this setting requires restarting the editor.



 |
| **Support Movable Spotlights** | 

Generate shaders for primitives to receive lighting from movable spotlights.

This incurs an additional cost when processing movable lights.

Changing this setting requires restarting the editor.



 |
| **Support Movable SpotlightShadows** | 

Generate shaders for primitives to receive shadows from movable spotlights.

Changing this setting requires restarting the editor.



 |

### Skinning

| **Section** | **Description** |
| --- | --- |
| **Support 16-bit Bone Index** | If enabled, a new mesh imported will use 8-bit (if it has 256 bones or fewer) or 16-bit (if it has more than 256 bones) bone indices for rendering. |
| **Limit GPU Skinning to 2-Bones Influence** | 
Defines whether to use 2-bones influence instead of the default of 4 for GPU skinning.

This does not change skeletal mesh assets but reduces the number of instructions required by the GPU skin vertex shaders.

Changing this setting requires restarting the editor.



 |
| **Use Unlimited Bone Influences** | If enabled, a new mesh imported will use an unlimited bone buffer instead of fixed `MaxBoneInfluences` for rendering. |
| **Unlimited Bone Influences Threshold** | When Unlimited Bone Influence is enabled, it still uses a fixed bone influence buffer until the max bone influence of a mesh exceeds this value. |
| **Maximum Bones Per Sections** | 

Sets a maximum limit of bones per material Section for any Skeletal Mesh being imported into the engine.

The number of bones allowed per Section is the number of bones that can be skinned on the GPU during a single draw call.

If the source mesh exceeds this limit, the Sections are divided into smaller chunks that fit within the limit.

Use the Add (+) button to specify per-platform maximum limits of bones to use per Section. For example, Mobile is already added and set to a maximum of 256.

Changing this setting requires restarting the editor.



 |

### Post-Process Calibration Materials

| **Section** | **Description** |
| --- | --- |
| **Visualize Calibration Color Material Path** | When the VisualizeCalibrationColor show flag is enabled (under **Level Viewport > Show > Developer** menu), this path will be used as the post-process material to render. |
| **Visualize Calibration Custom Material Path** | When the VisualizeCalibrationCustom show flag is enabled (under **Level Viewport > Show > Developer** menu), this path will be used as the post-process material to render. |
| **Visualize Calibration Grayscale Material Path** | When the VisualizeCalibrationGrayscale show flag is enabled (under **Level Viewport > Show > Developer** menu), this path will be used as the post-process material to render. |