# Memory Insights

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/memory-insights-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/memory-insights-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:39

---

**Unreal Engine 5** (UE5) expands the capabilities of **Unreal Insights** by adding improved memory tracking and profiling support into its **Memory Insights** feature. Developers can now see more detailed information about memory allocation and deallocation, including the **Low Level Memory (LLM) tags** and callstacks associated with each block of memory at any point in time.

Memory Insights features a query system that can find live allocations at a certain point in time, recognize increases or decreases in memory usage, differentiate short-term and long-term allocations, and find memory leaks.

UE5.4 and later supports memory tracing with callstacks for Android projects.

## Recording a Session

To begin using Memory Insights to record a trace in the memory channel, follow the steps below:

#### Run or Build Unreal Insights

Navigate to **Start** > **Command Prompt** and enter the following:

C++

`Engine\Binaries\Win64\UnrealInsights.exe`

Engine\\Binaries\\Win64\\UnrealInsights.exe

Copy full snippet(1 line long)

Alternatively, you can navigate to your `Engine\Binaries\Win64` folder and double-click to run the `UnrealInsights.exe`.

[![binaries-exe-in-unreal](https://dev.epicgames.com/community/api/documentation/image/6126dabc-764c-4804-8e2a-5b94ecce2caa?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6126dabc-764c-4804-8e2a-5b94ecce2caa?resizing_type=fit)

#### Run Your Game Project with Memory Tracing

Launch the **Command Prompt** from your operating system and run your project sample:

C++

`cd C:\MyEngineInstallLocation\  Samples\Games\MyGameSample\Binaries\Win64\MyGameSample.exe -trace=default,memory`

cd C:\\MyEngineInstallLocation\\ Samples\\Games\\MyGameSample\\Binaries\\Win64\\MyGameSample.exe -trace=default,memory

Copy full snippet(3 lines long)

Recording a session of your project requires the memory trace channel to be active from the beginning of the process. Otherwise, it won't be possible to start tracing allocation events in a late-connect session. Additionally, if you're running a trace on a packaged project, you need to ensure that it is packaged in **Development** mode.

You can use the trace command `metadata` and `assetmetadata` to provide additional filtering options for asset names and class names. For example, you can calculate the cost of memory allocation per asset, or per class name.

C++

`Samples\Games\MyGameSample\Binaries\Win64\MyGameSample.exe -trace=default,memory,metadata,assetmetadata`

Samples\\Games\\MyGameSample\\Binaries\\Win64\\MyGameSample.exe -trace=default,memory,metadata,assetmetadata

Copy full snippet(1 line long)

#### Open your Trace from the Insights Session Browser

Navigate back to the Unreal Insights Session Browser, then double-click your `.utrace` file to open it for analysis in the Unreal Engine **Timing Insights** window. Select **Menu** > **Memory Insights** to open the Memory Insights window.

[![memory-insights-menu-option](https://dev.epicgames.com/community/api/documentation/image/572e6ff0-70a0-46be-b019-0e07878dd911?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/572e6ff0-70a0-46be-b019-0e07878dd911?resizing_type=fit)

### Memory Allocation - Graph Tracks

Unreal Insights captures complete callstacks for each allocation event to provide you with an analysis of your project's allocated memory. The main interface for **Memory Insights** consists of a timeline showing an overview of memory usage during the session.

[![memory-insights-main-view](https://dev.epicgames.com/community/api/documentation/image/3cc2a8fe-e9bb-4ea4-8a0d-7cae949b9399?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3cc2a8fe-e9bb-4ea4-8a0d-7cae949b9399?resizing_type=fit)

The Memory Insights tracker shows information about the number of live allocations in memory. Pictured above is the Main Memory graph along with the Live Allocation and Free Event Count.

The **Main Memory Graph** shows the total amount of tracked memory in your project, including information on each tag that is gathered from the **LLM**. Additionally, there are graphs that display the total number of live allocations:

| Graph Type | Color | Description |
| --- | --- | --- |
| 
Total Allocated Memory

 | 

Blue

 | 

Shows the total amount of memory allocated at each point in time, based on detailed allocation tracking.

 |
| 

Live Allocation Count

 | 

Yellow

 | 

Shows the total number of active allocations at any point in time.

 |
| 

Allocation/Free Event Count

 | 

Green/Orange

 | 

Shows the number of allocation and free events per unit, which is represented as a "slice" of time.

 |

Each of these graphs is based on detailed allocation tracking. They start at a time value of 0 and have a granularity of approximately 1ms. The other graphs with the LLM prefix tags (RenderTargets, SceneRender, UObject) are based on a Low-Level Memory tracking runtime system.

These tags will start tracking several seconds after the session has started and contain a per-frame granularity.

By default we emit one timestamp at each 4096 allocation / free event, You can change this amount if needed by modifying the MarkerSamplePeriod located in `Engine/Source/Runtime/Core/Private/ProfilingDebugging/MemoryAllocationTrace.cpp`. For example, setting this variable to a value of 0 will emit a timestamp after each allocation / free event.

The Memory Insights timeline supports overlaying tracks onto the **Timing View**. When using the Memory Insights view there are four panels available, the **Timing**, **Investigation**, **LLM Tags**, and **Modules** panels.

#### Timing View

You can click **Timing** to toggle the display of the **Timing View** window. Here you can observe and filter the performance data of different tracks relating to memory usage.

[![](https://dev.epicgames.com/community/api/documentation/image/97f66d72-ab47-472a-9010-18127a0ff7c2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/97f66d72-ab47-472a-9010-18127a0ff7c2?resizing_type=fit)

#### Investigation Panel

The **Investigation** panel lets you make different queries about allocations.

[![](https://dev.epicgames.com/community/api/documentation/image/d63cd358-c0e0-4bf4-8478-683d7fe57f1a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d63cd358-c0e0-4bf4-8478-683d7fe57f1a?resizing_type=fit)

#### Low-Level Memory(LLM) Tags

The **LLM Tags** panel controls the visibility of different LLM tags. This data is traced directly from your operating system.

[![](https://dev.epicgames.com/community/api/documentation/image/37a6e411-d07d-46fd-9265-3b3f0a60f62c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/37a6e411-d07d-46fd-9265-3b3f0a60f62c?resizing_type=fit)

You can group **LLM tags**, **Assets**, and **Source files**. Additionally, you can right-click any LLM tag in the **LLM Tags** panel and select **Generate a New Color** or **Edit Color** to customize the color shown in the display.

#### Modules

When callstack symbols are resolved, the result is stored in the cache file. You can view these files by clicking **Modules**. This panel lets you open old trace files and use symbols.

[![](https://dev.epicgames.com/community/api/documentation/image/44f3616f-47c9-4fdf-b552-bc242218f4b9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/44f3616f-47c9-4fdf-b552-bc242218f4b9?resizing_type=fit)

You can observe the columns for the number of of symbols that are **Discovered**, **Cached**, **Resolved**, and **Failed**. List items that failed are highlighted in red, and list items that resolved properly are highlighted in green. Yellow indicates that some of the symbols have resolved and some have failed.

[![](https://dev.epicgames.com/community/api/documentation/image/965be3ee-b82f-4bbc-b5bb-7b4a568d1631?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/965be3ee-b82f-4bbc-b5bb-7b4a568d1631?resizing_type=fit)

The previous runtime implementation of memory tracking is implemented in the **LowLevelMemTracker** class located in the folder `Engine\Source\Runtime\Core\Public\HAL\LowLevelMemTracker.h`. Both the LLM Tags panel and the LLM graphs use data traced directly from this system. The detailed allocation data comes from a separate and specific trace implementation.

Memory Insights contains new querying features and tracked memory allocation information. You can identify blocks of memory that UE5 allocates and frees within certain time windows, before or after a specific moment in time, or check for memory leaks. You can access the query system by going to the **Investigation** tab after opening a trace log.

The status bar at the bottom of the Modules panel provides information about the total number and size of modules.

### Investigation - Allocation Queries

While the timeline provides an overview of memory usage, evaluating how individual allocations behave over a span of time is done by using "queries". A **Query** is defined by a **Rule** and one or more **Timestamps**, such as the labels **A** and **B**.

[![](https://dev.epicgames.com/community/api/documentation/image/215d1498-1443-4afc-9ec7-16f33892f92b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/215d1498-1443-4afc-9ec7-16f33892f92b?resizing_type=fit)

The Investigation panel contains query rules to evaluate data.

The available **Query Rules** are as follows:

| Query Rule | Time Variable | Description |
| --- | --- | --- |
| 
Active Alloc

 | 

A

 | 

Displays all active allocations at time A.

 |
| 

Before

 | 

A

 | 

Displays all allocations before time A.

 |
| 

After

 | 

A

 | 

Displays all allocations after time A.

 |
| 

Decline

 | 

A and B

 | 

Displays all allocations that were allocated before time A and freed between time A and time B.

 |
| 

Growth

 | 

A and B

 | 

Displays all allocations that were allocated between time A and B and freed after time B.

 |
| 

Growth Vs Decline

 | 

A and B

 | 

Identifies both "growth" allocations (allocated between time A and time B and freed after time B) and "decline" allocations (allocated before time A and freed between time A and time B). The decline allocations are changed to have a negative size, so the size aggregation shows variation between A and B. The result of this query is a comparison of what was allocated at time A with what was allocated at time B. A grouping of memory allocations by tags or callstack will show variation (B - A) for each group.

 |
| 

Free Events

 | 

A and B

 | 

Displays all allocations that were freed between time A and B.

 |
| 

Alloc Events

 | 

A and B

 | 

Displays all allocations that were allocated between time A and B.

 |
| 

Short Living Allocs

 | 

A and B

 | 

Displays all allocations that were allocated after time A and freed before time B. This rule can be used to identify allocations that could be stack allocations, meaning that this identifies temporary or short-lived allocations.

 |
| 

Long Living Allocs

 | 

A and B

 | 

Displays all allocations that were allocated before time A and freed after time B.

 |
| 

Memory Leaks

 | 

A, B, and C

 | 

Displays all allocations that were allocated between time A and B and not freed until after time C. This is useful to find memory that would be expected to be released at a given time, for example during a level transition.

 |
| 

Limited Lifetime

 | 

A, B, and C

 | 

Displays all allocations that were allocated between time A and B and freed between time B and C.

 |
| 

Decline of Long Living Allocs

 | 

A, B, and C

 | 

Displays all allocations that were allocated before time A and freed between time B and C.

 |
| 

Specific Lifetime

 | 

A, B, C, and D

 | 

Displays all allocations that were allocated between time A and B and freed between time C and D.

 |

Queries are made by selecting a rule and dragging the labeled markers in the timeline to desired locations, or by specifying a time in the **Investigation** tab.

[![](https://dev.epicgames.com/community/api/documentation/image/afe2d849-fb5b-4ce2-9b01-0b426fd3ffd7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/afe2d849-fb5b-4ce2-9b01-0b426fd3ffd7?resizing_type=fit)

Once the desired rules and times have been selected press the **Run Query** button in the Investigation tab to make the query.

[![](https://dev.epicgames.com/community/api/documentation/image/374ceb02-d5cc-4f4d-bf67-7ee2410931fd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/374ceb02-d5cc-4f4d-bf67-7ee2410931fd?resizing_type=fit)

Depending on the query and data set that is being captured the queries may take a considerable amount of time to execute.

### Allocation Breakdown View

When the query is run a new window appears, upon completion of the query the Alloc table is populated with the result. By default, these results will be displayed in a flat list.

By default, each allocation displays its:

-   **Count**
    
-   **Size**
    
-   **LLM Tag**
    
-   **Function (Alloc)**
    
-   **Alloc Callstack**
    
-   **Function (Free)**
    
-   **Free Callstack**
    

You can display additional parameters by right-clicking on a table heading and setting your desired settings under the **Column Visibility** heading. Additionally, you can hover over the bullet to the left of the allocation to view additional details.

You can view additional details about selected allocations in the status bar at the bottom of the screen, such as total count and memory size.

### Sorting

By clicking on the table headers, you can sort the list by different columns.

[![](https://dev.epicgames.com/community/api/documentation/image/a4de6d63-40ac-45e1-8995-566efcb4b61f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a4de6d63-40ac-45e1-8995-566efcb4b61f?resizing_type=fit)

| Sort Column | Description |
| --- | --- |
| 
Allocation Hierarchy

 | 

Sorts by the hierarchy of the allocation tree.

 |
| 

Allocation Count

 | 

Sorts by the numbers of allocations.

 |
| 

Size

 | 

Sorts by the size of the allocations.

 |
| 

LLM Tag

 | 

Sorts by the LLM tag of the allocations.

 |
| 

Top Function (Callstack)

 | 

Sorts by the resolved top function from the callstack of the allocations.

 |
| 

CallStack Size

 | 

Number of callstack frames.

 |

### Grouping

**Preset** options can be used to group allocations together.

[![](https://dev.epicgames.com/community/api/documentation/image/cf48cbc9-7b24-4da2-9388-216cf351bd13?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cf48cbc9-7b24-4da2-9388-216cf351bd13?resizing_type=fit)

| Preset Option | Description |
| --- | --- |
| 
Default

 | 

Displays the default allocations

 |
| 

Detailed

 | 

Configures the tree view to show detailed allocation information.

 |
| 

Heap

 | 

Investigates how different types of memory are used. See [Multiple Address spaces](https://dev.epicgames.com/documentation/en-us/unreal-engine/memory-insights-in-unreal-engine#multiple-address-spaces) .

 |
| 

Size

 | 

Finds any large allocations quickly.

 |
| 

Tags

 | 

Displays the allocations per system.

 |
| 

Asset (Package)

 | 

Configures the tree view to show a breakdown of allocations by Package and Asset Name metadata.

 |
| 

Class Name

 | 

Configures the tree view to show a breakdown of allocations by their Class name.

 |
| 

Alloc Callstack

 | 

Configures the tree view to show a breakdown of allocations by callstack.

 |
| 

Inverted Alloc Callstack

 | 

Configures the tree view to show a breakdown of allocations by inverted callstack.

 |
| 

Free Callstack

 | 

Configures the tree view to show a breakdown of allocations by free callstack.

 |
| 

Inverted Free Callstack

 | 

Configures the tree view to show a breakdown of allocations by inverted free callstack.

 |
| 

Address (4k Page)

 | 

Groups allocations into 4k aligned memory pages based on their address.

-   You can right-click on items in the context menu and select the action to **Open in Visual Studio**.
    
-   Pressing the **R** key shortcut will expand the critical path in the current tree.
    

 |

Navigating to **Hierarchy** and clicking **All** will open a dropdown menu to change the default **Flat view** into additional, alternative groups.

[![](https://dev.epicgames.com/community/api/documentation/image/8114f974-54d1-4ea2-8aa5-287e0bce0388?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8114f974-54d1-4ea2-8aa5-287e0bce0388?resizing_type=fit)

You can group the Hierarchy from the list of the following options.

| Hierarchy Group | Description |
| --- | --- |
| 
Flat

 | 

Creates a single group that includes all items.

 |
| 

Size

 | 

Groups allocations based on their size.

 |
| 

Tag

 | 

Creates a tree based on tag hierarchy.

 |
| 

Callstack

 | 

Creates a tree based on the Callstack of each allocation.

 |
| 

Inverted Callstack

 | 

Creates a tree based on the Callstack of each allocation.

 |
| 

Heap

 | 

Creates a tree based on Heap. Sub-groups for Allocs and Heaps are available for root heaps.

 |
| 

Unique Values - Event Distance

 | 

Creates a group for each Event Distance value

 |
| 

Unique Values - Start Time

 | 

Creates a group for each Start Time value

 |
| 

Unique Values - End Time

 | 

Creates a group for each End Time value

 |
| 

Unique Values - Duration

 | 

Creates a group for each Duration value

 |
| 

Unique Values - Address

 | 

Creates a group for each Address value

 |
| 

Unique Values - Memory Page

 | 

Creates a group for each Memory Page value

 |
| 

Unique Values - Size

 | 

Creates a group for each Size value

 |
| 

Unique Values - LLM Tag

 | 

Creates a group for each LLM Tag value

 |
| 

Unique Values - Asset

 | 

Creates a group for each Asset value

 |
| 

Unique Values - Class Name

 | 

Creates a group for each Class Name value

 |
| 

Unique Values - Top Function

 | 

Creates a group for each Top Function value

 |
| 

Unique Values - Top Source File

 | 

Creates a group for each Top Source File value

 |
| 

Unique Values - Callstack Size

 | 

Creates a group for each CallStack Size value

 |
| 

Path Breakdown - LLM Tag

 | 

Creates a tree hierarchy out of the structure of LLM Tag string values.

 |
| 

Path Breakdown - Asset

 | 

Creates a tree hierarchy out of the structure of Asset Tag string values.

 |
| 

Path Breakdown - Top Source File

 | 

Creates a tree hierarchy out of the structure of Top Source File string values.

 |

### Advanced Filtering

The search text box provides a method to quickly filter the result based on the hierarchical node text. The set of allocations produced by the query can be further filtered to isolate a group of allocations, by clicking **Filter Configurator** next to the search text box.

[![](https://dev.epicgames.com/community/api/documentation/image/c11d6ce5-f85b-4693-a9ee-cb0e95f564fe?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c11d6ce5-f85b-4693-a9ee-cb0e95f564fe?resizing_type=fit)

It is possible to build advanced queries using groups and AND/OR keywords.

### Call Stack Symbol Resolving

**Call Stack Symbol Tracing** from your project is accomplished using program counter addresses. In analysis, these addresses need to be resolved to readable strings along with information about the corresponding source files.

This requires that Memory Insights has access to the correct version of the file containing the debug information. either a `.pdb` or `.elf` file (depending on the platform). Insights will search for the correct file according to the following list:

1.  Any new paths entered by the user in this session.
    
2.  Path of the executable (If available on some platforms, this will be compiled into the binary).
    
3.  Paths from the `UE_INSIGHTS_SYMBOLPATH` environment variable. This variable accepts semicolon-separated paths.
    
4.  Paths from `_NT_SYMBOL_PATH`.
    
5.  Paths from the user configuration file.
    

When symbols are resolved, the results are stored in the cache file. You can view these files by clicking the **Modules** panel. You can then open these files by right-clicking your selected file and selecting one of the following options from the dropdown menu.

[![](https://dev.epicgames.com/community/api/documentation/image/37997f2c-da69-49bd-a4b4-ac1b509b882f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/37997f2c-da69-49bd-a4b4-ac1b509b882f?resizing_type=fit)

It provides you a method to send the trace file to other users without requiring them to have access to that debug information.

| Load Method | Description |
| --- | --- |
| 
Load symbols from file

 | 

Loads symbols for a module by specifying a file. If successful, it tries to load other failed modules from the same directory.

 |
| 

Load symbols from directory

 | 

Loads symbols for a module by specifying a directory. If successful, it tries to load other failed modules from the same directory.

 |

Symbol resolving is currently available on Win64, XB1/XSX, PS4/PS5 and Switch.

### Multiple Address Spaces

Memory tracing tracks memory in different **heaps**. Conceptually, any allocation must belong to a **root heap**, representing one type of memory. For example, on desktop platforms, one root heap is the system memory and the other is the video memory on the graphics card. Each root heap has its own address space. Under each root heap, heap allocations are made that can host allocations. Usually, this means virtual memory allocations which back up allocations, however, block-style allocators can also be represented with heap allocations. This provides the investigation of the use of those blocks of memory.

### Export Snapshot

You can export memory allocations as a `.csv` or `.tsv` file by right-clicking and selecting **Export Snapshot** from the context menu.