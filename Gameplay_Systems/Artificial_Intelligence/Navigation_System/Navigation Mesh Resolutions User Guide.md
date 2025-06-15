# Navigation Mesh Resolutions User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-mesh-resolutions-user-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-mesh-resolutions-user-guide)  
**Processed:** 2025-06-14 16:38:06

---

## Overview

The **Navigation Mesh Resolutions** feature gives users the ability to generate Navigation Mesh tiles at 3 different resolutions within the same Navigation Mesh. Users can now generate groups of tiles with a high, medium (default), or low precision setting, which can result in improvements in the generation speed of a dynamic Navigation Mesh at runtime.

In this instance, Navigation Mesh resolution refers to the accuracy and number of cells generated to cover a given navigation space. For example, a high resolution tile might subdivide a given space with more polygons to better approximate the shape of the space. However, a low resolution tile will cover the same space, but use fewer polygons. This results in faster generation of the tiles, at the cost of accuracy.

### Common Use Cases

Users can benefit from this feature in the following use cases:

| Use Case | Description |
| --- | --- |
| **Improve Generation Speed** | When using Dynamic Navigation Meshes, use low resolution tiles in open spaces or areas where AI Agents don't need good navigation accuracy. Only use default or high resolution tiles in dense areas where AI Agents need to navigate smaller spaces between obstacles. |
| **Reduce Memory Footprint** | Using low resolution tiles for your Navigation Mesh will result in a smaller memory footprint compared to using default or high resolution tiles. This can benefit games running on hardware with limited memory (like mobile). |

## Use Multiple Resolutions with your Navigation Mesh

1.  Click **Add + > Volumes > Nav Mesh Bounds Volume** to place a **Navigation Mesh Bounds Volume** in your level. Press '**P**' to visualize the Navigation Mesh.
    
    ![Add a Nav Mesh Bounds volume to your level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/721d2092-1aae-41ea-91bd-24319079b8b5/navmesh-res-1.png) ![Press P to visualize the Navigation Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ad537fc-03b2-4a38-aab3-185688c82ae7/navmesh-res-2.png)
2.  Select the **RecastNavMesh-Default** Actor in the **Outliner** window. Go to the **Details** panel and **enable** the **Draw Tile Build Times** checkbox. This shows you the time in milliseconds that it took to build each Navigation Mesh tile.
    
    ![In the Details panel, enable the Draw Tile Build Times checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7235e2ca-2b2d-4c79-96b8-e8007d0a2cd3/navmesh-res-3.png) ![The Navigation Mesh tiles will show their build times](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01486ba8-b90d-4594-bbc4-b3105d85b28b/navmesh-res-4.png)
3.  Click **Add + > Volumes > Nav Modifier Volume** to place a **Navigation Modifier Volume** in your level. Place your Modifier Volume so it overlaps with several Navigation Mesh tiles.
    
    ![Add a Navigation Modifier volume to your level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3175e29-fc47-44f4-9360-b0d5c3d3cdff/navmesh-res-5.png) ![Place the Navigation Modifier volume so it overlaps with the Navigation Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb6f660e-f4bd-4c3c-a933-13c1d14e02f9/navmesh-res-6.png)
4.  With the **Navigation Modifier** volume selected, go to the **Details** panel, then click the **Nav Mesh Resolution** dropdown and select **Low**. You can see how the build times are significantly reduced within the Navigation Modifier Volume.
    
    ![Click the Nav Mesh Resolution dropdown and select Low](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0358ca8-7e19-4a72-a9ce-9e6008286441/navmesh-res-7.png) ![The build times are reduced within the Navigation Modifier Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33e759de-7498-4c6b-9418-4214da7476b8/navmesh-res-8.png)
5.  You can modify Navigation Mesh tile resolutions by using a **Nav Modifier** component inside an Actor Blueprint. Add the NavModifier component, then go to the **Details** panel. Select your desired resolution from the **Nav Mesh Resolution** dropdown.
    
    ![Add the NavModifier component to your Blueprint Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81435695-3c84-4498-acd6-1843ade7bc1e/navmesh-res-9.png) ![Select your desired resolution from the Nav Mesh Resolution dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e68d4f58-3a99-4438-bedd-b1ec0b895543/navmesh-res-10.png)
6.  In the example below, we created an Actor Blueprint and added the **NavModifier** component. Then, we selected the **Low** resolution setting. Notice how the Navigation tiles are rebuilt as the Actor is dragged along the **Navigation Mesh** volume.
    
    ![As we move the Actor, the Navigation Mesh tiles are rebuilt in real time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ef21d55-3304-43e3-b5e5-4a836ed36df3/navmesh-res-component.gif)

## Navigation Mesh Resolution Can Affect Agent Navigation

The Navigation Mesh tile resolution can affect AI Agent navigation pathing. This is especially true when the Agent must navigate between close obstacles or tight spaces.

In the image below, we added 3 obstacles to our Navigation Mesh and set the tile resolution to **Low**. Notice how there is no available path between the bottom two obstacles. This is because there isn't enough resolution available to create the polygons between those obstacles.

![The Agent cannot go between the bottom two obstacles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0025a385-204d-431c-ad04-e34456ac202b/navmesh-res-11a.png)

In the example below, we changed the tile resolution to **Default**. This resolution allows for higher density of polygons, which results in an available path between the bottom two obstacles. In this example the Agent can navigate between those obstacles and its pathing is optimized (straight line).

![The Agent can now go between the bottom two obstacles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73a3aabe-9e18-4ca2-a675-f59fe96b662d/navmesh-res-11b.png)

## Optimal Settings

You can change the Navigation Mesh tile resolution settings by following these steps:

1.  Click **Settings > Project Settings** to open the **Project Settings**.
    
    ![Open the Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/117331e0-1502-4b22-8aba-6a856faa137f/navmesh-res-12.png)
2.  Click on the **Navigation Mesh** category and scroll down to the **Generation** section. Expand the **Nav Mesh Resolution Params** struct to see the settings for each resolution level.
    
    ![Expand the Nav Mesh Resolution Params struct](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a164a438-e45d-4c34-889d-9a1c265eb9b2/navmesh-res-13.png)
3.  You can now change the **Cell Size** for each resolution level. The bigger the Cell Size, the faster it will generate.
    
    ![Change the Cell Size for each resolution level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a210a1f1-76a0-406b-acd7-ebefd3fc7bbd/navmesh-res-14.png)

For optimal performance, you can set each Cell Size as a multiple of each other and ensure the **Tile Size UU** is divisible by all the **Cell Sizes**.

## Debug Tools

You can access the Navigation Mesh tile resolution debug tools by selecting the **RecastNavMesh-Default** Actor in the **Outliner** window and going to the **Details** panel.

## Draw Tile Resolutions

Enable the **Draw Tile Resolutions** checkbox to visualize the resolution of each tile by a different color. The table below shows how each color is related to the tile resolution.

| Resolution | Color |
| --- | --- |
| **Blue** | Low resolution. |
| **Green** | Default resolution. |
| **Yellow** | High resolution. |

![Enable the Draw Tile Resolutions checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abbff81b-3ac2-45ab-bd1e-2cb1e47a210f/navmesh-res-15.png) ![Each tile color represents a different resolution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb848bef-d599-48f6-a6ab-d89f72f3ae87/navmesh-res-16.png)

## Build Times Heat Map

You can enable the **Draw Tile Build Times Heat Map** checkbox to visualize a heatmap of tile build times in your Navigation Mesh. Each color represents a build time range, with light blue representing low build time and red representing high build time.

![Enable the Draw Tile Build Times Heat Map checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbdb884d-7a11-4f9c-8332-185e69b8318c/navmesh-res-17.png) ![A build heatmap is displayed in the Navigation Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d586858-8424-471b-8b07-b5db69ebfaeb/navmesh-res-18.png)