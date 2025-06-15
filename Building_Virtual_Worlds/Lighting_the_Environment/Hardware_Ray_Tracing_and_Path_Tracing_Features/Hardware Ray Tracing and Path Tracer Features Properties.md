# Hardware Ray Tracing and Path Tracer Features Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ray-tracing-and-path-tracer-features-properties-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ray-tracing-and-path-tracer-features-properties-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:43

---

This page contains reference for properties and settings of the features of [Real-Time Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) and the [Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine).

## Post Process Volume

The following features of Ray Tracing and the Path Tracer are found in the [Post Process Volume](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine) settings.

| Property | Description |
| --- | --- |
| Global Illumination |   |
| **Method** | Chose what global illumination method to use: None, Lumen, Screen Space, or Ray Traced. |
| Ray Tracing Global Illumination |   |
| **Type** | 
Sets what Ray Tracing Global Illumination method to use:

-   **Disabled:** Disables RTGI methods.
-   **Brute Force:** Uses the slower, more accurate brute force method for dynamic indirect lighting using RTGI.
-   **Final Gather:** Uses a faster, less accurate final gather method for dynamic indirect lighting using RTGI.

For more information, see the Ray Traced Global Illumination section of the [Real-Time Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) page.



 |
| **Max Bounces** | Sets the maximum number of bounces of light that will be used by RTGI. |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for RTGI. Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |
| Reflections |   |
| **Method** | Sets what method of dynamic scene reflections to use: None, Lumen, Screen Space, or Ray Traced. |
| Ray Tracing Reflections |   |
| **Max Roughness** | Sets the maximum roughness value that Ray Traced Reflections will be visible before falling back to raster methods that are less expensive. Reflection contribution is smoothly faded when close to the roughness threshold and this parameter behaves similarly to SSR's Max Roughness setting. Lower values fall back to other methods more quickly. |
| **Max Bounces** | Sets the maximum number of bounces that Ray Traced Reflections uses. More bounces create inter-reflection but comes at a higher cost. Set to 1 bounce by default. |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for Ray Traced Reflections. Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |
| **Shadows** | 

Sets how shadows should be reflected. Choose between:

-   **Hard Shadows** which has no soft shadows
    
-   **Area Shadows** to have soft shadowing like raytraced shadows
    
-   **Disable** to disable shadowing in Ray Traced Reflections
    



 |
| **Include Translucent Objects** | When the checkbox is checked, this sets whether translucent materials will be included in Ray Tracing Reflections. |
| Ray Tracing Ambient Occlusion |   |
| **Enabled** | When the checkbox is checked, it enables Ray Tracing Ambient Occlusion (RTAO). |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for [Ray Traced Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine) (RTAO). Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |
| **Intensity** | Defines how much ambient occlusion affects non-direct lighting for [Ray Traced Ambient Occlusion](/documentation/en-us/unreal-engine/distance-field-ambient-occlusion-in-unreal-engine). Lower values decrease the effect while higher values increase how strong the effect is. |
| **Radius** | Controls the distance in Unreal Units that ambient occlusion affects. |
| Translucency |   |
| **Type** | Sets whether to use **Ray Tracing** or **Raster** method for reflections within this volume. When selecting Raster, default translucency methods will be used instead of ray traced ones. |
| Ray Tracing Translucency |   |
| **Max Roughness** | Sets the maximum roughness value that Ray Traced Translucency will be visible before falling back to raster methods that are less expensive. Translucency contribution is smoothly faded when close to the roughness threshold and this parameter behaves similarly to SSR's Max Roughness setting. Lower values fall back to other methods more quickly. |
| **Max Refraction Rays** | Sets the maximum number of refraction rays that Ray Traced Translucency uses. Additional Samples decrease performance while increasing quality and accuracy. Set to 3 refraction rays by default. |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for Ray Traced Translucency. Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |
| **Shadows** | 

Sets how shadows should be reflected. Choose between:

-   **Hard Shadows** which has no soft shadows
    
-   **Area Shadows** to have soft shadowing like raytraced shadows
    
-   **Disable** to disable shadowing in Ray Traced Translucency
    



 |
| **Refraction** | Sets whether refraction should be enabled or not for Ray Traced Translucency. If disabled, rays will not scatter and only travel in the same direction as before the intersection event. |
| Path Tracing |   |
| **Max. Bounces** | Sets the maximum possible number of light bounces rays should travel before being terminated. |
| **Samples Per Pixel** | Sets the number of samples used per pixel for convergence. A higher number of samples reduces noise of the rendered image. |
| **Filter Width** | Improves quality of the rendered image by setting the filter width used by anti-aliasing. Lower widths yeild sharper (or more aliased) results. Larger values soften (or blur) aliasing results. |
| **Emissive Materials** | Enables bounce lighting for emissive materials. Enabling this property prevents double-counting illumination of surfaces that are also represented by actual light sources, and noise from small emitters. For example, having an emissive material representing a small light bulb while also using a point or spot light source to illuminate the area would be double-counted in this case. |
| **Max Path Exposure** | Sets the maximum exposure allowed for path tracing in order to reduce [firefly artifacts](https://en.wikipedia.org/wiki/Fireflies_computer_graphics) from occurring. Adjusting the exposure to a higher value than the scene's exposure helps mitigate these artifacts. (See [Additional Information](/documentation/en-us/unreal-engine/ray-tracing-and-path-tracer-features-properties-in-unreal-engine#additionalinformation) section of this page for more details and an example of this type of artifact). |
| **Denoiser** | This toggle uses the currently loaded denoiser plugin on the last sample to remove noise from the rendered output. By default, Intel's Open Image Denoiser plugin is used by the Unreal Engine. This toggle has no effect on the rendered output if the denoiser plugin is not enabled. |

## Types of Lights

Unreal Engine includes different [types of lights](/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) which have their own settings that work specifically with ray tracing and path tracing.

### Directional Light

The following properties of [Directional Lights](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine) affect real-time ray tracing and path tracing. Properties are located in the **Light** and **Ray Tracing** categories of the **Details** panel.

| Property | Description |
| --- | --- |
| Light |   |
| **Source Angle** | The angle subtended by light source in degrees (also known as angular diameter). Lower angles give sharper shadow contacts whereas higher degree angles give softer shadows. |
| **Cast Ray Traced Shadow** | Sets whether shadows from this light are computed with traditional shadow maps or ray-traced. When selecting **Use Project Setting**, the light will default to whether ray traced shadows is enabled or disabled in the Project Settings under Engine > Rendering > Hardware Ray Tracing with the property **Ray Traced Shadows**. |
| **Affect Ray Tracing Reflections** | Whether the light affects objects in reflections when Ray Traced Reflections is enabled. |
| **Affect Ray Tracing Global Illumination** | Whether the light contributes to ray traced global illumination when Ray Tracing Global Illumination is enabled. |
| Ray Tracing |   |
| **Shadow Source Angle Factor** | Adds a scaling factor to the shadow source angle relative to what is specified by **Light Source Angle**. This property requires that **Cast Ray Traced Shadow** be enabled. |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for Ray Traced Shadows from a Directional Light. Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |

### Point and Spot Lights

The following properties of [Point Lights](/documentation/en-us/unreal-engine/point-lights-in-unreal-engine) and [Spot Lights](/documentation/en-us/unreal-engine/spot-lights-in-unreal-engine) affect real-time ray tracing and path tracing. Properties are located in the **Light** and **Ray Tracing** categories of the **Details** panel.

| Property | Description |
| --- | --- |
| Light |   |
| **Source Radius** | The radius of the light sources shape. A smaller radius gives sharper shadow contacts whereas a higher radius gives softer shadows. |
| **Cast Ray Traced Shadow** | Sets whether shadows from this light are computed with traditional shadow maps or ray-traced. When selecting **Use Project Setting**, the light will default to whether ray traced shadows is enabled or disabled in the Project Settings under Engine > Rendering > Hardware Ray Tracing with the property **Ray Traced Shadows**. |
| **Affect Ray Tracing Reflections** | Whether the light affects objects in reflections when Ray Traced Reflections is enabled. |
| **Affect Ray Tracing Global Illumination** | Whether the light contributes to ray traced global illumination when Ray Tracing Global Illumination is enabled. |
| Ray Tracing |   |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for Ray Traced Shadows from Point and Spot Lights. Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |

### Rect Light

The following properties of [Rect Lights](/documentation/en-us/unreal-engine/rectangular-area-lights-in-unreal-engine) affect real-time ray tracing and path tracing. Properties are located in the **Light** and **Ray Tracing** categories of the **Details** panel.

| Property | Description |
| --- | --- |
| Light |   |
| **Source Width** | The width of the light source shape. |
| **Source Height** | The height of the light source shape. |
| **Barn Door Angle** | The angle of the winged doors at the edge of the Rect Light's shape. The angle controls the forward direction and spread of the light. |
| **Barn Door Length** | The length of the winged door at the edge of the Rect Light's shape. The length controls the sharpness of the light source's edge, similar to how Source Radius works with Point Lights and Spot Lights. |
| **Cast Ray Traced Shadow** | Sets whether shadows from this light are computed with traditional shadow maps or ray-traced. When selecting **Use Project Setting**, the light will default to whether ray traced shadows is enabled or disabled in the Project Settings under Engine > Rendering > Hardware Ray Tracing with the property **Ray Traced Shadows**. |
| **Affect Ray Tracing Reflections** | Whether the light affects objects in reflections when Ray Traced Reflections is enabled. |
| **Affect Ray Tracing Global Illumination** | Whether the light contributes to ray traced global illumination when Ray Tracing Global Illumination is enabled. |
| Ray Tracing |   |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for Ray Traced Shadows from a Rect Light. Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |

### Sky Light

The following properties of [Sky Lights](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) affect real-time ray tracing and path tracing. Properties are located in the **Light** and **Ray Tracing** categories of the **Details** panel.

| Property | Description |
| --- | --- |
| Light |   |
| **Cast Ray Traced Shadow** | Sets whether shadows from this light are computed with traditional shadow maps or ray-traced. When selecting **Use Project Setting**, the light will default to whether ray traced shadows is enabled or disabled in the Project Settings under Engine > Rendering > Hardware Ray Tracing with the property **Ray Traced Shadows**. |
| **Affect Ray Tracing Reflections** | Whether the light affects objects in reflections when Ray Traced Reflections is enabled. |
| **Affect Ray Tracing Global Illumination** | Whether the light contributes to ray traced global illumination when Ray Tracing Global Illumination is enabled. |
| Ray Tracing |   |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for Ray Traced Shadows from a Sky Light. Additional samples decrease performance while increasing quality and accuracy. Set to 1 sample per pixel by default. |

## Actors

The following properties of placed **Actors** affect real-time ray tracing and path tracing. Properties are located in the **Rendering** and **Ray Tracing** categories of the **Details** panel.

| Property | Description |
| --- | --- |
| Rendering: Advanced |   |
| **Visible in Ray Tracing** | When enabled, this component will be visible in ray tracing effects. When disabled, it will be removed from ray tracing effects like reflections, translucency, shadows, and more. |
| Ray Tracing: Advanced |   |
| **Evaluate World Position Offset** | When enabled, this Actor will be evaluated for ray tracing effects for any assigned Materials that make use of World Position Offset. |
| **Ray Tracing Far Field** | If true, this component is available to be ray traced as a far field primitive, even if it is hidden. |
| **Ray Tracing Group Id** | Defines the runtime groups of components. For example, it allows assembly of multiple parts of a building at runtime. When set to -1, the component doesn't belong to any group. |
| **Ray Tracing Group Culling Priority** | Defines how quickly this Actor should be culled. For example, buildings and larger objects should have a low priority, but smaller objects should have a higher priority so that they are culled sooner. |

## Materials

The following properties of [Materials](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide) affect real-time ray tracing and path tracing. Properties are located in the **Details** panel of the Material Editor.

| Property | Description |
| --- | --- |
| Material |   |
| **Cast Ray Traced Shadows** | Set whether this Material should allow its assigned Actor to cast ray traced shadows when Ray Tracing features are enabled. Requires that the Light Source casting shadows to have **Cast Ray Traced Shadows** enabled. |