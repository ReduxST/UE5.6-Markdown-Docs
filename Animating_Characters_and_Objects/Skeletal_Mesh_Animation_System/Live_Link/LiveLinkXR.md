# LiveLinkXR

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/livelinkxr-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/livelinkxr-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:03

---

**Live Link** provides a common interface for streaming and processing animation data from external sources into Unreal Engine (UE). It is designed to be extensible through Unreal Plugins, allowing third parties to develop new features— with no need to make and maintain Engine changes.

**LiveLinkXR** extends this functionality to be used with XR devices. By using the LiveLinkXR plugin, you can add XR sources such as Vive Trackers and HMDs for use with the Live Link tool.

LiveLinkXR currently only supports OpenXR. Currently the SteamVR platform supports headless rendering via OpenXR (running VR without invoking a render). To use Vive Trackers you must have SteamVR running and set it as your open XR runtime:

![The SteamVR Settings window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9e71951-cd8a-4b8f-9d83-ccec68703541/llxr_steamvrsettings.png)

This article walks you through setting up and configuring the LiveLinkXR plugin, adjusting the tools various settings, and provides potential troubleshooting and workaround steps.

## Enabling LiveLinkXR

1.  Click the **Edit** tab to expand., Under the **Configuration** heading, click **Plugins.**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7673de1e-ed0a-497e-9c0d-72d2e6e0e3b0/llxr_windowsplugin.png)
2.  Use the search box to find the **LiveLinkXR** plugin, then click **Enabled.**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70b22352-fce7-4eee-8546-e114b82764fa/llxr_locatellxrplugin.png)
3.  Click **Yes** in the box that appears.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b73d5dbe-9b2c-47b8-9aa9-01eb435a4395/llxr_betaoptin.png)
4.  Use the searchbox to find the Vivetracker plugin, then click **Enabled**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b93a98cb-a089-42df-b567-3e5661ae5939/llxr_vivetrackerplugin.png)
5.  Launch the **Live Link** tool by expanding the **Window** tab and clicking **Live Link.**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0c21cfb-9462-45b3-be1a-25adb246460b/llxr_openlivelink.png)
6.  Close and restart the engine with the following commandline parameter `-xrtrackingonly`
    
    Example: `D:\Program Files\UE_5.2\Engine\Binaries\Win64\UnrealEditor.exe -xrtrackingonly`
    
    If you do not use this command line parameter, your trackers, controllers, and headset will only be available while you are in VR preview mode or VR Editor mode.
    
7.  Expand the **LiveLinkXR Source** option to view the various settings associated with it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1885c6c-6584-434f-9ec2-14b567994b23/llxr_livelinkxrsourcesettings.png)

### Source Settings

The LiveLinkXR Source settings allow you to adjust data sources and adjust the local update rate.

| **Setting Name** | **Purpose** |
| --- | --- |
| **Track Trackers** | Track all Vive Trackers within OpenXR. |
| **Track Controllers** | Track all controllers. |
| **Track HMDs** | Track all HMDs. |
| **Local Update Rate in Hz** | Update rate (in Hz) at which to read the tracking data for each device. |

## Adding a LiveLinkXR Source

Although the process below was drafted using a Vive HMD with trackers, you should be able to use Live Link XR with any VR device that is supported by SteamVR.

SteamVR must be running to add a new LiveLinkXR source. Consult the [SteamVR Troubleshooting page](https://support.steampowered.com/kb_article.php?ref=8566-SDZC-9326) for help setting up SteamVR.

Once the LiveLinkXR plugin is enabled and you have adjusted the settings to match your needs, you will be able to add a XR source.

1.  Launch the **Live Link** tool, expand the **Source** window, and under **LiveLinkXR Source** click **Add.**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cdca0257-7618-4c5a-b088-9bc790255f54/llxr_livelinkxrsourcesettings.png)
2.  If you have configured everything correctly, after clicking **Add** you should see items added to the tables in the Live Link tool. These items should correspond to the **Data Sources** you have selected under the **Data Source** settings.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a379db95-abec-443c-862b-d4b33b2eba3e/llxr_livelinkxrnewsource.png)

If you want to use more than one Tracker Puck then you must set the role for each puck in SteamVR using the SteamVR Vive Tracker settings window: ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11e5580f-0903-4fcd-bce9-12be5ef48b0c/llxr_vivetrackerssettings.png) 

## Associating VR Sources with Blueprints and Meshes

After you enable the LiveLinkXR plugin, your project will gain access to LiveLinkXR Blueprints and Meshes. These valuable premade items can help you get started. This section will walk you through locating and using those items.

1.  Navigate to the **Content Browser,** expand the **View Options** menu, and select **Show Engine Content** and **Show Plugin Content.**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c9a31fa-1880-4e8f-b742-34724087effa/llxr_selectandviewoptions.png)
2.  You should immediately see new items appear within the **Content Browser** navigation window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/015c1ee2-7911-4067-b545-55b81b06a082/llxr_newcontent.png)
3.  Within the **Content Browser,** locate the **LiveLinkXR Content** folder and open the **Blueprints** folder under it.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47c29c4e-fdb8-4fd6-9bb6-bcf777d96ab5/llxr_livelinkxrblueprints.png)
4.  Drag the **BP\_LiveLinkXR\_DataHandler** into your scene.
    
    You can verify the tracking data you're receiving with the Toggle Debug Vis option. Do this by using the **Toggle Debug Vis** debugging tool.
    
    1\. After you have set up sources in **Live Link** and have dragged the **BP\_LiveLinkXR\_DataHandler** into your scene, select the handler from the **World Outlier** and navigate to the **Details** panel. 1. Expand the **Default** category and click the **Toggle Debug Vis** button.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59e0aa25-f182-4d99-a290-5b096e805c2b/llxr_datahandlertoggledebugvis.png)
    
    1\. A **BP\_LiveLinkXR\_DebugVis** debug visualization should appear in your level for each **Live Link Source** that you have set up. 1. These items should then move around based on their real-world movements.
    
5.  Select **BP\_LiveLinkXR\_DataHandler** from the **World Outliner** and navigate to the **Details** panel.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f83cbaec-ca3a-48a8-a1b9-7aeb4d99461e/llxr_datahandlerdetails.png)
6.  To add a new entry, expand the **Default** section under **Details,** and click the **Add (+)** button next to **Subject Name to Attached Actor** .
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70119eb0-cd92-4857-aae4-08fc99badbd0/llxr_datahandleraddattachedactor.png)
7.  In the textbox next to the new element, enter the **Subject Name** from the **Live Link** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/012189e7-edc0-4714-b603-e73079e90cb8/llxr_addsubjectnametodetails.png)
8.  Repeat this process as needed for all sources that you want to track.
9.  Use the **dropdown menu** next to your element to map the **tracking data** to the **Object** or **Actor** in the scene.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/623e28a0-8b60-4b1c-b55c-621f0b7b3d09/llxr_attachtrackingtotracker.png)

### Calibration

You can use the **Calibrate** button next to **Toggle Debug Vis** to set a new tracking origin relative to an arbitrary actor in the world. When you click it, the transform from the LiveLink Subject **Calibration Subject Name** is used to calculate a new world origin transform relative to the transform of the **Calibration Target Actor**.

1.  To take advantage of the Calibrate feature, first select **BP\_LiveLinkXR\_DataHandler** from the **World Outliner**. In the **Details** panel, select an actor in your level from the dropdown next to **Calibration Target Actor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52b648f0-9ecf-4205-88d5-a8baab0b641e/llxr_caliratepickactor.png)
2.  After selecting the target actor, enter the **Calibration Subject Name** in the box provided. This should match one of the LiveLink Subject names being tracked.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86db77e0-4961-4783-8c76-6724fe665ce0/llxr_calirateentersubject.png)
3.  After adjusting the settings, click the **Calibrate** button next to **Toggle Debug Vis**.
4.  Notice that the relative tracking origin of the devices is now relative to your new calibration.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/812218e7-2d08-4134-b0da-4144815bf1a3/llxr_datahandlerpostcalibration_raw.png)

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c4606d0-c492-423b-a6b0-3039f6ae88e9/llxr_datahandlerprecalibration_raw.png)

On the left is the location information for the BP\_LiveLinkXR\_DataHandler actor when initially dragged into the level. On the right is the location information after calibration relative to another actor in the level.

## Using Vive Trackers without an HMD

By default, you cannot use the Vive Trackers without an HMD. This section outlines a potential workaround that should allow you to use Trackers without an HMD within UE.

This process is a potential workaround that is unsupported by Valve, HTC, or Epic. It has the potential to stop working unexpectedly or cause unexpected issues with SteamVR. We recommend that you only attempt this workaround if you are an expert with SteamVR troubleshooting.

1.  First, fully shut down Steam and SteamVR.
    
    Ensure this by checking the Task Manager for any lingering Steam processes after closing the main program.
    
2.  Locate the following file on your computer: `<Steam Install Directory> /steamapps/common/SteamVR/drivers/null/resources/settings/default.vrsettings`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53fc4953-4888-450d-a40e-6e30b92177f1/llxr_workaroundsteamvrsettings_raw.png)
3.  Copy the file and add "\_BACKUP" to the end of the file extension.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ad6831e-f67d-4c73-a037-b82056efc2bc/llxr_workaroundsteamvrsettingsbackup.png)
4.  There are a few ways to back up the files outlined in this process. Copying the original and changing the file extension is the method shown below.
    
5.  Open the original `default.vrsettings` file in a text editor.
    
6.  In the `driver_null` object, change the `enable` property value from `false` to `true`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8c49eaf-ea38-453e-b8ca-64ca16928612/llxr_workaroundsteamvrsettingsnullenable_raw.png)
    
    If using nDisplay, set `windowWidth`, `windowHeight`, `renderWidth`, and `renderHeight` to **0** (zero). This will help you to avoid the un-minimizable VR Composer window in the middle of the screen.
    
7.  Save and close.
8.  Locate the following file: `<Steam Install Directory>/steamapps/common/SteamVR/resources/settings/default.vrsettings`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aeb598e2-9894-4152-8721-7b65d88f915e/llxr_workaroundsteamvrsettingssecondfile.png)
    
    The file names are similar, but they are located in different folders.
    
9.  Create a backup of the `default.vrsettings` file.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72035122-b4ce-4b96-a38e-e9160387dcb5/llxr_workaroundsteamvrsettingssecondbackup.png)
10.  Under the `steamvr` heading, change the `requireHmd` setting to `false`.
11.  Under the `steamvr` heading, change the `forcedDriver` setting to `"null"`.
12.  Under the `steamvr` heading, change the `activateMultipleDrivers` setting to `true`.
13.  Once you have updated the correct settings, the file should look something like this:
    
    ```
         `"steamvr": {      "requireHmd": false,      "forcedDriver": "null",      "forcedHmd": "",      "displayDebug": false,      "debugProcessPipe": "",      "enableDistortion": true,      "displayDebugX": 0,      "displayDebugY": 0,      "allowDisplayLockedMode": false,      "sendSystemButtonToAllApps": false,      "loglevel": 3,      "ipd": 0.063,      "ipdOffset": 0.0,      "background": "",      "backgroundUseDomeProjection": false,      "backgroundCameraHeight": 1.6,      "backgroundDomeRadius": 0.0,      "environment": "",      "hdcp14legacyCompatibility": false,      "gridColor": "",      "playAreaColor": "",      "showStage": false,      "activateMultipleDrivers": true,`
    Copy full snippet
    ```
    "steamvr": { "requireHmd": false, "forcedDriver": "null", "forcedHmd": "", "displayDebug": false, "debugProcessPipe": "", "enableDistortion": true, "displayDebugX": 0, "displayDebugY": 0, "allowDisplayLockedMode": false, "sendSystemButtonToAllApps": false, "loglevel": 3, "ipd": 0.063, "ipdOffset": 0.0, "background": "", "backgroundUseDomeProjection": false, "backgroundCameraHeight": 1.6, "backgroundDomeRadius": 0.0, "environment": "", "hdcp14legacyCompatibility": false, "gridColor": "", "playAreaColor": "", "showStage": false, "activateMultipleDrivers": true,
14.  Save and close the `default.vrsettings` file.
15.  Launch **Steam** and **SteamVR.**
16.  Because you have altered the SteamVR settings, you may need to run the **Room Calibration** setup again.
17.  After completing Room Calibration, relaunch **SteamVR** and you should be able to track devices without the need for an HMD.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5fd68de-e4f6-4545-918e-1ec35e8b25c2/llxr_workaroundsteamvrfinal_raw.png)
18.  When you are ready to use the HMD again, close **SteamVR**, restore the **edited files from the backups**, and relaunch **SteamVR.**

## Troubleshooting

### SteamVR Issues

If your HMD, Controllers, or Trackers are not appearing in SteamVR, then they will not appear in UE. If you are having issues setting up your VR devices, it is recommended that you review the [Steam VR Troubleshooting](https://support.steampowered.com/kb_article.php?ref=8566-SDZC-9326) guide for assistance.