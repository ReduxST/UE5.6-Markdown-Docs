# Landscape Flatten Tool

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-flatten-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-flatten-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:10

---

The **Flatten** tool pushes or pulls all other parts of the heightmap to the level that is currently under the mouse when activated. This can raise or lower the surrounding heightmap values to be the same value.

## Using the Flatten Tool

In this example, the Flatten tool is being used in the middle of the hillside to flatten out areas at the point where the mouse click was initiated. As long as the mouse is held down, the height value that was detected is used along any surface to raise or lower (depending on your tool settings) to that height.

Use the following controls to sculpt your Landscape heightmap:

| Controls | Operation |
| --- | --- |
| 
**Left Mouse Button**

 | 

Flattens or levels by both raising and lowering or individually raising and lowering the heightmap.

 |

![Before Flattening](https://dev.epicgames.com/community/api/documentation/image/253f09d8-01a7-4217-a22a-c9ef177d615d?resizing_type=fit&width=1920&height=1080)

![After Flattening](https://dev.epicgames.com/community/api/documentation/image/25eb1273-3852-4942-98e1-af2a8686a11a?resizing_type=fit&width=1920&height=1080)

Before Flattening

After Flattening

The brush strength determines the amount of Flattening that can happen when using the Flatten tool.

## Tool Settings

|  |  |
| --- | --- |
| 
[![Flatten Tool](https://dev.epicgames.com/community/api/documentation/image/09f48b82-f352-4c39-97d7-659d80f35efe?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/09f48b82-f352-4c39-97d7-659d80f35efe?resizing_type=fit)



 | 

[![Flatten Tool Properties](https://dev.epicgames.com/community/api/documentation/image/2b75ff61-d26d-4422-a90c-225dbc0bde84?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2b75ff61-d26d-4422-a90c-225dbc0bde84?resizing_type=fit)



 |

| Property | Description |
| --- | --- |
| 
**Flatten Target**

 | 

Sets the target height toward which to flatten.

 |
| 

**Tool Strength**

 | 

Controls how much smoothing occurs with each brush stroke has.

 |
| 

**Flatten Mode**

 | 

Determines whether the tool will raise or lower the heightmap section under the brush.

-   **Both**: Raises and lowers values to the current height value when the mouse click is activated.
    
-   **Raise**: Raises values that are lower than the currently selected height when the mouse click is activated. Any values above this clicked point will be left unchanged.
    
-   **Lower**: Lower values that are higher than the currently selected height when the mouse click is activated. Any values lower than this clicked point will be left unchanged.
    

 |
| 

**Use Slope Flatten**

 | 

If checked, flattens along the Landscape's existing slope instead of flattening toward a horizontal plane.

 |
| 

**Pick Value Per Apply**

 | 

If checked, constantly selects new values to flatten toward, instead of only using the first clicked point.

 |
| Advanced |   |
| --- | --- |
| 

**Show Preview Grid**

 | 

When Flatten Target is enabled, you can enable this option to show a preview grid for the flatten target height.

 |
| 

**Terrace Interval**

 | 

Sets the height of the Terrace interval for Terrace Flatten mode.

 |
| 

**Terrace Smoothing**

 | 

Sets the smoothing value for Terrace Flatten mode

 |