# Sculpt Mode

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-mode-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:32

---

The process of sculpting a Landscape involves using a variety of tools that modify the underlying heightmap. These tools range from the simple Sculpt tool that paints height values using a brush and strength scale, to many other tools that use complex algorithms to apply interesting effects to the heightmap, such as erosion. Each tool has a set of properties that determines how the tool affects the Landscape.

![Tools available in Landscape Sculpt Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a41ffe79-ad54-4b4b-95fb-bc0d1f8ba290/sculpt-mode-tools.png)

## Tool Workflow

Once you've [created your Landscape](/documentation/en-us/unreal-engine/creating-landscapes-in-unreal-engine), you will have access to the other features of the Landscape tool. To use sculpting, select the **Sculpt** mode tab.

Once selected, the Sculpt tool options will become available for choosing the type of sculpting tool along with the [brush style and falloff type](/documentation/en-us/unreal-engine/landscape-brushes-in-unreal-engine) you would like to use to apply their effects to your landscape heightmap using strokes.

![Sculpt Mode tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c56bb32-aabf-4b17-8fc9-c007058c308a/sculpt-mode-tab.png)

With your Sculpting tool selected, you can now use the following controls to start sculpting your landscape:

| **Common Controls** | **Operation** |
| --- | --- |
| **Left Mouse Button** | Performs a stroke that applies an additive application of the selected tool's effects to the heightmap and raises the terrain. |
| **Left Mouse Button + Shift** | Performs a stroke that applies an subtractive application of the selected tool's effects to the heightmap and lowers the terrain. |
| **Ctrl + Z** | Undo last stroke. |
| **Ctrl + Y** | Redo last undone stroke. |

## Sculpting Tools

Use the **Sculpting Tools** to modify the shape of your Landscape in various ways. Explore the different sculpting selections available below:

## Region Tools

Use the **Region Tools** to perform actions on specific regions of the Landscape. Explore the different Region options available below: