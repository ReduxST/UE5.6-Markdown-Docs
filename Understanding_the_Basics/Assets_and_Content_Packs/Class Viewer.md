# Class Viewer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/class-viewer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/class-viewer-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:38

---

The **Class Viewer** in Unreal Engine is used to:

-   Examine a hierarchical list of classes that the Editor uses.
-   Create and open Blueprints.
-   Open associated C++ Header files and create new C++ classes based on a specific class.

## Opening the Class Viewer

To open the Class Viewer, from Unreal Engine's main menu, go to **Tools > Class Viewer**.

## Class Viewer Interface

![Class Viewer window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/996bfe7c-c937-4235-b46e-851373e9e4c9/ue5_1-class-viewer-window.png)

The Class Viewer interface consists of the following areas:

| **Number** | **Name** | **Description** |
| --- | --- | --- |
| 1 | Filters and Search bar | 
Use the **Filters** drop-down to restrict the classes that appear to one or more of the following:

-   Actors
-   Placeable Actors
-   Blueprint base classes

Use the **Search** bar to find classes by name.



 |
| 2 | Settings button | 

Click this button to open the **Settings** menu, which you can use to:

-   Expand or collapse all classes.
-   Show or hide internal classes.
-   Show classes from other developers who use the Developer folder.



 |
| 3 | Classes view | Shows all classes that fit the criteria you selected. |

## Working with Classes

![Expanding classes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b198210-c1c3-4dbe-9f43-ccd1b74ae94e/ue5_1-class-viewer-working-with-classes.png)

If a class has children, click the drop-down arrow to the left of the class name (1) to show the children of that class.

Click the drop-down arrow to the right of a class name (2) or right-click the class name to open a context menu with the options below.

The actions you can perform on a class are different based on class type (Blueprint or C++).

| **Option** | **Blueprint Class** | **C++ Class** |
| --- | --- | --- |
| **Create Blueprint** | Creates a new Blueprint parented to the selected Blueprint. | Creates a new Blueprint parented to the selected Blueprint. |
| **Edit Blueprint** | Opens the selected Blueprint in the [Blueprint Editor](/documentation/en-us/unreal-engine/user-interface-reference-for-the-blueprints-visual-scripting-editor-in-unreal-engine). | N/A |
| **Find in Content Browser** | Finds the Blueprint Actor in the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine). | N/A |
| **Open Source Code** | N/A | Opens the class header file in Visual Studio. |
| **Create New C++ Class** | N/A | Opens the [C++ Class Wizard](/documentation/en-us/unreal-engine/using-the-cplusplus-class-wizard-in-unreal-engine) to create a new class with the selected class as the Parent class. |

### Dragging and Dropping Classes

Click and drag a Blueprint class from the Class Viewer into the viewport to add a new Blueprint Actor of that class to the currently open Level.

You can also drag any class from the Class Viewer to a combo box in the Details panel or World Settings window, if the class is a child of the class associated with the combo box. For example, you can drag any `GameMode` child class into the GameMode Override combo box in World Settings.

When dragging classes into a combo box, note that:

-   Classes that haven't been loaded will not appear in the combo box.
-   Dropping a class into the combo box will force-load the class.

## Using the Class Picker

You can switch the Class Viewer to **Class Picker** mode using only code. The Class Picker displays a list of available classes, such as for converting Static Meshes or selecting a parent for a new Blueprint.

Using the Class Picker requires knowledge of how to use C++ in Unreal Engine.

### Configuring the Class Picker

`FClassViewerInitializationOptions`, which is used for initializing a Class Picker, has the following options that control Class Picker behavior:

| **Option** | **Description** |
| --- | --- |
| `Mode` | 
This is set to `ClassPicker` by default.

You can change this to `ClassBrowsing`, which spawns a normal Class Viewer instead. Note that most of the options below don't work in a Class Viewer.



 |
| `DisplayMode` | 

You can choose from the following options:

-   `TreeView`, which shows parent-child relationships between classes.
-   `ListView`, which shows a simple list of classes.



 |

You can use the following filters to configure which classes show in the Class Picker:

| **Filter** | **Description** |
| --- | --- |
| `bIsActorsOnly` | Only shows classes that are children of `AActor`. |
| `bIsPlaceableOnly` | Only shows classes that are placeable in the Level. If this is `true`, `bIsActorsOnly` will also be assumed to be `true`. |
| `bIsBlueprintBaseOnly` | Only shows Blueprint base classes. This is useful if you only want to see lasses that Blueprints can be created from. |
| `bShowUnloadedBlueprints` | Shows unloaded Blueprints, despite their parents being filtered out due to custom filters. |
| `bShowNoneOption` | Shows a **None** option in Class Picker. Doesn't affect Class Viewer. When you pick an item, a `NULL` class is passed. |