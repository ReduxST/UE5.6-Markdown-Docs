# Content Browser Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-browser-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:24

---

The **Content Browser** is divided into the following areas:

![Areas of the Content Browser window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70c4db53-ac9f-44f0-845e-33464b63940a/ue5_1-content-browser-areas.png)

| **\*Number** | **Name** |
| --- | --- |
| 1 | Navigation Bar |
| 2 | Sources Panel |
| 3 | Collections |
| 4 | Filters |
| 5 | Search Bar |
| 6 | Asset View |
| 7 | Settings Button |

## Navigation Bar

The **Navigation Bar** contains controls for working with Assets, navigating back and forward between folder paths, and shows a breadcrumb trail path for the folder that is currently open.

![Navigation Bar in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49757298-d433-4ab5-8da0-0009bebbd89d/content-browser-navigation-bar.png)

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | **Asset Control Buttons** | 
These buttons have the following functionality:

-   **Add**: Click this button to add existing Assets to your project or create a new Asset.
-   **Import**: Click this button to open a file browser and select one or more Assets to add to your project.
-   **Save All**: Click this button to save all Assets that have unsaved changes.

To learn more about importing Assets to your project, refer to the [Importing Assets Directly](/documentation/en-us/unreal-engine/importing-assets-directly-into-unreal-engine) page.



 |
| 2 | **History Back and Forward Buttons** | These buttons function like the Back and Forward buttons in a web browser. Use them to navigate back and forward between recent file paths. |
| 3 | **Breadcrumb Trail Path** | This section shows the current folder path. Click any folder to quickly navigate to it. |

## Sources Panel

The **Sources** panel contains a list of all folders inside your Unreal Engine project.

![Sources Panel in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87464acb-948e-4385-a449-1ce11eb28778/content-browser-sources-panel.png)

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | **Favorites Panel** | This panel contains references to Assets that you have added to your Favorites. |
| 2 | **Project Name** | This is the name of the project that is currently open. Click the arrow next to the project name to collapse or expand the folders list. |
| 3 | **Search Buttons** | Click this button to open the Search bar, which you can use to narrow down the list of available folders in the button's associated panel by entering search criteria. Folders are filtered down in real time to only those whose names include the characters you enter. |
| 4 | **Asset Tree** | 
This hierarchical list shows all folders in your Unreal Engine project. It behaves the same as the folder tree in Windows Explorer or the Finder in macOS. To expand or collapse a folder, click the arrow next to its name.

You can exclude folders from the Asset Tree by prefixing the search text with a hyphen (-). For example, entering -anim in the Search box hides any folder whose name contains that string, such as Animation or Animator.



 |

For more information about the Sources panel, refer to the [Sources Panel Reference](/documentation/en-us/unreal-engine/sources-panel-reference-in-unreal-engine) page.

## Collections

The **Collections** panel displays a list of all the Collections you have access to.

![Sources Panel in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/648224d1-bed5-4bef-a8cd-90e1fa883b08/content-browser-collections.png)

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | **Collapse / Expand Button** | Click this button to collapse or expand the Collections area. |
| 2 | **Add Collections Button** | Click this button to create a new Collection. |
| 3 | **Search Buttons** | Click this button to open the Search bar, which you can use to narrow down the list of available Collections by entering search criteria. Collections are filtered down in real time to only those whose names include the characters you enter. |
| 4 | **Collections List** | An alphabetical list of all Collections in this project. |
| 5 | **Asset Count** | Shows the number of Assets in each Collection. |

For more information on Collections and their use, refer to the [Filters and Collections](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine) page.

## Filters Column

The **Filters** column contains all built-in and custom filters for the user that is currently logged in. Click a filter to enable or disable it.

![Filters column in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1a713c1f-cf73-4f84-8f9e-bdf24eb37385/ue5_1-content-browser-filters.png)

For more information on working with filters, refer to the [Filters and Collections](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine) page.

## Search Bar

The **Search** bar provides a wide range of functionality for quickly locating Assets based on their name and type. The **Asset View**, which displays the contents of the folder you select in the **Sources** panel, updates dynamically based on the parameters you enter here.

![Search bar in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/711a878f-7ed4-4dda-9a26-a6139015ee82/ue5_1-search-and-filters.png)

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | **Filters Button** | 
Click this button to open the Filters menu, which you can use to customize the kinds of Assets that display in the Asset View.

For more information on working with filters, refer to the [Filters and Collections](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine) page.



 |
| 2 | **Search Bar** | Use the Search bar to search for Assets by name. Assets are filtered down in real time to only those whose names include the characters you enter. |
| 3 | **Save Search Button** | Click this button to save your current search as a new filter or Collection. This is useful if you want to run the same search again in the future. |
| 4 | **Previous Searches Button** | Click this button to see a list of previous searches. |

## Asset View

The **Asset View** shows all available Assets within the currently selected folder or Collection.

From the Asset View, you can:

-   Drag and drop Assets directly into the Level.
    
-   Create and import Assets from the **context menu** that opens when you right-click inside the Asset View.
    
-   Create new folders.
    

![Asset View in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97197110-e198-4742-995c-c07fb528ee01/content-browser-asset-viewer.png)

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | **View Area** | This shows all of the Assets in the currently selected folders or Collections after all filters and search criteria have been applied. |
| 2 | **Asset Count** | Shows the current number of assets displayed once all filters and searches are applied. |

## Settings Button

![Settings button in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c237e77-87a4-4839-9e6e-0401cd300b38/content-browser-settings-button.png)

This button opens the **Settings** menu, where you can adjust the following settings for the Content Browser:

-   View style (how Assets are displayed: Tiles, Lists, or Columns).
    
-   Search filters.
    
-   Content to include or exclude.
    
-   Search options.
    

For more information, refer to the [Content Browser Settings Reference](/documentation/en-us/unreal-engine/content-browser-settings-in-unreal-engine) page.