# Level Streaming

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-streaming-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-streaming-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:15

---

The Level Streaming feature makes it possible to load and unload map files into memory as well as toggle their visibility during play. This makes it possible to have worlds broken up into smaller chunks so that only the relevant parts of the world are taking up resources and being rendered at any point. If done properly, this allows for the creation of very large, seamless games that can make the player feel as if they are playing within a world that dwarfs them in size.

## World Composition

World Composition is a specific form of level streaming used to create large worlds. Levels are arranged in a planar grid, and streamed in as the player approaches them.

World Composition is a legacy system used for level streaming. It is recommended to use [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) for level streaming in projects using Unreal Engine 5.0 or later.