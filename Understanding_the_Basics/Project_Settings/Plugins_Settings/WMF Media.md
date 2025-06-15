# WMF Media

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/wmf-media-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/wmf-media-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 17:04:28

---

## WMF Media

### Media

| **Setting** | **Description** |
| --- | --- |
| **Allow Non Standard Codecs** | 
Defines whether to allow the loading of media that uses non-standard codecs (default = off).

By default, the player will attempt to detect audio and video codecs that are not supported by the operating system out of the box, but may require the user to install additional codec packs.

Enable this option to skip this check and allow the usage of non-standard codecs.



 |
| **Low Latency** | 

Enable low latency processing in the Windows media pipeline (default = off).

When this setting is enabled, the media data is generated with the lowest possible delay.

This might be desirable for certain real-time applications, but it can negatively affect audio and video quality.

This setting is only supported on Windows 8 or newer.



 |
| **Hardware Accelerated Video Decoding (Experimental)** | Use hardware accelerated video acceleration (GPU) when possible, otherwise fall back to software implementation (CPU). Windows and DX11 only. |

### Debug

| **Setting** | **Description** |
| --- | --- |
| **Native Audio Out** | Play audio tracks via the operating system's native sound mixer (default = off). |