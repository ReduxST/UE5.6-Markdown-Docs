# Material Functions Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview)  
**Processed:** 2025-06-14 16:56:53

---

**Material Functions** let you package parts of a Material graph into a reusable asset that you can share to a library and easily insert into other Materials. Their purpose is to streamline Material creation by giving instant access to commonly used networks of Material nodes.

For example, the **Blend\_Overlay** function shown below contains the entire Material Expression network shown on the right side of the image. Instead of constructing this node network over and over, you can insert it directly into your graph from the Material Function library.

![Material Function example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b24b5058-c794-4665-be2a-dbc41cd206b0/overlay-function.png)

Functions are edited in the Material Editor like a normal Material, but with some restrictions on what nodes you can use. When used properly, they can reduce Material redundancy which in turn reduces artist maintenance effort. Material Functions keep duplicate expressions in sync, preventing the inevitable bugs that arise when one duplicate is missed during a modification.

Material Functions are a distinct asset class in the **Content Browser**. Their graphs are similar to Materials, but differ in one major regard. Instead of a Main Material node, Material Functions have FunctionOutput nodes, which appear as output pins on the final Material Function node when it is used in a Material.

It may help to think of a Material function like an electronics project enclosure. You can add as many inputs and outputs as you deem necessary. The heart of the function is the Material Expression network between those inputs and outputs. This example takes two layers and blends them together like a [Photoshop screen blend](https://helpx.adobe.com/photoshop/using/blending-modes.html). The function abstracts the details from an artist, so they do not have to actually know the math of a screen blend to use a screen blend operation.

![Blend Screen Function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9e41bf7-54a8-416a-96f0-608bb0471d83/blend-screen.png)

Material Function input (1) and output (2) nodes.

As you can see above, what happens between the input and the output is entirely up to you and will be defined by any network of standard Material expression nodes. Once you insert a Material Function into a Material, you will only see the Matrial Function Call node with its inputs and outputs. The rest of the graph is hidden within the function.

![Blend Screen example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ce8073e-6173-4c06-9305-bc7b1b6d9966/blend-screen-example.png)

## Material Function Library

When your Material Function is finished, you can publish it to the **Material Function library** for easy access during Material creation. The Material Function library is found within the Palette on the right side of the Material Editor. The Palette contains a categorized and filterable list of available Material Functions. This list is populated from any loaded functions, but also from any deault Material Functions found in the **Content Browser Database**.

![Material Function Library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/705f938f-db1b-4c93-b2d5-6da52171d078/palette-function-library.png)

You can hover over these entries to see their Description as a tooltip, or drag and drop one into your Material.

In order for a Material function to appear in the Material Function Library, its **Expose to Library** property must be checked. In the Material Function editor, deselect all nodes by clicking an empty space in the graph to show the base properties for the Material Function. The Expose to Library option is found in the Details panel.

For a full listing of the existing functions within the Material Function Library by default, please see the [Material Function Reference](/documentation/en-us/unreal-engine/unreal-engine-material-functions-reference).

## Function Related Nodes

Below are the Material expression nodes that relate to Material Functions, along with their purpose:

-   **MaterialFunctionCall** - Allows using an external function from another Material or function. The external function's input and output nodes become inputs and outputs of the function call node.
-   **FunctionInput** - Can only be placed in a Material Function, where it defines one of the function's input pins.
-   **FunctionOutput** - Can only be placed in a Material Function, where it defines one of the function's output pins.
-   **TextureObject** - Useful for providing a default texture for a texture function input within a function. This node does not actually sample the texture, so it must be used in conjunction with a TextureSample node.
-   **TextureObjectParameter** - Defines a texture parameter and outputs the texture object, used in Materials that call a function with texture inputs. This node does not actually sample the texture, so it must be used in conjunction with a TextureSample node.
-   **StaticSwitch** - Performs a compile time choice between two inputs, based on the input value.
-   **StaticBool** - Useful for providing a default bool value for a static bool function input within a function. This node does not switch between anything, so it must be used in conjunction with a StaticSwitch node.
-   **StaticBoolParameter** - Defines a static bool parameter and outputs the static bool value, used in Materials that call a function with static bool inputs. This node does not switch between anything, so it must be used in conjunction with a StaticSwitch node.

## Input and Output

Since Material functions are encapsulated networks of nodes, it is up to the user to make sure that data can flow into and out of them. This is handled by way of *FunctionInput* and *FunctionOutput* nodes. Understanding these nodes is critical for using Material functions.

Within the Material Function itself, FunctionInput and FunctionOutput nodes appear like so:

![Input and Output nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9262a4bd-2727-4540-8eeb-0a92255910b1/input-output.png)

When the Material Function is used in a Material, the FunctionInput and FunctionOutput nodes appear as input and output pins on the Material Function node:

![Input and output pins on Material Function Call](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f71e93a-8663-4f43-8031-85bd8fa0e1e6/input-output-node.png)

### FunctionInput Nodes

As stated, **FunctionInput** nodes serve as the gateway through which data enters a Material Function. A given function may have any number of these input nodes, each corresponding with an input pin on the Material Function Call node.

![FunctionInput node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c21f392c-61c8-4de4-9658-db8c65544ffc/function-input.png)

FunctionInput nodes have the following properties and data pins:

| Item | Description |
| --- | --- |
| Properties |   |
| **Input Name** | The name of the input, which is visible as an output pin on the Material Function when it is used within a Material. |
| **Description** | A description of the input, which is visible as a tooltip when you mouse over the corresponding input pin on the Material Function node. |
| **Input Type** | This defines what type of data the input accepts. See [Input Types](/documentation/en-us/unreal-engine/unreal-engine-material-functions-overview#inputtypes) below. |
| **Preview Value** | This serves as a means of testing and a way to help visualize that the function is doing during the construction process. Any value entered here is used as if it was passed in from an input outside the function. |
| **Use Preview Value as Default** | This checkbox allows the data set in the preview value to act as the default value. This is useful if you do not want to force the user to provide an input into the function for this value. |
| **Sort Priority** | This number is used to control the order in which input pins are displayed on the Material Function node. The order is lowest to highest. |
| Input Pins |   |
| **Preview** | Data passed into this input supersedes the Preview Value property. As with its associated property, this is useful for testing the function during construction and setting up default values. |
| Output Pins |   |
| **(Unlabled)** | This provides the output for the incoming data that will be processed by the function. |

### FunctionOutput Nodes

A FunctionOutput node provides the means by which data within a Material Function exits the function for further use in a Material. In other words, it outputs final result of the Material function. As with FunctionInput nodes, a function may have any number of output nodes, leading to any number of potential output pins.

![FunctionOutput node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2e1e7a4-3f28-4824-bf08-a8f072e74490/function-output.png)

When a **FunctionOutput** node is selected, the following properties are accessible in the Details panel.

| Item | Description |
| --- | --- |
| Material Expression Function Output |   |
| **Output Name** | The name of the output, which is visible as an output pin on the Material Function when it is used within a Material. |
| **Description** | A description of the output, which displays as a tooltip when you mouse over the corresponding output pin on the Material Function node. |
| Material Expression |   |
| **Sort Priority** | This number is used to control the order in which output pins are displayed on the Material Function node. The order is lowest to highest. |
| **Description** | This description field defines the text in Comment Bubble of the node. This is only visible **within** the Material Function editor. |
| Output Pins |   |
| **(Unlabled)** | This provides the output for the incoming data that will be processed by the function. |

### Input Types

Inputs have a specified type that is required of any expressions connected to them. To set the Input Type, select a **FunctionInput** node in the Material Function editor, and use the **Input Type** dropdown to select an option.

![Function input types](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01961969-2fe8-4ae8-b468-7759fa3ebba3/function-input-type.png)

When called in a Material, the input type is displayed as an abbreviation next to the input connectors. In this case, both the inputs were Vector3's so V3 is displayed. Anything connected to an input when used in a Material **must** be convertible to the correct input type, or you will receive an error.

![Color burn input types](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56a28a62-2514-43fa-9199-9d76ffd848ca/color-burn-input-types.png)

Below are the available input types and their associated abbreviations:

| Input Type | Abbreviation |
| --- | --- |
| **Scalar** | S |
| **Vector2** | V2 |
| **Vector3** | V3 |
| **Vector4** | V4 |
| **Texture2D** | T2D |
| **TextureCube** | TCube |
| **Texture2DArray** | T2dArr |
| **VolumeTexture** | TVol |
| **StaticBool** | B |
| **MaterialAttributes** | MA |
| **TextureExternal** | TExt |

## Common Properties

While editing a Material Function, deselecting all nodes or clicking in the background of the Material Graph will make the base properties of the function visible in the Details panel.

| Item | Description |
| --- | --- |
| Properties |   |
| **Description** | This description will display as a tooltip when users mouse over the Material Function in the palette, or mouse over the body of the Function Call node within the Material Editor. |
| **Expose to Library** | If this box is checked, the Material Function will appear within the Material Functions list inside the Material Editor palette so that you can insert it into Materials. You may need to restart the editor for a new function to appear. |
| **Library Categories** | This array holds all of the categories of the Material Functions tab under which this function will appear. |

## Previewing

When editing a Material Function, the preview viewport shows whichever node is being previewed. You can **right-click** on any node and choose **Start Previewing Node** to preview the results of the Material network up to that point.

![Start Previewing Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b6b73d3-a61b-4c89-8de9-daafc5cb2286/start-previewing-node.png)

Most of the time you will want to preview the function output, or the end result of the Material Function. The Material Function output node is previewed by default.

![Previewing Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa086176-baa0-45e7-a313-784d55c74b0c/preview-output.png)

### Function Input Preview

Function Input nodes have some options for specifying preview values, since they do not know the actual values that artists will use within the Material. Each input has a built-in **Preview Value** that you can use to show a constant for float input types. Function inputs also have a 'Preview' connector which allows you to override the built-in value with any value that matches the input type. In this example, texture samples are used to provide a preview value for the two Vector3 inputs.

![Preview texture sample inputs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bc779f0-8d7d-47b2-9e59-fe4a0d2d753e/preview-value-inputs.png)

Note that the input has an option in the details panel to **Use Preview Value As Default**. When this is enabled, the preview value is used any time the function is called in a Material and nothing is connected to that input. The preview value acts as a fallback, and prevents compilation errors when nothing is connected to the input. This makes the input an optional input, so it is drawn in gray.

## Parameters

You can use [Parameters](/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine) in a Material Function like you would in a regular Material. These parameters are passed directly to any Material for use. There are some slight differences in the procedure for using texture parameters.

### Texture Parameters

To use a texture parameter within a Material Function, create a **FunctionInput\* node and change the data type to** Texture2D**. Connect it to the texture object override pin in a** Texture Sample\*\* node.

![Texture Parameter within function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/09edc04c-05ef-4958-9e1c-6d749ac01248/texture-parameter-function.png)

When you use that Material Function in a Material, place a **TextureObjectParameter** node and connect it to the **Texture2D** input pin on the Material Function.

![Texture object parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ab3f7a5-6bc2-4206-9523-dc26da91cf40/texture-object-parameter.png)

### Static Bool Parameter

Similarly for Static Switch parameters, create a FunctionInput and change the Input Type to **StaticBool**. Connect it to a **StaticSwitch** node:

![Static Switch function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f145c88-3f02-4a16-871e-7972e0e747c6/static-switch-function.png)

In the Material that uses the function, place a **StaticBoolParameter** node and connect it to the input that accepts a Static Bool (**Enable Tiling** in this example).

![Static Bool Parameter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e734e3b-390f-42a4-a873-76ec1ff5b2f9/static-bool-param.png)

## Organization

By design, Material Functions are often used by many artists and teamates who did not have a hand in creating the function itself. Therefore, it is important to provide good documentation of what the functions do, and what values are needed for their inputs and outputs. For this reason, functions have several documentation fields on top of the function name and input/output names:

### Function Desctiption

Material Functions have a **Description** field where you can document what the function does. To add a description, click on an empty area in the Material Graph while editing a Material Function. This will display the function's properties in the Details panel, where you can enter a description in the field.

![Material Function description](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d878dae-d46d-49a7-b184-e56610ea6b6d/mat-function-description.png)

The description text displays as a tooltip when you mouse over the Material Function Call node within a Material Graph.

![Custom fresnel tooltip](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f582369a-ba29-48e8-ab61-cdfa2aec25e0/fresnel-description.png)

### Input and Output Descriptions

You can add a name and description for the input and output pins on your Material Function. While editing a Material Function select an input or output node in the Material Graph. In the details panel, fill out the **Input Name** and **Description** fields.

![Input descriptions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be5fadd6-58f6-4331-9a13-cfb200a7e87b/input-descriptions.png)

When this Material Function is used in a Material, the each input pin displays the name you entered, and the description is shown as a tooltip whe you mouse over the input.

![Input tooltip](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d36aa69-b57e-4c02-bc19-513a2496e204/input-tooltips.png)

While you are editing a Material Function, all tools for organizing and documenting your Material Graph are available to you. Read here about [organizing a Material Graph](/documentation/en-us/unreal-engine/organizing-a-material-graph-in-unreal-engine).

## Propagation

When you edit a Material Function and click the **Save** button to recompile and apply the changes, the new version propagates to any loaded Materials or functions which reference this Material Function. Any unloaded Materials which reference the function will be updated with the changes when they are next loaded.

When an input or output is deleted from a function and the changes are propagated, any links to these deleted connectors in Materials that use the function will be broken! It is important to consider this before you recompile a Material Function, because the propagation cannot be undone. The more Materials a function is used in, the bigger the potential for breakage, so be careful.

All loaded Materials that use the function will be marked dirty when the function change is propagated, which can be used to see which packages could be resaved to prevent increased load times. You can find all the loaded Materials which use a function by **right-clicking** in the **Content Browser** and choosing **Find Materials Using This**.

![Find Materials using this function](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f87a93d8-e7c2-482f-8866-c1eaba8509f4/find-materials-using.png)

## Nesting Functions

You can nest Material functions within other functions, and chain them together arbitrarily. The only caveat is that Material Functions cannot be nested in such a way that creates a circular dependency.

## Compilation Errors

If there are errors within a Material Function, a compilation error dialog is generated when you attempt to compile the Material. A red error message also appears on top of the Material Function that did not compile correctly. You can hover the mouse over the error message to see a tooltip that describes the compilation error. In this example, the Material Function is not receiving data in either of its inputs, which causes the compilation to fail.

![Compilation error message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4017ce6-4075-427c-a769-d19a3962b8c9/compilation-error.png)

You can avoid the above errors by supplying preview values for your inputs and then activating each input's **Use Preview Value as Default** property. However, this practice may serve as a double-edged sword, as there will be no highly obvious alert (such as an error message) to remind you that you have left an input unplugged.

![Use preview value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6657e8d9-d2f4-4e93-b758-c5e5fba67dfe/preview-value-default.png)

## Default Material Functions

Unreal Engine includes several dozen premade default Material functions. These are accessible from the [Material Editor Palette](/documentation/en-us/unreal-engine/unreal-engine-material-editor-ui#palettepanel), or the right-click search menu.

If you would like to edit one of the default Material Functions, you can find the assets in the **Content Browser** within the **Engine > Content > Functions** folder.

If any changes are made and saved to a default Material function, those changes will exist in all instances of the function. For this reason, it is strongly recommended that you make a duplicate copy of default functions when you want to make changes.

For more information about the default Material Functions included with Unreal Engine, please see the [Material Function Reference](/documentation/en-us/unreal-engine/unreal-engine-material-functions-reference).