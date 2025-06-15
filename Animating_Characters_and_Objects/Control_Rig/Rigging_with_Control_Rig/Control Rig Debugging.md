# Control Rig Debugging

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-debugging-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-debugging-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:33

---

Use Control Rig's debug tools to evaluate your rig behavior, and address issues in the Rig Graph. This document provides an overview of these tools.

#### Prerequisites

-   You have created a Control Rig Asset. See the **[Control Rig Quick Start](/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine)** page for information on how to do this.

## Debug Mode

Similar to **[Blueprint Debugging](/documentation/en-us/unreal-engine/blueprint-debugging-example-in-unreal-engine)**, Control Rig Graphs can be debugged using **Debug Mode**. Using this mode, you can add breakpoints to nodes, step through graph logic, and inspect the live value of properties at any point in the graph.

Debug Mode can be enabled by clicking **ReleaseMode** in the Control Rig Toolbar. This button toggles between **Debug** and **Release** modes.

![control rig debug mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6ef1084-a083-49a8-a8a8-f5f15176ce8e/debug1.png)

Debug mode supports your **[Solve Direction](/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine)** context, and will apply depending on if you are evaluating **Forwards Solve**, **Backwards Solve**, or **Setup Event**.

### Breakpoints

When debugging your node graph, use breakpoints to stop the evaluation of your graph at specified nodes and step through subsequent nodes.. With this, you can temporarily preview parts of your graph that were evaluated before the breakpoint within the viewport. When using breakpoints, time doesn't advance until the evaluation reaches the end of the graph, which causes accumulated time nodes to not change their results.

You can add breakpoints to pause graph evaluation at the chosen node by right-clicking a rig graph node and selecting **Add Breakpoint**. Adding breakpoints will also automatically enable Debug Mode if it is not already enabled.

![control rig breakpoint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1884a32-014c-4416-944d-e3a204e38ed2/breakpoint.png)

Once a breakpoint is specified, use the **Step** toolbar buttons to step through your graph evaluation, node by node. The Control Rig will only evaluate to the breakpoint or the currently evaluated node.

![control rig node step](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6580e56-863f-46fe-a0a6-1c89e664e765/stepping.gif)

The step buttons perform the following functions:

| Name | Icon | Description |
| --- | --- | --- |
| **Resume** | ![resume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/284dfbe7-e8b5-42b9-a308-12cbd8578f02/iconplay.png) | Resumes execution after being halted at a breakpoint. This will stop if another breakpoint is encountered. |
| **Focus** | ![focus](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fe52334-3460-4fb3-be9f-bbc7a9b1f07a/iconnavigate.png) | Focuses the graph view on the node currently being debugged. |
| **Step Next** | ![step node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60217821-2d38-48aa-ae10-698e1142d6ce/iconstep.png) | When stopped at a breakpoint, this will jump the debug focus to the next node in the evaluation. |
| **Step Into Function** | ![step in next](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c477e28-aab8-4e98-bbf4-ea64b26dc47e/iconstepin.png) | When stopped at a breakpoint, this will jump the debug focus to the next node in the evaluation. If the next node is contained within a function or collapsed group, the view will enter into the function to focus on the first node of that group. |
| **Step out of Function** | ![step out next](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d88e1e97-e1f8-4663-acb5-3553f4b658b9/iconstepout.png) | When stopped at a breakpoint, this will jump the debug focus to the next node in the evaluation. If the current node is contained within a function or collapsed group, and the next node is located outside the function or group, then the graph view will change to focus on the next node outside of the group. |

### Property Watching

When debugging, the property values for each graph node can be configured to display their updated values in real-time. To enable this, right-click the node pin you want to update in realtime and select **Watch this value**.

![control rig property watch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ba2f5e3-02b3-46f8-b945-d857ebf364ce/watch1.png)

Once a property is being watched, it will display value information on top of the node, and an icon next to the property to denote that it is being watched.

![control rig property watch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/45c11e54-b57e-40b7-82bd-b5e2f6783e69/watch2.png)

To stop debugging a property, right-click the pin and select **Stop watching this value**.

![control rig property watch](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0434acde-01ec-494d-8b56-046b6af5cfdf/watch3.png)

## Class Settings Debug and Profiling

The Class Settings Details panel contains tools and properties for debugging your graph's performance. Click **Class Settings** to reveal this panel.

![control rig class settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af6b6316-87e1-4d4d-af0e-6d438f9e0fc2/classsettings.png)

Enabling **Show Node Run Counts** will display the number of times a node has run in its execution. This can be useful when determining if looping or collection nodes are running correctly.

![control rig show node run count](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0fa956a-f3a9-4d93-86aa-d669b786b238/showcount.png)

### VM Profiling

**Virtual Machine Profiling**, or **VM Profiling**, can also be used to debug real-time graph performance and the speed of node execution.

Click **Enable Profiling** under the **VMRuntime Settings** category to start profiling the rig graph. The **Min** and **Max Duration Color** properties are used to show which nodes are taking the shortest or longest amount of time, in microseconds, to execute. The total microsecond (μs) count is also displayed next to the node.

![control rig vm profiling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad1248ca-f80e-451a-afba-1beefd4a827f/profiling.png)

## Execution Stack

The Execution Stack panel provides a reference for the order of node operations within your graph. This can be used to debug your nodes and evaluate the sequence of events.

The Execution Stack panel can be opened by navigating to the Control Rig menu bar and selecting **Window > Execution Stack**.

![execution stack](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4898b49-ec15-4fe6-888b-485b3d2cc804/execution1.png)

Once opened, the Execution Stack displays the following information:

![execution stack](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d7846f7-86fc-4b75-8499-0f8ba9b45670/execution2.png)

1.  **Node Column**, which displays the order of evaluation for all nodes from the given solve direction. Double-clicking any node here will frame the rig graph view to that node. Selecting a node in the Rig Graph will also highlight the instructions associated with it.
    
2.  **Node Run Count**, which displays the number of times the node has been executed. This will only display if **Show Node Run Counts** is enabled from [**Class Settings**](/documentation/en-us/unreal-engine/control-rig-debugging-in-unreal-engine#classsettingsdebugandprofiling).
    
3.  **Microsecond Count**, which displays the total time in microseconds (μs) it takes for the node to execute, if [**Profiling**](/documentation/en-us/unreal-engine/control-rig-debugging-in-unreal-engine#vmprofiling) is enabled.