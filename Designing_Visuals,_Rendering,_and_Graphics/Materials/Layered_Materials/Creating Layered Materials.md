# Creating Layered Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-layered-materials-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-layered-materials-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:36

---

This tutorial demonstrates the process of creating a simple **Layered Material** comprised of two layers: chrome and snow. The final Layered Material uses a world-aligned blend to automatically place snow on the upward facing surfaces of the mesh, effectively switching between the two Materials. The blend function always checks for the top surface, meaning even as you rotate the object, the snow Material remains on top, as shown in the image below:

Generally when creating Layered Materials, it is common to create each layer as a Material and copy/paste your node network into a new Material Function. To save time, this tutorial builds each layer within Functions to begin with.

## Simple Chrome

|   |   |
| --- | --- |
| Chrome Textures |   |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dba560d9-beed-48b5-957d-16942b39cb1d/t_examplelayers_metal01_bc.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69acd4c0-4970-4cf0-bd7b-18d8de0e2c9d/t_examplelayers_metal01_n.png) |
| T\_ExampleLayers\_Metal\_1\_BC.png | T\_ExampleLayers\_Metal01\_N.png |
| (Right-click and Save As) | (Right-click and Save As) |

The base layer is a simple chrome Material with some subtle surface imperfections to add visual interest. To help demonstrate editability, the Material includes several inputs that allow you to fine-tune the overall look.

1.  Right-click in the **Content Browser**, click **Materials** and select **Material Function** in the context menu.
    
    ![Create Material Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91e11dd6-15a1-4c9f-89e4-de65b1e8da30/create-material-function.png)
2.  Name the Material Function **Layer\_Chrome**.
    
    ![Rename function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab97e097-e2ae-4d64-a7f5-08d819240ec5/function-layer-chrome.png)
3.  **Double-click** the Material Function to open it in the Material Editor.
    
    ![New Material function in editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be6fb43b-ff64-41bf-9c74-f5be8a59f02f/new-material-function.png)
4.  **Right-click** in the Material Graph, and then search for and select **Make Material Attributes** in the context menu.
    
    ![Add Make Material Attributes from context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aee329bb-6c39-466f-a831-d480cab96980/add-make-material-attributes.png)
5.  Connect the **Make Material Attributs** node to the **Output Result** node.
    
    ![Connect Make Material Attributes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1603b6a-e3ed-43a9-83c8-95edb7d7eb3b/chrome-make-attributes.png)

### Chrome Material Network

The Material Graph for the chrome layer is shown below, with a breakdown beneath the image so you can replicate it easily. The two textures used are **T\_ExampleLayers\_Metal\_1\_BC.png** for the Base Color and Roughness, and **T\_ExampleLayers\_Metal01\_N.png** for the normal map, both downloadable at the top of this page.

Click to enlarge image.

See the following notes explaining the four comment blocks in the Material Graph.

1.  **Base Color** - For the Base Color, a Linear Interpolate (LERP) is used to blend between the base chrome color and a very dark gray value (0.3). For the base color, create a **Function Input** node and name it **Tint**. Make sure the input type is set to **Vector3** in the Details Panel, which allows you to input a color into the function to change the tint of the chrome. The red channel of the **T\_ExampleLayers\_Metal\_1\_BC** texture is used to drive the interpolation between the two values.
    
    ![Input type vector 3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c715f971-ddc8-4ba0-aaf7-f4cb6035c817/input-type-chrome.png)
2.  **Metallic** - Since this is a metal Material, a value of 1 is passed into the Metallic input.
3.  **Roughness** - Roughness should generally be very low for a chrome Material, but some subtle variation can add depth to the overall look of the Material. In this case, the red channel of the chrome texture is used to LERP between values of 0.2 and 0.4. This means darker areas on the texture map will have slightly higher roughness than the light areas.
4.  **Customizable Normal** - This network simply takes in a tangent space normal map and separates the green and red channels, which control the bulk of the map's detail. Each channel is multiplied by a value supplied from another Function Input. This input is set to a Scalar type and named **Normal Multiplier**, with a default value of 1.0. Using an **AppendVector node**, the results are appended together and then appended to the blue channel of the normal map. The result is that the user has the power to adjust the height of the normal by changing the Normal Multiplier value.

Make sure you compile and save your [Material Function](/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview) when finished.

## Simple Snow

|   |   |
| --- | --- |
| Snow Textures |   |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ff887a7-b958-4868-93a1-8c410acd2ef1/t_cave_ice_tiling_d.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1fbfe65-a5ae-4b23-99c2-1efaed007fea/t_cave_ice_noise_n.png) |
| T\_Cave\_Ice\_Tiling\_D.png | T\_Cave\_Ice\_Noise\_N.png |
| (Right-click and Save As) | (Right-click and Save As) |

Download the two textures above and import them into Unreal Engine. Follow the steps below to create a second Material Function for the snow layer.

1.  Right-click in the **Content Browser**, click **Materials** and select **Material Function** in the context menu.
    
    ![Create Material Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee391d2f-07b9-4bd4-9f11-95bd68479ed6/create-material-function.png)
2.  Name the Material Function **Layer\_Snow**.
    
    ![Rename function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/091ca33e-0e80-4570-8e3b-74b64fee6357/snow-layer-function.png)
3.  **Double-click** the Material Function to open it in the Material Editor.
    
    ![New Material Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20f99393-6c2c-4fd1-b25d-698b1353fbbe/new-function-snow.png)
4.  **Right-click** in the Material Graph, and search for **Make Material Attributes** in the context menu, and add it to the graph.
    
    ![Add Make Material Attributes from context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c0bc0ed-499b-4c8f-9525-c10c73d3ca64/add-make-material-attributes.png)
5.  Connect the **Make Material Attributs** node to the **Output Result** node.
    
    ![Connect Make Material Attributes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/196e850c-c2ca-4705-b22e-ae437763dd0b/chrome-make-attributes.png)

### Snow Layer Network

Below is a simple breakdown of the snow Material Graph. This layer uses the **T\_Cave\_Ice\_Tiling\_D.png** and **T\_Cave\_Ice\_Noise\_N.png** textures, both downloadable at the top of this page.

1.  **Base Color** - This is the only relatively sophisticated part of the network, and only because it uses the **FuzzyShading** Material Function. This function simply keeps the texture from getting too dark when the Material is receiving light. This is similar to the way light passes through fibrous surfaces. This makes it perfect for velvet, moss, or in this case, snow. Some contrast is removed from the Base Color texture (T\_Cave\_Ice\_Tiling\_D.png) by raising it to the power of 0.3.
    
    Next, plug the result into a FuzzyShading Material Function, which you can insert from the Functions tab in the Material Editor palette. Set **Core Darkness** to 0, **Power** to 1, and**EdgeBrightness** to 0.5. Finally, multiply the whole thing by a very pale blue color (R=0.8, G=0.9, B=0.95) to give it a cold, icy color cast.
    
2.  **Metallic** - This is a non-metallic surface, so Metallic is set to 0.
    
3.  **Roughness** - Snow should shine a little bit when the light hits it just right, so the red channel of the T\_Cave\_Ice\_Tiling\_D.png texture is used to drive a Lerp between 0.6 and 0.3.
    
4.  **Normal** - The normal map on its own is a little bit too strong. One way to reduce the effect of the tangent space normal map is to double the strength of the blue channel. This is done by multiplying the normal map by a Constant3 Vector with a value of (1,1,2).
    

Save your result when finished!

## Layered Material

You can now create a Material and blend the two layer functions together. This example is configured so that the snow always appears on the top of the surface. The Material also contains some parameters to make it customizable in Material instances.

1.  In the **Content Browser**, click the **Add New** button and choose Material from the context menu.
    
    ![Create new Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad3d1147-9a43-4923-8144-d2fc3691fb19/create-material.png)
2.  Name your new Material **Mat\_SnowyChrome**.
    
    ![Rename your Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36291a2d-c45c-4f88-9826-08e4d095d38e/rename-material.png)
3.  **Double-click** the Material to open it in the Material Editor.
    
    ![Open new Material in Material Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77426829-9dad-4c5a-afd4-55013b3da45b/open-new-material.png)
4.  Drag your **Layer\_Chrome** and **Layer\_Snow** Material Functions from the **Content Browser** into the Material Graph.
    
    ![Drag layers into Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6207eba1-cb30-4c44-880e-5f4740a10b7f/drag-from-content-browser.png)
5.  Click in the background of the Material Graph to display the base Material Properties in the Details panel. Enable **Use Material Attributes** by checking the box.
    
    ![Enable Use Material Attributes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50344b08-4a98-4122-b086-51c4af96d5cc/use-material-attributes.png)
6.  From the Palette, add a **MatLayerBlend\_Simple** Material Function, as well as a **WorldAlignedBlend** Function. The MatLayerBlend\_Simple will execute the transition from chrome to snow, and the World\_Aligned\_Blend will power the Layer Blend based on the direction the surface is pointed.
    

### Layered Material Network

Below is a breakdown of the Mat\_SnowyChrome Material network, along with descriptions for each of the commented areas.

1.  **Chrome Setup** - Two parameters are connected to the Layer\_Chrome Material Function. The first is a Scalar Parameter named **Chrome Normal**, which is used to drive the **NormalMultiplier** input. The second is a Vector Parameter named **ChromeTint** that is driving the **Tint** input. These parameters allow you to alter the strength of the normal map, and change the tint of the chrome when the Material is instanced later.
    
2.  **Snow Setup** - No additional nodes are needed. The Layer\_Snow Material Function is plugged directly into the blend node.
    
3.  **World Aligned Blend Setup** - The WorldAlignedBlend node controls the position and sharpness of the Material blend. Set the **Blend Sharpness** value to 10. Then create a Scalar Parameter named **BlendBias** and connect it to the **Blend Bias** input. This allows you to adjust the vertical position on your mesh where the blend occurs.
    
4.  **MatLayerBlend** - This node contains the logic used to drive the blend. In this case, the base Material is Layer\_Chrome and the top Material is Layer\_Snow. The WorldAlignedBlend is plugged into the Alpha input to drive the the transition.
    

Save your Material when done!

## Instancing a Layered Material

Since this Material contains two parameters, you can now create a Material Instance and customize aspects of the Material Layers.

1.  If you included the Starter Content in your project, you will have a set of chairs and a table to apply the new Material to. If not, feel free to place some of your own assets in the scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c4a82bc-5250-49b9-a5de-bc4566b58850/defaultlevel.png)
2.  Right-click on the **Mat\_SnowyChrome** Material and choose **Create Material Instance** in the context menu. The default name should be fine.
    
    ![Create Material Instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3ee6600-fef3-4cda-a55c-1f501913faf1/create-material-instance.png)
3.  Drag the Material Instance asset from the **Content Browser** onto one of the objects in the scene.
    
    ![Apply Material instance from Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83975d47-00b8-4492-b59e-db33a93ce577/apply-material-from-browser.png)
4.  **Double-click** the Material Instance to open it in the Material Instance Editor. You can override the tint of the chrome, the depth of the chrome's normal map, and how much snow has fallen on top of it.