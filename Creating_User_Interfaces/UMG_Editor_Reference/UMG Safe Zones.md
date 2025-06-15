# UMG Safe Zones

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-safe-zones-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-safe-zones-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:33

---

**Safe Zone** widgets are an essential part of developing a game user interface (UI) that can run on a lot of different devices. Safe zones are designed to keep the UI from displaying somewhere that it can technically use but the player can't see, such as the edge of a TV display or under the notch and home bar of the iPhoneX. The UMG Designer enables you to test the resolution (or rotation) of the device with your UI and applied Safe Zone widgets.

When you add a **Safe Zone** widget to the **Designer** , the widget will scale any other widgets that are made children of it from the **Hierarchy** panel. These child widgets will scale and adjust anytime there is an "unsafe" zone.

![Without Safe Zone widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d899957-1bf7-40c7-809d-0845d371a05c/withoutsafezone_opt-1.png)

![With Safe Zone widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79f15dfc-7524-4d77-98ca-54c6ea7220c7/withsafezone_opt.png)

In this example, a 1080p display has a **Uniform Safe Zone** area of 0.9 (red) for testing and debugging purposes. When the widgets are parented to a Safe Zone widget, the child widgets will scale to the safe zone area. This prevents widgets from being cut off at the screen edge deemed "unsafe". This can be seen in the example, with the "My Menu" title text.

## Setting and Testing Safe Zone Resolutions

In UMG (or for [Play-in-Editor](/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine) settings), the screen sizes chosen are now linked with [Device Profiles](/documentation/en-us/unreal-engine/setting-up-device-profiles-in-unreal-engine) which also takes into account the [Mobile Content Scale Factor](/documentation/en-us/unreal-engine/performance-guidelines-for-mobile-devices-in-unreal-engine#mobilecontentscalefactor), meaning that the final resolution and DPI scale will change based on the selected device.

To test the screen resolution of a device, use the UMG **Designer** viewport to select the **Screen Size** dropdown and select from the listed devices.

![ScreenSizeSelection.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57d5da6d-b88b-4e4f-8374-7b121b00c2b6/screensizeselection_opt.png)

If the device supports screen orientation, like a phone or tablet, use the **Portrait/Landscape** button to swap between the two view modes. This option will be grayed out when the device selected doesn't support orientation shifting.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9268f498-5dca-4937-bc5b-4918796047d3/orientationbutton.png)

Here is an example of the two view modes:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/399bcdc6-75d1-4e07-ad33-404d73acc283/iphonex_portraitandlandscape.png)

Left: Landscape, Right: Portrait

When a device is selected, relevant information and marked "unsafe" zones will be displayed in the **Designer** graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55c30e01-88ac-40cd-9a31-502182a435c1/devicedetails.png)

Marked "Unsafe" Zones Device Details for Mobile Content Scale Factor, Device Name or Uniform Safe Zone, and Screen Size DPI Scale

For non-uniform safe zones, you can use the **Flip** button to simulate device rotation for Landscape mode.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de3df761-fc72-4a65-8fe9-9c520bd96f9d/deviceflipbutton.png)

This option is only available on some devices and only for Landscape view mode.

When previewing TVs and Monitors from the list, if you've set a [debug title safe zone](/documentation/en-us/unreal-engine/setting-up-tv-safe-zone-debugging-in-unreal-engine) that is less than 1, the **Uniform Safe Zone** will display that size. The debug safe zone area is represented by the red area around the canvas widgets.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf2299c3-2e1d-42c7-801a-0eabf0b706a8/uniformsafezone.png)

The **Debug Safe Zone** mode is on by default in UMG which enables the red "unsafe" zone area to be represented.

For some devices, there are now custom "unsafe" zones represented within the Designer graph. These are used to represent hardware or software specific areas of the device that take up screen real estate, such as the iPhoneX where these zones represent the notch and home bar sections of the screen.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a338c98-fd99-46d4-bf4d-e9362f932bb9/iphonexunsafezones.png)

In this example of the iPhoneX, the Safe Zone widget is parented to the section of the widget hierarchy where the menu and buttons are contained. When areas are "unsafe," the encapsulated widgets scale to avoid these areas (see example above).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46cd8269-1870-46c5-bac2-71443b06a807/safezonehierarchypanel.png)

## Testing UI in PIE and Standalone Game

When testing your UI in the Editor, you can set the screen size based on a common device screen size when using PIE with a **New Editor Window** or when using **Standalone Game** without deploying content to a device. Use the **Editor Preferences** to set the device under **Level > Play > Game Viewport Settings** to choose a common device resolution.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d2685ad-4dcf-4ca0-b9cc-c87ddcd8850b/piesettings.png)

Use the **Landscape/Portrait Orientation** button to swap which orientation should be used.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a3b4b93-2413-4f10-a897-44069dfcb3df/piesettings_swaporientation.png)