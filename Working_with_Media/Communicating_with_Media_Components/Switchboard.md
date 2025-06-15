# Switchboard

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/switchboard-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/switchboard-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:14

---

**Switchboard** is a Python application for controlling multiple remote devices and relies on the companion application SwitchboardListener to communicate with them. **SwitchboardListener** is an Unreal Engine C++ application that runs a TCP socket server on each device to share JSON messages with Switchboard.

Switchboard's features include:

-   Start Unreal Engine remotely on a device in a [Multi-User session](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine).
-   Launch [nDisplay](/documentation/en-us/unreal-engine/rendering-to-multiple-displays-with-ndisplay-in-unreal-engine) on multiple devices.
-   Record with embedded [Take Recorder](/documentation/en-us/unreal-engine/record-gameplay-in-unreal-engine) controls.
-   Sync all devices to a specific changelist and build your Project and Unreal Engine from source.
-   Connect to and control the following devices: [KiPro](https://www.aja.com/family/digital-recorders), [Live Link Face](/documentation/en-us/unreal-engine/recording-face-animation-on-ios-device-in-unreal-engine), [Shogun](https://www.vicon.com/software/shogun/), and [SoundDevices](https://www.sounddevices.com/).
-   Add your own device plugins and extend Switchboard and SwitchboardListener for custom controls.

This page covers some of the features available in Switchboard. For getting started with Switchboard, follow the steps in the [Switchboard Quick Start](/documentation/en-us/unreal-engine/switchboard-quick-start-for-unreal-engine). See the [Switchboard Settings Reference](/documentation/en-us/unreal-engine/switchboard-settings-reference-for-unreal-engine) for specific details on all the settings available.

## Virtual Production Roles

The **Switchboard** application requires each user to occupy a **VP Role**, such as an **Editor** or **Render**, to differentiate and identify connected users.

1.  On your primary workstation in the Unreal Editor, navigate to the Toolbar, and select the **VP Roles**, then select (**+**) **Add Role** from the drop-down menu. Give the new role a name. In this workflow example the primary workstation is named Editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbfaba06-6a7b-49bd-b46b-1b2e08d6cc6d/addnewrole.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3eb1705d-860b-4e1a-8866-473012869138/editorprodrole.png)
2.  Using the same steps, add a second **Role** for your secondary device to occupy. In this workflow example, the secondary workstation is named Render.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44d66b75-4608-400a-b75f-fda481bd802a/renderprodrole.png)
3.  In the **Menu Bar**, navigate to **Edit** > **Project Settings**, and under the **Multi-User Editing** section,set the **Validation Mode** property to **Soft**, using the drop-down menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7c959b4-3377-4fb1-981b-566175874b4d/softauto.png)

If your project contains any dirty packages, an error prompt displays when you join a multi-user session. You then have the opportunity to cancel the connection or to fix any present issues. If you choose to proceed any dirty packages will be deleted.

Your project is now ready to connect other devices using Switchboard.

## Take Recording with Switchboard

You can record takes in a connected Unreal device using the TakeRecorder functionality embedded in Switchboard. Switchboard uses [OSC](/documentation/en-us/unreal-engine/osc-plugin-overview-for-unreal-engine) to communicate with the Unreal Instance for recording. The Switchboard plugin includes a default **OSC Listener** to create this connection for you.

Make sure the following settings are set up properly:

-   Enable **Start an OSC Server when the editor launches** in the **Virtual Production Editor** plugin.
-   The **OSC Server Port** in the **Virtual Production Editor** plugin matches the **OSC Client Port** in the [Switchboard Settings](/documentation/en-us/unreal-engine/switchboard-settings-reference-for-unreal-engine).
-   The **OSC Server Address** is reachable by Switchboard.

Click image to expand.

![Virtual production editor port settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8597bb88-99df-4c26-a6a5-ddc26f3dc55c/virtual_production_editor_port_settings.png)

In Switchboard, the status icon turns green if the OSC connection is successful for the device.

  ![Not connected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04766e2a-f89c-4847-9c34-57c7f1854b4f/switchboard_osc_status_1.png) ![Attempting to connect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28767d18-06ec-43ff-9ef1-ab17b27ffb2a/switchboard_osc_status_2.png) ![Successfully connected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fb9ca46-7273-4517-8f3c-d3a1c8e6866b/switchboard_osc_status_3.png)

Comparing the Switchboard status icons.

The status icon will turn orange after starting Unreal if the OSC connection is unsuccessful.

![Unsuccessful connection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55684340-1bc0-44bf-94dd-47d80b792c72/switchboard_osc_status_fail.png)

-   At the top of Switchboard, you can set the **Sequence** name, **Slate** name, and **Take** number.
-   The names should immediately be reflected in the **TakeRecorder** of the OSC-connected Unreal device.
-   Press the red button on the right to start and stop recording.
-   If a device is recording, its background is set to red in Switchboard.
-   After each recording, the **Take** number is incremented.
    
    ![Switchboard device recording](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33a0abd3-30c6-4717-b188-67be9138236f/switchboard_device_recording.png)

Check the Debug log to verify expected status changes for devices.

![Switchboard debug log](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38d879f5-dfd7-4279-bb74-4975306d0089/switchboard_debug_log.png)

## Launching nDisplay with Switchboard

You can set up Switchboard to communicate with all your nDisplay devices. When you choose to add an nDisplay device in Switchboard, you add the location of your [nDisplay config file](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine). Switchboard parses the config file and converts the cluster nodes specified in the file to Switchboard devices. See [Switchboard Settings](/documentation/en-us/unreal-engine/switchboard-settings-reference-for-unreal-engine) for more details on how the nDisplay devices can be further configured in Switchboard.

![nDisplay device list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c19151cd-98ed-4e64-9876-e8a9f3419cc9/ndisplay_device_list.png)

In addition to adding nDisplay devices, information on the status of the nDisplay cluster appears on the right side of the Switchboard window in the nDisplay Monitor panel. The following table describes the information included in the monitor. Whenever the values are unexpected, the color of the cell turns yellow as a warning.

You can execute commands remotely to the nDisplay cluster by entering a command in the **Console** text box (such as "stat fps" or "r.RayTracing.SceneCaptures 0") and clicking **Exec**.

![nDisplay monitor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31cfd1c2-7803-48ce-abfe-1d212157793c/ndisplay_monitor.png)

| **Column** | **Description** |
| --- | --- |
| Node | The nDisplay [scene node](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#scenenodeconfigurations). |
| Host | The device's IP address. |
| Connected | Displays **yes** or **no**. |
| Driver | The NVIDIA driver version. |
| PresentMode | The swap chain presentation mode. |
| Gpus | Indicates if the detected GPUs are being synchronized by a Quadro Sync card. |
| Display | Indicates if the detected displays are being synchronized. |
| SyncRate | The display refresh rate. |
| HouseSync | Indicates the presence of an external synchronization signal into the Quadro Sync card. |
| SyncSource | Indicates if the synchronization source is house sync or vsync. |
| Mosaics | Lists the display grid configuration. |
| Taskbar | Indicates whether the taskbar auto-hide setting is set or not. |
| InFocus | Indicates whether the nDisplay instance window is in focus. It is recommended to be in focus. |
| ExeFlags | Flags on the UnrealEngine executable. We recommend using the **Disable Fullscreen Optimizations** option. |
| OSVer | Operating system version. |
| CPUUtilization | Average CPU utilization. The number of overloaded cores are displayed in parentheses. |
| MemUtilization | Physical memory utilization |
| GpuUtilization | Average GPU utilization. Clock speed is specified in parentheses. |
| GpuTemperature | Max GPU Temperature in Celsius degrees across all sensors. |

## Syncing and Building

You can connect your source control to Switchboard, then sync and build your project and engine according to a certain changelist across all connected devices. You can see what changelists are on each connected device to know which ones need to be updated.

Follow these steps to add your source control information to Switchboard:

1.  Open **Switchboard Settings**.
2.  In the Switchboard Settings dialog, check the box next to **Source Control**.
3.  In the section under **Source Control**:
    
    1.  Set **P4 Project Path** to your project's Perforce Stream.
    2.  If you want to build the engine from source, set **P4 Engine Path** to your engine's Perforce Stream. Setting this path is not required if you only plan to sync and build your project.
    3.  Set **Workspace Name** to the name of your Perforce Workspace.
    
    ![Switchboard source control paths](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fa8dbfd-253c-42ef-83db-ef6faf501fd2/switchboard_source_control_paths.png)
4.  In the section under **Project Settings**:
    
    1.  Set **UProject** to the location of your Unreal Engine project.
    2.  Set **Engine Dir** to the directory where the binary release of the engine is located.
    3.  If you want to build the engine from source, check the **Build Engine** checkbox. If you are only building your project, leave it unchecked.
    
    ![Switchboard project paths](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df780176-1b47-4d3a-ac68-4d597fed8209/switchboard_project_paths.png)

When your source control information is added, the Engine and Project changelists appear in Switchboard above the list of devices. This means that there is only one place where the current changelist for all devices is specified.

![Switchboard changelists](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ebcecc7c-f855-40d1-bec4-fa71f28e6e4a/switchboard_changelists.png)

In this screenshot, the Project changelist and Engine changelist are shown.

Each device also shows what Engine and Project changelists it has. If a device's changelist is behind the one selected at the top of Switchboard, its text color turns red.

![Switchboard device changelist](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6288ea90-4253-4c4e-aa98-f79b59f460b7/switchboard_device_changelist.png)

### Source Control Buttons

| **Icon** | **Action** | **Description** |
| --- | --- | --- |
| ![Refresh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6df44932-7f95-43da-9e7a-6728729bca8f/refresh_icon.png) | Refresh | Updates the source control information in Switchboard. |
| ![Sync](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05d41b79-3688-4b6e-b3eb-9997864c3f40/sync_icon.png) | Sync | Syncs all connected devices to the changelist. If this button is on the device's row, Switchboard only syncs that device. Controls on the devices are locked during a sync. |
| ![Build](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/020d1772-035a-4a6a-ac0b-017abfb9396a/build_icon.png) | Build | Builds on all connected devices. If this button is on the device's row, Switchboard only builds on that device. Controls on the devices are locked during a build. |
| ![Sync and Build](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8f7db0f-4cd2-498a-af28-bc4808c1d1d9/sync_and_build_icon.png) | Sync and Build | Syncs and builds on all connected devices. If you enabled Build Engine in the settings, this option will sync and build the engine before the project. |

If you don't want to sync the engine or the project, select the **\--None--** entry in the changelist dropdown to ignore the engine or project in the next sync and build operation.