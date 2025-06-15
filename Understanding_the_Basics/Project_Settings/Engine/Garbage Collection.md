# Garbage Collection

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/garbage-collection-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/garbage-collection-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:25:12

---

## Garbage Collection

### General

| **Section** | **Description** |
| --- | --- |
| **Time Between Purging Pending Kill Objects** | Time in seconds (game time) to wait between purging object references to objects that are pending kill. |
| **Flush Streaming On GC** | If enabled, streaming will be flushed each time garbage collection is triggered. |
| **Number Of Retries Before Forcing GC** | 
Maximum number of times GC can be skipped if worker threads are currently modifying UObject state.

0 means GC is never forced.



 |

### Optimization

| **Section** | **Description** |
| --- | --- |
| **Allow Parallel GC** | If enabled, garbage collection will use multiple threads. |
| **Incremental BeginDestroy Enabled** | If enabled, the engine will destroy objects incrementally using a time limit each frame (few objects every frame). |
| **Multithreaded Destruction Enabled** | If enabled, the engine will free objects' memory on a worker thread. |
| **Create Garbage Collector UObject Clusters** | If enabled, the engine will attempt to create clusters of objects for better garbage collection performance. |
| **Asset Clustering Enabled** | Specifies whether to allow Asset files to create Actor clusters for GC. |
| **Actor Clustering Enabled** | Specifies whether to allow Levels to create Actor clusters for GC. |
| **Blueprint Clustering Enabled** | Specifies whether to allow Blueprint classes to create GC clusters. |
| **Use DisregardForGC On Dedicated Servers** | If disabled, `DisregardForGC` (a garbage collection optimization) will be disabled for dedicated servers. |
| **Pending Kill Enabled** | If enabled, objects marked as `PendingKill` will be automatically nulled and destroyed by Garbage Collector. |
| **Minimum GC Cluster Size** | Minimum size of GC cluster. |
| **Maximum Object Count Not Considered By GC** | 
Maximum object count not considered by GC.

Works only in cooked builds.



 |
| **Size of Permanent Object Pool** | 

Size of Permanent Object Pool in bytes.

Works only in cooked builds.



 |
| **Maximum Number of UObjects that Can Exist in Cooked Game** | 

Maximum number of UObjects that can exist in the cooked game.

Keep this as small as possible.



 |
| **Maximum Number of UObjects that Can Exist in the Editor Game** | 

Maximum number of objects that can exist in the editor game.

Make sure this can hold enough objects for the editor and commandlets within a reasonable limit.



 |

### Debug

| **Section** | **Description** |
| --- | --- |
| **Verify FGCObject names** | If enabled, the engine will verify if all `FGCObject`\-derived classes define `GetRef+erencerName()` function overrides. |
| **Verify UObjects Are Not FGCObjects** | If enabled, the engine will throw a warning when it detects a `UObject`\-derived class which also derives from `FGCObject`, or any of its members is derived from `FGCObject`. |