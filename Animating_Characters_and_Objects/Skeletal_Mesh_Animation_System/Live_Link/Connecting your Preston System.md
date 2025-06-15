# Connecting your Preston System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/connecting-your-preston-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/connecting-your-preston-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:00

---

## Steps

Follow these steps if you are using a Preston system with your production camera.

In this example, the Preston MDR unit needs to convert the serial output to Ethernet. This is done by using a Tibo serial-to-Ethernet converter. This Ethernet connection needs to be on the same network as Unreal Engine. There are other hardware devices for streaming Preston data. Refer to the vendor for the relevant plugin or setup if sending Preston data using a different device.

1.  Click **Settings > Plugins** to open the **Plugins Menu**. Click the **Virtual Production** category and search for the **LiveLinkPrestonMDR** plugin.
    
    ![Open the Plugins Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/691313a9-e941-45bf-b743-c409868ead29/cc-pluginmenu1.png)
2.  Enable the plugin and click **Yes** on the message window. Click **Restart Now** to restart the editor.
    
    ![Enable the Preston plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af28ffc6-c42b-4f7a-ad52-126b6bd5e1ca/ccs-preston0.png) ![Click Restart Now](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9c536e7-cef1-4313-aca9-08b6c345d7cc/ccs-restarteditor.png)
3.  Once the editor finishes loading, go to the **Live Link** window and click **\+ Source > PrestonMDR**. Enter the **Tibo's IP Address** and **Port Number 1001** and click **OK**.
    
    ![Add your Preston subject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1224732a-e217-49f3-80f4-6fd03ba0139b/ccs-preston1.png)
4.  Select your Preston subject from the list and set the **Incoming Data Mode** dropdown to **Calibrated Data**.
    
    ![Select Calibrated Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b239f2b-0619-4074-acf3-f9ba4b45cf99/ccs-preston2.png)
5.  Select the Preston MDR device with the green circle. Open the **View Options** dropdown and change the setting to **Show Frame Data**. This will display live link data.
    
    ![View Options Show Frame Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e932dce1-754a-473f-84ae-ae44e325774f/ccs-preston2a.png)
6.  Change the focus and iris on the Preston hand unit to see the values for Aperture and Focus distance change and verify that these values match the values on the camera.
    
7.  Select your **CineCamera Actor** in the **World Outliner** window and go to the **Details** panel. Select your **Live Link Controller** component and scroll down to the **Live Link** section. Click the **Subject Representation** dropdown and select your Preston subject.
    
    ![Select your Preston subject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3810319c-a61f-402d-a5a5-6d596c62a43b/ccs-preston3.png)
8.  Scroll down to the **Camera Calibration** section and click the **Lens File** dropdown. Select the Lens File for your camera.
    
    ![Select your Preston subject](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ee17932-bcbf-4cdc-b189-2322ad18792b/ccs-preston4.png)
9.  Change the **Focus Method** setting from **Manual** to **Disabled**. This stops the focus changing on the CG Cinema camera as focus is being controlled by the physical camera by the value manually input using the Live Link Virtual Subject.
    
    ![Change Focus Method from Manual to Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7e120fb-b95d-4151-8d6b-ad71d738c116/ccs-preston5.png)

#### Results

In this guide you set up and connected a Preston MDR using Live Link to stream Focus Iris and Zoom to the Lens File connected to the Cine camera in UE.