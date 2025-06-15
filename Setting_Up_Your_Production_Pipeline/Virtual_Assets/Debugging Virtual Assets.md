# Debugging Virtual Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-virtual-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-virtual-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:19:33

---

This page contains information about how to view information and debug output about **Virtual Assets** in your projects.

## Validate Your Package Virtualized

To determine whether your package has successfully been virtualized, hover your mouse over the asset in the content browser and check the **Has Virtualized Data** entry.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4789ebcd-b21a-4361-abe7-9e4ac333b7c4/verifyvirtualasset.png)

Alternatively, you can look at the file size of the asset. If the `.uasset` file is significantly smaller than it was before you virtualized it, the bulk data was separated from the `.uasset` and is now contained in the **Saved/VirtualizedPayloads** directory.

To investigate the contents of the package file, right-click the asset in the **Content Browser**, click **Copy File Path**, then input the following command in the console:

```
	`DumpPackagePayloadInfo [file path]`

Copy full snippet
```
DumpPackagePayloadInfo \[file path\]

Replace `[file path]` with the file path you copied from the Content Browser.

This console command can take either a full path or a package path, and it will write a summary of the payloads in the output window. The output displays a list of the locally stored payloads followed by a list of the virtualized payloads.

DumpPackagePayloadInfo does not use any cached information, such as the asset registry. Instead, it will re-parse the package's information each time you use it, so the information it gives should always be up to date.

## Monitor Virtual Assets With the Statistics Panel

The **Statistics Panel** shows information about how Virtual Assets behave on your machine. You can locate this panel in **Tool** > **Audit** \> **Virtual Assets.**

![Auditing virtual assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/520ad5f8-504f-4361-a483-858d7218dba6/auditvirtualassets.png)

The Virtual Assets Statistics Panel. The current panel displays the Read, Write, and Cache statistics for two different backends: the DDC backend and the project's source control.

Each row in the Virtual Assets tab represents a different backend that should be easy to identify based on your config file setup. Unreal Engine records stats for the following:

-   **Read**
    
    -   Pulling payloads from the backends when needed.
-   **Write**
    
    -   Pushing payloads to a backend when virtualizing.
-   **Cache**
    
    -   When a payload is pulled from a slower backend, such as a source control system, it is pushed to the faster backend to make repeated access faster.

## Debug Command Reference

This section provides the debug commands for debugging the **Virtual Asset** system in **Unreal Engine**. It provides commands for both the command line and the Console window in Unreal Editor where applicable. Most commands used in the command line can also be used in your config files. You can also use the command line versions of these commands in your [Virtualization Graphs](/documentation/en-us/unreal-engine/backend-graphs-for-virtual-assets-in-unreal-engine).

### Disable The Virtual Asset System

-   **Command line:** `-VADisable`
-   **Console:** `VA.DisableVirtualization`

Disables the virtualization system and mounts the null implementation instead.

This is the same as setting `SystemName` in the `[Core.ContentVirtualization]` section in the `DefaultEngine.ini` file to `None`.

When disabled, all methods in the virtualization system interface will return their failure states.

### Override The BackendGraph

-   **Command line:** -VABackendGraph=

Change which backend graph the virtualization system uses when initializing as though you were editing the 'BackendGraph' value of the `[Core.ContentVirtualization]` section in the `DefaultEngine.ini` file

The name of the graph must match an existing graph set up for the project you are trying to run. If it does not exist then the virtualization system will give a fatal error on startup.

### Disable Specific Backends

-   **Command line:** `-VAMissBackends=[backend name]`
-   **Console:** `VA.MissBackends`

Disable one or more backends from pulling payloads at all. This command can take any of the following inputs:

| **Input** | **Result** |
| --- | --- |
| **Backend name** | The name of the backend you want to disable. You can provide multiple backend names by combining them with a `+`. For example, `-VA-MissBackends=FastCache+SlowCache` would disable both of the listed backends. |
| **All** | Prevent any backend from pulling. |
| **Reset** | Reset and enable all backends. |
| **List** | List currently disabled backends. |

### Simulate Bad Connections

-   **Command line:** \`-VAMissChance=\[percent chance of failure\]
-   \*\*Console: `**VA.MissChance`

Simulate a bad connection by setting a percent chance that payload pulls will automatically fail. For example, `-VA-MissChance=50` will set a 50% chance of failure.

### Fail a Specified Number of Payload Pulls

-   **Console:** `VA.MissCount=[number of payload pulls to miss]`

Automatically miss the next `X` payload pulls, where `X` is the number you specify with this command.

There is no command line version for `VA.MissCount`.

### Validate Payload Pushes

-   **Command line:** `-VAValidatePushes`
-   \*\*Console: `**VA.ValidatePushes`

Validates payloads by pulling them after each push and comparing them to the original file. This is the same as setting the `ValidateAfterPushOperation` option in your `DefaultEngine.ini` file.

### Force Single-Threaded Mode

-   **Command line:** `-VASingleThreaded`
-   **Console:** `VA.SingleThreaded`

Forces the system to work in single-threaded mode, eliminating multi-threaded access as a potential source of bugs. This is the same as setting the `ForceSingleThreaded` option in your `DefaultEngine.ini` file.

## Logging

When UE initializes the virtualization system, a detailed log shows the settings enabled. This includes fatal log messages which notify if a setting has the potential to cause critical data failure.

By default, the virtualization system keeps logging to a minimum and only displays warnings and errors where appropriate. However, if you enable verbose logging the log will show additional information that is useful when debugging problems.

To enable logging, use the following commands on the command line:

```
`-LogCmds="LogVirtualization Verbose"  -ini:Engine:[Core.Log]:LogVirtualization=Verbose"`
Copy full snippet
```
\-LogCmds="LogVirtualization Verbose" -ini:Engine:\[Core.Log\]:LogVirtualization=Verbose"