# Setting Up A Groom Deformer Graph

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-groom-deformer-graph-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-groom-deformer-graph-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:00

---

The [Deformer Graph](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine) is a plugin with which you can create and edit **Deformer Graph** assets that perform and customize mesh deformations for any skinned mesh in Unreal Engine.. With Deformer Graphs, you can create and modify logic that adjusts the mesh's geometry to fine-tune deformation behaviors or create entirely new deformations within the engine. Deformer Graphs are often used to fine-tune skin, fabric, and groom behaviors in motion for characters, or for one-off animations that are easier to create using deformation logic than hand-authored animations.

This is an example of a groom with (left) and without a deformer "straightening" each curve.

|   |   |
| --- | --- |
| ![Groom with a deformer.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a0191af-734c-4d3f-bb80-b8307eaceb73/groom-with-deformer.png) | ![Groom without a deformer.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/494569cf-50ee-4d90-bef3-0fadb13be3d2/groom-without-deformer.png) |
| Groom without a deformer. | Groom with a deformer "straightening" each curve. |

## Groom Deformer Graph

A deformer graph expresses the applied deformation as a graph whereby the Custom Compute Kernel node contains the code handling the deformation. The input for deformation can come from various sources, such as Scene Data, Grooms, and Guides. The graph output writes the groom's values, such as position and attributes.

For a more in-depth overview of how to useDeformer Graph and familiarize yourself with its editor, see [Deformer Graph](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine).

The Deformer Graph has several key areas you'll want to be aware of:

![Example of a Deformer Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eab2f20e-9619-46bb-b407-f69020b35732/groom-deformer-graph-example.png)

1.  Source and Parameters panels
2.  Deformer Graph
3.  Details Panel
4.  Shader Text Editor panel

The key elements that make up a Deformer Graph are:

-   The **Primary** node provides a binding to the type of data it provides. This should be set to **Groom Component**.
    
    ![Primary node assigned to a Groom Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80560203-57ac-4951-b023-969d9ab61089/groom-deformer-graph-elements-1.png)
-   The **Groom** and **Guides** input nodes. These provide access to the groom and guides data, respectively.
    
    ![Groom and Guides nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/434ece47-0de6-48d2-a667-c0736f7d145b/groom-deformer-graph-elements-2.png)
-   The **Custom Compute Kernel (MyKernel)** node defines the deformation applied to the groom and guides.
    
    ![Custom Compute Kernel node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a71469a-0e8e-4818-852d-6d7a9982653e/groom-deformer-graph-elements-3.png)
-   The **Write Groom** output node writes out modified groom data.
    
    ![Write Groom output node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd891c13-278b-4446-93ce-3ca8e4346fa1/groom-deformer-graph-elements-4.png)
-   This node includes some limitations:
    -   Use the **Position** or **Radius** outputs to write the position and radius of the groom. Use the **Position and Radius** output to write out both position and radius.
    -   Only existing attributes within a groom can be written out. For instance, you can only write out roughness and not color if a groom asset has a Roughness attribute but no Color attribute.
-   In the **Shader Text Editor**, you can see the declarations (read-only) from the Custom Compute Kernel node and add your custom HLSL code to define the groom's deformation.

### Set up a Groom Deformer Graph

Using this feature requires first enabling the **Deformer Graph** plugin in the **Plugins** Browser and restarting the engine for the changes to take effect.

To setup a groom with a deformer graph:

1.  Create a **Deformer Graph** asset in the **Content Browser**.
2.  In the **Source** panel, set the **Primary** node dropdown to **Groom Component** and drag the node into the graph.
3.  Right-click in the graph and add the following nodes:
    
    -   A **Groom** data interface node that gives you access to all the properties of the primary groom.
    -   A **Write Groom** output data interface node that gives you access to all writable properties of the primary groom.
    -   A **Custom Compute Kernel** node to define the deformation logic of this groom.
4.  Connect the nodes in the graph to look like this:
    
    ![Groom Deformer Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f83155c1-8d2b-4184-b8b8-1c492f39eabc/groom-deformer-graph-setup-1.png)
    -   Dragging and dropping an output wire onto the **New Input** pin of the **Custom Compute Kernel** node automatically configures the node's user interface with the type and frequency. You can also set these up manually in the Details panel for this node.
5.  Select the **Custom Compute Kernel** node. In the **Details** panel under **Settings**, set the **Execution Domain** to be one of the following:
    
    ![Groom Deformer Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b492dc2-fd5f-48c0-b102-580fcceb6bec/groom-deformer-graph-setup-2.png)
    -   **Curve** uses one GPU thread per curve.
    -   **Control Points** uses one GPU thread per control point
6.  Use the **Shader Text Editor** to input your custom HLSL code for this groom's deformation logic.
    
    ![Groom Deformer Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e28a798-b122-4c5a-bfad-0d5c94eb3514/groom-deformer-graph-setup-3.png)
7.  **Compile** and **Save** the deformer graph.

Once the deformer graph is set up, you can apply a groom deformer to a **Groom** component added to a skeletal mesh. Use the **Mesh Deformers** selection box to apply the groom deformer you've created.

![Groom Deformer Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/627884bc-25ea-4117-932a-ffb26b8581e3/groom-deformer-graph-setup-4.png)

Some additional things to consider when setting up a groom deformer:

-   You can access additional data like scene data or input parameters with Blueprint logic.
-   The compute kernel defines the deformation logic. It consumes inputs and computes outputs. Each input has a specific **Type** (float, int, float3, and so on) and **Frequency** (control points or curves). You can drag and connect input wires from the Groom Interface to the Custom Compute Kernel to let the user interface automatically configure the type and frequency or set this up manually in the Details panel.
-   All **time** and **game** dependent effects on a groom are only visible when the editor is **Playing** or **Simulating**.

### Groom Deformer Graph Shader Code Example

The following example demonstrates a groom deformer applied to a groom containing four vertical strands. The deformer only changes the groom's position over time to create a "wave" effect. The groom on the left has no deformer, whereas the one on the right does.

![Groom with and without deformer.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6243d6d-b127-4848-b0af-6b0bad76aede/groom-dg-shader-code-example.png)

The groom on the left is undeformed. The groom on the right has a deformer.

To achieve this type of effect with a deformer graph, the groom's **Rest Position** and **U Coordinate** along each strand needs to be read to compute a dynamic offset based on time.

The kernel code to achieve such a deformation looks like this:

```
`if (Index < ReadControlPointCount()) { const float3 P = ReadInPosition(Index); const float U = ReadInCoordU(Index); const float T = abs(sin( U * ReadTime())); WriteOutPosition(Index, P + T * float3(5,0,0)); }`
Copy full snippet
```
if (Index < ReadControlPointCount()) { const float3 P = ReadInPosition(Index); const float U = ReadInCoordU(Index); const float T = abs(sin( U \* ReadTime())); WriteOutPosition(Index, P + T \* float3(5,0,0)); }

The kernel has an implicit `Index` variable defining the global GPU thread index. This is used for reading the correct control points using the input reading function:

```
`ReadInPosition(Index) ReadInCoordU(Index)`
Copy full snippet
```
ReadInPosition(Index) ReadInCoordU(Index)

You only need to ensure that invalid data isn't accessed since the kernel is dispatched in groups of x threads (where the default is 64 threads). The following condition is added for this:

```
`if (Index < ReadControlPOintCount())`
Copy full snippet
```
if (Index < ReadControlPOintCount())

The output is written using the output interface function `WriteOutPosition` like this:

```
`WriteOutPosition(Index, MyTransformedPosition)`
Copy full snippet
```
WriteOutPosition(Index, MyTransformedPosition)

## Shader Text Editor

The **Shader Text Editor** is where you'll modify **Custom Compute Kernel** node programming using high-level shader language (HLSL) to control specific mesh deformation behaviors.

This panel is in the bottom-right corner of the deformer graph. It contains two parts: **Declarations** and **Shader Text**. The declarations section displays the kernel input and output functions and is read-only. You'll input your custom HLSL code into the shader text section.

![Groom Deformer Graph Shader Text Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c2457f0-3d3a-4142-bd20-282dd782aa8d/groom-dg-shader-text-editor.png)

The Shader Text Editor panel displays the declarations and some custom deformation code.

When you compile the deformer graph, use the **Compiler Output** panel below the graph to check for any errors. Any errors found during compilation are displayed here.

![Groom Deformer Graph Compiler Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0363bdfa-ea38-46a5-9d20-f2b21533b07f/groom-dg-compiler-output.png)

For additional information and examples of how to use the Deformer Graph's Shader Text Editor, see:

-   [Deformer Graph](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine)
-   [How to Create a Deformer Graph guide](/documentation/en-us/unreal-engine/how-to-create-a-custom-deformer-graph-in-unreal-engine)
-   [Microsoft's High Level Shader Language reference documentation and programming guide](https://learn.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl)