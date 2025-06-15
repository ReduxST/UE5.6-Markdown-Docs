# Backend Graphs for Virtual Assets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/backend-graphs-for-virtual-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/backend-graphs-for-virtual-assets-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:36

---

The Virtual Assets system stores bulk data payloads for assets in a *backend*, typically a source control repository, **Derived Data Cache (DDC)**, or some other form of remote storage. When users need to edit a Virtual Asset, the system pulls the bulk data from the backend and loads it on their computer. However, all backend solutions have their own balance of speed, storage space, reliability, and practicality.

To get the best of all possible solutions, the Virtual Assets system uses **backend graphs** to look for files in multiple backends, using each type of backend for a different type of storage. Faster backends can contain temporary caches for frequently-used files, while slower ones can be used for long-term, persistent storage. This guide acts as a reference for how to configure backend graphs for your own projects so that you can tailor your project's use of virtual assets to optimize the process of running pulls.

## Overview

Backend graphs are groups of parameters in your `*Engine.ini` file that define what backends are available to pull bulk data from, as well as the order of priority that the Virtual Assets system uses when determining which ones it should pull from first.

### Storage Lists

Each backend graph is built mainly around two lists: **CacheStorageHierarchy** and **PersistentStorageHierarchy**.

PersistentStorageHierarchy is a list of slower, but more reliable backends. All of your files should always be available within a persistent storage backend. A typical example of a persistent storage backend would be a source control repository such as Perforce, which offers a permanent, centralized storage solution for all of a team's files, but can vary in performance depending on individual users' internet connections.

CacheStorageHierarchy is a list of faster, but less reliable backends that are used to speed up pulls, especially for frequently-used files. A typical example of cache storage would be a Shared Derived Data Cache (DDC), which would be located on a shared network drive within your organization's workplace. Because this is part of your local network, the DDC would be faster. However, if your team is highly distributed or has a large number of remote team members, a local resource like this would not be available to them, and the system would either need to fall back on something else, or they would need to have their own alternatives.

### Priority

When the Virtual Assets system tries to pull bulk data, it looks at backends in the cache storage list first, then falls back on persistent storage if it can't find the needed files. When it looks at either list, it will look at each backend in the order that they are listed in, so you should try to list them in order from fastest to slowest.

## How to Use Backend Graphs

### Create a Backend Graph

To create a backend graph, open your `DefaultEngine.ini` file and create a new category with the name of your backend graph. For your convenience, you should put it near `Core.ContentVirtualization`.

A backend graph requires the following entries:

-   `CacheStorageHierarchy=(Entry=[Name of Cache])`
    
-   `PersistentStorageHierarchy=(Entry=[Name of Persistent Storage])`
    
-   Entries for each backend you want to use, providing a name, type, and information needed to find a path to it, if applicable.
    

#### Define a Backend

Backends are defined with a name, followed by an entry containing the needed data to find the backend. This provides an alias to use in the Storage Hierarchy lists. Each entry contains the following information:

| **Parameter** | **Description** |
| --- | --- |
| Type | 
Describes the type of backend that the current alias uses. The available Types are as follows:

-   FileSystem – A local file system.
    
-   P4SourceControl – Your Perforce source control system.
    
-   DDCBackend – A shared DDC for your project.
    



 |
| DepotRoot | If using the P4SourceControl type, this is the root path for your depot. |
| Path | If using the FileSystem type, this is the root folder where you are storing payloads. |

#### Add Backends to Your Storage Lists

Each entry in the storage lists uses the format `Entry=[BackendName]`, where \[BackendName\] is replaced with one of the backends you defined. If you list more than one, you need to separate them with commas. For example:

CacheStorageHierarchy=(Entry=DDCCache1, Entry=DDCCache2, Entry=DDCCache3)

```
	`PersistentStorageHierarchy=(Entry=SourceControlCache)`

Copy full snippet
```
PersistentStorageHierarchy=(Entry=SourceControlCache)

When the system parses this information, it will look at each backend in the order it is listed. Therefore, you should list them in order from fastest to slowest.

#### Example

The following is an example of a backend graph with placeholder names:

```
	`[VABackendGraph_Name] 	CacheStorageHierarchy=(Entry=DDCCache) 	PersistentStorageHierarchy=(Entry=SourceControlCache) 	DDCCache=(Type=DDCBackend) 	SourceControlCache=(Type=P4SourceControl, DepotRoot="XXX" )`

Copy full snippet
```
\[VABackendGraph\_Name\] CacheStorageHierarchy=(Entry=DDCCache) PersistentStorageHierarchy=(Entry=SourceControlCache) DDCCache=(Type=DDCBackend) SourceControlCache=(Type=P4SourceControl, DepotRoot="XXX" )

This information is added in your `DefaultEngine.ini` file. The header is the name of the backend graph, and it contains a list of aliases defining which backend graphs are available. For example, `DDCCache` points at a shared DDC, while `SourceControlCache` points at a source control system used in your project. These names are arbitrary and can be changed as meets your needs. Once you have defined these entries, you can put them in the `CacheStorageHierarchy` and `PersistentStorageHierarchy` lists.

### Select a Backend Graph for Your Project to Use

After creating a backend graph, you need to configure your project to use one of them when using the Virtual Assets system.

#### Select a Backend Graph From Configuration Files

Navigate to the `Core.VirtualizationModule` section of your `DefaultEngine.ini` file. The BackendGraph parameter is set to `ContentVirtualizationBackendGraph_None` by default.

```
	`[Core.VirtualizationModule] 	BackendGraph=ContentVirtualizationBackendGraph_None`

Copy full snippet
```
\[Core.VirtualizationModule\] BackendGraph=ContentVirtualizationBackendGraph\_None

Change ContentVirtualizationBackendGraph\_None to the name of your own backend graph. After that, your project will use the graph you defined.

#### Override Your Backend Graph From The Command Line

You can override backend graphs from the command line by using the following command:

```
	`-VABackendGraph=[GraphName]`

Copy full snippet
```
\-VABackendGraph=\[GraphName\]

Where \[GraphName\] is a variable that represents the name of the graph you want to use. To troubleshoot any issues relating to this graph, the log should show the name of the graph from the configuration file, including the name of the graph that is overriding it from the command line, and the name of the graph that gets mounted.

### Recommended Backend Graph Setup

We recommend using your project's source control for the persistent storage solution and a shared DDC cache for your cache storage. You can create more complex schemes as needed for your organization, but this provides the best balance between improved performance and simplicity.

## Notes on Backend Implementations

### P4SourceControl

When you set up a backend for type P4SourceControl, you must provide a DepotPath to the location in perforce that you wish to store the virtualized payloads. However, the system needs to verify that this path is the correct location to avoid accidental submits.

To start using your DepotPath, submit a file named `payload_metainfo.txt` at the DepotPath directoryh. When the system is starting up, it will look for that file at the DepotPath and attempt to download it. The virtual asset system verifies the path is correct and ensures that the user has the correct perforce permissions to be able to access data, as that file is unlikely to exist unless intended for virtual asset storage.