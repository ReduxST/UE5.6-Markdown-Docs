# Material Function Expressions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-function-expressions-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:12

---

## FunctionInput

The **FunctionInput** expression can only be placed in a material function, where it defines one of the function's inputs.

| Item | Description |
| --- | --- |
| Properties |   |
| **Input Name** | The input's name, which will be displayed on MaterialFunctionCall expressions that use the material function containing the input. |
| **Description** | A description of the input, which will be displayed as a 'tooltip' when the connector for this input on a MaterialFunction Call expression is hovered over with the mouse. |
| **Input Type** | The type of data this input expects. Data passed to this input will be cast to this type, throwing a compiler error if the cast fails because the data is not compatible. |
| **Preview Value** | The value to use as a preview for this input when editing the material function containing it. |
| **Use Preview Value As Default** | If enabled, **Preview Value** will be used as the default value for this input if no data is passed in. |
| **Sort Priority** | Specifies the priority for this input to use when determining the order of the inputs to be displayed on a MaterialFunctionCall expression. |

This node is used with [Material Functions](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine).

## FunctionOutput

The **FunctionOutput** expression can only be placed in a material function, where it defines one of the function's outputs.

| Item | Description |
| --- | --- |
| Properties |   |
| **Output Name** | The output's name, which will be displayed on MaterialFunctionCall expressions that use the material function containing the output. |
| **Description** | A description of the output, which will be displayed as a tooltip when the connector for this output on a MaterialFunction Call expression is hovered over with the mouse. |
| **Sort Priority** | Specifies the priority for this output to use when determining the order of the outputs to be displayed on a MaterialFunctionCall expression. |

This node is used with [Material Functions](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine).

## MaterialFunctionCall

The **MaterialFunctionCall** expression allows you to use an external [Material Function](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine) from another material or function. The external function's input and output nodes become inputs and outputs of the function call node. If a MaterialFunction is selected in the **Content Browser** when placing one of these expressions, it will automatically be assigned.

**Shortcut:** *F + Left Mouse Click*

| Item | Description |
| --- | --- |
| Properties |   |
| **Material Function** | Specifies the [Material Function](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine) to be used. |

This node is used with [Material Functions](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine).

## StaticBool

The **StaticBool** expression is used to provide a default bool value for a static bool function input within a function. This node does not switch between anything, so it must be used in conjunction with a StaticSwitch node.

| Item | Description |
| --- | --- |
| Properties |   |
| **Value** | The value of the bool, *True* (checked) or *False*. |

This node is used with [Material Functions](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine).

## StaticSwitch

The **StaticSwitch** expression works like a StaticSwitchParameter, except that it only implements the switch and does not create a parameter.

| Item | Description |
| --- | --- |
| Properties |   |
| **Default Value** | The default bool value of the parameter that determines which input is active, *True* (checked) or *False*. |
| Inputs |   |
| **True** | The input that is used when the **Value** of the switch is *True*. |
| **False** | The input that is used when the **Value** of the switch is *False*. |
| **Value** | Takes in a bool value that determines which input is active. |

This node is used with [Material Functions](/documentation/en-us/unreal-engine/material-functions-in-unreal-engine).

## TextureObject

The **TextureObject** expression is used to provide a default texture for a texture function input within a function. This node does not actually sample the texture, so it must be used in conjunction with a TextureSample node.

| Item | Description |
| --- | --- |
| Properties |   |
| **Texture** | The texture from the **Content Browser** that will be applied to this node. |
| **Sampler Type** | The type of data that will be output from the node. |