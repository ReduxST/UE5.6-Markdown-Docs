# Outliner

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/outliner-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/outliner-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:47

---

The **Outliner** panel displays all the Actors within the scene in a hierarchical tree view. Using the Outliner, you can:

-   Select and modify Actors.
-   Search and filter Actors by name, type, and other characteristics.
-   Use advanced search operators to further refine Actor searches.
-   Customize which Actor information to display.

By default, the Outliner panel docks to the right side of the Unreal Editor window. Click the image for full size.

You can have up to four instances of the Outliner and customize the settings for each instance separately. Switch between Outliner instances by right-clicking the Outliner tab and selecting a different Outliner, or go to **Window > Outliner** from Unreal Engine's main menu.

![Multiple Outliners](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9de3bc3-067a-465a-b6c8-e321a74869cf/ue5_1-multiple-outliners.png)

Switching between different Outliner instances.

## Outliner Actions

You can perform the following actions on an Actor in the Outliner:

| **Action** | **Description** |
| --- | --- |
| **Left-click** | Selects that Actor. |
| **Right-click** | Displays the same context menu brought up by right-clicking an Actor in the Viewport. Use this to quickly modify an Actor without having to navigate to that Actor in the Viewport. |
| **Left-click and drag** | Attaches the Actor being Dragged to another Actor. |
| **F** keyboard shortcut | 
With an Actor selected in the Outliner: Focuses that Actor in the Viewport. With an Actor selected in the Viewport: Scrolls the list of Actors in the Outliner to the selected Actor.



 |

## Searching and Filtering in the Outliner

Use the **Search** box in the Outliner to search and quickly filter the list of Actors in the scene. By default, searching displays all Actors with a partial match to the search term. If you use more than one search term, only Actors that match all the terms will appear.

You can use all of the [advanced search syntax](/documentation/en-us/unreal-engine/advanced-search-syntax-in-unreal-engine) operators when searching in the Outliner.

Some of the most common operators are:

| Operator | Action | Example |
| --- | --- | --- |
| `-` | Excludes Actors that match a specific term. | `-Sky` |
| `+` | Forces a term to match exactly, as opposed to a partial match. | `+Sky` will match `Sky` but exclude `Skylight` |

You can save your search as a **custom filter** and access custom filters from the **Custom Filters** category of the **Filter** drop-down. Custom filters are saved globally for each user, which means they are available across all of the streams and projects of the user who created them.

![Filters in the Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/650263ca-7c3d-487c-994a-8ef984a18555/ue5_1-custom-filters-outliner.png)

Filters menu in the Outliner.

**Filtering** Actors in the Outliner works in the same way as [Asset filtering](/documentation/en-us/unreal-engine/filters-and-collections-in-unreal-engine) in the Content Browser.

## Customizing the Outliner

**Right-click** any column header to bring up a context menu where you can select which columns to show or hide in the Outliner by enabling or disabling the checkbox next to the column name.

![Show and hide Outliner columns](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d3c5786f-68c5-4799-b0bc-3523cc44f4a2/ue5_1-show-hide-outliner-columns.png)

Showing and hiding Outliner columns.

Searching matches terms in all columns in the Outliner, whether or not they are visible.

**Left-click and drag** the edge of a column header to resize that column.

The Outliner will always scroll to an Actor when you select that Actor in the Viewport. You can disable thai behavior by toggling **Always Frame Selection** from the Outliner's **Settings** menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20ad67b2-a0c6-4d32-871b-76fcd96d3958/ue5_1-center-actor.gif)

Animated demonstration of the Always Frame Selection option when toggled on or off.