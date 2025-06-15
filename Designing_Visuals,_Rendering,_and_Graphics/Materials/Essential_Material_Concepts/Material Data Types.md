# Material Data Types

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-data-types-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-data-types-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:11

---

Understanding how data is represented and manipulated in the [Material Editor](/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide) is one of the principle concepts in Unreal Engine Material creation. The inputs on the [Main Material Node](/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine), which define the physical attributes of a Material, are each programmed to accept a specific type of data. Similarly, many of the Material Expression nodes used to build Materials will fail to compile unless they receive a specific kind of data on their inputs.

This page provides an overview of the four data types available in the Material Editor and examples of how they are frequently used.

## Float Data Types

In computer graphics, a **float** is a data type that stores a single numeric value, positive or negative. Float is short for floating-point, which means the number contains a decimal place and does not need to be a whole number (or integer). Examples of float values might include 1.0, -0.5, or 2.0.

Ultimately all the data types in the Material Editor are variations of the float variable. Where they differ is in the quantity of values they store. Whereas a float represents a single number, a float2 stores two discrete floating-point values. For example: (1.0, 0.5).

The following table breaks down the four data types available in the Material Editor.

| Data Type | Material Expression(s) | Data Structure | Common Uses |
| --- | --- | --- | --- |
| Float | Constant, Scalar Parameter | (r) | Metallic, Roughness, arithmetic operations |
| Float2 | Constant2Vector | (r, g) | UV or XY coordinates, Scale |
| Float3 | Constant3Vector | (r, g, b) | Color (r, g, b) or 3D coordinates (x, y, z) |
| Float4 | Constant4Vector, Vector Parameter, Textures | (r, g, b, a) | Color with alpha channel, Textures (r, g, b, a) |

### Float

As described above, a **float** stores a single floating-point value. It can be positive or negative and contains a decimal place. There are two Material Expressions you can use to define a float.

#### Constant Material Expression

A **Constant Material Expression** node stores a single constant float value. Because it is a constant, this value does not change after the Material is compiled. The image below shows a Constant node which holds a value of **1.0**.

![Constant Material Expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5134eaf6-0a17-4323-b6a3-a2bae6c34802/constant-expression.png)

#### Scalar Parameter

A **Scalar Parameter** also stores a float. Unlike a Constant, the Scalar Parameter also becomes a named variable that you can modify in a Material Instance after the Material is compiled, or even at runtime. The image below shows a Scalar Parameter with a name of Roughness, and a default value of **0.6**. You could use this to define the Material's roughness attribute, while providing artists a way to override the value in a Material instance.

![Scalar Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ff2264d-528f-4b1e-9ecd-231012ce9a86/scalar-parameter.png)

For more information about when and how to use Scalar Parameters instead of Constants, read the [Instanced Materials](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) documentation.

#### Examples

Certain inputs on the [Main Material Node](/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine) are defined by a float. For example, the **Metallic**, **Specular**, and **Roughness** [inputs](/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine) all accept a float value between 0 and 1. Therefore, you can pass a Constant Material Expression or Scalar Parameter directly into the Main Material Node to define these attributes.

![Scalar and Constant Material Expressions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3797e8de-f293-418c-8b29-bfed99382fd4/scalar-and-constant-example.png)

Constants and Scalar Parameters are often used to control the magnitude of some effect. Below, a Scalar Parameter named Emissive Power is multiplied by a solid color and passed into the **Emissive Color** input. Changing the value in the **Emissive Power** parameter makes the emissive output brighter or dimmer.

![Scalar parameter as Emissive Power](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42f2c045-bb33-45d6-bd05-acb448a6a62f/scalar-multiplier.png)

### Float2

A **Float2** stores two numeric values. For example: (2.0, 3.0).

In the Material Editor, the **Constant2Vector** Material Expression is used to define a float2. Below, a Constant2Vector is shown with values of **2.0** and **3.0** in each of its two channels.

![Constant2Vector node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed163c7a-63c1-4c69-908c-a814342855ab/constant-2-vector.png)

#### Constant2Vector

The **Constant2Vector** is useful anytime you need to define or modify an attribute that requires two-channel data. In the details panel, the two values are labeled **R** and **G**, referring to the red and green channels in rgb color, but that is only one possible use. Coordinates (UV, XY) and scale (width, height) are other attributes you could define with a Constant2Vector.

In the example below, a Constant2Vector is added to a **Texture Coordinates** node to modify the position of the texture on a plane. In the first slide, the values in the Constant2Vector are (0, 0), so the texture position is unchanged.

  ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1145371-3f34-4031-a0e9-df6fbdc1912f/texture-coords-01.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0103bfed-5ef0-40ea-a144-61c45543d03e/texture-coords-02.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2242c951-e493-45b9-8a22-433479d8c5ab/texture-coords-03.png)

**The values in the Constant2Vector control the texture position.**

When the R value is changed to 0.5, the texture shifts along the horizontal axis, because it is being added to the U coordinate of the texture. This causes the texture to wrap around the left and right edges of the plane. When the G value is changed to 0.5, the texture shifts vertically. The center of the texture is now at the four corners of the plane.

### Float3

A **float3** stores three numeric values. In the Material Editor, the **Constant3Vector** node defines a float3.

![Constant3Vector node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adaa2dfc-1fe3-4a95-a174-f8c1a6f2c17d/constant-3-vector-expression.png)

#### Constant3Vector

In Unreal Engine, the color of a pixel is defined by three values representing the red, green, and blue color channels. Therefore, one common use for a float3 is to define a solid color.

If you double-click a **Constant3Vector** node, a color picker dialog appears, letting you select a color with the wheel or eyedropper tool. The color picker also provides fields to enter **RGB**, **HSV**, or **Hex** values if you need to create a specific color. You can also launch the color picker by clicking the color swatch in the details panel.

![Material Editor color picker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7364eff0-8cfb-4b08-8b60-3f8dd243b509/color-picker.png)

A second use case for a float3 is to define (x, y, z) coordinates. For example, the **World Position Offset** input accepts three values, which define how many units the Material is offset on the x, y, and z axes in world space.

In the four slides below, the values in a Constant3Vector are each changed to 800. You can see how the position of the sphere changes, first on the x-axis, then the y-axis, then on the z-axis in the third slide.

   ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/334f6a76-2781-4f9c-bfe9-888d32a3c80c/world-position-offset-01.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79848530-d052-4c0c-802b-f41d229914be/world-position-offset-02.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/faf7d9c8-9072-441c-b884-efdeb144c569/world-position-offset-03.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78224e91-f687-4c3b-9c1c-c7c7110ba46e/world-position-offset-04.png)

**World Position Offset takes three values, to offset the Material along the x, y, and z axes.**

#### Parameterizing a Constant3Vector

You can parameterize a Constant3Vector by right-clicking it and choosing **Convert to Parameter** from the context menu. This converts the node into a Vector Parameter. The **Vector Parameter** node actually stores four values (r, g, b, a), making it a float4.

However, any input that requires a float3 will simply use the first three values and discard the fourth. For example, the **Base Color** input accepts a float3. If you connect a Vector Parameter to Base Color, it will use the R, G, and B channels and discard the fourth value (the alpha channel). Because Unreal Engine knows which channel to discard, you can safely use a Vector Parameter when you need to parameterize a float3, even though the node is technically a float4.

### Float4

A **float4** stores four floating-point values. For example: (50.0, 0.0, 100.0, 0.5). There are two Material Expressions commonly used to define a float4.

#### Constant4Vector

The Constant4Vector stores four constant values. The Constant4Vector is most often used to represent RGBA color, that is color with an alpha channel. Like the Constant3Vector, you can double-click the node or click the swatch in the details panel to access a color picker.

![Constant4Vector](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eabc135f-9cbf-44f1-964b-2d4a5a4539a6/constant-4-vector.png)

#### Vector Parameter

A **Vector Parameter** is a parameterized float4. You can create a Vector Parameter directly from the palette, or can. The most common use for a **Vector Parameter** is to create color parameters in a Material that artists can easily override in Material Instances. For example, multiplying a Vector Parameter on top of a texture is one way to add a tint control to some aspect of a Material (Base Color and Emissive, for example).

![Vector Parameter expression](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c584c2d-6dce-49ca-8898-f90885011fe3/vector-parameter.png)

In addition to its utility in a parameterized Material workflow, Vector Parameter has an additional advantage. Unlike any prior examples on this page, each individual data channel within a Vector Parameter is accessible through the five output pins on the right side of the node. As labeled above, these are:

1.  **RGBA** - Outputs all the values in the float4. In the example above: (0.0, 1.0, 0.5, 0.0).
2.  **R** — Outputs the value in the **R** channel only.
3.  **G** — Outputs the value in the **G** channel only.
4.  **B** — Outputs the value in the **B** channel only.
5.  **A** — Outputs the value in the **A** channel only.

This emphasizes an important aspect of Material creation. Ultimately the information that flows through a Material graph is just floating-point values packaged and represented in different ways. Even though the channels of a Vector Parameter are labeled RGBA in the Details panel, it does not mean they need to be used that way in your Material.

Beyond representing color, you could use a Vector Parameter to parameterize four discrete but related values. One such use of the node is in the Megascans parent Material, where a Vector Parameter is used to parameterize the UV tiling and offset of the Material.

![Vector Parameter in Megascans Material](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99c52b10-aa79-4600-ab44-b90f961dbf51/megascans-vector-parameter.png)

Notice that the RGBA channels were renamed in this example to Tiling X, Tiling Y, Offset X, and Offset Y. You can rename the channels of a Vector Parameter in the Details panel under **Parameter Customization > Channel Names**. These names are visible in the Material Instance Editor when an artist overrides parameter values.

Read more about the [Vector Parameter](/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine#vectorparameter) node here, and learn more about [Material parameterization](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) on these pages.

## Further Reading

The four data types introduced on this page form the basis of all information that travels through a Material Graph. It is important to understand that data types are not necessarily immutable. For example, you can combine two floats to form a float2. Similarly, you can extract or isolate a single float from a larger data type.

Continue reading about manipulating data types and rules for performing arithmetic in a Material graph here: [Material Data Manipulation and Arithmetic](/documentation/en-us/unreal-engine/material-data-manipulation-and-arithmetic-in-unreal-engine).