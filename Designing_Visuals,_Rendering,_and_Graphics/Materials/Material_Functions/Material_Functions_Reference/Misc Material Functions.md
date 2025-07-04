# Misc Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/misc-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/misc-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:36:15

---

The Misc Material functions category includes a variety of one-off functions that do not readily fit into any of the other existing categories. They are placed here to avoid too many categories with only one function inside.

## TimeWithSpeedVariable

The **TimeWithSpeedVariable** functions just like a time node, but with an optional input for a multiplier. This function can output the multiplied result, or has an optional **Frac Time** output for only outputting the decimal places of the multiply operation.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Speed (Scalar)** | Takes in a multiplier to adjust the rate at which time plays out. Values greater than 1 will speed up the result. Values between 1 and 0 will slow it down. |
| Outputs |   |
| **Frac Time (Scalar)** | This outputs just the numbers after the decimal once the multiplier has been applied. The result is ramp wave behavior running between 0 and 1. |
| **Time (Scalar)** | The result of time multiplied by the *Speed* input. |

![Time with Speed Offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d2e6ff2-9f53-4ab4-be23-4927130b67a0/time-with-speed.png)

The Output Result will preview the node by default. In this case, the node will flicker.

## OffsetAndScaleTo1

The **OffsetAndScaleTo1** function takes in a value, offsets it by a given amount, and then scales the result back down to the 0-1 range.

| Inputs | Description |
| --- | --- |
| **Original Value (Scalar)** | The value that will be offset by the Offset Amount and then scaled back to the 0-1 range. |
| **Offset Amount (Scalar)** | This controls the amount of offset before the result is scaled back to 0-1. |

![Offset and Scale to 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b24d298-43e7-4f45-bc16-bf10a080efe4/offset-and-scale.png)

## PassThrough

As its name suggests, this node serves merely as a pass-through. Whatever is passed into it is returned unchanged via the output. It exists more for organizational purposes than anything else, as it would allow you have labeled nodes (via the Desc property) that connect much closer to another node, which is useful if the required node is far across the graph.

## SplitComponents

The **SplitComponents** function busts apart the components of an incoming color or image, giving you individual access to the red, green, or blue channels.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Color** | Takes in a given color or texture. |
| Outputs |   |
| **RGB** | Outputs the combined RGB components of a given color. |
| **R** | Outputs only the red component of the input color or texture. |
| **G** | Outputs only the green component of the input color or texture. |
| **B** | Outputs only the blue component of the input color or texture. |

![Split Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96769af5-6b73-48b5-bddf-d3d713551ca9/split-components.png)

## Flipbook

The **Flipbook** function takes in a Texture2D, such as a grid of sprite frames, and outputs an animation of them playing back in order.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Animation Phase (0-1) (Scalar)** | If this receives a static input, then the result will give the nearest frame of the flipbook as if the frames were numbered between 0 and 1. If no input is given, time is automatically used. |
| **Number of Rows (Scalar)** | This takes in the number of rows of the flipbook texture. |
| **Number of Columns (Scalar)** | This takes in the number of columns of the flipbook texture. |
| **Texture (Texture2D)** | Takes in a Texture2D containing a sprite sheet, or grid of frames of an animated texture. |
| **UVs (Vector2)** | Takes in a set of UV coordinates to assist in tiling. |
| Outputs |   |
| **Result** | Outputs an image as the result of the flipbook. |
| **UVs** | Outputs the UV coordinates corresponding with a given frame of the texture sheet. |

![FlipBook](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df727832-02ca-4a77-a3cb-c0ea12d0f70e/flipbook.png)