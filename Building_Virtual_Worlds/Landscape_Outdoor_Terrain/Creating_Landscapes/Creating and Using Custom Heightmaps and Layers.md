# Creating and Using Custom Heightmaps and Layers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-custom-heightmaps-and-layers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-custom-heightmaps-and-layers-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:07

---

There will be times your Landscape will require that you use external programs to create both the heightmap and layers that you will need. Unreal Engine accommodates this style of workflow by allowing for the import of custom heightmaps and layers.

![Image of From Landscape Mountains sample project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5c75cb9-553b-4fa6-b0a0-7e2e6e79d348/landscape_example_image.png "Landscape Mountains sample project")

If this is your first time using the Landscape tools, you might want to check out the [Landscape Overview](/documentation/en-us/unreal-engine/editing-landscapes-in-unreal-engine) first.

## Layers

Landscape layers are special textures that can contain both heightmaps and color data. Which can be used customize the look and feel of your Landscape.

### Layer Formats

Landscape layers can be imported from external programs via implementation of the `ILandscapeHeightmapFileFormat` and `ILandscapeWeightmapFileFormat` interfaces. The editor's existing support for image-based importing has been converted to use this interface and is fully supported. Images for the built-in formats are still required to be grayscale, 8 bits per pixel, single channel files in either .PNG or .RAW format. If you are creating layers in Photoshop, use the following settings when creating a new document:

![Image of Photoshop sample settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07816b99-68af-40db-96b7-8f8ded8fafaa/photoshop_layer_example.png)

### Layer Import

Importing Layers that were made in an external application provides you with the flexibility to use your preferred terrain workflow, but you first need to make sure that a few things are set up in order to get everything to work smoothly.

1.  First, make sure that you have created a Landscape to work with. If you have questions regarding the Landscape creation process, check out [Landscape Creation](/documentation/en-us/unreal-engine/creating-landscapes-in-unreal-engine).
    
2.  Next, make a new Material. For this example, we will be making a very basic Material that could be easily be expanded upon if needed. The Setup for your Material should look something like this.
    
    ![Image of basic Landscape shader setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/059db54b-7247-4e0c-adbc-844dca6238cf/landscape_simple_shader.png)

| Number | Description |
| --- | --- |
| 1 | LandscapeLayerCoords |
| 2 | TextureSample: T\_Ground\_Grass\_D (Found in **StarterContent/Textures**) |
| 3 | TextureSample: T\_Ground\_Gravel\_D (Found in **StarterContent/Textures**) |
| 4 | TextureSample: T\_Rock\_Slate\_D (Found in **StarterContent/Textures**) |
| 5 | LandscapeLayerBlend |

1.  Once the Material is complete, apply it to the Landscape Actor. This will turn your whole landscape black.
    
    ![Image of applying the Landscape Material to the Landscape Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72a2f4f2-0345-454c-a9ee-6bbfa2896cdb/landscape_applied_material.png)
2.  To fix the issue, you will need to add some **Layer Info** to your Landscape Actor. For this example, create one **Layer Info** object for each of our three layers. To read more about **Layer Info** objects, refer to the [Layer Info Objects](/documentation/en-us/unreal-engine/landscape-paint-mode-in-unreal-engine#layerinfoobjects) page.
    
    ![Image of Creating the Landscape Layer Info objects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9d6de03-8da9-4236-9a38-86a01a5a9b4e/landscape_create_layer.png)
3.  When completed, your **Target Layers** section of your Landscape panel should look something like this.
    
    ![Image showing all Layer Info objects in the Target Layers section of the Landscape panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82ea1ed9-53dc-43a3-b0da-3278fd88e4eb/landscape_target_layers.png)
4.  Now it is time to import our custom layer. To do this, right-click on the chosen **Target Layer** and select the **Import from file** option from the pop up menu. This will prompt you to choose the .PNG or .RAW file that contains your custom layer data. Your custom layer file should be the same resolution as your Landscape Actor's **Overall Resolution** that was set when you created it (the default is 505 x 505).
    
    ![Image of Importing custom layer data from file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e95220b-27c0-4ac7-b1e1-2a238cc07464/landscape_import_layer_option.png)
5.  If your layers are not output at the correct size, you will see the following warning:
    
    ![Image of Layer size warning](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38533914-9f7f-472c-b410-fd2e1d08bc18/landscape_layer_import_error.png)
    
    To fix this issue, return to your image editing software and resize your file to match the correct Landscape extent as displayed by the warning message.
    

## Heightmaps

Using external tools to create a base heightmap to use inside UE can be a excellent way of speeding up the Landscape creation process. Programs such as World Machine and Terragen can quickly create the base heightmap for your Landscape. Which can then be imported, cleaned up, or modified using the editing tools inside Unreal Editor, making it a better fit with the world and desired game play.

For more information on importing and exporting heightmaps, see [Importing and Exporting Landscape Heightmaps](/documentation/en-us/unreal-engine/importing-and-exporting-landscape-heightmaps-in-unreal-engine).