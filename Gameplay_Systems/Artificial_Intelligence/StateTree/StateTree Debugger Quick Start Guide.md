# StateTree Debugger Quick Start Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/statetree-debugger-quick-start-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/statetree-debugger-quick-start-guide)  
**Processed:** 2025-06-14 16:52:10

---

## Introduction

The **StateTree Debugger** monitors and records StateTree runtime behavior to help developers understand and diagnose potential problems in their StateTrees.

The system was built with two main goals in mind - to provide a visual representation of the active States in the tree, and to provide live monitoring of runtime values for States, Tasks, and Conditions.

The system offers live debugging for Editor Sessions (e.g. Play in Editor) and Remote Sessions (e.g. Standalone, Client, Server). In addition, users can perform deferred analysis by saving and loading recorded trace files.

The StateTree Debugger uses Unreal Engine’s **TraceServices**, such as [Unreal Insights](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine), to produce and analyze traced events. The system is built on top of the Trace Analyzer and Trace Providers, and it gathers the relevant events of one or multiple instances associated with a given StateTree asset.

This approach enables the system to debug multiple Editor, Client, and Dedicated Server processes at the same time from a single process.

## Pre-requisites

This guide will use the StateTree created in the [StateTree Quickstart Guide](/documentation/en-us/unreal-engine/statetree-quick-start-guide) to demonstrate the StateTree Debugger. Please complete the Quickstart to follow along with the examples in this document.

Once you complete the Quickstart guide, press **Play** to verify the behavior.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb71809e-8541-4bec-880c-e64bb37ec7a1/state-tree-debugger-demo-0.gif)

## Enable and Disable States

You can enable and disable individual specific States within a State Tree.

1.  Open the StateTree asset **ST\_ShootingTarget**.
    
    ![Open the StateTree asset ST_ShootingTarget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da447c2b-8d69-44b4-b977-81acd06e3351/state-tree-debugger-1.png)
2.  Right click the **MoveAlongSpline** State and deselect **State Enabled**. Alternatively, select the State and go to the **Details** panel. Click the **Debug Options** button and deselect **State Enabled**.
    
    ![Right click the MoveAlongSpline State and deselect State Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e2e78c7-6b6a-4b54-8786-63b8671a908d/state-tree-debugger-2.png) ![Click the Debug Options button and deselect State Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b239322d-1ab4-4b85-a9e5-386f0604bf30/state-tree-debugger-3.png)
3.  **Compile** and **Save** the State Tree. Notice how the disabled State is visualized with a darker color in the window.
    
    ![The disabled State is visualized with a darker color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7bf681f2-374e-41f6-9fc3-586694f3b5a8/state-tree-debugger-4.png)
4.  Press **Play** to see the results. The **MoveAlongSpline** State is disabled so the tree goes from the **Idle** to the **Dead** State immediately.
    
    ![The MoveAlongSpline State is disabled so the tree goes from the Idle to the Dead State](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0640ced1-e2be-484d-8be2-068b04146b62/state-tree-debugger-demo-1.gif)

## Enable and Disable Tasks

You can enable and disable individual Tasks within a State.

1.  Enable the **MoveAlongSpline** State and go to the **Details** panel. Click the **Debug Options** button next to the **STT\_MoveAlongSpline** Task and deselect **Task Enabled**.
    
    ![Click the Debug Options button and deselect Task Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c4ac4ed-cf02-490f-a7b5-44e67fd8cd70/state-tree-debugger-5.png)
2.  **Compile** and **Save** the State Tree. Notice how the disabled Task is visualized by the darker color.
    
    ![The disabled Task is visualized by the darker color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c442d750-3da6-44a1-a08e-4f43daa03b15/state-tree-debugger-6.png)
3.  Press **Play** to see the results. The **MoveAlongSpline** State is enabled, but the **STT\_MoveAlongSpline** Task is disabled. This results in the MoveAlongSpline State being evaluated, but because no Tasks are active, the tree returns to the Idle State.
    
    ![The MoveAlongSpline State is evaluated, but because no Tasks are active, the tree returns to the Idle State](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8c55551-2a01-4dd7-8342-599b43210daf/state-tree-debugger-demo-2.gif)

## Condition Debug Options

You can force the results of a condition check in a State Tree for testing purposes.

1.  For this example, select the **Idle** State and go to the **Details** panel. a. Expand the **Transitions** section, then expand the **On Tick Go to State Dead** struct. b. Finally, expand the **Conditions** to see the **Integer Compare** condition between the **HitCount** and the value of **5**.
    
    ![Expand the On Tick Go to State Dead struct and then expand Conditions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14c147d4-9010-4413-ad9a-7362044b8ad8/state-tree-debugger-7.png)
2.  Click the **Conditions Debug** button and select **Force True**. This will result in this condition always returning true when evaluated.
    
    ![Click the Conditions Debug button and select Force True](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0b3ab12-67ba-4535-b2b0-c6d7d58ec1d6/state-tree-debugger-8.png)
3.  Press **Play** to see the results. When the Idle State is executed, the **Transitions** are evaluated. In this case, the **On Tick Go to State Dead** returns **True** because the Integer Compare between the Actor **HitCount** and **5** always returns True. In other words, we are simulating the Actor being hit more than 5 times.
    
    ![The On Tick Go to State Dead returns True because the Integer Compare between the Actor HitCount and 5 always returns True](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f01d01e9-b323-4f91-aa02-34eab9d14eb9/state-tree-debugger-demo-3.gif)

## Breakpoints

Breakpoints can be added entering or exiting any State and Task, and while executing a Transition.

Breakpoints are stored temporarily throughout an Editor session. However, they will be lost if the asset gets reloaded. They do not require compilation of the StateTree, unlike Disabling States or Tasks.

1.  For this example, right click the **MoveAlongSpline** State and select Break on Enter. Notice how the State now has a red icon signifying that execution will break once the tree enters this State.
    
    ![Right click the MoveAlongSpline State and select Break on Enter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/559880bc-7bc3-4c96-9037-438949941950/state-tree-debugger-9.png) ![The State now has a red icon signifying that execution will break](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d498c17-3ba9-47a1-9897-c5360323af54/state-tree-debugger-10.png)
2.  **Compile** and **Save**. Click **Play** to test the results. As you can see, execution stops as soon as the State is entered.
    
    ![Execution stops as soon as the State is entered](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff50b85f-703c-4216-a2dc-5caabcc735f1/state-tree-debugger-demo-4.gif)
3.  You can also add a Breakpoint to a Task by clicking the **Task Debug Options** button next to the Task name and selecting **Break on Enter** or **Break on Exit**.
    
    ![Click the Debug icon next to the Task name and selecting Break on Enter or Break on Exit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af5b60ce-1146-4143-bcab-e865f7e0f59e/state-tree-debugger-11.png)

## The Debugger Tab

The **Debugger** tab provides detailed runtime information about the State Tree. It can be used to track its execution and get variable data during a pause.

You can open the tab by clicking **Window > Debugger**.

![Click Window - Debugger to open the Debugger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2c381c6-a769-4671-9019-1018a4c9acd3/state-tree-debugger-12.png)

The Debugger tab interface has the following areas:

![Debugger interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb13bf3b-06e1-49c8-98c3-79a9e91283c0/state-tree-debugger-13.png)

-   **(1) Editor simulation controls**: These buttons control simulation in the viewport. You can start, pause, and stop the simulation.
-   **(2) Trace Session recorder**: This button records the live session in the Visual Logger for later review. Pressing it will start the tracing with the Frame and StateTreeDebug channels enabled.
-   **(3) Analysis controls**: These buttons control the recorded session playback. You can start and stop the trace analysis, step through the session one frame at a time, or jump to the previous or next changed frame.
-   **(4) Trace and Execution area**: You can select a specific trace from the dropdown. You can also select a specific recorded execution.
-   **(5) Timeline**: The timeline shows the available executions along with their active States. You can scrub the timeline manually to get information about a specific state.
-   **(6) Details panel**: this panel shows execution details about the active State of the selected Execution. It displays information such as global Tasks and Evaluators, Tasks, and Transitions. It also shows the data and logic that was executed in the State.

In the example below, we clicked the **Play** button to start the play session and record the first **execution**. Once we stopped play mode, we scrubbed the timeline to view the recorded details of the executed States.

![Recording one execution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e34e3416-65c6-405c-85e3-30c4abf3f9c5/state-tree-debugger-demo-5.gif)