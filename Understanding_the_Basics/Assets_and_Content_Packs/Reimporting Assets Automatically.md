# Reimporting Assets Automatically

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/reimporting-assets-automatically-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/reimporting-assets-automatically-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:22

---

Auto reimporting in Unreal Engine allows you to work in your external content creation package and have any saved changes automatically reflected inside Unreal Engine without any user input. This can be a huge productivity win where you are iterating on a particular asset, and need to see the changes reflected in your game immediately.

UE monitors a set of user-defined folders for changes to source content files. Where a file has changed, and that file was used to import an asset in your game, Unreal Engine will automatically reimport the changed file into its dependent asset(s).

## Setup

Auto Reimport settings exist under **Editor Preferences > Loading & Saving > Auto Reimport**:

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07fdf46e-f64e-4c1d-b929-124f4cc7e1af/image_0.png)

The feature can be entirely enabled and disabled with the **Monitor Content Directories** checkbox.

Using the default settings, it is recommended that you place all source content files alongside their relevant assets in the Content folder. Custom configuration will be required for any other workflows.

| Property | Description |
| --- | --- |
| **Directories to Monitor** | This setting defines which folders Unreal Engine will monitor for changes. Folders can be virtual paths (for example /Game/Textures), or absolute paths (C:/Game/SourceArt/). Only source content files that reside inside these folders will be eligible for auto-reimport. |
| **Include/Exclude Wildcards** | 
By default, Unreal Engine will detect any changes to any files, and reimport them as necessary. Sometimes it's useful to limit this to only work on certain file types, or perhaps exclude a certain subfolder or extension. Multiple wildcards must be added as new entries. Here are some example configurations:

-   To include only fbx files, add a new *include* wildcard with the value \*.fbx
-   To operate on fbx, png and psd files, add 3 new *include* wildcard with the values *.fbx,* .png, and \*.psd
-   To ignore changes to any source files in a subfolder, add an *exclude* wildcard with the value Subfolder/\*



 |
| **Import Threshold Time** | Specifies the amount of time (in seconds) to wait after a change has been detected before processing the change. |
| **Auto Create Assets** | Determines whether a newly created file should automatically have an asset created for it. In order for this to work, you must be monitoring a virtual path (e.g. /Game/) or have specified a mount point (which determines *where* to create the new file) |
| **Auto Delete Assets** | Determines whether deleting a source content file should also delete its associated asset in UE. This will only happen where there is a 1-1 mapping between source file and asset. |
| **Detect Changes on Restart** | Unreal Engine is able to detect changes to files that have occurred since UE was shutdown. Any such changes will be processed when UE is reopened. This specific functionality may not be desirable where source control is enabled that will update source content. In this environment it is recommended that *Detect Changes on Restart* is turned off to avoid the potential of redundant reimporting after getting latest. |