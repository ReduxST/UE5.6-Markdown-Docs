# Sources Panel Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sources-panel-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sources-panel-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:44

---

The **Sources** panel, located on the left side of the **Content Browser**, contains a list of all folders and Collections within your Unreal Engine project. You can customize it to include other types of Assets and Asset organization features, and use it to initiate some common editor operations.

When you select one or more folders, collections, or other types of Asset groups from the Sources panel, the **Asset View** panel will display the contents of your selection.

![Sources Panel in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03d3eb60-0d7a-4914-ab99-496869f8fe02/ue5_1-sources-panel.png)

## Toggling the Sources Panel

You can open and close the Sources panel from the **Settings** menu in the upper-right corner of the Content Browser, by enabling or disabling the **Show Sources Panel** option. Closing the Sources panel gives you more space to work with Assets in the **Asset View**.

## Adding and Removing Sources

By default, the **Sources** panel displays two Asset sources to start:

-   A hierarchical list of all folders within your Unreal Engine project, grouped under the **project name**.
    
-   An alphabetical list of Asset **Collections** for the current project.
    

You can also add the following Asset sources:

| **Source** | **Contents** | **How to Add** |
| --- | --- | --- |
| **Favorites** | Assets that you've marked as Favorites by right-clicking them in the Asset View and selecting **Add To Favorites** from the context menu. | From the **Settings** menu, enable the **Show Favorites** option. |
| **C++ Classes folder** | Browseable hierarchy of all C++ classes in Unreal Engine. | From the **Settings** menu, enable the **Show C++ Classes** option. |
| **Developers folder** | Folder you can use to collaborate with other developers on multi-user projects. | From the **Settings** menu, enable the **Show Developers Content** option. |
| **Engine Content folder** | Collection of stock Assets with various contents and functionality. | From the **Settings** menu, enable the **Show Engine Content** option. |
| **Plugin-specific content folders** | Content folders added by various Unreal Engine plugins. | From the **Settings** menu, enable the **Show Plugin Content** option. |
| **Localized content** | Localized content in the `L10N/` folder. | From the **Settings** menu, enable the **Show Localized Content** option. |

## Source-Based Asset Display

The **Asset View** shows Assets from the currently selected source. You can use searches and filters to further control which Assets display in the Asset View.

To see Assets from multiple folders, you must select all the folders you want to search. You can use the following mouse and key combinations to select multiple folders:

-   **Left-click** replaces your current selection with the folder you clicked.
    
-   **Shift + Left-click** selects a range of folders between a start and end point.
    
-   **Ctrl + Left-click** selects or deselects individual folders.
    

## Right-Click Context Menu

If you **right-click** any of the folders within the Sources panel, the following context menu displays.

| **Option** | **Description** |
| --- | --- |
| **New Folder** | Creates a new folder as a child of the currently selected folder. |
| **Show in New Content Browser** | Opens this folder in a new Content Browser window. You can have up to four instances of the Content Browser open at the same time, not including the Content Drawer. |
| Folder Options |   |
| **Add/Import Content** | This submenu offers the same functionality as the Add button on the Content Browser's Navigation Bar. Use it to import or create new Assets in the currently selected folder. |
| **Show in Explorer (Windows)** / **Show in Finder (macOS)** | Opens the folder in Windows Explorer (Windows) or Finder (macOS). |
| **Rename** | Makes the folder name editable so you can change it. Press Enter to save your change, or Escape to cancel the renaming. |
| **Add to Favorites** | Adds the folder to the Favorites section. |
| **Set Color** | Sets the color of the selected folder for organizational purposes. |
| Bulk Operations |   |
| **Save All** | Saves all Assets in the current Folder that have been modified. |
| **Resave All** | Resaves all Assets in the current Folder, whether they have been modified or not. |
| **Delete** | Deletes the current folder and all of its contents. |
| **Fix Up Redirectors in Folder** | Finds referencers to all redirectors in the selected folders and resaves them if possible, then deletes any redirectors that had all their referencers fixed. |
| **Migrate** | Copies Assets found in this folder, as well as their dependencies, to another project's `Content` folder. For more information, refer to the [Migrating Assets](/documentation/en-us/unreal-engine/migrating-assets-in-unreal-engine) page. |
| **Reference Viewer** | Shows a graph of references for the folder. For more information, refer to the [Reference Viewer](/documentation/en-us/unreal-engine/reference-viewer-in-unreal-engine) page. |
| **Size Map** | Show an interactive map of the approximate memory used by the Assets in this folder and everything they reference. |
| **Audit Assets** | Opens an Assets Audit window that displays detailed information about the Assets in the current folder. You can use filters to further refine the information that displays in this window. |
| **Shader Cook Statistics** | Display statistics related to shader cooking. |
| **Validate Assets in Folder** | Validate Assets contained within the folder and flag Assets that have issues. |
| Source Control |   |
| **Connect to Source Control** | Connects this folder to source control. After you have connected this folder to source control, the operations below become available. |
| **Check Out** | Marks the selected folder as checked out, which locks it from edits by other users. |
| **Mark for Add** | Marks the selected folder for addition onto the source control server. |
| **Check In** | Submits all edits and additions, and then unlocks the checked-out folder. |
| **Sync** | 
Syncs all Assets in this folder to the latest version.

This might override any local changes you have made.



 |

| **Option** | **Description** |
| --- | --- |
| **Move Here** | Moves the folder to the new location and removes it from its original location. |
| **Copy Here** | Creates a duplicate of the selected folder in the destination folder. |
| **Advanced Copy Here** | Creates a duplicate of the selected folder in the destination folder, along with its dependencies. Also fixes any dependencies that were broken as a result of the move. |