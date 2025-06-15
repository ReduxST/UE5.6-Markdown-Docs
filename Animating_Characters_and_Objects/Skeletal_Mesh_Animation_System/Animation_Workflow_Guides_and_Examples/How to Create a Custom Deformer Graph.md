# How to Create a Custom Deformer Graph

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-custom-deformer-graph-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-custom-deformer-graph-in-unreal-engine)  
**Processed:** 2025-06-14 16:28:45

---

You can use [Deformer Graphs](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine) to create custom mesh deformations within **Unreal Engine**. After creating a custom Deformer Graph asset, you can use the [Deformer Graph Editor](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#deformergrapheditor), with its unique set of [Blueprint nodes](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#palettecomponentreference) to edit existing mesh deformation systems, such as [Morph Targets](/documentation/en-us/unreal-engine/morph-target-previewer) and [Cloth simulations](/documentation/en-us/unreal-engine/cloth-simulation-in-unreal-engine), or you can create new mesh deformation systems for any **Linear Skinned Mesh**.

This document provides an example workflow of how to create a custom Deformer Graph to apply a twisting mesh deformation to a Skeletal Mesh character at runtime.

#### Prerequisites

-   Enable the **Deformer Graph** [plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). Navigate in the **Menu Bar** to **Edit > Plugins** and locate the **Deformer Graph** in the **Animation** section, or using the **Search Bar**. **Enable** the plugin and **restart** the Editor.

![enabled the deformer graph beta plugin and restart the editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a19a403-c563-46f4-a568-5eb16d7aeff4/plugin.png)

-   Your project contains a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) Character. We used the Unreal Engine mannequin in the example workflow, and you can access it in the [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine).

## Create a Custom Deformer Graph

In the **Details** panel of your **Skeletal Mesh Character**, **enable** the **Mesh Deformer** property and then select the **Deformer Graph** option from the drop down menu to create a new Deformer Graph asset.

![create deformer graph in skeletal mesh details panel in deformer property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ae3fc2c-15f8-44a5-9b0e-6e014967d6eb/createdeformergraph.png)

After creating the asset, open the **Deformer Graph Editor** by **double-clicking** the asset in the **Mesh Deformer** property. In the Deformer Graph's **Details** panel, use the drop down menu in the **Mesh** property to select the mesh you are modifying.

![select the mesh in the deformer graph details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af7f9a03-0448-49bd-ab53-9880a83df443/meshdet.png)

From the **Pallet** panel, **drag-and-drop** the **Skeletal Mesh Component Binding** into the Deformer Graph's **Update Graph** to read the mesh's data.

![add skeletal mesh component binding from the palette panel pallet](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30452da0-98c4-4a56-b3de-a7c73cb42d41/addskelmesh.png)

Next, to rewrite the mesh's position data, add the **Write Skinned Mesh** node to the **Update Graph** and connect the **Skeletal Mesh** component binding.

![add write skinned mesh node to deformer graph from the palette panel and connect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/913783b7-ffb4-4b6c-bf6e-0abc51d3dc28/addwrite.png)

Add and connect the **Execute Skinned Mesh** to the **Skeletal Mesh component binding** to set the domain of the mesh deformation. Select the node and change the **Domain** property to the **Vertex** option.

![add and connect execute skinned mesh node to the graph from the palette panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fc09dfb-3775-4c80-9bb1-174a3296fa33/addexecute.png)

Next, add and connect the **Scene Data** node to the **Skeletal Mesh component binding**, to extract information about the scene the mesh occupies. This workflow uses the **Time** data to drive the mesh deformation at runtime.

![add and connect the scene data node to the graph from the palette panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a9bffdb-1203-4a55-8d1f-ac8540366bfa/addscene.png)

To read the position of the vertices of the skeletal mesh, add the **Skinned Mesh** node and connect it to the **Skeletal Mesh component binding**. This node provides the **Position**, **Tangent X**, and **Tangent Y** coordinates for the characters mesh vertices.

![add and connect the skinned mesh node to the graph from the palette panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72658f92-43de-4717-9192-48a0251ff97e/addskinned.png)

Now, add a **Custom Compute Kernel** to the **Update Graph**. The Custom Compute Kernel performs the actual mesh deformation calculations using **HLSL** (**High-Level Shader Language**) programming.

![add the custom compute kernel node to the graph from the palette panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/810596da-9561-4f83-87dc-a870cc416da1/addkernel.png)

Before writing the driving HLSL programming, or connecting the node to any other nodes in the graph, you must create the **input** and **output** pins, which are used by the HLSL program to perform the mesh deformation. In the **Details** panel of the **Custom Compute Kernel**, add the following **input** pins to make use of the information extracted from the Skeletal Mesh Component Binding using the various **Read** nodes.

![in the custom compute kernels details panel add the input bindings from the table below](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34af3af9-f49c-4fd3-8eeb-adc0e1fc1f63/inputref.png)

| Pin | Data Type | Domain | Description |
| --- | --- | --- | --- |
| `Num Threads` | **Int Vector 3** | **Parameter** | The Num Threads pin can accept the **Domain** of the mesh deformation from the **Execute Skinned Mesh** node's output pin. |
| `Twist` | **Float** | **Parameter** | Using a **Constant** or **Variable** value, this input pin determines the degree of the maximum amount of twist the mesh deforms. |
| `Start` | **Float** | **Parameter** | Using a **Constant** or **Variable** value, this input pin determines the start position of the twist on the Mesh's Z axis, in **Unreal Engine Units** (**cm**). |
| `End` | **Float** | **Parameter** | Using a **Constant** or **Variable** value, this input pin determines the end position of the twist on the mesh's **Z** axis, in **Unreal Engine Units** (**cm**). |
| `Time` | **Float** | **Parameter** | This variable input pin draws the game time from the mesh at runtime. |
| `Position` | **Vector 3** | **Vertex x1** | This input pin reads the position of each mesh axis at runtime. |
| `Tangent X` | **Vector 4** | **Vertex x1** | This input pin reads the **tangent** value of the X axis. |
| `Tangent Y` | **Vector 4** | **Vertex x1** | This input pin reads the **tangent** value of the Z axis. |

Connect the **Execute Skinned Mesh** node's **Num Threads output pin** to the **Custom Compute Kernel** node's **Num Threads input pin**. Then set the **Execution Domain** property to the **Vertex** setting in the Custom Compute Kernel's **Details** panel.

![connect the execute skinned mesh node to the num threads input on the custom compute kernel and change the kernels execution domain to vertex mode in the details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd748870-32cc-45de-81ac-3d8909499dcd/domain.png)

Next, add the following **Output** pins in the Custom Compute Kernel's **Details** panel, to output the deformed mesh data for the **Write Skinned Mesh** node to write back to the Skeletal Mesh.

![set the custom compute kernels output bindings in the details panel from the table below](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4b39068-f4c9-404e-8f8b-f4ace167367d/outputref.png)

| Pin | Data Type | Domain | Description |
| --- | --- | --- | --- |
| `Out Position` | **Vector 3** | **Vertex x1** | Outputs the newly deformed axis positions of the mesh vertices. |
| `OutTangentX` | **Vector 4** | **Vertex x1** | Outputs the modified **tangent** value on the **X** axis. |
| `OutTangentZ` | **Vector 4** | **Vertex x1** | Outputs the modified **tangent** value on the **Z** axis. |

**Save** and **Compile** the asset.

![save and compile the asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1e193e0-387f-4092-a0b5-cc537ec5b39f/complie.png)

Then ensure your **Custom Compute Kernel**'s **Declarations (Read-Only)** tab in the **Shader Text Editor** panel registers all of the input and output pins as HLSL declarations.

![reference the declarations read only section of the shader text editor panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5157f85-074c-406e-b104-0fa7a152bdd4/decref.png)

The **Decelerations (Read Only)** tab should contain the following text:

Decelerations (Read Only)

```
	`// Parameters and resource read/write functions 	int3 ReadNumThreads(); 	float ReadTwist(); 	float ReadStart(); 	float ReadEnd(); 	float ReadTime(); 	uint GetVertexCount(); 	float4 ReadTangentX(uint VertexIndex); 	float4 ReadTangentZ(uint VertexIndex); 	float3 ReadPosition(uint VertexIndex); 	void WriteOutTangentX(uint VertexIndex, float4 Value); 	void WriteOutTangentZ(uint VertexIndex, float4 Value); 	void WriteOutPosition(uint VertexIndex, float3 Value); 	// Resource Indexing 	uint Index;	// From SV_DispatchThreadID.x`

Copy full snippet
```
// Parameters and resource read/write functions int3 ReadNumThreads(); float ReadTwist(); float ReadStart(); float ReadEnd(); float ReadTime(); uint GetVertexCount(); float4 ReadTangentX(uint VertexIndex); float4 ReadTangentZ(uint VertexIndex); float3 ReadPosition(uint VertexIndex); void WriteOutTangentX(uint VertexIndex, float4 Value); void WriteOutTangentZ(uint VertexIndex, float4 Value); void WriteOutPosition(uint VertexIndex, float3 Value); // Resource Indexing uint Index; // From SV\_DispatchThreadID.x

Next, in the **Shader Text** section of the **Shader Text Editor** panel, input the following HLSL program to perform the vertex deformation on the Skeletal Mesh.

Shader Text Editor

```
	`if (Index > ReadNumThreads().x) return;  	float3 Position = ReadPosition(Index); 	float4 LocalTangentX = ReadTangentX(Index); 	float4 LocalTangentZ = ReadTangentZ(Index); 	float Twist = ReadTwist(); 	float Start = ReadStart(); 	float End = ReadEnd();  	float Time = sin(ReadTime()); 	float posz = min(max(Position.z, Start), End) / (End-Start); 	float theta = posz * Twist * 0.0174533 * Time; 	float sint = sin(theta); 	float cost = cos(theta);  	float3 TwistPosition; 	TwistPosition.x = Position.x * cost - Position.y * sint; 	TwistPosition.y = Position.x * sint + Position.y * cost; 	TwistPosition.z = Position.z;  	float3 TangentX; 	TangentX.x = LocalTangentX.xyz.x * cost - LocalTangentX.xyz.y * sint; 	TangentX.y = LocalTangentX.xyz.x * sint + LocalTangentX.xyz.y * cost; 	TangentX.z = LocalTangentX.xyz.z;  	float3 TangentZ; 	TangentZ.x = LocalTangentZ.xyz.x * cost - LocalTangentZ.xyz.y * sint; 	TangentZ.y = LocalTangentZ.xyz.x * sint + LocalTangentZ.xyz.y * cost; 	TangentZ.z = LocalTangentZ.xyz.z;  	float4 TwistTangentX = float4(normalize(TangentX), LocalTangentX.w); 	float4 TwistTangentZ = float4(normalize(TangentZ), LocalTangentZ.w);  	WriteOutPosition(Index, TwistPosition); 	WriteOutTangentX(Index, TwistTangentX); 	WriteOutTangentZ(Index, TwistTangentZ);`

Copy full snippet
```
if (Index > ReadNumThreads().x) return; float3 Position = ReadPosition(Index); float4 LocalTangentX = ReadTangentX(Index); float4 LocalTangentZ = ReadTangentZ(Index); float Twist = ReadTwist(); float Start = ReadStart(); float End = ReadEnd(); float Time = sin(ReadTime()); float posz = min(max(Position.z, Start), End) / (End-Start); float theta = posz \* Twist \* 0.0174533 \* Time; float sint = sin(theta); float cost = cos(theta); float3 TwistPosition; TwistPosition.x = Position.x \* cost - Position.y \* sint; TwistPosition.y = Position.x \* sint + Position.y \* cost; TwistPosition.z = Position.z; float3 TangentX; TangentX.x = LocalTangentX.xyz.x \* cost - LocalTangentX.xyz.y \* sint; TangentX.y = LocalTangentX.xyz.x \* sint + LocalTangentX.xyz.y \* cost; TangentX.z = LocalTangentX.xyz.z; float3 TangentZ; TangentZ.x = LocalTangentZ.xyz.x \* cost - LocalTangentZ.xyz.y \* sint; TangentZ.y = LocalTangentZ.xyz.x \* sint + LocalTangentZ.xyz.y \* cost; TangentZ.z = LocalTangentZ.xyz.z; float4 TwistTangentX = float4(normalize(TangentX), LocalTangentX.w); float4 TwistTangentZ = float4(normalize(TangentZ), LocalTangentZ.w); WriteOutPosition(Index, TwistPosition); WriteOutTangentX(Index, TwistTangentX); WriteOutTangentZ(Index, TwistTangentZ);

After adding the custom HLSL program to calculate the mesh deformation, connect the **read** and **write** nodes to the associated **input** and **output** pins on the **Custom Compute Kernel** node.

![connect the read and write nodes to the custom compute kernel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f200de07-93b4-4169-87bb-72cd243577b0/connections.png)

Finally, **drag-and-drop** three **Float Constant** nodes from the **Pallet** panel to the **Update Graph** to set the **Twist**, **Start,** and **End** values for the custom function. Connect one **Float Constant** node to each of the three available **input pins** on the **Custom Compute Kernel** node. Set the **Float Constant** node connected to the **Twist** **input pin** to a value of **180.0**, the **Float Constant** node connected to the **Start input pin** to a value of **0**, and the **Float Constant** node connected to the **End input pin** to a value of **100.0**.

![add three float constants to the graph and connect them to the custom compute kernels twist start and end inputs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc2c6b33-9045-4b02-964d-44e5fbf7dd6c/addconstants.png)

Alter these values to see how the function's inputs are modified, to dynamically change the deformation. Instead of constant values, the function is driven using [Deformer Graph variables](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#variables), [Resources](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#resources) or [animation curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine).

**Save** and **Compile** the asset to see the mesh now twisting in the **Preview Viewport** panel as well as in the level in real time.

![skeletal mesh will now twist at runtime](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b4a4a47-3d22-4dbe-96ae-0912e176089c/dgdemo.gif)

You can add the custom Deformer Graph to any character in a level, by selecting the mesh, and navigating to the **Deformers** section of its **Details** panel. You can assign the custom Deformer Graph to the character by **enabling** the **Deformer Graph** property, and selecting the custom graph from the drop down menu.

For more information about Deformer Graphs or the [Deformer Graph Editor](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine#deformergrapheditor) and [Blueprint nodes](/documentation/en-us/unreal-engine/how-to-create-a-custom-deformer-graph-in-unreal-engine#palettecomponentnodes), refer to the [Deformer Graph](/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine) documentation.

This and other application examples of mesh deformations controlled by custom Deformer Graph logic are present in the [Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine).

For more information about **HLSL** (**High-Level Shader Language**)programming used to drive the Deformer Graph's Custom Compute Kernels, refer to the [Microsoft High-Level Shader Language reference documentation and programming guide](https://docs.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl)

## Graph Reference

Here you can use the image slider to reference the full Deformer Graph, Custom Compute Kernel Details panel, and Shader Text Editor panel, used in the workflow example.

  ![final deformer graph reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c24fe6a-88db-46dd-bdef-8ed362a8cca9/graphref.png) ![final kernel details panel reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0e1904d-4c6d-401f-b822-b4888c508153/kernelref.png) ![final shader text editor reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/41b0d20d-a577-4f30-b9e1-25a4474eeddc/shadertextref.png)

**Reference Images**