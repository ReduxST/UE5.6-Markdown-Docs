# Render Dependency Graph

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/render-dependency-graph-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/render-dependency-graph-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:42

---

The **Render Dependency Graph**, also called Render Graph or **RDG**, is an immediate-mode application programming interface (API) which records render commands into a graph data structure to be compiled and executed. RDG simplifies high level rendering code by automating error-prone operations, and traverses the graph to optimize memory usage and parallelize render passes on the CPU and GPU.

Render Dependency Graph includes the following features :

-   Scheduling of asynchronous compute fences
-   Allocation of transient resources with optimal lifetimes and memory aliasing
-   Transitioning of sub-resources using split-barriers to hide latency and improve overlap on the GPU
-   Parallel command list recording
-   Culling of unused resources and passes in the graph
-   Validation of API usage and resource dependencies
-   Visualization of the graph structure and memory lifetimes in RDG Insights

The Render Graph API has been converted for both deferred and mobile renderers along with associated plugins. All high-level rendering code should be written using RDG, especially if any of the advanced features listed above are required.

## RDG Programming Guide

For those writing low-level rendering features in C++ with some familiarity of shaders and the render hardware interface (RHI), this guide demonstrates use of the API through examples while explaining underlying concepts.

### Shader Parameter Structs

RDG expresses graph dependencies through extensions to the shader parameters struct system.

Consider the following shader parameters declared in an HLSL source file.

**Shader Inputs in an HLSL Source File:**

```
	`float2 ViewportSize; 	float4 Hello; 	float World; 	float3 FooBarArray[16];  	Texture2D BlueNoiseTexture; 	SamplerState BlueNoiseSampler;  	Texture2D SceneColorTexture; 	SamplerState SceneColorSampler;  	RWTexture2D<float4> SceneColorOutput;`
Copy full snippet
```
float2 ViewportSize; float4 Hello; float World; float3 FooBarArray\[16\]; Texture2D BlueNoiseTexture; SamplerState BlueNoiseSampler; Texture2D SceneColorTexture; SamplerState SceneColorSampler; RWTexture2D<float4> SceneColorOutput;

These shader parameters can also be represented by a flat C++ data structure.

**An ideal C++ Equivalent:**

```
	`struct FMyShaderParameters 	{ 		FVector2D ViewportSize; 		FVector4 Hello; 		float World; 		FVector FooBarArray[16];  		FRHITexture*    	BlueNoiseTexture = nullptr; 		FRHISamplerState*   BlueNoiseSampler = nullptr;  		FRHITexture*    	SceneColorTexture = nullptr; 		FRHISamplerState*   SceneColorSampler = nullptr;  		FRHIUnorderedAccessView* SceneColorOutput = nullptr; 	};`
Copy full snippet
```
struct FMyShaderParameters { FVector2D ViewportSize; FVector4 Hello; float World; FVector FooBarArray\[16\]; FRHITexture\* BlueNoiseTexture = nullptr; FRHISamplerState\* BlueNoiseSampler = nullptr; FRHITexture\* SceneColorTexture = nullptr; FRHISamplerState\* SceneColorSampler = nullptr; FRHIUnorderedAccessView\* SceneColorOutput = nullptr; };

The shader parameters struct system employs a set of declaration macros to achieve this.

**Shader Parameter Structs:**

```
	`BEGIN_SHADER_PARAMETER_STRUCT(FMyShaderParameters, /** MODULE_API_TAG */) 		SHADER_PARAMETER(FVector2D, ViewportSize) 		SHADER_PARAMETER(FVector4, Hello) 		SHADER_PARAMETER(float, World) 		SHADER_PARAMETER_ARRAY(FVector, FooBarArray, [16])  		SHADER_PARAMETER_TEXTURE(Texture2D, BlueNoiseTexture) 		SHADER_PARAMETER_SAMPLER(SamplerState, BlueNoiseSampler)  		SHADER_PARAMETER_TEXTURE(Texture2D, SceneColorTexture) 		SHADER_PARAMETER_SAMPLER(SamplerState, SceneColorSampler)  		SHADER_PARAMETER_UAV(RWTexture2D, SceneColorOutput) 	END_SHADER_PARAMETER_STRUCT()`
Copy full snippet
```
BEGIN\_SHADER\_PARAMETER\_STRUCT(FMyShaderParameters, /\*\* MODULE\_API\_TAG \*/) SHADER\_PARAMETER(FVector2D, ViewportSize) SHADER\_PARAMETER(FVector4, Hello) SHADER\_PARAMETER(float, World) SHADER\_PARAMETER\_ARRAY(FVector, FooBarArray, \[16\]) SHADER\_PARAMETER\_TEXTURE(Texture2D, BlueNoiseTexture) SHADER\_PARAMETER\_SAMPLER(SamplerState, BlueNoiseSampler) SHADER\_PARAMETER\_TEXTURE(Texture2D, SceneColorTexture) SHADER\_PARAMETER\_SAMPLER(SamplerState, SceneColorSampler) SHADER\_PARAMETER\_UAV(RWTexture2D, SceneColorOutput) END\_SHADER\_PARAMETER\_STRUCT()

These macros generate an equivalent flat C++ data structure along with compile-time reflection metadata, which is accessible as a static member of the struct.

**Compile-Time Reflection Metadata:**

```
	`const FShaderParametersMetadata* ParameterMetadata = FMyShaderParameters::FTypeInfo::GetStructMetadata();`
Copy full snippet
```
const FShaderParametersMetadata\* ParameterMetadata = FMyShaderParameters::FTypeInfo::GetStructMetadata();

This metadata enables runtime traversal of the struct, which is necessary to dynamically bind parameters to the RHI. Information available for each member include the **name**, **C++ type**, **HLSL type**, and **byte offset**.

Refer to `FShaderParametersMetadata::FMember` for more information. RDG relies on this metadata to traverse **pass parameters** (later in this page).

#### Shader Bindings

A shader parameter struct is paired with an `FShader` to generate the bindings necessary to submit to an RHI command list.

You would do this by declaring the parameter struct as an `FParameters` type in your `FShader` derived class.

It can be done as either an inline definition or through a using / typedef directive. Then, use the `SHADER_USE_PARAMETER_STRUCT` macro to generate a constructor for the class which will register the bindings.

**First Shader Class:**

```
	`class FMyShaderCS : public FGlobalShader 	{ 		DECLARE_GLOBAL_SHADER(FMyShaderCS);  		// Generates a constructor which will register FParameter bindings with this FShader instance. 		SHADER_USE_PARAMETER_STRUCT(FMyShaderCS, FGlobalShader);  		// Assign an FParameters type to the shader--either with an inline definition or using directive. 		using FParameters = FMyShaderParameters; 	};`
Copy full snippet
```
class FMyShaderCS : public FGlobalShader { DECLARE\_GLOBAL\_SHADER(FMyShaderCS); // Generates a constructor which will register FParameter bindings with this FShader instance. SHADER\_USE\_PARAMETER\_STRUCT(FMyShaderCS, FGlobalShader); // Assign an FParameters type to the shader--either with an inline definition or using directive. using FParameters = FMyShaderParameters; };

Binding shader parameters to an RHI command list is done by instantiating the struct, filling it with data, and calling the `SetShaderParameters` utility function.

**Assigning Parameters:**

```
	`TShaderMapRef<FMyShaderCS> ComputeShader(View.ShaderMap); 	RHICmdList.SetComputeShader(ComputeShader.GetComputeShader());  	FMyShaderCS::FParameters ShaderParameters;  	// Assign the parameters. 	ShaderParameters.ViewportSize = View.ViewRect.Size(); 	ShaderParameters.World = 1.0f; 	ShaderParameters.FooBarArray[4] = FVector(1.0f, 0.5f, 0.5f);  	// Submit the parameters. 	SetShaderParameters(RHICmdList, ComputeShader, ComputeShader.GetComputeShader(), Parameters);  	RHICmdList.DispatchComputeShader(GroupCount.X, GroupCount.Y, GroupCount.Z);`
Copy full snippet
```
TShaderMapRef<FMyShaderCS> ComputeShader(View.ShaderMap); RHICmdList.SetComputeShader(ComputeShader.GetComputeShader()); FMyShaderCS::FParameters ShaderParameters; // Assign the parameters. ShaderParameters.ViewportSize = View.ViewRect.Size(); ShaderParameters.World = 1.0f; ShaderParameters.FooBarArray\[4\] = FVector(1.0f, 0.5f, 0.5f); // Submit the parameters. SetShaderParameters(RHICmdList, ComputeShader, ComputeShader.GetComputeShader(), Parameters); RHICmdList.DispatchComputeShader(GroupCount.X, GroupCount.Y, GroupCount.Z);

### Uniform Buffers

**Uniform Buffers** group shader parameters into an RHI resource which is, itself, bound as a shader parameter. Each uniform buffer defines a global namespace in HLSL. Uniform buffers are declared using the `BEGIN_UNIFORM_BUFFER_STRUCT` and `END_UNIFORM_BUFFER_STRUCT` macros.

**Define Uniform Buffer:**

```
	`BEGIN_UNIFORM_BUFFER_STRUCT(FSceneTextureUniformParameters, RENDERER_API) 		SHADER_PARAMETER_TEXTURE(Texture2D, SceneColorTexture) 		SHADER_PARAMETER_SAMPLER(SamplerState, SceneColorTextureSampler) 		SHADER_PARAMETER_TEXTURE(Texture2D, SceneDepthTexture) 		SHADER_PARAMETER_SAMPLER(SamplerState, SceneDepthTextureSampler)  		// ... 	END_UNIFORM_BUFFER_STRUCT()`

Copy full snippet
```
BEGIN\_UNIFORM\_BUFFER\_STRUCT(FSceneTextureUniformParameters, RENDERER\_API) SHADER\_PARAMETER\_TEXTURE(Texture2D, SceneColorTexture) SHADER\_PARAMETER\_SAMPLER(SamplerState, SceneColorTextureSampler) SHADER\_PARAMETER\_TEXTURE(Texture2D, SceneDepthTexture) SHADER\_PARAMETER\_SAMPLER(SamplerState, SceneDepthTextureSampler) // ... END\_UNIFORM\_BUFFER\_STRUCT()

Use the `IMPLEMENT_UNIFORM_BUFFER_STRUCT` in a C++ source file to register the uniform buffer definition with the shader system and generate its HLSL definitions.

**Implement Uniform Buffer:**

```
	`IMPLEMENT_UNIFORM_BUFFER_STRUCT(FSceneTextureUniformParameters, "SceneTexturesStruct")`

Copy full snippet
```
IMPLEMENT\_UNIFORM\_BUFFER\_STRUCT(FSceneTextureUniformParameters, "SceneTexturesStruct")

Uniform buffer parameters are automatically generated by the shader compiled and accessed using `UniformBuffer.Member` syntax.

**Uniform Buffers in HLSL:**

```
	`// Generated file containing uniform buffer declarations. Automatically included by Common.ush. 	#include "/Engine/Generated/GeneratedUniformBuffers.ush"  	// Reference uniform buffer members like a struct. 	Texture2DSample(SceneTexturesStruct.SceneColorTexture, SceneTexturesStruct.SceneColorTextureSampler);`

Copy full snippet
```
// Generated file containing uniform buffer declarations. Automatically included by Common.ush. #include "/Engine/Generated/GeneratedUniformBuffers.ush" // Reference uniform buffer members like a struct. Texture2DSample(SceneTexturesStruct.SceneColorTexture, SceneTexturesStruct.SceneColorTextureSampler);

Now the `SHADER_PARAMTER_STRUCT_REF` macro can be used to include a uniform buffer as a parameter in the parent shader parameter struct.

**SHADER\_PARAMETER\_STRUCT\_REF:**

```
	`BEGIN_SHADER_PARAMETER_STRUCT(FParameters, ) 		// ...  		// Defines a refcounted TUniformBufferRef<FSceneTextureUniformParameters> instance. 		SHADER_PARAMETER_STRUCT_REF(FSceneTextureUniformParameters, SceneTextures) 	END_SHADER_PARAMETER_STRUCT()`
Copy full snippet
```
BEGIN\_SHADER\_PARAMETER\_STRUCT(FParameters, ) // ... // Defines a refcounted TUniformBufferRef<FSceneTextureUniformParameters> instance. SHADER\_PARAMETER\_STRUCT\_REF(FSceneTextureUniformParameters, SceneTextures) END\_SHADER\_PARAMETER\_STRUCT()

#### Static Bindings

Shader parameters are bound uniquely for each shader and each shader stage (for example, vertex and pixel) requires its own shader. Shaders are bound together as a Pipeline State Object (PSO) on an RHI command list using `Set{Graphics, Compute}PipelineState`.

Binding a pipeline state on the command list **invalidates all shader bindings**.

You are required to bind all shader parameters after setting the PSO. For example, consider the flow of commands for a typical set of draw calls sharing a PSO.

-   Set PSO A
-   For each draw call
    -   Set vertex shader parameters
    -   Set pixel shader parameters
    -   Draw
-   Set PSO B
-   For each draw call
    -   Set vertex shader parameters
    -   Set pixel shader parameters
    -   Draw

A problem with this approach is the Mesh Draw Commands in the renderer are cached and shared between multiple passes and views. It would be incredibly inefficient to generate a unique set of draw commands for each pass / view combination every frame. However, the Mesh Draw Command would also need to know the pass / view uniform buffer resources in order to properly bind them. To solve this, a **Static** binding model is used for Uniform Buffers.

When declared with static bindings, a uniform buffer is bound to a **static slot** directly to the RHI command list rather than to a **unique slot** for each individual shader. The command list pulls the binding directly from the static slot when the uniform buffer is requested by the shader. The binding now occurs at the **pass** frequency rather than the **PSO** frequency.

Consider the same example as above, but shader inputs are supplied from a Static Uniform Buffer instead:

-   Set Static Uniform Buffer
-   Set PSO A
-   For each draw call
    -   Draw
-   Set PSO B
-   For each draw call
    -   Draw

This model allows each draw call to inherit the shader bindings from the command list.

##### Defining Static Uniform Buffers

To define a uniform buffer with static binding, use the `IMPLEMENT_STATIC_UNIFORM_BUFFER_STRUCT` macro. An additional slot declaration is required. It is specified with the `IMPLEMENT_STATIC_UNIFORM_BUFFER_SLOT` macro.

Multiple static uniform buffers definitions can reference the same static slot, but only one of them may be bound at a time. It's best to reuse slots when possible to reduce the total number of them in the engine.

**Static Uniform Buffers:**

```
	`// Defines a unique static slot by name. 	IMPLEMENT_STATIC_UNIFORM_BUFFER_SLOT(SceneTextures);  	// Defines the SceneTexturesStruct uniform buffer with a static binding to the SceneTextures slot. 	IMPLEMENT_STATIC_UNIFORM_BUFFER_STRUCT(FSceneTextureUniformParameters, "SceneTexturesStruct", SceneTextures);  	// Defines the MobileSceneTextures uniform buffer with the same static slot. Only one is bound at a time. 	IMPLEMENT_STATIC_UNIFORM_BUFFER_STRUCT(FMobileSceneTextureUniformParameters, "MobileSceneTextures", SceneTextures);`
Copy full snippet
```
// Defines a unique static slot by name. IMPLEMENT\_STATIC\_UNIFORM\_BUFFER\_SLOT(SceneTextures); // Defines the SceneTexturesStruct uniform buffer with a static binding to the SceneTextures slot. IMPLEMENT\_STATIC\_UNIFORM\_BUFFER\_STRUCT(FSceneTextureUniformParameters, "SceneTexturesStruct", SceneTextures); // Defines the MobileSceneTextures uniform buffer with the same static slot. Only one is bound at a time. IMPLEMENT\_STATIC\_UNIFORM\_BUFFER\_STRUCT(FMobileSceneTextureUniformParameters, "MobileSceneTextures", SceneTextures);

Use the `RHICmdList.SetStaticUniformBuffers` method to bind static uniform buffers. **RDG automatically binds static uniform buffers to the command list prior to executing each pass**. Any static uniform buffers should be included in the pass parameter struct.

### Render Graph Builder

Render Dependency Graph is designed to be straightforward to use.

-   Instantiate an `FRDGBuilder` instance, create resources and add passes to set up the graph. Then, call `FRDGBuilder::Execute` to compile and execute the graph.
-   Create a texture with `FRDGBuilder::CreateTexture` or a buffer with `FRDGBuilder::CreateBuffer`.
    -   These methods only allocate descriptors. The underlying RHI resources are allocated later during execution.
-   Add a pass using the `FRDGBuilder::AddPass` function, specifying a pass parameter struct and execution lambda as arguments.
    -   Pass parameter structs extend shader parameter structs with parameters containing RDG resources.
        -   RDG uses these parameters to derive dependencies between passes in the graph and lifetimes for transient resources.
        -   Allocate pass parameters with `GraphBuilder::AllocParameters` and assign all relevant RDG resources used in the execution lambda.
    -   The pass execution lambda records work to submit to an RHI command list during graph execution.
        -   Use `FRHIComputeCommandList` for compute passes (the shared interface between asynchronous and graphics compute), or `FRHICommandList` for raster passes.
        -   Avoid using `FRHICommandListImmediate` unless strictly necessary, as it disqualifies the pass from executing in parallel.
        -   Ideally all pass lambdas are thread safe, but in reality a few passes still require creation or locking of RHI resources during execution, which must be done on the render thread. Use the immediate command list for these cases.

The example code snippet below is a starting example.

**Graph Builder:**

```
	`{ 		FRDGBuilder GraphBuilder(RHICmdList);  		FMyShaderCS::FParameters* PassParameters = GraphBuilder.AllocParameters<FMyShaderCS::FParameters>(); 		//... 		PassParameters->SceneColorTexture = SceneColor; 		PassParameters->SceneColorSampler = TStaticSamplerState<SF_Point, AM_Clamp, AM_Clamp>::GetRHI(); 		PassParameters->SceneColorOutput = GraphBuilder.CreateUAV(NewSceneColor);  		GraphBuilder.AddPass( 			// Friendly name of the pass for profilers using printf semantics. 			RDG_EVENT_NAME("MyShader %d%d", View.ViewRect.Width(), View.ViewRect.Height()), 			// Parameters provided to RDG. 			PassParameters, 			// Issues compute commands. 			ERDGPassFlags::Compute, 			// This is deferred until Execute. May execute in parallel with other passes. 			[PassParameters, ComputeShader, GroupCount] (FRHIComputeCommandList& RHICmdList) 		{ 			FComputeShaderUtils::Dispatch(RHICmdList, ComputeShader, PassParameters, GroupCount); 		});  		// Execute the graph. 		GraphBuilder.Execute(); 	}`

Copy full snippet
```
{ FRDGBuilder GraphBuilder(RHICmdList); FMyShaderCS::FParameters\* PassParameters = GraphBuilder.AllocParameters<FMyShaderCS::FParameters>(); //... PassParameters->SceneColorTexture = SceneColor; PassParameters->SceneColorSampler = TStaticSamplerState<SF\_Point, AM\_Clamp, AM\_Clamp>::GetRHI(); PassParameters->SceneColorOutput = GraphBuilder.CreateUAV(NewSceneColor); GraphBuilder.AddPass( // Friendly name of the pass for profilers using printf semantics. RDG\_EVENT\_NAME("MyShader %d%d", View.ViewRect.Width(), View.ViewRect.Height()), // Parameters provided to RDG. PassParameters, // Issues compute commands. ERDGPassFlags::Compute, // This is deferred until Execute. May execute in parallel with other passes. \[PassParameters, ComputeShader, GroupCount\] (FRHIComputeCommandList& RHICmdList) { FComputeShaderUtils::Dispatch(RHICmdList, ComputeShader, PassParameters, GroupCount); }); // Execute the graph. GraphBuilder.Execute(); }

The graph builder API is single-threaded and only one instance may be instantiated at a time, precluding hierarchical or side-by-side graphs. Both the deferred and mobile renderers use a single builder instance for each scene render invocation.

#### Setup and Execute Timelines

RDG splits the render pipeline into two timelines: **setup** and **execute**.

The graph is built during the setup timeline. This is where resource creation and render pipeline configuration branching is done. All RHI commands are deferred into pass lambdas, which are called on the execute timeline.

Code specified in the pass lambdas should be free from side effects and simply record commands into the command list, as pass execution may be parallelized.

![Setup and execute timelines with and without RDG.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d33cdcc-e5e2-47d5-ba42-19d034080a48/setup-and-execute-timelines-with-and-without-rdg.png)

The diagram above depicts the render pipeline timeline with and without RDG.

In the diagram without RDG, rendering features are written on a single timeline where both setup and execution are done in place. RHI commands are recorded and submitted directly in line with pipeline branching and resource allocation.

With RGD, the setup code is separated from execution through user-supplied pass execution lambdas. RDG performs an additional compilation step prior to invoking the pass execution lambdas, and execution is performed across several threads, calling into the lambdas to record render commands into RHI command lists.

### RDG Utilities Functions

Render Dependency Graph includes several helpful utility functions for adding common passes, located in `RenderGraphUtils.h`. These utilities should be used where possible to reduce boilerplate across the engine.

For example, use `FComputeShaderUtils::AddPass` for a compute shader pass for `FPixelShaderUtils::AddFullscreenPass` for a full screen pixel shader pass.

The examples that follow are written verbosely for educational purposes. **Use utility functions where possible.**

### RDG Resources and Views

An RDG resource initially contains the RHI resource descriptor. The associated RHI resource is only accessible within the execution lambda of a pass which declares the resource as a pass parameter.All RDG resources provide an `FRDGResource::GetRHI` overload for the specific subclass type. Access to this method is restricted to pass lambdas and the validation layer will assert if the method is improperly called.

The following properties are specific to the **Buffer** and **Texture** resources:

-   A resource can be **Transient**, whereby its lifetime is constrained to the graph and the memory can potentially alias with other transient resources with disjointed lifetimes.
-   Alternatively, a resource can be **External**, whereby its lifetime extends outside the graph. This happens if the user registers an existing RHI resource into the graph, or extracts a resource out of the graph after the execution has completed.

An RDG buffer and texture may be specialized with an RDG unordered access or shader resource view. Like other RDG resources, the underlying RHI resource is allocated on demand during execution and access is only allowed for passes that declare it as a parameter. The code sample below demonstrates how to create textures, buffers, and views resources.

**Resource Creation Examples:**

```
	`// Create a new transient texture instance. No GPU memory is allocated at this point, just the descriptor. 	FRDGTexture* Texture = GraphBuilder.CreateTexture(FRDGTextureDesc::Create2D(...), TEXT("MyTexture"));  	// Invalid! Will trigger an assert. This is only allowed in a pass lambda if declared on the pass! 	FRHITexture* TextureRHI = Texture->GetRHI();  	// Create a new UAV referencing the texture at a specific mip level. 	FRDGTextureUAV* TextureUAV = GraphBuilder.CreateUAV(FRDGTextureUAVDesc(Texture, MipLevel));  	// Invalid! 	FRHIUnorderedAccessView* UAVRHI = TextureUAV->GetRHI();  	// Create a new transient structured buffer instance. 	FRDGBuffer* Buffer = GraphBuilder.CreateBuffer(FRDGBufferDesc::CreateBufferDesc(...), TEXT("MyBuffer"));  	// Invalid! 	FRHIBuffer* BufferRHI= Buffer->GetRHI();  	// Create a new SRV referencing the buffer with an R32 float format. 	FRDGBufferSRV* BufferSRV = GraphBuilder.CreateSRV(Buffer, PF_R32_FLOAT);  	// Invalid! 	FRHIShaderResourceView* SRVRHI = TextureSRV->GetRHI();`

Copy full snippet
```
// Create a new transient texture instance. No GPU memory is allocated at this point, just the descriptor. FRDGTexture\* Texture = GraphBuilder.CreateTexture(FRDGTextureDesc::Create2D(...), TEXT("MyTexture")); // Invalid! Will trigger an assert. This is only allowed in a pass lambda if declared on the pass! FRHITexture\* TextureRHI = Texture->GetRHI(); // Create a new UAV referencing the texture at a specific mip level. FRDGTextureUAV\* TextureUAV = GraphBuilder.CreateUAV(FRDGTextureUAVDesc(Texture, MipLevel)); // Invalid! FRHIUnorderedAccessView\* UAVRHI = TextureUAV->GetRHI(); // Create a new transient structured buffer instance. FRDGBuffer\* Buffer = GraphBuilder.CreateBuffer(FRDGBufferDesc::CreateBufferDesc(...), TEXT("MyBuffer")); // Invalid! FRHIBuffer\* BufferRHI= Buffer->GetRHI(); // Create a new SRV referencing the buffer with an R32 float format. FRDGBufferSRV\* BufferSRV = GraphBuilder.CreateSRV(Buffer, PF\_R32\_FLOAT); // Invalid! FRHIShaderResourceView\* SRVRHI = TextureSRV->GetRHI();

RDG resource pointers are owned by the Graph Builder. They become invalid after it is destroyed. **Any pointers after execution of the graph should be null.**

### Passes and Parameters

Pass parameters are allocated using the `FRDGBuilder::AllocParameters` function, which guarantees the correct memory lifetime. RDG extends the shader parameter struct system with its own macros. `FRDGBuilder:AddPass` consumes the custom RDG macros while ignoring shader parameter macros.

The coupling of pass parameters with shader parameters is intentional. The majority of pass parameters across the Unreal Engine are also shader parameters. Declaring them both using the same API reduces boilerplate.

The following specific examples best illustrate using passes and parameters.

#### Shader Parameter Example

This shader parameter example declares a simple hypothetical compute shader and binds some shader parameters to it without any RDG involvement at all.

This establishes a baseline that helps show how RDG is an extension of the shader parameter struct system.

Read the commented code to understand what is fully happening in this example.

**HLSL Code Example:**

```
	`Texture2D MyTexture; 	Texture2D MySRV; 	RWTexture2D MyUAV; 	float MyFloat;`

Copy full snippet
```
Texture2D MyTexture; Texture2D MySRV; RWTexture2D MyUAV; float MyFloat;

**C++ Code Example:**

```
	`class FMyComputeShader: public FGlobalShader 	{ 	public: 		DECLARE_GLOBAL_SHADER(FMyComputeShader);  		// Generates shader bindings for FParameters. 		SHADER_USE_PARAMETER_STRUCT(FMyComputeShader, FGlobalShader);  		// Inline shader parameter definition. Use FParameters name by convention. 		BEGIN_SHADER_PARAMETER_STRUCT(FParameters, /** MODULE_API */)  			// An FRHITexture* which maps to 'MyTexture' in HLSL code. 			SHADER_PARAMETER_TEXTURE(Texture2D, MyTexture)  			// An FRHIShaderResourceView* which maps to 'MySRV' in HLSL code. 			SHADER_PARAMETER_SRV(Texture2D, MySRV)  			// An FRHIUnorderedAccessView* which maps to 'MyUAV' in HLSL code. 			SHADER_PARAMETER_UAV(RWTexture2D, MyUAV)  			// A float shader parameter, which maps to 'MyFloat' in HLSL code. 			SHADER_PARAMETER(float, MyFloat)  		END_SHADER_PARAMETER_STRUCT() 	};  	IMPLEMENT_GLOBAL_SHADER(FMyComputeShader, "Path/To/Shader.usf", "MainCS", SF_Compute);  	void Render(FRHICommandList& RHICmdList, TShaderMapRef<FMyComputeShader> ComputeShader) 	{ 		RHICmdList.SetComputeShader(ComputeShader.GetComputeShader());  		// Instantiate just like any C++ struct. 		FMyComputeShader::FParameters Parameters;  		FRHITexture* MyTexture = ...; 		Parameters.MyTexture = MyTexture;  		FRHIUnorderedAccessView* MyUAV = ...; 		Parameters.MyUAV = MyUAV;  		FRHIShaderResourceView* MySRV = ...; 		Parameters.MySRV = MySRV;  		Parameters.MyFloat = 1.0f;  		// Set the entire shader parameter struct on the RHI command list using bindings from the shader. 		SetShaderParameters(RHICmdList, ComputeShader, ComputeShader.GetComputeShader(), Parameters);  		// ... 	}`
Copy full snippet
```
class FMyComputeShader: public FGlobalShader { public: DECLARE\_GLOBAL\_SHADER(FMyComputeShader); // Generates shader bindings for FParameters. SHADER\_USE\_PARAMETER\_STRUCT(FMyComputeShader, FGlobalShader); // Inline shader parameter definition. Use FParameters name by convention. BEGIN\_SHADER\_PARAMETER\_STRUCT(FParameters, /\*\* MODULE\_API \*/) // An FRHITexture\* which maps to 'MyTexture' in HLSL code. SHADER\_PARAMETER\_TEXTURE(Texture2D, MyTexture) // An FRHIShaderResourceView\* which maps to 'MySRV' in HLSL code. SHADER\_PARAMETER\_SRV(Texture2D, MySRV) // An FRHIUnorderedAccessView\* which maps to 'MyUAV' in HLSL code. SHADER\_PARAMETER\_UAV(RWTexture2D, MyUAV) // A float shader parameter, which maps to 'MyFloat' in HLSL code. SHADER\_PARAMETER(float, MyFloat) END\_SHADER\_PARAMETER\_STRUCT() }; IMPLEMENT\_GLOBAL\_SHADER(FMyComputeShader, "Path/To/Shader.usf", "MainCS", SF\_Compute); void Render(FRHICommandList& RHICmdList, TShaderMapRef<FMyComputeShader> ComputeShader) { RHICmdList.SetComputeShader(ComputeShader.GetComputeShader()); // Instantiate just like any C++ struct. FMyComputeShader::FParameters Parameters; FRHITexture\* MyTexture = ...; Parameters.MyTexture = MyTexture; FRHIUnorderedAccessView\* MyUAV = ...; Parameters.MyUAV = MyUAV; FRHIShaderResourceView\* MySRV = ...; Parameters.MySRV = MySRV; Parameters.MyFloat = 1.0f; // Set the entire shader parameter struct on the RHI command list using bindings from the shader. SetShaderParameters(RHICmdList, ComputeShader, ComputeShader.GetComputeShader(), Parameters); // ... }

#### Shader and Pass Parameters Example

In this example, the code has been converted to RDG. The compute shader contains RDG resources in its `FParameters` struct, and a new RDG pass is added to bind the compute shader parameters.

**C++ Code Example:**

```
	`class FMyComputeShader: public FGlobalShader 	{ 	public: 		DECLARE_GLOBAL_SHADER(FMyComputeShader); 		SHADER_USE_PARAMETER_STRUCT(FMyComputeShader, FGlobalShader);  		BEGIN_SHADER_PARAMETER_STRUCT(FParameters, )  			// Declares read access to an FRDGTexture* which maps to 'MyTexture' in HLSL code. 			SHADER_PARAMETER_RDG_TEXTURE(Texture2D, MyTexture)  			// Declares read access to an FRDGTextureSRV* which maps to 'MySRV' in HLSL code. 			SHADER_PARAMETER_RDG_TEXTURE_SRV(Texture2D, MySRV)  			// Declares write access to an FRDGTextureUAV* which maps to 'MyUAV' in HLSL code. 			SHADER_PARAMETER_RDG_TEXTURE_UAV(RWTexture2D, MyUAV)  			// A float shader parameter, which maps to 'MyFloat' in HLSL code. Ignored by RDG. 			SHADER_PARAMETER(float, MyFloat)  		END_SHADER_PARAMETER_STRUCT() 	};  	IMPLEMENT_GLOBAL_SHADER(FMyCS, "Path/To/Shader.usf", "MainCS", SF_Compute);  	void AddPass(FRDGBuilder& GraphBuilder, TShaderMapRef<FMyCS> ComputeShader) 	{ 		FMyComputeShader::FParameters* PassParameters = GraphBuilder.AllocParameters<FMyCS::FParameters>();  		// Consumed by FRDGBuilder::AddPass and SetShaderParameters 		FRDGTexture* MyTexture = ...; 		PassParameters->MyTexture = MyTexture;  		FRDGTextureUAV* MyUAV = ...; 		PassParameters->MyUAV = MyUAV;  		// NOTE: You can also assign null pointers just like with shader parameters. RDG will ignore null parameters. 		FRDGTextureSRV* MySRV = nullptr; 		PassParameters->MySRV = MySRV;  		// Ignored by FRDGBuilder::AddPass, consumed by SetShaderParameters 		PassParameters->MyFloat = 1.0f;  		// Adds a single compute pass to be executed later during GraphBuilder.Execute(). The user provides the PassParameter struct 		// as well as a C++ lambda to call later during graph execution. ERDGPassFlags::Compute tells RDG that this pass will only 		// issue Compute commands (e.g. no Raster commands would be allowed).  		GraphBuilder.AddPass( 			RDG_EVENT_NAME("MyComputeShader"), 			PassParameters, // <- RDG will consume the pass parameters here. 			ERDGPassFlags::Compute, 			[ComputeShader, PassParameters /** <- PassParameters is marshaled into the lambda here */](FRHIComputeCommandList& RHICmdList) 		{ 			RHICmdList.SetComputeShader(ComputeShader.GetComputeShader());  			// PassParameters are set here. All non-null RDG parameters are dereferenced to their respective RHI resources. 			SetShaderParameters(RHICmdList, ComputeShader, ComputeShader.GetComputeShader(), *PassParameters);  			// ... 		}); 	}`

Copy full snippet
```
class FMyComputeShader: public FGlobalShader { public: DECLARE\_GLOBAL\_SHADER(FMyComputeShader); SHADER\_USE\_PARAMETER\_STRUCT(FMyComputeShader, FGlobalShader); BEGIN\_SHADER\_PARAMETER\_STRUCT(FParameters, ) // Declares read access to an FRDGTexture\* which maps to 'MyTexture' in HLSL code. SHADER\_PARAMETER\_RDG\_TEXTURE(Texture2D, MyTexture) // Declares read access to an FRDGTextureSRV\* which maps to 'MySRV' in HLSL code. SHADER\_PARAMETER\_RDG\_TEXTURE\_SRV(Texture2D, MySRV) // Declares write access to an FRDGTextureUAV\* which maps to 'MyUAV' in HLSL code. SHADER\_PARAMETER\_RDG\_TEXTURE\_UAV(RWTexture2D, MyUAV) // A float shader parameter, which maps to 'MyFloat' in HLSL code. Ignored by RDG. SHADER\_PARAMETER(float, MyFloat) END\_SHADER\_PARAMETER\_STRUCT() }; IMPLEMENT\_GLOBAL\_SHADER(FMyCS, "Path/To/Shader.usf", "MainCS", SF\_Compute); void AddPass(FRDGBuilder& GraphBuilder, TShaderMapRef<FMyCS> ComputeShader) { FMyComputeShader::FParameters\* PassParameters = GraphBuilder.AllocParameters<FMyCS::FParameters>(); // Consumed by FRDGBuilder::AddPass and SetShaderParameters FRDGTexture\* MyTexture = ...; PassParameters->MyTexture = MyTexture; FRDGTextureUAV\* MyUAV = ...; PassParameters->MyUAV = MyUAV; // NOTE: You can also assign null pointers just like with shader parameters. RDG will ignore null parameters. FRDGTextureSRV\* MySRV = nullptr; PassParameters->MySRV = MySRV; // Ignored by FRDGBuilder::AddPass, consumed by SetShaderParameters PassParameters->MyFloat = 1.0f; // Adds a single compute pass to be executed later during GraphBuilder.Execute(). The user provides the PassParameter struct // as well as a C++ lambda to call later during graph execution. ERDGPassFlags::Compute tells RDG that this pass will only // issue Compute commands (e.g. no Raster commands would be allowed). GraphBuilder.AddPass( RDG\_EVENT\_NAME("MyComputeShader"), PassParameters, // <- RDG will consume the pass parameters here. ERDGPassFlags::Compute, \[ComputeShader, PassParameters /\*\* <- PassParameters is marshaled into the lambda here \*/\](FRHIComputeCommandList& RHICmdList) { RHICmdList.SetComputeShader(ComputeShader.GetComputeShader()); // PassParameters are set here. All non-null RDG parameters are dereferenced to their respective RHI resources. SetShaderParameters(RHICmdList, ComputeShader, ComputeShader.GetComputeShader(), \*PassParameters); // ... }); }

#### Pass Parameters Without Shader Parameters Example

Continuing with this example, the code shows how some pass parameters do not have shader semantics by implementing a simple `CopyTexture` utility function in RDG.

This is useful in cases where the pass is not one-to-one with a shader, or when no shader is involved at all.

**C++ Code Example:**

```
	`BEGIN_SHADER_PARAMETER_STRUCT(FCopyTextureParameters, )  		// Declares CopySrc access to an FRDGTexture* 		RDG_TEXTURE_ACCESS(Input,  ERHIAccess::CopySrc)  		// Declares CopyDest access to an FRDGTexture* 		RDG_TEXTURE_ACCESS(Output, ERHIAccess::CopyDest)  	END_SHADER_PARAMETER_STRUCT()  	void AddCopyTexturePass( 		FRDGBuilder& GraphBuilder, 		FRDGTextureRef InputTexture, 		FRDGTextureRef OutputTexture, 		const FRHICopyTextureInfo& CopyInfo) 	{ 		FCopyTextureParameters* Parameters = GraphBuilder.AllocParameters<FCopyTextureParameters>(); 		Parameters->Input = InputTexture; 		Parameters->Output = OutputTexture;  		GraphBuilder.AddPass( 			RDG_EVENT_NAME("CopyTexture(%s -> %s)", InputTexture->Name, OutputTexture->Name), 			Parameters, 			ERDGPassFlags::Copy, 			[InputTexture, OutputTexture, CopyInfo](FRHICommandList& RHICmdList) 		{ 			RHICmdList.CopyTexture(InputTexture->GetRHI(), OutputTexture->GetRHI(), CopyInfo); 		}); 	}`

Copy full snippet
```
BEGIN\_SHADER\_PARAMETER\_STRUCT(FCopyTextureParameters, ) // Declares CopySrc access to an FRDGTexture\* RDG\_TEXTURE\_ACCESS(Input, ERHIAccess::CopySrc) // Declares CopyDest access to an FRDGTexture\* RDG\_TEXTURE\_ACCESS(Output, ERHIAccess::CopyDest) END\_SHADER\_PARAMETER\_STRUCT() void AddCopyTexturePass( FRDGBuilder& GraphBuilder, FRDGTextureRef InputTexture, FRDGTextureRef OutputTexture, const FRHICopyTextureInfo& CopyInfo) { FCopyTextureParameters\* Parameters = GraphBuilder.AllocParameters<FCopyTextureParameters>(); Parameters->Input = InputTexture; Parameters->Output = OutputTexture; GraphBuilder.AddPass( RDG\_EVENT\_NAME("CopyTexture(%s -> %s)", InputTexture->Name, OutputTexture->Name), Parameters, ERDGPassFlags::Copy, \[InputTexture, OutputTexture, CopyInfo\](FRHICommandList& RHICmdList) { RHICmdList.CopyTexture(InputTexture->GetRHI(), OutputTexture->GetRHI(), CopyInfo); }); }

#### Raster Passes

RDG exposes fixed-function render targets for raster passes through the `RENDER_TARGET_BINDING_SLOTS` parameter. The RHI utilizes render passes to bind render targets to a command list. RDG handles all of this for you automatically by determining when to begin and end the render pass. You just need to supply the bindings for it to do so.

##### Load Actions

Binding a color or depth/stencil target requires specifying one or more **Load Actions**. These actions are used to control initial pixel values for each target. Tiled rendering hardware requires accurate actions to achieve the best performance.

The following are valid load actions:

-   **Load:** Preserves existing contents of the texture.
-   **Clear:** Clears the texture to its optimized clear value.
-   **NoAction:** May not preserve contents. This option is faster on some hardware if all valid pixels are being written to.

A unique load action is specified separately for depth and stencil. Depth stencil targets also require `FExclusivieDepthStencil` struct to control whether each plane has read or write access.

The following example shows a couple of different ways to clear render targets with RDG. The color target is manually cleared, while the depth and stencil target uses the hardware clear action.

**C++ Code Example:**

```
	`BEGIN_SHADER_PARAMETER_STRUCT(FRenderTargetParameters, RENDERCORE_API)  		// These binding slots contain color and depth stencil targets. 		RENDER_TARGET_BINDING_SLOTS()  	END_SHADER_PARAMETER_STRUCT()  	void AddClearRenderTargetPass(FRDGBuilder& GraphBuilder, FRDGTexture* Texture, const FLinearColor& ClearColor, FIntRect Viewport) 	{ 		FRenderTargetParameters* Parameters = GraphBuilder.AllocParameters<FRenderTargetParameters>();  		Parameters->RenderTargets[0] = FRenderTargetBinding( 			Texture, 			ERenderTargetLoadAction::ENoAction // <- We do not want to load prior contents of the render target, since we are manually clearing. 		);  		GraphBuilder.AddPass( 			RDG_EVENT_NAME("ClearRenderTarget(%s) [(%d, %d), (%d, %d)] ClearQuad", Texture->Name, Viewport.Min.X, Viewport.Min.Y, Viewport.Max.X, Viewport.Max.Y), 			Parameters, 			ERDGPassFlags::Raster, 			[Parameters, ClearColor, Viewport](FRHICommandList& RHICmdList) 		{ 			RHICmdList.SetViewport(Viewport.Min.X, Viewport.Min.Y, 0.0f, Viewport.Max.X, Viewport.Max.Y, 1.0f); 			DrawClearQuad(RHICmdList, ClearColor); 		}); 	}  	void AddClearDepthStencilPass(FRDGBuilder& GraphBuilder, FRDGTextureRef Texture) 	{ 		auto* PassParameters = GraphBuilder.AllocParameters<FRenderTargetParameters>();  		PassParameters->RenderTargets.DepthStencil = FDepthStencilBinding( 			Texture, 			ERenderTargetLoadAction::EClear, // <- Clear depth to its optimized clear value. 			ERenderTargetLoadAction::EClear, // <- Clear stencil to its optimized clear value. 			FExclusiveDepthStencil::DepthWrite_StencilWrite // <- Allow writes to both depth and stencil. 		);  		GraphBuilder.AddPass( 			RDG_EVENT_NAME("ClearDepthStencil (%s)", Texture->Name), 			PassParameters, 			ERDGPassFlags::Raster, 			[](FRHICommandList&) 		{ 			// No actual work to do in the lambda! RDG handles the render pass for us! The clear is done via the clear action. 		}); 	}`

Copy full snippet
```
BEGIN\_SHADER\_PARAMETER\_STRUCT(FRenderTargetParameters, RENDERCORE\_API) // These binding slots contain color and depth stencil targets. RENDER\_TARGET\_BINDING\_SLOTS() END\_SHADER\_PARAMETER\_STRUCT() void AddClearRenderTargetPass(FRDGBuilder& GraphBuilder, FRDGTexture\* Texture, const FLinearColor& ClearColor, FIntRect Viewport) { FRenderTargetParameters\* Parameters = GraphBuilder.AllocParameters<FRenderTargetParameters>(); Parameters->RenderTargets\[0\] = FRenderTargetBinding( Texture, ERenderTargetLoadAction::ENoAction // <- We do not want to load prior contents of the render target, since we are manually clearing. ); GraphBuilder.AddPass( RDG\_EVENT\_NAME("ClearRenderTarget(%s) \[(%d, %d), (%d, %d)\] ClearQuad", Texture->Name, Viewport.Min.X, Viewport.Min.Y, Viewport.Max.X, Viewport.Max.Y), Parameters, ERDGPassFlags::Raster, \[Parameters, ClearColor, Viewport\](FRHICommandList& RHICmdList) { RHICmdList.SetViewport(Viewport.Min.X, Viewport.Min.Y, 0.0f, Viewport.Max.X, Viewport.Max.Y, 1.0f); DrawClearQuad(RHICmdList, ClearColor); }); } void AddClearDepthStencilPass(FRDGBuilder& GraphBuilder, FRDGTextureRef Texture) { auto\* PassParameters = GraphBuilder.AllocParameters<FRenderTargetParameters>(); PassParameters->RenderTargets.DepthStencil = FDepthStencilBinding( Texture, ERenderTargetLoadAction::EClear, // <- Clear depth to its optimized clear value. ERenderTargetLoadAction::EClear, // <- Clear stencil to its optimized clear value. FExclusiveDepthStencil::DepthWrite\_StencilWrite // <- Allow writes to both depth and stencil. ); GraphBuilder.AddPass( RDG\_EVENT\_NAME("ClearDepthStencil (%s)", Texture->Name), PassParameters, ERDGPassFlags::Raster, \[\](FRHICommandList&) { // No actual work to do in the lambda! RDG handles the render pass for us! The clear is done via the clear action. }); }

##### UAV Raster Passes

REG supports raster passes, which output to unordered access views (UAV) instead of fixed function render targets. The most straightforward way is with the `FPixelShaderUtils::AddUAVPass` utility that creates a custom render pass without any render targets and binds the RHI viewport for you.

**C++ Code Example:**

```
	`BEGIN_SHADER_PARAMETER_STRUCT(FUAVRasterPassParameters, RENDERCORE_API) 		SHADER_PARAMETER_RDG_TEXTURE_UAV(RWTexture2D, Output) 	END_SHADER_PARAMETER_STRUCT()  	auto* PassParameters = GraphBuilder.AllocParameters<FUAVRasterPassParameters>(); 	PassParameters.Output = GraphBuilder.CreateUAV(OutputTexture);  	// Specify the viewport rect. 	FIntRect ViewportRect = ...;  	FPixelShaderUtils::AddUAVPass( 		GraphBuilder, 		RDG_EVENT_NAME("Raster UAV Pass"), 		PassParameters, 		ViewportRect, 		[](FRHICommandList& RHICmdList) 	{ 		// Bind parameters and draw. 	});`
Copy full snippet
```
BEGIN\_SHADER\_PARAMETER\_STRUCT(FUAVRasterPassParameters, RENDERCORE\_API) SHADER\_PARAMETER\_RDG\_TEXTURE\_UAV(RWTexture2D, Output) END\_SHADER\_PARAMETER\_STRUCT() auto\* PassParameters = GraphBuilder.AllocParameters<FUAVRasterPassParameters>(); PassParameters.Output = GraphBuilder.CreateUAV(OutputTexture); // Specify the viewport rect. FIntRect ViewportRect = ...; FPixelShaderUtils::AddUAVPass( GraphBuilder, RDG\_EVENT\_NAME("Raster UAV Pass"), PassParameters, ViewportRect, \[\](FRHICommandList& RHICmdList) { // Bind parameters and draw. });

##### Resources Dependency Management

When a RDG resource is present on the pass parameter struct supplied to `FRDGBuilder::AddPass`, the associate may extend the lifetime of the resource, or create a dependency with a prior pass. Ideally, resources are declared only when necessary to reduce graph complexity, and unused resource parameters should be marked as null to remove them from the pass.

The challenge is that the shader dictates whether a resource is used since a permutation of the shader might compile out a resource or introduce a new one. To solve this problem, RDG includes the `ClearUnusedGraphResources` utility function which nulls out resources that are not used by the shader.

**ClearUnusedGraphResources Utility Example:**

```
`FMyShaderCS::FParameters* PassParameters = GraphBuilder.AllocParameters<FMyShaderCS::FParameters>(); //...  ClearUnusedGraphresources(*ComputeShader, PassParameters); GraphBuilder.AddPass(  	RDG_EVENT_NAME("..."), 	PassParameters, 	ERDGPassFlags::Compute, 	[PassParameters, ComputeShader, GroupCount] (FRHIComputeCommandList& RHICmdList) { 	FComputeShaderUtils::Dispatch(RHICmdList, ComputeShader, *PassParameters, GroupCount); });`
Copy full snippet
```
FMyShaderCS::FParameters\* PassParameters = GraphBuilder.AllocParameters<FMyShaderCS::FParameters>(); //... ClearUnusedGraphresources(\*ComputeShader, PassParameters); GraphBuilder.AddPass( RDG\_EVENT\_NAME("..."), PassParameters, ERDGPassFlags::Compute, \[PassParameters, ComputeShader, GroupCount\] (FRHIComputeCommandList& RHICmdList) { FComputeShaderUtils::Dispatch(RHICmdList, ComputeShader, \*PassParameters, GroupCount); });

A version of the `ClearUnusedGraphResources` utility exists for multiple shaders. This variant only clears resources unused by any shader.

##### Mipmap Generation Example

With all the major pieces in place, the code example in this section demonstrates how to generate a mipmap chain using both **Raster** and **Compute** passes. Multiple passes are chained together using texture unordered access views (UAV) and shader resource views (SRV) to express subresources.

The following is a simplified example taken from the Unreal Engine codebase that illustrates the use of utility functions to reduce boilerplate for simple fullscreen draws, or compute dispatches.

**Raster Mipmap Generation Example:**

```
	`class FGenerateMipsVS : public FGlobalShader 	{ 	public: 		DECLARE_GLOBAL_SHADER(FGenerateMipsVS); 	};  	IMPLEMENT_GLOBAL_SHADER(FGenerateMipsVS, "/Engine/Private/ComputeGenerateMips.usf", "MainVS", SF_Vertex);  	class FGenerateMipsPS : public FGlobalShader 	{ 	public: 		DECLARE_GLOBAL_SHADER(FGenerateMipsPS); 		SHADER_USE_PARAMETER_STRUCT(FGenerateMipsPS, FGlobalShader);  		BEGIN_SHADER_PARAMETER_STRUCT(FParameters, ) 			SHADER_PARAMETER(FVector2D, HalfTexelSize) 			SHADER_PARAMETER(float, Level) 			SHADER_PARAMETER_RDG_TEXTURE_SRV(Texture2D, MipInSRV) 			SHADER_PARAMETER_SAMPLER(SamplerState, MipSampler) 			RENDER_TARGET_BINDING_SLOTS() 		END_SHADER_PARAMETER_STRUCT() 	};  	IMPLEMENT_GLOBAL_SHADER(FGenerateMipsPS, "/Engine/Private/ComputeGenerateMips.usf", "MainPS", SF_Pixel);  	void FGenerateMips::ExecuteRaster(FRDGBuilder& GraphBuilder, FRDGTexture* Texture, FRHISamplerState* Sampler) 	{ 		auto ShaderMap = GetGlobalShaderMap(GMaxRHIFeatureLevel); 		TShaderMapRef<FGenerateMipsVS> VertexShader(ShaderMap); 		TShaderMapRef<FGenerateMipsPS> PixelShader(ShaderMap);  		for (uint32 MipLevel = 1, MipCount = Texture->Desc.NumMips; MipLevel < MipCount; ++MipLevel) 		{ 			const uint32 InputMipLevel = MipLevel - 1;  			const FIntPoint DestTextureSize( 				FMath::Max(Texture->Desc.Extent.X >> MipLevel, 1), 				FMath::Max(Texture->Desc.Extent.Y >> MipLevel, 1));  			FGenerateMipsPS::FParameters* PassParameters = GraphBuilder.AllocParameters<FGenerateMipsPS::FParameters>(); 			PassParameters->HalfTexelSize = FVector2D(0.5f / DestTextureSize.X, 0.5f / DestTextureSize.Y); 			PassParameters->Level = InputMipLevel; 			PassParameters->MipInSRV = GraphBuilder.CreateSRV(FRDGTextureSRVDesc::CreateForMipLevel(Texture, InputMipLevel)); 			PassParameters->MipSampler = Sampler; 			PassParameters->RenderTargets[0] = FRenderTargetBinding(Texture, ERenderTargetLoadAction::ELoad, MipLevel);  			FPixelShaderUtils::AddFullscreenPass( 				GraphBuilder, 				ShaderMap, 				RDG_EVENT_NAME("GenerateMips DestMipLevel=%d", MipLevel), 				PixelShader, 				PassParameters, 				FIntRect(FIntPoint::ZeroValue, DestTextureSize)); 		} 	}`

Copy full snippet
```
class FGenerateMipsVS : public FGlobalShader { public: DECLARE\_GLOBAL\_SHADER(FGenerateMipsVS); }; IMPLEMENT\_GLOBAL\_SHADER(FGenerateMipsVS, "/Engine/Private/ComputeGenerateMips.usf", "MainVS", SF\_Vertex); class FGenerateMipsPS : public FGlobalShader { public: DECLARE\_GLOBAL\_SHADER(FGenerateMipsPS); SHADER\_USE\_PARAMETER\_STRUCT(FGenerateMipsPS, FGlobalShader); BEGIN\_SHADER\_PARAMETER\_STRUCT(FParameters, ) SHADER\_PARAMETER(FVector2D, HalfTexelSize) SHADER\_PARAMETER(float, Level) SHADER\_PARAMETER\_RDG\_TEXTURE\_SRV(Texture2D, MipInSRV) SHADER\_PARAMETER\_SAMPLER(SamplerState, MipSampler) RENDER\_TARGET\_BINDING\_SLOTS() END\_SHADER\_PARAMETER\_STRUCT() }; IMPLEMENT\_GLOBAL\_SHADER(FGenerateMipsPS, "/Engine/Private/ComputeGenerateMips.usf", "MainPS", SF\_Pixel); void FGenerateMips::ExecuteRaster(FRDGBuilder& GraphBuilder, FRDGTexture\* Texture, FRHISamplerState\* Sampler) { auto ShaderMap = GetGlobalShaderMap(GMaxRHIFeatureLevel); TShaderMapRef<FGenerateMipsVS> VertexShader(ShaderMap); TShaderMapRef<FGenerateMipsPS> PixelShader(ShaderMap); for (uint32 MipLevel = 1, MipCount = Texture->Desc.NumMips; MipLevel < MipCount; ++MipLevel) { const uint32 InputMipLevel = MipLevel - 1; const FIntPoint DestTextureSize( FMath::Max(Texture->Desc.Extent.X >> MipLevel, 1), FMath::Max(Texture->Desc.Extent.Y >> MipLevel, 1)); FGenerateMipsPS::FParameters\* PassParameters = GraphBuilder.AllocParameters<FGenerateMipsPS::FParameters>(); PassParameters->HalfTexelSize = FVector2D(0.5f / DestTextureSize.X, 0.5f / DestTextureSize.Y); PassParameters->Level = InputMipLevel; PassParameters->MipInSRV = GraphBuilder.CreateSRV(FRDGTextureSRVDesc::CreateForMipLevel(Texture, InputMipLevel)); PassParameters->MipSampler = Sampler; PassParameters->RenderTargets\[0\] = FRenderTargetBinding(Texture, ERenderTargetLoadAction::ELoad, MipLevel); FPixelShaderUtils::AddFullscreenPass( GraphBuilder, ShaderMap, RDG\_EVENT\_NAME("GenerateMips DestMipLevel=%d", MipLevel), PixelShader, PassParameters, FIntRect(FIntPoint::ZeroValue, DestTextureSize)); } }

**Compute Mipmap Generation Example:**

```
	`class FGenerateMipsCS : public FGlobalShader 	{ 	public: 		DECLARE_GLOBAL_SHADER(FGenerateMipsCS) 		SHADER_USE_PARAMETER_STRUCT(FGenerateMipsCS, FGlobalShader)  		BEGIN_SHADER_PARAMETER_STRUCT(FParameters, ) 			SHADER_PARAMETER(FVector2D, TexelSize) 			SHADER_PARAMETER_RDG_TEXTURE_SRV(Texture2D, MipInSRV) 			SHADER_PARAMETER_RDG_TEXTURE_UAV(RWTexture2D, MipOutUAV) 			SHADER_PARAMETER_SAMPLER(SamplerState, MipSampler) 		END_SHADER_PARAMETER_STRUCT() 	};  	IMPLEMENT_GLOBAL_SHADER(FGenerateMipsCS, "/Engine/Private/ComputeGenerateMips.usf", "MainCS", SF_Compute);  	void FGenerateMips::ExecuteCompute(FRDGBuilder& GraphBuilder, FRDGTexture* Texture, FRHISamplerState* Sampler) 	{ 		TShaderMapRef<FGenerateMipsCS> ComputeShader(GetGlobalShaderMap(GMaxRHIFeatureLevel));  		// Loop through each level of the mips that require creation and add a dispatch pass per level. 		for (uint32 MipLevel = 1, MipCount = TextureDesc.NumMips; MipLevel < MipCount; ++MipLevel) 		{ 			const FIntPoint DestTextureSize( 				FMath::Max(TextureDesc.Extent.X >> MipLevel, 1), 				FMath::Max(TextureDesc.Extent.Y >> MipLevel, 1));  			FGenerateMipsCS::FParameters* PassParameters = GraphBuilder.AllocParameters<FGenerateMipsCS::FParameters>(); 			PassParameters->TexelSize  = FVector2D(1.0f / DestTextureSize.X, 1.0f / DestTextureSize.Y); 			PassParameters->MipInSRV   = GraphBuilder.CreateSRV(FRDGTextureSRVDesc::CreateForMipLevel(Texture, MipLevel - 1)); 			PassParameters->MipOutUAV  = GraphBuilder.CreateUAV(FRDGTextureUAVDesc(Texture, MipLevel)); 			PassParameters->MipSampler = Sampler;  			FComputeShaderUtils::AddPass( 				GraphBuilder, 				RDG_EVENT_NAME("GenerateMips DestMipLevel=%d", MipLevel), 				ComputeShader, 				PassParameters, 				FComputeShaderUtils::GetGroupCount(DestTextureSize, FComputeShaderUtils::kGolden2DGroupSize)); 		} 	}`

Copy full snippet
```
class FGenerateMipsCS : public FGlobalShader { public: DECLARE\_GLOBAL\_SHADER(FGenerateMipsCS) SHADER\_USE\_PARAMETER\_STRUCT(FGenerateMipsCS, FGlobalShader) BEGIN\_SHADER\_PARAMETER\_STRUCT(FParameters, ) SHADER\_PARAMETER(FVector2D, TexelSize) SHADER\_PARAMETER\_RDG\_TEXTURE\_SRV(Texture2D, MipInSRV) SHADER\_PARAMETER\_RDG\_TEXTURE\_UAV(RWTexture2D, MipOutUAV) SHADER\_PARAMETER\_SAMPLER(SamplerState, MipSampler) END\_SHADER\_PARAMETER\_STRUCT() }; IMPLEMENT\_GLOBAL\_SHADER(FGenerateMipsCS, "/Engine/Private/ComputeGenerateMips.usf", "MainCS", SF\_Compute); void FGenerateMips::ExecuteCompute(FRDGBuilder& GraphBuilder, FRDGTexture\* Texture, FRHISamplerState\* Sampler) { TShaderMapRef<FGenerateMipsCS> ComputeShader(GetGlobalShaderMap(GMaxRHIFeatureLevel)); // Loop through each level of the mips that require creation and add a dispatch pass per level. for (uint32 MipLevel = 1, MipCount = TextureDesc.NumMips; MipLevel < MipCount; ++MipLevel) { const FIntPoint DestTextureSize( FMath::Max(TextureDesc.Extent.X >> MipLevel, 1), FMath::Max(TextureDesc.Extent.Y >> MipLevel, 1)); FGenerateMipsCS::FParameters\* PassParameters = GraphBuilder.AllocParameters<FGenerateMipsCS::FParameters>(); PassParameters->TexelSize = FVector2D(1.0f / DestTextureSize.X, 1.0f / DestTextureSize.Y); PassParameters->MipInSRV = GraphBuilder.CreateSRV(FRDGTextureSRVDesc::CreateForMipLevel(Texture, MipLevel - 1)); PassParameters->MipOutUAV = GraphBuilder.CreateUAV(FRDGTextureUAVDesc(Texture, MipLevel)); PassParameters->MipSampler = Sampler; FComputeShaderUtils::AddPass( GraphBuilder, RDG\_EVENT\_NAME("GenerateMips DestMipLevel=%d", MipLevel), ComputeShader, PassParameters, FComputeShaderUtils::GetGroupCount(DestTextureSize, FComputeShaderUtils::kGolden2DGroupSize)); } }

##### Asynchronous Compute

RDG supports asynchronous compute scheduling by inspecting graph dependencies and inserting fences at synchronization points.

Asynchronous compute is enabled by tagging a pass with the `ERDGPassFlags::AsyncCompute` flag and use the `FRHIComputeCommandList` type as the argument in the pass lambda.

Asynchronous compute must also be enabled by the platform and by RDG. Platforms which do not support asynchronous compute fall back to the graphics pipe. RDG support can be disabled explicitly with the console command `r.RDG.AsyncCompute` (which is enabled by default).

**C++ Code Example:**

```
	`GraphBuilder.AddPass( 		RDG_EVENT_NAME("MyAsyncComputePass"), 		ERDGPassFlags::AsyncCompute, // <- Specify the AsyncCompute flag here. 		PassParameters, 		[] (FRHIComputeCommandList& RHICmdList) // <- Specify the FRHIComputeCommandList here. 	{ 		// Execute. 	});`
Copy full snippet
```
GraphBuilder.AddPass( RDG\_EVENT\_NAME("MyAsyncComputePass"), ERDGPassFlags::AsyncCompute, // <- Specify the AsyncCompute flag here. PassParameters, \[\] (FRHIComputeCommandList& RHICmdList) // <- Specify the FRHIComputeCommandList here. { // Execute. });

For simple compute shaders, use the async compute variant of `FComputeShaderUtils::AddPass`.

Asynchronous compute work is scheduled using the dependency graph. When one or more passes are tagged, RDG traverses the graph to find the last producer on the graphics pipeline and inserts a fence. Likewise, asynchronous compute joins back to graphics when the work is first consumed on the graphics pipeline.

The diagram below depicts the scenario described above.

![Asynchronous compute scheduling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee9678d6-d800-481e-9563-2c3bbda7868b/asynchronous-compute-scheduling.png)

This diagram depicts the graphics and asynchronous compute queues, with time shown as the horizontal axis.

In the diagram above, **Pass A** is a producer for **Pass C**. So, a fence is introduced just after Pass A executes, which signals Pass C to start work. The asynchronous compute pipe runs until **Pass D** completes, at which time it synchronizes back with the graphics pipe so that the consumer — **Pass E** — sees the correct results.

Use the RDG Insights tool to visualize asynchronous compute events in the graph. The screenshot shows a similar view to the diagram above in the RDG Insights tool, but it is captured from an actual workload in the engine. See the [RDG Insights](/documentation/en-us/unreal-engine/render-dependency-graph-in-unreal-engine#rdginsightsplugin) section of this page for more information about using the tool.

![RDG Insights Timeline Views](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71276684-6518-446a-81ca-1371497b7540/rdg-insights-views.png)

##### External Resources

A resource is considered **external** if its lifetime extends outside the graph, which can happen under two circumstances: if the resource is registered into the graph, or extracted out of the graph.

Registration into the graph is done using the `FRDGBuilder::RegisterExternal{Texture, Buffer}` methods. This creates a new RDG resource with a pre-allocated reference-counted pool RHI resource pointer: `IPooledRenderTarget` for textures, or `FRDGPooledTexture` for buffers.

Extraction from the graph fills a pooled resource pointer after execution completes. Registering a resource extends the lifetime of the RDG resource to the front of the graph. It is necessary considering the allocation occurs during graph setup. Extraction does the opposite whereby it extends the resource lifetime to the end of the graph since the user now holds a reference.

If the user does not hold a reference outside of the graph, registered or extracted resources can still technically share pooled memory with other RDG resources later, or earlier, in the frame.

The code excerpt below illustrates various ways of registering or extracting textures with the graph builder. Notice how registration and extraction use the same pooled texture type, allowing round-tripping from graph to graph.

**C++ Code Example:**

```
	`// Extract pooled render target. The pointer is filled AFTER Execute() is called. 	TRefCountPtr<IPooledRenderTarget> ExtractedTexture;  	// First graph produces the texture and extracts it. 	{ 		FRDGBuilder GraphBuilder(RHICmdList);  		FRDGTexture* Texture = GraphBuilder.CreateTexture(...);  		// ...  		GraphBuilder.QueueTextureExtraction(Texture, &ExtractedTexture); 		GraphBuilder.Execute();  		check(ExtractedTexture); // Valid 	}  	// Second graph registers the pooled texture. 	{ 		FRDGBuilder GraphBuilder(RHICmdList);  		// Register pooled render target to get RDG texture. 		FRDGTexture* Texture = GraphBuilder.RegisterExternalTexture(ExtractedTexture);  		// ...  		GraphBuilder.Execute(); 	}`
Copy full snippet
```
// Extract pooled render target. The pointer is filled AFTER Execute() is called. TRefCountPtr<IPooledRenderTarget> ExtractedTexture; // First graph produces the texture and extracts it. { FRDGBuilder GraphBuilder(RHICmdList); FRDGTexture\* Texture = GraphBuilder.CreateTexture(...); // ... GraphBuilder.QueueTextureExtraction(Texture, &ExtractedTexture); GraphBuilder.Execute(); check(ExtractedTexture); // Valid } // Second graph registers the pooled texture. { FRDGBuilder GraphBuilder(RHICmdList); // Register pooled render target to get RDG texture. FRDGTexture\* Texture = GraphBuilder.RegisterExternalTexture(ExtractedTexture); // ... GraphBuilder.Execute(); }

The code is effectively the same for buffers, except with the `FRDGPooledBuffer` class used instead.

##### Alternative Approach: Convert to External

An alternative approach to external resources is `FRDGBuilder:ConvertToExternal{Texture, Buffer}`. It performs an immediate allocation of the underlying pooled resource and returns it.

This method is useful in situations where it is not possible to wait until the end of the graph to extract the resource. The biggest difference between conversion and extraction is the lifetime extension. Conversion extends the lifetime to the beginning of the graph, while extraction extends it to the end of the graph, meaning the resource will not be able to share the underlying allocation with any other resource in the frame.

#### Transient Resources

The Render Dependency Graph employs a transient resource allocator during graph compilation to plan allocations across the execution timeline. Resources with disjoint lifetimes may overlap in memory.

Platforms with a transient allocator implemented can achieve a significant reduction in the GPU memory watermark over the default resource pool approach. This is due to increased flexibility in aliasing the memory. The resource pools are forced to compare and match RHI descriptors to determine their reuse. Whereas the transient allocator can share underlying memory.

You can control whether the transient allocator is enabled or not with the console variable `r.RDG.TransientAllocator`.

This variable is useful to toggle when looking for aliasing-specific issues. In particular, it is important to not rely on well-defined prior contents of a resource. The resource pools typically mask these issues since it is often the same, or similar, resources being reused, but that's not the case with the transient allocator. Prior contents will be garbage.

### RDG Uniform Buffers

RDG uniform buffers may contain RDG resources. As expected, RDG initializes the descriptor during graph setup and defers the creation of the underlying RHI uniform buffer until execution. If the resource is determined to be unused, it is culled and never initialized.

Creation of an RDG uniform buffer is done with `FRDGBuilder::CreateUniformBuffer` with a **uniform parameter struct** as input. The uniform parameter struct is an extension of the pass parameters and may contain RDG resources. `FRDGBuilder::AddPass` traverses child uniform parameters in addition to root pass parameters.

The current major downside to RDG uniform buffers is that they may not null resource parameters, and it is not possible for a shader to reflect and cull unused parameters. For the moment, resources must be manually pruned by creating a unique uniform buffer for each set of parameters.

See the Scene Textures Uniform Buffers in the Deferred Shading Renderer for a practical example.

RDG uniform buffers **must** be declared using `SHADER_PARAMETER_RDG_UNIFORM_BUFFER` on the pass parameter struct provided to `FRDGBuilder:AddPass` for the uniform buffer to be dereferencable in the pass lambda.

**C++ Code Example:**

```
	`// Simple uniform buffer containing a single RDG texture. 	BEGIN_UNIFORM_BUFFER_STRUCT(FMyUniformParameters, ) 		SHADER_PARAMETER_RDG_TEXTURE(Texture2D, Texture) 	END_UNIFORM_BUFFER_STRUCT()  	//  Define pass parameters with a single RDG uniform buffer parameter. 	BEGIN_SHADER_PARAMETER_STRUCT(FMyPassParameters, ) 		SHADER_PARAMETER_RDG_UNIFORM_BUFFER(FMyUniformParameters, UniformBuffer) 		RENDER_TARGET_BINDING_SLOTS() 	END_SHADER_PARAMETER_STRUCT()  	void AddPass(FRDGBuilder& GraphBuilder, TShaderMapRef<FShader> PixelShader, FRDGTexture* InputTexture, FRDGTexture* OutputTexture) 	{ 		// Create the uniform buffer first. 		FMyUniformParameters* UniformParameters = GraphBuilder.AllocParameters<FMyUniformParameters>(); 		UniformParameters->Texture = InputTexture;  		TRDGUniformBuffer<FMyUniformParameters>* UniformBuffer = GraphBuilder.CreateUniformBuffer(UniformParameters);  		// Now construct the pass. 		FMyPassParameters* PassParameters = GraphBuilder.AllocParameters<FMyPassParameters>(); 		PassParameters->UniformBuffer = UniformBuffer; 		PassParameters->RenderTargets[0] = FRenderTargetBinding(OutputTexture, ERenderTargetLoadAction::ELoad);  		GraphBuilder.AddPass( 			RDG_EVENT_NAME("MyPass"), 			PassParameters, 			ERDGPassFlags::Raster, 			[PassParameters, UniformBuffer, PixelShader](FRHICommandList& RHICmdList) 		{ 			// ... bind shaders, etc.  			// You can access the RHI uniform buffer here! 			FRHIUniformBuffer* UniformBufferRHI = UniformBuffer->GetRHI();  			// You can also access the RDG texture and it is RHI texture! 			FRHITexture* TextureRHI = (*UniformBuffer)->Texture->GetRHI();  			// You can also call the same SetShaderParameters helper method to bind the RDG uniform buffer. 			SetShaderParameters(RHICmdList, PixelShader, PixelShader.GetComputeShader(), *PassParameters); 		}); 	}`
Copy full snippet
```
// Simple uniform buffer containing a single RDG texture. BEGIN\_UNIFORM\_BUFFER\_STRUCT(FMyUniformParameters, ) SHADER\_PARAMETER\_RDG\_TEXTURE(Texture2D, Texture) END\_UNIFORM\_BUFFER\_STRUCT() // Define pass parameters with a single RDG uniform buffer parameter. BEGIN\_SHADER\_PARAMETER\_STRUCT(FMyPassParameters, ) SHADER\_PARAMETER\_RDG\_UNIFORM\_BUFFER(FMyUniformParameters, UniformBuffer) RENDER\_TARGET\_BINDING\_SLOTS() END\_SHADER\_PARAMETER\_STRUCT() void AddPass(FRDGBuilder& GraphBuilder, TShaderMapRef<FShader> PixelShader, FRDGTexture\* InputTexture, FRDGTexture\* OutputTexture) { // Create the uniform buffer first. FMyUniformParameters\* UniformParameters = GraphBuilder.AllocParameters<FMyUniformParameters>(); UniformParameters->Texture = InputTexture; TRDGUniformBuffer<FMyUniformParameters>\* UniformBuffer = GraphBuilder.CreateUniformBuffer(UniformParameters); // Now construct the pass. FMyPassParameters\* PassParameters = GraphBuilder.AllocParameters<FMyPassParameters>(); PassParameters->UniformBuffer = UniformBuffer; PassParameters->RenderTargets\[0\] = FRenderTargetBinding(OutputTexture, ERenderTargetLoadAction::ELoad); GraphBuilder.AddPass( RDG\_EVENT\_NAME("MyPass"), PassParameters, ERDGPassFlags::Raster, \[PassParameters, UniformBuffer, PixelShader\](FRHICommandList& RHICmdList) { // ... bind shaders, etc. // You can access the RHI uniform buffer here! FRHIUniformBuffer\* UniformBufferRHI = UniformBuffer->GetRHI(); // You can also access the RDG texture and it is RHI texture! FRHITexture\* TextureRHI = (\*UniformBuffer)->Texture->GetRHI(); // You can also call the same SetShaderParameters helper method to bind the RDG uniform buffer. SetShaderParameters(RHICmdList, PixelShader, PixelShader.GetComputeShader(), \*PassParameters); }); }

### Upload Buffers

If a RDG resource requires initial data from the CPU prior to executing the graph, the `FRDGBuilder::QueueBufferUpload` method is the most efficient way to schedule it. RDG batches uploads together during graph compilation and may be able to overlap the work with other compilation tasks.

The example code below demonstrates how to upload an array of CPU data to an RDG buffer.

**Buffer Upload Example:**

```
	`FRDGBuffer IndexBuffer = GraphBuilder.CreateBuffer( 		FRDGBufferDesc::CreateUploadDesc(sizeof(uint32), NumIndices), 		TEXT("MyIndexBuffer"));  	// Allocates an array of data using the internal RDG allocator for deferral. 	FRDGUploadData<int32> Indices(GraphBuilder, NumIndices);  	// Assign Data 	Indices[0] = // ...; 	Indices[1] = // ...; 	Indices[NumIndices - 1] = // ...;  	// Upload Data 	GraphBuilder.QueueBufferUpload(IndexBuffer, Indices, ERDGInitialDataFlags::NoCopy);`
Copy full snippet
```
FRDGBuffer IndexBuffer = GraphBuilder.CreateBuffer( FRDGBufferDesc::CreateUploadDesc(sizeof(uint32), NumIndices), TEXT("MyIndexBuffer")); // Allocates an array of data using the internal RDG allocator for deferral. FRDGUploadData<int32> Indices(GraphBuilder, NumIndices); // Assign Data Indices\[0\] = // ...; Indices\[1\] = // ...; Indices\[NumIndices - 1\] = // ...; // Upload Data GraphBuilder.QueueBufferUpload(IndexBuffer, Indices, ERDGInitialDataFlags::NoCopy);

Consider the following when using upload buffers in RDG:

-   Do use RDG to perform uploads.
    -   A manual lock / unlock using the immediate command list within a pass introduces a sync point and inhibits parallel execution.
    -   Upload buffers are automatically marked as non-transient. Transient resources do not support CPU uploads.
-   Do use the most accurate `ERDGInitialDataFlags`.
    -   Use `NoCopy` if data lifetime is sufficient to survive graph deferral. Otherwise, let RDG make a copy.

### Memory Lifetimes

The setup and execution timeline split requires some care when dealing with memory lifetimes. A common mistake is to pass memory into RDG lambda that is not guaranteed to exist later when the graph is executed.

To assist with this, RDG includes its own linear allocator with proper lifetime guarantees. The API supports allocation of varying cost.

For POD types, use `FRDGBuilder::AllocPOD`.

If destructor tracking is required for a C++ object, use `FRDGBuilder::AllocObject`.

**C++ Code Example:**

```
	`// Bad! 	FMyObject Object; 	GraphBuilder.AddPass(..., [&Object] (FRHICommandList&) { /** Object is captured by reference but exists on the stack! Invalid pointer! */ });  	// Good 	TUniquePtr<FMyObject> Object(new FMyObject()); 	GraphBuilder.AddPass(..., [Object = MoveTemp(Object)] (FRHICommandList&) { /** Object is valid but was expensive to allocate. */ });  	// Best if C++ object (calls destructor, adds a bit of cost) 	FMyObject* Object = GraphBuilder.AllocObject<FMyObject>(); 	GraphBuilder.AddPass(..., [Object = MoveTemp(Object)] (FRHICommandList&) { /** Object is valid and was cheap to allocate. */ });  	// Best if POD struct (will not call destructor) 	FMyObject* Object = GraphBuilder.AllocPOD<FMyObject>(); 	...  	// For raw memory. 	void* Memory = GraphBuilder.Alloc(SizeInBytes, AlignInBytes);  	// For RDG pass parameters -- may perform additional tracking. 	FMyPassParameters* PassParameters = GraphBuilder.AllocParameters<FMyPassParameters>();`
Copy full snippet
```
// Bad! FMyObject Object; GraphBuilder.AddPass(..., \[&Object\] (FRHICommandList&) { /\*\* Object is captured by reference but exists on the stack! Invalid pointer! \*/ }); // Good TUniquePtr<FMyObject> Object(new FMyObject()); GraphBuilder.AddPass(..., \[Object = MoveTemp(Object)\] (FRHICommandList&) { /\*\* Object is valid but was expensive to allocate. \*/ }); // Best if C++ object (calls destructor, adds a bit of cost) FMyObject\* Object = GraphBuilder.AllocObject<FMyObject>(); GraphBuilder.AddPass(..., \[Object = MoveTemp(Object)\] (FRHICommandList&) { /\*\* Object is valid and was cheap to allocate. \*/ }); // Best if POD struct (will not call destructor) FMyObject\* Object = GraphBuilder.AllocPOD<FMyObject>(); ... // For raw memory. void\* Memory = GraphBuilder.Alloc(SizeInBytes, AlignInBytes); // For RDG pass parameters -- may perform additional tracking. FMyPassParameters\* PassParameters = GraphBuilder.AllocParameters<FMyPassParameters>();

Any allocated memory will persist until the graph builder instance is destroyed. It uses a linear allocator and is very fast.

### Performance Profiling

RDG supports scope defines for various profilers in the engine:

-   Use `RDG_EVENT_SCOPE` to add a GPU profile scope around passes. These are consumed by external profilers like RenderDoc, as well as RDG Insights.
-   Use `RDG_GPU_STAT_SCOPE` to add a new scope for the `stat gpu` command.
-   Use `RDG_CSV_STAT_EXCLUSIVE_SCOPE` to add a new scope for the CSV profiler.

The RDG scopes take the builder as input and properly account for the separate setup and execute timelines.

### Conventions

The following are general coding conventions to use when writing code using RDG. Following these conventions ensures consistency across the renderer.

-   Construct namespaces for resources separated by dots.
    -   For example, `TSR.History.ScreenPercentage`. This simplifies name filtering in RDG insights and other tools.
-   Name graph builder instances: `GraphBuilder`
-   Name shader parameters inline on a shader instance: `FParameters`
-   Use `RDG_EVENT_SCOPE` as a namespace for passes.
-   Use utilities in `RenderGraphUtils.h` or `ScreenPass.h` where possible.

## Debugging and Validation

The Render Graph system adds complexity by introducing a deferred-mode data structure. It can be difficult to find the pass setup location associated with its execution lambda when failure occurs during execution. That is further compounded when the RHI thread is enabled, as an executing RHI command is now two degrees removed from its setup location.

For example, if a crash occurs when setting an RHI shader parameter inside a platform RHI, it is not possible to deduce where the failure occurred just from the call stack location. Both RDG and the RHI have tools to help address these issues. RDG **Immediate Mode** is a debug feature which bypasses graph compilation in favor of executing the pass directly in the `AddPass` call.

Enable the following methods when using Debug or Development builds.

| Method | Variable |
| --- | --- |
| Console Variable | `r.RDG.ImmediateMode` |
| Command Line Argument | `-rdgimmediate` |

In another example, if there is a crash within the RDG pass lambda due to a null pointer in the pass parameter struct, the debugger breaks inside the lambda and at that point it is too late to inspect any of the setup code (where the real issue was introduced). The lambda is executed on the setup timeline when immediate mode is enabled, allowing the setup code to be inspected directly.

Using the console command `r.RHICmdBypass` disables parallel rendering and software command lists. Combined with RDG immediate mode, it removes all deferral mechanisms giving a single call stack for debugging.

Additional console variables exist to control RHI threading behavior and can be referenced in the [Parallel Rendering Overview](/documentation/en-us/unreal-engine/parallel-rendering-overview-for-unreal-engine) documentation.

All graph optimizations are disabled when in Immediate Mode, including transient allocation, graph culling, render pass merging, and so on. This will introduce side-effects from them being disabled.

Additionally, use the following CVars to disable individual features in RDG without invoking immediate mode to rule them out if issues arise.

| Variable | Description |
| --- | --- |
| `r.RDG.CullPasses` | Disable to rule out whether a pass is being culled. |
| `r.RDG.MergeRenderPasses` | Disable to require a unique render pass per RDG raster pass. |
| `r.RDG.ParallelExecute` | Disable to run all passes serially on the render thread. |
| `r.RDG.TransientAllocator` | Disable to fall back to resource pooling. |

#### Validation Layer

RDG includes a validation layer which is enabled by default when using Debug or Development builds. This layer emits fatal checks with clearly marked resource / pass names as early as possible if RDG is used incorrectly. It adds additional CPU overhead and is compiled out in Test and Shipping builds.

### Resource Transition Debugging

The resource transition API in the RHI assigns an `ERHIAccess` and `ERHIPipeline` mask to each subresource. RDG takes care of transitioning individual subresources between states across the graph, assuming the resources are properly declared using RDG pass parameters. RHI validation logs when a resource is improperly transitioned, but it can be difficult to debug transitions that occur within RDG, because the call stack location will always look the same.

RDG itself has been rigorously tested to ensure that it produces the correct transitions. Should the need arise, however, RDG transition logging can be mixed with RHI transition logging to spot inconsistencies.

**RDG Transition Log:**

-   Use -rdgtransitionlog or r.rdg.transitionlog X (where X is the number of frames to log) to log all transitions that occur within RDG.
-   Use `r.RDG.Debug.ResourceFilter [ResourceName]` to filter the log by resource name.
-   Use `r.RDG.Debug.PassFilter` PassName to filter the log by pass name.

**RHI Transition Log:**

Use `-rhivalidation` and `-rhivalidationlog=ResourceName` to log a specific resource.

By default, RDG prints transitions from the **Render Thread**, whereas the RHI prints transition logs from the **RHI Thread**. To make them line up you must specify `-norhithread -forcerhibypass` or `-onethread`. Unfortunately, disabling the RHI thread can mask certain cross-pipeline transition errors, but in most cases the issue will still reproduce.

For example, to log all RDG and RHI activity for `SceneDepthZ`, use the command line arguments:

\-rhivalidation -rhivalidationlog=SceneDepthZ -rdgtransitionlog -rdgdebugresourcefilter=SceneDepthZ -onethread

### Visualize Texture

RDG publishes all texture UAV or RTV writes to the `vis` command in Development builds. Use this command to visualize resources on the screen. Type 'vis' into the command line to see the list of available resources and format of the command.

### Transient Allocator Debugging

The transient allocator introduces a source of potential artifacts. Use `r.RDG.TransientAllocator` to enable or disable the system.

If disabling the system eliminates the artifact, consider the following additional tests:

-   Use `.RDG.ClobberResources` to force-initialize all resources to a known value. If this produces a similar artifact without the transient allocator enabled, then the likely explanation is that the resource was not properly initialized before being read.
-   Use `r.RDG.Debug.ExtendResourceLifetimes` to disable all aliasing within the graph. This is useful to rule out missing aliasing barriers or incorrect resource lifetimes.
-   Use `r.RDG.Debug.DisableTransientResources` to disable resources from the transient allocator.

For either of the above commands, use `r.RDG.Debug.ResourceFilter` to filter which resources are affected. This can help narrow down problematic resources.

### RDG Insights Plugin

As an extension to the [Unreal Insights](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) tool, Render Dependency Graph has its own plugin called **RDG Insights** for real-time visualization of the RDG graph structure. Traces are captured and displayed as a track in the **Timing Insights** view alongside other CPU tracks.

Enable the **RDG Insights** plugin by going to the main menu and selecting **Edit > Plugins > Insights**.

![RDG Insights Timeline Views](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c744411b-380b-43bb-a752-2d9291a3e61f/rdg-insights-views.png)

The RDG Insights plugin can be used to inspect properties about the graph:

-   Resource lifetimes, pass associations, and resource pool allocation overlap
-   Asynchronous compute fences and overlap
-   Graph culling and render pass merging
-   Parallel execution pass ranges
-   Transient Memory Layouts

The RDG Insights plugin can also be used as a debugging and diagnostic tool to answer questions like:

-   Why aren't asynchronous compute passes overlapping with graphic passes?
-   How are resources being used across the frame?
-   Does a resource allocation overlap with other resources?
-   Which resources are used by post processing?
-   Which passes were culled?

#### Capturing a Trace

Capturing a trace only requires enabling the RDG channel in Unreal Insights. When launching the client application, specifying the `-trace=rdg,defaults` argument is sufficient.

If connected to a Live Trace in Unreal Insights, enabling the RDG channel is sufficient.

RDG traces generate a lot of data.

#### Slide Deck

For a more in-depth walkthrough of the tool, refer to the following [slide deck](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/a19f41fa-543f-4fb1-88f4-b2c09d5951c6/rdg-insights-presentation.pdf).