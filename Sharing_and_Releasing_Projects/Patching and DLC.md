# Patching and DLC

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/patching-content-delivery-and-dlc-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/patching-content-delivery-and-dlc-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:12

---

**Unreal Engine** can divide content into **.pak** files and deliver them to users separately from the main executable. This functionality supports DLC and patching for live services.

## General Information

The following pages contain information about the UE cooking and chunking process, how to prepare .pak files for distribution, and reference information for mounting chunks.

## Chunk Downloader Plugin

The **ChunkDownloader** plugin is a general patching solution intended for games that need to deliver a large number of small files.

## Google Play Asset Delivery (GooglePAD)

The **GooglePAD** plugin uses Google's **Play Asset Delivery** system on the Google Play store. This patching solution is a companion to the **Android App Bundle** system, which delivers customized APKs that are optimized for users' individual devices.

You can read more about GooglePAD in the [Google Play Asset Delivery Reference](/documentation/en-us/unreal-engine/using-google-play-asset-delivery-in-unreal-engine).