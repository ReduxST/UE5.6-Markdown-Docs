# Datasmith Import Options

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-import-options-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/datasmith-import-options-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:52

---

This page describes the options that you can configure when you use Datasmith to import a file from a supported design application or data file format, or to re-import a Datasmith Scene Asset from its original source.

All file formats offer you the **Common Import Options** described in the first section. Then, depending on the type of file you're importing, you may have additional options specific to that format. See the following sections for details.

## Common Datasmith Import Options

When you use Datasmith to import any kind of file, you can set the following options.

![Common Datasmith import options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/375bf2af-d999-400f-a3db-9c5e52a87b07/import-options-common-424.png "Common Datasmith import options")

| Property | Description |
| --- | --- |
| **Geometry** | Specifies whether or not Datasmith should import geometry from your source file and turn it into Static Mesh assets in your Project. |
| **Materials & Textures** | Specifies whether or not Datasmith should import materials and textures from your source file and turn them into Material and Texture assets in your Project. |
| **Lights** | Specifies whether or not Datasmith should include lights from your source file in the scene hierarchy maintained by the Datasmith Scene, and create Light Actors in your Level to represent them. |
| **Cameras** | Specifies whether or not Datasmith should include cameras from your source file in the scene hierarchy maintained by the Datasmith Scene, and create Cine Camera Actors in your Level to represent them. |
| **Animations** | Specifies whether or not Datasmith should import object animations from your source scene into Level Sequences that you can use to play back the animations inside the Unreal Engine. |
| Static Mesh Options |   |
| **Min Lightmap Resolution** | Sets the minimum lightmap resolution for the Static Mesh Assets that Datasmith generates. This value is used to determine the amount of padding between packed UV charts when generating lightmap UVs in Unreal Engine 4. A good value is typically half of the Max Lightmap Resolution. |
| **Max Lightmap Resolution** | 
Sets the lightmap resolution for the Static Mesh Assets that Datasmith generates. These lightmaps are used to store lighting information per instance when you use precomputed lighting (Static and Stationary lights) in your Level.

Don't set this value too high on import. Set it to a good baseline level for your Project, then increase it for individual Static Mesh assets that need higher resolution to achieve good results when you build your lighting.



 |
| **Generate Lightmap UVs** | 

Determines whether or not Datasmith should generate lightmap UVs for each Static Mesh Asset it imports. This option is enabled by default, and is typically recommended to ensure that you'll be able to use baked lighting for all geometry that you import through Datasmith.

However, generating lightmaps automatically at import time has downsides. It takes time during the import process. It creates additional UV channels on your Static Meshes, which makes their memory size slightly larger. Finally, you have no direct control over the resulting lightmap.

You may be able to save time and memory by disabling lightmap generation if any of the following are true:

-   You have already created UV mappings suitable for lightmap baking in your source application.
-   You intend to use only dynamic lighting or ray tracing for lighting your scene in Unreal.
-   You intend to generate your own lightmap UVs after import, using tools built in to the Unreal Editor.

See also [Working with UV Channels](/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine) and [Understanding Lightmapping in Unreal Engine](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine).



 |

When you reimport a Datasmith scene, the checkboxes under the **Include** section indicate only whether each type of Asset or Actor should be updated with new and modified content from your source file. If you uncheck one of these items, existing Assets or Actors of that type are not deleted from your Project.

## CAD Import Options

When you use the **Datasmith** importer to import a CAD file (that is, any file that is listed on the [Datasmith Supported Software and File Types](/documentation/en-us/unreal-engine/datasmith-supported-software-and-file-types) page as being provided by the **CAD** importer), you can set the following additional options.

If your source file contains any surfaces that are defined by curves, Datasmith tessellates those surfaces into triangular meshes. These parameters control the tessellation process. They control how closely the generated meshes follow the original surfaces, and therefore also the complexity of the meshes. For all settings, smaller values increase the number of triangles, and higher values decrease the number of triangles.

![Geometry and Tessellation Options for CAD](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cc35f2b-f9d6-4c4c-a327-947389d83d7f/import-options-cad-425.png "Geometry and Tessellation Options for CAD")

| Property | Description |
| --- | --- |
| Geometry & Tessellation Options |   |
| **Geometry** | This option only appears when you import a Rhino file. It determines whether Datasmith should tessellate surfaces into triangular meshes using the parameters in this section, or whether it should reuse triangular meshes generated by Rhino and saved in your Rhino file. For details, see [Rhino](/documentation/en-us/unreal-engine/using-datasmith-with-rhino-in-unreal-engine). |
| **Chord Tolerance** | Sets the maximum distance between any point in a generated triangle and the original surface. |
| **Max Edge Length** | Sets the maximum length of any edge in any generated triangle. |
| **Normal Tolerance** | Sets the maximum angle between any adjacent triangles generated from a surface. |
| **Stitching Technique** | Determines whether the import process should try to merge together surfaces that appear to be connected, but that are actually modeled as separate objects. |

For an in-depth description of these tessellation parameters and how they affect the resulting Static Mesh geometry, see [Using Datasmith with CAD File Formats](/documentation/en-us/unreal-engine/importing-cad-files-into-unreal-engine-using-datasmith).

## GLTF Import Options

When you use the Datasmith GLTF importer to import a `.glTF` file ([GL Transmission Format](https://www.khronos.org/gltf/)), you can set the following additional options:

![glTF import options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d571cf2b-36da-4633-9247-9cb345bb6b84/import-options-gltf-422.png "glTF import options")

| Property | Description |
| --- | --- |
| Lightmaps |   |
| **Generate Lightmap UVs** | 
In order to use Static or Stationary lighting in the Unreal Engine, your models need to have lightmap UVs in which no two triangles overlap.

-   Enable this option to have the Datasmith importer automatically generate these lightmap UVs for the Static Mesh Assets it creates. In order for this to work, your models need to have at least one non-empty UV set to start with. If a model does not have any UV sets at all, the importer will create a blank UV set for the Static Mesh Asset, but this blank UV set will not be usable for applying textures or lightmaps to the Static Mesh.
    
-   If you've already created valid, non-overlapping lightmaps for the objects in your source application, you can leave this option unchecked to have the Datasmith importer skip creating new lightmap UVs. In this case, your Static Mesh Assets will use the UV set with the highest index as its lightmap UVs.
    

For more background information, see [Working with UV Channels](/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine).



 |
| Asset Importing |   |
| **Import Uniform Scale** | 

Determines the scaling factor the importer uses to convert linear distances. The default value of 100 converts from meters (as specified in the glTF specification) to centimeters (as used in the Unreal Engine). If your source scene uses a different unit of measurement than meters, adjust this value to the number of centimeters per unit.



 |

## VRED Import Options

When you use the Datasmith **VRED** importer to import an `.fbx` file that you exported from VRED, you can set the following additional options:

![VRED import options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/495b47ee-b29d-4907-881e-5bbdf11bfa80/datasmith-import-settings-vred.png "VRED import options")

| Property | Description |
| --- | --- |
| Processing |   |
| **Merge Nodes** | 
Combines subtrees of StaticMesh nodes that are not used for animations, variants or other functionality into single StaticMesh nodes. This can make scene management in Unreal easier by reducing the depth and complexity of the scene hierarchy. However, this option is not recommended if you need to clean up your imported Static Meshes manually, or if your scene contains many instances of the same geometry.



 |
| **Optimize Duplicated Nodes** | Reduces the total count of nodes in the scene hierarchy by reusing entire identical subtrees. |
| Asset Importing |   |
| **Import FBX animations** | Enable this option to import animations from the VRED scene into Unreal, and make them available to Blueprint scripts in your Project. |
| **Import variants file** | Enable this option to import variants and variant sets from your VRED scene into Unreal, and make them available to Blueprint scripts in your Project. |
| **Variants file path** | Specifies the path to the `.var` file that contains data about the variants in your VRED scene. By default, this is set to the path and filename that matches the `.fbx` file you are importing. You only need to set this path manually if you need to import a `.var` file from a different location. |
| **Import lights file** | 

If you disable this option, but leave the **Import > Lights** setting enabled in the common Datasmith properties, the lights that Datasmith creates in Unreal will contain only information stored in the `.fbx` file. If you enable this option, Datasmith imports extra information about the lights in your VRED scene from a `.lights` file that was created when you exported your scene. This carries over extra properties about your lights that are not supported by FBX, such as IES light profiles, and typically leads to better visual results that more closely match your lighting in VRED.



 |
| **Light file path** | Specifies the path to the `.lights` file that contains data about the variants in your VRED scene. By default, this is set to the path and filename that matches the `.fbx` file you are importing. You only need to set this path manually if you need to import a *.lights* file from a different location. |
| **Textures folder** | Specifies a folder path for Datasmith to search for texture files that are referenced in the `.fbx` file. |
| Debug |   |
| **Intermediate Serialization** | Enable this option to store scene data read from the `.fbx` file to an intermediate format. This setting might be useful if you need to import the same scene frequently, and the FBX importer is a bottleneck. |
| **Colorize materials** | Enable this option to use randomly colored simple materials instead of importing material parameters like DiffuseColor or textures. |
| Lightmaps |   |
| **Generate Lightmap UVs** | 

In order to use Static or Stationary lighting in the Unreal Engine, your models need to have lightmap UVs in which no two triangles overlap. 

-   Enable this option to have the Datasmith importer automatically generate these lightmap UVs for the Static Mesh Assets it creates. In order for this to work, your models need to have at least one non-empty UV set to start with. If a model does not have any UV sets at all, the importer will create a blank UV set for the Static Mesh Asset, but this blank UV set will not be usable for applying textures or lightmaps to the Static Mesh.
    
-   If you've already created valid, non-overlapping lightmaps for the objects in your source application, you can leave this option unchecked to have the Datasmith importer skip creating new lightmap UVs. In this case, your Static Mesh Assets will use the UV set with the highest index as its lightmap UVs.
    

For more background information, see [Working with UV Channels](/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine).



 |

## Deltagen Import Options

When you use the Datasmith **Deltagen** importer to import an `.fbx` file that you exported from Deltagen, you can set the following additional options:

![Deltagen import options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38b713d8-1d74-4937-9542-b587eac58159/datasmith-import-settings-deltagen.png "Deltagen import options")

| Property | Description |
| --- | --- |
| Processing |   |
| **Merge Nodes** | 
Combines subtrees of StaticMesh nodes that are not used for animations, variants or other functionality into single StaticMesh nodes. This can make scene management in Unreal easier by reducing the depth and complexity of the scene hierarchy. However, this option is not recommended if you need to clean up your imported Static Meshes manually, or if your scene contains many instances of the same geometry.



 |
| **Optimize Duplicated Nodes** | Reduces the total count of nodes in the scene hierarchy by reusing entire identical subtrees. |
| **Remove Invisble Nodes** | Enable this setting to avoid importing any geometry that were hidden in the Deltagen scene. |
| **Simplify Node Hierarchy** | Enable this setting to flatten the Datasmith Scene hierarchy. |
| Asset Importing |   |
| **Import VAR** | Enable this option to import variants from your Deltagen scene into Unreal, and make them available to Blueprint scripts in your Project. |
| **Import POS** | Enable this option to import state data from your Deltagen scene into Unreal. |
| **Import TML** | Enable this option to import animation data from your Deltagen scene into Unreal, and make them available to Blueprint scripts in your Project. |
| **Textures Dir** | Specifies a folder path for Datasmith to search for texture files that are referenced in the `.fbx` file. |
| Debug |   |
| **Intermediate Serialization** | Enable this option to store scene data read from the `.fbx` file to an intermediate format. This setting might be useful if you need to import the same scene frequently, and the FBX importer is a bottleneck. |
| **Colorize materials** | Enable this option to use randomly colored simple materials instead of importing material parameters like DiffuseColor or textures. |
| Lightmaps |   |
| **Generate Lightmap UVs** | 

In order to use Static or Stationary lighting in the Unreal Engine, your models need to have lightmap UVs in which no two triangles overlap. 

-   Enable this option to have the Datasmith importer automatically generate these lightmap UVs for the Static Mesh Assets it creates. In order for this to work, your models need to have at least one non-empty UV set to start with. If a model does not have any UV sets at all, the importer will create a blank UV set for the Static Mesh Asset, but this blank UV set will not be usable for applying textures or lightmaps to the Static Mesh.
    
-   If you've already created valid, non-overlapping lightmaps for the objects in your source application, you can leave this option unchecked to have the Datasmith importer skip creating new lightmap UVs. In this case, your Static Mesh Assets will use the UV set with the highest index as its lightmap UVs.
    

For more background information, see [Working with UV Channels](/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine).



 |