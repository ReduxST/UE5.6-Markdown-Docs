# Blueprint Editor Details Panel

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/details-panel-in-the-blueprints-visual-scriting-editor-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/details-panel-in-the-blueprints-visual-scriting-editor-for-unreal-engine)  
**Processed:** 2025-06-14 16:20:06

---

The **Details** panel is a context-sensitive area that provides editing access to the properties of selected items within the Blueprint Editor. It is composed of a search bar for fast access to specific properties, and will generally contain one or more collapsible categories to organize the included properties.

The **Details** panel is also where you will handle many Blueprint editing tasks, including:

-   Editing process for [Blueprint variables](/documentation/en-us/unreal-engine/blueprint-variables-in-unreal-engine), including changing name, type, and whether the variable is an array.
-   Implement [Blueprint interfaces](/documentation/en-us/unreal-engine/blueprint-interface-in-unreal-engine) after clicking the Blueprint Props button.
-   Adding inputs and outputs for [Blueprint functions](/documentation/en-us/unreal-engine/functions-in-unreal-engine).
-   Add [Events](/documentation/en-us/unreal-engine/events-in-unreal-engine) for selected [Components](/documentation/en-us/unreal-engine/components-window-in-unreal-engine).

## Interface

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/789bcfe1-9faa-49d9-9603-6ba57afa681e/blueprintdetails2.png)

1.  **Search Filter** - Type the name of the property you need and the properties below filter down.
2.  **Property Matrix** - Opens the **Property Matrix** panel for spreadsheet-like editing of available properties.
3.  **Visibility Filter** - Allows you to show or hide modified or advanced properties, as well as collapse or expand all categories.
4.  **Collapsible Categories** - These areas are used to group together related properties, and can be expanded and collapsed using the small white triangle to the left of the name.

Each of these areas are context sensitive. In any case where one of these areas does not apply to the currently selected item, the area simply will not appear. It is normal with many Blueprint nodes, for example, to see a primarily blank **Details** panel.