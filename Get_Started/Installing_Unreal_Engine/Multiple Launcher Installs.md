# Multiple Launcher Installs

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multiple-launcher-unreal-engine-installs](https://dev.epicgames.com/documentation/en-us/unreal-engine/multiple-launcher-unreal-engine-installs)  
**Processed:** 2025-06-14 16:37:39

---

Installing the **Epic Games Launcher** and **Unreal Engine** on multiple computers can be time-consuming and difficult to maintain, especially for IT staff and developers managing dozens or even hundreds of computers in academic, office or Internet cafe environments. To help those users, we updated the Launcher with functionality that makes it easier to set up and update applications, such as Unreal Engine (UE). The following overview describes how to install the Launcher on multiple computers so that you can set up and maintain applications with ease. 

By the end of this document, you will learn how to enable **Launcher PCB Mode** and if necessary, you will know how to set the **Windows Registry Install Path Override** after enabling the PCB Mode feature.

At this time, these features are only supported on the Windows operating system.

## Launcher PCB Mode

On Windows, the Launcher typically stores manifest, dynamic, and temporary files in the system's **ProgramData** folder (for example, `%programdata%\\Epic` or `C:\ProgramData\Epic`). Often, if an office, academic, or Internet cafe administrator installs the Launcher and Unreal Engine on a server without mirroring the program data to client machines, they will encounter installation issues, including a client's inability to find game installs and re-installs of applications.

Sometimes, system administrators need to run a series of complicated steps to mirror the program data folder onto client machines. To simplify their workflow, the Launcher now supports **PCB Mode**. After enabling PCB Mode, the Launcher stores the program data folder inside of its install folder. Internet cafe owners, for example, will be able to set up the Launcher once on the server machine, such that the server's install folder will be cloned to its clients. With all of the program data files in the install folder, no additional work is necessary.

If you have never installed UE before, take some time to read through our initial installation guide, which goes through the basics of [Installing Unreal Engine](/documentation/404).

### Enabling Launcher PCB Mode

Follow these steps to enable Launcher PCB Mode:

1.  Install the Launcher on at least one machine (this can be a server). Later on, we will call this machine the 'original computer'.
    
2.  Before moving onto the next step, make sure that the Launcher is closed.
    
3.  To enable **Launcher PCB Mode**, move (or copy) the **Epic** folder into the Launcher's install directory. For illustrative purposes, we are moving the Epic folder from `C:\ProgramData\Epic` to `C:\Program Files (x86)\Epic Games\Launcher`.
    

![Relocatinf Epic Folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aec45671-5d7f-4246-9ffe-7ba5ab76af42/ue5-relocate-epic-folder.png)

PCB Mode attempts to simplify a user's workflow for installing multiple Engines from a Launcher. Read through the Launcher PCB Mode section to learn more about this new Launcher mode.

1.  Using the Launcher, install the engine(s)-of-choice into the new computer(s).
    
2.  Finally, copy the Launcher's and Engine's install directory to the new computer(s).
    

If the new computer's Engine install path is different from the original computer's path or if the new computer has different drive letters, you need to add a **Registry Install Path Override** after enabling the Launcher PCB Mode.

### Disabling Launcher PCB Mode

To disable this mode, close the Launcher, and move the **Epic** folder from the Launcher's install directory back into the **ProgramData** directory, making sure to restart the Launcher after the move.

We encourage you to move the **Epic** folder rather than deleting it, because if you delete the folder from the Launcher install directory, you will probably lose manifest files (binary files that cannot be modified), which tell the Launcher where your game or application is installed.

## Windows Registry Install Path Override

The Launcher stores game and application install location information in manifest files living in the system's **ProgramData** folder. At this time, if you move an installed game or application to a new location, the Launcher can't discover the moved installs. This can be problematic, especially for users who are moving the Launcher and game (or application) installs to machines that do not have the same drive letter or directory structure as the original install machine. If you find yourself having problems moving (or copying) the Launcher or its installs onto new machines, you may need to specify a registry install path override to point to the copied or moved game or application folder.

Typically, registry install path overrides are used with PCB Mode.

Install path (InstallLocation) overrides are specified in the Windows registry on a per game (or per application) basis, and the **InstallLocation** overrides may be added to any one of the following registry locations:

-   `HKEY_LOCAL_MACHINE\SOFTWARE\Epic Games\EpicGamesLauncher\Overrides`
-   `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Epic Games\EpicGamesLauncher\Overrides`
-   `HKEY_CURRENT_USER\SOFTWARE\Epic Games\EpicGamesLauncher\Overrides`
-   `HKEY_CURRENT_USER\SOFTWARE\WOW6432Node\Epic Games\EpicGamesLauncher\Overrides`

The next section uses the [Registry](https://docs.microsoft.com/en-us/windows/desktop/sysinfo/registry) Editor in Windows 10.

### Adding a Registry Install Path Override

Perform the following steps to add a Registry Install Path Override:

1.  In the search bar on the taskbar, type `regedit`.
    
2.  Select the **regedit Run command** to open the **Registry Editor**.
    
    You are going to use the **Registry Editor** to add the InstallLocation Override Subkey, which can be added to any one of the registry locations being listed in the Registry Install Path Override section. For the purposes of illustration, we are adding the Subkey to the following Key:
    
    `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Epic Games\EpicGamesLauncher\Overrides`
    
3.  Navigate to the following registry location: `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Epic Games\EpicGamesLauncher`, making sure to select the **EpicGamesLauncher** Key.
    
4.  To create a new Subkey for the **EpicGamesLauncher** Key, select the **Edit** menu, hover over the **New** option, and select the **Key** command.
    
5.  Name the new Subkey, `Overrides`.
    
6.  Now, repeat the previous two steps to create a new Subkey for Overrides, which you'll name `UE_(Engine Version)`.
    
    The registry path's format must include UE's mandatory folder name, which you can find in the Launcher's **Install Dialog**. As you can see in the following image, the mandatory folder name for this example is `UE_5.0`:
    
    ![LauncherInstallDialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08bd3f4f-f9c4-4dba-ac10-3b019b49509e/ue5-launcer-install.png)
7.  Select the **Edit** menu, hover over the **New** option, and select the **String Value** command.
    
8.  Name the new String Value name, `InstallLocation`.
    
9.  Finally, define the data value for **InstallLocation**, matching UE's mandatory folder name. In this example, we are using `C:\Epic Games\UE_5.0`.
    
    ![(Install Location Override](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4707f607-600a-4738-9dec-4751fb04378d/ue5-install-location.png)
    
    The Launcher only reads registry values once on start-up, so if you update the registry, you need to restart the Launcher for it to discover the changes.