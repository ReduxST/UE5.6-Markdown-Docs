# Horde and UnrealGameSync Metadata Server

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-and-unrealgamesync-metadata-server-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-and-unrealgamesync-metadata-server-for-unreal-engine)  
**Processed:** 2025-06-14 16:27:39

---

UnrealGameSync (**UGS**) is a tool designed to simplify syncing from Perforce, supporting retrieval of pre-built editor binaries for artists or correctly versioning the local build so engineers can modify content. It is a convenient hub for surfacing build health, flagging issues, and scripting common workflow tasks outside Unreal Editor.

For more information on UGS, see the [UnrealGameSync](/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine) docs.

Horde includes an updated version of the legacy MetadataServer IIS web app that ships alongside UGS, integrating seamlessly with Horde's CI functionality.

## Configuration

To configure UnrealGameSync to source data from Horde, add the following lines in the `UnrealGameSync.ini` config file:

```
`[Default] ApiUrl=https://{{ HORDE_SERVER_URL }}/ugs`
Copy full snippet
```
\[Default\] ApiUrl=https://{{ HORDE\_SERVER\_URL }}/ugs

This config file can be in a project-specific location (e.g. `{{ PROJECT_DIR }}/Build/UnrealGameSync.ini`) or in a location that applies to all projects in a stream (e.g. `{{ ENGINE_DIR }}/Programs/UnrealGameSync/UnrealGameSync.ini`).