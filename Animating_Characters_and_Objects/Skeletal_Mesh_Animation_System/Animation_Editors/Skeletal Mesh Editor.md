# Skeletal Mesh Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:41

---

The **Skeletal Mesh Editor Mode** is where you can find the tools to manipulate and preview **Skeletal Mesh** assets. It is similar to the [Static Mesh Editor](/documentation/en-us/unreal-engine/static-meshes). In the Skeletal Mesh Editor you can make changes to the polygonal mesh by assigning [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials), adding clothing elements, setting up [LODs](/documentation/en-us/unreal-engine/creating-and-using-lods-in-unreal-engine) (Level of Detail), and previewing any [Morph Targets](/documentation/en-us/unreal-engine/static-mesh-morph-targets-in-unreal-engine) applied to the mesh.

Here is the Skeletal Mesh Editor, with the following tools and panels:

![skeletal mesh editor overview window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/415d2412-396e-4d69-a330-4c7cda1322b8/skeletalmesheditoroverview.png)

1.  [Toolbar](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#toolbar)
    
2.  [Asset Details / Skeleton Tree](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#assetdetails/skeletontree)
    
3.  [Viewport](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#viewport)
    
4.  [Preview Scene Settings / Morph Target Previewer](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#previewscenesettings/morphtargetpreviewer)
    

## Toolbar

The Toolbar found in the Skeletal Mesh Editor is similar to the **Toolbar** found across Unreal's many editors and windows. For general Animation Editor functions refer to the [Animation Editors Overview's Toolbar Section](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#toolbar) for more information. The following are features unique to the Skeletal Mesh Editor Mode.

![skeletal mesh editor toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c24a9704-53a9-4144-ad92-9bd52a503f21/skeletalmesheditortoolbar.png)

### Reimport Base Mesh

With **Reimport Base Mesh**, you can begin the re-import process for the Base Mesh of the current Skeletal Mesh. This can be helpful if the mesh was not imported correctly and adjustments need to be made, or if you need a fresh start with the current mesh.

![reimport base mesh button icon toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01d69c8a-f1b8-43d1-9690-78a162fb1e1e/reimportbasemeshbutton.png)

| Option | Description |
| --- | --- |
| **Reimport Base Mesh** | Opens the current skeletal meshes original source FBX file, with a new import options window. |
| **Reimport Base Mesh With New File** | A file browser opens where a new source FBX file can be selected and imported. Unreal will work to assign any of the existing Materials, Bones, and other Assets to the new mesh, and will ask for permission in some instances where an exact match is not available. Any assets unable to be assigned will be marked as failed. |
| **Reimport Base Mesh + LODs** | Re-imports the Mesh's original source file, including the base LOD and any custom LODs associated with the source file. |
| **Reimport Base Mesh + LODs With New File** | Imports the base mesh, the base LOD, and any custom LODs from new source files. LODs can be imported directly with FBX files, but can also be found in separate source files. See the **Source Import Filename** property in the [Asset Details](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#asset%20details%20/%20skeleton%20tree) panel to see how your mesh's source files are organized. |
| **Reimport Content** | Only re-imports specific content elements of the Mesh for it's base LOD. Elements can be either Geometry or the Skinning and weights exclusively. |

By clicking any of these options associated with the original source file, Unreal will automatically open the mesh from its original known location. If the file cannot be located, or the option involves selecting a new source file, a browser window will open where one can be assigned.

### Cloth Paint

Unreal provides an efficient and lightweight clothing solver, with integrated editing and preview tools, accessible from the Skeletal Mesh Editor Toolbar.

![activate cloth paint icon button toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5d4a01f1-2751-464a-bc9b-b9cb3dc638f8/activateclothpainticon.png)

Clicking the button will open the Clothing panel that will dock next to the **Asset Details** and **Skeleton Tree** panels. Here you will have access to properties and settings that will assist in assigning your mesh's clothing materials and controlling their behaviors.

For more information and workflow examples regarding clothing in Unreal, refer to the [Clothing Tool](/documentation/en-us/unreal-engine/clothing-tool-in-unreal-engine) page.

### Make Static Mesh

The **Make Static Mesh** button will create a new Static Mesh Asset from the current Skeletal Mesh's pose.

![make static mesh icon button toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b90ee8d-d4e8-427e-bb83-18c347f021a7/makestaticmeshicon.png)

After manipulating the Skeletal Mesh to a desired pose and clicking Make Static Mesh**,** you are prompted to choose a location to save the new Static Mesh. This asset can now be placed in a level or edited similar to any other static mesh object.

## Asset Details / Skeleton Tree

By default this window contains two panels, the [Asset Details](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#asset%20details) panel and the [Skeleton Tree](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#skeleton%20tree) panel, that, while accessible in other editors, contains unique features for the Skeletal Mesh Editor.

### Asset Details

The Skeletal Mesh Asset Details panel is a context-sensitive property editor that you can use to edit and modify settings pertaining to the selected Skeletal Mesh and its elements such as its Materials, LODs, and the [Reduction Tool](/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine#reduction%20tool). Many of the properties found under this tab are general to all Meshes and will be described in detail on the [Static Mesh](/documentation/en-us/unreal-engine/static-meshes) page.

![asset details tab panel window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2bf0573f-d16d-4e61-9188-53c3e76a5fd7/assetdetailspanel.png)

Here you will find a description and function of all of the unique and relevant properties of the Asset Details panel.

| Property | Description |
| --- | --- |
| **Sections** | Many of the same properties for assigning and previewing Static Mesh Materials are present here. However, a unique property to Skeletal Mesh LOD generation is the **Generate Up To** property, where you choose up to which LOD the current material is generated. This can be helpful when you want to swap materials at different LODs. |
| LOD Info |   |
| **LOD Hysteresis** | This value is used to avoid 'flickering' when crossing a LOD threshold. Only taken into account when transitioning from a complex to a simple LOD. Higher values will increase the hysteresis, or lag, of the perceived model, which can smooth transitions between radically different LODs. |
| **Bones to Prioritize** | While the Skeletal Mesh Reduction tool is effective at reducing the triangle count of Skeletal Meshes, there can be instances where the reduction is too aggressive. To provide more control over what is optimized and what is not, the Bones to Prioritize array makes sure that any geometry skinned to the bones in the list will not be optimized. Listed here is an array of Bones which should be prioritized to retain quality. Use the **Weight of Prioritization** property to control the value at which these are prioritized. |
| **Sections to Prioritize** | Similar to the Bones to Prioritize property above, this property is an array of Sections, or Material Slots, which should be prioritized to retain quality. Use the **Weight of Prioritization** property to control the value at which these are prioritized. |
| **Weight of Prioritization** | Listed here is the value that determines how much consideration to give the Bones to Prioritize and Sections to Prioritize properties. The weight is an additional vertex simplification penalty where 0 means nothing. Higher values increase the weight of prioritization for listed Bones and Sections, while lower values reduce the weight of prioritization. |
| **Source Import Filename** | Listed is the source file directory, for the base mesh FBX file, and any separated associated custom LOD source files. |
| **Skin Cashe Usage** | 
This drop down menu will set the LODs behavior in using the skin cache feature. Options are as follows:

-   **Auto** defers to the default project global option established in the project settings.
-   **Disabled** means the Mesh will not use the skin cache.
-   **Enabled** means the mesh to use the Skin Cache.

If the **Support Ray Tracing** property is enabled on the mesh, it implies **Enabled** by default.



 |
| **Morph Target Position Error Tolerance** | The property value is displayed in microns. Larger values result in better compression and lower memory footprint, but also lower quality. |
| **Bake Bose** | Select a single frame of animation to bake into a pose. This is useful when automatic LOD generation is removing bones for lower detail LODs but you want to retain a finer detail that has been removed. For more information, refer to the [Pose Asset](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine) page. |
| **Bake Pose Override** | Overrides the Bake Pose property. The source Bake Pose can be disabled if some LOD settings are in use. For more information, refer to the [Pose Asset](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine) page. |
| **Bones to Remove** | An array of Bones to be removed from the skeleton for this LOD level. |
| Skeletal Mesh Reduction Tool |   |
| **Termination Criterion** | 

The Termination Criterion option in the Skeletal Mesh Reduction tool gives you the ability to change the way the simplifier reduces the Skeletal Mesh asset in LOD generation. For example, you can specify the number (or percentage) of vertices, instead of triangles, to provide more control to better fit memory or performance targets.

The available options for reduction technique are as follows:

-   **Triangles**: Relying on the **Percent of Triangles** property, the Reduction Tool targets a percentage of triangles of the base mesh to generate a LOD.
-   **Vertices**: Relying on the **Percent of Vertices** property, the Reduction Tool targets a percentage of vertices of the base mesh to generate a LOD.
-   **First Percent Simplified**: This option will generate a simplified LOD by factoring both Percent of Triangles and Percent of Vertices, completing the LOD with whichever factor is achieved first.
-   **Max Triangles**: This option will generate a LOD using an established maximum number of triangles, in the **Max Triangle Count** property.
-   **Max Vertices**: This option will generate a LOD using an established maximum number of vertices, in the **Max Vertex Count** property.
-   **First Max Satisfied**: This option will generate a simplified LOD by factoring both **Max Triangles** and **Max Vertices**, completing the LOD with whichever factor is achieved first.

Depending on which Termination Criterion is selected the following options will dynamically change to the relevant properties.



 |
| **Percent of Triangles** | This property is a target percentage value of triangles to generate a simplification of the source mesh for a new LOD. |
| **Percent of Vertices** | This property is a target percentage value of vertices to generate a simplification of the source mesh for a new LOD. |
| **Max Triangles Count** | The maximum number of triangles to retain when using the percentage criterion. A maximum value to limit the automatic generation. |
| **Max Vertices Count** | The maximum number of vertices to retain when using the percentage criterion. A maximum value to limit the automatic generation. |
| **Max Triangles Count** | The maximum triangles to retain when using the Max Triangle criterion. |
| **Max Vertex Count** | The maximum vertices to retain when using the Max Vertices criterion. |
| **Remap Morph Targets** | Remaps the existing morph targets from the base LOD to the reduced LOD selected. |
| **Max Bone Influence** | The maximum number of bones that are assigned to each vertex. |
| **Enforce Bone Boundaries** | If enabled, Unreal will penalize edge collapses between vertices that have different major bones attached. This helps articulated segments like tongues, but can lead to undesirable results under extreme simplification. |
| **Merge Coincident Vertices Bones** | If enabled, the same location, for example UV boundaries, always has the same bone weights. This can fix bone merge errors when the characters are animated. |
| **Volumetric Correction** | A slider to determine the Volumetric Correction implemented at this LOD level. The default value of 1 attempts to preserve volume. Smaller values will lose volume by flattening curved surfaces, and larger values will accentuate curved surfaces. |
| **Lock Mesh Edges** | If enabled, cuts in the mesh's surface are preserved by locking vertices in one place. This increases the quality of the simplified mesh at edges, at the cost of more triangles. |
| **Lock Vertex Color Boundaries** | If enabled, edges that connect two vertex colors are locked. This increases the quality of the simplified mesh at edges at the cost of more triangles. |
| **Regenerate** | If pressed, Unreal will regenerate the current LOD with the applied Reduction Tool properties above. |
| LOD Settings |   |
| **LODSettings** | Choose the data asset with which to save the current LOD info. This data can be saved to an existing data asset or, if none is selected, a new one can be generated by clicking **Generate Asset**. |
| **Disable Below Min LOD Stripping** | If enabled, below minimum LOD stripping is disabled. With the plus(+) button, you can add an override for a specific platform or group. |
| **Override LodStreaming Settings** | If enabled, overrides the LOD streaming settings. With the plus(+) button, you can add an override for a specific platform or group. |
| **Stream LODs** | If enabled, supports LOD streaming. With the plus button, you can add an override for a specific platform or group. |
| **Max Num Streamed LODs** | The maximum number of Streamed LODs allowed. With the plus(+) button, you can add an override for a specific platform or group. |
| **Max Num Optional LODs** | The maximum number of Optional LODs allowed. With the plus(+) button, you can add an override for a specific platform or group. |
| Clothing |   |
| **Mesh Clothing Assets** | An array listing the Mesh Clothing Assets associated with the current mesh. |
| Mesh |   |
| **Skeleton (Mesh)** | The current Skeletal Mesh's Skeleton asset. Double clicking the Skeleton will open the skeleton in the Skeleton Editor. |
| Animation Rig |   |
| **Default Animation Rig** | The Control Rig Asset associated with the current Skeletal Mesh. |
| Physics |   |
| **Enable Per Poly Collision** | If enabled, Per Poly Collision is allowed, or the inhibition of the mesh's individual polygons to overlap. |
| **Physics Asset** | The Physics asset associated with the Skeletal Mesh. Double clicking the Physics asset will open the Physics Editor. |
| Lighting |   |
| **Shadow Physics Asset** | The Shadow Physics asset associated with the Skeletal Mesh. |
| Skeletal Mesh |   |
| **Post Process Anim Blueprint** | Assign or access a [Post Process Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine#assigning%20post%20process%20animation%20blueprints) which runs after any Animation Blueprint assigned to the Main Anim Instance for a Skeletal Mesh Component. By assigning a Post Process Anim Blueprint to a Skeletal Mesh, you can create AnimDynamics, Skeletal Controls, or other Anim Blueprint logic without having to copy that logic to other Animation Blueprints. |
| **Advanced User Data** | An array of stored user data, used for implementing uniform functions or accessing stored information. |
| Animation |   |
| **Node Mapping Data** | An array of stored node mapping data, used for implementing uniform functions or accessing stored information. |
| Import Settings |   |
| **Import Content Type (Import/Mesh)** | 

Select what content from the source file you wish to import. Options are as follows:

-   **Geometry and Skinning Weight** imports all source file content.
-   **Geometry Only** imports the respective content exclusively.
-   **Skinning and Weights Only** import the respective content exclusively.



 |
| **Update Skeleton Reference Pose** | If enabled, the mesh's skeleton's reference pose will be updated when importing. |
| **Use T0 As Ref Pose** | If enabled, frame 0 will be used as the reference pose when importing. |
| **Preserve Smoothing Groups** | If enabled, triangles with non-matching smoothing groups will be physically split when importing. |
| **Import Meshes In Bone Hierarchy** | If enabled, meshes in bone hierarchies will be imported instead of being converted to bones. |
| **Import Morph Targets** | If enabled, creates Unreal morph objects for the imported meshes. |
| **Threshold Position** | Edit the threshold to compare vertex position equality. |
| **Threshold Tangent Normal** | Edit the threshold to compare normal, tangent of bi-normal equality. |
| **Threshold UV** | Edit the threshold to compare UV equality. |
| **Morph Threshold Position** | The threshold to compare vertex position equality when computing morph target deltas. |
| **Normal Input Method** | 

Select the normal input method for normals and tangents associated with the mesh. Options in the dropdown are as follows:

-   **Compute Normals** in Unreal.
-   **Import Normals** from the source file.
-   **Import Normals and Tangents** from the source file.



 |
| File Path |   |
| **Source File (Geometry and Skinning Weights)** | The file directory of the source file. |
| Skin Weights |   |
| **Skin Weight Profiles** | An array of stored skin weight profiles, used for implementing uniform functions or accessing stored information. |
| Ray Tracing |   |
| **Ray Tracing Min LOD** | Decide which LOD of the current mesh is the minimum LOD for which Ray Traced reflections are enabled. |
| **Cloth LOD Bias Mode** | 

Decide the LOD bias towards Cloth simulation. Options are as follows:

-   **Mapping to Same LOD** only stores the strict minimum amount of cloth deformer mappings to save on memory usage. Ray Tracing of cloth elements must never be of a different LOD to the one rendered when using this mode.
-   **Mapping to a Min LOD** stores additional cloth data deformer mappings to allow Ray Tracing of the cloth elements at the Ray Tracing minimum LOD. When using this mode, Ray Tracing of cloth elements must never be of a different LOD to the one rendered, or to the one set for the Ray Tracing minimum LOD.
-   **Mappings to Any LOD** stores all cloth deformer mappings at the expense of memory usage to allow the Ray Tracing of the cloth elements at any higher LOD. Use this mode when the Ray Tracing LOD Bias console variable is in use.



 |
| Sampling |   |
| **Regions** | An array of stored regions sampling data, used for implementing uniform functions or accessing stored information. |

### Skeletal Tree

The Skeleton Tree tab displays the **Skeletal Hierarchy** of the current Skeleton Asset that you can use to create and edit [Sockets](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine) and define settings related to [Animation Retargeting](/documentation/en-us/unreal-engine/animation-retargeting-in-unreal-engine).

![skeleton tree panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4efd045d-aacd-4d5f-88c2-cb394ff2075f/skeletontreepanel.png)

Although the skeleton tree is most relevant to the Skeleton Editor Mode, the [Skeletal Mesh Sockets](/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine) feature is also important when working with the Skeletal Mesh Editor.

## Viewport

With the [Viewport](/documentation/en-us/unreal-engine/editor-viewports-in-unreal-engine) window you can preview your selected Skeletal Mesh and see provided information about your assets.

![skeletal mesh editor viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed6740bb-ea11-45ee-b581-acb0b3fedd9f/skeletoneditorviewport.png)

For more information about the unique animation centric features of the viewport, refer to the [Animation Editors Overview Page](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine).

## Preview Scene Settings / Morph Target Previewer

This panel has two tabs, **Preview Scene Settings** and **Morph Target Previewer**.

### Preview Scene Settings

[Preview Scene Settings](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine#preview%20scene%20settings) enable control of the preview settings such as the selected animation and applied Skeletal Meshes, as well as Viewport lighting and Post Process settings.

![skeletal mesh preview scene settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef4384ec-f791-49e2-b620-5464a719cbd8/previewscenesettings.png)

### Morph Target Previewer

With the **Morph Target Previewer** you can preview edits and modifications made to the Morph Targets associated with your Skeletal Mesh.

![morph target previewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1627393-b99f-49b6-a254-f0548bd44048/morphtargetpanel.png)