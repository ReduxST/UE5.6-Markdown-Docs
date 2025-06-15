# Level Editor Details Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-details-panel-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-details-panel-in-unreal-engine)  
**Processed:** 2025-06-14 16:33:00

---

Windows macOS Linux

The **Details** panel contains information, utilities, and functions specific to the current selection in the viewport. It contains transform edit boxes for moving, rotating, and scaling Actors, displays all of the editable properties for the selected Actors, and provides quick access to additional editing functionality depending on the types of Actors selected in the viewport. For instance, selected Actors can be exported to FBX and converted to another compatible type. The Details panel also allows you to view the Materials used by the selected Actors, if any, and quickly open them for editing.

Click image for full size.

## Actor Names

You can set friendly names for Actors directly in the editor. These names can be used to access related Actors or find them using the search functionality in the [World Outliner panel](/documentation/en-us/unreal-engine/outliner-in-unreal-engine).

To edit the Actor Name, simply type the name into the text box at the top of the **Details** panel.

Click image for full size.

## Search Filter

The properties displayed within the Details panel can be filtered using the **Search Details** box. As you type, the properties are automatically filtered to display only those properties matching the text.

Click image for full size.

To clear the filter, click the ![Clear Search](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d826fca0-ccc8-4bbf-b2dd-6abec6c8ce0f/04-clear-search.png "Clear Search") button on the right of the **Search** box.

Because this text box data hides properties that do not match the search criteria, check to make sure it is cleared if you do not see the property you are looking for.

## Favorites

This option is currently considered experimental and some features may not work as expected.

If there are properties within an Actor that you frequently change or want quick access to, you can use the **Favorites** property to flag them so they appear at the top of the **Details** panel.

Click image for full size.

Above, we checked two options as Favorites, indicated by the star icon next to their property name.

**To enable Favorites:**

1.  In the **Edit** menu, select **Editor Preferences**.
    
    ![Main Menu Bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5aa844f-6dfe-4d28-8d4a-9d65d598bad6/editorprefs.png "Main Menu Bar") ![Main Menu Bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a83b3936-b283-44ce-84dd-34d149544713/editorprefs_mac.png)
2.  Under **Experimental**, check the **Enable Details Panel Favorites** option.
    
    ![Experimental](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7c05ceaf-b0f7-4e2d-a584-565c9059e554/experimental.png "Experimental")

You may need to restart the editor for the changes to be applied.

**To mark a Property as a Favorite:**

1.  With the option enabled, click the star icon next to a property in any Details panel.
    
    Click image for full size.
    
    Some properties may not offer the ability to favorite them, due to the complexity of their customization.
    
2.  The property (along with any other marked favorites) is listed under the **Favorites** section of the panel.
    
    Click image for full size.
    

## Default Values

When a property is modified to a value other than its default value, an indicator is displayed.

Click image for full size.

Reset all properties to their default values by clicking the ![Reset to Default](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11717779-4b4d-49e3-b4f2-55ddbf59aa0c/09-reset-to-default.png "Reset to Default") indicator and choosing to reset the value from the menu.

Click image for full size.

The value of the property is reset to the default value as shown in the menu and the indicator is no longer present.

Click image for full size.

## Edit Conditions

Properties can be either be enabled or disabled. A property can only be edited when it is enabled. By default, all properties are enabled unless they have an edit condition. Properties with an edit condition rely on the value of another variable to determine if they are enabled and can be edited.

In some cases, edit conditions are used to determine whether the property will override some other value or if it has any affect at all. Other times, certain properties may simply not make sense unless some condition is met. For example, you may have a group of properties that pertain to indirect lighting and a `bool` property that globally toggles whether indirect lighting is enabled or disabled. Each property in the group could be conditional on the global toggle so they are only enabled when indirect lighting is being used.

A property with a simple edit condition will be displayed with a checkbox in the left margin. When the checkbox is toggled on, the property is enabled. When not checked, the property is disabled and grayed out.

Click image for full size.

## EditConst Properties

Properties declared as `editconst`, which cannot be modified in the editor, display their values and are highlighted to indicate they cannot be edited.

Click image for full size.

Click image for full size.

## Categories

Properties in the **Details** panel are displayed in categories. Categories such as **Rendering**, **Lighting**, and **Collision** are determined by how the property is declared in code, and are used as a means of organizing related properties into groups. Other categories, such as **Transform**, **Static Mesh**, **Materials**, **Actor**, **Code View**, and **Layers** are custom widgets designed to expose certain properties or functionality in a manner that makes them easier to find, modify and use.