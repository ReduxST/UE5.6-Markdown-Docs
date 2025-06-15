# Generating Groom Textures

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/generating-groom-textures-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/generating-groom-textures-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:24

---

A Groom asset includes added functionality to create their textures based on the strands data in your groom. You can create **Follicle** and **Strands** textures to use with your groom. This is important for creating the groom's level of detail (LOD) meshes. Follicle textures create a mask for a skeletal mesh to better blend hair with its surface. Strands textures create multiple textures from projected strands data onto meshes, which is useful for creating card and hair helmet meshes.

## Creating Groom Textures In-Editor

To create a **Follicle** or **Strands** texture:

1.  Locate your **Groom** asset in the **Content Browser**.
2.  Right-click on the **Groom** asset to open its **Context Menu**.
3.  At the top of the menu, select **Create Follicle Texture** or **Create Strands Textures**.
4.  Optionally, you can configure settings in either dialog or leave them as-is.
5.  Click **Create** to generate the textures.

Depending on your selected option, you'll see one of the following dialogs to create either a follicle or strands texture. Generated textures are saved in the same location as the grooms they generate from.

|   |   |
| --- | --- |
| ![Groom Follicle Mask Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/feb46b26-3fb8-4a13-90eb-b147e82f1f51/groom-follicle-mask-options.png) | ![Groom Strands Texture Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d6ac2e4-d2fe-498e-afda-561e2fa20cff/groom-strands-texture-options.png) |
| Groom Follicle Texture Options | Groom Strands Textures Options |

## Follicle Texture

A **Follicle** texture contains a small distance field of the hair roots that make up your groom. This allows some effects within the shaders of the underlying surface materials to be captured from a skeletal mesh.

When creating a Follicle texture:

-   The color channels store texture information.
-   You can choose multiple grooms to use with the generated texture.

You can apply grooms individually to different color channels or have them be in the same color channel, meaning you don't need each groom to have a follicle texture mask.

The example follicle textures below use the default "Hudson" [MetaHuman character](https://www.unrealengine.com/metahuman) that uses three separate grooms: one for hair, one for eyelashes, and one for mustache and stubble. The image shows three follicle texture masks created individually for the three separate grooms on the left. On the right, if selecting these three grooms together and generating a follicle texture, they are combined and can have each groom's texture mask applied to a different color channel or into the same color channel. This shows them packed into separate color channels using the red, green, and blue channels.

![Groom Follicle Mask Textures](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df83c0ba-fce3-4def-b757-618383d7b346/groom-follicle-mask-output.png)

This is an example of how you can combine several grooms follicle textures into a single texture mask using the Create Follicle Texture workflow..

You can find the following properties in the Groom Follicle Mask Options dialog:

![Groom Follicle Mask Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73fa372c-1d6b-4308-b972-01a404381a3c/groom-follicle-mask-options.png)

| Property | Description |
| --- | --- |
| Options |   |
| **Resolution** | Set the texture resolution to be used for the follicle mask. The resolution is rounded to the closest power-of-two size. For example, 256, 512, 1024, and so on. |
| **Root Radius** | The radial size (in pixels) of the root of the strand in the generated follicle mask. |
| Grooms |   |
| **Groom** | The groom asset used to generate the follicle texture mask. |
| **Channel** | Set which color channel the texture mask is stored in for the follicle texture. |

## Strands Textures

The **Strands** textures include multiple textures generated from your groom using a specified static or skeletal mesh. The **Groom Strands Texture Options** output textures for Depth, Coverage, Tangent, Attributes, and Material by default.

![Groom Strands Textures Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6dbd73f4-8298-4d10-be2d-f295d5ee64ba/groom-strands-textures-output.png)

Examples of generated Strands textures. Textures from left to right: Depth, Coverage, Tangent, Attributes, Material.

These generated textures can be used on grooms made of cards and grooms using hair "helmets" for the highest detail levels but lowest geometric quality. Below is an example showing (from left to right) the strands groom, cards grooms, and mesh hair "helmet" groom. Strands and Cards provide the highest quality for viewing up close to mid-range, while the hair helmet is ideal when the character is much farther from the player camera.

|   |   |   |
| --- | --- | --- |
| ![Groom Strands](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61d32ff9-f066-4215-bd78-92826570317f/groom-strands.png) | ![Groom Cards](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a70fd03-fac1-4718-8e52-974fd4119d04/groom-cards.png) | ![Groom Hair Helmet](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c218ecd-ce43-415f-9353-3c163ac24b27/groom-hair-helmet.png) |
| Strands Groom | Cards Groom | Hair "Helmet" Groom |

The following properties are found in the Groom Strands Texture Options dialog:

![Groom Strands Textures Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccaae27f-4eae-4e59-ae3c-83f3a72d1574/groom-strands-texture-options.png)

| Property | Description |
| --- | --- |
| Options |   |
| **Layout** | This setting determines how the attributes of the groom are packed into textures. You can choose between Card / Mesh **Default** and **Compact**. Default packs attributes separately into textures where it makes sense. Compact groups more attributes into fewer textures. |
| **Resolution** | Set the texture resolution to be used for the follicle mask. The resolution is rounded to the closest power-of-two size. For example, 256, 512, 1024, and so on. |
| **Trace Type** | 
Choose the direction of the traces being performed for the projection of the strands' textures when they're being generated.

-   **Trace Outside:** Performs traces from the mesh's surface to the outside. This works well for facial hair.
-   **Trace Inside:** Performs traces from the mesh's surface to the inside. This works well for hair grooms.
-   **Trace Bidirectional:** Performs traces in both directions: inside and outside.



 |
| **Trace Distance** | Sets the distance from the mesh surface until the hair is projected onto the mesh. |
| **Mesh Type** | Select which type of input mesh should be used for tracing: Static or Skeletal. |
| **Static Mesh** | Select the static mesh asset onto which the groom strands will be projected to generate textures. This requires you to set the **Mesh Type** to **Static Mesh**. |
| **Skeletal Mesh** | Select the skeletal mesh asset onto which the groom strands will be projected to generate textures. This requires you to set the **Mesh Type** to **Skeletal Mesh**. |
| **LOD Index** | Set the index for which level of detail mesh the texture projection is performed. |
| **Section Index** | Set the index of the mesh on which the texture projection is performed. |
| **UV Channel Index** | Set the UV channel index to use for texture projection. |
| Group Index |   |
| **Index \[n\]** | The groom group index that should be baked into textures. When the array is empty, all groups are included by default. When adding indexes, you can specify which groups are used. |