# Exporting Unreal Engine Content to glTF

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf](https://dev.epicgames.com/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf)  
**Processed:** 2025-06-14 16:22:57

---

Use the **glTF exporter** to export individual **Assets** or the current **Level** to one of the following formats:

| Format | Description |
| --- | --- |
| JSON `.gltf` | 
Includes the following elements, saved separately in a directory you specify:

-   **Full scene description:** saved as a JSON-formatted, human-readable UTF-8 text file with the `.gltf` extension.
-   **Texture files:** saved to the format you specify, `.png`, `.jpeg`, and so on.
-   **Binary data files:** saved separate files with a `.bin` file extension.



 |
| Binary `.glb` | Combines the full scene description, all binary data, and all textures into a single self-contained binary file. |

This page explains how to export glTF files from the Unreal Editor UI. You can also export glTF files from the Editor using Blueprint, Python scripting, or C++. Runtime export without the Editor is also possible, but there are some limitations. For details, see [Scripting glTF Exports](/documentation/en-us/unreal-engine/scripting-gltf-exports-in-unreal-engine).

## What You Can Export

You can export the following types of Asset as glTF files:

-   Static Meshes
-   Skeletal Meshes
-   Animation Sequences
-   Levels
-   Level Sequences
-   Materials
-   Level Variant Sets

For more information about how the glTF exporter handles each of these Asset types, see [How the glTF Exporter Handles Unreal Engine Content](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content).

## Export an Asset

To export an Asset to glTF:

1.  In the **Content Browser**, right-click the Asset you want to export.
2.  From the right-click menu, select **Asset Actions > Export…** . A file save dialog opens.
3.  In the file save dialog, choose a name and location for the exported file. Make sure Save as type is set to `.gltf` or `.glb`, and click **Save**. The **glTF Export Options** dialog opens.
4.  Set the export options as needed. For more information, see [glTF Export Options Reference](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#gltfexportoptionsreference).
5.  Click **Save**.

## Export the Current Level

To export the all Actors in the current level to glTF:

1.  Do one of the following:
    
    -   From the main menu, select **File > Export All…** .
        
        or
        
    -   In the **Content Browser**, right click the Level Asset, and from the right-click menu, select **Asset Actions > Export…**
        
    
    A file save dialog opens.
    
2.  In the file save dialog, choose a name and location for the exported file. Make sure **Save as type** is set to `.gltf` or `.glb`, and click **Save**. The **glTF Export Options** dialog opens.
3.  Set the export options as needed. For more information, see [glTF Export Options Reference](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#gltfexportoptionsreference).
4.  Click **Save**.

## Export Part of the Current Level

To export a selection of Actors in the current level to glTF:

1.  Select one or more Actors in the current level.
2.  From the main menu, select **File > Export Selected…** . A file save dialog opens.
3.  In the file save dialog, choose a name and location for the exported file. Make sure **Save as type** is set to `.gltf` or `.glb`, and click **Save**. The **glTF Export Options** dialog opens.
4.  Set the export options as needed. For more information, see [glTF Export Options Reference](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#gltfexportoptionsreference).
5.  Click **Save**.

## glTF Export Options Reference

The glTF Export Options dialog includes the following options:

-   [General Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#generaloptions)
-   [Material Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#materialoptions)
-   [Mesh Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#meshoptions)
-   [Animation Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#animationoptions)
-   [Texture Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#textureoptions)
-   [Scene Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#sceneoptions)
-   [Variant Set Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#variantsetsoptions)

### General Options

| Option | Description |
| --- | --- |
| **Export Uniform Scale** | Scales exported Assets to compensate for differences in units. The default value is **0.01**, to convert from Unreal Engine's default unit of centimeters to glTF's default unit of meters. |
| **Export Preview Mesh** | When enabled, the glTF exporter exports the preview mesh for a standalone animation or Material Asset. |
| **Skip Near Default Values** | When enabled, the glTF exporter does not export floating-point-based JSON properties that are nearly equal to the default values specified in the glTF specification or the specifications for glTF extensions. This reduces the size of the exported JSON data. Skipped properties are treated as though they're set to their exact default values. |

### Material Options

| Option | Description |
| --- | --- |
| **Export Proxy Materials** | When enabled, the glTF exporter checks whether each exported Material has a glTF proxy Material defined in its user data. If it does, the exporter exports the proxy instead of converting the original material. This setting does not affect glTF proxy Materials you reference directly, the way you would any other material. For more information, see [glTF Proxy Materials](/documentation/en-us/unreal-engine/gltf-proxy-materials-in-unreal-engine). |
| **Export Unlit Materials** | When enabled, Materials that use the Unlit shading model are exported correctly. The glTF exporter uses the [KHR\_materials\_unlit](https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_materials_unlit) extension to export Unlit materials. For more information, see [Shading Model Support](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#shadingmodelsupport). |
| **Export Clear Coat Materials** | 
When enabled, materials that use the clear coat shading model are exported correctly.

The glTF exporter uses the [KHR\_materials\_clearcoat](https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_materials_clearcoat) extension to export clear coat Materials.

Some glTF viewers do not support KHR\_materials\_clearcoat.

For more information, see [Shading Model Support](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#shadingmodelsupport).



 |
| **Bake Material Inputs** | 

Specifies whether to bake a Material into a texture, and if so, how to bake it.

-   **Disabled**: Never use material baking and only rely on material expression matching.
-   **Simple**: If a material input needs baking, then only use a simple plane as mesh data.
-   **Use Mesh Data**: If a Material input uses mesh-specific data such as vertex color, world position, vector transform nodes and so on, this setting includes that data in the Material baking process, and the resulting texture. For materials that don't use mesh-specific data, the exporter uses a simple plane.

The exporter only uses baking for complex material inputs. For simple texture or constant expressions, it uses Material expression matching.

For more information, see [Material Baking](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#materialbaking).



 |
| **Default Material Bake Size** | 

When **Bake Material Inputs** is enabled, this setting specifies the default size of the baked texture that contains the Material input.

You can override this default setting with Material-specific and input-specific bake settings. For more information, see the following sections:

-   [Configure Global Material Bake Settings for Specific Inputs](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#configureglobalmaterialbakesettingsforspecificinputs).
-   [Configure Asset Specific Material Bake Options](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#configureassetspecificmaterialbakeoptions).



 |
| **Default Material Bake Filter** | 

When **Bake Material Inputs** is enabled, this setting specifies the default filtering mode used to sample the baked texture.

You can override this default setting with Material-specific and input-specific bake settings. For more information, see the following sections:

-   [Configure Global Material Bake Settings for Specific Inputs](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#configureglobalmaterialbakesettingsforspecificinputs).
-   [Configure Asset Specific Material Bake Options](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#configureassetspecificmaterialbakeoptions).



 |
| **Default Material Bake Tiling** | 

When Bake Material Inputs is enabled, this setting specifies the default addressing mode used to sample the baked texture.

You can override this default setting with Material-specific and input-specific bake settings. For more information, see the following sections:

-   [Configure Global Material Bake Settings for Specific Inputs](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#configureglobalmaterialbakesettingsforspecificinputs).
-   [Configure Asset Specific Material Bake Options](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#configureassetspecificmaterialbakeoptions).



 |
| **Default Input Bake Setting** | Input-specific default bake settings that override the general defaults. For details, see [Configure Global Material Bake Settings for Specific Inputs](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#configureglobalmaterialbakesettingsforspecificinputs). |

### Mesh Options

| Option | Description |
| --- | --- |
| **Default Level Of Detail** | Default LOD level used to export a mesh. You can override this setting with Component or Asset settings. For example, a minimum or forced LOD level. For more information about how to control which LOD setting the glTF exporter uses, see [Level of Detail (LOD)](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#levelofdetail_lod_). |
| **Export Vertex Colors** | 
Specifies whether to export vertex colors.

If you set **Bake Material Inputs**, in the Material Options, to **Use Mesh Data**, the exporter bakes vertex colors automatically for any Material that needs them.

The glTF format always uses vertex colors as a base color multiplier, which often produces undesirable results. We recommend disabling this option in most cases.



 |
| **Export Vertex Skin Weights** | Specifies whether to export the vertex bone weights and vertex indexes of Skeletal Meshes, which are required for animation sequences. |
| **Use Mesh Quantization** | When enabled, the glTF exporter uses quantization for vertex tangents and normals. This setting uses the [KHR\_mesh\_quantization](https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_mesh_quantization) extension, which might cause the Mesh to not load in some glTF viewers. For more information about mesh quantization, see [Mesh Quantization for High Quality Lighting and Reflections](/documentation/en-us/unreal-engine/how-the-gltf-exporter-handles-unreal-engine-content#meshquantizationforhighqualitylightingandreflections), and the [KHR\_mesh\_quantization documentation](https://github.com/KhronosGroup/glTF/blob/main/extensions/2.0/Khronos/KHR_mesh_quantization/README.md#overview). |

### Animation Options

| Option | Description |
| --- | --- |
| **Export Level Sequences** | Specifies whether the glTF exporter exports Level Sequences. It only supports transform tracks. The exported Level Sequence plays at the Level Sequence Asset's **Sequence Display Rate** (frames-per-second setting). |
| **Export Animation Sequences** | Specifies whether the glTF exporter exports a single animation Asset used by a Skeletal Mesh Component. If you enable this setting, you must also enable **Export Vertex Skin Weights** in the [Mesh Options](/documentation/en-us/unreal-engine/exporting-unreal-engine-content-to-gltf#meshoptions). |

### Texture Options

| Option | Description |
| --- | --- |
| **Texture Image Format** | 
Specifies the image file format to use for exported textures.

-   **None**: The exporter does not export any textures.
-   **PNG**: The exporter always exports textures as `.png` files.
-   **JPEG (if no alpha)**: The exporter exports textures that do not have an alpha channel as `.jpeg` files. If a texture has an alpha channel, the exporter exports it as a `.png` file instead.



 |
| **Texture Image Quality** | Specifies the level of compression for textures exported in a lossy image format. You can set values between **1** (least compressed) and **100** (most compression). Set a value of **0** to use the default compression level for the format. For `.jpeg` files, **0** is equivalent to the default value of **85**. |
| **Export Texture Transforms** | When enabled, the glTF exporter exports UV tiling and un-mirroring settings in a **Texture Coordinate** expression node for simple Material input expressions. This setting exporter uses the [KHR\_texture\_transform](https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_texture_transform) extension. |
| **Adjust Normalmaps** | When enabled, the glTF exporter flips the direction of the green channel in normal maps to conform to the glTF convention. |

### Scene Options

| Option | Description |
| --- | --- |
| **Export Hidden In Game** | Specifies whether to export Actors and Components that are set as hidden in-game. |
| **Export Lights** | Specifies whether to export directional, point, and spot light Components. This setting uses the [KHR\_lights\_punctual](https://github.com/KhronosGroup/glTF/tree/main/extensions/2.0/Khronos/KHR_lights_punctual) extension. |
| **Export Cameras** | Specifies whether to export Camera Components. |

### Variant Sets Options

| Option | Description |
| --- | --- |
| **Export Material Variants** | 
Specifies whether and how to export material variants that change the Materials property on a Static or Skeletal Mesh component.

-   **None**
-   **Simple**
-   **Use Mesh Data**



 |