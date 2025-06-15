# Paper2D - Import

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paper2d-import-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/paper2d-import-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:42:03

---

## Paper2D - Import

### New Asset Settings

| **Section** | **Description** |
| --- | --- |
| **Pick Best Material when Creating Sprites** | 
Defines whether the source texture should be scanned when creating new sprites to determine the appropriate material.

If disabled, the Default Masked Material is always used.



 |
| **Pick Best Material when Creating Tile Maps** | 

Defines whether the source texture should be scanned when creating new tile maps (from a tile set or through importing) to determine the appropriate material.

If disabled, the Default Masked Material is always used.



 |
| **Analysis Can Use Opaque** | Defines whether opaque materials can be applied as part of the "best material" analysis. |
| **Default Pixels Per Unreal Unit** | The default scaling factor between pixels and Unreal Units (cm) to use for newly created sprite Assets (for example, 0.64 makes a 64 pixel wide sprite take up 100 cm). |

### Import Settings

| **Section** | **Description** |
| --- | --- |
| **Normal Map Texture Suffixes** | A list of default suffixes to use when looking for associated normal maps while importing sprites or creating sprites from textures. |
| **Base Map Texture Suffixes** | The default suffix to remove (if present) from a texture name before looking for an associated normal map using `NormalMapTextureSuffixes`. |
| **Default Sprite Texture Group** | 
The default texture group for imported sprite textures, tile sheets, and so on.

This option is typically set to **UI** for modern-style 2D assets, or **2D pixels** for retro-style 2D assets.



 |
| **Override Texture Compression** | Defines whether the texture compression settings should be overridden on imported sprite textures, tile sheets, and so on. |
| **Default Sprite Texture Compression** | 

Compression settings to use when building the texture.

The default texture group for imported sprite textures, tile sheets, and so on.

This option is typically set to **UI** for modern-style 2D assets, or **2D pixels** for retro-style 2D assets.

You can choose from the following options:

-   **Default (DXT1/5, BC1/3 on DX11)**
-   **Normalmap (DXT5, BC5 on DX11)**
-   **Masks (no sRGB)**
-   **Grayscale (R8, RGB8 sRGB)**
-   **Displacementmap (8/16bit)**
-   **VectorDisplacementmap (RGBA8)**
-   **HDR (RGB, no sRGB)**
-   **UserInterface2D (RGBA)**
-   **Alpha (no sRGB, BC4 on DX11)**
-   **DistanceFieldFont (R8)**
-   **HDRCompressed (RGB, BC6H, DX11)**
-   **BC7 (DX11, optional A)**
-   **Half-Float (R16F)**



 |

### Material Settings

| **Section** | **Description** |
| --- | --- |
| **Unlit Default Masked Material** | The unlit default masked material for newly created sprites. "Masked" means binary opacity: things are either opaque or see-through, with nothing in-between. |
| **Unlit Default Translucent Material** | The unlit default translucent material for newly created sprites. "Translucent" means smooth opacity, which can vary continuously bewteen 0 and 1, but translucent rendering is more performance-intensive than opaque or masked rendering and has different sorting rules. |
| **Unlit Default Opaque Sprite Material** | The unlit default opaque material for newly created sprites. |
| **Lit Default Masked Material** | The lit default masked material for newly created sprites. "Masked" means binary opacity: things are either opaque or see-through, with nothing in-between. |
| **Lit Default Translucent Material Name** | The lit default translucent material for newly created sprites. "Translucent" means smooth opacity, which can vary continuously bewteen 0 and 1, but translucent rendering is more performance-intensive than opaque or masked rendering and has different sorting rules. |
| **Lit Default Opaque Material** | The lit default opaque material for newly created sprites. |