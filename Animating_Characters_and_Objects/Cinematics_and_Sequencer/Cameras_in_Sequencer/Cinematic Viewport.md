# Cinematic Viewport

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-viewport-controls-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-viewport-controls-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:25

---

In the Unreal Editor, you can change any **Level Viewport** to a specialized **Cinematic Viewport**. The Cinematic Viewport enables additional functionality, behavior, and display modes that can assist you with cinematic content creation. This guide gives an overview of how to enable the Cinematic Viewport and its features.

#### Prerequisites

-   You have a project that is using Sequencer. You can use one of the provided [**Cinematic Samples**](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine#cinematicsamples) if you don't already have one.
    
-   **[Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)** is currently open in your Level.
    

## Enabling the Cinematic Viewport

To enable the Cinematic Viewport mode, select the **Viewport Perspective** menu and enable **Cinematic Viewport**.

![enable cinematic viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3de0f659-1133-4074-bf0b-d0e845e1938a/enableviewport.png)

## Overview

Once the Cinematic Viewport is enabled and **Sequencer** is opened, your viewport should now be displaying new cinematic elements.

![cinematic viewport layout](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca8200f2-7d13-4910-8aca-344338be6cb5/overview.png)

1.  [**Film Overlays**](/documentation/en-us/unreal-engine/cinematic-viewport-controls-in-unreal-engine#filmoverlays)
    
2.  [**Playback Preview and Controls**](/documentation/en-us/unreal-engine/cinematic-viewport-controls-in-unreal-engine#playbackpreviewandcontrols)
    

### Film Overlays

The **Film Overlays** menu contains visual guides for the viewport that you can enable to assist with your framing and composition. There are two main categories of overlays, **Composition** and **Frame** overlays.

![film overlays menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74f6fd98-9c57-480f-9d71-17da1214004d/overlaysmenu.png)

#### Composition Overlays

| Name | Description |
| --- | --- |
| **Disabled** | The default view mode, which does not display any overlay. |
| **Grid (3x3)** | 
Displays a 3x3 grid on the viewport, allowing for framing based on **[Rule of Thirds](https://en.wikipedia.org/wiki/Rule_of_thirds)**.

![3x3 grid](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f388b944-e49c-4a56-b6e4-012d737aa90a/3x3.png)

 |
| **Grid (2x2)** | 

Displays a 2x2 grid on the viewport.

![2x2 grid](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c615d97b-260f-4d02-8e32-535ef7767167/2x2.png)

 |
| **Crosshair** | 

Displays a central reticle, useful for emulating photography reticles.

![crosshair reticle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96423ea7-4a15-4ca2-9790-924bee2abca9/crosshair.png)

 |
| **Rabatment** | 

Displays a rabatment overlay on the viewport, allowing for framing based on **[Rabatment of the Rectangle](https://en.wikipedia.org/wiki/Rabatment_of_the_rectangle)**.

![rabatment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46a2f290-72b7-453e-9416-ea03f3fd244a/rabatment.png)

 |

Composition overlay lines can also be tinted to any color or alpha value you want. Clicking the color bar next to **Tint** will open the **Color Picker** where you can select the color and transparency of the lines.

![composition lines color](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9949b05-79d0-4eea-8392-69603e245193/comptinting.gif)

#### Frame Overlays

**Frame Overlays** are guidelines used to emulate **[Safe Areas](https://en.wikipedia.org/wiki/Safe_area_%28television%29)** or **[Letterboxing](https://en.wikipedia.org/wiki/Letterboxing_%28filming%29)** when framing your image.

| Name | Description |
| --- | --- |
| **Action Safe** | 
Displays the "Action" safe guidelines. By default it appears to appear at **95%** of the screen space margins and is colored **red**.

![action safe guidelines](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13bdc313-d033-4803-a8bb-e32e0a73044d/action.png)

 |
| **Title Safe** | 

Displays the "Title" safe guidelines. By default it appears at **90%** of the screen space margins and is colored **yellow**.

![title safe guidelines](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24ccb1df-12b2-44a1-a0dc-19f6eaca49af/title.png)

 |
| **Custom Safe** | 

Displays a custom safe guideline. By default it appears at **85%** of the screen space margins and is colored **green**.

![custom safe guidelines](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e42c6c33-048f-4340-8650-9a846030f22e/custom.png)

 |
| **Letterbox Mask** | 

Displays a letterbox overlay, showing what the target aspect ratio will crop out of the original image. By default the letterbox aspect ratio is **2.35:1**.

![letterbox overlay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74a8088d-f01d-4a84-9811-17eda740274d/letterbox.png)

You will need to ensure that the **Constrain Aspect Ratio** property is enabled on your [**Camera's Properties**](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#properties) in order for the letterboxing to be accurate for your camera's sensor size.



 |

Each safe region entry has a percentage field next to it, which corresponds to the screen size of the guideline. A value of 100% will make the guidelines reach the outer edges of the screen, and 0% will cause the guidelines to reach the centerpoint of the screen. The guideline ranges are clamped between 1% and 99% in order to remain fully visible.

![safe region size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a67d194-577a-4fc7-8fc6-0da7d32925d1/safesize.gif)

You can input different letterbox aspect ratios next to the **Letterbox Mask** entry. Doing this will change the shape of the letterbox to conform to the input aspect ratio.

![letterbox ratio change](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01f35ec2-ce45-4dd0-914d-e93fec006e53/letterboxchange.png)

Both the safe and letterbox guidelines can be tinted to any color by clicking the color bar under their properties. Doing this will open the **Color Picker** where you can select the color and transparency of the guidelines.

![frame overlay tinting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81f4009b-b49c-4da6-9c3d-e444a744ea11/framestinting.png)

### Playback Preview and Controls

When the Cinematic Viewport is enabled, new controls and displays will appear at the bottom of the viewport.

![cinematic viewport playback display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cab6d983-ec81-4394-b54c-8a8731546618/playbackdisplay.png)

The upper region of this area displays information about the current shot, camera, and timing.

![cinematic viewport time display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70078498-f5d3-43db-8f2e-7b1361e4b3e1/timingdisplay.png)

1.  The name of the current **Sequence** and current **[Camera](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)**.
2.  The current camera's [**Filmback Properties**](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#properties).
3.  The current **Time** of the sequence or **[Master Sequence](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine)**.

A time bar is also displayed and can be interacted with by utilizing similar [**Playhead**](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead) interactions from Sequencer. The displayed time bar synchronizes with the time bar in Sequencer.

![cinematic viewport timebar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83fe7235-1c66-4d8d-91cb-433ffae3006e/timebar.gif)

The bottom region displays time and playback controls.

![cinematic viewport playback controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9e8c134-cb72-4e07-9bae-1063e6c775cb/playbackcontrols.png)

1.  The start times of the **Working Range** and **Playback Range**.
2.  The current time of the active sequence.
3.  [**Playback Controls**](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playbackcontrols). These can be clicked to play, pause, and perform other playback functions.
4.  The end time of the **Playback Range** and **Working Range**.

In the bottom region, the time displays can be interacted with by clicking them and typing in different values, or by clicking and dragging left and right to scrub their values.

![cinematic viewport time interaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62ae4272-55ee-43f9-b019-8b21f48af904/timeinteract.gif)

## Allow Cinematic Control

When working on cinematic content in Unreal Engine, you may want to use [Multiple Viewports](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine#viewportlayout) in order to preview your scene from different perspectives in conjunction with the main cinematic view. You can use the **Allow Cinematic Control** option to choose which viewport should display the cinematic when **Sequencer** has camera control.

![cinematic control viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fca37b0-4330-4e0f-950b-ed1955c8c390/cinecontrol1.png)

**Allow Cinematic Control** can only be enabled or disabled on viewports using the **Perspective** view mode.

By default, Unreal Engine's primary viewport has **Allow Cinematic Control** enabled.

![allow cinematic control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce05e152-7ae3-439d-888c-14556f10b886/4panelcompare.png)

In situations where you have more than one viewport set to the Perspective viewport, you can choose which viewports will have the full cinematic control by enabling or disabling **Allow Cinematic Control** in the viewport options menu. In most cases, you will want to enable **Allow Cinematic Control** for at least one viewport, and leave it disabled for all others.

![allow cinematic control comparison](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0136a64a-5f4f-4091-a657-f16ee4f40dec/cinecontrol2.png)