# PSO Precaching

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pso-precaching-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pso-precaching-for-unreal-engine)  
**Processed:** 2025-06-14 16:45:10

---

Manual **PSO caching** requires playing a build of your game to collect PSO (Pipeline State Object) information into a [Bundled Cache](https://dev.epicgames.com/documentation/en-us/unreal-engine/manually-creating-bundled-pso-caches-in-unreal-engine), **PSO Precaching** performs automatic PSO collection and async compilation for all PSOs that could be used during rendering.

## Configure PSO Precaching

The following console variables control PSO precaching:

| Console Variable | Description | Default State |
| --- | --- | --- |
| 
`r.PSOPrecaching`

 | 

Global console variable to enable PSO precaching. This relies on the RHI flag `GRHISupportsPSOPrecaching`.

 | 

Enabled

 |
| 

`r.PSOPrecache.Components`

 | 

Precache PSOs used by components.

 | 

Enabled

 |
| 

`r.PSOPrecache.Resources`

 | 

Precache PSOs used by all resources (`UStaticMesh`, `USkinnedMesh`, and so on). These PSOs might not have the correct render states because certain states can only be derived from components. However, they should give the driver the correct shaders to compile.

 | 

Disabled

 |
| 

`r.PSOPrecache.ProxyCreationWhenPSOReady`

 | 

Wait for component proxy creation until all required PSOs are compiled. If they are still compiling when creating the proxy, those PSOs are marked as high-priority.

 | 

Enabled

 |
| 

`r.PSOPrecache.ProxyCreationDelayStrategy`

 | 

When PSOs are still compiling during proxy creation of the component, this adds an option to replace the material with the default material. This relies on `r.PSOPrecache.ProxyCreationWhenPSOReady`. See Proxy Creation Delay Strategy below for more information.

 | 

0 (see below)

 |
| 

`r.PSOPrecaching.WaitForHighPriorityRequestsOnly`

 | 

Only wait for high-priority PSOs during loading. All non-essential PSOs will still compile during gameplay. A PSO is marked as high-priority when it is needed by a proxy and is not done compiling yet.

 | 

Disabled

 |
| 

`r.PSOPrecache.GlobalShaders`

 | 

Whether to precache global compute and graphics PSOs as well during startup of the engine.

 | 

Enabled

 |

## Global Shader PSO Precaching

Certain **Global Shader** PSOs are precached because these can introduce runtime hitches on first usage. These PSOs are compiled at start up time of the engine and is enabled with `r.PSOPrecache.GlobalShaders` console variable by default. All global compute shaders permutations which can be used by the game are precached.

C++

`static EShaderPermutationPrecacheRequest ShouldPrecachePermutation(const FShaderPermutationParameters& Parameters)`

static EShaderPermutationPrecacheRequest ShouldPrecachePermutation(const FShaderPermutationParameters& Parameters)

Copy full snippet(1 line long)

This used to check if a given permutation can be used at runtime by checking the current console variable settings to exclude certain combinations. By default it uses `ShouldCompilePermutation`, so the precache permutation should be a subset of the compiled permutations.

Most of the global graphic PSOs are created during the first few frames right after loading, and hitches can be noticed during these frames. Using a very small PSO bundled cache to collect these global graphics PSOs can help. But certain global graphic PSO permutations are also created and compiled at runtime, so these should be precached as well. For global graphics PSOs, specific PSO collectors are needed to collect all the correct render state, which is needed to compile the graphics PSO.

PSO precaching is currently implemented for the following global shader types:

-   Slate
    
-   Deferred Lights
    
-   Cascade Particle Simulation
    
-   Volumetric fog
    

Compiling all the global PSOs at startup takes some time and normally happens while navigating the main menu. While this is not blocking the engine at startup, it should be part of the PSO compilation waiting phase during the initial loading screen.

## Component PSO Precaching

**Primitive Components** (`UPrimitiveComponent`) precache all the PSOs needed for rendering immediately after loading (during PostLoad). The precache collects all the pipeline state information needed to compile the PSOs, including:

-   Materials
    
-   Vertex factories
    
-   Vertex element information
    
-   Specific precache parameters
    

Unreal Engine uses this information to iterate over all possible mesh pass processors where the component can be rendered. Each mesh pass processor adds the possible PSO initializers which it could need during rendering. Background tasks check a shared PSO cache to make sure the needed data isn't already being precached, and compile these requests asynchronously.

A single component might need a lot of PSOs to render correctly in all the different passes, such as base, custom depth, depth, distortion, shadow, virtual shadow map, velocity, and so on. It's important that all of these PSOs are ready before the component is ready so as to not introduce graphical artifacts because, for example, it might be rendered in one pass and not in another.

When UE creates a **Primitive Proxy** for a Primitive Component and its required PSOs are still compiling, several options are available:

-   Delay the proxy creation until the PSO compilation is finished (default). This will effectively skip the draw until the PSO is ready.
    
-   Replace the material with the engine's default material.
    
-   Continue and have a possible hitch. The draw will block on the PSO compilation.
    

### Proxy Creation Delay Strategy

The `r.PSOPrecache.ProxyCreationDelayStrategy` console variable relies on the `r.PSOPrecache.ProxyCreationWhenPSOReady` console variable. If `ProxyCreationWhenPSOReady` is set to 1 (enabled), `ProxyCreationDelayStrategy` will run the following behaviors depending on its value:

| Value | Behavior |
| --- | --- |
| 
0

 | 

Skip the draw until the PSO is ready.

 |
| 

1

 | 

Fallback to the engine's default material until the PSO is ready.

 |

## Loading screen

We highly recommend setting up your initial loading screen with PSO Precache requests in mind. .

When setting up the initial loading screen for your game, you should have this wait for all the currently outstanding PSO precache requests. Otherwise, you might see some noticeable visual popping and even some runtime hitches for components which don't support the delay proxy creation, such as landscape terrain, where it might not be advisable to replace these meshes with a default material or not render them.

`FShaderPipelineCache::NumPrecompilesRemaining()` is useful for checking the number of outstanding PSO precache compiles for both the bundled cache and PSO precaching. You can modify your loading screen logic to check for this number and keep the loading screen up until it reaches zero. In most cases, the initial PSO compile time with an empty driver cache should take less than a minute on medium spec CPUs.

## Manage System Resources

PSO precaching relies on asynchronous compilation using background threads and has an impact on system memory and performance. This section explains the options available for adjusting and optimizing the use of these resources as fits your project.

### Memory

To save runtime system memory, UE deletes PSOs compiled for precaching after compilation. That is because if the amount of PSOs precached by your application is very high, it can dramatically increase the memory footprint of the application unless they are cleaned up (hundreds of megabytes or even gigabytes).

PSO precaching relies on the existence of an underlying compressed driver cache. Even when PSOs are deleted after precaching, they are retained in the driver cache. If a PSO is needed at runtime, the graphics driver will load it from its compressed driver cache. However, this can also be resource-intensive, and the first retrievals from these caches can take a few milliseconds. You can disable deletion of the precached PSOs in D3D12 with `D3D12.PSOPrecache.KeepLowLevel`.

Creating PSOs from the driver cache can be slow on certain Independent Hardware Vendors (IHVs). For NVIDIA, there is an option to keep a certain amount of precached graphics and compute PSOs in memory with `r.PSOPrecache.KeepInMemoryUntilUsed`, which keeps the last `N` precached PSOs in memory and avoids the driver cache performance hit. The number of PSOs retained in memory can be adjusted for compute and graphics separately with `r.PSOPrecache.KeepInMemoryGraphicsMaxNum` and `r.PSOPrecache.KeepInMemoryComputeMaxNum`. If you decide to use this option, it''s recommended to test the resulting memory cost for your application with different settings to determine an acceptable trade-off between PSO creation performance and memory overhead.

### Performance

By default, Unreal Engine uses a PSO precaching thread pool to compile the PSO asynchronously. If `r.pso.PrecompileThreadPoolSize` or `r.pso.PrecompileThreadPoolPercentOfHardwareThreads` is set, then the thread pool will be used. Otherwise, PSO compilation falls back to using regular background tasks, which are scheduled with the rest of the engine's workloads.

| Console Variable | Description | Default State |
| --- | --- | --- |
| 
`r.pso.PrecompileThreadPoolSize`

 | 

Sets the exact amount of threads to use in the pool

 | 

0

 |
| 

`r.pso.PrecompileThreadPoolPercentOfHardwareThreads`

 | 

Sets the thread pool size to be a percentage of available hardware threads and creates a thread pool with that size. The default size is 75, which represents 75% of hardware threads.

 | 

75

 |
| 

`r.pso.PrecompileThreadPoolSizeMin`

 | 

The minimum amount of threads to use in the PSO thread pool.

 | 

2

 |
| 

`r.pso.PrecompileThreadPoolSizeMax`

 | 

The maximum amount of threads to use in the PSO thread pool. The default is `INT_Max` for no maximum amount of threads.

 | 

INT\_Max

 |

Additional Notes:

-   With an unbounded amount of max threads in the thread pool it might be possible to run out of system memory while compiling PSOs on systems with a lot of processors but not a lot of memory. Each thread compiling PSOs can use up to 2 Gbs of memory, so limiting this amount might make sense for your project.
    
-   During gameplay, 75 percent of hardware threads might be a lot. Contention with regular foreground threads might be noticeable causing minor frame drops. Increasing this value during loading time, and decreasing it again during gameplay can help, but it might delay the PSO compilation and increase the delayed proxy creation — it shouldn't introduce runtime hitches.
    

You can use the command line argument `-clearPSODriverCache` to force-clear the driver cache, which we recommend for testing the first-time startup experience of your game.

When testing on PCs with a large number of cores, we also recommend limiting the core count to 8, or another typical core count for a consumer-grade PC, using the command line argument `-corelimit=n`, where `n` is the number of cores, and `-processaffinity=n` which will further ensure that Windows will only schedule the game on `n` physical cores. This ensures that you will more accurately replicate the final user experience.

Use the `-clearPSODriverCache` switch consistently for all test runs that assess the smoothness of your game. Without it, hitches may be masked by the PSO cache built by the graphics driver and left over from the previous runs.

## Validation and Tracking

There are several options to validate and track the performance of the PSO precaching system.

You can enable Validation with `r.PSOPrecache.Validation` using the following values:

| Console Variable | Description |
| --- | --- |
| 
0

 | 

Disabled

 |
| 

1

 | 

Lightweight tracking with high-level numbers only. This has minimal performance impact and can be used in shipped titles.

 |
| 

2

 | 

Detailed tracking and logging on PSO precache misses.

 |

When PSO precache validation is active, you can inspect the stats collected using the `stat PSOPrecache` console command.

[![PSO stats displaying onscreen after using stat PSOPrecache](https://dev.epicgames.com/community/api/documentation/image/7fa0512d-6664-447c-8c54-d64a3afd9794?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7fa0512d-6664-447c-8c54-d64a3afd9794?resizing_type=fit)

*The statistics collected by the PSO precaching validation system. Use the stat PSOPrecache console command to view them.*

Stats are split into 3 groups:

| Group | Description |
| --- | --- |
| 
Shader-only PSOs

 | 

These stats only track the used RHI shaders and ignore all the other state information in the PSOs. This is useful to see if at least all the shaders are precached and whether something is missing/wrong with the other render states. Requires `r.PSOPrecache.Validation.TrackMinimalPSOs`.

 |
| 

Minimal PSOs

 | 

Contains the shaders and all the render stats and vertex element information except render target information. Render target information is only available for validation at draw time, but the minimal PSO stats can be updated and checked during MeshDrawCommand building. Requires `r.PSOPrecache.Validation.TrackMinimalPSOs`.

 |
| 

Full PSOs

 | 

The complete runtime-required PSO state used by the graphics API. This is the same as Minimal PSOs but with extra render target information.

 |

For each group, the following parameters are tracked:

| Parameter | Description |
| --- | --- |
| 
Missed

 | 

The number of PSOs that were not precached, but should have been because they were needed at draw or dispatch time. Possible reasons: wrong shader, render target state, vertex attributes, render target information.

 |
| 

Untracked

 | 

The number of PSOs for which precaching is not enabled. Possible reasons: validation disabled, global material, unsupported vertex factory, unsupported mesh pass processor type. In shipping builds, where certain debug information is not available, untracked PSOs will show up as missed instead.

 |
| 

Hit

 | 

The number of PSOs used at runtime that were successfully precached.

 |
| 

Too late

 | 

The number of PSOs that were queued for precaching, but were not compiled in time for when they were needed.

 |
| 

Used

 | 

The number of PSOs used at runtime (sum of all the above).

 |
| 

Precached

 | 

The number of PSOs that were precached (but not necessarily used).

 |

The **Shader Pipeline Cache** also gives information about how many actual runtime hitches were detected due to PSO compilation itself. A PSO compilation is marked as a hitch if the compilation took longer than a certain amount of milliseconds for the runtime PSO to be compiled. The default threshold is 20 milliseconds. You can modify this with `r.PSO.RuntimeCreationHitchThreshold`, but you should keep it as small as possible.

The default value of 20 milliseconds is high because the first hits on the driver cache can take a long time.

## Collect Information on PSO Precaching

You can use the **Log file**, **Visual Studio** debugger and **Unreal Insights** to get more information about PSO precaching and investigate why certain PSOs may still cause hitches at runtime. Correct PSO precache states will only show up in the log and Insights when PSO validation is enabled (see [Validation and Tracking](https://dev.epicgames.com/documentation/en-us/unreal-engine/pso-precaching-for-unreal-engine) above).

When a PSO miss or Too late is found the UE will print the following information in the log:

C++

```code
`PSO PRECACHING MISS: 		Type:				FullPSO 		PSOPrecachingState:		Missed 		Material:				M_AdvancedSkyDome 		VertexFactoryType:		FLocalVertexFactory 		MDCStatsCategory:		StaticMeshComponent 		MeshPassName:			SkyPass 		Shader Hashes: 			VertexShader:		EC68796503F829FDEACC56B913C4CA86C6AD3C16 			PixelShader:		651BF1ABBAEC0B74C8D2A5E917702A00EF29817B`

```

Expand codeCopy full snippet(24 lines long)

Insights is a handy tool to debug PSO precaching. Adding the timers PSOPrecache: Missed and PSOPrecache: Too Late to the game frame state series gives a handy overview of all hitches caused by PSO compilation over a certain period of time. In the screenshot below there are a few 5 to 10 msec hitches from PSO precaching misses but also a big one of 117 msec which will be noticeable by the player. The other big hitches are not coming from PSO compilation.

[![A PSO precache miss displays in Unreal Insights](https://dev.epicgames.com/community/api/documentation/image/7b877137-4e34-49bc-848e-aa6102aa0067?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7b877137-4e34-49bc-848e-aa6102aa0067?resizing_type=fit)

*Click to enlarge image.*

When zooming in we can see it's coming from the Translucency pass (and the log should have more information about this):

[![Unreal Insights displays a hitch coming from untracked PSOs](https://dev.epicgames.com/community/api/documentation/image/73c4d219-9487-4db7-af07-4b5839f6ca33?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/73c4d219-9487-4db7-af07-4b5839f6ca33?resizing_type=fit)

*Click to enlarge image.*

You can find more detailed information in global PSO validation helper objects. When validation is set to full tracking (`r.PSOPrecache.Validation=2`), it groups numbers by mesh pass processor and vertex factory type, which can help track down where certain misses are coming from. It can also help provide a clearer idea of where all the precached PSOs are coming from, and it can help find outliers which shouldn't precache that many shaders.

While these per-pass and per-vertex factory statistics are not exposed directly, they can be inspected during debugging by navigating the data structures that collect them. They are in `PSOPrecacheValidation.cpp`:

-   `FullPSOPrecacheStatsCollector`
    
-   `ShadersOnlyPSOPrecacheStatsCollector`
    
-   `MinimalPSOPrecacheStatsCollector`
    

The screenshot below shows an example.

[![Stats displayed during debugging](https://dev.epicgames.com/community/api/documentation/image/9c4517ae-00ab-445c-a0cb-c84224efdb48?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9c4517ae-00ab-445c-a0cb-c84224efdb48?resizing_type=fit)

*Click to enlarge image.*

## Extend PSO Precaching with Engine features

This section provides information about how to extend the supporting objects for PSO precaching.

### UPrimitiveComponent

`UPrimitiveComponent` collects all the information needed to set up the PSO initializer. It needs the material instance, vertex factory (with possible vertex element set), and the set of parameters which could influence the final shader or render state used in the `FMeshPassProcessor`.

The parameters are stored in `FPSOPrecacheParams` and the correct default values are set up in `UPrimitiveComponent::SetupPrecachePSOParams`.

The base entry function for PSO precaching is:

C++

`/** Precache all PSOs which can be used by the primitive component */  	ENGINE_API virtual void PrecachePSOs();`

/\*\* Precache all PSOs which can be used by the primitive component \*/ ENGINE\_API virtual void PrecachePSOs();

Copy full snippet(3 lines long)

In most cases, the derived component doesn't need to implement this function, and it can simply override the precache parameter collection function:

C++

```code
`/** 	 * Collect all the data required for PSO precaching  	 */  	struct FComponentPSOPrecacheParams  	{  		EPSOPrecachePriority Priority = EPSOPrecachePriority::Medium;`


```

Expand codeCopy full snippet(21 lines long)

A fully-featured example can be found in `UStaticMeshComponent::CollectPSOPrecacheData`, and a simpler use case can be found in `WaterMeshComponent::CollectPSOPrecacheData`.

### FVertexFactory

A new Vertex Factory needs to flag that it supports PSO precaching using the flag `EVertexFactoryFlags::SupportsPSOPrecaching`, which can be provided with the vertex factory declaration macro `IMPLEMENT_VERTEX_FACTORY_TYPE`.

Then, the vertex factory must implement the following function:

C++

`static void GetPSOPrecacheVertexFetchElements(EVertexInputStreamType VertexInputStreamType, FVertexDeclarationElementList& Elements);`

static void GetPSOPrecacheVertexFetchElements(EVertexInputStreamType VertexInputStreamType, FVertexDeclarationElementList& Elements);

Copy full snippet(1 line long)

`FVertexFactory::GetPSOPrecacheVertexFetchElements` is used during PSO precaching if no explicit vertex element set is provided.

The fixed vertex element set will be valid if the `EVertexFactoryFlags::SupportsManualVertexFetch` flag is set on the vertex factory or if a fixed vertex element set is used in the shader.

If the vertex element list is dependent on the vertex buffer data of the mesh, then the correct set will need to be provided in `FPSOPrecacheVertexFactoryData`. This should happen during `UPrimitiveComponent::CollectPSOPrecacheData`. See `UStaticMeshComponent::CollectPSOPrecacheData` and `FLocalVertexFactory::GetVertexElements` for examples.

### FMeshPassProcessor

The mesh pass processor has to implement the following function to collect all the PSOs which can be used when drawing a certain material with the given `FPSOPrecacheParams`:

C++

`virtual void CollectPSOInitializers(const FSceneTexturesConfig& SceneTexturesConfig, const FMaterial& Material, const FPSOPrecacheVertexFactoryData& VertexFactoryData, const FPSOPrecacheParams& PreCacheParams, TArray<FPSOPrecacheData>& PSOInitializers) override {}`

virtual void CollectPSOInitializers(const FSceneTexturesConfig& SceneTexturesConfig, const FMaterial& Material, const FPSOPrecacheVertexFactoryData& VertexFactoryData, const FPSOPrecacheParams& PreCacheParams, TArray<FPSOPrecacheData>& PSOInitializers) override {}

Copy full snippet(1 line long)

The logic is mostly the same as `AddMeshBatch` (and can ideally be partially shared), but while AddMeshBatch is called at MeshDrawCommand building time, the PSO precaching system tries to collect the information a lot sooner (PostLoad of the component).

For a simple example, see `FDistortionMeshProcessor::CollectPSOInitializers` For a more comprehensive example, see `FBasePassMeshProcessor::CollectPSOInitializers`.

### IPSOCollector

Not all material shaders go through a mesh pass processor or have `EMeshPass::Type` defined anymore (such as Hair, Nanite or Ray Tracing dynamic geometry updates). For these it might be needed to derive directly from the base interface instead.

The `IPSOCollector` has a single virtual function which needs to be implemented:

C++

`// Collect all PSO for given material, vertex factory & params 	virtual void CollectPSOInitializers(const FSceneTexturesConfig& SceneTexturesConfig, const FMaterial& Material, const FPSOPrecacheVertexFactoryData& VertexFactoryData, const FPSOPrecacheParams& PreCacheParams, TArray<FPSOPrecacheData>& PSOInitializers) = 0;`

// Collect all PSO for given material, vertex factory & params virtual void CollectPSOInitializers(const FSceneTexturesConfig& SceneTexturesConfig, const FMaterial& Material, const FPSOPrecacheVertexFactoryData& VertexFactoryData, const FPSOPrecacheParams& PreCacheParams, TArray<FPSOPrecacheData>& PSOInitializers) = 0;

Copy full snippet(2 lines long)

The PSO collector also needs to be registered for creation via a global `FRegisterPSOCollectorCreateFunction`. There are a few simple examples in the engine: `FTranslucentLightingMaterialPSOCollector`, `FRayTracingDynamicGeometryPSOCollector`, …

### GlobalPSOCollector

As mentioned earlier in this page, a few global graphic PSOs are precached already at startup time for which we know they can compile runtime permutations. For this, the `GlobalPSOCollector` is used. It is a simplified version of the IPSOCollector. A global `FRegisterGlobalPSOCollectorFunction` object needs to be declared, which provides the global PSO collector function:

C++

`typedef void (*GlobalPSOCollectorFunction)(const FSceneTexturesConfig& SceneTexturesConfig, int32 GlobalPSOCollectorIndex, TArray<FPSOPrecacheData>& PSOInitializers);`

typedef void (\*GlobalPSOCollectorFunction)(const FSceneTexturesConfig& SceneTexturesConfig, int32 GlobalPSOCollectorIndex, TArray<FPSOPrecacheData>& PSOInitializers);

Copy full snippet(1 line long)

See `DeferredLightGlobalPSOCollector` or `RegisterVolumetricFogGlobalPSOCollector` for some examples of how to use these.

## Debug a PSO Precache Miss

To Debug where the above PSO precache miss comes from, you need to use manual debugging in Visual Studio.

Debugging misses on minimal PSO state is straightforward because these can be triggered during MeshDrawCommand building and not at draw time. The final render target information — needed to compute the full PSO — is only available during drawing, which makes it harder to debug.

The function `LogPSOMissInfo` is a convenient place to break with the debugger when a miss occurs at runtime. The call stack and watch window can give more information about the used material, render pass, vertex factory, and the `FPrimitiveSceneProxy`. You can also get information about the `UPrimitiveComponent` using the `ComponentForDebuggingOnly` member. Most of this data is also printed in the log file when it finds a miss (collected in this function).

However, by the time `LogPSOMissInfo` runs, PSO precaching has usually already happened on that component. If you are trying to find out why an incorrect shader or render state was used during precaching for the PSOs of that component, you need to add a breakpoint during PSO precaching for that component and / or material for the given pass.

`r.PSOPrecache.BreakOnMaterialName` is useful to break during PSO precaching when it finds a material with a given name - this can help to find out why certain render state is different when compared to the runtime state. `r.PSOPrecache.BreakOnPassName` and `r.PSOPrecache.BreakOnShaderHash` can also be used to narrow down the problematic PSO. This information can be found in the log, as mentioned above.

`r.PSOPrecache.UseBackgroundThreadForCollection` is useful to disable the background thread tasks for PSO initializer collection to make it easier to track down component information or other state while debugging a PSO precaching miss.

You might also need to check the values of `FPSOPrecacheParams`, because these could also influence the shader and render state used in the PSO.