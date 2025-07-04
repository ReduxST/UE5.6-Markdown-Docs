# Android Development Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/android-development-basics-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/android-development-basics-for-unreal-engine)  
**Processed:** 2025-06-14 16:05:40

---

## Overview

The Android Development Reference pages contain a high-level explanation of the various software components and system settings you will need to make sure you have installed and setup on the computer you are using to develop your **Unreal Engine** (UE) Android project.

## Android Development Requirements

For information on the required SDK components and compatible hardware for the current version of Unreal Engine, refer to the [Android Development Requirements](/documentation/404) page.

## Environment Variables

Unless you installed CodeWorks for Android 1R7u1 from the provided UE installer, you will need to verify that some environment variables are set properly.

Once you have completed the installation (either by setting environment variables in the System Control Panel or by installing CodeWorks for Android 1R7u1), you will need to restart both the Editor and Launcher applications. This is due to how Windows applications store environment variables and then pass the old versions along to applications they start.

If you continue seeing the message about the Android SDK not being installed properly, it is recommended that you reboot your computer.

To set an environment variable:

-   Right-click on your **Computer** icon OR press **Windows-Break** on your keyboard.
-   Select **Advanced system settings** on the left.
-   Click **Environment Variables...**
-   For each variable (see below):
    -   Look for the environment variable (from below) to already be set in at least one of the lists (either System or User).
    -   If not found, then click **New...** next in the System section
    -   Enter the name and value.
    -   Click **OK**.
-   Click **OK** to close the **Environment Variables** window.

Here are the variables that we depend on, and where they should point:

**ANDROID\_HOME**

-   Set this to the directory where you installed the Android SDK or the `sdk` directory if you installed ADT.
-   It must contain a directory called `platform-tools`.

**JAVA\_HOME**

-   Set this to where the JDK is installed. It will probably be called something like `jdk1.8.0_121`.
-   It must contain a directory called `bin` with `javac.exe` in it.

**AGDE\_JAVA\_HOME**

-   Set this to the JDK installation required for using [AGDE](/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-for-android-in-visual-studio-with-the-agde-plugin).
-   It must contain a directory called `bin` with `javac.exe` in it.

**ANT\_HOME**

-   Set this to where you unzipped Ant.
-   It must contain a directory called `bin` with `ant.bat` in it.

**NDKROOT**

-   Set this to where you unzipped the NDK. It will probably be called something like `android-ndk-r11c`.
-   It must contain a file called `ndk-build.cmd`

Unless you installed CodeWorks for Android 1R7u1, you will need to verify that some environment variables are set properly.

Once you have completed the installation (either by editing your .bash\_profile file or by installing CodeWorks for Android 1R7u1), you will need to restart both the Editor and Launcher applications.

To set an environment variable you need to edit the **.bash\_profile** file in your home directory. The file is hidden in Finder, so you'll need to use Terminal to open it for editing. If you're not familiar with Unix terminal commands please do the following.

1.  Open **Terminal app** from /Applications/Utilities.
2.  Type **touch .bash\_profile** to create the file if it doesn't exist yet.
3.  Type open **.bash\_profile** to open the file in a text editor.
4.  Copy the following lines to the file (replacing paths to point to where you installed SDK and tools) and save it:
    
    -   export ANDROID\_HOME="/Users/epicgames/Devel/NVPACK/android-sdk-macosx"
    -   export NDKROOT="/Users/epicgames/Devel/NVPACK/android-ndk-r12b"
    -   export ANT\_HOME="/Users/epicgames/Devel/NVPACK/apache-ant-1.8.2"

Here are the name of the variables that we depend on and where they should point to.

-   **ANDROID\_HOME**
    -   Set this to the directory where you installed the Android SDK or the SDK directory if you installed ADT.
    -   It must contain a directory called platform-tools.
-   **ANT\_HOME**
    -   Set this to where you unzipped Ant.
    -   It must contain a directory called bin with a file called ANT in it.
-   **NDKROOT**
    -   Set this to where you unzipped the NDK and look for something similar to **android-ndk-r12b**.
    -   It must contain a file called **ndk-build**.

## Android Tips and Tricks

If you do not see your device listed in the **Launch** menu, here are some things to try:

-   Wait a few seconds and look again, as the background scanning for connected devices can take a short amount of time.
-   Check that your USB debugging connection is working.
-   Open a command prompt (Press **Windows+R**, and run `cmd.exe`)
    -   Type the following command: `adb devices`
    -   If you do not see any devices listed, your USB driver is not installed properly. How to install the driver depends on the model of your Android device. Search online for your device model and "USB driver", then install the driver.
    -   Additionally, you will need to make sure your device has Developer mode enabled with USB debugging is turned on. See the [Android Developer Using Hardware Devices guide](http://developer.android.com/tools/device.html) for more information (specifically items 2 and 3).
    -   Afterwards make sure the `adb devices` command works; without this, the engine will not be able to do anything with your Android device.

If your device shows up in the Launch menu but gets stuck deploying to the device, it is most likely because the device is not authorized for your PC to talk to it. If you click on the **Show Log** line in the progress bar, you may see that the last line indicates that it is calling `adb uninstall`.

-   As above, use `cmd.exe` to run the `adb devices` command.
-   If the device is listed but shows unauthorized, that indicates that you need to get the device to ask if you want to authorize the PC.
-   You may need to unplug and reconnect your device to make it show up.
-   It is recommended you check the **Always allow** checkbox.

If you do not see your device listed in the Launch menu, here are some things to try:

-   Wait a few seconds and look again, as the background scanning for connected devices can take a short amount of time to register the device.
-   Check that your USB debugging connection is working.
-   Open the Terminal app and then try the following.
    -   Type the following command into the terminal: `adb devices`.
    -   If you do not see any devices listed, your USB driver is not installed properly. How to install the driver depends on the model of your Android device. Search online for your device model and **USB driver**, then install the required driver.
    -   Additionally, you will need to make sure your device has Developer mode enabled with USB debugging is turned on. See the [Android Developer Using Hardware Devices](http://developer.android.com/tools/device.html) guide for more information (specifically items 2 and 3).
    -   Afterwards make sure the `adb devices` command works; without this, the engine will not be able to do anything with your Android device.

If your device shows up in the **Launch menu** but gets stuck deploying to the device, it is most likely because the device is not authorized to interact with your Mac. If you click on the **Show Log** line in the progress bar and see that the last line indicates that it is calling `adb uninstall`, try the following.

-   Open up the Terminal app and run the `adb devices` command.
-   If the device is listed but shows unauthorized, that indicates that you need to get the device to ask if you want to authorize the Mac.
-   It is recommended you check the **Always allow** check box to always allow your Mac to talk to this device.

## Android Texture Formats

Not all Android devices are made the same. In particular, there are 4 different kinds of rendering hardware. They each support different formats of compressed textures.

| Format | Description |
| --- | --- |
| **ETC1** | Supported by all Android based devices but cannot compress alpha textures (they are stored uncompressed). Recommend using an RGB and a separate alpha texture if need alpha to get better compression. |
| **ETC2** | Supported by all OpenGL 3.x class devices and supports alpha compression. |
| **ATC** | Supported by Qualcomm Adreno GPUs and supports alpha compression. |
| **DXT** | Supported by Nvidia Tegra GPUs and supports alpha compression. |
| **PVRTC** | supported by PowerVR GPUs and supports alpha compression. |
| **ASTC** | Latest Texture compression format allowing more quality control by specifying block size and supports alpha compression. Available on some devices at this point and will be required for Vulkan Level 1. |
|   |   |  

When you deploy or package your game for Android, the data will be converted to a format usable by an Android device (we call this process "cooking"). Because different devices support different compressed formats, you have a choice of what format you want to be cooked. In the **Launch** or **Package** submenu, you will see **Android** followed by the possible formats.

The first one (**Android**) actually takes all formats and puts them into the cooked packages. This will take longer, and will make larger packages, but will guarantee the minimal memory usage by choosing the best format at runtime. It will work on any device (as will **Android (ETC1)**).

Unreal Engine version 4.8 and later will now support the use of **ES31** and **AEP** rendering on Tegra K1 devices. Please note that due to the limited number of devices that currently support ES31 and AEP rendering, very little performance and compatibility testing has been completed at this time. If you are developing a project that is aimed at using one of these devices, it is highly recommended that you perform extensive performance and compatibility testing to ensure that the device delivers your project in the manner you intended.

### Choosing a Format

You most likely will want to choose an optimal format for your device. If you know the type of GPU in your device, you can look at the table above to choose a format. However, if you do not know, then you can choose **Android** or **Android (ETC1)**. When you run the game, if you tap the screen with 4 fingers at once, a dialog will pop up. This dialog is usually used to enter a console command (like `stat fps`), but it will also display the formats that your device supports. Once you have that list, you can use that to choose an ideal type when deploying/packaging. If you choose a format that your device does not support, it will fail to load.