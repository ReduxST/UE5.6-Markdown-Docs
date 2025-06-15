# Source Control

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/source-control-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/source-control-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:41

---

The Unreal Editor has built-in support for source control packages. Source control is used to manage changes over time to code and data, and enables teams to coordinate their game development efforts.

Perforce and SVN are supported by default.

## Activating Source Control

You can activate source control in one of two ways:

-   In the Level Editor's **Preferences** window.
-   In the **Content Browser**.

### Activating Source Control via Editor Preferences

You can activate source control via the Editor Preferences window (**Edit > Editor Preferences > Loading & Saving**).

![SourceControlPreferences.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39c2a7fc-a673-4f4e-a13f-b7f95d90ca44/sourcecontrolpreferences.png)

| Item | Description |
| --- | --- |
| **Automatically Checkout on Asset Modification** | When checked, this will automatically check out any asset that has been modified. |
| **Prompt for Checkout on Package Modification** | When checked, a prompt will appear when you make changes to a source controlled-package, asking if you would like to check out (lock) that package. |
| **Add New Files when Modified** | This will add new files into source control when they are modified. |
| **Use Global Settings** | Use global source control login settings, rather than per-project. Changing this will require you to login again. |
| **Tool for diffing text** | Specifies the file path to the tool to be used for diffing text files. |

### Activating Source Control via the Content Browser

You can also activate Source Control in the **Content Browser**. To do so, right-click any asset or folder. At the bottom of the context menu, in the **Source Control** section, click **Connect to Source Control**.

![Connect to Source Control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33efedc5-913f-47ac-9cf1-dadf6c2acb0a/cb_sourcecontrol.png)

This will open a log-in screen where you can select your source-control system and enter any appropriate settings and other information.

![Source Control Login](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/726962f0-8ff8-47d4-b001-978443d2a7ff/cb_sourcecontrollogin.png)

Enter the appropriate information, and click **Accept Settings**. After source control is activated, the display of the assets in the **Content Browser** will change to reflect their source-control status, and some source-control options will be included on the right-click context menu.

## Status Icons

The **Content Browser** will display special icons on the upper-right corner of assets to give the source control status. Below are the available icons and their meanings:

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
| ![CheckedOutByYou.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9162b98-19f8-45fa-b325-84eaf84d1d71/checkedoutbyyou.png) | ![CheckedOut.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cee5894-a385-492a-a847-d6ef6c77a188/checkedout.png) | ![MarkedForAdd.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6642602e-22f4-4ad9-b980-61709bd3d26d/markedforadd.png) | ![NotInTheDepot.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a695e96c-d5b2-4747-a182-435bdbe87ca2/notinthedepot.png) | ![NotHeadRevision.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14ba5f3e-aaad-4e56-b0b2-ace21fd25657/notheadrevision.png) |
| Checked out by you | Checked out by another user | Marked for add | Not in depot | Newer version of file exists in source control |

## Source Control Actions

While source control is active, the following context menu will be available when you right-click on an asset:

![SourceControlMenu.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04963f53-4f68-4dd2-b4a3-e5a4ac0bb51c/sourcecontrolmenu.png)

| Item | Description |
| --- | --- |
| **Check Out** | Checks out (locks) the asset for editing. This prevents other users from editing the asset at the same time. |
| **Refresh** | Refreshes the source control status of the asset. |
| **History** | Gives a revision history list of the selected asset, allowing you to see previous edits. |
| **Diff Against Depot** | This allows you to check the asset against the version currently stored in the source control depot. |

## Checking Out and Checking In

To check out an asset for editing, simply right-click it and choose **Check Out**. When checking the asset back in, adhere to the following protocol:

-   Right-click on the asset and choose **Check In**. A dialog will appear with a required changelist description for the check-in.
-   Enter a description, which will be added to the asset's revision history.
-   Click **OK** when finished.

![ChangelistDescription.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bbdd703-ec4d-41eb-91f4-34c9e300e03e/changelistdescription.png)

A changelist description is required, so the **OK** button will not be enabled until a description is entered.

## Content Hot Reloading

**Content Hot Reloading** is a new feature that the in-editor source control uses to reload content automatically when the content has been modified by source control operations. Currently, automatic reloading only works when performing source control operations via the in-editor source control integration, and any external changes won't trigger a reload. We intend to remove this requirement in a later engine version, so that external changes will also trigger hot reloads.

Content Hot Reloading also provides the ability to reload an asset from its last saved state on command. This can be done by right-clicking the asset in the **Content Browser** and selecting the **Reload** option under the **Asset Actions** group. This can be extremely useful if you have unsaved changes to an asset that you wish to discard in order to revert back to the on-disk version.

![ContentHotReload.png](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1669afbd-924d-4a94-829d-0e6341676f03/contenthotreload.png) This feature currently carries the requirement that you have source control active for your project.

## Deactivating Source Control

You may find that you want to deactivate source control after activating it.

Only use this option if you are absolutely certain that you do not want to use source control. Deactivating source control will put your content out of sync with your source-control system, and will make it impossible to check in changes.

**To deactivate source control**:

1.  In the upper-right corner of the Level Editor window, click the green double-arrow icon (![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3c8eec0-1bcd-4228-b3fe-a618d803fe3b/icon_sourcecontrol.png)). This brings up the **Source Control Login** screen.
2.  Click the **Run Without Source Control** button. The green icon in the Level Editor window changes to a red circle with a slash (![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9200ce3-129b-43c0-b97a-f674806dd46f/icon_cb_sourcecontroloff.png)), to indicate that source control is not being used.