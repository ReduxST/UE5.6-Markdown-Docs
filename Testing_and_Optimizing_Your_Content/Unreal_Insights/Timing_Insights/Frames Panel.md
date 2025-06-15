# Frames Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-frames-panel-in-unreal-insights-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-frames-panel-in-unreal-insights-for-unreal-engine)  
**Processed:** 2025-06-14 17:01:27

---

The **Frames** panel displays the total time taken by each frame using a bar graph format. This is useful for identifying general trends, such as low performance or framerate drops when a level is loaded, an unoptimized scene is visible, or spawning a large number of Actors simultaneously.

![The Frames Panel displayed in Unreal Insights.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/737e1ced-fd1e-43ac-b668-2559377f6bbb/main-image.png)

The frames panel displays the Frames, Timing, Timers, Callers, Callees, Counters, and Log tracks.

Hovering the cursor over a bar causes that frame's index and running time to appear.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a759e74-7752-4165-9b6a-1c13c48b72f1/frames-timeline.png)

If you right-click on on the bar, the following **Zoom** context menu options will appear:

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2499386a-ba05-4af0-a83e-7d42f5696230/zoom-options.png)

| **Option** | **Description** |
| --- | --- |
| **Auto Zoom** | Toggles auto zoom, which fits the entire session time range into the frames display window. |
| **Zoom Timing View on Frame Selection** | Toggles whether the timing view is zoomed when a frame is selected. |

These options are also available to edit in the UnrealInsightsSettings.ini file.