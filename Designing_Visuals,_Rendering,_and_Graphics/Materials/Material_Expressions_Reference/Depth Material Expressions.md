# Depth Material Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/depth-material-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/depth-material-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:19:48

---

## DepthFade

The **DepthFade** Material Expression is used to hide unsightly seams that occur when translucent objects intersect with opaque ones.

| Property | Description |
| --- | --- |
| **Fade Distance** | World space distance over which the fade should take place. This is used if the FadeDistance input is unconnected. |
| Inputs |   |
| **Opacity** | Takes in the existing opacity for the object prior to the depth fade. |
| **FadeDistance** | World space distance over which the fade should take place. |

In the comparison below, a translucent sphere intersects an opaque one (green). Note the smoother transition when DepthFade is used.

![Without Depth Fade](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d86702e3-c42f-445d-bf13-d9a9ce1de887/depth-fade-slider-01.png)

![With Depth Fade](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3b59de9-9780-4bac-9aef-75a3677dfa0e/depth-fade-slider-02.png)

The Material network for this example is pictured below.

![Depth Fade Material Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6064fe2-1be1-497c-941e-4ee1877f5967/depth-fade-graph.png)

## PixelDepth

The **PixelDepth** Material Expression outputs the depth, or distance from the camera, of the pixel currently being rendered.

|   |   |
| --- | --- |
| ![Pixel Depth Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b274390-987b-4100-a46f-9d693724287d/pixeldepthexample.png) | 
 |
| Result | Material Graph (Click to enlarge.) |

In this example, the Material network was applied to the floor. Notice how the linear interpolation blends between the two colors as the floor recedes beyond 2048 units. A Power expression was used to boost the contrast between the two colors and yield a more meaningful visual result.

## SceneDepth

The **SceneDepth** Material Expression outputs the existing scene depth. This is similar to [PixelDepth](/documentation/en-us/unreal-engine/depth-material-expressions-in-unreal-engine#pixeldepth), except that PixelDepth can sample the depth only at the pixel currently being drawn, whereas SceneDepth can sample depth at **any location**.

Only translucent materials may utilize SceneDepth.

| Inputs | Description |
| --- | --- |
| **UVs** | Takes in UV texture coordinates used to determine how the depth "texture" is sampled. |

|   |   |
| --- | --- |
| ![Scene Depth Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4196d52f-a569-494b-9813-647bbab96610/scene-depth-example.png) | 
 |
| Result | Material Graph (Click to enlarge.) |

In this example, we have applied the material network to a translucent sphere. Notice how the SceneDepth node is reading the pixels behind the sphere, rather than the ones on its surface.

The resulting normalized depth is linear in the 0.0 to 1.0 range.