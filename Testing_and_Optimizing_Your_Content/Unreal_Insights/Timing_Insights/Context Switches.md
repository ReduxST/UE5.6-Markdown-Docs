# Context Switches

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/context-switches-in-unreal-engine-5](https://dev.epicgames.com/documentation/en-us/unreal-engine/context-switches-in-unreal-engine-5)  
**Processed:** 2025-06-14 16:15:29

---

## Context Switches

A **Context Switch** stores the state of a process or a thread, so it can be restored and resume execution at a later point. When attempting to profile Context Switches with a Launcher Build, You will want to ensure that you enable "Editor Symbols for Debugging" from the Options for your Engine Version.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e816fdb-8978-426b-aa47-4f14f27a85f5/editorsymbolsfordebugging.png)

Context Switches are supported on Windows, XB1/XSX, and PS4/PS5 platforms.

1.  You can enable the **ContextSwitch** trace channel in the command line:
    
    ```
             `-trace=default,ContextSwitch`
    		
    Copy full snippet
    ```
    \-trace=default,ContextSwitch On Windows, depending on your user permission settings your project runtime should be "run as administrator".
2.  Open your trace file in Unreal Insights, If a session has the `ContextSwitch` trace event enabled, then the following information will be displayed in the Timing Insights view:
    

a) Additional CPU Core tracks. One for each CPU core in the recorded trace; shows timing events indicating what thread does execute on the respective CPU core. "Unknown" timing events indicate execution of threads from other applications / processes or from the OS.

b) Each CPU Thread has a header lane with core number events indicating on which core the respective thread is executing. The time range when a thread is executing and when it is preempted it is highlighted.

![cpu-thread](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d168735-7c66-4571-a19c-abe6a7a7cc23/cputhread.png)

c) CPU/GPU drop down menu shows additional options re Context Switches:

![cou-gpu-context-menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02a12ab3-981e-4aed-b0f9-71e7e63966c9/contextcpu.png)

d). The context menu of a "Core" timing event in a Cpu Thread track shows additional options:

![core-timing-event-track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f568e62-64c8-4d8a-87b3-4931a5b174ea/coretiming.png)

e). The context menu of a "Thread" timing event in a CPU Core track shows additional options:

![thread-timing-event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8880973f-f2c0-40cf-ac14-69f838203056/threadtiming.png)