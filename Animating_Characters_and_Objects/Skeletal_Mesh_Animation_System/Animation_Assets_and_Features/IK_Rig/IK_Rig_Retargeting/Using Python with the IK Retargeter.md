# Using Python with the IK Retargeter

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-python-to-create-and-edit-ik-retargeter-assets-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-python-to-create-and-edit-ik-retargeter-assets-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:41

---

When creating and using [IK Retargeter](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine) assets to retarget animations for characters and objects using [IK Rigs](/documentation/en-us/unreal-engine/unreal-engine-ik-rig) in **Unreal Engine**, you can use custom [Python scripting](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python) to control and automate IK Retargeter asset workflows.

This document provides an overview and example python scripts you can reference and use to edit and interface with IK Retargeter assets.

## Overview

An IK Retargeter asset consists of multiple parts:

-   A **Source** and **Target IK Rig** to define the retarget relationship.
    
-   A **Source** and **Target Skeletal Mesh** override from the Source and Target IK Rig.
    
-   **Retarget Chain** mappings between the source and target, defining the relationship between each chain.
    
-   A list of **Retarget Poses** for either the Source or Target, defining the starting pose of which the retarget will solve.
    
-   A list of properties for the **Global**, **Retarget Root**, and each **Retarget Chain**.
    
-   A preview scene used exclusively for an in editor preview.
    

The IK Retargeter data model using the following terminology:

-   **Source** and **Target IK Rig**: The IK Rigs that will be used to map the Retarget Chains together in order to transfer the motion from source to target.
    
-   **Source** and **Target Mesh**: The Skeletal Mesh in which you want to use to define the Source and Target proportions for a retarget and to access the source animations to preview.
    
-   **Source** and **Target Retarget Pose**: The Pose in which you want either the Source or Target to use to transfer the motion. Ideally, the target should match to the pose that the source is in.
    
-   **Global Settings**: Macro level settings that affect the entire retarget.
    
-   **Root Settings**: Settings that affect the Retarget Root.
    
-   **Chain Settings**: Settings that affect the specified Retarget Chain.
    

## Accessing the IK Retargeter

The first step when scripting against any IK Retargeter asset is to gain access to the main object you'll interact with, the `IKRetargeter`. There are several ways you can gain access to the object depending on your project.

### Loading an existing RTG asset

To access an existing IK Retargeter asset (`rtg`) you can simply load the asset using the following example script:

```

`import unreal  #  Ensure the file path is correct for the location of your asset in your project.  rtg = unreal.load_asset(name = '/Game/Characters/Mannequins/Rigs/RTG_Mannequin', outer = None)`

Copy full snippet
```
import unreal # Ensure the file path is correct for the location of your asset in your project. rtg = unreal.load\_asset(name = '/Game/Characters/Mannequins/Rigs/RTG\_Mannequin', outer = None)

## Create a new RTG asset

To create a new IK Retargeter asset you can use the following factory:

```

``# Get asset tools.  asset_tools = unreal.AssetToolsHelpers.get_asset_tools()  # Create an IK Retargeter asset in the location defined by the file path. For example, `.../Game/RTG_Mannequin`.  rtg = asset_tools.create_asset(asset_name='RTG_Mannequin', package_path='/Game/', asset_class=unreal.IKRetargeter, factory=unreal.IKRetargetFactory())``

Copy full snippet
```
\# Get asset tools. asset\_tools = unreal.AssetToolsHelpers.get\_asset\_tools() # Create an IK Retargeter asset in the location defined by the file path. For example, \`.../Game/RTG\_Mannequin\`. rtg = asset\_tools.create\_asset(asset\_name='RTG\_Mannequin', package\_path='/Game/', asset\_class=unreal.IKRetargeter, factory=unreal.IKRetargetFactory())

## Editing an IK Retargeter

### Preparing for an Edit by Accessing the Controller

The controller is the central object you can use to make any change to the IK Retargeter. The controller has many functions that you can use to make edits. The following examples are a subset of methods you can use Python scripting to make edits to IK Retargeter assets:

```

`# Get the IK Retargeter controller.  rtg_controller = unreal.IKRetargeterController.get_controller(rtg)`

Copy full snippet
```
\# Get the IK Retargeter controller. rtg\_controller = unreal.IKRetargeterController.get\_controller(rtg)

### Assigning the Source and Target IK Rigs and Meshes to a new asset

To run a retarget, you must provide a source and a target IK Rig. In this case, we are going to create an IK Retargeter asset to retarget animations from the Manny Character to the Quinn Character, which means we can assign the `IK_Mannequin` as both the source and target.

You can access the Manny and Quinn Skeletal Mesh characters, as well as the `IK_Mannequin` IK Rig asset, using the [Third Person Template project](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine).

```

`# Load the Source and Target IK Rigs.  source_ik_rig = unreal.load_asset(name = '/Game/Characters/Mannequins/Rigs/IK_Mannequin', outer = None)  target_ik_rig = unreal.load_asset(name = '/Game/Characters/Mannequins/Rigs/IK_Mannequin', outer = None)  # Assign the Source and Target IK Rigs.  rtg_controller.set_ik_rig(unreal.RetargetSourceOrTarget.SOURCE, source_ik_rig)  rtg_controller.set_ik_rig(unreal.RetargetSourceOrTarget.TARGET, target_ik_rig)`

Copy full snippet
```
\# Load the Source and Target IK Rigs. source\_ik\_rig = unreal.load\_asset(name = '/Game/Characters/Mannequins/Rigs/IK\_Mannequin', outer = None) target\_ik\_rig = unreal.load\_asset(name = '/Game/Characters/Mannequins/Rigs/IK\_Mannequin', outer = None) # Assign the Source and Target IK Rigs. rtg\_controller.set\_ik\_rig(unreal.RetargetSourceOrTarget.SOURCE, source\_ik\_rig) rtg\_controller.set\_ik\_rig(unreal.RetargetSourceOrTarget.TARGET, target\_ik\_rig)

We can also get the source or target IK Rig, this is useful to query for retarget chains.

```

`# Get the Source and Target IK Rig assigned to the IK Retargeter asset.  rtg_controller.get_ik_rig(unreal.RetargetSourceOrTarget.SOURCE)  rtg_controller.get_ik_rig(unreal.RetargetSourceOrTarget.TARGET)`

Copy full snippet
```
\# Get the Source and Target IK Rig assigned to the IK Retargeter asset. rtg\_controller.get\_ik\_rig(unreal.RetargetSourceOrTarget.SOURCE) rtg\_controller.get\_ik\_rig(unreal.RetargetSourceOrTarget.TARGET)

Not only can we set the source/target IK Rigs, but we can provide overrides to the source/target preview mesh. This will override the default preview meshes provided by the IK Rigs.

```

`# Load the Skeletal Mesh.  source_skel_mesh = unreal.load_asset(name = '/Game/Characters/Mannequins/Meshes/SKM_Manny_Simple.SKM_Manny_Simple')  target_skel_mesh = unreal.load_asset(name = '/Game/Characters/Mannequins/Meshes/SKM_Quinn_Simple.SKM_Quinn_Simple')  # Assign the Source and Target Skeletal Meshes.  rtg_controller.set_preview_mesh(unreal.RetargetSourceOrTarget.SOURCE, source_skel_mesh)  rtg_controller.set_preview_mesh(unreal.RetargetSourceOrTarget.TARGET, target_skel_mesh)  # Get the Source and Target Skeletal Meshes assigned to the IK Retargeter asset.  rtg_controller.get_preview_mesh(unreal.RetargetSourceOrTarget.SOURCE)  rtg_controller.get_preview_mesh(unreal.RetargetSourceOrTarget.TARGET)`

Copy full snippet
```
\# Load the Skeletal Mesh. source\_skel\_mesh = unreal.load\_asset(name = '/Game/Characters/Mannequins/Meshes/SKM\_Manny\_Simple.SKM\_Manny\_Simple') target\_skel\_mesh = unreal.load\_asset(name = '/Game/Characters/Mannequins/Meshes/SKM\_Quinn\_Simple.SKM\_Quinn\_Simple') # Assign the Source and Target Skeletal Meshes. rtg\_controller.set\_preview\_mesh(unreal.RetargetSourceOrTarget.SOURCE, source\_skel\_mesh) rtg\_controller.set\_preview\_mesh(unreal.RetargetSourceOrTarget.TARGET, target\_skel\_mesh) # Get the Source and Target Skeletal Meshes assigned to the IK Retargeter asset. rtg\_controller.get\_preview\_mesh(unreal.RetargetSourceOrTarget.SOURCE) rtg\_controller.get\_preview\_mesh(unreal.RetargetSourceOrTarget.TARGET)

### Editing and Querying Retarget Chain Mappings

Similar to the Editor, you can do an auto map for the retarget chains using Python. You can also access automap options, such as a **fuzzy string match**, an **exact string match**, or **clear maps** in total.

```

`# Map chains using a fuzzy string match, which will force a remap.  rtg_controller.auto_map_chains(unreal.AutoMapChainType.FUZZY, True)  # Map chains using an exact string match, which will force a remap.  rtg_controller.auto_map_chains(unreal.AutoMapChainType.EXACT, True)  # Clear all mappings.  rtg_controller.auto_map_chains(unreal.AutoMapChainType.CLEAR, True)`

Copy full snippet
```
\# Map chains using a fuzzy string match, which will force a remap. rtg\_controller.auto\_map\_chains(unreal.AutoMapChainType.FUZZY, True) # Map chains using an exact string match, which will force a remap. rtg\_controller.auto\_map\_chains(unreal.AutoMapChainType.EXACT, True) # Clear all mappings. rtg\_controller.auto\_map\_chains(unreal.AutoMapChainType.CLEAR, True)

If you don't want to do an automap, you can get or set the mapping of each target chain.

```

`# Get the Source chain that is mapped to a given Target chain.  source_mapped_chain_name = rtg_controller.get_source_chain("Spine")  # Set the Source chain that the Target is mapped to, formatted in the Python script as ("Source",  "Target").  rtg_controller.set_source_chain("Spine", "Spine")`

Copy full snippet
```
\# Get the Source chain that is mapped to a given Target chain. source\_mapped\_chain\_name = rtg\_controller.get\_source\_chain("Spine") # Set the Source chain that the Target is mapped to, formatted in the Python script as ("Source", "Target"). rtg\_controller.set\_source\_chain("Spine", "Spine")

### Adding, Editing, and Querying Retarget Poses

Retarget Poses are used to determine the base pose that the source or target should retarget from. This is useful if your target character is in a different pose than your source or if the source needs to face in the proper front axis.

You can query the retarget poses for the source or target by using this command:

```

`# Get all retarget poses for the Target.  all_target_poses = rtg_controller.get_retarget_poses(unreal.RetargetSourceOrTarget.TARGET)`

Copy full snippet
```
\# Get all retarget poses for the Target. all\_target\_poses = rtg\_controller.get\_retarget\_poses(unreal.RetargetSourceOrTarget.TARGET)

You can create, duplicate, rename, or remove a retarget pose, as long as you provide the retarget pose's name and specify if it is the source or target.

```

`# Create a new retarget pose.  rtg_controller.create_retarget_pose("my_new_pose", unreal.RetargetSourceOrTarget.TARGET)  # Duplicate the new pose.  rtg_controller.duplicate_retarget_pose("my_new_pose", "duplicated_pose", unreal.RetargetSourceOrTarget.TARGET)  # Rename the duplicate pose.  rtg_controller.rename_retarget_pose("duplicated_pose", "renamed_pose", unreal.RetargetSourceOrTarget.TARGET)  # Remove the duplicate pose.  rtg_controller.remove_retarget_pose("renamed_pose", unreal.RetargetSourceOrTarget.TARGET)`

Copy full snippet
```
\# Create a new retarget pose. rtg\_controller.create\_retarget\_pose("my\_new\_pose", unreal.RetargetSourceOrTarget.TARGET) # Duplicate the new pose. rtg\_controller.duplicate\_retarget\_pose("my\_new\_pose", "duplicated\_pose", unreal.RetargetSourceOrTarget.TARGET) # Rename the duplicate pose. rtg\_controller.rename\_retarget\_pose("duplicated\_pose", "renamed\_pose", unreal.RetargetSourceOrTarget.TARGET) # Remove the duplicate pose. rtg\_controller.remove\_retarget\_pose("renamed\_pose", unreal.RetargetSourceOrTarget.TARGET)

You can then set the current retarget pose to our newly created pose.

```

`rtg_controller.set_current_retarget_pose("my_new_pose", unreal.RetargetSourceOrTarget.TARGET)  print(rtg_controller.get_current_retarget_pose_name(unreal.RetargetSourceOrTarget.TARGET))`

Copy full snippet
```
rtg\_controller.set\_current\_retarget\_pose("my\_new\_pose", unreal.RetargetSourceOrTarget.TARGET) print(rtg\_controller.get\_current\_retarget\_pose\_name(unreal.RetargetSourceOrTarget.TARGET))

Now that you have a new retarget pose, you can use python scripts to edit the pose. The retarget root is the only bone that can have translation and rotation offset delta values in the retarget pose. For every other bone, the retarget pose will only store the relative rotation offset delta values.

For example, your Target's retarget root needs to be raised and flipped to be in the right direction. The following python script raises it 15 units up and rotate it 90 degrees:

```

`# Create a vector for the translation.  translation_offset = unreal.Vector()  translation_offset.z = 15  # Set the retarget root's translation offset.  rtg_controller.set_root_offset_in_retarget_pose(translation_offset, unreal.RetargetSourceOrTarget.TARGET)  print(rtg_controller.get_root_offset_in_retarget_pose(unreal.RetargetSourceOrTarget.TARGET))  # Create a rotator for the rotation.  rotation_offset = unreal.Rotator()  rotation_offset.roll = 90  # Set the retarget root's rotation offset, which works for any bone, and requires a defined bone name.  rtg_controller.set_rotation_offset_for_retarget_pose_bone("pelvis", rotation_offset.quaternion(), unreal.RetargetSourceOrTarget.TARGET)  print(rtg_controller.get_rotation_offset_for_retarget_pose_bone("pelvis", unreal.RetargetSourceOrTarget.TARGET))`

Copy full snippet
```
\# Create a vector for the translation. translation\_offset = unreal.Vector() translation\_offset.z = 15 # Set the retarget root's translation offset. rtg\_controller.set\_root\_offset\_in\_retarget\_pose(translation\_offset, unreal.RetargetSourceOrTarget.TARGET) print(rtg\_controller.get\_root\_offset\_in\_retarget\_pose(unreal.RetargetSourceOrTarget.TARGET)) # Create a rotator for the rotation. rotation\_offset = unreal.Rotator() rotation\_offset.roll = 90 # Set the retarget root's rotation offset, which works for any bone, and requires a defined bone name. rtg\_controller.set\_rotation\_offset\_for\_retarget\_pose\_bone("pelvis", rotation\_offset.quaternion(), unreal.RetargetSourceOrTarget.TARGET) print(rtg\_controller.get\_rotation\_offset\_for\_retarget\_pose\_bone("pelvis", unreal.RetargetSourceOrTarget.TARGET))

Finally, you can reset a list of bones back to their original transform.

```

`rtg_controller.reset_retarget_pose("my_new_pose", ["pelvis"], unreal.RetargetSourceOrTarget.TARGET)`

Copy full snippet
```
rtg\_controller.reset\_retarget\_pose("my\_new\_pose", \["pelvis"\], unreal.RetargetSourceOrTarget.TARGET)

### Auto Align Retarget Poses

```

`# Auto align all bones and apply to the target retarget pose. rtg_controller.auto_align_all_bones(unreal.RetargetSourceOrTarget.TARGET)   # Define a list of bones, align them to the source and apply to the target retarget pose. bones = ["spine_01", "spine_02", "spine_03"] rtg_controller.auto_align_bones(bones, unreal.RetargetAutoAlignMethod.CHAIN_TO_CHAIN, unreal.RetargetSourceOrTarget.TARGET)`

Copy full snippet
```
\# Auto align all bones and apply to the target retarget pose. rtg\_controller.auto\_align\_all\_bones(unreal.RetargetSourceOrTarget.TARGET) # Define a list of bones, align them to the source and apply to the target retarget pose. bones = \["spine\_01", "spine\_02", "spine\_03"\] rtg\_controller.auto\_align\_bones(bones, unreal.RetargetAutoAlignMethod.CHAIN\_TO\_CHAIN, unreal.RetargetSourceOrTarget.TARGET)

### Editing and Querying Global Settings

In the Retargeter, Global Settings is where you can edit the stride adjustment properties or the different phases of a retarget, such as the Retarget Root, FK, and IK. You can query and edit these phases using the following python scripts:

```

`# Get global settings, change IK, and set global settings.  global_settings = rtg_controller.get_global_settings()  global_settings.set_editor_property("enable_ik", False)  rtg_controller.set_global_settings(global_settings)`

Copy full snippet
```
\# Get global settings, change IK, and set global settings. global\_settings = rtg\_controller.get\_global\_settings() global\_settings.set\_editor\_property("enable\_ik", False) rtg\_controller.set\_global\_settings(global\_settings)

### Editing and Querying Root Settings

In the Retargeter, Root Settings is where you would edit any properties pertaining to the Retarget Root. This would allow translation or rotation offsets to the hips, scaling the vertical or horizontal motion, or how the IK goals are affected in the vertical or horizontal planes. You can query and edit these proiperties using the following python scripts:

```

`# Get root settings, raise hips by 10 units, set root settings.  root_settings = rtg_controller.get_root_settings()  root_settings.translation_offset = unreal.Vector(0,0,10)  rtg_controller.set_root_settings(root_settings)`

Copy full snippet
```
\# Get root settings, raise hips by 10 units, set root settings. root\_settings = rtg\_controller.get\_root\_settings() root\_settings.translation\_offset = unreal.Vector(0,0,10) rtg\_controller.set\_root\_settings(root\_settings)

### Editing and Querying Chain Settings

In the Retargeter, Chain Settings is where you would edit any properties pertaining to each of the Retarget Chains. For FK chains, this would be where you change the rotation retarget mode, or For IK chains, this would be where you edit if you want the IK goal to pin to the source location, add an offset to the IK, or vertically scale the IK. You can query and edit these properties using the following python scripts:

```

`# Get the left leg chain specifically.  left_leg_chain_settings = rtg_controller.get_retarget_chain_settings("LeftLeg")  # Alternatively, you can get a chain by querying from all chains and using a one line for loop conditional.  chains = rtg_controller.get_all_chain_settings()  left_leg_chain_settings = next((chain.settings for chain in chains if chain.source_chain == "LeftLeg"), None)  # Edit the FK settings.  left_leg_chain_settings.fk.rotation_mode = unreal.RetargetRotationMode.INTERPOLATED  left_leg_chain_settings.fk.pole_vector_matching = 1  # Edit the IK settings.  left_leg_chain_settings.ik.blend_to_source = 1  left_leg_chain_settings.ik.static_offset = unreal.Vector(0,5,0)  # Edit the Speed Plant settings.  left_leg_chain_settings.speed_planting.enable_speed_planting = True  left_leg_chain_settings.speed_planting.speed_curve_name = "ball_l_translation_speed_XYZ"  # Set the retarget chain settings.  rtg_controller.set_retarget_chain_settings("LeftLeg", left_leg_chain_settings)`

Copy full snippet
```
\# Get the left leg chain specifically. left\_leg\_chain\_settings = rtg\_controller.get\_retarget\_chain\_settings("LeftLeg") # Alternatively, you can get a chain by querying from all chains and using a one line for loop conditional. chains = rtg\_controller.get\_all\_chain\_settings() left\_leg\_chain\_settings = next((chain.settings for chain in chains if chain.source\_chain == "LeftLeg"), None) # Edit the FK settings. left\_leg\_chain\_settings.fk.rotation\_mode = unreal.RetargetRotationMode.INTERPOLATED left\_leg\_chain\_settings.fk.pole\_vector\_matching = 1 # Edit the IK settings. left\_leg\_chain\_settings.ik.blend\_to\_source = 1 left\_leg\_chain\_settings.ik.static\_offset = unreal.Vector(0,5,0) # Edit the Speed Plant settings. left\_leg\_chain\_settings.speed\_planting.enable\_speed\_planting = True left\_leg\_chain\_settings.speed\_planting.speed\_curve\_name = "ball\_l\_translation\_speed\_XYZ" # Set the retarget chain settings. rtg\_controller.set\_retarget\_chain\_settings("LeftLeg", left\_leg\_chain\_settings)

### Post Retarget phases

```

`# Load RTG_Mannequin asset  rtg = unreal.load_asset(name = '/Game/Characters/Mannequins/Rigs/RTG_Mannequin')  rtg_controller = unreal.IKRetargeterController.get_controller(rtg)  # Get number of operations  num_ops = rtg_controller.get_num_retarget_ops()  # Get first op object  first_op = rtg_controller.get_retarget_op_at_index(0)  # Get first op index  first_op_index = rtg_controller.get_index_of_retarget_op(first_op)  # See if op is enabled  is_op_enabled = rtg_controller.get_retarget_op_enabled(first_op_index)  # Set op to be disabled  rtg_controller.set_retarget_op_enabled(first_op_index, False)  # Check result  is_op_enabled = rtg_controller.get_retarget_op_enabled(first_op_index)  rtg_controller.set_retarget_op_enabled(first_op_index, True)  # Move op in stack  rtg_controller.move_retarget_op_in_stack(first_op_index, 1)  first_op_index = rtg_controller.get_index_of_retarget_op(first_op)  # Add Curve remap op  added_curve_op_index = rtg_controller.add_retarget_op(unreal.CurveRemapOp)  added_curve_op = rtg_controller.get_retarget_op_at_index(added_curve_op_index)  added_curve_op.set_editor_property("copy_all_source_curves", True)  curve_pair_element = unreal.CurveRemapPair()  curve_pair_element.set_editor_property("source_curve", "source")  curve_pair_element.set_editor_property("target_curve", "target")  added_curve_op.set_editor_property("curves_to_remap", [curve_pair_element])  # Remove op  rtg_controller.remove_retarget_op(added_curve_op_index)  # Add Pin Bone op  added_pin_bone_op_index = rtg_controller.add_retarget_op(unreal.PinBoneOp)  added_pin_bone_op = rtg_controller.get_retarget_op_at_index(added_pin_bone_op_index)  translate_vector = unreal.Vector()  translate_vector.x = 120  translate_vector.y = 120  translate_vector.z = 120  offset_transform = unreal.Transform()  offset_transform.translation = translate_vector  bone_pair_element = unreal.PinBoneData()  bone_pair_element.set_editor_property("bone_to_pin", "ik_foot_root")  bone_pair_element.set_editor_property("bone_to_pin_to", "root")  added_pin_bone_op.set_editor_property("pin_type", unreal.PinBoneType.ROTATE_ONLY)  added_pin_bone_op.set_editor_property("pin_to", unreal.RetargetSourceOrTarget.SOURCE)  added_pin_bone_op.set_editor_property("maintain_offset", False)  added_pin_bone_op.set_editor_property("local_offset", offset_transform)  added_pin_bone_op.set_editor_property("global_offset", offset_transform)  added_pin_bone_op.set_editor_property("bones_to_pin", [bone_pair_element])  # Remove op  rtg_controller.remove_retarget_op(added_pin_bone_op_index)  # Add Root Motion generator op - auto fills names of bones  added_rm_gen_op_index = rtg_controller.add_retarget_op(unreal.RootMotionGeneratorOp)  added_rm_gen_op = rtg_controller.get_retarget_op_at_index(added_rm_gen_op_index)  translate_vector = unreal.Vector()  translate_vector.x = 120  translate_vector.y = 120  translate_vector.z = 120  offset_transform = unreal.Transform()  offset_transform.translation = translate_vector  added_rm_gen_op.set_editor_property("global_offset", offset_transform)  added_rm_gen_op.set_editor_property("maintain_offset_from_pelvis", False)  added_rm_gen_op.set_editor_property("propagate_to_non_retargeted_children", True)  added_rm_gen_op.set_editor_property("root_height_source", unreal.RootMotionHeightSource.SNAP_TO_GROUND)  added_rm_gen_op.set_editor_property("root_motion_source", unreal.RootMotionSource.GENERATE_FROM_TARGET_PELVIS)  added_rm_gen_op.set_editor_property("rotate_with_pelvis", False)  # Remove op rtg_controller.remove_retarget_op(added_rm_gen_op_index)`

Copy full snippet
```
\# Load RTG\_Mannequin asset rtg = unreal.load\_asset(name = '/Game/Characters/Mannequins/Rigs/RTG\_Mannequin') rtg\_controller = unreal.IKRetargeterController.get\_controller(rtg) # Get number of operations num\_ops = rtg\_controller.get\_num\_retarget\_ops() # Get first op object first\_op = rtg\_controller.get\_retarget\_op\_at\_index(0) # Get first op index first\_op\_index = rtg\_controller.get\_index\_of\_retarget\_op(first\_op) # See if op is enabled is\_op\_enabled = rtg\_controller.get\_retarget\_op\_enabled(first\_op\_index) # Set op to be disabled rtg\_controller.set\_retarget\_op\_enabled(first\_op\_index, False) # Check result is\_op\_enabled = rtg\_controller.get\_retarget\_op\_enabled(first\_op\_index) rtg\_controller.set\_retarget\_op\_enabled(first\_op\_index, True) # Move op in stack rtg\_controller.move\_retarget\_op\_in\_stack(first\_op\_index, 1) first\_op\_index = rtg\_controller.get\_index\_of\_retarget\_op(first\_op) # Add Curve remap op added\_curve\_op\_index = rtg\_controller.add\_retarget\_op(unreal.CurveRemapOp) added\_curve\_op = rtg\_controller.get\_retarget\_op\_at\_index(added\_curve\_op\_index) added\_curve\_op.set\_editor\_property("copy\_all\_source\_curves", True) curve\_pair\_element = unreal.CurveRemapPair() curve\_pair\_element.set\_editor\_property("source\_curve", "source") curve\_pair\_element.set\_editor\_property("target\_curve", "target") added\_curve\_op.set\_editor\_property("curves\_to\_remap", \[curve\_pair\_element\]) # Remove op rtg\_controller.remove\_retarget\_op(added\_curve\_op\_index) # Add Pin Bone op added\_pin\_bone\_op\_index = rtg\_controller.add\_retarget\_op(unreal.PinBoneOp) added\_pin\_bone\_op = rtg\_controller.get\_retarget\_op\_at\_index(added\_pin\_bone\_op\_index) translate\_vector = unreal.Vector() translate\_vector.x = 120 translate\_vector.y = 120 translate\_vector.z = 120 offset\_transform = unreal.Transform() offset\_transform.translation = translate\_vector bone\_pair\_element = unreal.PinBoneData() bone\_pair\_element.set\_editor\_property("bone\_to\_pin", "ik\_foot\_root") bone\_pair\_element.set\_editor\_property("bone\_to\_pin\_to", "root") added\_pin\_bone\_op.set\_editor\_property("pin\_type", unreal.PinBoneType.ROTATE\_ONLY) added\_pin\_bone\_op.set\_editor\_property("pin\_to", unreal.RetargetSourceOrTarget.SOURCE) added\_pin\_bone\_op.set\_editor\_property("maintain\_offset", False) added\_pin\_bone\_op.set\_editor\_property("local\_offset", offset\_transform) added\_pin\_bone\_op.set\_editor\_property("global\_offset", offset\_transform) added\_pin\_bone\_op.set\_editor\_property("bones\_to\_pin", \[bone\_pair\_element\]) # Remove op rtg\_controller.remove\_retarget\_op(added\_pin\_bone\_op\_index) # Add Root Motion generator op - auto fills names of bones added\_rm\_gen\_op\_index = rtg\_controller.add\_retarget\_op(unreal.RootMotionGeneratorOp) added\_rm\_gen\_op = rtg\_controller.get\_retarget\_op\_at\_index(added\_rm\_gen\_op\_index) translate\_vector = unreal.Vector() translate\_vector.x = 120 translate\_vector.y = 120 translate\_vector.z = 120 offset\_transform = unreal.Transform() offset\_transform.translation = translate\_vector added\_rm\_gen\_op.set\_editor\_property("global\_offset", offset\_transform) added\_rm\_gen\_op.set\_editor\_property("maintain\_offset\_from\_pelvis", False) added\_rm\_gen\_op.set\_editor\_property("propagate\_to\_non\_retargeted\_children", True) added\_rm\_gen\_op.set\_editor\_property("root\_height\_source", unreal.RootMotionHeightSource.SNAP\_TO\_GROUND) added\_rm\_gen\_op.set\_editor\_property("root\_motion\_source", unreal.RootMotionSource.GENERATE\_FROM\_TARGET\_PELVIS) added\_rm\_gen\_op.set\_editor\_property("rotate\_with\_pelvis", False) # Remove op rtg\_controller.remove\_retarget\_op(added\_rm\_gen\_op\_index)

### Batch Retarget Animations with Duplicate and Retarget

For batch processing your retargeted animations, you can run the same command as duplicate and retarget in Python.

```

`# Use the asset subsystem to get asset data.  asset_subsystem = unreal.get_editor_subsystem(unreal.EditorAssetSubsystem)  # Get a list of asset data, which you can use for Anim Sequences, Anim Blueprints, Pose Assets, and more.  assets_to_retarget = [          asset_subsystem.find_asset_data("/Game/Characters/Mannequins/Animations/Manny/MM_Fall_Loop"),          asset_subsystem.find_asset_data("/Game/Characters/Mannequins/Animations/Manny/MM_Idle")]  retarget_asset = unreal.load_asset(name = '/Game/Characters/Mannequins/Rigs/RTG_Mannequin')  source_mesh = None # will use mesh from source ik rig  target_mesh = None # will use mesh from target ik rig  batch_op = unreal.IKRetargetBatchOperation.duplicate_and_retarget(                                                  assets_to_retarget,                                                  source_mesh,                                                  target_mesh,                                                  retarget_asset,                                                  search = "",                                                  replace = "",                                                  prefix = "",                                                  suffix = "",                                                  remap_referenced_assets = True)`

Copy full snippet
```
\# Use the asset subsystem to get asset data. asset\_subsystem = unreal.get\_editor\_subsystem(unreal.EditorAssetSubsystem) # Get a list of asset data, which you can use for Anim Sequences, Anim Blueprints, Pose Assets, and more. assets\_to\_retarget = \[ asset\_subsystem.find\_asset\_data("/Game/Characters/Mannequins/Animations/Manny/MM\_Fall\_Loop"), asset\_subsystem.find\_asset\_data("/Game/Characters/Mannequins/Animations/Manny/MM\_Idle")\] retarget\_asset = unreal.load\_asset(name = '/Game/Characters/Mannequins/Rigs/RTG\_Mannequin') source\_mesh = None # will use mesh from source ik rig target\_mesh = None # will use mesh from target ik rig batch\_op = unreal.IKRetargetBatchOperation.duplicate\_and\_retarget( assets\_to\_retarget, source\_mesh, target\_mesh, retarget\_asset, search = "", replace = "", prefix = "", suffix = "", remap\_referenced\_assets = True)