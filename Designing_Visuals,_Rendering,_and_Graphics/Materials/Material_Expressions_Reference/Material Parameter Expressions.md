# Material Parameter Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-parameter-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:17

---

## Collection Parameters

A **Collection Parameter Expression** is used to reference a **Material Parameter Collection** asset. These are groups of parameters that you can easily reuse in many different assets such as Materials, Blueprints, and more.

They enable you to modify a global value once in the Parameter Collection, and have it propagate to multiple Materials that reference the collection. For more information, read the [Material Parameter Collections](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-material-parameter-collections-in-unreal-engine) documentation.

[![Material Parameter Collection Example](https://dev.epicgames.com/community/api/documentation/image/15f0e436-3420-4b57-affa-6653f60cc01d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/15f0e436-3420-4b57-affa-6653f60cc01d?resizing_type=fit)

Click to enlarge image.

A Material can reference, at most, two different MaterialParameterCollections. One is typically used for game-wide values while the other can be used for level specific parameters. A collection can have up to 1024 scalar parameters and 1024 vector parameters.

## DynamicParameter

The **DynamicParameter** expression provides a conduit for particle emitters to pass up to four values to the Material to be used in any manner. These values are set in **Niagara** by means of a **ParameterDynamic** module placed on an emitter.

| Property | Description |
| --- | --- |
| 
**Param Names**

 | 

An array of the names of the parameters. The values here will determine the text displayed on the outputs of the expression in the Material Editor and will be the names used to reference the parameters in the ParameterDynamic module in Niagara.

 |
| 

**Default Value**

 | 

Specifies the initial values that the parameter outputs (Vector4).

 |
| Outputs |   |
| --- | --- |
| 

**Param1**

 | 

Outputs the value of the first parameter in the Param names property. The name of this output can change based on the values in the Param Names property.

 |
| 

**Param2**

 | 

Outputs the value of the second parameter in the Param names property. The name of this output can change based on the values in the Param Names property.

 |
| 

**Param3**

 | 

Outputs the value of the third parameter in the Param names property. The name of this output can change based on the values in the Param Names property.

 |
| 

**Param4**

 | 

Outputs the value of the fourth parameter in the Param names property. The name of this output can change based on the values in the Param Names property.

 |

## FontSampleParameter

The **FontSampleParameter** expression provides a way to expose a font-based parameter in a Material Instance Constant, making it easy to use different fonts in different instances. The alpha channel of the font will contain the font outline value. Only valid font pages can be specified.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Font**

 | 

Holds the default font asset (from the **Content Browser**) to be held within the expression.

 |
| 

**Font Texture Page**

 | 

The current font texture page to be used as a part of the texture.

 |

[![Font Sample Parameter](https://dev.epicgames.com/community/api/documentation/image/8a1d3e40-934c-4314-80a2-162e02137a57?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8a1d3e40-934c-4314-80a2-162e02137a57?resizing_type=fit)

## ScalarParameter

The **ScalarParameter** expression outputs a single float value ([constant](https://dev.epicgames.com/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine)) that you can access and change in a Material Instance or on the fly by Blueprint or code.

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Default Value**

 | 

Specifies the initial value that the constant takes on.

 |

You can update the value in a Scalar Parameter, and immediately see the results without recompiling the Material.

![Scalar parameter updated from 0 to 10.](https://dev.epicgames.com/community/api/documentation/image/06f78c5a-5195-4a46-a67e-c0eed04818c5?resizing_type=fit&width=1920&height=1080)![Scalar parameter updated from 0 to 10.](https://dev.epicgames.com/community/api/documentation/image/6030426c-ec06-46cd-a550-21d47294120e?resizing_type=fit&width=1920&height=1080)

**Scalar parameter updated from 0 to 10.**

## StaticSwitchParameter

The **StaticSwitchParameter** expression takes in two inputs, and outputs the first if the value of the parameter is *true*, and the second otherwise.

This parameter is named static because it cannot change at runtime; it can only be set in the Material Instance Editor. Static Switches are applied at compile time, not at runtime. This means that whatever branch of the Material was dropped is never executed, so static switches are effectively free at runtime. On the other hand, a new version of the Material must be compiled for every **used** combination of static parameters in a Material, which can lead to a massive increase in shader permutations if abused. Try to minimize the number of static parameters in the Material and the number of permutations of those static parameters that are actually used.

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Default Value**

 | 

If *true*, the first input is output. Otherwise, the second input is output.

 |
| 

**Extended Caption Display**

 | 

If *true*, the title bar of the expressions displays the value of the expression.

 |
| Inputs |   |
| --- | --- |
| 

**A**

 | 

Takes in a value of any number of channels.

 |
| 

**B**

 | 

Takes in a value of any number of channels.

 |

**Example Usage:** You can use Static Switches to remove an entire branch of a Material with no runtime cost. Material Instances can have different values, making it possible to have a templated shader setup with no performance loss.

![Static Switch updated from True to False.](https://dev.epicgames.com/community/api/documentation/image/498e688a-d3f8-4db6-ae95-6c4236a69646?resizing_type=fit&width=1920&height=1080)![Static Switch updated from True to False.](https://dev.epicgames.com/community/api/documentation/image/8020f5b9-d4ad-4a25-a0cc-e774ecb17d98?resizing_type=fit&width=1920&height=1080)

**Static Switch updated from True to False.**

## StaticBoolParameter

The **StaticBoolParameter** works like a StaticSwitchParameter, except that it only creates a bool parameter and does not implement the switch. You can use a StaticBoolParameter to pass a default value into a boolean input on a Material Function.

[![Static Bool Parameter](https://dev.epicgames.com/community/api/documentation/image/d20f59b5-6d94-4b5a-b05a-1f9daba3e4ff?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d20f59b5-6d94-4b5a-b05a-1f9daba3e4ff?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Default Value**

 | 

The default bool value of the parameter, *True* (checked) or *False*.

 |

Static Switches are applied at compile time (not at runtime), meaning you can override the parameter in the Material Instance Editor, but it cannot change during gameplay. Whatever branch of the Material was dropped is never executed, which means static switches are effectively free at runtime. On the other hand, a new version of the Material must be compiled for every **used** combination of static parameters in a Material, which can lead to a massive increase in shader permutations if abused. Try to minimize the number of static parameters in the Material and the number of permutations of those static parameters that are actually used.

This node is used with [MaterialFunctions](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-functions-in-unreal-engine).

## StaticComponentMaskParameter

The **StaticComponentMaskParameter** expression behaves like an ordinary Component Mask, except that you can override the mask values in a Material Instance.

This parameter is named static because it cannot change at runtime; it can only be set in the Material Instance Editor. Static Switches are applied at compile time, not at runtime. This means that whatever branch of the Material was dropped will never be executed, so static switches are effectively free at runtime. On the other hand, a new version of the Material must be compiled out for every **used** combination of static parameters in a Material, which can lead to a massive increase in shader permutations if abused. Try to minimize the number of static parameters in the Material and the number of permutations of those static parameters that are actually used.

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Default R**

 | 

If checked, the red, or first, channel of the input value is passed through to the output.

 |
| 

**Default G**

 | 

If checked, the green, or second, channel of the input value is passed through to the output.

 |
| 

**Default B**

 | 

If checked, the blue, or third, channel of the input value is passed through to the output.

 |
| 

**Default A**

 | 

If checked, the alpha, or fourth, channel of the input value is passed through to the output.

 |

**Example Usage:** You can use Static Component Masks to let instances dictate which channel of a mask texture to use. If the mask is static (does not need to change at runtime) then this approach should always be used instead of multiplying a texture lookup by a Vector Parameter to mask out channels, since the latter wastes texture bandwidth and shader instructions.

![Checked channels pass through to the output, while unchecked channels are discarded.](https://dev.epicgames.com/community/api/documentation/image/6064e4cb-71c2-4d13-8d94-8fd6fa78c94a?resizing_type=fit&width=1920&height=1080)![Checked channels pass through to the output, while unchecked channels are discarded.](https://dev.epicgames.com/community/api/documentation/image/8ea7bac2-4582-41d6-a608-6a1035a09526?resizing_type=fit&width=1920&height=1080)

**Checked channels pass through to the output, while unchecked channels are discarded.**

## VectorParameter

The **VectorParameter** expression is identical to the [Constant4Vector](https://dev.epicgames.com/documentation/en-us/unreal-engine/constant-material-expressions-in-unreal-engine), except that it is a parameter you can modify in instances of the Material and through code. One nicety of the VectorParameter is that you can set its value using the Color Picker.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Default Value**

-   **R**
    
-   **G**
    
-   **B**
    
-   **A**
    

 | 

The vector to output by default unless overridden by a Material Instance Constant.

-   Specifies the float value of the red, or first, channel of the vector the expression outputs.
    
-   Specifies the float value of the green, or second, channel of the vector the expression outputs.
    
-   Specifies the float value of the blue, or third, channel of the vector the expression outputs.
    
-   Specifies the float value of the alpha, or fourth, channel of the vector the expression outputs.
    

 |

[![Vector Parameter example graph](https://dev.epicgames.com/community/api/documentation/image/c23c4548-fda7-47b3-a407-b5965c2d34f7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c23c4548-fda7-47b3-a407-b5965c2d34f7?resizing_type=fit)

VertexColor is mutually exclusive with the Transform node due to limited interpolators. If you use both a Transform node and VertexColor, then VertexColor will come out all white.

**Programmers:** For sprite particles, colors are communicated to the shader per vertex, whereas colors for mesh particles are set as shader constants.

## TextureObjectParameter

The **TextureObjectParameter** expression defines a texture parameter and outputs the texture object. This expression is frequently used to pass texture parameters into a Material Function with texture inputs. Texture inputs on a Material Function node are not compatible with Float3 data from a TextureSample 2D node, so the Texture Object (T2d) is required. This node does not actually sample the texture, so it must be used in conjunction with a **TextureSample** node.

[![Texture Object Parameter](https://dev.epicgames.com/community/api/documentation/image/c798b13e-8a10-466a-84b4-b0dde09b021f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c798b13e-8a10-466a-84b4-b0dde09b021f?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Texture**

 | 

Specifies the texture sampled by the expression.

 |
| 

**Sampler Type**

 | 

The type of data that will be sampled and output from the node.

 |
| 

**MipValueMode**

 | 

Selects how to customize the sample's mip-level or derivatives from the default hardware computed. Affects the look and performance.

 |

This node is used with [MaterialFunctions](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-functions-in-unreal-engine).

## TextureSampleParameter2D

The **TextureSampleParameter2D** expression is identical to the TextureSample except that it is a parameter that you can modify in Material Instances and through Blueprint or code.

[![Texture Sample Parameter](https://dev.epicgames.com/community/api/documentation/image/702e4d79-64bb-45b8-a4b9-0de5e5b57fc6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/702e4d79-64bb-45b8-a4b9-0de5e5b57fc6?resizing_type=fit)

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Texture**

 | 

Specifies the texture sampled by the expression.

 |
| 

**Sampler Type**

 | 

The type of data that will be sampled and output from the node.

 |
| 

**MipValueMode**

 | 

Selects how to customize the sample's mip-level or derivatives from the default hardware computed. Affects the look and performance.

 |
| Inputs |   |
| --- | --- |
| 

**UVs**

 | 

Takes in UV texture coordinates to use for the texture. If no values are input to the UVs, the texture coordinates of the mesh the material is applied to are used.

 |
| Outputs |   |
| --- | --- |
| 

**RGB**

 | 

Outputs the three-channel RGB vector value of the color.

 |
| 

**R**

 | 

Outputs the red channel of the color.

 |
| 

**G**

 | 

Outputs the green channel of the color.

 |
| 

**B**

 | 

Outputs the blue channel of the color.

 |
| 

**A**

 | 

Outputs the alpha channel of the color. If a texture does not contain an alpha channel, connecting the 'alpha' channel to something, while not technically illegal, will always result in zero (black).

 |

## TextureSampleParameterSubUV

The **TextureSampleParameterSubUV** expression is identical to the [ParticleSubUV](https://dev.epicgames.com/documentation/en-us/unreal-engine/particle-material-expressions-in-unreal-engine) except that it is a parameter that can be modified in instances of the material and through code.

| Item | Description |
| --- | --- |
| Properties |   |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Blend**

 | 

Blends together each frame of the SubUV sprite layout, rather than instantly "popping" from one frame to the next.

 |
| 

**Texture**

 | 

Specifies the texture sampled by the expression.

 |
| 

**Sampler Type**

 | 

The type of data that will be sampled and output from the node.

 |
| 

**MipValueMode**

 | 

Selects how to customize the sample's mip-level or derivatives from the default hardware computed. Affects the look and performance.

 |
| Inputs |   |
| --- | --- |
| 

**UVs**

 | 

The UV input is ignored and does nothing.

 |
| Outputs |   |
| --- | --- |
| 

**RGB**

 | 

Outputs the three-channel RGB vector value of the color.

 |
| 

**R**

 | 

Outputs the red channel of the color.

 |
| 

**G**

 | 

Outputs the green channel of the color.

 |
| 

**B**

 | 

Outputs the blue channel of the color.

 |
| 

**A**

 | 

Outputs the alpha channel of the color. If a texture does not contain an alpha channel, connecting the 'alpha' channel to something, while not technically illegal, will always result in zero (black).

 |

## TextureSampleParameterCube

The **TextureSampleParameterCube** expression is identical to the TextureSample except that it only accepts cubemaps and it is a parameter that can be modified in instances of the material and through code.

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Texture**

 | 

Specifies the texture sampled by the expression.

 |
| 

**Sampler Type**

 | 

The type of data that will be sampled and output from the node.

 |
| 

**MipValueMode**

 | 

Selects how to customize the sample's mip-level or derivatives from the default hardware computed. Affects the look and performance.

 |
| Inputs |   |
| --- | --- |
| 

**UVs**

 | 

Takes in UV texture coordinates to use for the texture. If no values are input to the UVs, the texture coordinates of the mesh the Material is applied to are used. This input accepts a two-channel vector value.

 |
| Outputs |   |
| --- | --- |
| 

**RGB**

 | 

Outputs the three-channel RGB vector value of the color.

 |
| 

**R**

 | 

Outputs the red channel of the color.

 |
| 

**G**

 | 

Outputs the green channel of the color.

 |
| 

**B**

 | 

Outputs the blue channel of the color.

 |
| 

**A**

 | 

Outputs the alpha channel of the color. If a texture does not contain an alpha channel, connecting the 'alpha' channel to something, while not technically invalid, will always result in zero (black).

 |

## TextureSampleParameterMovie

The **TextureSampleParameterMovie** expression is identical to the TextureSample except that it only accepts movie textures (Bink movies) and it is a parameter that you can modify in instances of the Material and through code.

| Property | Description |
| --- | --- |
| 
**Parameter Name**

 | 

Specifies the name used to identify the parameter in instances of the Material and through code.

 |
| 

**Group**

 | 

Provides a way to organize parameter names into groups, or categories, within a MaterialInstanceConstant. All parameters within a Material that have the same Group property name will be listed underneath that category in the Instance Editor.

 |
| 

**Texture**

 | 

Specifies the texture sampled by the expression.

 |
| 

**Sampler Type**

 | 

The type of data that will be sampled and output from the node.

 |
| 

**MipValueMode**

 | 

Selects how to customize the sample's mip-level or derivatives from the default hardware computed. Affects the look and performance.

 |
| Inputs |   |
| --- | --- |
| 

**UVs**

 | 

Takes in UV texture coordinates to use for the texture. If no values are input to the UVs, the texture coordinates of the mesh the Material is applied to are used.

 |
| Outputs |   |
| --- | --- |
| 

**RGB**

 | 

Outputs the three-channel RGB vector value of the color.

 |
| 

**R**

 | 

Outputs the red channel of the color.

 |
| 

**G**

 | 

Outputs the green channel of the color.

 |
| 

**B**

 | 

Outputs the blue channel of the color.

 |
| 

**A**

 | 

Outputs the alpha channel of the color. If a texture does not contain an alpha channel, connecting the 'alpha' channel to something, while not technically illegal, will always result in zero (black).

 |