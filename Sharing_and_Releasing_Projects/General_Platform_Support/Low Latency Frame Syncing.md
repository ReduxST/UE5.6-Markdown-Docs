# Low Latency Frame Syncing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/low-latency-frame-syncing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/low-latency-frame-syncing-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:23

---

**Low-latency frame syncing** mode modifies the way thread syncing is performed between the game, rendering and RHI threads, and the GPU, to greatly reduce and control input latency. In previous engine releases, the game thread synced with the rendering thread at the end of the frame. When the **r.OneFrameThreadLag** CVar is enabled (as the default), this syncing ensures that the game thread does not get more than one whole frame ahead of the rendering thread. Platform-specific graphics drivers generally stall the thread that calls Present() to prevent the game running faster than the frames are presenting. The driver allows the swap chain to be filled, and then stalls the calling thread when there is no more room. Before UE4's parallel rendering was introduced, this syncing behavior was correct, as the game thread would wait on the rendering thread, which would then be stalled by the graphics driver/OS. However, with the introduction of parallel rendering, the RHI thread is now the thread that calls Present(), so it is that thread which is throttled by the driver. The game thread continues to sync with only the rendering thread, which allows both these threads to get much further ahead of the GPU and flipped frames than it used to. In a 30 Hz title with **rhi.SyncInterval** set to 2, this can lead to a worst case input latency of up to 130 ms.

To achieve the same input latency as pre-parallel rendering, it is necessary to synchronize the game thread to the RHI thread instead. In addition, when vsyncing is enabled, the swap chain provides a regular, predictable syncing interval, meaning the point in time when the swap chain flips the front/back buffers. We can accurately control input latency by syncing the start of the game thread frame to an arbitrary point relative to the vsync. By carefully choosing this point, we can trade input latency for performance, or the reverse.

The new low-latency frame-syncing mode adds a new CVar called **r.GTSyncType** (game thread sync thread). This CVar drives how the frame syncing mechanism work using the following values:

| **Value** | **Description** |
| --- | --- |
| 0 | Game thread syncs with rendering thread (old behaviour, and default). |
| 1 | Game thread syncs to the RHI thread (equivalent to UE4 before parallel rendering) |
| 2 | Game thread syncs with the swap chain present +/- an offset in milliseconds. |

To achieve mode 2 syncing, the engine tracks presented frames with an index that is passed to the driver when Present() is called. This index is retrieved from platform frame flip statistics, which indicates the exact time when each frame flipped. The engine uses these values to predict when the next frame flip is due, then kicks off the next game thread frame based on this time.

The CVar **rhi.SyncSlackMS** drives the offset we apply to the next predicted vsync time. Decreasing this value will reduce input latency at the cost of shortening the engine pipeline, making it more likely for hitches to cause dropped frames. Likewise, increasing this value will lengthen the engine pipeline, giving the title more resilience to hitches at the cost of increased input latency.

Generally, titles using this new frame-syncing system should aim to reduce **rhi.SyncSlackMS** as much as possible whilst maintaining acceptable frame rates.

Take as an example, a 30 Hz title with the following CVar settings:

-   **rhi.SyncInterval 2**
-   **r.GTSyncType 2**
-   **r.OneFrameThreadLag 1**
-   **r.Vsync 1**
-   **rhi.SyncSlackMS 0**

This would have a best case input latency of ~66ms (two 30 Hz frames). Increasing **rhi.SyncSlackMS** to 10 would result in a ~76ms best-case input latency.

**r.GTSyncType 2** works for 60 Hz titles too (i.e **rhi.SyncInterval** is set to 1), but the benefit of this will be less noticeable as the input latency is halved to start with, given the doubled frame rate vs 30hz.

On unsupported platforms, **r.GTSyncType 2** will fall back to mode 1 instead.