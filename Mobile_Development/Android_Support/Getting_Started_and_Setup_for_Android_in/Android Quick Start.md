# Android Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development)  
**Processed:** 2025-06-14 16:49:55

---

![Banner Image](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9ec73e0-3190-4dcf-a51d-29af360abea0/android-quick-start-banner.png "Banner Image")

This Quick Start Guide will walk you through all of the essentials for setting up **Unreal Engine (UE)** for Android game development, including the following topics:

-   Setting up your test device and computer for Android game development.
-   Configuring new projects for mobile development.
-   Setting up **Unreal Editor** for packaging Android builds.
-   Setting the Editor to preview with mobile rendering feature levels.
-   Testing your project on-device from the Editor.
-   Packaging a standalone build of your project.

When you have completed this guide, you will be prepared to take an Android project from initial setup to testing and packaging.

## 1 - Android Development Prerequisites

In order to create and deploy an Android project, you will need to install several Android development prerequisites included with UE and ensure that your device is ready for testing.

1.  Follow the guide in [Setting Up Android SDK and NDK for Unreal](/documentation/en-us/unreal-engine/advanced-setup-and-troubleshooting-guide-for-using-android-sdk) to install Android Studio and set up the required SDK components for Android development in UE.
    
2.  On the device that you want to use for testing, open the **Settings** and enable **Developer Mode**.
    
3.  Locate **Developer Options** in your device's Settings, then enable **USB Debugging**.
    
    Click to full view
    
4.  Plug your device into your computer, then allow your computer to access your device's data.
    
5.  Permit your computer to install any needed drivers for your device.
    

Once you have completed these steps, you will be ready to develop new Android projects.

-   For more details about device setup, refer to our guide on [Setting up Your Android Device for Development](/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine).

## 2 - Creating Your Project

The following section shows the process of creation a new UE5 project, based on the Third Person template. This example demonstrates how quickly you can get a UE5 project running on an Android device.

1.  Launch **Unreal Editor**. In the **Unreal Project Browser**, use the following settings to create a new project:
    
    -   Project Category: **Games**
    -   Template: **Third Person**
    -   Target Hardware: **Mobile**
    -   Quality Level: **Scalable**
2.  Name your project **AndroidQuickStart** and click the **Create** button to finish creating the project.
    

Click to enlarge image.

Choosing Mobile for your target hardware and Scalable for your target quality level will ensure that your project accounts for the user interface and hardware limitations of mobile devices.

## 3 - Setting Up Unreal Editor for Android

Next, you need to make sure your **Project Settings** in Unreal Editor are configured for Android APK builds.

1.  Click **Edit > Project Settings** to bring up the Project Settings window.
    
    ![Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90f3c378-a8c3-49c8-979b-6e092e4e0575/ue5_1-03-project-settings.png "Project Settings")
2.  Inside of the **Project Settings** window, navigate to **Platforms > Android**.
    
3.  Under **APK Packaging**, find the **Android Package Name** and fill it with an appropriate company and project name. In this instance it uses **com.EpicGames.AndroidQuickStart**.
    
    Click to enlarge image.
    
4.  Under **APK Packaging**, find the **Minimum SDK Version** and **Target SDK Version**, fill it with an appropriate Android API version of devices, you create project for. In this instance it uses SDK Version 19 and SDK Version 28 accordingly.
    
    Click to enlarge image.
    
5.  Under **APK Packaging**, there will be a warning that reads "Project is not configured for the Android platform". Click the **Configure Now** button to automatically set up your project to write the required platform files.
    
6.  If the **Accept SDK License** button is enabled, click it in order to accept Android's SDK license agreement. If you have previously accepted this agreement, then you will not need to complete this step.
    
    Click to enlarge image.
    
7.  Under **Google Play Services**, there will be a warning that reads "Project is not configured for the Google Play services". Click the **Configure Now** button to automatically set up your project to write the required files.
    
    Click to enlarge image.
    

Your project will now be enabled to create Android builds and launch on an Android device.

## 4 - Configuring Editor and PIE for Mobile Previews

You can set Unreal Editor's **Play-In-Editor (PIE)** mode to provide a preview of how your game will look in the Mobile renderer.

1.  In the **Toolbar**, click **Settings > Preview Rendering Level**, then select one of the available rendering levels for Android.
    
    ![Preview Rendering Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/655ee6d4-bc21-4185-b654-55f46c610aa6/ue5_1-08-preview-level.png "Preview Rendering Level")
2.  Click the **dropdown** of the **Play** panel in the **Toolbar**. Choose one of the available **Mobile Preview** modes corresponding to the rendering level you selected.
    
    ![Mobile Preview PIE](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/06a13b6a-b322-4445-96b3-913d063f80d6/ue5_1-09-mobile-preview-mode.png "Mobile Preview PIE")

The Editor will now display your game in a way that is visually consistent with your target renderer. Additionally, when you press the PIE button, your game will launch in a standalone window set to a standard mobile aspect ratio and configured to emulate a touchscreen using your mouse. These settings will not affect packaging for mobile devices, but they will ensure that you have an accurate preview when working in the Editor.

Refer to the [Mobile Previewer](/documentation/en-us/unreal-engine/using-the-mobile-previewer-in-unreal-engine) reference for more information about how you can configure the Mobile Previewer.

## 5 - Launching on an Android Device

To test your current **Level** on an Android-based device, you will need to do the following:

1.  First need to make sure you have the Level you want to test open. In this example, it uses the **ThirdPersonMap** Level from the Blueprint based project that was created in the last step.
    
    ![Open Level Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0dde12e-66e8-4b80-be57-447ba10c4f57/ue5_1-10-correct-level-open.png "Open Level Blueprint")
2.  With the **ThirdPersonMap** now open, go to the **Main Toolbar** and click on **Platforms** button that displays more options.
    
    ![Level Platforms options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cec21085-511a-4e59-8010-7730f372869a/ue5_1-11-level-platform-options.png "Level Platforms options")
3.  From the **Platforms** menu under the **Quick Launch** section select your Android device from the list by clicking on it.
    
    ![Launch project on the device](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4306901b-7d65-4655-8116-2751f3ab71c6/ue5_1-12-launch.png "Launch project on the device")
4.  While your Level is being launched on your device, the progress will be displayed in the bottom right-hand corner of the screen like in the following image.
    
    ![Packaging progress message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/230a5110-a8f0-42a2-9c79-2de32b601785/ue5_1-13-packing-progress.png "Packaging progress message")
5.  When the deployment has finished, the project should automatically start running on your Android device. If the project fails to automatically start, you can start it by finding the App on your device and tapping on it to launch it.
    
    Click to enlarge image.
    

## 6 - Packaging Android Builds

The above steps provide a way to package and immediately launch a project on device. To package a standalone APK for distribution and testing, follow these steps:

1.  Go to the **Main Toolbar** and click on **Platforms > Android**. Enable the **Android (Multi:ASTC,DXT,ETC2)** option and click on **Package Project**.
    
    Click to enlarge image.
    
2.  When the **Package Project** dialogue appears, choose the directory where you want to save it. Here we save it in **AndroidQuickStart/Build**.
    
    ![Package Project dialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96fa8f9b-860b-4fd2-835d-133ec1a77f13/ue5_1-16-package-project-dial.png "Package Project dialog")
3.  Click **Select Folder** and Unreal Editor will begin packaging your project. Wait for it to finish packaging.
    

If you navigate to the folder where you output your build, the folder will contain the APK and OBB files necessary to install your game on an Android device. There are also a pair of **.bat** files that you can use to automatically install or uninstall your build to a connected device.

![Packaging Output](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f1c599e-782d-45a9-af22-da21a5acc3e4/ue5_1-17-output.png "Packaging Output")

For more detailed information on configuring the Packaging settings for Android builds, refer to the [Packaging Android Projects](/documentation/en-us/unreal-engine/packaging-android-projects-in-unreal-engine) reference page.

## 7 - On Your Own

With what you have learned in this Quick Start you are now prepared to package and distribute your UE5 projects to general Android devices. You should expand on UE5's provided templates by creating new gameplay and levels in order to create fully functional mobile game. Depending on your project's needs and the devices that you are specificially targeting, further configuration will be required in order to optimize your builds. The following links will provide you with more information for taking the next steps in building your projects:

-   [**Android Development Reference**](/documentation/en-us/unreal-engine/android-development-basics-for-unreal-engine) - General reference information for Android developers in UE.
-   [**Android Development Requirements**](/documentation/404) - Reference for compatible hardware as well as SDK and OS requirements to use specific versions of UE.
-   [**Android Debugging**](/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-for-android-using-android-studio) - How-to guide for debugging Android projects on-device.
-   [**Mobile Rendering**](/documentation/en-us/unreal-engine/rendering-features-for-mobile-games-in-unreal-engine) - Information about Mobile-specific rendering features.
-   [**Mobile Services**](/documentation/en-us/unreal-engine/in-app-purchases-and-ads-in-unreal-engine-projects) - Information about implementing online services and notifications.
-   [**Shipping with Android**](/documentation/en-us/unreal-engine/packaging-and-publishing-android-projects-in-unreal-engine) - Guidelines about preparing your game for distribution.