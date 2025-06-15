# Console Variables Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-variables-editor)  
**Processed:** 2025-06-14 16:15:09

---

The **Console Variables Editor** is a panel that displays information about all the console variables set in the project, and provides a central location to view and modify all the variables. You can create presets to use the same console variables and values across multiple projects. The Console Variables Editor also supports controlling variables across multiple computers in a [Multi-User](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine) session.

![Console Variables Editor user interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ebdfa8ee-5cf5-4194-a8c3-9327ef0f2f56/console-variables-editor.png)

The Console Variables Editor plugin also adds Blueprint API for accessing and controlling console variable presets created in the Console Variables Editor. Refer to the [Blueprint API Reference](https://docs.unrealengine.com/5.0/BlueprintAPI/ConsoleVariablesEditor) for more details.

To use the Console Variables Editor, enable the **Console Variables Editor** plugin in your project. Refer to [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) for steps on enabling plugins in a project.

![Console Variables Editor plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/339e3127-0b08-4d31-98d4-96497c3d5a6d/console-variables-editor-plugin.png)

In the main menu, choose **Window > Console Variables** to open the Console Variables Editor. You can dock this panel anywhere in Unreal Editor.

![Open Console Variables Editor from the main menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb529ff9-a087-4fb9-b7e0-108fbd35418e/open-console-variables.png)

## Console Variables List

The list contains all currently tracked console variables and executed commands. When you first open the Console Variables Editor, a blank preset is loaded with no console variables added. If **Add All Changed Console Variables to Current Preset** is set to **True** in the plugin settings, then you may see variables in the list already since console variables are often set through Project Settings.

To add console variables and commands to the list, click **(+) Add Console Variable** and search for a command or variable in the input box. As you enter text, a list appears below the text field showing matched console variable names, but console commands, such as `stat unit`, may not appear in the suggested list.

If the console variable you enter is valid, it then appears in the list. If you enter a console variable or command with a valid value, the command is executed with that value and the console variable appears in the list with its new value.

![Clicks add console variable button and enters the console command ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6f9a175-75d4-4150-9403-ad2470c639fc/enter-console-command.gif)

When you add a variable to the list, the current value is saved as the **preset value**. Each individual variable can be reset to its startup value or have its changes temporarily reverted by unchecking the row's checkbox.

![Checks and unchecks row to show how the value changes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/933edb8d-dbee-4c28-9dc6-68a8bfe5f79a/uncheck-check-row.gif)

You can remove a console variable from the list by hovering over the right side of its row and clicking **Remove**. When you remove the console variable from the list, its value is reset to the value it had when the plugin was loaded.

![Remove console variable button appears on hover in the row](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a53b191c-84c0-40fb-8d24-68a25b6a1f5a/remove-console-variable.png)

Hover over the console variable to see a tooltip with its description and what its values mean.

![Tooltip appears for the console variable when hovering over its name in the editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ce8b846-f0f8-4356-89fa-af068c7f034f/tooltip-for-console-variable.png)

Each row in the console variables list has a group of cells in the order specified in the table below. You can sort the list by **Sort Order Number**, **Console Variable Name**, and **Source** by clicking on the respective column header.

| Column | Description |
| --- | --- |
| Sort Order Number | 
The order the console variables are displayed in the list. You can drag and drop rows to change the order if you're sorting by this column.

If you sort by another column, you can update the sort order of the list to match by clicking Set Sort Order. Refer to [Show Options](/documentation/en-us/unreal-engine/console-variables-editor#showoptions) for more details.



 |
| Checkbox | 

You can temporarily disable changes made to individual console variables by unchecking the row. When unchecked, the console variable's value is set to the value the console variable had when the plugin was loaded at startup.

When you recheck the row, the value is set to the last cached value before you unchecked the row. Changes made to the console variable while the row is unchecked are not reflected when you recheck the row.

Currently, only console variables can be toggled.



 |
| Console Variable Name | Displays the name of the console variable. If you hover over the name, you can see the help text for the console variable if it exists. |
| Value | 

An editable field for the console variable that matches the type of the variable or command.

When you change the value fields, the console command or variable is executed. If multi-user is enabled, users in the multi-user session will have these variables set to the updated value or have commands executed on their local machines.

Hovering over the variable's value shows the following three values:

-   Custom Value
-   Preset Value
-   Startup Value

If the current value of a variable is different from the preset value, the option to reset the value appears beside the value widget. When you click **Reset**, the variable is set to the preset value again.



 |
| Source | Describes the last method used to set the variable. If the last method was through the Console Variables Editor, the Source type is Console. |

## Show Options

Click **Show Options** to customize which rows appear in the list. Refer to the table below for descriptions of each option.

![Show options dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/081d9020-ec0a-4a9d-8eaf-fbf8cbb0c146/show-options.png)

| Option | Description |
| --- | --- |
| Show |   |
| Show Constructor | When enabled, shows any console variables that are set by a default constructor in code. That is, if an engine class starts up and sets a console variable. |
| Show Scalability | When enabled, shows any console variables set by Scalability options. |
| Show Game Setting | When enabled, shows any console variables set by `UGameUserSettings(config=GameUserSettings)`. |
| Show Project Setting | When enabled, shows any console variables set by Project Settings. |
| Show System Settings ini | When enabled, shows any console variables set by System Settings. |
| Show Device Profile | When enabled, shows any console variables set by Device Profiles. |
| Show Game Override | When enabled, shows any console variables set by an override in game, such as a platform requiring a certain value to run properly. |
| Show Console Variables ini | When enabled, shows any console variables set in the Startup section of `Engine/Config/ConsoleVariables.ini`. |
| Show Command line | When enabled, shows any console variables set in Command-Line Arguments. |
| Show Code | When enabled, shows any console variables set by source code outside of a constructor, typically in a plugin. |
| Show Console | When enabled, shows any console variables set by you in a Blueprint, the CMD input, or the Console Variables Editor. |
| Show Only Modified | When enabled, shows any console variables whose current values differ from their preset value. |
| Sort |   |
| Set Sort Order | When selected, the current order of the console variables list is saved. |
| Options |   |
| Track All Variable Changes | This option is the same as Add All Changed Console Variables to Current Preset in the plugin settings. |

## Search

There are two types of searches: preset search and global search. Any text you enter becomes search tokens. Pipe characters separate text into OR tokens, and spaces combine text into AND tokens.

For example, if the text you enter is "lumen|screen percentage", then the search tokens are "lumen" and "screen percentage". The search returns results that either contain "lumen", or contain both "screen" and "percentage".

### Preset Search

Preset search is the default option when searching. Any console variables in the preset, whose **Name**, **Source**, or help text doesn't match the search tokens, are filtered out of the list.

![Preset search example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aefdfb93-34e5-42bc-af61-10611b3c09dc/preset-search.gif)

### Global Search

You enable global search by clicking **Search All** after typing text in the search field. Any console variables in Unreal Engine, whose **Name** matches the search tokens, appears in the list. The search tokens you enter appear below the search field. Any matching variables will be shown as rows in the list and can be manipulated just like rows in a preset.

![Global search example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecd13873-1565-48d3-919e-f3780dc70bd3/global-search.gif)

Toggle search tokens on or off by clicking them.

![Toggles search tokens on and off for global search](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07163b05-ddc7-46fc-be14-ee9694f3378e/toggle-search-tokens.gif)

**Right-click**, or **ctrl+click**, tokens to remove tokens individually.

![Removes search tokens from global search](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8bc3b01-fdf3-48c4-908f-36e27bfb8ccc/remove-search-token.gif)

Click **Remove** to remove all search tokens and revert to preset search.

![Highlights remove button to remove all search tokens and rever to preset search](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6bc57287-c8f7-4e9e-a4f1-1eb1f13ce04c/remove-search-tokens.png)

You can add a console variable from the global search list to your preset by hovering over the row and clicking **Add CVAR** when it appears in the row. If you enabled tracking all variable changes, then variables you change in this view are added to the current preset as well.

![Add console variable to preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6848037c-4ca3-4b38-b83a-c5399733e41e/add-console-variable.png)

## Presets

Open the **Presets** panel to save and load presets. When you load a preset, all variables in the current list are removed from the list but their values are not affected. All variables in the newly loaded preset are set to their saved values unless a given row is unchecked.

![Presets panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f61b886-5dd1-4a3e-a730-3b212248b67f/open-presets-panel.png)

## Multi-User

If you have the Multi-User plugin enabled in your project, the Multi-User option appears in the Console Variables Editor, and you can choose to propagate variable changes and command calls to other users in your session.

When you click Multi-User Controls, settings for Multi-User appear at the bottom of the Console Variables Editor. You can enable or disable console variables synchronization for individual session members from this control panel.

![Shows multi-user options with multiple users in a session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0071e890-66d8-4fa2-970a-50a98cf6644e/multi-user-options.png)

## Plugin Settings

You can customize the functionality and display of the Console Variable Editor in the plugin settings under **Project Settings > Plugins > Console Variables Editor**. The table below describes all the plugin settings.

![Console Variables Editor plugin settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9791429-931e-4060-b9cc-3f88d5505ee7/console-variables-editor-plugin-settings.png)

| Setting | Description |
| --- | --- |
| Unchecked Row Display Type | 
Determines how values are displayed in an unchecked row's value input. The following are the display options for unchecked rows:

-   Show Current Value
-   Show Last Entered Value



 |
| Add All Changed Console Variables to Current Preset | When enabled, any console variables that are changed outside of the Console Variables Editor are added to the list. Only console variables will be tracked this way; commands will not be added when entering them outside of the Console Variables Editor. |
| Changed Console Variable Skip List | If Add All Changed Console Variables to Current Preset is enabled, any console variables listed here will be filtered out when they are changed outside of the Console Variables Editor. |