# Managing Platforms in Unreal Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-platforms-dropdown-in-unreal-editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-platforms-dropdown-in-unreal-editor)  
**Processed:** 2025-06-14 17:01:41

---

**Unreal Editor** now features a dedicated **Platforms** dropdown in the toolbar. This dropdown accesses the **Turnkey** platform support system, providing a means for quickly installing and updating SDKs, as well as an interface for launching and testing on devices.

![Accessing the Platform Menu in the Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e812cc1-6a77-49ce-b695-de0c7601b79c/platformmenu.png)

This page provides a reference for the tools available through this menu.

The editor functions here access the same system as the [Turnkey commandline](/documentation/en-us/unreal-engine/using-the-turnkey-commandline-for-unreal-engine).

## Prerequisites

To use the Platforms menu for installing SDKs, your organization must make the SDK files for your platforms available in a file source repository, and you must have a valid TurnkeyManifest XML file pointing to that repository. For more information about how to prepare a file source repository, refer to Setting up [Turnkey for Your Organization](/documentation/en-us/unreal-engine/setting-up-turnkey-for-your-organization-in-unreal-engine).

## Installing and Managing SDKs

Each platform supported by your project appears in the **Content/SDK/Device Management** section of the Platforms dropdown. To install SDKs, navigate to the menu entry for the platform whose SDK you want to install, then click **Install Sdk**.

![Selecting an SDK to install](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7229f5d8-3fc3-4ff4-a287-f8693b0ac34a/platforminstallsdk.png)

If the platform you want does not appear in this list, navigate to **Platforms With No Compiled Support**, which will display all platforms that Unreal Engine supports but that you do not have SDKs set up for.

![Accessing platforms with no compiled support](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/691ded20-744a-42a9-a106-c9a1e508e5ca/platformsdksnotfound.png)

Selecting **Install Sdk** will start up Turnkey and initialize the download and installation process for the selected SDK. **Prefer Full** will favor a full SDK installation. **Prefer Minimal** will prefer the smallest possible SDK installation, such as a Flash SDK for testing purposes.

Depending on which SDK you are installing, additional prompts may appear for setting up specific SDK components, like Android Studio.

You can check the SDK status by looking at a platform's **SDK Management** section, which will display your current SDK and the range of compatible SDKs for your platform. You can check the SDK status for an individual device in the submenu for its platform. Locate the **All Devices** section and highlight the entry for a device to display this information.

![Showing device information for an Android device](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f76ccd23-afe4-4997-87c9-7b7ac7bbd2b9/platformdevice.png)

## Packaging Projects

To package a project, click the **Platforms** dropdown in the editor, then navigate to the platform that you want to package for and click **Package Project**. A dialog will prompt you to save the packaged project, then initiate the packaging process when you select a directory to save to.

![Packaging a project for Android](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11f9808c-3612-4046-a6fe-d2d8be78a314/platformpackaging.png)

You can change build targets and binary configurations with the settings in the submenu for your platform.

To configure packaging settings, you can either click **Packaging Settings** in the Platforms dropdown menu, or you can open **Project Settings > Packaging Settings**.

## Setting Up Target Devices

If you click **Device Manager** in the dropdown, it will open the Device Manager window.

![Using the Device Manager](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d35ed40a-4725-4a66-bd2e-a1200ef15d9a/platformdevicemanager.png)

This window will display recognized devices and dev kits on your local network, including compatible mobile devices connected to your computer. You can use this menu to claim, release, or share devices. Only devices that you have claimed will appear in the **Project Launcher**. You can also use this menu to control devices remotely by powering them on or off, rebooting them, or connecting/disconnecting them.

If you select a device, the **Running Processes** tab will display a snapshot about current processes that device is running and their resource load, provided that device supports process snapshots. Additionally, the **Device Details** tab will list what features are available on that device.

## Launching Projects on Devices

The Platforms dropdown has a **Quick Launch** section, and you can click one of the devices listed here to immediately install and launch a build on it using the default settings.

![Accessing Quick Launch from the Platform menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fc8a62d-7770-4580-824c-1cfbbbe69922/platformquicklaunch.png)

Quick Launch options are also available in the dropdown menu for the **Play** button.

![Accessing Quick Launch from the Play dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85a65a79-1e9a-4eae-98e1-6225426744ad/platformquicklaunchplaybutton.png)

### Project Launcher

For advanced use cases, you can also click the **Project Launcher** button in the **Platforms** dropdown to bring up the **Project Launcher** window.

![Using the Project Launcher window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/900bce08-fb72-48d7-b246-c01b03082981/platformprojectlauncher.png)

This menu will show any devices that you have set up using the Device Manager, and you can configure the profile that you want to use to launch it. By default the **variant** field is displayed, but toggling the **Advanced** button will show the project configuration and cooking settings. The **Custom Launch Profiles** menu enables you to set up custom profiles with detailed packaging and deployment options for even more advanced use cases on specific projects.

![Creating a custom profile in the Project Launcher window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43176382-7304-4e98-bfbb-2167e3f14d30/platformprojectlaunchercustom.png)