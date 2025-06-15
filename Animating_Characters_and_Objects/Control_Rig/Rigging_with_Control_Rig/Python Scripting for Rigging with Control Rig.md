# Python Scripting for Rigging with Control Rig

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-python-scripting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-python-scripting-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:46

---

Use [Python scripting](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python) in Control Rig to automate workflows and create tools for the rigging process. You can also use the **Control Rig Python Log** to reverse-engineer commands and copy scripts to share to other projects.

This document provides an overview of Python scripting in Control Rig, the Control Rig Python Log, and a few scripting examples.

#### Prerequisites

-   You have a Control Rig Asset open.
    
-   You have some experience with [Python scripting in Unreal Engine](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python).
    

## Scripting Overview

Python is primarily used in Control Rig to interact with the Rig Graph, which consists of multiple modules:

| Module Name | Description |
| --- | --- |
| **ControlRig** | Contains the runtime for the rigs. |
| **ControlRigDeveloper** | Contains all of the functionality to make changes to rigs. |
| **ControlRigEditor** | Contains front-end and user-interface logic. |

The Control Rig Graph has been implemented using the **Model - View - Controller** design pattern. The model is the graph itself using the following terminology:

| Control Rig Python Terms | Description |
| --- | --- |
| **RigUnit** | A C++ struct defining a function for a rig (Example: FRigUnit\_GetBoneTransform). |
| **Pin** | A single input or output of a function. |
| **Link** | A connection between two pins. |
| **Node** | A visual representation of a RigUnit. |
| **Graph** | A directed graph containing all nodes and links within a rig. |
| **PinPath** | A string describing the address of a pin within the graph (Example: NodeA.Translation.X). |
| **Controller** | An object used to make changes in the graph. |
| **RigElementKey** | Chosen from Bone, Control, Null, or Curve. |
| **Bone** | An element of the rig in the skeleton used for deformation. |
| **Control** | An element of the rig used for interaction. |
| **Null** | An element of the rig used for intermediate transforms. |
| **Curve** | An element of the rig used to store a float channel. |
| **Shape** | A visual representation of a Control in the Viewport. |
| **Hierarchy** | A container storing all Bones, Controls, Nulls, and Curves within the rig. |
| **HierarchyController** | Similar to the Controller, the HierarchyController is used to make changes to the hierarchy. |
| **Compiler** | An object to turn a Control Rig graph into a high performance runtime. |
| **VM** | The virtual machine runtime used to execute the rig. |
| **Constant** | A value that does not change at runtime. |
| **Parameter** | A value that can be used as an input to or output from the rig |
| **Variable** | A value that can be changed and runtime and is retained following executions of the rig. |
| **ControlRigBlueprint** | The asset containing the Graph, the Controller, Compiler and VM. |
| **Factory** | An object responsible for creating and importing new objects. This is used throughout the Unreal Editor to create assets. |

Python is enabled from the **Python Editor Script Plugin**, which itself is enabled by default in Unreal Engine. The plugin also automatically enables when the **Control Rig Plugin** is enabled, as it is a dependency.

### Accessing Control Rig

The first step when scripting is to access the main object you will be interacting with, in this case the **ControlRigBlueprint** object. There are several ways to access it, however your first command will usually be to load the ControlRigDeveloper module in order to make changes to Control Rig.

```
`unreal.load_module('ControlRigDeveloper')`
Copy full snippet
```
unreal.load\_module('ControlRigDeveloper')

To access an existing rig, load the asset with the following example command:

```
`rig = unreal.load_object(name = '/Game/ControlRig/Samples/Mannequin_ControlRig', outer = None)`
Copy full snippet
```
rig = unreal.load\_object(name = '/Game/ControlRig/Samples/Mannequin\_ControlRig', outer = None)

You can also load any currently open Control Rig Asset using:

```
`rigs = unreal.ControlRigBlueprint.get_currently_open_rig_blueprints()`
Copy full snippet
```
rigs = unreal.ControlRigBlueprint.get\_currently\_open\_rig\_blueprints()

Creating a new Control Rig Asset is done using:

```
`factory = unreal.ControlRigBlueprintFactory() rig = factory.create_new_control_rig_asset(desired_package_path = '/Game/TestRig')`
Copy full snippet
```
factory = unreal.ControlRigBlueprintFactory() rig = factory.create\_new\_control\_rig\_asset(desired\_package\_path = '/Game/TestRig')

Lastly, you can create a Control Rig Asset based on a Skeleton or Skeletal Mesh with the following example code:

```
`# load a skeletal mesh mesh = unreal.load_object(name = '/Game/Mannequin/Character/Mesh/SK_Mannequin.SK_Mannequin', outer = None)   # create a control rig for the mesh factory = unreal.ControlRigBlueprintFactory rig = factory.create_control_rig_from_skeletal_mesh_or_skeleton(selected_object = mesh)`
Copy full snippet
```
\# load a skeletal mesh mesh = unreal.load\_object(name = '/Game/Mannequin/Character/Mesh/SK\_Mannequin.SK\_Mannequin', outer = None) # create a control rig for the mesh factory = unreal.ControlRigBlueprintFactory rig = factory.create\_control\_rig\_from\_skeletal\_mesh\_or\_skeleton(selected\_object = mesh)

## Python Log

The **Python Log** provides a text log of all the actions that you performed within the Control Rig Editor. This includes actions within the viewport, the hierarchy, and the graph. Use this to reference commands to use in your Python scripts.

To access the log, click **Window > Message Log** from the main Control Rig menu, then select **Control Rig Python Log** from the Message Log sidebar.

![control rig python log](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95aaa525-825d-4c9f-9fc9-8df18dd60bff/pythonlog.png)

You can now perform actions in the Rig Graph and see them recorded in the log.

![python log record actions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f484378-72cd-4193-8073-563151bda5e3/pythonlog2.gif)

If you want to save a command to share or use elsewhere, you can select any line from the log and press **Ctrl + C** to copy it, then you can paste in any text editor. You can also select multiple lines by holding **Shift**.

![python log copy paste](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e8a8d7f-0809-412b-bfdb-f32d8dd854c4/pythonlog3.gif)

You can test commands by pasting them into the **Output Log** and executing them, ensuring the log type is set to Python. In this example, a new control is created.

![python output log command](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82175281-bd90-478a-b678-c662141ec7a5/outputlog.gif)

### Python Context

Python context is used to contextualize which Control Rig asset should be affected when running Python commands. By default, no context is set when viewing a Control Rig. You can set the context for the current Control Rig by clicking **Run Python Context** within the **Class Settings** Details panel.

![run python context](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bece0bcb-6377-4cff-8f91-a7220818aff3/context1.png)

This will execute a series of commands that bind the current Control Rig Asset to the Python context. This allows for commands copied from the Python Log to be pasted and executed within this Control Rig Asset.

![run python context commands](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3aaa89e-6f1c-4c13-9e0f-7ef7daa40188/context2.png)
```
`blueprint.get_controller_by_name('').set_node_selection([]) import unreal blueprint = unreal.load_object(name = '/Game/ShowAndTell202009/Pretzel/Mannequin_FBIK_CtrlRig', outer = None) library = blueprint.get_local_function_library() library_controller = blueprint.get_controller(library) hierarchy = blueprint.hierarchy hierarchy_controller = hierarchy.get_controller()`
Copy full snippet
```
blueprint.get\_controller\_by\_name('').set\_node\_selection(\[\]) import unreal blueprint = unreal.load\_object(name = '/Game/ShowAndTell202009/Pretzel/Mannequin\_FBIK\_CtrlRig', outer = None) library = blueprint.get\_local\_function\_library() library\_controller = blueprint.get\_controller(library) hierarchy = blueprint.hierarchy hierarchy\_controller = hierarchy.get\_controller()

### Copy Python Script

You can also copy the entirety of a Control Rig's nodes, rig elements, and properties to your clipboard. This can then be pasted into an external script editor, or back to the Output Log to execute on another Control Rig. Copy Python Script is useful for sharing, debugging and comparing the logic between different rigs. Similar to copying individual commands, copying whole rigs can also be useful for reverse-engineering Python commands from Control Rigs.

To copy a Control Rig, click **Copy Python Script** within the **Class Settings** Details panel.

![copy python script](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c95bdbb5-a6c2-4213-8003-821b58a4e4f3/copyscript1.png)

## Python Script Examples

### Adding Nodes

Since nodes are visual representations of **RigUnit** structs, you will need access to the unit in order to add a node to the graph.

```
`unreal.load_module('ControlRigDeveloper')  # get an array of all available units units = unreal.ControlRigBlueprint.get_available_rig_units()  # print details about the units for unit in units:       print(unit.get_path_name())       print(unreal.EditorAssetLibrary.get_metadata_tag(unit, 'Keywords'))`
Copy full snippet
```
unreal.load\_module('ControlRigDeveloper') # get an array of all available units units = unreal.ControlRigBlueprint.get\_available\_rig\_units() # print details about the units for unit in units: print(unit.get\_path\_name()) print(unreal.EditorAssetLibrary.get\_metadata\_tag(unit, 'Keywords'))

Next, you will need to access the Controller. The Controller is the central object used to make changes to the graph.

```
`controller = rig.get_controller()`
Copy full snippet
```
controller = rig.get\_controller()

To add a node to the graph you can use the `add_struct_node`, `add_comment_node`, `add_parameter_node` or `add_variable_node` functions. The example below focuses on the struct node, which is the most common type. A struct node is a visual representation of a RigUnit, therefore most of the nodes in a graph are struct nodes.

```
`# get the unit - you might also get this by path or similar unit = unreal.RigUnit_MathFloatAdd.static_struct()  # add the node to the graph provided the unit struct, the method (is always Execute) and 2D position in the graph node = controller.add_unit_node(script_struct = unit, method_name = "Execute", position = unreal.Vector2D(0, 0))`
Copy full snippet
```
\# get the unit - you might also get this by path or similar unit = unreal.RigUnit\_MathFloatAdd.static\_struct() # add the node to the graph provided the unit struct, the method (is always Execute) and 2D position in the graph node = controller.add\_unit\_node(script\_struct = unit, method\_name = "Execute", position = unreal.Vector2D(0, 0))

### Editing the Hierarchy

In addition to editing the graph, you can also edit the hierarchy using Python code. Each rig element in the Control Rig hierarchy is identified using **RigElementKey**, which contains the name and the type of the element. When you create or interact with elements in the hierarchy you will need to use this key.

Control Rig elements are structs, which means they are copied using their total values. As a result, if you change an element you may have to set it again in the hierarchy.

**Hierarchy** can be used to query elements, get or set global / local transforms, and reset elements back to their initial values.

**HierarchyController** can be used to add, remove and edit elements. You can also use it to rename and re-parent elements if needed.

To perform an inspection of the current hierarchy, you can use the following Python code:

```
`# access the hierarchy object hierarchy = rig.hierarchy  # get all element keys and print them elements = hierarchy.get_all_keys() for element in elements:       print(element)`
Copy full snippet
```
\# access the hierarchy object hierarchy = rig.hierarchy # get all element keys and print them elements = hierarchy.get\_all\_keys() for element in elements: print(element)

To create a rig element, such as a bone, you can use the following code:

```
`# access the hierarchy controller object hierarchy_ctrlr = rig.get_hierarchy_controller()  # add a new bone new_bone_key = hierarchy_ctrlr.add_bone(name = "MyBone", parent = unreal.RigElementKey(), transform = unreal.Transform())  # add a new child bone to a parent that is 10 units away on Z child_transform = unreal.Transform(location = [0, 0, 10])  new_child_bone_key = hierarchy_ctrlr.add_bone(name = "ChildBone", parent = new_bone_key, transform = child_transform)`
Copy full snippet
```
\# access the hierarchy controller object hierarchy\_ctrlr = rig.get\_hierarchy\_controller() # add a new bone new\_bone\_key = hierarchy\_ctrlr.add\_bone(name = "MyBone", parent = unreal.RigElementKey(), transform = unreal.Transform()) # add a new child bone to a parent that is 10 units away on Z child\_transform = unreal.Transform(location = \[0, 0, 10\]) new\_child\_bone\_key = hierarchy\_ctrlr.add\_bone(name = "ChildBone", parent = new\_bone\_key, transform = child\_transform)

### Variable and Asset Manipulation

To create a Control Rig variable with getter and setter nodes, you can use the following code:

```
`rig.add_member_variable("MyVariable", "Transform", is_public = True, is_read_only = False, default_value ="")  # Create variable getter node controller.add_variable_node_from_object_path(MyVariable, 'FTransform', '/Script/CoreUObject.Transform', is_getter = True, default_value = '', position = unreal.Vector2D(), node_name = 'MyVariable_Getter')  # Create variable setter node controller.add_variable_node_from_object_path(MyVariable, 'FTransform', '/Script/CoreUObject.Transform', is_getter = False, default_value = '', position = unreal.Vector2D(), node_name = 'MyVariable_Setter')`
Copy full snippet
```
rig.add\_member\_variable("MyVariable", "Transform", is\_public = True, is\_read\_only = False, default\_value ="") # Create variable getter node controller.add\_variable\_node\_from\_object\_path(MyVariable, 'FTransform', '/Script/CoreUObject.Transform', is\_getter = True, default\_value = '', position = unreal.Vector2D(), node\_name = 'MyVariable\_Getter') # Create variable setter node controller.add\_variable\_node\_from\_object\_path(MyVariable, 'FTransform', '/Script/CoreUObject.Transform', is\_getter = False, default\_value = '', position = unreal.Vector2D(), node\_name = 'MyVariable\_Setter')

The preview mesh can also be changed using the following code:

```
`# load a skeletal mesh mesh = unreal.load_object(name = '/Game/Mannequin/Character/Mesh/SK_Mannequin.SK_Mannequin', outer = None)  # create a new (empty) asset factory = unreal.ControlRigBlueprintFactory() rig = factory.create_new_control_rig_asset(desired_package_path = '/Game/TestRig')  # set the preview mesh rig.set_preview_mesh(preview_mesh = mesh)`
Copy full snippet
```
\# load a skeletal mesh mesh = unreal.load\_object(name = '/Game/Mannequin/Character/Mesh/SK\_Mannequin.SK\_Mannequin', outer = None) # create a new (empty) asset factory = unreal.ControlRigBlueprintFactory() rig = factory.create\_new\_control\_rig\_asset(desired\_package\_path = '/Game/TestRig') # set the preview mesh rig.set\_preview\_mesh(preview\_mesh = mesh)

The Control Rig can be compiled using any of the following code, depending on your context:

```
`# force a recompile of the VM rig.recompile_vm()  # compile the VM if there are pending changes rig.recompile_vm_if_required()  # request a compilation if auto compile is enabled and the editor is open rig.request_auto_vm_recompilation()  # request the control rig to run an init pass (initialize all units) rig.request_control_rig_init()  # request the control rig to run a full blueprint compile unreal.BlueprintEditorLibrary.compile_blueprint(rig)`
Copy full snippet
```
\# force a recompile of the VM rig.recompile\_vm() # compile the VM if there are pending changes rig.recompile\_vm\_if\_required() # request a compilation if auto compile is enabled and the editor is open rig.request\_auto\_vm\_recompilation() # request the control rig to run an init pass (initialize all units) rig.request\_control\_rig\_init() # request the control rig to run a full blueprint compile unreal.BlueprintEditorLibrary.compile\_blueprint(rig)

## Editor Startup

Python scripts can be loaded upon editor startup, which is useful for loading custom tools and built-in Python functions. You can locate this script and sample scripting functions from your project directory, under the following folder path:

```
`Engine\Plugins\Animation\ControlRig\Content\Python`
Copy full snippet
```
Engine\\Plugins\\Animation\\ControlRig\\Content\\Python

Within this folder is the init\_unreal.py script, which contains the following code:

```
`import RigHierarchy.add_controls_for_selected import RigHierarchy.add_null_above_selected import RigHierarchy.align_items  RigHierarchy.add_controls_for_selected.run() RigHierarchy.add_null_above_selected.run() RigHierarchy.align_items.run()`
Copy full snippet
```
import RigHierarchy.add\_controls\_for\_selected import RigHierarchy.add\_null\_above\_selected import RigHierarchy.align\_items RigHierarchy.add\_controls\_for\_selected.run() RigHierarchy.add\_null\_above\_selected.run() RigHierarchy.align\_items.run() ![init_unreal.py python custom command](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48e8904e-1f66-4bcc-93e8-967aee344d1f/init.png)

This code loads example scripts which enable extra functionality.

For example, **add\_controls\_for\_selected** enables functionality for creating controls on selected bones with additional rules. These rules are determined by the custom Python script located in Engine\\Plugins\\Animation\\ControlRig\\Content\\Python\\RigHierarchy\\add\_controls\_for\_selected.py.

![add controls for selected](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02f4adbc-8ce0-4ff3-a397-0c6d7cadacde/addcontrolsscript.png)