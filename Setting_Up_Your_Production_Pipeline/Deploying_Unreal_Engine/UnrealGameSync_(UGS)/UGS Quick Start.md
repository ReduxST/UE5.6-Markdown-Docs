# UGS Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-quick-start-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-game-sync-quick-start-guide)  
**Processed:** 2025-06-14 16:57:20

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bbca8a2-21f0-4716-a36f-b52206ca3ed7/ugs-quick-start-top-image.png "ugs-quick-start-top-image.png")

The goal of this guide is to show you the primary workflow of syncing your **Unreal Project** (`.uproject`) using **UnrealGameSync (UGS)**. After working through this tutorial, you will know how to open an Unreal Project with UGS, and how to sync from the **Project Overview** and **Changelist Areas** of the application's main menu.

**Required Setup:** The following steps assume that your team has distributed and set up UGS on your machine or machines.

## 1 - Opening a Local File

The following steps show you how to open a local Unreal Project file with UGS.

1.  To open a `.uproject` on your local drive, click the **Open project...** link.
    
    ![Unreal Game Sync start page](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d80360cc-cb1a-47be-a8fe-908eadd78837/ugs-quick-start-step-1-1.png)
2.  When the **Open Project** window opens, UGS enables the **Local File** radio button by default. To select a local file, click the **Browse...** button.
    
    ![Open Project window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9c4d49a-ae96-4f45-b507-cae8ca98d14c/ugs-quick-start-step-1-2.png "ugs-quick-start-step-1-2.png")
3.  Navigate to and select the `.uproject` file before clicking **Open**.
    
    ![Open File Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a3140b1-cc2e-49b7-bf0a-1be16e4dc85b/ugs-quick-start-step-1-3.png)
    
    We are using the [Lyra Sample Game](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine) as an example Unreal Project.
    
4.  To open the Unreal Project with UGS, click the **Ok** button.
    
    ![Open Project window with local file selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/751d98a7-4eeb-4b3c-9d68-9b6f715419a0/ugs-quick-start-step-1-4.png "ugs-quick-start-step-1-4.png")

## 2 - Opening a Workspace File

The following steps show you how to open a workspace Unreal Project file with UGS.

1.  To open a `.uproject` file on your local drive, click the **Open project...** link.
    
    ![Unreal Game Sync start page](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/727e855c-bb7c-403d-b62a-55fb1485c18a/ugs-quick-start-step-2-1.png)
2.  When the **Open Project** window opens, UGS selects the **Local File** radio button by default. Select the **Workspace** radio button to get started.
    
    ![Open Project window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0fb7d48b-cf22-4086-b955-84e25c48508c/ugs-quick-start-step-2-2.png)
3.  The first field that needs to be populated is the Workspace's name. If you already have a Workspace to point UGS to, click the **Browse...** button next to the **Name:** field.
    
    ![Open Project window with Workspace selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19c834fe-4c3e-49b4-9653-4e271b248a65/ugs-quick-start-step-2-3.png)
    
    If you need to create a new Workspace, click the **New...** button to set up a New Workspace.
    
    ![New Workspace Setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/539e33e5-6432-421e-a78e-e19bcca7cc3f/ugs-quick-start-step-2-3-note.png)
4.  When the **Select Workspace** menu opens, it will show you a list of Workspaces that you can choose from. Go ahead and select a **Workspace (1)** and click the **Ok** button **(2)**.
    
    ![Select Workspace](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87029a3b-9579-423a-bb8c-d0865396d201/ugs-quick-start-step-2-4.png "ugs-quick-start-step-2-4.png")
5.  Now, click the **Browse...** button next to the **Path:** field.
    
    ![Open Project window with Workspace field populated](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbb7bbd2-145b-4637-ab82-07da974b15bc/ugs-quick-start-step-2-5.png "ugs-quick-start-step-2-5.png")
6.  With the **Select Project** menu open, expand the Workspace tree, select the `.uproject` file **(1)**, and click the **Ok** button **(2)**.
    
    ![Select Project menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02bf1e23-1ca9-410d-8e9c-9f0124281f1e/ugs-quick-start-step-2-6.png "ugs-quick-start-step-2-6.png")
    
    We are using the [Lyra Sample Game](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine) as an example Unreal Project.
    
7.  Now that you have specified the **Workspace Name** and **Path**, you are ready to open the Unreal Project with UGS by clicking the **Ok** button.
    
    ![Open Project window with both Workspace Name and Path selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e4acbb0-c57c-4c97-9409-cd583308c626/ugs-quick-start-step-2-7.png "ugs-quick-start-step-2-7.png")

## 3 - Syncing from the Changelist Area

Now that you have opened a project with UGS, you will want to perform a common task with UGS, syncing from the **Changelist Area**.

Make sure that you have logged into **Perforce** before proceeding with the following steps.

1.  Now that you have opened your project with UGS, locate the **Changelist Area** in the **Main Menu**.
    
    ![Unreal Game Sync project tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b90cbf4d-6a60-4742-8185-e2e0e6b018e9/ugs-quick-start-step-3-1.png "ugs-quick-start-step-3-1.png")
2.  Locate the change that you are using, it will have an **arrow icon** next to it.
    
    ![Project tab with current change indicated by arrow icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9844ccc5-11c9-4cca-af10-2c03f42acb06/ugs-quick-start-step-3-2.png "ugs-quick-start-step-3-2.png")
3.  To update to another change that was committed to the project's stream, double click on the other change while inside of the **Changelist Area**.
    
    ![Project tab with another change selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/136bd8d9-93e8-42c1-8dfe-bfcac1d69bfc/ugs-quick-start-step-3-3.png "ugs-quick-start-step-3-3.png")

When the sync finishes, UGS updates the **Output Log (3)**, the **Changelist Area (2)**, and the **Project Overview Area (1)**, which is where you will sync your project from in the next step.

![Project tab with new sync finished](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6014dedd-b667-489c-bff0-fa2567d12ac2/ugs-quick-start-step-3-4.png "ugs-quick-start-step-3-4.png")

## 4 - Syncing from the Project Overview Area

Now that you have performed a sync from the **Changelist Area**, having already opened the project with UGS, you will want to perform another common task with UGS, syncing from the **Project Overview Area**.

1.  First, locate the **Project Overview Area** in the **Main Menu**.
    
    ![Project tab with Project Overview Area highlighted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a70598e-8770-4f55-96f3-0019ddf980a6/ugs-quick-start-step-4-1.png "ugs-quick-start-step-4-1.png")
2.  Click the **down arrow** button next to the **Sync Now - To...** button link to open the shortcut menu.
    
    ![Project tab with Sync Now - To... button highlighted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acfbfd7d-51af-430d-8e40-3a8d489a8b17/ugs-quick-start-step-4-2.png "ugs-quick-start-step-4-2.png")
3.  Now, select the **Latest Change** option.
    
    ![Project tab with Latest Change selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5330af30-6f7f-4877-8a1a-9c0a7f62d022/ugs-quick-start-step-4-3.png "ugs-quick-start-step-4-3.png")
    
    To learn more about navigating the interface, options, and menus built into UGS, check out the [UGS Reference](/documentation/en-us/unreal-engine/unreal-game-sync-reference-guide-for-unreal-engine) Guide.
    

At the end of the sync, UGS will notify you that you have successfully updated to the latest **Change**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/132e86bc-ba8d-434f-82ed-044e313d884b/ugs-quick-start-step-4-end.png "ugs-quick-start-step-4-end.png")

You have now reached the end of this guide, where you learned how to open a project and how to sync it from the **Changelist** and **Project Overview Areas** of the user interface. If you want to continue learning more about UGS on your own, including how to deploy a binary version of your project or how to navigate the interface with all of its menus and options, check out the next section of this guide.

## 5 - On Your Own!

Now that you have opened your project, having performed a couple of common sync methods with UGS, try the following:

-   Enable the **Build** and **Run** check boxes, which are found at the bottom of the UGS main menu to sync, build, and run your Unreal project.
    
    ![Unreal Editor opened after selecting Build and Run](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6ce451e-fb4b-492e-9871-fd756c23acfc/ugs-quick-start-step-5.png "ugs-quick-start-step-5.png")
-   If you are a developer looking to make use of the precompiled binaries feature for Creators who do not need to compile from source, read through the [UGS Reference](/documentation/en-us/unreal-engine/unreal-game-sync-reference-guide-for-unreal-engine) guide for more information on how to set up your build system to periodically submit a zip file containing Editor binaries to Perforce, enabling UGS to extract it to your creative's workspace.