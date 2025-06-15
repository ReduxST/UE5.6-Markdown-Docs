# Opacity Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/opacity-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/opacity-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:04

---

Opacity Material Functions exist to speed up the handling of complex opacity calculations.

## SoftOpacity

The **SoftOpacity** function takes in an Opacity value and then runs a variety of calculations on it to give it a softer feel. It applies a Fresnel effect, depth-based alpha, and pixel depth. The end result causes the object to fade away as the camera approaches it.

| Item | Description |
| --- | --- |
| Inputs |   |
| **DepthFadeDistance (Scalar)** | The depth at which objects have completely faded away. Only viable if using the *OutputUsesDepthBias* output. |
| **OpacityIn (Scalar)** | This is the incoming opacity value. |
| **FadeDistance (Scalar)** | How close you should get to the surface before it starts fading out. |
| Outputs |   |
| **OutputUsesDepthBias** | This output causes the object to fade completely away to complete transparency by the time it reaches the distance set in the *DepthFadeDistance* input. |
| **OutputNoDepthBias** | This output causes the object to fade completely away as it reaches the camera, meaning there is no offset. This output is 12 instructions less expensive than *OutputUsesDepthBias*. |

![Soft Opacity](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f12cc3b-5b1a-45ce-b283-f0e3e8930eb3/soft-opacity.png)

In this example, the cylinder appears more transparent along the edges, where the mesh curves away from the camera. This is due to the Fresnel effect in the Material Function.