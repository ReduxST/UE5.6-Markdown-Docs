# Virtual Assets Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-virtual-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-virtual-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:16

---

As projects grow larger and reach later stages of development, both the size and number of assets increase. This results in several common pain points:

-   Syncing large projects from source control takes increasingly longer amounts of time for all developers. This potentially creates a high opportunity cost for syncing a new workspace.
    
-   Larger projects use a large amount of hard drive space for each individual developer.
    
-   Developers with slow internet speeds suffer from even slower syncs than their team members due to large file transfers and high data use.
    
-   Source control systems often perform duplicate work, distributing multiple copies of identical files.
    

**Virtual Assets** provide a faster and more efficient method for syncing data among all members of your team as your project grows in size. The core goal of the Virtual Asset system is to reduce the disk space requirements of projects by storing editor bulk data separately from core asset metadata.

This guide provides an overview of how Virtual Assets work and how to use them in your project.

## How Virtual Assets Work

When working with [Assets](/documentation/en-us/unreal-engine/assets-and-content-packs-in-unreal-engine), users only need a minimal amount of information about their assets to display them in the editor. For example, a [Texture](/documentation/en-us/unreal-engine/textures-in-unreal-engine) only needs a thumbnail image and editor properties (such as coordinates and scale) to appear in the Content Browser. Otherwise, the bulk of the `.uasset` file for textures is pixel data, which the user might never call to load.

Virtual Assets separate this information into two parts:

-   **Core asset metadata** – portions that exist where the assets are in your source control.
    
-   **Bulk data** – The main part of the asset's data, held in a shared [**Derived Data Cache (DDC)**](/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine) in a separate location within your source control.
    

This makes it possible to sync only the core asset data when you sync your project in source control. You can then browse the assets as if you had them on your machine, and selectively sync and load their bulk data when needed. Virtual Assets also support the use of different feature development branches, which provides a way to keep experimental features from affecting other team members until they are stabilized.

## Benefits of Virtual Assets

Virtual Assets provide the following benefits. These are most strongly felt on large projects with growing data footprints, but can benefit projects of all sizes.

#### Sync to Projects Faster

Individual contributors only sync bulk data for files when they need them. This uses significantly less data, which can be beneficial if you do not have access to a high-speed connection, and reduces the amount of sync time needed to pull a project. This is especially useful on live service games with a large backlog of assets.

#### Store Less Data

Bulk data lives primarily in your source control or in a derived data cache in a centralized location rather than on individual developers' hard drives. This means that your projects use less hard drive space for your team members. The savings depend on what types of assets are in your project, but a 5x or greater reduction in hard drive use is common.

#### Reduce Duplication

If you have multiple workspaces for your project, this can result in duplicates of many identical files. If you use Virtual Assets with a shared DDC, these files are de-duplicated, further reducing the footprint on individual users' machines.

## Requirements for Virtual Assets

The following requirements must be met to use Virtual Assets in your project.

### Source Control

To use Virtual Assets, you need to integrate your project with Perforce. We recommend using the Unreal Editor check-in workflow as well, as this ensures that files will be virtualized when checked in.

### Shared DDC (Optional)

Using a Derived Data Cache is not required to use Virtual Assets, but we do recommend it, as these can have better performance than accessing Perforce. DDC backends should only be used as your cache storage, as DDCs are not usually safe for use as persistent storage.

### Internet Connectivity

Virtual Assets work well if your users have reasonable access to a shared data cache with a reliable, fast connection. Otherwise, it is reccomended to accomodate the sync time and storage space in advance, as the user may see noticeable hitches without a reliable internet connection.

Unreal Editor cannot continue execution after failing to pull a payload because of the high risk of data corruption. Instead, the user is presented with the option of retrying the pull operation or quiting the editor.

We don't recommend the virtual assets system if your team does not have access to reliable internet connections.

## How to Deploy Virtual Assets

Virtual Assets are currently disabled by default. You can enable them by adding the following properties in your project's `DefaultEngine.ini` file:

DefaultEngine.ini

```
	`[Core.ContentVirtualization] 	SystemName=Default  	[Core.VirtualizationModule] 	BackendGraph=VABackendGraph_Example  	[VABackendGraph_Example] 	PersistentStorageHierarchy=(Entry=SourceControlCache) 	CacheStorageHierarchy=(Entry=DDCCache) 	SourceControlCache=(Type=p4SourceControl, DepotRoot=[asset location]) 	DDCCache=(Type=DDCBackend)`
Copy full snippet
```
\[Core.ContentVirtualization\] SystemName=Default \[Core.VirtualizationModule\] BackendGraph=VABackendGraph\_Example \[VABackendGraph\_Example\] PersistentStorageHierarchy=(Entry=SourceControlCache) CacheStorageHierarchy=(Entry=DDCCache) SourceControlCache=(Type=p4SourceControl, DepotRoot=\[asset location\]) DDCCache=(Type=DDCBackend)

In the above example, replace "\[asset location\]" with the path to the location on your Perforce server where you want to store the virtualized payloads. Make sure your path is surrounded with quotation marks.

These settings enable virtualization for all assets that are currently supported. From this point on, any assets you commit to your repository using the editor or the Unreal Virtualization Tool will virtualize automatically. Once the payloads are virtualized, they are stored permanently in Perforce at the location you provided and will be temporarily cached in DDC using your project's usual DDC settings for faster access.

To check that a package is virtualized, hover over the asset in the content browser. If the tooltip's entry for Has Virtualized Data says `true`, the asset has been successfully converted to using the Virtual Asset system.

![Hover over an asset to verify that it virtualized](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54a1363d-04b5-46e8-83bc-092c64735419/verifyvirtualizeddata.png)

For more information about how to configure Virtual Assets, including the above config file, refer to the [Virtual Asset Quickstart Guide](/documentation/en-us/unreal-engine/virtual-assets-quickstart-in-unreal-engine).

### How to Manually Target Files

If you want to virtualize assets without having to make changes to files, use the **Unreal Virtualization Tool** to convert them. The source code for this tool is located in `Engine\Source\Programs\UnrealVirtualizationTool\`. After you compile the Unreal Virtualization Tool, run it in a command line with the following arguments:

Command Line

```
	`-ClientSpecName=[Workspace Name] -Mode=Changelist -Changelist=[Changelist Number]`
Copy full snippet
```
\-ClientSpecName=\[Workspace Name\] -Mode=Changelist -Changelist=\[Changelist Number\]

-   **ClientSpecName:** the name of the workspace to submit from.
    
-   **Changelist:** The change list to virtualize and submit.
    

All files contained in the targeted Changelist will be converted to using Virtual Assets, then submitted.

### Define Your Project's Backend

**Backend graphs** define where Unreal Engine stores virtual assets in your project's backend. This is defined mainly by two lists:

-   **CacheStorageHierarchy:** Fast backends used to speed up pulling operations. It is preferable to find payloads in these backends, but not essential.
    
-   **PersistentStorageHierarchy:** Slower, but more reliable backends. You must always be able to find files in Persistent Storage.
    

When developers pull payloads, the system looks at the backends in CacheStorageHierarchy first, then if it does not find the requested data in one of those backends, it falls back to PersistentStorageHierarchy. If either list contains more than one backend entry, the system processes them in the same order they are listed, so they should be listed in order from fastest to slowest. Typically, CacheStorageHierarchy contains shared DDCs, whereas PersistentStorageHierarchy would refer to your source control system.

You can define a backend graph in your `DefaultEngine.ini` file alongside the other config variables for Virtual Assets. The following is an example backend graph with placeholder names:

DefaultEngine.ini

```
	`[VABackendGraph_Example] 	PersistentStorageHierarchy=(Entry=SourceControlCache) 	CacheStorageHierarchy=(Entry=DDCCache) 	SourceControlCache=(Type=p4SourceControl, DepotRoot="...") 	DDCCache=(Type=DDCBackend)`
Copy full snippet
```
\[VABackendGraph\_Example\] PersistentStorageHierarchy=(Entry=SourceControlCache) CacheStorageHierarchy=(Entry=DDCCache) SourceControlCache=(Type=p4SourceControl, DepotRoot="...") DDCCache=(Type=DDCBackend)

To target a backend graph, set the `BackendGraph` variable under `[Core.ContentVirtualization]` to the name of the graph you want to use.

DefaultEngine.ini

```
	`[Core.ContentVirtualization] 	BackendGraph=VABackendGraph_FileSystem`
Copy full snippet
```
\[Core.ContentVirtualization\] BackendGraph=VABackendGraph\_FileSystem

For more information about how to build a backend graph, refer to the [Backend Graphs for Virtual Assets](/documentation/en-us/unreal-engine/backend-graphs-for-virtual-assets-in-unreal-engine) page.

## Guidelines for Virtual Assets

The following sections provide advice for how you should incorporate Virtual Assets into your project.

### Methods for Virtualizing Assets

If you are starting a new project, you should start using Virtual Assets immediately. This will give your team all the performance benefits without the problems that can occur if you add Virtual Assets later, providing the smoothest development experience.

If you are adding Virtual Assets to an existing project, then you need to consider whether you want to use manual, bulk, or rolling methods for adding this support. Which approach is right for your project depends on its scope and your production timeline.

#### Bulk Virtualization

Virtualizing an entire project all at once gains the best sync performance as quickly as possible, but becomes riskier the larger your project is. All binary content has to be checked in to make the switch possible. Additionally, all the bulk data for your project is pushed to the shared DDC at once, which poses potential security risks. This can result in significant disruptions to your project, which may be infeasable for especially large projects in later stages of production.

#### Virtualizing in Batches

To avoid disruptions, you can use a script to periodically run the Unreal Virtualization Tool with a pre-determined set of changelists, effectively virtualizing your assets in batches. This makes it possible to handle different teams or features in stages while ultimately ensuring you apply Virtual Asset use globally.

#### Manual Virtualization

Virtualizing only specific folders provides a greater degree of control over which assets have bulk data in your shared DDC, which also makes it easier to roll out Virtual Assets in stages. However, you will only improve sync performance in the features or folders that you have given direct attention to.

To get the most benefit immediately with the least disruption to your project, you should target the largest assets in your project. You can also safely target assets that haven't changed in a long time.

To ensure you apply the benefits of Virtual Assets widely, you can virtualize assets as team members save their files. While this will not catch assets that your team isn't actively working on, it ensures that Virtual Assets are introduced steadily over time.

#### Summary of Guidelines

-   If you are starting a new project, you should start using Virtual Assets immediately.
    
-   If your project is in mid or late production, you may not want to implement Virtual Assets on content you are heavily iterating, as this can disrupt your project. However, you could safely virtualize assets that your team has not changed for a long time.
    
-   To limit the impact of switching to Virtual Assets on your project's stability, but still benefit from them, you can also target only the largest assets in your project.
    

## Caveats for Virtual Assets

Although Virtual Assets are beneficial, there are some cases where they can introduce complications to your project or lose effectiveness.

### Network and Asset Usage

Several factors in a user's network connection can reduce the effectiveness of the Virtual Asset system:

-   Slow network connection to a DDC.
    
-   No access to a DDC.
    
-   Very few people using similar assets.
    

If any of the above are true, the bulk data pull might be so slow that users will compile and cook many or all assets locally. This uses the same amount of disk space and may take longer than just syncing upfront.