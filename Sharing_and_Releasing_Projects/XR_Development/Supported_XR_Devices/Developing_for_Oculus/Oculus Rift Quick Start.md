# Oculus Rift Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/oculus-rift-quick-start-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/oculus-rift-quick-start-in-unreal-engine)  
**Processed:** 2025-06-14 16:39:23

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dbbd506-5d74-4ea2-8f93-368db6b537ce/oculus_topic_image.png)

### Goals

The Oculus Quick Start will walk you through setting up your computer and your Oculus Rift to be used with Unreal Engine (UE).

### Objectives

-   Download and install the needed software for the Oculus Rift Head Mounted Display (HMD) to work with your development PC.
    
-   Create a new UE project that is targeted towards Oculus Rift VIrtual Reality (VR) development.
    
-   Setting up the required project settings so your project can be used with the Oculus Rift VR HMD.
    

## 1 - Oculus Rift Initial Setup

In the following section, we will take a look at what software you need to install so that your Oculus Rift will work with UE.

You will need to be connected to the internet for 30 to 60 minutes while the Oculus runtimes are installing.

1.  Visit the [Oculus Setup page](https://www.oculus.com/setup/)[](https://www.oculus.com/en-us/setup/) and download the Oculus runtimes by clicking on the **Start Download** button in the center of the page.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76a6c268-3e0a-4693-973a-24a3c543112e/or_download_runtimes_00.png)
    
2.  Once the **Oculus Setup** executable has finished downloading, double click on it to begin the install process.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/434177e8-f893-44b8-9f0e-f760477433b2/oculus_rift_exe_00.png "Oculus_Rift_Exe_00.png")
    
    During the install process, you will be asked to install device software from **Oculus VR, LLC**. When this is displayed, press the **Install** button to continue the installation.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17637c66-a805-4091-8abf-18c6fe874429/rift_device_software_install_00.png)
    

### End Result

When the Oculus Rift software has completed installing, open the Oculus program and then go to the **Devices** tab. If everything has been setup correctly the Devices tab should look similar to the following image:  
![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/79a1761b-eb2e-4069-bade-864e3db09666/oculus_rift_devicestab_00.png "Oculus_Rift_DevicesTab_00.png")

## 2 - Testing out the Rift and UE

In the following section, we will go over How To set up a new UE project to work with the Oculus Rift.

1.  Create a new blank **Blueprint** project with hardware set to **Mobile / Tablet**, graphics set to **Scalable 3D or 2D** and **No Starter Content**.
    
2.  Once UE has launched, go to the **Main Menu** and change the **Play** option from the default of **Selected Viewport** to **VR Preview**, pressing VR Preview to launch the level.  
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1323882-31e4-4e96-bb6b-51d913335cff/rift_vr_preview_00.png "Rift_VR_Preview_00.png")
    

### End Result

When the VR Preview launches, put on your HMD and you should now see the basic level being displayed. You should also have the ability to rotate your head around in any direction like in the video below.

## 3 - On Your Own!

Here are some additional resources that provide useful information for developing VR projects inside of Unreal Engine.

### Documentation

-   [Virtual Reality Development](/documentation/en-us/unreal-engine/developing-for-xr-experiences-in-unreal-engine)
    -   [VR Cheat Sheet](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine)
        
    -   [Oculus Rift Best Practices](/documentation/en-us/unreal-engine/xr-best-practices-in-unreal-engine)
        
-   [Oculus Documentation](https://developer.oculus.com/documentation/)
    -   [User Guide](https://support.oculus.com/857827607684748/)
        
    -   [Developer Guide](https://developer.oculus.com/documentation/unreal/latest/concepts/unreal-engine/)
        

### Content to Try

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6cf35845-9e6c-4260-b1d1-6ab7fab2c823/store_couchknights_screenshot_3.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbc7a256-e900-45a3-a4c0-2719b6b05d56/store_showdown_screenshot_5.png) |
| CouchKnights | Showdown |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df4fe069-3a3c-4ebc-8ef7-584302ad65e2/store_vreditor_screenshot_5.png) |   |
| VR Mode |   |