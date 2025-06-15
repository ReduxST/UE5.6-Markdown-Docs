# Hair Card Generator

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hair-card-generator-for-grooms-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hair-card-generator-for-grooms-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:03

---

Creating these hair cards can be a difficult and time-consuming task, especially when trying to match the volume and styling of a strand based groom counterpart. The **Hair Card Generator** plugin makes this process simpler by converting strand based grooms to card based representations within the [Groom Asset Editor](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine).

|   |   |
| --- | --- |
| ![strand based groom](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/babbc696-e0d8-4cfa-a0e9-ef7106d64ffd/generator-strands.png) | ![generated card based groom](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f85a4dcf-3943-48b0-a700-19de764a2d59/generator-cards.png) |
| Original Strand Based Groom | Generated Card Based Groom |

## Enabling the Hair Card Generator Plugin

You can enable the **Hair Card Generator** plugin from the **Plugins** browser under the **Geometry** category. You can open the plugins browser from the found in the main menu under **Edit**.

![Hair Card Generator Plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7643e2b6-2ff6-46b1-84c0-746933d79f6b/hair-card-generator-plugin.png)

To learn how to enable plugins, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

Once enabled, you can access the card generator from the [Groom Asset Editor](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine) in the **Cards** panel to add entries under this panel with the **Add (+)** icon for **Add Card asset**.

![Groom Asset Editor Cards Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16b5e9b3-4585-4bc0-aad1-d2ad8518616f/groom-cards-panel.png)

## Hair Card Generator Dialogs and Settings

In the Groom Asset Editor under the **Cards** panel, you can initiate card generation for this groom by clicking **Generate Hair Cards** under the **Mesh** assignment slot.

![Groom Cards Panel Generate Hair Cards Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3072d6e7-0852-44ba-83b0-1cdaccd5b691/groom-generate-hair-cards-button.png)

The **Card Generation Settings** dialog then opens. Here you can configure the various properties to generate the cards mesh for a hair groom group.

![Card Generation Settings Layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01cae0d2-f44b-4a93-84c5-9a740349b2be/card-generation-settings-layout.png)

These are the key areas of the Card Generation Setting dialog:

1.  The named groom and LOD being generated.
2.  A button to reset any settings to default.
3.  Configurable settings for the generation of a card mesh.
4.  Information about the generated card mesh along with target values for number of cards, textures, and triangles.
5.  Buttons to access advanced settings, force regenerate the card mesh, and to generate the card mesh.

The following properties are available in the **Card Generation Settings**:

| Property | Description |
| --- | --- |
| Asset |   |
| **Base Filename** | Name to identify the generated set of cards. |
| **Generate Geometry for All Groups** | When enabled, generate cards using all physics groups. When disabled, generates card geometry using only the current groom group. This setting should be disabled if groom groups have different physics simulation settings. |
| **LODIndex** | Sets the LOD index, editable only in the **Cards** panel. |
| **Generate for Groom Group** | Sets the index of the groom group. This is editable in the **Cards** panel. This setting is only relevant if **Generate Geometry for All Groups** is disabled. |
| Import |   |
| **Destination Path** | Path of the generated mesh and textures. The default option is a subfolder placed in the folder where the groom lives in the Content Browser. |
| Level of Detail |   |
| **Reduce Cards from Previous LOD** | When enabled, this generates cards that share the textures of the previous LOD, if they exist. Only the **riangles** and **Max Flyaway Cards** can be modified with respect to the previous LOD. |
| Randomness |   |
| **Random Seed** | This is a number used to initialize the card generator by clustering the cards and textures in various ways. Change the seed number to obtain slightly different results. |
| Texture Rendering |   |
| **Use Reserved Space from Previous LOD** | If a previous LOD exists and has some reserved space in the texture atlas, the same texture is used, placing the generated textures of the current LOD in the reserved space. |
| **Atlas Size** | Size in pixels of the generated texture assets. |
| **Reserved Texture Space LOD** | Percentage of the texture that is reserved for the subsequent generation of a new LOD. |
| **Use Groom Asset Strand Width** | When enabled, this creates textures using the **Hair Width**, **Hair Root Scale**, and **Hair Tip Scale** from the **Strands** panel. |
| Filter Options |   |
| **ID** | Strand Filter Group ID number. |
| **Card Groups** | If Card Groups (groom\_group\_cards\_id\_attributes) exist, this will display in the Card Group labels. The Card Group labels associated with the Strand Filter Group can be modified in the **Advanced** settings to apply different geometry generation settings to sets of Card Groups. |
| **Number of Cards** | Number of generated cards. The final number can vary slightly from the selected ideal number and depends on the geometry being generated. |
| **Number of Textures** | Number of textures in the atlas. If this value is smaller than the number of cards, some cards will share textures. The final number can vary slightly from the selected ideal value. |
| **Number of Triangles** | Triangle count of the generated mesh. The final number can vary slightly from the selected ideal value. |
| **Max Flyaway Cards** | Maximum number of flyaway cards. These contain a single strand, representing flyaway hair. |
| **Strand Count** | Number of strands in the Strand Filter Group. |
| **Generate** | Shows if the cards will be regenerated fully or partially. This depends on the parameters that have been changed from a previous card generation. |

#### Card Group Settings

You can access the **Card Group Settings** from the Card Generation Settings dialog by clicking the **Advanced**button at the bottom of the window.

![Card Generation Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/206a4e06-e672-4bcd-9b3d-7e9d454914bd/card-generation-settings.png)

The following properties are available in the **Card Group Settings**.

![Card Group Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bdfa419-f0c8-40d7-98c1-9eece44f0b7b/card-group-settings.png)

| Property | Description |
| --- | --- |
| Settings Group |   |
| **Strand Count** |   |
| Asset |   |
| **Generate Filename** | Generates a name for the generated cards based on the name of the groom the cards are being generated from. |
| **LODIndex** | Specify the level of detail index these generated cards will be assigned to. |
| Cards |   |
| **Apply to Cards Group** | The set of Card Groups (groom\_group\_cards\_id) that these settings should apply to. |
| **Target Number of Cards** | The target number of cards to generate. This is the same as the **Number of Cards** in the main settings dialog. |
| **Max Number of Flyaways** | Maximum number of flyaway cards to be generated, which contain a single strand representing a flyaway hair. This is the same as **Max Flyaway Cards** in the main settings dialog. |
| Geometry |   |
| **Target Triangle Count** | The target number of triangles for all cards in this Strand Filter Group. This is the same as the **Number of Triangles** in the main settings dialog. This setting is disabled and ignored if **Use Adaptive Subdivision** is disabled. |
| Geometry: Advanced |   |
| **Use Adaptive Subdivision** | Subdivide card geometry to better match the local curvature of strands, using less geometry for straight areas. Adaptive subdivision uses the **Target Triangle Count** setting to determine the acceptable error rate in order to approximately hit the target number of triangles. |
| **Max Vertical Segments Per Card** | The number of vertical segments (quads) per card, if **Use Adaptive Subdivision** is disabled. |
| Textures |   |
| **Number of Textures in Atlas** | The number of textures to store in the texture atlas. This is the same as the **Number of Textures** in the main settings dialog. |
| Texture Rendering |   |
| **Strand Width Scaling Factor** | When generating the strand textures, this scales the strand width by the scale factor used. This should generally be left at 1.0 unless the strand width units are not in Unreal units. |
| **Use Optimized Compression** | When generating the strand textures, textures are compressed with very straight strands along the strand direction to save texture space. |

## Generating Card Meshes in Unreal Engine

Follow these steps to generate a hair card mesh from a strand based groom:

1.  Enable the **Hair Card Generator** plugin in the **Plugins** browser.
2.  Open a **groom** asset in the **Groom Asset Editor**.
3.  Select the **Cards** panel.
4.  Click **Add Card Asset** to add a new entry.
5.  Set the following in your card entry:
    -   Set a **LOD Index**.This is the level of detail the card mesh is generated for, such as LOD 0.
    -   Expand **Textures** and set the **Layout**.This is the desired layout for any generated textures.
    -   Set the **Group Index**. This is the geometry the cards is to be generated for and mapped onto (see the **LODs** panel for groups).
6.  Click **Generate Hair Cards** under the Mesh assignment slot. This activates the **Card Generation Settings** dialog.
7.  In the **Card Generation Settings** dialog, set the following:
    -   **Optional:** Modify the **Base Filename** and **Destination Path** to change the asset output locations.
    -   Set **\# Cards** to approximate the desired number of unique cards to represent strand data in the groom.
    -   Set **\# Textures** to set the number of unique strand textures to create in the output atlas.
        
        The target number of textures cannot be larger than the number of cards. When the number of textures is lower than the number of cards, cards with similar looking strands are mapped to the same texture.
        
    -   Set **\# Triangles** to approximate the target triangle count across all cards.
        
        This setting, along with the number of cards, determines the accuracy of the card geometry. In general, more cards will cover the groom better but the number of triangles must also be increased so that the individual cards have enough triangles to accurately follow groom strands.
        
    -   Set **Max Flyaway Cards** to select the number of cards that are devoted to single flyaway strands of hair.
    -   **Optional:** Modify any other settings for more advanced control over the generated cards and textures.
8.  At the bottom of the Card Generation Settings dialog, click **Generate** to start the card generation process.

Upon completion of the card generation process, which can take several minutes to complete, the generated cards and textures are automatically applied to the **Mesh** and **Textures** assignment slots in the Groom Asset Editor.

## Additional Resources

-   [You can watch a video tutorial of this process on the Epic Developer Community forums for generating a hair card mesh from a strand based groom.](https://dev.epicgames.com/community/learning/tutorials/pwbl/unreal-engine-metahuman-hair-card-generator)