# Switchboard Settings Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/switchboard-settings-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/switchboard-settings-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:53:17

---

This page describes the settings you can change for Switchboard.

## Switchboard Plugin Settings

To access the Switchboard plugin settings, in the main menu of the Unreal Editor choose **Edit > Project Settings > Plugins > Switchboard**.

![Switchboard plugin settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1238528-b159-430e-a292-bec8bed292ee/project-settings.png)

You can set the OSC Listener in the plugin settings. Switchboard requires an OSC Listener to be able to use Take Recorder. Refer to [Take Recording with Switchboard](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine#takerecordingwithswitchboard) for more details. You can configure how Switchboard launches and install any required dependencies in the Editor Preferences for the Switchboard plugin. The following table describes the parameters you can set in Editor Preferences.

![Switchboard editor preferences](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b71a4ce-9d7e-440f-81c7-2a931ee95269/editor-preferences.png)

| **Parameter** | **Description** |
| --- | --- |
| **Switchboard** |   |
| Virtual Environment Path | The default Python version for Switchboard is Python 3.7.7. To use a different version of Python, change this field to point to a different Python interpreter on your machine. |
| **Switchboard Listener** |   |
| Listener Commandline Arguments | 
SwitchboardListener expects the following arguments:

-   `-ip`: Sets the IP address that Switchboard Listener listens on
-   `-port`: Sets the port that Switchboard Listener listens on



 |
| Launch Switchboard Listener on Login | When enabled, Switchboard Listener is launched on the local machine every time you log into the computer. |

## Switchboard Settings

Settings that are common to all device plugins are in the general section of the **Settings** panel, including the values added during the initial project set up. After you add a device, settings for those devices are appended to the settings panel, and a tab appears on the left so you can choose to filter the settings based on the device type.

![Switchboard settings panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5955927-afdf-4f9d-9d64-953905f73d9d/switchboard-settings-tabs.png)

Some general settings are repeated in a device's settings so you can override the value per device if needed. If you override a setting in a specific device, a different background color appears. As long as the override is in place, changing the global setting will not cause a change for this setting in the device.

![Switchboard settings overriden](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c18cd00d-27a1-48d3-97ad-b0a5e91c42d7/override-settings.png)

The following sections describe all the settings that can be modified in the **Settings** panel.

### General Settings

| **Parameter** | **Description** |
| --- | --- |
| Config Path | The path where Switchboard config files are stored. These files hold all of the switchboard state. |
| IP Address | The IP address of the machine running Switchboard and the internal OSC server. Change the address here if you have multiple network controllers in the computer running Switchboard. |
| Transport Path | Currently not used in Switchboard. |
| Listener Executable Name | The program name to use for launching the switchboard listener application |

### Project Settings

| **Parameter** | **Description** |
| --- | --- |
| Project Name | The name of the Switchboard project. Will be used as a basis for the filename that settings and devices are stored in. |
| UProject | The local path to the UE project file. |
| Engine Directory | The local path to the Unreal Engine directory. |
| Build Engine | The flag to enable building the engine from source in Switchboard. |
| Map Path | The relative path from the **Content** folder to maps that will appear in the **Level** dropdown in Switchboard. |
| Map Filter | The file filter for limiting what maps appear in the Level dropdown. |
| **OSC** |   |
| OSC Server Port | The port for the OSC server in Switchboard to listen on. |
| OSC Client Port | The port of the OSC client specified in the Unreal Editor. |
| **Source Control** |   |
| Workspace Name | The name of the Perforce workspace that maps to the depot project path. |
| Perforce Project Path | The Perforce depot path for the Unreal project specified in UProject. Only the depot folder containing the uproject file needs to be specified. |
| Perforce Engine Path | The P4 Engine Path setting is only required if you plan to build the engine from source, and not just the project. Refer to [Syncing and Building](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine#syncingandbuilding) for more details. |

### Multi-User Server Settings

| **Parameter** | **Description** |
| --- | --- |
| Server Name | The name appended to the Project Name to create the full server name. |
| Command Line Args | Optional arguments passed to the Multi-User Server executable. |
| Unicast Endpoint | The Unicast Endpoint specified for Mult-User on launch. This is the port that the server listens for connections, and corresponds to the **UDP Messaging** settings in the Project Settings. The default value is **0.0.0.0:9030**. |
| Multicast Endpoint | This is the multicast group that Multi-User should subscribe to. All Unreal nodes participating in the same Multi-User session should have the same multicast endpoint. Modification of this variable is for advanced configurations. |
| Multiuser Executable Name | The name of the program for launching a Multi-User Server session. |
| Auto Launch | Enable this option to launch the Multi-User Server the first time either an Unreal or nDisplay device is started. The server always runs on the same device as Switchboard. |
| Clean History | Passes the argument `-ConcertClean` to the server so the server session's working directory is cleaned on launch. |
| Auto Build | Enable this option if the Multi-User Server should be rebuilt when the source changes in the Engine folder. |
| Auto Endpoint | Enable this option if the static endpoint of the Multi-User Server should be assigned when launching an Unreal Editor or nDisplay node. This is equivalent to adding a static endpoint to the Multi-User Server Unicast Endpoint in the Project Settings. |
| Unreal Multi-user Server Auto Join | Enable this option to have each Unreal or nDisplay device automatically join the Multi-User Server. |

### Unreal Device Settings

| **Parameter** | **Description** |
| --- | --- |
| 
Is Recording Device



 | 

Enable this option if this device type is going to record sequences.



 |
| Buffer Size | The internal buffer size of the socket client connected to SwitchboardListener. |
| Command Line Arguments | Optional command line arguments that are passed to Unreal on start. |
| 

ExecCmds



 | 

Sets `-ExecCmds` (console commands) that are passed to Unreal on start as command line arguments.



 |
| 

DPCVars



 | 

Pass Device Profile Console variables in a comma separated list.



 |
| 

Listener Port



 | 

The port number the listener listens on. The default port is 2980.



 |
| 

Roles Filename



 | 

The filename of the .ini file that contains the [Virtual Production Roles](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine#virtualproductionroles).



 |
| 

Stage Session ID



 | 

An ID that groups Stage Monitor providers and monitors. Instances with different Session IDs are invisible to each other in [Stage Monitor](/documentation/en-us/unreal-engine/stage-monitor-with-unreal-engine).



 |
| Unreal Editor filename | The filename of the Unreal Editor executable. |
| 

Number of GPUs



 | 

The number of GPUs to use on a device in case there is more than one.



 |
| 

Process Priority



 | 

Overrides the priority of the process.



 |
| 

Skip Package Recovery



 | 

Automatically discards auto-saved packages at startup, skipping the restore prompt. Useful in multi-user scenarios, where restoring from auto-save may be undesirable.



 |
| 

Unicast Endpoint



 | 

The Unicast endpoint for the node. Typically this should be the default assigned value. Switchboard will use the name of the switchboard assigned IP address with :0.



 |
| Extra Static Endpoints | Additional static endpoints to set when the Unreal Editor is launched. This corresponds to the static endpoint setting for **UDP Messaging** in Project Settings. |
| 

Multicast Endpoint



 | 

Overrides the multicast endpoint.



 |
| Log Download Dir | Destination folder for collecting logs and Unreal Insights trace files from remote devices. By default, the path is in the project directory in the folder **/Saved/Logs/Switchboard**. |
| Reflect Editor Visibility to Game | Enable this option to reflect the state of the editor visibility of an object to the corresponding `-game` visibility, such as Hidden in Game, in a Multi-User session. In an nDisplay configuration you typically want to enable this for the operator station so that changes to level visibility will properly reflect the `-game` instances. |
| Rsync Server Port | The assigned port for the rsync server that runs on the Switchboard application. The rsync server is used to transfer larger data from the connected nodes to the main Switchboard instance. |
| Listener Timeout | The timeout period for a Switchboard Listener process. If the Switchboard Listener does not detect a message from the main Switchboard application within the given timeout period, then the connection to the Switchboard application is terminated. |

For each Unreal instance:

| **Parameter** | **Description** |
| --- | --- |
| 
IP address



 | 

The remote address on which the SwitchboardListener listens.



 |
| 

Roles



 | 

Dropdown menu enabling selection of a [Virtual Production Role](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine#virtualproductionroles) from those provided in the Roles .ini file.



 |
| Exclude from build | When enabled, the engine builds should not occur on this node. |
| Is Recording Device | Override for whether this device is used for recording. |
| Command Line Arguments | Override for optional command line arguments. |
| 

ExecCmds



 | 

Override for exec commands for Unreal.



 |
| 

DPCVars



 | 

Override for the Device Profile Console variables.



 |
| 

Number of GPUs



 | 

Override for the GPU count to use.



 |
| 

Process Priority



 | 

Override for the priority of this instance.



 |
| 

Skip Package Recovery



 | 

Override for whether auto-saved packages are automatically discarded at startup.



 |
| 

Unicast Endpoint



 | 

Overrides the unicast endpoint.



 |
| 

Extra Static Endpoints



 | 

Overrides the extra static endpoints.



 |
| 

Engine Directory



 | 

Override for the local path to the engine.



 |
| 

Workspace Name



 | 

Overrides the Perforce Workspace name.



 |
| 

uProject Path



 | 

Override for the local path to the uproject file.



 |

### KiPro Device Settings

| **Parameter** | **Description** |
| --- | --- |
| 
Is Recording Device



 | 

Enable this option if this device type is going to record sequences.



 |
| IP address | The address of the KiPro web server. |
| Auto Play After Stop | Enable this option to playback automatically when the recording ends. |

### Live Link Face

| **Parameter** | **Description** |
| --- | --- |
| 
Is Recording Device



 | 

Enable this option if this device type is going to record sequences.



 |
| IP address | Currently not used in Switchboard. |

### Motive Device Setttings

| **Parameter** | **Description** |
| --- | --- |
| 
Is Recording Device



 | 

Enable this option if this device type is going to record sequences.



 |
| Motive Command Port | Communication port used for Motive devices. |
| IP address | The assigned IP address of the Motive Device |

### nDisplay Device Settings

| **Parameter** | **Description** |
| --- | --- |
| nDisplay Config File | Both the .cfg and the JSON formats are supported. |
| Use All Available Cores | Enable this option to use all cores. |
| Texture Streaming | Toggle texture streaming. |
| Render API | The options are DirectX11 or DirectX12. |
| Render Mode | Allows selection of nDisplay render modes. |
| Render Sync Policy | Refer to [Render Sync Policies](/documentation/en-us/unreal-engine/synchronization-in-ndisplay-in-unreal-engine#rendersyncpolicies) for more details. |
| nDisplay Executable Filename | Sets the name of the executable for the project. This is useful for packaged builds. |
| Extra Cmd Line Args | Optional command line arguments that are passed to nDisplay on start. |
| 
ExecCmds



 | 

Sets `-ExecCmds` (console commands) that are passed to Unreal on start as command line arguments.



 |
| 

DPCVars



 | 

Pass Device Profile Console variables in a comma separated list.



 |
| Unattended | Enable this option to indicate that it is an unattended application and all dialog windows should be suppressed. |
| 

Number of GPUs



 | 

The number of GPUs to use on a device in case there is more than one.



 |
| 

Process Priority



 | 

Overrides the priority of the process.



 |
| Minimize Before Launch | Enable this option if all windows on the host computer should be minimized prior to launching the nDisplay node. |
| Logging | Custom logging that can be controlled per device. |
| 

Unicast Endpoint



 | 

The Unicast endpoint for the node. Typically this should be the default assigned value. Switchboard will use the name of the switchboard assigned IP address with :0.



 |
| 

Extra Static Endpoints



 | Additional static endpoints to set when the nDisplay Renderer is launched. This corresponds to the static endpoint setting for **UDP Messaging** in Project Settings. |
| Disable Ensures | Disable ensure conditions in the running instance. The ensure condition will still be logged but will not cause instances to terminate. |
| Disable All Screen Messages | Enable this option if on-screen messages should be disabled. |
| 

Listener Port



 | 

The port number the listener listens on. The default port is 2980.



 |
| 

Roles



 | 

Dropdown menu enabling selection of a [Virtual Production Role](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine#virtualproductionroles) from those provided in the Roles .ini file.



 |
| 

Stage Session ID



 | 

An ID that groups Stage Monitor providers and monitors. Instances with different Session IDs are invisible to each other in [Stage Monitor](/documentation/en-us/unreal-engine/stage-monitor-with-unreal-engine).



 |

For each nDisplay node:

| **Parameter** | **Description** |
| --- | --- |
| 
IP address



 | 

The remote address on which the SwitchboardListener listens.



 |
| 

Roles



 | 

Dropdown menu enabling selection of a [Virtual Production Role](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine#virtualproductionroles) from those provided in the Roles .ini file.



 |
| Exclude from build | Overrides whether to exclude this node for enginge builds. |
| UE Command Line | The full command for launching the nDisplay renderer on this node. |
| Extra Cmd Line Args | Override for optional command line arguments. |
| ExecCmds | Override for exec commands for nDisplay |
| 

DPCVars



 | 

Override for the Device Profile Console variables.



 |
| 

Number of GPUs



 | 

Override for the GPU count to use.



 |
| 

Process Priority



 | 

Override for the priority of this instance.



 |
| 

Unicast Endpoint



 | 

Overrides the unicast endpoint.



 |
| 

Extra Static Endpoints



 | 

Overrides the extra static endpoints.



 |
| 

Engine Directory



 | 

Override for the local path to the engine.



 |
| 

Workspace Name



 | 

Overrides the Perforce Workspace name.



 |
| 

uProject Path



 | 

Override for the local path to the uproject file.



 |

### Shogun Device Settings

| **Parameter** | **Description** |
| --- | --- |
| 
Is Recording Device



 | 

Enable this option if this device type is going to record sequences.



 |
| IP Address | The address of the device running Shogun. |
| Save Path | Path to Shogun's capture folder. |

### SoundDevices Device Settings

| **Parameter** | **Description** |
| --- | --- |
| 
Is Recording Device



 | 

Enable this option if this device type is going to record sequences.



 |
| IP Address | The address of the SoundDevices web server. |