# Paper 2D Sprites

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-import-and-use-paper-2d-sprites-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-import-and-use-paper-2d-sprites-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:08

---

Paper 2D's primary asset type is called a **Sprite**. Sprites are static 2-dimensional textures that you can use to represent characters or objects, when developing projects in **Unreal Engine**.

![sprite example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdde2050-0cba-494a-9fc1-fae866b82410/bigsprite.png)

Sprites often come in the form of a **Sprite Sheet**, or a single image file that contains many variations of the sprite, that you can use to animate characters and objects.

![sprite sheet example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e850e834-31a7-42b8-9560-fe7dbf0cb640/bigspritesheet.png)

You can download any of the example sprites found on this document by Right-clicking the images and selecting save as from the context menu. You can then use these image files in your own projects or as example content.

See the Example Content section for a single image file containing all of the example sprites used in this document.

![example flipbook character animation running](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad6591ba-65b0-4dba-97ee-e3b4f6cbad6f/run.gif)

For more information on animating sprites, see the [Flipbook](/documentation/en-us/unreal-engine/paper-2d-flipbooks-in-unreal-engine) documentation.

#### Tiles

**Tiles** are specific kinds of sprites that you can use to build 2D levels and environments.

![example tile image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f37a1e38-d1f6-46fa-a656-f3af77a7eae8/tilemap.png)

For more information on Tile Sets and Tile Maps, see the Tile documentation.

## Importing Sprites

To get started using sprites in your project, you must first Import the assets into **Unreal Engine**. To import a sprite or a sprite sheet, click **Import** in the **Content Browser** and navigate in the file browser to your sprite's image file. This file will be imported into Unreal Engine as a **Texture Asset**.

![import button in content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74306172-6eb1-4f74-89f3-1ff6047c135f/import.png)

### Paper 2D Texture Settings

By default, all 2D images, imported into Unreal Engine will be imported as **Texture Assets**. The default image processing, designed to process textures for 3d models and objects, smooths and softens low-resolution files like 2D characters and objects.

In order to preserve the low resolution look of Sprites, you can apply a Paper 2D Texture Setting to the asset.

|   |   |
| --- | --- |
| ![default texture settings on a sprite](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e25bd17-7979-4334-a17f-e3e4414ba643/filtered.png) | ![sprite using the paper 2d texture settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abccad53-a097-4951-b836-0fd06540b540/unfiltered.png) |
| Default Texture Settings | Paper 2D Texture Settings |

You can apply the Paper 2D Texture Settings by **Right-clicking** the Texture asset in the **Content Browser** and navigating in the context menu to **Sprite Actions > Apply Paper 2D Import Settings**.

![apply paper 2d texture settings to texture asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/589ba65a-7bf4-408e-a968-e9560e0fc900/applypaper2dsections.png)

The Paper 2D Texture Setting, removes **Mipmaps**, sets the **Filter** to **Nearest**, and uses the **Editor Icon** as the **Compression Setting**. You can modify the default Paper 2D Texture Settings in the **Paper 2D - Import** section of the **Project Settings**.

You can also apply other **Materials** to Sprites to alter their appearance, color and lighting behaviors.

You can now convert the texture asset into an individual sprite by **right-clicking** the asset and selecting **Sprite Actions > Create Sprite**. A new Sprite asset will be created using the naming convention: `NameOfTextureAsset_Sprite`.

![converted sprite and texture asset in the content browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8870a11e-1f36-4c06-ae8e-e476ebfa6e2d/spriteandtexture.png)

### Extracting Sprites

If you are importing a Sprite Sheet containing many animation frames of a single character or object, you can extract each individual frame as its own sprite by **right-clicking** the texture asset and selecting **Sprite Actions > Extract Sprites** to open the **Extract Sprites** panel.

The naming convention for sprites is important for **Flipbook** implementation, so it's best to decide upon a name **before** extracting sprites from a Sprite Sheet to not encounter errors later. You can name the set of extracted sprites by using the **Naming Template** property in the **Extract Sprites** window.

![extract sprites window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/440dad99-7a09-429b-b64d-96b9a9aabaf7/extractspriteswindow.png)

With the **Sprite Extract Mode** setting, you can choose how to separate the sprites within the sprite sheet. Using **Auto**, Unreal Engine will outline groups of pixels that are surrounded by a transparent background or alpha layer. In instances where this feature is not automatically detecting the proper grouping of sprites, your sprite sheet does not contain a transparent background or alpha spacing in between sprints, or you want uniform sprite sizes, you can set the **Sprite Extract Mode** to **Grid**.

When using **Grid** as the **Sprite Extract Mode** it is important to use a Sprite Sheet that has a uniform sizing and distribution of the sprites for the extraction process.

It is also helpful to know the size of the individual sprites in X and Y pixel-length to, and if there is a uniform spacing between sprites.

![grid settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da3f7915-8314-4f51-a7f5-d5f1e4057320/gridsettings.png)

With the **Naming Template** property you can define the naming convention with which your sprites will be named. The field outside the curly brackets (**{}**) will be consistent for each generated sprite. Within the curly brackets a number will be generated starting with the **Naming Start Index** property value, and will increase by 1 for each subsequent sprite. When extracting sprites, the first sprite will be recognized as the top left most box, then proceeding left to right, and returning to the left for each new row.

![demo extraction grid diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec2acb4f-c224-4dd6-9ae1-e6cb65c105bf/demoextraction.png)

This naming convention is important to consider, especially when creating a Flipbook using a set of sprites. When creating a flipbook from a selected group of sprites, Unreal Engine will automatically organize the sprites in alpha-numerical order. The order can be changed later, but is most conveniently set up during sprite extraction.

After making all adjustments to the sizing and properties of your sprites, select **Extract** to create unique sprite assets from each outlined box.

![extract button highlighted in the extract sprites window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83f66222-2984-492a-8d47-a36ebcb97ccc/extractbutton.png)

### Extract Sprites Property Reference

Here you can reference the Extract Sprites properties and their descriptions.

| Property | Description |
| --- | --- |
| **Sprite Extract Mode** | 
Here you can select how to Extract Sprites from a Sprite Sheet.

-   **Auto**: Extracts sprites by grouping pixels separated by a transparent background or alpha layer. These groupings will then be contained in a box only surrounding the group of pixels.
-   **Grid**: Extracts sprites using a user defined grid. By selecting this option, a Grid section of properties will be accessible in the Extract Sprites window.



 |
| **Outline Color** | Here you can select the color of the outline box that will indicate separated sprites. |
| **Viewport Texture Tint** | Here you can apply a texture tint that will alter the color of the sprites only in the Extract Sprites panel's viewport. This can be helpful for distinguishing sprites from the background. |
| **Background Color** | Here you can change the color of the viewport's background. This can be helpful for distinguishing the background from the sprites. |
| **Naming Template** | Here you can set a template to name the extracted sprites. The field outside the curly brackets (**{}**) will be consistent for each generated sprite. Within the curly brackets a number will be generated starting with the **Naming Start Index** property value, and will increase by 1 for each subsequent sprite. When extracting sprites, the first sprite will be recognized as the top left most box, then proceeding left to right, and returning to the left for each new row. By default this property is `Sprite_{0}`. |
| **Naming Start Index** | Here you can set the starting index value that will be used by the **Naming Template** property to number the extracted sprites. |
| **Cell Width** | When the **Sprite Extract Mode** is set to **Grid**, you can set the **Width (X)** of each cell, in pixel count, to divide the Sprite Sheet into individual Sprites. |
| **Cell Height** | When the **Sprite Extract Mode** is set to **Grid**, you can set the **Height (Y)** of each cell, in pixel count, to divide the Sprite Sheet into individual Sprites. |
| **Num Cells X** | When the **Sprite Extract Mode** is set to **Grid**, you can use this property to **limit** the number of cells that can be used, to limit the number of sprites that can be extracted on the **X axis**. A value of **Zero** will not impose a limit. |
| **Num Cells Y** | When the **Sprite Extract Mode** is set to **Grid**, you can use this property to **limit** the number of cells that can be used, to limit the number of sprites that can be extracted on the **Y axis**. A value of **Zero** will not impose a limit. |
| **Margin X** | When the **Sprite Extract Mode** is set to **Grid**, you can set an offset on the **X axis** that surrounds the full sprite sheet in pixels. |
| **Margin Y** | When the **Sprite Extract Mode** is set to **Grid**, you can set an offset on the **Y axis** that surrounds the full sprite sheet in pixels. |
| **Spacing X** | When the **Sprite Extract Mode** is set to **Grid**, you can add spacing to occur in between sprite extraction cells, on the **X Axis** in pixels. |
| **Spacing Y** | When the **Sprite Extract Mode** is set to **Grid**, you can add spacing to occur in between sprite extraction cells, on the **Y Axis** in pixels. |

## Example Content

Here you can download and use the example sprites used in this document. To save the image file, right-click the image and select save as from the context menu. The image file will need to be converted to a `.png` file format, and you must add an alpha layer to remove the background. You can then import the image file, using the method detailed in the [Import Sprites](/documentation/en-us/unreal-engine/how-to-import-and-use-paper-2d-sprites-in-unreal-engine#importingsprite) section.

![manny sprite sheet example conent](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceb05a49-fad9-4ff4-9031-7f9750e5e66f/mannyspritesheet.png)

If extracting sprites from the provided sprite sheet using the **Grid Sprite Extract Mode**, each sprite is **95 pixels** by **95 Pixels** that you can use as the **Cell Width** and **Cell Height** properties to extract uniformly sized sprites from the sprite sheet.

The sprite sheet does not contain spacing between sprites.

The sprite sheet cotains the following frames of animation in extraction order:

| Animation | Frame Count |
| --- | --- |
| **Idle** | 4 |
| **Run** | 10 |
| **Jump Start** | 5 |
| **Jump Loop** | 1 |
| **Jump Land** | 7 |