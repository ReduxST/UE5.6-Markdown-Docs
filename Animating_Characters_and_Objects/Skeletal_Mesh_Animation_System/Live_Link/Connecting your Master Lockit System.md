# Connecting your Master Lockit System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/connecting-your-master-lockit-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/connecting-your-master-lockit-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:59

---

## Steps

In this section you will connect a Smart lens using an Ambient Master Lockit Plus device using Live Link.

The Smart lens on the production camera will be connected to the Master Lockit Plus and the Master Lockit Plus will connect to the Unreal Engine workstation network by Ethernet.

1.  Click **Settings > Plugins** to open the **Plugins Menu**. Click the **Virtual Production** category and search for the **LiveLinkMasterLockit** plugin.
    
    ![Open the Plugins Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0bddf03-b31d-4d47-9a7a-703abd7bb4f9/cc-pluginmenu1.png)
2.  Enable the plugin and click **Yes** on the message window. Click **Restart Now** to restart the editor.
    
    ![Add a Master Lockit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be892be1-e9ae-4681-a5e7-45bc5c64277b/ccs-lockit0.png) ![Click Restart Now](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c6d4830-1b93-48f7-8433-d3e70870c43a/ccs-restarteditor.png)
3.  Once the editor finishes loading, go to the **Live Link** window and click **\+ Source > MasterLockit**. Enter the **Master Lockit's IP Address** and click **OK**.
    
    ![Add a Master Lockit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34fef0f1-597e-4b38-9003-021e2d4e0c49/ccs-lockit1.png)
4.  Select the **Master Lockit Device** in the window and click **View Options**, then select **Show Frame Data**. Confirm the values are updating correctly in the **Live Link** section.
    
    ![Show Frame Data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfe4418c-beea-4ea6-8c6f-7119a617d895/ccs-lockit2.png)
5.  Select the **CineCamera Actor** in the **World Outliner** window and go to the **Details** panel. Select the **Live Link Controller** component and scroll down to the **Live Link** section. Click the **Subject Representation** dropdown and select your **Master Lockit Device**.
    
    ![Add a Master Lockit Device to the Subject Representation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7032d152-7706-427a-b0bf-dac5c36021d2/ccs-lockit3.png)
6.  Select the **Camera Component** and scroll down to the **Focus Settings**. Verify that changing the focus and aperture on the physical camera updates those same settings in the **CineCamera Actor**.
    
7.  Change the **Focus Method** setting from **Manual** to **Disabled**. This stops the focus changing on the CG Cinema Camera as focus is being controlled by the physical camera
    
    ![Change Focus Method from Manual to Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b45d1128-5a5a-441e-a512-31038f41c56c/ccs-preston5.png)

#### Results

In this guide you connected your Master Lockit Device by using Live Link and streamed Focus Iris and Zoom from a Smart Lens on the Production camera.