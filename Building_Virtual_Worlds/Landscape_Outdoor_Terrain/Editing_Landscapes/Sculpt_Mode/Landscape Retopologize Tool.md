# Landscape Retopologize Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-retopologize-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-retopologize-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:31

---

The **Retopologize** tool automatically adjusts Landscape vertices with an X/Y offset map to improve vertex density in areas that need it, like steep cliffs. This allows for reduced texture stretching in these types of areas by spreading the vertices into these areas that are less dense.

An X/Y offset map will make the Landscape slower to render and paint on with other tools, so only use the Retopologize tool if needed.

## Using the Retopologize Tool

In this example, we have a steep incline that was created by flattening an area, however, it left these vertical areas with fewer Landscape vertices spread across the surface which caused the textures to appear stretched and some jagged artifacts around the edges of the flattened area. By using the Retopologize tool the surrounding vertices have been pulled and redistributed without significantly altering the work that was done to make the flattened area. This reduces the stretching and jagged edges that appear.

Use the following controls to paint an X/Y offset map to retopologize your Landscape heightmap:

| **Controls** | **Operation** |
| --- | --- |
| **Left Mouse Button** | Heightens or increases the heightmap or selected layer's weight. |

**Retopologize Lit View**

![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/662f9d21-cc82-4554-9a44-1ef16e669010/01-before-retopologize-lit-view.png "Before")

![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ec74335-2d0d-4a2d-9326-c1fffa29a859/02-after-retopologize-lit-view.png "After")

**Retopologize Wireframe View**

![Before](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5876a1d9-74d2-4257-b8bd-1d8bbf37a1e0/03-before-retopologize-wireframe-view.png "Before")

![After](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bfe5640-d703-444c-a3fa-8733ac938c6e/04-after-retopologize-wireframe-view.png "After")

In these comparison examples, you can see how the texture stretching has been reduced in these sharp inclines for the lit view and with the wireframe view you can see how the vertices have been redistributed to be more evenly spaced in these steep inclines.

### Tool Settings

![Retopologize Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bfe5762-d14a-45b7-b794-f46fe15fac65/05-retopologize-tool.png "Retopologize Tool")

There are no tool settings specific to Retopologize that can be adjusted. Simply select the tool from the selection and paint the areas in your Landscape that need to have their vertex density redistributed.