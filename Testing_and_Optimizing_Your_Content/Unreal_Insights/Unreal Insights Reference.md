# Unreal Insights Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-insights-reference-in-unreal-engine-5](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-insights-reference-in-unreal-engine-5)  
**Processed:** 2025-06-14 16:57:29

---

## Trace Channels

Trace is capable of emitting large amounts of data. Channels provide you with control of the data rate when tracing. Each event type is tied to one or more channels, if the required channels are not enabled then the event will not be emitted to the trace stream.

Channel presets groups many channels and provides scenario-based entry points. Users can define their own presets using config files added to the \[Trace.ChannelPresets\] category.

Available trace channels are included in the table below. You can observe a list of channels that include details on each Channel's **File Path**, **Supported Platforms** and **Notes**:

The plural forms of the name are automatically deduced, "bookmark" and "bookmarks" are treated identically.

| Channel | Notes | Supported Platforms | File Path |
| --- | --- | --- | --- |
| **Animation** | Animation Insights(GameplayInsights/RewindDebugger) plugin. |   | `Runtime\Engine\Private\Animation\AnimTrace.cpp` |
| **AssetLoadTime** | Named CPU timers for `UObject::Serialize`. Also toggles on Blueprint names. Requires CPU channel and `-statnamedevents`. | All platforms. | 
`Runtime\Core\Private\Serialization\LoadTimeTrace.cpp` `Runtime\CoreUObject\Private\UObject\LinkerLoad.cpp`



 |
| **Asset Metadata** | Asset Names and Class Names as metadata for memory allocations. Requires Metadata channel. Used by the MemAlloc channel. | 

-   Win64
-   XB1/XSX
-   PS4/PS5
-   Switch
-   Linux



 | `Engine\Source\Runtime\Core\Public\ProfilingDebugging\MetadataTrace.h` |
| **BookMark** | Low frequency markers signifying important transitions, providing a quick overview for users. Such as level loading or engine boot phases. |   | `Runtime\Core\Private\ProfilingDebugging\MiscTrace.cpp` |
| **Callstack** | 

Callstack descriptions. Allows allocations to be associated with callstacks.

Requires Module channel to be enabled for symbol resolution to be possible.



 | 

-   Win64
-   XBox
-   PS4/PS5
-   Switch



 | `Runtime\Core\Private\ProfilingDebugging\CallstackTrace.cpp` |
| **Concert** | Concert plugin. |   | `Plugins\Developer\Concert\ConcertMain\Source\ConcertTransport\Private\ConcertLogGlobal.cpp` |
| **ContextSwitch** | Trace context switch events. On Windows, game/editor runtime should be "run as administrator". | 

-   Win64
-   XBox
-   PS4/PS5



 | `Runtime\Core\Private\ProfilingDebugging\PlatformEvents.cpp` |
| **Cook** | Displays named CPU timers specific to cooking. This requires the CPU channel. It will add the "CookByTheBook" and "SaveCookedPackage" cpu timing events (with metadata). |   | `Editor\UnrealEd\Private\Cooker\CookProfiling.h/.cpp` |
| **Counter** | Generic counters. Allows tracing of values (float, integer) over time. Counters Trace API. It also enables the CSV Profiler Trace. |   | `Runtime\Core\Private\ProfilingDebugging\CountersTrace.cpp` |
| **CPU** | 

Named cpu timers.

Additional timers can be added using `-statnamedevents` command line argument.



 |   | `Runtime\Core\Private\ProfilingDebugging\CpuProfilerTrace.cpp` |
| **File** | File I/O trace channel (Open, ReOpen, Read, Write, Close events). | 

-   Win64
-   Mac,
-   XBox
-   PS4.



 | `Runtime\Core\Private\ProfilingDebugging\PlatformFileTrace.cpp` |
| **Frame** | Game and Rendering frames. |   | `Runtime\Core\Private\ProfilingDebugging\MiscTrace.cpp` |
| **GPU** | Named gpu timers. Based on GpuProfiler data. |   | `Runtime\RHI\Private\GpuProfilerTrace.cpp` |
| **LevelSnapshots** | Level Snapshots plugin. |   | `Plugins\VirtualProduction\LevelSnapshots\Source\LevelSnapshots\Private\LevelSnapshotsLog.cpp` |
| **LoadTime** | Asset Loading Insights trace channel. Package load times (specific trace events) + named cpu timers specific to package loading. Requires "cpu" channel. Also adds the "LoadPackageInternal" cpu timing events (with metadata). See usage of SCOPED\_LOADTIMER and SCOPED\_CUSTOM\_LOADTIMER macros. |   | `Runtime\Core\Public\ProfilingDebugging\LoadTimeTracker.h Runtime\Core\Private\Serialization\LoadTimeTrace.cpp` |
| **Log** | Logs Messages. |   | `Runtime\Core\Private\Logging\LogTrace.cpp` |
| **MemAlloc** | Memory allocations. Uses Module and Callstack. | 

-   Win64
-   XBox
-   PS4/PS5
-   Switch



 | `Runtime\Core\Private\ProfilingDebugging\MemoryTrace.cpp` |
| **Memory** | Includes all alloc events, callstacks, and tags. This is equivalent to `-trace=memalloc,callstack,memtag`. |   | `Runtime\Core\Private\ProfilingDebugging\MemoryTrace.cpp` |
| **Memory\_Light** | Includes all alloc events and tags. This is equivalent to `-trace=memalloc,memtag`. |   | `Runtime\Core\Private\ProfilingDebugging\MemoryTrace.cpp` |
| **MemTag** | Memory tag statistics. Traces snapshots of memory usage per tag at regular rate. Relies on LLM subsystem for tracing. Implies "-llm". Available after Init(). |   | `Runtime\Core\Private\HAL\LowLevelMemTracker.cpp` |
| **Messaging** | UDP Messaging plugin. |   | `Plugins\Messaging\UdpMessaging\Source\UdpMessaging\Private\UdpMessagingTracing.cpp` |
| **Metadata** | Support for generic metadata scopes. | All platforms. | `Engine\Source\Runtime\Core\Public\ProfilingDebugging\MetadataTrace.h` |
| **Module** | Module loading information | 

-   Win64
-   XBox
-   PS4/PS5
-   Switch



 | `Runtime\Core\Private\ProfilingDebugging\ModuleDiagnostics.cpp` |
| **Net** | Networking trace channel. Requires -NetTrace=1 (it enables the "Frame" channel) |   | `Runtime\Net\Core\Private\Net\Core\Trace\Reporters\NetTraceReporter.cpp` |
| **NetworkPrediction** | Network Prediction Insights plugin. |   | `Plugins\Runtime\NetworkPrediction\Source\NetworkPrediction\Private\NetworkPredictionTrace.cpp` |
| **Niagara** | Niagara plugin. |   | `Plugins\FX\Niagara\Source\Niagara\Private\NiagaraTrace.cpp` |
| **Object** | GameplayInsights/RewindDebugger plugin. UObject classes, worlds, instances and events. |   | `Runtime\Engine\Private\ObjectTrace.cpp` |
| **ObjectProperties** | GameplayInsights/RewindDebugger plugin. |   | `Plugins\Animation\GameplayInsights\Source\GameplayInsights\Private\ObjectPropertyTrace.cpp` |
| **Physics** | Chaos Visual Debugger. |   | `Runtime\Experimental\Chaos\Private\ChaosVisualDebugger\ChaosVisualDebuggerTrace.cpp` |
| **PoseSearch** | PoseSearch plugin. |   | `Plugins\Experimental\Animation\PoseSearch\Source\Runtime\Private\Trace\PoseSearchTraceLogger.cpp` |
| **RDG** | RDG Insights plugin. |   | `Runtime\RenderCore\Private\RenderGraphTrace.cpp` |
| **Regions** | Long-duration timing events. | All platforms. | `Runtime\Core\Public\ProfilingDebugging\MiscTrace.h` |
| **RenderCommands** | Cpu/Gpu named timers for commands executed on the rendering thread. |   | `Runtime\RenderCore\Private\RenderingThread.cpp` |
| **RHICommands** | Cpu/Gpu named timers for RHI commands. |   | `Runtime\RHI\Private\RHICommandList.cpp` |
| **SaveTime** | Named CPU timers specific to package saving. This requires the CPU channel. Adds cpu timers named with `UPackage_Save_` prefix. See the usage of the SCOPED\_SAVETIMER macro for additional details. |   | `Runtime\CoreUObject\Private\UObject\SavePackage\SavePackageUtilities.h / .cpp` |
| **Screenshot** | Captures screenshots triggered with Trace.Screenshot console command or using the `TRACE_SCREENSHOT()` API. | All platforms. | `Runtime\Core\Public\ProfilingDebugging\MiscTrace.h` |
| **Slate** | Slate Insights plugin. |   | `Runtime\SlateCore\Private\Trace\SlateTrace.cpp` |
| **Stats** | Stats counters. Based on the Stats system. |   | `Runtime\Core\Private\Stats\StatsTrace.cpp` |
| **Task** | Task Graph trace channel. |   | `Runtime\Core\Private\Async\TaskTrace.cpp` |
| **TraceSourceFilters** | Trace Source Filtering plugin. |   | `Plugins\Developer\TraceSourceFiltering\Source\SourceFilteringTrace\Private\SourceFilterTrace.cpp` |
| **VisualLogger** | Visual Logger starts recording to file. |   | `Runtime\Engine\Private\VisualLogger\VisualLoggerTraceDevice.cpp` |

Some plugins or runtime code enables or disables channels automatically, they are listed in the table below:

| Plugin | Channel Description |
| --- | --- |
| Gameplay Insights / Rewind Debugger | Toggles the **Object** channel when Play in Editor (PIE) is started, and toggles **ObjectProperties**, **Animation**, and **Frame** when a recording is started. |
| TraceSourceFiltering | When the plugin is enabled, the **TraceSourceFilters** channel is toggled on. |
| NetworkPrediction | When the plugin is enabled, the **NetworkPrediction** channel is toggled on. |
| PoseSearch | When the plugin is enabled, the **Pose Search** channel is toggled on. |
| Visual Logger | When recording the **Visual Logger** channel is toggled on. |
| \-NetTrace=1 | When enabled from the command line, the **Net** and **Frame** channels are toggled on. |

## Controlling Runtime

### Macros

To get the most out of the many features that ship with **Unreal Insights**, You can customize your project's output with macros and command-line options. Additionally, mouse and keyboard input shortcuts provide users with the capability to navigate Insights windows more efficiently. You can reference the table below to determine which macros you may want to adjust based on the data that you want to see in Unreal Insights:

| Macro name | Default State | Source File | Area Description |
| --- | --- | --- | --- |
| `UE_TRACE_ENABLED` | On | `Engine/Source/Runtime/TraceLog/Public/Trace/Config.h` | Master control for the entire system. |
| `UE_TASK_TRACE_ENABLED` | On | `Engine/Source/Runtime/Core/Public/Async/TaskTrace.h` | Controls tracing of Task Graph events. `-trace=default,task` |
| `LOGTRACE_ENABLED` | On | `Engine/Source/Runtime/Core/Public/Logging/LogTrace.h` | Controls whether log messages are reported to Unreal Insights. `-trace=log` |
| `MISCTRACE_ENABLED` | On | `Engine/Source/Runtime/Core/Public/ProfilingDebugging/MiscTrace.h` | Controls tracing for bookmarks, frames, threads, and thread groups. `-trace=bookmark,frame` |
| `CPUPROFILERTRACE_ENABLED` | On | `Engine/Source/Runtime/Core/Public/ProfilingDebugging/CpuProfilerTrace.h` | Controls tracing for CPU timers and timing events. `-trace=cpu` |
| `LOADTIMEPROFILERTRACE_ENABLED` | On | `Engine/Source/Runtime/CoreUObject/Public/Serialization/LoadTimeTrace.h` | Controls tracing for events related to load assets. `-trace=loadtime` |
| `STATSTRACE_ENABLED` | On | `Engine/Source/Runtime/Core/Public/Stats/StatsTrace.h` | Controls tracing for stats counters. `-trace=stats` |
| `PLATFORMFILETRACE_ENABLED` | On | 
The default enabled behavior only applies for Windows, Mac, and PS4 platforms.

`Engine/Source/Runtime/Core/Public/ProfilingDebugging/PlatformFileTrace.h`



 | Controls tracing for file activity, such as opening, closing, reading, and writing files. -trace=file |
| `PLATFORM_SUPPORTS_PLATFORM_EVENTS` | On | `Engine/Source/Runtime/Core/Private/ProfilingDebugging/PlatformEvents.h` | On for platforms with support for platform events (context switch events). `-trace=ContextSwitch` |
| `GPUPROFILERTRACE_ENABLED` | On | `Engine/Source/Runtime/RHI/Public/GpuProfilerTrace.h` | Controls GPU timers and timing events. `-trace=gpu` |
| `UE_NET_TRACE_ENABLED` | On | `Engine/Source/Runtime/Net/Core/Public/Net/Core/Trace/NetTrace.h` `Engine/Source/Runtime/Net/Core/Public/Net/Core/Trace/Config.h` | Controls tracing of network packet content. `-trace=net` |
| `UE_MEMORY_TAGS_TRACE_ENABLED` | On | `Engine/Source/Runtime/Core/Public/ProfilingDebugging/TagTrace.h` | Enables tracing of tag scopes. If disabled traced allocation will not have an associated tag. `-trace=memtag` |
| `UE_CALLSTACK_TRACE_ENABLED` | On | `Engine/Source/Runtime/Core/Public/ProfilingDebugging/CallstackTrace.h` | Enables tracing of callstacks. If disabled traced allocations will not contain callstacks. `-trace=callstack` |

### Command-Line Options

When combined with macros, the following command-line options enable trace data:

| Command-Line Option | Description |
| --- | --- |
| `-trace` `-trace=<channel1>` | 
Provides you the capability to manage how much trace data to generate by categorizing events into named groups.

For example, `-trace=cpu,frame,bookmark` enables CPU profiler events, frame markers, and bookmarks.

Trace data for enabled channels is cached in the "Always on" buffers.



 |
| `-tracehost=<ip>` | 

Sends a trace to the specified IP address. Will default to a local host address.

To learn about `-tracehost`, refer to the [Unreal Insights](/documentation/en-us/unreal-engine/trace-in-unreal-engine-5).



 |
| `-tracefile, -tracefile =<filename>` | Performs a "WriteTo" file trace control command. This will run the trace default command. |
| `-tracefiletrunc` |   |
| `-tracetailmb= N` | N specifies the size of the trace tail buffer in MiB. The default size of the trace tail buffer is 4 MiB. |
| `-notraceserver` | If specified, the game or editor will not start the local trace server. |
| `-statnamedevents` | logs trace data for stat named events. Can be enabled by `GCycleStatsShouldEmitNamedEvents = 1;` or from calling "Stat NamedEvents" as a console command. |
| `-verbosenamedevents` | logs trace data for verbose named events. Can be enabled by `GCycleStatsShouldEmitVerboseNamedEvents = 1;` or from calling "Stat VerboseNamedEvents" as a console command. An example of a verbose cycle status: "CPU Stall - \[...\]", "Other TaskGraph Stalls", "FQueuedThread::Run.WaitForWork". |

### Console Commands

| Command | Description |
| --- | --- |
| `Trace.Send <Host> [ChannelSet]` | Starts tracing to a trace store. is the IP address or hostname of the trace store. \[ChannelSet\] is an optional comma-separated list of trace channels/presets to be enabled. |
| `Trace.SnapshotSend <Host> <Port>` | Send a snapshot of the current in-memory trace buffer to a trace store. |
| `Trace.File [<File>] [ChannelSet]` | 
Begins tracing events to a file. If a file path is not specified, then the default path directory for the utrace file is: `YourProject/Saved/Profiling`. If a name is not specified, the name of the utrace file is generated automatically based on the current timestamp. Supports Late Connect.

Use Examples:

-   `trace.file [ChannelSet]`paths to `YourProject}/Saved/Profiling/` the `*.utrace. Filename` is generated automatically.
-   `trace.file MyFile.utrace [ChannelSet]` paths to `YourProject/Saved/Profiling/MyFile.utrace`.
-   `trace.file C:/Path/ [ChannelSet]` is an absolute path, the filename is generated automatically.
-   `trace.file Path/ [ChannelSet]` is a relative path to `YourProject/Saved/Profiling/`, the filename is generated automatically.



 |
| `Trace.Start[ChannelSet]` | Keeps the default enabled channels. |
| `Trace.Stop` | Stops tracing profiling events. |
| `Trace.Enable[ChannelSet]` | Enables a set of channels. |
| `Trace.Disable[ChannelSet]` | Disables a set of channels. If no channel set is specified, all channels will be disabled. |
| `Trace.Pause` | Pauses all trace channels currently sending events. |
| `Trace.Resume` | Resumes tracing that was previously paused (re-enables the pushed channels). |
| `Trace.Status` | Prints the trace status to the console. |

## Controlling Unreal Insights

### Command-Line Options

| Command-Line Option | Usage | Description |
| --- | --- | --- |
| `-OpenTraceId` | `-OpenTraceId=id` | Forces Unreal Insights to start analyzing the specified ID in "Viewer mode" |
| `-OpenTraceFile` | `-OpenTraceFile=file.utrace` | Forces Unreal Insights to start analyzing the specified file in "Viewer mode" |
| `-Store` | `-Store=<ip>:port` | 
Connects Browser with specified trace store

`-StoreHost=address` and `-StorePort=port` are also available.



 |
| `-TraceAutoStart` | `-TraceAutoStart=[0|1]` | Start tracing to the local trace server automatically at start if Unreal Insights is running or wait to initiate via console command. Default is on. |
| `-NoTraceThreading` | `-NoTraceThreading` | Disable the trace worker thread. |

## Keyboard Input Shortcuts

All input operations and control references are limited and subject to change.

### Timing Insights Window

The following mouse and keyboard commands help you navigate Timing Insights more efficiently:

#### Frames Panel

| Keyboard Input Shortcut | Function |
| --- | --- |
| **Left mouse click** | 
Select a frame

The timing view centers on the selected frame.



 |
| **Right mouse click** | Open context menu |
| **Left/right mouse drag** | Horizontal zoom |
| **Mouse wheel** | Horizontal zoom |
| **Shift + mouse wheel** | Vertical zoom |

#### Timing Panel

| Input Shortcut | Function |
| --- | --- |
| **Left/right mouse drag** | Horizontal or vertical pan |
| **Ctrl + left/right mouse drag** | Horizontal pan |
| **Shift + left/right mouse drag** | Vertical pan |
| **Mouse wheel** | Zoom |
| **Ctrl + mouse wheel** | Horizontal scroll |
| **Shift + mouse wheel** | Vertical scroll |
| **Right mouse click** | 
Open context menu

Options available for Graph track.



 |
| **Left mouse click on Timing Event** | Select the timing event |
| **Left mouse click on empty space** | Clear selection |
| **Ctrl + double left mouse click** | 

Select time range of selected timing event

Pressing ENTER performs the same function.



 |
| **Left/right mouse drag over Time Ruler** | 

Select time region

Aggregated states automatically update in Timers and Counters views.



 |
| **Ctrl+F** | Toggles the Quick Find menu. |
| **F** | 

Frame the last selection and then alternate between framing the time range or the timing event

The last selection can be a time range or a timing event.



 |
| **G** | Toggle Graph track visibility, showing Game and Rendering frames, including a placeholder for Counter series |
| **Y** | Toggle GPU Timing track visibility |
| **U** | Toggle CPU Timing track visibility |
| **I** | Toggle I/O Overview and Activity track visibility |
| **O** | Toggle visibility of background events for file activities in the I/O Activity track |
| **L** | Toggle Asset Loading track visibility |
| **C** | Switch between normal and compact mode, affecting how timing events are visualized |
| **V** | 

Auto hide empty timelines

Empty timelines are ones without timing events.



 |
| **X** | Chooses the next event depth limit: Single Lane, 4 Lanes, Unlimited. |
| **B** | 

Toggle visibility of bookmarks

Bookmarks display by default.



 |
| **M** | 

Toggle visibility of time markers (all trace logs instead of just bookmarks)

Time markers do not display by default.



 |
| \*\*-/+ | Zoom |
| **Ctrl + left/right/Up/Down arrows** | Horizontal and vertical pan |
| **Left/right/Up/Down arrows** | Select timing event that is its previous or next sibling/parent/largest child |
| **Enter** | 

Select time range of selected timing event

Pressing Ctrl + Double Left Mouse Click performs the same function.



 |

### Networking Insights Window

The following mouse and keyboard commands help you navigate Networking Insights more efficiently:

| Input Shortcut | Function |
| --- | --- |
| **Left mouse click on packet** | Selects the respective packet |
| **Shift + left mouse click on different packet** | Selects a range of packets |
| **Ctrl + A** | Select all packets |
| **Left/right arrows** | Selects previous/next package |
| **Shift + left/right arrows** | Extends selection (multiple packages) toward Left/right side |
| **Ctrl + shift + left/right arrows** | Shrink selection (multiple packages) from Left/right side |
| **Double click an Event** | Highlights all packets containing the event in the Packet Content view while masking out all other events |