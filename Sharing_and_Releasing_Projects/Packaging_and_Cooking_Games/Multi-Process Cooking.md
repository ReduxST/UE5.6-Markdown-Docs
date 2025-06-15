# Multi-Process Cooking

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-multi-process-cooking-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-multi-process-cooking-for-unreal-engine)  
**Processed:** 2025-06-14 17:00:10

---

In UE 5.4, multi-process cook does not report all errors correctly, and it can sometimes report a successful cook process even though it failed. If you encounter this problem, we recommend turning off multi-process cook. This issue is fixed un UE 5.4.3.

**Multi-Process Cook** reduces the time it takes to produce a cooked build by leveraging available CPU cores and memory resources. To do this, it breaks cooking into the following:

-   Several **worker** sub-processes cook groups of assets.
-   A **director** process divides up and assigns sets of assets to the workers, then collates their results and combines their output when necessary.

This page provides:

-   Information about Multi-Process Cook's current limitations.
-   Instructions on how to set up Multi-Process Cook.
-   Guidelines on how to maximize its benefit for your project.

## Benefits and Limitations

Multi-Process Cook essentially trades memory for parallelism. You should expect a Multi-Process Cook to use more RAM than a single-process cook to make it effective.

For projects with a large amount of assets, Multi-Process Cook significantly reduces the amount of time required to complete a cooked build. Epic Games internally tested cooking a large project with 4 sub-processes, which reduced build time roughly 40% compared with cooking the same project with single-process cooking.

For small projects such as [Lyra](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine), Multi-Process Cook is unlikely to reduce build times, as the processing or memory overhead of multiple workers outweighs the benefit for cooking only a handful of assets.

### System Resource Bottlenecks

Multi-Process Cook currently only runs worker processes on the same machine that the director process is running. Sharing machine resources imposes an upper limit on the number of processes that can effectively be used.

Multi-process cook will be updated to allow remote workers in a future release

The two major bottlenecks are:

-   The amount of RAM on your machine.
-   The number of cores available for processing.

When RAM runs out, the director and worker processes start garbage collecting more frequently. The cost of garbage collection slows down the cook more than the extra workers improve it.

When the number of available cores runs out, each worker runs single-threaded. Long-running async tasks that ordinarily happen on worker threads block the main thread and slow down the cook more than the extra workers speed it up.

### Debugging

The increased complexity of multiple processes also makes debugging system-specific cooker bugs more difficult. Logs and artifacts from each worker are replicated back to the director. This works well for Epic Games internally, specifically for bugs that can be diagnosed from log statements and artifacts. However, for problems that require attaching with a debugger, the multiple processes add a layer of complexity.

Multi-Process Cook imposes an additional burden on the authors of some advanced plugins. Plugins that aggregate data during the cooking process across multiple packages now need to use the `IMPCollector` API to write tick functions on the workers that replicate the collected data to the director.

## Enable Multi-Process Cook

You can enable Multi-Process Cook by setting the **CookProcessCount** variable to a number larger than 1, either using your project's configuration files or startup arguments to the cooker.

For best results, test different values for CookProcessCount. An optimal value for CookProcessCount might vary depending on your project and your machine's available resources.

### Enable Multi-Process Cook in Your Configuration Files

To enable Multi-Process Cook, add an entry to your project's `*Editor.ini` for `[CookSettings]:CookProcessCount`, and set it to an integer larger than 1. For example:

```

	`[CookSettings]  	CookProcessCount=4`

Copy full snippet
```
\[CookSettings\] CookProcessCount=4

### Enable Multi-Process Cook Through Startup Parameters

To enable Multi-Process Cook through cooker startup parameters, set CookProcessCount using `-cookprocesscount=N`, where `N` is the number of processes you want to use. For example:

```

	`-cookprocesscount=4.`

Copy full snippet
```
\-cookprocesscount=4.

If you are using UnrealAutomationTool (UAT) to package your build, this argument can be passed through the AutomationTool into the cooker process using `AdditionalCookerOptions`:

```

	`-AdditionalCookerOptions="<YourOtherOptions> -cookprocesscount=4"`

Copy full snippet
```
\-AdditionalCookerOptions="<YourOtherOptions> -cookprocesscount=4"

If you are using **Project Launcher** to launch the automation tool from Unreal Editor, there is an **AdditionalCookerOptions** field in Project Launcher settings that specifies the AdditionalCookerOptions argument.

## Configuration and Tuning

The primary tuning parameter for Multi-Process Cook is the number of processes used (CookProcessCount), and projects should increase this value as far as it can go before the cook process begins to slow down due to overhead. When the cost starts increasing, there are additional parameters you can change that might impact the bottleneck and allow more workers.

### Cooker Memory Settings

The cooker has only one set of options to control memory use, which specifies at what point it collects garbage. Refer to the the comments in the `[CookSettings]` section of `Engine\Config\BaseEngine.ini`, and try tuning them if your machine is running out of memory:

DefaultEditor.ini

```

	`[CookSettings] 	MemoryMinFreePhysical= 	MemoryMaxUsedPhysical= 	SoftGCStartNumerator= 	SoftGCDenominator=`

Copy full snippet
```
\[CookSettings\] MemoryMinFreePhysical= MemoryMaxUsedPhysical= SoftGCStartNumerator= SoftGCDenominator=

## Troubleshooting

The following are potential errors that might occur during Multi-Process Cooking along with suggested actions:

-   **Package %s can only be cooked by a now-disconnected CookWorker. The package can not be cooked.**
    
    This error appears when a CookWorker crashes. The CookWorker crash should be debugged and this follow up error should be ignored; the crash should have been logged as an earlier error.
    
-   **Retraction results message received from %s; no packages were available for retraction.**
    
    When one CookWorker finishes before the others, the cooker tries to offload work from a busy worker onto it. In the case of World Partition levels, this isn't possible yet. The cooker continues attempting and failing to retract repeatedly, causing a performance problem as well as log spam. There is no fix for this in the current version of UE. The planned fix is to fix the World Partition case to allow a level's generated packages to be split among multiple CookWorkers.
    
-   **%s has not responded to a RetractionRequest message for %.1f seconds. Continuing to wait…**
    
    When the reported duration goes above 1000 seconds, this usually indicates a deadlock on the CookWorker. Attach to the CookWorker with a debugger to see what it is doing.