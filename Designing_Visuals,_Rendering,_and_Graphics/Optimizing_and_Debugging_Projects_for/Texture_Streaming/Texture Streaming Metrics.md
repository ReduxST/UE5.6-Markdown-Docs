# Texture Streaming Metrics

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-streaming-metrics-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-streaming-metrics-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:16

---

You can profile texture streaming stats with the `STAT STREAMING` console command. This reports the performance, memory usage, and other metrics used by the texture streamer.

`STAT STREAMING sortby=name maxhistoryframes=1`

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37ccb94f-ccf2-470d-a91c-269777f1cd7a/statstreaming.png)

When reading memory data, the term "pool" refers to the conceptual (reserved) memory, and does not relate to the actual memory taken. The word "mips" maps to memory currently used by textures, rather than to expected or future usage. The memory metrics are classified in three main pools:

-   Texture
-   Streaming
-   Wanted

These pool sizes are indicated on the right of each line in the Memory Counters category.

| Stat | Description |
| --- | --- |
| Cycle Counters |   |
| Game Thread Update Time | The time taken by the streamer update function. This accounts for most of the texture streaming work. Only a few tasks are processed outside the texture streamer, like removing reference to a texture, a component, or a level. During a game thread update, the streamer performs one step toward the full update. The full update takes several frames and relates to `r.Streaming.FramesForFullUpdate`. There are different update steps, as defined in the **Counter** section of the stats. |
| Memory Counters |   |
| Texture Pool | The total memory availabe for texture resources. This includes non-streaming resources like render targets, GPU particle buffers, cubemaps, UI textures, and non-streamable textures. On some platforms, this memory can be used to store non-texture resources like Static Meshes. **Texture Pool** is approximately equal to **Safety Pool** + **Temporary Pool** + **Streaming Pool** + **NonStreaming Mips** (only the amount of the fluctuation, if any, up to the size of the safety pool) |
| Safety Pool | This value is set in the `Engine` configuration file, under `[TextureStreaming]`, as `MemoryMargin`. It is memory reserved for unexpected (non-streaming) allocations. If the memory available fluctuates cyclically by an amount under this value, the texture streamer will stabilize its streaming pool to the maximum taken by this fluctuation. If a normal (expected) fluctuation takes more than the safety pool size, then the texture streamer will constantly adapt its budget, possibly creating infinite cycles of streaming textures in and out. |
| Temporary Pool | 
This value is controlled by `r.Streaming.MaxTempMemoryAllowed` and specifies how much extra memory the streamer is allowed to use when resizing textures. When changing the mip count of a texture, the engine has to create a new texture, either smaller or larger, which will hold the future mip data. This indirectly controls the amount of inflight requests since the streamer sends to the IO system as many requests as the temporary pool allows.

Note that the temporary pool must be at least as large as the largest resource to stream, but setting it too large will waste memory (as it is reserved for that purpose). On the other hand, setting it too small could slow down the streaming speed (not generating enough work for the IO system, making it idle). Note also that the streamer has very little control on the processing order within the inflight requests. That means using a relatively small temporary pool gives better control of what is loaded first.



 |
| Streaming Pool | The amount of memory available to the texture streamer. The streamer will usually take all its available memory to either stream new mips, or to keep previously streamed mips in memory as long as possible. The Streaming Pool contains Visible Mips, Hidden Mips, Force Mips and Cached Mips. **Streaming Pool** is approximately equal to **Visible Mips\*** + **Hidden Mips** + **Forced Mips** + **Cached Mips** (\*: when fully used, otherwise unused space must be accounted for) |
| NonStreaming Mips | The amount of memory used by non-streaming allocations. If those allocations regularly fluctuate by more than the safety pool value, this will affect the streaming pool budget, and should be avoided (by either decreasing the allocations or increasing the safety pool). |
| Required Pool | The amount of mip data the texture streamer needs to load according to its metrics. This can exceed 100% of the texture streaming pool, in which case some compromise will be made and some texture(s) will not be loaded to their required resolution. |
| Visible Mips | The wanted memory currently taken by visible texture mips. This does not include forced mips. |
| Hidden Mips | The wanted memory currently taken by non-visible texture mips. This does not include forced mips. To prevent seeing low resolution textures the first time a texture is shown, the streamer prestreams textures in advance, althought usually with one less mip than required (see [`r.Streaming.HiddenPrimitiveScale`](/documentation/en-us/unreal-engine/texture-streaming-configuration-in-unreal-engine)). |
| Forced Mips | The wanted memory currently taken by textures that are forced in. Textures are usually forced in through gameplay mechanisms for a small period of time. This does not include textures that are flagged as non-streamable. |
| Cached Mips | Memory taken by texture mips that are not needed anymore. They will be kept cached unless their memory is needed by other wanted mips. |
| Wanted Pool | The part of the required pool that will eventually be streamed in. |
| Wanted Mips | How much of the wanted pool is actually streamed in. Once it reaches 100%, the streamer has stopped sending IO requests to load new mips. **Wanted Mips\* is equal to** Visible Mips **+** Hidden Mips **+** Forced Mips\*\* |
| Inflight Requests | How much memory has still to be processed by the IO. When 0, all previous requests have been processed at the time of creating new requests. If this happens when the streamer is streaming content, that would be an indication that the streamer is not using all of the available bandwidth. The bandwith could be increased by increasing `r.Streaming.MaxTempMemoryAllowed` (at the expense of more wasted memory and less load order control), or by decreasing `r.Streaming.FramesForFullUpdate` (at the expense of longer update times). |
| IO Bandwidth | The size of loaded mips completed since the last update, divided by the time since the last update. This is not an accurate IO bandwidth measurement but can still be used to get an idea of how fast the system loads requests. |
| Counters |   |
| Setup Async Task | The time taken to prepare the data for the async streamer task. It runs as the first step of the full update loop. |
| Update Streaming Data | This is the time used to incrementally update the streaming data. This includes refreshing the visibility, updating the texture states, updating the bounds of any used dynamic components. The step will run several frames in a row, as defined by `r.Streaming.FramesForFullUpdate`. |
| Streaming Texture | The time taken to prepare and send the load and cancellation requests. |

## Incremental Processing of Newly Loaded Levels

Starting with Unreal Engine 4.15, the texture streamer processes the level data incrementally, so just a little bit each frame, between the time they are loaded and the moment they become visible. Previously, this processing would happen in the frame the level became visible and could generate some noticeable hitches while doing so.

The amount of work processed each frame is controlled by `r.Streaming.NumStaticComponentsProcessedPerFrame`, which has a default value of 50. Setting **0** for this value will disable the incremental work and it will make the system behave as it did prior to 4.15.

It's important to mention that the incremental level processing will only apply to components with their Mobility set to **Static**. Movable components have always been processed incrementally in the engine tick.

Once the incremental processing completes, no more processing will be required before the level becomes visible. If it becomes visible before the incremental processing completes, then all pending work needs to be finished immediately and there could be a small hitch when this happens.

You can investigate incremental processing by running the console command:

```
	`Stat Streaming SortBy=name`

Copy full snippet
```
Stat Streaming SortBy=name

The cost gets included in the category *Update Streaming Data*.

## Performance

With the improvements to the texture streamer in 4.15, the following information lists describe the targeted improvements with some concrete metrics about how things were improved.

### Reducing The Number Of Textures Taken By the Texture Streamer

This has been improved by handling per-component visibility. Textures that are used by non-visible and hidden components are streamed with one fewer mips, as a prefetch. The addition of the per-material texture streaming data also helped by computing correctly the scales applied to the UV Channels for things like detail maps.

Finally, the other improvements here came from computing (smaller) per-material bounds for static geometry.

The metrics below were taken from Paragon using three different viewpoints around the level.

| Required Texture Pool | Before | After | Amount Visible |
| --- | --- | --- | --- |
| Startup | 678 MB | 564 MB | 370 MB |
| Side Lane of Map | 796 MB | 597 MB | 308 MB |
| Middle Lane of Map | 1086 MB | 674 MB | 271 MB |

### Reducing Time For Visible Textures To Stream In

In order to reduce the amount of time it takes to stream in visible textures (aside from reducing the global texture budget); the streamer keeps a table of visible versus budgeted mips. By keeping track of the visible mips from those that are budgeted, the streamer is able to stream in perceptible data prior to streaming in prefetch and forced load data.

The metrics below were taken from Paragon using three different viewpoints around the level.

| Loading Visible MIPs | Before | After |
| --- | --- | --- |
| Startup | 20s | 10s |
| Side Lane of Map | 19s | 9s |
| Middle Lane of Map | 20s | 6s |

### Reducing CPU Time Taken By The Streamer

The CPU time taken has been improved by moving the dynamic component processing to the async texture streaming task. Other things have also been moved, like the handling of overbudget situations and the determining texture load order.

In the example below, this shows the improvement of the Worst Update Frame from Paragon.

| Game Thread Update Cost | Before | After |
| --- | --- | --- |
| Worst Update Frame | 1.1 ms | 0.6 ms |

Another key improvement in this area is the incremental processing of newly loaded level streaming data while the level is loaded but not yet visible.

| Game Thread Level Loaded Cost | Before | After |
| --- | --- | --- |
| Incemental Update | 150 ms | 3 ms |

### Eliminating Low Quality and Bad Behaviors

Mesh UV densities are computed per material instead of per-mesh. This new data takes into account LODs as well. This resolved most issues where the texture would appear low-resolution.

Also, there is now a wider texture streaming support from the component, including Particle Systems and Instanced Meshes. This resolves other low resolution issues and, sometimes, high memory consumption.

### Eliminating Manual Tweaks for Different Memory Budgets

The texture streamer can automatically fit different memory budgets without the hassle of manual tweaks. The streamer will select which textures need to be reduced using different heuristics to minimize visual impact.

Only the least amount of textures will be affected and the effect is localized so that in different locations the sacrifices will not be the same.