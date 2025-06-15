# Using Media Plate in Virtual Production

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-media-plate-on-virtual-production-stage-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-media-plate-on-virtual-production-stage-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:54

---

The [Media Plate Actor](/documentation/en-us/unreal-engine/the-media-plate-actor-in-unreal-engine) is especially useful in clustered rendering setups with large LED displays, where the Actor maximizes the 2D plate or 360 latlong EXR playback performance and quality. The Media Plate Actor can use EXR tiling and mipmaps to balance load on render nodes and improve per-PC bandwidth limitations.

## VP specifics

-   To make use of this maximization, we recommend you use an EXR media format, and select a **Sphere** or **Plane** mesh under the [Mesh settings](/documentation/en-us/unreal-engine/the-media-plate-actor-in-unreal-engine#mesh). These two meshes use optimized streaming, so the media plate only streams the tiles visible to the camera frustum.
-   If you have the Virtual Production Utilities plugin enabled, an extra property becomes available in the [Settings for the Media Plate](/documentation/en-us/unreal-engine/the-media-plate-actor-in-unreal-engine#generalsettings):
    -   Materials > Create Dynamic Material You can create a dynamic material, which has any available parameter within the root Material exposed, so you can configure individual parameters.
-   When playing large latlong tiled `.exr` files on LED stages, you can experience increased tile requests at the poles. Increased tile requests typically happen on ceiling nDisplay nodes where the IO requirements can jump past the hardware capabilities, which causes stalls or playback stutters.
    -   To prevent stalls and playback stutters, you can set the Media Plate Actor to either automatically increase the MIP levels requested (lower resolution), or cap the Media Plate bandwidth EXR tiles requests. You can change these settings in the [EXR Tiles & Mips settings](/documentation/en-us/unreal-engine/the-media-plate-actor-in-unreal-engine#exrtilesandmaps).

In a clustered rendering setup using nDisplay, we recommend you try to use multiple PCs to help with bandwidth requirements. The more PCs you have, the fewer visible EXR tiles you will get per render node. Leveraging the support for tiles and mips, this should cut the per-PC input/output (IO) requirements. For high resolution EXR playback, for example simultaneous 8K+ latlongs, we also recommend that you have an SSD / NVMe raid configuration that throughputs at least 7-10 GB/sec on all nDisplay PCs.