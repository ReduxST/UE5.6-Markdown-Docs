# Background Blur Widget

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-background-blur-widget-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-background-blur-widget-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:19

---

**Background Blur** is a widget you can add to the UI layout. Use this widget to provide an opportunity to surround its content with adjustable padding and apply a post-process Gaussian blur to background. Background Blur Widget can contain one child widget.

This page gives basic information about using and adjustment the Background Blur Widget in the UI layout. Also, get familiar with example of using and adjustment the Background Blur Widget below using **Unreal Motion Graphics UI Designer (UMG)**.

## Details

In the **Details** panel for a placed **Background Blur** widget, there are a couple of specific options that can be set, which pertain to the Widget:

![Background Blur widget options in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e1a5a37-7d6e-4b9f-858e-8597fc0b9cd5/ue5_1-01-appearance.png "Background Blur widget options in the Details panel")

| Option | Description |
| --- | --- |
| **Apply Alpha to Blur** | If true, modulates the strength of the blur based on the widget alpha. |
| **Blur Strength** | Sets blurry level of the background. Larger numbers increase blur, resulting in a larger runtime cost on the GPU. |
| **Low-Quality Fallback Brush** | An image to draw (instead of applying a blur) when Low-Quality Override mode is enabled. You can enable Low-Quality Mode for background blurs by setting the cvar `Slate.ForceBackgroundBlurLowQualityOverride` to **1**. This is usually done in the project's scalability settings. |
| **Blur Radius** | This is the number of pixels that will be weighted in each direction from any given pixel when computing the blur. A larger value is more costly but allows for stronger blurs. |
| **Corner Radius** | This is the number of pixels that will be weighted in each direction from any given pixel when computing the blur. A larger value is more costly but allows for stronger blurs. |

Each of the aforementioned properties can also be set (or changed) at runtime through Blueprint Script.

![Background Blur widget options in the Action menu in the Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65476d56-5e67-4d15-b7d5-f8290aa782ab/ue5_1-02-action-graph.png "Background Blur widget options in the Action menu in the Graph")

The ability to set other appearance settings (such as Horizontal and Vertical Alignment), as well as any padding around the Widget, can also be defined.

## Usage Example

The following example shows how to use the Background Blur Widget to highlight a menu when the game is paused, blurring out the background.

For achieving this result, add the Blur Widget with simplified menu, using the **Blur Strength** value to determine the strength of background blur being applied.

Create a script in the Menu Widget Blueprint's Graph to handle how menu reacts to button clicks.

![Blueprint script to handle how menu reacts to button clicks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65b41cd0-cf1e-41a6-b1c1-bc1887c9663b/ue5_1-04-bp-script.png "Blueprint script to handle how menu reacts to button clicks")

Above, when you construct the widget, you are turning on the Mouse Cursor. When the **Resume** button is pressed, you hide the cursor, un-pause the game, and remove the menu from being displayed. When the **Quit** button is pressed, you quit the game. Inside of your player character's Blueprint (see below), you add a script to create and display the menu when a key is pressed. In this case, whenever **P** is pressed, the game is paused when the menu is displayed.

![Blueprint script in the Character's Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/944dcc5b-7bef-4f68-8199-16e14774f245/ue5_1-05-character-bp-script.png "Blueprint script in the Character's Blueprint")

The result is the ability to pause the game and blur the background, keeping your menu intact for players to interact with.

![Example of the Pause Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93528e81-51be-4a15-8c91-9ddf986dbd82/ue5_1-06-example-blur-50.png "Example of the Pause Menu")

You could also decrease the Blur Strength from 50 (above) down to 10 (below) to make the background slightly more visible.

![Example of the Pause Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9894d43a-5caf-44f6-a0db-f16674b11f3a/ue5_1-07-example-blur-10.png "Example of the Pause Menu")