# Hierarchical Level of Detail

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-level-of-detail-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hierarchical-level-of-detail-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:24

---

A complex level in Unreal Engine contains hundreds of detailed Static Mesh assets that combine together to build a virtual world. With this level of detail, it can become difficult to load a multi-kilometer level all at once.

The Hierarchical Level of Detail (HLOD) system can be used to organize multiple Static Mesh Actors and combine them into a single proxy mesh and Material at long view distances. This helps reduce the number of Actors that need to be rendered for the scene, which reduces the number draw calls per frame and increases performance. This is especially useful when working with large open worlds.