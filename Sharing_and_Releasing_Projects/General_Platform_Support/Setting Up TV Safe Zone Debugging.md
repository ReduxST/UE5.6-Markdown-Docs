# Setting Up TV Safe Zone Debugging

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-tv-safe-zone-debugging-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-tv-safe-zone-debugging-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:54

---

During working on UI for **Unreal Engine** (UE) projects, it's important to avoid placing UI elements (text or widgets) too close to the edges of the screen. If you place UI elements near edge of the screen, it can cause them to be distorted depends on device. Use **TV Safe Zone Debugging** tool for ensure that UI items are located as you need. Get familiar with this document for understanding how to use TV Safe Zone Debugging tool in UE projects.

## What are TV Safe Zones

A TV Safe Zone or Safe Area is the term used in television production to describe the area of the television picture that ensures the content can be cleanly viewed by a majority of TV viewers. Generally speaking, the most important content for a TV show will be placed in this area to ensure that it will not be distorted when viewed on a wide range of TV sets.

You can read more about TV Safe Zones and Safe Areas on the following Wikipedia page: [TV Safe area](http://tinyurl.com/zq55mzl).

## Difference between Title Safe Zones & Action Safe Zones

UE has two different types of TV Safe Zones: the Title Safe Zone and the Action Safe Zone.

-   **Title Safe Zone -** The Title Safe Zone is for UI or Text elements, to make sure they are not cut off or distorted when viewed.
    
-   **Action Safe Zone -** The Action Safe Zone is used to allow characters or enemies to wander partially offscreen.
    

The area outside of the Action Safe zone will probably be clipped on displays with overscan, while areas between the Action Safe zone and Title Safe zone may be partially clipped. It's OK to have some action (such as other characters or enemies) occur in that region. The Action Safe zone is the same size as the Title Safe zone on many platforms.

## TV Safe Zone Commands

Following section provides commands you can use with the TV Safe Zone. Also section describes two different ways you can enable and use the TV Safe Zone Debugging tool in your UE project.

Use following TV Safe Zone commands via the UE console.

| Command Name | Value | Description |
| --- | --- | --- |
| `r.DebugSafeZone.Mode` | 0 | Disables all overlays. |
| `r.DebugSafeZone.Mode` | 1 | Enables Title safe zone. |
| `r.DebugSafeZone.Mode` | 2 | Enables Action safe zone. |
| `r.DebugSafeZone.OverlayAlpha` | 0 to 1 | Controls how opaque the debug visualization overlay is (Default is 0.3) |
| `r.DebugSafeZone.TitleRatio` | 0 to 1 | Controls the action safe zone margins returned in FDisplayMetrics (Default is 0.9). |
| `r.DebugActionZone.ActionRatio` | 0 to 1 | Controls the action safe zone margins returned in FDisplayMetrics (Default is 0.9). |

You can also place the TV Safe Zone commands in your projects `DefaultEngine.ini` file under the `[SystemSettings]` section.

```
	`[SystemSettings] 	r.DebugSafeZone.Mode 1 	r.DebugSafeZone.TitleRatio 0.9 	r.DebugSafeZone.ActionRatio 0.9`

Copy full snippet
```
\[SystemSettings\] r.DebugSafeZone.Mode 1 r.DebugSafeZone.TitleRatio 0.9 r.DebugSafeZone.ActionRatio 0.9

## Activating the Title Safe Zone Debug Preview

To correctly display the ratio of the safe areas, you **must** run the project in either **Windowed Fullscreen** or **Fullscreen** mode. If you don't, the safe zone will not display correctly, or will display a smaller size than expected.

Following section shows how to activate the Safe Zones in the Debug preview.

1.  From the **Main Toolbar**, go to the **Play** buttons panel and click to open drop-down menu. In the **Play Modes** menu, select **New Editor Window (PIE)**. This launches the game in a new window.
    
    ![Launch project in New Editor Window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3fa6fa98-710b-4e7f-b0c0-9e4442296154/ue5_1-01-launch-new-window.png "Launch project in New Editor Window")
2.  Enlarge window with launched project for fullscreen view.
    
    ![Enlarge window to fullscreen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e72f0b9-4260-4d19-b2ba-48cdf03650de/ue5_1-02-fullscreen.png "Enlarge window to fullscreen")
3.  Press the **TILDE ( ~ )** key to open the **Unreal Console**. Do the following:
    
    -   Type `r.DebugSafeZone.TitleRatio 0.9`, and press the **ENTER** key to apply it.
    -   Type `r.DebugSafeZone.OverlayAlpha 0.4`, and press the **ENTER** key to apply it.
    -   Type `r.DebugSafeZone.Mode 1`, and press the **ENTER** key to apply it.
    
    ![Example entering command](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c28677d-e319-4b14-b640-10a04f81d3f1/ue5_1-03-enter-command.png "Example entering command")
4.  You should now see a slightly transparent red border placed around the entire play window, as seen in the image below.
    
    Click image for full view.
    

## Adjusting the Size of the Safe & Action Zones

You can adjust the size of either the Safe or Action Zones by entering the following commands into the Unreal Console.

| Command Name | Value | Description |
| --- | --- | --- |
| `r.DebugSafeZone.TitleRatio` | 0 to 1 Range | Controls the Safe Zone margins returned in FDisplayMetrics (Default is 0.9). |
| `r.DebugActionZone.ActionRatio` | 0 to 1 Range | Controls the Action Safe Zone margins returned in FDisplayMetrics (Default is 0.9). |

It is not possible to have both the Safe and Action Zone active at the same time. To view another zone, you will have to disable the one you are currently viewing and then enable the one you want to view.

In the images below, the command `r.DebugActionZone.ActionRatio` was used to decrease to size of the Action Zone from **0.99** all the way down to **0.1**.

         ![Set Action Ratio 0.99](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e941d09-d0b7-4a20-a16a-9daa42b0ec4b/ue5_1-05-action-ratio-1.png "Set Action Ratio 0.99") ![Set Action Ratio 0.9](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d35e2225-d177-422e-8c0b-0ee8424709ab/ue5_1-06-action-ratio-2.png "Set Action Ratio 0.9") ![Set Action Ratio 0.8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ce272cc-a1f9-4549-bf27-711facdc3bd4/ue5_1-07-action-ratio-3.png "Set Action Ratio 0.8") ![Set Action Ratio 0.7](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84192826-41cb-4ae9-965a-ba5850eab4c2/ue5_1-08-action-ratio-4.png "Set Action Ratio 0.7") ![Set Action Ratio 0.6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4250d11-2b07-497e-966b-68e01e7b3533/ue5_1-09-action-ratio-5.png "Set Action Ratio 0.6") ![Set Action Ratio 0.5](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/303025a4-2245-4854-a696-3362a245bff4/ue5_1-10-action-ratio-6.png "Set Action Ratio 0.5") ![Set Action Ratio 0.4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d62bb11d-75da-4e62-9333-7e89e56cf4b8/ue5_1-11-action-ratio-7.png "Set Action Ratio 0.4") ![Set Action Ratio 0.3](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64c838e6-b3d3-43fc-b8ad-b126857976ae/ue5_1-12-action-ratio-8.png "Set Action Ratio 0.3") ![Set Action Ratio 0.2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/956b4ab2-5b3d-4a22-b25e-a768671f7fdf/ue5_1-13-action-ratio-9.png "Set Action Ratio 0.2") ![Set Action Ratio 0.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/833454b7-6677-41e5-9967-239852faeffa/ue5_1-14-action-ratio-10.png "Set Action Ratio 0.1")

**Dragging the slider will show what happens when adjusting the size of the Safe Zone.**

## Adjusting the Alpha of the Safe & Action Zone Overlay

You can increase or decrease the opacity of the Safe & Action Zones by entering the following command into the Unreal console.

| Command Name | Value | Description |
| --- | --- | --- |
| `r.DebugSafeZone.OverlayAlpha` | 0 to 1 | Controls the opacity of the Safe & Action Zones overlays(Default is 0.3). |

In the images below you can see what happens to the opacity of the Safe & Action Zone overlays when the value of `r.DebugSafeZone.OverlayAlpha` was set from a value of 1.0 to a value of 0.1.

    ![Set Overlay Alpha 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fdd8150-0dec-4aca-93c6-def6e6b358ca/ue5_1-15-overlay-alpha-1.png "Set Overlay Alpha 1") ![Set Overlay Alpha 0.8](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7671b968-c1ed-47ae-ac1a-f30493627b91/ue5_1-16-overlay-alpha-2.png "Set Overlay Alpha 0.8") ![Set Overlay Alpha 0.6](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f2c8995-89ce-4726-b1f0-b9daf0d201eb/ue5_1-17-overlay-alpha-3.png "Set Overlay Alpha 0.6") ![Set Overlay Alpha 0.4](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55ee1486-4655-4bfa-87b7-c79785c9eaad/ue5_1-18-overlay-alpha-4.png "Set Overlay Alpha 0.4") ![Set Overlay Alpha 0.2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c64c95ff-a21c-4a3a-8d51-31fae446c181/ue5_1-19-overlay-alpha-5.png "Set Overlay Alpha 0.2")

**Dragging the slider will show what happens when adjusting the opacity of the Overlay Alpha.**

## TV Safe Zone Troubleshooting

In the following section we will go over some pieces of information you need to be aware of to ensure that you are using the TV Safe Zone tool correctly.

-   Right now the safe areas are defined in terms of the full screen size (the API wasn't really designed for non-consoles) rather than returning the ratios directly to let them be used in windowed mode. This could be changed in the future, but for now you need to be running in **windowed fullscreen** or **fullscreen** for the ratio to be correct.
    
-   The UI isn't currently expected to be able to handle this changing at runtime, so if you change the TitleRatio / ActionRatio via the console while running you'll probably need to switch game modes to see the changes (e.g., go from front-end to in-game or vis-versa, or 'open FrontEndScene' again).
    
-   When using this tool on the PS4, you only need the first command, **r.DebugSafeZone.Mode 1** as the Safe Zone values are driven by the system setting you can pick in the PS4 OS menus.