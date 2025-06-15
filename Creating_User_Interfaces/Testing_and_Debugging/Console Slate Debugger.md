# Console Slate Debugger

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/console-slate-debugger-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-slate-debugger-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:07

---

While developing the user-interface (UI) for applications, UI developers sometimes need to debug Slate, which is where the **Console Slate Debugger** can help. Console Slate Debugger hooks into the available systems in [FSlateDebugging](/documentation/en-us/unreal-engine/API/Runtime/SlateCore/Debugging/FSlateDebugging) to print internal Slate data. Additionally, as the UI focus changes (or attempts to change), developers will need to know what system is handling those focus updates.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5cd2e01-0780-49a8-8803-01c15b1a86a3/slateconsole.png)

Console Slate Debugger

Extensions for Console Slate Debugger include the following:

-   GlobalInvalidation, which helps to identify the widgets responsible for a costly frame.
-   A paint option that displays widgets that were painted in a given frame.
-   An additional routing option to see how the system chooses a widget as the event handler.
-   Additional filter and event console commands.

This page's screenshots are taken from the Lyra Sample Game project. To test SlateDebugger commands in Lyra, use the command `Slate.EnableGlobalInvalidation 1` to enable [Global Invalidation](/documentation/en-us/unreal-engine/invalidation-in-slate-and-umg-for-unreal-engine), as it is not active by default.

## SlateDebugger

While running the project in PIE mode, press the tilde (~) key to open the PIE Console, and type `SlateDebugger`.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0e0f829-ff4d-4c6c-a184-e93b14158c40/slatedebuggerconsole.gif)

SlateDebugger logs are typically written to a `[ProjectName].txt` log file under `[ProjectName]/Saved/Logs`.

### Event Commands

Slate Debugger offers a lot of different commands to pinpoint specific information like enabling or disabling specific logs and filtering events. If more information is needed CaptureStack can also provide the call stack of the triggered event.

| SlateDebugger.Event | Command Description |
| --- | --- |
| **Start** | Alias for `SlateDebugger.Event.Start` that starts the Slate Console Debugger. |
| **Stop** | Alias for `SlateDebugger.Event.Stop` that stops the Slate Console Debugger. |
| **SetInputFilter** | Enables or disables specific input filters. |
| **SetFocusFilter** | Enables or disables specific focus filters. |
| **LogWarning** | Logs warning events. |
| **LogInputEvent** | Logs input events. |
| **LogFocusEvent** | Logs focus events. |
| **LogExecuteNavigationEvent** | Logs execute navigation events. |
| **LogCaptureStateChangeEvent** | Logs cursor state change events. |
| **LogCursorChangeEvent** | Logs cursosr change events. |
| **LogAttemptNavigationEvent** | Logs attempt navigation events. |
| **InputRoutingModeEnabled** | If enabled, outputs the route taken by an input event. |
| **EnableAllInputFilters** | Enables all input filters. |
| **DisableAllInputFilters** | Disables all input filters. |
| **EnableAllFocusFilters** | Enables all focus filters. |
| **DisableAllFocusFilters** | Disables all focus filters. |
| **CaptureStack** | If enabled, captures the stack when there are events. |

### Invalidate Commands

These commands allow you to use the Invalidate command to show on-screen widgets that are invalidated. Each invalidated widget will be highlighted in different colors based on the type of invalidation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ee65f7a-8d5e-42be-a662-79980e7bdbcc/debuggerinvalidate.png)

SlateDebugger.Invalidate displays the state of each widget during the invalidation process.

| SlateDebugger.Invalidate | Command Description |
| --- | --- |
| **Enable** | Starts the Invalidation Widget debug tool and display when widgets invalidate or stop the Invalidation Widget debug tool, depending on the current status. |
| **Start** | Starts the Invalidation Widget debug tool and displays when widgets invalidate. |
| **Stop** | Stops the Invalidation Widget debug tool. |
| **SetInvalidateRootReasonFilter** | 
Enables the Invalidate Widget Reason Filters.

Usage is `SetInvalidateRootReasonFinder [None][ChildOrder][Root][ScreenPosition][Any]`.



 |
| **SetInvalidateWidgetReasonFilter** | 

Enable the Invalidate Root Reason filters.

Usage is `SetInvalidateWidgetReasonFinder [None][ChildOrder][Root][ScreenPosition][Any][None][Layout][Paint][Volatility][ChildOrder][RenderTransform][Visibility][Any]`.



 |
| **ToggleLegend** | Displays the color legend. |
| **ToggleLogInvalidateWidget** | Logs the invalidated widget to the console. |
| **ToggleWidgetNameList** | Displays the name of the invalidated widget. |

### Paint Commands

This command is used to highlight widgets that are painted in each frame. This can be useful to identify widgets that are painted even if they did not change. Note that volatile widgets are painted every frame.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a61414e5-d2bf-4461-8488-a69734275c57/debuggerpaint.png)

SlateDebugger.Paint displays which widgets are re-drawing on the screen.

| SlateDebugger.Paint | Command Description |
| --- | --- |
| **Enable** | Starts the Paint Widget debug tool and display when widgets paint or stop the Paint Widget debug tool, depending on the current status. |
| **Start** | Starts the Paint Widget debug tool and displays when widgets paint. |
| **Stop** | Stops the Paint Widget debug tool. |
| **LogOnce** | Logs the widgets that paint once during the last update |
| **LogWarningIfWidgetIsPaintedMoreThanOnce** | Logs a warning if a widget paints more than once in the same frame. |
| **MaxNumberOfWidgetDisplayedInList** | Displays the maximum number of widgets that will display when `DisplayWidgetNameList` is active. |
| **ToggleWidgetNameList** | Displays painted widget names. |

### Update Commands

This command is used to highlight widgets that are updated more often than needed. Since Widget Update can be overridden or executed in Blueprint, it is a common source of poor performance if the widget code was not designed correctly.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb9b2e35-6716-44a8-957f-90ce725d3adc/debuggerupdate.png)

SlateDebugger.Update displays which widgets are updating with color coded information. This image is set to filter for only Repaint events, which use yellow.

| SlateDebugger.Update | Command Description |
| --- | --- |
| **Enable** | Starts the Update Widget debug tool and displays when widgets update, or stops the Update Widget debug tool, depending on the current status. |
| **Start** | Starts the Update Widget debug tool and display when widgets update. |
| **Stop** | Stops the Update Widget debug tool. |
| **SetInvalidationRootIdFilter** | Only display widgets that are part of an invalidation root. |
| **SetWidgetUpdateFlagsFilter** | 
Logs a warning if a widget paints more than once in the same frame.

Enable or disable specific widget update flags filters. Usage is `SetWidgetUpdateFlagsFilter [None][Tick][ActiveTimer][Repaint][VolatilePaint][Any]`.



 |
| **ToggleLegend** | Displays the color legend. |
| **ToggleUpdateFromPaint** | Displays widgets that do not have an update flag but which are still updated as a side effect of another widget. |
| **ToggleWidgetNameList** | Displays the names of Update Widgets. |