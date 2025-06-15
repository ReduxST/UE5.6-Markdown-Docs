# Control Rig Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:35

---

This page outlines the user interface, tools, and features contained within the Control Rig Editor.

![control rig editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cfebc692-17b7-48f7-bde5-1fbabe91be9d/editoroverview.png)

1.  [**Toolbar**](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#toolbar)
2.  [**Viewport**](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#viewport)
3.  [**Rig Hierarchy**](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#righierarchy)
4.  [**Rig Graph**](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#riggraph)
5.  [**Details**](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#details)

## Toolbar

![control rig toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c01eb5a2-071f-4fbc-b2ab-aa433f0e859b/toolbar.png)

The **Control Rig** toolbar contains buttons and settings for previewing behavior and Control Rig construction. The buttons with specific Control Rig functionality are as follows:

| Name | Image | Description |
| --- | --- | --- |
| **Compile** | ![control rig compile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13c17118-a4b4-460a-8222-7e24a15e85fa/toolbarcompile.png) | 
Similar to **[Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine)**, Control Rigs must be **compiled** in order to fully save and begin executing their logic. Clicking this button will compile your rig, as well as visually provide feedback on whether or not your rig needs to be compiled.

You are required to compile whenever changes are made within the Rig Hierarchy. This can include adding, removing, reparenting, or renaming Controls, Bones or spaces. Recompiling is also required when creating variables.

The Compile button also resets your controls after you manipulate them in the viewport.



 |
| **Solve Direction** | ![toolbar forwards solve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81c1be96-bd65-43da-b35d-d4e40f0f92f4/toolbarsolvedirection.png) | 

The Solve Direction button switches between different Solver event chains. Use this to preview different [Solve Directions](/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine). Each option is associated with a Rig Graph solve direction event node. Selecting an option will begin previewing that solve chain.

![solve direction menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9044554d-d879-4318-99d8-032d085115ef/solvedirection.png)

Clicking the main button will swap the mode between the current mode and the previously selected mode.



 |
| **Auto Compile** | ![toolbar auto compile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/013f37bc-72a2-48b2-9e8a-dd91ece56df4/toolbarautocompile.png) | Enable **Auto Compile** to set compiling to automatically occur when you make changes in the Rig Graph. This includes actions like creating and linking nodes. All other changes mentioned above will still require you to manually compile. |
| **Debug Object** | ![control rig editor preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcbcba3d-6d40-4b7c-a246-5d0371d8312c/toolbardebug.png) | This drop-down menu links the Control Rig viewport to an active Control Rig in a simulating or playing session. This previews the current Control Rig animation from that session in the Control Rig viewport. |
| **Class Settings** | ![toolbar class settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20fc8d97-d87d-4a72-9c4a-60d124479331/toolbarclass.png) | 

The Class Settings button toggles Blueprint class settings to be visible in the [Details](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#details) panel. The **Shape Libraries** property is located here, which can be used to change the control shapes available to you when rigging. Visit the [Control Shapes and Control Shape Library](/documentation/en-us/unreal-engine/control-shapes-and-control-shape-library-in-unreal-engine) page to learn more about this feature.

![shape library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2b2932a-30a1-474d-bdae-fcf295052589/shapelibrary.png)

You can also access Control Rig Python commands such as [Python Context](/documentation/en-us/unreal-engine/control-rig-python-scripting-in-unreal-engine#pythoncontext) and [Copy Python Script](/documentation/en-us/unreal-engine/control-rig-python-scripting-in-unreal-engine#copypythonscript).



 |

## Viewport

From the Viewport, you can:

-   Preview interaction with your Control Rig nodes.
-   Set different display modes and debug displays.
-   Select and manipulate controls.
-   Change the preview mode using the top toolbar.

![control rig viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/405cf608-ca63-4e91-892f-9fba896030e5/viewport.png)

The **View Options** menu has the following Control Rig settings:

![control rig view options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f5448d2-b490-4421-947e-95a4876298c2/viewoptions.png)

| Name | Description |
| --- | --- |
| **Display Nulls** | 
Displays a selectable axis of [Nulls](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine) in the viewport.

![control rig display nulls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fc39587-a9a4-440d-923d-22e7bb8d5215/nulls.png)

 |
| **Display Axes On Selection** | 

Displays a local axis when you select any rig element.

![control rig display axes on selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a3df61d-f46a-4bab-a5ae-b64a6cce1c0b/axisdisplay.png)

 |
| **Axes Scale** | 

The size of the axis display when drawing axes from either the **Display Nulls** or **Display Axes On Selection** options.

![control rig axes scale](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87a29ed1-5eb3-41b8-bc6d-9b1b6de5170c/axisscale.png)

 |
| **Bone Radius** | 

The size of the Bones when Bones are visible by either selecting them or by showing Bones from the **Character > Bones** menu.

![control rig bone radius](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54c757a1-e037-47a9-8c08-587dba499b98/bonesize.png)

 |
| **Pin Control Space** | When controlling a pin value, you can select an element from this to offset the manipulator to be relative to a different element. |

## Rig Hierarchy

The **Rig Hierarchy** panel is used to view and select your control hierarchy in an outliner-type view. This is also the primary area to create new [Controls, Bones, and Nulls](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine).

![control rig hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99e86f79-9351-4c44-bb87-0ba9629861cd/righierarchy.png)

Create these elements by right-clicking in the panel and selecting **New > Control, Bone, or Null**. Your selection determines the location where these elements are created. If nothing is selected, then new elements will be created at the origin (0,0,0).

![new control bone null](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9943b09-e1d0-4821-9a65-b8a080121273/newcontrol.png)

The context menu contains the following commands:

![rig hierarch right click menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd419755-dbe7-4feb-8cca-fb5026492216/righierarchycontext.png)

| Name | Description |
| --- | --- |
| **New** | Creation menu for creating new **Controls**, **Bones**, or **Nulls**. |
| **Delete** | Deletes the current selection. |
| **Duplicate** | Duplicates the current selection. |
| **Rename** | Renames the current selection. |
| **Mirror** | 
Copies your currently selected elements and mirrors the copy along an axis. When clicked, a dialog window will appear where you can specify how you want the mirror action to function.

![control rig mirror controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c05675b3-c15b-454c-b080-0b7aeb553b98/mirror.png)

-   **Mirror Axis** is the axis to mirror against. For characters that face Y-Forward in Unreal, you can keep this at the default value of **X**.
-   **Axis to Flip** is the axis to rotate 180 degrees in order for rotations to be properly mirrored. For characters that face Y-Forward in Unreal, you can keep this at the default value of **Z**.
-   **Search** is where you specify a keyword or letter to search for to be replaced. If you are mirroring a control with the postfix "\_left", then you will want to write "left" here.
-   **Replace** is where you specify a keyword or letter to replace the text used in **Search**. If you are mirroring a control with the postfix "\_left", then you will want to write "right" here.



 |
| **Test Space Switching** | 

Opens a dialog window for previewing [Space Switching](/documentation/en-us/unreal-engine/re-parent-control-rig-controls-in-real-time-in-unreal-engine) behavior for your controls.

![control rig test space switching](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1ca35f8-05c8-4ed6-8dd1-58ac818a8390/testspaceswitch.png)

-   **Parent** is the default behavior, where the control will follow any space changes by the parent.
-   **World** will detach the control from any parent influence and attach it to the world.
-   Click the **Add (+)** button to add any other control to parent to.



 |
| **Copy** | Copies the current selection, including the local and global transform, which can be used in conjunction with **Paste Local** / **Global Transform**. |
| **Paste** | Pastes the current selection. |
| **Paste Local Transform** | Pastes the currently copied control's local transform. |
| **Paste Global Transform** | Pastes the currently copied control's world transform |
| **Reset Transform** | Resets the currently selected control back to its initial transform. |
| **Reset All Transforms** | Resets all controls back to their initial transform. |
| **Set Initial Transform from Current** | After moving a transform in the viewport, clicking this will set the new location as the new initial transform. |
| **Set Initial Transform from Closest Bone** | Using this command will snap your selected Control to the nearest Bone and set that location as the Initial Transform. This is useful for aligning your controls to Bones. |
| **Set Shape Transform From Current** | If you are transforming your control, performing this command will reset the control's pivot point back to its initial transform, but maintain the current visual position of the control shape. This is useful if you want to customize your control's visual position while keeping the pivot the same. |
| **Unparent** | Moves the currently selected element to the top of the hierarchy. |
| **Import** | Imports a skeleton hierarchy to the current rig. |
| **Refresh** | Refreshes the existing initial transform from the selected mesh. This only updates if the node is found. |

## My Blueprint

The **My Blueprint** panel, similar to that found in [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine), contains your various Control Rig **Functions** and **Variables**. Variables in Control Rig are meant to be used within your Rig Graph as a way to drive logic, rather than being exposed directly to an instance in a Level.

![control rig my blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8a56c5a-9024-480b-a726-c953f59dae81/mybp.png)

## Execution Stack

The **Execution Stack** panel previews the order of operations within your graph. Use this to debug your nodes and evaluate the sequence of events.

![control rig execution stack](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f278ea1-3fdb-4286-873b-eb132999c853/execution.png)

Right-clicking on an execution node and selecting **Focus on Selection** will frame that current node in the Rig Graph. You can also double-click a node to focus it.

## Curve Container

The **Curve Container** panel displays the list of **Anim Curves** from your **Skeleton**, and provides functionality to control them in the Rig Graph.

![control rig curve container](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/746f259c-b65c-46c9-a448-b7215c672b62/curves.png)

Curves can be referenced in the Rig Graph by using the **Get Curve Value** and **Set Curve Value** nodes.

![control rig get set curve value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/be07f6d6-7329-4498-86d4-e8417bbcc57d/curveref.png)

## Rig Graph

The **Rig Graph** is where you script the Control Rig's behavior.

Hierarchy nodes can be referenced into the graph by dragging and dropping them from the Rig Hierarchy panel into the graph and selecting your desired reference type.

![control rig graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43010ec9-fdb3-4770-a2e7-93827380d9c9/riggraph1.png)

You can also create nodes by right-clicking. Search or navigate the context menu for your desired node.

![control rig graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e8796b6-cfc1-47b7-820a-7457245ed1be/riggraph2.png)

Similar to [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine), multiple nodes can be collapsed into groups or **Functions** by right clicking on your selected nodes and selecting either **Collapse Nodes** or **Collapse to Function**.

![control rig functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4de3ec33-2f1f-434f-bb2d-1e194a768a23/collapse1.png)

Your functions are accessible from the **My Blueprint** panel in the **Functions** category. With functions, you can better organize large graphs, repeat logic, and easily share functionality across Control Rigs.

![control rig functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03743b34-93b3-4fc7-8551-86b17e10f58d/collapse2.png)

## Details

The **Details** panel contains information for your selected elements within the Control Rig Editor. These can include elements such as Controls, Bones, and rig graph nodes. Selecting Controls will reveal the following properties:

![control rig properties details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceb58003-e2f2-4244-ba44-08c9da192235/details.png)

| Name | Description |
| --- | --- |
| **Name** | The name of the selected rig element. |
| **Display Name** | The name of the Control as it will appear in [Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine) and the [Anim Outliner](/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine#animoutliner). If not used, then the name will fallback to what is specified in **Name**. |
| **Control Type** | The [type](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine#controltypes) of Control to use. This is used to limit or change the Control's data if you intend the Control to only affect certain values, such as a Control that only rotates, translates, or provides a single property. |
| **Animatable** | Determines whether or not the Control will be animatable in Sequencer. This is useful if your rig has Controls that are visual-only. |
| **Available Spaces** | An array where you can add [predefined custom spaces](/documentation/en-us/unreal-engine/re-parent-control-rig-controls-in-real-time-in-unreal-engine#pre-definingcustomspaces) for your Controls, which are used for [space switching](/documentation/en-us/unreal-engine/re-parent-control-rig-controls-in-real-time-in-unreal-engine). |
| **Draw Limits** | 
Draws a debug line if [transform limits](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine#transformlimits) are being used on the selected Control.

![control rig draw limits](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e3df615-982d-4b6f-a3ca-b30cdcc90e1d/drawlimits.gif)

 |
| **Transform** | Displays the different [transform types](/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine#transformtypes) for the selected rig element. Bones and Nulls will only display **Initial** and **Current**, while Controls will display **Initial**, **Current**, **Offset**, and **Min/Max** limits. |
| **Shape** | The **Shape** category contains properties for [customizing the shape](/documentation/en-us/unreal-engine/control-shapes-and-control-shape-library-in-unreal-engine) of the selected Control. |

## Preview Scene Settings

The **Preview Scene Settings** panel contains properties that control your Skeletal Mesh, animation, and viewport environment settings.

![control rig preview scene settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0df96e27-b340-45b5-bcd1-42d5909db6ba/previewsettings.png)

The following properties can be used to affect the Control Rig viewport:

| Name | Description |
| --- | --- |
| **Preview Controller** | 
Use the Preview Controller to play back animations in the viewport. This can be useful when testing how your Controls behave when animation is playing on your character, or for testing **[Backwards Solve](/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine)** behavior.

![control rig preview controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9d69cae-3ffe-4880-bf50-f2932fdf64a6/previewcontroller.gif)

 |
| **Preview Mesh** | The Skeletal Mesh to use for your character in the viewport. You can change this to any other meshe with a compatible skeleton. |
| **Clothing Simulation Factory** | The cloth simulation to use in the viewport. |
| **Allow Different Skeletons** | If enabled, you can select Skeletal Meshes with incompatible skeletons in the **Preview Mesh** or **Skeletal Meshes** properties. |
| **Allow Custom AnimBP Override** | When using Preview Collections, enable Animation Blueprints to override from those collections. |
| **Additional Meshes** | Specify a **Preview Collection** here. |
| **Skeletal Meshes** | Additional meshes to add to the viewport. This can be useful if you are using [Modular Characters](/documentation/en-us/unreal-engine/working-with-modular-characters-in-unreal-engine). |