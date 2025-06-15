# Landscape Manage Mode

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-manage-mode-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-manage-mode-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:13

---

In **Manage** Mode, you can create new Landscapes and use the component tools to modify an existing Landscape's components. You can also select components and modify their properties in the **Details** panel.

For information about creating Landscapes, see [Creating Landscapes](/documentation/en-us/unreal-engine/creating-landscapes-in-unreal-engine).

## Landscape Selection

In the **Landscape** panel, select which Landscape to modify from a list of all the Landscapes currently in your level.

![Image of the Landscape dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bd2b35b-9ac7-4411-a756-cf5096c75862/01-landscape-dropdown-menu.png "Landscape dropdown menu")

**To select a Landscape:**

-   In the Landscape panel click the **Landscape** drop-down box in the **Landscape Editor** section to display a list of all Landscapes currently in the map.
-   Choose the Landscape you want to edit.

Selecting a Landscape from the list makes that the active Landscape. All subsequent editing will then be applied to that Landscape.

## Components

**Components** are the building blocks of any Landscape Actor. You can work with them using the Component tools and adjust their properties individually in the **Details** panel.

### Component Tools

The tools described below act on the component level of the currently selected Landscape.

#### Selection

![The Landscape Select button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6aacfd8-a2af-43c7-b520-5efb33cf5cd0/02-landscape-select-button.png "Landscape Select button")

The **Selection** tool selects Landscape components for subsequent use with other tools, such as moving them to a streaming level or deleting components.

| **Control** | **Operation** |
| --- | --- |
| **Left Mouse Button click** | Toggles the selection of the component. |
| **Shift + Left Mouse Button click** | De-Selects components. |

The selection cursor is always limited to one component:

![Image of the Landscape Selection cursor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5cdf3c13-f899-43ba-95eb-1e2aab1b0603/03-landscape-selection-cursor.png "Landscape Selection cursor")

When components have been selected, they become shaded red:

![Image of selected Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23c6e1d5-0909-49ee-811b-3da516151b92/04-selected-components.png "Image of selected Components")

| Option | Description |
| --- | --- |
| **Clear Component Selection** | Clears the current selected component(s). |

#### Add

![Add Component button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86d97daf-558c-4c4c-82fc-6d5bc94bc1b8/05-add-component-button.png "Add Component button")

The **Add** tool creates new components for the current Landscape, one at a time.

| **Control** | **Operation** |
| --- | --- |
| **Left Mouse Button click** | Adds a new component. |

When the Add Landscape Component tool is active, the cursor shows a green wireframe where new components can be added:

![Image of green wireframe Add Component cursor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2d366ea-375e-416a-9ba6-8a202fb068e2/06-component-cursor.png "Add Component cursor")

Using the tool adds a new component where the cursor is located:

![Adding a Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/706e586f-db00-4a98-b258-33dc12023987/07-adding-a-component.png "Adding a Component")

#### Delete

![Delete Component button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2d1e9ba-c494-4c79-ad31-588d07c7b2ee/08-delete-component-button.png "Delete Component button")

The **Delete** tool deletes any selected components.

| **Control** | **Operation** |
| --- | --- |
| **Left Mouse Button click** | Deletes highlighted components selected by the Selection tool. If no components are currently selected, deletes the component highlighted by moving the mouse cursor over it. |

![Deleting currently selected Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df24c97c-697a-402b-baab-9948e2fa6794/09-deleting-currently-selected-components.png "Deleting currently selected Components")

Using the tool removes the selected components:

![Landscape Components deleted](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28354bc8-2ef0-4592-9e30-43a9d617e6fc/10-landscape-components-deleted.png "Landscape Components deleted")

#### Move Level

![Move Level button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ae75e82-dc1e-43d2-8fdc-5007e2df8622/11-move-level-button.png "Move Level button")

This tool moves the selected components, via using the Selection tool, to the current streaming level. This makes it possible to move sections of a Landscape into a streaming level so that they will be streamed in and out with that level, optimizing the performance of the Landscape.

When the streaming level is visible, the Landscape renders all the components:

![Selection visible in streaming level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7a78cc0-35c4-4322-a8aa-6f8bf67d105e/12-selection-visible-in-streaming-level.png "Selection visible in streaming level")

You can toggle the visibility of the level by clicking the eye icon (![Level Window Eye Icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cefa5cd-88b1-483f-aecb-d7ea94e41073/13-level-window-eye-icon.png "Level Window Eye Icon")) for that level in the **Levels** panel (accessible on the Level Editor's **Window** menu). Doing so causes the components in that level to no longer be rendered:

![Selection not visible](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e1d1573-0978-4944-a708-9a150c46cefc/14-selection-not-visible.png "Selection not visible")

#### Edit Splines

![Edit Splines button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dceb0a8d-dd66-4697-94c9-78186f09e16d/15-edit-splines-button.png)

**Landscape Splines** are a flexible system for creating any linear feature that needs to conform to a Landscape, and can even push and pull the terrain to better facilitate building these features. They are created and edited using the spline tool in the Landscape tool.

![Editing Splines on a Landscape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d815b80-2ece-4d16-8032-610ee3c45d9b/16-editing-splines-landscape.png "Editing Splines on a Landscape")

For information about how to create and modify spline curves, see [Landscape Splines](/documentation/en-us/unreal-engine/landscape-splines-in-unreal-engine).

### Component Properties

You can set the properties of individual components, including LODs and component-specific Materials, in the **Details** panel.

#### Component LODs

You can also set LODs for selected component, which means an individual component can have its own LOD settings.

**To set LODs for selected component:**

1.  Select the components whose LODs you want to set. For information about selecting components, see [Selection](/documentation/en-us/unreal-engine/landscape-manage-mode-in-unreal-engine#selection).
    
2.  In the **Details** panel, under **Landscape Component**, adjust the **Forced LOD** and **LODBias** settings to obtain the desired result.
    
    ![Changing ForcedLOD and LODBias in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d233de9d-41d7-4aad-b1ba-b7487abc8e98/17-landscape-component-lod.png "ForcedLOD and LODBias in the Details panel")

#### Component Material Overrides

You can set a Material Override for selected components, which means that an individual component can have a different Material assigned to it than its Landscape does.

**To set a Material Override for selected components:**

1.  Select the components that you want to use a different Material for. For information about selecting components, see [Selection](/documentation/en-us/unreal-engine/landscape-manage-mode-in-unreal-engine#selection).
    
2.  In the **Content Browser**, find and select the Material you want to use.
    
3.  In the Level Editor's **Details** panel, under **Landscape Component**, click the Assign arrow icon (![Assign](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4cd3e4b4-883f-4f6b-8636-4da9a6b8c4b3/18-assign.png "Assign")) to assign that Material to the selected components.
    
    ![Override Material field in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aee890ca-e400-4033-a73e-1330194877f2/19-override-material-details-panel.png)