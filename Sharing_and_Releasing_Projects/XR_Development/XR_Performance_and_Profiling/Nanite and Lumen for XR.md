# Nanite and Lumen for XR

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-and-lumen-for-xr-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-and-lumen-for-xr-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:00

---

Nanite and Lumen on XR are considered experimental and are not officially supported.

## Requirements

-   Only supported on PC with the Deferred Renderer and DX12.
-   Not supported on Mobile XR hardware.

## Considerations

XR devices and their platforms come with special considerations and limitations. Since Unreal Engine 5.1, [Nanite](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) and [Lumen](/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) render in both views (each display of your XR headset), so you might struggle to achieve your target frame rate even with top-of-the-line hardware.