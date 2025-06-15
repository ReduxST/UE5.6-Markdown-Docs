# Generating Lightmap UVs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/generating-lightmap-uvs-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/generating-lightmap-uvs-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:26

---

[Unwrapping UVs for lightmaps](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine) is time-consuming and one way you can mitigate this is to use Unreal Engine 5's (UE5) auto-generation tool to generate a lightmap UV from your existing texture UVs on import or through the **Static Mesh Editor**.  

## Caveats and Considerations

By default, an auto-generated lightmap UV repacks the existing UV charts from the static mesh's first UV (UV Channel 0 in UE5). This UV is commonly used as the texture UV, so it's possible that the UV charts aren't laid out or set up in a way that is best suited for a lightmap UV, even with the auto-generation tools in UE5.

Consider the following when creating an auto-generated lightmap UV.

-   Generated lightmap UVs require an existing source UV to repack and that process is only as good as the UV used meaning that if the UV charts aren't broken up and properly laid out, a good repack will not be possible.
-   During repacking, UE5 will not split UV chart edges to create separate UV islands. It only repacks the existing UV charts from the source UV index.
-   UV charts are normalized when generated over maximizing coverage of the UV space with independently scaled or stretched charts.

## Import Options Settings

During import, a lightmap UV will be generated for any static mesh by default when **Generate Lightmap UVs** is enabled. The lightmap UV will be generated from UV Index 1 of your Static Mesh (UV Channel 0 in UE5) and assigned to **Lightmap Coordinate Index** 1. 

Click image for full size.

You can inspect your generated lightmap UV using the Static Mesh Editor. See [Unwrapping UVs for Lightmaps](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine) for more information.

## Lightmap Generation Settings

The Static Mesh Editor **Build Settings** contains settings to generate and repack lightmap UVs. These options enable you to generate a lightmap UV without having to do so during import or post import if you want to refine the generated lightmap UV. 

Click image for full size.

Enable **Generate Lightmap UVs** to use the UV generation options detailed below in the table to control how the Lightmap UV is generated and repacked:

Click image for full size.

| Property | Description |
| --- | --- |
| **Min Lightmap Resolution** | Dictates the minimum padding needed for UV charts when packing the UVs. This target value ensures that packing is texel accurate down to the minimum lightmap resolution used. It will limit the light and shadow bleed that can happen when the value of **Lightmap Resolution** is lower than this value. |
| **Source Lightmap Index** | Chooses the UV channel from which to generate the lightmap UV. |
| **Destination Lightmap Index** | Sets the UV channel that the generated lightmap UV will be stored in. |

## Generating a Lightmap UV

The following steps walk through the process of generating a new lightmap UV from the Static Mesh Editor.

1.  Open the **Static Mesh Editor**. In the **Details** panel, navigate to the **Build Settings** of **LOD0**.
    
    Click image for full size.
    
2.  Generate lightmap UVs with the following settings:
    
    Click image for full size.
    
    -   Enable **Generate Lightmap UVs**.
    -   Set the **Min Lightmap Resolution** to an ideal power of 2, which should be the lowest lightmap resolution that this mesh would ever use. This ensures that less light and shadow artifacts might affect the UV charts.
    -   Typically, the **Source Lightmap Index** should be left on **0** or set to an existing UV channel to generate the lightmap UV from. Only available UV channels will be available to choose from.
    -   The **Destination Lightmap Index** sets the UV channel to create or store the lightmap UV in. It can be any value (where value represents the actual number of current UV channels for this Static Mesh) plus one.
3.  Click **Apply Changes**. 
    
4.  In the **Details** panel under **General Settings**, set the following:
    
    Click image for full size.
    
    -   Enter a **Lightmap Resolution** that this static mesh should use by default for any instances placed in a level. The resolution entered should be higher than the **Min Lightmap Resolution** used for generating the lightmap UV in the **Build Settings**.
    -   Set the **Lightmap Coordinate Index**  to the UV channel being used for your Lightmap UV. Typically, this should match the **Destination Lightmap Index** used to generate the lightmap UV in the **Build Settings**. This UV channel dictates which UV channel is used when generating the lightmap textures during a lighting build.

In this example, the texture UV has been used to create a new lightmap UV. The texture UV is used as the source to repack for the lightmap UV, and the Texture UV has been laid out in a way that works best not to waste any texture space. With that approach, parts of the mesh are scaled larger (or smaller) based on their importance to get adequate texture resolution without wasting space in the texture. 

![UV Channel 0 | Texture UV Layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a0d7196-aa17-4ae1-af46-b7107cee45bf/07-uv-channel-0.png "Texture UV Layout")

![UV Channel 1 | Generated Lightmap UV Layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bace4d3c-921e-49bd-b300-4125b009ed24/08-uv-channel-1.png "Generated Lightmap UV Layout")

When the lightmap UV is generated, it is scaled to have the same density (normalized) and then packed into the UV space with enough padding between each UV chart to avoid light and shadow artifacts from a light build. Here, you may notice a little bit of wasted space in the generated lightmap UV, however, this is negligible and would not justify reworking the UV in a custom tool just to make it use this space.

## Regenerating Existing Lightmap UVs

Regenerating (or repacking) an existing lightmap UV can be performed using the Static Mesh Edtior's **Build Settings**. There are benefits to regenerating a lightmap UV for a Static Mesh.

-   It enables you to change the padding between UV charts to use a higher or lower **Min Lightmap Resolution** without reimporting the mesh. This is most ideal when you have a lot of individual UV charts and gets a tighter pack in the lightmap UV.
-   It enables you to repack any existing lightmap UVs from any **Source Lightmap Index**, including a previously generated lightmap UV channel.

The following steps demonstrate regenerating a custom UV from an imported static mesh:

1.  Open the **Static Mesh Editor**. In the **Details** panel, navigate to the **Build Settings** of **LOD0** to set the following options:
    
    Click image for full size.
    
    -   **Optional** Set the **Min Lightmap Resolution** to a new value that is higher or lower. This adjusts how much padding should be between the UV charts.
    -   Set the **Source Lightmap Index** to the UV channel you want to re-pack
    -   Set the **Destination Lightmap Index** to be the same one as the Source Lightmap Index.
2.  Click **Apply Changes**. 
    

Below is a comparison of the custom lightmap UV that was originally imported with the static mesh. You'll notice that the UV charts have been disproportionately scaled to one another, but it's perfectly acceptable as a lightmap UV because it meets the criteria for no overlapping UVs. Regenerating the UV will normalize all the UV charts for an evenly distributed light and shadow bake result. Each UV chart will also be given an appropriate amount of padding between them to ensure less shadow and light leaking artifacts.

![Imported Custom Lightmap UV](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02a98464-17a1-4dbc-840b-66b73e7f4e4a/10-imported-custom-lightmap-uv.png "Imported Custom Lightmap UV")

![Re-packed Lightmap with | Min Lightmap Resolution of 256](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33c32c04-f420-4b96-bd28-d11b4606b3fd/11-re-packed-min-lightmap-resolution-256.png "Re-packed Lightmap with Min Lightmap Resolution of 256")

It is worth noting that the custom lightmap UV focuses more on having coverage for smaller pieces that the player will see more closely. By increasing coverage of some pieces, the lightmap resolution can be lower to get the same result as the repacked lightmap resolution. You can use your judgment if this is something that you should resolve outside of UE5 for your particular assets.