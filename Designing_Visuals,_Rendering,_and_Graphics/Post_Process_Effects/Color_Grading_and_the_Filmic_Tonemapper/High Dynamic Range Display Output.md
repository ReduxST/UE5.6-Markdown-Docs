# High Dynamic Range Display Output

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/high-dynamic-range-display-output-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/high-dynamic-range-display-output-in-unreal-engine)  
**Processed:** 2025-06-14 16:27:31

---

You can output to High Dynamic Range (HDR) displays to take advantage of features such as higher contrast and a wider color gamut! The goal here is to give the displayed images characteristics that are more like natural light conditions experienced in the "real world". This is part of the move to the **Academy Color Encoding System** (ACES) standard wiich is a pipeline to ensure the consistent color is preserved across multiple formats and displays, and also as a way to *future-proof* the source material used without having to adjust it for another medium.

![Low Dynamic Range (LDR) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80f8f93b-2d90-4534-b365-353eac4197df/ue5_1-low-dynamic-range.png)

![High Dynamic Range (HDR) ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c92f44e-2bf9-4860-9272-44973ed6b081/ue5_1-high-dynamic-range.png)

This example is simulated and purely for demonstration purposes only. It is impossible to convey HDR differences on an LDR screen.

With the current implementation, the full processing of the rendered scene is handled through what is known as the **ACES Viewing Transform**. This process works by using scene-referred and display-referred images.

-   **Scene-referred** images maintain the original *linear light* values of the source materials without limiting the exposure range.
-   **Display-referred** is the final image transformed into the color space of the display being used.

By using this pipeline, the source files do not have to be edited each time they are used with a different display to guarantee correct coloring. Instead, the display being output maps it to the correct color space.

The ACES Viewing Transform works in the following order in the viewing pipeline:

-   **Look Modification Transform (LMT)** - This part of the process takes the ACES color-encoded image that has had a creative "look" (color grading and correction) applied to it and then outputs the images rendered with ACES in combination with the Reference Rendering Transform (RRT) and an Output Device Transform (ODT).
-   **Reference Rendering Transform (RRT)** - Then, this part takes the scene-referred color values and converts them to display-referred. In this process, it enables the rendered images to not rely on a specific display and, instead, can ensure a larger gamut and dynamic range that is correct for the specific display it's being output to, including ones that have yet to be created.
-   **Output Device Transform (ODT)** - Finally, this takes the HDR Data output of the RRT to then match it with the different devices and color spaces they can display. Because of this, each target requires its own ODT to be matched against (eg Rec709, Rec2020, DCI-P3, etc.).

For additional information on the ACES Viewing Transform, you can download the PDF documentation from the [ACES GitHub](https://github.com/ampas/aces-dev/tree/master/documents) page or follow the links in the Reference Material section of this page.

## Enabling HDR Output

You can enable HDR output at runtime by toggling the console variables or by using the **GameUserSettings** node in Blueprints.

![Enabling HDR Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9abbd79-4000-4eaf-83eb-791fadfb5846/ue5_1-high-dynamic-range-display-game-user-settings.png)

The Game User Settings controls will automatically clamp to the closest available match for the current output device and set all flags accordingly. Alternatively, you can use the following console variables to enable and change the available options for the HDR device and color gamut output needed.

| Console Variable | Description |
| --- | --- |
| **r.AllowHDR** | Creates an HDR-compatible swap chain and enables HDR display output on platforms that supports it. Takes values 0 (disabled) and 1 (enabled). |
| **r.HDR.EnableHDROutput** | When set to 1, this recreates the swap chain and enables HDR output. |
| **r.HDR.Display.OutputDevice** | 
This is the device format of the output display:

-   **0**: sRGB (LDR) (default)
-   **1**: Rec709 (LDR)
-   **2**: Explicit gamma mapping (LDR)
-   **3**: ACES 1000-nit ST-2084 (Dolby PQ) (HDR)
-   **4**: ACES 2000-nit ST-2084 (Dolby PQ) (HDR)
-   **5**: ACES 1000-nit ScRGB (HDR)
-   **6**: ACES 2000-nit ScRGB (HDR)



 |
| **r.HDR.Display.ColorGamut** | 

This is the color gamut of the output display:

-   **0**: Rec709 / sRGB, D65 (default)
-   **1**: DCI-P3, D65
-   **2**: Rec2020 / BT2020, D65
-   **3**: ACES, D60
-   **4**: ACEScg, D60



 |

Once you've set up the Blueprint or C++ call for GameUserSettings, you can run any cooked project, use the command line argument `-game mode`, use Standalone game mode, or Play-in-Editor (PIE) in a new window using exclusive fullscreen (press **Alt** + **Enter** or use the command `fullscreen` from the console window).

Using borderless window or windowed mode will not currently work for HDR output.

### Low Dynamic Range (LDR) UI support in HDR

This particular feature is experimental and may change in a future release.

When HDR output has been enabled your User Interface (UI) may not look correct. We've added experimental support for LDR UI composition for this reason. It attempts to match the LDR look as closely as possible, although, it's recommended to boost the UI slightly to avoid looking washed out next to the vibrancy of the main scene.

To do this, you can use the following console variables:

| Console Variable | Description |
| --- | --- |
| **r.HDR.UI.CompositeMode** | When set to 1, this enables HDR UI composition, which attempts to preserve LDR visuals and blending. |
| **r.HDR.UI.Level** | This adjusts the brightness of the composited UI. It is recommended to use a value of 1.5 or 2. |

## HDR Hardware and Setup Considerations

With the many different types of displays and TVs that are available, along with console and PC considerations, you may find that you need to use a specific piece of hardware or change a setting to get HDR output to work properly. The following are some things to consider when you're running through your setup process:

-   Make sure that your system is connected to the HDR display using a high-speed HDMI 2.0 cable so that you can take advantage of the transfer speeds. (HDMI 1.4 may work, but may have issues displaying the content.) Not all HDMI ports may accept HDMI 2.0 and HDR. Refer to your display's manual if you're unsure.
-   Ensure that the TV port is HDR enabled. Sometimes this may be listed in your TV or display settings as "HDMI Deep Color" or "Enhanced Format." Refer to your display's manual if you're unsure.
-   With some consoles, like the PS4, you may need to disable the system setting for **Enable HDCP** for HDR output to work properly.
-   For some displays, you may need to adjust display settings to get the correct output.
    -   With NVIDIA GPUs, use the NVIDIA Control Panel and adjust the display resolution Output Color Format to use **RGB** and the Output Color Depth to use **10-bit** or **12-bit**. Depending on your hardware you may only have certain options available. Refer to your display's manual if you're unsure.
        
        Click the image for a full-size view.
        

## Notes and Limitations

-   By default, the film-mapping curve is disabled during HDR output due to poor compatibility with LDR controls.
-   Currently, only paths for 1000-nit and 2000-nit display outputs are implemented.
-   D3D11 restrictions limit HDR output to exclusive fullscreen support only. With D3D12 support in Windows 10, this can likely be extended to enable individual viewports for HDR Output. The implementation on Mac currently supports this, already.

## Reference Material

-   ["ACES." Oscars.org | Academy of Motion Picture Arts and Sciences. N.p., 06 Feb. 2017. Web. 05 June 2017.](http://www.oscars.org/science-technology/sci-tech-projects/aces)
-   ["Aces Documentation." Oscars.org | Academy of Motion Picture Arts and Sciences. N.p., 26 Sept. 2016. Web. 05 June 2017.](http://www.oscars.org/science-technology/aces/aces-documentation)