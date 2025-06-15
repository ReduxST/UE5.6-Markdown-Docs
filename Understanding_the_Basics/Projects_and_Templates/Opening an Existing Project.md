# Opening an Existing Project

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/opening-an-existing-unreal-engine-project](https://dev.epicgames.com/documentation/en-us/unreal-engine/opening-an-existing-unreal-engine-project)  
**Processed:** 2025-06-14 16:40:13

---

There are several ways to open an existing Unreal Engine project, depending on where it is located and the version of Unreal Engine it was created with.

## Opening Projects from the Epic Games Launcher

In the Epic Games Launcher, click **Unreal Engine** on the left navigation, then click **Library** at the top of the Launcher. You will see a list of all Unreal Engine projects on your local machine.

If you copied a project from another computer or from the Internet, the project will not appear in this list until you have opened it locally at least once. Refer to the **Opening Projects From Disk** section on this page to learn more.

My Projects section of the Epic Games Launcher. Click the image for full size.

Double-click any project thumbnail to open that project.

The Launcher displays the following information for each Project:

-   Project name
-   Project thumbnail
-   Unreal Engine version that the project is compatible with

Right-clicking a project's thumbnail in the Launcher brings up a context menu with the following options:

| **Option** | **Description** |
| --- | --- |
| **Open** | Opens the project in the version of Unreal Engine that it is compatible with. |
| **Show in folder** | Opens the project folder in a new Windows Explorer (Windows) or Finder (macOS) window. |
| **Create shortcut** | Creates a shortcut to the project on the desktop. |
| **Clone** | Creates an exact copy of the project. You can specify the name and location of the new project. |
| **Delete** | 
Permanently deletes the project.

The project files are **not** moved to the Recycle Bin, like they would be if you deleted the project folder from Windows Explorer or Finder. If you accidentally delete a project using this option, you will not be able to recover it.



 |

## Opening Projects from the Project Browser

When you launch any version of **Unreal Engine**, the **Project Browser** displays and opens the **Recent Projects** panel by default. Much like the projects list in the Epic Games Launcher, this section displays all the Unreal Engine projects on your disk.

If you copied a project from another computer or from the Internet, the project will not appear in this list until you have opened it locally at least once. Refer to the **Opening Projects From Disk** section on this page to learn more.

Project Browser in Unreal Engine 5. Click the image for full size.

Double-click any project thumbnail to open that project. Alternatively, click the project to select it, then click **Open**.

The Launcher displays the following information for each Project:

-   Project name
-   Project thumbnail
-   Unreal Engine version that the project is compatible with

Right-clicking a project's thumbnail in the Project Browser brings up a context menu with an option to open your project folder in a Windows Explorer or Finder window.

Enable the **Always load last project on startup** checkbox in the bottom-left corner of the Project Browser to have Unreal Engine 5 always open the last project you worked on when you launch the engine.

## Opening Projects from Unreal Engine

In **Unreal Engine**, from the main menu, go to **File > Open Project**. This opens a window that displays a list of local projects, similar to the **Project Browser**.

Opening a project from Unreal Engine. Click the image for full size.

To open a project, either:

-   Select the project from the list, then click **Open**.
-   Double-click the project thumbnail.

If the project you want to open for isn't in the list, click **Browse**, then browse to the project folder and open the `(ProjectName).uproject` file.

Opening a project with a different version of Unreal Engine than the one it was created in can lead to data corruption and data loss. It is recommended to open a copy of the project to preserve the original.

## Opening Projects From Disk

If you copied a project from another computer or from the Internet, the project will not appear in this list until you have opened it locally at least once.

To open a project from disk, follow these steps:

1.  Make sure you have installed the Unreal Engine version that the project was created with.
    
2.  Navigate to the project's folder on disk.
    
3.  Double-click the `(ProjectName).uproject` file. This file is located directly inside your project's folder.
    

![Opening an Unreal Engine project from disk](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4beffea5-7abc-415d-a80d-ba2f36c91756/open-project-from-disk.png)

In this example, you would double-click the MyProject.uproject file.

If you don't have the version of Unreal Engine that the project was created with, you will see a pop-up window asking you to select which version of Unreal Engine to open the project with.

![Selecting a version of Unreal Engine to open a project with](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a471884b-cbca-413c-8807-8bfc9e132a43/select-ue-version.png)

Select an Unreal Engine version from the drop-down, or click the **ellipsis** (**...**) button to browse to an Unreal Engine executable on your disk, then click **OK**.

Opening a project with a different version of Unreal Engine than the one it was created in can lead to data corruption and data loss. It is recommended to open a copy of the project to preserve the original.