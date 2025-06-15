# Mobile Previewer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-mobile-previewer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-mobile-previewer-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:37

---

![Example of Rendering Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acef0600-e77c-49dc-a38c-a1bb6508afb1/ue5_1-01-rendering-level-example.png "Example of Rendering Level")

1:Mobile / HTML5 - Open GL ES2, 2:Shader Model 4.0 - DX10/ OpenGL 3.3+, 3:Shader Model 5.0 - DX11/ OpenGL 4.3+.

In **Unreal Engine** (UE), you can use the **Mobile Previewer** to preview what your scene will look like on different mobile devices directly in the **Viewport**. When enabling the different preview rendering levels, the Materials in your scene will be recompiled to best emulate the look and feature set of the renderer preview that you selected. The Mobile Previewer enables you to switch back and forth between rendering levels seamlessly, without having to restart the Editor.

## Using the Mobile Previewer

The Mobile Previewer enables you to quickly change between different renderers for your current UE session so that you can get an idea of what your game will look like on the device(s) that you're targeting while allowing you to work in the UE. To learn how to change to a different renderer preview, follow these steps:

While you do not need to restart the UE for the new preview rendering level to take effect, the first time you change to a preview rendering level the UE will need to time to recompile the shaders. Subsequent changes to previously used rendering levels should be nearly instantaneous.

1.  From the **Main Toolbar**, select the **Settings** button to expand the listed menu items. Under the **Scalability** section, hover over the **Preview Rendering Level** to expose the different rendering levels options you can select from.
    
    ![Enable Preview Rendering Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee3b8003-d73a-478e-958c-3428d6d1745d/ue5_1-02-mobile-preview-rendering.png "Enable Preview Rendering Level")
2.  Hover the mouse over the section rendering level you'd like to preview and click to select it.  
    You will see the **Changing Preview Rendering Level** progress bar pop-up. Wait for this to finish and recompile shaders.
    
    ![Changing Preview Rendering Level progress bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3838cc5c-3e5c-4d32-b77b-38476367bb49/ue5_1-03_change-preview-rendering-level.png "Changing Preview Rendering Level progress bar")
    
    The **Preview Mode** button appears next to the **Sequencer** button, the button shows the icon for the selected preview mode. Clicking it disables the Mobile Previewer.
    
    ![Previewer Icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/000ae8b5-2efa-448b-bc04-4d982e8b9b61/ue5_1-04-previewer-icon.png "Previewer Icon")
3.  Once a rendering level has been selected, the Materials in the viewport will automatically update to reflect the new rendering method using the **Material Qualities** enabled or disabled for that target platform. (See the [Platform Material Quality Settings](/documentation/en-us/unreal-engine/using-the-mobile-previewer-in-unreal-engine#platformmaterialqualitysettings) section of this page for more details on how to adjust these further.)
    
    ![Android Vulkan Preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82d7234e-8ea8-4478-80e6-da62449b195d/ue5_1-05-vulkan-preview.png)
    
    ![Desktop Shader Model 5 (SM5) Preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc51dc35-26f4-4cc7-9b6f-36cdebe58afa/ue5_1-06-sm5-preview.png)
    

The Mobile Previewer is intended to match mobile devices as closely as possible but it may not always be indicative of what your project is going to look like on the target device. You should always make sure to fully test your project on your target device and only use the mobile previewer to see if your work is headed in the right direction.

### Mobile Previewer in PIE

You can use the **Mobile Preview ES3.1 (PIE)** option to launch a standalone version of your UE mobile project that will use the same rendering path as if the project was run on a mobile device. This is a great way to preview the changes you are making without having to go through the entire cooking and deploying process. To launch your UE project in a Standalone game that uses the Mobile Preview, you will need to do the following:

1.  From the **Main Toolbar**, click on the drop-down button of the **Play** panel to expose the **Change Play Mode and Play Settings** settings.
    
    ![Show Play Mode Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cd4cbc5-df26-4f90-ba7e-fecfdd03f8f4/ue5_1-07-show-play-mode-options.png "Show Play Mode Options")
2.  Select **Mobile Preview ES3.1 (PIE)** option and your project will then be launched in a new window that simulates what your project should look like on a mobile device.
    
    ![Mobile Preview ES3.1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f12ea929-6a3b-40f9-b907-616b5187bf89/ue5_1-08_actions-mob-preview.png "Mobile Preview ES3.1")

## Enabling Vulkan Mobile Preview

You can use the **Vulkan Mobile Preview (PIE)** option to launch a standalone version of your UE mobile project using the Vulkan render. This is a great way to preview the changes you are making without having to go through the entire cooking and deploying process. To launch your UE project in a Standalone game that uses the Vulkan Mobile Preview, you will need to do the following:

1.  To enable the **Vulkan Previewer** you will need to first open up the **Editor Preferences** by going to the **Main Toolbar** and clicking on **Edit** and then select **Editor Preferences**.
    
    ![Open the Editor Preferences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23aa32ec-b1d9-496a-aa79-0424034c2d13/ue5_1-09-open-editor-preference.png "Open the Editor Preferences")
2.  In the **Editor Preferences** menu, locate the **General** heading and then click on the **Experimental** section.
    
    Click for full image.
    
3.  Locate the **PIE** section and then click on the **Allow Vulkan Mobile Preview** option to enable it.
    
    Click for full image.
    
4.  Close the **Editor Preferences** and then from the **Main Toolbar**, click on the drop-down button of the **Play** panel to expose the **Change Play Mode and Play Settings** settings.
    
    ![Show Play Mode Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7e75d01-0165-41f1-874f-faf6f64a1644/ue5_1-07-show-play-mode-options.png "Show Play Mode Options")
5.  Select the **Vulkan Mobile Preview (PIE)** option and your project will then be launched in a new window that simulates what your project should look like on a mobile device.
    
    ![Select the Vulkan Mobile Preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42b18ad1-7d48-4e62-9a48-c6cd87759b4b/ue5_1-12_vmp-use.png "Select the Vulkan Mobile Preview")

## Platform Material Quality Settings

In the **Project Settings** under the **Platforms** category, you can select different platform **Material Quality** sections to enable or disable specific features for the target platform.

Click for full image.

For any of these changes to take effect, be sure to click the **Update Preview Shaders** button.

![Update Preview Shaders](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fbbc05a-bad3-4828-9a50-ce83bc038d99/ue5_1-14-update-preview-shaders-button.png "Update Preview Shaders")

## Preview Rendering Level Selections

When you select your Preview Rendering Level, you will have a few options to select from. Use the table below to select the option that best fits your target device.

| Device Target | Description |
| --- | --- |
| High-End Mobile / Metal |   |
| **Default High-End Mobile** | This will emulate the default high-end mobile material quality settings without using any material quality overrides specified in the Project Settings. |
| **Android GLES 3.1** | Provides a preview emulation of supported Android OpenGL ES3.1 quality settings. The Material Quality settings can be set in the **Project Settings** > **Android Material Quality - ES31** section. |
| **Android Vulkan** | Provides a preview emulation of supported Android Vulkan quality settings. The Material Quality settings can be set in the **Project Settings** > **Android Material Quality - Vulkan** section. |
| **iOS Metal** | Provides a preview emulation of supported iOS Metal quality settings. The Material Quality settings can be set in the **Project Settings** > **iOS Material Quality - Metal** section. |
| Mobile / HTML5 |   |
| **Default Mobile / HTML5** | This will emulate the default mobile material quality settings without using any material quality overrides specified in the Project Settings. |
| **Android** | Provides a preview emulation of supported Android OpenGL ES2 quality settings. The Material Quality settings can be set in the **Project Settings** > **Android Material Quality - ES2** section. |

Some of the available Preview Rendering Levels are not visible until you've enabled them as a target platform via the Project Settings, namely, Android OpenGLES 3.1 and Android Vulkan. iOS Metal defaults to on, however, it will also be removed as an available preview option if its target platform is disabled.

## Mobile Device Preview Options

Due to the wide range of mobile phone bezel designs, it can be challenging to make sure that parts of your UI are not obscured by the mobile device's bevel. To help make sure your UI is not obscured by the device, you can use the **Device Launch** option to overlay different mobile phone bezel designs. To use this in your UE project, all you need to do is the following.

1.  First, open up your **Editor Preferences** by going to the **Main Toolbar** and clicking on **Edit** and then select **Editor Preferences**.
    
    ![Open the Editor Preferences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/688efe56-9fe8-447f-bd17-c03323a86b41/ue5_1-09-open-editor-preference.png "Open the Editor Preferences")
2.  In the **Editor Preferences** menu, locate the **General** heading and then click on the **Experimental** section.
    
    Click for full image.
    
3.  Locate the **PIE** section and then click on the **Enable mobile PIE with preview device launch options** to enable the bezel overlays. Close the **Editor Preferences** menu and restart UE for applying this settings.
    
    Click for full image.
    
4.  From the **Main Toolbar**, click on the drop-down button of the **Play** panel to expose the **Change Play Mode and Play Settings** settings.
    
    ![Show Play Mode Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b10ea02-6656-4b78-91d6-89073f1dcf0b/ue5_1-07-show-play-mode-options.png "Show Play Mode Options")
5.  From the displayed menu, go to **Mobile Preview (PIE)** > **Android** and then select the device you want to test against from the list.
    
    Click for full image.
    
6.  Now click the **Launch** button to launch your project. When your project loads it will be using the device preview like in the following image.
    
    ![Device Playing Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81fff9dd-669b-44d8-afd6-e104a0bbfa71/ue5_1-17-phone-bezel.png "Device Playing Example")

## Copying a Physical Device's Configuration in the Previewer

In Unreal Engine (UE 5.5) and newer, you can save a JSon file containing the device profile and CVars used on a specific device, then load it in UE to use in the Mobile Previewer, providing a 1:1 match for all your project's graphics settings as they would appear on your device. This page provides a walkthrough for this process.

### Prerequisites

To follow this guide, you need to set up your project for Android development, and you need to connect an Android device to your computer with development mode enabled. Refer to the [Android Quickstart Guide](/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development) for a walkthrough of all basic setup for an Android project, and refer to [Setting Up Your Device for Development](/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine) for a walkthrough of preparing your device and connecting it to UE.

### Saving Device Data to JSon

To save your target device's data to a JSon file, follow these steps:

1.  Click the **Settings** button in the upper-right corner of Unreal Editor, then navigate to **Preview Platform** and open the sub-menu for your preferred platform. This example uses Android.
    
2.  Click **Generate Platform JSon**. Select the test device you want to generate a JSon file for.
    
    Click image to enlarge.
    
3.  In the dialog that appears, choose where you want to save your JSon file.
    

## Loading JSon Device Data

To load your device's data in Unreal Editor's Mobile preview window, follow these steps:

1.  Open **Settings** \> **Preview Platform**, then open the sub-menu for your preferred platform. This example uses Android.
    
2.  Select either **Preview OpenGL** or **Preview Vulkan**, then click **Preview via JSon**.
    
    Make sure to choose the appropriate graphics API for your device from the **Preview Platform** > **Android** menu, otherwise you will not get an accurate preview.
    
3.  A dialog appears prompting you to open a JSon file. Locate the JSon file you saved and open it.
    

Unreal Editor will load all applicable CVars from the device profile of your target device. When you use the Mobile Preview, it should be a 1:1 match with what you would see on the screen of your device.

### Further Reading

For more information about Vulkan compatibility with Android devices, see the [Vulkan Mobile Renderer page](/documentation/en-us/unreal-engine/using-the-android-vulkan-mobile-renderer-in-unreal-engine).

For more information about device profiles, see the following pages:

-   [Device Profiles](/documentation/en-us/unreal-engine/setting-up-device-profiles-in-unreal-engine)
    
-   [Customizing Android Device Profiles page](/documentation/en-us/unreal-engine/customizing-device-profiles-and-scalability-in-unreal-engine-projects-for-android)