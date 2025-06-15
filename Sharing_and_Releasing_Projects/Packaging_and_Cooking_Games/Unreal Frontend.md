# Unreal Frontend

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool)  
**Processed:** 2025-06-14 17:02:06

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02f56aaa-30e0-42a6-b3fb-8ab1ec11e6b0/unrealfrontend.png)

**UnrealFrontend** (UFE) is a tool intended to simplify and speed up daily video game development and testing tasks, such as preparing game builds, deploying them to a device, and launching them. UFE is designed to be the central interface for all game deployment, profiling, and testing tasks.

## Features

UFE provides the following features:

| Feature | Description |
| --- | --- |
| **Launcher** | 
Build, cook, deploy and launch your game. UFE allows you to simultaneously deploy to multiple target devices running different target platforms, either locally connected or anywhere on the network. You will be able to launch multiple instances per device (on supporting platforms) and configure different roles per instance in order to drastically speed up your workflow for testing your single or multiplayer cross-platform games.



 |
| **Sessions** | 

Remotely monitor and interact with any of your currently active game sessions running on the network. The new **Session Browser** will allow you to locate instances of your game currently running on the network. The Session Console shows you a real-time feed of each game instance's output log, and it allows you to remotely execute console commands on one or more target devices. It will soon be possible to share your active sessions remotely with other developers or artists in order to get a second opinion without them having to come to your desk.



 |
| **Automation** | 

Automatically test code and content and verify their integrity. This is a new feature not available in previous versions of the engine. You will be able to write unit/feature/stress tests for your game's custom C++ classes and content, and you can create automated tests for verifying common workflows, such as verifying that all maps and packages are loading without errors. We are also working on integrating automation tests into our build system, so that it will be possible to run them automatically and detect potential problems as part of the continuous integration process.



 |
| **Profiling** | 

Remotely analyze the performance of your game and locate bottlenecks. If you are familiar with our previous suite of profiling tools in UE3, you will be excited to hear that we are working on integrating all these disparate tools into a single user experience inside UFE.



 |
| **Device Management** | 

Manage your devkits, mobile devices and other test computers. Simple device discovery was already available in previous versions of UFE, but in UE4 it will be a lot more powerful. We are dropping the restriction that a target device has to be connected to the local PC, either physically or through the device's SDK. You will be able to detect locally connected and networked devices and share them with others. Windows and Mac computers are now also able to act as target devices for deployment, launching, and automation.



 |

## Getting Started

Unreal Frontend is available as both a tab for Unreal Editor and a standalone application. While their functionality is equivalent, the lightweight standalone application is likely the preferred tool for QA personnel and programmers. Artists may prefer the in-editor version, because they already have Unreal Editor opened most of the day. The Unreal Editor tab can be accessed from the **Window** menu:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1358723-edd7-46f6-aa36-8356d56194bf/workspace_menu.png)

The standalone application is located in the /Engine/Binaries/Win64 and /Engine/Binaries/Mac directories:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6e1e6c6-4972-4f47-a8fb-fa280c6ea5b8/explorer.png)

Please note that if you are using a source build of the engine, you will need to build UnrealFrontend from Visual Studio or XCode first.

## Interface

The UnrealFrontend user interface is made up of the following components:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b1d02d2-ec5a-4710-a535-81fcfb525721/unrealfrontend_ui.png)

1.  [Device Browser](/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool#devicebrowser)
2.  [Launcher](/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool#launcher)
3.  [Session Browser](/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool#sessionbrowser)
4.  [Automation](/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool#automation)
5.  [Session Console](/documentation/en-us/unreal-engine/using-the-unreal-frontend-tool#sessionconsole)

## Launcher

The Launcher tab allows you to build, cook, deploy, and launch your game. There will eventually be many different ways to accomplish this, but as of this writing, only the following settings are supported:

-   Build: Create new build.
-   Cook: On the fly (Windows and selected consoles).
-   Deploy: File server (local Windows and selected consoles), Deploy to device (local Windows).
-   Launch: Using default role (i.e. single instance per device + same settings for all).

All settings in the Launcher are combined into profiles. This allows you to maintain different groups of settings in parallel, which is particularly handy for QA personnel who need to run many different tests a day. When you open the Launcher for the first time, no profiles will be present, and you will have to create a new one:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d5f7577-6a7f-4b08-986c-b451a914f64c/profile_add.png)

Once a profile is created, a number of settings categories will be shown:

### Build

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e4155d6-4791-44a4-a80f-1ecc075c975b/launcher_build.png) | 
-   **Game**: Specifies the game project to build.
-   **Build Configuration**: Sets the configuration to use when building the game.



 |

### Cook

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d16e21a-9a5e-4c86-814b-d72410b767b9/launcher_cook.png) | 
-   **Cooked Platforms**: Specifies which platforms the game content is to be cooked for.
    
    Uncooked content is currently unsupported on any platform.
    
-   **Cooked Languages**: Specifies the language the game content is to be cooked for.
-   **Cooked Maps**: Specifies the maps to cook.
-   **Only cook modified content**: If enabled, the cooker will ignore any content that has not been modified.
-   **Save packages without versions**
-   **Cooker Build Configuration**: Sets the configuration to determine which binary to use for cooking.
-   **Additional Cooker Options**



 |

## Device Browser

The **Device Browser** is currently quite limited in functionally, but it will eventually allow for managing and sharing all target devices on the network (including the transfer of log files). It automatically detects devices that are available locally and also provides an interface for manually adding devices that cannot be discovered.

There is currently no true concept of device ownership. To what extent we will implement it (including the locking of devices that are shared amongst multiple developers) is still TBD.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e9f4941-09f9-45e4-af19-d02ab01a207d/device_browser.png)

Currently, we only support devices that can be discovered locally. At the time of this writing, this includes the local Windows PC (both Win32 and Win64 platforms) and selected console devices on the network.

## Session Browser

When launching a game on one or more devices, the Launcher will create a new session that consists of every game instance that is running, and which can be tracked in the **Session Browser**. It plays a very central role in UFE, because the currently selected session (or session instances) determines the functionality of other UFE tabs, such as the Session Console tab, the Automation tab and the upcoming Profiler.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47a9c576-1cb2-4352-af94-089f5192b668/session_browser.png)

Like the Device Browser, the Session Browser is still limited in functionally. It currently consists of a split list layout. The top list shows all discovered sessions and the bottom list shows the game instances that are part of a selected session. A session does not necessarily consist of only games, but may also include auxiliary tools, such as content cookers and file servers.

When running UFE from within the Unreal Editor, there is currently always an *Unnamed Session* being shown (which represents the Unreal Editor instance itself).

## Session Console

The **Session Console** is the central hub for gathering the log output from all game instances that are currently selected in the Session Browser. Which logs are being displayed depends on the currently selected instances in the Session Browser. The list of log messages (4a) can then be filtered using a search string or category and verbosity filters (4b). It is possible to send console commands to selected game instances (4c). Commands sent to multiple instances will be executed by each instance. Last but not least, it is also possible to export all or selected log messages to a file (4d).

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23dc5c92-dfbb-44ef-8152-5280670d8989/console.png)

As of this writing, only the log since the discovery of a session will be available. We will change this soon to allow for retrieving log that was generated prior to running UFE.

## Automation

The **Automation** panel provides access to automated testing functionality. Each instance in a session (including the local Unreal Editor instance when running UFE in-editor) is able to perform automated unit/feature/stress tests for code and content verification at any given time.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc124ffb-5c66-4d40-aec3-1600298ae6b3/automation.png)

1.  **Control Panel**
2.  **Filter Panel**
3.  **Test list**
4.  **Results**

After selecting one or more instances in the Session Browser, the Test List will display all tests that are available for those instances. You can then select which tests you actually want to run by selecting the checkbox of one or more tests, or you can filter the list of tests using the Filter Panel. To execute the selected tests, press the start button in the **Control Panel**. The results of the tests (including error messages) are then aggregated in the **Results View**.

It is possible to run automated tests on multiple instances in parallel (by selecting multiple instances). We are currently working on the implementation of test groups that will allow for different levels of parallelization (various types of load balancing, redundant testing etc.). Please check the documentation for the Automation system on details about how to create new tests.

## Unreal Remote Agent

**Unreal Remote Agent** (URA) is a standalone program that runs in the system tray of remote PCs (and eventually Macs) to make those PCs and console devices connected to them available over the network. URA, previously required to deploy and launch games, is currently not supported and in the process of being upgraded.