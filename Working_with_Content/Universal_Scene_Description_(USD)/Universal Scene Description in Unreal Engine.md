# Universal Scene Description in Unreal Engine

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/universal-scene-description-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/universal-scene-description-in-unreal-engine)  
**Processed:** 2025-06-14 16:55:55

---

Films, games, and other 3D graphic productions often generate, store, and transmit a great deal of data. This data can come from a variety of softwares (such as Unreal Engine, Maya, Houdini, or Blender) from within the art pipeline that each have their own proprietary form of scene description.

The **Universal Scene Description (USD)** interchange format is an open-source format developed by Pixar to address the need to robustly and scalably interchange and augment arbitrary 3D scenes that may be composed of many elemental assets. USD not only provides a rich toolset for reading, writing, editing, and rapidly previewing 3D geometry and shading, but it also provides for the interchange of elemental assets (for example, models) or animations.

Unlike other interchange packages, USD also enables assembly and organization of any number of assets into virtual sets, scenes, and shots. You can then transmit these from application to application, and non-destructively edit them (as overrides), with a single, consistent API, in a single scenegraph.

## Why use USD?

USD provides a common language for moving significant amounts of data between multiple 3D applications. This provides flexibility when making decisions about your art pipeline and facilitates collaboration between multiple 3D artists (animators, lighting or shading artists, modelers, FX artists, and more) using iterative and non-destructive methods.

## USD Support in Unreal Engine

Unreal Engine provides USD support through the **USD Stage** panel and bi-directional **Python** workflows.

The USD Stage window. Click image for full size.

Rather than converting USD data into native Unreal Engine Assets like Static Meshes and Materials, the USD Stage workflow works natively with your USD data. This makes it faster to get your USD data into Unreal Engine, gives you a clearer view of how your USD content was originally structured, and handles live updates as you make changes to the source USD file on disk.

The USD Stage provides the following functionality:

-   Represents 3D data as "prims": static meshes, skeletal meshes, HISM, Materials, Lights, Cameras, Variants, Animation, and Blend shapes.
-   Non-destructive attribute editing.
-   USD scene graph and hierarchy visualization.
-   Loading and unloading content using Payloads.
-   Support for Textures with USD Preview Surfaces.
-   Support for Materials with PreviewSurface and DisplayColor.
-   Support for USD Plugins such as Alembic and Custom path Resolver.
-   USD features supported at runtime. For more information, see [USD Runtime Support](/documentation/en-us/unreal-engine/universal-scene-description-in-unreal-engine#usdruntimesupport).
-   Loads `.usd`, `.usda`, `.usdc`, and `.usdz` formats.

For more general information on Universal Scene Description, see Pixar's [Introduction to USD](https://graphics.pixar.com/usd/docs/index.html).

For more information on working with the Python workflow, see [Python Scripting](/documentation/en-us/unreal-engine/universal-scene-description-in-unreal-engine#pythonscripting).

## Supported Actions

### Importing Into Unreal Engine

Content that is displayed on the USD Stage (**Static Meshes**, **Skeletal Meshes**, **Lights**, **Foliage**, and **Landscapes**) can be imported into Unreal Engine using the following methods:

-   Using **File > Import Into Level**. This process will import both Assets (static mesh, skeletal mesh, materials, textures, and so on) and Actors.
-   Using the **Add/Import** button in the Content Browser. This process will only import assets.
-   Dragging and dropping the file into the Content Browser. This process will only import assets.
-   Using **Action > Import** option in the **USD Stage Editor**. This process will import both assets and Actors. After the import process is complete, assets on the USD stage are replaced with new Actors from the **Content Browser**.

### Authoring and Editing Animation

Animations stored within a USD file are accessible using the associated Level Sequence found in the **Properties** panel of the **USDStageActor**.

Open the Level Sequence by selecting the USD Level Stage and double-clicking the Sequence in the Properties panel. Click image for full size.

USD xform animations are displayed as **Transform** tracks within the Level Sequence. Other forms of animation such as floats, boolean, and skeletal bones, are displayed via the **Time** track. The USD animation data in the image above is represented as a key / value pair at each timecode for the duration of the animation.

Through the **USD Stage** generated **Level Sequence**, you can bind to an Actor that is spawned on the USD Stage and add additional animation through a **Transform** track.

### USD Runtime Support

Unreal Engine supports the loading of USD files at runtime through calling the Set Root Layer Blueprint node on a USD Stage Actor inside the Level.

The Set Root Layer node. Click on image for full size.

This node creates the required Assets and spawns Actors and components into the Level identically to how the process is handled in the editor. Additional Blueprint functions for controlling various USD Stage Actor properties include:

| Blueprint Function | Description |
| --- | --- |
| **Get Generated Assets** | Gets the Assets generated for a prim within a given prim path and places them in an array. Uses a USD Stage Actor and Prim Path as inputs. |
| **Get Generated Components** | Gets the component generated for a prim within a given prim path. Uses a USD Stage Actor and Prim Path as inputs. |
| **Get Source Prim Path** | Gets the Prim Path for a given object on the USD Stage. Uses a USD Stage Actor and an Object reference as inputs. |
| **Get Time** | Gets the current timestamp within the target USD Stage Actor. Takes a USD Stage Actor as Target. |
| **Set Initial Load Set** | 
Sets the initial payload to load. Uses a USD Stage Actor as input and provides the following options.

-   **Load All**: Load all payloads initially.
-   **Load None**: Load no payloads initially.



 |
| **Set Purpose to Load** | 

Sets the initial Purpose to load. Uses a USD Stage Actor and an integer as input.

-   0 = Default
-   1 = Proxy
-   2 = Render
-   3 = Guide



 |
| **Set Render Context** | Sets the Render Context of a USD Stage. Takes a USD Stage Actor as Target and reference to a Render Context as input. |
| **Set Time** | Sets the current timestamp of a USD Stage. Takes a USD Stage Actor as Target and a float value as input. |

For more information on the Purpose attribute and other USD terms, see Pixar's [USD Glossary](https://graphics.pixar.com/usd/docs/USD-Glossary.html#USDGlossary-Purpose).

Using this process, you can create applications capable of loading and displaying the contents of a USD file at runtime.

To enable the USD importer at runtime, add the following line to your `Project.Target.cs` file located in the `UE_(version)\Engine\Source` folder, where Project is your project name:

```

`GlobalDefinitions.Add("FORCE_ANSI_ALLOCATOR=1");`

Copy full snippet
```
GlobalDefinitions.Add("FORCE\_ANSI\_ALLOCATOR=1");

For example:

```
	`public class YourProjectTarget : TargetRules 	{ 	public YourProjectTarget( TargetInfo Target) : base(Target) 	{ 	 Type = TargetType.Game; 	 DefaultBuildSettings = BuildSettingsVersion.V2; 	 ExtraModuleNames.AddRange( new string[] { "YourProject" } );  	 GlobalDefinitions.Add("FORCE_ANSI_ALLOCATOR=1"); 	} 	}`

Copy full snippet
```
public class YourProjectTarget : TargetRules { public YourProjectTarget( TargetInfo Target) : base(Target) { Type = TargetType.Game; DefaultBuildSettings = BuildSettingsVersion.V2; ExtraModuleNames.AddRange( new string\[\] { "YourProject" } ); GlobalDefinitions.Add("FORCE\_ANSI\_ALLOCATOR=1"); } }

### Nvidia MDL Support

Unreal Engine supports MDL surface materials using the Nvidia MDL USD schema. For more information on Nvidia MDL, see Nvidia's [USD Shader Attributes](https://developer.nvidia.com/usd/mdlschema).

### Multi-User Editing Support

Multi-user Editing is supported by many USD Stage operations, including the following:

-   Adding and removing prims.
-   Renaming prims.
-   Editing prim attributes.
-   Toggling visibility.
-   Opening, closing, or changing the current stage.

To enable multi-user support for your USD project, enable the **USD Multi-User synchronization** plugin. To find out more about how to work with Plugins, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine)

USD multi-user editing synchronizes the **Root Layer** property of the USD Stage for each client, ensuring that all users have the same USD files. This is done by having each client open the same USD stage locally, spawning assets and components on their own system, and then only synchronizing the operations done to those assets.

During a multi-user editing session, it is important for all users to access the USD files using the same file path. To make certain that each client can access the same files, we recommend that the target USD files are stored within the project folder and managed using source control.

For more information on Multi-User Editing in Unreal Engine, see [Multi-User Editing in Unreal Engine](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine).

It is not possible to undo prim deletion during a multi-user session.

## Enabling the USD Import Plugin

To begin working with a USD file in the Unreal Editor, you will need to enable the **USD Importer** plugin from the **Plugins** menu. To find out more about how to work with Plugins, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine)

After the editor restarts, you will see a new **USD Stage** option listed under the **Window > Virtual Production** menu in the Level Editor.

The **Place Actors** panel lists a new **Usd Stage Actor** that you can add to your Level.

![USD Place Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37dc85c4-9f32-4a08-a491-ec224a04b744/5-0-040-place-actors-usd.png "New USD Actors available in the Place Actors panel")

New USD Actors available in the Place Actors panel.

## Using USD in Unreal Engine

Working with USD content in Unreal Engine begins with the USD Stage Editor and the USD Stage Actor.

The USD Stage panel.

| **Number** | **Description** |
| --- | --- |
| **1** | Hierarchy |
| **2** | Properties |
| **3** | Layers |

## USD Stage Workflow

A USD Stage Actor acts as a container for the contents of a loaded USD file and provides an anchor for that data within your Level. The 3D scene objects that are loaded from the USD file and seen in the viewport are fully compatible with most other Unreal Engine features, and you can treat them exactly like other Actors. You can add additional prims that reference content found in other USD files, including animated Skeletal Meshes.

Saving changes made to your USD stage using the **File > Save** menu in the USD Stage Editor writes those changes back to your USD file.

For more information on working with the USD Stage, see [USD Stage Editor Quick Start](/documentation/en-us/unreal-engine/usd-stage-editor-quick-start-in-unreal-engine).

Unreal Engine does not automatically create lightmaps for assets loaded on the USD Stage when a USD file is opened. This can result in a completely black scene when static lighting is built.

## Python Scripting

Python scripting with USD provides a flexible way to perform a variety of actions such as batch operations and scene edits that may be difficult or time consuming to do using the user interface. Operations such as hiding or editing the attributes of a large number of prims can be automated quickly using a flexible Python script launched from the **Output Log** panel.

Prior to using Python, you must enable the **Python Editor Script** plugin. To find out more about plugins, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

You can then use the Output Log located at the bottom of the Level Editor to execute python scripts. You can also open the Output Log as its own panel from **Window > Output Log**.

Click image for full size.

For more information on using Python scripting with Unreal Engine, see [Scripting the Unreal Editor Using Python](/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python).

### Use Case for using a Python script

When the USD SDK version that ships with Unreal Engine was upgraded to 21.05, the update renamed several attributes within the USDLux Light schemas. To resolve the issue, Unreal Engine includes a Python script that renames USDLux prim attributes to the 21.05 naming convention.

```
	``from pxr import Usd, Sdf, UsdLux 	import argparse  	def rename_spec(layer, edit, prim_path, attribute, prefix_before, prefix_after): 		path_before = prim_path.AppendProperty(prefix_before + attribute) 		path_after = prim_path.AppendProperty(prefix_after + attribute)  		# We must check every time, because adding a namespace edit that can't be applied will just cancel the whole batch 		if layer.GetAttributeAtPath(path_before): 			print(f"Trying to rename '{path_before}' to '{path_after}'") 			edit.Add(path_before, path_after)  	def rename_specs(layer, edit, prim_path, reverse=False): 		prefix_before = 'inputs:' if reverse else '' 		prefix_after = '' if reverse else 'inputs:'  		# Light 		rename_spec(layer, edit, prim_path, 'intensity', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'exposure', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'diffuse', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'specular', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'normalize', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'color', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'enableColorTemperature', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'colorTemperature', prefix_before, prefix_after)  		# ShapingAPI 		rename_spec(layer, edit, prim_path, 'shaping:focus', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shaping:focusTint', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shaping:cone:angle', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shaping:cone:softness', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shaping:ies:file', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shaping:ies:angleScale', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shaping:ies:normalize', prefix_before, prefix_after)  		# ShadowAPI 		rename_spec(layer, edit, prim_path, 'shadow:enable', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shadow:color', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shadow:distance', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shadow:falloff', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'shadow:falloffGamma', prefix_before, prefix_after)  		# DistantLight 		rename_spec(layer, edit, prim_path, 'angle', prefix_before, prefix_after)  		# DiskLight, SphereLight, CylinderLight 		# Note: treatAsPoint should not have the 'inputs:' prefix so we ignore it 		rename_spec(layer, edit, prim_path, 'radius', prefix_before, prefix_after)  		# RectLight 		rename_spec(layer, edit, prim_path, 'width', prefix_before, prefix_after) 		rename_spec(layer, edit, prim_path, 'height', prefix_before, prefix_after)  		# CylinderLight 		rename_spec(layer, edit, prim_path, 'length', prefix_before, prefix_after)  		# RectLight, DomeLight 		rename_spec(layer, edit, prim_path, 'texture:file', prefix_before, prefix_after)  		# DomeLight 		rename_spec(layer, edit, prim_path, 'texture:format', prefix_before, prefix_after)  	def collect_light_prims(prim_path, prim, traverse_variants, light_prim_paths, visited_paths): 		if not prim: 			return  		if prim_path in visited_paths: 			return 		visited_paths.add(prim_path)  		# Traverse manually because we may flip between variants, which would invalidate the stage.Traverse() iterator 		for child in prim.GetChildren():  			# e.g. /Root/Prim/Child 			child_path = prim_path.AppendChild(child.GetName())  			if UsdLux.Light(child): 				light_prim_paths.add(child_path)  			traversed_grandchildren = False 			if traverse_variants: 				varsets = child.GetVariantSets() 				for varset_name in varsets.GetNames(): 					varset = varsets.GetVariantSet(varset_name) 					original_selection = varset.GetVariantSelection() if varset.HasAuthoredVariantSelection() else None  					# Switch selections only on the session layer 					with Usd.EditContext(prim.GetStage(), prim.GetStage().GetSessionLayer()): 						for variant_name in varset.GetVariantNames(): 							varset.SetVariantSelection(variant_name)  							# e.g. /Root/Prim/Child{VarName=Var} 							varchild_path = child_path.AppendVariantSelection(varset_name, variant_name)  							collect_light_prims(varchild_path, child, traverse_variants, light_prim_paths, visited_paths) 							traversed_grandchildren = True  							if original_selection: 								varset.SetVariantSelection(original_selection) 							else: 								varset.ClearVariantSelection()  			if not traversed_grandchildren: 				collect_light_prims(child_path, child, traverse_variants, light_prim_paths, visited_paths)  	def update_lights_on_stage(stage_root, traverse_variants=False, reverse=False): 	""" Traverses the stage with root layer `stage_root`, updating attributes of light prims to/from USD 21.05.  		The approach here involves traversing the composed stage and collecting paths to prims that are UsdLux lights 		(flipping through variants or not according to the input argument), and later on traverse all the stage's 		layers and renaming all specs of of light prim attributes to 21.05 (by adding the 'inputs:' prefix) or to 		the schema before 21.05 (by removing the 'inputs:' prefix).  		We traverse the composed stage first to make sure we're modifying exclusively UsdLux light prim attributes, 		avoiding modifications to a Sphere's "radius" attribute, for example. 		""" 		stage = Usd.Stage.Open(stage_root, Usd.Stage.LoadAll) 		layers_to_traverse = stage.GetUsedLayers(True)  		# Collect UsdLux prims on the composed stage 		light_prim_paths = set() 		visited_paths = set() 		collect_light_prims(Sdf.Path("/"), stage.GetPseudoRoot(), traverse_variants, light_prim_paths, visited_paths)  		print("Collected light prims:") 		for l in light_prim_paths: 			print(f"\t{l}")  		# Traverse all layers, and rename all relevant attributes of light prims 		visited_paths = set() 		for layer in layers_to_traverse: 			# Batch all rename operations for this layer in a single namespace edit 			edit = Sdf.BatchNamespaceEdit()  			def visit_path(path): 				attr_spec = layer.GetAttributeAtPath(path) 				if attr_spec: 					prim_path = attr_spec.owner.path  					# Only visit each prim once, as we'll handle all UsdLux properties in one go 					if prim_path in visited_paths: 						return 					visited_paths.add(prim_path)  					if prim_path in light_prim_paths: 						rename_specs(layer, edit, prim_path, reverse)  			layer.Traverse("/", visit_path)  			if len(edit.edits) == 0: 				print(f"Nothing to rename on layer '{layer.identifier}'") 			else: 				if layer.CanApply(edit): 					layer.Apply(edit) 					print(f"Applied change to layer '{layer.identifier}'") 				else: 					print(f"Failed to apply change to layer '{layer.identifier}'")  		# Save all layers 		for layer in layers_to_traverse: 			if not layer.anonymous: 				layer.Save()  	if __name__ == "__main__": 	parser = argparse.ArgumentParser(description='Update light prims to USD 21.05') 		parser.add_argument('root_layer_path', type=str, 						help='Full path to the root layer of the stage to update e.g. "C:/MyFolder/MyLevel.usda"') 		parser.add_argument('--v', '--traverse_variants', dest='traverse_variants', action='store_true', 						help='Whether to also flip through every variant in every variant set encountered when looking for light prims') 		parser.add_argument('--r', '--reverse', dest='reverse', action='store_true', 						help='Optional argument to do the reverse change instead: Rename 21.05 UsdLux light attributes so that they follow the schema from before 21.05') 		args = parser.parse_args()  		update_lights_on_stage(args.root_layer_path, args.traverse_variants, args.reverse)``

Copy full snippet
```
from pxr import Usd, Sdf, UsdLux import argparse def rename\_spec(layer, edit, prim\_path, attribute, prefix\_before, prefix\_after): path\_before = prim\_path.AppendProperty(prefix\_before + attribute) path\_after = prim\_path.AppendProperty(prefix\_after + attribute) # We must check every time, because adding a namespace edit that can't be applied will just cancel the whole batch if layer.GetAttributeAtPath(path\_before): print(f"Trying to rename '{path\_before}' to '{path\_after}'") edit.Add(path\_before, path\_after) def rename\_specs(layer, edit, prim\_path, reverse=False): prefix\_before = 'inputs:' if reverse else '' prefix\_after = '' if reverse else 'inputs:' # Light rename\_spec(layer, edit, prim\_path, 'intensity', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'exposure', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'diffuse', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'specular', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'normalize', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'color', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'enableColorTemperature', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'colorTemperature', prefix\_before, prefix\_after) # ShapingAPI rename\_spec(layer, edit, prim\_path, 'shaping:focus', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shaping:focusTint', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shaping:cone:angle', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shaping:cone:softness', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shaping:ies:file', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shaping:ies:angleScale', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shaping:ies:normalize', prefix\_before, prefix\_after) # ShadowAPI rename\_spec(layer, edit, prim\_path, 'shadow:enable', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shadow:color', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shadow:distance', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shadow:falloff', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'shadow:falloffGamma', prefix\_before, prefix\_after) # DistantLight rename\_spec(layer, edit, prim\_path, 'angle', prefix\_before, prefix\_after) # DiskLight, SphereLight, CylinderLight # Note: treatAsPoint should not have the 'inputs:' prefix so we ignore it rename\_spec(layer, edit, prim\_path, 'radius', prefix\_before, prefix\_after) # RectLight rename\_spec(layer, edit, prim\_path, 'width', prefix\_before, prefix\_after) rename\_spec(layer, edit, prim\_path, 'height', prefix\_before, prefix\_after) # CylinderLight rename\_spec(layer, edit, prim\_path, 'length', prefix\_before, prefix\_after) # RectLight, DomeLight rename\_spec(layer, edit, prim\_path, 'texture:file', prefix\_before, prefix\_after) # DomeLight rename\_spec(layer, edit, prim\_path, 'texture:format', prefix\_before, prefix\_after) def collect\_light\_prims(prim\_path, prim, traverse\_variants, light\_prim\_paths, visited\_paths): if not prim: return if prim\_path in visited\_paths: return visited\_paths.add(prim\_path) # Traverse manually because we may flip between variants, which would invalidate the stage.Traverse() iterator for child in prim.GetChildren(): # e.g. /Root/Prim/Child child\_path = prim\_path.AppendChild(child.GetName()) if UsdLux.Light(child): light\_prim\_paths.add(child\_path) traversed\_grandchildren = False if traverse\_variants: varsets = child.GetVariantSets() for varset\_name in varsets.GetNames(): varset = varsets.GetVariantSet(varset\_name) original\_selection = varset.GetVariantSelection() if varset.HasAuthoredVariantSelection() else None # Switch selections only on the session layer with Usd.EditContext(prim.GetStage(), prim.GetStage().GetSessionLayer()): for variant\_name in varset.GetVariantNames(): varset.SetVariantSelection(variant\_name) # e.g. /Root/Prim/Child{VarName=Var} varchild\_path = child\_path.AppendVariantSelection(varset\_name, variant\_name) collect\_light\_prims(varchild\_path, child, traverse\_variants, light\_prim\_paths, visited\_paths) traversed\_grandchildren = True if original\_selection: varset.SetVariantSelection(original\_selection) else: varset.ClearVariantSelection() if not traversed\_grandchildren: collect\_light\_prims(child\_path, child, traverse\_variants, light\_prim\_paths, visited\_paths) def update\_lights\_on\_stage(stage\_root, traverse\_variants=False, reverse=False): """ Traverses the stage with root layer \`stage\_root\`, updating attributes of light prims to/from USD 21.05. The approach here involves traversing the composed stage and collecting paths to prims that are UsdLux lights (flipping through variants or not according to the input argument), and later on traverse all the stage's layers and renaming all specs of of light prim attributes to 21.05 (by adding the 'inputs:' prefix) or to the schema before 21.05 (by removing the 'inputs:' prefix). We traverse the composed stage first to make sure we're modifying exclusively UsdLux light prim attributes, avoiding modifications to a Sphere's "radius" attribute, for example. """ stage = Usd.Stage.Open(stage\_root, Usd.Stage.LoadAll) layers\_to\_traverse = stage.GetUsedLayers(True) # Collect UsdLux prims on the composed stage light\_prim\_paths = set() visited\_paths = set() collect\_light\_prims(Sdf.Path("/"), stage.GetPseudoRoot(), traverse\_variants, light\_prim\_paths, visited\_paths) print("Collected light prims:") for l in light\_prim\_paths: print(f"\\t{l}") # Traverse all layers, and rename all relevant attributes of light prims visited\_paths = set() for layer in layers\_to\_traverse: # Batch all rename operations for this layer in a single namespace edit edit = Sdf.BatchNamespaceEdit() def visit\_path(path): attr\_spec = layer.GetAttributeAtPath(path) if attr\_spec: prim\_path = attr\_spec.owner.path # Only visit each prim once, as we'll handle all UsdLux properties in one go if prim\_path in visited\_paths: return visited\_paths.add(prim\_path) if prim\_path in light\_prim\_paths: rename\_specs(layer, edit, prim\_path, reverse) layer.Traverse("/", visit\_path) if len(edit.edits) == 0: print(f"Nothing to rename on layer '{layer.identifier}'") else: if layer.CanApply(edit): layer.Apply(edit) print(f"Applied change to layer '{layer.identifier}'") else: print(f"Failed to apply change to layer '{layer.identifier}'") # Save all layers for layer in layers\_to\_traverse: if not layer.anonymous: layer.Save() if \_\_name\_\_ == "\_\_main\_\_": parser = argparse.ArgumentParser(description='Update light prims to USD 21.05') parser.add\_argument('root\_layer\_path', type=str, help='Full path to the root layer of the stage to update e.g. "C:/MyFolder/MyLevel.usda"') parser.add\_argument('--v', '--traverse\_variants', dest='traverse\_variants', action='store\_true', help='Whether to also flip through every variant in every variant set encountered when looking for light prims') parser.add\_argument('--r', '--reverse', dest='reverse', action='store\_true', help='Optional argument to do the reverse change instead: Rename 21.05 UsdLux light attributes so that they follow the schema from before 21.05') args = parser.parse\_args() update\_lights\_on\_stage(args.root\_layer\_path, args.traverse\_variants, args.reverse)

The script can be found within the USDImporter source files located in `Engine/Plugins/Importers/USDImporter/Content/Python/usd_unreal/update_lights_to_21_05.py`.

Follow these steps to execute the script from the **Output Log**:

1.  Open the **Output Log** by selecting **Window > Output Log**.
    
2.  Click the **Cmd** dropdown to the left of the command line field and select Python.
    
3.  Enter the following in the command line field: `"C:\Program Files\Epic Games\UE_4.27\Engine\Plugins\Importers\USDImporter\Content\Python\usd_unreal\update_lights_to_21_05.py" "C:/path/to/root_layer.usda"`
    
    Where `"C:/path/to/root_layer.usda"` is the path to your USD file.
    
    The sample above contains the default path to the Unreal Engine install. Be sure to update the path if you did not install your version of Unreal Engine in the default location.
    
4.  Press **Enter** to execute the command.