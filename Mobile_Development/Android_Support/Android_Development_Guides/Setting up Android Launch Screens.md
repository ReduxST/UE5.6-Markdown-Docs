# Setting up Android Launch Screens

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-android-launch-screens-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-android-launch-screens-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:15

---

Support for custom launch screens in **Android** projects is available inside the **Project Settings** under the **Platforms > Android > Launch Images** section. You can set the background, portrait, or landscape images used as well as whether or not the feature is enabled/disabled (refer to the table below for more information).

*Launch Images Options*

| Option | Description |
| --- | --- |
| **Show Launch Image** | Shows the launch image as a startup splash screen. If enabled, either or both launch images selected for the project will be included depending on the orientation setting in the project. |
| **Download Background Vertical Image** | Used as the background for OBB downloading when a device is in a vertical orientation. |
| **Download Background Horizontal Image** | Used as the background for OBB downloading when a device is in a horizontal orientation. |
| **Launch Portrait** | Used as a splash screen for applications with Portrait, Reverse Portrait, Sensor Portrait, Sensor or Full Sensor orientation. |
| **Launch Landscape** | Used as a splash screen for applications with Landscape, Sensor Landscape, Reverse Landscape, Sensor or Full Sensor orientation. |

You can change your application's orientation settings in Project Settings. Navigate to **Platforms > Android > APK Packaging** and click the **Orientation** dropdown to select what orientations you want to be valid for your application.

![Orientation Settings Dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc2fd605-e7fd-45b3-97d4-eff3794534cc/ue5_1-01-orientation-menu.png "Orientation Settings Dropdown menu")

## Configuring Launch Images

To configure your project to use the Launch Images:

1.  Inside your project from the **Main** menu, select **Edit > Project Settings**.
    
    ![Open the Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1298aab-93ea-485c-9684-f2001f2a9f52/ue5_1-02-open-project-settings.png "Open the Project Settings")
2.  In the **Project Settings**, on the left under **Platforms** select **Android** to display the project settings for Android apps.
    
    ![Navigate to the Android section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d6e451f-865f-4565-ab8c-b7038ebec8ac/ue5_1-03-select-android-section.png "Navigate to the Android section")
3.  Scroll down to the **Launch Images** section and make sure the **Show launch image** check box is enabled.
    
    ![Set the Show launch image option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/634f902a-4f65-40de-a4b9-fe047f155bcb/ue5_1-04-set-show-launch-image.png "Set the Show launch image option")
4.  Click the **...** icon next to each image to open a browser where you can select your image from your computer.
    
    ![Open browser for selecting the image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39207a53-34d0-4911-b924-2fa8bde4a1a2/ue5_1-05-browse-image.png "Open browser for selecting the image")
5.  Once you have selected the images you want to use they will be added to the project and included during the startup splash screen.
    
    ![Example of the final setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7bd7032-7d45-4ed8-9869-f4f7a1ee011a/ue5_1-06-final-setup.png "Example of the final set up")

Examples for portrait and landscape images may be found in the Engine/Build/Android/Java/res/drawable folder as PNG files.