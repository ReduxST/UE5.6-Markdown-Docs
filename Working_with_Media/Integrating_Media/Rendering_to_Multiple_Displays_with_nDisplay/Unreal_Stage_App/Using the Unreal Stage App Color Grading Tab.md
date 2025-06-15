# Using the Unreal Stage App Color Grading Tab

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-stage-app-color-grading-tab-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-stage-app-color-grading-tab-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:09

---

## Color Grading

The nDisplay Color Grading Tab enables you to perform color grading operations on the nDisplay cluster as a whole, just as you can in the ICVFX Editor. You can apply color grading to the entire cluster or on a per-viewport basis, as well as any ICVFX Cameras (plural) with per-node granularity if desired.

## Outliner

When on the nDisplay Color Grading Tab, a modified Outliner will appear with two panes instead of one:

-   Color Grading Outliner
    -   All color grade-able content in the Level will appear here, which can include Post Process Volume(s) in addition to the nDisplay Root actor.
    -   ICVFX Camera components are listed underneath the corresponding nDisplay Root Actor. Select the Root to color grade the viewports vs. the cameras.
-   Per-Viewport/Per-Node Color Grading
    -   Per-Viewport (for the outer viewports) and Per-Node (for the inner frustums) color grading can be defined in Unreal Engine and appear as options here to color grade specific areas of the LED volume, such as the ceiling.
    -   Per-Viewport and Per-Node configurations cannot yet be created and modified directly in Unreal Stage, but this is planned to be included in a future release.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1dad093-6827-4f30-926f-980f8991037e/colorgrading-1.gif)

## Preview Thumbnail

The Color Grading tab offers a preview thumbnail to provide an in-app visual while modifying properties. The preview thumbnail can be moved to any corner of the Unreal Stage UI or stowed/minimized.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/699770c8-c922-4458-9b5e-0f661ac671aa/colorgrading-2.gif)