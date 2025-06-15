# Grass Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/grass-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/grass-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:26:25

---

### Overview

In this Quick Start guide, we will take a look at how you can set up and apply a grass texture to a landscape. Over the course of this Quick Start tutorial you will learn how to create, set up, and spawn static meshes to make your Landscape appear covered in thick grass. You will be introduced to key properties and settings that will help you shape your virtual grasslands to fit your project's needs.

Click image for full size.

You will also learn about the Actors and properties required for a grassy-looking result to function correctly and deliver the results you want. When you have completed this Quick Start, you will have a new level that should look similar to the image above.

Currently, the Grass system will only work with the Landscape Terrain Actor. Trying to use the Grass system to spawn grass on any other Actor type will not work.

## 1 - Prerequisites

Download the **Open World Demo Collection** content pack as some of the content from the collection will be used in the following Quick Start. Once the Open World Demo Collection is downloaded, add it to the project that you are using to follow along with this Quick Start by doing the following:

1.  From the Epic Games Launcher in either the **Learn** or **Marketplace** tab, locate and then download the **Open World Demo Collection**.
    
    Click image for full size.
    
2.  Go the the **Library** section of the launcher and under **Vault** section locate the Open World Demo Collection.
    
    Click image for full size.
    
3.  Click on the **Add to Project** button.
    
    Click image for full size.
    
4.  A list of projects that you can add this to will appear. Select the project that you are using to follow along with this Quick Start and then press the **Add to Project** button.
    
    Click image for full size.
    

## 2 - Initial Level Setup

Now, we will create a new level and Landscape terrain so that we have something on which to apply the grass.

1.  Create a new level that uses the blank **Default** template as a base.
    
    Click image for full size.
    
2.  Add a new Landscape Actor to the level. In the Main Toolbar, click the **Modes** button, and select **Landscape** to display the Landscape panel and toolbar, and then click on the **Create** button.
    
    Click image for full size.
    
3.  To help better show off the Grass Tool, we are going to add a some noise to our Landscape terrain so it is not completely flat. In the **Landscape** toolbar **Sculpt** tab, click **Noise** from the tool list. Set the Noise properties with the following values.
    
    Click image for full size.
    
    | Property Name | Value | Additional Details |
    | --- | --- | --- |
    | **Brush Size** | 65536.0 | This gives us a brush that is big enough to effect the entire Landscape terrain at once. |
    | **Tool Strength** | 0.01 | Since we only want a very subtle effect, set the Tool Strength very low and add more intensity by painting more. |
    | **Noise Scale** | 256 | Making the Noise Scale bigger makes the noise look smoother and more natural when applied to the Landscape. |
    
4.  Position the Landscape Brush in the viewport so that it covers the entire Landscape terrain. Click the Left Mouse Button **3** to **4** times to add some very subtle noise to the Landscape terrain.
    
5.  Exit Landscape mode. Click the **Modes** button, and choose **Select** to display the **Place Actors** panel.
    
    Click image for full size.
    
    When completed, you should have something that looks similar to the following image.
    
    Click image for full size.
    
    The Grass system works on a completely flat Landscape terrain. The above modification to the Landscape was done purely for artistic reasons, to help show the final result.
    

## 3 - Grass Tool Actor Creation and Setup

We will create the required Actors and Materials the Grass Tool needs to function correctly. We will continue to work with the the level that was created in the last step.

1.  Create a Landscape Grass Type: **right-click** in the **Content Browser**. From the displayed context menu, go to **Foliage** > **Landscape Grass Type** and name it **Grass\_00**.
    
    Click image for full size.
    
2.  Open up the Landscape Grass Type and add a new item to the **Grass Varieties** array: **double-click** on **Landscape Grass Type** and once opened, press the **Plus** icon that is to the right of the **Grass Varieties** name.
    
    Click image for full size.
    
3.  Inside of the **Landscape Grass Type** Actor look for the **Grass Mesh** section, click on the input box that says **None** and enter **SM\_FieldGrass\_01** as the search term, then click on the **SM\_FieldGrass\_01** to load it as the **Grass Mesh**.
    
    Click image for full size.
    
4.  With the Static Mesh added we need to set the following properties to ensure that we are spawning enough grass mesh and that those meshes are randomly rotated and aligned to the Landscape terrain.
    
    Click image for full size.
    
    | Property Name | Value | Additional Details |
    | --- | --- | --- |
    | **Grass Density** | 400.0 | Because we want this to look like grass, we must spawn a lot of Static Meshes to make the Landscape appear densely covered in grass. |
    | **Use Grid** | Enabled | To make the Static Meshes look more naturally placed, this offset is their placement position. |
    | **Random Rotation** | Enabled | Giving the Static Meshes used for the plants and grasses a random rotation makes sure that the same side of the Static Mesh used is not seen all the time, adding to the visual variety of the scene. |
    | **Align to Surface** | Enabled | This makes sure that the Static Mesh used conforms to the surface of the Landscape terrain. |
    

## 4 - Landscape Materials and the Grass Tool

Before we can begin to use the Grass Tools we first have to create a Material that can work with both the Landscape terrain and the **Landscape Grass Type**. We will cover how to set up this Material, as well as how to link it so that it will work with the Landscape Grass Type.

If you would like to have a more in-depth look at how the Landscape terrain works in UE5, refer to the [Landscape](/documentation/en-us/unreal-engine/landscape-outdoor-terrain-in-unreal-engine) pages for more information.

1.  Create a new Material for our Landscape Terrain by **right-clicking** in the **Content Browser**, then selecting the **Material & Textures** option from the **Create Basic Asset** section, and name the new Material, **MAT\_GT\_Grass**.
    
    Click image for full size.
    
2.  Open up the **MAT\_GT\_Grass** Material by **double-clicking** on the Material inside of the **Content Browser**, then add the following two Textures from the **Open World Demo Collection** to the Material Graph.
    
    -   **T\_AlpinePatch001\_D\_alt\_R**
    -   **T\_GDC\_Grass01\_D\_NoisyAlpha**
        
        Click image for full size.
        
3.  Using the **Palette** search function, search for the Material Expression nodes listed below. Once you locate a required Material Expression node, select it in the Palette and then drag it into the Material Graph.
    
    | Material Expression Name | Amount | Additional Details |
    | --- | --- | --- |
    | **Landscape Layer Blend** | 1 | To make the Landscape terrain look more realistic you will often need to blend and paint multiple together or separately and that is what the Landscape Layer Blend allows you to do. |
    | **Landscape Layer Sample** | 1 | This Material Expression allows the Material and the Landscape to talk to one another to ensure the right Static Mesh is used whenever a certain Landscape layer is painted. |
    | **Landscape Grass Output** | 1 | This enables the Landscape terrain to be able to spawn the Grass Types based on the setup in the Landscape Material. |
    
    Click image for full size.
    
    If you are unfamiliar with how the UE5 Material Editor works or would just like more information about it, check the official **[Unreal Engine Material documentation](/documentation/en-us/unreal-engine/unreal-engine-materials)** for more information on all things related to Materials.
    
4.  Select the **Landscape Layer Blend** node and under the **Details** panel in the **Layers** section and add two new Layers to it by clicking the **Plus** icon 2 times.
    
    Click image for full size.
    
5.  Once 2 layers have been added, set the **Layer Name** of one to **Grass** and set the **Layer Name** of the other one to **Rock** also setting the **Preview Weight** to **1.0** for each.
    
    Click image for full size.
    
6.  Connect the **T\_AlpinePatch001\_D\_alt\_R** Texture to the **Layer Rock** input on the **Landscape Layer Blend** node then connect the **T\_GDC\_Grass01\_D\_NoisyAlpha** to the **Layer Grass** input finally connect the **Output** of the **Landscape Layer Blend** node into the **Base Color** input on the Main Material Node, **Mat\_GT\_Grass**.
    
    Click image for full size.
    
7.  In the **Content Browser**, select the **Grass\_00** Landscape Grass Type that was created in the last step.
    
8.  In the **Material** under the **Grass Type** option, press the **Arrow** icon to load the Actor that is currently selected in the Content Browser.
    
    Click image for full size.
    
9.  Select the **Landscape Layer Sample** node under the **Parameter Name** input **Grass** for the name and connect the Output from the **Landscape Layer Sample** to the input of the **Landscape Grass Output** node.
    
    Click image for full size.
    
10.  When completed you should have a Material that looks like the following. As always, do not forget to press the **Apply** and **Save** buttons to compile and save the Material.
    
    Click image for full size.
    

## 5 - Using the Grass Tools

In order to see the Grass system in action, we need to apply the Material that was created in the last step to the Landscape and then use the Landscape painting tools to define where we want the grass to be spawned. In the following section, we will go over how to apply our Material to the Landscape Terrain, then how to use the Landscape Painting Tools to define areas where grass should spawn. We will continue to work in the level that was created in the last step.

1.  Select the Landscape Actor that was placed in the level by clicking on it in the viewport.
    
    Click image for full size.
    
2.  Locate the **MAT\_GT\_Grass** Material in the **Content Browser** and click on it to select it.
    
3.  On the Landscape Terrain under the **Details** panel in the **Landscape Material** section, press the **Arrow** icon to apply the **MAT\_GT\_Grass** Material to the Landscape Terrain.
    
    Click image for full size.
    
4.  In the **Main Toolbar**, click the **Modes** button, select **Landscape** mode. From the **Landscape** toolbar, click on the **Paint** tab to go into **Paint** mode.
    
    Click image for full size.
    
    Click image for full size.
    
5.  Under the **Target Layers** section, add a new **Layer Info** by pressing the **Plus** icon on the far right of the layer name.
    
    Click image for full size.
    
6.  When prompted, select the **Weight-Blended Layer (normal)** option, then select a location to save the new Layer Blend in the Content Browser. Make sure that you create **Layer Info** for both the Rock and the Grass.
    
7.  Select the **Grass** Target Layer, then hold down the **Left Mouse Button** inside the viewport to begin painting the Grass Material to the Landscape Terrain. For this step, try to completely cover the Landscape, giving you results that look like this.
    
    Click image for full size.
    
    Depending on the power of your development PC, when you start to paint on the Landscape the editor might become unresponsive as the grass is spawned. This is normal behavior as the grass is dynamically spawned after you have finished painting. Turning down the **Grass Density** in the **Landscape Grass Type** while working, then putting it back up to the desired level when done, is a great way to help mitigate this as much as possible.
    
8.  To remove grass from the Landscape Terrain, select the Rock Target Layer then inside of the viewport hold down the **Left Mouse button** to begin replacing the grass Texture with the rock Texture.
    
    Adjusting the **Brush Size** and **Tool Strength** will help to better define how the grass is placed or removed while painting on the Landscape.
    

## 6 - On Your Own

Now that you have seen the power that the Grass tool offers, try using the tools listed below in conjunction with what you have just learned to make a level that looks like the following image:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e2551d2-366a-45d2-82d2-98fe8522fc1c/44-t-on-your-own.png "On Your Own")

-   Use the [Procedural Foliage Tool](/documentation/en-us/unreal-engine/procedural-foliage-tool-in-unreal-engine) Tool to make the Landscape look like it is densely covered in grass, flowers and bushes.
    
-   Define the look and feel of the Landscape terrain using the **[Landscape Sculpt](/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine)** tools to add features such as hills, mountains and lakes.
    
-   Give the surface of the Landscape more visual variety and detail by creating a [Landscape Material](/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine) that has multiple Textures that can be painted on the Landscape terrain.
    
-   Adjust the **[Directional Light](/documentation/en-us/unreal-engine/directional-lights-in-unreal-engine)** to make the level lighting resemble lighting that happens in the early morning or late afternoon.
    
-   Set up the level lighting to use a completely dynamic based lighting solution that will make use of dynamic shadows as well as **[Ray Traced Distance Field Soft Shadows](/documentation/en-us/unreal-engine/distance-field-soft-shadows-in-unreal-engine)**.
    
-   Try using the [Foliage System](/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine) tools to remove or tweak the placement, rotation and scale of the Foliage meshes that are placed by the Procedural Foliage tool so that you can get the exact look you are going for.
    
-   Show off your creation to others by using a [Camera](/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine) in conjunction with [Sequencer](/documentation/en-us/unreal-engine/real-time-compositing-with-sequencer-in-unreal-engine) to render out a video of your level for you to share with the world.