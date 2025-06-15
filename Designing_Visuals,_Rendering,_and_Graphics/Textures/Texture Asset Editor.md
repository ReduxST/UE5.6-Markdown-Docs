# Texture Asset Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:00

---

The **Texture Asset Editor** provides a means for you to preview a **Texture Asset** and edit its properties, such as previewing specific color channels, making color adjustments directly in the Editor, modifying compression properties, and much more. Texture Assets are often used in combination with the Material Editor but can be used directly with some components in Unreal Engine, such as applying a cubemap to a Sky Light.

## Types of Textures Assets

There are multiple supported texture file types you can import into or create in Unreal Engine. This can include standard image types (.png and .jpg), cubemaps (.exr), IES Profiles (.ies), volume textures, and render targets.

You can import and save each of these types of files as **Texture Assets** in the Content Browser. When you open one, depending on the type of texture it is, the Texture Asset Editor customizes the toolbar with texture-specific options.

## Opening a Texture Asset Editor

Double-clicking on any texture asset in the Content Browser or in an assignment slot of another asset, such as a Static Mesh, opens it in the **Texture Asset Editor**. Alternatively, in the Content Browser when you right-click on a texture, you can select **Edit** from the context menu to do the same thing.

[![Examples of texture assets in the Content Browser.](https://dev.epicgames.com/community/api/documentation/image/ac9b506b-21f8-48fb-b089-c700d479f6cf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ac9b506b-21f8-48fb-b089-c700d479f6cf?resizing_type=fit)

*Three example texture assets used for the ThirdPerson Template character Quinn.*

## Texture Asset Editor Interface

When you open a Texture Asset, the **Texture Asset Editor** will look similar to the example below. From this editor, you can preview the texture and make adjustments to the asset.

[![Texture Asset Editor interface.](https://dev.epicgames.com/community/api/documentation/image/f5f3a4eb-cd68-4307-8bb8-65fef039212c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f5f3a4eb-cd68-4307-8bb8-65fef039212c?resizing_type=fit)

The interface includes the following:

1.  [Toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine#toolbar)
    
2.  [Viewport](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine#viewport)
    
3.  Settings Panels:
    
    -   [Details Panel](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine)
        
    -   [Oodle Panel](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine)
        
    -   [Platform panel](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine#additional-notes)
        

### Toolbar

The **Toolbar** provides non-destructive tools and toggles to inspect and preview this texture. Depending on the type of texture asset (cubemap, volume, texture), the toolbar will display texture-specific options.

[![Texture Asset Editor Toolbar options](https://dev.epicgames.com/community/api/documentation/image/64f29e94-ecf6-4839-b69e-9d35c5d508a4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/64f29e94-ecf6-4839-b69e-9d35c5d508a4?resizing_type=fit)

*A cubemap texture opened with the Texture Asset Editor displaying many of the toolbars tools.*

| Toolbar Option | Description |
| --- | --- |
| 
**Compress**

 | 

Compress this texture.

 |
| 

**Reimport**

 | 

Reimports the texture from its source file.

 |
| 

**Color Channels (RGBA)**

 | 

Toggle which color channels are currently displayed by clicking them. When grayed out, that color channel is not shown in the preview window.

 |
| 

**Mip Level Selector**

 | 

Enabled the checkbox to enable mip selection. Use the dropdown to select a specific mip or use the +/- buttons to scroll through the mip levels.

 |
| 

**Exposure Bias**

 | 

For Cubemap / IES textures, use this setting to brighten or darken the source image.

 |
| 

**Slice**

 | 

When enabled, Texture2DArray or TextureCubeArray displays the array element with the specified index instead of the standard view where all the array elements are partially visible at the same time.

 |
| 

**Face Selector**

 | 

For Cubemap textures, enabling this checkbox allows you to preview individual faces that make up the cubemap texture.

 |
| 

**3D View**

 | 

For Cubemap textures, enabling this checkbox allows you to preview the cubemap as a 3D scene. Left-mouse click and drag the preview to rotate the view.

 |
| 

**Zoom**

 | 

Use the slider to scale the textures preview size. Use the dropdown to select predefined sizes along with setting scaling options for scaling it to fit or fill.

 |
| 

**View Settings**

 | 

This dropdown includes the following viewport options:

-   **Desaturation:** Toggles color desaturation.
    
-   **Background:** Sets whether the background area is checkered or a solid color in the preview window.
    
-   **Draw Border:** If enabled, a border is drawn around the texture in the preview window.
    
-   **Advanced Settings:** Open the Editor Preferences, the Texture Editor settings is where you can set things like the background color, size of the checkered tiles, and the border color around the texture.
    

 |

### Face Selector

Texture assets that are a cubemap, texture array, or volume texture include the **Face** option to view individual faces that make up that texture. For example, when you view a cubemap and enable the Face checkbox, you can view one of the six individual faces that make up the long-lat unwrap by entering an ID number into the text field.

The face of the cubemap displayed matches the DDS orientation and order: Positive X, Negative X, Positive Y, Negative Y, Positive Z, Negative Z.

### 3D View

Texture assets that are a cubemap, texture array, or volume texture include the **3D View** option to preview the texture in its intended 3D representation. You can rotate the view of the 3D representation by left-clicking the mouse and dragging in the preview window.

### Slice

Texture 2D Array and Texture Cube Array Assets store a set of specified Texture Assets in a single texture array. Use the **Details** panel to specify the **Source Textures** in a Texture 2D Array and Texture Cube Array. When you have assigned texture assets to all added slots, the preview will display the sliced preview in the viewport.

Use the **Slice** checkbox to preview the individual Texture Assets that make up the array.

### Viewport

The **Viewport** displays a preview of a Texture Asset. While most toolbar options are similar across all Texture Assets, such as RGBA toggles, exposure bias, and zoom amount, some textures offer additional options such as face selection and 3D view.

### Details Panel

The **Details** panel displays the properties and settings of the Texture you can edit.

#### Texture Information

The top-most section displays texture-specific data, such as its size in various ways, how much disk space it consumes, format, and so on. Below this section, you can make adjustments to this texture. Some of the settings you adjust are reflected in this texture information, such as the properties for Encode Speed and LOD Bias.

[![Texture Asset Editor texture information.](https://dev.epicgames.com/community/api/documentation/image/35450dfd-72d7-4675-bcf7-8674748164b9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/35450dfd-72d7-4675-bcf7-8674748164b9?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Imported**

 | 

The size of the source texture imported.

 |
| 

**Displayed**

 | 

The currently displayed texture size in the preview window.

 |
| 

**Max In-Game**

 | 

The maximum size this texture can be while in-game. This will not be larger than the source texture's imported size, but could be smaller depending on configuration and texture settings.

 |
| 

**Resource Size**

 | 

The amount of unaligned memory used by the raw texture data.

 |
| 

**Has Alpha Channel**

 | 

Specifies whether the texture is currently using an alpha channel or not. You can disable the texture's alpha channel through settings found in the Details panel, while the source texture still supports the alpha channel.

 |
| 

**Source Alpha Detected**

 | 

Specifies whether the source texture has an alpha channel or not.

 |
| 

**Method**

 | 

Specifies whether the current texture is using streaming or not.

 |
| 

**Format**

 | 

The compression setting format used for this texture.

 |
| 

**Combined LOD Bias**

 | 

Displays the bias set by **LOD Bias** towards a max mip level to use.

 |
| 

**Number of Mips**

 | 

The number of mip levels this texture uses. Higher resolution textures will have more mips than lower resolution textures.

 |
| 

**Encode Speed**

 | 

Displays the speed of encoding used for this texture, such as Fast, Final, or Custom (when using the Oodle panel).

 |

#### Level of Detail Settings

The **Level of Detail** section provides mip and LOD settings. During import of the texture, a mip map chain is created starting with Mip 0. The mip map chain consists of multiple levels of sample images, with each being half the resolution of the level before.

[![Texture Asset Editor details level of detail settings.](https://dev.epicgames.com/community/api/documentation/image/61f8ed45-7832-47ca-9176-9ad25820f45f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/61f8ed45-7832-47ca-9176-9ad25820f45f?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Mip Gen Settings**

 | 

Per Asset specific setting to define the mip-map generation properties, like sharpening and kernel size.

-   FromTextureGroup
    
-   SimpleAverage
    
-   Sharpen
    
-   NoMipMaps
    
-   LeaveExistingMips
    
-   Blur
    
-   Unfiltered
    
-   Angular
    

 |
| 

**LOD Bias**

 | 

A bias to the index of the top mip level to use.

 |
| 

**Texture Group**

 | 

The texture grouping this texture belongs to.

 |
| Advanced Properties |   |
| --- | --- |
| 

**Preserve Border**

 | 

When checked, the texture's border will be preserved during mip map generation.

 |
| 

**Downscale**

 | 

How much to downscale the source texture for textures without mips.

-   **0** uses the scale value from the Texture Group.
    
-   **1.0** does not scale the texture.
    
-   **\> 1.0** scales the texture.
    

 |
| 

**Downscale Options**

 | 

Downscaling options available when downscaling is used for textures without mips. Choose from:

-   Default
    
-   Unfiltered
    
-   Simple Average
    
-   Sharpen
    

 |
| 

**Num Cinematic Levels**

 | 

The number of mip levels to use when the scalability setting is set to Cinematic.

 |
| 

**Never Stream**

 | 

When enabled, this texture will never be streamed.

 |
| 

**Global Force Resident Mip Levels**

 | 

Global and serialized version of ForceMipLevelsToBeResident.

 |

##### Mipmapping

**Mipmapping** is the process of downscaling higher resolution textures to lower resolution ones through mip levels. Each mip level halves the resolution of the preceding one, enabling textures to have different levels of detail at farther distances — often where less detail is needed to maintain its look. This process saves rendering time by using lower resolution textures, and reduces occurrences of artifacts.

Mip mapping generates as many mips as are needed based on the size of the source texture. For example, if the texture is 1024 x 1024, it will have ten mip levels. If the texture is 4096 x 4096, it has twelve mip levels.

[![Example of mip levels.](https://dev.epicgames.com/community/api/documentation/image/b268cd42-6f59-42c6-bca7-9417710f24b2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b268cd42-6f59-42c6-bca7-9417710f24b2?resizing_type=fit)

*Click image for full size.*

In the scene below, two materials are set up using their own diffuse and normal map textures. The material on the left has textures with no mip maps. The material on the right uses mip mapping. Notice how the material on the left causes undesirable aliasing in the far distance compared to the material on the right that uses mip maps. Lowering the resolution through mip levels also helps improve the overall look of the textures at these far distances as well.

[![Example of mipmapping compared with no mipmapping.](https://dev.epicgames.com/community/api/documentation/image/8d10b764-3716-405e-8e5c-c0601ed35b2d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8d10b764-3716-405e-8e5c-c0601ed35b2d?resizing_type=fit)

*Left, material with textures with no mips; Right, material with textures using mips.*

Zooming in on the two materials, you can see the different mip mapping has in reducing aliasing.

[![Zoomed in example of mipmapping compared with no mipmapping.](https://dev.epicgames.com/community/api/documentation/image/c0ade6a7-a262-45ec-bdb5-4e3d69a72b7a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c0ade6a7-a262-45ec-bdb5-4e3d69a72b7a?resizing_type=fit)

*Left, material with textures with no mips; Right, material with textures using mips.*

You can view individual mip levels by checking the box next to the **Mip Level** selector. When enabled, choose a mip level from the dropdown menu.

When selecting a mip level, it will automatically switch to that mip in the viewport and in the **Details** panel's texture information section, the currently **Displayed** size will change to reflect the selected mip level's size.

#### Compression Settings

The **Compression** category provides configurable settings for quality that affect the amount of compression applied to the texture and ultimately its size on disk.

[![Texture Asset Editor details compression settings.](https://dev.epicgames.com/community/api/documentation/image/344eea6f-e6fb-4834-83d5-603fe7cfad4b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/344eea6f-e6fb-4834-83d5-603fe7cfad4b?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Compress without Alpha**

 | 

If enabled, force the texture's alpha channel to be opaque for any compressed texture output. Does not apply if the output format is uncompressed RGBA.

 |
| 

**Editor Show Final Encode**

 | 

If enabled, compress the texture with final quality during this Editor session, making it use the Final level (RDO) encoding rather than the Fast level (non-RDO) which would be the default. This enables you to visually inspect the RDO encoding which will be used in the game.

 |
| 

**Editor Defer Compression**

 | 

If enabled, defer compression of the texture until save or manually compressed in the texture editor.

 |
| 

**Compression Settings**

 | 

Compression settings to use when building the texture. Choose a compression method from the dropdown.

 |
| Advanced Properties |   |
| --- | --- |
| 

**Maximum Texture Size**

 | 

The maximum resolution for generated textures. A value of 0 means the maximum size for the format on each platform.

 |
| 

**Lossy Compression Amount**

 | 

Controls Oodle Texture RDO Lambda (the compression factor) per texture. The project has an overall RDO quality level, but in some cases, it needs to be adjusted per-texture. You can use this to turn RDO off, or to increase / decrease the trade off quality with the compression ratio.

 |
| 

**Oodle Texture SDK Version**

 | 

This selects the version of the Oodle Texture libs to use for encoding a texture. When you create new textures, this is set to the current version and it stays with that version so that future updates don't cause patches. In some cases, you may want to change a texture to use the latest version to fix an encoding issue. You can enter "latest" in the numeric field to update. If you leave the field blank, the legacy fallback for the project is used. When you reimport a texture, it is automatically updated to use the latest SDK version.

 |
| 

**ASTC Compression Quality**

 | 

The compression quality for generated ATSC textures, such as those mobile platform textures. Use the dropdown to set the quality.

 |
| 

**Compression Cache ID**

 | 

Change this optional ID to force the texture to be recompressed by changing its cache key.

 |
| 

**Cook Platform Tiling Settings**

 | 

If the platform supports it, tile the texture when cooking, or keep it linear and tile it when it's actually submitted to the GPU.

 |

#### Texture Settings

The **Texture** category provides configurable settings for handling the texture asset which can affect its appearance and usage in materials or optimization methods, like [Texture Streaming](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-streaming-in-unreal-engine).

[![Texture Asset Editor details texture settings.](https://dev.epicgames.com/community/api/documentation/image/288f6c3a-a4da-4853-88aa-81a17a2fb4a0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/288f6c3a-a4da-4853-88aa-81a17a2fb4a0?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Power of Two Mode**

 | 

How to pad the texture to a power of 2 size (if necessary).

-   **Pad to Power of 2:** Pad the texture to the nearest power of 2 size.
    
-   **Pad to Square Power of 2:** Pad the texture to the nearest square power of 2 size.
    

 |
| 

**Padding Color**

 | 

The color used to pad the texture out if it is resized due to **Power of Two Mode**.

 |
| 

**sRGB**

 | 

Specifies whether the texture and its source are in sRGB Gamma color space. This can only be used with 8-bit and compressed formats. This should be unchecked if using alpha channels individually as masks.

 |
| Advanced Properties |   |
| --- | --- |
| 

**X-axis Tiling Method**

 | 

The addressing mode to use for the X-axis. Choose from wrap, clamp, or mirror.

 |
| 

**Y-axis Tiling Method**

 | 

The addressing mode to use for the Y-axis. Choose from wrap, clamp, or mirror.

 |
| 

**Do Scale Mips for Alpha Coverage**

 | 

Specifies whether mip RGBA should be scaled to preserve the number of pixels with values greater than or equal to **Alpha Coverage Threshold**. If this is unchecked, alpha coverage thresholds are ignored.

 |
| 

**Alpha Coverage Threshold**

 | 

The alpha values per channel to compare when preserving alpha coverage. 0 means the channel is disabled. Typical good values are in the 0.5 to 0.9 range, and not 1.0.

 |
| 

**Use New Mip Filter**

 | 

When enabled, it uses a faster mip generation filter with usually the same result. In rarer cases, the new filters can cause chroma shifts that the old filters didn't. If that's the case, disable this feature.

 |
| 

**Flip Green Channel**

 | 

When enabled, the texture's green channel will be inverted. This is useful for some normal maps.

 |
| 

**Filter**

 | 

The texture filtering mode to use when sampling this texture. Choose from:

-   Nearest
    
-   Bi-linear
    
-   Tri-linear
    
-   Texture Group (default)
    

 |
| 

**Mip Load Options**

 | 

Choose how the texture mips should be loaded with:

-   **Default** falls back to the LODGroup settings.
    
-   **All Mips** load all mips in the texture.
    
-   **Only First Mip** loads only the first mip in the texture.
    

 |
| 

**Normalize after making Mips**

 | 

This setting affects normal maps only. It normalizes colors in normal maps after mip generation for better and sharper quality. When mip maps are made for normal maps, the normals are blended together, which has a tendency to make them shorter (unnormalized). When you put them into an encoding, such as BC5, that drops components, you should normalize them before dropping components. Failing to do this means that the normal detail goes away in mip maps, making them flatter or softer in the distance mip levels.

The softening at distances is different from intentional softening which you can do using the composite normal to roughness transform.

This setting does not affect the top mip level, only lower mip levels. Turning this on should make normal maps in the distance look shaper (more correct).

 |
| 

**sRGB Use Legacy Gamma**

 | 

When enabled, it uses a simplified legacy gamma space, such as pow(color, 1/2.2), for converting from FColor to FLinearColor, if doing sRGB.

 |
| 

**Source Color Settings**

 | 

Texture color management settings for source encoding and color space.

-   **Encoding Override:** The source encoding of the texture, exposing more options than just sRGB.
    
-   **Color Space:** The source color space of this texture.
    
-   **RGBA Chromaticity Coordinate:** The individual color channel chromaticity coordinate of the source color space. Can be specified individually for the red, green, blue, and white channels.
    
-   **Chromatic Adaptation Method:** The method applied if the source white point differs from the working color space white point.
    

 |
| 

**Virtual Texture Streaming**

 | 

Enable if you are streaming this texture using Virtual Texturing.

 |
| 

**Asset User Data**

 | 

An array of user data stored with this asset.

 |

#### Texture Adjustment Settings

The **Adjustment** category provides configurable properties to edit your texture in a non-destructive way without having to leave the Texture Editor, such as adjusting its brightness, vibrance, saturation, and more.

[![Texture Asset Editor details adjustment settings.](https://dev.epicgames.com/community/api/documentation/image/bc4bb7a8-d8af-468d-a0e0-b9b16a8f8d2f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bc4bb7a8-d8af-468d-a0e0-b9b16a8f8d2f?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Brightness**

 | 

Adjusts the texture brightness by scaling the HSV value. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**Brightness Curve**

 | 

Adjusts the texture curve by raising the HSV value to a specified power. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**Vibrance**

 | 

Adjusts the intensity of muted colors while leaving saturated colors alone using an HSV saturation algorithm. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**Saturation**

 | 

Adjusts the saturation by scaling HSV saturation. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**RGBCurve**

 | 

Adjusts the texture RGB curve by raising linear-space RGB color to the specified power. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**Hue**

 | 

Adjusts the texture hue (between 0 to 360) by offsetting HSV hue by a value in degrees. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**Min Alpha**

 | 

Remaps the alpha to the specified min/max range and defines the new value of 0. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**Max Alpha**

 | 

Remaps the alpha to the specified min/max range and defines the new value of 1. This is a non-destructive adjustment and requires the source art to be available.

 |
| 

**Chroma Key Texture**

 | 

Whether to chroma key the image, replacing any pixels that match the **Chroma Key Color** with transparent black.

 |
| 

**Chroma Key Threshold**

 | 

The threshold that components have to match for the texel to be considered equal to the **Chroma Key Color** when chroma keying. To require an exact match, the value must be less than or equal to 0.

 |
| 

**Chroma Key Color**

 | 

The color that will be replaced with transparent black if chroma keying is enabled.

 |

#### Compositing Settings

The **Compositing** category provides settings for handling compositing with this texture and how its applied.

[![Texture Asset Editor details compositing settings.](https://dev.epicgames.com/community/api/documentation/image/ba222a7c-7ef7-4da4-8acf-2ab0798b094e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ba222a7c-7ef7-4da4-8acf-2ab0798b094e?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Composite Texture**

 | 

Can be defined to modify the roughness based on the normal map variation (mostly from mip maps). Max Alpha is helpful to define a base roughness if no source alpha is there. The normal map should have at least as many mips as this texture.

 |
| Advanced Properties |   |
| --- | --- |
| 

**Composite Texture Mode**

 | 

Defines how the **Composite Texture** is applied. For example, CTM\_RoughnessFromNormalAlpha.

 |
| 

**Composite Power**

 | 

Controls how strong the compositing effect is. The default is 1 and higher whole number values (1, 2, 4, 8) result in a stronger effect. This is not a slider because the texture update would not be fast enough.

 |

#### Oodle Panel

The **Oodle** panel provides information about the current settings affecting this texture, and lets you see how the Rate Distortion Optimization (RDO) encoding options will affect the compressed size on disk.

#### Oodle Texture Encoding Information

The top-most section of the Oodle panel displays information about how the texture is encoded. This is a good place to check whether RDO is on or off when diagnosing potential artifacts.

[![Texture Asset Editor Oodle panel settings.](https://dev.epicgames.com/community/api/documentation/image/adb4de7b-8ed3-4569-84d3-dee0c0357220?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/adb4de7b-8ed3-4569-84d3-dee0c0357220?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Encoder**

 | 

The name of the encoder used for the texture.

 |
| 

**Encode Speed**

 | 

Specifies whether the texture was encoded with Fast or Final encoding settings.

 |
| 

**RDO Lambda**

 | 

The RDO lambda value used for this texture. RDO lambda controls how much Oodle should trade image quality for distribution sizes. This is **not** memory usage.

 |
| 

**RDO Lambda Source**

 | 

Where the RDO lambda value comes from. Lambda values can come from Project Settings, the texture level of detail (LOD) group's Lossy Compression Amount, or the texture's Lossy Compression Amount.

 |
| 

**Effort**

 | 

The encoding effort used, which refers to how much CPU time Oodle spent trying to find a higher quality result.

 |
| 

**Universal Tiling**

 | 

When enabled, Oodle adjusts its RDO calculations to consider that the texture will get tiled for console platforms. This has no effect for non-RDO encodes. For example, RDO Lambda must not be **0**. This has no effect if you are not distributing on consoles.

 |

#### Try Encodings

The **Try Encodings** provide a means for you to experiment with various texture encoding settings to see how they affect this specific texture.

These changes are visible while playing in the editor but are not saved or used once the Texture Asset Editor is closed. For these changes to be permanent, you need to update the settings in the **Project Settings**. Some settings are not configurable per-texture, such as Effort and Universal Tiling.

[![Texture Asset Editor Oodle Try Encodings settings.](https://dev.epicgames.com/community/api/documentation/image/75179d09-825d-4700-951a-9c22c3aa650b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/75179d09-825d-4700-951a-9c22c3aa650b?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Enabled**

 | 

If checked, allows you to experiment with Oodle Rate Distortion Optimization (RDO) compression settings to visualize results.

 |
| 

**RDO Lambda**

 | 

The Rate Distortion Optimization (RDO) lambda to encode for experimentation. 0 disables RDO entirely. 1 is the largest file size, and 100 is the smallest.

 |
| 

**Effort**

 | 

The encoding effort to try. Effort controls how much CPU time is spent on finding better results. See the [Oodle Texture documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-oodle-in-unreal-engine) for more information.

 |
| 

**Universal Tiling**

 | 

The universal tiling to try. See the [Oodle texture documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-oodle-in-unreal-engine) for more information.

 |

#### On-disk Sizes

The **On-disk Sizes** shows the benefits of RDO encoding for your texture by pulling the compression settings for your project and using those to compress the texture bits in a manner **similar to** how it happens during actual packaging of your project.

This is not exact! However, when combined with the **Try Encodings** section settings, it gives you an idea of the scale of benefits you can expect for different RDO lambda values.

[![Texture Asset Editor Oodle On-disk Sizes settings.](https://dev.epicgames.com/community/api/documentation/image/ca3e6e7d-b601-48e6-ba2f-b7bef3654db8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ca3e6e7d-b601-48e6-ba2f-b7bef3654db8?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Enabled**

 | 

If checked, texture data will be compressed in the same manner as project packaging in order to estimate the benefits of Rate Distortion Optimization (RDO) encoding of the texture.

 |
| 

**Packaging Configuration**

 | 

Specifies which set of packaging settings to use from Project Settings under **Project > Packaging > Advanced > Compressor Effort Level**. Generally, this should be left at Distribution. Choose between **Debug Development**, **Test Shipping**, and **Distribution**.

 |
| 

**Oodle Compressor**

 | 

The Oodle **Data** compressor used on this texture.

 |
| 

**Oodle Compression Level**

 | 

The compression level for the Oodle compressor. This is the corresponding name for the numeric value specified in the Compressor Effort Level in the Project Settings. It represents how much time Oodle spends trying to get smaller results.

 |
| 

**Compression Block Size**

 | 

The chunk size passed to Oodle Data during packaging. You control this in the Project Settings under **Packaging > Advanced > Package Compression Commandline Options** with `-compressionblocksize=`. The default block size is 64kb if one is not set.

 |
| 

**Uncompressed Size**

 | 

How big the texture is without any packaging compression. If you disable packaging compression, this is the size you get.

 |
| 

**Compressed Size (Estimate)**

 | 

How big the texture is likely to be after compression. As the RDO lambda gets larger, this should get smaller.

 |

#### Platforms Panel

The **Platforms** panel provides information on various texture properties that get "resolved" on a per-platform basis. These properties can be influenced by several factors which can make predicting the result difficult without doing a full cook and examining the output on an actual running game with a command like `listtextures`.

[![The resolved setting for each platform supported by the project is displayed.](https://dev.epicgames.com/community/api/documentation/image/3c862f1b-87ac-4d62-b862-ba34b52ebc08?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3c862f1b-87ac-4d62-b862-ba34b52ebc08?resizing_type=fit)

The resolved setting for each platform supported by the project is displayed.

##### Properties

Texture Format is the underlying texture encoder used and the requested pixel format.

**Pixel Format** is the actual final pixel format selected by the texture format. In some cases, this requires knowing whether the texture source has alpha information or not. In these cases, you can go to the Details panel and click Detect button next to Source Alpha Detected.   

[![](https://dev.epicgames.com/community/api/documentation/image/e328195d-acef-4321-b464-5a109a50fc2a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e328195d-acef-4321-b464-5a109a50fc2a?resizing_type=fit)

**LODBias** is the final resolved level of detail bias that will be used for the texture. 

**Size** is the final size of the top mip for the texture after applying LOD bias. 

**Mips** is the number of mips in the texture, as well as how many of these mips are streaming, optional, or inlined. Additionally, if the platform packs mip tails together, the number of mips in that tail is displayed.

[![](https://dev.epicgames.com/community/api/documentation/image/539b1d57-2382-4f73-9cab-f84125b582ee?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/539b1d57-2382-4f73-9cab-f84125b582ee?resizing_type=fit)

**Optional / Streaming / Inline** are the byte count totals for the encoded texture. Hovering over any of these will show the breakdown for the entire mip chain, showing which mips are dropped due to LODBias, which are in separate optional iostore containers, which will be streamed off of disk, and which will be loaded as part of the initial texture load (inline).

[![](https://dev.epicgames.com/community/api/documentation/image/5ff7b740-4e0e-46c6-9774-08eec9692212?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5ff7b740-4e0e-46c6-9774-08eec9692212?resizing_type=fit)

For this platform, the top mip will be dropped (X), the next 5 will be streamed (S), and the remainder will be inline (I). Optional mips would be indicated with an "O".

Due to platform alignment requirements and / or block sizes of the underlying pixel formats, the sizes might not be what you expect. This is especially noticeable for inline mips and packed mip tails, as the entire mip tail must be inline.

## Additional Notes

The following are some additional notes that are useful when working with textures in your project. These include best practices and optimizations you can make to improve textures in your project.

#### BC6 and BC7 Compression

Consider the following when using BC6 and BC7 compression for your textures:

-   We recommend using HDR Compressed (BC6) and BC7 since they have good best-fit mappings for mobile targets that don't support them natively. For example, BC6 will map to RGBA16F and BC7 will map to ASTC 4x4 which is not natively supported.
    
-   HDR Compressed/BC6H is high quality and should be used instead of uncompressed HDR (RGBA16F) except where quality dictates. HDR compressed is 8x smaller in GPU memory than HDR (RGBA16F).
    
-   BC7 is higher quality than BC1 (AutoDXT) and takes 2x as many bytes for RGB (non-alpha) images. BC7 is a good choice for images that do not encode well in BC1, such as when there are unrelated mask images packed into different color channels.
    
-   BC7 with alpha (RGBA) takes the same number of bytes as BC3 (AutoDXT with alpha, also called DXT5). It can be higher quality at the same size in GPU memory.
    
    We do not recommend changing existing BC3 usage habits to BC7 at this time, but it is an option for specific textures that could benefit from doing so.
    

#### Non-Power of 2 Mip Maps

Non-power of 2 textures support mip maps. However, power of 2 textures is still required in order for them to texture stream. The top mip map level must be a multiple of 4 in order to use texture compression. Non-power of 2 textures have their **Mip Gen Settings** automatically set to **NoMipMap** at time of import. To enable mip maps for non-power of 2 textures, change the **Mip Gen Settings** to another from the dropdown list.

#### Float32 Import and GPU Texture Formats

You can import and store 32-bit float image data in the UASSET. Previously, this would automatically be converted to a 16-bit float at time of import. You can also choose 32-bit float images as a GPU texture format. However, 32-bit float is not available on all GPUs and mobile only supports point-sampled 32-bit float images. If you don't set the texture to the **Nearest** filter on those targets, the texture will be converted to a 16-bit float.

#### Import and Export Pixel Format Support

Consider the following Import and Export options for textures:

-   Importing and exporting supports a variety of pixel formats and usually stores the imported pixels losslessly in the UASSET (without conversion). Import HDR either imports the image as a 2D texture or a LatLong Cubemap. Export gives you output formats that can store the texture data without any conversion. If you're not sure, use the DDS export output format since it stores all the Unreal Engine UASSET formats natively.
    
-   You can import a JPEG, store it as a JPEG in the TextureSource, and export the original JPEG back out losslessly. It will be lossless in the sense that you get the same JPEG back out, but no additional loss is created as a result. You retain the original lossiness of the JPEG format before import.
    
-   You can import textures up to 32768 x 32768 (without UDIM) as [Virtual Textures](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-texturing-in-unreal-engine).
    

#### Texture Arrays

You can make Texture Arrays from source images of varied formats and sizes (they don't have to all match). Sizes are unconstrained and image sizes will be stretched to match the largest image in the array.

#### Fast and Final Encode

This mainly impacts the Oodle Texture RDO, which makes textures more compressible in packages.

The Oodle Texture encoding includes two sets of options and speed levels with **Fast** and **Final**. For many projects, the Final level encode is set to RDO encode, which is used for cooking. The Fast encode is non-RDO. In the editor, Final RDO textures are loaded if they are available, such as from a shared DDC or a cook, but newly imported textures are encoded with the Fast non-RDO option for speed. If you work with an existing texture which was Final encoded and you modify it, it changes to Fast encoded. This may cause it to visually change as you are no longer seeing the RDO encoding.

The Fast and Final settings for your project are found in the **Project Settings** under **Engine > Texture Encoding**.