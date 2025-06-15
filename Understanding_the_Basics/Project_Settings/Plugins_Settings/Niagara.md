# Niagara

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/niagara-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/niagara-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:39:03

---

## Niagara

### Niagara

| **Setting** | **Description** |
| --- | --- |
| **Additional Parameter Types** | 
If enabled, you can save a struct of parameters into the project. You can then reuse your struct in different Niagara scripts.

Create a struct Asset through the **Content Browser**: right-click in an empty area, then select **Blueprints > Structure**.



 |
| **Additional Payload Types** | If enabled, you can save a payload struct in your project. A payload is also a struct of parameters, but with the additional ability to perform read and write events on it. |
| **Additional Parameter Enums** | Save an enum into your project for reuse in different Niagara scripts. |
| **Show Convertible Inputs in Stack** | If enabled, the "link input" menu will also show variables of different types, as long as there is a conversion script for them. |
| **Systems Support Large World Coordinates** | 

If enabled, active effects rebase the simulation positions to not lose precision.

If you don't need this setting, disable it to skip unnecessary rebasing calculations.



 |
| **Enforce strict type checks in the graph** | 

If enabled, types like positions and vectors can't be assigned to each other without an explicit conversion step.

If disabled, type checks are loosened and some types can be implicitly converted into each other.

Don't disable this when working with large world coordinates.



 |
| **Default Effect Type** | 

Default effect type to use for effects that don't define their own.

Can be `null`.



 |
| **Position Pin Type Color** | 

Position pin type color.

The other pin colors are defined in the general editor settings.



 |

### Viewport

| **Setting** | **Description** |
| --- | --- |
| **System Viewport in Orbit Mode** | Sets the default navigation behavior for the system preview viewport. |

### Scalability

| **Setting** | **Description** |
| --- | --- |
| **Quality Levels** | The quality levels Niagara uses. |

### Renderer

| **Setting** | **Description** |
| --- | --- |
| **Component Renderer Warnings Per Class** | Info texts that the component renderer displays based on the selected component class. |
| **Default Render Target Format** | 
The default render target format used by all Niagara Render Target Data Interfaces unless overridden.

You can choose from the following options:

-   **RTF R8:** R channel, 8 bit per channel fixed point, range \[0, 1\].
-   **RTF RG8:** RG channels, 8 bit per channel fixed point, range \[0, 1\].
-   **RTF RGBA8:** RGBA channels, 8 bit per channel fixed point, range \[0, 1\].
-   **RTF RGBA8 SRGB:** RGBA channels, 8 bit per channel fixed point, range \[0, 1\]. RGB is encoded with sRGB gamma curve. Alpha is always stored as linear.
-   **RTF R16f:** R channel, 16 bit per channel floating point, range \[-65504, 65504\].
-   **RTF RG16f:** RG channels, 16 bit per channel floating point, range \[-65504, 65504\].
-   **RTF RGBA16f:** RGBA channels, 16 bit per channel floating point, range \[-65504, 65504\].
-   **RTF R32f:** R channel, 32 bit per channel floating point, range \[-3.402823 x 10^38, 3.402823 x 10^38\].
-   **RTF RG32f:** RG channels, 32 bit per channel floating point, range \[-3.402823 x 10^38, 3.402823 x 10^38\].
-   **RTF RGBA32f:** RGBA channels, 32 bit per channel floating point, range \[-3.402823 x 10^38, 3.402823 x 10^38\].
-   **RTF RGB10A2:** RGBA channels, 10 bit per channel fixed point and 2 bit(s) of alpha.



 |
| **Default Grid Format** | 

The default buffer format used by all Niagara Grid Data Interfaces unless overridden.

You can choose from the following options:

-   **Float:** 32-bit per channel floating point, range \[-3.402823 x 10^38, 3.402823 x 10^38\]
-   **Half Float:** 16-bit per channel floating point, range \[-65504, 65504\]
-   **Unsigned Normalized Byte:** 8-bit per channel fixed point, range \[0, 1\].



 |
| **Default Renderer Motion Vector Setting** | 

The default setting for motion vectors in Niagara renderers.

You can choose from the following options:

-   **Precise:** Motion vectors are generated precisely (ideal for motion blur and temporal anti-aliasing). Requires relevant emitters to store more data per particle, and may affect vertex processing performance.
-   **Approximate:** Approximates the motion vectors from current velocity. Saves memory and performance, but can result in lower quality motion blur and/or anti-aliasing.



 |
| **Default Pixel Coverage Mode** | 

The default setting for pixel coverage mode when automatic is set on the Niagara Renderer.

You can choose from the following options:

-   **Enabled:** When the renderer is set to automatic mode, pixel coverage is enabled.
-   **Disabled:** When the renderer is set to automatic mode, pixel coverage is disabled.



 |

### Skeletal Mesh Data Interface (DI)

| **Setting** | **Description** |
| --- | --- |
| **Gpu Max Bone Influences** | 
Controls the maximum number of influences that the Skeletal Mesh Data Interface can use on the GPU.

Changing this setting requires restarting the Editor.

You can choose from the following options:

-   **Allow Max 4:** Allow up to 4 bones to be sampled.
-   **Allow max 8:** Allow up to 8 bones to be sampled.
-   **Unlimited:** Allow an unlimited amount of bones to be sampled.



 |
| **Gpu Uniform Sampling Format** | 

Controls the format used for uniform sampling on the GPU.

Changing this setting requires restarting the Editor.

You can choose from the following options:

-   **Full:** 64 bits per entry. Allow for the full int32 range of triangles (2 billion).
-   **Limited 24.8:** 32 bits per entry. Allow for ~16.7 million triangles and 8 bits of probability precision.
-   **Limited 23.9:** 32 bits per entry. Allow for ~8.4 million triangles and 8 bits of probability precision.



 |
| **Adjacency Triangle Index Format** | 

Controls the format used for specifying triangle indexes in adjacency buffers.

Changing this setting requires restarting the Editor.

You can choose from the following options:

-   **Full:** 32 bits per entry. Allow for the full int32 range of triangles (2 billion).
-   **Half:** 16 bits per entry. Allow for half (int16) range of triangles (64k).



 |

### Static Mesh DI

| **Setting** | **Description** |
| --- | --- |
| **Allow Distance Fields (Experimental)** | 
When enabled, the Static Mesh data interface is allowed to sample from the distance field data (if present) on the GPU.

Enabling this feature will move all systems that contain Static Mesh samples into the `PostRenderOpaque` tick group regardless of the features used.

Changing this setting requires restarting the Editor.



 |

### Async GPU Trace DI

| **Setting** | **Description** |
| --- | --- |
| **Trace Provider Priorities (Experimental)** | 
Defines how traces tagged as Project Default will be interpreted when using the `AsyncGpuTrace` data interface.

The system will go through (starting at element 0) to find the first available provider.



 |