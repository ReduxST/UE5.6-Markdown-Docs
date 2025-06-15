# Packaging Android Projects

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-android-projects-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/packaging-android-projects-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:21

---

Windows macOS Linux

This page takes a look how to package your **Unreal Engine** (UE) project for deployment to an Android device. The Android packaging process in UE is simple to use and outputs several convenient files for installing and uninstalling your project from phones for testing.

## Essential Setup

First, it is better to fulfill the following requirements and project setup:

-   You will need **Android Studio** set up on your computer. See [Setting up Android SDK and NDK](/documentation/en-us/unreal-engine/advanced-setup-and-troubleshooting-guide-for-using-android-sdk).
-   Your Android device must have **Development Mode** and **USB Debugging** enabled. See [Setting Up Your Android Device For Development](/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine).
-   You will need to configure your **Project Settings** for Android and accept the Android SDK license agreement. See the [Android Quick Start Guide](/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development).

If you have not already created a project, create one using the **Third Person Template**, with **Target Platform** set to **Mobile** and quality set to **Scalable**.

## 1\. Packaging Your Project

This section explaines how to package the project as a `.APK` file.

In the example package configuration is set to **Development** for testing this game, but when your game is complete, you can package it using **Shipping** configuration. Navigate to **Platforms > Android** and select **Shipping** for setting packaging configuration to Shipping.

1.  In the **File** menu, go to **Package Project > Android** and select the Texture format you want to package. This example uses Android **ETC2** as it is supported by all devices.
    
    Click image for full view.
    
    ![Select Package Project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/612b00c4-9ebd-4af7-920b-2948ad9889e1/aqs_mac_01.png "Select Package Project")
    
    Click image for full view.
    
    Different devices support different Texture formats depending on the hardware they run on. See, [Android Development Reference](/documentation/en-us/unreal-engine/android-development-basics-for-unreal-engine) for a detailed breakdown of the various formats.
    
    | **Format** | **Description** |
    | --- | --- |
    | **ETC2** | Supported by all OpenGL 3.x class devices and supports alpha compression. |
    | **DXT** | Supported by Nvidia Tegra GPUs and supports alpha compression. |
    | **ASTC** | Latest Texture compression format allowing more quality control by specifying block size and supports alpha compression. Available on some devices at this point. |
    
    If you are using an older version of Unreal Engine to support an existing project, you will also have access to the following legacy Texture formats.
    
    | **Format** | **Description** |
    | --- | --- |
    | **ETC1** | Supported by all Android based devices but cannot compress alpha textures (they are stored uncompressed). Recommend using an RGB and a separate alpha texture if need alpha to get better compression. |
    | **ETC1a** | Uses ETC1 for non-alpha textures and ETC2 for alpha texture. If the device does not support ETC2, alpha textures will be uncompressed into RGBA at runtime. This format can be used on both ETC1 and ETC2 devices, but ETC1 for non-alpha textures may not be as high-quality as ETC2. |
    | **ATC** | Supported by Qualcomm Adreno GPUs and supports alpha compression. |
    | **PVRTC** | Supported by PowerVR GPUs and supports alpha compression. |
    
2.  You will be prompted for a location to save your packaged game, which should default to your project folder. Create a new folder and call it **AndroidBuilds**.
    
    ![Create folder for packaging project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8943a700-4727-4f59-bade-f2d5502f6419/ue5_1-02-package-project-folder-win.png "Create folder for packaging project")
    
    Click image for full view.
    
3.  While your project is being packaged a packaging message will appear in the bottom right corner showing the progress of the packing.
    
    ![Packaging Progress message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8a17a4d-dfd9-47c4-a794-2de7d155cf7d/ue5_1-03-packaging-progress.png "Packaging Progress message")
4.  Once packaging is successful, a Packaging Complete message will appear in the bottom right of the Editor.
    
    ![Packaging Complite message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5eb2be5a-4b56-4a3f-9301-57205601b2c7/ue5_1-04-packaging-complete-message.png "Packaging Complite message")
5.  Navigate to the folder you created in step two.
    
    ![Open folder for packaging project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56b31380-5ce3-4812-9255-3d8271d64be7/ue5_1-05-open-package-folder-win.png "Open folder for packaging project")
    
    Click image for full view.
    

## 2\. Deploying A Packaged Project to Device

Now that you have packaged your project as a `.APK`, this section will instruct you on how to deploy your build to a device.

1.  Plug your Android device into your PC with a USB cable. If prompted, allow your PC to change files.
    
2.  **Double-click** on the `Install_[ProjectName]_Development.bat` batch file to install the project on your Android device.
    
    ![Install the project to Android device](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3091e12f-1984-4a32-9c97-2d9b8047ba6d/ue5_1-06-install-to-device-win.png "Install the project to Android device")
    
    If you do not have your device plugged in via USB, running the `.BAT` file will do nothing.
    

1.  Plug your Android device into your PC with a USB cable. If prompted, allow your PC to change files.
    
2.  Open up the Android\_ETC2 folder and then **Double-click** on the `Install_[ProjectName]_Development_armv7-es3.command` file to install the project on your Android device.
    
    If you do not have your device plugged in via USB, running the `.command` file will do nothing.
    

1.  Plug your Android device into your PC with a USB cable. If prompted, allow your PC to change files.
    
2.  Open the **Android\_ETC2** folder, where you'll find the files that were created during the packaging process.
    
    Click image for full view.
    
    You should see the **Installation** and **Uninstallation** shell scripts (*.sh) along with the Android Application Package (*.apk) that contains all of the files you need to install the project onto any Android device that supports the ETC1 compression scheme.
    
3.  Now, open up the terminal from this folder's location by right-clicking inside of the folder and selecting **Open in Terminal**.
    
    Click image for full view.
    
4.  Enter `./Install_LinuxAndroidProject_Development-arm64.es2.sh` into the terminal to install the project onto your Android device.
    
    Click image for full view.
    
    If you're having trouble running the shell script, try entering `adb devices` into the terminal to verify that your device is connected to your computer.
    
5.  During the installation process, the shell script should flush the following output to your terminal
    
    Click image for full view.
    
    When the shell script has completed the installation process, you should see an **Installation successful** message.
    

When you have completed this How-To, your project should appear on your Android device per the following image:

Click image for full view.

In addition, you will have packaged `.APK` files and accompanying helpers to deploy them to other devices for testing.

## Packaging App Bundles

**Android App Bundles** are a distribution format offered by Google as an alternative to packaging `.APKs`. Instead of creating different `.APKs` for different subsets of devices, you can create a single Android App Bundle build (`.aab`) and upload it to the **Google Play Store**. The store's dynamic distribution system then uses the contents of the App Bundle to generate a `.APK` optimized for the user's specific device when they download the application.

In addition to greatly condensing the work involved in maintaining builds on the Google Play Store, App Bundle builds can distribute `.APKs` with up to 150 MB instead of the previous limit of 100 MB. This limit applies to the final `.APK` and not the App Bundle used to generate it.

To create an App Bundle Build, open your **Project Settings** and navigate to the **Platforms > Android** section. In the **App Bundles** section, enable **Generate Bundle (AAB)**.

Click image for full view.

Now when you package a project for Android, you will generate a `.aab` file to upload to Google Play. You will also generate a universal `.apk` for testing purposes.

As a limitation of the Google Play Store, Android App Bundles can not be distributed with `.obb` files.

The other settings available for configuring App Bundle builds enable you to fine-tune the degree of sensitivity that the App Bundle will use in generating the final `.apks` for your project.

| Setting | Description |
| --- | --- |
| **Generate Universal APK from Bundle** | Enabling this setting will allow the App Bundle to generate a universal .apk file for end-users, which can be run on any kind of device. This does not affect the universal .apk that is generated for testing on your machine. |
| **Enable ABI Split** | The App Bundle will generate separate .apks based on the Application Binary Interface used by the user's CPU. For example: arm64-v8a, x86, x86\_64. |
| **Enable language split** | The App Bundle will generate separate .apks based on the user's language. Only strings localized for the user will be downloaded. |
| **Enable density split** | The App Bundle will generate separate .apks based on image resolution and DPI. Only icons and splash screens compatible with the user's device will be downloaded. |

As an example, if you enabled ABI split but disabled language split, the `.aab` would tailor the final `APK` to a user's device based on the compatible ABI for their device, but every user would receive resources for all languages regardless of their device or language settings.

The default settings will result in the smallest possible size for the final `.apk`, while disabling these settings will result in larger `.APKs`.

For information on how to upload either `.APKs` or `.AABs` to the Google Play Store, refer to the guide on [Shipping with Android](/documentation/en-us/unreal-engine/packaging-and-publishing-android-projects-in-unreal-engine).