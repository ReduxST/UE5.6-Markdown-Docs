# In-Camera VFX Production Test

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine)  
**Processed:** 2025-06-14 16:30:45

---

The In-Camera VFX Production Test is a Virtual Production sample that uses Unreal Engine and an LED Volume to feature traveling vehicle shots, multi-camera setups, and multi-user setup for making quick changes between takes. This sample was created in collaboration with filmmakers' collective [Bullitt](https://bullittbranded.com/). The team produced final pixels in-camera over four days on [Nant Studios](https://www.nantstudios.com/)' LED stage in Los Angeles.

The short produced from the project.

Exploring and modifying the sample will help you learn how you can:

-   Structure your Virtual Production project so multiple artists can collaborate simultaneously on scenes during production.
    
-   Use GPU Lightmass with Multi-User to bake lighting on one computer and share to all computers in the session for faster lighting changes.
    
-   Render the inner frustum using mGPU on a multi-screen nDisplay cluster.
    
-   Apply color correction and OCIO profiles to your nDisplay renders to achieve the desired look for each scene.
    
-   Build the UI of your Remote Control Web Application to meet your production's needs and make quick changes on set from a tablet.
    
-   Apply cvars to improve performance in the project.
    

This guide covers how the production team used Unreal Engine's features in the project to make the final result. Use this project as an example for designing your production. For learning the basics of in-camera VFX, refer to the [In-Camera VFX Quick Start](/documentation/en-us/unreal-engine/in-camera-vfx-quick-start-for-unreal-engine). For behind the scenes footage of this production, refer to the [Unreal Engine Spotlight](https://www.unrealengine.com/en-US/spotlights/taking-unreal-engine-s-latest-in-camera-vfx-toolset-for-a-spin).

## Stage Setup and Hardware

Click image to expand.

Four nDisplay nodes were used to render the following volume, with 2 LED panels assigned to each node:

-   **Walls**: Total resolution of **15312 x 2112** over **5** LED panels.
    
-   **Ceiling**: Total resolution of **4160 x 5280** over **3** LED panels.
    

This real production sample is both CPU-intensive and GPU-intensive so it can render on this large LED volume at a camera-ready resolution. The diagram below shows every device contributing to the production and the connections between devices on stage. To learn about the roles of each device in the shoot, refer to [In-Camera VFX Overview](/documentation/en-us/unreal-engine/in-camera-vfx-overview-in-unreal-engine) for details. To learn what hardware is recommended for an in-camera VFX shoot, refer to [In-Camera VFX Recommended Hardware](/documentation/en-us/unreal-engine/recommended-hardware-for-in-camera-vfx-in-unreal-engine).

Diagram showing what devices were used and how they communicated with each other on stage. Click image to expand.

## Getting Started

In addition to the [nDisplay Config](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine) that represents the topology of the real stage used in production, a simple nDisplay Config is included in the project so you can view the scenes on a single computer without an LED volume. This section shows how to use the simple nDisplay Config to render the scene and make changes in a multi-user session on a single computer.

Follow these steps to launch an instance of the Unreal Editor and another instance of Unreal Engine with the nDisplay renderer in a multi-user session on your computer.

1.  Access the [In-Camera VFX Production Test sample](https://fab.com/s/c9a039f679f8) from **Fab** and click **Add to My Library** for the project file to show in the **Epic Games Launcher**.
    
2.  From the **Epic Games Launcher**, go to **Unreal Engine > Library > Fab Library** to access the project.
    
    Sample projects only appear in **Fab Library** when you install the compatible engine version.
    
3.  Click **Create Project** and follow the on-screen instructions to download the sample and start a new project.
    1.  To learn more about accessing sample content and the Fab plugin for Unreal Engine, see [Samples and Tutorials](/documentation/en-us/unreal-engine/samples-and-tutorials-for-unreal-engine).
4.  Go to the Unreal Engine folder on your computer and run Engine\\Binaries\\Win64\\SwitchboardListener.exe to launch **SwitchboardListener** on your computer. The listener will minimize its window automatically on start to avoid issues with nDisplay devices. You can find the application in your OS's taskbar.
    
    The following is an example of a full path: `C:\Program Files\Epic Games\UE_4.27\Engine\Binaries\Win64\SwitchboardListener.exe`
    
5.  In the Unreal Engine folder, run Engine\\Plugins\\VirtualProduction\\Switchboard\\Source\\Switchboard\\Switchboard.bat to launch **Switchboard** on your computer. If this is your first time running Switchboard, it will install any required dependencies before opening the application window.
    
    The following is an example of a full path: `C:\Program Files\Epic Games\UE_4.27\Engine\Plugins\VirtualProduction\Switchboard\Source\Switchboard\Switchboard.bat`
    
6.  Create a new **Switchboard Configuration**.
    
    -   If this is your first time running Switchboard, the **Add New Switchboard Configuration** window appears when Switchboard launches.
        
    -   If you have run Switchboard before, click **Configs > New Config** in the top left corner of the window to open the **Add New Switchboard Configuration** window.
        
        ![Adding a new Switchboard configuration](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd1315f0-5c5c-4608-a354-e24b2f0bb456/switchboard-configs.png)
7.  In the **Add New Switchboard Configuration** window:
    
    1.  Set **Config Path** to the name and location where you want to store your Switchboard Configuration file.
        
    2.  Set **uProject** to the location of the In-Camera VFX Production Test sample project file, `TheOrigin.uproject`.
        
    3.  Make sure **Engine Dir** is pointing to the **Engine** folder for your Unreal Engine.
        
    4.  Click **Ok** to create the Switchboard Configuration.
        
        ![New Switchboard configuration paths](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d6ceb7b-1680-49ee-8f9e-82d764800f2f/new-switchboard-config.png)
8.  Set **Level** to **CaveEntrance\_NantStudiosSimple**.
    
    ![Setting the Level in Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/155e13f4-3119-43c0-ba38-1768c6d19b3e/switchboard-set-level.png)
9.  Add an nDisplay device to Switchboard:
    
    1.  Click **Add Device** and select **nDisplay** from the dropdown.
        
        ![Adding an nDisplay device](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6758bb2-3931-42ef-adf9-40ae8676cd30/add-ndisplay-device-1.png)
    2.  In the **Add nDisplay Device window**, click **Browse** and navigate to Content\\TheOrigin\\Content\\Stages\\NantStudiosSimple\\Config\\NDC\_NantStudiosSimple.uasset in the sample project's folder.
        
        ![Browsing to the nDisplay device .uasset file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/697a2f80-131b-4e37-9063-18139b8f8122/add-ndisplay-device-2.png)
    3.  Click **OK** to see one nDisplay device added to Switchboard.
        
        ![The nDisplay device added to Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a40ab7bf-bfaf-49c3-8077-b72a600d55a4/ndisplay-added-switchboard.png)
10.  Add an Unreal device to Switchboard:
    
    1.  Click **Add Device** again and select **Unreal** from the dropdown.
        
        ![Adding an Unreal device](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c8daa1d-1bab-412b-a209-0e832da8a46b/add-unreal-device.png)
    2.  In the **Add Unreal Device** window, set the **IP Address** to the local computer: **127.0.0.1**.
        
        ![Setting the Unreal device local IP address](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f10c4794-1c14-4c98-9605-e4c717ccb2dc/set-ip-address.png)
    3.  Click **OK** and see one Unreal device added to Switchboard.
        
        ![The Unreal device added to Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d2a8a72-95df-4196-9b2c-ad17f0efbddf/unreal-added-switchboard.png)
11.  Click the **Connect to Listener** button for the nDisplay **Render\_2** device to connect to SwitchboardListener.
    
    ![Connect to Listener button for nDisplay device in Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f12bd0a-bbe2-4b9a-870f-449d8bcd80c2/connect-to-listener.png)
12.  Click the **Start Unreal** button for the nDisplay **Render\_2** device to launch Unreal with the nDisplay renderer in a multi-user session.
    
    ![Start Unreal button for nDisplay device in Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee6ae664-3134-474e-a5e9-03577b44f173/start-unreal.png)
13.  All windows automatically minimize and the full screen nDisplay render appears. The view might be dark but you will change the view in a later step.
    
14.  Open the minimized Switchboard window, and click the **Connect to listener** button for the Unreal device to connect to SwitchboardListener.
    
    ![Connect to Listener button for Unreal device in Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83a4cb8f-ea3e-4e6a-991e-38b7f89b9131/connect-unreal-device.png)
15.  Click the **Start Unreal** button for the Unreal device to launch an instance of the Unreal Editor in the Multi-User Session.
    
    ![Start Unreal button for Unreal device in Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22725761-6cd1-4ae1-92b6-3666d899a147/start-unreal-ud.png)
16.  In the Editor, on the toolbar click **Open Level Snapshots Editor**.
    
    ![Open the Level Snapshots editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9b2d1af-8d56-4e0d-a667-7af8058c0f37/open-level-snapshots.png)
17.  In the Level Snapshots Editor, double-click the **CaveEntrance\_NantStudiosSimple\_SetupA** Level Snapshot and click **Restore Level Snapshot**.
    
    ![Restore the Setup A Level Snapshot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5862b19d-61f5-4537-b423-1553db0a9ad5/restore-level-snapshot.png)
18.  In the Unreal Editor's **World Outliner panel**, select the nDisplay Root Actor **NDC\_NantStudios\_Simple** to see its updated position.
    
    ![Before Level Snapshot restore](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3930aa68-48fa-4bc6-8ca1-e3671ab56e18/ndisplay-root-slider-1.png)
    
    ![After Level Snapshot restore](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/420ea6ce-95d1-49c5-8ad3-27472af1e209/ndisplay-root-slider-2.png)
    
19.  The nDisplay view updates with the changes you make in the Unreal Editor instance.
    
    ![nDisplay view updates](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dd3cf0e-0920-487c-a494-05325f98d0dc/view-updates.png)
20.  Select **InnerCamera\_A** under the nDisplay Root Actor and move it around the scene to see the inner frustum move in the nDisplay view.
    
    ![Moving InnerCamera A around the scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d04d63e-acfc-4179-9c97-52d20c79af02/moving_inner_frustum_updated_look_smaller.gif)

These steps showed how to run the project on a single computer. You can use similar steps and modify the nDisplay Config that represents the real stage to test on your own LED volume.

## mGPU and Multi-Screen Cluster

![The In-Camera VFX Production Test shoot in progress](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47245502-0900-4237-968a-fc74be3d74b1/shoot-in-progress.png)

The production leveraged multi-GPU to improve performance during the shoot. Rather than relying on a single GPU to render all viewports, a second GPU was dedicated to rendering only what appeared in-camera, to allow for the highest fidelity where it counted most. Refer to the [nDisplay Overview](/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine#multi-gpu-support) to learn how to use mGPU in a project.

Unreal Engine includes the **Stage Monitor** tool so you can receive reports associated with specific events from all the nDisplay cluster nodes in one application. You can have the tool enter a critical state while filming so you can easily notice events that could affect your shot. For more on how to use this tool, refer to [Stage Monitor](/documentation/en-us/unreal-engine/stage-monitor-with-unreal-engine).

## Remote Control

With [Remote Control](/documentation/en-us/unreal-engine/remote-control-for-unreal-engine), the production team, while on set, was able to control the displays and virtual environment dynamically from a web application running on a tablet. Exposed controls from the project included lighting, color grading of the displays, and modifying the position and rotation of the stage in the virtual environment.

![Using Remote Control to control the stage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/080e8457-34c6-45df-ad58-fc9b1f2693a5/remote-control-stage.png)

### Using Remote Control

In the [Getting Started](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#gettingstarted) section, you used an Unreal Editor instance to make changes to the scene and see the updates immediately in the nDisplay render. This section shows how to do the same thing using the Remote Control Web Application designed for the project.

Follow these steps to view the Remote Control Web Application designed for this project, and move the nDisplay Root Actor remotely:

1.  In the **Content Browser**, go to **TheOrigin > Content > Tools > RemoteControl** and double-click **RCP\_NantStudios** to open the Remote Control Preset in the **Remote Control Panel**.
    
    ![Open the Remote Control Preset in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb8dde71-c8a9-4cf3-b2d5-bd857c6037d7/rcp-production-test.png)
2.  The Remote Control Panel shows all the exposed parameters in the [Remote Control Preset](/documentation/en-us/unreal-engine/remote-control-presets-and-web-application-for-unreal-engine). Launch the web application by clicking the angled arrow icon in the top right of the panel.
    
    ![Launch the web application from the Remote Control panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/809f0d32-70ef-480f-8661-a3a742d6d1f0/rcp-prod-test-launch.png)
    
    If there is no option to launch the web application in the Remote Control Panel, ensure the web application was built properly. You may need to modify the Remote Control section of the Project Settings to build it on your computer. Scan the Output Log in the Unreal Editor for errors.
    
3.  You might need to rebind properties to work with the level and stage you have open.
    
    ![Rebinding properties in the Remote Control panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8f51d3f-643d-45dc-924b-d1d032a26508/rebind-properties.png)
4.  Switch to the **Stage** tab of the Remote Control Web Application.
    
5.  Move the joysticks to change the location of the nDisplay Root Actor.
    
    ![Moving the joystick to change the nDisplay Root Actor location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7eb4aa15-2fd4-4608-b5f9-59b6a4df926a/remotecontrol_movestage_smaller.gif)

### Designing the Web Application

The [Remote Control Web Interface](/documentation/en-us/unreal-engine/remote-control-presets-and-web-application-for-unreal-engine) is a plugin that provides a companion web application to Remote Control. The web application includes a UI builder so you can create and customize your own web application without any code.

To switch to the UI builder of the Remote Control Web Application, toggle the **Control** button to **Design**, and modify the UI for the project. Save the **Remote Control Preset Asset** to save changes to the Remote Control Web Application's UI design.

![Remote Control Design mode to modify UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3590176a-8d5d-46c2-86de-2b3d44abffd7/rcp-ui-design.png)

The following list describes the controls exposed in each tab of the Remote Control Web Application designed for this production.

-   **Stage**: Combines the controls for the Stage Position and Rotation within the Level.
    
    ![Stage controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16afc04c-2546-464c-9c9a-8c0e4471992b/rcp-stage-location.png)
-   **Viewport Settings**: Combines the controls for the global Viewport Screen Percentage and per-viewport Screen Percentage parameters.
    
    ![Viewport settings controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40718c1d-aeb6-4134-9a77-2921208d2cdb/rcp-viewport-controls.png)
-   **Color Correction**: Combines the controls for global Color Correction and per-viewport Color Correction parameters.
    
    ![Color correction controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf9ef6d4-2238-4354-b970-d9a4b83a2d71/rcp-color-correction.png)
-   **LightCard**: Combines the controls for Light Cards.
    
    ![Light cards controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca07210b-026a-4695-9513-c71c1c8f71a4/rcp-lightcards.png)
-   **Snapshot**: Shows all Level Snapshots in the project, and combines controls for taking and applying Level Snapshots. See [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine) for more details.
    
    ![Level Snapshot controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdbd2fef-76ee-45bb-90b6-f41a9c0220e5/rcp-level-snapshot.png)

## Color Grading and OCIO

In order to preserve accurate and consistent color across the pipeline, the art and stage teams leveraged [OpenColorIO (OCIO)](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) to standardize color space conversions. These color space conversions accounted for display differences between monitors, LED panels, and production cameras.

A sample OCIO configuration and its look- up tables (LUTs) are included in the OCIO Plugin. This project has an example OCIO Configuration Asset that references this OCIO configuration and is assigned to both nDisplay Config Assets. You can find the OCIO Configuration Asset in **TheOrigin/Content/OCIO**.

To learn more about creating OCIO configurations and color space conversions for your displays, see [In-Camera VFX Camera Calibration](/documentation/en-us/unreal-engine/camera-color-calibration-for-in-camera-vfx-in-unreal-engine).

Follow these steps to use your own OCIO configuration in the project:

1.  In the **Content Browser**, right-click and select **Miscellaneous > OpenColorIOConfiguration** to create a new **OpenColorIO Configuration Asset**.
    
    ![Add an OCIO configuration asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ebc0e5d-b638-4674-8999-12ef240a73e8/add-ocio-asset.png)
2.  Double-click the new asset to open its editor.
    
3.  In the Asset Editor, under the **Config** section, set the **Configuration File** field to the path of your OCIO configuration file on disk.
    
    ![Set the path to the OCIO configuration file](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da25dcca-f2c6-448c-98ff-2f4b39443592/ocio-config-path.png)
4.  Click **Reload and Rebuild** to load the OCIO configuration.
    
5.  When the OCIO configuration is successfully loaded, expand the **Color Space** section.
    
6.  Add the Source and Destination color spaces you wish to use. The options available are determined by the OCIO config you specified.
    
    ![Add source and destination color spaces](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00429ca9-6cb4-4b9e-b4ed-aa541c5227c0/ocio-color-spaces.png)
7.  To apply this configuration to your nDisplay viewport, open the level containing your **nDisplay Config Asset**, and search for **OCIO** in the **Details Panel** of the actor. Ensure that you have **Enable Viewport OCIO** set to true.
    
8.  Expand **All Viewports Color Configuration:**
    
    1.  Specify the Config asset you want to use.
        
    2.  Set the Source and Destination color spaces.
        
        ![Set the Source and Destination color spaces](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37d37e6c-46a6-4036-958b-e43a5ab679c3/ocio-set-source-dest.png)

These steps demonstrate how to add your own OCIO configuration to the project. You can also set OCIO configurations per viewport and separately on the inner frustum. For more information, refer to [Color Management in nDisplay](/documentation/en-us/unreal-engine/color-management-in-ndisplay-in-unreal-engine).

## GPU Lightmass and Multi-User

The production team used the new [GPU Lightmass](/documentation/en-us/unreal-engine/gpu-lightmass-global-illumination-in-unreal-engine) feature to bake the scenes' lighting and thus minimize how long the production had to wait for lighting changes in their multi-GPU and multi-user environment. Light baking occurred on a single multi-GPU workstation and then was distributed over the network through the multi-user session. This meant that the scene could be baked quickly and reloaded on the LED walls without needing to close and relaunch the cluster.

Follow these steps to use GPU Lightmass to bake lighting for the scene:

1.  In the **Toolbar**, click the arrow next to **Build** and select **GPU Lightmass** from the dropdown.
    
    ![Select GPU Lightmass in the Build dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99c2ba64-a539-47a3-9202-7e126dd353d8/build-gpu-lightmass.png)
2.  In the **GPU Lightmass** window, click **Build Lighting** to begin your bake.
    
    ![Build Lighting using GPU Lightmass](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4369d1e4-57fa-4b0b-8d05-b5f1a1002ef4/build-lighting.png)
3.  When the lighting finishes building, in the main menu choose **File > Save All** to transmit the changes to the other computers in the multi-user session.
    
    ![Save All to transmit the baked lighting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8cb307bb-c275-4925-8e51-8122efc3be4c/lightmass-save-all.png)

Instead of sharing all changes with the other computers in the multi-user session, you can also choose what changes to transmit.

1.  In the main menu, choose **File > Choose Files to Save…**
    
    ![Choose files to save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9ef9dfe-fef4-4c99-95a6-11b19ee3279a/lightmass-choose-files.png)
2.  Select only the levels and build data you want to save and transfer.
    
    ![Select baked lighting files to save and transmit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19af9c09-4e2a-4a7a-a3d5-2557f933f34a/save-selected.png)
3.  Click **Save Selected** to transmit the changes to the other computers in the multi-user session.
    

For more on the settings you can change for your lightmass bakes, refer to [GPU Lightmass](/documentation/en-us/unreal-engine/gpu-lightmass-global-illumination-in-unreal-engine).

Transferring GPU Lightmass bakes through the multi-user session is an experimental feature. Scenes that produce large BuildData files may experience issues with the transfer. If this happens, you can:

1.  Check your updated levels and BuildData into source control.
2.  Through source control, sync the changes to your render nodes to distribute the updated lightmaps.

## Level Snapshots

The production team used [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine) to save configurations of the Actors in a Level for each scene. Once Level Snapshots were created, the team was able to restore the scene later to exactly how it was set up for a specific shot. Level Snapshots also track changes to the nDisplay Root Actor, so modifications to the inner frustum and color grading can be saved and applied to the nDisplay renders at any time.

The following sections describe how to use the filters and presets included in the project. To learn about creating your own filters and other features in the tool, refer to [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine).

### Filtering with Level Snapshots

Included in the project is an example **Blueprint Level Snapshot Filter** that lets you filter Actors in the Level Snapshot changes by their Class. You can find the filter **LSF\_FilterByClass** in **TheOrigin/Content/Tools/LevelSnapshotFilters**. This section shows how to use this filter in the project.

Diagram showing what devices were used and how they communicated with each other on stage. Click image to expand.

Follow these steps to filter Level Snapshot changes and apply them to your project:

1.  In Unreal Editor's **Content Browser**, go to **TheOrigin > Content > StageLevels > NantStudiosSimple > StageLevels** and double-click **CaveEntrance\_NantStudiosSimple** to open the Level.
    
2.  In the **Toolbar**, click the arrow next to the **Level Snapshots** button and select **Open Level Snapshots Editor** from the dropdown.
    
    ![Open Level Snapshot Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/836f3259-2281-4456-bfff-4e993e6489e7/open-lvl-snap-editor.png)
3.  There are two Level Snapshots already created for the Level CaveEntrance\_NantStudiosSimple. Double-click **CaveEntrance\_NantStudiosSimple\_SetupA** to see how the Actors saved in the Level Snapshot differ from the current state of the Level.
    
    ![The In-Camera VFX Production Test Level Snapshots](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ba655f2-8c00-40f1-a746-4a028885bdf2/prod-test-level-snapshots.png)
4.  Click **Filter Group**.
    
    ![The Setup A Level Snapshot selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a8d979c-f8fd-450a-b19d-7e875c63ca2c/prod-test-setupa-lvl-snap.png)
5.  Click **Add Filter** and in the dropdown choose **Blueprint Filters > LSF Filter by Class**.
    
    ![Add the LDF Filter by Class Blueprint filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/763fd64d-bc2f-46cf-92a5-661403c0d832/prod-test-setupa-add-filter.png)
6.  Click **LSF Filter by Class** in the Filter Group.
    
    ![Click the filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28e19177-1123-4991-8acb-8c1ba7bea3d7/prod-test-lsf-filter.png)
7.  In the **Default** section next to **Class**, click the dropdown and search for **Light Card**.
    
    ![Search for Light Card](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a44a364c-30d3-49fe-8b48-925c828ed1f9/prod-test-light-card-filter.png)
8.  Click the **Refresh Results** button to apply the filter changes.
    
    ![Refresh Results to apply filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d93bb17b-f893-4cfb-b850-7f54e3637ccb/refresh-results.png)
9.  Now, only changes to Light Card Actors are shown. To turn off the filter, right-click the filter and select **Ignore Filter**.
    
    ![Only changes to Light Card Actors shown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bfdd873-a925-4bb9-beab-13357b270f90/lvl-snap-only-light-card.png)
10.  Click **Refresh Results** and see the nDisplay Root Actor appear in the list again.
    
    ![Disabled filter means all Actors are shown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e985e7b-f538-41d6-9922-9e6fbf0f8669/lvl-snap-disable-filter.png)

### Using Presets with Level Snapshots

With Level Snapshot Presets, you can set up logic using Blueprint and C++ filters and save it as a preset. Later, you can load the preset to use this logic again. Included in the project is an example Level Snapshot Preset located in **TheOrigin/Content/Tools/LevelSnapshotPresets**.

This preset strings multiple instances of the **Filter by Class** Blueprint Filter together with the OR boolean so only Actors that match any of those Classes will appear. The Classes used in the preset are: LightCards, Stages, Cameras, SyncTestBall, ColorCorrectRegion, and PostProcessVolume.

Follow these steps to use the Level Snapshot Preset in the project.

1.  In the **Content Browser**, go to **TheOrigin > Content > StageLevels > NantStudiosSimple > StageLevels** and double-click **CaveEntrance\_NantStudiosSimple** to open the Level.
    
2.  In the **Toolbar**, click the arrow next to the **Level Snapshots** button and select **Open Level Snapshots Editor** from the dropdown.
    
    ![Open Level Snapshot Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c925488-8546-46bc-acf4-9df73b14d2b4/open-lvl-snap-editor.png)
3.  There are two Level Snapshots already created for the Level CaveEntrance\_NantStudiosSimple. Click **Load/Save Filter** and choose **ExampleStagePreset**.
    
    ![Load the Example Stage Preset filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60598f66-f3a5-4d63-85bb-23cea3786512/prod-test-preset-filter.png)
4.  Double-click **CaveEntrance\_NantStudiosSimple\_SetupA** to see how the Actors saved in the Level Snapshot differ from the current state of the Level.
    
    ![The Preset Filter loaded](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c33ea4e-375e-4d5c-9b58-9d581b27e8a4/lvl-snap-filter-loaded.png)
5.  When the Level Snapshot is opened, only the Actors that fit the filter loaded from the preset are shown.
    
    ![The Setup A Level Snapshot filtered by the Preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e5068765-57d9-4f15-a820-0c38e5c4f166/lvl-snap-setupa-filtered.png)

## Project Structure

The In-Camera VFX Production Test is a great example to see how to structure an Unreal Project for Virtual Production. The following folders define the overall structure for the project's content and separate it into relevant categories.

-   [Assets](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#assets)
    
-   [Envs](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#environments)
    
-   [OCIO](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#ocio)
    
-   [StageLevels](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#stagelevels)
    
-   [Stages](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#stages)
    
-   [Tools](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#tools)
    

### Assets

This folder typically contains all assets for creating Characters, Environments, and FX. Level Assets are not included here. The following list is how the assets were categorized for this sample project.

-   **Atlases**
    
-   **Decals**
    
-   **FX**
    
-   **IES**
    
-   **Landscape**
    
-   **Materials**
    
-   **MS\_Presets**
    
-   **Props**
    
-   **Rocks**
    
-   **Scatter**
    
-   **Sky**
    
-   **Textures**
    
-   **Vegetation**
    

### Environments

Three environments from the shoot are included in the project:

-   CaveEntrance
    
    ![The Cave Entrance environment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab691da8-3988-4eef-a2c9-a9a55104c2d2/prod-test-cave-entrance.png)
-   CavePath
    
    ![The Cave Path environment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd9ed653-b1d7-4167-b0c3-aa04256097d2/prod-test-cave-path.png)
-   SpaceJunkyard
    
    ![The Space Junkyard environment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/208d5a1e-03e0-4073-95fc-c547188ce469/prod-test-space-junkyard.png)

#### Environment Structure

Since source control only lets you exclusively check out binary assets, such as `.umap` files, each artist working on an environment at the same time must work in their own level. The solution to this is to divide an environment up into multiple [sublevels](/documentation/en-us/unreal-engine/managing-multiple-levels-in-unreal-engine) based on the type of Actors in each.

For example, a lighting artist would work in the lighting sublevel, and an FX artist in the FX sublevel. It is also common to have multiple GEO levels that divide the environment up into regions, each being worked on by a different artist. The number and types of sublevels used should be dependent on the needs of the production.

The following are the folders used for each environment in this project:

-   **LevelSnapshots**: Level Snapshot Assets associated with the Level.
    
-   **SubLevels**: In this project, each Level was separated into the Caustics, FX, Geo, and Lighting sublevels.
    
-   **Level Asset**: Level Assets follow a {LevelName}\_{Descriptor} structure. The \_P suffix is given to the Persistent Level, which acts as a container for the sublevels. Open this Level Asset to view the full environment composed of all the sublevels.
    

### OCIO

This folder contains the OpenColorIO Configuration Assets. There is one Asset for this project: ExampleOCIO. For more details on using OCIO in this project, refer to the [Color Grading and OCIO section](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine#colorgradingandocio) on this page.

![The Example OCIO asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4bca531-8d9f-4901-b4b7-010b4b6c7e7e/prod-test-ocio-asset.png)

### Stage Levels

The folder contains all the Level Assets that have both the environment and stage Actors. Open these assets when you want to render with nDisplay. The stage levels are categorized by the stage used in the Level Asset. This sample project uses the following structure to match the stages:

-   NantStudios
    
    -   CaveEntrance\_NantStudios
        
    -   CavePath\_NantStudios
        
    -   SpaceJunkyard\_NantStudios
        
-   NantStudiosSimple
    
    -   CaveEntrance\_NantStudiosSimple
        
    -   CavePath\_NantStudiosSimple
        
    -   SpaceJunkyard\_NantStudiosSimple
        

### Stages

This folder contains the nDisplay Configurations which describe the topology of the LED volumes. The production used one stage for all the shots: Nant Studios. A simpler version of the stage is provided as well so you can render the front walls on a single desktop.

Click image to expand.

#### NantStudios

-   **Config**: An nDisplay Config Asset for the stage that defines the topology of the LED volume and how to render on it.
    
    ![The NantStudios nDisplay Config asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08ef4e9f-b6e7-4059-b1ae-102d7b7cafee/nantstudios-config-asset.png)
-   **LEDMeshes**: Static Meshes and materials with the LED panel resolution used in the **nDisplay Config Asset**.
    
    ![NantStudios LED meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb03ccfb-722e-4db6-9ce9-e050c1e9602c/nantstudios-led-meshes.png)
-   **LiveLinkPresets**: These are previously created configurations for Live Link that are required to load LiveLink sources on the nDisplay nodes at launch. The default preset is specified in **Project Settings > Live Link > Default Live Link Preset.** They can also be used to quickly reload different sources in an editor environment.
    
-   **NantStudios\_Stage**: A Level Asset that contains only the Actors that represent the stage, such as the **nDisplay Root Actor**, **ICVFX Cameras**, and **Light Cards**.
    

#### Simple Nant Studios

-   **Config**: An nDisplay Config Asset for the stage that defines the topology of the LED volume and how to render on it. The topology looks the same as the Nant Studios configuration, but only two of the front walls are set up to render.
    
-   **NantStudiosSimple\_Stage**: A Level Asset that contains only the Actors that represent the stage, such as the **nDisplay Root Actor**, **ICVFX Cameras**, and **Light Cards**.
    

### Tools

This folder contains custom Blueprint controls, Level Snapshot Filters and Presets, and Remote Control Presets. The following list describes each tool.

-   **CaveMaterialControl**: A blueprint controller for various Material Parameter Collections used by objects in the scene. Contains controls for things such as caustic speed, light shaft intensity, and global color shifts for the rocks.
    
-   **HierarchicalInstanceConverter**
    
-   **HolePunch**: A spherical actor used to create a hole in the geometry of the cave. This was used on the day of the shoot to create an additional light shaft.
    
-   **InnerFrustumCamera**: A CineCameraActor with a LiveLinkComponent. This Blueprint simplifies the camera tracking by not requiring the user to manually add an instanced LiveLinkComponent to the scene actor.
    
-   **LevelSnapshotFilters**: Custom Blueprint Filters for Level Snapshots.
    
-   **LevelSnapshotPresets**: Presets of groups of filters for Level Snapshots.
    
-   **RemoteControl**: Remote Control Presets.
    
-   **SyncTestBall**: This tool creates a bouncing red ball used to test synchronization. Place the ball in the scene so that it appears on the seam between two walls. A visible tearing of the ball occurs at the seam if the synchronization is not functioning properly.
    

## Cvars

To improve performance while rendering with nDisplay on stage, the production team used the cvars in the table below to tweak settings. You can set cvars during an nDisplay session in Switchboard and have them applied to the cluster.

To set cvars in Switchboard:

1.  Open Switchboard.
    
2.  Under the **nDisplay Monitor** tab, in the **Console:** text box, enter the cvar and the desired value, if applicable.
    
3.  Click **Exec**.
    

![The nDisplay Monitor Console](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf6f8fb4-7680-4232-9901-f6cfabeaeff4/prod-test-console.png)

The following values are what were used for the In-Camera VFX Production Test. You might need to use different values depending on the content in your project and what look you want to achieve.

| Cvar | Value | Description |
| --- | --- | --- |
| `r.ExrReadAndProcessOnGPU` | N/A | Switches EXR playback between CPU and GPU. When enabled for the GPU, Unreal Engine 4 can load large, uncompressed EXR files directly into a Structured Buffer and process them on the GPU. |
| Ray Tracing |   |   |
| `r.RayTracing.ForceAllRayTracingEffects` | 0 | 
Forces all ray tracing effects either on or off. Options for value include:

-   \-1: Do not force (default)
-   0: Disable all ray tracing effects
-   1: Enable all ray tracing effects

Setting this cvar to 0 turns off all the additional ray tracing features that are enabled by default. When using GPU Lightmass, which requires ray tracing, you can still use GPU-accelerated light baking. This cvar can also be useful for figuring out how much performance is required with ray tracing enabled.



 |
| `r.RayTracing.Reflections.MaxRoughness` | 0.2 | Sets the maximum roughness for visible ray tracing reflections (default = -1 (max roughness driven by post processing volume)). This guarantees that only Materials with roughness values lower than 0.2 will have ray-traced reflections. |
| `r.RayTracing.Reflections.MaxRayDistance` | 500 | 

Sets the maximum ray distance for ray traced reflection rays. When ray shortening is used, the skybox will not be sampled in the RT reflection pass and will be composited later, together with local reflection captures. Negative values turn off this optimization (default = -1 (infinite rays)). Using a value other than -1 will help reduce the amount of ray tracing that is done in a scene.



 |
| `r.RayTracing.Reflections.SortMaterials` | 0 | 

Determines whether reflected materials will be sorted before shading. Options:

-   0: Disabled
-   1: Enabled, using Trace > Sort > Trace (Default)



 |
| `r.DiffuseIndirect.Denoiser` | 2 | Denoising options (default = 1) |
| `r.RayTracing.Reflections` | 0 | 

Turn OFF only ray tracing reflections in your level. This is useful in case you still want to use ray-traced shadows or other ray tracing features, and not pay the cost of ray-traced reflections. Options:

-   \-1: Value driven by the postprocess volume (default)
-   0: Use traditional rasterized SSR.
-   1: Use ray-traced reflections.



 |
| `r.RayTracing.Geometry.Landscape` | 0 | 

Include landscapes in ray tracing effects (default = 1 (landscape enabled in ray tracing)) In order to optimize the levels that needed ray-traced reflections, we disabled landscape ray-tracing as it was not adding much to the final look, and disabling it gave us some performance boost.



 |
| `r.RayTracing.Reflections.ScreenPercentage` | 50 | 

Screen percentage the reflections should be ray traced at (default = 100). If your scene doesn't have very shiny and clean reflections you can reduce this value and you will gain some performance.



 |
| Upscaling Resolution |   |   |
| `r.ScreenPercentage` | 75 | 

Render in lower resolution and upscale for better performance (combined with the blendable post process setting). 75 is a good value for low aliasing and performance, verify with 'show TestImage'.

In percent, use >0 and <=100, larger numbers are possible (supersampling) but the downsampling quality is improvable. Numbers <0 are treated like 100.



 |
| `r.TemporalAA.Algorithm` | 1 | 

Algorithm to use for Temporal AA Options:

-   0: Gen 4 TAAU (default)
-   1: Gen 5 TAAU (experimental) This will turn ON our new Gen5 TAAU in case some resolution upscaling is needed .



 |
| `r.TemporalAA.Upsampling` | 1 | 

Whether to perform primary screen percentage with temporal AA or not. Options:

-   0: Perform the spatial upscale pass independently of TAA (default).
-   1: TemporalAA performs the spatial and temporal upscale using the screen percentage method.



 |
| SSGI |   |   |
| `r.SSGI.Enable` | 0 | 

Whether to enable or disable Screen Space GI Options:

-   0: Disable
-   1: Enable Turns OFF Screen Space GI.



 |
| `r.SSGI.HalfRes` | 1 | 

Whether to perform SSGI at half resolution. Options:

-   0: Disable (defaults)
-   1: Enable



 |
| `r.SSGI.Quality` | 1 | Quality setting to control the number of rays shot with SSGI, between 1 and 4 (defaults to 4). |
| Volumetric Fog |   |   |
| `r.VolumetricFog.GridPixelSize` | 6 | 

XY size of a cell in the voxel grid, in pixels. Lower values produce better Volumetric Fog Quality but it will affect performance.



 |
| `r.VolumetricFog.GridSizeZ` | 96 | 

How many Volumetric Fog cells to use in the Z axis. Higher values can help increase accuracy and reduce noise but it can impact performance.



 |
| `r.VolumetricFog` | 0 | 

Whether to enable the Volumetric Fog feature. Options

-   0: Disabled
-   1: Enabled This can be used to quickly turn OFF Volumetric Fog and determine how much performance it uses.



 |
| Rendering |   |   |
| `ShowFlag.DirectLighting` | 0 | 

This cvar is useful for quickly disabling direct lighting in order to understand what is baked and what isn't, and its performance implications. Options:

-   0: Disable the showflag.
-   1: Enable the showflag.
-   2: Do not override this showflag (default).



 |
| `r.SetNearClipPlane` | 150 | 

Set the near clipping plane (in cm). This cvar will allow you to modify the Near Clip Plane in case you want to quickly remove any geometry that is in front of your render camera.



 |
| `r.TextureStreaming` | 0 | 

Defines whether texture streaming is enabled, which can be changed at run time. Options

-   0: Disabled
-   1: Enabled (default)



 |
| `r.Streaming.PoolSize` | 3600 | 

\-1: Default texture pool size, otherwise the value is the size in MB. This cvar can be used to increase the texture pool size at runtime in order to allow higher mipmaps to be loaded, if the pool size originally was set too low and your hardware allows a higher texture pool size.



 |
| `r.DFShadowScatterTileCulling` | 1 | 

Whether to use the rasterizer to scatter objects onto the tile grid for culling. Options

-   0: Disabled
-   1: Enabled



 |
| `r.ForceLOD` | 5 | 

LOD level to force, -1 is disabled. This is useful for testing how much performance or quality can be gained by forcing a specific LOD on the scene.



 |