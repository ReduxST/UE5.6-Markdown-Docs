# Neural Post Processing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/neural-post-processing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/neural-post-processing-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:46

---

**Neural Post Processing** is a user-friendly way to use neural networks in the post processing pipeline. You can use the material editor to setup Post Process Materials that utilize neural networks without writing any code.

## Enabling Neural Post Processing

Before you can begin, you must first enable the **Neural Rendering** plugin in your project. You can do so from the **Plugins** browser located in the main menu under **Edit**. This plugin contains all the necessary code to run the network based on the neural profile and the neural buffer / texture set by the material editor.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9632e8e-0c12-4faa-b9d4-901e7e521379/npp-pluginbrowser.png)

## Setting up a Neural Post Processing Material

Follow the sections below to import and set up an ONNX format neural network, and create a Post Process Material that can use this neural network.

### Setting up the Neural Network Profile

Follow these steps to import and set up a compatible neural network model in Unreal Engine.

1.  Import an **ONNX (\*.onnx)** machine learning model file into Unreal Engine to create a **NNE Model Data** asset.
2.  In the Content Browser, use the **Add (+)** menu to create a **Neural Profile** asset. You can add one from the **Material > Profiles** rollout menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5e0c019-e8d3-417e-8a4b-3d05a571a289/npp-addneuralprofile.png)
3.  Open the newly created **Neural Profile** asset.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9690425-34e0-4597-9ec4-15dd4a9144d0/npp-neuralprofileasseteditor.png)
4.  Use the NNE Model Data assignment slot to set the NNE Model Data asset created when you imported your ONNX file.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19bb0787-eeb6-4385-9f23-269b8e314eb9/npp-neuralprofile-nnemodeldataslot.png)

### Creating the Post Process Material

Follow these steps to set up a Post Process Material that uses the Neural Profile with some graph logic.

1.  In the Content Browser, create a new **Material** and open it.
2.  In the Material Editor, use the **Details** panel to set the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f19e9962-c1b2-46e2-8749-00d2a8176702/npp-materialsettings.png)
    -   **Material Domain:** Post Process
    -   **Used with Neural Networks:** Checked
    -   **Neural Profile:** Neural Profile asset.
3.  In the Material Graph, prepare the input to the network using the **Neural Input** node, and get the output from the network through the **Neural Output** node. Once connected to the **Emissive Color** pin of the main material node so that you have something that looks like this:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d5d416b-bb2c-4608-95e7-10f43eaea375/npp-materialgraph.png)
4.  Click **Apply** in the Material Editor toolbar.

With this setup, the material can pre-process and post-process the data using all available nodes in the material editor. This example applies a simple gamma correction of 1/2.2 and scales the value range from 0 ~ 1 to 0 ~ 255 for the input, and reverses it back for the display after getting the output from the neural output. Scaling is not always required. It depends on the neural network model input and output range. If the model input and output is in range 0 ~ 1, we have a simpler setup as below:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56b3023b-22db-444c-8752-a9b2f5c32b4f/npp-exampematerial1.png)

Below is an example taking this further to apply custom regions to use a default light material as a mask.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c812421-64a7-48e9-86e8-3ae39cb6a52f/npp-examplematerial2.png)

This setup can create results like the following:

![Basic Scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/989f78b3-828c-4ff6-b7c2-f4093f90e215/npp-examplescene1.png)

![Scene with Neural Post Process Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56246ef2-b313-46fd-bcd2-1d4e7e21c8af/npp-examplescene2.png)

## Neural Profile Asset Settings

The neural profile is used to bind with neural networks, specify the runtime, batch size and tile configuration.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d5ec91a-eb98-4947-91d6-1d5612a26304/npp-neuralprofileasseteditor1.png)

| Property | Description |
| --- | --- |
| Model |   |
| **Runtime Type** | The type of NNE runtime to support; NNERuntimeORTDml or NNERuntimeRDGHlsl. |
| **NNE Model Data** | Stores the NNE model data imported into the engine, for example, the ONNX model. |
| **Input Dimension** | The input dimensions of the NNE model data being used. |
| **Output Dimension** | The output dimensions of the NNE model data being used. |
| Override |   |
| **Batch Size** | used to override the batch size if the batch dimension is dynamic (-1). |
| Tile |   |
| **Tile Size** | The total tiles used. Each tile will be executed by 1 batch. The NNE model is loaded and used as is with no dimension augmentation. For example, if the input texture has different dimensions, it will be scaled down before application. If set to Auto, tiled buffers are created in batch dimensions automatically, where each tile runs the neural model. For example, if the model input dimension is (1x3x200x200) and the used buffer size of the post processing is 1000x1000, then 5x5 tiles ((5x5)x3x200x200) are run and recombined. |
| **Border Overlaps** | Tile border overlaps (left / right, top / bottom). The larger this value, the more tiles are required to cover the whole screen when the Tile Size is set to auto. |
| **Overlap Resolve Type** | Sets how overlap is resolved. Ignore means the overlapped tile regions have no contribution to adjacent tiles. Feathering means overlapped regions are blended linearly to adjacent tiles. |

### Tiling

Tiling is supported with the texture indexing mode, including overlapping of tiles. Overlapped tile regions can be set to either **Ignored** or **Feathered** during concatenation to support applications like neural filtering and style transfer. More tiles can help increase details but might be costly based on the network complexity.

This is an example of a neural style transfer using 2x2 tiling with feathering, and the seams are hidden.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d4ae072-4c72-4a6a-b748-86088f62bb27/npp-tiling1.png)

You can visualize tile overlapping with the visualization console command `r.Neuralpostprocess.TileOverlap.Visualize 1`.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d28d0af0-f4d5-4f91-872b-dee076b42efb/npp-tiling2.png)

When Tile Size is set to **Auto**, the tile size will not apply scaling but directly apply the network over the neural input texture. Tiles outside of the texture are mirrored at this moment.Here is an example of this with the visualization of the tile overlap when the tile size is set to auto.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddb034f4-4847-4449-8e52-3826979932b2/npp-tiling3.png)

### Buffer Indexing

Textures are downscaled and upscaled to and from their target dimension or kept the same if **Auto** is set for the Tile Size. The current texture indexing mode supports \[1 x 3 x H x W\] for texture indexing mode as the default.

To use an arbitrary ONNX model with other dimensions \[B x C x H x W\], you can use the **Buffer Indexing Mode**. This mode provides full control of the actual value read / written. There is no filtering done natively, you would need to apply any filters needed using either material logic in a material graph or write custom shader code.

Below is an example of breaking the scene into B=2x2 batches and they are set through the Neural Input and Neural Output (Buffer) nodes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7e6fe86-cd85-4db4-b213-93f13755d4fe/npp-buffering1.png)

You’ll also need to modify some settings in the Neural Profile asset. You can use either of the following options:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a172905a-a8ab-4b1a-86f7-00ec8921d72d/npp-buffering2.png)

-   Set **Batch Size Override** to **4** if dynamic batch is supported.
-   Set the **Tile Size** to **2x2** if dynamic batch is **not** supported.

Tiles are called sequentially, while batches are distributed in a single run. These two options can also be used together, as it depends on your design of how to read / write from / to the buffers. At this moment, each call of the **Neural Output** node reads three consecutive channels.

### Runtime Type

You can choose between two NNE Runtimes:

-   **NNERuntimeORTDml:** This uses DirectML as the backend.
-   **NNERuntimeRDGHlsl:** This uses convolution optimized for output width as a modulo of 32.

## Applications

You can use neural post processing in your project in real time rendering or as a tool through Scene Capture. Below are some potential applications:

-   **Stylization:** Fast style transfer, AnimeGAN, CartoonGAN, Pix2Pix, CycleGAN
-   **Sketch:** ShadeSketch
-   **Neural tone mapping**
-   **Image segmentation and Classification**

## Additional Notes

-   **Number of calls of neural input/output nodes.**
    -   While only one Neural Input node can be called in one post process material, multiple calls of Neural Output are legitimate.
-   **Mask of Neural Input.**
    -   A mask can be used to select a portion of the screen to write to the buffer / texture. For example, if a rectangular figure is at top left, you could set that region to 1 to make the UVs and input effective and write to the buffer while ignoring other UVs and inputs if the mask is set to 0.
-   **If the result resolution is low.**
    -   The result resolution is affected by the model output dimension. Check the output dimension in the Neural Profile. To increase the resolution, you can either export a higher resolution model, or use buffer indexing / tiling mentioned above to increase the dimension. Note that some models might have discontinuity at the borders.
-   **Buffer layout.**
    -   In texture indexing mode, the natively supported layout is BCHW. Since the layout of models developed can be in BHWC (for example, tensorflow), you should explicitly export to BCHW.

## Useful Console Commands

-   `r.Neuralpostprocess.Apply` to enable or disable the application of neural networks. When disabled, the neural input is directly returned as neural output.