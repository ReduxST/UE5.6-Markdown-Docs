# Zenserver as Cooked Output Store

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-zen-storage-server-as-cooked-output-store-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-zen-storage-server-as-cooked-output-store-for-unreal-engine)  
**Processed:** 2025-06-14 17:02:28

---

The purpose of using Zenserver as cooked output store is to:

-   Improve cook-time efficiency by reducing the filesystem overhead of having one million+ files as output from the cook on large projects.
    
-   Allow for reliable incremental cook in the future.
    
-   Allow for much faster staging and deployment through the use of the [Zen Streaming](/documentation/en-us/unreal-engine/how-to-use-zenserver-streaming-to-play-on-target-in-unreal-engine) feature, which builds upon Zenserver as a cooked output store.
    
-   Allow easy importing of cooked state through the use of the [Cooked Data Snapshots](/documentation/en-us/unreal-engine/cooked-data-snapshots-with-zen-storage-server-for-unreal-engine) feature, which builds upon Zenserver as a cooked output store.
    
-   Allow for a more efficient representation of derived data included in cooked output data in the future.
    
-   Allow for more direct and efficient targeted workflows in the future by allowing us to cook to the same storage that the game loads from without large data transformations having to happen in between.
    

## Understanding Cooked Output

To understand how Zenserver is used as cooked output storage, it is worth first understanding how cooked output is handled by default, and how it fits into the wider pipeline for cooking, staging, and deploying data for Unreal Engine.

Consider the following representation of the pipeline for cooking, staging, and deployment in Unreal Engine 5.4.

The quantities and sizes of data are hypothetical but within the range of a large game project.

If you follow the flow from left to right, you can see that the first step is the Cook operation, which loads `.uasset` files as well as data from the Derived Data Cache (DDC). As of Unreal Engine 5.4, this DDC data is stored in a separate process named Zenserver, which you can see running alongside Unreal Editor. Zenserver will decide internally how this data is represented and stored on disk.

In the default configuration, the cooked output files are written as many separate files in your project’s `Saved/Cooked/<Platform>` folder. The quantity of these files can be high, as can the number of bytes written to them.

This high quantity of files can cause performance bottlenecks for the filesystem. This manifests as:

-   Long operations to delete cooked output (15+ minutes). Even if done asynchronously, this will still cause filesystem write cache flushes that affect other I/O operations.
    
-   Endpoint security software (such as Windows Defender) getting involved in each file open/close operation, slowing down cook.
    
-   Filesystem metadata (such as Last Access Time tracking) contributes to filesystem write caches becoming full and having to flush to disk, slowing down cook.
    

These issues don’t amount to a large amount of time for smaller projects, but as a project grows, they can become significant.

In switching to the use of Zenserver as a cooked output store, we allow this cooked output to be stored in Zenserver instead of as loose files.

Zenserver is responsible for writing the cooked output to disk in a representation it chooses. This can mean that small pieces of data get aggregated into larger block files if they are below some configured size threshold. As a result, in our example, we might be storing 1,000,000 pieces of data as before, **but the file quantity as seen by the filesystem can be much smaller**.

## Enabling Zenserver as Cooked Output Store

As of Unreal Engine 5.5, Zenserver is not used for cooked output storage by default. This is planned to change in future releases. For now, you can opt in to using Zenserver as cooked output store for your project by launching Unreal Editor, selecting the [Edit > Project Settings](/documentation/en-us/unreal-engine/project-settings-in-unreal-engine) menu item, then selecting the [Project > Packaging](/documentation/en-us/unreal-engine/project-section-of-the-unreal-engine-project-settings#packaging-2) section. Within that section, you will find a setting named **Use Zenserver as cooked output store**, which will be disabled by default.

![Zenserver settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e03077d-1294-4421-bc95-84b585758590/image_3.png)

You can enable that setting and ensure you also have **Use Io Store** enabled (it will be enabled by default). If they are both enabled, you can ensure your settings are saved (you may have to check out the file to save the settings change if you are using source control). At this point, you will be using Zenserver as cooked output store.

## Location of Cooked Data when Using Zen as Cooked Output Store

When using Zen as cooked output store, the engine will still create and write some data to your project’s `Saved/Cooked/<Platform>` folder, but it will write **much less data** there, as all cooked asset data is being stored in Zenserver instead. You should expect that the `Saved/Cooked/<Platform>` folder **no longer contains** any `.uasset`, `.ubulk`, or `.uexp` files. What you will find is a `ue.projectstore` file at that location that is a small, internal descriptor of where the cooked data is stored. This file is required for the engine to be able to find and access the cooked data.

![The ue.projectstore file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/061e47a6-16ce-421e-a03b-083a818b6f67/image_4.png)

So where is the cooked asset data stored? Zenserver will keep its data in files (some aggregated) in a data directory for Zenserver. This includes data for **both local DDC and cooked output**.

The default location for Zenserver data is:

-   **Windows:** `%LOCALAPPDATA%\UnrealEngine\Common\Zen\Data`
    
-   **Mac:** `~/Library/Application Support/Epic/UnrealEngine/Common/Zen/Data`
    
-   **Linux:** `~/.config/Epic/UnrealEngine/Common/Zen/Data`
    

Because Zenserver is also used to store the local DDC, its data storage location will override the default by following DDC configuration mechanisms:

-   A global local DDC path set in Unreal Editor DDC settings.
    
-   A local DDC path override via an environment variable (`UE-LocalDataCachePath`).
    
-   A local DDC path override via a command line argument (`-LocalDataCachePath=<path>`).
    

Finally, there are Zenserver-specific path configurations that will override both the default and the local DDC path configuration options:

-   A Zenserver path override via an environment variable (`UE-ZenDataPath`).
    
-   A Zenserver path override via a command line argument (`-ZenDataPath=<path>`).
    

We recommend that you select an appropriate path for Zenserver data (both DDC and cooked output) by setting the global local DDC path using the [Edit > Editor Preferences](/documentation/en-us/unreal-engine/unreal-editor-preferences) menu item, then selecting the General > Global section.

![Editor Preferences > General > Global menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4b5e031-8d12-4baf-9825-21c939898d85/image_5.png)

We advise that you select a global local DDC path (and implicitly for Zenserver), that is:

-   A fast, **local** drive.
    
-   Not a network drive.
    
-   Not a virtual drive like Google drive.
    

## Storage of Multiple Cooked Output Platforms, Projects, and Workspaces

Zenserver operates as a single storage service for all cooked platforms, projects, and workspaces. It is designed to store data for one or many cooked outputs for different platforms, projects, and workspaces without data from one overwriting data from another. Internally, data is stored using content-addressable storage, which provides the benefit of de-duplication. This means if you have two projects that both cook the same piece of data and produce the same output bytes for some target platform, Zenserver will only store those bytes once on your hard drive, with each project having a reference to that blob in the underlying content addressable storage layer.

## Data Deletion and Cleanup

Within Zenserver, cooked output data is stored using references into a content-addressable storage layer. Data is retained as long as something is referencing it.

Zenserver will periodically perform garbage collection, and if during garbage collection it finds that some data no longer has any references, that data will be evicted and you can recoup the disk space it was using.

For cooked output data, referencing is controlled by the presence of the `ue.projectstore` file. If you have cooked to Zenstorage, it will have produced a `ue.projectstore` file and that file will be used as a marker indicating a reference to the cooked data. At the time of garbage collection within Zenserver, if:

-   The `ue.projectstore` file has been deleted
    
-   The `ue.projectstore` file modification time is greater than 14 days old
    

then the cooked data will not be considered to have a reference from that cooked output. If no cooked output contains a reference to a piece of data, then that piece of data will be evicted by garbage collection, and space for it on the disk will be recouped.

## Inspection and Debugging

Cooked output data stored in Zenserver has limitations around your ability to debug and inspect it.

In the meantime, there is a small utility program named Unreal Zen Dashboard (program name: ZenDashboard) that can be used to inspect basic stats about Zenserver and issue some basic control commands. You can access this utility program by clicking the **Derived Data** button in the bottom right of the editor, then selecting **Launch Zen Dashboard.**

If you have enabled Zenserver as a cooked output store, you could encounter a situation where you want to run a cook to loose files on the filesystem instead of storing them in Zenserver. To do this, you can pass the following argument when invoking the cook commandlet:

Cook Commandlet

```
`-skipzenstore`
Copy full snippet
```
\-skipzenstore

Low-level debugging functionality is accessible through the use of a command prompt utility for interacting with the local Zenserver. This is accessed through the Zen Dashboard using the **Tools > Launch Utility Command Prompt** menu sequence.

![The Launch Utility Command Prompt menu option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d99ad16-ceb1-4133-b699-eba3e79c42aa/image_7.png)

This gives access to a number of commands for interacting with data in the local Zenserver.

# Impact on Staged Data

Staging is the next step in the content pipeline after cooking. Staging is invoked using Unreal Automation Tool (UAT), either directly or by the editor. This allows staging to either:

-   **Container files**: Cooked output data is aggregated and optionally compressed into a handful of `*.pak`, `*.utoc`, and `*.ucas` files under your project’s `Saved/StagedBuilds/<Platform>` directory.
    
-   **Loose files**: Cooked output data is copied one-for-one into subdirectories of your project’s `Saved/StagedBuilds/<Platform>` directory.
    

Staging to container or loose files is controlled by the presence or absence of the `-pak` commandline argument when invoking Unreal Automation Tool. Using Zenserver as a cooked output store influences the output of the cooking step, which means the staging step must also adapt as described below.

## When Staging to Container Files

When using Zenserver as cooked output store, staging to container (`*.pak`, `*.utoc`, `*.ucas`) files will cause the Unreal Automation Tool (and the UnrealPak executable that it spawns) to obtain cooked output data from Zenserver instead of from the filesystem.

If Zenserver needs to be launched to obtain the data, Unreal Automation Tool and UnrealPak are both capable of launching it automatically. When the cooked output data is obtained from Zenserver, the data is aggregated (and optionally compressed) as it would have been in the past. This means that the output of staging is identical to what it would have been before enabling Zenserver as cooked output store: the `Saved/StagedBuilds/<Platform>` directory will contain the same data in the same files (including the same `*.pak`, `*.utoc`, and `*.ucas` files) as it did before you enabled Zenserver as a cooked output store.

Notably, the staged build directory will **not** contain a `ue.projectstore` file.

The overall content pipeline when staging to container files while using Zenserver as cooked output store looks like this:

## When Staging to Loose Files (Without Containers)

When using Zenserver as a cooked output store, staging to loose files will have significantly different behavior.

Instead of copying cooked output files, the staged build will not contain cooked output data at all, which greatly reduces the deployed size of the game in the staging directory and on the target platform. Instead, it will contain the ue.projectstore that includes information about the Zenserver that is storing the cooked output data.

The presence of this `ue.projectstore` file allows the game runtime to connect to Zenserver and stream cooked data on demand. See documentation for [Zen Streaming](/documentation/en-us/unreal-engine/how-to-use-zenserver-streaming-to-play-on-target-in-unreal-engine) for more information.

The overall content pipeline when using Zenserver streaming looks like this: