# Mesh Paint Mode Tools and Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-paint-tool-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-paint-tool-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:53

---

This page contains information about the tools and settings available for the various mesh painting modes.

## Mesh Paint Mode Tools

Each mesh painting mode includes a set of tools for how you can paint and manage color data for a mesh. Most tools are common across the different painting modes, but some are exclusive to a selected painting mode.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8542f90-8e85-424b-b929-cf2f4dba35fc/mp-settings-toolsbar.png)

The table below lists all available tools across the mesh painting modes and in which modes they are available for use.

| Tool | Description | Vertex Color | Vertex Weight | Texture Color | Textures |
| --- | --- | --- | --- | --- | --- |
| **Select** | This is used to select the mesh for painting. | Y | Y | Y | Y |
| **Paint** | This is used to enable the mesh painting tools settings. | Y | Y | Y | Y |
| **Swap** | This swaps the paint color and erase color used for mesh painting. Alternatively, you can use the icon next to Paint Color in the settings. | Y | N | Y | Y |
| **Fill** | This fills the mesh or instance being painted using the paint color, respecting the channels settings. | Y | Y | Y | Y |
| **To LODs** | This applies the vertex colors from LOD0 to all LOD levels. | Y | Y | N | N |
| **To Mesh** | This propagates vertex colors on the instance to the source meshes. | Y | Y | N | N |
| **Save** | This saves any modified source meshes or textures for the selected mesh instances. | Y | Y | Y | Y |
| **Add** | This adds a new mesh paint texture to the selected mesh instance. | N | N | Y | N |
| **Remove** | For vertex painting tools this removes vertex colors from the selected mesh instances. For the texture color painting tool this removes the mesh paint texture from the selected mesh instance. | Y | Y | Y | N |
| **Copy** | This copies the painted color from the selected mesh instance to a copy buffer before pasting on another mesh instance. | Y | Y | Y | N |
| **Paste** | This pastes copied color on the selected mesh instance. | Y | Y | Y | N |
| **Import** | This imports a TGA image file type to populate the vertex colors of the selected instances. | Y | Y | N | N |
| **From Textures** | This imports the current mesh paint texture colors to populate the vertex colors of the selected instances. | Y | N | N | N |
| **From Vertex** | This imports the current vertex colors to populate the mesh paint textures of the selected instances. The vertex colors are always taken from LOD0. | N | N | Y | N |
| **Fix** | For vertex painting tools, this fixes vertex colors applied to the selected meshes. For the texture color painting tool, this will resize the mesh paint texture to match the currently requested texture size. In both cases the Fix tool is only enabled if there is work to do. | Y | Y | Y | N |

## Mesh Paint Tool Settings

The Mesh Paint Tool includes settings to control how painting colors on meshes works. Some settings are exclusive to their mesh painting method, while others are common.

All the settings are available in the Mesh Paint panel when the **Paint** tool is selected.

### Resource Usage Settings

The **Resource Usage** category displays information about the data and texture size of the currently selected mesh.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e1d3205-e1da-4190-8416-4ac091861fd0/mp-settings-resourceusage.png)

| Setting | Description |
| --- | --- |
| **Instanced vertex color size** | For meshes using painted vertex colors, this displays the number of bytes of memory used by the vertex color data. This value reflects the total color data for all instances currently selected. |
| **Mesh paint texture resource size** | 
For meshes using painted texture colors, this displays the size of the texture resource in bytes. This value reflects the total texture data for all instances currently selected.

For texture colors, the mesh paint texture resource size isn’t the final size in a staged package because it doesn’t take into account packaging compression that happens for all textures in the project. Also, this is not the size in memory because this mode uses virtual texturing, which has a fixed memory cost overhead defined by shared virtual texture pools.



 |

### Visualization Settings

The **Visualization** category includes the **Color View Mode** to visualize how color is being applied to a mesh within the level viewport. With this option, you can choose to view RGB, Alpha, or individual color channels.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d571dc97-b239-4064-b3b9-860e1355e51f/mp-settings-colorviewsettings.png)

The **Color View Mode** property includes the following visualization options in its dropdown list:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ec41272-07c4-4cc4-9b6c-dcad57e9e795/mp-settings-colorviewmode.png)

| Setting | Description |
| --- | --- |
| **Off** | This restores the default editor view mode. |
| **RGB Channels** | This option displays the selected meshes unlit with their painted RGB colors. |
| **Alpha Channel** | This option displays the selected meshes unlit with only painted Alpha values showing. |
| **Red Channel** | This option displays the selected meshes unlit with only the painted red channel shown. |
| **Green Channel** | This option displays the selected meshes unlit with only the painted green channel shown. |
| **Blue Channel** | This option displays the selected meshes unlit with only the painted blue channel shown. |

### Color and Weight Painting Settings

The **Color Painting** and **Weight Painting** categories have settings specific to mesh paint methods.

The mesh paint methods for **Vertex Color**, **Texture Color**, and **Textures** share similar properties under the **Color Painting** category for painting and erasing colors and specifying which channels the color painting effects.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/870cbf19-1a7b-43cc-a21c-2e7f97a38d48/mp-settings-vertexcolorsettings.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5c4b34b-cca4-425d-93c6-69a39bb4a5ec/mp-settings-texturecolorsettings.png) |
| Vertex Color and Texture Painting Settings | Texture Color Settings |

| Setting | Description | Vertex Color | Texture Color | Textures |
| --- | --- | --- | --- | --- |
| **Paint Color** | Choose a color that will be applied while painting. The color swatch displays a preview of the currently selected color. Click the swatch to open the color picker to choose a different color. You can also expand this property and type in color values directly to the R, G, B, and A values. | Y | Y | Y |
| **Erase Color** | Choose the color to use as an “eraser” color while painting. This does not, in fact, erase previous colors left by the Paint Color. Instead, it’s better to think of this as a secondary paint color that you can swap between. The color swatch displays a preview of the currently selected color. Click the swatch to open the color picker to choose a different color. You can also expand this property and type in color values directly to the R, G, B, and A values. | Y | Y | Y |
| **Channels** | The color channel check boxes set which color / alpha channels are affected by the paint brush. | Y | Y | Y |
| **Propagate to Vertex Color** | Whether to copy all texture color painting to vertex colors. | N | Y | N |

The mesh paint method for **Vertex Weights** has properties under the **Weight Painting** category that sets how texture painting should blend between target layers based on the painted weight. This setup requires a [Texture Blended Material](/documentation/en-us/unreal-engine/setting-up-a-texture-blended-material-for-vertex-weights-painting-in-unreal-engine) to be set up for the mesh being painted on.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4bcce820-e0d3-4b51-850b-ea9bec0b9eb9/mp-settings-weightpainting.png)

| Setting | Description |
| --- | --- |
| **Texture Weight Type** | 
This configures the blend weight “strategy” for this mesh by setting the number of textures you are blending between in the material assigned to the mesh. When you change this option, the choices available for Paint Texture and Erase Texture are updated. Each selectable option requires a different type of material to be in place for this to work properly. You can choose between the following options:

-   Alpha (Two Textures)
-   RGB (Three Textures)
-   ARGB (Four Textures)
-   ARGB - 1 (Five Textures)

See the [Painting Texture Weights](/documentation/en-us/unreal-engine/mesh-paint-tool-reference-in-unreal-engine#paintingtextureweights) section below.



 |
| **Paint Texture Weight Index** | The texture Blend Weight index that will be used when applied during painting.You can only select options based on the texture weight type selected. Others not available with the selection type are grayed out. |
| **Erase Texture Weight Index** | The texture Blend Weight index that will be used when erased during painting. You can only select options based on the texture weight type selected. Others not available with the selection type are grayed out. |

#### Painting Texture Weights

When painting texture weights, the mesh you’re painting on must have a material assigned that is set up to blend textures for different layers. This material will have multiple textures setup in a way that each layer can be painted and erased to reveal parts of the texture on the mesh. For example, think of this like painting a water puddle on a dirt path material.

To use this workflow, you’ll want to:

1.  Setup a [Texture Blended Material for Mesh Painting](/documentation/en-us/unreal-engine/setting-up-a-texture-blended-material-for-vertex-weights-painting-in-unreal-engine).
2.  Choose a **Texture Weight Type** that matches the number of textures being blended with the mesh paint tools.
3.  Use the **Paint Texture Weight Index** and **Erase Texture Weight Index** to paint to a specific layer. This selection is based on the Texture Weight Type for the number of layers available to blend.

The **Texture Weight Type** includes the following options to blend painted layers:

| Selection Option | Description |
| --- | --- |
| **Alpha (Two Textures)** | This provides two texture channels, which are controlled by painting alpha. This means the material will use only alpha values of 0 (black) and 1 (white) for blending. This setting requires that the mesh have a 2-way alpha lerp blend material applied. |
| **RGB (Three Textures)** | This provides three texture channels, which are controlled by painting RGB values. This means the material will use only RGB values to blend textures. This setting requires that the mesh have a 3-way lerp blend material applied. |
| **ARGB (Four Textures)** | This provides four texture channels, which are controlled by painting ARGB values. This means the material will use only RGB values as well as alpha to blend textures. This setting requires that the mesh have a 4-way lerp blend material applied. |
| **ARGB - 1 (Five Textures)** | This provides five texture channels, which are controlled by painting ARGB values. This means the material will use only RGB values as well as alpha to blend the first four textures. An internal one-minus calculation on the alpha provides a fifth channel for blending. This setting requires that the mesh have a 5-way lerp blend material applied. |

### Brush Settings

The Mesh Paint tool is a brush-based system. The **Brush category includes settings found under the** Paint\*\* tool for a selected mesh paint method. These settings establish a brush designed for either wide areas or fine details.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/319cc501-9bef-4dd2-9fab-1a74f3ca8208/mp-settings-brushsettings.png)

The brush settings include the following:

| Setting | Description |
| --- | --- |
| **Size** | This sets the size of the brush. The size is in normalized units according to the size of the instance or instances being painted. You can press CTRL + Left Bracket (\[) to decrease the brush size, and CTRL + Right Bracket (\]) to increase the brush size. |
| **Strength** | This sets the amount of paint to apply each time you click or move the mouse cursor while painting is enabled. If **Enable Brush Flow** is checked, a percentage (flow amount) of the brush’s strength is applied to the surface. |
| **Falloff** | 
This sets how the brush’s strength falls off with distance. A falloff value of 1.0 means that the center of the brush is 100% strong and fades linearly towards the radius of the brush. A falloff value of 0.5 means that the brush is 100% strong halfway towards the radius, then falls off linearly. A falloff value of 0.0 means the brush is 100% strong over the entire radius.

The brush has a depth-based falloff equal to half of its radius — that is always active — regardless of this setting.



 |
| **Enable Brush Flow** | When this box is checked, this setting configures the brush to apply paint to every single render frame, even when you are not moving the cursor. It yields results similar to an airbrush. |
| **Ignore Back-Facing** | When this box is checked, this setting ignores triangles facing away from the camera. These triangles will not be affected by the paint brush. |
| Advanced |   |
| **Specify Radius** | When this box is checked, the **Radius** value is used instead of the **Size** value to set the brush size for painting. |
| **Radius** | This sets the radial size of the brush in Unreal units. |

### Vertex and Texture Painting Settings

The **Vertex Painting** and **Texture Painting** categories include settings to affect how color data is shared with vertex color data and to access texture asset properties when using mesh paint methods.

The **Vertex Color** and **Vertex Weights** mesh paint methods have additional settings under their **Vertex Painting** categories. These settings make it simpler to work with multiple levels of detail (LOD) on a mesh and with meshes of varying vertex densities.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbdf7107-bc6f-4a3c-aacf-df7adf039ebf/mp-settings-vertexpainting.png)

| Setting | Description |
| --- | --- |
| **LOD Model Painting** | This is the specific Level of Detail (LOD) that vertex color painting will be applied to. The default is to paint to all levels of detail. |
| **Vertex Preview Size** | This is the size of vertex points drawn when the mesh painting is active. This can be useful to adjust the size of the vertex points when the mesh has a high density of vertices. |

The **Texture Color** and **Textures** painting mode’s settings are found under the “Texture Painting” category. These settings paint on texture assets instead of the vertices of the mesh to apply color data.

The **Texture Color** paint mode creates a mesh paint texture asset that stores painted color information. The **Textures** paint mode applies painted brush strokes directly to a texture, and additional texture properties specific to the assigned mesh and its available textures.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/691460ad-e42c-42e3-8dec-513fcc35b9c5/mp-settings-texturepainting1.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2afe8d53-2c65-4466-b7ad-2970c5c2d154/mp-settings-texturepainting2.png) |
| Texture Color Settings | Textures Settings |

The Texture Painting categories have the following settings:

| Setting | Description | Texture Color | Textures |
| --- | --- | --- | --- |
| **UV Channel** | The UV channel of the selected Actor that will be used for the painted texture. | N | Y |
| **Paint Texture** | This swatch shows the texture to apply painting to. To change the texture, click the Name field to the right of the swatch. | N | Y |
| **Enable Seam Painting** | If this box is checked, dilation is used to allow the painting of texture seams. | Y | Y |
| **Paint Brush** | If a texture is set here it is used as a brush shape for the painting, replacing the default circular brush shape. | Y | Y |
| **Point Brush Rotation** | An initial rotation to apply to any Paint Brush shape. | Y | Y |
| **Rotate Brush Towards Direction** | If this box is checked, any Paint Brush shape will be continuously rotated towards the painting direction. | Y | Y |

## Mesh Texture Color Painting Settings

The settings below are specific to the **Texture Color** painting mode and its use of mesh paint textures.

To learn more about using texture color data and its mesh paint texture, see [Getting Started with Mesh Texture Color Painting](/documentation/en-us/unreal-engine/getting-started-with-mesh-texture-color-painting-in-unreal-engine).

### Static Mesh Editor Settings

The static mesh editor contains the following settings specific to the Texture Color mode and its mesh paint textures.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44e2de09-ad18-4cbb-bca1-c1b2a61b1000/mp-settings-staticmesheditorsettings.png)

| Property | Description |
| --- | --- |
| **Support Texture Color Mesh Painting** | 
Whether this mesh can use texture color painting:

-   **Default:** This mesh uses the **Mesh paint default static mesh support** setting from the Engine - Rendering project settings.
-   **Enabled:** This mesh can use painted texture color data.
-   **Disabled:** This mesh cannot use painted texture color data.



 |
| **Mesh Paint Texture Coordinate Index** | The default UV coordinate index to use when texture color painting on this mesh. This should also be set to match this value on the Texture Sample node in the material used for this mesh. |
| **Mesh Paint Texture Resolution** | The resolution of texture color mesh paint textures on this mesh. The final size is rounded up to a power of two and a multiple of the “Mesh Paint Texture Size” project settings. A default value of 0 will automatically calculate the size using the Mesh Paint Texels Per Vertex project setting. |

### Static Mesh Component Settings

The static mesh component includes the following properties related to the texture color painting mode.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c381c1e-8759-481a-b703-4eca0cc2290c/mp-settings-staticmeshcomponents.png)

| Property | Description |
| --- | --- |
| **Enable Vertex Color Mesh Painting** | If false, vertex color mesh painting is disabled on this component. Note that this may be set to false by Blueprint functions that override vertex colors in a construction script. |
| **Enable Texture Color Mesh Painting** | If false, texture color mesh painting is disabled on this component. |
| **Mesh Paint Texture** | Texture containing texture color mesh painting for this mesh component. |
| **Overridden Mesh Paint Texture Coordinate Index** | The overridden UV coordinate index to use when texture color painting on this component. |
| **Overridden Mesh Paint Texture Resolution** | The overridden resolution of the texture color mesh paint textures on this component. |

### Virtual Textures Mesh Paint Project Settings

The **Texture Color** mesh paint method creates a Mesh Paint Texture asset for any instance of a mesh being painted on. Mesh paint textures are always virtual textures, and they come with their own project settings that can be found under the **Engine - Rendering** category.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/219c7ea3-2dee-4475-915b-4f0985a3dedb/mp-settings-virtualtextures.png)

The Project Settings have the following virtual texture settings related to the Mesh Paint:

| Property | Description |
| --- | --- |
| **Mesh paint tile size** | The size in pixels for mesh paint virtual texture tiles. This value is rounded to the next power of two when one is not entered. |
| **Mesh paint tile border size** | The size in pixels for virtual texture tile borders. This value is rounded to the next multiple of two when one is not entered. |
| **Mesh paint use compressed textures** | Whether to use a compressed texture format for storing mesh paint textures. |
| **Mesh paint default static mesh support** | The default setting for whether static mesh assets support mesh paint textures. This can be overridden on the static mesh component for individual instances. |
| **Mesh paint texels per vertex** | The default ratio of texels to vertices when creating a mesh paint texture for a mesh. |
| **Mesh paint maximum texture size** | The maximum size in pixels for mesh paint virtual textures to be. This value is rounded to the next power of two when one is not entered. |