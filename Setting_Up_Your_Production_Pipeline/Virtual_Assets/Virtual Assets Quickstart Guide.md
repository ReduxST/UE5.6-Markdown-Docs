# Virtual Assets Quickstart Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-assets-quickstart-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-assets-quickstart-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:07

---

This guide explains how to virtualize a small sample or test project.

## 1\. Required Setup

This guide does not require a specific platform or template project, and you can follow along with any Unreal Engine project. However, your project must be set up to use **Perforce** as source control, and you need to set up the **in-editor check-in workflow**. For more information about Perforce setup, refer to [Using Perforce as Source Control](/documentation/en-us/unreal-engine/using-perforce-as-source-control-for-unreal-engine) and [Source Control Inside Unreal Editor](/documentation/en-us/unreal-engine/using-source-control-in-the-unreal-editor).

You also need to set up a **shared Derived Data Cache (DDC)** for your project to act as your fast cache storage. For more information, refer to [Derived Data Cache (DDC)](/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine).

## 2\. Config File Setup

Open your project's `DefaultEngine.ini` file and add the following text:

```

	`[Core.ContentVirtualization] 	SystemName=Default  	[Core.VirtualizationModule] 	BackendGraph=VABackendGraph_Example  	[VABackendGraph_Example] 	PersistentStorageHierarchy=(Entry=SourceControlCache) 	CacheStorageHierarchy=(Entry=DDCCache) 	SourceControlCache=(Type=p4SourceControl, DepotRoot="...") 	DDCCache=(Type=DDCBackend)`
Copy full snippet
```
\[Core.ContentVirtualization\] SystemName=Default \[Core.VirtualizationModule\] BackendGraph=VABackendGraph\_Example \[VABackendGraph\_Example\] PersistentStorageHierarchy=(Entry=SourceControlCache) CacheStorageHierarchy=(Entry=DDCCache) SourceControlCache=(Type=p4SourceControl, DepotRoot="...") DDCCache=(Type=DDCBackend)

This enables virtualization for all currently-supported assets. These settings have the following impact:

-   **VABackendGraph\_Filesystem** defines a backend graph.
    
-   **SourceControlCache** defines your Perforce source control system as a backend for virtualized payloads and provides an alias to reference it with. Change the DepotRoot value to your project's root directory.
    
-   **DDCCache** defines your shared DDC as a backend for virtualized payloads and provides an alias to reference it with.
    
-   **CacheStorageHierarchy** sets DDCCache as your fast cache storage backend. If your project can find bulk data payloads here, it will prefer pulling that data from this source.
    
-   **PersistentStorageHierarchy** sets SourceControlCache as the persistent storage backend. This is a location where your project is guaranteed to find bulk data payloads if all other backends fail.
    

Refer to the [Backend Graphs](/documentation/en-us/unreal-engine/backend-graphs-for-virtual-assets-in-unreal-engine) page for more details about defining backends for your project.

## 3\. Virtualize a Package

After enabling Virtual Assets, any package you submit from the editor in your project should be virtualized when submitted. This will work for any editor submission method.

The **Unreal Virtualization Tool** can also submit change lists. The source code for the Unreal Virtualization Tool is located in `Engine\Source\Programs\UnrealVirtualizationTool\`. To use it, compile the tool, then run it in a command line with the following arguments:

```

	`-ClientSpecName=[WorkspaceName] -Mode=Changelist -Changelist=[Changelist]`
Copy full snippet
```
\-ClientSpecName=\[WorkspaceName\] -Mode=Changelist -Changelist=\[Changelist\]

| **Command** | **Description** |
| --- | --- |
| ClientSpecName | The name of the workspace to submit from. |
| Changelist | The changelist to virtualize and submit. |

Normally you should not virtualize assets without submitting them. However, this tool makes it possible by adding `-NoSubmit` to the command line. The packages in the changelist will be virtualized, but the changelist itself will not be submitted.

## 4\. Validate Your Virtualized Package

To determine whether your package has successfully virtualized, hover your mouse over the asset in the content browser and check the **Has Virtualized Data** entry.

![Verify that your asset virtualized by hovering over it with your mouse cursor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0974c6b-e7a0-4914-8039-4730e05a779a/verifyvirtualasset.png)

Alternatively, you can look at the file size of the asset. If the `.uasset` file is significantly smaller than it was before you virtualized it, the bulk data was separated from the `.uasset` and is now contained in the **Saved/VirtualizedPayloads** directory.

To investigate the contents of the package file, right-click the asset in the **Content Browser**, click **Copy File Path**, then input the following command in the console:

```
	`DumpPackagePayloadInfo [file path]`

Copy full snippet
```
DumpPackagePayloadInfo \[file path\]

Replace `[file path]` with the file path you copied from the Content Browser.

This console command can take either a full path or a package path, and it will write a summary of the payloads in the output window. The output displays a list of the locally stored payloads followed by a list of the virtualized payloads. `DumpPackagePayloadInfo` does not use any cached information, such as the asset registry. Instead, it re-parses the package's information each time you use it, so the information it provides should always be up to date.

## Configure Virtual Assets for Your Project

Now that you have a basic implementation of Virtual Assets in place, you can configure it to suit your project's needs. The following pages provide more information about the ways you can customize your setup:

-   [Virtual Assets Overview](/documentation/en-us/unreal-engine/overview-of-virtual-assets-in-unreal-engine) has guidelines about how to configure and deploy Virtual Asset support in your project.
    
-   [Backend Graphs for Virtual Assets](/documentation/en-us/unreal-engine/backend-graphs-for-virtual-assets-in-unreal-engine) provides information about setting up Virtualization Graphs.
    
-   [Debugging Virtual Assets](/documentation/en-us/unreal-engine/debugging-virtual-assets-in-unreal-engine) explains how to output information about Virtual Assets for troubleshooting and debugging.