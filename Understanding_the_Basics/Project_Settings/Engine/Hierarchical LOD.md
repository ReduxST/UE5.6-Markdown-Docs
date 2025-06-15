# Hierarchical LOD

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-lod-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-lod-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:27:30

---

## Hierarchical LOD

### HLODSystem

| **Section** | **Description** |
| --- | --- |
| **Force Settings in All Maps** | If enabled, will force the project-wide set HLOD level settings to be used across all Levels in the project when building clusters. |
| **Save LODActors to HLODPackages** | If enabled, will save LOD Actor descriptions in the HLOD packages. |
| **Default Setup** | 
When the **Force Settings in All Maps** option is enabled, this sets the HLOD setup configuration that should be used by default for all Levels.

You can choose any `HierarchicalLODSetup` class in your project.



 |
| **Base Material** | Base material used for creating a Constant Material Instance as the Proxy Material. |
| **Directories Containing Maps Used for Building HLOD Data Through the Commandlet** | Directories containing maps used for building HLOD data through the Commandlet. |
| **Map UAssets Used for Building HLOD Data Through the ResavePackages Commandlet** | Map UAssets used for building HLOD data through the ResavePackages Commandlet. |