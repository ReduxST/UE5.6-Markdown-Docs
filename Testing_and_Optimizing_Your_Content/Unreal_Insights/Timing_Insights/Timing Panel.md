# Timing Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-timing-panel-in-unreal-insights-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-timing-panel-in-unreal-insights-for-unreal-engine)  
**Processed:** 2025-06-14 17:02:00

---

The **Timing panel** shows a detailed view of CPU/GPU usage organized into separate tracks for each thread. Each track represents a processing thread and displays a timeline of events. The width of each event indicates how much time the thread spent processing it.

![Default view of the timing panel.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f68118e-eb3a-4571-98d6-21471f5d76e1/main-image.png)

## Selecting Events

Click an event in any of the tracks on the timeline to highlight it in the Timers and Counters panels.

![Several events are selected in the Timers panel. They display in the Main Graph track in the Timing panel.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/294e9d1b-fd5a-4a00-b2c3-8d20adb0f33e/select-events.png)

Double-click an event to highlight that event and any other instances of it. All other events will turn grey. Double-click an instance of that event again to re-highlight all other events.

![Events are highlighted in the timing panel. Unrelated tracks are darkened.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a4a720c-3dd3-41e2-918e-7cb0526c8e9c/example-highlight.png)

## Navigating the Timeline

Click and drag anywhere below the timeline to scroll through the Timing Panel.

Click anywhere inside the Timing Panel and use your mouse scroll wheel to zoom closer or farther out on the timeline. This expands and contracts the range of time that it displays.

## Selecting Time Ranges

To highlight a region of the Timing Panel, click and drag inside the timeline at the top of the panel. All processes within this region display in the Timers and Counters panels.

![A time range is highlighted in the timing panel.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8214abc5-941f-4dbf-853f-4ecd33946c2a/time-range.png)

You can also use the Frames panel to select a time range. Click on a frame within the Frames panel, then Shift-Click a different frame to select the entire region that includes both frames.

## Timing Regions Track

![The timing regions track.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cb7f1d0-b9f2-49a8-bbb3-8d862397ec64/timing-regions.png)

The **Timing Regions** track displays long-duration events emitted by the `TRACE_BEGIN_REGION` and `TRACE_END_REGION` API. This trace data is controlled by the new **Regions** trace channel, which is included in the **Default** preset.

## Main Graph

Click **All Tracks** \> **Main Graph** to display the Main Graph. This graph shows any events you've highlighted in the Timers and Counters panels with an alternate visualization of the time those events are using.

![The main graph track displayed at the top of the timing panel.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/716c0260-465b-4450-a414-def054cba275/main-graph-1.png)

Click in the Main Graph, then hold the Shift key and use your mouse's scroll wheel to scale the graph. This does not zoom in and out on the timeline. Instead, it changes the scale of time on the vertical axis, which can make small time values more readable.

![The man graph track after scaling down to 1 ms.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/548b7b67-31dd-4c08-a138-4a6cdd19ab13/main-graph-2.png)

## Plotting Events

To plot an event in the Main Graph, hold the **Shift** key and click the event in the timeline. It will appear in the main graph with a color code assigned to it. See Plotting Events in the Main Graph section below for more information and options for plotting events.

## Timing Filters

![The timing filter bar.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/292ab9c8-441a-42f3-b14c-552dd3c2f896/filters.png)

The Timing Panel has a list of filters you can use to narrow down what tracks you are displaying.

### All Tracks

Clicking the **All Tracks** dropdown arrow displays a list of all available tracks.

### CPU/GPU

![The dropdown for the CPU and GPU filters.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f330a91-2027-4fc9-8929-b4a68f3bbb80/cpu-gpu-filters.png)

Clicking the **CPU/GPU** dropdown arrow displays theCPU and GPU tracks and thread group options.

### Other

![The dropdown for other filters.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d999558-8d9f-4cd8-9bd2-2bf5c03acb26/other-filters.png)

Clicking the **Other** dropdown arrow displays options for visibility of the **Main Graph**, **File Activity**, **Asset Loading**, and **Frames Tracks**.

### Plugins

![The dropdown for plugin filters.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2101f09a-98db-4a3b-8f93-42f6cad6c851/plugins-filters.png)

Clicking the **Plugins** dropdown arrow displays Tracks and options that are exposed by plugins, including information about **Slate**, **Gameplay**, **Animation**, and **RDG Tracks**.

### How to Use Metadata Filters

When you add a Metadata filter, it provides multiple fields you can fill in with metadata you want to filter for. These fields are as follows:

| **Index** | **Field** | **Description** |
| --- | --- | --- |
| 1 | **Key** | Contains a metadata field. It must be a string value, and it must be an exact match. |
| 2 | **DataType** | The type of the metadata field you want to search for. For example, a string or a float. |
| 3 | **Operator** | The operator you want to apply to the metadata value and the value in the Value text box (see below). Available operators depend on the selected DataType. |
| 4 | **Value** | The value you want to use as the second member of the operator. The inputted value must be compatible with the selected DataType. |

As an example, you can create a metadata filter with the key "AssetPath" with String as youir type and a value containing the string "Pawn."

The second example below shows a combination of a metadata filter with other types of filters. It searches for all timer name events with the name "FRDGBufferPool\_CreateBuffer" that have a metadata field with the key "SizeInBytes" of a type Int, and a value greater than 6500.

You can use the special string \* to display all events that have attached metadata, regardless of key, type, or value.

## View Mode

![The view modes dropdown unfolded.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/384699c6-7a71-4859-b731-e789c4f8be9b/view-modes.png)

The **View Mode** dropdown arrow displays controls for various options for the Timing View.

| **Timing View Option** | **Description** |
| --- | --- |
| **Compact Mode** (*key shortcut: C*) | Toggles compact mode which displays the timing tracks with reduced height supporting tracks. |
| **Auto Hide Empty Tracks** (*key shortcut: V*) | Auto-hides empty tracks without timing events. This option is persistent to the UnrealInsightsSettings.ini file. |
| **Depth Limit** (*key shortcut: X*) \* Unlimited / 4 Lanes / Single Lane | Toggles the display of different CPU depth options. The **X** key can be used as a shortcut to cycle through the different CPU depth options. |
| **Coloring Mode** (CPU Thread tracks) | You can assign a color to CPU / GPU timing events. See Coloring Modes below for more information. |
| **Allow Panning on Screen Edges** | When enabled, panning continues when the mouse cursor reaches the edges of the screen. |

### Coloring Modes

The following coloring modes are available for CPU and GPU thread tracks:

| **Mode** | **Description** |
| --- | --- |
| By Timer Name | Colors CPU/GPU tracks based on the names of the timers associated with them. |
| By Timer ID | Colors CPU/GPU tracks based on the unique IDs of the timers associated with them. |
| By Source File | Colors CPU/GPU tracks based on what file is responsible for the timer. The file name for the selected event is displayed in the lower-right corner of the Timing Panel. The full file name, including its path, is displayed in the tooltip for the timer in the Timers panel. Events with no filename associated with them are colored in black. |
| By Duration | Colors CPU/GPU tracks based on their duration (inclusive time). The color coding for this mode is as follows: |

≥ 10ms : red. ≥ 1ms : yellow. ≥ 100μs : green. ≥ 10μs : cyan. ≥ 1μs : blue. < 1μs : grey. |

## Context Switches

Context Switches are supported on Windows, XB1/XSX, and PS4/PS5 platforms.

**Context Switches** provide additional display options for viewing GPU and CPU threads in the Timing Panel, as well as new options in their context menus. However, this functionality is not enabled by default. To enable the **ContextSwitch** trace channel, add `-trace=default,contextswitch` in the command line for running Unreal Editor or your application. For example:

Command Line

```
	`MyGame.exe -trace=default,ContextSwitch -tracehost=1.2.3.4`
Copy full snippet
```
MyGame.exe -trace=default,ContextSwitch -tracehost=1.2.3.4

On Windows, depending on your user permission settings, you need to run the command line or your application as an Administrator for the ContextSwitch channel to take effect.

Once you have recorded a trace session with this channel active, open your trace file in Unreal Insights. If a session has the ContextSwitch enabled, then the following information is displayed in the Timing Insights view:

See the [Context Switches](/documentation/en-us/unreal-engine/context-switches-in-unreal-engine-5) page for more information.

## Tasks

To record and view **Task** information, add `task` to the list of tracks in the -trace parameter when you run Unreal Editor or your application from a command line. For example:

```

`D:\EpicGames\UE_5.4\Engine\Binaries\Win64\UnrealEditor.exe -trace=default,task -tracehost=127.0.0.1`

Copy full snippet
```
D:\\EpicGames\\UE\_5.4\\Engine\\Binaries\\Win64\\UnrealEditor.exe -trace=default,task -tracehost=127.0.0.1

When Task support is enabled, task events will appear in the timeline. Additionally, the **Other** dropdown will include a new sub-menu for tasks. The options in this sub-menu toggle which relationships between tasks display in the timing panel, which can assist with tracking the flow of logic between tasks.

![Example of tasks displayed in the Timing panel.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7832534-1d24-4dc2-8e05-592c6f9286c3/tasks.png)

See the [Task Graph Insights](/documentation/en-us/unreal-engine/task-graph-insights-in-unreal-engine-5) page for more information.