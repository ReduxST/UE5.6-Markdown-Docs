# UGS Menu Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-menu-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-menu-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:57:18

---

This page provides a reference for the menus and options available in **UnrealGameSync (UGS)**.

![Unreal Game Sync main screen](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88e2810e-38ab-4672-8e05-e53daa16b51d/ugs-menu-main.png)

## Project Overview

Provides information about:

-   The stream opened.
-   The local path to the `.uproject`/`.uprojectdirs` file.
-   The latest sync status.

| Option | Description |
| --- | --- |
| **Settings** | Change what file is being used to open the project. |
| **Sync Now** | 
Sync the project using the **To…** setting:

-   **Latest Change**: Sync to the absolute latest, could be unstable.
-   **Latest Good Change**: Sync to the latest change that has been used by another member of the organization (requires a metadata server).
-   **Latest Starred Change**: Sync to the latest change marked by someone using the **Add Star** context menu option in the **Changelist** area.



 |
| **Unreal Editor** | Run the project in the editor. Leverages the **Precompiled Binary (PCB) editor** when available. |
| **SDK Info** | View SDK availability in the stream. |
| **Perforce** | Open the stream in **Helix Visual Client (P4V)**. |
| **Visual Studio** | Open the project in **Visual Studio**. |
| **Windows Explorer** | Open the project in **Windows Explorer**. |
| **More -> Clean Workspace** | Clean the **Perforce** Workspace |
| **Show Log** | Show the log of the latest sync in the **Log** section. Available upon a failed or cancelled sync operation. |

## Changelists

Sync to a particular changelist, and view information about each changelist.

| Option | Description |
| --- | --- |
| **Type** | Code change, content change, or both. |
| **Change** | The changelist number in Perforce. |
| **Time** | Identifies when the change was submitted. |
| **Author** | Identifies who submitted the change. |
| **Description** | The description of the changelist written by its author. |
| **CIS** | The status of the **Continuous Integration System (CIS)** merge after this change. Requires a metadata server. |
| **Status** | Identifies who is currently using the build from a changelist, and their status with it. Requires a metadata server. |

### Right-Click Context Menu

Different options are available for each changelist, some of which are replicated from the Project Overview Area.

![Changelist right-click context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63335957-0848-4339-81f9-e2f41c340e68/ugs-changelist-context-menu.png)

| Option | Description |
| --- | --- |
| Currently Synced Changelist |   |
| **Launch Editor** | Available if the editor has been previously built for the given changelist. |
| **Build** | Build the changelist. |
| **Rebuild** | Rebuild the changelist. |
| **Generate project files** | Generate project files. |
| **Open in Visual Studio** | Opens the changelist in Visual Studio. |
| General Options |   |
| **Sync** | Sync with Perforce. |
| **Sync (Just this Change)** | Does not pick up changes in between the currently synced changelist and the selected changelist. |
| **Mark as good** | Visible to other users. Requires a metadata server. |
| **Mark as bad** | Visible to other users. Requires a metadata server. |
| **Withdraw review** | Cancels **Mark as good** or **Mark as bad**. Requires a metadata server. |
| **Leave comment** | Leave a comment that is visible to other UGS users. Requires a metadata server. |
| **Start investigating** | Mark the changelist as bad, along with all following changelists, and open up an investigation. Requires a metadata server. |
| **Add Star** | Add a star to the build that others can see, meaning it's a special or approved build. Requires a metadata server. |
| **Copy Changelist** | Copy the changelist number to your clipboard. |
| **More Info…** | Open the changelist in P4V. |

## Log

The log of the current sync operations, including Perforce operations and build operations. The right-click context menu allows for selecting and copying from the log.

## Filter Menu

![Unreal Game Sync filter menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1f2fb08-f94a-4c04-9e32-e57a2037c6b0/ugs-filter.png)

| Option | Description |
| --- | --- |
| **Type** | Switch between code and content changelists, or both (default). |
| **Badges** | Filter based on CIS badges. |
| **Show Build Machine Changes** | Show build machine changelists as well as user changelists (off by default). |

## After Sync Options

![Unreal Game Sync after sync options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbec05e7-93f8-4662-9651-de3f8c727ea1/ugs-after-sync.png)

| Option | Description |
| --- | --- |
| **Build** | Use **Unreal Build Tool (UBT)** to build the project automatically in the **Editor Build Configuration** selected from the **Options** menu. Default is **Debug**. |
| **Run** | Automatically runs the output of the build step upon a successful build. |
| **Open Solution** | Open the solution in Visual Studio automatically after generating the project files. |

## Options Menu

![Unreal Game Sync Options menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/343a2575-4e52-46f9-b40b-dded64167096/ugs-options.png)

| Option | Description |
| --- | --- |
| **Application Settings** | Refer to the [Application Settings](/documentation/en-us/unreal-engine/unreal-game-sync-menu-reference-for-unreal-engine#applicationsettings) table. |
| **Scheduled Sync** | 
Set what projects are synced and built, what changelist type, and when:

![Unreal Game Sync scheduled sync settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ffe175f5-e937-45fa-874a-c8dc348411b9/ugs-sched-sync.png)

This can also be used to turn off the scheduled syncs.



 |
| **Sync Precompiled Binaries** | Sync PCBs automatically if available. |
| **Auto-Resolve Conflicts** | Automatically resolve Perforce conflicts. |
| **Sync Filter…** | Open up the sync filter options dialog. For more information on this dialog and its usage, refer to the [UGS Sync Filter Setup](/documentation/en-us/unreal-engine/unreal-game-sync-filters-for-unreal-engine) documentation. |
| **Editor Build Configuration** | Select from **Debug**, **DebugGame**, or **Development**. |
| **Customize Build Steps…** | Refer to the [Custom Build Steps](/documentation/en-us/unreal-engine/unreal-game-sync-menu-reference-for-unreal-engine#custombuildsteps) table |
| **Editor Command Line Arguments…** | 

![Unreal Game Sync command line arguments](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2de5ba57-9e1c-4ec3-8e87-6ff91e918001/ugs-command-args.png)

The **Command Line Arguments** window lets you edit, add, and remove command line arguments, as well as change the order they're passed. You can force this dialog on each launch if you find yourself editing command line arguments repeatedly.



 |
| **Tab Names** | Select from **Stream**, **Workspace Name**, **Workspace Root**, or **Project File**. |
| **Show Changes** | Independently toggle showing changes without reviews and showing changes by automated processes. |
| **Time Zone** | Select either **Local** or **Perforce Server** time. |
| **Diagnostics…** | 

![Unreal Game Sync diagnostics window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/347bbb47-bb3e-4743-91af-fc9c8f65b974/ugs-diagnostics.png)

Open the **Diagnostics** window for UGS. Clicking **View logs** in this dialog will take you to where UGS writes its logs. This can be very useful for diagnosing UGS-related issues.



 |

### Application Settings

![Unreal Game Sync application settings window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d24778c0-4dc5-4289-8def-90a023e04e45/ugs-application-settings.png)

| Setting | Description |
| --- | --- |
| **Startup and Shutdown** | Configure the app to run on startup and keep running when minimized. |
| **Default Perforce Settings** | The credentials UGS will use to log into Perforce. |
| **Updates** | Where the program will look in Perforce to update itself, and if it's acceptable to use an unstable (test) version of the application. |
| **Integration** | Mechanisms for UGS to integrate with other applications and tools. |
| **Custom Tools** | Tools to use along with UGS. |
| **Advanced** | 
![Unreal Game Sync advanced application settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4896ff57-4ac8-4ef7-bffa-98b196c28dee/ugs-advanced-app-settings.png)

| Option | Description |
| --- | --- |
| **Retries on timeout** | How many times to try again after a timeout. |
| **TCP Buffer Size** | The size of the TCP buffer in bytes. |





 |

### Custom Build Steps

The **Custom Build Steps** window lets you modify and add new build steps.

![Unreal Game Sync custom build steps window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/196d31df-92c2-4fde-aa8f-2d48a032636a/ugs-custom-build-steps.png)

| Option | Description |
| --- | --- |
| **Normal Sync** | Run the step every time a user syncs. |
| **Scheduled Sync** | Run the step as part of a scheduled (automatic) sync. |
| **Show as Tool** | The step will be displayed in the **Project Overview**'s **More…** option as a tool the user can run. |
| **New Step…** | Refer to the [New Step](/documentation/en-us/unreal-engine/unreal-game-sync-menu-reference-for-unreal-engine#newstep) table. |

#### New Step

The **New Step** window shows all the fields necessary to define and execute a new build step task.

![Unreal Game Sync New Step window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e38c36e-2c01-4710-a102-ed017289127e/ugs-edit-build-step.png)

| Field / Option | Description |
| --- | --- |
| **Description** | The name or short description of the step. |
| **Status Text** | The status text displayed when running the task. |
| **Approximate Duration** | How long it will take to run the step. |
| **Compile** | Build a target using UBT with the selected configuration, platforms, and additional command line arguments to UBT. |
| **Cook** | Cook through **BuildCookRun** given a specified profile. |
| **Other** | Run a generic executable from a given working directory with a given set of command line arguments. Also allows you to use the log window to show the program's output. |
| **Variables** | 
![Unreal Game Sync Variables window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c9f30f1-efd5-4568-85dd-071697d48bed/ugs-variables.png)

The **Variables** window will open up the environment variables for the task and allows editing them.



 |