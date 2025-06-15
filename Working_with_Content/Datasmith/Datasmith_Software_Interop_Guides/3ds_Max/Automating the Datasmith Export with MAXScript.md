# Automating the Datasmith Export with MAXScript

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-maxscript-to-automate-the-datasmith-export-to-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-maxscript-to-automate-the-datasmith-export-to-unreal-engine)  
**Processed:** 2025-06-14 16:59:53

---

When you install the **Datasmith 3ds Max Exporter** plugin, it adds a small `Datasmith_Export` interface to the MAXScript environment. Use the interface to automate exports of 3ds Max scenes to `.udatasmith` files, instead of manually exporting scenes. This page describes the methods that the `Datasmith_Export` interface exposes.

The syntax for Datasmith 3ds Max export scripts changed in version 5.1. Scripts written for previous versions will not work in version 5.1. You can rewrite existing scripts using the new syntax described on this page.

Some of these methods correspond to commands on the Datasmith tab of the 3ds Max Ribbon (see The [3ds Max Ribbon](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine#the3dsmaxribbon)). When you call a method in MAXScript, the user interface for the corresponding command in the ribbon might not update immediately. To refresh the user interface, go to another tab in the 3dsMax ribbon, and then return to the Datasmith tab.

## Getting and Setting Export Options

### Datasmith\_GetExportOption\_AnimatedTransforms()

Returns `true` if Datasmith is set to export the full animation timeline, and `false` if it's set to export the current frame only.

### Datasmith\_SetExportOption\_AnimatedTransforms

Specifies whether Datasmith exports the full animation timeline or the current frame.

-   `true`: Datasmith exports the full animation timeline.
-   `false`: Datasmith exports the current frame only.

### Datasmith\_GetExportOption\_TextureResolution()

Returns the index value of the current resolution limit for baked procedural textures that Datasmith exports. Each value corresponds to the number of pixels in a target resolution, regardless of the specific widths / heights of exported textures.

| Value | Resolution |
| --- | --- |
| 0 | 4096 pixels |
| 1 | 16,384 pixels |
| 2 | 65,536 pixels |
| 3 | 0.25 megapixels |
| 4 | 1 megapixel |
| 5 | 4 megapixels |
| 6 | 16 megapixels |

For more information about limiting baked procedural texture resolution, see [Procedural Textures](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#proceduraltextures).

### Datasmith\_SetExportOption\_TextureResolution

Specifies the maximum resolution for baked procedural textures that Datasmith exports. Accepts values between 0 and 6. Each value corresponds to the number of pixels in a target resolution, regardless of the specific widths / heights of exported textures.

For more information about limiting baked procedural texture resolution, see [Procedural Textures](/documentation/en-us/unreal-engine/how-datasmith-translates-3ds-max-content-for-unreal-engine#proceduraltextures).

**Example:**

`Datasmith_SetExportOption_TextureResolution 4`

Sets the maximum baked / procedural texture resolution to one million pixels, or one megapixel.

## Logging Messages to the Datasmith Messages Window

Use these commands to log custom messages to the Datasmith Messages window. Each type of message displays in a different color.

| Message Type | Color |
| --- | --- |
| Info | Gray |
| Warning | Yellow |
| Error | Red |
| Completion | Green |

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6031ed16-8ec5-4db6-a95a-c0aaa23bfc85/datasmith-3ds-max-message-types.png)

### Datasmith\_LogInfo

Logs an Info-type message to the Datasmith Messages window. Info messages appear in gray.

**Example:** `Datasmith_LogInfo "this is an Info message"`

### Datasmith\_LogWarning

Logs a Warning-type message to the Datasmith Messages window. Warning messages appear in yellow.

| Parameter | Type | Description |
| --- | --- | --- |
| `<msg>` | string | The message to output to the Datasmith Messages window |

**Example:** `Datasmith_LogInfo "this is a Warning message"`

### Datasmith\_LogError

Logs an Error-type message to the Datasmith Messages window. Error messages appear in red.

| Parameter | Type | Description |
| --- | --- | --- |
| `<msg>` | string | The message to output to the Datasmith Messages window |

**Example:** `Datasmith_LogInfo "this is an Error message"`

### Datasmith\_LogCompletion

Logs a Completion-type message to the Datasmith Messages window. Completion messages appear in green.

| Parameter | Type | Description |
| --- | --- | --- |
| `<msg>` | string | The message to output to the Datasmith Messages window |

**Example:** `Datasmith_LogInfo "this is a Completion message"`

### Datasmith\_LogFlush()

Writes log messages that are queued in memory to the log file. The log file is stored in the `%LOCALAPPDATA%\UnrealDatasmithExporter\Saved\Logs` directory.

## Exporting .udatasmith Files

### Datasmith\_ExportDialog()

Opens the Datasmith file export dialog, where you can specify the name and path for the exported `.udatasmith` file.

### Datasmith\_Export selected:\[boolean\] quiet:\[boolean\]

Exports the 3ds Max model or selection as a `.udatasmith` file, without opening the Datasmith file export dialog.

This method takes the following arguments:

| Parameter | Type | Description | Optional? |
| --- | --- | --- | --- |
| `name` | string | The name of the file to export, without the file extension. | n |
| `path` | string | The full path to the directory to export the file to. | n |
| `selected:` | boolean | 
Specifies whether Datasmith exports the entire scene, or only the currently selected objects.

-   `true`: Datasmith exports only the visible selected objects.
-   `false`: Datasmith exports the entire scene (visible objects only).



 | y |
| `quiet:` | boolean | 

-   `true`: Datasmith exports the `.udatasmith` file silently, meaning it does not open any associated UI or display a progress bar. This is useful for automation scenarios.
-   `false`: Datasmith displays a progress bar and other associated UI when it exports the scene.



 | y |

**Example:**

`Datasmith_Export "DatasmithExportName" "D:\DatasmithExports\3dsMax" selected:true quiet:true`

The example above automatically exports selected objects as a `.udatasmith` file with the name DatasmithExportName at the path `D:\DatasmithExports\3dsMax`, without displaying a progress bar or other export UI.

## Direct Link and Direct Link Auto Sync

### Datasmith\_OpenDirectlinkUi()

Opens the Datasmith Direct Link Connection Status window.

### Datasmith\_GetDirectlinkCacheDirectory()

Returns the path to the Direct Link Cache Directory. You can also get the path from the Datasmith Direct Link Connection Status window.

### Datasmith\_GetUnrealEnginePath() / Datasmith\_GetUnrealEnginePathFromRegistry()

These methods return the path to the installed Unreal Engine connected via DirectLink. `Datasmith_GetUnrealEnginePath()` calls `Datasmith_GetUnrealEnginePathFromRegistry()` and returns the path stored in the registry. If the registry does not contain a path, it returns the default hardcoded path: `C:/ProgramData/Epic/Exporter/3dsMaxEngine/`.

### Datasmith\_ToggleAutoSync()

Toggles Direct Link Auto Sync on and off. Use `Datasmith_IsAutoSyncEnabled()` to check whether Auto Sync is currently enabled .

### Datasmith\_IsAutoSyncEnabled()

Returns true if Direct Link Auto Sync is currently enabled, false otherwise.

### Datasmith\_GetExportOption\_StatSync()

Returns `true` if Datasmith is set to output statistics to the Datasmith Messages window when you synchronize the scene using Direct Link or Direct Link Auto Sync, `false` otherwise.

### Datasmith\_SetExportOption\_StatSync

Specifies whether Datasmith outputs statistics to the Datasmith Messages window when you synchronize the scene using Direct Link or Direct Link Auto Sync

-   `true`: Datasmith outputs statistics to the Datasmith Messages window.
-   `false`: Datasmith does not output statistics.

### Datasmith\_SetAutoSyncDelay

Specifies the interval of the timer that checks conditions for Direct Link Auto Sync.

This method takes the following arguments:

| Parameter | Type | Description |
| --- | --- | --- |
| `<seconds>` | float | The duration of the interval between Auto Sync condition checks, in seconds. |

### Datasmith\_SetAutoSyncIdleDelay

When Direct Link Auto Sync is enabled, this method specifies the minimum amount of time for which the user has to be idle before Datasmith attempts a Direct Link Auto Sync.

This method takes the following arguments:

| Parameter | Type | Description |
| --- | --- | --- |
| `<seconds>` | float | The number of seconds the user has to be idle for before Datasmith attempts a Direct Link Auto Sync. |

### Datasmith\_UpdateScene quiet:\[boolean\]

Updates the Datasmith 3ds Max Exporter plugin's scene representation to match current 3ds Max scene.

Returns `true` if the scene changed since the last update, `false` otherwise.

When you use the Synchronize command from the Datasmith tab of the 3ds Max ribbon, Datasmith first calls this command, and then, if it detects any changes, calls `Datasmith_DirectLinkUpdateScene()`.

This method takes the following arguments:

| Parameter | Type | Description | Optional? |
| --- | --- | --- | --- |
| `quiet:` | boolean | 
-   `true`: Datasmith updates the scene silently, meaning it does not open any associated UI or display a progress bar. This is useful for automation scenarios.
-   `false`: Datasmith displays a progress bar and other associated UI when it updates the scene.



 | y |

### Datasmith\_DirectLinkUpdateScene()

Synchronizes the Datasmith 3ds Max Exporter plugin's scene representation with Unreal Engine via Datasmith Direct Link. Sets up tracking for scene changes.

When you use the Synchronize command from the Datasmith tab of the 3ds Max ribbon, Datasmith first calls Datasmith\_UpdateScene(). If it detects any changes, it then calls this method.

For more information, see File Export Panel in [The Datasmith 3ds Max UI](/documentation/en-us/unreal-engine/the-datasmith-3ds-max-ui-for-exporting-to-unreal-engine), and [Synchronizing 3ds Max and Unreal with Direct Link](/documentation/en-us/unreal-engine/using-direct-link-to-synchronize-3ds-max-and-unreal-engine).

### Datasmith\_Reset()

Stops tracking scene changes, and resets the Datasmith 3ds Max Exporter plugin's scene representation.