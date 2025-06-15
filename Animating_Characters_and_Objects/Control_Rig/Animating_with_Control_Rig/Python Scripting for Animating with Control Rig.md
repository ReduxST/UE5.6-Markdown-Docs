# Python Scripting for Animating with Control Rig

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/python-scripting-for-animating-with-control-rig-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/python-scripting-for-animating-with-control-rig-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:16

---

[Python scripting](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python) can be used to automate and control various parts of animating your **Control Rig** in **Sequencer**. This document provides an overview of the main ways to use Python with animating your Control Rig, [Animation Mode](/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine), and other various animation workflows.

#### Prerequisites

-   You have some experience with [Python scripting in Unreal Engine](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python), as well as [scripting in Sequencer](/documentation/en-us/unreal-engine/python-scripting-in-sequencer-in-unreal-engine).
-   You have an understanding of creating and using [Control Rigs](/documentation/en-us/unreal-engine/control-rig-in-unreal-engine).

## Create an FK Control Rig Track

Creating a Control Rig track is slightly different from normally [creating Tracks in Sequencer](/documentation/en-us/unreal-engine/python-scripting-in-sequencer-in-unreal-engine#creatingtracksandsections). A Control Rig track needs to have a Control Rig class defined to be created. To create a Control Rig Track, use the following commands:

```
`# Get the Editor world editor_system = unreal.get_editor_subsystem(unreal.UnrealEditorSubsystem) world = editor_system.get_editor_world()   # Get the rig class rig_class = unreal.FKControlRig.static_class()   # Using the level sequence and actor binding, we can either find or create a control rig track from the class rig_track = unreal.ControlRigSequencerLibrary.find_or_create_control_rig_track(world, level_sequence, rig_class, actor_binding)   # Get actor_binding from default mesh level_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get_focused_level_sequence() skeletal_mesh_component = rig.get_preview_mesh() actor_binding = level_sequence.add_spawnable_from_instance(skeletal_mesh_component)  # Get actor_binding from skeletal mesh path skeletal_mesh_component = unreal.load_asset(skeletal_mesh_path) actor_binding = level_sequence.add_spawnable_from_instance(skeletal_mesh_component)`
Copy full snippet
```
\# Get the Editor world editor\_system = unreal.get\_editor\_subsystem(unreal.UnrealEditorSubsystem) world = editor\_system.get\_editor\_world() # Get the rig class rig\_class = unreal.FKControlRig.static\_class() # Using the level sequence and actor binding, we can either find or create a control rig track from the class rig\_track = unreal.ControlRigSequencerLibrary.find\_or\_create\_control\_rig\_track(world, level\_sequence, rig\_class, actor\_binding) # Get actor\_binding from default mesh level\_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get\_focused\_level\_sequence() skeletal\_mesh\_component = rig.get\_preview\_mesh() actor\_binding = level\_sequence.add\_spawnable\_from\_instance(skeletal\_mesh\_component) # Get actor\_binding from skeletal mesh path skeletal\_mesh\_component = unreal.load\_asset(skeletal\_mesh\_path) actor\_binding = level\_sequence.add\_spawnable\_from\_instance(skeletal\_mesh\_component)

## Create a Control Rig Track

Same as an FK Control Rig Track, you need to get the specific Control Rig class:

```
`# Get the Editor world world = unreal.EditorLevelLibrary.get_editor_world()  # Get the control rig asset rig = unreal.load_asset("/Game/Animation/ControlRig/Mannequin_ControlRig")  # Get the rig class rig_class = rig.get_control_rig_class()  # Using the level sequence and actor binding, we can either find or create a control rig track from the class rig_track = unreal.ControlRigSequencerLibrary.find_or_create_control_rig_track(world,level_sequence, rig_class, actor_binding)`
Copy full snippet
```
\# Get the Editor world world = unreal.EditorLevelLibrary.get\_editor\_world() # Get the control rig asset rig = unreal.load\_asset("/Game/Animation/ControlRig/Mannequin\_ControlRig") # Get the rig class rig\_class = rig.get\_control\_rig\_class() # Using the level sequence and actor binding, we can either find or create a control rig track from the class rig\_track = unreal.ControlRigSequencerLibrary.find\_or\_create\_control\_rig\_track(world,level\_sequence, rig\_class, actor\_binding)

## Layered Control Rig

### Create a Layered Control Rig Track

Creating a Layered Control Rig track is the same as adding a normal Control Rig track, but using the `is_layered` keyword argument on `find_or_create_control_rig_track`.

```
`# Get the Editor world editor_system = unreal.get_editor_subsystem(unreal.UnrealEditorSubsystem) world = editor_system.get_editor_world()   # Get the control rig asset rig = unreal.load_asset("/Game/Animation/ControlRig/Mannequin_ControlRig")   # Get the rig class rig_class = rig.get_control_rig_class()   # Using the level sequence and actor binding, we can either find or create a control rig track from the class rig_track = unreal.ControlRigSequencerLibrary.find_or_create_control_rig_track(world, level_sequence, rig_class, actor_binding, is_layered_control_rig = True)`
Copy full snippet
```
\# Get the Editor world editor\_system = unreal.get\_editor\_subsystem(unreal.UnrealEditorSubsystem) world = editor\_system.get\_editor\_world() # Get the control rig asset rig = unreal.load\_asset("/Game/Animation/ControlRig/Mannequin\_ControlRig") # Get the rig class rig\_class = rig.get\_control\_rig\_class() # Using the level sequence and actor binding, we can either find or create a control rig track from the class rig\_track = unreal.ControlRigSequencerLibrary.find\_or\_create\_control\_rig\_track(world, level\_sequence, rig\_class, actor\_binding, is\_layered\_control\_rig = True)

### Check If Control Rig Is Layered

In the cases where you need to determine if a Control Rig is layered or not, you can check from the Control Rig object from the `ControlRigSequencerBindingProxy` instance.

```
`# Get the first Control Rig in Sequencer, then get the Rig object rig_proxy = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)[0] rig = rig_proxy.control_rig   print(unreal.ControlRigSequencerLibrary.is_layered_control_rig(rig))`
Copy full snippet
```
\# Get the first Control Rig in Sequencer, then get the Rig object rig\_proxy = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence)\[0\] rig = rig\_proxy.control\_rig print(unreal.ControlRigSequencerLibrary.is\_layered\_control\_rig(rig))

### Change Rig Evaluation Order

You can layer multiple Control Rigs and change the priority order. Similar to Hierarchal Bias with Subsequences, Layered Control Rigs operate with the highest number evaluating first. For example, if `FKControlRig` is set to `100` and `CR_Mannequin_Body` is set to `99`, then the `FKControlRig` will evaluate first.

```
`# Get rigs inside Sequencer rigs = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)   # Loop through each rig for rig in rigs:       rig_track = rig.track     rig_obj = rig.control_rig       # get and set the priority order print(unreal.ControlRigSequencerLibrary.get_control_rig_priority_order(rig_track)) unreal.ControlRigSequencerLibrary.set_control_rig_priority_order(rig_track, 200)`
Copy full snippet
```
\# Get rigs inside Sequencer rigs = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Loop through each rig for rig in rigs: rig\_track = rig.track rig\_obj = rig.control\_rig # get and set the priority order print(unreal.ControlRigSequencerLibrary.get\_control\_rig\_priority\_order(rig\_track)) unreal.ControlRigSequencerLibrary.set\_control\_rig\_priority\_order(rig\_track, 200)

### Change Layered Mode

You can also change the mode by changing it on the rig track:

```
`unreal.ControlRigSequencerLibrary.set_control_rig_layered_mode(rig_track, True)`
Copy full snippet
```
unreal.ControlRigSequencerLibrary.set\_control\_rig\_layered\_mode(rig\_track, True)

## Masking Sections

For sections where you want to show only some controls, you can set the masking within Python:

```
`# Get the control rig track and the section to key ls = unreal.LevelSequenceEditorBlueprintLibrary.get_current_level_sequence() rig = unreal.ControlRigSequencerLibrary.get_control_rigs(ls)[0] rig_track = rig.track keyed_section = rig_track.get_section_to_key()   # Hide these specific controls on the keyed section ctrls = ["thigh_l_fk_ctrl", "calf_l_fk_ctrl", "foot_l_fk_ctrl", "ball_l_fk_ctrl"] unreal.ControlRigSequencerLibrary.set_controls_mask(keyed_section, ctrls, False)   # Show all controls unreal.ControlRigSequencerLibrary.show_all_controls(keyed_section)`
Copy full snippet
```
\# Get the control rig track and the section to key ls = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_level\_sequence() rig = unreal.ControlRigSequencerLibrary.get\_control\_rigs(ls)\[0\] rig\_track = rig.track keyed\_section = rig\_track.get\_section\_to\_key() # Hide these specific controls on the keyed section ctrls = \["thigh\_l\_fk\_ctrl", "calf\_l\_fk\_ctrl", "foot\_l\_fk\_ctrl", "ball\_l\_fk\_ctrl"\] unreal.ControlRigSequencerLibrary.set\_controls\_mask(keyed\_section, ctrls, False) # Show all controls unreal.ControlRigSequencerLibrary.show\_all\_controls(keyed\_section)

## Animating Controls

The following examples explain a variety of ways you can edit and animate controls.

### Control Selection

These commands can be used to select controls and query control selection:

```
`# Get the Control Rigs in Sequencer, returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Get the first proxy, assuming it is Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Selects a specified control rig.select_control("body_ctrl")  # Get the current control selection selected_controls = rig.current_control_selection() print(selected_controls)  # Clear the control selection rig.clear_control_selection()`
Copy full snippet
```
\# Get the Control Rigs in Sequencer, returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Get the first proxy, assuming it is Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Selects a specified control rig.select\_control("body\_ctrl") # Get the current control selection selected\_controls = rig.current\_control\_selection() print(selected\_controls) # Clear the control selection rig.clear\_control\_selection()

### Get and Set Control Values

You can get specific values from any of the controls at any given frame number with the following commands:

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Get frame 0 frame_num = unreal.FrameNumber(0)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Gets the local control values, each control type will have their own typed function transform = unreal.ControlRigSequencerLibrary.get_local_control_rig_transform(level_sequence, rig, "body_ctrl", frame_num) bool = unreal.ControlRigSequencerLibrary.get_local_control_rig_bool(level_sequence, rig, "twist_ctrl_vis", frame_num)  print(transform) print(bool)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Get frame 0 frame\_num = unreal.FrameNumber(0) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Gets the local control values, each control type will have their own typed function transform = unreal.ControlRigSequencerLibrary.get\_local\_control\_rig\_transform(level\_sequence, rig, "body\_ctrl", frame\_num) bool = unreal.ControlRigSequencerLibrary.get\_local\_control\_rig\_bool(level\_sequence, rig, "twist\_ctrl\_vis", frame\_num) print(transform) print(bool)

You can also set specific values on any of the controls at any given frame number using these commands:

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Get the current time current_time = unreal.LevelSequenceEditorBlueprintLibrary.get_current_time()  # Convert current time to a FrameNumber object current_frame = unreal.FrameNumber(current_time)  # Create the proper value objects for the controls transform_value = unreal.Transform(location=[0, 10, 20], rotation=[0,30,0], scale=[1,1,1])  bool_value = True  # Sets the local control values, each control type will have their own typed function # Each typed function will also have a set_key flag that is by default True unreal.ControlRigSequencerLibrary.set_local_control_rig_transform(level_sequence, rig, "body_ctrl", frame_num, transform_value) unreal.ControlRigSequencerLibrary.set_local_control_rig_bool(level_sequence, rig, "twist_ctrl_vis", frame_num, bool_value, set_key = False)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Get the current time current\_time = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_time() # Convert current time to a FrameNumber object current\_frame = unreal.FrameNumber(current\_time) # Create the proper value objects for the controls transform\_value = unreal.Transform(location=\[0, 10, 20\], rotation=\[0,30,0\], scale=\[1,1,1\]) bool\_value = True # Sets the local control values, each control type will have their own typed function # Each typed function will also have a set\_key flag that is by default True unreal.ControlRigSequencerLibrary.set\_local\_control\_rig\_transform(level\_sequence, rig, "body\_ctrl", frame\_num, transform\_value) unreal.ControlRigSequencerLibrary.set\_local\_control\_rig\_bool(level\_sequence, rig, "twist\_ctrl\_vis", frame\_num, bool\_value, set\_key = False)

## Keyframes

### Querying Selected Keyframes

```
`# Get channels from selected keys - assuming there was is a selection keyed_channels = unreal.LevelSequenceEditorBlueprintLibrary.get_channels_with_selected_keys()   # Get select keys selected_keys = unreal.LevelSequenceEditorBlueprintLibrary.get_selected_keys(keyed_channels[0])   # Getting channel object channel_obj = keyed_channels[0].section.get_channel(keyed_channels[0].channel_name)   # Convert key indices to key objects key_objs = channel_obj.get_keys_by_index(selected_keys)   # Print all the time values from the selected keys for key_obj in key_objs: print(key_obj.get_time().frame_number.value)`
Copy full snippet
```
\# Get channels from selected keys - assuming there was is a selection keyed\_channels = unreal.LevelSequenceEditorBlueprintLibrary.get\_channels\_with\_selected\_keys() # Get select keys selected\_keys = unreal.LevelSequenceEditorBlueprintLibrary.get\_selected\_keys(keyed\_channels\[0\]) # Getting channel object channel\_obj = keyed\_channels\[0\].section.get\_channel(keyed\_channels\[0\].channel\_name) # Convert key indices to key objects key\_objs = channel\_obj.get\_keys\_by\_index(selected\_keys) # Print all the time values from the selected keys for key\_obj in key\_objs: print(key\_obj.get\_time().frame\_number.value)

### Editing Keyframe Selection

The following example assumes that there is a level sequence using the Mannequin/MH Control Rig with keys on `hand_l_fk_ctrl`.

```
`ls = unreal.LevelSequenceEditorBlueprintLibrary.get_current_level_sequence() start_frame = ls.get_playback_start() end_frame = ls.get_playback_end()   # Get control rig rig = unreal.ControlRigSequencerLibrary.get_control_rigs(ls)[0] rig_track = rig.track keyed_section = rig_track.get_section_to_key()   # Getting channel proxy by providing a simple channel name sc = unreal.SequencerChannelProxy() sc.section = keyed_section sc.channel_name = 'hand_l_fk_ctrl.Location.X'   # Get channel object and get all key objects channel_obj = keyed_section.get_channel('hand_l_fk_ctrl.Location.X') keys = channel_obj.get_keys()   # Empty array for keys to select timed_keys = []   # Loop through all the keys for key in keys:       # Get the key time     key_time = key.get_time().frame_number.value       # Check if the key's time is right after start frame and right before end frame     if key_time >= start_frame+1 and key_time <= end_frame-1:           # Add key to array         timed_keys.append(keys.index(key))   # Select keys unreal.LevelSequenceEditorBlueprintLibrary.select_keys(sc, timed_keys)`
Copy full snippet
```
ls = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_level\_sequence() start\_frame = ls.get\_playback\_start() end\_frame = ls.get\_playback\_end() # Get control rig rig = unreal.ControlRigSequencerLibrary.get\_control\_rigs(ls)\[0\] rig\_track = rig.track keyed\_section = rig\_track.get\_section\_to\_key() # Getting channel proxy by providing a simple channel name sc = unreal.SequencerChannelProxy() sc.section = keyed\_section sc.channel\_name = 'hand\_l\_fk\_ctrl.Location.X' # Get channel object and get all key objects channel\_obj = keyed\_section.get\_channel('hand\_l\_fk\_ctrl.Location.X') keys = channel\_obj.get\_keys() # Empty array for keys to select timed\_keys = \[\] # Loop through all the keys for key in keys: # Get the key time key\_time = key.get\_time().frame\_number.value # Check if the key's time is right after start frame and right before end frame if key\_time >= start\_frame+1 and key\_time <= end\_frame-1: # Add key to array timed\_keys.append(keys.index(key)) # Select keys unreal.LevelSequenceEditorBlueprintLibrary.select\_keys(sc, timed\_keys)

## Curve Editor

```
`# Getting the curve editor ses = unreal.get_editor_subsystem(unreal.LevelSequenceEditorSubsystem) curve_editor = ses.get_curve_editor() if not curve_editor.is_curve_editor_open(): curve_editor.open_curve_editor()   # Get selected keys and channels keyed_channels = curve_editor.get_channels_with_selected_keys() selected_keys = curve_editor.get_selected_keys(keyed_channels[0]) curve_editor.empty_selection()   # Reselect every key curve_editor.select_keys(selected_keys)   # getting channel object channel_obj = keyed_channels[0].section.get_channel(keyed_channels[0].channel_name)   # Convert key indices to key objects key_objs = channel_obj.get_keys_by_index(selected_keys)   # Print all the times of the selected keys for key_obj in key_objs: print(key_obj.get_time())   # Close the curve editor curve_editor.close_curve_editor()`
Copy full snippet
```
\# Getting the curve editor ses = unreal.get\_editor\_subsystem(unreal.LevelSequenceEditorSubsystem) curve\_editor = ses.get\_curve\_editor() if not curve\_editor.is\_curve\_editor\_open(): curve\_editor.open\_curve\_editor() # Get selected keys and channels keyed\_channels = curve\_editor.get\_channels\_with\_selected\_keys() selected\_keys = curve\_editor.get\_selected\_keys(keyed\_channels\[0\]) curve\_editor.empty\_selection() # Reselect every key curve\_editor.select\_keys(selected\_keys) # getting channel object channel\_obj = keyed\_channels\[0\].section.get\_channel(keyed\_channels\[0\].channel\_name) # Convert key indices to key objects key\_objs = channel\_obj.get\_keys\_by\_index(selected\_keys) # Print all the times of the selected keys for key\_obj in key\_objs: print(key\_obj.get\_time()) # Close the curve editor curve\_editor.close\_curve\_editor()

## Load Animation Sequence into Control Rig Sections

```
`level_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get_focused_level_sequence() rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence) rig_proxy = rig_proxies[0] sequencer_binding_proxy = rig_proxy.proxy   # Frame at which to insert animation start_frame = unreal.FrameNumber(0)   # Gather movie scene section from control rig cr_tracks = sequencer_binding_proxy.find_tracks_by_type(unreal.MovieSceneControlRigParameterTrack) cr_movie_scene_section = cr_tracks[0].get_section_to_key()   # Bring in the animation to apply anim_sequence = "/Game/Characters/Mannequins/Animations/Manny/MM_Walk_Fwd" anim_sequence = unreal.load_asset(anim_sequence)   # Get the skeletal mesh component seq_bindings = level_sequence.get_bindings() playback_range = level_sequence.get_playback_range() editor_system = unreal.get_editor_subsystem(unreal.UnrealEditorSubsystem) world = editor_system.get_editor_world() bound_objects = unreal.SequencerTools.get_bound_objects(world, level_sequence, seq_bindings, playback_range) # Note: assuming first bound object has the skeletal mesh skel_mesh_comp = bound_objects[0].bound_objects[0].skeletal_mesh_component   # load animation into CR (uses backwards solve graph under the hood) unreal.ControlRigSequencerLibrary.load_anim_sequence_into_control_rig_section(cr_movie_scene_section, anim_sequence, skel_mesh_comp, start_frame, reset_controls = True)`      
Copy full snippet
```
level\_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get\_focused\_level\_sequence() rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) rig\_proxy = rig\_proxies\[0\] sequencer\_binding\_proxy = rig\_proxy.proxy # Frame at which to insert animation start\_frame = unreal.FrameNumber(0) # Gather movie scene section from control rig cr\_tracks = sequencer\_binding\_proxy.find\_tracks\_by\_type(unreal.MovieSceneControlRigParameterTrack) cr\_movie\_scene\_section = cr\_tracks\[0\].get\_section\_to\_key() # Bring in the animation to apply anim\_sequence = "/Game/Characters/Mannequins/Animations/Manny/MM\_Walk\_Fwd" anim\_sequence = unreal.load\_asset(anim\_sequence) # Get the skeletal mesh component seq\_bindings = level\_sequence.get\_bindings() playback\_range = level\_sequence.get\_playback\_range() editor\_system = unreal.get\_editor\_subsystem(unreal.UnrealEditorSubsystem) world = editor\_system.get\_editor\_world() bound\_objects = unreal.SequencerTools.get\_bound\_objects(world, level\_sequence, seq\_bindings, playback\_range) # Note: assuming first bound object has the skeletal mesh skel\_mesh\_comp = bound\_objects\[0\].bound\_objects\[0\].skeletal\_mesh\_component # load animation into CR (uses backwards solve graph under the hood) unreal.ControlRigSequencerLibrary.load\_anim\_sequence\_into\_control\_rig\_section(cr\_movie\_scene\_section, anim\_sequence, skel\_mesh\_comp, start\_frame, reset\_controls = True)

## Animation Mode

[Animation Mode Tools](/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine#animationmodetools) can also be affected with Python scripting. The following examples are provided.

### Tween Tool

The following commands can be used for the [Tween Tool](/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine#tweenstool):

```
`# Set tween value between -1 - 1 # -1 will blend to previous frame # 1 will blend to next frame tween_value = -1  unreal.ControlRigSequencerLibrary.tween_control_rig(level_sequence, rig, tween_value)`
Copy full snippet
```
\# Set tween value between -1 - 1 # -1 will blend to previous frame # 1 will blend to next frame tween\_value = -1 unreal.ControlRigSequencerLibrary.tween\_control\_rig(level\_sequence, rig, tween\_value)

### Snapper Tool

The following commands can be used for the [Snapper Tool](/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine#snappertool). If the driver object is animated, then the driver object has to be added to the active sequence.

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Get the editor actor subsystem to add an actor editor_actor_subsystem = unreal.get_editor_subsystem(unreal.EditorActorSubsystem)  # Add a cube to the editor world and set the location cube_mesh = unreal.load_asset("/Engine/BasicShapes/Cube") cube_location = unreal.Vector(0, 10, 20) cube_actor = editor_actor_subsystem.spawn_actor_from_object(cube_mesh, cube_location)  # Set start and end frame ranges start_frame = unreal.FrameNumber(0) end_frame = unreal.FrameNumber(5)  # Create ControlRigSnapperSelection objects for the parent and the children parent = unreal.ControlRigSnapperSelection() children = unreal.ControlRigSnapperSelection()  # Create an ActorForWorldTransforms object # Set the cube actor as the parent parent_actor = unreal.ActorForWorldTransforms() parent_actor.actor = cube_actor  # Create a ControlRigForWorldTransforms object # Set to the proper control rig and the left hand control as the control # It is possible to have multiple control names in here child_control_rig = unreal.ControlRigForWorldTransforms() child_control_rig.control_rig = rig child_control_rig.control_names = ["hand_l_ctrl"]  # Take the ActorForWorldTransforms object, set it as the parent ControlRigSnapperSelection # Take the ControlRigForWorldTransforms object, set as the child ControlRigSnapperSelection parent.actors = [parent_actor] children.control_rigs = [child_control_rig]  # Create and set snap settings snap_settings = unreal.ControlRigSnapSettings() snap_settings.keep_offset = False snap_settings.snap_position = True snap_settings.snap_rotation = True snap_settings.snap_scale = False  # Then snap the left hand control to the cube from frame 0-5 unreal.ControlRigSequencerLibrary.snap_control_rig(level_sequence, start_frame, end_frame, children, parent, snap_settings)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Get the editor actor subsystem to add an actor editor\_actor\_subsystem = unreal.get\_editor\_subsystem(unreal.EditorActorSubsystem) # Add a cube to the editor world and set the location cube\_mesh = unreal.load\_asset("/Engine/BasicShapes/Cube") cube\_location = unreal.Vector(0, 10, 20) cube\_actor = editor\_actor\_subsystem.spawn\_actor\_from\_object(cube\_mesh, cube\_location) # Set start and end frame ranges start\_frame = unreal.FrameNumber(0) end\_frame = unreal.FrameNumber(5) # Create ControlRigSnapperSelection objects for the parent and the children parent = unreal.ControlRigSnapperSelection() children = unreal.ControlRigSnapperSelection() # Create an ActorForWorldTransforms object # Set the cube actor as the parent parent\_actor = unreal.ActorForWorldTransforms() parent\_actor.actor = cube\_actor # Create a ControlRigForWorldTransforms object # Set to the proper control rig and the left hand control as the control # It is possible to have multiple control names in here child\_control\_rig = unreal.ControlRigForWorldTransforms() child\_control\_rig.control\_rig = rig child\_control\_rig.control\_names = \["hand\_l\_ctrl"\] # Take the ActorForWorldTransforms object, set it as the parent ControlRigSnapperSelection # Take the ControlRigForWorldTransforms object, set as the child ControlRigSnapperSelection parent.actors = \[parent\_actor\] children.control\_rigs = \[child\_control\_rig\] # Create and set snap settings snap\_settings = unreal.ControlRigSnapSettings() snap\_settings.keep\_offset = False snap\_settings.snap\_position = True snap\_settings.snap\_rotation = True snap\_settings.snap\_scale = False # Then snap the left hand control to the cube from frame 0-5 unreal.ControlRigSequencerLibrary.snap\_control\_rig(level\_sequence, start\_frame, end\_frame, children, parent, snap\_settings)

### Space Switching

The following commands and examples can be used for [Space Switching](/documentation/en-us/unreal-engine/re-parent-control-rig-controls-in-real-time-in-unreal-engine).

To start space switching, you will need to create space keyframes. You can set a control's space to its default parent, world space, or to another control at any given frame number.

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Set the space of the left hand control to world space at frame 0 control_name = "hand_l_ctrl" space = unreal.ControlRigSequencerLibrary.get_world_space_reference_key() time = unreal.FrameNumber(value = 0)  unreal.ControlRigSequencerLibrary.set_control_rig_space(level_sequence, rig, control_name, space, time)  # Afterwards, set space switch to the head control at frame 30 space = unreal.RigElementKey(type = unreal.RigElementType.CONTROL, name = "head_ctrl") time = unreal.FrameNumber(value = 30)  unreal.ControlRigSequencerLibrary.set_control_rig_space(level_sequence, rig, control_name, space, time)  # Then lastly, set space switch to it's default parent at frame 60 space = unreal.ControlRigSequencerLibrary.get_default_parent_key() time = unreal.FrameNumber(value = 60)  unreal.ControlRigSequencerLibrary.set_control_rig_space(level_sequence, rig, control_name, space, time)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Set the space of the left hand control to world space at frame 0 control\_name = "hand\_l\_ctrl" space = unreal.ControlRigSequencerLibrary.get\_world\_space\_reference\_key() time = unreal.FrameNumber(value = 0) unreal.ControlRigSequencerLibrary.set\_control\_rig\_space(level\_sequence, rig, control\_name, space, time) # Afterwards, set space switch to the head control at frame 30 space = unreal.RigElementKey(type = unreal.RigElementType.CONTROL, name = "head\_ctrl") time = unreal.FrameNumber(value = 30) unreal.ControlRigSequencerLibrary.set\_control\_rig\_space(level\_sequence, rig, control\_name, space, time) # Then lastly, set space switch to it's default parent at frame 60 space = unreal.ControlRigSequencerLibrary.get\_default\_parent\_key() time = unreal.FrameNumber(value = 60) unreal.ControlRigSequencerLibrary.set\_control\_rig\_space(level\_sequence, rig, control\_name, space, time)

Once space keyframes are created, you can move them to any frame number by using these commands:

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Let's assume from the Set Space Key example that we have space keys at 0, 30, and 60 # on the left hand control. Let's move the space key from frame 30 to frame 45 control_name = "hand_l_ctrl" old_time = unreal.FrameNumber(value = 30) new_time = unreal.FrameNumber(value = 45)  unreal.ControlRigSequencerLibrary.move_control_rig_space(level_sequence, rig, control_name, old_time, new_time)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Let's assume from the Set Space Key example that we have space keys at 0, 30, and 60 # on the left hand control. Let's move the space key from frame 30 to frame 45 control\_name = "hand\_l\_ctrl" old\_time = unreal.FrameNumber(value = 30) new\_time = unreal.FrameNumber(value = 45) unreal.ControlRigSequencerLibrary.move\_control\_rig\_space(level\_sequence, rig, control\_name, old\_time, new\_time)

Space keyframes can be deleted by using these commands:

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Let's assume from the Move Space Key example that we have space keys at 0, 345 and 60 # on the left hand control. Let's remove the space key from frame 45 control_name = "hand_l_ctrl" time = unreal.FrameNumber(value = 45)  unreal.ControlRigSequencerLibrary.delete_control_rig_space(level_sequence, rig, control_name, time)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Let's assume from the Move Space Key example that we have space keys at 0, 345 and 60 # on the left hand control. Let's remove the space key from frame 45 control\_name = "hand\_l\_ctrl" time = unreal.FrameNumber(value = 45) unreal.ControlRigSequencerLibrary.delete\_control\_rig\_space(level\_sequence, rig, control\_name, time)

You can bake the final animation to a specific space by using the following commands:

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig  # Get all selected rig controls control_names = rig.current_control_selection()  # Get the start and end frame from the level sequence, create FrameNumber objects for bake settings start_frame_num = level_sequence.get_playback_start() end_frame_num = level_sequence.get_playback_end()  start_frame = unreal.FrameNumber(value = start_frame_num) end_frame = unreal.FrameNumber(value = end_frame_num)  # Set baking settings for space, we will be baking to the default parent space  space_bake_settings = unreal.RigSpacePickerBakeSettings() space_bake_settings.target_space = unreal.ControlRigSequencerLibrary.get_default_parent_key() space_bake_settings.start_frame = start_frame space_bake_settings.end_frame = end_frame space_bake_settings.reduce_keys = False space_bake_settings.tolerance = 0  unreal.ControlRigSequencerLibrary.bake_control_rig_space(level_sequence, rig, control_names, space_bake_settings)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Get all selected rig controls control\_names = rig.current\_control\_selection() # Get the start and end frame from the level sequence, create FrameNumber objects for bake settings start\_frame\_num = level\_sequence.get\_playback\_start() end\_frame\_num = level\_sequence.get\_playback\_end() start\_frame = unreal.FrameNumber(value = start\_frame\_num) end\_frame = unreal.FrameNumber(value = end\_frame\_num) # Set baking settings for space, we will be baking to the default parent space space\_bake\_settings = unreal.RigSpacePickerBakeSettings() space\_bake\_settings.target\_space = unreal.ControlRigSequencerLibrary.get\_default\_parent\_key() space\_bake\_settings.start\_frame = start\_frame space\_bake\_settings.end\_frame = end\_frame space\_bake\_settings.reduce\_keys = False space\_bake\_settings.tolerance = 0 unreal.ControlRigSequencerLibrary.bake\_control\_rig\_space(level\_sequence, rig, control\_names, space\_bake\_settings)

### Animation Mode Settings

[Animation Mode Settings](/documentation/en-us/unreal-engine/python-scripting-for-animating-with-control-rig-in-unreal-engine#animationmodesettings) can be edited using Python scripting. Each property uses the following terminology:

| Name | Description |
| --- | --- |
| **bDisplayHierarchy** | Draws Bones on the character. |
| **bDisplayNulls** | Draws Nulls on the character. |
| **bHideManipulators** | Hides all Controls in the Viewport. This will also hide Bones and Nulls if **Display Hierarchy** or **Display Nulls** are enabled. |
| **bCoordSystemPerWidgetMode** | Restores the coordinate space when changing Gizmo modes in the Viewport. |
| **bOnlySelectRigControls** | Enabling this will only make Control Rig controls be selectable in the Viewport. All other objects, including the character, will not be selectable. |
| **bLocalTransformsInEachLocalSpace** | Enabling this will transform each selected control relative to their local transform space, if your transformation gizmo is set to local coordinates. |
| **GizmoScale** | Increases or decreases the gizmo scale. |

The following commands can be used:

```
`# load the mode settings class and get default object ControlRigSettingsClass = unreal.load_class(None, '/Script/ControlRigEditor.ControlRigEditModeSettings') ControlRigSettings = unreal.get_default_object(ControlRigSettingsClass)  # print out the queried data print(ControlRigSettings.get_editor_property('bDisplayHierarchy')) print(ControlRigSettings.get_editor_property('bDisplayNulls')) print(ControlRigSettings.get_editor_property(GizmoScale))  # set the properties ControlRigSettings.set_editor_property('bDisplayHierarchy', True) ControlRigSettings.set_editor_property('bDisplayNulls', True) ControlRigSettings.set_editor_property('GizmoScale', 5)`
Copy full snippet
```
\# load the mode settings class and get default object ControlRigSettingsClass = unreal.load\_class(None, '/Script/ControlRigEditor.ControlRigEditModeSettings') ControlRigSettings = unreal.get\_default\_object(ControlRigSettingsClass) # print out the queried data print(ControlRigSettings.get\_editor\_property('bDisplayHierarchy')) print(ControlRigSettings.get\_editor\_property('bDisplayNulls')) print(ControlRigSettings.get\_editor\_property(GizmoScale)) # set the properties ControlRigSettings.set\_editor\_property('bDisplayHierarchy', True) ControlRigSettings.set\_editor\_property('bDisplayNulls', True) ControlRigSettings.set\_editor\_property('GizmoScale', 5)

## Constraints

Constraints are used to create a relationship between one object to another. This can be useful for animation authoring. Constraints can be added to animated and non-animated scenarios.

### Have a Camera Look At Constrained to a Cube without Sequencer

```
`import unreal   # Create a camera camera_location = unreal.Vector(0.0,0.0,200.0) camera_actor = unreal.EditorLevelLibrary().spawn_actor_from_class(unreal.CineCameraActor, camera_location) camera_actor.set_actor_label('CineCameraActor')   # Create a cube obj = unreal.load_asset("/Engine/BasicShapes/Cube") cube_location = unreal.Vector(400.0,0.0,200.0) cube_actor = unreal.EditorLevelLibrary().spawn_actor_from_object(obj, cube_location) cube_actor.set_actor_label('CubeActor')   # Get the Editor world world = unreal.EditorLevelLibrary().get_editor_world()   # Create a constraints library constraints_lib = unreal.ConstraintsScriptingLibrary()   # Create child handle to the camera child_handle = constraints_lib.create_transformable_component_handle(world, camera_actor.root_component, "")   # Create parent handle to the cube parent_handle = constraints_lib.create_transformable_component_handle(world, cube_actor.root_component, "")   # Create and add the constraint (note that this will create the constraints manager if needed) look_at_constraint = constraints_lib.create_from_type(world, unreal.TransformConstraintType.LOOK_AT) constraints_lib.add_constraint(world, parent_handle, child_handle, look_at_constraint, True)`
Copy full snippet
```
import unreal # Create a camera camera\_location = unreal.Vector(0.0,0.0,200.0) camera\_actor = unreal.EditorLevelLibrary().spawn\_actor\_from\_class(unreal.CineCameraActor, camera\_location) camera\_actor.set\_actor\_label('CineCameraActor') # Create a cube obj = unreal.load\_asset("/Engine/BasicShapes/Cube") cube\_location = unreal.Vector(400.0,0.0,200.0) cube\_actor = unreal.EditorLevelLibrary().spawn\_actor\_from\_object(obj, cube\_location) cube\_actor.set\_actor\_label('CubeActor') # Get the Editor world world = unreal.EditorLevelLibrary().get\_editor\_world() # Create a constraints library constraints\_lib = unreal.ConstraintsScriptingLibrary() # Create child handle to the camera child\_handle = constraints\_lib.create\_transformable\_component\_handle(world, camera\_actor.root\_component, "") # Create parent handle to the cube parent\_handle = constraints\_lib.create\_transformable\_component\_handle(world, cube\_actor.root\_component, "") # Create and add the constraint (note that this will create the constraints manager if needed) look\_at\_constraint = constraints\_lib.create\_from\_type(world, unreal.TransformConstraintType.LOOK\_AT) constraints\_lib.add\_constraint(world, parent\_handle, child\_handle, look\_at\_constraint, True)

### Have a Control Rig Control Parent Constrained to a Cube with Sequencer

```
`# Get the current level sequence level_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get_current_level_sequence()   # Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)   # Grab the first proxy- let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]   # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig_proxy.control_rig   # Get the first selected control selected_ctrl = rig.current_control_selection()[0]   # Create a cube that will drive the control obj = unreal.load_asset("/Engine/BasicShapes/Cube") cube_location = unreal.Vector(400.0,0.0,200.0) cube_actor = unreal.EditorLevelLibrary().spawn_actor_from_object(obj, cube_location)   # Get the world world = unreal.EditorLevelLibrary().get_editor_world()   # Create a Constraints scripting library object constraints_lib = unreal.ConstraintsScriptingLibrary()   # Create a child handle for the Control Rig Control child_handle = rig.create_transformable_control_handle(selected_ctrl)   # Create a parent handle for the cube parent_handle = constraints_lib.create_transformable_component_handle(world, cube_actor.root_component, "")   # Create a Parent Constraint object parent_constraint = constraints_lib.create_from_type(world, unreal.TransformConstraintType.PARENT)   # Add the constraint with the handles, turn off maintain offset constraints_lib.add_constraint(world, parent_handle, child_handle, parent_constraint, False)`
Copy full snippet
```
\# Get the current level sequence level\_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_level\_sequence() # Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy- let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the ControlRig object rig = rig\_proxy.control\_rig # Get the first selected control selected\_ctrl = rig.current\_control\_selection()\[0\] # Create a cube that will drive the control obj = unreal.load\_asset("/Engine/BasicShapes/Cube") cube\_location = unreal.Vector(400.0,0.0,200.0) cube\_actor = unreal.EditorLevelLibrary().spawn\_actor\_from\_object(obj, cube\_location) # Get the world world = unreal.EditorLevelLibrary().get\_editor\_world() # Create a Constraints scripting library object constraints\_lib = unreal.ConstraintsScriptingLibrary() # Create a child handle for the Control Rig Control child\_handle = rig.create\_transformable\_control\_handle(selected\_ctrl) # Create a parent handle for the cube parent\_handle = constraints\_lib.create\_transformable\_component\_handle(world, cube\_actor.root\_component, "") # Create a Parent Constraint object parent\_constraint = constraints\_lib.create\_from\_type(world, unreal.TransformConstraintType.PARENT) # Add the constraint with the handles, turn off maintain offset constraints\_lib.add\_constraint(world, parent\_handle, child\_handle, parent\_constraint, False)

## Baking and Merging

### Bake to Control Rig

If you already have an animation sequence on your Actor in Sequencer, you can create a Control Rig Track by baking the current animation to a Control Rig. To do this, use the following commands:

```
`# Get the current editor level editor_system = unreal.get_editor_subsystem(unreal.UnrealEditorSubsystem) world = editor_system.get_editor_world()  # Get the animation sequence export options anim_seq_export_options = unreal.AnimSeqExportOption() anim_seq_export_options.export_transforms = True anim_seq_export_options.export_curves = True  # Get key tolerance number and key reduction state tolerance = 0.01 reduce_keys = False  # Bake to Control Rig unreal.ControlRigSequencerLibrary.bake_to_control_rig(world, level_sequence, rig_class, anim_seq_export_options, False, tolerance, actor_binding)`
Copy full snippet
```
\# Get the current editor level editor\_system = unreal.get\_editor\_subsystem(unreal.UnrealEditorSubsystem) world = editor\_system.get\_editor\_world() # Get the animation sequence export options anim\_seq\_export\_options = unreal.AnimSeqExportOption() anim\_seq\_export\_options.export\_transforms = True anim\_seq\_export\_options.export\_curves = True # Get key tolerance number and key reduction state tolerance = 0.01 reduce\_keys = False # Bake to Control Rig unreal.ControlRigSequencerLibrary.bake\_to\_control\_rig(world, level\_sequence, rig\_class, anim\_seq\_export\_options, False, tolerance, actor\_binding)

### Bake to Animation Sequence

Once a Control Rig animation is completed, you can export the animation as an Animation Sequence to be used in other areas of Unreal Engine by using the following commands:

```
`# Get the current level sequence level_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get_current_level_sequence()  # Get the SkeletaMeshActor binding called SK Mannequin # This is the default name when dragging a Mannequin_ControlRig into the Level Editor binding = level_sequence.find_binding_by_name("SK Mannequin")  # Grab the Level Editor World editor_subsystem = unreal.get_editor_subsystem(unreal.UnrealEditorSubsystem) world = editor_subsystem.get_editor_world()  # Create animation sequence export options anim_seq_export_options = unreal.AnimSeqExportOption() anim_seq_export_options.export_transforms = True anim_seq_export_options.export_morph_targets = True  # Get asset tools # Create an empty AnimSequence - /Game/Test_Anim asset_tools = unreal.AssetToolsHelpers.get_asset_tools() anim_sequence = unreal.AssetTools.create_asset(asset_tools, asset_name = "Test_Anim", package_path = "/Game/", asset_class = unreal.AnimSequence, factory = unreal.AnimSequenceFactory())  # Bake to the created AnimSequence unreal.SequencerTools.export_anim_sequence(world, level_sequence, anim_sequence, anim_seq_export_options, binding, False)  # If we want to create a linked animation sequence, simply change the last arg to True unreal.SequencerTools.export_anim_sequence(world, level_sequence, anim_sequence, anim_seq_export_options, binding, True)`
Copy full snippet
```
\# Get the current level sequence level\_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_level\_sequence() # Get the SkeletaMeshActor binding called SK Mannequin # This is the default name when dragging a Mannequin\_ControlRig into the Level Editor binding = level\_sequence.find\_binding\_by\_name("SK Mannequin") # Grab the Level Editor World editor\_subsystem = unreal.get\_editor\_subsystem(unreal.UnrealEditorSubsystem) world = editor\_subsystem.get\_editor\_world() # Create animation sequence export options anim\_seq\_export\_options = unreal.AnimSeqExportOption() anim\_seq\_export\_options.export\_transforms = True anim\_seq\_export\_options.export\_morph\_targets = True # Get asset tools # Create an empty AnimSequence - /Game/Test\_Anim asset\_tools = unreal.AssetToolsHelpers.get\_asset\_tools() anim\_sequence = unreal.AssetTools.create\_asset(asset\_tools, asset\_name = "Test\_Anim", package\_path = "/Game/", asset\_class = unreal.AnimSequence, factory = unreal.AnimSequenceFactory()) # Bake to the created AnimSequence unreal.SequencerTools.export\_anim\_sequence(world, level\_sequence, anim\_sequence, anim\_seq\_export\_options, binding, False) # If we want to create a linked animation sequence, simply change the last arg to True unreal.SequencerTools.export\_anim\_sequence(world, level\_sequence, anim\_sequence, anim\_seq\_export\_options, binding, True)

### Merging Animation Layers

If you are using multiple sections and layers within the Control Rig Track, you can bake and merge their animations into a single layer using these collapse commands:

```
`# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig_proxies = unreal.ControlRigSequencerLibrary.get_control_rigs(level_sequence)  # Grab the first proxy - let's assume it is the Mannequin_ControlRig rig_proxy = rig_proxies[0]  # From the ControlRigSequencerBindingProxy, we can get the MovieSceneControlRigParameterTrack object # With the track, we can collapse all the sections in the track to one section rig_track = rig_proxy.track  unreal.ControlRigSequencerLibrary.collapse_control_rig_anim_layers (level_sequence, rig_track, key_reduce = False, tolerance = 0.001)`
Copy full snippet
```
\# Get the Control Rigs in Sequencer - returns a list of ControlRigSequencerBindingProxy rig\_proxies = unreal.ControlRigSequencerLibrary.get\_control\_rigs(level\_sequence) # Grab the first proxy - let's assume it is the Mannequin\_ControlRig rig\_proxy = rig\_proxies\[0\] # From the ControlRigSequencerBindingProxy, we can get the MovieSceneControlRigParameterTrack object # With the track, we can collapse all the sections in the track to one section rig\_track = rig\_proxy.track unreal.ControlRigSequencerLibrary.collapse\_control\_rig\_anim\_layers (level\_sequence, rig\_track, key\_reduce = False, tolerance = 0.001)

### Accessing Linked Animation Sequences from a Level Sequence

```
`# We will first get the current level sequence level_sequence  = unreal.LevelSequenceEditorBlueprintLibrary.get_current_level_sequence()   # Then check if there are any links to animation sequences link_check = unreal.SequencerTools.get_anim_sequence_link_from_level_sequence(level_sequence)   # If there are... if link_check:       # Get the links     links = link_check.anim_sequence_links       # Loop through each link     for link in links:           # Get the soft object path         anim_seq_soft_path = link.path_to_anim_sequence           # Resolve it to get the asset         anim_seq = unreal.SystemLibrary.conv_soft_obj_path_to_soft_obj_ref(anim_seq_soft_path)`
Copy full snippet
```
\# We will first get the current level sequence level\_sequence = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_level\_sequence() # Then check if there are any links to animation sequences link\_check = unreal.SequencerTools.get\_anim\_sequence\_link\_from\_level\_sequence(level\_sequence) # If there are... if link\_check: # Get the links links = link\_check.anim\_sequence\_links # Loop through each link for link in links: # Get the soft object path anim\_seq\_soft\_path = link.path\_to\_anim\_sequence # Resolve it to get the asset anim\_seq = unreal.SystemLibrary.conv\_soft\_obj\_path\_to\_soft\_obj\_ref(anim\_seq\_soft\_path)

### Accessing Linked Level Sequences from an Animation Sequence

```
`# Let's assume we have a linked animation sequence called Test_Anim in the Content folder anim_seq = unreal.load_object("/Game/Test_Anim")   # See if there is a link link = unreal.SequencerTools.get_level_sequence_link_from_anim_sequence(anim_seq)   # If there is... if link:       # Get the soft object path     level_seq_soft_path = link.path_to_level_sequence       # Resolve it to get the asset     level_seq = unreal.SystemLibrary.conv_soft_obj_path_to_soft_obj_ref(level_seq_soft_path)`

Copy full snippet
```
\# Let's assume we have a linked animation sequence called Test\_Anim in the Content folder anim\_seq = unreal.load\_object("/Game/Test\_Anim") # See if there is a link link = unreal.SequencerTools.get\_level\_sequence\_link\_from\_anim\_sequence(anim\_seq) # If there is... if link: # Get the soft object path level\_seq\_soft\_path = link.path\_to\_level\_sequence # Resolve it to get the asset level\_seq = unreal.SystemLibrary.conv\_soft\_obj\_path\_to\_soft\_obj\_ref(level\_seq\_soft\_path)

## FBX Export and import

### FBX Export

```
`# Get the level sequence and the rig section ls = unreal.LevelSequenceEditorBlueprintLibrary.get_current_level_sequence() rig = unreal.ControlRigSequencerLibrary.get_control_rigs(ls)[0] rig_track = rig.track keyed_section = rig_track.get_section_to_key() filename = "D:/test.fbx"   # Create export fbx settings with the filename export_fbx_settings = unreal.MovieSceneUserExportFBXControlRigSettings() export_fbx_settings.set_editor_property("ascii", True) export_fbx_settings.set_editor_property("export_file_name", filename)   # Export the Control Rig FBX unreal.ControlRigSequencerLibrary.export_fbx_from_control_rig_section(ls, keyed_section, export_fbx_settings)`
Copy full snippet
```
\# Get the level sequence and the rig section ls = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_level\_sequence() rig = unreal.ControlRigSequencerLibrary.get\_control\_rigs(ls)\[0\] rig\_track = rig.track keyed\_section = rig\_track.get\_section\_to\_key() filename = "D:/test.fbx" # Create export fbx settings with the filename export\_fbx\_settings = unreal.MovieSceneUserExportFBXControlRigSettings() export\_fbx\_settings.set\_editor\_property("ascii", True) export\_fbx\_settings.set\_editor\_property("export\_file\_name", filename) # Export the Control Rig FBX unreal.ControlRigSequencerLibrary.export\_fbx\_from\_control\_rig\_section(ls, keyed\_section, export\_fbx\_settings)

### FBX Import

```
`# Get the level sequence and the rig track & section and the editor world ls = unreal.LevelSequenceEditorBlueprintLibrary.get_current_level_sequence() rig = unreal.ControlRigSequencerLibrary.get_control_rigs(ls)[0] rig_track = rig.track keyed_section = rig_track.get_section_to_key() editor_system = unreal.get_editor_subsystem(unreal.UnrealEditorSubsystem) world = editor_system.get_editor_world()   # Create a list for selected controls, only works if import_onto_selected_controls is set to True selected_ctrls = ["thigh_l_fk_ctrl", "calf_l_fk_ctrl", "foot_l_fk_ctrl", "ball_l_fk_ctrl"]   # Create import settings object, assign settings and file name import_fbx_settings = unreal.MovieSceneUserImportFBXControlRigSettings() import_fbx_settings.set_editor_property("import_onto_selected_controls", True) import_fbx_settings.set_editor_property("insert_animation", True) fbx_file = "D:/test.fbx"   # Import the Control Rig FBX unreal.ControlRigSequencerLibrary.import_fbx_to_control_rig_track(world, ls, rig_track, keyed_section, selected_ctrls, import_fbx_settings, fbx_file)`
Copy full snippet
```
\# Get the level sequence and the rig track & section and the editor world ls = unreal.LevelSequenceEditorBlueprintLibrary.get\_current\_level\_sequence() rig = unreal.ControlRigSequencerLibrary.get\_control\_rigs(ls)\[0\] rig\_track = rig.track keyed\_section = rig\_track.get\_section\_to\_key() editor\_system = unreal.get\_editor\_subsystem(unreal.UnrealEditorSubsystem) world = editor\_system.get\_editor\_world() # Create a list for selected controls, only works if import\_onto\_selected\_controls is set to True selected\_ctrls = \["thigh\_l\_fk\_ctrl", "calf\_l\_fk\_ctrl", "foot\_l\_fk\_ctrl", "ball\_l\_fk\_ctrl"\] # Create import settings object, assign settings and file name import\_fbx\_settings = unreal.MovieSceneUserImportFBXControlRigSettings() import\_fbx\_settings.set\_editor\_property("import\_onto\_selected\_controls", True) import\_fbx\_settings.set\_editor\_property("insert\_animation", True) fbx\_file = "D:/test.fbx" # Import the Control Rig FBX unreal.ControlRigSequencerLibrary.import\_fbx\_to\_control\_rig\_track(world, ls, rig\_track, keyed\_section, selected\_ctrls, import\_fbx\_settings, fbx\_file)

## Editing Animation Mode Window

When animating with Control Rig in the Level Editor and Sequencer, the Animation Mode window will pop up with tools and options that an animator would need. These options are also editable via Python.

The Animation Mode window includes the following properties:

-   **bDisplayHierarchy**: Draws lines and dots for each control and bone in the control rig
-   **bDisplayNulls**: Draws lines and dots for each null in the control rig
-   **bHideManipulators**: Hides all the controls and displays in the control rig
-   **bCoordSystemPerWidgetMode**: Option to maintain local/global space manipulator state per translate, rotate, and scale mode
-   **bOnlySelectRigControls**: Allows only viewport selection of control rig controls
-   **bLocalTransformsInEachLocalSpace**: When transform multiple selected controls, each control will transform in their own local space
-   **GizmoScale**: Change the scale of the viewport gizmo manipulator

```
`# load the mode settings class and get default object ControlRigSettingsClass = unreal.load_class(None, '/Script/ControlRigEditor.ControlRigEditModeSettings')  ControlRigSettings = unreal.get_default_object(ControlRigSettingsClass)    # print out the queried data print(ControlRigSettings.get_editor_property('bDisplayHierarchy')) print(ControlRigSettings.get_editor_property('bDisplayNulls')) print(ControlRigSettings.get_editor_property(GizmoScale))   # set the properties ControlRigSettings.set_editor_property('bDisplayHierarchy', True) ControlRigSettings.set_editor_property('bDisplayNulls', True) ControlRigSettings.set_editor_property('GizmoScale', 5)`
Copy full snippet
```
\# load the mode settings class and get default object ControlRigSettingsClass = unreal.load\_class(None, '/Script/ControlRigEditor.ControlRigEditModeSettings') ControlRigSettings = unreal.get\_default\_object(ControlRigSettingsClass) # print out the queried data print(ControlRigSettings.get\_editor\_property('bDisplayHierarchy')) print(ControlRigSettings.get\_editor\_property('bDisplayNulls')) print(ControlRigSettings.get\_editor\_property(GizmoScale)) # set the properties ControlRigSettings.set\_editor\_property('bDisplayHierarchy', True) ControlRigSettings.set\_editor\_property('bDisplayNulls', True) ControlRigSettings.set\_editor\_property('GizmoScale', 5)