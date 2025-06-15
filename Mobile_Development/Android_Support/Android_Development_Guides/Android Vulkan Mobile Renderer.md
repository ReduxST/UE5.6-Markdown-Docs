# Android Vulkan Mobile Renderer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-android-vulkan-mobile-renderer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-android-vulkan-mobile-renderer-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:16

---

**Unreal Engine** (UE) has built-in support for the **Vulkan** graphics API. Vulkan is a low-overhead, cross-platform 3D graphics library that gives developers more control over the GPU and lower level CPU usage for their Android base mobile projects. The following document shows how you can enable and use Vulkan in your UE Android projects.

## Vulkan Video Drivers for PC Development

To make sure that you can visualize the rendering options Vulkan has available on your development PC, you will need to make sure you download and install the latest version of video card drivers for your graphics card. Below you will find the minimal driver version you need to use to be able to preview what Vulkan will look like on your development PC.

-   [NVIDIA](http://www.nvidia.com/Download/index.aspx): 390.0 or later
-   [AMD](https://support.amd.com/en-us/download): 17 or later

## Checking Vulkan Device Compatibility

Determining if your smartphone supports the Vulkan rendering API can be challenging due to the wide range of Android smartphones on the market. To help you quickly find out if your smartphone supports the Vulkan API, it is recommended to install the following program from Google Play Store: [Hardware Caps Viewer for Vulkan](https://play.google.com/store/apps/details).

The Vulkan Hardware Capability Viewer is a client tool aimed at developers needing to gather hardware implementation details for devices that support the new Vulkan Graphics API.

## Supported Vulkan Devices

The following devices have Vulkan-specific profiles available in addition to non-Vulkan profiles:

-   Adreno 6xx
-   Mali G72
-   Mali G76
-   Mali G77
-   PowerVR GM9xxx
-   Samsung XClipse series

If your device uses Android 9 or higher and you have Vulkan enabled as a feature level for your project, it will use the Vulkan-enabled version of these GPU families' device profiles.

Please note that the ability to use the Vulkan API depends on if your mobile carrier has released the Vulkain update for your specific device variant. To find if this support has been pushed to your mobile device, you will need to contact your mobile carrier.

## Building for Vulkan

To build a UE project that has support for the Vulkan API you will need to do the following:

1.  Before you begin, make sure that you have your Android smartphone plugged into your development PC via USB and that your Android smartphone has developer mode enabled.
    
2.  Launch the UE Editor and create a new project using the **Games > Blank** template using the following settings:
    
    -   **Blueprint Project** enabled
    -   **Mobile** enabled
    -   **Maximum Quality** enabled
    -   **Starter Content** disabled
    
    When that is completed, press the **Create** button to create and load the new project.
    
    Click image for full view.
    
3.  Once the project has loaded, go to **Edit > Project Settings**, then under **Engine**, go to the **Rendering** section and make sure that **Mobile HDR** has been enabled under **VR**.
    
    Click image for full view.
    
4.  In the **Project Settings**, navigate to the **Platforms**, go to the **Android** section, make sure that the following options are enabled under **Build**:
    
    -   **Support OpenGL ES3.2**
    -   **Support Vulkan**
        
        Click image for full view.
        
5.  From the menu bar, click on the **Platform** button, go to **Android**, make sure, that **Android(ASTC)** option is selected and click on **Package Project**.
    
    ![Launch packaging project process](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/828fcd56-e514-4c32-8c95-2db7524ace7d/ue5_1-04-launch-packaging-project.png "Launch packaging project process")
6.  Select a location for UE to save the Android build and then press the **Select Folder** button to start the packaging process.
    
    ![Set packaging project folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9c77841-31fa-4fef-a00e-c0600a00e79d/ue5_1-05-save-build-location.png "Set packaging project folder")
7.  When the packaging process has been completed, open up the folder that the packaged build was placed in. Inside this folder, you should see two `BAT` files. Locate the `BAT` file that has the word **Install** in the name and double-click on it to install it to your device.
    
    ![Launch installation to device](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d06752c1-81d1-4913-9da0-a9d4a05468ab/ue5_1-06-launch-installation.png "Launch installation to device")
8.  Once installed on your device, press on the UE icon that has your project name under it to launch the project on the device.
    
    Click image for full view.
    

## Enabling Vulkan Preview Rendering in Editor

If you have enabled Vulkan in your project as described above, a preview rendering option will appear automatically. On the **Main Toolbar**, click on the **Settings** button and go to the **Preview Rendering Level** option. Select the **Android Vulkan** option to enable the Vulkan preview in the UE Viewport.

![Set Preview Rendering Level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf37303f-b007-4325-90e2-9e55ba43bc1b/ue5_1-08-set-preview-rendering-level.png "Set Preview Rendering Level")

The Viewport should read **Feature Level: Android Vulkan ES31** in the lower-right corner.

After doing this, the Editor will need to recompile the entire shader cache to include the required Vulkan options. Depending on the size of your project and power of your development computer, this process could take anywhere from a few minutes, to an hour or more to complete.

## Enabling the Vulkan Mobile Preview Render

To enable Vulkan Render with the Mobile Preview Render, do the following in your project:

1.  From the **Main Toolbar**, go to the **Edit** option and then select the **Editor Preferences** option from the main menu.
    
    ![Open Editor Preferences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1961faf-48a9-448c-b3e9-cca815b55c95/ue5_1-09-open-editor-preferences.png "Open Editor Preferences")
2.  In the **General** section under the **Experimental** category, expand the **PIE** section then select the checkmark box next to the **Allow Vulkan Mobile Preview** option.
    
    Click image for full view.
    
3.  On the **Main Toolbar**, click on options menu on the **Play** panel and select the **Vulkan Mobile Preview (PIE)** from the drop down list.
    
    ![Run project in Vulkan Mobile Preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7aa0a653-482b-4179-b9f1-8bca8ee5ac64/ue5_1-11-run-project-in-vmp.png "Run project in Vulkan Mobile Preview")
4.  Click on the **Play** button that is on the **Main Toolbar** to launch your UE project in a new preview window with Vulkan Render enabled. If everything has been setup successfully, you should see something similar to the image below.
    
    Click image for full view.
    

If you do not see **(SF\_VULKAN\_ES31)** at the top of the preview window next to the project name, that means the project is not using the Vulkan API. Should this happen, make sure that your video card drivers are up to date.