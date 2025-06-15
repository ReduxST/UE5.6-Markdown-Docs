# Using PCG with GPU Processing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-with-gpu-processing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-with-gpu-processing-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:30

---

The **Procedural Content Generation Framework (PCG)** is a toolset for creating your own procedural content and tools inside Unreal Engine. **PCG GPU Processing** provides technical artists and designers with the ability to send many PCG processing tasks directly to the GPU to free up resources on the CPU. 

PCG GPU processing is efficient for a variety of tasks, such as point processing, [Runtime Generation](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-generation-modes-in-unreal-engine#using-runtime-generation), and [static mesh spawning](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-framework-node-reference-in-unreal-engine#spawner).

GPU processing is currently available on a [small number of nodes](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-with-gpu-processing-in-unreal-engine#supported-nodes), including the Copy Points and Static Mesh Spawner, as well as a new Custom HLSL node has been added which can be scripted using the [HLSL language](https://learn.microsoft.com/en-us/windows/win32/direct3dhlsl/dx-graphics-hlsl). 

Additional nodes that support GPU Execution will be available in the future.

Nodes that are set to target the GPU are labeled with **GPU** in the PCG Graph. A subset of connected GPU nodes executes together on the GPU efficiently and is called a **Compute Graph**.

[![PCG GPU Compute Graph example](https://dev.epicgames.com/community/api/documentation/image/321d4c5d-5a64-471e-ab6d-5cd3a4f711ac?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/321d4c5d-5a64-471e-ab6d-5cd3a4f711ac?resizing_type=fit)

|  |  |
| --- | --- |
| 
Number

 | 

Description

 |
| 

1

 | 

Transferring data between the CPU and GPU. These points represent a performance cost.

 |
| 

2

 | 

GPU execution nodes that are executed together.

 |

Targeting the GPU may give performance increases over CPU execution when there are enough points in the data to fully utilize the GPU hardware. Additionally, a sequence of connected GPU nodes with a GPU-enabled Static Mesh Spawner node provides a fast path for [static mesh spawning](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-framework-node-reference-in-unreal-engine#spawner).

It is important to note that there is a CPU cost for transferring data between the CPU and GPU, and for preparing a compute graph for execution. Therefore the optimal way to use the GPU execution feature is to group GPU-enabled nodes together, and minimize how much data is transferred into and out of each compute graph.

## Supported Nodes

### Custom HLSL Node

The Custom HLSL node can be used for arbitrary data processing tasks to be scripted via user created HLSL source code. The source code is injected into a compute shader and executed over data elements in parallel on GPU hardware.

This node provides low level access to GPU hardware and is available for advanced users.

|  |  |
| --- | --- |
| 
**Option**  


 | 

**Description**

 |
| 

**Kernel Type**

 | 

Selects a preset for the behavior of the node. The available options are documented in the [Custom HLSL Node Kernel Types](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-with-gpu-processing-in-unreal-engine#custom-hlsl-node-kernel-types) section below.

 |
| 

**Input Pins**

 | 

Defines the data that is taken as input. Opening the rollout provides the following options:

-   **Label:** Name displayed on the input pin.
    
-   **Usage:** Not relevant for the Custom HLSL node.
    
-   **Allowed Types:** Defines the data type that this input will accept.
    
-   **Allow Multiple Data:** Provides for multiple data on the same pin, if checked. Used with only certain data types.
    
-   **Allow Multiple Connections:** Currently disabled for all GPU node input pins.
    
-   **Pin Status:** Not relevant for Custom HLSL node.
    
-   **Tooltip:** Defines the tooltip displayed to users.
    

 |
| 

**Output Pins**

 | 

Defines the data that is output from the node. Contains the same options as the Input Pins, with additional options for setting up the output data. These are covered in the  section [Pin Setup](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-with-gpu-processing-in-unreal-engine#pin-setup) below.

 |
| 

**Kernel Source Override**

 | 

Used to replace your **Shader Source** field with a UComputeSource asset.

 |
| 

**Additional Sources**

 | 

Allows referencing additional UComputeSource assets to be bundled with your Custom HLSL node.

 |
| 

**Mute Unwritten Pin Data Errors**

 | 

Mutes warnings on output pins with potentially uninitialized data.

 |
| 

**Seed**

 | 

Defines the seed value used to drive random generation.

 |
| 

**Dump Cooked HLSL**

 | 

Prints the cooked HLSL data into the log when it is generated for debugging.

 |
| 

**Dump Data Descriptions**

 | 

Prints the data descriptions of the input and output data into the log when it is generated for debugging.

 |
| 

**Print Shader Debug Values**

 | 

Provides simple debug logging from shader code. Covered in the  [Debugging Custom HLSL](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-with-gpu-processing-in-unreal-engine#debugging-custom-hlsl) section below.

 |

### HLSL Source Editor

The HLSL Source Editor provides quick authoring of Custom HLSL nodes. It can be found in the PCG Graph editor under **Window->HLSL Source Editor**, or by selecting a Custom HLSL node and clicking the **Open Source Editor** button in the node settings.

The HLSL Source Editor has three parts:

-   **Declarations panel**
    
-   **Shader Functions**
    
-   **Shader Source**
    

[![PCG HLSL Source Editor](https://dev.epicgames.com/community/api/documentation/image/c562104a-cde0-4525-a943-d1385a390e32?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c562104a-cde0-4525-a943-d1385a390e32?resizing_type=fit)

The **Declarations panel** serves as an API reference for writing your shader code. The declarations are automatically generated from the Custom HLSL node settings, such as the kernel type and input/output pin settings.

The **Shader Functions** field allows authors to create reusable functions to call in their **Shader Source**.

The **Shader Source** field is where you implement the main entry point for your kernel implementation.

### Custom HLSL Node Kernel Types

The **Kernel Type** defines a preset for the behavior of the node.

#### Point Processor

The **Point Processor** kernel type is ideal for modifying points. It requires the primary input and output pin to be of type Point, and executes the HLSL code once for each point. Data sent by the primary output pin has the same layout as the primary input pin, meaning the number of data and number of elements are identical.

All points in the primary output are automatically initialized from the primary input so it is only necessary to set output attributes that should be changed.

You can also use the Point Processor to create additional input and output pins which you must configure manually to set the desired data type and data/element counts.

[![Custom HLSL node Point Processor](https://dev.epicgames.com/community/api/documentation/image/07f74bf6-0987-40eb-a181-eaea1fea5837?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/07f74bf6-0987-40eb-a181-eaea1fea5837?resizing_type=fit)

#### Point Generator

The Point Generator kernel type is ideal for creating and populating a set of points. It requires the primary output pin to be of type Point, and executes the HLSL code once for each point. 

This kernel type has the following additional options:

|  |  |
| --- | --- |
| 
**Option**  


 | 

**Description**

 |
| 

**Point Count**  


 | 

Determines the number of points that are generated. The shader code is executed on each generated point.

 |

[![Custom HLSL node Point Generator](https://dev.epicgames.com/community/api/documentation/image/49852a4a-7ac7-43f0-a610-8f58f9e69ed2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/49852a4a-7ac7-43f0-a610-8f58f9e69ed2?resizing_type=fit)

Similar to the Point Processor, you can use the Point Generator to create additional input and output pins which you must configure manually to set the desired data type and data or element counts.

#### Custom

The **Custom** kernel type exposes fine-grained control over the execution for advanced use cases. Unlike the other two kernel types, there are no settings enforced on the input or output pins, as the node does not assume any specific relationship between the input and output. The output data must be configured in the output pin settings which are documented below. The number of threads that should execute the shader code must also be configured.

[![Custom HLSL node Custom](https://dev.epicgames.com/community/api/documentation/image/77d4f609-fb13-4420-b379-a01f1ee530d4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/77d4f609-fb13-4420-b379-a01f1ee530d4?resizing_type=fit)

This kernel type has the following additional options:

|  |  |
| --- | --- |
| 
**Option**

 | 

**Description**

 |
| 

**Dispatch Thread Count**

 | 

Determines the number of threads the shader code uses to execute. The following modes are available:

-   **From First Output Pin:** Dispatches one thread per data element (e.g. per point) on the first output pin. Can have a user-defined thread multiplier.
    
-   **Fixed Thread Count:** Defines a specific thread count.
    
-   **From Product of Input Pins:** Dispatches a thread per data element coming from one or more input pins. Can have a user-defined thread multiplier.
    

 |

### Pin Setup

Any pins not driven by the  **Kernel Type** should be configured manually.

For output pins, it is required to explicitly describe the data size and layout, which can be set under the **GPU Properties** dropdown in the output pin settings.

|  |  |
| --- | --- |
| 
**Initialization Mode**

 | 

Describes how the output data for this pin will be initialized. The menu contains the following modes:

-   **From First Output Pin:** Dispatches one thread per element on the first output pin. Can have a user-defined thread multiplier.
    
-   **Fixed Thread Count:** Defines a specific thread count.
    
-   **From Product of Input Pins:** Dispatches a thread per data element coming from one or more input pins. Can have a user-defined thread multiplier.
    

 |
| 

**Pins to Initialize From**

 | 

Defines the input pins to initialize this pin's data from.

 |
| 

**Data Count Mode**

 | 

Defines the number of data objects. The menu contains the following modes:

-   **From Input Data:** Acquire data counts from the **Pins to Initialize From**.
    
-   **Fixed:** Specifies a number of data to output.
    

 |
| 

**Data Multiplicity**

 | 

Combines data counts if there are multiple Pins to Initialize From.

Available modes:

-   **Pairwise:** A data item is produced for each pair/tuple/etc of input data items across the input pins. Requires all pins to have the same number of data.
    
-   **Cartesian:** If there are two input pins with N and M data items respectively, the output will have NxM data items.
    

 |
| 

**Element Count Mode**

 | 

Defines the number of elements. The menu contains the following modes:

-   **From Input Data:** Acquire element counts from the **Pins to Initialize From**.
    
-   **Fixed:** Specify a number of elements to output.
    

 |
| 

**Element Multiplicity**

 | 

Combines element counts if there are multiple Pins to Initialize From.

Available modes:

-   **Product:** Element count will be the product of the elements in each pair/tuple/etc. of input data.
    
-   **Sum:** Element count will be the sum of the elements in each pair/tuple/etc. of input data.
    

 |
| 

**Attribute Inheritance Mode**

 | 

Defines how to inherit attribute names, types, and values.The menu contains the following modes:

-   **None:** No attributes inherited from **Pins to Initialize From**.
    
-   **Copy Attribute Setup:** Takes attribute names and types from **Pins to Initialize From**. Pins declared first will take priority during conflicts. Does not copy values.
    

 |
| 

**Attributes to Create**

 | 

Defines a list of new attributes to create on the output data.

 |

### Debugging Custom HLSL

The Debug Display (default hotkey ‘D’) and Inspection (default hotkey ‘A’) features work for GPU nodes and enable inspection of the data flowing through the GPU nodes.

It is also possible to debug custom shader code by toggling the **Print Shader Debug Values** option on the Custom HLSL node. This exposes a new function `WriteDebugValue`, which can be used to write float values to a buffer which gets logged during execution. The buffer size is controlled by the **Debug Buffer Size** property.

### Examples

#### Example 1: Height Offset Using a Sine Wave

In the example below, a Point Processor is used to apply a sine wave-based height offset to a set of points.

The following code is added to the Shader Source field of HLSL Source Editor window:

C

```code
`// Get the position of the incoming point from input pin ‘In’. float3 Position = In_GetPosition(In_DataIndex, ElementIndex);  // Compute a sine wave with amplitude 500cm and wavelength 400cm. const float Wave = 500.0f * sin(Position.x / 400.0f);  // Add the wave to the Z coordinate of the point’s position. Position.z += Wave;  // Write the offset position to the output point on pin ‘Out’.`

```

Expand codeCopy full snippet(11 lines long)

[![Height offset using a sine wave](https://dev.epicgames.com/community/api/documentation/image/e731392e-7a32-41a9-84f7-25f172a48a16?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e731392e-7a32-41a9-84f7-25f172a48a16?resizing_type=fit)

[![Source editor code for height offset using a sine wave](https://dev.epicgames.com/community/api/documentation/image/16872fd1-f9c1-493c-b5ef-e9ee0d1ecd67?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/16872fd1-f9c1-493c-b5ef-e9ee0d1ecd67?resizing_type=fit)

#### Example 2: Creating an Attribute

In the example below, a Point Generator is used to create a grid of points, and uses an attribute set to control the height of the grid.

The following code is added to the **Shader Source** field of **HLSL Source Editor** window:

C

```code
`// Get PCG Component bounds. const float3 BoundsMin = GetComponentBoundsMin(); const float3 BoundsMax = GetComponentBoundsMax();  // Get the current point position in a 2D grid, based on the  // number of points and the component bounds. float3 Position = CreateGrid2D(ElementIndex, NumPoints, BoundsMin, BoundsMax); Position.z += InHeight_GetFloat(0, 0, 'GridHeight');  // Set the point's position.`

```

Expand codeCopy full snippet(11 lines long)

Attributes can be accessed in shader code using the provided Get and Set functions, and querying the attribute by name by wrapping it in apostrophes. For example, ‘GridHeight’.

[![Creating an attribute](https://dev.epicgames.com/community/api/documentation/image/d5124122-aca9-4ac9-b367-6236ec7f08a4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d5124122-aca9-4ac9-b367-6236ec7f08a4?resizing_type=fit)

[![Creating an attribute source editor code](https://dev.epicgames.com/community/api/documentation/image/f2431c05-83d8-4f90-8084-65fb7fb7e6ec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f2431c05-83d8-4f90-8084-65fb7fb7e6ec?resizing_type=fit)

#### Example 3: Spawning Random Meshes on a Landscape

The Custom HLSL node is also capable of running a sequence of operations. 

In the example below, the shader code performs the following operations:

-   Creates several points on a landscape.
    
-   Applies a random position adjustment to each point.
    
-   Sets the point position
    
-   Writes a random seed value to each point
    
-   Reads an attribute set containing a list of static meshes and assigns a random to each point.
    

Downstream of the Custom HLSL node is a Static Mesh Spawner with GPU execution enabled and the mesh attribute set to 'MeshPath'.

On the GPU attributes of type String, Name, Soft Object Path, Soft Class Path become StringKeys, which uniquely identify each string.

The following code is added to the Shader Source field of HLSL Source window:

C

```code
`// Get generation volume bounds const float3 BoundsMin = GetComponentBoundsMin(); const float3 BoundsMax = GetComponentBoundsMax();  // Compute a position on a 2D grid within the volume. float3 Pos = CreateGrid2D(ElementIndex, NumPoints, BoundsMin, BoundsMax);  // Initialize the random seed from the position. uint Seed = ComputeSeedFromPosition(Pos);`


```

Expand codeCopy full snippet(30 lines long)

[![Spawning random meshes on a landscape](https://dev.epicgames.com/community/api/documentation/image/641b184a-4183-45ac-acbb-690d8377afc8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/641b184a-4183-45ac-acbb-690d8377afc8?resizing_type=fit)

[![Spawning random meshes on a landscape source editor code](https://dev.epicgames.com/community/api/documentation/image/0c7e69d1-2d79-4ce9-b410-0de11b5b3d48?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0c7e69d1-2d79-4ce9-b410-0de11b5b3d48?resizing_type=fit)

## Static Mesh Spawner Node

You can cause the Static Mesh Spawner node to execute on the GPU by toggling the **Execute on GPU** option in the node settings.

### Procedural Instancing

When the Static Mesh Spawner is set to run on the GPU, it sets up mesh instances entirely on the GPU, saving CPU time and memory. This uses the **Procedurally Instanced Static Mesh Component**. This can be a very efficient path for spawning meshes, but is experimental and comes with the following tradeoffs:

-   Instances are not persisted or saved in any way. They exist only at runtime in GPU memory.
    
    -   Therefore the primary use case is **Runtime Generation**.
        
    -   Static Baked Lighting and HLOD require persisted instance information and are also not supported at this time.
        
-   Several features currently require CPU access to instance data and are not supported:
    
    -   Collisions / physics
        
    -   Navigation
        
    -   Ray tracing
        
    -   Affecting Distance Field lighting
        

The GPU implementation is Experimental and not all Static Mesh Spawner features are supported.

### Mesh Selector Types

The following mesh selectors are supported when executing on the GPU, and due to how instances are allocated, there are slight differences in behavior.

-   Weighted (**PCGMeshSelectorWeighted**)
    
    -   Similar to the CPU implementation, this mode uses the input point random seeds and the configured selection weights to randomly select the mesh for each instance. These meshes must be set on the node rather than driven by attribute.
        
    -   The system uses weights to determine how many instances should be allocated for each mesh. An over allocation is made based on a heuristic to minimize the chance of saturating the allocation for one or more primitives and losing instances.
        
    -   This mode relies on the Seed attribute on points being well-initialized, for example using the provided shader function \`ComputeSeedFromPosition()\`. If all point seeds are set to the same value, the same selection will be made for all points and the estimated allocation may be exceeded which will result in instances missing from the result.
        
-   By-Attribute (**PCGMeshSelectorByAttribute**)
    
-   Other mesh selector types (for example, **PCGMeshSelectorWeightedByCategory**) are not currently supported when executing on GPU.
    

The final allocated instance counts can be inspected by selecting the generated **procedurally instanced static mesh components** and checking the **Num Instances** property.

### Instance Data Packing

Similar to CPU execution, attributes can be packed into instance data.

The system needs to know prior to GPU execution how many attributes will be packed, and therefore only the by-attribute packer type (**PCGInstanceDataPackerByAttribute**) is supported.

## Other Nodes

The following nodes currently support GPU execution:

-   Copy Points
    
-   Attribute Partition
    
    -   Currently only supports partitioning on attributes of type String, Soft Object Path or Soft Class Path.
        
-   Normal To Density
    
-   Data Count
    
-   Static Mesh Spawner
    
-   Custom HLSL
    
    -   CPU execution not supported.
        

## Compute Sources

**Compute Source** assets make sharing source code easier and reduces code duplication between nodes.

The assets support in-line editing of HLSL source code with syntax highlighting and PCG specific syntax like data labels and attribute names.

Compute Source assets can also reference other Compute Source assets by using the **Additional Sources** property which creates dependency hierarchies between multiple compute sources.

[![Compute source assets](https://dev.epicgames.com/community/api/documentation/image/b6f8e3c4-8a73-4f78-9d9d-a7c6c7d59726?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b6f8e3c4-8a73-4f78-9d9d-a7c6c7d59726?resizing_type=fit)

## Data Labels

Data labels can be used to reference data by label rather than index in Custom HLSL source. Data labels are communicated on data through tags with the prefix PCG\_DATA\_LABEL.

Some nodes automatically label their output data, including:

-   **Get Texture Data**
    
-   **Get Virtual Texture Data**
    
-   **Generate Grass Maps**
    

[![Data labels 1](https://dev.epicgames.com/community/api/documentation/image/2dc6e999-9cf6-4322-87ba-b59e77606d74?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2dc6e999-9cf6-4322-87ba-b59e77606d74?resizing_type=fit)

[![Data labels 2](https://dev.epicgames.com/community/api/documentation/image/3ac8aebd-5908-4d48-ada3-22b413d14524?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3ac8aebd-5908-4d48-ada3-22b413d14524?resizing_type=fit)

## Generating Grass Maps

PCG supports sampling Landscape Grass Layers from a specified Landscape material to support runtime procedural generation workflows.

1.  Set up your Landscape material with a Landscape Grass Output node. For more information on setting up a Landscape material, see [Landscape Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-materials-in-unreal-engine).
    
    [![Landscape material with a landscape grass output node](https://dev.epicgames.com/community/api/documentation/image/f8f534d0-d0a8-4f23-8b90-71dbfadc419d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f8f534d0-d0a8-4f23-8b90-71dbfadc419d?resizing_type=fit)
    
2.  Connect your landscape data into a **Generate Grass Maps** node. Select your desired grass types directly using override or through exclusion.
    
3.  Sample your grass map textures. You can sample by index or by the automatically assigned data labels. The following code is added to the **Shader Source** field of **HLSL Source Editor** window:
    

C++

```code
`float3 Min = GetComponentBoundsMin(); float3 Max = GetComponentBoundsMax();  float3 Position = CreateGrid2D(ElementIndex, NumPoints, Min, Max); uint Seed = ComputeSeedFromPosition(Position); Position.xy += (float2(FRand(Seed), FRand(Seed)) - 0.5) * 45.0; Position.z = LS_GetHeight(Position);  float Density = FRand(Seed); float Thresh = GrassMaps_SampleWorldPos('GSM_PCGGrass1', Position.xy).x;`

```

Expand codeCopy full snippet(21 lines long)

[![Generate grass maps node](https://dev.epicgames.com/community/api/documentation/image/24e7bf9e-cee7-47fb-9741-8a3d6ddb407b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/24e7bf9e-cee7-47fb-9741-8a3d6ddb407b?resizing_type=fit)

If you plan to sample your grass map textures only on the GPU, you can toggle Skip Readback to CPU in the PCG Graph for significant performance improvements.

[![Generate grass maps - skip Readback to CPU](https://dev.epicgames.com/community/api/documentation/image/1bb59e9c-1bfb-4a11-8bd2-7a2e12abd8f4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1bb59e9c-1bfb-4a11-8bd2-7a2e12abd8f4?resizing_type=fit)

Painted landscape layers:

[![Painted landscape layers](https://dev.epicgames.com/community/api/documentation/image/ce301987-ee91-4a4c-a6b7-e69aa799c743?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ce301987-ee91-4a4c-a6b7-e69aa799c743?resizing_type=fit)

Resulting generation:

[![Grass map generation](https://dev.epicgames.com/community/api/documentation/image/8cc507c3-c029-4916-a92c-f9955b79ac16?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8cc507c3-c029-4916-a92c-f9955b79ac16?resizing_type=fit)

## Using Virtual Textures in PCG

PCG supports using virtual textures as part of your procedural content generation workflow. 

### Virtual texture sampling

Virtual textures can be sampled from Landscape data to improve the performance of height sampling.

#### Example 1: Landscape Data

To sample Landscape Data using virtual textures, make sure **Sample Virtual Textures** is toggled on in the **Get Landscape Data** node settings. This gives the ability to the Landscape Data node to use any virtual textures provided through the corresponding Landscape Material.

This only affects GPU sampling.

C

```code
`// Get Position and Height float3 Position = CreateGrid2D(ElementIndex, NumPoints, GetComponentBoundsMin(), GetComponentBoundsMax()); Position.z = A_GetHeight(Position);  // Get Normal and Orientation const float3 Normal = A_GetNormal(Position); const FQuat Orientation = QuatFromNormal(Normal);  // Get Base Color const float3 BaseColor = A_GetBaseColor(Position);`

```

Expand codeCopy full snippet(15 lines long)

[![Landscape data generated using virtual textures](https://dev.epicgames.com/community/api/documentation/image/ed106620-00aa-48d7-8295-0a3b34c4d409?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ed106620-00aa-48d7-8295-0a3b34c4d409?resizing_type=fit)

#### Example 2: Virtual Texture Data

To sample a virtual texture, query the world for runtime virtual texture components. Each one will produce a virtual texture data, tagged with a data label for the runtime virtual texture asset.

C++

```code
`float3 Position = CreateGrid2D(ElementIndex, NumPoints, GetComponentBoundsMin(), GetComponentBoundsMax());  // Sample virtual textures bool bInsideVolume; float3 BaseColor; float Specular; float Roughness; float WorldHeight; float3 Normal; float Displacement;`

```

Expand codeCopy full snippet(19 lines long)

[![Virtual texture data](https://dev.epicgames.com/community/api/documentation/image/5034a9ce-e33c-404b-a7ef-5d2b25bf6097?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5034a9ce-e33c-404b-a7ef-5d2b25bf6097?resizing_type=fit)

## Virtual texture priming

It’s important to make sure the virtual textures are primed before generation, otherwise your sampling results may be inaccurate.

To request virtual texture priming, add a graph parameter of type FPCGVirtualTexturePrimingInfo to your PCG Graph. This exposes the following options:

|  |  |
| --- | --- |
| 
**Virtual Texture**

 | 

Defines the virtual texture to be primed.

 |
| 

**Grid**

 | 

Defines the largest grid on which the virtual texture is sampled in the graph. The virtual textures are primed for the generation radius dictated by this grid.

 |
| 

**World Texel Size**

 | 

Defines the desired size of a texel in the primed virtual texture. This will determine what mip map level should be primed.

 |

You can control virtual texture priming using the console command pcg.VirtualTexturePriming.Enable. You can debug this feature using the command pcg.VirtualTexturePriming.DebugDrawTexturePrimingBounds.

[![VIrtual texture priming](https://dev.epicgames.com/community/api/documentation/image/763fe6dc-f82c-4c11-ad56-27c56848c5bf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/763fe6dc-f82c-4c11-ad56-27c56848c5bf?resizing_type=fit)