# Post Process Effects

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:02

---

Post-processing effects enable artists and designers to define the overall look and feel of the scene through a combined selection of properties and features that affect coloring, tonemapping, lighting, and more. A special type of volume, called a **Post Process Volume**, can be added to a Level to access these features. Multiple volumes can be placed to define the look of a specific area, or it can be set to affect the entire scene.

## Using Post Process Volumes

You can add a **Post Process Volume** into your Level using the **Place Actors** panel.

Click image for full size.

Once placed in the Level, use the **Details** panel to access all the available properties and features. You'll find that they are broken up into categories for the type of feature they are and what they affect.

Click image for full size.

The **Post Process Volume Settings** are specific settings for this placed volume and how it interacts with the scene and with any other Post Process Volumes it may overlap with. For example, you can toggle the **Infinite Extent** property to make this Post Process Volume affect everywhere in the scene, or leave it unchecked to have it affect only a certain area. When Volumes overlap, you can control how they interact with one another to blend from one to another, which is useful when you have radically different looks between them.

| Property | Description |
| --- | --- |
| **Priority** | Specifies the priority of this volume. In the case of overlapping volumes, the one with the highest priority overrides the lower priority ones. The order is undefined if two or more overlapping volumes have the same priority. |
| **Blend Radius** | Sets the radius (in world units) around the volume that is used for blending. For example, when walking into a volume, the look can be different than that outside of the volume. The blend radius creates a transitional area around the volume. |
| **Blend Weight** | The amount of influence the volume's properties have. A value of 1 has full effect, while a value of 0 has no effect. |
| **Enabled** | Whether this volume affects post processing or not. If enabled, the volume's settings are used for blending. |
| **Infinite Extent (Unbound)** | Whether the bounds of the volume are taken into account. If enabled, the volume affects the entire scene, regardless of its volume's bounds. When not enabled, the volume only has an effect within its bounds. |

## Post Process Features and Properties

Access a Post Process Volume's properties and settings by selecting one placed in the Level. The **Details** panel will list the available categories and their available properties.

Unreal Engine uses some default post processing settings, even if you don't have a placed Post Process Volume in your Level. These default post process settings can be found and configured in the **Project Settings** in the **Rendering > Default Settings** section.

Configuring these options can be useful for Level Editing to stabilize auto exposure or bloom before you start working on defining the look of the scene.

## Lens

The **Lens** category contains properties and settings that simulate common real-world effects from a camera lens.

### Depth of Field

Similar to what happens with real-world cameras, **Depth of Field** applies a blur to a scene based on the distance in front of, or behind, a focal point. The effect is used to draw the viewer's attention to a specific subject in the shot based on depth. It also adds an aesthetic which makes the rendered image appear more like a photograph, or film.

![Depth of Field Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddbff770-3014-4665-bbef-f23359ab1c38/dof_cine_disabled.png)

![Cinematic Depth of Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b1fd02a-7cff-48cc-af40-27c0f75c6a7f/dof_cine_enabled.png)

There are two depth of field options available:

-   [Cinematic Depth of Field](/documentation/en-us/unreal-engine/cinematic-depth-of-field-in-unreal-engine) is used for desktop and console platforms. It provides a filmic look with properties that align with those found on real-world cameras. The Post Process Volume provides some settings, but primarily the camera properties found on a [Cinematic Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine) should be used to control depth of field.
-   [Mobile Depth of Field](/documentation/en-us/unreal-engine/mobile-depth-of-field-in-unreal-engine) is an optimized, low-cost option that works for mobile platforms. It uses gaussian blurring to set a focal region with near and far transition areas.

For more information, see [Depth of Field](/documentation/en-us/unreal-engine/depth-of-field-in-unreal-engine)

### Bloom

**Bloom** is a lighting artifact of real-world cameras that also adds to the perceived realism of the rendered image by reproducing glow around lights and reflective surfaces. Bloom is an effect that works with other effects, like lens flares and dirt masks, but those are not covered by the general bloom properties.

![Convolution for Bloom: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09687b5d-42de-4b64-a2f3-68e0494bd9ee/fftbloom_enabled.png)

![Convolution for Bloom: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6a15cc3-f3a6-46a2-84d6-20af5f3e447f/fftbloom_disabled.png)

For more information, see [Bloom](/documentation/en-us/unreal-engine/bloom-in-unreal-engine)

### Exposure and Local Exposure

The engine automatically controls exposure — though it's sometimes called eye adaptation — which adjusts how bright, or dark, the scene becomes for the current view based on current scene luminance. This effect recreates the experience of human eyes adjusting to different lighting conditions, like when walking from a dimly lit interior to a brightly lit exterior, or the other way around.

The **Exposure** category contains properties to select the type of exposure method to use and to specify how bright or dark it should allow the scene to become over a given time.

There is an additional control for exposure called **Local Exposure** that has its own category or properties. These properties apply local adjustments to exposure (within artist-controlled parameters) using edge-aware data structure while preserving luminance detail. This makes it particularly useful in challenging high contrast scenes, such as indoor scenes with very bright outdoors that are visible through doors and windows.

For more information, see [Exposure](/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine)

### Chromatic Aberration

**Chromatic Aberration** is an effect that simulates the color shifts in real-world camera lenses. It's a phenomena where light rays enter a lens at different points causing separation of RGB colors.

![Without Chromatic Aberration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c3c2365-c13c-4078-a3bb-5d48d14c3ddb/scenefringe_0.png)

![With Chromatic Aberration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e72ba27-18f0-4c16-bdde-2e30051bdbe8/scenefringe_2.png)

| Property | Description |
| --- | --- |
| **Intensity** | The amount of aberration/camera fringe, or camera imperfection, to simulate an artifact that happens in real-world camera lenses. |
| **Start Offset** | A normalized distance to the center of the framebuffer where the effect takes place. |

### Dirt Mask

The **Dirt Mask** is a texture-driven effect that brightens up the [Bloom](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#bloom) in defined areas of the screen. It can be useful to create a specific look of a camera lens and its imperfections, or something like dirt and dust that has gotten on the lens.

![Dirt Mask Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95beae32-942d-4beb-998a-f2e7af1920f4/dirtmaskenabled.png)

![Dirt Mask Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a14f3dd-1da2-4565-9735-892281f8a5f1/dirtmaskdisabled.png)

| Property | Description |
| --- | --- |
| **Dirt Mask Texture** | Texture that defines the dirt on the camera lens where the light of very bright objects is scattered. |
| **Dirt Mask Intensity** | The intensity of the dirt mask. |
| **Dirt Mask Tint** | Apply an RGB color value to the dirt mask texture. |

### Camera

A set of properties controlling the camera shutter and cinematic depth of field.

Full properties and physically based properties of the camera should be set on the [Cinematic Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine).

| Property | Description |
| --- | --- |
| **Shutter Speed (1/s)** | The camera shutter speed in seconds. |
| **ISO** | The camera sensor sensitivity to light. |
| **Aperture (F-stop)** | Defines the opening of the camera lens. Aperture is 1/f-stop. Typical lenses go down to f/1.2 (a large opening). Small numbers have a larger aperture opening, blurring more of the foreground and background. Larger values have a smaller aperture, blurring less of the foreground and background. |
| **Maximum Aperture (min F-stop)** | Defines the maximum opening of the camera lens to control the curvature of blades of the diaphragm. set it to 0 to get straight blades. |
| **Number of diaphragm blades** | Defines the number of blades of the diaphragm within the lens (between 4 and 16). This defines the shape of the bokeh. |

### Lens Flare

The **Lens Flare** effect is an image-based technique that simulates the scattering of light when viewing bright objects due to imperfections in the camera lens.

![lens flare](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/139ebc0b-6c9a-4c01-977a-20786bdeeee9/lens-flare.png)

| Property | Description |
| --- | --- |
| **Intensity** | Brightness scale of the image cased lens flares. |
| **Tint** | Tint color for the image based lens flares. |
| **BokehSize** | 
Size of the lens blur (in percent of the view width) that is done with the Bokeh texture.

Performance cost is radius x radius.



 |
| **Threshold** | 

Minimum brightness the lens flare starts having effect.

This should be as high as possible to avoid the performance cost of blurring content that is too dark to see.



 |
| **BokehShape** | Defines the shape of the Bokeh when the image based lens flares are blurred. It cannot be blended. |
| **Tints** | The RGB defines the lens flare color. The Alpha (A) is its position. |

### Image Effects: Vignette

**Vignette** is an image-based effect that creates a borderless window that fades the image out towards the edges.

![Vignette Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdf05617-91bb-4f54-be31-194b56d95b2f/vignette-0.png)

![Vignette Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ef3d2d9-b9ea-49c7-833b-24f9118fffa5/vignette-1.png)

**Vignette Intensity** controls darkening of the screen corners to create a borderless window from the rendered image to the edge of the window. Larger values increase the amount of vignetting. 0 is no vignetting.

## Color Grading and Tonemapper

**Color Grading** and **Film** are two categories that work together to define a large part of the look of your project. The Color Grading category contains properties that allow for color correction of the rendered scene.

### Color Grading

The **Color Grading** category includes properties to control the contrast, color, saturation, and much more for full artistic control of the look of the scene.

You'll find sections for:

-   Color temperature control
-   Color balance properties for global, shadows, midtones, and highlights
-   Additional miscellaneous properties, such as expanded gamut and look-up tables (Luts)

For more information, see [Coloring Grading and Filmic Tonemapper](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine)

#### Additional Color Grading Topics

%designing-visuals-rendering-and-graphics/post-process-effects/color-grading/look-up-tables:Topic%

### Film

The **Film** category includes properties that meet the [Academy Color Encoding System](http://www.oscars.org/science-technology/sci-tech-projects/aces) (ACES) for television and film. These properties ensure that consistent color is preserved across multiple formats and displays while also future proofing the source material to not have to adjust it for each new medium that comes along.

The properties in this category enable you to set values that mimic different types of film stock.

| Property | Description |
| --- | --- |
| **Slope** | Sets the steepness of the S-curve used for the tonemapper. Larger values make the slope steeper making the image darker, while lower values lessen the steepness making the image lighter. |
| **Toe** | Sets dark colors of the tonemapper. |
| **Shoulder** | Sets the bright colors of the tonemapper. |
| **Black Clip** | 
Sets where the crossover happens where black colors start to cut off their value.

Ideally, this shouldn't ever need to be adjusted.



 |
| **White Clip** | Sets where the crossover happens where white colors start to cut off their value. Changes to this value are subtle in most cases. |

For more information, see [Coloring Grading and Filmic Tonemapper](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine)

## Global Illumination

The Post Process Volume Settings for **Global Illumination** enable you to select the type of dynamic global illumination to use, advanced properties enable you to adjust the intensity and color of some global illumination methods, such as precomputed lighting.

Dynamic global illumination methods can be selected from from the **Method** dropdown menu:

-   [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine)
-   [Screen Space Global Illumination](/documentation/en-us/unreal-engine/screen-space-global-illumination-in-unreal-engine)
-   [Ray Tracing Global Illumination](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine)

Under the **Advanced** section, the **Indirect Lighting Color** and **Indirect Lighting Intensity** to use a color picker to adjust the color of the indirect lighting and intensity will increase or lessen the amount of indirect lighting being applied.

For more information, see [Global Illumination](/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine).

### Lumen Global Illumination

[Lumen Global Illumination](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) is a fully dynamic global illumination system that works with all lights, emissive materials casting light, and sky light occlusion. It renders diffuse interreflection with infinite bounces and indirect specular reflections in large, detailed environments at scales ranging from millimeters to kilometers.

![Lumen Global Illumination Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c4ee931-e404-4572-a3c3-d0c6499e74b2/lumen-gi-on.png)

![Lumen Global Illumination Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b76185dc-e1e2-400d-bfbd-06b0dd697a14/lumen-gi-off.png)

The only property available is the **Final Gather Quality** property that scales Lumen's the amount of noise artifacts that are visible. Larger scales reduce noise, but greatly increase GPU cost.

### Screen Space Global Illumination

[Screen Space Global Illumination](/documentation/en-us/unreal-engine/screen-space-global-illumination-in-unreal-engine) is a low-cost dynamic global illumination method, but it is limited to information visible on the screen. It's best used as an additive feature with precomputed lighting data from [CPU Lightmass](/documentation/en-us/unreal-engine/cpu-lightmass-global-illumination-in-unreal-engine) or [GPU Lightmass](/documentation/en-us/unreal-engine/gpu-lightmass-global-illumination-in-unreal-engine).

![Baked Global Illumination | with Screen Space Global Illumination Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4522df0e-1d38-4b3f-a3ef-41aebb2d54eb/ssgi_enabled.png)

![Baked Global Illumination | with Screen Space Global Illumination Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d7e5524-ae1e-4977-abed-78ba96e39af6/ssgi_disabled.png)

There are not any properties to adjust in the Post Process Volume settings, but you can increase the quality using console commands found under `r.SSGI.*`.

### Ray Tracing Global Illumination

Ray Traced Global Illumination (RTGI) is deprecated and may be removed in a future release.

Requires that **Support Hardware Ray Tracing** and **DirectX 12** be enabled for the project.

[Ray Tracing Global Illumination](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine)

| Property | Description |
| --- | --- |
| **Type** | 
Sets the ray tracing global illumination type:

-   **Brute Force:** A slower, but more accurate ray-traced global illumination method. It requires multiple bounces and increased sample counts to produce a good looking result with fewer artifacts, but comes at greater GPU cost.
-   **Final Gather:** A faster, less accurate ray-traced global illumination method. It uses only a single bounce of indirect lighting with a high number of samples per pixel. It amortizes the cost over multiple frames, trading quality for runtime performance.



 |
| **Max Bounces** | The maximum number of indirect diffuse lighting to ray trace. |
| **Samples Per Pixel** | Sets the number of samples per pixel to use for indirect lighting. Higher samples produce better quality and accuracy but at added GPU cost. Lower values should be used for real-time performance. |

## Reflections

The Post Process Volume settings enable you to select from the types of dynamic reflections you want to use with the **Method** dropdown selection.

Choose between:

-   [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine)
-   [Screen Space Reflections](/documentation/en-us/unreal-engine/screen-space-reflections-in-unreal-engine)
-   [Standalone Ray Traced Reflections](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine)

For more information, see [Reflections Environment](/documentation/en-us/unreal-engine/reflections-environment-in-unreal-engine)

### Lumen Reflections

Lumen reflections are part of the dynamic lighting system [Lumen Global Illumination and Reflections](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine). It works the vast majority of features to support all lights, emissive materials casting light, and sky lighting.

Lumen only has a single **Quality** property which scales the reflection noise quality. Larger scales reduce the amount of noise in reflections, but greatly increases GPU cost.

### Screen Space Reflections

[Screen Space Reflections](/documentation/en-us/unreal-engine/screen-space-reflections-in-unreal-engine) are a low-cost, view-dependent reflection system, but it is limited to information present within the current screen view.

![Screen Space Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6ff57bd-81f2-4c06-bb95-f95528cfd8c9/reflections-screen-space.png)

![Lumen Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df181305-4a34-47cf-be7b-9fae96ce62cd/reflections-lumen.png)

| Property | Description |
| --- | --- |
| **Intensity** | How much screen space reflections should affect the scene. Lower values fade out screen space reflections, falling back to either no reflections or placed [Reflection Captures](/documentation/en-us/unreal-engine/reflections-captures-in-unreal-engine). |
| **Quality** | Controls the quality of the reflections. 0 is no soft transition, 50 (default for better performance) is some transition, and 100 is maximum quality with better reflection representation. |
| **Max Roughness** | Controls at what roughness screen space reflections are faded out. 0.8 works well, and smaller values give better performance |

### Ray Tracing Reflections

Ray Tracing Reflections is deprecated and may be removed in a future release.

Requires that **Support Hardware Ray Tracing** and **DirectX 12** be enabled for the project.

[Ray Tracing Reflections](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine#raytracedreflections) simulate physical light properties with multiple bounces of light on surfaces.

![Ray Tracing Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56e2bb22-4598-45b2-8756-cc5e75e9090a/reflections-ray-tracing.png)

![Screen Space Reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86f4b995-cf4d-47bc-a41c-232b53175d4c/reflections-screen-space-alt.png)

| Property | Description |
| --- | --- |
| **Max Roughness** | Sets the maximum roughness until which ray tracing reflections will be visible. (A lower value is faster) Reflection contribution is smoothly faded when close to roughness threshold. |
| **Max Bounces** | Sets the maximum number of ray tracing reflection bounces from hit surfaces. Larger numbers of bounces allows for reflections in reflections, but at added GPU cost. |
| **Samples Per Pixel** | Sets the number of samples per pixel to use for reflections. Higher samples produce better quality and accuracy but at added GPU cost. Lower values should be used for real-time performance. |
| **Shadows** | Sets the type of ray traced shadows should appear in reflections: none, hard shadows, or soft area shadows. The quality of area shadows is dependent on the number of samples per pixel that are used and costs more to render than hard shadows. |
| **Include Translucent Objects** | Enables Ray Tracing Translucency in ray-traced reflections. |

## Rendering Features

The following are general rendering features that are set and controlled by the Post Process Volume.

### Post Process Materials

**Post Process Materials** allow for materials that have their Domain set to **Post Process** to create visual screen effects. These can be used for just about anything you can do in a material and have that affect gameplay or the visual look of the scene. For example, it can be used for applying a damage effect, creating a stylized or video effect to the screen.

![post process materail examples](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf0519eb-1b3d-4da7-b4d1-c545e3b7eae3/post-process-materials-examples.png)

For more information, see [Post Process Material](/documentation/en-us/unreal-engine/post-process-materials-in-unreal-engine)

### Ambient Cubemap

The **Ambient Cubemap** lights the scene from a provided cubemap texture. The image is mapped to a sphere in the far distance (implemented as a cubemap texture with mipmaps storing pre-blurred versions of the image). The pre-blurred versions of the cubemap are computed in a way that they can be used for specular highlighting with varying glossiness (sharp versus blurry reflections), and they can be used for diffuse lighting as well. This effect is independent of the position a material is lit from. Viewer position, material roughness (for specular effects), and the material surface normal are all taken into account.

The Ambient Cubemap has limited local shadowing (screen space ambient occlusion only). Use a [Sky Light](/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) instead when representing the sky's lighting. The Ambient Cubemap is only intended to be used for a subtle directional ambient term (useful in games with completely dynamic lighting), or for model viewer applications. Because light comes from many directions, it cannot simply use shadowmaps for this light type. Screen Space Ambient Occlusion is applied to get contact shadows from nearby geometry.

| Property | Description |
| --- | --- |
| **Tint** | Use a RGB color value to apply a color on top of the assigned cubemap texture. |
| **Intensity** | Scales the brightness of the assigned Ambient Cubemap texture. 0 is off. |
| **Cubemap Texture** | Assign a cubemap to this Post Process Volume that blends additively to objects in the scene. |

### Ambient Occlusion

The **Ambient Occlusion** properties control the screen space effect called Screen Space Ambient Occlusion (SSAO), which approximates the attenuation of light due to self-occlusion. This is a screen space effect that is limited to information available within the current view. Ambient Occlusion is generally used as a subtle effect, in addition to global illumination, that darkens corners, crevices, and other features to bring a more natural, realistic look to the scene.

![Screen Space Ambient Occlusion: Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f15b180f-6c3c-4dbd-ad47-4b8cd032a133/ssao-enabled.png)

![Screen Space Ambient Occlusion: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c234a646-e228-4a0c-a9de-260a59ed2fa2/ssao-disabled.png)

| Property | Description |
| --- | --- |
| **Intensity** | Defines how much ambient occlusion affects non-direct lighting after the base pass. |
| **Radius** | Affects the distance around objects that surfaces are affected. Larger values affect distance objects. |
| Advanced Properties |   |
| **Static Fraction** | Affects how much ambient occlusion affects Static lighting. 1 affects static lighting, and 0 is free, meaning no extra rendering pass is used. |
| **Radius in WorldSpace** | When enabled, ambient occlusion Radius is measured in world space units, opposed to locked to the view space in 400 units. |
| **Fade Out Distance** | The distance at which ambient occlusion disappears in the distance. This can avoid artifacts and ambient occlusion effects happening on large objects. |
| **Fade Out Radius** | The radius at which ambient occlusion starts to fade out before the Fade out Distance property. |
| **Power** | Controls the strength of the darkening effect that is computed. |
| **Bias** | Adjusts the amount of ambient occlusion detail. Some bias is needed to avoid precision artifacts in the distance. A value of 3 works well for flat surfaces, but can reduce details. |
| **Quality** | Adjusts the quality and perceived accuracy of screen space ambient occlusion. |
| **Mip Blend** | Affects the blend over the multiple mips (or lower resolution versions). 0 uses full resolution. 1 uses only low resolution. values in between find a balance. |
| **Mip Scale** | Affects the ambient occlusion Radius scale over multiple mips. |
| **Mip Threshold** | Adjusts the bilateral upsampling when using multiple mips. |
| **Temporal Blend Weight** | How much to blend the current frame with the previous frames when using Ground Truth Ambient Occlusion with temporal accumulation. |

### Ray Tracing Ambient Occlusion

Requires that **Support Hardware Ray Tracing** and **DirectX 12** be enabled for the project.

**Ray Tracing Ambient Occlusion** (RTAO) accurately shadows areas to ground objects in the environment. Similarly to baked lighting, ambient shadowing is not screen space dependent. RTAO adds depth to the scene, producing natural looking shadowing in indirectly lit areas, such as under objects, or in corners and crevices.

![Screen Space Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35eb3127-5315-4c0b-87cb-bdea23f7efae/ao-screenspace.png)

![Ray Tracing Ambient Occlusion](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ba83086-2bab-4c42-98da-03e70f6d0307/ao-ray-traced.png)

| Property | Description |
| --- | --- |
| **Enabled** | Whether ray tracing ambient occlusion should be enabled for this Post Process Volume. |
| **Samples Per Pixel** | Sets the number of samples to use per pixel for ray tracing ambient occlusion. |
| **Intensity** | Scales the ray tracing ambient occlusion in the scene for this Post Process Volume. |
| **Radius** | Defines (in world space units) the search radius for occlusion rays for this Post Process Volume. |

For more information, see [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine).

### Motion Blur

**Motion Blur** is the blurring of objects based on its motion. In photography and film (like with a sequence of frames), motion blur is the result of an object moving before the image has been captured, creating the blurring effect that is seen. Depending on how fast the object is moving can determine how much motion blur there is for the object.

![motion blur](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e46bfac6-83c9-45ec-9a70-bee63a551473/motion-blur.png)

The motion blur system in the engine uses a full screen velocity map, and objects are blurred based on their contribution to this map. The following properties control the contribution of objects in the scene to the velocity map.

| Property | Description |
| --- | --- |
| **Amount** | The strength of motion blur. 0 is off. |
| **Max** | The maximum distortion caused by motion blur (in percent of the screen width). 0 is off. |
| **Target FPS** | Defines the target frames per second (fps) for motion blur. It makes motion blur independent of actual frame rate and relative to the specified target FPS results in shorter frames, which means shorter shutter times and less motion blur. Lower FPS means more motion blur. A value of 0 makes the motion blur dependent on the actual measured frame rate. |
| **Per Object Size** | The minimum projected screen radius for a primitive to be drawn in the velocity pass for motion blur consideration. The radius is a percentage of screen width. Smaller radii cause more draw calls. The default is 4%. |

Motion blur is visualized in the editor using the Level Viewport **Show > Visualize > Motion Blur**.

### Ray Tracing Translucency

This feature of ray tracing is deprecated and may be removed in a future release.

Requires that **Support Hardware Ray Tracing** and **DirectX 12** be enabled for the project.

The Post Process Volume settings enable you to decide how you want translucency to be rendered, with traditional raster translucency or ray-traced. **Ray Tracing Translucency** uses rays to trace the path of light through translucent materials based on real-world physical properties.

![Ray Tracing Translucency:Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8aa8bc9e-3494-4468-8d7e-f5364b8f1ab0/ray-tracing-transluency-enabled.png)

![Ray Tracing Translucency: Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d43670b-707d-4d89-af9d-34a005a07377/ray-tracing-transluency-disabled.png)

For more information, see [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine).

### Path Tracing

The **Path Tracer** is a progressive, hardware-accelerated rendering mode that produces physically correct global illumination, reflections, refractions, and more. It shares the same ray tracing architecture as [Hardware Ray Tracing](/documentation/en-us/unreal-engine/hardware-ray-tracing-in-unreal-engine) to create comparable results to offline renders.

When path tracing is enabled for the Level Viewport (View Modes > Path Tracing), the properties in the category enables you to configure how the path tracer accumulates samples and renders the frame.

For more information, see [Path Tracer](/documentation/en-us/unreal-engine/path-tracer-in-unreal-engine)

## Film Grain

**Film Grain** is an optical effect that simulates the look of processed photographic film. It can appear as tiny, randomized particles and adds a filmic look to the rendered frame.

| Property | Description |
| --- | --- |
| **Film Grain Intensity** | The amount of grain to apply to the scene. 0 is no film grain, and 1 is full film grain. |
| **Film Grain Intensity Shadows** | The amount of film grain to apply to shadowed areas of the scene. |
| **Film Grain Intensity Midtones** | The amount of film grain to apply to mid-toned areas of the scene. |
| **Film Grain Intensity Highlights** | The amount of film grain to apply to areas with highlights in the scene. |
| **Film Grain Shadows Max** | Sets a maximum range for film grain to be applied to shadowed areas of the scene. |
| **Film Grain Highlights Max** | Sets a maximum range for film grain to be applied to highlighted areas of the scene. |
| **Film Grain Texel Size** | Size of the texel of the film grain on the screen. |
| **Film Grain Texture** | Defines a texture to use for the film grain being applied. It can be used to create a specific look to the noise that film grain has. |