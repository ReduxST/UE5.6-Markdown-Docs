# Landscape Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-overview)  
**Processed:** 2025-06-14 16:32:23

---

Using the **Landscape** system, you can create terrain for your world. Mountains, valleys, uneven or sloped ground, and even openings for caves are possible. Using the collection of tools in the Landscape system, you can modify your terrain's shape and appearance.

For information about opening and using the Landscape tool, refer to the [Landscape Quick Start Guide](/documentation/en-us/unreal-engine/landscape-quick-start-guide-in-unreal-engine).

## Landscape Tool Modes

![Landscape Tool Modes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50b5ee0f-6089-4375-b2ec-5d83e6ea54be/01-landscape-tool-modes.png "Landscape Tool Modes")

The Landscape tool has three modes, accessible by their icons at the top of the Landscape tool's window.

| Icon | Mode | Description |
| --- | --- | --- |
| ![Manage mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fb11cb4-a2da-4cab-8551-f364393fbe9d/02-landscape-manage-mode.png "Manage mode") | **Manage mode** | Create new Landscapes, and modify Landscape components. Manage mode is also where you work with [Landscape Copy Tool](/documentation/en-us/unreal-engine/landscape-copy-tool-in-unreal-engine) to copy, paste, import, and export parts of your Landscape. For more information about Manage mode, refer to [Landscape Manage Mode](/documentation/en-us/unreal-engine/landscape-manage-mode-in-unreal-engine). |
| ![Sculpt mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32b0915b-3e53-4070-8b0c-745ad798be56/03-landscape-sculpt-mode.png "Sculpt mode") | **Sculpt mode** | Modify the shape of your Landscape by selecting and using specific tools. For more information about Sculpt mode, refer to [Landscape Sculpt Mode](/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine). |
| ![Paint mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/307042a4-9f75-4cbf-a75c-9e52858794f7/04-landscape-paint-mode.png "Paint mode") | **Paint mode** | Modify the appearance of parts of your Landscape by painting textures on it, based on the layers defined in the Landscape's Material. For more information about Paint mode, refer to [Landscape Paint Mode](/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine). |

Creating a Landscape means creating a Landscape Actor. As with other Actors, you can edit many of its properties, including its assigned Material, in the Level Editor's **Details** panel. For more information about **Details** panels, refer to [Level Editor Details Panel](/documentation/en-us/unreal-engine/level-editor-details-panel-in-unreal-engine).

## Landscape Features

Below are the main features and techniques employed by the Landscape terrain system.

### Large Terrain Sizes

The Landscape system paves the way for terrains that are orders of magnitude larger than what has been possible in Unreal Engine previously. Because of its powerful **Level of Detail** (**LOD**) system and the way it makes efficient use of memory, heightmaps up to 8192x8192 are now legitimately possible and feasible. Unreal Engine now supports expansive outdoor worlds, which means quick game creation without modifiying stock engine or tools.

Click image to expand.

### Landscape Memory Usage

Landscapes are generally a better choice for creating large terrains than **Static Meshes**.

Landscapes use 4 bytes per vertex for the vertex data. Static Meshes store position as a 12-byte vector, and tangent X and Z vectors packed into 4 bytes each, and either 16-bit or 32-bit float UVs for a total of either 24 or 28 bytes per vertex.

This means Static Meshes use 6 or 7 times the memory Landscapes use for the same vertex density. Landscapes also store their data as **Textures** and can stream out unused LOD levels for distant areas and load them from disk in the background as you approach them. Landscapes use a regular heightfield that efficiently stores collision data compared to the collision data for Static Meshes.

### Static Render Data Stored as Textures in GPU Memory

On most platforms, the Landscape system stores the render data for the terrain in Textures in GPU memory. This storage can be used for data look-up in the vertex shader. The render data uses a 32-bit Texture for storage, with the height occupying 16-bits in the form of the R and G channels and the normal stored as 28-bit values for X and Y, occupying the B and A channels, respectively. Additionally, if the [Retopologize](/documentation/en-us/unreal-engine/landscape-retopologize-tool-in-unreal-engine) tool is being used, another 32-bit Texture will store the X and Y offsets.

### Continuous Geo-MipMap LOD

Standard Texture mipmaps handle LODs for Landscape terrains. Each mipmap is a level of detail, and the mipmap to sample can be specified using the `text2Dlod` HLSL instruction. Your Landscape can have a large number of LODs, yet maintain smooth LOD transitions, because mip levels for both LODs involved in a transition can be sampled, and then the heights and X and Y offsets can be interpolated in the vertex shader creating a clean morphing effect.

|   |   |   |
| --- | --- | --- |
| ![Landscape LOD1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dd0527d-6d13-4a1a-a02d-2b8d0c126422/06-landscape-lod-1.png "Landscape LOD1") | ![Landscape LOD1 to LOD2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c75a3fa4-7867-4325-9029-fd513ced547d/07-landscape-lod-1-to-lod-2.png "Landscape LOD1 to LOD2") | ![Landscape LOD2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ece7a46-b029-4c34-a92c-d73209a3a823/08-landscape-lod-2.png "Landscape LOD2") |
| **Fully LOD 1** | **Morphing from LOD 1 to LOD 2** | **Fully LOD 2** |

### Heightmap and Weight Data Streaming

With Textures storing data, the standard Texture streaming system in Unreal Engine handles streaming mipmaps in and out as needed. This applies to the heightmap data and the weights for Texture layers. Only requiring the mipmaps needed for each LOD minimizes the amount of memory used at any time, which means you can create a more extensive terrain.

### High Resolution LOD-Independent Lighting

The entire high-resolution (non-LOD'd) normal data is available for lighting calculations due to the storage of the X and Y slopes of the Landscape.

|   |   |
| --- | --- |
| ![Landscape LODs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30699714-3c42-4a86-9fd6-4d1c67593d91/09-landscape-lods.png "Landscape LODs") | ![Landscape Full Resolution Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adfef46c-102b-46ce-9156-02b0054b4777/10-landscape-full-resolution-normals.png "Landscape Full Resolution Normals") |
| **Landscape LODs** | **Full Resolution Normals** |

This means you can always use the highest resolution of the terrain for per-pixel lighting, even on distant components that have been LOD'd out.

|   |   |
| --- | --- |
| ![Landscape Simple Vertex Lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7203468-e9c9-43a7-b3fa-77ae60554853/11-landscape-simple-vertex-lighting.png "Landscape Simple Vertex Lighting") | ![Landscape High Res Per-Pixel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36874c90-8042-4c50-ac64-01f437c15527/12-landscape-hr-per-pixel.png "Landscape High Res Per-Pixel") |
| **Simple Vertex Lighting** | **High Res Per-Pixel Lighting** |

When this high-resolution normal data combines with detailed normal maps, Landscape terrains can achieve highly detailed lighting with very little overhead.

|   |   |
| --- | --- |
| ![Landscape Geometry Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7a8c3c4-3a49-4a1c-9602-4f523e0f079b/13-landscape-geometry-normals.png "Landscape Geometry Normals") | ![Landscape Detail Normals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccd07da4-a858-40d2-958d-8d84a8a55a00/14-landscape-detail-normals.png "Landscape Detail Normals") |
| **Geometry Normals Only** | **With Detail Normals** |

### Collision

Landscape uses a heightfield object for its collision. Layers can specify a [Physical Materials](/documentation/en-us/unreal-engine/physical-materials-in-unreal-engine). The collision system will use the dominant layer at each position to determine which Physical Material to use. It is possible to use a reduced resolution collision heightfield (for example, 0.5x render resolution) to save on memory requirements for large Landscape terrains. The collision and render components for distant Landscapes can also be streamed out using the level streaming system.

## Landscape Project Settings

Landscape Project Settings.

| **Option** | **Description** |
| --- | --- |
| **Max Number of Layers** | Defines the maximum number of edit layers that can be added to the landscape. |
| **Default Layer Info Object** | Defines which **Layer Info Object** is added to a new landscape by default. |
| **Max Components** | Defines the maximum number of components in a Landscape. |
| **Max Image Import Cache Size Mega Bytes** | Defines the maximum size of the import image cache in MB. |
| **Paint Strength Gamma** | Defines the exponent used for adjusting the strength of the **Paint** tool. |
| **Landscape Dirtying Mode** | 
Defines when the engine requires the Landscape to be resaved:

-   **Auto**: Landscapes that are marked as needing to be resaved will appear in the **Choose files to save** dialog. Changes are saved whenever the Landscape requires it. Default mode.
-   **In Landscape Mode Only**: Landscapes that are marked as needing to be resaved will not appear in the **Choose files to save** dialog. This is a manual saving mode that puts the responsibility on the user to avoid file contention with other team members. The viewport will display an error message indicating that landscape actors are not up-to-date and need to be resaved. This is done using **Build > Save Modified Landscapes**.
-   **In Landscape Mode and User Triggered Changes**: Landscapes that are marked as needing to be resaved will not appear in the **Choose files to save** dialog. However, any user-triggered changes (direct or indirect) will require the Landscape to be resaved. This mode is recommended for team collaboration as it provides the best features of the other two modes while ensuring that modified landscape actors are still saved and properly submitted to source control.



 |
| **Default Landscape Material** | Defines which landscape material is assigned to new landscapes by default. |