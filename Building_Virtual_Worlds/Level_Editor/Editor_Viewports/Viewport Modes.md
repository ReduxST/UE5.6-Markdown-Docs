# Viewport Modes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:01

---

![Viewmode Header](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b123ed17-8ad8-48f3-8ad7-658c31b612ea/01-view-mode-header.png "Viewmode Header")

The Unreal Editor viewports have a large number of visualization modes to help you see the type of data being processed in your scene, as well as to diagnose any errors or unexpected results. The more common view modes have their own hotkeys, but all can be accessed from the viewport within the **View Mode** menu.

Click image for full size.

Click image for full size.

## Lit

Click image for full size.

-   View Mode Hotkey: **Alt + 4**
-   Console command: `viewmode lit`

**Lit** view mode shows the final result of your scene once all of the Materials and lighting have been applied.

## Unlit

Click image for full size.

-   View Mode Hotkey: **Alt + 3**
-   Console command: `viewmode unlit`

**Unlit** view mode removes all lighting from the scene, showing you Base Color only.

## Wireframe

Click image for full size.

-   View Mode Hotkey: **Alt + 2**
-   Console command: `viewmode wireframe`

**Wireframe** shows all of the polygon edges in the scene. In the case of Brushes, you will see the resultant geometry.

## Detail Lighting

Click image for full size.

-   View Mode Hotkey: **Alt + 5**
-   Console command: `viewmode lit_detaillighting`

**Detail Lighting** activates a neutral Material across the entire scene, using the normal maps of the original materials. This is useful for isolating whether your BaseColor is obscuring lighting by being too dark or noisy.

## Lighting Only

Click image for full size.

-   View Mode Hotkey: **Alt + 6**
-   Console command: `viewmode lightingonly`

**Lighting Only** shows a neutral Material that is only affected by lighting. It differs from *Detail Lighting* mode in that you will not see normal maps.

## Light Complexity

Click image for full size.

Click image for full size.

-   View Mode Hotkey: **Alt + 7**
-   Console command: `viewmode lightcomplexity`

Light Complexity shows the number of non-static lights affecting your geometry. This is useful for tracking lighting cost - the more lights affecting a surface, the more expensive it will be to shade.

| Light Complexity Coloration |   |   |   |   |   |   |
| --- | --- | --- | --- | --- | --- | --- |
| **Color** | ![LightComplexity_0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9aa6fc4-1064-49fd-a9d0-dcc92c54457a/lightcomplexity_0.gif "LightComplexity_0") | ![LightComplexity_1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aea88a56-f2fe-48f0-8ff4-001d3fb8c588/lightcomplexity_1.gif "LightComplexity_1") | ![LightComplexity_2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ee2885c-14b3-4f0c-9fce-03a2d8a5c8f0/lightcomplexity_2.gif "LightComplexity_2") | ![LightComplexity_3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/536956f1-1f5a-4c25-b481-f19c26c8d76b/lightcomplexity_3.gif "LightComplexity_3") | ![LightComplexity_4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b919d3a7-c414-4de8-84b7-33c0812c0f89/lightcomplexity_4.gif "LightComplexity_4") | ![LightComplexity_5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c677d05-6c64-4b46-8f63-cbcde7072f9b/lightcomplexity_5.gif "LightComplexity_5") |
| **Number of Lights Affecting Surface** | **0** | **1** | **2** | **3** | **4** | **5+** |

This color scheme is defined in the shader code.

## Shader Complexity

Click image for full size.

-   View Mode Hotkey: **Alt + 8**
-   Console command: `viewmode shadercomplexity`

**Shader Complexity** Mode is used to visualize the number of shader instructions being used to calculate each pixel of your scene. It is generally a good indication of how performance-friendly your scene will be. In general, it is used to test overall performance for your base scene, as well as to optimize particle effects, which tend to cause performance spikes with a large amount of overdraw for a short period of time.

Only instruction count is used to calculate shader complexity, which may not always be accurate. For example, a shader with 16 instructions, all texture lookups, will be much slower on all platforms than a shader with 16 math instructions. Also shaders which contain loops that are not unrolled will not be represented accurately by the instruction count, this is mainly an issue for vertex shaders. Overall the instruction count is a good metric in the vast majority of cases.

The view mode uses a color spectrum to indicate how expensive the scene is. Green through red represent a linear relationship of "very inexpensive" to "expensive", while pink and white indicate a large jump to "very expensive" pixels. Small areas of white can be tolerated, but if the majority of your screen is covered in bright red or white, the performance will be poor.

|   |   |   |   |   |   |   |   |   |   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Shader Complexity Coloration |   |   |   |   |   |   |   |   |   |
| \[REGION:shadercomplexity sc\_1\]\[/REGION\] | \[REGION:shadercomplexity sc\_2\]\[/REGION\] | \[REGION:shadercomplexity sc\_3\]\[/REGION\] | \[REGION:shadercomplexity sc\_4\]\[/REGION\] | \[REGION:shadercomplexity sc\_5\]\[/REGION\] | \[REGION:shadercomplexity sc\_6\]\[/REGION\] | \[REGION:shadercomplexity sc\_7\]\[/REGION\] | \[REGION:shadercomplexity sc\_8\]\[/REGION\] | \[REGION:shadercomplexity sc\_9\]\[/REGION\] |   |
| **Ideal** |   |   | **Moderate** |   |   | **Expensive** | **Very Expensive** |   |   |

**+ShaderComplexityColors** is defined in the `BaseEngine.ini` file and is linearly interpolated (lerped) based on the total number of instructions for a given pixel.

```
`+ShaderComplexityColors=(R=0.0,G=1.0,B=0.127,A=1.0)   +ShaderComplexityColors=(R=0.0,G=1.0,B=0.0,A=1.0)   +ShaderComplexityColors=(R=0.046,G=0.52,B=0.0,A=1.0)   +ShaderComplexityColors=(R=0.215,G=0.215,B=0.0,A=1.0)   +ShaderComplexityColors=(R=0.52,G=0.046,B=0.0,A=1.0)   +ShaderComplexityColors=(R=0.7,G=0.0,B=0.0,A=1.0)   +ShaderComplexityColors=(R=1.0,G=0.0,B=0.0,A=1.0)   +ShaderComplexityColors=(R=1.0,G=0.0,B=0.5,A=1.0)   +ShaderComplexityColors=(R=1.0,G=0.9,B=0.9,A=1.0)`  
Copy full snippet
```
+ShaderComplexityColors=(R=0.0,G=1.0,B=0.127,A=1.0) +ShaderComplexityColors=(R=0.0,G=1.0,B=0.0,A=1.0) +ShaderComplexityColors=(R=0.046,G=0.52,B=0.0,A=1.0) +ShaderComplexityColors=(R=0.215,G=0.215,B=0.0,A=1.0) +ShaderComplexityColors=(R=0.52,G=0.046,B=0.0,A=1.0) +ShaderComplexityColors=(R=0.7,G=0.0,B=0.0,A=1.0) +ShaderComplexityColors=(R=1.0,G=0.0,B=0.0,A=1.0) +ShaderComplexityColors=(R=1.0,G=0.0,B=0.5,A=1.0) +ShaderComplexityColors=(R=1.0,G=0.9,B=0.9,A=1.0)

**MaxPixelShaderAdditiveComplexityCount** is set to a default range of 2000, however, this value can be changed in the `BaseEngine.ini` file to help with the optimization of materials in your project.

```
`MaxPixelShaderAdditiveComplexityCount=2000`
Copy full snippet
```
MaxPixelShaderAdditiveComplexityCount=2000

**MaxES3PixelShaderAdditiveComplexityCount** defines the range in the ES3 Preview Mode and is set to a default range of 800.

```
`MaxES3PixelShaderAdditiveComplexityCount=800`
Copy full snippet
```
MaxES3PixelShaderAdditiveComplexityCount=800

These Colors can be modified in the `BaseEngine.ini` file. The max pixel shader additive complexity count variables can also be overridden in your project's `DefaultEngine.ini` file.

## Stationary Light Overlap

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

## Lightmap Density

Click image for full size.

View Mode Hotkey: **Alt + 0**

**Lightmap Density** mode displays the lightmap density of objects that are texture mapped, color coding them by their relation to an ideal/max density setting and displaying a grid that maps to the actual lightmap texels. It is important to have even texel density across your scene to get consistent lightmap lighting.

|   |   |   |
| --- | --- | --- |
| ![Lightmap Density Light](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7ce4535-5ae4-4336-a691-0ff70c7515e6/lightmapdensitylight.gif "Lightmap Density Light") | ![Lightmap Density Medium](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb40f911-3029-44d4-b285-9083e9efc12a/lightmapdensitymedium.gif "Lightmap Density Medium") | ![Lightmap Density Heavy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80420a3f-86a3-45a6-9f01-30166c3e00dc/lightmapdensityheavy.gif "Lightmap Density Heavy") |
| Less than ideal texel density | Ideal texel density | Max or greater than ideal texel density |

Skeletal Meshes will appear in light brown and are not considered in this calculation.

## Reflections

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Reflections** view mode overrides all materials with a flat normal and a roughness of 0, which is a mirror. This is useful for diagnosing the detail of reflections and allowing you to place more Reflection Capture Actors in areas where you need more detail.

## Player Collision

Click image for full size.

-   Console command: `viewmode CollisionPawn`

The **Player Collision** viewmode highlights assets that collide with a character or Pawn and uses the following colors:

| Player Collision Coloration |   |   |   |   |   |   |
| --- | --- | --- | --- | --- | --- | --- |
| **Color** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57cca282-8296-410c-b993-23cc787621a0/color-static.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30ad502f-629a-4164-831c-011769810a00/color-stationary.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d851e7c6-0768-4623-949b-3f6cfe9a5fc9/color-movable.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bfbc957-7f08-4062-a59f-22e8e9fa6517/color-volume.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df205fb4-201b-46ba-b972-2175742d9cb9/color-trigger.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8688986-0102-461e-b714-7b953e3339a0/color-brush.png) |
| **Description** | **Static Mesh** | **Stationary Static Mesh** | **Movable Static Mesh** | **Volume** | **Trigger Volume** | **Brush** |

## Visibility Collision

Click image for full size.

-   Console command: `viewmode CollisionVisibility`

The **Collision Visibility** viewmode highlights whitch Actors will block visibility. It uses the following colors:

| Collision Visibility Coloration |   |   |   |   |   |
| --- | --- | --- | --- | --- | --- |
| **Color** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f97ecc93-2c3d-4b8a-b3b5-6853d86d5ac4/color-static.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b3c57f0-f358-460b-8ff4-9d5ff7ad7410/color-stationary.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec01b371-52f0-4497-accf-4245c98e2a23/color-movable.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef8ef531-07fa-46aa-bf6b-f9b6461ccdf4/color-volume.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b9ea6b7-dac2-4a05-a979-37b1f3713330/color-brush.png) |
| **Description** | **Static Mesh** | **Stationary Static Mesh** | **Movable Static Mesh** | **Volume** | **Brush** |

## LOD Coloration

Click image for full size.

Click image for full size.

-   Console command: `viewmode LODColoration`

**LOD Coloration** view mode displays the current LOD index of a primitive. This is useful for diagnosing any LOD issues or to see at which distance your LODs are switching.

| LOD Primitive Coloration |   |   |   |   |   |   |   |   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Color** | ![LOD Coloration_0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c585bb94-18e2-42de-8874-be9771e6aaa5/lodcoloration_0.png "LOD Coloration_0") | ![LOD Coloration_1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3d2f3e6-95a0-4601-a89d-ac0d7221e77b/lodcoloration_1.png "LOD Coloration_1") | ![LOD Coloration_2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/379151a4-1145-465b-91cb-f5c0d3548e0c/lodcoloration_2.png "LOD Coloration_2") | ![LOD Coloration_3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0c5f678-e48c-4d48-8790-6f552950ba21/lodcoloration_3.png "LOD Coloration_3") | ![LOD Coloration_4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/131820de-2355-438e-9a21-6cd40cb3f6f4/lodcoloration_4.png "LOD Coloration_4") | ![LOD Coloration_5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d3d79ad-74d8-4318-9d84-a33e9398bd40/lodcoloration_5.png "LOD Coloration_5") | ![LOD Coloration_6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f9cbe8e-b8e6-475e-b19a-66a29594c7d2/lodcoloration_6.png "LOD Coloration_6") | ![LOD Coloration_7](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29fbbce1-ceb4-4624-9fda-5268d859ad2a/lodcoloration_7.png "LOD Coloration_7") |
| **LOD Primitive Color** | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** |

```
`+LODColorationColors=(R=1.0,G=1.0,B=1.0,A=1.0)      +LODColorationColors=(R=1.0,G=0.0,B=0.0,A=1.0)      +LODColorationColors=(R=0.0,G=1.0,B=0.0,A=1.0)      +LODColorationColors=(R=0.0,G=0.0,B=1.0,A=1.0)      +LODColorationColors=(R=1.0,G=1.0,B=0.0,A=1.0)      +LODColorationColors=(R=1.0,G=0.0,B=1.0,A=1.0)      +LODColorationColors=(R=0.0,G=1.0,B=1.0,A=1.0)      +LODColorationColors=(R=0.5,G=0.0,B=0.5,A=1.0)`     
Copy full snippet
```
+LODColorationColors=(R=1.0,G=1.0,B=1.0,A=1.0) +LODColorationColors=(R=1.0,G=0.0,B=0.0,A=1.0) +LODColorationColors=(R=0.0,G=1.0,B=0.0,A=1.0) +LODColorationColors=(R=0.0,G=0.0,B=1.0,A=1.0) +LODColorationColors=(R=1.0,G=1.0,B=0.0,A=1.0) +LODColorationColors=(R=1.0,G=0.0,B=1.0,A=1.0) +LODColorationColors=(R=0.0,G=1.0,B=1.0,A=1.0) +LODColorationColors=(R=0.5,G=0.0,B=0.5,A=1.0)

By default the engine uses only four LODs, but this can be extended in the source code.

## HLOD Coloration

Click image for full size.

-   Console command: `viewmode hlodcoloration`

**HLOD Coloration** view mode displays the Hierarchial LOD Cluster index of a primitive.

| HLOD Primitive Coloration |   |   |   |   |   |
| --- | --- | --- | --- | --- | --- |
| **Color** | ![LOD Coloration_3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a9ed48f-6a82-4ae2-ae96-d0afc4bc2e34/lodcoloration_3.png "LOD Coloration_3") | ![LOD Coloration_4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae305ae0-75cb-498b-b984-b2bd6722b551/lodcoloration_4.png "LOD Coloration_4") | ![LOD Coloration_7](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/985e8290-03dc-4a70-b42e-3d6fb6e51502/lodcoloration_7.png "LOD Coloration_7") | ![LOD Coloration_6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c2b15f1-7c97-4ca1-9005-46b8187592e4/lodcoloration_6.png "LOD Coloration_6") | ![LOD Coloration_8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7969182c-ad99-48e2-b0c1-bb4936676964/lodcoloration_8.png "LOD Coloration_8") |
| **HLOD Primitive Color** | **0** | **1** | **2** | **3** | **4** |

```
`+HLODColorationColors=(R=1.0,G=1.0,B=1.0,A=1.0)  //white (not part of HLOD)    +HLODColorationColors=(R=0.0,G=1.0,B=0.0,A=1.0)  //green (part of HLOD but being drawn outside of it)    +HLODColorationColors=(R=0.0,G=0.0,B=1.0,A=1.0)  //blue (HLOD level 0)    +HLODColorationColors=(R=1.0,G=1.0,B=0.0,A=1.0)  //yellow (HLOD level 1)    +HLODColorationColors=(R=1.0,G=0.0,B=1.0,A=1.0)  //purple    +HLODColorationColors=(R=0.0,G=1.0,B=1.0,A=1.0)  //cyan    +HLODColorationColors=(R=0.5,G=0.5,B=0.5,A=1.0)  //grey`    
Copy full snippet
```
+HLODColorationColors=(R=1.0,G=1.0,B=1.0,A=1.0) //white (not part of HLOD) +HLODColorationColors=(R=0.0,G=1.0,B=0.0,A=1.0) //green (part of HLOD but being drawn outside of it) +HLODColorationColors=(R=0.0,G=0.0,B=1.0,A=1.0) //blue (HLOD level 0) +HLODColorationColors=(R=1.0,G=1.0,B=0.0,A=1.0) //yellow (HLOD level 1) +HLODColorationColors=(R=1.0,G=0.0,B=1.0,A=1.0) //purple +HLODColorationColors=(R=0.0,G=1.0,B=1.0,A=1.0) //cyan +HLODColorationColors=(R=0.5,G=0.5,B=0.5,A=1.0) //grey

## Buffer Visualization

Click image for full size.

The Buffer Visualization area offers you access to individual buffers within the graphics card, which can help you diagnose problems how your scenes look. In order to make the most out of the buffer visualization modes, it will help to understand the basics of [Material Inputs](/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine) and [Material Properties](/documentation/en-us/unreal-engine/unreal-engine-material-properties).

### Buffer Overview

Click image for full size.

The **Buffer Overview** visualization mode allows you to see multiple images from the graphics card's GBuffer. Many of these correlate to inputs on Materials, meaning you can see how the scene looks with just a single Material input being used.

### Base Color

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

The **Base Color** mode allows you to see the only the Base Color of the Materials in your scene.

### Decal Mask

![Decal Mask](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a93dc9c0-b970-4fe3-aea0-1974573baf57/buffer_decalmask.png "Decal Mask")

-   View Mode Hotkey: **None (Menu only by default)**

The **Decal Mask** mode shows in white any surface which can receive deferred decals. Objects which cannot appear in black.

### Diffuse Color

\[![Diffuse Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/462d93d2-d5cf-4444-b071-c84c1a421449/vm_diffusecolor.png "Diffuse Color")

-   View Mode Hotkey: **None (Menu only by default)**

**Diffuse Color** shows the result of Base Color and the Material's Ambient Occlusion inputs.

### Shading Model

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

The **Shading Model** mode shows value of the Shading Model property for each Material in the scene.

| Light Complexity Coloration |   |   |   |   |
| --- | --- | --- | --- | --- |
| **Color** | ![Light Model Lit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8c763a8-89f3-475e-b80a-54e67d72fb6e/lightmodel_lit.gif "Light Model Lit") | ![Light Model Unlit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7cbdb2e-f770-41c7-86a5-90b82a6f3c9f/lightmodel_unlit.gif "Light Model Unlit") | ![Light Model Subsurface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a61457e7-097e-4911-b010-bc3bfc2eba02/lightmodel_subsurface.gif "Light Model Subsurface") | ![Light Model Preintegratedskin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b2bdfd3-841d-48f7-bfe5-988f0c65bf1d/lightmodel_preintegratedskin.gif "Light Model Preintegratedskin") |
| **Material's Shading Model** | **Default Lit** | **Unlit** | **Subsurface** | **Preintegrated Skin** |

### Material AO

![Scene in Lit Mode (Game View On)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0e3cabb-bb47-4521-b240-66e0875c76af/24-scene-in-lit-mode.png "Scene in Lit Mode")

![Scene in Buffer Material AO Mode (Game View On)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3fd16d9-a4fd-445d-bb7e-1b201f6371de/25-scene-in-buffer-material-ambient-occlusion.png "Scene in Buffer Material AO Mode")

-   View Mode Hotkey: **None (Menu only by default)**

The **Material AO** visualization mode shows the result of any texturing or Material Expression nodes that are connected to the Material's *Ambient Occlusion* input.

### Metallic

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

The **Metallic** visualization mode shows the result of any texturing or Material Expression nodes that are connected to the Material's *Metallic* input.

Note: Materials should generally have Metallic values of 0 or 1, not in between. Values between 0 and 1 will happen due to layer blending, but physical materials will always be a metal or not.

### Opacity

![Scene in Lit Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1ea9046-eab1-4e12-b158-097282311e1b/27-scene-in-lit-mode.png "Scene in Lit Mode")

![Scene in Buffer Material Opacity Mode (Game View On)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1f6d647-87fb-442a-9852-35c9adad9c5a/28-scene-in-buffer-material-opacity-mode.png "Scene in Buffer Material Opacity Mode")

-   View Mode Hotkey: **None (Menu only by default)**

**Opacity** visualization mode shows the result of any texturing or Material Expression nodes that are connected to the Material's Opacity input. In the images above, you can see the dreadlocks on the character are somewhat transparent.

The Opacity viewmode only shows opaque materials with Opacity being used, which is important in the case of subsurface scattering materials, as the Opacity controls how far light can penetrate.

### Roughness

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Roughness** visualization mode shows the result of any texturing or Material Expression nodes that are connected to the Material's Roughness input. Roughness variation is where a lot of reflection variation will come from.

### Scene Color

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Scene Color** shows the result of the scene before any post processing is done. This means before any exposure, bloom, color correction, or antialiasing. In the above image, the scene appears very dark because exposure has not brightened it up for us.

### Scene Depth

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Scene Depth** shows the depth of the scene in a constant gradient from white (farthest away) to black (closest).

### Separate Translucency RGB

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Separate Translucency RGB** shows the color information of any Materials that are Translucent and using Separate Translucency.

### Separate Translucency A

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Separate Translucency A** shows only the alpha information of any Materials that are Translucent and using Separate Translucency.

### Specular Color

![Specular Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01d0f1b1-4938-499b-9190-9cd15c244e47/buffer_speccolor.png "Specular Color")

-   View Mode Hotkey: **None (Menu only by default)**

**Specular Color** shows the color being imparted to the specular reflections of a Material. Generally, this is inferred from a combination of the Base Color and Metallic values.

### Specular

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Specular** shows the results of any texturing or Material Expression nodes that are fed into a Material's Specular input.

### Subsurface Color

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Subsurface Color** shows the results of any texturing or Material Expression nodes that are fed into a Material's Subsurface Color input.

### World Normal

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**World Normal** shows the world space normal of any opaque surfaces.

### Ambient Occlusion

Click image for full size.

-   View Mode Hotkey: **None (Menu only by default)**

**Ambient Occlusion (AO)** shows the result of any ambient occlusion calculations that are taking place on the scene. This is separate from any AO textures applied to Materials, as this is a calculation the engine makes based on surfaces and normal maps.

## Landscape Visualizers

Click image for full size.

### Normal

Click image for full size.

The **Normal** Landscape visualization mode shows a Landscape in its normal, lit state.

### LOD

Click image for full size.

The **LOD** Landscape visualization mode breaks a landscape up into color-coded panels which represent their current LOD state.

### Layer Density

Click image for full size.

The **Layer Density** Landscape visualization mode shows the landscape in a color-coded mode which shifts from green to red as more layers are added to the Landscape.

## Exposure

Click image for full size.

Exposure is a post-processing effect that controls the overall brightness of a scene. This can be set to a fixed value or left to automatic.

### Automatic vs. Fixed Exposure

When playing games with Exposure activated in your post processing, you will notice that moving from a light to a dark area or vice versa will cause the camera to temporarily adjust, similarly to how our eyes adjust when moving to different light environments. In most cases, this will be the desired result. However, if the constant shifting is distracting in your particular level, then you can set the view to a fixed exposure. This will lock the exposure in place so it no longer automatically changes as you move from light to dark or dark to light, but it also means that you can easily end up in a situation where the lights are overbright or overdark for the work you need to do.