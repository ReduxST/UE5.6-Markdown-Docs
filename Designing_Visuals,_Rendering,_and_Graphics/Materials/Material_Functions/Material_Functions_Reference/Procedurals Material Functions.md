# Procedurals Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedurals-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedurals-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:35

---

The **Procedural** Material functions provide a quick way to make simple procedurally generated textures and masks. This saves memory over having to use imported textures.

## GeneratedBand

The **GeneratedBand** function generates a horizontal or vertical band from the default TextureCoordinates.

| Inputs | Description |
| --- | --- |
| **Width (Scalar)** | A 0-1 value that calculates the width of the procedural band. The default is 0.25. |
| **Sharpness (Scalar)** | This controls the falloff of the band's edges. A setting of 100 will produce a very sharp band with aliasing. |
| **Offset (Scalar)** | This value will slide the band around the texture space. |
| **Direction Switch (StaticBool)** | Setting this to *true* will cause the band to be vertical instead of horizontal. Default is *false*, or horizontal. |
| **Compare (Scalar)** | This is the value the texture coordinate is compared against in order to produce the band. The default is 0.5. |
| **Input Coordinates (Vector2)** | Takes in a custom set of UVs rather than the default ones already built into the function. |

![Generated Band](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a0f4066-5d8c-43a2-907e-6adc6750a94c/generated-band.png)

## GeneratedOffsetBands

Like the GeneratedBand function, **GeneratedOffsetBands** creates procedurally generated bands of texture across the UV space. However, this function can produce multiple bands instead of just one.

| Inputs | Description |
| --- | --- |
| **Width (Scalar)** | A 0-1 value that calculates the width of the procedural band. The default is 0.25. |
| **Sharpness (Scalar)** | This controls the falloff of the band's edges. A setting of 100 will produce a very sharp band with aliasing. |
| **Offset (Scalar)** | This value will slide the band around the texture space. |
| **Direction Switch (StaticBool)** | Setting this to *true* will cause the band to be vertical instead of horizontal. Default is *false*, or horizontal. |
| **Compare (Scalar)** | This is the value the texture coordinate is compared against in order to produce the band. The default is 0.5. |
| **Bands (Scalar)** | This modifies the total number of bands. |
| **Input Coordinates (Vector2)** | Takes in a custom set of UVs rather than the default ones already built into the function. |

![Generated Offset Bands](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4102aaa1-aad6-4f81-9132-4e4a88854bf4/generated-offset-bands.png)

## NormalFromHeightmap

This function serves as a quick way to make a normal map out of an existing black and white heightmap, rather than having to load a separate texture into memory.

This function takes in a TextureObject (T2d) expression node, rather than a TextureSample.

| Inputs | Description |
| --- | --- |
| **Coordinates (Vector2)** | Takes in the coordinates for proper scaling/tiling of the heightmap. |
| **Height Bias (Scalar)** | This is the spread used to derive a proper height from the heightmap. Default value is 0.005. |
| **Height (Scalar)** | This controls the final strength of the normal map. Default is 8. |
| **Heightmap In (TextureObject)** | Takes in the heightmap texture from a TextureObject expression node. |

![Normal From Height Map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd25456f-90c7-41bb-b1f4-ee8bd9c5ae81/normal-from-height.png)

## NormalFromHeightmapChaos

The **NormalFromHeightMapChaos** function takes a heightmap and pans it in 4 directions, then blends the result back together to make a chaotically animated normal map.

This function is considered expensive and should be used with care.

| Inputs | Description |
| --- | --- |
| **Coordinates (Vector2)** | Takes in the coordinates for proper scaling/tiling of the heightmap. |
| **Height Bias (Scalar)** | This is the spread used to derive a proper height from the heightmap. Default value is 0.005. |
| **Height (Scalar)** | This controls the final strength of the normal map. Default is 8. |

At the time of this writing, there is currently no input for a heightmap. Such an input can be added using the steps below. However, if you see a heightmap input, then this has been corrected and the steps below are not needed.

![Input correction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f2799f4-9e87-460a-90a8-c3535a133a83/add-heightmap-input.png)

1.  **Double-click** on the NormalFromHeightmapChaos function node to open it in a new Material Editor tab.
    
2.  Locate the **Texture Object** (T2d) expression node. It should currently have the default texture inside it.
    
3.  Create a **FunctionInput** expression node and connect it to the *Texture (T2d)* inputs on the 3 *Motion\_4WayChaos* function nodes.
    
4.  In the properties for the new FunctionInput expression, set the **Input Type** property to *FunctionInput\_Texture2D*.
    
5.  Set the **Input Name** property to "Heightmap In" to label the input.
    
6.  Connect the original *Texture Object (T2d)* expression node into the *Preview* input of the new FunctionInput expression node.