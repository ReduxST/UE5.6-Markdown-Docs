# Impostor Baker Plugin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/impostor-baker-plugin-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/impostor-baker-plugin-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:33

---

The Impostor Baker plugin provides a way to bake out simplified representations of complex geometry for use in far-distance rendering as level of detail (LOD) meshes. There are three main types of impostors that you can generate using the Imposter Baker:

-   **Full Sphere Impostor** to capture and render views for all angles around the object.
    
-   **Upper Hemisphere Impostor** to only capture and render views from above the terrain. This option provides better quality for objects that typically sit on terrain and cannot be viewed from underneath from very far away. This saves on processing resources by not rendering views that are not used.
    
-   **Traditional Billboards LOD** uses the older technique of capturing images around fixed horizontal angles and a single image from above to represent the top view. These images are each placed on their own sprite card and based on the viewing angle. Cards facing away fade using a dither effect.
    

The first two types of imposter are based on the same technique. The tool captures a specified number of views around the object. When rendering, the impostor material finds the three captured frames closest to the current camera view, and blends between them to come up with a representation that more closely matches the actual view angle. These three frames are rendered onto a single sprite plane.

Imposters provide a smoother and more realistic simulation of 3D geometry by always rendering a single blended sprite frame from the perspective of the viewer, when compared with billboards which use specific fixed-perspective sprite planes that won't look entirely correct from some angles. The video below demonstrates this difference.

*Left: Impostor; Right: Billboards.*

In Fortnite Battle Royale (FNBR), we use Upper Hemisphere Imposters for all of our trees when [Nanite](designing-visuals-rendering-and-graphics\rendering-optimization\nanite) is disabled.This provides better quality for our trees spread over the island that are viewed from far away.

## Comparing Imposters to Billboards

The difference between an Imposters and Billboards is that Imposters use a sprite card that contains 8 triangles with 9 vertices, and Billboards use 8 cards that contain 72 triangles with 81 total vertices. This means that Billboard representations have eight times the number of vertices and triangles to represent as that of an Imposter.

Impostors are generally much faster to render than billboards because they contain fewer vertices, even though the pixel shader is more expensive for imposters due to blending the three nearest frames — impostor rendering for mobile falls back to a single frame sample. Billboards still have worse overdraws for their masked materials. The main advantage for using billboards is you can get more resolution in the texture because only nine views are captured (in a 3x3 grid).

For distance foliages, we use a value of 12 for the imposter's XY frame distribution. We do this for most assets in Fortnite Battle Royale. This results in 12 frames by 12 frames for a total of 144 frames used.

### Enabling the Imposter Baker Plugin

Before you begin, enable the **ImposterBaker** plugin in Unreal Engine for your project. You can do this by opening the **Plugins** browser from the **Edit** menu. The plugin is located under the **BUILT-IN > Mesh** category.

[![](https://dev.epicgames.com/community/api/documentation/image/e4867ee6-37e0-47ea-8ea9-bc896cf38984?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e4867ee6-37e0-47ea-8ea9-bc896cf38984?resizing_type=fit)

## Changes to the Impostor Baker Plugin in Unreal Engine 5.5 and later versions

There are newer features to the Impostor Baker that make it easier to use while also covering more use cases. These improvements include:

-   Impostor Baker can now render using GBuffer without needing a material switch placed on material assets.
    
-   Impostor Baker can now render out all color maps and scalar maps that materials use, and channel pack the scalar maps in any combination you specify.
    
-   Impostor Baker now includes a full assets editor for rendering and tweaking values which can be saved automatically to data assets as 'Presets'.
    
-   You can now automatically save texture and mesh data directly to the source asset with one click.
    
-   Impostor Baker now includes a batch-renderer that can render impostors for multiple meshes using the specified Preset and save them all out.
    
-   You can now toggle between **No Parallax**, **Single BumpOffset Parallax**, and **Full Iteration Parallax** directly from the Impostor Editor or the resulting material instance.
    

## Using the Impostor Editor

The sections below describe the various sections of the Impostor Baker editor.

### Impostor Editor Widget

The Impostor Editor widget gives you full control to customize and create your impostor.

[![](https://dev.epicgames.com/community/api/documentation/image/2e5ee53f-4453-4571-b8f0-de6d8578ca72?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2e5ee53f-4453-4571-b8f0-de6d8578ca72?resizing_type=fit)

### Preset Widget

Generating impostors using the **Preset** widget provides a way for you to generate and save multiple impostors at once.

[![](https://dev.epicgames.com/community/api/documentation/image/752f555c-0940-4de8-b992-acb08b628345?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/752f555c-0940-4de8-b992-acb08b628345?resizing_type=fit)

To access either of these widgets, right click any **Static Mesh** asset in the Content Browser and select the **Scripted Asset Actions > Impostor Baker** option.

[![](https://dev.epicgames.com/community/api/documentation/image/5877527a-a4f9-4a92-8033-681c9f1326d8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5877527a-a4f9-4a92-8033-681c9f1326d8?resizing_type=fit)

### Preset DataAsset

The **Preset DataAsset** contains all the defaults initialized when you open the Impostor Editor. This saves time when you repeatedly render many impostors by keeping the settings consistent (see below for descriptions of the individual settings).

[![](https://dev.epicgames.com/community/api/documentation/image/4244d26d-3a12-487f-80c4-1b9f3314fd55?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4244d26d-3a12-487f-80c4-1b9f3314fd55?resizing_type=fit)

You can change your current **Settings Preset** using the buttons above it, as follows:

-   **Load Settings:** Applies the settings from the DataAsset to the Impostor Editor.
    
-   **Apply to DataAsset:** Applies the current Impostor Editor settings to the DataAsset.
    
-   **New DataAsset:** Creates a new DataAsset in the path specified under **Asset Saving**.
    

You can specify which DataAsset to use by default when launching the Impostor Editor or Preset Renderer in your project's `DefaultEditor.ini` (located at `\(Your Project Root)\config\DefaultEditor.ini`). Include the following information in the `.ini` file:

C++

`[/ImpostorBaker/BP/EUW_Impostor_Editor.EUW_Impostor_Editor_C] DefaultSettingsAssetPath=/Game/ImpostorPresets  [/ImpostorBaker/BP/EUW_Generate_Impostor_using_Preset.EUW_Generate_Impostor_using_Preset_C] DefaultSettingsAssetPath=/Game/ImpostorPresets`

\[/ImpostorBaker/BP/EUW\_Impostor\_Editor.EUW\_Impostor\_Editor\_C\] DefaultSettingsAssetPath=/Game/ImpostorPresets \[/ImpostorBaker/BP/EUW\_Generate\_Impostor\_using\_Preset.EUW\_Generate\_Impostor\_using\_Preset\_C\] DefaultSettingsAssetPath=/Game/ImpostorPresets

Copy full snippet(5 lines long)

Then change the **DefaultSettingsAssetPath** to point to a data asset you have created in your project (or the default installed with the plugin).

### Bake Settings

The **Bake settings** section contains the main settings that affect impostor generation.

[![](https://dev.epicgames.com/community/api/documentation/image/7968cb87-b85c-441a-b0fd-275c1df62098?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7968cb87-b85c-441a-b0fd-275c1df62098?resizing_type=fit)

| Bake Settings | Description |
| --- | --- |
| 
**Static Mesh**

 | 

Determines which static mesh asset to generate an impostor for.

 |
| 

**FramesXY**

 | 

Determines how many subframes on each axis to generate. For example, a value of 16 would create 16x16=256 subframes.

 |
| 

**Color Maps to Render**

 | 

Determines which full color maps the impostor baker will render for your impostor. The majority of impostors only require BaseColor and Normal. The full list of color map output options is as follows:

-   BaseColor
    
-   Normal
    
-   Emissive
    
-   Subsurface
    
-   Tangent
    
-   CustomLighting
    
-   Lit
    

[![](https://dev.epicgames.com/community/api/documentation/image/7ad6899c-834c-4595-a9f8-38884190d31d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7ad6899c-834c-4595-a9f8-38884190d31d?resizing_type=fit)



 |
| 

**Channel Packed Masks**

 | 

Provides for rendering of custom Scalar maps and packing the results together into different color channels in a single texture. The options are:

-   Specular
    
-   Roughness
    
-   Metallic
    
-   Opacity
    
-   Opacity Mask
    
-   Depth, Anisotropy
    
-   Clear Coat
    
-   Clear Coat Roughness
    
-   None (leaves channel blank)
    
-   If None is specified for the Alpha channel, the resulting texture will have no alpha and use DXT1 compression instead of DXT5.
    

[![](https://dev.epicgames.com/community/api/documentation/image/9b1abaa1-a9c6-424f-80fd-1d2d496a84cd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b1abaa1-a9c6-424f-80fd-1d2d496a84cd?resizing_type=fit)



 |
| 

**Impostor Type**

 | 

Determines the type of impostor to render. The options are:

-   **Full Sphere Impostor:** Capture and render views for all angles around the object.
    
-   **Upper Hemisphere Impostor:** Only capture and render views from above the terrain.
    
-   **Traditional Billboards:** Uses the older technique of capturing images around fixed horizontal angles and a single image from above to represent the top view.
    

 |
| 

**Resolution**

 | 

The texture resolution to use for the resulting textures.

Epic Games uses a resolution of 2048 for its projects, such as Fortnite Battle Royal.



 |

### Material Settings

The **Material settings** section contains the settings for which material your impostor will use, and various settings to apply to the resulting material.

[![](https://dev.epicgames.com/community/api/documentation/image/1587063f-4b3a-4622-9e62-0f155c54e164?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1587063f-4b3a-4622-9e62-0f155c54e164?resizing_type=fit)

| Material Settings | Description |
| --- | --- |
| 
**Hemisphere Material**

 | 

Determines which parent material to use for your impostor. It is usually unnecessary for you to change this. The setting shows the correct default for each type based on the selected impostor type in the [Bake](https://dev.epicgames.com/documentation/en-us/unreal-engine/impostor-baker-plugin-in-unreal-engine) settings.

 |
| 

**Sharing Model Override**

 | 

Provides a way for you to change the current sharing model to any available shading model.

 |
| 

**Parallax Mode**

 | 

Toggles between three modes:

-   No Parallax
    
-   Single Sample Parallax: This is similar to Bump Offset, whereby this provides some illusion of depth in the material without adding additional triangles.
    
-   Iterative Parallax: The most expensive option, but useful while tweaking settings to rule out other differences, as a control.
    

 |
| 

**Constant Specular**

 | 

Sets the value to use for specular when there is no Specular map being rendered in the Channel Packed masks array. This option is hidden when a Specular map is rendered.

 |
| 

**Constant Roughness**

 | 

Sets the value to use for roughness when there is no Roughness map being rendered in the Channel Packed masks array. This option is hidden when a Roughness map is rendered.

 |
| 

**Constant Opacity**

 | 

Sets the value to use for Opacity when there is no Opacity map being rendered in the Channel Packed masks. This option is hidden when an Opacity map is rendered.

 |
| 

**Subsurface Color**

 | 

Sets the value to use for subsurface color when there is no Subsurface Color map being rendered. This color will be multiplied against the BaseColor as well as masked using the distance field alpha (which is stored in the opacity mask, in BaseColor Alpha). This option is hidden when a Subsurface Color map is rendered.

 |
| 

**Scatter Mask Min**

 | 

This sets the minimum value at which scattering takes effect, enabling distance field alpha to be used as a subsurface scattering mask for this imposter. This has the added benefit of bringing back some self-shadowing otherwise missing from the scattering.

 |
| 

**Scatter Mask Length**

 | 

This sets the value for how wide the edge gradient is for the scattering mask created using the distance field alpha. This has the added benefit of bringing back some self-shadowing otherwise missing from the scattering.

 |
| 

**Mask Offset**

 | 

This value expands or shrinks the offset of the mask created using the distance field alpha.

 |

### Billboard Settings

The **Billboard Settings** are only shown when the **Impostor Type** (located under the [Bake settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/impostor-baker-plugin-in-unreal-engine))is set to **Traditional Billboards**. Imposter Type provides some settings to specifically adjust billboards.

[![](https://dev.epicgames.com/community/api/documentation/image/3e9e2985-6998-4698-b1ed-c78f5d02e103?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3e9e2985-6998-4698-b1ed-c78f5d02e103?resizing_type=fit)

| Billboard Settings | Description |
| --- | --- |
| 
**Center XY On Mesh Pivot**

 | 

This setting is disabled by default. When disabled, the Static Mesh is captured with the camera rotating around the center of its bounds. This usually ensures the object stays within the captured frames. In some cases, specifically for trees, the actual center of the bounds may not be exactly at the pivot, which is usually where the tree trunk is. This can result in an artifact where you briefly see the ghost of slightly offset trunks together as the camera rotates around the resulting billboards. Enabling this setting forces the capture to center around the mesh pivot on the XY position, which corrects this artifact. This setting can cause issues if used on meshes that have their pivot not close to the center.

[![](https://dev.epicgames.com/community/api/documentation/image/63ae2251-5f73-4950-bfc2-f0063772de3e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/63ae2251-5f73-4950-bfc2-f0063772de3e?resizing_type=fit)

Left: disabled, Right: enabled





 |
| 

**Reference Plane Top**

 | 

Shifts the reference plane of the top facing card. The value is normalized from 0-1 where 0.5 represents the mesh's midpoint. When you modify this setting, position the top card at the widest part of the static mesh. For this example using a pine tree, the top card is pushed down some, which helps in reducing artifacts.

[![](https://dev.epicgames.com/community/api/documentation/image/35cbf579-67d9-4a6e-8d65-9b1b7c5bffa3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/35cbf579-67d9-4a6e-8d65-9b1b7c5bffa3?resizing_type=fit)

Before and after changing the Reference Plane Top value from 0.5 to 0.35.





 |
| 

**Reference Plane Sides**

 | 

This setting functions similarly to Reference Plane Top, but instead shifts the side planes along their normal. Usually there is no reason to adjust this setting, unless you are capturing a very dense object that occupies most of the bounds everywhere, and you have enabled parallax options.

 |
| 

**Use Sprite Vertex Shader**

 | 

This setting should only be enabled when enabling Parallax options. It causes the UVs to offset beyond the geometry’s bounds, which will show clipping. The example below demonstrates an extreme case where you can see clipping around the bottom of the mesh. Use this setting sparingly because its effects worsens masked overdraw.

[![](https://dev.epicgames.com/community/api/documentation/image/19c0ee3f-a2be-4651-8615-21cd586f8164?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/19c0ee3f-a2be-4651-8615-21cd586f8164?resizing_type=fit)

Demonstrating the effects of the Sprite Vertex Shader setting.





 |

There are additional billboard material instance values which control additional settings that are not exposed to the Blueprint, but these settings can still be adjusted in more advanced cases. The main categories are **Dithering** settings which define how much to dither the transition and **Vertex Shader** settings which define the threshold to remove cards as they begin to face away from the camera.

### Asset Saving Settings

The **Asset Saving settings** define where assets get saved to.

[![](https://dev.epicgames.com/community/api/documentation/image/40d3c83b-6764-4b98-9e83-176433b77180?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/40d3c83b-6764-4b98-9e83-176433b77180?resizing_type=fit)

| Asset Saving Settings | Description |
| --- | --- |
| 
**New Asset Path**

 | 

The folder location for textures and materials. By default, the path is relative to the static mesh. When the path is relative, you can begin the path with `../` to move up a folder level (or use `../../` to move up two folder levels, and so on).

 |
| 

**New Asset Texture Prefix**

 | 

This is the prefix prepended to the name of new Texture assets.

 |
| 

**New Asset MIC Prefix**

 | 

This is the prefix prepended to the name of the new [Material Instance Constant](https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) assets.

 |
| 

**Use Relative Path**

 | 

Sets the path relative to the source mesh. When this is false, the path should begin with `/Game/` to place assets in the project content folder, or the name of a plugin (for example, \` /ImpostorBaker/\` would place assets in the folder for this plugin). The engine warns you if you try to use an invalid path.

 |

The name of the static mesh asset will always be appended to the specified prefix, followed by the name of each map. For example, if you have a static mesh named `S_Tree_01`, the resulting BaseColor would be `T_Impostor_S_Tree_01_BaseColor` based on the values shown in the image above.

### Advanced Settings

The **Advanced** settings contain values that you do not often need to edit.

[![](https://dev.epicgames.com/community/api/documentation/image/78c1030f-3df9-4ba9-b921-bb0fab6d386e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/78c1030f-3df9-4ba9-b921-bb0fab6d386e?resizing_type=fit)

| Advanced Settings | Description |
| --- | --- |
| 
**Capture Using GBuffer**

 | 

When enabled, the GBuffer will be used to capture the impostor data. This works for all opaque and masked materials but does not work with translucency. If the source mesh contains any translucent materials, the Impostor Editor will warn you with red text in the viewport.

Previous versions of this plugin required you to place the material function "Impostor Capture Switch" into each material first. This is no longer required but may still be desirable in some cases. An example use case would be how we use this in Fortnite Battle Royale to modify a material to remove certain world-based coloration effects so that the imposter material can be dynamically colored after generation.



 |
| 

**Orthographic**

 | 

When true, the capturing is done using orthographic rendering. This setting should almost never be changed. Perspective rendering is almost never needed, because the material with parallax recreates accurate perspective later. However, there are certain material effects such as fresnel that cannot be captured properly using orthographic rendering, so this setting can be disabled for those cases.

 |
| 

**Camera Distance**

 | 

**Only used when Orthographic is disabled.** Sets the distance of the capture.

 |
| 

**Scene Capture Resolution**

 | 

The resolution to capture each sub-frame at. The value of this setting automatically rounds to the nearest power of 2 because certain parts of the process require a mip-map chain of the scene capture textures (specifically, generating the sprite geometry cutouts at the end). Set this value to at least twice the resolution of each subframe in the final texture, so the result is super-sampled. For example, if the final texture is 4096 with 16 XY frames, each sub-frame will be 256x256. The default Scene Capture Resolution of 512 means the sub-frames will be rendered at 200% screen percentage, which will produce better anti-aliased results.

 |
| 

**Show Floor In Preview Scenes**

 | 

Toggles showing a floor mesh in the viewport. Has no impact on results.

 |
| 

**Impostor Casts Shadows**

 | 

Toggles whether the impostor casts shadows in the preview viewport. This does not affect the capture process or resulting created assets.

 |
| 

**Shader Debug Mode**

 | 

Toggles a debug overlay on the material that shows the grid of all captured frames, and pinpoints the location of the camera ray through this grid for both the camera and the sunlight (by viewing a dithered shadow). The current "triangle" containing the 3 nearest view frames is also shown and is colored by the blend weight at that position.

[![](https://dev.epicgames.com/community/api/documentation/image/f97f3026-9456-4b59-9aa7-71748e1ec053?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f97f3026-9456-4b59-9aa7-71748e1ec053?resizing_type=fit)



 |
| 

**Show Debug Values**

 | 

Displays a new category of details settings called **Debug** that show a variety of debug information internal to the Impostor Editor (such as the Material Instance Dynamics being used, various statistics on bounds and pivots, and so on). Only useful for debugging issues.

 |
| 

**Show Render Targets**

 | 

Displays a new category of details settings called **Render Targets** showing all the various arrays of render targets for the different maps and scene capture mips. Potentially useful to inspect on occasion.

 |
| 

**Manual S RGB Retainer Box**

 | 

The Impostor Editor currently renders the FPreviewScene without a gamma curve due to a bug. This checkbox enables a workaround that uses a UMG retainer widget to apply an sRGB curve, and is enabled by default.

 |

### Preview Modes

You can control the Viewport in various ways to preview your impostors. By default, the viewport swaps between the source mesh and the rendered impostor according to configurable **Swap by Distance** value, but you can also set it to show both in a **Side-by-Side** view, and force **Impostor Only**:

[![](https://dev.epicgames.com/community/api/documentation/image/35303b54-127a-4c06-a6e0-ee45a0fb8932?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/35303b54-127a-4c06-a6e0-ee45a0fb8932?resizing_type=fit)

The side-by-side view is useful in combination with the View Mode settings, which you can use to find and display any differences between the source mesh and the impostor. This view is especially useful when you are trying to approximate a constant specular or roughness value without capturing those values.

Below is an example of the viewport showing the normals for both the impostor and the original source mesh together:

[![](https://dev.epicgames.com/community/api/documentation/image/c389388a-bb31-4b4b-8484-651b363d116a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c389388a-bb31-4b4b-8484-651b363d116a?resizing_type=fit)

You can rotate the sunlight by holding the L key and clicking and dragging the mouse. You can orbit the camera by left-clicking and dragging, or move it forward and backwards by right-clicking and dragging or using the mouse wheel:

[![](https://dev.epicgames.com/community/api/documentation/image/b2934eb5-947b-4f35-8277-891c91fc92fc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b2934eb5-947b-4f35-8277-891c91fc92fc?resizing_type=fit)

Rotating the sun, and manipulating the camera.

## Parent Materials

You can find the base parent material for impostors here in the Content Browser under **Engine/Plugins/ImposterBaker Content/Materials/Parents**. Open the one named **M\_Imposter** to inspect it.

The core of the impostor behavior, including one set of Channel Packed Masks, is assembled in one function here:

[![](https://dev.epicgames.com/community/api/documentation/image/397a5268-39e5-4972-bbb9-d5842161bf8c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/397a5268-39e5-4972-bbb9-d5842161bf8c?resizing_type=fit)

The section that passes in the values for the constant specular is just to the right of the function shown in the previous image, as shown below. This function also handles the built-in subsurface scattering that is masked by the distance field alpha:

[![](https://dev.epicgames.com/community/api/documentation/image/b09bcc7e-e0cd-48a3-8c47-507f252b2f16?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b09bcc7e-e0cd-48a3-8c47-507f252b2f16?resizing_type=fit)

### Optional Color Maps

The additional optional color maps you can render (Emissive, Subsurface, Tangent) are already connected to the material using this function. The tool automatically flips a static switch to enable the correct ones when they are rendered:

[![](https://dev.epicgames.com/community/api/documentation/image/02744adc-ec17-4797-a031-afd016a3c9ad?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/02744adc-ec17-4797-a031-afd016a3c9ad?resizing_type=fit)

You can add additional color maps, such as the Lit texture (which is not currently connected anywhere), or additional scalar maps beyond the four you get with the included Channel Packed texture, to the material by using the function shown below (which is present in the material below the functions described in the images above, just disconnected):

[![](https://dev.epicgames.com/community/api/documentation/image/67ac0b0a-08d1-4d6a-bf44-4080cd1cef97?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/67ac0b0a-08d1-4d6a-bf44-4080cd1cef97?resizing_type=fit)

### Scalar Maps

The additional scalar maps you can render such as Roughness, Specular, Clear Coat, and others are already connected using this material function, which also flips static switches automatically to enable whichever textures are rendered along with their corresponding color channel.

[![](https://dev.epicgames.com/community/api/documentation/image/2a17b927-5864-4728-ba87-47c01b965156?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2a17b927-5864-4728-ba87-47c01b965156?resizing_type=fit)

The parent material for the Traditional Billboards is located in the Content Browser in **Engine/Plugins/ImposterBaker Content/Materials**. Open the one named **M\_Billboard\_01\_Inst**. `/Script/Engine.Material/ImpostorBaker/Materials/Parents/M_Billboard_01_Inst`

It is set up exactly the same as the Impostor material above; you can refer to those images to understand the Traditional Billboards material layout. The material functions are named the same way, but they include `_Billboard` in the name. The logic is also essentially similar, only the internal details of the functions are different.

### Rendering without GBuffer

For capturing translucency or for special cases where you need to disable certain features during capture, you need to disable **Capture using GBuffer**, and place the material function **ImpostorCaptureSwitch** at the end of the graph that the mesh uses:

[![](https://dev.epicgames.com/community/api/documentation/image/30d66b66-68ef-4d26-90d9-3254221bc590?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/30d66b66-68ef-4d26-90d9-3254221bc590?resizing_type=fit)

If you disable **Capture using GBuffer** but do not include the **ImposterCaptureSwitch** material function, the captured imposter will render incorrectly with many artifacts. This is because the material will interpret base color and lighting as depth, which will then apply parallax to the output and produce many rendering errors.

For context about the severity of this problem, consider that the direct quote from the dev reads as follows:

*"If you uncheck Capture using GBuffer but do NOT include the above function in the materials, the captured impostor will basically look like a steaming ball of artifacty sadness, because the material will interpret base color and lighting as depth and will proceed to parallax it into a pixel-soup of busted oblivion.*

*Sad Impostor has a bad case of impostor syndrome today; its settings are not even valid."*

## Generating Multiple Impostors Using the Presets

You can generate imposters for multiple static meshes by selecting them, right-clicking and choosing **Scripted Asset Actions > Impostor Baker > Generate Impostor Using Preset** from the context menu.

When you have set your Settings Preset and decided what action to take if a static mesh already has an impostor at the last LOD, click **Generate and Save Impostors**.

[![](https://dev.epicgames.com/community/api/documentation/image/1d6d7c3a-2305-4d89-8305-6e06f7b5f89a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1d6d7c3a-2305-4d89-8305-6e06f7b5f89a?resizing_type=fit)

If you have set **Present Dialogue**, the process will pause if a pre-existing imposter is detected. This process will stay paused until you make a selection on the pop-up dialogue and choose an action to take, whether that’s to replace the last LOD, add a new LOD, or to skip this step entirely. This can also occur from within the Impostor Editor.

[![](https://dev.epicgames.com/community/api/documentation/image/19eec7ae-5936-4d5e-98c6-7829288baa5d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/19eec7ae-5936-4d5e-98c6-7829288baa5d?resizing_type=fit)

## Full Iterative Parallax Mode

The **Full Iterative Parallax** mode is capable of producing a render that is almost indistinguishable from the original mesh as long as the impostor captures the data for all the channels the original uses. It chooses the best ray result for each pixel from a neighbor frame to essentially trace around corners from the neighbors. This option is called **Depth Derived Weights**.

Here is an example comparing single parallax to iterative parallax using the color calibrator while capturing the specular, roughness, clearcoat, and metallic maps into one channel packed texture. This is a very demanding test that magnifies artifacts of blending.