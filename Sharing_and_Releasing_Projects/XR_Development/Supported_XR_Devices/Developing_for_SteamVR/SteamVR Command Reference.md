# SteamVR Command Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/steamvr-command-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/steamvr-command-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:32

---

Below you will find various Console commands that can be used to adjust the way Unreal Engine and SteamVR interact with one another.

| Command | Description |
| --- | --- |
| **vr.SteamVR.AdaptiveDebugGPUTime** | Added to the the GPU frame timing, in ms, for testing. |
| **vr.SteamVR.AdaptiveGPUTimeThreshold** | Time, in ms, to aim for stabilizing the GPU frame time at. |
| **vr.SteamVR.PixelDensityAdaptiveDebugCycle** | If non-zero, the adaptive pixel density will cycle from max to min pixel density, and then jump to max. |
| **vr.SteamVR.PixelDensityAdaptiveDebugOutput** | If non-zero, the adaptive pixel density will print debugging info to the log. |
| **vr.SteamVR.PixelDensityAdaptivePostProcess** | If non-zero, when the adaptive density changes, we'll disable Temporal Anti-Aliasing (TAA) for a few frames to clear the buffers. |
| **vr.SteamVR.PixelDensityMax** | Maximum pixel density, as a float. |
| **vr.SteamVR.PixelDensityMin** | Minimum pixel density, as a float. |
| **vr.SteamVR.ShowDebug** | If non-zero, will draw debugging info to the canvas. |
| **vr.SteamVR.UsePostPresentHandoff** | Whether or not to use PostPresentHandoff. If true, more GPU time will be available, but this relies on no SceneCaptureComponent2D or WidgetComponents being active in the scene. Otherwise, it will break async re-projection. |
| **vr.SteamVR.UseVisibleAreaMesh** | If non-zero, SteamVR will use the visible area mesh in addition to the hidden area mesh optimization. This may be problematic on beta versions of platforms. |