# Building Texture Streaming Data

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/building-texture-streaming-data-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/building-texture-streaming-data-in-unreal-engine)  
**Processed:** 2025-06-14 16:11:32

---

Every time a Material or Material Instance is modified and resaved, it recomputes texture streaming data related to each texture that is used. Per-texture data includes the UV Channel Index and Scale, where the UV Channel Index is used to sample the texture, and the Scale is the multiplication factor applied to the channel prior to being sampled.

This, however, does not cover all cases, as the sampling could be based on world position, mesh vertex color, or any combination of UV channels. This would make the analysis fail to find the related data, and the engine will assume a dependency on UV Channel 0 and a Scale of 1.

The analysis is run at different steps, depending on what is being edited:

1.  **Material:** This runs when the user applies or saves a modification.
2.  **Material Instance:** This runs when the Material Instance Editor is closed, or when the package holding the Material Instance is saved.
3.  **Level:** This runs for every used Material when the user runs "Build Texture Streaming". This is to ensure that every Material is up-to-date. The reason for materials not being up-to-date are:
    -   Materials prior to 4.15 not having any data.
    -   Material Parent has changed and the instance data is outdated.
    -   There have been improvements done after the Material was last saved.
    -   There is a bug fix.

For a given primitive component, the data required to accurately compute the required resolution of each used texture comes from:

-   The bounds of the primitive
-   The texture coordinate sizes of the mesh
-   The material texture coordinate scale for sampling each texture

When this information is missing, conservative heuristics will be used.

**To build Texture Streaming data:**

1.  Click on the dropdown arrow next to the **Build** button in the **Toolbar**.
2.  Click on **Build Texture Streaming**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b69220d-c91f-4ca9-9d08-e425babd8a5d/buildtexturestreaming.png)

This will generate component and level data to be used at runtime.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b041b7c-6bf0-4dda-856b-4760b716e802/buildingtexturestreaming.png)

Note that this generates the data to be used for all material quality levels and platform feature levels, using the highest quality level and supported feature level.

At runtime, if the component is using fewer textures than those that were used in the build process, the unused ones will be ignored.

## Migrating Streaming Data to 4.15

Because any materials edited before 4.15 did not have any texture streaming data stored with the material, it won't have any data until they are modified and resaved. This includes resaving the child instances of a material as well. To migrate the data quickly, you can use the console command `BuildMaterialTextureStreamingData`.

This will parse all materials currently loaded in memory and generate any missing data. Updated materials will then be marked for resaving.

## Inspecting The Material Data

The data that is built can be inspected in the **Material Texture Scales** viewmode. This viewmode will only show what has been computed successfully and any fallback cases will be shown as *undefined*. This viewmode shows the accuracy of the material scales and is used to validate changes in the analysis. It also identifies possible culprits when there are quality issues related to texture streaming.

To inspect the material texture streaming data, you can either select a Material from the **Content Browser**, or select primitives in the scene view. The **Texture** tab in the main viewport shows where the selection comes from by adding "(Scene Selection)" or "(Content Browser)" to the end of the tab's label.

When using Scene Selection the individual materials can not be selected and the UI will group data from all materials.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bd6fcbe-f8a1-4898-864a-5925c9c683aa/noselection.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf693df3-14ae-47db-b633-4073dabbe400/contentbrowser.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aa42967-4e9e-4b7a-8b39-148e6704d748/sceneselection.png) |
| Nothing Selected | Material from Content Browser | Scene Selected Actor |

#### Scene Selection

When using **Scene Selection**, the individual materials cannot be selected and the UI will group data from all materials. When you hover over one of the texture selections from the dropdown you can see in the tooltip all the listed textures.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/156b62a1-6f9a-42d1-8bec-1918676c4139/singleselection.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d50c797-c4c0-4f35-817b-4e09bf28ea0b/multipleselection.png) |
| Single Object Scene Selection | Multiple Object Scene Selection |

#### Content Browser Selection

When using the **Content Browser** selection, the textures are identified by their texture index, the material name (if several Materials are selected), and the texture name. The texture index is an identifier within each material. The displayed accuracy is computed by comparing the GPU value used, with the value computed in the material analysis. in the material analysis.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dc0651b-c782-4e60-b4bc-b9b97198afd3/cb_singleselection.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f534e320-d7ca-409e-b64f-448607ed8393/cb_multipleselection.png) |
| Single Material Content Browser Selection | Multiple Material Content Browser Selection |

#### All Textures Mode

In the **All Textures** mode, the worst cases are shown from all used textures. If the global value is accurate (light gray), then all textures have accurate values. Unfortunately, there is a limitation in this mode; whereas if the same texture is sampled several times with different scales, this will usually show up as over streaming. This is due to the fact that only the scale requiring the most resolution is used, and the scale requiring less resolution gets ignored in the analysis. This limitation doesn't apply in the per-texture view.

## Build Accuracy

The accuracy of the data computed during the texture streaming build can be inspected by looking at the texture streaming accuracy view modes:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be21cade-c681-4b1a-9a76-45dbec64608d/showtexturestreamingaccuracies.png)

These view modes will show the accuracy of the built data. When the accuracy result is too low or too high (red or green), it is sometimes possible to correct the data with manual [configuration changes](/documentation/en-us/unreal-engine/texture-streaming-configuration-in-unreal-engine). The texture streaming build aims at generating the best data without requiring manual tweaks.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f6fcc21-bc39-4471-992f-3d6003ce52a3/originaltexturescene.png)

The above image is the scene used to build the texture data shown below. For all the view modes, use the following legend:

-   Red: 2X+ mips missing
-   Yellow: 1 mip missing
-   White: Good data
-   Cyan: 1 extra mip
-   Green: 2X+ extra mips

### Primitive Distance Accuracy

This shows the accuracy of the view-mesh distance computed by the streamer compared to the real GPU distance. The streamer computes the distance from the viewpoint to the texture instance axis-aligned bounding box (AABB). This bounding box is computed in the build process by summing up the component LOD-section AABBs that are using the texture.

When the viewpoint gets very close to, or enters the AABB, this mode will always show as 2X+ over, unless the geometry fits the AABB. This is because the streamer computed distance becomes a zero value, while the GPU distance is typically a non-zero value. The ratio between the streamer computed distance and the GPU distance, therefore, becomes very big. This is not an error and there is no need to fix it at this time.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff3ef520-22f8-4bb6-af49-f095e3609695/primitivedistanceaccuracy.png)

The value displayed here can be adjusted by changing the mesh component's **Streaming Distance Multiplier**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f83879c5-2c0e-4e18-aa5c-b966f8750401/streamingdistancemultiplier.png)

### Mesh UV Density Accuracy

This view mode shows the accuracy of the mesh world texture coordinate (texcoord) size used by the streamer, being compared with the real GPU value. This size relates the variation of texcoords by unit of world space. It is used by the streamer to evaluate the impact of the texcoord on the sampling of the texture.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7c643d5-0779-40e3-ad2a-0d1c6f6023a7/uvdensities.png)

This view mode is relatively viewpoint agnostic, and when a mesh has bad values, they are usually not scene related but rather mesh related. This means that if any mesh has the wrong data, any component using this mesh is likely be incorrect as well. This value can be changed within the Static Mesh or Skeletal Mesh Editors by tweaking the `StreamingDistanceMultiplier` until the mesh is in the **Good** range.

### Material Texture Scale Accuracy

Most of the textures used in a material are sampled using a scaled value of one of the Mesh UV Densities. The texture streaming build tries to compute which texture coordinate is used and what scale is applied to each sampled texture. This could fail for many reasons, in which case, the streamer assumes that the texture was sampled with texcoord 0 and a scale of 1.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be998143-efdb-4e78-b338-9f177bbae8b9/materialtexture.png)

In addition to the standard legend, a black and white checkerboard indicates that the build could not generate the required shader for some reason. Also, because the material samples many textures, this view mode shows the worst error across all sampled textures. The two extrema (under-streaming and over-streaming) are displayed via the checkerboard: one shows the worst oversampling, while the other shows the worst undersampling.

Individual errors per texture can be investigated by using the console command `r.Streaming.AnalysisIndex X`, where X is a value between 0 and 31.

### Required Texture Resolution

In this viewmode, the relationship between the currently streamed texture resolution and the required texture resolution can be shown.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/551b7224-cfc3-4415-8a95-dc3d4160195f/requiredtextureres.png)

This viewmode has some similarities with Material Texture Scales, but rather than showing the accuracy of the texture streaming data, it shows the usefulness of the currently loaded texture resolution in an absolute way.

The resolution loaded at any time for a texture comes from a combination of logics and metrics. For example, a texture could be missing resolution because there is not enough space available to load it, or it could have too much resolution because its higher mips are cached in the texture pool waiting for future use. Also, the streamer is usually driven by the component requiring the highest resolution, so investigating the behavior of a texture on one component only makes sense if it is the component that is driving its resolution.

Because of all of this, this viewmode is best used to investigate the behavior of the texture streamer in controlled environments. A useful setup for this is to set:

`r.Streaming.DropMips 2`

This tells the streamer to only keep visible mips, therefore disabling caching and prefetching. By moving the Camera around, you will see if the streamer loads/unloads the right mips at the right time.

Please note that the texture selection menu will present a per-texture selection if there are less than 32 textures selected in the selected components materials. When a texture is selected in this manner, it will be shown on all scene components using it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2707f58-ec7d-4600-a663-f030a91e7246/requiredres_textureselection.png)

## Limitations & Known Issues

-   Not all Materials are supported by the analysis. Currently, Decal and Landscape materials are not supported. There are also cases where the engine fails to generate the shader that is used for analysis. In this case, the primitives will be seen with a uniform dark gray color. Detailed logs of all issues can be enabled through the console command: `log TextureStreamingBuild level all`.
-   Material Instances can have deprecated data if their parents were changed and resaved while the child instances were not resaved. This is because the texture streaming data is stored in the materials, and modifying parent materials does not trigger a resave of the child material instances.
-   At runtime, the engine uses the texture names to access the material streaming data. This is to prevent hard references to the assets at runtime while still giving good performance. This means that if several textures with the same names are used in a material, the required resolution coming from both data will apply to both textures.
-   The shaders used in the Material Texture Scales viewmode are not persistent, and can be missing or deleted if certain kinds of operations are performed, such as compiling shaders, or loading maps. Selecting the viewmode again will regenerate the missing shaders.