# Vertex Animation Tool - Timeline Meshes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/vertex-animation-tool---timeline-meshes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/vertex-animation-tool---timeline-meshes-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:54

---

In the following section we will cover how you can use the 3Ds Max Animation Timeline in conjunction with the Vertex Animation tools to create a 2D Texture that stores the position of vertices in any given 3D mesh.

## 3Ds Max Content Creation

1.  First from the **Standard Primitives** create a **Teapot** at 0,0,0 in the world with the following options.
    
    -   **Radius:** 70.0
    -   **Segments:** 5
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c17a71d-f670-4576-86c0-702a45345976/vat_teapot_setup_00.png)
2.  Next from the Modifier List, apply a **Bend** Modifier to the Teapot and then set the **Direction** to **90**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67359098-8af8-4db5-92bc-45db52c2c3ff/vat_teapot_bendmod_00.png)
3.  Now enable **Auto Key** and then move the **Time Slider** to **10** and set the **Angle** on the **Bend Modifier** to **\-50** and then move the **Time Slider** to **25** and set the Bend **Angle** to **50**. Finally move the **Time Slider** to **35** and then set the Bend **Angle** to **0**. Once all of that has been completed make sure to turn off **Auto Key** to ensure that you do not place any extra keys by accident.
    
4.  With the Teapot now bending, open up the Vertex Animation Tools, if not already open, and set the **Animation Options** to **Animated Meshes** and the **Anim End** to **35**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95899fc2-18df-4492-aa9a-567fc10db304/vat_tool_settings_setup.png)
5.  Now that the correct tool options have been set, press the **Process Animated Meshes** button to begin the Texture creation process. About half way through the process a Windows Dialogue box will be displayed asking for a location to store the Textures that are generated. For this example a folder was placed on the Desktop called **Vertex\_Anims** and the Textures where saved to that folder. When completed the folder that was placed on the Desktop should now have two Texture files inside of it, a **.EXR** Texture which contains the vertices position data and a **.BMP** Texture that contains the Teapots Normal information.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bfe971d-bd0e-448a-8beb-ba85b906e3ed/vat_output_textures.png)
6.  With the Textures now created go back to 3Ds Max and select the Teapot mesh with "**\_MorphExport**" added to the name and export it as a .FBX file to the same folder that the Textures where exported to. Name the mesh "**SM\_Teapot\_Bend\_00**" and in the FBX options make sure that **Smoothing Groups** are enabled and leave all other setting with the default values.
    

## Unreal Engine Content Setup

Once all of the content has been exported from 3Ds Max it is now time to import and set that content up so that it will work correctly inside Unreal Engine. Please keep in mind that each and every step listed below **MUST BE** completed exactly how it is described below or you run the risk of things not working correctly inside Unreal Engine.

### Texture Import & Setup

If you are unfamiliar with the Unreal Engine Texture Import process please read the **[Textures](/documentation/en-us/unreal-engine/textures-in-unreal-engine)** documentation for more information.

The first thing that needs to be completed is that both Textures that were exported from 3Ds Max need to be imported into Unreal Engine. To do select each Texture from its export location in Windows Explorer and drag them into the Content Browser, releasing the left mouse button to trigger the import process. When you do this, you will be prompted with a warning message about the Textures not being a power of 2 resulting in the Texture not working with Streaming or Mip Mapping. Press the **Yes** button to dismiss the prompt and continue with the import process.

Once each Texture has been imported, they then need to be setup in a very specific manner to ensure that they work correctly. The first Texture to setup is the .EXR Texture that contains the vertices position data. Open up this Texture by **Double-Clicking** on it in the Content Browser with the **Left Mouse Button** and make sure the following options are set / enabled.

-   Make sure the Mip Gen Settings is set to **No Mip Maps**.
-   Change the Texture Group to **UI**.
-   Make sure that **SRGB** has been disabled.
-   Set the Compression Settings to **TC\_HDR**.
-   Set the Filter to **Nearest**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29b5babc-d3eb-481d-86ea-410aa1081510/vat_exr_texture_setup.png)

Next open up the Normal Map Texture and make sure that the following options are set / enabled.

-   Make sure the Mip Gen Settings is set to **No Mip Maps**.
-   Change the Texture Group to **UI**.
-   Make sure that **SRGB** has been disabled.
-   Set the Compression Settings to **TC\_Vector Displacement Map**.
-   Set the Filter to **Nearest**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39434a17-f80c-4c4c-bb7b-3f64fb8091af/vat_normal_texture_setup.png)

With the Textures now set up correctly, make sure to press the **Save All** button in the Content Browser to save all changes that have been made.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3410a8ed-8d05-4766-96e1-8131b7a13d9f/vat_save_all.png)

### Static Mesh Import & Setup

Now that the Textures have been imported and setup, it is now time to import and setup the Teapot Static Mesh. Import the Teapot Static Mesh in the same way the Texture were imported by first selecting the Teapot Static Mesh in Windows Explorer and then dragging it into the Content Browser and releasing the Left Mouse Button to trigger the import process. When you do this the following dialogue box will be displayed. From this dialogue make sure that the following options are set / disabled.

If you are unfamiliar with how to import Static Meshes into Unreal Engine please check out the **[Importing Assets Directly](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine)** document for more information about this.

-   Disable the **Auto Generate Collision** option.
-   Disable the **Remove Degenerates** option.
-   Disable the **Generate Lightmap UV's** option.
-   Enable the **Combine Meshes** option.
-   Disable both **Import Materials** & **Import Textures** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c82353b-d010-4cd7-b9ea-ccff494f5e3e/vat_sm_import_options.png)

Once all those options have been set, press the Import button to begin the import process. After the Static Mesh has been imported, open the Static Mesh up and make sure the following options are enabled / disabled.

-   Enable the **Use Full Precision UVs** option.
-   Set **Distance Field Resolution Scale** to 0.0.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d57b31a-4593-47cf-b754-7c626807fba2/vat_sm_setup_options.png)

With the Static Mesh now set up correctly, make sure to press the **Apply Changes** button in the Static Mesh editor and then press the **Save All** button in the Content Browser to save all changes that have been made so far.

### Unreal Engine Material Setup and Uses

Now that all of the required content has been imported and properly setup, it is now time to create a that can Material use the content.

If you are unfamiliar with how Materials work inside Unreal Engine please refer to the **[Materials](/documentation/en-us/unreal-engine/unreal-engine-materials)** documentation for more information.

1.  First create a new **Materia**l by **Right-Clicking** with the Mouse and then choosing the **Material** option that is under the **Create Basic Asset** section. Name the Material **MAT\_Vertex\_Animation**.
    
2.  Next open up the **MAT\_Vertex\_Animation** Material and locate the two Textures that were imported into the Content Browser in the previous step. Select both **Texture**s and then **Drag** them from the Content Browser and Drop them into the Material Graph.
    
3.  Then select the **Main Material Node** and in **Details Panel** search for **Num Customized UVs**. When you located the **Num Customized UVs** input, input a value of **4**. You should now see four new inputs on the Main Material Node with Customized UV and then a number starting at 0 going to 3.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f73ca9be-44f9-4835-97f5-dae967ab6e4e/vat_cus_uvs.png)
4.  Next while still in the Main Material Node Details Panel, **Un-Check** the **Tangent Space Normal** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/459e178b-6c46-4e49-8598-07eb99b2409e/vat_uncheck_tan_normals.png)
5.  Then hold down the **1** key on the Keyboard and then click inside the Material Graph with the **Left Mouse Button** to place down a Constant Parameter node. Set the value of the Constant to **0.5** and then plug the output into the **BaseColor** input in the Main Material Node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f133b5f-166c-4a2d-b891-b7086343e599/vat_add_const.png)
6.  Now it is time to add the Material Function that powers the effect. To do this **Right-Click** with the Mouse inside the Material Graph and then from the menu that is displayed, type **MS** to show the Maxscript Material Functions. Then click on the **MS\_VertexAnimationTools\_MorphTargets** Material Function with the mouse to add it to the Material Graph.
    
7.  With all the required Textures and Material Function now added to the Material Graph, we can now begin to connect everything together but first, select both Texture Samplers and convert them to **Texture Objects** by **Right-Clicking** on one of the Textures and selecting the **Convert To Texture Object** option.
    
8.  Next connect the output from the Normal Texture Object to the **Morph Normal(T2d)** input. Then connect the .EXR Texture Object to the **Morph Texture (T2d)** input. Finally connect the outputs of the **MS\_VertexAnimationTools\_MorphTargets** Material Function to the related inputs on the Main Material node.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33a9a98e-fe9c-4501-9f3b-98ed2dcc11ad/vat_wired_up.png)
9.  Now add another Constant Parameter to the Material Graph by holding down the **1** key on the Keyboard and then clicking in the Material Graph with the **Left Mouse Button** to place the node in the Material Graph. Once the Constant Node has been added set its value to 51 and connect it to the **Number of Morph Targets** input on the **MS\_VertexAnimationTools\_MorphTargets** Material Function.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cf63a0e-b122-4706-bf27-7b0d505f8842/vat_num_morph_targets.png)
    
    The number that is used for the **Number of Morph Targets** input comes from the Y value of the .EXR and Normal Textures. Make sure to always use the number that comes from the Texture as using any other number could result in your effect not working the same in Unreal Engine as it did in 3Ds Max.
    
10.  Once everything has been connected press the **Apply** button to compile the Material and then press the **Save** button to save your work and once that is completed closed down the Material Graph Editor.
    
11.  From the **Content Browser** select the Teapot mesh that was imported and drag it from the Content Browser into the level. Then once the Teapot mesh is in the level, select the Material that was created, **MAT\_Vertex\_Animation**, and apply it to the Teapot mesh by dragging it from the Content Browser on to the Teapot mesh that is placed in the level.