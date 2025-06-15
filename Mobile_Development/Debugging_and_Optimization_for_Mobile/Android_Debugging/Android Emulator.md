# Android Emulator

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-with-virtual-devices-using-the-android-emulator](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-with-virtual-devices-using-the-android-emulator)  
**Processed:** 2025-06-14 16:19:32

---

You can launch **Unreal Engine (UE)** applications for **Android** on the **Android Emulator** included with **Android Studio**, providing a way to test on a wide range of virtual Android devices without relying on a stock of physical devices. Once you have a virtual device set up, launch your application using Unreal Editor or UAT like you would with a physical device. This page provides a guide to:

-   Setting up a virtual device.
    
    -   Required specifications for running on Unreal Engine.
-   Launching the virtual device on your desktop.
    
-   Playing builds of your projects on your virtual device.
    
-   Debugging on a virtual device.
    

## Set Up a Virtual Device

By default, virtual devices in Android Studio are set up with roughly 256 MB of RAM and a limited amount of internal storage. You need to override these with the following specifications to be able to run Unreal applications reliably:

-   **RAM:** At least **4 GB**
    
-   **Internal Storage:** Twice the size of your packaged game.
    

To create a new device and set it up according to these specifications, follow these steps:

1.  Open **Android Studio**.
    
2.  Open the **Device Manager**.
    
    1.  If you do not have an Android Studio project to load, in the **Welcome to Android Studio** dialog, click the **More Actions** dropdown and select \*\*Virtual Device Manager.
        
        ![The Welcome to Android Studio dialog. The More Actions dropdown is clicked and the Virtual Device Manager is highlighted.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/444d330a-f9eb-499c-8af2-509627fc7a56/virtual-device-manager-noproject.png)
    2.  If you have an Android Studio project open, click **Tools** > **Device Manager**.
        
        ![The Tools dropdown in Android Studio, with a project open. The Device Manager is highlighted.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/011e4b00-cdab-4b67-bfc9-6f33ae02c643/device-manager-tools.png)
3.  When the Device Manager panel appears, click the **+** symbol and click **Create Virtual Device**. This opens the Virtual Device Configuration window.
    
    ![The Device Manager panel. The + button is clicked, and Create Virtual Device is highlighted.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf4a69c8-7bbf-4003-a99f-204e4d8bb1d3/create-device.png)
4.  In the Virtual Device Configuration window, right-click a profile for an existing device and click **Clone**. This opens the Hardware Profile Configuration window. This example uses the **Pixel 8 Pro** as a base.
    
    ![The Select Hardware dialog. The Pixel 8 Pro entry is highlighted in the hardware list, and the user has right-clicked. The Clone button is highlighted in the context menu.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cd521e2-4982-4f71-b2a0-4a7a00483c6c/clone-pixel-8.png)
5.  Set the following parameters for your device:
    
    1.  **Device Name:** Rename it using a naming convention that suits your organization. This example adds the suffix `(UE)` to denote that this hardware profile is tuned for UE.
        
    2.  **Memory**: Set your device's RAM to at least 4 GB.
        
6.  Click **Finish** to return to the Virtual Device Configuration window.
    
7.  Select your custom profile, then click **Next**.
    
    ![The Select Hardware Dialog. The custom Pixel 8 Pro (UE) profile is selected.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/244a367a-d9db-4213-98d1-5c7c9fabc447/custom-profile.png)
8.  You will be prompted to select a **System Image**. Select Vanilla Ice Cream or later. Make sure whatever version you choose supports **API 35** or later. When you are ready to proceed, click **Next**.
    
    1.  If the System Image you want is grayed out, or if you can't click the Next button after selecting it, click the download button next to the release name, which will install the components needed for that device image.
        
        If you do not use a system image that is compatible with Android 35, you can't run arm64. Instead, you need to target x86-64.
        
9.  You will be prompted to verify your configuration. Click **Show Advanced Settings**.
    
    ![The Android Virtual Device Configuration dialog. The Show Advanced Settings button is highlighted near the bottom.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ace4b782-8ffc-43cc-b047-e91f825a6a8b/avd-advanced-settings.png)
10.  In the advanced settings, make sure you have the following settings for **Memory and Storage**:
    
    1.  Double-check that the **RAM** is at **4 GB** or greater. The dropdown defaults to MB, so check that you switch it to GB or increase the memory accordingly before proceeding.
        
    2.  Set the **Internal Storage** to roughly twice the size of your game. For example, if your game is expected to be 2 GB in size, set this value to 4 GB.
        
    
    ![The Android Virtual Device configuration dialog. RAM is set to 4 GB, Internal Storage is set to 4 GB.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19b79fea-bec4-4dc9-aa31-31e757570631/desired-settings.png)
11.  Click **Finish** and the device will appear in the list of devices you can launch. You can click the **Play** button to start running your application. This may take a few minutes as the emulator loads up.
    
    ![The Device Manager panel. The custom Pixel 8 Pro (UE) profile is available in the device list, and the virtual device is running.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc3ccb5a-b435-41bb-a11f-a2231b589d82/virtual-device-running.png)

### Set Up Required Android Features For Your Virtual Device

For your virtual device to fully support UE projects, you need to enable some graphics features for it:

1.  Open the `Users/Username/.Android` folder.
    
2.  Open `AndroidFeatures.ini`.
    
    1.  If an `AndroidFeatures.ini` file does not exist, create one.
3.  Add the following variables:
    
    1.  `Vulkan=on`.
        
    2.  `GLDirectMem=on`. This enables hardware GPU acceleration.
        

## Run Your Android Virtual Device

You need to run your virtual device in the Android emulator to launch applications on your virtual device and attach debug processes to it. You can think of this as the emulator equivalent of turning your device on and hooking it up to your computer in developer mode. You can launch from Android Studio, or you can launch a standalone version of the emulator.

### Launch From Android Studio

To launch your virtual device from Android Studio:

1.  Open Android Studio, then click **Tools** \> **Device Manager**.
    
2.  In the **Device Manager**, click the **Play** button next to the device you want to launch.
    

The emulator will take a few minutes to load, but once it is loaded, you can control the virtual device with your mouse as you would a touchscreen.

### Launch a Standalone Emulator From Your Desktop

You can launch it from Android Studio from the **Device Manager**, or you can follow these steps to launch a standalone version of the emulator:

1.  Open the Android SDK root directory, then open the `Emulator` folder. You should see an executable called `Emulator.exe`.
    
2.  Use a command line to run this executable with the argument `-avd=[name of virtual device profile]`. For example, if you named your profile Pixel8\_UE, you would run with the argument `-avd=Pixel8_UE`.
    

The Android Emulator will display your virtual device on your desktop.

## Launch Your UE Application On a Virtual Device

Once your Android Emulator is running, it will be visible to UE through the Device Manager and the Platforms dropdown in Unreal Editor.

![The Platforms dropdown. The virtual device is highlighted at the top of the list.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1e1e5ca-7400-4a49-b9a1-6262725c784e/virtual-device-platforms-dropdown.png)

See the [Build Operations](/documentation/en-us/unreal-engine/cooking-content-in-unreal-engine) guide for more information.

While you specified a name for your virtual device's profile in Android Studio, this is not the same as the name of an *instance* of that virtual device. Double-check the device's name before providing the device name in command line arguments.

## Debugging On a Virtual Device

As long as your Android virtual device is running, you can debug on it with [Android Studio](/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-for-android-using-android-studio) or [Visual Studio using AGDE](/documentation/en-us/unreal-engine/debugging-unreal-engine-projects-for-android-in-visual-studio-with-the-agde-plugin) the same way you could with a physical device. However, to use the debugger, your Android app's architecture needs to match your PC's host architecture. For example:

-   If you are running on an x86\_64 PC or an Intel mac, your app must be set to use the x86\_64 architecture to debug on your desktop.
    
-   If you are using an Apple Silicon Mac or an arm64 Linux machine, your app must be set to use the arm64 architecture to debug on your desktop.
    

You can also take advantage of the following debugging and profiling resources:

-   Using [Android File Server and Unreal Android File Tool](/documentation/en-us/unreal-engine/android-file-server-for-unreal-engine) for debugging and file management.
    
-   Running Traces with [Unreal Insights](/documentation/en-us/unreal-engine/how-to-use-unreal-insights-to-profile-android-games-for-unreal-engine).