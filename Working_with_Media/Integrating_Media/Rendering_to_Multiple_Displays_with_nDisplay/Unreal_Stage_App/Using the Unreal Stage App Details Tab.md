# Using the Unreal Stage App Details Tab

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-stage-app-details-tab-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-stage-app-details-tab-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:10

---

## Details Tab Properties

The available properties match the equivalent properties in the desktop Unreal Engine scene and will vary based on the type of content selected.

### Light Cards and Flags

For Light Cards and Flags, the following properties are available:

-   **Color**
    -   RGB or HSV values.
-   **Orientation:**
-   **Mask**
    -   Toggle between a circle or square mask for the Light Card
-   **Scale X and Scale Y**
    -   Sliders can provide more precise control compared to resizing with pinch zoom
-   **Latitude and Longitude**
-   **Longitude**
    -   Sliders can provide precise control for placement and positioning compared to touch-only
-   **Spin**
    -   Sliders can provide more precise control for rotation compared to touch-only
-   **Appearance:**
    -   **Temperature**
    -   **Tint**
    -   **Gain**
    -   **Opacity**
    -   **Feathering**
    -   **Exposure**
        -   Exposure controls include convenient buttons for quarter-, half-, and full-stop increments.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79ffeb9a-9eef-4e76-abd7-6815f8cceff4/details-1.gif)

### Color Correction Regions and Windows

For Color Correction Windows, the following properties are available:

-   Color Grading
-   RGB or HSV values
-   Color Grading Modes:
    -   **Global**
    -   **Shadows**
    -   **Midtones**
    -   **Highlights**
-   Color Grading Properties (each available per mode):
    -   **Saturation**
    -   **Contrast**
    -   **Gamma**
    -   **Gain**
    -   **Offset**
-   Orientation:
    -   Mask
        -   Toggle between a circle or square mask for the Color Correction Window
    -   Scale X and Scale Y
        -   Sliders can offer more fine-grain control over precise resizing than pinch zoom
    -   Latitude and Longitude
        -   Sliders can offer more fine-grain control over precise placement and positioning
    -   **Spin**
        -   Sliders can offer more fine-grain control over precise rotation than touch-only.
    -   **Radial Offset**
        -   Push/pull the Color Correction Window away from the LED volume representation along an axis with the nDisplay Root Actor's origin. This is useful to apply color grading behind some content in the scene but in front of others (as opposed to in front of everything in the scene visible to nDisplay).
-   Appearance:
    -   Color Temperature
    -   Tint
    -   Intensity
    -   Inner
    -   Outer
    -   Falloff

**Color Correction Regions** do not offer appearance controls because there are no 3D placement tools in Unreal Stage. Only color grading and appearance properties can be modified in the app.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/761b609c-c66e-468f-9c28-dc250ee944c5/details-2.gif)

### Preview Thumbnail

The Details tab offers a preview thumbnail to provide a visual in the app while modifying properties. The preview thumbnail can be moved to any corner of the Unreal Stage UI or stowed/minimized.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ad8f87c-1629-454c-b098-5b7f9857e590/details-3.gif)

### Set a Property to an Explicit Value

In addition to the sliders, properties can also be modified and set to an explicit value by double-tapping on it to bring up an input dialog and the keyboard.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63d6219b-5cc9-4b06-8e13-e204f3e85646/details-4.gif)