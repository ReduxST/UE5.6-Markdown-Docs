# Deformer Graph

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine)  
**Processed:** 2025-06-14 16:19:41

---

Using **Unreal Engine**'s **Deformer Graph** plugin, you can create and edit Deformer Graph assets to perform and customize mesh deformations for any skinned mesh in Unreal Engine. Using Deformation Graphs, you can create and modify logic that adjusts the geometry of the mesh to fine tune mesh deformation behaviors, or create entirely new deformations within Unreal Engine. Most often Deformer Graphs are used to fine-tune realistic skin and fabric behaviors in motion for characters, or for one-off animations that are easier to create using deformation logic than hand-authored animations.

![deformer graph demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d8b4c28-4ad8-4d90-93ce-3d36b788b7aa/dgdemo.gif)

Mesh Deformers come in many forms, such as [Morph Targets](/documentation/en-us/unreal-engine/morph-target-previewer), [Cloth simulation](/documentation/en-us/unreal-engine/cloth-simulation-in-unreal-engine), and even generated models created in external DCC (Digital Content Creation) software such as the [Machine Learning (ML) Deformer](/documentation/en-us/unreal-engine/how-to-use-the-machine-learning-deformer-in-unreal-engine).

This document provides an overview of the Deformer Graph system in Unreal Engine.

## How to Use the Deformer Graph

Here you can read about how to set up and begin using the Deformer Graph in Unreal Engine.

#### Prerequisites

-   Enable the **Deformer Graph** [plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). Navigate in the **Menu Bar** to **Edit > Plugins** and locate the **Deformer Graph** in the **Animation** section, or using the **Search Bar**. Enable the plugin and restart the editor.

![enable the deformer graph plugin and restart the editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87fa5d53-0e4c-462e-ba54-83649ad2e2dd/plugin.png)

-   Your project contains a skinned mesh, which could be a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) character, or a [Static Mesh](/documentation/en-us/unreal-engine/static-meshes) object.

## Creating a Deformer Graph Asset

Create a **Deformer Graph** asset by **right-clicking** in the **Content Browser** and navigating to **Animation > Deformers > Deformer Graph**.

![to create a new asset right click in the content browser and navigate to animation deformers and select deformer graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a9d448b-b4ad-4353-9a9f-6a7e32b6aa92/contentbrowser.png)

With a Mesh selected in the Viewport, you can also navigate in the **Details** panel to the **Mesh Deformer** property, and after **enabling** the Mesh Deformer property, you can create a new Deformer Graph by selecting the **Deformer Graph** option from the selection menu.

![enable the mesh deformer property in the characters details panel and select create new deformer graph from the drop down selection menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00b8308f-5426-4505-970e-9876214df9aa/createdeformergraph.png)

The following default Deformer Graph Assets are packaged alongside the Deformer Graph Plugin and are available for you to use or customize when creating custom mesh deformer logic for your characters and objects. These Deformer Graphs can be accessed in the Content Browser by navigating to **Engine > PlugIns > Deformer Graph Content > Deformers**.

![find the default deformer graphs packaged with the deformer graph plugin in the engine folder under plugins deformer graph content deformers ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e51fa91-9cf3-400f-b1ae-72672336b57a/defaultgraphs.png)

| Asset | Description |
| --- | --- |
| **DG\_LinearBlendSkin** | This graph applies the standard linear blend skinning pipeline. All skinning features are supported using this graph. |
| **DG\_LinearBlendSkin\_Morph** | This graph applies the standard linear blend skinning and [Morph Target](/documentation/en-us/unreal-engine/morph-target-previewer) pipelines. All features of those pipelines are supported using this graph. |
| **DG\_LinearBlendSkin\_Morph\_Cloth** | This graph applies the standard linear blend skinning, [Morph Target](/documentation/en-us/unreal-engine/morph-target-previewer) and [Cloth simulation](/documentation/en-us/unreal-engine/cloth-simulation-in-unreal-engine) pipelines. All features of those pipelines are supported using this graph. This is a superset of the **DG\_LinearBlendSkin and DG\_LinearBlendSkin\_Morph** Deformer Graph, and can be used instead of those without any performance penalty. The simpler Deformer Graph assets, **DG\_LinearBlendSkin** and **DG\_LinearBlendSkin\_Morph**, exist individually as reference for those who want to build their own implementations. |
| **DG\_LinearBlendSkin\_Morph\_Cloth\_RecomputeNormals** | This graph applies the standard linear blend skinning, [Morph Target](/documentation/en-us/unreal-engine/morph-target-previewer), and [Cloth simulation](/documentation/en-us/unreal-engine/cloth-simulation-in-unreal-engine) pipelines. It also applies additional passes to recompute vertex normals. This emulates the existing behavior of the GPU Skin Cache with Recompute Tangents settings. |

If you do not see the **Engine** folder, or the default Deformer Graphs as available options when selecting a Deformer Graph in a mesh's Details panel, ensure you have **Plugin Content** enabled in the **View Settings** of the **Content Browser**.

![enable show plug in content in the content browser settings menu to show the plug in content](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b0fd88c-b36b-428d-8ecd-d850f2ff1a00/plugincontent.png)

For more information about creating and using Deformer Graph assets, refer to the [How to create a custom Deformer Graph](/documentation/en-us/unreal-engine/how-to-create-a-custom-deformer-graph-in-unreal-engine) guide.

## Opening The Deformer Graph

After enabling the **Deformer Graph Plugin,** you can open the **Deformer Graph Editor** by **double-clicking** any Deformer Graph Asset in the **Content Browser** or in a game objects **Details** panel, in the **Mesh Deformer** property.

![double click a characters deformer graph asset in the details panel to open the deformer graph editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54a45b25-cd3a-405b-b3f7-871750065c9e/opendeformergraph.png)

### Deformer Graph Interface

Here is a reference for the Deformer Graph interface you can use when creating and editing custom Deformer Graph assets, to deform meshes in Unreal Engine.

![deformer graph editor interface with highlighted boxes representing the editors unique panels and features](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/776dbb03-58d2-4370-8d27-371d7ef2d8de/interface.png)

| Interface | Description |
| --- | --- |
| 1\. **Compile** | Compiles the Deformer Graph. |
| 2\. [Viewport](/documentation/en-us/unreal-engine/editor-viewports-in-unreal-engine) | See the effect of the Deformer Graph logic on the mesh. |
| 3\. [Palette](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#palettepanel) | A toolbox of unique Deformer Graph Blueprint nodes. |
| 4\. [Explorer](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#deformergraphsubgraphs) | Add and manage Deformer Graph [Subgraphs](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#deformergraphsubgraphs), [Component Bindings](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#componentbindings), [Variables](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#variables), and [resources](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#resources). |
| 5\. [Graph Editor](/documentation/en-us/unreal-engine/user-interface-reference-for-the-blueprints-visual-scripting-editor-in-unreal-engine) | Similar to other **Blueprint Editors**, manage and edit Deformer Graph logic using a series of unique [Deformer Graph nodes](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#palettecomponentreference). |
| 6\. **Compile Output** | Review compiler logs and information, after successful and unsuccessful compiles of the Deformer Graph. |
| 6\. [Details](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#detailspanel) | Access component and node specific information and properties. |
| 7\. [Shader Text Editor](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#shadertexteditor) | A text editor used to modify **Custom Compute Kernel** node programming using **HLSL** (**High-Level Shader Language**). |

### Palette Panel

Using the Deformer Graph **Palette**, you can drag and drop custom Deformer Graph nodes and Kernels to reference or use when creating mesh deformation logic.

![palette pallet panel demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2c71da6-d646-4b4a-9422-21b3cbe3e2e8/palettedemo.gif)

For a comprehensive list and description of the available components in the Palette panel, refer to the [Palette Component Reference](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#palettecomponentreference) list at the bottom of this document.

### Deformer Graph Subgraphs

There are 3 types of **Subgraphs** you can use within a Deformer Graph.

![select a graph from the sub graph menu in the deformer graph explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2f30f60-f3d1-4511-9914-bcc6601205f8/subgraphs.png)

By default, a Deformer Graph only contains an **Update Graph** which is executed once per frame.

You can optionally add a **SetUp Graph** that executes when the owning object is **initialized**.

Additionally, you can create and use **Trigger Graphs,** which can be executed by request from a Blueprint or C++ code. When Trigger Graphs are requested, they are queued and executed **after** an initial Setup Graph, if one is present, and **before** the Update Graph every frame.

You can add a Subgraph to the Deformer Graph by clicking **Add** (**+**), adjacent to the **Graphs** section of the Explorer panel, or by clicking the green (**+**) **Add New** button at the top of the Explorer panel. After clicking either, you can then choose to create either a **Setup Graph** or a **Trigger Graph** from the drop down menu.

![create a graph using the green add new button or the plus button in the explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd486f30-6d85-4c3e-b1cf-d57f4fdc5f78/createnewsubgraph.png)

No additional Update Graphs, and only one Setup Graph, can be added to a Deformer Graph. You can add as many Trigger Graphs as your project needs. Trigger Graphs can then be renamed, by **double-clicking** the name of the desired Trigger Graph in the **Explorer** panel or by selecting the Trigger Graph and pressing the **F2** key.

### Component Bindings

Component Bindings are references to available components contained in the owning object.

![select a component from the component bindings menu in the deformer graph explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59d1396e-abae-46cd-bd66-a3130b39c845/componentbindings.png)

You can create additional component bindings to the Deformer Graph by clicking **Add** (**+**), adjacent to the **Component Bindings** section of the **Explorer** panel, or by clicking the green (**+**) **Add New** button at the top of the **Explorer** panel.

![create a component binding using the green add new button or the plus button in the explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67f9bbe1-04e9-4fc8-8338-a37b31dbd773/createcomponentbinding.png)

The following are some examples of Component Bindings that you can use when creating Deformer Graph logic:

| Component Binding | Descriptions |
| --- | --- |
| **Skeletal Mesh Component** | Add a reference to the owning object's **Skeletal Mesh** component. Using the Skeletal Mesh, many properties and components can be referenced, such as the **Mesh Vertices** and **Triangles**, and **Scene Time**. |
| **Scene Component** | 
A **Scene** component draws data and information from the **scene** the character or subject the Deformer Graph is occupying. Game time and other useful information can be drawn from scene components.

Scene information can also be gathered from a Skeletal Mesh or Skinned Mesh component binding, but there may be a context where using a separate Scene component binding is useful for control or organizational purposes.



 |
| **Skinned Mesh Component** | A Skinned Mesh component can be representative of any kind of skinned mesh. This can be an auxiliary object attached to the character, or this can represent a character or object without bones. |

### Variables

In the **Variables** section of the **Explorer Tab** you can create and manage externally visible variables you can reference to adjust and control logic in the Deformer Graph.

![select a variable from the variables menu in the deformer graph explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7276e45a-1181-4e51-840f-57b7608bbe8a/variables.png)

You can create a variable by clicking **Add** (**+**), adjacent to the **Variables** section of the **Explorer** panel, or by clicking the green (**+**) **Add New** button at the top of the **Explorer** panel.

![create a variable using the green add new button or the plus button in the explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dd78008-438a-468c-8125-5e47c13ecad3/createnewvariable.png)

After creating a new variable, you can open its properties in the Details panel, by selecting the variable in the Explorer panel.

![select a variable in the graph to see its properties in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b971a62b-4baa-4382-af6f-b55db09936dc/variabledetails.png)

In the Details panel, you can name the variable using the **Variable Name** property, and define its **Data Type**. Variables can be assigned any data type, or component, for use with the other Deformer Graph nodes.

### Resources

Similar to [Variables](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#variables), you can create and manage **Shader Resources** in the **Resources** section of the Explorer panel. Resources are internal references to values and components that other nodes in the Deformer Graph can reference to perform mesh deformation functions.

![select a resource from the resources menu in the deformer graph explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc1c58aa-940a-4def-b9e0-1830694b318b/resources.png)

You can create a resource by clicking **Add** (**+**), adjacent to the **Resources** section of the **Explorer** panel, or by clicking the green (**+**) **Add New** button at the top of the **Explorer** panel.

![create a resource using the green add new button or the plus button in the explorer panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/706945b9-6bbd-4ccb-8220-1acdb146a24b/createresource.png)

After creating a resource, you can select it in the Explorer tab to open its properties in the Details panel.

![slelect a resource in the explorer panel to open its properties in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b9ff26c-af63-4fae-ae3f-210b7df4dfa9/resourcesdetails.png)

You can adjust the following resource parameters:

| Property | Description |
| --- | --- |
| **Resource Name** | Name the resource in the provided field. |
| **Data Type** | Set the type of data the resource can store. |
| **Component Binding** | Set the component binding the resource is bound to. |
| **Data Domain** | 
Set the data domain for the resource.

In the first drop down menu you can select the dimension. You can select from the following dimensions:

-   **Triangle**: Select all triangles.
-   **Vertex**: Select all vertices.
-   **Vertex > Bone**: Select groups of vertices by bone.
-   **Vertex > Index0**: Select groups of vertices within Index 0.
-   **Vertex > UVChannel**: Select groups of Vertices by UVChannel.
-   **Expression…**: Input a custom data type using the provided field.

When the dimension is set to Triangle or Vertex, you can additionally specify how many data values should be stored per entry. Beginning at **x1**, for one data point per entry, you can also select from **x3**, **x4**, or **x8**.

Data points must match, not only in their dimension but also in the amount of data values present for each entry. If you are experiencing input/output pin incompatibility, or unresponsive resources in the Defromer Graph logic, ensure your **Data Domain** properties are set to compatible values.



 |

Unlike variables, you can **set**, as well **reference** resource values and components within the Deformer Graph. After creating a resource, you can **drag-and-drop** the resource into the Deformer Graph Editor, and choose from a **Get** instance, used for referencing the existing value contained in the resource, a **Set** instance, used for setting or defining the resource for use later, or a **Get/Set** instance, that can be used to both set and reference the stored value.

![select get set getset resource instance from context menu when adding to graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7b68fce-6475-492a-89fd-ffb0f5ce5943/getsetresourcedemo.gif)

After creating a **Get/Set Resource**, **Get Resource**, or **Set** **Resource node**, you can modify how the instance of the resource interacts with the **resource buffer**. You can define this behavior by selecting the node in the **Graph** and setting the **Write Type** property in the node's **Details** panel.

![select the resource in the graph to adjust its write type property in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ffbc796-8d0f-4d19-82b3-017b808d89e9/writetype.png)

You can choose from the following write type property options:

| Option | Description |
| --- | --- |
| **Write** | Writes the value to the resource buffer. |
| **Write Atomic Add** | Overwrites the graph value to the value in the resource buffer. |
| **Write Atomic Min** | Overwrites the graph **Min** value to the value in the resource buffer. |
| **Write Atomic Max** | Overwrites the graph **Max** value to the value in the resource buffer. |

### Details Panel

The **Deformer Graph Details** panel shows information and settings regarding each Deformer Graph node. To see a node's properties, select the node in the Graph Editor, and the Details Panel shows its properties.

![select a kernel in the graph to open its properties in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31b6940e-3355-4464-8488-45da8f637638/kerneldetails.png)

When selecting Kernel Nodes, **Input** and **Output** bindings can be added and modified.

To achieve functional results, Input and Output bindings must match the exact data type they are connected to. Please ensure any Kernel Input or Output binding is set to match the desired connected or extracted value.

### Shader Text Editor

Using the **Shader Text Editor,** you can program **Custom Compute Kernel** nodes to control specific mesh deformation behaviors.

![after creating a kernel you can edit and reference its hlsl programming in the shader text panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be58abed-4d47-411d-bda3-2f3ac85492a4/kernelshadertext.png)

The Shader Text Editor operates in **HLSL** (High-Level Shader Language) to program kernels.

For each Custom Compute Kernel added to a Deformer Graph, a new tab opens within the Shader Text Editor panel.

![switch between custom kernel tabs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0925df37-c3cf-4059-a796-0f4f0460ea81/kerneltabsdemo.gif)

Within each Custom Compute Kernel tab, you can access the node's **Declarations**, which are read-only, and represent the Graph Editor modification made to the node, such as added Input and Output bindings.

![the declarations section of the shader text editor displays the hlsl declarations of the kernel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fa6653ce-f546-42e9-9627-053c8120cba1/declerations.png)

You can also access the node's **Shader Text** where you can write custom HLSL code to create mesh deformations.

![the shader text section of the shader text editor displays the custom hlsl programming of the kernel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/342ce9a1-eb4a-4a18-a3dd-e5dbc799ecc3/shadertext.png)

For more information about the HLSL coding standard, refer to the [Microsoft High Level Shader Language reference documentation and programming guide](https://learn.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl).

For an example workflow of using the Shader Text Editor, refer to the [How to Create a Deformer Graph](/documentation/en-us/unreal-engine/how-to-create-a-custom-deformer-graph-in-unreal-engine) guide.

## Palette Component Reference

Here you can reference a list of the available components found in the Deformer Graph **Palette** and a description of their function.

![the palette pallet panel is where you can access the custom deformer graph nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21b312ce-f1a3-45ad-b3f5-fdfdef8fa882/palette.png)

| Palette Component | Node | Description |
| --- | --- | --- |
| **Animation Attributes** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12b652ca-745d-4dc5-bdca-e9e04a9d5d76/animationattributes.png) | Add references to [Animation Attributes](/documentation/en-us/unreal-engine/fbx-attributes-in-unreal-engine) that you can use to trigger or activate Deformer logic. |
| **Cloth** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6bcd56a-a6a0-4319-84dd-4748a26e2c38/cloth.png) | Add and attach references to [Cloth simulation](/documentation/en-us/unreal-engine/cloth-simulation-in-unreal-engine) models associated with the skeletal mesh. Refer to [Cloth Simulation Models](/documentation/en-us/unreal-engine/cloth-simulation-in-unreal-engine) for more information. |
| **Connectivity** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec71fbab-6d19-4277-a5e7-56dbd8e0024a/connectivity.png) | Connect Skinned Mesh components to an existing vertex or vertice data set. |
| **Debug Draw** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41046f9c-0d4f-4b49-b635-65f73257d657/debug.png) | 
Uses a connected Skinned Mesh component binding to draw a debug view of the mesh in the Viewport. Debug data is extracted as a **string** and is accessible using the nodes **output** pin in the Graph.

Options in the Details panel include:

-   **Force Enable**: Forces the debug draw to occur in the Viewport.
-   **Max Line count**: Set the maximum amount of lines between vertices the debug drawing can display.
-   **Max triangle Count**: Set the maximum amount of geometry triangles the debug drawing can display.
-   **Max Character Count**: Set the maximum number of characters the debug drawing can display.
-   **Font Size**: Set the font size for the debug drawing overlay.



 |
| **Morph Target** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83560f8a-e44a-42d6-90b1-6074ea9c27dd/morphtarget.png) | Using a Skinned Mesh component, the [Morph Target](/documentation/en-us/unreal-engine/morph-target-previewer) node can isolate the **Delta** Position **and** Delta Normal **as** Vector 3\*\* values. |
| **Scene Data** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d80106d-3c64-4494-b350-f8f293d4ae57/scenedata.png) | Extract scene data you can use to control or trigger Deformer Graph logic. A **Scene component binding** can be created, but you can also use a **Skeletal Mesh component binding** to reference the current scene the skeletal mesh occupies at runtime. |
| **Skeleton** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da51d17b-5159-42c6-97c6-45d8bb01e78e/skeleton.png) | 

Extract Skeleton data from a Skeletal Mesh component binding. The available outputs include:

-   **Num Bones**: Output value is a **UInt** and represents the number of bones in the skinned mesh's skeleton.
-   **Bone Matrix**: Output value is a 3x4 matrix of bone positions.
-   **Bone Weight**: Output value is the **alpha** weight of bones, in the form of a float.
-   **Weighted Bone Matrix**: Output value is a 3x4 matrix of weighted bone positions.



 |
| **Skinned Mesh** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1462b7c-d9c4-4957-960c-33f2476cce91/skinnedmesh.png) | 

Extract mesh data from any **Skinned Mesh** component binding. The available outputs include:

-   **Num Vertices**: Output the number of vertices contained in the mesh as an integer.
-   **Position**: Output the position of the Vertices in a **Vector 3**.
-   **Tangent X**: Output the **tangent** on the **X** axis as a **Vector 2**.
-   **Tangent Z**: Output the **tangent** on the **Z** axis as a **Vector 2**.
-   **Num UV Channels**: Output the number of UVChannels the mesh possesses as an integer.
-   **UV**: Output the mesh vertices by a set UVChannel as a Vector 2 value.
-   **Color**: Output the **R**, **G**, **B**, and **W** values of the meshes color as a **Vector 4**.
-   **Num Triangles**: Output the number of triangles that comprise the mesh's geometry as an integer.
-   **Index Buffer**: Output and isolate the mesh's index buffer coordinates from its mesh vertice coordinates, as an array.



 |
| **Custom Compute Kernel** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10bb6ad3-bde5-44a2-8ef8-a99bf21a6326/kernel.png) | Create a **Custom Compute Kernel** that can be programmed using **HLSL** (**High-Level Shader Language**), to perform custom mesh deformations. For more information on creating and using Custom Compute Kernels, refer to the [How to Create a Custom Deformer Graph](/documentation/en-us/unreal-engine/how-to-create-a-custom-deformer-graph-in-unreal-engine) documentation. |
| **Execute Skinned Mesh** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22e102d3-c953-4ade-a518-e420d81af7df/execute.png) | 

Using a **Skinned Mesh** component as an input, you can execute mesh data threads for use in a **Kernel**. In the Details panel you can set the **Domain** of the function to either run the Kernel with one thread per **vertex**, or one thread per **triangle**.

The **Execute Skinned Mesh** node outputs an **IntVector 3** value that can be connected and used with a **Custom Compute Kernel**. To isolate the output data on only the **X**, **Y**, or **Z** axis, expand the **output** pin using the **triangle** next to the output pin. Each axis has a separate **Integer** output pin.



 |
| **Write Skinned Mesh** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2aae6de-8cf3-4b75-9994-945f0ce946a3/writemesh.png) | 

The **Write Skinned Mesh** output node is the final operation of a Deformer Graph, writing any modifications performed to the mesh's **vertices or** triangles\*\*.

The **Skinned Mesh** input pin connects to the initial mesh **component binding**. Then, using the Vector 3 **Position** input pin, and the Vector 4 **Tangent X**, **Tangent Z**, and **Color** input pins, the new mesh properties can be written to the mesh.



 |
| **Bool Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34c3e4a3-fbd2-433d-b005-81bd2f27b4d1/bool.png) | Set a constant **boolean** value. The node can accept a bool variable value, or you can manually toggle the boolean in the graph or in the node's **Details** panel using the **Value** property. |
| **Component Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b27a5e6-ce3d-453a-8a21-f63def9b903b/component.png) | Set a **component constant**, using a component binding. A component constant can be set in the graph, or manually defined using the **Value** property in the node's **Details** panel. |
| **Float Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b04a38f1-41c6-477c-aa7d-d65bbdc1a844/float.png) | Set a constant **float** value. The node can accept a **float** value from another component, or you can manually set a value in the graph or in the node's **Details** panel. |
| **Int Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03eb6849-6655-4321-8f88-cb93dda1e697/int.png) | Set a constant **signed integer** value. The node can accept **zero** and **positive** integer values from another component, or you can manually set a value in the graph or in the node's **Details** panel. |
| **UInt Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee91ab41-d3a7-4efd-a1f7-b0844cc60331/uint.png) | Set a constant **unsigned integer** value. The node can accept **any** integer value from another component, or you can manually set a value in the graph or in the node's **Details** panel. |
| **Double Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abbc6f86-3061-4e65-a189-a64e106f0d24/double.png) | Set a constant **double** value. The node can accept any double value from another component, or you can manually set a value in the graph or in the node's **Details** panel. |
| **Int Vector 2 Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e84f8cc1-9437-4922-b08c-0bc75ee35616/intvec2.png) | Set a constant **Vector 2** value on the **X** and **Y** axes. The node can accept any vector 2 value from another component, or you can manually set **X** and **Y** integer values in the graph by expanding the input pin using the triangle or in the node's **Details** panel. Using the triangle near the output pin you can also split the vector 2 value into Integer values for the **X** and **Y**. |
| **Int Vector 3 Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa939f40-2564-4f42-8a72-96ea26949f25/intvec3.png) | Set a constant **Vector 3** value on the **X**, **Y**, and **Z** axes. The node can accept any Vector 3 value from another component, or you can manually set **X**, **Y**, and **Z** integer values in the graph by expanding the input pin using the triangle or in the node's **Details** panel. Using the triangle near the output pin you can also split the Vector 3 value into Integer values for the **X**, **Y**, and Z\*\* values. |
| **Int Vector 4 Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27212883-4296-4f0a-847c-d3a66d7d84a7/intvec4.png) | Set a constant **Vector 4** value on the **X**, **Y**, **Z**, and **W** axes. The node can accept any Vector 4 value from another component, or you can manually set **X**, **Y**, **Z**, and **W** integer values in the graph by expanding the input pin using the triangle or in the node's **Details** panel. Using the triangle near the output pin you can also split the Vector 4 value into Integer values for the **X**, **Y**, **Z**, and **W** values. |
| **Linear Color Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c19cc54e-8376-4950-8dbb-c22706f1c426/color.png) | Set a constant **Color** value for the **R**, **G**, **B**, and **A** values stored as a **float 4** value. The node can accept any float 4 or Color value from another component, or you can manually set **R**, **G**, **B**, and **A** float values in the graph by expanding the input pin using the triangle or in the node's Details panel. Using the triangle near the output pin you can also split the Color value into float values for the individual **R**, **G**, **B**, and **A** values. |
| **Quat Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/945733c9-046b-403d-a764-ea28bbaa5cc7/quat.png) | Set a constant **Quat** or **float 4** value on the **X**, **Y**, **Z**, and **W** axes. The node can accept any Quat or float 4 value from another component, or you can manually set **X**, **Y**, **Z**, and **W** float values in the graph by expanding the input pin using the triangle or in the node's **Details** panel. Using the triangle near the output pin you can also split the Quat value into separate float values for the individual **X**, **Y**, **Z**, and **W** values.. |
| **Rotator Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/965401fc-a6de-470f-91fd-bcaf6d76643b/rotator.png) | Set a constant **Rotator** or **float 3** value on the **X** (**Pitch**), **Y** (**Yaw**), and **Z** (**Roll**) axes. The node can accept any Rotator or float 3 value from another component, or you can manually set **Pitch**, **Yaw**, and **Roll** values in the graph by expanding the input pin using the triangle or in the node's **Details** panel. Using the triangle near the output pin you can also split the Rotator value into float values for the **Pitch**, **Yaw**, and **Roll**. |
| **Transform Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb56db1f-7f47-4323-a99f-8dfa004ec217/transform.png) | Set a constant **Transform** value. The node can accept any transform value from another component, or you can manually set the Location, Rotation, and Scale values on the **X**, **Y**, and **Z** axes in the node's **Details** panel. |
| **Vector 2 Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57471180-a8a9-4d35-be0f-b6e8954f1e87/floatvector2.png) | Set a constant **Vector 2** value on the **X**, **Y**, and **Z** axes. The node can accept any Vector 2 value from another component, or you can manually set **X**, **Y**, and **Z** float values in the graph by expanding the input pin using the triangle or in the node's **Details** panel. Using the triangle near the output pin you can also split the Vector 2 value into float values for the **X**, **Y**, and **Z** axes. |
| **Vector 3 Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a09668a-b0b8-4107-9363-28dd5e630915/floatvector3.png) | Set a constant **Vector 3** value on the **X**, **Y**, and **Z** axes. The node can accept any Vector 3 value from another component, or you can manually set **X**, **Y**, and **Z** float values in the graph by expanding the input pin using the triangle or in the node's **Details** panel. Using the triangle near the output pin you can also split the Vector 3 value into float values for the **X**, **Y**, and **Z** axes. |
| **Vector 4 Constant** | ![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d3e654e-3ff2-4416-9c4f-3bfa7a1520c8/floatvector4.png) | Set a constant **Vector 4** value on the **X**, **Y**, **Z**, and **W** axes. The node can accept any Vector 4 value from another component, or you can manually set **X**, **Y**, **Z**, and **W** float values in the graph by expanding the input pin using the triangle or in the node's Details panel. Using the triangle near the output pin you can also split the Vector 4 value into float values for the **X**, **Y**, **Z**, and **W** axes. |