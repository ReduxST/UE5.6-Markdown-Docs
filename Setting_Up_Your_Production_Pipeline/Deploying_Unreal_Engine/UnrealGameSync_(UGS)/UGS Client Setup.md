# UGS Client Setup

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-client-setup-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-client-setup-for-unreal-engine)  
**Processed:** 2025-06-14 16:57:15

---

This guide will go over the simplest route to setting up the **UnrealGameSync (UGS) client** for a new user, but if you need more detailed information or additional methods, check out the [UGS Quick Start](/documentation/en-us/unreal-engine/unreal-game-sync-quick-start-guide) guide. This also assumes that your team has already set up their Perforce server, added all the proper source and content files, installed the proper version of Perforce on the machines you will use UGS with, and have distributed UGS to members who will use it.

If you need additional setup information, please refer to the [UGS Overview](/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine).

1.  Before you install UGS, confirm that you have [set up a Perforce Workspace](/documentation/en-us/unreal-engine/using-perforce-as-source-control-for-unreal-engine#settingupalocalworkspace) and have pointed it to the stream that you want to sync your project from. Try to make the local path to your workspace as short as possible.
    
    Perforce (P4) setup is normally done by someone who has experience with the version control system, and has experience with using it with **Unreal Engine (UE)**. If you are experiencing issues seeing files in Perforce, and have all the proper permissions, this may be due to having an out of date version of Perforce that does not handle the modern features used in Epic's tools. 2020.1 has been confirmed to work with UGS, but even more recent versions could as well.
    
2.  Run the **UGS Installer** that was distributed by the owner of UGS at your studio. Make sure you have administrator privileges when running it.
    
3.  When UGS starts up, you will see this UI:
    
    ![Unreal Game Sync start up user interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c11501d1-53ca-451a-8216-b41e2d3d89d1/ugs-cs-start-up.png)
    -   In the **Server** and **User** fields, enter your Perforce connection settings that you use for connecting through P4V.
        
    -   Set the **Depot Path** to where your binaries for UGS are being stored on Perforce.
        
    -   After you've confirmed that these fields match your Perforce credentials and the location of the UGS binaries, click **Connect**.
        
4.  After UGS successfully connects to your Perforce server, you will see the **Getting Started** menu. Click **Open Project**.
    
    ![Open a project in unreal game sync](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c98dc79-7c76-420a-84e3-3b9b41039e58/ugs-cs-open-project.png)
5.  In the **Open Project** dialog box, click **Browse** and look for the Workspace you set up in step 1.
    
    After clicking **Open Project** you can safely follow the [Workspace](/documentation/en-us/unreal-engine/unreal-game-sync-quick-start-guide#2-openingaworkspacefile) method detailed in the [UGS Quick Start](/documentation/en-us/unreal-engine/unreal-game-sync-quick-start-guide) Guide to get your project open. If you'd like to use the **Local File** method instead, see the [Local File section of the UGS Quick Start Guide](/documentation/en-us/unreal-engine/unreal-game-sync-quick-start-guide#1-openingalocalfile). The steps are also described here with updated screenshots.
    
    ![Click Browse next to the Name field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f254b570-ef10-45b1-b814-86e17a0f2e16/ugs-cs-browse-1.png) ![Select a workspace](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db587ace-773d-4081-8d24-3cbf3ae1219e/ugs-cs-browse-2.png)
    
    Depending on how the Workspace was set up, you may need to uncheck **Only show workspaces for this computer** in the bottom left to see your workspace.
    
6.  Now that you've selected your previously created workspace, click **Browse** next to the **Path** field, and select either a `.uprojectdirs` file (shown by enabling **Show \*.uprojectdirs files** in the **Select Project** dialog), or a `.uproject` file from within one of the projects in that stream. For this example we'll be using a `.uprojectidirs` file, but you can just as easily select a `.uproject` file.
    
    ![Click Browse next to the Path field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d65c5af2-1d56-4d9c-b8f1-6c0fc0f54f3a/ugs-cs-browse-path.png) ![Select a project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9d1b19b-fe7f-443a-b0b7-85e5b1238b41/ugs-cs-projects.png)
    
    After this, the **Path** field will be filled in and you can click **Ok** to continue.
    
    ![Click OK](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81d00e95-793f-4024-8e55-62cb4b8c30a9/ugs-cs-ok.png)
7.  Before proceeding to sync everything to your machine and build / run your project, review the [UGS Sync Filter Setup](/documentation/en-us/unreal-engine/unreal-game-sync-filters-for-unreal-engine) documentation, to see if **Sync Filters** will help your workflow.
    
    Sync Filters are helpful for making sure that you're not syncing more data than you need. For example, if you have multiple large projects in the same stream, you can set up a filter to sync only the one you need to work on. These are very powerful, but they can lead to unintended consequences if they're too widely applied. Use them with care, and if in doubt, double check them with someone on your team that's comfortable with using sync filters.
    
8.  After opening your project, you will see the main menu, which is typically where you'll be working from day-to-day.
    
    For a full overview of this menu, refer to the [UGS Menus Overview](/documentation/en-us/unreal-engine/unreal-game-sync-menu-reference-for-unreal-engine) documentation.
    
    Sync to the latest changelist for your build either by double-clicking the top-most changelist in the **Changelists** area by clicking **Sync Now** in the **Project Overview** area.
    
    Select **Latest** in the **Changelists** area:
    
    ![Select the latest changelist](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92ea0d83-7e96-4b1c-b333-6496507e3f03/ugs-cs-latest.png)
    
    Click **Sync Now**:
    
    ![Click Sync Now](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8354788-b770-44da-8842-45434a5ec7bb/ugs-cs-sync-now.png)
    
    The options for **To…** that apply to what changelist **Sync Now** syncs are **Latest**, **Latest Good**, and **Latest Starred** which are the absolute latest, the latest approved, and latest manually marked builds, respectively.
    
9.  After your project is synchronized, you should be able to open the project in Visual Studio using the **Visual Studio** option in the **Project Overview** area, or open the project's Editor using the **Unreal Editor** option in the same area, if you're using precompiled binaries or you've built the Editor.
    
    You may be prompted to build the project if you haven't before when opening the Editor, and you're not using [precompiled binaries](/documentation/en-us/unreal-engine/using-precompiled-binaries-in-unreal-game-sync-for-unreal-engine).
    
    ![Open the project in Visual Studio or Unreal Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee7748a3-a963-423c-904f-81c3aa14afe0/ugs-cs-ue-or-vs.png)
    
    You can make building, opening the Visual Studio project, and running the project happen automatically using the **After syncing** options at the bottom of the window.
    
    ![After syncing options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6ad76f9-1035-450d-b6bc-ed25cd2e253e/ugs-cs-after-sync.png)