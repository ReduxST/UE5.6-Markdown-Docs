# DMX Control Console

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-control-console](https://dev.epicgames.com/documentation/en-us/unreal-engine/dmx-control-console)  
**Processed:** 2025-06-14 16:20:56

---

The **Control Console** simplifies **DMX** debugging and gives you quick control of a set of fixtures, which can be virtual or physical. It auto-generates and populates faders based on your library and patch selection. You can then use these faders to generate and send DMX data.

![The DMX Control Console](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82a5f515-ffde-414e-a646-67ad0b1dabb8/control-console.png)

## Workflow

To open the DMX Control Console, go to the **Main Toolbar** and click **DMX** > **Control Console**.

![Open the DMX Control Console from the Main Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/960ec640-1d1a-4e57-a065-65161c6163dd/open-control-console.png)

### Library Selection

A Control Console can use a single **DMX Library**. In the **DMX Control Console** details panel, use the dropdown to browse to the DMX Library asset that contains the patch and fixture database to use in the console.

![Select the correct DMX library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f24ac749-4d8e-4895-aee2-47527a385c38/select-library.png)

### Library Layout Options

You can select one of two layout modes for a DMX Library:

-   **Auto**: A layout that auto-generates Fader groups only for selected Fixture Patches. If you select more than one Patch, then multiple Fader Groups will be created and then organized using the global Layout options.
-   **Custom**: A user-defined layout where you manually create Fader groups for Fixture Patches in the right panel.

If you select the Auto layout mode, you can also select **Auto-Group Patches** to automatically create Patch Groups when selecting multiple Patches.

### Patch Selection

The Fixture Patch list shows all the Patches in the current DMX Library. You can toggle each Fixture Patch to enable or disable sending DMX for the specific Patch.

![The Fixture Patch list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df3d800a-b1ba-4be0-ba33-28829a304a78/patch-selection.png)

| Number | Name | Description |
| --- | --- | --- |
| 1 | Search bar | Filter patches in the list by search term. |
| 2 | Filter dropdown | Filter patches in the list and the columns shown. |

The Filter dropdown has the following options:

-   Filter:
    -   All Patches
    -   Only Active
    -   Only Inactive
-   Columns:
    -   Show Name
    -   Show FID
    -   Show Type
    -   Show Mode
    -   Show Patch

![The filter dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/556544b1-d52a-4498-8b4a-401e1dd81437/filter-dropdown.png)

### Add Fixture Patches

In **Auto** layout mode, patches are added to the console by selecting them (see [Layout Options](/documentation/en-us/unreal-engine/dmx-control-console#librarylayoutoptions)).

In **Custom** layout mode, you can add fixture patches to the console by selecting them one by one or already in group form:

-   **\+ Add All Patches**: Add all fixture Patches in the list to Fader groups.
-   **\+ Add Patch**: Add the selected Fixture Patches to the layout.
-   **To the right**: Add the selected Fixture Patches to the right side of the selected row.
    -   **To the next row**: Add the selected Fixture Patches to a new row.
    -   **To selection**: Add the selected Fixture Patches to the selected Fader group, replacing the previous Patch.
    -   **Group to the right**: Add the selected Fixture Patches to a new Fader group on the right side of the selected row.
    -   **Group to the next row**: Add the selected Fixture Patches to a new Fader group on a new row.
-   **\+ Add Empty**: Add an empty Fader group to the layout.
    -   **To the right**: Add an empty Fader group to the right side of the selected row.
    -   **To the next row**: Add an empty Fader group to a new row.

![Buttons and options for adding fixture patches](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28b98b33-7d69-458f-9196-03af8d364af5/add-fixture-patches.png)

When you add a fixture patch to the Console, a **Fader** is created for each of its functions and placed in a **Fader group**. You can inspect a Fader group's details, and edit them where applicable, in the **Details View** on the right side.

![Fader group Details View](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4aed074-d5e8-422a-9db1-a4e0147d8d6f/details-view.png)

### Send DMX Data to Output Ports

To start sending DMX data to external devices, click **Send DMX** in the Control Console toolbar. To stop sending DMX data, click **Stop sending DMX**.

While DMX data is being sent, you can change Fader values and see the changes reflected in real time in Unreal Engine or your fixture.

![The Send DMX button in the Control Console toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b1ef494-a191-462d-a914-2652379df6e8/send-dmx.png)

Sent DMX data can be received back in Unreal Engine, either by adding a corresponding Input Port, or by internal loopback when **Send or Receive DMX** is disabled in the Level Editor Toolbar menu. When set up like this, you can change Fader values and see the changes reflected in real time in Unreal Engine.

For Fixture Patch-based faders, DMX is sent to the Output Ports used in the DMX Library. For raw faders, DMX is sent to the first Output Port. For more on defining Input and Output Ports, see [DMX Quickstart](/documentation/en-us/unreal-engine/dmx-quick-start-in-unreal-engine#inputports).

### Add Raw Faders

A Raw Fader is a DMX Fader that's not connected to a fixture patch. To create a Raw Fader:

1.  In the Fader group area, click the **Add New (+)** button and then click **Next** or **Next Row**.
    
    ![Add a new fader group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e56e4d2a-7e27-4091-951e-6f6f37dcfcd4/add-fader-group.png)
2.  Click on the **Add (+)** button inside the fader group to create a Raw Fader.
    
    ![Add a new fader](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e2da0c5-0a21-4477-b4f5-fa92bcda109d/add-fader.png)
3.  Select the Raw Fader and edit the Fader properties in the Details panel to specify its precision (8-bit, 16-bit, or 24-bit) and other required parameters such as the Universe ID, Starting Address, Min Value, and Max Value.
    
    ![Fader settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f0bea36-de5a-4f5c-a4d6-a44f8125c854/fader-settings.png)

### Oscillators

Oscillators provide a way to animate selected sliders. By default, the Control Console provides a square wave and sine wave oscillator. Custom oscillators can be created in Blueprints.

![Oscillators for animating sliders](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3ee1b7c-7721-46e9-898a-01d1652347c0/oscillators.png)

#### Create Custom Oscillator Blueprints

1.  In the **Content Drawer**, click **Add +** > **Blueprint** > **Blueprint Class**.
    
2.  Under **All Classes**, search for and select **DMXControlConsoleOscillator**.
    
3.  Click **Select** to confirm.
    
    ![The Select button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/743761d0-b679-4758-a3c4-17aa9b325f4b/select-oscillator.png)
4.  In the **Content Drawer**, go to the **Blueprints** folder and open your new blueprint.
    
5.  Click **Override** **Get Normalized Value**.
    
    ![The submenu that contains the Get Normalized Value option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4236ee51-9d20-4192-8ecc-31698097145f/override.png)

## Options

### Clear Options

The Clear options help you to clear or reset Control Console data.

![Clear options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3de98070-a996-43e4-b449-dd4f0510d2d5/clear-options.png)

-   **Clear All**: Clear all the groups in the current layout. If you are in Auto layout mode, then this option also resets the DMX Library.
-   **Reset to Default**: The values of all the Faders are reset to the default, as set in the DMX Library.
-   **Reset to Zero**: The values of all the Faders are reset to zero.
-   **Reload**: Reloads the Control Console data from the disk.

### Control Options

The **Control** options change how Fader controls work:

![The Control options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/452edd1a-b98a-4259-9858-8133d69d5861/control-options.png)

-   **Absolute**: The values of all selected Faders are set to the same percentage.
-   **Relative**: The values of all selected Faders are increased or decreased by the same percentage. If the Faders start with different values, they keep this difference so long as you don't clamp them to either lower or upper bounds.
-   **DMX**: The values of all selected Faders are displayed according to their bitcoded data type (8-24 bit).
-   **Normalized**: The values of all selected Faders are displayed in a decimal range 0 to 1.
-   **Physical**: The values of all selected Faders are displayed using physical units as specified in the GDTF model. You can set physical values per channel for non-GDTF fixtures in the DMX library.
-   \*Send Raw Data to All Ports\*\*: Sends DMX data that is not using a patch to all created Ports in the Project Config.

### View Options

The **View** options adjust the shape and exposed properties of Fader Groups.

![The View options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c06d8bdf-4852-4dd3-af09-8c880cd31033/view-options.png)

-   **Collapse All** or **Expand All** Fader Groups. In the following example, the left is collapsed and the right is expanded. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/593bc0b7-851d-43fe-8014-7295b92be189/collapse-expand.png)
-   Set Faders view to Basic or Advanced mode. In Advanced mode, you can set min/max Fader values. ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63dd10a6-0568-4bd3-aaad-3ae55de99945/advanced-mode.png)

### Layout Options

The **Layout** options change the way that Fader groups are displayed:

-   **Horizontal**: Sets all Fader groups to be on the same line.
-   **Vertical**: Sets all Fader groups vertically one on top of each other.
-   **Grid**: Sets all Fader groups in a grid pattern. In default layout mode, Patches of the same Universe appear on the same horizontal line.

![The Layout options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbb1308e-728b-4703-bba1-955afa3f754b/layout-options.png)

### Selection Options

Selection options can select all Fader groups in the DMX Library or only filtered ones:

![The Selection options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/460681d1-097a-46f3-8a91-018063cca302/selection-options.png)

-   **Select All**: Select all Faders regardless of the active search filter.
-   **Select Only Filtered**: Select Faders that correspond to the search filter.
-   **Auto-Select**: Automatically select Faders inside a Fader group when selecting a Patch or multiple Patches from the DMX Library.

### Search Options

Use global search to quickly filter the exposed control sliders. It accepts a range of inputs such as Fader group names, attribute names ("Red, Green, Blue, Dimmer"), fixture IDs ("1, 2, 4-5"), universes ("Uni 1, 2, 4-5"), or addresses ("1.512").

To access the search history, click the dropdown arrow on the right.

![Search history](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/750f4a98-d3a1-4d52-b149-8e0ad9f91754/search-history.png)

#### Filters

Use the Filters tab to create and quickly select filters that update the Global Search results. The user can click the filters to enable or disable them.

![Search filters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c5364e3-4467-4647-b849-44be2fc28987/search-filters.png)

Each time a DMX Library is loaded, the filter tab is automatically updated with ready-to-use filters based on the attributes, universes, and fixture IDs of the patches in the library. You can also create a custom filter.

#### Create a Custom Filter

To create a custom filter, follow these steps:

1.  In the **Global Search** bar, click the **Add (+)** button.
2.  In the pop-up window, set the **Filter Label**, **Filter String**, and **Color**.
3.  Click **Create**.
    
    ![Create a filter pop-up window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcdd5e45-e662-4c80-97ea-92c98553f47b/create-filter.png)

User filters are displayed in the **User** dropdown at the top of the **Filters** tab.

### Show Compact Editor

Click **Show Compact Editor** to show a compact version of the Control Console that can be docked in the level editor.

![The Show Compact Editor button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af3ab7b8-31fb-484e-9e81-b81a35c729b5/show-compact-editor.png)

### Cues

Use cues to quickly store multiple versions of the faders configurations alongside their values and to load them back up on demand while the tool is actively sending DMX.

Click **Add (+)** to add a cue. Use the dropdown menu to load an existing cue.

![The Add button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d6a2dbb-c64f-4dce-8dd5-e0eb253bf0ff/add-cue.png)

To rename, reorder, and manage cues, click **Cue Stack**.

![The Cue Stack](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f0ae547-3fb6-47c1-b1b2-758f09c38756/cue-stack.png)