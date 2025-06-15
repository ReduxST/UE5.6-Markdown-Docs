# Mutable Texture Streaming

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-texture-streaming-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-texture-streaming-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:57

---

Mutable instances can generate their textures progressively. This has the following impact:

-   Objects are ready to render much faster, but at a lower quality.
-   Objects use less memory because larger texture mipmaps that are not needed won't be generated and won't use CPU or GPU memory.
-   Total object generation time is larger, because some work is repeated for every mipmap update.
-   There is a visible transition when texture mipmaps are updated, exactly like with the standard Unreal Engine texture streaming.
-   Mutable runtime is busier more often, which may delay the updates of other objects.

The general recommendation (and also the default behavior) is to toggle texture streaming on when in-game and toggle texture streaming off when the player is customizing an object, to prevent texture popping on mipmap updates.

Mutable toggles texture streaming for [States](/documentation/en-us/unreal-engine/using-customizable-states-in-mutable-with-unreal-engine) using the **Texture Compression Strategy** set to **None**. This is a heuristic that assumes that uncompressed textures will only be used in Customizable Object States that prioritize low update latency and popping is not allowed, for example while changing the skin color in a lobby.

Additionally, global Mutable texture streaming can be toggled using the cvar `mutable.EnableMutableProgressiveMipStreaming`.

At runtime it can be controlled with the following method: `UCustomizableObjectSystem::SetProgressiveMipStreamingEnabled(bool bIsEnabled)`.