# Landscape Technical Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-technical-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-technical-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:39

---

Striking the balance between beauty and performance when creating a Landscape in Unreal Engine can be a challenge. When building a Landscape, it is important to understand how the Landscape Actor is constructed and what dimensions provide the best performance. Valid dimensions for Landscape heightmaps are not always obvious when getting started. Being able to determine which heightmap dimensions are valid and which are optimal requires a thorough understanding of the underlying architecture of the Landscape, which are covered on this page.

## Landscape Components

Landscapes are divided into multiple Landscape Components, which are Unreal Engine's base unit for rendering, visibility calculations, and collision. All of the Landscape Components in a Landscape are the same size and are always square. The size of the Landscape Component is decided when the Landscape is created and depends on the Landscape's size and detail.

Each Landscape Component's height data is stored in a single texture. Because of this, the texture's size must be a power-of-two number of vertices. The shared row of vertices along the edge of two neighboring Landscape Components is duplicated and stored in each one. For this reason, it makes sense to think about the number of 4-sided polygons (quads) in each Landscape Component.

The illustration below shows a very simple Landscape (outlined in green) that contains four Landscape Components. Each is made up of a single quad and one has been separated to show how the vertices where the Landscape Components meet are duplicated.

A Landscape made of four Landscape Components

## Component Sections

Components can optionally be divided into either 1 or 4 (2x2) subsections to increase the resolution of the Landscape. These subsections are the base unit of Landscape LOD calculation.

Using 4 (2x2) subsections gives you the same size heightmap as using four times as many Landscape Components with only one subsection each, but using fewer Landscape Components gives better performance.

The size of each section (in number of vertices) must be a power of two value (with a maximum of 256x256) so that different LOD levels can be stored in the mipmaps of the texture. This will lead to the number of quads in a Landscape Component in each direction (x or y) either being a power of two value minus 1 (if 1 section per Landscape Component) or a power of two value minus 2 (if 4 sections per Landscape Component).

The illustration below shows an individual Landscape Component (outlined in green) that contains four sections. Each section is made up of 9 (3x3) quads. Again, you can see that the vertices where the sections meet are duplicated.

A Landscape Component containing four subsections.

## Landscape Component UI

A Landscape Actor is color-coded to make it easier to identify each type of Landscape Component. The edges of the Landscape are highlighted in yellow, the edge of each component is in light green, section edges (if set to 2x2 sections) are in medium green, and the individual Landscape quads are in dark green.

A new Landscape being created in the Viewport showing the UI colors.

| **Color** | **Description** |
| --- | --- |
| **Yellow** | Landscape Actor Edge |
| **Light Green** | Landscape Component Edge |
| **Medium Green** | Landscape Section Edge |
| **Dark Green** | Landscape Individual Quad |

## Performance Considerations

The choice of Landscape Component size compared to the total number of Landscape Components is a performance trade-off. Smaller Landscape Component sizes facilitate quicker LOD transitions and the occlusion of more terrain, but the smaller size also means you will need more Landscape Components.

Each Landscape Component has a render-thread CPU processing cost and each section is a draw call, so try to keep these numbers to a minimum. For the largest Landscapes, Epic recommends a maximum of 1024 Landscape Components.

## Calculating Heightmap Dimensions

To create a system that can accommodate very large terrain sizes and still be efficient in terms of memory and performance, the architecture applies restrictions on the dimensions of the heightmap. These restrictions are described below. This means that some dimensions are valid and others are not.

The dimensions for a Landscape are based on the number of quads in each section, the number of sections in each Landscape Component, and the total number of Landscape Components in the Landscape. Once you determine the number of total Components and the resolution of each one, you can calculate the dimensions of the Landscape as a whole using the formula below:

(A*Quads + 1, B*Quads + 1)

A and B are the number of Landscape Components in each direction, and Quads is the number of quads per Landscape Component.

Below are two different examples of using this formula.

### Example 1

If you start with a Landscape Component consisting of a single subsection that contains 64x64 vertices, then the Landscape Component size is 63x63 quads. If your Landscape has10x10 of these Landscape Components, then you have 630x630 quads total in your Landscape. To import the heights for this Landscape, you need a heightmap of 631x631 vertices, because there is always one more row of vertices than there are quads (think of a 1x1 quad - it needs 4 vertices). Therefore, 631x631 is a valid Landscape size.

### Example 2

If you have a Landscape Component divided into 4 subsections, each of which is made up of 64x64 vertices, that leads to 63x63 quads per section and 126x126 quads per Landscape Component. If you have 32x32 of these components, you get 126 \* 32 = 4032 quads total in each direction. Therefore, the total Landscape will be 4033x4033 vertices.

These examples focus on square Landscapes. However, you can create Landscapes that are not square. Assuming 63 quads per Component, you could have any Landscape of AxB Components with a total size in vertices of (A*63+1 , B*63+1).

## Calculating Heightmap Z Scale

Unreal Engine calculates your heightmap's height by using values between -256 and 255.992, stored with 16-bit precision. The calculated height is then multiplied by the Z scale value that you input when you import the heightmap data. For example, a Z scale value of 1 results in a maximum height of roughly 256 cm and a maximum depth of -256 cm. Therefore, at the default Z scale value of 100, your height values will be between 256 m and -256 m.

Adjusting the Z scale during the import process.

Calculating a custom height requires the use of a ratio to convert your custom height value into the -256 to 256 range that Unreal Engine uses. Since the height range is a total of 512 units (-256 to 0 is 256 units and 0 to 256 is another 256 units), the ratio is 1/512 or 0.001953125.

You apply this by first converting your measurement to centimeters and then multiplying by the ratio.

Here is an example:

To represent Mauna Kea, the highest peak in Hawaii at 4207m, in an Unreal Engine Level:

1.  Start by multiplying 4207 by 100 to convert the height into centimeters. This equals 420,700 cm.
2.  Next, multiply this new value by the ratio: 420,700 multiplied by 0.001953125 equals 821.6796875‬.
3.  This gives you a Z scale value of 821.6796875‬ and results in a heightmap that will go from -210,350 cm to 210,350 cm.

This process will give you the exact height of the mountain with no room for values below sea level. If you would like some additional space in your Landscape's height, adjust your initial height accordingly. To use the same example, Mauna Kea also extends 5761 m below sea level. This would give a total height to start with of 9968 m.

## Recommended Landscape Sizes

Below is a list of recommended Landscape sizes that maximize the area while minimizing the number of Landscape Components.

| Overall size (vertices) | Quads / section | Sections / Component | Landscape Component size | Total Landscape Components |
| --- | --- | --- | --- | --- |
| 8129 x 8129 | 127 | 4 (2x2) | 254x254 | 1024 (32x32) |
| 4033 x 4033 | 63 | 4 (2x2) | 126x126 | 1024 (32x32) |
| 2017 x 2017 | 63 | 4 (2x2) | 126x126 | 256 (16x16) |
| 1009 x 1009 | 63 | 4 (2x2) | 126x126 | 64 (8x8) |
| 1009 x 1009 | 63 | 1 | 63x63 | 256 (16x16) |
| 505 x 505 | 63 | 4 (2x2) | 126x126 | 16 (4x4) |
| 505 x 505 | 63 | 1 | 63x63 | 64 (8x8) |
| 253 x 253 | 63 | 4 (2x2) | 126x126 | 4 (2x2) |
| 253 x 253 | 63 | 1 | 63x63 | 16 (4x4) |
| 127 x 127 | 63 | 4 (2x2) | 126x126 | 1 |
| 127 x 127 | 63 | 1 | 63x63 | 4 (2x2) |

## Importing RAW Format Heightmaps

Unreal Engine supports importing heightmap images using the following formats:

-   16-bit grayscale PNG
-   8-bit grayscale r8
-   16-bit grayscale r16

These formats are preferred because the bit depth is known and they are assumed to be square.

Heightmap data can also be imported using the .raw format using a separate JSON file. This file is used to define the width, height, and bit depth of your heightmap.

To import a .raw heightmap file, use the process below:

1.  Create a new .JSON file located in the same folder as your heightmap.
2.  Name the file the exact same name as your heightmap.
3.  Add the following script to your file:
    
    ```
    		
                 `json              {              "width": 1024,              "height": 1024,            	 "bbp": 8              }`
    		
    Copy full snippet
    ```
    json { "width": 1024, "height": 1024, "bbp": 8 }

In the above example, the script tells the engine that the heightmap with the same name is 1024 x 1024 and has a bit depth of 8. For more information on importing heightmaps, see [Importing and Exporting Landscape Heightmaps](/documentation/en-us/unreal-engine/importing-and-exporting-landscape-heightmaps-in-unreal-engine).

## Layer Debug Mode

Enabling Layer Debug mode toggles the visibility of specific layer weights on the Landscape in the viewport. Toggle the Layer Debug mode from the viewport menu: go to **View > Landscape Visualizers**.

Enabling the Landscape Debug visualizer

When Layer Debug Visualizer is enabled, you can select individual color channels for each of the target layers in the list.

Using the Landscape Debug Visualizer to visualize your Landscape's Paint Layers.

Selecting a channel will apply a shader to the Landscape which shows the area of the selected target layer that is covered by that channel.

Landscape Debug Visualizer applied to a Landscape.