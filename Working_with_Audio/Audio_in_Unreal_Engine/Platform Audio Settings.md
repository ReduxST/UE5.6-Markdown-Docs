# Platform Audio Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/platform-audio-settings-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/platform-audio-settings-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:26

---

Each platform supported by **Unreal Engine** has an **Audio** category in its **Project Settings** menu. This category contains platform-specific options for how your application manages audio, including **Audio Mixer** settings and compression settings. These values override your global audio settings. Although the Audio settings are written to different config files for each platform, all platforms have the same possible settings.

For most audio settings, if you use a value of 0 or lower, that setting will be ignored in favor of the global audio settings.

These settings are written to each platform's `(PlatformName)Engine.ini` file alongside all other platform-specific project settings.

### Configuring Platform Audio Settings

Click **Settings > Project Settings** to open the **Project Settings** window. Go to the **Platforms** section and click on the name of your target platform. Scroll to the **Audio** category and expand it to reveal all the platform-specific audio settings.

![Click Settings - Project Settings to open the Project Settings window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a4f1dbd-2ae6-4a3c-99d4-feb0c97a3f45/platform-audio-settings-1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/689c415f-137e-4d1d-8b46-85e90d7e4a35/platform-audio-settings-1.png)

The following table is a summary of each of these settings.

| Setting Name | Description |
| --- | --- |
| Audio Mixer Sample Rate | The sample rate at which to run the audio mixer. |
| Callback Buffer Size | The amount of audio to compute in each audio callback block. Lower values decrease audio latency, but may increase CPU cost. |
| Number of Buffers to Enqueue | The number of audio buffers to keep enqueued. More buffers increase audio latency, but can compensate for varying availability of threads in the job pool on some platforms. |
| Max Channels | The maximum number of audio voices for this platform. The value used in your application will be the smaller of the two when comparing this setting and the global setting. |
| Number of Source Workers | The number of workers available to compute source audio. Sources are evenly divided between workers. |
| Compression Overrides | A list of audio compression settings that will be overridden for the selected platform. Refer to the Compression Overrides table below for more information. |
| Cook Overrides | A list of cooking settings overridden for the selected platform. Refer to the Cook Overrides table below for more information. |
| Spatialization Plugin | Which of the currently-enabled spatialization plugins to use on this platform. |
| Reverb Plugin | Which of the currently-enabled reverb plugins to use on this platform. |
| Occlusion Plugin | Which of the currently-enabled occlusion plugins to use on this platform. |
| Sound Cue Cook Quality | Quality level to cook SoundCues at. If set, all other levels will be stripped by the cooker in favor of this setting. |

**Compression Overrides**

| Setting Name | Description |
| --- | --- |
| Override Compression Times | If set to true, this will override Sound Groups and use the Duration Threshold to determine whether a sound should be fully decompressed during initial loading. |
| Duration Threshold | A value measured in seconds. If Override Compression Times is enabled, any sound shorter than the Duration Value will be fully decompressed on load. Otherwise, a segment of the sound is cached at load time, and the rest is decompressed in real time. |
| Maximum Branches on Random SoundCue nodes | On this platform, SoundCues that use the Random node will preload this number of branches and dispose of any others. This can dramatically cut down on memory usage. |
| Quality Index for SoundCues | Use the specified quality level at this index to override the quality setting used for SoundCues on this platform. |

**Cook Overrides**

| Setting Name | Description |
| --- | --- |
| Max Size Per Streaming Chunk (KB) | Determines how compressed audio files are split into chunks when cooking for this platform. The smaller this value is, the more chunks a file will be split into. |
| Use Stream Caching (Experimental) | 
Enables use of Audio Stream Caching when cooking projects, which changes how audio is managed in memory.

Stream Caching separates compressed audio data from USoundWave files and instead places them at the end of a `.pak` file, which makes loading audio into memory and releasing it when not in use significantly easier.

This can result in audio not immediately playable when a USoundWave is loaded, but it enables use of a large variety of sounds without the risk of overstepping memory boundaries. It also provides a way for audio engineers to load chunks of audio without depending on the state of the audio engine, and provides benefits for mitigating audio latency.

For more information about Stream Caching, refer to the **Audio Stream Caching** documentation.



 |
| Resample for Device | When True, resamples Sound Waves according to their Sample Rate Quality. The exact Sample Rates to be used for each member of the Sample Rate Quality Enum can be set in Resampling Quality. |
| Compression Quality Modifier | Scales all quality settings for this platform. For example, a value of 0.5 will halve the quality settings on all SoundCues. |
| Stream All Soundwaves Longer Than: | If this is set to any value larger than 0, any SoundWaves longer than this value in seconds will stream directly off the disk. |
| Stream Caching | Contains the Max Cache Size and Max Chunk Size Override. Refer to the Stream Caching table below for more information. |
| Resampling Quality | Mapping of which sample rates are used at which sample rate quality levels on this platform. Includes values for Min, Low, Medium, High, and Max. |

**Stream Caching**

| Setting Name | Description |
| --- | --- |
| Max Cache Size (KB) | Sets the maximum amount of memory in KB used for the cache at any given time. If this is a small value (lower than 8 MB), this will lower the size of individual audio chunks during cooking. |
| Max Chunk Size override (KB) | Overrides the default max chunk size used when chunking audio for stream caching. This value is ignored if it is 0 or less. |