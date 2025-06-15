# Using the Main Material Node

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:34

---

**Materials** are created using a specialized coding language called **High Level Shading Language** or HLSL. HLSL allows Materials to send instructions directly to the graphics hardware, giving artists and coders control over what is displayed on screen. Inside Unreal Engine 5 (UE5) the **Material Expression** nodes that are used to create Materials contain small snippets of this HLSL code.

The inputs on the **Main Material Node** are the last stop in a UE5 Material graph. Whatever combination of Material Expression nodes is connected to the inputs on the Main Material Node is what determines the overall appearance of the final Material when it is compiled and used in your Level.

![UE5 Main Material Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d10e4fe-111a-4a32-b150-fa25bbe06453/main-material-node-ue5.png)

The Main Material Node with default inputs.

## Material Inputs

Each **input** on the Main Material Node defines a single unique aspect of the appearance and surface properties of your Material. For example, if you connect a **Constant3Vector** to the **Base Color** input and give it a value of (1,0,0), you can make the Material red.

![Vector 3 in Base Color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53baddc5-8cf3-4408-b73f-c4eb595b4ee4/base-color.png)

This Material graph only explicitly defines a single aspect of the Material—its Base Color.

However, the overall appearance of the Material is the collective result of all the enabled inputs in the Main Material Node. Enabled input pins are white on the Main Material Node, and disabled inputs are grayed out.

![Enabled inputs in Main Material Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a947be3-2c18-4840-9932-b1f4fdf22ff8/active-inputs.png)

Inputs that do not receive any data from Material expressions in the graph simply revert to their default values. For example, even though there is nothing plugged into Metallic, Specular, or Roughness, these properties still contribute to the appearance of the Material.

![Empty material inputs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a67964db-9463-4d62-9738-bd7a085f1fe8/empty-inputs.png)

-   **Metallic** defaults to 0 (non-metallic).
-   **Specular** defaults to 0.5.
-   **Roughness** defaults to 0.5.

Therefore, a Material with those values plugged into Metallic, Specular, and Roughness looks exactly the same as the one shown previously.

  ![Default values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e296cabd-a72a-4e72-be5d-688be71d2d7e/default-no-inputs.png) ![Default Spec Metallic Roughness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42c8a0ae-2102-48ed-ae61-3d95560fc5f1/default-spec-metallic-roughness.png) ![New values in color and roughness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ff62541-d032-4d02-a238-26232ed12f43/new-values.png)

Slider: Note that the preview render does not change when default values are connected the the Main Material Node.

By changing the values, you can alter the appearance and surface properties of the Material. In the third image, the roughness value is changed from **0.5 to 0.07**, and the Material appears more polished. Changing the values in the **Constant3Vector** to **(0,0,1)** makes the Base Color blue instead of red.

### Understanding Material Inputs

UE5 uses a **Physically Based Rendering** (PBR) workflow for Materials, meaning Materials closely approximate the way surfaces interact with light in the real world. To create Materials effectively it is important to understand exactly how each input affects the final Material. These two pages provide foundational information about the PBR Materials workflow in Unreal Engine 5.

-   Read the [Physically Based Materials](/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine) overview to learn best practices for creating Materials in a PBR workflow.
-   Read the [Material Inputs](/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine) page for examples and descriptions of what each input on the Main Material Node does.

### Enabled and Disabled Inputs

Some of the input pins in the Main Material Node are enabled by default, while others are disabled. The following properties in the **Details Panel** determine which inputs are enabled.

-   Material Domain
-   Blend Mode
-   Shading Model

![Default Main Material Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af693307-51cd-451d-8537-8839f389eeec/enabled-inputs.png)

Modifying any of these three Material properties can change the inputs that are enabled and disabled in the Main Material Node.

In the middle example, changing the Blend Mode from **Opaque** to **Translucent** enables the Opacity and Refraction inputs. It also disables any inputs that are not used by translucent Materials.

![Main Material Node variations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7c0d207-5a2c-4294-bca6-15c0561753c2/main-mat-node-variations.png)

On the far right, selecting the **Clear Coat Shading Model** enables the inputs for Clear Coat and Clear Coat Roughness.

You must select the Main Material Node to access these properties in the **Details** panel. To select the Main Material Node, click it with the **left mouse button** or click anywhere in the background of the Material graph.

### Nodes Connected to Disabled Inputs are Ignored

When switching between Blend Modes or Shading Models, some inputs may become disabled. Material Expressions remain connected to disabled inputs, but are ignored when the Material is compiled.

In this example, a constant value was connected to Opacity. The Blend Mode was changed from **Translucent** to **Opaque**, causing the Opacity input to become disabled.

![Opacity disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6055e10-30f6-4adc-9346-d597514e32d8/opacity-ignored.png)

The constant node remains connected to the Opacity input, but the cable and input are grayed out to indicate that the input is disabled. Nodes connected to disabled inputs do not affect the compiled Material in any way.

## Main Material Node Details Panel Properties

When the Main Material Node is selected in the Material Editor, the **Details** panel displays a list of all editable properties relating to how the Material can be used.

As demonstrated above, properties like **Blend Mode** and **Shading Model** directly influence which inputs are enabled in the Main Material Node. Other sections let you modify how the Material interacts with specific platforms or rendering features.

Here is a brief breakdown of what each section in the Main Material Node Details panel does:

![Details panel properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/728d59b6-d5b5-49cd-a732-d54350049f45/details-panel-properties.png)

| Section Name: | Description |
| --- | --- |
| **Physical Material** | This allows you to specify what type of Physical Material is used for this Material. |
| **Material** | This is where you will spend most of your time when editing Materials. The Material section is where you can change the Material Domain, Blend Mode, and Shading Model along with many more options. |
| **Physical Material Mask** | An array of Physical Material Maps to be used for this Material. |
| **Translucency** | This is where you can adjust how Translucency in this Material will function. Please note that this is only editable if the Material Blend Mode is set to Translucent. |
| **Translucency Self Shadowing** | This is where you can adjust how Translucent self shadowing looks and behaves. Please note that this is only editable if the Material Blend Mode is set to Translucent. |
| **Usage** | This is where you set what type of objects this Material will work with. Usage flags are usually set automatically by the editor. However if you know that this Material is supposed to be used with a certain object type, make sure you enable it here to avoid any future mistakes |
| **Mobile** | This is where you set how this Material should work when used on a mobile device like a smart phone. |
| **Forward Shading** | Per-material overrides for when the Forward Shading Renderer is in use. |
| **Group Sorting** | Allows you to change the order of Parameter Groups in your Material. |
| **Post Process Material** | This is where you define how this Material should work with Post Process and Tone Mapping. Please note that this is only editable if the Material Domain is set to Post Process. |
| **Refraction** | Properties to change the refraction mode and refraction depth bias. |
| **Lightmass** | This is where you can adjust how this Material will interact with Lightmass. |
| **Previewing** | Change the Static Mesh used to preview the Material in the Material Editor viewport. |
| **Import Settings** | A selection of import data types and options relevant to the selection for use with this Material. |

Read more about these settings on the [Material Properties](/documentation/en-us/unreal-engine/unreal-engine-material-properties) page.

## Using the Main Material Node

Inputs on the Main Material Node work exactly like any other Material Expression or Function in the Material graph.

To connect a Material Expression to an input in the Main Material Node:

1.  **Left-click** the output pin of a Material Expression and drag the mouse to an input pin on the Main Material Node.
    
    ![Drag connection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4b75033-fd24-4678-b05a-caa2af7efdc2/drag-connection.png)
2.  Release the **left mouse button** over the input pin when the green check icon appears.
    
    ![Connect Material node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1799d479-d384-4c02-b71a-4dade55e94d3/connect-node.png)

If you do not know how to place Material Expressions and Functions in your Material graph, [read here](/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine).

## Previewing and Applying Materials

The Main Material node is the end-point of a UE5 Material graph. The information that you pass into the inputs on the Main Material node is what ultimately determines the appearance of the Material. As you connect Material expressions to the Main Material node, the preview in the Material Editor viewport updates continuously so you can evaluate your changes and make sure you are getting the desired results.

Continue reading about the [various ways to preview Materials](/documentation/en-us/unreal-engine/previewing-and-applying-your-materials-in-unreal-engine) and how to apply them to the Actors in your Level.