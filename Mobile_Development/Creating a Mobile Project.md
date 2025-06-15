# Creating a Mobile Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-an-unreal-engine-project-for-mobile-platforms](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-an-unreal-engine-project-for-mobile-platforms)  
**Processed:** 2025-06-14 16:49:13

---

This guide provides details about how to set up a new **Unreal Engine** game project for Mobile platforms. While Mobile devices have a wide range of specifications and some may support more robust rendering features, the settings detailed here will work with the broadest range of new projects.

## 1\. Project Setup

Click image for full size.

1.  Open **Unreal Editor**. When the **Unreal Project Browser** appears, click **Games**.
    
2.  Configure your project as follows:
    
    -   **Project Template:** Top Down
        
    -   **Target Platform:** Mobile
        
    -   **Quality Preset:** Scalable
        
    -   **Project Name:** MobileTestGame
        

You can create a project that uses either **Blueprint** or **C++**.

1.  Click **Create** to create the project and open it in Unreal Editor.

## 2\. Overview of Project Defaults

This section provides details on the project defaults from the previous section and why these are recommended for new Mobile projects.

### Project Template: Top Down

While all game templates are equipped for Mobile user interfaces, the point-and-click interface for the top-down game is ideally suited for touchscreen use. You can just as easily use the third-person template.

### C++ Project vs. Blueprint-Only

Blueprint-only projects can publish to iOS and Android, but there are many features for configuring these platforms that are only available in C++.

-   You can build and test iOS projects on an iOS device with Blueprint-only projects, even from a Windows machine. However, iOS applications require Xcode to sign and provision a project for shipping on the App Store, so you will need a Mac with Xcode to ship your game eventually.
    
-   Android projects benefit from additional debugging options and tools when using a C++ project.
    

### Target Platform: Mobile

Selecting **Mobile** as your target hardware will disable several features that are either not supported by Mobile devices at all, not commonly supported, or that are too resource-intensive for the lower-end Mobile devices that Unreal Engine supports.

-   **Engine – Rendering**
    
    -   Bloom is disabled.
        
    -   Separate Translucency is disabled.
        
    -   Motion Blur is disabled.
        
    -   Ambient Occlusion is disabled.
        
    -   Anti-Aliasing Method is set to None.
        
-   **Project – Maps and Modes**
    
    -   Use Splitscreen is disabled.
-   **Slate**
    
    -   Explicit Canvas Child ZOrder is enabled.

### Quality Preset: Scalable

The **Scalable** setting provides a minimal rendering feature set that disables several post-processes and favors performance over fidelity.

-   **Engine – Rendering**
    
    -   Motion Blur is disabled.
        
    -   Auto Exposure is disabled.
        
    -   Anti-Aliasing Method is set to None.
        

You can change the target Platform and Quality Preset in **Project Settings** > **Target Hardware**. You can also change individual settings as necessary for your project, or you can override them on a per-device basis in your [Device Profiles](/documentation/en-us/unreal-engine/setting-up-device-profiles-in-unreal-engine).

## 3\. Setting Up Your Project for Android

For full details on setting up your project for Android, refer to the [Android Quickstart Guide](/documentation/en-us/unreal-engine/setting-up-unreal-engine-projects-for-android-development). The following is a summary of the required steps:

1.  Install the latest version of **Android Studio** that is compatible with Unreal Engine. Refer to the [Android Development Requirements](/documentation/404) page for information about the Android Studio, SDK, and NDK versions that are compatible with your current version of Unreal Engine. Refer to the Android SDK and NDK setup guide for information about the specific settings you need in Android Studio.
    
2.  Run the `SetupAndroid.bat`, `SetupAndroid.command`, or `SetupAndroid.sh` script located in your engine's **Extras** \> **Android** folder.
    
3.  Open **Project Settings** \> **Android**, locate the prompt for configuring your project for the Android platform, then click **Configure Now**. This will add the `Build/Android` folder to your project.
    
4.  If you have not accepted the Android SDK license, click **Accept SDK License** in your Project Settings as well.
    
5.  If you need to support the Google Play Store, scroll down to the **Google Play Services** section, locate the prompt for configuring for Google Play, then click **Configure Now**.
    
6.  Add an **Android Package Name** with a reverse-domain style string taking the format `com.(OrganizationName).(ProjectName)`. For this example project, the package name is `com.YourCompany.MobileTestGame`.
    
7.  Set up your Android device in **Developer Mode**, then connect it to your local area network with wi-fi or connect it to your computer with a USB cable. See [Setting Up Your Android Device for Development](/documentation/en-us/unreal-engine/setting-up-your-android-device-for-developing-applications-in-unreal-engine) for more details.
    

## 4\. Setting Up Your Project for iOS

To build a project for iOS, you need an Apple Developer Account and a MacOS computer with Xcode. For full details on setting up your project for iOS, refer to the [iOS Quickstart Guide](/documentation/en-us/unreal-engine/setting-up-an-unreal-engine-project-for-ios). The following is a summary of the required steps:

1.  Connect Xcode with your **Developer Account** in **Xcode** \> **Preferences** \> **Accounts**.
    
2.  Connect your iOS device to your Mac with a USB cable, then connect Xcode to your device in **Window** \> **Devices and Simulators**.
    
3.  Create an **Identifier (App ID)** for your app on your **Apple Developer page**. For the **Bundle Identifier**, provide a reverse-domain string taking the format `com.(OrganizationName).(ProjectName)`. For this example project, the package name is `com.YourCompany.MobileTestGame`.
    
4.  Register your device on the Apple Developer page.
    
5.  Set Xcode to **automatically manage code signing** for your project. Make sure the **Bundle Identifier** uses the same name you used in your App ID.
    
6.  Create a **Provisioning Profile** on the Apple Developer page using your Identifier, the Signing Certificate generated by Xcode, and your registered device. Download it to a convenient location, then click and drag it onto Xcode in your dock.
    
7.  Open your project in **Unreal Editor**. In **Project Settings** > **Platforms** \> **iOS**, set the **Bundle Identifier** to the same name you used in your App ID. After the editor discovers your Provisioning Profile and Signing Certificate, check the box for each of them.
    

## 5\. Testing Your Project On-Device

To test your project on a device, connect it to your computer with a USB cable, then click the **Platforms** dropdown. Your device should appear in the **Quick Launch** section. If you click the device's name, Unreal Engine will build your project and deploy it to that device.

## 6\. Final Result

After following the steps in this guide, your Mobile project is now ready to build, deploy, and test on both Android and iOS.