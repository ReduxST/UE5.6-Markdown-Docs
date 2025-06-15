# Stats System Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-stats-system-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-stats-system-overview)  
**Processed:** 2025-06-14 16:57:07

---

The **Stats System** enables you to collect and display performance data so that it can be used to optimize your game.

For help with Stat Commands, type `stat` into the console, or refer to the `PrintStatsHelpToOutputDevice();` method.

## Types

The Stats System supports the following types:

| Stats Type | Description |
| --- | --- |
| **Cycle Counter** | A generic cycle counter used to count the number of cycles during the object's lifetime. |
| **Float/Dword Counter** | A counter that is cleared every frame. |
| **Float/Dword Accumulator** | A counter that is not cleared every frame, being a persistent stat that can be reset. |
| **Memory** | A special type of counter that is optimized for memory tracking. |

## Grouping Stats

Each stat must be grouped, which usually corresponds with displaying the specified stat group. For example, **stat statsystem** displays stats' related data.

To define a stat group, use one of the following methods:

| Method | Description |
| --- | --- |
| `DECLARE_STATS_GROUP(GroupDesc, GroupId, GroupCat)` | Declares a stats group that is enabled by default. |
| `DECLARE_STATS_GROUP_VERBOSE(GroupDesc, GroupId, GroupCat)` | Declares a stats group that is disabled by default. |
| `DECLARE_STATS_GROUP_MAYBE_COMPILED_OUT(GroupDesc, GroupId, GroupCat)` | Declares a stats group that is disabled by default and which may be stripped by the compiler. |

Where:

-   `GroupDesc` is a text description of the group
-   `GroupId` is a `UNIQUE` id of the group
-   `GroupCat` is reserved for future use
-   `CompileIn`, the compiler may strip it out if it is set to true

Depending on the usage scope, grouping can be done in the source or header file.

### Example Usage

```
	`DECLARE_STATS_GROUP(TEXT("Threading"), STATGROUP_Threading, STATCAT_Advanced); 	DECLARE_STATS_GROUP_VERBOSE(TEXT("Linker Load"), STATGROUP_LinkerLoad, STATCAT_Advanced);`

Copy full snippet
```
DECLARE\_STATS\_GROUP(TEXT("Threading"), STATGROUP\_Threading, STATCAT\_Advanced); DECLARE\_STATS\_GROUP\_VERBOSE(TEXT("Linker Load"), STATGROUP\_LinkerLoad, STATCAT\_Advanced);

## Declaring and Defining Stats

Now, you can declare and define a stat, but before you do, note that a stat can be used in:

-   Only one cpp file
-   The function scope
-   The module scope
-   The whole project

### For a Single File

For the scope of a single file, you must use one of the following methods, depending on the stat type:

| Method | Description |
| --- | --- |
| `DECLARE_CYCLE_STAT(CounterName, StatId, GroupId)` | Declares a cycle counter stat. |
| `DECLARE_SCOPE_CYCLE_COUNTER(CounterName, StatId, GroupId)` | Declares a cycle counter stat and uses it at the same time. Additionally, it is limited to one function scope. |
| `QUICK_SCOPE_CYCLE_COUNTER(StatId)` | Declares a cycle counter stat that will belong to a stat group named 'Quick'. |
| `RETURN_QUICK_DECLARE_CYCLE_STAT(StatId, GroupId)` | Returns a cycle counter, and is sometimes used by a few specialized classes. |
| `DECLARE_FLOAT_COUNTER_STAT(CounterName, StatId, GroupId)` | Declares a float counter, and is based on the double type (8 bytes). |
| `DECLARE_DWORD_COUNTER_STAT(CounterName, StatId, GroupId)` | Declares a dword counter, and is based on the qword type (8 bytes). |
| `DECLARE_FLOAT_ACCUMULATOR_STAT(CounterName, StatId, GroupId)` | Declares a float accumulator. |
| `DECLARE_DWORD_ACCUMULATOR_STAT(CounterName, StatId, GroupId)` | Declares a dword accumulator. |
| `DECLARE_MEMORY_STAT(CounterName, StatId, GroupId)` | Declares a memory counter the same as a dword accumulator, but it will be displayed with memory specific units. |
| `DECLARE_MEMORY_STAT_POOL(CounterName, StatId, GroupId, Pool)` | Declares a memory counter with a pool. |

### For Multiple Files

If you want to have stats accessible to the whole project (or for a wider range of files) you need to use extern version. These methods are the same as the previously mentioned but with `_EXTERN` and the end of the name:

`DECLARE_CYCLE_STAT_EXTERN(CounterName, StatId, GroupId, API)` `DECLARE_FLOAT_COUNTER_STAT_EXTERN(CounterName, StatId, GroupId, API)` `DECLARE_DWORD_COUNTER_STAT_EXTERN(CounterName, StatId, GroupId, API)` `DECLARE_FLOAT_ACCUMULATOR_STAT_EXTERN(CounterName, StatId, GroupId, API)` `DECLARE_DWORD_ACCUMULATOR_STAT_EXTERN(CounterName, StatId, GroupId, API)` `DECLARE_MEMORY_STAT_EXTERN(CounterName, StatId, GroupId, API)` `DECLARE_MEMORY_STAT_POOL_EXTERN(CounterName, StatId, GroupId, Pool, API)`

Then in the source file, you need to define these stats with the following, which defines stats that are declared with `_EXTERN`:

Where:

-   `CounterName` is a text description of the stat
-   `StatId` is a `UNIQUE` id of the stat
-   `GroupId` is the id of the group that the stat will belong to, the `GroupId` from `DECLARE_STATS_GROUP*`
-   `Pool` is a platform-specific memory pool
-   `API` is the `*_API` of a module, and it can be empty if the stat will only be used in that module

## Examples

## Custom Memory Stats with Pools

First you need to add a new pool to `enum EMemoryCounterRegion`, which can be global or platform specific:

```
	`enum EMemoryCounterRegion 	{ 		MCR_Invalid,		// not memory 		MCR_Physical,		// main system memory 		MCR_GPU,			// memory directly a GPU (graphics card) 		MCR_GPUSystem,		// system memory directly accessible by a GPU 		MCR_TexturePool,	// pre-sized texture pools 		MCR_MAX 	};`

Copy full snippet
```
enum EMemoryCounterRegion { MCR\_Invalid, // not memory MCR\_Physical, // main system memory MCR\_GPU, // memory directly a GPU (graphics card) MCR\_GPUSystem, // system memory directly accessible by a GPU MCR\_TexturePool, // pre-sized texture pools MCR\_MAX };

The following is an example that will allow using the pools everywhere (see `CORE_API`).

The pool name must start with `MCR_`.

### Header File Sample

```
	`DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Physical Memory Pool [Physical]"), MCR_Physical, STATGROUP_Memory, FPlatformMemory::MCR_Physical, CORE_API); 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("GPU Memory Pool [GPU]"), MCR_GPU,STATGROUP_Memory, FPlatformMemory::MCR_GPU, CORE_API); 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Texture Memory Pool [Texture]"), MCR_TexturePool, STATGROUP_Memory, FPlatformMemory::MCR_TexturePool,CORE_API);`

Copy full snippet
```
DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Physical Memory Pool \[Physical\]"), MCR\_Physical, STATGROUP\_Memory, FPlatformMemory::MCR\_Physical, CORE\_API); DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("GPU Memory Pool \[GPU\]"), MCR\_GPU,STATGROUP\_Memory, FPlatformMemory::MCR\_GPU, CORE\_API); DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Texture Memory Pool \[Texture\]"), MCR\_TexturePool, STATGROUP\_Memory, FPlatformMemory::MCR\_TexturePool,CORE\_API);

### Source File Sample

```
	`DEFINE_STAT(MCR_Physical); 	DEFINE_STAT(MCR_GPU); 	DEFINE_STAT(MCR_TexturePool);  	// This is a pool, so it needs to be initialized - typically in F*PlatformMemory::Init(). 	SET_MEMORY_STAT(MCR_Physical, PhysicalPoolLimit); 	SET_MEMORY_STAT(MCR_GPU, GPUPoolLimit); 	SET_MEMORY_STAT(MCR_TexturePool, TexturePoolLimit);  	// Now that we have pools, we can set up memory stats for them.  	// The following are accessible everywhere. 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Index buffer memory"), STAT_IndexBufferMemory, STATGROUP_RHI, FPlatformMemory::MCR_GPU, RHI_API); 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Vertex buffer memory"), STAT_VertexBufferMemory, STATGROUP_RHI, FPlatformMemory::MCR_GPU, RHI_API); 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Structured buffer memory"), STAT_StructuredBufferMemory,STATGROUP_RHI, FPlatformMemory::MCR_GPU, RHI_API); 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Pixel buffer memory"), STAT_PixelBufferMemory, STATGROUP_RHI, FPlatformMemory::MCR_GPU, RHI_API);  	// The following are only accessible in the module where they were defined. 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Pool Memory Size"), STAT_TexturePoolSize, STATGROUP_Streaming, FPlatformMemory::MCR_TexturePool, ); 	DECLARE_MEMORY_STAT_POOL_EXTERN(TEXT("Pool Memory Used"), STAT_TexturePoolAllocatedSize, STATGROUP_Streaming, FPlatformMemory::MCR_TexturePool, );  	// And the last thing, we need to update the memory stats.  	// Increases the memory stat by the specified value. 	INC_MEMORY_STAT_BY(STAT_PixelBufferMemory,NumBytes); 	// Decreases the memory stat by the specified value. 	DEC_MEMORY_STAT_BY(STAT_PixelBufferMemory,NumBytes); 	// Sets the memory stat by the specified value. 	SET_MEMORY_STAT(STAT_PixelBufferMemory,NumBytes);`

Copy full snippet
```
DEFINE\_STAT(MCR\_Physical); DEFINE\_STAT(MCR\_GPU); DEFINE\_STAT(MCR\_TexturePool); // This is a pool, so it needs to be initialized - typically in F\*PlatformMemory::Init(). SET\_MEMORY\_STAT(MCR\_Physical, PhysicalPoolLimit); SET\_MEMORY\_STAT(MCR\_GPU, GPUPoolLimit); SET\_MEMORY\_STAT(MCR\_TexturePool, TexturePoolLimit); // Now that we have pools, we can set up memory stats for them. // The following are accessible everywhere. DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Index buffer memory"), STAT\_IndexBufferMemory, STATGROUP\_RHI, FPlatformMemory::MCR\_GPU, RHI\_API); DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Vertex buffer memory"), STAT\_VertexBufferMemory, STATGROUP\_RHI, FPlatformMemory::MCR\_GPU, RHI\_API); DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Structured buffer memory"), STAT\_StructuredBufferMemory,STATGROUP\_RHI, FPlatformMemory::MCR\_GPU, RHI\_API); DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Pixel buffer memory"), STAT\_PixelBufferMemory, STATGROUP\_RHI, FPlatformMemory::MCR\_GPU, RHI\_API); // The following are only accessible in the module where they were defined. DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Pool Memory Size"), STAT\_TexturePoolSize, STATGROUP\_Streaming, FPlatformMemory::MCR\_TexturePool, ); DECLARE\_MEMORY\_STAT\_POOL\_EXTERN(TEXT("Pool Memory Used"), STAT\_TexturePoolAllocatedSize, STATGROUP\_Streaming, FPlatformMemory::MCR\_TexturePool, ); // And the last thing, we need to update the memory stats. // Increases the memory stat by the specified value. INC\_MEMORY\_STAT\_BY(STAT\_PixelBufferMemory,NumBytes); // Decreases the memory stat by the specified value. DEC\_MEMORY\_STAT\_BY(STAT\_PixelBufferMemory,NumBytes); // Sets the memory stat by the specified value. SET\_MEMORY\_STAT(STAT\_PixelBufferMemory,NumBytes);

## Regular Memory Stats Without Pools

```
	`DECLARE_MEMORY_STAT(TEXT("Total Physical"), STAT_TotalPhysical, STATGROUP_MemoryPlatform); 	DECLARE_MEMORY_STAT(TEXT("Total Virtual"), STAT_TotalVirtual, STATGROUP_MemoryPlatform); 	DECLARE_MEMORY_STAT(TEXT("Page Size"), STAT_PageSize, STATGROUP_MemoryPlatform); 	DECLARE_MEMORY_STAT(TEXT("Total Physical GB"), STAT_TotalPhysicalGB, STATGROUP_MemoryPlatform);`

Copy full snippet
```
DECLARE\_MEMORY\_STAT(TEXT("Total Physical"), STAT\_TotalPhysical, STATGROUP\_MemoryPlatform); DECLARE\_MEMORY\_STAT(TEXT("Total Virtual"), STAT\_TotalVirtual, STATGROUP\_MemoryPlatform); DECLARE\_MEMORY\_STAT(TEXT("Page Size"), STAT\_PageSize, STATGROUP\_MemoryPlatform); DECLARE\_MEMORY\_STAT(TEXT("Total Physical GB"), STAT\_TotalPhysicalGB, STATGROUP\_MemoryPlatform);

Or, if you prefer, you can `DECLARE_MEMORY_STAT_EXTERN` in the header file and then `DEFINE_STAT` in the source file.

Updating the memory stats is done the same way as in the version with pools.

## Performance Data Using Cycle Counters

First, you need to add cycle counters:

```
	`DECLARE_CYCLE_STAT(TEXT("Broadcast"), STAT_StatsBroadcast, STATGROUP_StatSystem); 	DECLARE_CYCLE_STAT(TEXT("Condense"), STAT_StatsCondense, STATGROUP_StatSystem);`

Copy full snippet
```
DECLARE\_CYCLE\_STAT(TEXT("Broadcast"), STAT\_StatsBroadcast, STATGROUP\_StatSystem); DECLARE\_CYCLE\_STAT(TEXT("Condense"), STAT\_StatsCondense, STATGROUP\_StatSystem);

Or, you can `DECLARE_CYCLE_STAT_EXTERN` in the header file and then `DEFINE_STAT` in the source file.

Now, you can grab the performance data:

```
	`Stats::Broadcast() 	{ 		SCOPE_CYCLE_COUNTER(STAT_StatsBroadcast); 		// ... 		// a piece of code 		// ... 	}`

Copy full snippet
```
Stats::Broadcast() { SCOPE\_CYCLE\_COUNTER(STAT\_StatsBroadcast); // ... // a piece of code // ... }

Sometimes, you do not want to grab the stats every time the function is called, so you can use a conditional cycle counter — it is not very common, but it may be useful:

```
	`Stats::Broadcast(bool bSomeCondition) 	{  		CONDITIONAL_SCOPE_CYCLE_COUNTER(STAT_StatsBroadcast,bSomeCondition); 		// ... 		// a piece of code 		// ... 	}`

Copy full snippet
```
Stats::Broadcast(bool bSomeCondition) { CONDITIONAL\_SCOPE\_CYCLE\_COUNTER(STAT\_StatsBroadcast,bSomeCondition); // ... // a piece of code // ... }

If you want to grab the performance data from one function, you can use the following construction:

```
	`Stats::Broadcast(bool bSomeCondition) 	{ 		DECLARE_SCOPE_CYCLE_COUNTER(TEXT("Broadcast"), STAT_StatsBroadcast, STATGROUP_StatSystem); 		// ... 		// a piece of code 		// ... 	}`

Copy full snippet
```
Stats::Broadcast(bool bSomeCondition) { DECLARE\_SCOPE\_CYCLE\_COUNTER(TEXT("Broadcast"), STAT\_StatsBroadcast, STATGROUP\_StatSystem); // ... // a piece of code // ... }

You can also do the following:

```
	`Stats::Broadcast(bool bSomeCondition) 	{ 		QUICK_SCOPE_CYCLE_COUNTER(TEXT("Stats::Broadcast")); 		// ... 		// a piece of code 		// ... 	}`

Copy full snippet
```
Stats::Broadcast(bool bSomeCondition) { QUICK\_SCOPE\_CYCLE\_COUNTER(TEXT("Stats::Broadcast")); // ... // a piece of code // ... }

This is mostly used for temporary stats.

All of the previously mentioned cycle counters are used to generate the hierarchy so that you can get more detailed information about performance data. However, there is also the option of setting a flat cycle counter:

```
	`Stats::Broadcast(bool bSomeCondition) 	{ 		const uint32 BroadcastBeginTime = FPlatformTime::Cycles(); 		// ... 		// a piece of code 		// ... 		const uint32 BroadcastEndTime = FPlatformTime::Cycles(); 		SET_CYCLE_COUNTER(STAT_StatsBroadcast, BroadcastEndTime-BroadcastBeginTime); 	}`

Copy full snippet
```
Stats::Broadcast(bool bSomeCondition) { const uint32 BroadcastBeginTime = FPlatformTime::Cycles(); // ... // a piece of code // ... const uint32 BroadcastEndTime = FPlatformTime::Cycles(); SET\_CYCLE\_COUNTER(STAT\_StatsBroadcast, BroadcastEndTime-BroadcastBeginTime); }

## Performance Data Using GetStatId

A few tasks implemented in Unreal Engine use a different approach in terms of getting the performance data. They implement method `GetStatId()`, and if there is no `GetStatId()`, the code will not compile.

Here is an example:

```
	`class FParallelAnimationCompletionTask 	{ 		// ... 		// a piece of code 		// ... 		FORCEINLINE TStatId GetStatId() const 		{ 			RETURN_QUICK_DECLARE_CYCLE_STAT(FParallelAnimationCompletionTask, STATGROUP_TaskGraphTasks); 		} 		// ... 		// a piece of code 		// ... 	};`

Copy full snippet
```
class FParallelAnimationCompletionTask { // ... // a piece of code // ... FORCEINLINE TStatId GetStatId() const { RETURN\_QUICK\_DECLARE\_CYCLE\_STAT(FParallelAnimationCompletionTask, STATGROUP\_TaskGraphTasks); } // ... // a piece of code // ... };

## Logging Performance Data

If you just want to log performance data, we provide the following functionality:

### Method

The following method captures the time (passed in seconds), and adds delta time to the variable that is passed in:

`SCOPE_SECONDS_COUNTER(double& Seconds)`

#### Code Sample

```
	`Stats::Broadcast() 	{ 		double ThisTime = 0; 		{ 	       SCOPE_SECONDS_COUNTER(ThisTime); 	  		// ... 			// a piece of code 			// ... 		} 		UE_LOG(LogTemp, Log, TEXT("Stats::Broadcast %.2f"), ThisTime); 	}`

Copy full snippet
```
Stats::Broadcast() { double ThisTime = 0; { SCOPE\_SECONDS\_COUNTER(ThisTime); // ... // a piece of code // ... } UE\_LOG(LogTemp, Log, TEXT("Stats::Broadcast %.2f"), ThisTime); }

### Utility Class and Methods

| Class | Description |
| --- | --- |
| `FScopeLogTime` | Utility class that logs the time (passed in seconds), adding cumulative stats to passed-in variable, and printing the performance data to the log in the destructor. |
| Method | Description |
| `SCOPE_LOG_TIME(Name, CumulativePtr)` | Using the provided name, prints the performance data and gathers cumulative stats. |
| `SCOPE_LOG_TIME_IN_SECONDS(Name, CumulativePtr)` | The same functionality as SCOPE\_LOG\_TIME, but it prints in seconds. |
| `SCOPE_LOG_TIME_FUNC()` | Using the function name, it prints the performance data, and it cannot be nested. |
| `SCOPE_LOG_TIME_FUNC_WITH_GLOBAL(CumulativePtr)` | The same functionality as SCOPE\_LOG\_TIME\_FUNC, but it gathers cumulative stats. |

#### Code Sample

```
	`double GMyBroadcastTime = 0.0; 	Stats::Broadcast() 	{ 		SCOPE_LOG_TIME("Stats::Broadcast", &GMyBroadcastTime); 		SCOPE_LOG_TIME_IN_SECONDS("Stats::Broadcast (sec)", &GMyBroadcastTime); 		// ... 		// a piece of code 		// ... 	}  	Stats::Condense() 	{ 		SCOPE_LOG_TIME_FUNC(); // The name should be "Stats::Condense()", may differ across compilers 		SCOPE_LOG_TIME_FUNC_WITH_GLOBAL(&GMyBroadcastTime); 		// ... 		// a piece of code 		// ... 	}`

Copy full snippet
```
double GMyBroadcastTime = 0.0; Stats::Broadcast() { SCOPE\_LOG\_TIME("Stats::Broadcast", &GMyBroadcastTime); SCOPE\_LOG\_TIME\_IN\_SECONDS("Stats::Broadcast (sec)", &GMyBroadcastTime); // ... // a piece of code // ... } Stats::Condense() { SCOPE\_LOG\_TIME\_FUNC(); // The name should be "Stats::Condense()", may differ across compilers SCOPE\_LOG\_TIME\_FUNC\_WITH\_GLOBAL(&GMyBroadcastTime); // ... // a piece of code // ... }

## Generic Data Using FLOAT or DWORD Counters

Generally, the first thing you need to do is add your counters, such as the following:

```
	`DECLARE_FLOAT_COUNTER_STAT_EXTERN(STAT_FloatCounter,StatId,STATGROUP_TestGroup, CORE_API); 	DECLARE_DWORD_COUNTER_STAT_EXTERN(STAT_DwordCounter,StatId,STATGROUP_TestGroup, CORE_API); 	DECLARE_FLOAT_ACCUMULATOR_STAT_EXTERN(STAT_FloatAccumulator,StatId,STATGROUP_TestGroup, CORE_API); 	DECLARE_DWORD_ACCUMULATOR_STAT_EXTERN(STAT_DwordAccumulator,StatId,STATGROUP_TestGroup, CORE_API);`

Copy full snippet
```
DECLARE\_FLOAT\_COUNTER\_STAT\_EXTERN(STAT\_FloatCounter,StatId,STATGROUP\_TestGroup, CORE\_API); DECLARE\_DWORD\_COUNTER\_STAT\_EXTERN(STAT\_DwordCounter,StatId,STATGROUP\_TestGroup, CORE\_API); DECLARE\_FLOAT\_ACCUMULATOR\_STAT\_EXTERN(STAT\_FloatAccumulator,StatId,STATGROUP\_TestGroup, CORE\_API); DECLARE\_DWORD\_ACCUMULATOR\_STAT\_EXTERN(STAT\_DwordAccumulator,StatId,STATGROUP\_TestGroup, CORE\_API);

Then, to update and manage your counters, you can use the following methods:

### Methods to Update Counters

| Method | Description |
| --- | --- |
| `INC_DWORD_STAT(StatId)` | Increases a dword stat by 1. |
| `DEC_DWORD_STAT(StatId)` | Decreases a dword stat by 1. |
| `INC_DWORD_STAT_BY(StatId, Amount)` | Increases a dword stat by the specified value. |
| `DEC_DWORD_STAT_BY(StatId, Amount)` | Decreases a dword stat by the specified value. |
| `SET_DWORD_STAT(StatId, Value)` | Sets a dword stat to the specified value. |
| `INC_FLOAT_STAT_BY(StatId, Amount)` | Increases a float stat by the specified value. |
| `DEC_FLOAT_STAT_BY(StatId, Amount)` | Decreases a float stat by the specified value. |
| `SET_FLOAT_STAT(StatId, Value)` | Sets a float stat to the specified value. |

### Helper Methods to Manage Counters

| Method | Description |
| --- | --- |
| `GET_STATID(StatId)` | 
Returns an instance of the `TStatId` of the stat.

This is advanced.



 |
| `GET_STATDESCRIPTION(StatId)` | Returns a description of the stat. |