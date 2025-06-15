# Using the Proxy Geometry Tool in Blueprints and Python

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-proxy-geometry-tool-in-blueprints-and-python-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-proxy-geometry-tool-in-blueprints-and-python-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:44

---

You can invoke the Proxy Geometry tool from Blueprint and Python scripts. This can help you automate your Asset creation and data preparation pipeline, combining and simplifying Static Mesh Actors and their Materials from scripts that you run inside the Unreal Editor. This can significantly improve rendering performance at the cost of some visual precision.

For example, this wheel assembly contains 147 separate Static Mesh Actors with a total of 900,000 triangles, with a separate Material for each mesh. This adds up to hundreds of heavy drawcalls on the GPU. After running the Proxy Geometry tool, the Actors are merged into a single model with a single Material, which can be rendered with one drawcall.

![Before: 147 Static Meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c6f4f18-c1aa-414a-b0d2-b108179200c5/proxygeom-wheel-before-1.png)

![After: 1 Static Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d269370b-5a35-461e-999f-c7e4d28dbef6/proxygeom-wheel-after.png)

The triangle count is also reduced by 97%. This has caused some deformation, but you can adjust the settings in your script to find the right balance between simplification and visual quality.

Because the Proxy Geometry tool involves some relatively complex transformations to your geometry, and offers many settings to control its operation, we recommend getting started with the tool by using it through its UI in the Editor. Move on to invoking it from scripts only when you are confident that you understand the tool, its settings, and have a good idea of the effects you're expecting. See the rest of the guides in this section for more information.

**Prerequisite:** If you haven't already done so, you'll need to install the Editor Scripting Utilities Plugin. For details, see [Scripting and Automating the Editor](/documentation/en-us/unreal-engine/scripting-and-automating-the-unreal-editor).

Blueprints Python

The Proxy Geometry tool is exposed through the **Editor Level Library > Create Proxy Mesh Actor** node.

![Create Proxy Mesh Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39c4b83e-a767-4d8a-a3d2-8ff58797fd54/proxy-scripting-createproxymeshactor.png "Create Proxy Mesh Actor")

You'll need to give this node the following inputs:

-   An Array that contains all Static Mesh Actors that you want to merge. Note that these must be Static Mesh Actors, not Actors that contain Static Mesh Components.
-   An **Editor Scripting Create Proxy Mesh Actor Options** object that contains the settings used by the proxy geometry tool. This object exposes most of the settings that are shown in the Proxy Geometry tool's UI. To get one of these objects, drag to the left from the **Merge Options** input, and choose **Make EditorScriptingCreateProxyMeshActorOptions**.
    
    Click for full image.
    
    Use this object to provide the settings for the Proxy Geometry tool. Many of the detailed settings are provided in another object, which you pass to the **Mesh Proxy Settings** input. To get one of these objects, repeat what you did above: drag left from the **Mesh Proxy Settings** input, and choose **Make MeshProxySettings**.
    
    Click for full image.
    

For example, the following snippet takes all the Actors that are currently selected in the Level Viewport and World Outliner, merges them together into a proxy mesh, saves the result to an Asset with a specified name and location, and replaces the original Static Mesh Actors in the Level with a single instance of the newly generated proxy Asset.

Click for full image.

The Proxy Geometry tool is exposed through the `unreal.EditorLevelLibrary.create_proxy_mesh_actor()` function. You'll need to pass this function the following parameters:

-   An Array that contains all of the Static Mesh Actors that you want to merge. Note that these must be Static Mesh Actors, not Actors that contain Static Mesh Components.
-   An `unreal.EditorScriptingCreateProxyMeshActorOptions` object that contains the settings to be used by the proxy geometry tool. This object exposes most of the settings that are shown in the Proxy Geometry tool's UI. You'll need to create one of these objects and set up its properties.

For example, the following snippet takes all the Static Mesh Actors in the Level, merges them together into a proxy mesh, saves the result to an Asset called Proxy, and swaps out the original Static Mesh Actors in the Level for a single instance of the Proxy Asset.

```
	`import unreal 	actors = unreal.EditorLevelLibrary.get_selected_level_actors() 	merge_options = unreal.EditorScriptingCreateProxyMeshActorOptions() 	merge_options.base_package_name = "/Game/Proxy" 	merge_options.destroy_source_actors = False 	merge_options.new_actor_label = "Proxy" 	merge_options.spawn_merged_actor = True 	merge_options.mesh_proxy_settings.set_editor_property("allow_adjacency", False) 	merge_options.mesh_proxy_settings.set_editor_property("allow_distance_field", False) 	merge_options.mesh_proxy_settings.set_editor_property("allow_vertex_colors", False) 	merge_options.mesh_proxy_settings.set_editor_property("calculate_correct_lod_model", True) 	merge_options.mesh_proxy_settings.set_editor_property("compute_light_map_resolution", True) 	merge_options.mesh_proxy_settings.set_editor_property("create_collision", False) 	merge_options.mesh_proxy_settings.set_editor_property("generate_lightmap_u_vs", True) 	merge_options.mesh_proxy_settings.set_editor_property("merge_distance", 1.0) 	merge_options.mesh_proxy_settings.set_editor_property("voxel_size", 0.1) 	merged_actor = unreal.EditorLevelLibrary.create_proxy_mesh_actor(actors, merge_options)`
Copy full snippet
```
import unreal actors = unreal.EditorLevelLibrary.get\_selected\_level\_actors() merge\_options = unreal.EditorScriptingCreateProxyMeshActorOptions() merge\_options.base\_package\_name = "/Game/Proxy" merge\_options.destroy\_source\_actors = False merge\_options.new\_actor\_label = "Proxy" merge\_options.spawn\_merged\_actor = True merge\_options.mesh\_proxy\_settings.set\_editor\_property("allow\_adjacency", False) merge\_options.mesh\_proxy\_settings.set\_editor\_property("allow\_distance\_field", False) merge\_options.mesh\_proxy\_settings.set\_editor\_property("allow\_vertex\_colors", False) merge\_options.mesh\_proxy\_settings.set\_editor\_property("calculate\_correct\_lod\_model", True) merge\_options.mesh\_proxy\_settings.set\_editor\_property("compute\_light\_map\_resolution", True) merge\_options.mesh\_proxy\_settings.set\_editor\_property("create\_collision", False) merge\_options.mesh\_proxy\_settings.set\_editor\_property("generate\_lightmap\_u\_vs", True) merge\_options.mesh\_proxy\_settings.set\_editor\_property("merge\_distance", 1.0) merge\_options.mesh\_proxy\_settings.set\_editor\_property("voxel\_size", 0.1) merged\_actor = unreal.EditorLevelLibrary.create\_proxy\_mesh\_actor(actors, merge\_options)