# Utility Material Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/utility-material-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:29

---

**Utility Material Expressions** are nodes that can affect Materials in a number of different ways than one might be used to. For example the **GIReplace** node will replace an object's indirect bounce color with a given value you input, while the Linear Interpolate node will help blend between two textures based on an Alpha input. On the following page you will find detailed descriptions for all of the Utility expressions are available in the Material Editor.

## AntialiasedTextureMask

The **AntialiasedTextureMask** expression allows you to create a Material using a soft (anti-aliased) transition mask. The mask can be used to blend between two complex Material properties or to fade out an alpha blended Material (works well with SoftMasked). Specify a texture with the mask specified in one channel (red, green, blue, or alpha), set the used channel in the expression and specify the comparison value. Assuming the channel stores a grayscale value in the range 0 = black to 1 = white the comparison function defines if the resulting mask should be 0 or 1. This expression is a parameter, allowing the **Texture** property to be overridden by child MaterialInstances.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Threshold**

 | 

Specifies the value used as the cutoff point in pixel coverage. Pixel coverage values less than this become black; values greater become white.

 |
| 

**Channel**

 | 

Specifies the channel of the Texture to use as the mask.

 |
| 

**Texture**

 | 

Specifies the mask texture to use.

 |
| Inputs |   |
| --- | --- |
| 

**UVs**

 | 

Takes in texture coordinates to apply to the texture mask.

 |

**Pseudo code:**

C++

`Result = 1     if TextureLookup < Threshold then Result = 0`

Result = 1 if TextureLookup &lt; Threshold then Result = 0

Copy full snippet(2 lines long)

The actual implementation is quite a bit more complicated as it tries to return values between 0 and 1 depending on the actual pixel coverage to avoid aliasing.

Example (this tiny 128x128 texture, uncompressed for best quality):

[![ULogoLowBlurred.png](https://dev.epicgames.com/community/api/documentation/image/9ff5c452-c621-4c1d-b04c-27c111a7f94f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9ff5c452-c621-4c1d-b04c-27c111a7f94f?resizing_type=fit)

Was used as a normal texture (left top) and used with the described material expression (bottom right):

[![AAMasked_Demo.png](https://dev.epicgames.com/community/api/documentation/image/09c91591-a784-4be8-8651-4d2ab6ea06c5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/09c91591-a784-4be8-8651-4d2ab6ea06c5?resizing_type=fit)

The technique works best in magnification and with blurred input content. Compression hurts the quality a lot so try to use uncompressed low resolution textures.

## BlackBody

The **BlackBody** expression simulates the effects of [black body radiation](http://en.wikipedia.org/wiki/Black-body_radiation) within your Material. The user inputs a temperature (in Kelvin) and the resulting color and intensity can be used to drive Base Color and Emissive values to get a physically accurate result.

[![Blackbody Expression](https://dev.epicgames.com/community/api/documentation/image/ba5b19cc-ed8b-4483-ac9d-06259e4e7d70?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ba5b19cc-ed8b-4483-ac9d-06259e4e7d70?resizing_type=fit)

## BumpOffset

**BumpOffset** is the Unreal Engine 4 term for what is commonly known as 'Parallax Mapping'. The Bump Offset expression allows a material to give the illusion of depth without the need for additional geometry. BumpOffset materials use a grayscale *heightmap* to give depth information. The brighter the value in the heightmap, the more 'popped out' the material will be; these areas will parallax (shift) as a camera moves across the surface. Darker areas in the heightmap are 'further away' and will shift the least.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**HeightRatio**

 | 

Multiplier for the depth taken from the *heightmap*. The larger the value, the more extreme the depth will be. Typical values range from 0.02 to 0.1.

 |
| 

**ReferencePlane**

 | 

Specifies the approximate height in texture space to apply the effect. A value of 0 will appear to distort the texture completely off the surface, whereas a value of 0.5 (the default) means that some of the surface will pop off while some areas will be sunken in.

 |
| Inputs |   |
| --- | --- |
| 

**Coordinate**

 | 

Takes in base texture coordinates to be modified by the expression.

 |
| 

**Height**

 | 

Takes in the texture (or a value) to be used as the heightmap.

 |
| 

**HeightRatioInput**

 | 

Multiplier for the depth taken from the *heightmap*. The larger the value, the more extreme the depth will be. Typical values range from 0.02 to 0.1. If used, this input supersedes any value in the Height Ratio property.

 |

[![Bump Offset Expression](https://dev.epicgames.com/community/api/documentation/image/1038d30e-27ea-4721-99ed-0e1d65db48f1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1038d30e-27ea-4721-99ed-0e1d65db48f1?resizing_type=fit)

## ConstantBiasScale

The **ConstantBiasScale** expression takes an input value, adds a bias value to it, and then multiplies it by a scaling factor outputting the result. So for example, to convert input data from \[-1,1\] to \[0,1\] you would use a bias of 1.0 and a scale of 0.5.

| Properties | Description |
| --- | --- |
| 
**Bias**

 | 

Specifies the value to be added to the input.

 |
| 

**Scale**

 | 

Specifies the multiplier for the biased result.

 |

[![Constant Bias Scale Expression](https://dev.epicgames.com/community/api/documentation/image/cd071141-b35c-450e-a257-10b2a6112e6a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cd071141-b35c-450e-a257-10b2a6112e6a?resizing_type=fit)

## DDX

The **DDX** expression exposes DDX derivative calculation, a GPU hardware feature used in pixel shader calculation.

## DDY

The **DDY** expression exposes DDX derivative calculation, a GPU hardware feature used in pixel shader calculation.

## DepthFade

The **DepthFade** expression is used to hide unsightly seams that take place when translucent objects intersect with opaque ones.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Fade Distance**

 | 

World space distance over which the fade should take place. This is used if the FadeDistance input is unconnected.

 |
| Inputs |   |
| --- | --- |
| 

**Opacity**

 | 

Takes in the existing opacity for the object prior to the depth fade.

 |
| 

**FadeDistance**

 | 

World space distance over which the fade should take place.

 |

![Without Depth Fade](https://dev.epicgames.com/community/api/documentation/image/6b54ecb4-5b8f-4100-8d71-048e90d36058?resizing_type=fit&width=1920&height=1080)

![With Depth Fade](https://dev.epicgames.com/community/api/documentation/image/6af200ab-476b-44b8-b307-b14a143762b0?resizing_type=fit&width=1920&height=1080)

Without Depth Fade

With Depth Fade

The Material network for this example is pictured below.

[![Depth Fade Material Graph](https://dev.epicgames.com/community/api/documentation/image/e0069ebe-cb51-478d-a016-a782520080f0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0069ebe-cb51-478d-a016-a782520080f0?resizing_type=fit)

## DepthOfFieldFunction

The **Depth of Field Function** expression is designed to give artists control over what happens to a Material when it is being blurred by Depth of Field. It outputs a value between 0-1 such that 0 represents "in focus" and 1 represents "completely blurred." This is useful for interpolating between sharp and blurry versions of a texture, for instance. The Depth input allows for the existing results from the scene's Depth of Field calculations to be overridden by other calculations.

![Blended Colors](https://dev.epicgames.com/community/api/documentation/image/f1399c21-712e-4034-ac7c-940604716185?resizing_type=fit&width=1920&height=1080)

![Blending regular and blurred textures](https://dev.epicgames.com/community/api/documentation/image/5a2ae174-b794-4596-9dae-f725c5cce56c?resizing_type=fit&width=1920&height=1080)

Blended Colors

Blending regular and blurred textures

[![Depth of Field function](https://dev.epicgames.com/community/api/documentation/image/189bdf95-0221-4840-b856-6f3fb160062f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/189bdf95-0221-4840-b856-6f3fb160062f?resizing_type=fit)

Click image for full size view.

## Desaturation

The **Desaturation** expression desaturates its input, or converts the colors of its input into shades of gray, based a certain percentage.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Luminance Factors**

 | 

Specifies the amount that each channel contributes to the desaturated color. This is what controls that green is brighter than red which is brighter than blue when desaturated.

 |
| Inputs |   |
| --- | --- |
| 

**Fraction**

 | 

Specifies the amount of desaturation to apply to the input. Percent can range from 0.0 (full original color, no desaturation) to 1.0 (fully desaturated).

 |

[![Desaturation Example](https://dev.epicgames.com/community/api/documentation/image/1123c67c-3d78-429e-8a30-d917472004b4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1123c67c-3d78-429e-8a30-d917472004b4?resizing_type=fit)

**Programmers:** Define desaturated color `D`, input color `I` and luminance factor `L`. The output will be `O = (1 - Percent)*( D.dot( I )) + Percent * I`

## Distance

The **Distance** expression computes the (Euclidian) distance between two points/colors/positions/vectors and outputs the resulting value. This works on one, two, three and four component vectors, but both inputs to the expression must have the same number of channels.

| Item | Description |
| --- | --- |
| Inputs |   |
| --- | --- |
| 
**A**

 | 

Takes in a value or vector of any length.

 |
| 

**B**

 | 

Takes in a value or vector of any length.

 |

![Note how the color changes as the camera distance increases.](https://dev.epicgames.com/community/api/documentation/image/c64edd57-f128-4f51-80ac-21d48bcb68a5?resizing_type=fit&width=1920&height=1080)![Note how the color changes as the camera distance increases.](https://dev.epicgames.com/community/api/documentation/image/bee45474-c093-4977-8c80-798e7ab9bfe3?resizing_type=fit&width=1920&height=1080)

**Note how the color changes as the camera distance increases.**

**Pseudo code:**

C++

`Result = length (A - B)`

Result = length (A - B)

Copy full snippet(1 line long)

**Low level HLSL code:**

C++

`float Result = sqrt (dot (A-B, A-B))`

float Result = sqrt (dot (A-B, A-B))

Copy full snippet(1 line long)

## DistanceFieldGradient

The **DistanceFieldGradient** Material Expression node, when normalized, outputs the X,Y,Z direction an object would move with in the distance field. This makes the Distance Field Gradient Material Expression node well-suited for Materials that need to simulate the flow of liquids.

**Generate Mesh Distance Fields** must be enabled in **Project Settings** under **Rendering** for this expression to work correctly.

| Item | Description |
| --- | --- |
| 
**Position**

 | 

Defaults to current World Position if nothing is input.

 |

Here is an example of how to use the **DistanceFieldGradient** Material Expression in your Materials. In this example below make sure to note that the DistanceFieldGradient was first normalized and then input into a Mask Channel node. The reason for this is because without normalizing the DistanceFieldGradient first you can not get directional data. The Mask Channel Parameter was added to allow for easier RGB channel switching with in the Material Instance.

[![Distance field gradient](https://dev.epicgames.com/community/api/documentation/image/dbdd0a6a-3215-410d-8445-a1d1e53f9262?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dbdd0a6a-3215-410d-8445-a1d1e53f9262?resizing_type=fit)

Click image for full size view.

Here is an example of the DistanceFieldGradient in action. The image below shows what data the DistanceFieldGradient will use when the various RGB are enabled.

[![](https://dev.epicgames.com/community/api/documentation/image/7b29e9bc-da49-4115-8267-4bf3697ceb39?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7b29e9bc-da49-4115-8267-4bf3697ceb39?resizing_type=fit)

Click image for full size view.

| Number | Description |
| --- | --- |
| 
**1**

 | 

Enabling the R channel and disabling all other channels.

 |
| 

**2**

 | 

Enabling the G channel and disabling all other channels.

 |
| 

**3**

 | 

Enabling the B channel and disabling all other channels.

 |

## DistanceToNearestSurface

The **Distance To Nearest Surface** Material Expression node allows Materials to sample any point in the levels Global Distance Field. This Material Expression works by outputting the signed distance in world space units from the distance field to the nearest occluders in the scene.

**Generate Mesh Distance Fields** must be enabled in **Project Settings** under **Rendering** for this expression to work correctly.

| Item | Description |
| --- | --- |
| 
**Position**

 | 

Defaults to current World Position if nothing is input.

 |

Here is an example of the **Distance To Nearest Surface** Material Expression in action.

[![Distance to Surface](https://dev.epicgames.com/community/api/documentation/image/5df17fa9-83c4-4f01-9fec-8e0ceeb63f3a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5df17fa9-83c4-4f01-9fec-8e0ceeb63f3a?resizing_type=fit)

Click image for full size view.

[![](https://dev.epicgames.com/community/api/documentation/image/9657c903-1e9d-45e0-a434-0692102180d4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9657c903-1e9d-45e0-a434-0692102180d4?resizing_type=fit)

In this example the Distance To Nearest Surface was fed into the Opacity input on a Material and that Material was applied to a Static Mesh plane that was placed just above the levels floor. What the Distance To Nearest Surface is doing is telling the Material to only color areas red were the Static Meshes plane will start to intersect other Static Meshes placed in the scene.

## FeatureLevelSwitch

The **Feature Level Switch** node allows you to make simplified materials for lower powered devices.

**Example Usage**: You might have a material with 10 textures overlapping and complex math, but just a single static texture for mobile (feature level ES2).

| Inputs | Description |
| --- | --- |
| 
**Default**

 | 

The default Feature Level.

 |
| 

**ES2**

 | 

Feature Level defined by the core capabilities of OpenGL ES2.

 |
| 

**ES3.1**

 | 

Feature Level defined by the capabilities of Metal-level devices.

 |
| 

**SM4**

 | 

Feature Level defined by the core capabilities of DX10 Shader Model 4.

 |
| 

**SM5**

 | 

Feature Level defined by the core capabilities of DX11 Shader Model 5.

 |

## Fresnel

The **Fresnel** expression calculates a falloff based on the dot product of the surface normal and the direction to the camera. When the surface normal points directly at the camera, a value of 0 is output. When the surface normal is perpendicular to the camera, a value of 1 is output. The result is clamped to \[0,1\] so you do not have any negative color in the center.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Exponent**

 | 

Specifies the how quickly the output value falls off. Larger values mean tighter or quicker falloff.

 |
| 

**Base Reflect Fraction**

 | 

Specifies the fraction of specular reflection the surface is viewed from straight on. A value of 1 effectively disables the Fresnel effect.

 |
| Inputs |   |
| --- | --- |
| 

**ExponentIn**

 | 

Specifies the how quickly the output value falls off. Larger values mean tighter or quicker falloff. If used, value will always supersede the Exponent property value.

 |
| 

**Base Reflect Fraction**

 | 

Specifies the fraction of specular reflection the surface is viewed from straight on. A value of 1 effectively disables the Fresnel effect. If used, value will always supersede the Exponent property value.

 |
| 

**Normal**

 | 

Takes in a three-channel vector value representing the normal of the surface, in world space. To see the results of a normal map applied to the surface of the Fresnel object, connect the normal map to the Normal input of the material, then connect a [PixelNormalWS](https://dev.epicgames.com/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine) expression to this input on the Fresnel. If no normal is specified, the tangent normal of the mesh is used.

 |

[![Fresnel Example](https://dev.epicgames.com/community/api/documentation/image/88827916-4412-45e6-bf31-dc8431941fe1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/88827916-4412-45e6-bf31-dc8431941fe1?resizing_type=fit)

## GIReplace

**GIReplace** allows artists to specify a different, usually simpler, expression chain when the material is being used for GI.

**Example Usage**: Lightmass static GI and LPV dynamic GI use it.

| Inputs | Description |
| --- | --- |
| 
**Default**

 | 

The default GI.

 |
| 

**StaticIndirect**

 | 

Used for baked indirect lighting.

 |
| 

**DynamicIndirect**

 | 

Used for dynamic indirect lighting.

 |

## LightmassReplace

The **LightmassReplace** expression simply passes through the Realtime input when compiling the material for normal rendering purposes, and passes through the Lightmass input when exporting the material to Lightmass for global illumination. This is useful to work around material expressions that the exported version cannot handle correctly, for example WorldPosition.

| Inputs | Description |
| --- | --- |
| 
**Realtime**

 | 

Takes in the value(s) to pass through for normal rendering.

 |
| 

**Lightmass**

 | 

Takes in the value(s) to pass through when exporting the material to Lightmass.

 |

## LinearInterpolate

The **LinearInterpolate** expression blends between two input value(s) based on a third input value used as a mask. This can be thought of as a mask to define transitions between two textures, like a layer mask in Photoshop. The intensity of the mask Alpha determines the ratio of color to take from the two input values. If Alpha is 0.0, the first input is used. If Alpha is 1.0, the second input is used. If Alpha is between 0.0 and 1.0, the output is a blend between the two inputs. Keep in mind that the blend happens per channel. So, if Alpha is an RGB color, Alpha's red channel value defines the blend between A and B's red channels **independently** of Alpha's green channel, which defines the blend between A and B's green channels.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Const A**

 | 

The value mapped to 0.0. Only used if the A input is unconnected.

 |
| 

**Const B**

 | 

The value mapped to 1.0. Only used if the B input is unconnected.

 |
| 

**Const Alpha**

 | 

Takes in the value to use as the mask alpha. Only used if the Alpha input is unconnected.

 |
| Inputs |   |
| --- | --- |
| 

**A**

 | 

Takes in the value(s) mapped to 0.0.

 |
| 

**B**

 | 

Takes in the value(s) mapped to 1.0.

 |
| 

**Alpha**

 | 

Takes in the value to use as the mask alpha.

 |

**Programmers:** LinearInterpolate does a per-channel lerp between A and B based on the parametric value Alpha.

[![Lerp Example](https://dev.epicgames.com/community/api/documentation/image/bb7d87b0-52d0-439f-95a5-c803230f69ce?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bb7d87b0-52d0-439f-95a5-c803230f69ce?resizing_type=fit)

## Noise

The **Noise** expression creates a procedural noise field, giving you control over how it is generated.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Scale**

 | 

Changes the overall size of the noise cells. Lower numbers make the noise bigger.

 |
| 

**Quality**

 | 

A look/performance setting. Lower values are faster but may look worse, higher values are slower but may look better.

 |
| 

**Function**

 | 

-   **Simplex** (Texture Based): High quality for direct use and bumps about 77 instructions per level, 4 Texture lookups, can not tile.
    
-   **Gradient** (Texture Based): High quality for direct use and bumps. Non-tiled: about 61 instructions per level, 8 Texture lookups. Tiling: about 74 instructions per level, 8 Texture lookups. Even "non tiled' mode has a repeat of 128. Useful repeat size range <= 128. Formerly labeled as Perlin Noise.
    
-   **Fast Gradient** (3D Texture): High quality for direct use, **BAD** for bumps. about 16 instructions per level, 1 Texture lookup. Always tiles with a repeat of 16, "Tiling" mode is not an option for Fast Gradient noise.
    
-   **Gradient** (Computational): High quality for direct use and bumps. Non-tiled: about 80 instructions per level, no Textures. Tiling: about 143 instructions per level, no Textures.
    
-   **Value** (Computational): Low quality, but pure computation. Non-tiled: about 53 instructions per level, no Textures. Tiling: about 118 instructions per level, no Textures. Formerly mislabeled as Gradient noise.
    
-   **Voronoi**: Also know as Worley or Cellular noise. Quality = 1 searches 8 cells, Quality = 2 searches 16 cells, Quality = 3 searches 27 cells, Quality = 4 searches 32 cells. All are about about 20 instructions per cell searched.
    

 |
| 

**Turbulence**

 | 

With Turbulence on, each noise octave will add only absolute values to the result. Changes the visual characteristics and can great shapes resembling sharp mountain ridges

 |
| 

**Levels**

 | 

How many different levels of noise at different scales to combine, multiplies the computational cost by the number of levels.

 |
| 

**Output Min**

 | 

The lowest value output by the noise calculation.

 |
| 

**Output Max**

 | 

The highest value output by the noise calculation.

 |
| 

**Level Scale**

 | 

Level scale is always active and determines how much the scale changes for each new octave.

 |
| 

**Tiling**

 | 

For noise functions that support it, allows noise to tile. This is more expensive, but useful when baking noise into a seamless wrapping texture.

 |
| 

**Repeat Size**

 | 

When tiling, how often should the noise repeat.

 |
| Inputs |  |
| --- | --- |
| 

**Position**

 | 

Allows the texture size to be adjusted via a 3D vector.

 |
| 

**FilterWidth**

 | 

In effect, controls how much blur will be applied to the noise texture.

 |

[![Noise Example](https://dev.epicgames.com/community/api/documentation/image/5830b58e-faba-43aa-a206-e2f4d48231e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5830b58e-faba-43aa-a206-e2f4d48231e0?resizing_type=fit)

## Previous Frame Switch

The **Previous Frame Switch** Material Expression assists with the implementation of complex [vertex animations](https://dev.epicgames.com/documentation/en-us/unreal-engine/vertex-animation-tool-in-unreal-engine) in Materials by providing a way to generate correct motion vectors which work correctly with Temporal AA and Motion Blur.

Materials that are only a function of time already work without modification, however, they cannot account for other variables, such as Material Parameters, that can affect the animation at runtime. The Previous Frame Switch Material Expression provides a means to solve these problems manually by tracking how these parameters change. For example, in Blueprints they could manually provide expressions for motion vector generation that is caused by changes in World Position Offset between frames.

Velocities from vertex deformation must be enabled in **Project Settings** under **Rendering** for this expression to work.

-   4.24 and later versions use **Accurate velocities from Vertex Deformation**
    
-   4.25 and future versions use **Output velocities due to vertex deformation**
    

| Item | Description |
| --- | --- |
| 
Current Frame

 | 

Directional Vector used as the starting position reference.

 |
| 

Previous Frame

 | 

Directional Vector used as the XYZ reference for the amount of blur to add.

 |

Here is an example using **Previous Frame Switch** Material Expression in a Material.

[![Previous Frame Switch](https://dev.epicgames.com/community/api/documentation/image/3f971fed-7970-4eba-a7f2-f84472c26215?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3f971fed-7970-4eba-a7f2-f84472c26215?resizing_type=fit)

In this example, the Previous Frame Switch is using a constant value to control the directional blur through a Multiply node.

In this example, you can see how this is being used in Epic's own games, like Fortnite, to control the motion blur with a Vertex Animation that assembles on screen. The animation on the right is using Previous Frame Switch to add some motion blur, while the animation on the left is not.

#### Viewport Show Flag

There is a show flag in the Editor viewport under **Show** > **Visualize** > **Previous Frame's Reprojection** that you can use with the **Previous Frame Switch** to diagnose and correct discrepancies in the directional vectors of the current and previous frame.

[![Previous Frame Reprojection Show Flag](https://dev.epicgames.com/community/api/documentation/image/b9be4c80-39cf-4620-8274-7fe6d4443125?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b9be4c80-39cf-4620-8274-7fe6d4443125?resizing_type=fit)

When enabled, this visualizer compares the current frame color with the previous, and returns the difference between the two frames. When the difference is zero, the Material appears gray in the viewport (pictured left). When the directional vectors do not match, the Material displays a colored overlay (pictured right).

[![Previous Frame Reprojection example](https://dev.epicgames.com/community/api/documentation/image/dfa12004-8cc3-4b4f-bce4-0e7896c2cd6e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dfa12004-8cc3-4b4f-bce4-0e7896c2cd6e?resizing_type=fit)

## QualitySwitch

The **QualitySwitch** expression allows for the use of different expression networks based on the engine is switched between quality levels, such as using lower quality on lower-end devices.

| Inputs | Description |
| --- | --- |
| 
Default

 | 

This input is used for networks designed for default visual quality.

 |
| 

Low

 | 

This input is used for networks designed for lower visual quality.

 |
| 

High

 | 

This input is used for networks designed for higher visual quality.

 |

## RotateAboutAxis

The **RotateAboutAxis** expression rotates a three-channel vector input given the rotation axis, a point on the axis, and the angle to rotate. This node outputs the Delta to the rotated position, not the fully rotated position itself. This makes it a useful and easy way to input the result into the World Position Offset input for simple rotations.

| Inputs | Description |
| --- | --- |
| 
**NormalizedRotationAxis**

 | 

Takes in a normalized (0-1) vector which represents the axis about which the object will rotate.

 |
| 

**RotationAngle**

 | 

The angle of rotation. A value of 1 equals a full 360-degree rotation.

 |
| 

**PivotPoint**

 | 

Takes in the three-channel vector representing the pivot point about which the object will rotate.

 |
| 

**Position**

 | 

Takes in the three-channel vector representing the position of the object.

 |

[![Rotate About Axis](https://dev.epicgames.com/community/api/documentation/image/bbee1724-00c1-404e-82df-a7563aeb799d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bbee1724-00c1-404e-82df-a7563aeb799d?resizing_type=fit)

In the above example, the preview plane would appear to spin on its vertical axis.

## SphereMask

The **SphereMask** expression outputs a mask value based on a distance calculation. If one input is the position of a point and the other input is the center of a sphere with some radius, the mask value is 0 outside and 1 inside with some transition area. This works on one, two, three, and four component vectors

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Attenuation Radius**

 | 

Specifies the radius to use for the distance calculation.

 |
| 

**Hardness Percent**

 | 

Specifies the transition area size. This works like the Photoshop brush hardness value. 0 means the transition is hard, 100 means the transition area is maximal(soft).

 |
| Inputs |   |
| --- | --- |
| 

**A**

 | 

Takes in the value representing the position of the point to check.

 |
| 

**B**

 | 

Takes in the value representing the center of the sphere.

 |

![The node outputs a value of 1 until the camera passes beyond a certain distance, after which it outputs 0.](https://dev.epicgames.com/community/api/documentation/image/89204f07-79d4-4593-9793-04ffc7e12b71?resizing_type=fit&width=1920&height=1080)![The node outputs a value of 1 until the camera passes beyond a certain distance, after which it outputs 0.](https://dev.epicgames.com/community/api/documentation/image/914e7da9-918c-430b-a416-ef7472dc4346?resizing_type=fit&width=1920&height=1080)

**The node outputs a value of 1 until the camera passes beyond a certain distance, after which it outputs 0.**

## Thin Translucent

The **Thin Translucent Material Output** expression accurately represents physically based transparent materials in a single pass. This enables you to create *true* tinted or colored transparent materials that accurately respond to lighting and shading.

[![Thin Translucent Graph](https://dev.epicgames.com/community/api/documentation/image/6aa1e7e4-48e2-4469-bfbe-60c7f54264e8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6aa1e7e4-48e2-4469-bfbe-60c7f54264e8?resizing_type=fit)

Click image for full size.

When creating a tinted glass material, a white specular highlight and tinted background are needed. These are rendered in a single pass with a physically based shader that accounts for light bounces from the air into the glass and the glass into the air.

![Standard Translucent Shading Model](https://dev.epicgames.com/community/api/documentation/image/ffbf0497-fcb7-471f-b3d8-57c837cd9784?resizing_type=fit&width=1920&height=1080)

![Thin Translucent Shading Model](https://dev.epicgames.com/community/api/documentation/image/85a451c9-261a-4866-90e0-2a7fad85fefd?resizing_type=fit&width=1920&height=1080)

Standard Translucent Shading Model

Thin Translucent Shading Model

Enable Thin Translucent material output by setting the following in the Material Details panel:

-   **Blend Mode:** Translucent
    
-   **Shading Model:** Thin Translucent
    
-   **Lighting Mode:** Surface ForwardShading
    

## Vector Noise

[![](https://dev.epicgames.com/community/api/documentation/image/faf9d63f-cd92-4fa5-ac47-6f5d60120dd2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/faf9d63f-cd92-4fa5-ac47-6f5d60120dd2?resizing_type=fit)

The Vector Noise Material expression adds several more 3D or 4D vector noise results to use in your Materials. Due to the run-time expense of these functions, it is recommended that once a look is developed with them, all or part of the computation be baked into a Texture using the Render Targets feature.

These Material graph Expressions allow procedural looks to be developed in the engine on final assets, providing an alternative to creating procedurally generated Textures with an external tool. Inside the Vector Noise Material Expression, you will find the following Vector Noise types.

| Image | Item | Description |
| --- | --- | --- |
| 
[![Cellnoise](https://dev.epicgames.com/community/api/documentation/image/6b4711eb-41cd-421c-8be7-3eba44813edb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b4711eb-41cd-421c-8be7-3eba44813edb?resizing_type=fit)



 | 

**Cellnoise**

 | 

Returns a random color for each cell in a 3D grid (i.e. from the mathematical floor operation applied to the node input). The results are always consistent for a given position, so can provide a reliable way to add randomness to a Material. This Vector Noise function is extremely cheap to compute, so it is not necessary to bake it into a Texture for performance.

 |
| 

[![Perlin 3D noise](https://dev.epicgames.com/community/api/documentation/image/c440bc87-d793-4dd8-b059-d148f9dd22a9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c440bc87-d793-4dd8-b059-d148f9dd22a9?resizing_type=fit)



 | 

**Perlin 3D Noise**

 | 

Returns a random color for each cell in a 3D grid (i.e. from the mathematical floor operation applied to the node input). The results are always consistent for a given position, so can provide a reliable way to add randomness to a Material. This Vector Noise function is extremely cheap to compute, so it is not necessary to bake it into a Texture for performance.

 |
| 

[![Perlin Gradient](https://dev.epicgames.com/community/api/documentation/image/8a6f6175-6e59-4b60-9577-4c9d9fcdcdfb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8a6f6175-6e59-4b60-9577-4c9d9fcdcdfb?resizing_type=fit)



 | 

**Perlin Gradient**

 | 

Computes the analytical 3D gradient of a scalar Perlin Simplex Noise. The output is four channels, where the first three (RGB) are the gradient, and the fourth (A) is the scalar noise. This noise type is useful for bumps on a surface or for flow maps.

 |
| 

[![Perlin Curl](https://dev.epicgames.com/community/api/documentation/image/7ffc20b6-b50d-4d83-9a50-c1e87d6b356b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7ffc20b6-b50d-4d83-9a50-c1e87d6b356b?resizing_type=fit)



 | 

**Perlin Curl**

 | 

Computes the analytical 3D curl of a vector Perlin Simplex Noise (aka Curl Noise). The output is a 3D signed curl vector and is useful for fluid or particle flow.

 |
| 

[![Voronoi Noise](https://dev.epicgames.com/community/api/documentation/image/ae0c1ff3-1ccf-497f-8b94-64a520d6f045?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ae0c1ff3-1ccf-497f-8b94-64a520d6f045?resizing_type=fit)



 | 

**Voronoi**

 | 

Computes the same Voronoi noise as the scalar Noise material node. The scalar Voronoi noise scatters seed points in 3D space and returns the distance to the closest one. The Vector Noise version returns the location of the closest seed point in RGB, and the distance to it in A. Especially coupled with Cellnoise, this can allow some randomized behavior per Voronoi cell.

 |

Below is a simple stone bed Material using the distance component of the Voronoi Vector Noise to modulate some surface bumps and blend moss into the cracks. The seed position together with Vector Noise > Cellnoise is used to change the color and bump height per rock.

[![Stone blend example](https://dev.epicgames.com/community/api/documentation/image/8c5f4711-87a7-41fc-a2bc-3a61581b6fd3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8c5f4711-87a7-41fc-a2bc-3a61581b6fd3?resizing_type=fit)

The derivative-based operations **Perlin Curl** and **Perlin Gradient** can be added together in octaves, just as regular Perlin noise can. For derivatives of more complex expressions, it is necessary to compute the gradient of the result of the expression. To help with this, place the expression to compute into a Material Function and use it with the following helper nodes.

| Item | Description |
| --- | --- |
| 
**Prepare3DDeriv**

 | 

Uses positions offset in a tetrahedral pattern to compute 3D derivatives. Evaluate the same 3D function at each offset position produced by this function, then feed the resulting values into Compute3DDeriv.

 |
| 

**Compute3DDeriv**

 | 

Uses positions offset in a tetrahedral pattern to compute 3D derivatives. Use with Prepare3DDeriv.

 |
| 

**GradFrom3DDeriv**

 | 

Computes 3D gradient vector from result of Prepare3DDeriv/Compute3DDeriv.

 |
| 

**CurlFrom3DDeriv**

 | 

Computes curl of a 3D vector field from result of Prepare3DDeriv/Compute3DDeriv.

 |

These helper Material Functions use four evaluations of the base expression spaced in a tetrahedral pattern to approximate these derivative-based operations.

Below you will find descriptions of the various noise functions you will find in the Vector Noise Material Expression.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Function**

 | 

-   **Cellnoise**: Random color for each integer grid cell in 3D space. About 10 instructions.
    
-   **Perlin 3D Noise**: Computational Perlin noise with 3D output, each channel output ranges from -1 to 1. About 83 instructions if only the red channel is used, 125 instructions if all three channels are used.
    
-   **Perlin Gradient**: Computes the gradient of a Perlin noise function. RGB output contains the gradient vector, A is the scalar noise. About 106 instructions.
    
-   **Perlin Curl**: Computes a 3D curl noise. The output is the mathematical curl of Perlin 3D Noise. About 162 instructions.
    
-   **Voronoi**: The same algorithm and instruction counts as the Voronoi function in the *Noise* expression, but RGB is the location of the closest seed point in each Voronoi cell, and A is the distance to that seed point.
    

 |
| 

**Quality**

 | 

A look/performance setting. Lower values are faster but may look worse, higher values are slower but may look better.

 |
| 

**Tiling**

 | 

For noise functions that support it this allows noise to tile. This is more expensive, but useful when baking noise into a seamless wrapping texture.

 |
| 

**Tile Size**

 | 

When tiling, how often should the noise repeat. For Perlin noise variants, the Tile Size must be a multiple of three.

 |
| Inputs |  |
| --- | --- |
| 

**Position**

 | 

Allows the texture size to be adjusted via a 3D vector.

 |

-   **Cell Noise** Material Example:
    
    [![Cell Noise](https://dev.epicgames.com/community/api/documentation/image/1d03940e-2b89-42a3-85b6-7b96de633cb7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1d03940e-2b89-42a3-85b6-7b96de633cb7?resizing_type=fit)
    
    Click image for full size.
    
-   **Perlin Gradient** Material Example:
    
    [![Perlin Gradient](https://dev.epicgames.com/community/api/documentation/image/6018011f-b419-49db-8e37-dae36dea81a8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6018011f-b419-49db-8e37-dae36dea81a8?resizing_type=fit)
    
    Click image for full size.
    
-   **Voronoi** Material Example:
    
    [![Voronoi Noise](https://dev.epicgames.com/community/api/documentation/image/8c46f32b-2269-4b25-ac78-1de7e8e81b6c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8c46f32b-2269-4b25-ac78-1de7e8e81b6c?resizing_type=fit)
    
    Click image for full size.