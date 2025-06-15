# Landscape Sculpt Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-sculpt-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:33

---

The **Sculpt** tool enables you to raise and lower the height of the Landscape heightmap in the shape of the currently selected brush and falloff.

## Using the Sculpt Tool

In this example, the Sculpt tool applies height values to raise or lower the height data for the Landscape. Simply clicking and applying movement over the region you want to paint will adjust the values based on the tool settings used.

Use the following controls to sculpt your Landscape heightmap:

| **Controls** | **Operation** |
| --- | --- |
| **Left Mouse Button** | Heightens or increases the heightmap or selected layer's weight. |
| **Shift + Left Mouse Button** | Lowers or decreases the heightmap or selected layer's weight. |

## Tool Settings

|   |   |
| --- | --- |
| ![Sculpt Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1811e183-72da-4f6d-af0d-4b61f4439a89/01-sculpt-tool.png) | ![Sculpt Tool Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1aafa6d-1f65-48ac-838f-61d032a54511/02-sculpt-tool-properties.png) |

| **Property** | **Description** |
| --- | --- |
| **Tool Strength** | Controls how much effect each brush stroke has. If you're using a pen/tablet with pressure-sensing used, this will affect the strength of the tool. |
| **Use Target Value** | Enables a target value that the tools blend toward with each brush stroke. |

The brush strength determines the amount of raising or lowering that can happen when using the Sculpting tool.