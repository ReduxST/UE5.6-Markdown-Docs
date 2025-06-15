# Material Inputs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:15

---

This page documents all the available inputs on the Main Material Node. By feeding data (by way of constants, parameters, and textures) into these inputs, you can define the surface properties of your Material and create an almost infinite variety of physical surfaces.

Not all inputs are required for every Material, and some Material types require inputs that are not visible on the Main Material Node by default.

## Inputs and Material Properties

When you change certain Material properties in the Details panel, you will notice that some inputs on the Main Material Node turn white (indicating that they are enabled), while others are grayed out.

Three material properties control which inputs are enabled in the Material:

-   **Blend Mode** - This controls how your Material blends with the pixels behind it.
-   **Shading Model** - This defines how light is calculated for the surface of the Material.
-   **Material Domain** - This dictates how the Material is intended to be used. For instance, whether it is meant to be part of a surface, a Light Function, or a Post Process Material.

If an input you need for your Material is disabled, it is because one or more of the above properties is set incorrectly. For example, if you are trying to make a pane of glass, but the opacity input is disabled. The solution in that example is to change the **Blend Mode** to **Translucent**.

## Base Color

Base Color defines the overall color of the Material. In principle, Base Color should represent the diffuse light reflected off a surface, minus any specular reflections/highlights.

If taken from the real world, base color textures should be photographed using a polarizing filter. Polarization removes the specular of nonmetals when aligned.

![Base Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e93bf7b7-94c0-4548-b011-17315b208d62/base-color.png)

## Metallic

The Metallic input controls how 'metal-like' your surface will be. Metallic accepts any value between 0 and 1, but in a majority of cases Metallic is considered an either/or property.

-   Nonmetals have a Metallic value of 0.
-   Metals have a Metallic value of 1.

For pure surfaces, such as pure metal, pure stone, or pure plastic this value will be 0 or 1, not anything in between. When creating hybrid surfaces like corroded, dusty, or rusty metals, you may find that you need some value between 0 and 1.

  ![Metallic Value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8eae3894-43a8-4f4c-9b05-6707f0fb8e74/metallic-slider-00.png) ![Metallic Value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61502971-7603-49a3-9b6c-29b144770705/metallic-slider-05.png) ![Metallic Value 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/598fa6c5-35b4-4d18-ad8b-e66fda094ce7/metallic-slider-10.png)

**Metallic values of 0, 0.5, and 1.**

When using metallic masks, the values in the texture should be pure black or pure white. Only use grayscale values if you specifically mean to create a blend (corroded metal, for example).

## Specular

Specularity is a measure of how much light a surface reflects. The Specular input takes a value between 0 and 1, and defines the extent to which a surface is reflective:

-   **Value of 0** - Fully non-reflective
-   **Value of 1** - Fully reflective
-   The default value is 0.5, which represents approximately 4% reflectivity.

  ![Specular value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5e91e51-6b1b-4a19-92a3-9a9b17f23922/spec-slider-00.png) ![Specular value 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28410273-6094-4c8b-91fd-88995237a401/spec-slider-05.png) ![Specular value 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff0dbe2d-9816-47ac-89bf-943a918bca4a/spec-slider-10.png)

**Specular values of 0, 0.5, and 1**

## Roughness

The Roughness input controls how rough or smooth a Material's surface is. Rough Materials scatter reflected light in more directions than smooth Materials. This value controls how blurry or sharp a reflection is (or how broad or tight a specular highlight is).

-   A Roughness of 0 (smooth) results in a mirror-like reflection.
-   A Roughness of 1 (rough) results in a diffuse or matte surface.

  ![Roughness Value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c38614c0-e729-4e27-89ac-8ae5cfec484d/roughness-slider-00.png) ![Roughness Value 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/507b367d-49bd-49fb-a0e0-25c62d4f97fa/roughness-slider-10.png) ![Roughness Value 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6623ee94-76ed-4898-a4c0-afb1f9b12cf3/roughness-slider-20.png)

**Roughness values of 0, 0.5, and 1.**

Most surfaces are not uniformly rough or smooth. Roughness is a property that is frequently mapped on your objects in order to add physical variation to the surface.

Scratches on metal, scuffs on a wood floor, or fingerprints on plastic are examples of materials that would require a roughness map.

![Roughness map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4982eb29-f942-4732-95df-ee41186bec3e/roughness-map.png)

## Anisotropy and Tangent

The **Anisotropy** and **Tangent** inputs enable you to control how anisotropic the roughness of the Material is and its light directionality. These two inputs are used to recreate the anisotropic effect of something like brushed metal.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05757c21-c109-45ff-9672-651b28d6c75d/anisotropicmaterialgraph.png)

Without using the Anisotropic and Tangent inputs, materials have an isotropic response. This is also true when the anisotropic input has a value of 0.

![Isotropic Material Response](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73b7e137-5b81-46a8-9427-a097d88d7495/isotropicresponse.png)

![Anisotropic Material Response](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66dcdc51-484d-4d45-8806-64d3b4d9e888/anisotropicresponse.png)

The anisotropic response is controllable using a value between -1.0 and 1.0, where a value of 0 has no anisotropic effect.

Anisotropic materials are enabled by default but can be disabled using the console command `r.AnisotropicMaterials.` When enabled, anisotropy works with supported Gen5 platforms, and when scalabiltiy settings are High, Epic, or Cinematic.

          ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc26c6c3-b17c-46f0-aafb-5482a8cffe28/ani0.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f4781d8-00f6-4d49-95a0-05c55cb5044a/ani1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8359a7f-a68c-40a1-acbc-e21ab0483085/ani2.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/516fb53c-d3dd-4319-9c23-b775c2cf3085/ani3.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d36db377-e607-4080-b48d-0f6b168cf637/ani4.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a440b92-3a4e-4ffa-87b0-96604d8168a1/ani5.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a206ec7d-74c3-4a6a-a5e7-1b49663a4e16/ani6.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcd3ed6d-50d4-443a-baa6-59f0753c7aee/ani7.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73549c05-60ae-4973-b7dd-2eb8ac1f145c/ani8.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3d25021-3f02-41d9-81b2-6510dcbdd09e/ani9.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd69517a-bb4e-4ee6-8146-26a69ab1367c/ani10.png)

**Dragging the slider shows the anisotropic response positively increasing from 0.0 to 1.0.**

Use the **Tangent** input to define light directionality with a texture or Vector expression.

## Emissive Color

The **Emissive Color** input controls which parts of your Material will glow or emit light, and the brightness of the emission. Ideally this input will receive a masked texture (mostly black except the areas that need to glow).

Values greater than 1 are allowed as HDR lighting is supported.

![Emissive map](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f2f234f-cf9b-495f-aa58-285f932c8c2a/emissive-map.png)

## Opacity

The Opacity input is enabled when the [Translucent Blend Mode](/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine#translucent) is selected, typically for Translucent, Additive, and Modulated Materials.

-   0.0 represents a completely transparent Material.
-   1.0 represents a fully opaque Material.
-   Fractional values between 0 and 1 produce semi-transparent or translucent Materials.

Opaque and masked blend modes also use Opacity when using one of the subsurface shading models.

![Translucency Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ff1680f-c93e-4687-9403-b2bc0e25708c/opacity.png)

Opacity is mostly used for **Translucent**, **Additive**, and **Modulated** Materials.

## Opacity Mask

**Opacity Mask** is similar to Opacity, but is only available when using the Masked Blend Mode.

Unlike the opacity input, the opacity mask does not allow for partial or intermediate transparency levels. When using an opacity mask, regions of the Material are either fully visible, or fully invisible. This makes it a good solution when you need Materials that define complex solid surfaces such as wire mesh, chain link faces, and so on.

![Opacity masked Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0862e551-335b-4e72-a5bb-74dfd2d981b1/opacity-mask.png)

The **Opacity Mask Clip Value** property allows you to set the value at which clipping takes place. For example, if the Opacity Mask Clip Value is set to 0.5:

-   Pixels with a value greater than 0.5 on the Opacity Mask become fully opaque.
-   Pixels with a value lower than 0.5 on the Opacity Mask become fully transparent.

See the [Masked Blend Mode documentation](/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine#masked) for more details.

## Normal

The **Normal** input takes in a normal map, which is used to add significant physical detail to the surface by modifying the "normal," or facing direction, of each individual pixel.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8688369-1a70-4134-9aeb-8e022fc23b71/axes.png)

**In the image above**, both weapons are using the same Static Mesh. The lower one employs a highly detailed normal map, which provides additional detail. This gives the illusion that the surface contains many more polygons than are actually being rendered.

Typically, normal maps are often created from high-resolution modeling packages.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1525ad3f-ed1f-492b-91a3-ffe7aca91393/normalnetwork.png)

## World Position Offset

The World Position Offset input allows a Material to manipulate the vertices of a mesh in world space. This is useful for making objects move, change shape, rotate, and a variety of other effects. World Position Offset is often used for subtle, ambient animation.

The above network causes the sphere to grow and shrink along its vertex normals with a sinusoidal period of one second.

When using World Position Offset to expand your object beyond its original bounds, keep in mind that the renderer still uses those original bounds. This means that you may see culling and shadowing errors. You may go into the properties of a mesh and set its **Scale Bounds** property to compensate, though this has a draw on performance and may lead to shadowing errors.

## Subsurface Color

The **Subsurface Color** input is only enabled when the [Shading Model](/documentation/en-us/unreal-engine/subsurface-shading-model-in-unreal-engine) property is set to Subsurface. This input allows you to add a color to your Material to simulate shifts in color when light passes through the surface.

For example, human skin shaders often use a red Subsurface Color to simulate blood beneath the surface. Subsurface skin effects are most noticeable in extremities like the tip of the nose, fingers or earlobes when backlit by a strong light source.

## Custom Data

The Custom Data Material inputs are disabled by default, and are only enabled when certain Shading Models are in use. The Custom Data slots are populated with context-specific inputs that support the unique needs of some Shading Models.

For example, if you select the **Eye** shading model, the Custom Data inputs become **Iris Mask** and **Iris Distance**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0858dad-1802-47ab-90e8-82caf5cf2cfe/eye-shading-model.png)

Shading Models that use the Custom Data inputs include:

-   Clear Coat
-   Subsurface Profile
-   Hair
-   Cloth
-   Eye

## Hair

The **Hair** Shading Model is used to better simulate the translucent nature of hair. This shading model approximates the way light passes through hair, accounting for the fact that strands of hair are not perfectly cylindrical.

Additionally, instead of rendering a unified specular highlight, the specular reflections are independently placed based on the direction that the hair is pointing.

![Hair Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab20a810-3a0b-4bf4-b72b-06914d5a0188/hair_character.png)

When the hair shading model is selected, three inputs are enabled on the Main Material Node:

-   **Scatter:** This input controls the amount of light scatter that is allowed to happen through the hair.
-   **Tangent:** This input replaces the **Normal** input and is used to control the normal direction along the U and V texture coordinates.
-   **Backlit:** This input controls the amount of backlighting that affects this hair material.

For an example of hair set up using this Shading Model, see the [Digital Humans](https://docs.unrealengine.com/4.27/en-US/samples-and-tutorials/) documentation and sample project available on the Epic Games Launcher in the **Learn** tab.

## Cloth

The **Cloth** Shading Model can be used to better simulate cloth-like materials that have a thin layer of fuzz over the surface of the Material.

![Cloth example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/904e467b-e13b-4028-8b2d-b99bc896ac2c/cloth-new.png)

The Cloth Shading Model opens up two inputs on the Main Material node:

-   **Fuzz Color:** This input enables you to add color to your Material to simulate shifts in color when light passes through the surface.
-   **Cloth:** This input enables you to control the strength of the **Fuzz Color** as a mask. A value of 0 indicates no fuzz color contribution to the Base Color, whereas a value of 1 blends fully over the Base Color.

## Eye

This is an advanced shading model that is highly technical and has very strong dependencies between shader code, the Material, the shape of the geometry and its UV layout. Epic recommends using our [Digital Humans](https://docs.unrealengine.com/4.27/en-US/samples-and-tutorials/) sample project as a starting point when developing your own eye assets or migrating them directly from this project.

The **Eye** Shading Model is designed to simulate that of an eye's surface.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a26b690e-a142-432c-abb7-3a2e1622583b/eyematerialgraph.png)

The Eye Material Instance below has been set up to expose artistic cotnrol over the different biological parts of the eye shader that can be found in the [Digital Humans](https://docs.unrealengine.com/4.27/en-US/samples-and-tutorials/) sample project.

Click image for full size.

The Eye Shading Model adds two additional inputs to the Main Material node:

-   **Iris Mask:** This helps control the index of refraction and depth of the iris.
    
    In the Material **M\_EyeRefractive** in the Digital Humans sample project, see the **IOR** and **Depth Scale** parameters.
    
-   **Iris Distance:** This controls the concavity of the refracted iris.
    
    In the Material **M\_EyeRefractive** in the Digital Humans sample project, see the **Iris Concavity Scale** and **Iris Concavity Power** parameters.
    

## Clear Coat

The **Clear Coat** Shading Model is used to better simulate multilayer materials that have a thin translucent layer of film over the surface of the Material. You can use Clear Coat with either metal or non-metal surfaces.

Examples of clear coat Materials include lacquer clear coats (used on furniture, for example), or colored films over uncolored metal, such as with car paint or soda cans.

![Clear coat example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d34f3ecb-2966-4c8e-a903-e42f1e9b5dd5/clear-coat.png)

The Clear Coat Shading Model enables two new Material inputs on the Main Material Node:

-   **Clear Coat**: Amount of clear coat layer, 0 acts like the standard shading model, 1 is the full clear coat model. This is useful for masking.
-   **Clear Coat Roughness**: Roughness for the clear coat layer. Our approximation is accurate for small values. Very rough clear coat layers are supported but will not be very accurate compared to their real world counterparts.

## Ambient Occlusion

The **Ambient Occlusion** input is used to help simulate the self-shadowing that happens within the crevices of a surface. Generally this input will be connected to an ambient occlusion texture map of some kind, which is often created within 3D modeling packages such as Maya, 3ds Max, or Zbrush.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/477c6d9c-8cbc-4612-a41d-2dd599815a77/normalnetwork.png)

Note that this input relies on light sources using **Static** or **Stationary** mobility to generate built lighting. This material input is silently ignored when its Material is used in conjunction with any **Movable** light sources.

## Refraction

The Refraction input takes in a texture or value that simulated the index of refraction of the surface. This is useful for things like glass and water, which refract light passing through them.

In the graph pictured above a Fresnel Material function is used to blend between two different IOR values.

![Refraction network](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58194be5-ee75-4298-bf43-13cd519b12fb/refraction.png)

| Common Indices of Refraction |   |
| --- | --- |
| **Air** | 1.00 |
| **Water** | 1.33 |
| **Ice** | 1.31 |
| **Glass** | 1.52 |
| **Diamond** | 2.42 |

## Pixel Depth Offset

The **Pixel Depth Offset** input is used to control pixel depth in the shader graph using logic you set up. This enables you to create your own logic to blend or fade objects based on their scene depth.

![Pixel depth offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75fae20a-621b-4f17-a6cc-b2c45805f3ee/pixel-depth-offset.png)

In this comparison, using Pixel Depth Offset with the DitherTemporalAA Material Function enables you to set an "offset" value that blends the ground with the object intersecting it using a stipple pattern texture.

![Without Pixel Depth Offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d94402c-9cdc-4b40-af5d-e464c343afea/pdo_0.png)

![With Pixel Depth Offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52e123a0-ae06-4773-b1d2-2c0a37a9c281/pdo_1.png)

## Shading Model

This input requires you to select the **From Material Expression** Shading Model in the Material **Details** panel.

The **Shading Models** input enables you to use logic in your Material Graph to select from a list of available Shading Models to use for part of your Material. This input is useful when you have a single object that needs to use multiple shading models, like Clear Coat and Default Lit. This can reduce the number of Materials required, in turn, saving performance and draw calls. All of this can be driven by logic in your Material using the Shading Model expression node and some texture masks.

The following is a simple example using an **If** expression to choose between Shading Models.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/403e3ddc-f077-4041-8cf8-9c06aa529354/perpixel_if_graph.png)

Using this example, when A is greater than B, the resulting shading model is **Default Lit**. When A is less or equal to B, a texture mask is used to display **Default Lit** and **Clear Coat** shading models on parts of the mesh.

![A > B: Uses Default Lit | B = 0.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b12f6142-f8c1-41a8-8c3a-3de149b61e97/perpixel_if_a.png)

![A <= B: Uses Clear Coat | B = 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b8ea0e7-3fec-4622-b879-ac4e72e50ab6/perpixel_if_b.png)

For more information and examples of this inputs usage, see the [From Material Expression](/documentation/en-us/unreal-engine/from-material-expression-shading-model-in-unreal-engine) page.