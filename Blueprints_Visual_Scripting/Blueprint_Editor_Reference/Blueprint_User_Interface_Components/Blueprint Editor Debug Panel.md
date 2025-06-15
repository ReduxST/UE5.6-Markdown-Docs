# Blueprint Editor Debug Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/debug-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/debug-panel-in-the-blueprints-visual-scripting-editor-for-unreal-engine)  
**Processed:** 2025-06-14 16:19:14

---

The **Debug** panel provides a list of all debug tools currently in use for the Blueprint, such as Breakpoints and Watch Values. During Play-In-Editor, it also provides access to the Execution Trace, showing you each node execution taking place within a given Blueprint.

For more information on debugging Blueprints, please see [Blueprint Debugger](/documentation/en-us/unreal-engine/blueprint-debugger-in-unreal-engine).

## Interface

The interface for the **Debug** panel changed depending on whether or not you are playing or simulating in the Editor.

**When not playing or simulating:**

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53d65810-c5ef-40cc-be29-649a9603b08e/debugnotsim.png)

When not playing, the Debug panel lists off any watch values and breakpoints within your current Blueprint.

**When playing or simulating:**

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46efe3fa-6f07-472c-8a95-59ac0c994d7a/debugpanel.png)

When playing or simulating the Debug panel shows debug info, as well as the Execution Trace, which shows how long each node is taking to execute.