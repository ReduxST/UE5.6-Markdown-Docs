# Scriptable Tools System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/scriptable-tools-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/scriptable-tools-system-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:04

---

The **Scriptable Tools** system provides functions and an editor mode to create custom interactive tools. The goal of the system is to make it possible for non-C++ programmers to build interactive tools in Unreal Engine.

The main point of reference for an interactive tool is the [Modeling editor mode](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine). However, the Scriptable Tools system has no direct connection to Modeling Mode or Geometry Scripting.

The Scriptable Tools system plugin exposes the **Interactive Tools Framework** to [Blueprint](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine) (BP), providing creators and technical artists the means to design tools that behave similarly to Modeling Mode.

We recommend understanding the fundamentals of Blueprints to get started with Scriptable Tools. To learn more, see [Introduction to Blueprints](/documentation/en-us/unreal-engine/introduction-to-blueprints-visual-scripting-in-unreal-engine).

By creating Blueprint (BP) subclasses of base classes, you can add custom-defined tools to the **Scriptable Tools** editor mode. With the editor mode, artists can access these custom tools for their projects.

## What is a Scriptable Tool For

You can use a scriptable tool to:

-   Run arbitrary Blueprint (BP) graphs at tool setup and shutdown, as well as on tick.
-   Draw basic 3D geometry (for example, lines and points) and 2D HUD geometry (for example, text at projected 3D locations)
-   Add property sets to a tool, defined through Blueprints, which act as user-visible tool settings.
-   Listen for and respond to changes to those property set parameters.
-   Create one or more 3D gizmos, control their positions, and respond to transform changes.
-   Provide feedback messages to the user.
-   Add input device behaviors, like mouse click, mouse hover, and keyboard watchers, and run Blueprint graphs on their key events.
-   Integrate with [Blueprint Slate Widgets](/documentation/en-us/unreal-engine/creating-user-interfaces-with-umg-and-slate-in-unreal-engine) (UMG) to provide custom user interface (UI) as in viewport widgets.
-   Define custom conditions for the tool to start based on current scene selections.

You can pair Scriptable Tools with other features of the engine, such as [Procedural Content Generation](/documentation/en-us/unreal-engine/procedural-content-generation--framework-in-unreal-engine) (PCG) and [Motion Design](/documentation/en-us/unreal-engine/motion-design-in-unreal-engine).

For an overview of the system and how developers used it with other features to build a dungeon, see the [Geometry Scripting and Scriptable Tools | Unreal Fest 2024](https://youtu.be/gNKVGbwfX4c?feature=shared) video.

## Access Scriptable Tools Editor Mode and Nodes

### Enable Plugin

To use the Scriptable Tools editor mode and access the nodes, you must enable the associated plugin.

To enable the plugin or verify that it is already enabled, follow these steps:

1.  In the **menu bar**, select **Edit > Plugins**.
    
2.  In the **search bar**, type "scriptable tools".
    
3.  Enable **Scriptable Tools Editor Mode** plugin, and select **Yes** in the dialog popup.
    

You do not need to enable the Scriptable Tools Framework module. The editor mode automatically includes it.

![Scriptable Tool Plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9dfdc22f-beca-4539-8af4-78029d53266b/scriptable-tool-plugin.png)

### Editor Mode

You access all scriptable tools from the **Scriptable Tools** editor mode. To open the editor mode, click the **Selection Mode** dropdown in the Level Editor.

![Scriptable Tools Editor Mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca40fcb2-73f7-4e7e-a8c6-2bbf46c6439d/scriptable-tool-mode-ui.png)

Each tool appears in an automatically-managed tool palette in the editor mode, and the property sets for an active tool appear in the settings panel. To learn more about editor modes, see [Level Editor Modes](/documentation/en-us/unreal-engine/level-editor-modes-in-unreal-engine).

The tool palette includes a filter option that displays tools based on a group tag. The feature provides the means to group tools together and select which groups of tools to load in the editor mode. The grouping helps organize a project with many tools, which can reduce the cognitive load of seeing all the tools.

![Scriptable Tools Filter Tags](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2b43cfa-dd06-482a-a801-8cb75de3d801/scriptable-tools-filter-tags.png)

### Blueprint Nodes

To create tools that appear in the editor mode, use the Scriptable Tool functions exposed in Blueprints. You can use either a Blueprint Class or Editor Utility Blueprint to access the scriptable tool base class. To learn more about the base class and subclass, see the [Scriptable Tool Classes](/documentation/en-us/unreal-engine/scriptable-tools-system-in-unreal-engine#scriptabletoolclasses) section on this page.

In the Blueprint Editor, all the Scriptable Tool nodes live under the Scriptable Tool sub-menu.

![Scriptable Tool sub-menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a86a61c2-7a3b-48fe-837c-5c5271574169/scriptable-tools-input-behaviors.png)

Scriptable Tool sub-menu in the Blueprint Editor.

For a full list of functions, see the [Blueprint](/documentation/en-us/unreal-engine/BlueprintAPI/ScriptableTool) and [Python](/documentation/en-us/unreal-engine/python-api/class/ScriptableInteractiveTool?application_version=5.5) API documentation.

## Scriptable Tool and Editor Utility Widget Differences

An Editor Utility Widget (EUW) is a non-modal dialog window, containing a custom UI built with a visual GUI builder, where you can do any kind of editor scripting. This is an extremely powerful facility, but as a non-modal dialog there are various limitations.

An interactive tool (the basis for Scriptable Tools) is **modal**. Modal means that no other tool can be active while the tool is active, and the editor state is more strictly managed. For example, the tool automatically shuts down before saving, changing levels, or starting Play In Editor (PIE), and autosave is deferred until you exit the tool. This functionality means many things are safer to do in a tool than otherwise. For example, if you create temporary actors in a level and destroy them during tool shutdown, then they are not accidentally saved.

Similarly, as a modal state, a tool can capture the mouse more efficiently.

In terms of UI, a scriptable tool is more structured than an EUW. You can define property sets as separate BP objects with public variables. Those public variables are then displayed in a standard editor mode settings panel.

Scriptable Tools are available at runtime, however some additional infrastructure must be set up to take advantage of this in a UE project.

Additionally, Scriptable Tools provide a more central location to discover and access all tools found in the project, whereas EUWs are primarily accessed from the Content Browser, leaving it up to the user to manage discoverability and organization.

## Scriptable Tool Classes

`UScriptableInteractiveTool` is the base class for all scriptable tools. The class includes events, general settings such as tool name, rendering options, gizmos, messaging, tool shutdown options, and more for the subclasses. You can use its editor-variant, `UEditorScriptableInteractiveTool`, to provide access to editor-only BP functions.

The `UScriptableModularBehaviorTool` and `UEditorScriptableModularBehaviorTool` are the subclasses for supporting mouse and keyboard interactions within the tool. These two are the common classes to use, unless mouse and keyboard behavior are not needed.

![Scriptable Tool Classes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78fe31cf-dea7-47ce-9b0f-a06de0fa5016/scriptable-tools-classes.png)

`UScriptableClickDragTool` is deprecated. However, tools you previously created from the class will function in the latest editor version.

When you create a Blueprint Class or Utility Widget Blueprint you must select one of the classes above to access the Scriptable Tools nodes. To learn more about these classes, see the [Modular Base Tool](/documentation/en-us/unreal-engine/scriptable-tools-system-in-unreal-engine#modularbasetool) section on this page.

### Scriptable Tool Settings

The base class exposes various settings that are primarily for the Scriptable Tool editor mode UI, but also controls tool behavior. When you open your Blueprint, the Details panel for the tool contains the following options.

![Scriptable Tool Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/563875f2-171e-456c-8900-2dd2a2d78c55/scriptable-tool-settings.png)

| Node | Description |
| --- | --- |
| **Tool Name** | Short name for the tool. This is currently what is shown under the tool's icon in the editor mode. |
| **Long Name** | Shown in other places, for example next to the tool completion buttons. |
| **Category** | Determines which tool palette section the tool is placed in. |
| **Tooltip** | The hover-on-icon text that provides insight of what the tool is. |
| **Custom Icon Path** | Links to the image format path (.png or .sv) to display the tool icon. |
| **Visible in Editor** | Determines whether to show the tool class in the editor mode's UI. This can be useful to hide in-development tools or tool BP base classes that are meant to be subclassed. |
| **Shutdown Type** | Determines if the tool has an **Accept/Cancel** or **Complete** option in the tool confirmation panel. This option affects tool functionality. |
| **Tool Startup Requirements** | 
Determines the starting conditions for the tool.

Includes the following options:

-   **None:** The tool can start under any conditions.
-   **ToolTarget:** The tool matches the current selection against a set of tool target interfaces. Click the + icon in Tool Builder Class to add a Blueprint condition. You can set target requirements similar to the modeling tools, like static mesh and dynamic mesh.
-   **Custom:** The user provides a UCustomScriptableToolBuilder instance to determine if conditions are met. Click the **+** icon in **Tool Builder Class** to add a Blueprint condition.



 |
| **Group Tags** | Lists all group tags the tool belongs under. Used by the mode to filter which tools should load by the mode and made available for running by the user. |

### Scriptable Tool Events

The Scriptable Tool class provides a set of standard events for your tool to do different things at different times. There are standard events that every tool class has, and various additional functions are available in the base tools.

-   **Event On Script Setup:** Runs a single time when the tool is launched. This is generally where you would add Property Sets, create any preview objects, and more.
    
-   **Event On Script Tick:** Runs every Editor tick, just like other ticks.
    
-   **Event On Script Shutdown:** Runs when the tool is shut down. For example, when the user explicitly closes the tool, the mode forces it to shut down, or the tool shuts itself down.
    
-   **Event On Script Draw HUD:** Runs every frame and where the tool can draw a 2D HUD from a **HUD API** object. For more information, see the section below.
    

![Scriptable Tool Events](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c2ace88f-89c5-483e-86e7-01b4500f5da7/scriptable-tool-events.png)

**Event On Script Render** is a legacy drawing method. The event runs every frame and allows the tool to draw simple 3D geometry like lines and points. You can use the legacy feature but should note the following:

-   The event is real-time, so the lines are redrawn each and every time Render is called.
    
-   There aren't any persistent references held to the geometry, so you must manage the manipulations of the primitives in the Blueprint.
    

### Custom Conditions

You can add custom conditions based on current scene selections to start the tool. Define the custom conditions in **Class Defaults > Details panel > Scriptable Tool Settings > Tool Setup Requirements > Custom**.

The custom class contains the following functions:

-   **OnCanBuildTool:** Has to be run on tick.
    
-   **OnSetupTool:** Runs after user clicks and before tool runs.
    

The tool builder graph is run every tick, so complex conditions here can risk slowing the editor's performance.

### Tool Rendering

It is common for a tool to provide visual feedback. One way to define this feedback is by spawning temporary actors. For example, you can spawn temporary dynamic mesh actors with meshes procedurally generated by Geometry Scripting. However, a line or a text label is often more effective.

Scriptable Tools support this rendering by providing API objects with a set of `UFunction` nodes.

#### Rendering Options

![Scriptable Tools Render Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c9e3269-0170-41f3-8865-833d58e14878/scriptable-tools-render-options.png)

The **Drawing** API of Scriptable Tools includes render option sets for lines, points, and triangles. Each set then includes additional relative options in the Drawing category.

These drawing options are allocated by the tool and contain the geometry. With these sets, you can add and remove the respective geometry at any point during the tool's lifetime and update them as needed.

The **Add Triangle Set** node includes options for quads.

![Scriptable Tools Quad Drawing Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57d8d094-3724-4cc3-8ddb-aab2355d7b19/scriptable-tools-quad-render-options.png)

#### Legacy Options

You execute the legacy rendering commands in the **Event On Script Render** event node.

As noted earlier with this event:

-   You can override with the rendering API.
    
-   Draw lines and points.
    
-   It runs on the tick and goes away on the next tick.
    
-   No persistence.
    

The 2D Draw HUD and 3D Render events are called with `DrawHUDAPI` and `RenderAPI` objects, respectively. The tool creates and manages these API objects internally. The only place you can access them is from these events, as they depend on per-frame temporary state information provided by the tool.

BP also has a standard library of Debug Draw functions. You can use these as an alternative to the DrawHUD and Render functions and call them at any time. However, they are development only, and the tool Render APIs will provide more functionality.

### Gizmos

Another functionality of the Scriptable Tool base class is the option to create multiple 3D transform gizmos. This widget is not the standard editor gizmo but rather [Modeling Mode's gizmo](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#gizmo). A set of functions is provided to develop and manage gizmos and an event to respond to gizmo changes.

Gizmo objects are not directly exposed to Blueprints. Instead, you spawn a gizmo with a string **Identifier**, and the various gizmo functions and events work from this Identifier.

![Gizmo Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b5c4855-ccf2-40c4-a2be-b9acc6594f52/gizmos.png)

| Node | Description |
| --- | --- |
| **CreateTRSGizmo** | Creates a TRS (translate, rotate, and scale) gizmo with the given **Identifier** and **Gizmo Options**. For more information on the options, see the text following the table. |
| **DestoryTRSGizmo** | Destroys an existing gizmo by name. All gizmos created in the context of a tool are destroyed on tool shutdown. |
| **Get Gizmo Transform** | Gets the current transform on a gizmo by name. |
| **Set Gizmo Transform** | Updates the current transform on a gizmo by name. |
| **Set Gizmo Visible** | Hides or shows a gizmo by name. |
| **Event On Gizmo Transform Changed** | Fires whenever any active gizmo is transformed. Use the Identifier to differentiate which gizmo was modified. |

The basic TRS gizmo combines translation, rotation, and scale elements for all axes. However, by customizing the **Gizmo Options** you can create simpler gizmos for specific tasks. For example, only enabling translation and rotation in the XY plane, by disabling the other gizmo sub-elements.

![Gizmo Options Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a329421-b277-4b34-8977-8e841692d30d/gizmo-options-node.png)

### Tool Messaging

The standard scriptable tool BP API provides various functions for messaging to the user.

-   **Display User Help Message:** Updates a help string at the bottom of the Editor UI.
    
    ![Display User Help Message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c901be7d-e4a0-4e62-a46f-b0dc977cb9f0/display-user-help-message.png)
-   **Display User Warning Message:** Updates a string in the tool Settings panel.
    
    ![Display User Warning Message](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f76eef85-e499-4cef-ad4d-b1516355c930/display-user-warning-message.png)
-   **Clear User Messages:** Clears current help or warning messages.
-   **Add Log Message:** Currently prints a message to the editor's log.

The messages above are FText strings, and so are localizable. Currently only a single Warning can be displayed, this may be improved in future.

### Miscellaneous

A scriptable tool always runs in the context of a current world. For example, in the Level Editor, it is the standard level world. You can use the **Get Tool World** function to access this world in the context of a tool.

### Tool Shutdown

The standard flow for exiting a scriptable tool is clicking an **Accept**, **Cancel**, or **Complete** button presented in the UI. However, you can explicitly shut down a scriptable tool from the **Request tool Shutdown** function, which the tool can call itself. This function takes a **bAccept** flag, which is only relevant to tools with the accept or cancel shutdown option and an optional user popup message.

## Tool Property Sets

A scriptable tool can expose UI widgets to the user from **Property Set** UObjects, which are displayed in a standard tool settings panel. Currently, there is no way to customize this UI in Blueprints, so only standard property settings ( similar to what can be done for a parameter in an actor BP) are available.

To create a property set, create a BP subclass of the type **ScriptableInteractivetoolPropertySet**, as shown below.

![Tool Property Sets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2c6289c-84a1-43a8-ac77-bff5d7e94338/tool-property-sets.png)

You can then open the property set subclass BP for editing and add public member variables. Below a boolean, integer, and enum type is added.

![Property Set Variables](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84fee4dc-30f8-4eb3-bb46-e309a8f361b3/property-set-variables.png)

To create the property set in a particular scriptable tool, use the **Add Property Set of Type** function. This function is generally used in the **Event On Script Setup**. However, you can use it at any point.

You must select the correct class type for the **Property Set Type** parameter. Choose the type name of your BP subclass you created above. In addition, you must set a unique **Identifier** for each property set (you can combine multiple property sets in a single tool). You will likely need access to this property set object later. We recommend you cast the output of **Add Property Set Of Type** to your BP subclass type and store it in a local variable.

![Add Property Set of Type Script](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ebdf857-e5ad-4bc2-9e03-34d585f97515/add-propertyt-set-of-type-script.png)

When the user creates an instance of your scriptable tool, the public member variables of your property set are shown in the **Scriptable Tools** settings panel on the left, next to the tool palette.

![Scriptable Tools Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4cd79f7-681e-4ca8-b15c-03cb13300d98/scriptable-tools-settings.png)

The Scriptable Tool class has various helper functions for working with Property Sets. You can use **Remove Property Set by Name** to remove a property set, however note that this is not necessary to do in most cases. If you simply want to hide or show a Property Set based on some criteria or other parameter change, use **Set Property Set Visible by Name**.

In addition, you can use **Save Property Set Settings** on tool shutdown to store the current values of a property set, and **Restore Property Set Settings** can recover those saved values on tool setup. By default, the same values are restored in any tool using the Property Set class. However, an optional **Save Key** can be provided to save or restore different values in different tools, or even within the same tool.

![Property Set Nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab6681ee-fe33-4e23-845d-1b0ddbf388f2/property-set-nodes.png)

### Property Watchers

A common function you will likely want to do with a Property Set is react to changes in the property values. The only fully reliable solution is to poll for value changes in the tick function. However, since this is a common pattern, the Scriptable Tool system provides utility Property Watcher functions that can automatically do this polling.

You can use the functions below in a scriptable tool to watch for changes in a specific property of a Property Set and call an event when the value is modified.

In BP, it is currently not possible to automatically detect a UProperty Type from a variable reference. To set up the detection, ensure the following:

-   Make sure to use the function that matches the type of the public variable in the property set.
-   Pass the correct **Property Name** (the name of the public variable in the property set).

If the type is not simple (Int, Float, Bool, String, FName, Enum, or Object Property), use the general-purpose **Watch Property** version. However, its callback event is more limited.

![property watcher nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51a1f54c-eb51-4ffd-99d5-24dd0aac3b5c/property-watcher-nodes.png)

Below is an example of the **Watch Enum Property** function. This is the most complex of the simple types, as the Enum type is unknown. The **New Value** parameter that is passed to the callback event is a uint8 and must be explicitly cast to the correct UEnum type (in this case, **EGeometryScriptAxis**). It is currently not possible to check any errors here. The editor will cast the function to any Enum type.

![Watch Enum Property Script](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46e13918-7d4e-4937-802b-59c9b076cbdf/watch-enum-property-script.png)

For complex parameters, such as a nested UStruct like an FVector member variable, you can use the **Watch Property** function. This function can detect changes in nearly any UProperty variable. However, the callback event will not receive a **New Value** parameter like the other fields. If you create a member variable for the property set in your tool, you can directly fetch the property value in the event. This watcher type is also more computationally expensive, and you should only use it when necessary.

![Watch Property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30fb6c7a-e28a-4dc1-bdb7-6588ce6838b0/watch-property.png)

## Modular Base Tool

Base tools are C++ subclasses of Scriptable Interactive Tool Framework that provide additional built-in functionality to handle common cases and expose additional functionality such as input device handling and capture. You choose a base tool based on what type of tool you want to create. The editor version of the base tool provides access to editor-only BP functions.

The **Scriptable Modular Behavior Tool** class and its editor instance provide access to behavior functions, which are parameterized by a list of callbacks. This system replaces the built-in events and provides the means to mix and match behaviors, potentially even with duplication. This replacement is helpful because you can create multiple click behaviors within a single tool that triggers different conditions. For example, one click with the left mouse button, another with the right, and another with left + ctrl.

The exposed behaviors include the following:

-   Click and drag
-   Hover
-   Mousewheel
-   Multi-click
-   Click or drag
-   Single and multi keyboard inputs

![Scriptable Tool Input Behaviors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/304d043c-0f47-469e-b529-8296c47db9c2/scriptable-tools-input-behaviors.png)

Scriptable Tools behavior inputs.

## Enable Plugins for Editor-Only

In Unreal Engine, you can define plugin dependencies for project modules and plugins.

In the `.uproject` and `.uplugin` files that require `UScriptabletoolsFramework` or `UScriptabletoolsEditorMode` for in-editor usage, configure the `TargetAllowList` section to `Editor`. To learn more about plugins and file configuration, see [Plugins](/documentation/en-us/unreal-engine/plugins-in-unreal-engine).

```
		`{  			"Name": "ScriptabletoolsEditorMode",  			"Enabled": true,  			"TargetAllowList": [  				"Editor"  			]  		},`	
Copy full snippet
```
{ "Name": "ScriptabletoolsEditorMode", "Enabled": true, "TargetAllowList": \[ "Editor" \] },

## Next Steps

With a base understanding of the Scriptable Tools system, you can get started making your tools with the [Creating a Scriptable Tool](/documentation/en-us/unreal-engine/creating-a-scriptable-tool-in-unreal-engine) tutorial.