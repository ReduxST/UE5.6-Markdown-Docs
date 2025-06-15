# Derived Data

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/derived-data-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/derived-data-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:19:51

---

## Derived Data

### Warnings

| **Section** | **Description** |
| --- | --- |
| **Enable Warnings** | 
Enable warnings when certain configurations have not been set or are not being used.

The *Recommend* settings below check how the [Derived Data Cache (DDC)](/documentation/en-us/unreal-engine/using-derived-data-cache-in-unreal-engine) is configured and show a pop-up message on Editor startup when certain configurations have not been set or are not being used.



 |
| **Recommend Everyone Setup AGlobal Local DDCPath** | If enabled, Unreal Engine warns when local cache is not set by `UE-LocalDataCachePath` env variable or the **Global Local DDC Path** Editor setting. |
| **Recommend Everyone Setup AGlobal Shared DDCPath** | If enabled, Unreal Engine warns when the shared cache is not set by `UE-SharedDataCachePath` env variable or the **Global Shared DDC Path** Editor setting. |
| **Recommend Everyone Setup AGlobal S3DDCPath** | If enabled, Unreal Engine warns when the **Enable AWS S3 Cache** Editor setting is disabled. |
| **Recommend Everyone Enable S3DDC** | If enabled, Unreal Engine warns when the **Global Local S3DDC Path** Editor setting is not set. |
| **Recommend Everyone Use Unreal Cloud DDC** (previously named Horde Storage) | If enabled, Unreal Engine warns if Unreal Cloud DDC (Horde Storage) is not used. |