# SteamVR Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/steamvr-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/steamvr-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:38

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f1be034-1ada-4a8b-8b92-06c2dac787f5/steamvrht_bannerimage_00.png "SteamVRHT_BannerImage_00.png")

## Goals

The SteamVR Quick Start will walk you through How To setup your Unreal Engine 4 (UE4) project to work with and SteamVR and the Vive Head Mounted Display (HMD) headset.

## Objectives

-   Create a new UE4 project that is targeted towards SteamVR development.
    
-   Setting the required project settings so your project can be used with SteamVR.
    

## 1 - SteamVR Initial Setup

In the following section, we will take a look at how to get SteamVR setup so that it will work with Unreal Engine (UE).

### Steps

With each SteamVR development kit, Valve has provided [detailed instructions](http://media.steampowered.com/apps/steamvr/vr_setup.pdf) that will show you how to correctly set everything up. If you have not read this document, please do so before going any further as the following information is not a substitute for the information contained in the document created by Valve.

1.  Ensure that the Vive Head Mounted Display (HMD), Steam Controllers, Breakout Box, and Lighthouse Base stations are all unpacked, powered on, connected and setup according to the [instructions](http://media.steampowered.com/apps/steamvr/vr_setup.pdf) provided by Valve.
    
2.  If you have not done so already, make sure to download and install the [Steam Client](http://store.steampowered.com/about/) on your development PC.
    
3.  To install the **SteamVR** tools, use your mouse to hover over the Steam **Library** option and from the menu that is displayed, select the **Tools** option.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63bdf3ed-83db-4807-b9e6-7e910e6f5666/t_launch_steamvr_tools.png)
    
4.  Once you are in the Tools section, search for **SteamVR** using the search bar at the top. Once SteamVR is located, double-click on it to download and install it.
    
    Click for full image.
    
    You can also install SteamVR by clicking on the **VR** icon that is located on the upper right-hand corner of the Steam Client and following the provided instructions.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2cdb1e6c-2664-42f7-a6a6-0e8041b7191e/t_steamvr_icon_install.png)
    
5.  Double-clicking on the **SteamVR** option in the Tools menu will launch the SteamVR tools as shown in the image below.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d007372-a1d9-414c-9713-a338a8bfad57/t_steam_vr_ready.png)
    
    When SteamVR shows all devices in green (like in the image above) that means everything is working correctly. If a device shows up in gray then there is a problem with that device. SteamVR will tell you what is wrong with a grayed out device if you hover your mouse over it.
    
6.  Before you can use SteamVR with UE4, you must set up the SteamVR interaction area. To do this, right-click on the SteamVR window and select the **Run Room Setup** and follow the on-screen directions to set up the SteamVR interaction area.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2fd29405-dd8f-45f0-8a39-3e4a078cbdbc/t_steam_vr_app.png)
    

### End Result

When completed you will now have SteamVR setup and ready to be used with UE.

## 2 - Setting up UE to work with SteamVR

In the following section, we will go over How To set up a new Unreal Engine (UE) project to work with SteamVR.

### Steps

If you have not done so already, make sure to run the SteamVR **Room Setup** to establish and calibrate the VR tracking area. Failing to do this could result in SteamVR and UE4 not working correctly together.

1.  Create a new Project from the **Games > Blank** template, with the following settings:

***Blueprint** enabled* **Scalable 3D or 2D** enabled ***Mobile / Tablet** enabled* **No Starter Content** enabled

1.  Once the project loads, click on the small triangle next to the **Play** button and then from the menu that is displayed, select the **VR Preview** option.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18e814ae-39a8-4385-81b1-7ae74bd21a41/check_vr_working_00.png)

### End Result

When the VR Preview launches, put on your HMD and you should now see the basic level being displayed. You should also have the ability to rotate your head around in any direction like in the video below.

## 3 - On Your Own!

Now that you can view a UE project using SteamVR and the HTC Vive, try adding the following items to your project.

-   Use the [Migrate Tool](/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine) to move content from one of the mobile content examples into your project for use.
    
-   Add support for [Motion Controllers](/documentation/en-us/unreal-engine/motion-controller-component-setup-in-unreal-engine) so that the user can move objects around in VR just like they would in real life.
    
-   Use the [Render Resource Viewer](/documentation/en-us/unreal-engine/render-resource-viewer-in-unreal-engine) to help track your project's performance while you are building it.
    

Here are some additional resources that provide useful information for developing VR projects inside of Unreal Engine.

### Documentation

-   [Virtual Reality Development](/documentation/en-us/unreal-engine/developing-for-xr-experiences-in-unreal-engine)
    
    -   [VR Cheat Sheet](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine)
        
    -   [SteamVR Best Practices](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine)
        
-   [SteamVR Documentation](https://support.steampowered.com/kb_article.php)
    
    -   [User Guide](https://steamcommunity.com/steamvr)
        
    -   [Developer Guide](https://steamcommunity.com/steamvr)
        

### Content to Try

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21439a59-9a8f-48e7-919b-ae8b20e52973/store_couchknights_screenshot_3.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c59a10f-ebac-42de-bd86-0093e8a8e9a0/store_showdown_screenshot_5.png) |
| CouchKnights | Showdown |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/440b721a-df6e-4916-aaa5-c961a4512fae/store_vreditor_screenshot_5.png) |   |
| VR Mode |   |