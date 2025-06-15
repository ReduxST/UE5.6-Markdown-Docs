# Gameplay Targeting System Debugging

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-targeting-system-debugging-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-targeting-system-debugging-in-unreal-engine)  
**Processed:** 2025-06-14 16:25:05

---

## Debugging and Troubleshooting

You can enable debugging from the Editor by pressing the tilde (~) key. See the table below for a complete list of Console Commands.

Currently debug visualizations only run on targeting requests on the client.

| Console Command | Description |
| --- | --- |
| `ts.debug.EnableTargetingDebugging false/true` | Toggles whether the targeting system is actively in debugging mode. |
| `ts.debug.PrintTargetingDebugToLog false/true` | Toggles whether to print the targeting debug text to the log. |
| `ts.debug.TotalDebugRecentRequestsTracked #` | Sets the total number of targeting requests that will be tracked upon starting. The default amount is 5. |
| `ts.debug.ClearTrackedTargetRequests` | Clears all tracked targeting handles when in debug mode. |
| `ShowDebug TargetingSystem` | Brings up the visualization of the targeting tasks when `ts.debug.EnableTargetingDebugging` is enabled. |

## Developer Reference

For an in-depth Engineering reference guide, see the [Gameplay Targeting Plugin Reference](/documentation/en-us/unreal-engine/gameplay-targeting-system-reference-in-unreal-engine) documentation.