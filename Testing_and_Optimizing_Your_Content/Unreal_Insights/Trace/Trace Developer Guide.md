# Trace Developer Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/developer-guide-to-tracing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/developer-guide-to-tracing-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:14

---

**Trace** is a structured logging framework for tracing instrumentation events from a running process. The framework is designed to produce a stream of high-frequency traced events that are self-describing, easily consumed, and easily shared. The modules **TraceLog** and **TraceAnalysis** are the principal modules that constitute the framework.

The major components of **Unreal Insights** are **Trace events**, the **Unreal Trace Server** which records and saves traces from the application, and **Timing Insights** which analyzes and visualizes the data.

![insights-major-components-diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56d71c9f-1932-46de-b6a3-b0c0a288e5d1/diagram.png)

The stored trace sessions are self-descriptive and backward compatible. Trace sessions are stored in `.utrace` files with generated companion data stored in `.ucache` files next to the trace file.

Trace data travels in packets, known as the **Transport**. Each packet starts with an **internal identifier** indicating which thread the events came from and a size. Packets are [**LZ4**\-compressed](https://lz4.org/) unless they are too small to benefit from compression.

## Using Built-in Event Types

Unreal Engine has a range of predefined event types. These types cover common profiling information such as performance timers and memory allocations. Events are exposed by macros or interfaces and are located in the following directory:

-   `Source/Runtime/Core/Public/ProfilingDebugging`

We strongly recommend you use the provided API before implementing your own custom event types. By using the built-in event types, you benefit from the built-in analyzers and visualizations.

### Timers

The most common profiling task is measuring the performance of an application. In `Source/Runtime/Core/Public/ProfilingDebugging/CpuProfilingTrace.h`, you can find the functionality to emit timer events. We recommend you use the macro family `TRACE_CPUPROFILER_EVENT_SCOPE_`, which provides a method to easily measure how long the application spends in a scope:

```
	`// out of scope 	{ 		TRACE_CPUPROFILER_EVENT_SCOPE_STR("Fancy work"); 		// do fancy work in this scope 	} 	// out of scope`
Copy full snippet
```
// out of scope { TRACE\_CPUPROFILER\_EVENT\_SCOPE\_STR("Fancy work"); // do fancy work in this scope } // out of scope

This code sample will produce a "Fancy work" timer that appears in the [Timing Insights](/documentation/en-us/unreal-engine/timing-insights-in-unreal-engine-5) timeline. The example uses a static string. Dynamic strings are supported, but there is extra performance and memory overhead compared to static strings.

Many built-in macros include the `TRACE_CPUPROFILER_EVENT_SCOPE`, for example, `SCOPE_CYCLE_COUNTER`, `QUICK_SCOPE_CYCLE_COUNTER`, and `SCOPED_NAMED_EVENT` (if `-statnamedevents` is set).

### Counters

The `Source/Runtime/Core/Public/ProfilingDebugging/CountersTrace.h` file contains a generic interface for declaring and tracing named values. You can use the interface to track these values over time. The interface supports integer, float, and memory values including common operations (set, increment, decrement).

For example:

```
	`TRACE_DECLARE_INT_COUNTER(AlienBytes, TEXT("Alien Bytes Written")); 	TRACE_DECLARE_INT_COUNTER(AlienHits, TEXT("Alien Hit Count"));  	void SomeFunc(uint32 WriteSize) 	{ 		TRACE_COUNTER_INCREMENT(AlienHits); 		TRACE_COUNTER_ADD(AlienBytes, WriteSize); 	}`
Copy full snippet
```
TRACE\_DECLARE\_INT\_COUNTER(AlienBytes, TEXT("Alien Bytes Written")); TRACE\_DECLARE\_INT\_COUNTER(AlienHits, TEXT("Alien Hit Count")); void SomeFunc(uint32 WriteSize) { TRACE\_COUNTER\_INCREMENT(AlienHits); TRACE\_COUNTER\_ADD(AlienBytes, WriteSize); }

This code sample produces two counters (`AlienHits` and `AlienBytes`) which appear in the [Timing Insight](/documentation/en-us/unreal-engine/timing-insights-in-unreal-engine-5)'s **Counters** tab.

### Memory

**Memory tracing** is implemented as a wrapper for **GMalloc** which covers allocations that are normally made. Additionally, the virtual allocator functions on relevant platforms. However, if you implement your own custom allocators, you can instrument them using the functions located in the `Source/Runtime/Core/Public/ProfilingDebugging/MemoryTrace.h` file.

Memory tracing takes advantage of the [Low-Level Memory (LLM)](/documentation/en-us/unreal-engine/memory-insights-in-unreal-engine) tagging system and implements code with `LLM_SCOPE` events that help allocation tracing to track tags. We recommend using those macros directly since both LLM and Memory tracing can take advantage of them. However, in specific cases the `Source/Runtime/Core/Public/ProfilingDebugging/TagTrace.h` file contains macros to add custom instrumentation for only memory tracing.

### Miscellaneous Utilities

In the `Source/Runtime/Core/Public/ProfilingDebugging/MiscTrace.h` file, you can find a set of utility macros that help with context when profiling. For example, **Frame markers**, and **Bookmarks**. Bookmarks can be helpful to identify important changes in your application at a glance. You can add your own by using the `TRACE_BOOKMARK` macro.

For example:

```
	`int32 OpenInventory() 	{ 		TRACE_BOOKMARK(TEXT("Inventory.Open")); 	}`
Copy full snippet
```
int32 OpenInventory() { TRACE\_BOOKMARK(TEXT("Inventory.Open")); }

Bookmarks display in the timelines when using Unreal Insights, providing you with a visual indication of this change and in the log view for easier searching. Bookmarks are meant to be used for infrequent changes in the game state. If you need a higher frequency, event timers or counters are a better choice.

## Creating Custom Events

If the built-in events are insufficient for your needs, you can implement your own **Custom events**. Custom events provide you a method to define your own custom payload; however, you need to implement analyzers to handle the events and extract the data.

### Defining Events

A trace session is made up of a stream of events. **Events** are statically described in the application and composed of a **logger name**, **event name**, **event flags**, and a number of fields that are defined as follows:

```
	`UE_TRACE_EVENT_BEGIN(LoggerName, EventName[, Flags]) 		UE_TRACE_EVENT_FIELD(Type, FieldName) 		... 	UE_TRACE_EVENT_END()`
Copy full snippet
```
UE\_TRACE\_EVENT\_BEGIN(LoggerName, EventName\[, Flags\]) UE\_TRACE\_EVENT\_FIELD(Type, FieldName) ... UE\_TRACE\_EVENT\_END()

The `EventName` and `FieldName` parameters define the event and specify a field that it should include. Events are grouped by "loggers", a concept that helps to organize events into a namespace and ease subscription when analyzing a Trace stream. The optional `Flags` parameter modifies how events are traced.

#### Event Fields

**Fields** are named and strongly-typed. Field types can be the standard integer or floating-point primitives (such as `uint8`, `uint32`, `float`), as well as arrays and strings:

| **Field type** | **Description** | **Example** |
| --- | --- | --- |
| `uint8`, `uint16`, `uint32`, `uint64` | Common integer types. | `<< FieldName(-10)` |
| `float`, `double` | Common floating-point types. | `<< FieldName(1.0f)` |
| `UE::Trace::Widestring` | Wide strings. | `<< FieldName(Ptr, NumChars*)` |
| `UE::Trace::Ansistring` | ANSI strings. | `<< FieldName(Ptr, NumChars*)` |
| `Type[]` | Arrays. | `<< FieldName(Ptr, NumElements)` |

`NumChars` in the above table refers to the number of characters excluding null terminator.

Fields are written to the stream without padding. There is no support for nested structures or events as fields, but a common pattern is to refer to previous events by embedding a unique **id field** and resolving in analysis.

Events are usually defined at a global scope in a `.cpp` file. If you need to trace events from multiple translation units, you can use the `UE_TRACE_EVENT_BEGIN_EXTERN` and `UE_TRACE_EVEN_BEGIN_DEFINE` pair.

##### Arrays

You can add variable-length fields to a Trace event by defining them as arrays with unspecified sizes.

```
	`UE_TRACE_EVENT_BEGIN(BoniLogger, BerkEvent) 	UE_TRACE_EVENT_FIELD(int32[], DruttField) 	UE_TRACE_EVENT_END()`
Copy full snippet
```
UE\_TRACE\_EVENT\_BEGIN(BoniLogger, BerkEvent) UE\_TRACE\_EVENT\_FIELD(int32\[\], DruttField) UE\_TRACE\_EVENT\_END()

Array-type fields have no storage cost in an event's payload if no data is set on the field. Array data follows the main event's data in the trace stream and is rejoined at analysis time. Tracing an array field only requires a pointer to the array data and an integer count indicating the number of elements in the array.

For example:

```
	`UE_TRACE_LOG(BoniLogger, BerkEvent, UpstairsChannel) 		<< BerkEvent.DruttField(IntPtr, IntNum);`
Copy full snippet
```
UE\_TRACE\_LOG(BoniLogger, BerkEvent, UpstairsChannel) << BerkEvent.DruttField(IntPtr, IntNum);

##### Attachments

Initially, Trace did not support variable length fields. **Attachments** were introduced as opaque binary blobs that the system appends to events. We recommend using Array-type fields instead of attachments because they benefit from being structured and reflected at analysis time.

Attachment support incurs a cost that every logged event has to pay, whereas array-type fields do not. In the future, attachments may become opt-in to optimize away this overhead.

##### Strings

Trace events support string-type fields using the `Trace::AnsiString` or `Trace::WideString` types when declaring event fields with `UE_TRACE_EVENT_FIELD()`.

```
	`UE_TRACE_EVENT_BEGIN(MyLogger, MyEvent) 		UE_TRACE_EVENT_FIELD(Trace::AnsiString, MyFieldA) 		UE_TRACE_EVENT_FIELD(Trace::WideString, MyFieldW) 	UE_TRACE_EVENT_END()`
Copy full snippet
```
UE\_TRACE\_EVENT\_BEGIN(MyLogger, MyEvent) UE\_TRACE\_EVENT\_FIELD(Trace::AnsiString, MyFieldA) UE\_TRACE\_EVENT\_FIELD(Trace::WideString, MyFieldW) UE\_TRACE\_EVENT\_END()

String-type fields are written much the same as primitive-type fields, with a few additional extras; ASCII-type fields will automatically truncate wide strings to 7-bit characters, and an optional string length can be given. This is preferable for performance if string length is already known.

```
	`UE_TRACE_LOG(MyLogger, MyEvent) 		<< MyFieldA(AnAnsiBuffer, [, ExplicitStringLen]) 		<< MyFieldW(WideName)`
Copy full snippet
```
UE\_TRACE\_LOG(MyLogger, MyEvent) << MyFieldA(AnAnsiBuffer, \[, ExplicitStringLen\]) << MyFieldW(WideName)

#### Event Flags

The following table lists the event flags available when you define an event:

| **Event Flag** | **Description** |
| --- | --- |
| `NoSync` | By default, events are synchronized with events being traced on other threads. Events with the `NoSync` flag skip this synchronization. They're smaller and faster to trace at the expense of being uncoordinated with other threads during analysis. |
| `Important` | Marks the event as important. See the [Important Events](/documentation/en-us/unreal-engine/developer-guide-to-tracing-in-unreal-engine#importantevents) section below for more information on normal and important events. `Important` events also require the `NoSync` flag since they are processed out-of-band with normal events. |

##### Normal Events

When you trace an event at a `UE_TRACE_LOG` site, the system writes a header and the event's field values into a buffer that is local to the current thread as **Thread Local Storage (TLS)**. TLS buffers have a small fixed size and link together to form a list. Trace's worker thread traverses the list of buffers, sending event data that has been committed (and is therefore completely visible). The benefit of using TLS is that it avoids conflicts between tracing threads. Order of operations across threads is significant for event types and must be reconstructed when trace data is analyzed, such as memory tracing events where memory addresses can be reused. If synchronization is required for an event, Trace precedes each event with an automically incrementing 24-bit serial number. Events are synchronized by default, but you can use the `NoSync` flag to opt-out of this feature. `NoSync` avoids incurring the associated performance cost and decreases its size, but removes the ability to coordinate with other threads during analysis.

##### Important Events

Tracing can start and stop at any point in the runtime. However, some events are crucial for analysis and are only emitted once during the process lifetime. For example an event describing the processor frequency or events specifying a human readable name for a timer. To be able to emit these events on every new connection, Trace provides a way to mark events as important.

**Important events** are stored in a special buffer which is kept during the process's entire lifetime, which means developers have to consider the memory cost when using this feature.

### Channels

**Channels** in trace help to constrain the stream of events based on the user's interest. This improves CPU and memory usage by only tracing events that are relevant to what the user is trying to observe. You can define a channel with the following syntax:

```
	`UE_TRACE_CHANNEL(ItvChannel);`
Copy full snippet
```
UE\_TRACE\_CHANNEL(ItvChannel);

There is also a `UE_TRACE_CHANNEL_EXTERN` and `UE_TRACE_CHANNEL_DEFINE` pair for more specific use cases. By default, channels are disabled and must be explicitly opted into. Refer to the [Trace](/documentation/en-us/unreal-engine/trace-in-unreal-engine-5) for how to enable channels.

Channels can be combined in the log macro to gate tracing of an event with multiple channels. A `UE_TRACE_LOG(..., ItvChannel|BbcChannel)` will only emit an event if both the **Itv** and **Bbc** channels are enabled.

Channels use the bitwise OR (`|`) operator to create a composite mask, similar to how a bitmask is constructed from different flags.

### Tracing Events

Log an event at runtime using the `UE_TRACE_LOG` macro:

```
	`UE_TRACE_LOG(RainbowLogger, ZippyEvent, ItvChannel) 		<< ZippyEvent.Field0(Value0) 		<< ZippyEvent.Field1(BundleValue) 		<< ZippyEvent.Field2(Data, Num); 		<< ZippyEvent.Field3(String[, Num]);`
Copy full snippet
```
UE\_TRACE\_LOG(RainbowLogger, ZippyEvent, ItvChannel) << ZippyEvent.Field0(Value0) << ZippyEvent.Field1(BundleValue) << ZippyEvent.Field2(Data, Num); << ZippyEvent.Field3(String\[, Num\]);

If the Channel **ItvChannel** is enabled, this adds a 'RainbowLogger.ZippyEvent' event to the Trace stream.

Not all fields need to be written, but there is no delta or run-length compression when tracing events. All defined fields are present, even if no data is written to them. There is no padding between fields. A traced event is essentially analogous to a struct declared with `#pragma pack(1)`. We recommend developers think strategically to use these features to their complete capability.

While `UE_TRACE_LOG` represents a singular point in time, it is sometimes useful to represent a **time range**. `UE_TRACE_LOG_SCOPE` allows an event to be emitted as a start point and an end point. See the [Tracing Important Events](/documentation/en-us/unreal-engine/developer-guide-to-tracing-in-unreal-engine#tracingimportantevents) section for details on how this can be used. The scope allows you to determine which other events occur inside the scope but does not provide timestamps. If you need to correlate with other events using time, you can use `UE_TRACE_LOG_SCOPE_T`.

This system makes heavy use of macros to hide a large amount of boilerplate so that definitions and log sites compile to nothing when Trace is off without requiring developers to use `#if` and `#endif` pairs throughout their code.

#### Tracing Important Events

Tracing important events has some additional requirements. Due to these events being stored in a cache shared across threads, the logging macro needs to know in advance how much variable memory is going to be consumed. For example, consider the following event:

```
	`UE_TRACE_EVENT_BEGIN(BoniLogger, BarkEvent, Important|NoSync) 		UE_TRACE_EVENT_FIELD(WideString, WoofString) 		UE_TRACE_EVENT_FIELD(int64[], DratField) 	UE_TRACE_EVENT_END()`
Copy full snippet
```
UE\_TRACE\_EVENT\_BEGIN(BoniLogger, BarkEvent, Important|NoSync) UE\_TRACE\_EVENT\_FIELD(WideString, WoofString) UE\_TRACE\_EVENT\_FIELD(int64\[\], DratField) UE\_TRACE\_EVENT\_END()

This event will be traced as below:

```
	`void Func(const TCHAR* Woof, const TArray<int64>& Drat) 	{ 		const uint32 WoofLen = FCString::Len(Woof); 		const uint32 WoofSize = WoofLen * sizeof(TCHAR); 		const uint32 DratSize = Drat.Num() * sizeof(int64);  		UE_TRACE_LOG(BoniLogger, BarkEvent, BoniChannel, WoofSize + DratSize) 			<< BarkEvent.WoofString(Woof, WoofLen) 			<< BarkEvent.DratField(Drat.GetData(), Drat.Num()); 	}`
Copy full snippet
```
void Func(const TCHAR\* Woof, const TArray<int64>& Drat) { const uint32 WoofLen = FCString::Len(Woof); const uint32 WoofSize = WoofLen \* sizeof(TCHAR); const uint32 DratSize = Drat.Num() \* sizeof(int64); UE\_TRACE\_LOG(BoniLogger, BarkEvent, BoniChannel, WoofSize + DratSize) << BarkEvent.WoofString(Woof, WoofLen) << BarkEvent.DratField(Drat.GetData(), Drat.Num()); }

Notice that the total size of the variable data is passed to the ellipsis argument of the log macro.

## Analyzing Custom Events

Now that you have defined a new event, enabled the related Channel or Channels, and added at least one log site, you can consume and analyze the events and publish them. We use a pattern of **Analyzers** and **Providers** to do this. Analyzers extract the data from each event and feed it to the corresponding provider, which serves the data to the UI or other output.

Analyzers derive from the **IAnalyzer** interface and implement two primary methods:

-   **OnAnalysisBegin** to subscribe to events.
-   **OnEvent** to receive those subscriptions.

Providers derive from the **IProvider** interface. There are no mandatory methods to implement them, but make sure access to the data in the provider is thread-safe, since the analyzer thread and the UI thread access to the provider is unsynchronized.

Analyzers and providers need to be added to the analyzer session to receive events. A common pattern is to feed a pointer to the provider and to the analyzer on construction:

```
	`FRainbowProvider* RainbowProvider = new FRainbowProvider(Session); 	Session.AddProvider(TEXT("RainbowProvider"), RainbowProvider); 	Session.AddAnalyzer(new FRainbowAnalyzer(Session, RainbowProvider));`
Copy full snippet
```
FRainbowProvider\* RainbowProvider = new FRainbowProvider(Session); Session.AddProvider(TEXT("RainbowProvider"), RainbowProvider); Session.AddAnalyzer(new FRainbowAnalyzer(Session, RainbowProvider));

### Analyzers

Analyzers subscribe to events using the logger name and the name of the events. The subscription interface associates each event type with an user defined index known as **route ID** (usually defined in an enum).

```
	`void FRainbowAnalyzer::OnAnalysisBegin(const FOnAnalysisContext& Context) 	{ 		auto& Builder = Context.InterfaceBuilder; 		Builder.RouteEvent(RouteId_Zippy, "RainbowLogger", "ZippyEvent"); 	}`
Copy full snippet
```
void FRainbowAnalyzer::OnAnalysisBegin(const FOnAnalysisContext& Context) { auto& Builder = Context.InterfaceBuilder; Builder.RouteEvent(RouteId\_Zippy, "RainbowLogger", "ZippyEvent"); }

When analysis encounters an event that the analyzer has subscribed to, the analyzer's OnEvent method is called with the registered route ID. The event context provides methods to extract the data for each **field**, **thread**, and **timing information**. This API reflects the self-describing nature of Trace streams. There is no binary or runtime-code dependency on interpreting Trace streams.

```
	`bool FRainbowAnalyzer::OnEvent(uint16 RouteId, EStyle Style, const FOnEventContext& Context) 	{ 		switch(RouteId) 		{ 			case RouteId_Zippy: 			{ 				uint32 Field0 = Context.EventData.GetValue<uint32>("Field0"); 				FStringView Field3; 				Context.EventData.GetString("Field3", Field3); 				TArrayReader<int64>& Field4 = EventData.GetArray<int64>("Field4"); 				RainbowProvider->AddZippy(Field0, Field3, Field4); 			} 			break; 		} 	}`
Copy full snippet
```
bool FRainbowAnalyzer::OnEvent(uint16 RouteId, EStyle Style, const FOnEventContext& Context) { switch(RouteId) { case RouteId\_Zippy: { uint32 Field0 = Context.EventData.GetValue<uint32>("Field0"); FStringView Field3; Context.EventData.GetString("Field3", Field3); TArrayReader<int64>& Field4 = EventData.GetArray<int64>("Field4"); RainbowProvider->AddZippy(Field0, Field3, Field4); } break; } }

### Writing a Custom Analyzer

If you want to output data in a different way to generate reports or provide a similar need, you can implement a standalone program and use a custom analyzer to extract the events you are interested in, and output the data in the format you require. An example of this can be found in the `FStoreBrowser::UpdateMetadata()` method located in the `\Engine\Source\Developer\TraceInsights\Private\Insights\StoreService\StoreBrowser.cpp` file. In this method we create an analysis context. The analyzer FDiagnosticsSessionAnalyzer is added, which looks for one specific event type ("Session/Session2"). When reading the trace all other events are skipped, and once the session event is found no further processing is needed. The information is used to display the metadata for traces in the session browser.

### Debugging Trace Analysis

The Trace Analysis module provides debugging and logging functionality for the `UE::Trace::IAnalyzer` class and its sub-classes. These macros and their associated logic are defined in `TraceAnalysisDebug.h`. Unreal Engine also provides a standalone command-line tool to debug trace analysis and the contents of `.utrace` files.

#### Trace Analysis Log API

The following table describes the logging macros provided in `Engine\Source\Developer\TraceAnalysis\Public\TraceAnalysisDebug.h`:

| **Macro** | **Values** | **Description** | **Notes** |
| --- | --- | --- | --- |
| `UE_TRACE_ANALYSIS_DEBUG_API` | 
-   0: disabled (default)
-   1: enabled



 | Enable debug API in `UE::Trace::IAnalyzer` class and sub-classes. | Enabling this should not add any impact on analysis performance or behavior. |
| `UE_TRACE_ANALYSIS_DEBUG` | 

-   0: disabled (default)
-   1: enabled



 | Enable debug functionality and logging in Trace Analysis code. | Enabling this can add significant impact on analysis performance and could alter behavior. |
| `UE_TRACE_ANALYSIS_DEBUG_LOG_IMPL` | 

-   1: `printf`
-   2: `printf` with `TAnsiStringBuilder`
-   3: `GLog`
-   4: `FPlatformMisc::LowLevelOutputDebugStringf`



 | Default implementation to use for the `UE_TRACE_ANALYSIS_DEBUG_LOG` API. |   |
| `UE_TRACE_ANALYSIS_DEBUG_LOG` |   | See [Trace Analysis Log API](/documentation/en-us/unreal-engine/developer-guide-to-tracing-in-unreal-engine#traceanalysislogapi) for information. |   |
| `UE_TRACE_ANALYSIS_DEBUG_LEVEL` | 

-   1: minimum
-   2: normal (default)
-   3: verbose
-   4: very verbose



 | Level of trace analysis debug log verbosity. | Only used when `UE_TRACE_ANALYSIS_DEBUG` is enabled. |

The implementation of the `UE_TRACE_ANALYSIS_LOG` API depends on the value of the `UE_TRACE_ANALYSIS_DEBUG_LOG_IMPL` macro.

| **Macro** | **Description** |
| --- | --- |
| `UE_TRACE_ANALYSIS_DEBUG_LOG` | Print a format string to log. |
| `UE_TRACE_ANALYSIS_DEBUG_BeginStringBuilder` | Initialize a `TAnsiStringBuilder`. |
| `UE_TRACE_ANALYSIS_DEBUG_Append` | Append a string to the string builder. |
| `UE_TRACE_ANALYSIS_DEBUG_Appendf` | Append a format string to the string builder. |
| `UE_TRACE_ANALYSIS_DEBUG_AppendChar` | Append a character to the string builder. |
| `UE_TRACE_ANALYSIS_DEBUG_EndStringBuilder` | Print the contents of the string builder. |
| `UE_TRACE_ANALYSIS_DEBUG_ResentStringBuilder` | Reset the string builder. |

#### Trace Analyzer Tool

The **Trace Analyzer** is a standalone command-line tool to debug trace analysis and the content of `.utrace` files. You can find the tool in the directory `Engine\Binaries\PLATFORM` where `PLATFORM` is the platform you are developing on.

The syntax for using Trace Analyzer (on Windows) is:

```
	`TraceAnalyzer.exe <TRACE_FILE> [-o=<OUT_FILE>] [-no_new_event_log] [-no_event_log] [-no_analysis_stats] [-no_event_stats]`
Copy full snippet
```
TraceAnalyzer.exe <TRACE\_FILE> \[-o=<OUT\_FILE>\] \[-no\_new\_event\_log\] \[-no\_event\_log\] \[-no\_analysis\_stats\] \[-no\_event\_stats\]

The parameters are defined in the following table:

| **Parameter** | **Description** |
| --- | --- |
| `<TRACE_FILE>` | The `.utrace` file to use as input to the trace analyzer tool. |
| `-o=<OUT_FILE>` | The output text file for the analysis. Defaults to `stdout` if not specified. |
| `-no_new_event_log` | No new event logging. |
| `-no_event_log` | No event logging. |
| `-no_analysis_stats` | No analysis stats. |
| `-no_event_stats` | No event stats. |

## Thread IDs

The primary thread ID is not the same as the system thread ID, although the system ID is available. This removes the need for special handling to guard against cases where the Operating System might reuse a thread ID. As a result, you may encounter the reuse of system IDs from one thread to the next, but the ID coming from Trace should be unique.

### Unreal Insights Plugins

Generally, the components in Unreal Insights consume and visualize the data in the providers. If you implemented a custom provider, you may need to implement a custom visualization. **SlateInsights** and **RenderGraphInsights** are two example plugins that are distributed with the engine and serve as a reference.

## Going Further

Trace and Unreal Insights are designed to be flexible and extendable for advanced users. Beyond using the Unreal Insights application and implementing plugins, it is possible to use the components in different ways.