# Creating Levels of Detail in Blueprints and Python

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-levels-of-detail-in-blueprints-and-python-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-levels-of-detail-in-blueprints-and-python-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:39

---

Creating Levels of Detail (LODs) for your meshes can be a good way to increase the performance and frame rate of your game without sacrificing visual quality.

In general, the more triangles your meshes have, and the smaller those triangles are on screen, the harder it is for your GPU to render them. Trying to render too many detailed meshes all at the same time can slow down your frame rate. However, you typically don't need every mesh in the scene to be rendered with the same fidelity: when a mesh is far away, you are often able to swap it out for a less-detailed version of the mesh that contains fewer triangles without a noticeable difference in visual quality.

Unreal Engine 5 offers a built-in LOD management system that automatically chooses the most appropriate version of a mesh to show at runtime, based on the amount of screen space the mesh is currently occupying in each frame. This system relies on you setting up these different alternative versions of your meshes in the Editor ahead of time.

The Editor can generate these Levels of Detail for your Static Mesh assets automatically, by progressively simplifying the mesh to thresholds that you specify. For more information about how this system works and how to set it up in the Static Mesh Editor, see [Automatic LOD Generation](/documentation/en-us/unreal-engine/static-mesh-automatic-lod-generation-in-unreal-engine).

Click image for full size.

However, even though the Editor can generate these LODs automatically, it may not be feasible for you to open every Static Mesh Asset in your project one-by-one in order to set them all up. You could bulk edit the Assets, but this doesn't help if you want to apply different settings to different Static Mesh Assets based on their characteristics. For example, you might want to apply different reduction settings based on the number of existing triangles in the mesh, or based on an Asset naming convention. It also doesn't help if you want to create your LODs as a sub-step within a larger custom Asset pipeline that you've scripted. For these kinds of cases, you can use Blueprints or Python to script the automatic LOD creation system.

**Prerequisite:** If you haven't already done so, you'll need to install the **Editor Scripting Utilities Plugin**. For details, see [Scripting and Automating the Editor](/documentation/en-us/unreal-engine/scripting-and-automating-the-unreal-editor).

## Creating New Levels of Detail

Blueprints Python

You'll find the nodes you'll need to manage LODs under the **Editor Scripting > Static Mesh** category.

To use these nodes, your Blueprint class must be derived from an Editor-only class, such as the **PlacedEditorUtilityBase** class. For details, see [Scripting the Editor using Blueprints](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-blueprints).

-   The key node is **Set Lods**, which automatically creates levels of detail for the Static Mesh Asset you pass in. To use this node, you'll need to provide it with a set of reduction settings that define the screen size threshold and relative triangle percentage for each level of detail you want to create. See the example below.
    
    The first **EditorScriptingMeshReductionSettings** item that you pass to the **Reduction Settings** input of the **EditorScriptingMeshReductionOptions** node has no effect. LOD 0 always contains all triangles in the mesh.
    
-   You can use **Get Lod Count** and **Get Lod Screen Sizes** to get information about the Levels of Detail that are currently set up for a Static Mesh.
-   You can also use **Remove Lods** to remove all existing LODs (except LOD 0, which always contains all triangles in the mesh).
-   Setting up LODs modifies the Static Mesh Asset. Assuming you want to keep the changes you make, you'll also need to use a node like **Save Asset** or **Save Loaded Asset** afterward.

The following example loads each Static Mesh Asset in an input path in turn. Whenever it finds one that has more vertices than a minimum threshold, it sets up three additional LODs for the Static Mesh, and saves it afterward.

Click image for full size.

You'll find the LOD management functions in the `unreal.EditorStaticMeshLibrary` class.

-   The key function is `unreal.EditorStaticMeshLibrary.set_lods()`, which automatically creates levels of detail for the Static Mesh Asset you pass in. To use this function, you'll need to pass in an `EditorScriptingMeshReductionOptions` object, which contains a set of `EditorScriptingMeshReductionSettings` that define the screen size threshold and relative triangle percentage for each level of detail you want to create. See the example below.
    
    The first `EditorScriptingMeshReductionSettings` item that you set in the `EditorScriptingMeshReductionOptions.reduction_settings` array has no effect. LOD 0 always contains all triangles in the mesh.
    
-   You can use `unreal.EditorStaticMeshLibrary.get_lod_count()` and `unreal.EditorStaticMeshLibrary.get_lod_screen_sizes` to get information about the Levels of Detail that are currently set up for a Static Mesh.
-   You can also use `unreal.EditorStaticMeshLibrary.remove_lods()` to remove all existing LODs (except LOD 0, which always contains all triangles in the mesh).
-   Setting up LODs modifies the Static Mesh Asset. Assuming you want to keep the changes you make, you'll also need to use a function like `unreal.EditorAssetLibrary.save_asset()` or  `unreal.EditorAssetLibrary.save_loaded_asset()` afterward.

The following example loads each Static Mesh Asset in an input path in turn. Whenever it finds one that has more vertices than a minimum threshold, it sets up three additional LODs for the Static Mesh, and saves it afterward.

```
	`import unreal 	asset_path = "/Game/studio" 	# we define a function that generates new LODs for a specified Static Mesh Asset. 	def apply_lods(static_mesh): 		# check if the mesh is complex enough. 		number_of_vertices = unreal.EditorStaticMeshLibrary.get_number_verts(static_mesh, 0) 		if number_of_vertices < 10: 			return 		print("treating asset: " + static_mesh.get_name()) 		print("existing LOD count: " + str(unreal.EditorStaticMeshLibrary.get_lod_count(static_mesh))) 		# set up options for auto-generating the levels of detail. 		options = unreal.EditorScriptingMeshReductionOptions() 		# we request three new levels of detail. Each has: 		# - the percentage of the triangles from the fully detailed mesh that should be retained at this LOD level 		# - a screen space threshold at which this level of detail appears. 		options.reduction_settings = [ unreal.EditorScriptingMeshReductionSettings(1.0, 1.0), 			unreal.EditorScriptingMeshReductionSettings(0.8, 0.75), 			unreal.EditorScriptingMeshReductionSettings(0.6, 0.5), 			unreal.EditorScriptingMeshReductionSettings(0.4, 0.25) 		] 		# use the screen space thresholds set above, rather than auto-computing them. 		options.auto_compute_lod_screen_size = False 		# set the options on the Static Mesh Asset. 		unreal.EditorStaticMeshLibrary.set_lods(static_mesh, options) 		# save the changes. 		unreal.EditorAssetLibrary.save_loaded_asset(static_mesh) 		print("new LOD count: " + str(unreal.EditorStaticMeshLibrary.get_lod_count(static_mesh))) 	# get a list of all Assets in the path. 	all_assets = unreal.EditorAssetLibrary.list_assets(asset_path) 	# load them all into memory. 	all_assets_loaded = [unreal.EditorAssetLibrary.load_asset(a) for a in all_assets] 	# filter the list to include only Static Meshes. 	static_mesh_assets = unreal.EditorFilterLibrary.by_class(all_assets_loaded, unreal.StaticMesh) 	# run the function above on each Static Mesh in the list. 	list(map(apply_lods, static_mesh_assets))`

Copy full snippet
```
import unreal asset\_path = "/Game/studio" # we define a function that generates new LODs for a specified Static Mesh Asset. def apply\_lods(static\_mesh): # check if the mesh is complex enough. number\_of\_vertices = unreal.EditorStaticMeshLibrary.get\_number\_verts(static\_mesh, 0) if number\_of\_vertices < 10: return print("treating asset: " + static\_mesh.get\_name()) print("existing LOD count: " + str(unreal.EditorStaticMeshLibrary.get\_lod\_count(static\_mesh))) # set up options for auto-generating the levels of detail. options = unreal.EditorScriptingMeshReductionOptions() # we request three new levels of detail. Each has: # - the percentage of the triangles from the fully detailed mesh that should be retained at this LOD level # - a screen space threshold at which this level of detail appears. options.reduction\_settings = \[ unreal.EditorScriptingMeshReductionSettings(1.0, 1.0), unreal.EditorScriptingMeshReductionSettings(0.8, 0.75), unreal.EditorScriptingMeshReductionSettings(0.6, 0.5), unreal.EditorScriptingMeshReductionSettings(0.4, 0.25) \] # use the screen space thresholds set above, rather than auto-computing them. options.auto\_compute\_lod\_screen\_size = False # set the options on the Static Mesh Asset. unreal.EditorStaticMeshLibrary.set\_lods(static\_mesh, options) # save the changes. unreal.EditorAssetLibrary.save\_loaded\_asset(static\_mesh) print("new LOD count: " + str(unreal.EditorStaticMeshLibrary.get\_lod\_count(static\_mesh))) # get a list of all Assets in the path. all\_assets = unreal.EditorAssetLibrary.list\_assets(asset\_path) # load them all into memory. all\_assets\_loaded = \[unreal.EditorAssetLibrary.load\_asset(a) for a in all\_assets\] # filter the list to include only Static Meshes. static\_mesh\_assets = unreal.EditorFilterLibrary.by\_class(all\_assets\_loaded, unreal.StaticMesh) # run the function above on each Static Mesh in the list. list(map(apply\_lods, static\_mesh\_assets))

An alternative approach is to set the **LOD Group** option for each Static Mesh Asset. This option makes the mesh use one of the pre-set LOD reduction settings that are defined in the `[StaticMeshLODSettings]` section of your project's **BaseEngine.ini** file, such as `LevelArchitecture`, `SmallProp`, `LargeProp`, or `HighDetail`.

For example:

```
	`import unreal 	asset_path = "/Game/studio/" 	def set_high_detail(static_mesh): 		# Set the LOD group. 		static_mesh.set_editor_property("lod_group", "HighDetail") 		# Save the Asset. 		unreal.EditorAssetLibrary.save_loaded_asset(static_mesh) 	# get a list of all Assets in the path. 	all_assets = unreal.EditorAssetLibrary.list_assets(asset_path) 	# load them all into memory. 	all_assets_loaded = [unreal.EditorAssetLibrary.load_asset(a) for a in all_assets] 	# filter the list to include only Static Meshes. 	static_mesh_assets = unreal.EditorFilterLibrary.by_class(all_assets_loaded, unreal.StaticMesh) 	# run the function above on each Static Mesh in the list. 	list(map(set_high_detail, static_mesh_assets))`

Copy full snippet
```
import unreal asset\_path = "/Game/studio/" def set\_high\_detail(static\_mesh): # Set the LOD group. static\_mesh.set\_editor\_property("lod\_group", "HighDetail") # Save the Asset. unreal.EditorAssetLibrary.save\_loaded\_asset(static\_mesh) # get a list of all Assets in the path. all\_assets = unreal.EditorAssetLibrary.list\_assets(asset\_path) # load them all into memory. all\_assets\_loaded = \[unreal.EditorAssetLibrary.load\_asset(a) for a in all\_assets\] # filter the list to include only Static Meshes. static\_mesh\_assets = unreal.EditorFilterLibrary.by\_class(all\_assets\_loaded, unreal.StaticMesh) # run the function above on each Static Mesh in the list. list(map(set\_high\_detail, static\_mesh\_assets))

For more information about how this system works and how to use it in the Editor, see [Automatic LOD Generation](/documentation/en-us/unreal-engine/static-mesh-automatic-lod-generation-in-unreal-engine#usinglodgroups).

## Reusing a LOD from Another Static Mesh

As an alternative to generating LODs for a Static Mesh automatically using the process outlined above, you can take a LOD that already exists in a Static Mesh (called the *source* Static Mesh), and reuse it as a LOD for another Static Mesh (called the *destination* Static Mesh).

Blueprints Python

To reuse an existing LOD in a Blueprint script, use the **Editor Scripting > Static Mesh > Set Lod From Static Mesh** node.

Click image for full size.

This node needs the following input:

-   A reference to the target. It requires Static Mesh Editor Subsystem Object.
-   A reference to the destination Static Mesh. This is the Static Mesh that you want to create a new LOD for. You'll need to load this Asset first, using the **Editor Scripting > Asset > Load Asset** node.
-   The index of the LOD that you want to create for the destination Static Mesh.
    
    If the destination Static Mesh already has an LOD with the same index, it will be overwritten.
    
-   A reference to the source Static Mesh. This is the Static Mesh that has an existing LOD that you want to point to from the destination Static Mesh. As above, you'll need to load this Asset first, using the **Editor Scripting > Asset > Load Asset** node.
-   The index of the LOD within the source Static Mesh that you want to use for the destination Static Mesh.
-   A Boolean parameter that determines whether you want to try to merge Material slots in the source LOD with slots that already exist in the destination Static Mesh. If you enable this setting, then the function looks for any section in the source geometry that is assigned the same Material as a section in the destination mesh. If it finds any, it will try to remap the section in the LOD to match the existing section in the destination Static Mesh. This could save some memory in cases where both Static Meshes use the same Materials. If you leave this setting disabled, then all mesh sections from the source LOD are appended to the destination Static Mesh.

Setting the LOD modifies the destination Static Mesh Asset. Assuming you want to keep the changes you make, you'll also need to use a node like **Save Asset** or **Save Loaded Asset** afterward.

For example, the following script takes a specified LOD from a source Static Mesh, and reuses that geometry in a destination Static Mesh at a different specified LOD index:

Click image for full size.

When the **Set Lod from Static Mesh** node runs, a copy of the LOD from the source Static Mesh is added into the destination Static Mesh. There is no ongoing connection between the Static Mesh Assets, so any changes you make to the source Static Mesh from this point on will not automatically affect the destination Static Mesh.

To reuse a LOD in a Python script, call the `unreal.EditorStaticMeshLibrary.set_lod_from_static_mesh()` function. You need to pass this function:

-   The destination Static Mesh. This is the Static Mesh that you want to create a new LOD for. You'll need to load this Asset first, using the `unreal.EditorAssetLibrary.load_asset()` function.
-   The index of the LOD that you want to create for the destination Static Mesh. This value must be greater than 0. You cannot replace LOD 0 in the destination Static Mesh.
    
    If the destination Static Mesh already has an LOD with the same index, it will be overwritten.
    
-   The source Static Mesh. This is the Static Mesh that has an existing LOD that you want to point to from the destination Static Mesh. As above, you'll need to load this Asset first, using the `unreal.EditorAssetLibrary.load_asset()` function.
-   The index of the LOD within the source Static Mesh that you want to use for the destination Static Mesh.
-   A Boolean parameter that determines whether you want to try to merge Material slots in the destination Static Mesh. If you set this parameter to `True`, then the function looks for any section in the source geometry that is assigned the same Material as a section in the destination mesh. If it finds any, it will try to remap the section in the LOD to match the existing section in the destination Static Mesh. If you set this parameter to `False`, then all mesh sections from the source LOD are appended to the destination Static Mesh.

Setting up this LOD modifies the Static Mesh Asset. Assuming you want to keep the changes you make, you'll also need to use a function like `unreal.EditorAssetLibrary.save_asset()` or `unreal.EditorAssetLibrary.save_loaded_asset()` afterward.

For example, the following script takes LOD 0 from a simplified source Static Mesh, and reuses that geometry as LOD 1 in a more complex destination Static Mesh:

```
	`import unreal 	destination_name = "/Game/MyGeometries/Accumulator_case" 	source_name = "/Game/MyGeometries/Simplified_box" 	def set_mesh_as_lod(destination_name, source_name): 		destination_mesh = unreal.EditorAssetLibrary.load_asset(destination_name) 		source_mesh = unreal.EditorAssetLibrary.load_asset(source_name) 		lod_count = unreal.EditorStaticMeshLibrary.get_lod_count(destination_mesh) 		print("Current LOD count: " + str(lod_count)) 		slot_replaced = unreal.EditorStaticMeshLibrary.set_lod_from_static_mesh(destination_mesh, 1, source_mesh, 0, True) 		if slot_replaced > 0: 			print("Added mesh as LOD for slot " + str(slot_replaced)) 			lod_count = unreal.EditorStaticMeshLibrary.get_lod_count(destination_mesh) 			print("New LOD count: " + str(lod_count)) 			unreal.EditorAssetLibrary.save_loaded_asset(destination_mesh) 		else 			unreal.log_error("Unable to add mesh as LOD!") 	set_mesh_as_lod(destination_name, source_name)`

Copy full snippet
```
import unreal destination\_name = "/Game/MyGeometries/Accumulator\_case" source\_name = "/Game/MyGeometries/Simplified\_box" def set\_mesh\_as\_lod(destination\_name, source\_name): destination\_mesh = unreal.EditorAssetLibrary.load\_asset(destination\_name) source\_mesh = unreal.EditorAssetLibrary.load\_asset(source\_name) lod\_count = unreal.EditorStaticMeshLibrary.get\_lod\_count(destination\_mesh) print("Current LOD count: " + str(lod\_count)) slot\_replaced = unreal.EditorStaticMeshLibrary.set\_lod\_from\_static\_mesh(destination\_mesh, 1, source\_mesh, 0, True) if slot\_replaced > 0: print("Added mesh as LOD for slot " + str(slot\_replaced)) lod\_count = unreal.EditorStaticMeshLibrary.get\_lod\_count(destination\_mesh) print("New LOD count: " + str(lod\_count)) unreal.EditorAssetLibrary.save\_loaded\_asset(destination\_mesh) else unreal.log\_error("Unable to add mesh as LOD!") set\_mesh\_as\_lod(destination\_name, source\_name)

When the `unreal.EditorStaticMeshLibrary.set_lod_from_static_mesh()` function runs, a copy of the LOD from the source Static Mesh is added into the destination Static Mesh. There is no ongoing connection between the Static Mesh Assets, so any changes you make to the source Static Mesh from this point on will not automatically affect the destination Static Mesh.