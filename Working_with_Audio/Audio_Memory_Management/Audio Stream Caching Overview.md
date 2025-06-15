# Audio Stream Caching Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/an-overview-of-audio-stream-caching-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/an-overview-of-audio-stream-caching-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:35

---

**Audio stream caching** significantly changes the way audio is loaded and released from memory.

At cook time, almost all compressed audio data is separated from the `USoundWave` asset and placed at the end of the `.pak` file. This makes it possible for audio to be loaded into memory at any point, and released again when it has not been recently used.

This method of memory management is popular for open world games, where the actual audio needed for a specific use case is difficult to determine ahead of time. The primary disadvantage of this method is that just because `USoundWave` is loaded, this does not guarantee that the audio will be immediately playable. However, the benefit is a system that lets designers reference as many audio assets as they want without overstepping memory boundaries. The system also provides a way for engineers to load and reference chunks of compressed audio without relying on the state managed by the audio engine. Also, mitigating latency when playing back audio with the stream cache is easier than mitigating memory issues without the stream cache.

## Determining the Right Cache Size

The **Max Cache Size** is a hard limit for memory used by the compressed audio data, with the exception of headers and sounds explicitly marked to stay in memory. When a cache is too small, sounds will be unloaded too quickly, causing latency when loading sounds.

### An Extreme Example

If your cache limit is set to 8 MB, chunks are a maximum of 256 KB each, so you could have 32 chunks in your cache at any time. This means that if you are playing 32 sounds at once, no more chunks can be loaded.

### A Less Extreme Example

Now assume your cache limit is set to 16 MB. This would allow for 64 256-KB chunks in the cache. If you are playing 32 sounds at once, you have room to prime 32 more sounds. However, if all 32 sounds you are playing are long enough to be in multiple chunks, The next chunk in sequence will stay loaded into the cache automatically. This means that any sounds you try to prime during this time will be stomped by the 32 chunks that are loaded in advance for your 32 playing sounds.

### A Normal Example

If your cache limit is set to 32 MB, it can contain 128 elements, each at a max of 256 KB. If you are playing 32 sounds at the same time, you still have 96 additional chunks of audio you can keep in the cache to avoid latency. If your limit is 48 MB, you have room for 192 elements, so even if you play 32 sounds concurrently, you can keep 160 chunks primed.

## Configuring the Cache Size

1.  With the project open, from the main menu, select **Edit > Project Settings**.
    
2.  From the **Project** menu, go to **Platforms > Windows > Audio > Compression Overrides > CookOverrides > Stream Caching**.
    
3.  Set **Max Cache Size (KB)** to determine how many elements are in the cache.
    

When the value is set to **0**, the value defaults to 32 KB. The max cache size is 2,147,483,647 MB, but you should be cautious of using a cache size so large that it would cause the machine you are running on to run out of memory.

![Configuring the Cache Size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6242ece6-2acb-469b-a0a9-5c4b3def6b8c/01-configure-cache-size.png)

## Avoiding Latency by Caching Sounds In Time

Ideally, sounds are always in memory by the time they play. This can be achieved the following ways.

### Priming a Sound for Playback

If you anticipate that a sound is going to play in the near future, you can call *Prime Sound For Playback* in Blueprints (or `UAudioMixerBlueprintLibrary::PrimeSoundForPlayback` from C++):

![Prime Sound For Playback](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e05a8489-c36c-4d8a-81a0-bf2c6d44955b/02-priming-sound-for-playback.png)

For example, in an open world game, vehicle sounds and radio stations are loaded into the cache when the player comes within a few feet of a car. If the player does not enter the car, the sounds remain in the cache until they are eventually released.

Sound Cues can also be primed, but no delegate fires when loading is complete. (A **delegate** is a Class that wraps a pointer or reference to an object instance—a member method of that object's Class to be called on that object instance, and that provides a method to trigger that call.)

![Prime Sound Cue for Playback](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74c89aae-dee0-424a-91d2-e5f34431eed1/03-priming-sound-cue-for-playback.png)

### Setting the Default Loading Behavior for a Sound

If you expect sounds to play shortly after they are loaded, you can set the Loading Behavior of a Sound Wave to **Prime on Load**:

![Setting the Default Loading Behavior for a Sound Wave](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49c0a1ed-a4f4-4932-9823-37fb7a315f20/04-set-loading-behavior-for-sound.png)

You can also set the Sound Class Loading Behavior for a Sound Wave to **Prime on Load**:

Additionally, you can set all Sound Waves to prime on load by setting `au.streamcache.DefaultSoundWaveLoadingBehavior` to **2**.

## Keeping Sounds In Memory

If a sound must play with zero latency under any circumstance, it can be useful to keep it in memory for the full duration of the `USoundWave` life span.

### Forcing a Sound Wave to Stay in Memory

When you set the Loading Behavior for a Sound Wave to **Retain on Load**, you set that sound's first chunk of audio to live in the cache forever.

You can set all Sound Waves to retain their first chunk by default by setting `au.streamcache.DefaultSoundWaveLoadingBehavior` to *2*.

## Trimming Memory

If the application requires more memory, you can release unused chunks of audio from the cache using the **Trim Audio Cache** function (`UAudioMixerBlueprintLibrary::TrimAudioCache`).

![TrimmingMemory.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69b6115d-3829-403f-ad52-c395efdf6354/trimmingmemory.png)

The **Trim Audio Cache** function iterates through the cache and frees chunks that are not in use until you reach the amount specified by the **In Megabytes To Free** argument. The function returns memory that was freed successfully.

When called from C++, this function is thread safe. However, keep in mind that it locks the cache, and is potentially expensive. This means that streaming audio may underrun while the function is running.

## Blowing the Cache

If you try to load or play a chunk of audio while every element of the cache is in use (either because chunks are playing or are in the process of loading in from disk), you will blow the cache. In this case, this ensures hits in `AudioStreamingCache.cpp`:

![BlowingCache.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a28ad9e-ad72-49f4-9e3d-abb63cb7b741/blowingcache.png)

If you are consistently blowing the cache, you have five options:

*Increase the size of your cache.* Decrease the amount of Sound Waves you are retaining. *Decrease your voice limit.* Decrease the amount of sounds you are attempting to load when the cache is blown. \* Ignore it and drop chunk requests.

## Increasing Worst-Case Cache Utilization

For cases where you have many short sounds, the cache will be filled with tiny chunks, and you will only use a small part of your cache size.

For example, if your cache is 128 chunks long and the max chunk size is 256 KB, and you load in a large number of 64-KB sounds, you will only use 8 MB of your cache when the limit is 32 MB.

To compensate for this, you can set your maximum number of chunks to be larger than the **MaxCacheSize/MaxChunkSize**, keep a running counter of the number of bytes currently allocated in the pool, and evict the least recent chunk, either when that memory counter hits your cache size or when you hit your maximum number of chunks. You determine your maximum number of chunks using the cvar `au.streamcaching.MinimumCacheUsage`.

### Setting au.streamcaching.MinimumCacheUsage

The `au.streamcaching.MinimumCacheUsage` can be set between **0.0–1.00**. This can only be set before the `IAudioStreamingManager` is initialized. Setting this during gameplay will not affect anything.

Increasing this value increases the maximum number of chunks that can be in the cache. For example, if `au.streamcaching.MinimumCacheUsage` is 0.75 and your cache size is 32 MB, your maximum number of chunks would be 512. If you loaded in a large number of 64-KB audio assets, you would still be able to use 32 MB. This means that the closer `au.streamcaching.MinimumCacheUsage` gets to 1, the lower the average size of a chunk is needed to fully utilize the cache.

| au.streamcaching.MinimumCacheUsage | Cache Size (Megabytes) | Maximum Number of Chunks | Minimum Average Size of a Chunk in KB for 100% Utilization |
| --- | --- | --- | --- |
| 0.0 | 32 | 128 | 256 |
| 0.0 | 16 | 64 | 256 |
| 0.5 | 32 | 256 | 128 |
| 0.5 | 16 | 128 | 128 |
| 0.75 | 32 | 512 | 64 |
| 0.75 | 16 | 256 | 64 |
| 0.825 | 32 | 1024 | 32 |
| 0.825 | 16 | 512 | 32 |

We can never guarantee 100% cache utilization for any size of an individual audio asset, because that would require the Maximum Number of Chunks to be infinite.

Increasing `au.streamcaching.MinimumCacheUsage` has the following implications:

-   Average case disk IO reads decrease, because you keep more audio cached in the worst case.
-   Average case memory usage increases, since you can handle more chunks when they are smaller.
-   Average case CPU cost for finding a chunk in the cache increases.
-   Costs for insertion/eviction of chunks remain the same.

### Using au.streamcaching.TrimCacheWhenOverBudget

The `au.streamcaching.TrimCacheWhenOverBudget` value defaults to **1**. This solves a potential vector for leaked memory in the streaming cache when `au.streamcaching.MinimumCacheUsage` is set to any value greater than zero. The leak occurs when you evict a small asset for a large asset in the LRU cache. Since this can happen many times in sequence, it results in cache usage that is much larger than your targeted max cache size.

The solution that `au.streamcaching.TrimCacheWhenOverBudget` uses is to trim your least recently-used chunks until you get back under budget. The trade-off is that calls to prime or play a sound may result in less-recently used sounds being evicted.

## Prioritizing Audio Reads

Chunks of audio are read from the disk using instances of `IAsyncReadRequest`, similarly to your texture streaming and geometry streaming systems. Because of this, you can prioritize audio chunk loading above or below other streaming systems in the engine using the cvar `au.streamcaching.ReadRequestPriority`. This value can be set from 0 to 4, where 0 is the highest priority and 4 is the lowest. The default value for cached audio streaming requests is **2**.

| au.streamcaching.ReadRequestPriority | AsyncIOPriority | Other Streaming Managers that use this priority |
| --- | --- | --- |
| 0 | AIOP\_High | Animations, Textures, Shader Code |
| 1 | AIOP\_Normal | Async Pak Reads |
| 2 | AIOP\_BelowNormal | Geometry Streaming |
| 3 | AIOP\_Low |   |
| 4 | AIOP\_MIN |   |