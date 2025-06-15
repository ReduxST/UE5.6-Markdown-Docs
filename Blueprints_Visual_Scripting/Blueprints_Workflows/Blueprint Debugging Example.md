# Blueprint Debugging Example

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-debugging-example-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprint-debugging-example-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:33

---

Blueprint debugging is a powerful feature that provides the functionality to pause the execution of a game during Play In Editor(**PIE**) or Simulate In Editor(**SIE**) mode. When debugging, you can step through any graph of a Blueprint or Level Blueprint through the use of Breakpoints.

## Debugging Controls

The Blueprint Debugger provides control over execution of the game during PIE and SIE sessions. The controls become enabled in the [Toolbar](/documentation/en-us/unreal-engine/toolbar-in-the-blueprints-visual-scripting-editor-for-unreal-engine) when the game is running. Different debugging controls appear depending on the type of Blueprint being debugged and the current state of the debugging session. Some controls only become enabled when relevant, such as when a **Breakpoint** is hit.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32fe74bf-9d5e-4166-a455-b797d00a0529/debugging_editor.png)

Both the Debug tab, which can be opened from the Blueprint Editor's window menu, and the Blueprint Debugger will display the context-sensitive debugging buttons when PIE or SIE modes are active.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89a397bf-fdd6-485d-8b14-a57442f57411/blueprint_debugger.png)

## Enable Debugging

To Enable Debugging of a Blueprint, you must first specify the instance of the Blueprint you wish to debug that is in your level.

Inside your Blueprint, click the **Debug Object** drop-down menu, then select the instance you wish to see in the debugger.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e00bb1c5-3ff3-4314-bd1a-ca6212a8794e/debughowto1.png)

Once you have an object selected, you can jump to that object in your level by clicking the magnifying glass icon.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2dd8fc1-93ff-4422-87b1-c44b9ceffab8/debughowto2.png)

When you play in the editor, with your Blueprint up in another window, you should see the pulsating "Active Wires" as your script executes.

![](pulse.gif)

In the example above, there are two Input Axis Events that call a function in Blueprints to add movement to the Pawn's Controller. You can see in the left window that the script executes when the game is launched (as the pulsating wire leaves the red InputAxis Event node and enters the Add Controller input nodes)

## Breakpoints

**Breakpoints** are markers that can be placed on Blueprint graph nodes. When a node with a Breakpoint is about to be executed during PIE or SIE mode, the game will pause and the developer will be taken to the node in the Blueprint Editor's graph view. This provides the opportunity to observe the values of variables and examine or step through the flow of execution within the Blueprint. All Breakpoints for a given Blueprint are displayed in the **Debug tab**, and can be viewed in the Blueprint's graph when selected. To place a Breakpoint on a node, right-click the node and select **Add Breakpoint** from the context menu, at which point a solid, red octagon will appear in the upper-left corner of the node. The Breakpoint can be removed by right-clicking the node again, or by right-clicking the Breakpoint's entry in the Debug tab, and selecting the **Remove Breakpoint** command.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e4c6211-76a8-4bc8-ba78-f52d8502c3ec/activebreakpoint.png "ActiveBreakpoint.png")

This Breakpoint will interrupt the game when the Jump node is executed.

To disable a Breakpoint temporarily without fully removing it, you can right-click on either the Blueprint node itself, or the Breakpoint's entry in the Debug tab, and choose **Disable Breakpoint** from the context menu. A disabled Breakpoint will appear as an outline of a red octagon. Disabled Breakpoints will not execute, but can easily be enabled again. This process is more convenient and less prone to human error than destroying and remaking Breakpoints repeatedly.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df11b31e-06ec-488a-a3d5-814a6665f9d6/inactivebreakpoint.png "InactiveBreakpoint.png")

This Breakpoint has been disabled and currently does nothing, but can easily be enabled again if it is needed.

To enable a disabled Breakpoint, **Right-click** on the node and choose **Enable Breakpoint** or click the icon next to the Breakpoint in the **Debug** tab. This can also be done by **Right-clicking** the Breakpoint in the **Debug** tab and choosing **Enable Breakpoint**. Breakpoints can be created, disabled, enabled, or destroyed at any time, including during a debugging session. Breakpoints are saved in project .ini files, so they will persist between Editor sessions.

If a Breakpoint is placed at an invalid location, it may appear yellow and feature an exclamation point. In some cases, compiling the Blueprint will resolve the issue. If this is not the case, holding the mouse cursor over the Breakpoint icon will reveal an explanation.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9aca88ba-6c55-48c1-b098-8cee2a1a874b/warningbreakpoint.png "WarningBreakpoint.png")

This Breakpoint is invalid and will never be hit. In some cases, recompiling the Blueprint can fix this.

When pausing execution with a Breakpoint, the Editor will highlight and focus the node, and will place a large, red arrow over it.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bc03656-0853-467c-9c62-8cd7e1335bda/breakingonbreakpoint.png "BreakingOnBreakpoint.png")

This Breakpoint has just been hit, pausing execution.

## Watches

**Watches** keep track of the value of Blueprint node pins for quick reference during debugging sessions. A pin holds the value that was computed on the most recent time the node containing the pin executed. To place a Watch on a pin, right-click the pin's name in the Blueprint Graph and select **Watch this value** from the context menu. Pins that you are already watching will replace **Watch this value** with **Stop watching this value** in the context menu.

Pins whose nodes have not executed yet do not have debugging information available, and will show a message indicating this fact rather than a data value. This is because the pin's value is only updated when the node executes its underlying code, and is therefore invalid until the node has executed at least once. Even Blueprint variable nodes need to execute code to retrieve the variable's value, and will do so only when another node attempts to access their output value.

## Debug Window and Blueprint Debugger

The **Debug** window shows Breakpoints, Watches, and the current code execution trace stack. This window also features execution controls, so you can stop, resume, or step through your code when using Breakpoints. You can use tabs to switch between the full execution call stack and the Breakpoint, Watch, and call stack information for specific Blueprint instances.

### Watch Window

The **Blueprint Watch Window** speeds up debugging by giving you access to the data that you want to watch. You can watch Blueprint classes that you open in the Editor and that are part of the current call stack. When execution pauses, you can see a consolidated call stack populated with current data. You can jump between Blueprints with ease and inspect property values and node outputs. This view supports expansion of Arrays, Sets, Maps, and other data structures, making drill-down examination of any data they contain quick and convenient. You can also click on an entry in the **Node Name** column to go to that node in any Blueprint class, or select an entry in the **Object Name** column to select that specific instance.

### Call Stack

The **Call Stack** that is available during debugging sessions is similar in concept to the call stack that is found in most C++ development environments. It reveals the flow of execution between Blueprints visual scripting functions and native (C++) code functions. The Blueprint visual scripting function currently executing is at the top of the stack.

Blueprint Macros do not show up in the Call Stack. Instead, they appear as part of the function that called them.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25cae0da-1c27-435f-8d62-7c0f5454ac1a/activebreakpoint.png "ActiveBreakpoint.png")

The Blueprint Function above get's all Actors of a certain class and deactivates its components. A Breakpoint has been set at the end of the function.

When a Breakpoint is hit, the Call Stack lists the functions currently in operation, starting with the current function at the top, and proceeding downward to the calling functions. This means that each line entry contains the name of a function that was called by the function named on the line immediately below it. In the case of a recursive (self-calling) function, the same function name may appear multiple times in a row.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7643cc6e-ad36-4ad2-96b6-6cba813b7d97/callstack.png "CallStack.png")

This Call Stack shows a call into the Third Person Character's Event Graph when the Player pressed the custom function "FindActorPressed" as shown above. This was originally called from the Actor's Blueprint Event Graph, which in turn was responding to the FindActorPressed Action mapping event called from the Player Input Component in Native code.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db948036-4468-4899-9de2-95ed9968c868/bpcallstack.png "BpCallStack.png")

To view (or hide) the Call Stack, right-click on the Blueprint Debugger window, then from the dropdown, select Call Stack.

The Blueprint call stack can be tedious to inspect from the C++ call stack. To get a snapshot of the Blueprint call stack in your IDE, call `{,,UnrealEditor-Core}::PrintScriptCallstack()` in the Immediate window when stopped at a breakpoint. This only works in editor builds.

### Execution Trace

The **Execution Trace** stack shows a list of the nodes executed with the most recent at the top.

![Blueprint Debugging - Execution Trace Stack](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4a6bc4e-5e68-4f20-a29b-5e0e2b8eb568/k2_debug_exectrace.png)

This list updates as you step through the graph when debugging.