# Convert Colors in the Viewport and Play in Editor mode

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/apply-color-conversion-to-the-level-viewport-and-play-in-editor-with-opencolorio-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/apply-color-conversion-to-the-level-viewport-and-play-in-editor-with-opencolorio-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:47

---

You can apply OCIO configurations directly within the **Viewport** by adjusting the **Viewport View Modes** and you can apply OCIO configurations to **Play in Editor Mode** by creating and configuring a **Create In-Game OpenColorIO Display Extension** Blueprint node.

This page shows you how to apply your **OpenColorIO Configuration Asset** to the Viewport and to your project in Play in Editor mode.

## Prerequisites

You must set up the following in your project to complete the sections below:

-   An OpenColorIO Configuration Asset. Refer to the [OpenColorIO Quick Start](/documentation/en-us/unreal-engine/opencolorio-quick-start-for-unreal-engine) for steps on creating this Asset.

## Convert the Level Viewport's Colors

Follow these steps to apply color conversion to the Level Viewport.

1.  In the **Viewport**, click the **View Mode** button to open its dropdown menu. Choose **OCIO Display** to open the **Display Configuration** settings.
    
    ![The Viewport color management display configuration menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b0c8516-794a-43fc-b1d2-f0bd881ebd0c/viewport-color-management-display-configuration.png)
2.  In the **Display Configuration** settings, choose **Select an OCIO Asset** and select your **OCIO Configuration Asset** to add it to the Viewport view settings.
    
    ![Select an OCIO configuration asset from the display configuration menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2a337ca-268c-4373-ab71-90b1cc22e2e6/viewport-display-configuration-ocio-asset.png)
3.  The following two settings are the source and destination of the color transform. In this example, the source is **Utility - Linear - sRGB**, and the destination is **Output - sRGB Monitor**.
    
    ![An empty display configuration menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44350e26-5767-4033-8c6b-d9f174903b06/empty-ocio-conversion-settings-in-viewport.png)
4.  Click **Enable Display** to apply the OCIO color transformation to the Viewport.
    
    ![The display configuration menu after changing the settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce25c93c-bd18-4bee-b08e-8eaa1cbc5e73/ocio-color-conversion-filled-out-in-viewport.png)
5.  When you enable these settings, the Viewport disables **Tone Curve** and inserts color conversion into the post processing stage of rendering. It does this right after UE applies the **Tone Map** but before everything else.
    

The following image shows how the viewport's color is changed by the OpenColorIO configuration.

![OpenColorIO Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40acf826-8f60-48d3-bcd0-177ee47d1622/viewport-color-conversion-before.png)

![OpenColorIO Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d4449ad-56cb-43f3-b4ae-eaf1beb2833d/viewport-color-conversion-after.png)

OpenColorIO disabled / enabled in Viewport View Modes.

## Convert Colors in the In-Game Viewport

To convert colors in the in-game viewport, you must add a **Create In-Game OpenColorIO Display Extension** Blueprint Node to your Camera Actor's Blueprint class, and associate your OCIO configuration with it.

Steps

1.  Open your Camera Actors's **Blueprint Class** or create a new Camera Component Blueprint Class if you do not already have one and attach it to your Camera.
    
2.  Create a new **OpenColor IODIsplay Configuration** variable by clicking and dragging from the **In Display Configuration** pin, or by creating a new variable in the **My Blueprint** tab.
    
    ![The Blueprint editor window with the OpenColor IODisplay Configuration variable visible ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b19098c6-57ae-4ea3-8d7c-6b8c86bcea4a/pie-color-conversion-variable.png)
3.  Edit this variable in the **Details** panel by adding your **OCIO Configuration Asset** and adjusting the other settings to match your desired color configuration.
    
    ![The Blueprint editor showing a completed Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b27e269-47c5-4439-8d7a-b4fcead4e38f/pie-color-conversion-blueprint-overview.png)
4.  Create a new **Create In-Game OpenColorIO Display Extension** node and attach it to the **EventBeginPlay** node and your OCIO configuration variable as shown in the screenshot below.
    
5.  **Compile** and **Save** your Blueprint.
    
6.  From the **Level Editor Viewport**, click **Play** to open your project in Play in Editor mode to test your Blueprint.