# Atmosphere Material Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/atmosphere-material-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/atmosphere-material-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:08:29

---

## Atmospheric Fog Color

The **Atmospheric Fog Color** Material Expression allows you to query the current color of the level's Atmospheric Fog, at any position in World Space. If no World Position is fed into it, then the world position of the pixel in question is used. This is useful when you need Materials to appear to fade into a distant fog color.

In the example below, The Base Color is being set using an Atmospheric Fog node, with the World Position receiving a simple network that queries the location that is always 50,000 units behind the object, relative to the position of the camera.

![Atmosphere Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abe78613-131f-4f8d-b341-28c1f270956c/atmosphere-material-expression.png)

The Atmospheric Fog Color Material Expression is deprecated in Unreal Engine 5, and should not be used. Instead, you should use the **Sky Atmosphere Component**, which is [documented on this page](/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine). You may also want to consider using [Volumetric Fog](/documentation/en-us/unreal-engine/volumetric-fog-in-unreal-engine).