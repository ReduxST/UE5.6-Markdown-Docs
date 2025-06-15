# Animating UMG Widgets

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-umg-widgets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-umg-widgets-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:06

---

![Banner Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af1a915b-751e-4def-9b09-db728aae54b8/ue5_1-animating-umg-banner.png "Banner Image")

Located along the bottom of the **Widget Blueprint Editor** are two windows which allow you to implement and control animations for your UI Widgets. The first, the **Animations** window, allows you to create essentially animation tracks which are used to drive the animation of your Widgets. The second, the **Timeline** window, is how an animation is applied to a Widget over time which is done by placing **Keyframes** at specified times then defining how the attached Widget should appear at that Keyframe (this could be size, shape, location, or even coloring options).

## Adding Animations

In order to get started with animations in UMG, you will need to first add an animation track. This can be done by clicking the **+Animation** button in the **Animations** window. Once you add an animation (yellow box below), you will be prompted to enter a name for the animation track.

![Adding an animation track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c8d5f38-1932-4cb5-89b5-75c07845cf33/ue5_1-01-add-animation.png "Adding an animation track")

After adding an animation track, the **Timeline** will become active and you can begin adding **Animation Keys** that are associated with values that shift over time for your Widgets. It should also be noted that you can have multiple animation tracks for each Widget, for example, having a button move across the screen and flash at the same time.

## Adding Animation Keys

There are two methods in which you can add Keys to an animation track. The first is by using the **Auto Key** checkbox located inside the **Timeline** window. This will automatically add Keys to the Timeline when you make adjustments to a value that supports Keyframing.

![Enabling the Auto Key checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f730144-63f4-46c7-8aaf-06316b4bb1d6/ue5_1-02-auto-keys-button.png "Enabling the Auto Key checkbox")

The currently selected animation track is highlighted at the top of the **Timeline** (indicated by the yellow box above).

The general workflow for adding Keys via the **Auto Key** option is to specify a time in which you want to reach your desired value for your Widget, then moving the **Timeline Bar** to that time and setting the value via the **Details** panel or by using the Grid (mostly used for location, rotation, or scale). Once you have set your end result, scrub to the beginning of your sequence and set the default state for your Widget. When scrubbing the Timeline bar between the two time periods, you should see your change occur gradually over the time period.

The second method in which you can add Keys is by clicking the **Add Key** button next to a setting that supports Keyframing.

![Example of Add Key buttons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dba6f572-b161-4914-88ed-8df89f4d58aa/ue5_1-03-add-key-buttons.png "Example of Add Key buttons")

In the image above, the icon next to each of the settings can be clicked on and doing so will result in a Key for the value being added to the Timeline at its current position. In the image below, Keyframes for **Background Color** have been added at 0.00 and 2.00 where the Background Color of a Button Widget is changed from White to Yellow over 2 seconds.

![Example of the animation track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd0ff3c1-bd68-4968-96fd-02a30f383e9a/ue5_1-04-animation-example.png "Example of the animation track")

## Changing Key Values

You can change the value for multiple Keys at a particular time on the Timeline by holding **Ctrl** and clicking on the Keys.

![Selecting multiple Keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c0a10f4-dc9c-47ef-992b-6c6d25e7efaf/ue5_1-05-select-multiply-keys.png "Selecting multiple Keys")

Above, we have selected each of the Keys associated with the position of a Vertical Box containing Buttons so that we may set them manually via the **Details** panel. Manually entering values allows for more precise control (for example) over moving Widgets as we only want to move the object along one axis.

## Calling Animations

When you create an animation, a variable for it is also created. If you look on the **Graph** tab under the **Animation** dropdown menu in the **MyBlueprint** window, you will see all your animation tracks you have created. By holding **Ctrl** and dragging the animation into the graph, you will be able to issue commands to it such as Play or Stop.

![Adding animation variable to the Graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3e40352-18d4-43d1-9d29-3c78925713f6/ue5_1-06-add-animation.png "Adding animation variable to the Graph")

Here we are telling our **Start Animation** to Play when the Widget Blueprint is constructed.

![Example of the script for Play animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c145e755-16e1-4203-bcc1-0aa9d5b07978/ue5_1-07-start-script.png "Example of the script for Play animation")

And here we are telling our **Blinking Button** animation to Stop playing when our **Start\_Button** is clicked on.

![Example of the script for Stop animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5f39c62-51f7-4293-9a72-a7d92d08118f/ue5_1-08-stop-script.png "Example of the script for Stop animation")

## Example: Animated Main Menu

Get familiar with the following example of using animations in a simple **Main Menu** screen. In the first animation Buttons move from the bottom of the screen to its center. In the second animation **Start** Button blinks. Follow the steps below to get result similar to the example.

This example is for demonstrating how to set up animation in UMG only as the Buttons do not do anything when clicked on.

1.  Set up your Main Menu layout. This layout has two **Vertical Box**. The first **Vertical Box** includes **Text "GAME TITLE"**, the second **Vertical Box** includes two Buttons named **START** and **QUIT**. The following image shows this layout and its structure.
    
    *Click image for full view.*
    
2.  Select the second **Vertical Box** that contains **Buttons**. Navigate to its properties in the **Details** panel and set **Anchor** as shown in the following image.
    
    *Click image for full view.*
    
3.  Set properties for selected **Vertical Box** that contains **Buttons** under **Slot (Canvas Panel Slot)** section.
    
    -   **Position X**: -300.0;
    -   **Position Y**: 500.0;
    -   **Size X**: 600.0;
    -   **Size Y**: 200.0.
    
    *Click image for full view.*
    
4.  Set **Position Y** to **1200.0** for selected **Vertical Box** that contains **Buttons** under **Slot (Canvas Panel Slot)** section.
    
    *Click image for full view.*
    
5.  Click the **+Animation** button in the **Animations** window and name it **StartAnimation**.
    
    ![Create StartAnimation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b893f574-d2ee-407e-932a-36ef679c102d/ue5_1-13-add-animation-1.png "Create StartAnimation")
6.  Click the **Add Key** button next to the **Position Y** option in the **Animations** window and give the Animation a name such as **StartAnimation**.
    
    ![Create the Key for the Position Y option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77d8aace-e1d6-4ecd-b46c-aea7d43a6795/ue5_1-14-add-key.png "Create the Key for the Position Y option")
7.  Move the **Timeline Bar** to **1.00** on the Timeline.
    
    ![Move the Timeline Bar to 1.00](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54266044-21dc-4ba0-876c-b3ba380af56b/ue5_1-15-move-timebar-1.png "Move the Timeline Bar to 1.00")
8.  Set **Top** to **500.0** and click the **Add key to the current time**.
    
    ![Set Top to 500.0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62b9f3a6-81c1-4753-9c04-84763372133f/ue5_1-16-set-top.png "Set Top to 500.0")
9.  Click the **+Animation** button in the **Animations** window and name it **BlinkingButton**. Move the **Timeline Bar** to **1.00** on the Timeline.
    
    ![Create BlinkingButton and set Timeline Bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea80757e-1a45-491c-a0f2-53290f0327ba/ue5_1-17-add-animation-2.png "Create BlinkingButton and set Timeline Bar")
10.  Select the **Start** Button in the layout of the widget. Navigate to the **Details** panel and click the **Add Key** button next to the **Background Color** under **Appearance** section.
    
    *Click image for full view.*
    
11.  Move the **Timeline Bar** to **1.50** on the Timeline.
    
    ![Move the Timeline Bar to 1.50](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/883eb8b1-25d7-4f9f-b96d-49480cb06d35/ue5_1-19-move-timebar-2.png "Move the Timeline Bar to 1.50")
12.  Set **Background Color** properties in the **Animations** window:
    
    *Set **R** to **0.1**;* Set **R** to **1.0**; \*Set **R** to **0.1**.
    
    ![Set Background Color properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c224798-a5bd-419c-aff1-16540c578e40/ue5_1-20-set-background-color-1.png "Set Background Color properties")
13.  Move the **Timeline Bar** to **2.00** on the Timeline. Set **Background Color** properties in the **Animations** window:
    
    *Set **R** to **1.0**;* Set **R** to **1.0**; \*Set **R** to **1.0**.
    
    ![Set Background Color properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/995fbb63-2462-4c48-b2eb-ec37357fadc8/ue5_1-21-set-background-color-2.png "Set Background Color properties")
14.  Click the **Graph** tab to create a Blueprint script for this widget.
    
    ![Navigate to the Graph window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d83576ea-b9d9-46db-9808-5730d9f458be/ue5_1-22-graph.png "Navigate to the Graph window")
15.  Create Blueprint Script as following image shows.
    
    ![Blueprint Script of the Main Menu widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/648c2ce1-663d-45ca-922a-9c633d98d8ba/ue5_1-23-widget-bp-script.png "Blueprint Script of the Main Menu widget")
    
    In this script when Widget Blueprint is constructed, it plays the **Start Animation** (Buttons move from the bottom of the screen to its center). Then it uses the **Set Timer** node to call a **Custom Event** called **StartBlinking** every 2 seconds (the Set Timer node is set to Looping). **StartBlinking** Custom Event plays the **Blinking Button** animation every 2 seconds (which is color shift over time from white to green for Start Button).
    
16.  Finally, create the Widget Blueprint from either the **Level Blueprint** or your playable Character Blueprint.
    
    ![Blueprint Script of the Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/373e04f7-cf35-4bcd-bdc3-bb1cb74eea6f/ue5_1-24-level-blueprint.png "Blueprint Script of the Level")
    
    In the **MyCharacter** Blueprint, we are creating the Widget containing the animations and UI layout of our Main Menu and adding it to the viewport by using the **Add to Viewport** node.