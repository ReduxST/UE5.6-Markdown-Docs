# Sync Filters

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-filters-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-filters-for-unreal-engine)  
**Processed:** 2025-06-14 16:57:17

---

**Sync Filters** enable developers to update the client workspace with syntax that can be customized with **UnrealGameSync (UGS)**. Keep reading to learn more about setting up Sync Filters for UGS.

## User Interface

To access the Sync Filter menu, click the **Options** dropdown on the bottom right of the main UGS window, and then click **Sync Filter...**

![UGS Sync Filters UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89c6ff74-8028-4f8a-b38a-f2e76ecc55d3/ugs-sync-filters-user-interface.png)

Once inside the user interface, take note of the following options.

![UGS Sync Filters UI Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0f1bc36-35ce-4bd1-81ff-502f6a9eb5d9/ugs-sync-filters-user-interface-options.png)

| Element | Name | Description |
| --- | --- | --- |
| 1 | Global Workspace Tab | These settings will be applied to all workspaces, unless a specific workspace conflicts, then the specific workspace will take precedence. |
| 2 | Current Workspace Tab | These settings will be combined with the global settings, and any conflicting settings will override the global settings. |
| 3 | General Settings | **Sync all projects in stream** syncs the entire contents of the stream, and **Include all synced projects in solution** will include any synced projects (and the solution) when the solution is generated for this workspace with UGS. |
| 4 | Sync Category Allowlist | Anything checked here will get synced, otherwise it will be ignored. For example, checking "Platform Support: PS4" will make UGS sync PS4 platform files, and unchecking "Platform Support: XboxOne" will make sure the XboxOne platform files are not synced. |
| 5 | Custom Sync Filters | Using the above syntax, or the syntax noted in modal dialogue behind the "Syntax" button, use this section to add single custom filters, line by line. |
| 6 | Combined Filters | Clicking this button will show you the summary of all filters you've created, including custom filters, the allowlisted filters, the defaulted excluded filters (not checked in categories), and general settings. If you need to see exactly what your filters list will look like, use this. |

## Custom Filter Syntax

Whether editing an `UnrealGameSync.ini` directly, or using the UGS UI, there is some syntax to be aware of when adding custom sync filters.

Specify a custom view of the stream using Perforce-style wildcards (one per line).

-   All files are visible by default.
    
-   To exclude files matching a pattern, prefix it with a '-' character (for example, -/Engine/Documentation/...).
    
-   Patterns may match any file fragment (eg. \*.pdb), or may be rooted to the branch (eg. /Engine/Binaries/.../\*.pdb).
    

The view for the current workspace will be appended to the view shared by all workspaces.

These syntax rules are available within the UGS UI as well in case you don't want to visit this page again.

![UGS Sync Filters Syntax Rules](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb2a466d-1420-4656-be64-cfbfc028d6ff/ugs-sync-filters-syntax-rules.png)

## UnrealGameSync.ini

For a quick primer on creating and editing a project-specific `UnrealGameSync.ini`, located at `[Unreal Project Root Directory]\Build\UnrealGameSync.ini` (and submitted to Perforce), read about [Customizing for Your Project](/documentation/en-us/unreal-engine/unreal-game-sync-reference-guide-for-unreal-engine#customizingforyourproject).

### Additional Reference Information

A few reference items include the following additions.

#### Sync Steps

Sync steps are run after any sync operation, with or without a following compilation step. This enables updating synced changelist information in custom version files.

```
	`[Sync] 	+Step=(FileName="$(ProjectDir)\\Path\\To\\SyncStep.bat", Arguments="/arg1")`

Copy full snippet
```
\[Sync\] +Step=(FileName="$(ProjectDir)\\\\Path\\\\To\\\\SyncStep.bat", Arguments="/arg1")

#### Build Steps

```
	`[Build] 	+Step=(UniqueId="d9610e2f-7f6f-4898-bc98-d39dd7053d75", Description="Launch Game", StatusText="Launching Game...", EstimatedDuration="5", Type="Other", FileName="$(ProjectDir)\\Build\\BatchFiles\\Launch.bat", Arguments="", bUseLogWindow="False", OrderIndex="5", bNormalSync="False", bScheduledSync="False", bShowAsTool="True")`

Copy full snippet
```
\[Build\] +Step=(UniqueId="d9610e2f-7f6f-4898-bc98-d39dd7053d75", Description="Launch Game", StatusText="Launching Game...", EstimatedDuration="5", Type="Other", FileName="$(ProjectDir)\\\\Build\\\\BatchFiles\\\\Launch.bat", Arguments="", bUseLogWindow="False", OrderIndex="5", bNormalSync="False", bScheduledSync="False", bShowAsTool="True")

When adding Build or Sync Steps, the following attributes are possible to use with the above syntax.

| Attribute | Description |
| --- | --- |
| **UniqueId** | Randomly generated GUID. |
| **OrderIndex** | Ascending value that determines where this step is in the order of the steps list. |
| **Description** | Displays in the UGS UI. |
| **StatusText** | Displays when this step is being executed. |
| **EstimatedDuration** | How long the step will last in minutes, used for advancing the progress bar in the UGS UI the correct amount |
| **Type** | When a build step is created, it will have the type of **Compile** (default), **Cook**, or **Other**, which is used for deciding which attributes are valid to leverage. See the [Types table](/documentation/en-us/unreal-engine/unreal-game-sync-filters-for-unreal-engine#typestable) below for details. |
| **bNormalSync** | Sets the flag that determines if the step should be run on each normal (user-initiated) sync. |
| **bScheduledSync** | Sets the flag that determines if the step should be run on each scheduled sync. |
| **bShowAsTool** | Sets the flag that determines if the steps should be shown as a tool in the "more tools" menu in the UGS status panel. |

#### Types

| Attribute | Description |
| --- | --- |
| **Type - Compile** | 
-   **Target** is the name of the target for the compile step (for example, "BlankGame").
-   **Platform** is the platform that a compile step is intended for (for example, "Win64" or "Linux").
-   **Configuration** is the configuration for a compile step (for example, "Debug" or "Shipping").
-   **Arguments** are arguments to pass to the file or process being run.



 |
| **Type - Cook** | 

-   **FileName** is the path, including the file name, of the file to run for this step.



 |
| **Type - Other** | 

-   **WorkingDir** is the directory that the file should be run from.
-   **bUseLogWindow** enables whether or not to use the log window when reporting the step.
-   **Arguments** and **FileName** are the same as mentioned in Type - Compile and Type - Cook, respectively.



 |

#### Safe to Delete Folders

These paths are safe to be checked by default when you run the "clean workspace" tool in UGS.

```
	`[Default] 	+SafeToDeleteFolders=FolderName 	+SafeToDeleteFolders=Path/To/FolderName`

Copy full snippet
```
\[Default\] +SafeToDeleteFolders=FolderName +SafeToDeleteFolders=Path/To/FolderName

#### Zipped Binaries Sync Filters

These are files that should be excluded from the sync if using precompiled binaries.

```
	`[//UE4/Main/Samples/Games/ShooterGame/ShooterGame.uproject] 	ZippedBinariesPath=//UE4/Dev-Binaries/++UE4+Main-Editor.zip 	ZippedBinariesSyncFilter=-/FolderToFilter/...`
Copy full snippet
```
\[//UE4/Main/Samples/Games/ShooterGame/ShooterGame.uproject\] ZippedBinariesPath=//UE4/Dev-Binaries/++UE4+Main-Editor.zip ZippedBinariesSyncFilter=-/FolderToFilter/... Use the same syntax for custom filters in the UGS UI.