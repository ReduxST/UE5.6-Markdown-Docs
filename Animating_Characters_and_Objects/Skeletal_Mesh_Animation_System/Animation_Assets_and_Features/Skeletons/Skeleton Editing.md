# Skeleton Editing

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:50

---

You can use Unreal Engine's Skeleton Editing tools to edit and modify existing skeletons, to perform actions such as renaming bones, editing the placement of bones, or changing the hierarchy of bones.

You can also create new Skeleton assets for any Static Mesh without the need to import an FBX file using tools such as Bone Creation and Skin Weight Painting. In conjunction with tools such as Control Rig and Sequencer, you can use Unreal Engine to Skin and Animate Characters entirely within the editor.

#### Prerequisites

-   Enable the **Skeletal Mesh Editing Tools** [Plugin](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine). Navigate in the **Menu Bar** to **Edit > Plugins** and locate **Skeletal Mesh Editing Tools** in the **Animation** section, or use the **Search Bar**. Enable the Plugin and restart the editor.
    

-   Your Project contains a Static Mesh object that you can create a Skeleton for or a Skeletal Mesh character you wish to edit the Skeleton asset.
    

## Create a Skeletal Mesh

**Right-click** any Static Mesh object in the **Content Browser** and select the **Convert to Skeletal Mesh** option in the context menu.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/c11ca7c6-032e-42c6-95bd-2e18078c7c9b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c11ca7c6-032e-42c6-95bd-2e18078c7c9b?resizing_type=fit)

After selecting the Convert to Skeletal Mesh option, a menu will appear allowing you to select an existing Skeleton asset that will be bound to the Static Mesh, or you can select **Create New**, to create a new Skeleton asset.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/fe66306b-4efe-4c6d-af3f-762e5afde932?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fe66306b-4efe-4c6d-af3f-762e5afde932?resizing_type=fit)

When creating a new Skeleton asset, a single `root` bone will be created at the origin point of the Static Mesh.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/39b6b10f-fe0a-4e5f-8f4b-efbf707787a4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/39b6b10f-fe0a-4e5f-8f4b-efbf707787a4?resizing_type=fit)

## Editing a Skeleton Asset

After creating a new Skeleton asset, or selecting an existing asset you wish to edit, open the Skeleton in the Skeleton Editor. After opening the Editor, select the Editing Tools button in the Toolbar to begin editing the skeleton.

Here you can reference an overview of the tools and panels of the Skeleton Editor.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/30087292-5f19-4fce-8f06-949bee735a4e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/30087292-5f19-4fce-8f06-949bee735a4e?resizing_type=fit)

1.  **Tools Panel**
    
2.  **Skeleton Tree**
    
3.  **Details/Asset Details/Preview**
    

### Create and Edit Bones

To start creating bones, select the Skeleton mode in the Tools Panel.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/47549ab4-9bf7-4d58-bcd5-ad2490db24ee?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/47549ab4-9bf7-4d58-bcd5-ad2490db24ee?resizing_type=fit)

Using the **Edit Skeleton** tool will let you place bones within the mesh in the viewport.

Activate the **Add** mode (**N**), then select a bone in the viewport and drag the new bone to the correct length and position on the character. The first selected bone will act as the parent to the new bone.

After creating any new bones, select **Accept** to confirm the new bone and its placement.

Use the **Axis Length** and the **Axis Thickness** to visualize what direction the new bones are pointing.

When enabled, **Update Children** property will move any bones parented to the selected bone when edited. This is useful for adjusting entire chains.

### Parenting Bones

Bones can be reparented in the Skeleton hierarchy, by selecting bones in the Skeleton Tree panel and dragging and dropping the bone to a new parent.

### Renaming Bones

Bones can be **Renamed** (**F2**) by right-clicking on the bone and selecting the **Rename Bone** option from the context menu.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/642ea0b2-67b1-49db-81bc-9208d52d5467?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/642ea0b2-67b1-49db-81bc-9208d52d5467?resizing_type=fit)

You can also bulk rename bones by multi-selecting a chain. Additionally you can use a hashtag (**#**) operator at the end of the name to rename many bones using a successive numeral. For example you can multi-select a chain and rename the first bone to `tail_##1`, and after entering the change, the first bone would become `tail_001` with its successive bones becoming `tail_002`, `tail_003`.

### Edit Mode

You can edit existing bones in the Skeleton by selecting the **Edit Mode**, using tools such as the [Orient Bones](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine#orient-bones) and [Mirror Bones](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine#mirror-bones) tools.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/38ca4791-28b7-453f-9703-668dda7fb533?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/38ca4791-28b7-453f-9703-668dda7fb533?resizing_type=fit)

### Orient Bones

Bones need to point the correct direction so they rotate in a desirable manner. This is called **Bone Orientation**. To Orient your bones select the chain you want to orient and expand the Orient section.

Here you can reference a list of the Bone Orientation properties and a description of their function:

| Property | Description |
| --- | --- |
| 
**Primary**

 | 

Set the direction the bones will face, which is typically the **X**\-axis.

 |
| 

**Secondary**

 | 

Set the axis that will represent the up direction of the bones

 |
| 

**Use Plane as Secondary**

 | 

When enabled, this property will build a plane through the bones to help you orient.

 |
| 

**Secondary Target**

 | 

Set the position to use for the secondary axis

 |
| 

**Orient Children**

 | 

When enabled, this property will orient all children below the selected bone.

 |

You can also manually Orient bones by selecting the bone and using the Rotate Gizmo (**R**), or explicitly specifying a transform value on each axis (**X**, **Y**, and **Z**).

### Mirror Bones

In order to expedite the Skeleton creation process, you can use the Mirror Bones tool to mirror a bone chain, in order to copy limbs or other mirrored bone structures. To mirror a bone chain, select the chain or bones you would like to Mirror and use the **Mirror** button in the **Edit** mode.

Here you can reference a list of the Mirror Bones properties and a description of their function:

| Property | Description |
| --- | --- |
| 
**Mirrox Axis**

 | 

Set the axis plane to mirror across.

 |
| 

**Mirror Rotation**

 | 

When enabled, the rotation across the plane will be inverted. This is typically necessary for animation.

 |
| 

**Left String**

 | 

Define the naming that will be used to search on the left side

 |
| 

**Right String**

 | 

Define the naming that will be used to search on the right side

 |
| 

**Mirror Children**

 | 

When enabled, mirrored bones will also mirror all of their children within the selected bone chain.

 |

## Skin Weights

When adding new bones to your Skeletal Mesh, the **Bind Skin** tool will help you add **Skin Weights** for those bones in order for the bones to have an influence on the geometry of the mesh. Skin Weights are values assigned to each vertex of the skeletal mesh's geometry that represent the influence a bone has to deform the vertex when the bone moves. Each vertex can be influenced by multiple bones in the skeleton. As a user, you need to assign a weight to each vertex for each bone to tell it which bones it should be attached to. Each vertex contains a value from `0.0` to 1.0 for every bone, where a value of `0` means that vertex is completely unaffected by the bone and a value of `1` means that vertex is fully attached to the bone. Values between `0` and `1` allow a vertex to be partially affected by a bone. It's not practical to set the Skin Weight for each vertex individually, so instead, painting skin weight maps provides a better solution to create elegant deformations on an entire character.

Skin Wight values for each vertex are normalized meaning the total weight on each vertex must equal `1`. This ensures that when the skeleton, as a whole, is translated, the vertices in the mesh move with it. If the total weight on a vertex were less than 1, the vertex movement would appear delayed from the skeleton's movement. Conversely, if the total value were greater than 1, the vertex would move more than the skeleton. For this reason, a total value of 1 is enforced by Unreal Engine by normalizing the Skin Weight values for each vertex of the mesh.

For example, if a vertex on the elbow has a value of `0.7` on the forearm bone, then the remaining `0.3` weight will be assigned to one or more other bones. In this case, it likely belongs to the upper arm.

When you edit a vertex weight, Unreal will automatically normalize the other weights to ensure that the total value is always equal to 1, which may result in Unreal Engine automatically adjusting values of Skin Weights.

In the case that the vertex only has 1 influence, only 1 bone with a weight greater than zero, you cannot meaningfully modify the weight on that bone. Setting the weight to anything other than `1.0` will trigger the normalization procedure which will set the value back to `1.0`, regardless of the value you assign. Once a vertex has a non-zero weight assigned to multiple bones, the normalization procedure will dump extra weight onto the other influences as needed to achieve the weight set by the user.

Consider the previous example with a vertex with a weight of 0.7 on the forearm and 0.3 on the upper arm. If the user attempts to *remove* weight on the forearm, perhaps by setting it to a lower value of 0.6, then the normalization procedure will automatically change the upper arm value from 0.3 to 0.4, so as to maintain a total value of 1.

It is best to only explicitly add vertex weights, allowing the normalization procedure to remove weight as needed to achieve the desired value.

If you want a bone to have less influence, it is better to add additional weight to a different bone. This allows you to be explicit about where the influence belongs, rather than relying on normalization to split it evenly among the other influences.

### Binding Skin Weights

To begin painting skin weights, select the Skin mode in the Tools panel, and then select the Bind Skin tool to set your assets baseline settings.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/b9ca36ed-f81e-448e-bee2-594d712a2c3b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b9ca36ed-f81e-448e-bee2-594d712a2c3b?resizing_type=fit)

Here you can reference a list of the Bind Skin tool's properties and a description of their functionality:

| Property | Description |
| --- | --- |
| 
**Binding Type**

 | 

Select the method to use for binding. You can select from the following methods.

-   **Direct Distance**: Uses straight-line distance between bones and vertices to bind vertices to their nearest bones.
    
-   **Geodesic Voxel**: Uses the distance within a voxelized signed distance field to bind vertices to bones.
    

 |
| 

**Stiffness**

 | 

Set the stiffness of the binding. Lower values allow more distant bones to contribute to the bind.

 |
| 

**Max Influences**

 | 

Set the maximum number of bones that will influence each vertex.

 |
| 

**Voxel ResolutionVoxel Resolution**

 | 

When the **Binding Type** is set to **Geodesic Voxel**, you can use this property to set the resolution of the voxelized grid. High values can impact performance, but may help resolve finer details.

 |

### Paint Weights

Once you have a set of base weights you can now paint skin weight maps to set the area of the mesh each bone has influence over. To begin painting skin weight maps, select the **Edit Weights** button within the **Skin** mode.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/411cfc58-15f1-41b7-81a2-89a8630b763c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/411cfc58-15f1-41b7-81a2-89a8630b763c?resizing_type=fit)

You can then select which tool you want to use in order to paint skin weight maps on your mesh. There are two Weight Editing Modes:

-   [Brush](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine#brush-mode): Uses a paint brush tool to paint weights on the entire mesh. This mode is primarily used for painting weights on large areas, or simple structures.
    
-   [Vertices](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine#vertices-mode): Uses a selection tool that you can use to select individual vertices to edit skin weights. This mode is primarily used for detailed weight editing and masking.
    

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/89c1aeba-4d68-4497-baed-4a1e30d1f6fb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/89c1aeba-4d68-4497-baed-4a1e30d1f6fb?resizing_type=fit)

#### Brush Mode

To begin painting weights using the Brush mode, select a bone from the hierarchy in the Skeleton Tree panel. This will then display the weights assigned to that bone on the mesh.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/0c7c1c45-4768-44d5-b281-c04b4eb9afc6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0c7c1c45-4768-44d5-b281-c04b4eb9afc6?resizing_type=fit)

The Brush mode contains a set of brush **Operations** to help you edit weights:

| Operation | Description |
| --- | --- |
| 
**Add**

 | 

This mode is the default brush that will add weights to the current weight values until the maximum value of `1.0` is reached.

 |
| 

**Replace**

 | 

This mode replaces current weights, minus the strength value.

 |
| 

**Multiply**

 | 

This mode multiplies current weights by the strength value.

 |
| 

**Relax**

 | 

This mode applies the average of the connected vertex weights, by edges, to the current weights. This mode operates similarly to smoothing.

 |

You can also select from two **Types** of brushes:

| Brush | Description |
| --- | --- |
| 
**Surface**

 | 

The Surface Brush affects vertices proportional to the distance along the surface of the mesh, known as **Geodesic Distance**. This is useful when painting in tight spots with high curvature, like lips. The Surface Brush will not affect the top lip when painting the bottom, or vice versa.

 |
| 

**Volume**

 | 

The Volumetric Brush affects vertices proportional to the straight line distance from the brush center to the vertex. Regardless of connectivity or distance along the mesh.

 |

Each brush can also be modified with the following settings:

| Setting | Description |
| --- | --- |
| 
**Radius**

 | 

Set the size of the brush.

 |
| 

**Strength**

 | 

Set the strength of the brush that influences the result of the brush operations.

 |
| 

**Falloff**

 | 

Set the exponential falloff of the brush, or how the brush fluences point surrounding the center of the brush.

 |

After selecting your brush and mode, you can begin to paint the skin weight map for the selected bone by clicking and dragging the brush tool on the mesh in the viewport.

The **B** hotkey can be used to visually edit the **Brush Size** and the **Brush Strength.**

Hold down B and **drag left & right** to edit the *Radius* of the brush.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/671f1870-3b6d-4845-8c12-90d4191be50c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/671f1870-3b6d-4845-8c12-90d4191be50c?resizing_type=fit)

Hold down B and **drag up & down** to edit the *Strength* of the brush.

When you are finished with your weight edits, hit **Accept** to finalize your new weights and exit the tool.

If you are not happy with the result you can easily undo the modifications even after Accepting the weights by using **ctrl+z.**

#### Vertices Mode

Using the **Vertices** mode, you can select specific vertices you want to edit weights on using the **Marquee** selection tool.

Here you can reference a list of the Vertices Mode operations and a description of their functionality:

| Operation | Description |
| --- | --- |
| 
**Mirroring**

 | 

Mirrors the currently selected bones and vertice weights to the other side based on the **Mirror Plane** direction.

 |
| 

**Flood Weights**

 | 

Flood the selected weights using the **Brush Operations**. You can flood weights by selecting vertices and a bones and using the **Add** operation.

If weights on a Bone are flooded to `0.0`, or no weight, that bones' weights will be sent back to the Root bone of the hierarchy.



 |
| 

**Prune Weights**

 | 

Weights below the given threshold value will be removed. This is particularly useful for improving performance.

 |

To smooth hard perimeters of weight maps, select vertices, a bone, and use the **Relax** operation.

### Mirror Weights

To expedite the skin weight painting workflow, you can mirror symmetrical structures, such as limbs or other mirrored structures, using the Mirror button. To mirror a structure, select the bone, bone chain, or vertices you want to mirror, then select the **Mirror** button in the **Tools** panel under the **Edit Weights** tab.

When using the Vertices mode, if no vertices are selected the operations will run on all vertices affected by the selected bone. This can be useful for mirroring weights for the entire Left side of a character to the Right side

### Paint Attribute Maps

**Attribute Maps** are per-vertex weight maps that can be painted to send as data elsewhere in Unreal Engine, such as the [Deformer Graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/deformer-graph-in-unreal-engine). To Create a new Attribute Map to begin painting on, navigate to the **Edit Attributes** tab, give your Map a new name, and execute **Add Weight Map Layer**.

[![ImageAltText](https://dev.epicgames.com/community/api/documentation/image/996aa4f6-072d-4a0d-8277-89d422ce52bd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/996aa4f6-072d-4a0d-8277-89d422ce52bd?resizing_type=fit)

This new map will now display in the **Vertex Attributes** section under the **Attributes Inspector.**

After creating a new Attribute map, you can paint the map by selecting the **Paint Maps** tab in the Tool panel. You can choose the type map to paint under **Selected Attribute** then begin painting the mesh by clicking and dragging the **Viewport**.

## Hotkey Reference

Here you can reference a list of the available hotkeys for each of the Skeleton Creation Modes.

### Weight Editing

| Hotkey | Description |
| --- | --- |
| 
**B** (Hold) (drag-left-right)

 | 

Change radius size of brush

 |
| 

**B** (Hold) (drag-up-down)

 | 

Change strength of brush

 |
| 

**Shift**

 | 

Relax Brush

 |
| 

**Ctrl**

 | 

Invert Current Brush

 |
| 

**Middle-Mouse Click** (on a bone)

 | 

Visually select influence to paint

 |
| 

**F**

 | 

Frame camera on selected vertices or bones

 |

### Bone Editing

| Hotkey | Description |
| --- | --- |
| 
**N**

 | 

Create New Bone

 |
| 

**ESC**

 | 

Edit Bone

 |
| 

**B**

 | 

Reparent

 |
| 

**Shift** + **P**

 | 

Disconnect (unparent)

 |
| 

**Delete**

 | 

Remove bone

 |

## Python API

Here you can reference the Python API for the Skeleton Editing tools, that you can use to write scripts to automate your workflow.

### Accessing Bones and Weights

C++

`mesh_path = "/Game/Characters/Mannequins/Meshes/SKM_Quinn_Simple"  asset_editor = unreal.EditorAssetLibrary()  skel_mesh = asset_editor.load_asset(mesh_path)`

mesh\_path = "/Game/Characters/Mannequins/Meshes/SKM\_Quinn\_Simple" asset\_editor = unreal.EditorAssetLibrary() skel\_mesh = asset\_editor.load\_asset(mesh\_path)

Copy full snippet(5 lines long)

### Load the Modifier Libraries

C++

`# load the weight modifier  weight_modifier = unreal.SkinWeightModifier()  # load the skeleton modifier  skeleton_modifier = unreal.SkeletonModifier()`

\# load the weight modifier weight\_modifier = unreal.SkinWeightModifier() # load the skeleton modifier skeleton\_modifier = unreal.SkeletonModifier()

Copy full snippet(7 lines long)

### Creating New Bones

C++

`# Create two bones, a and b  skeleton_modifier.set_skeletal_mesh(skel_mesh)  skeleton_modifier.add_bones(["a", "b"],["root", "root"], [unreal.Transform(), unreal.Transform()])`

\# Create two bones, a and b skeleton\_modifier.set\_skeletal\_mesh(skel\_mesh) skeleton\_modifier.add\_bones(\["a", "b"\],\["root", "root"\], \[unreal.Transform(), unreal.Transform()\])

Copy full snippet(5 lines long)

### Parenting Bones

C++

`# Parent bone b to bone a  skeleton_modifier.parent_bone("b", "a")`

\# Parent bone b to bone a skeleton\_modifier.parent\_bone("b", "a")

Copy full snippet(3 lines long)

### Commit Changes

C++

`# Commit the changes  skeleton_modifier.commit_skeleton_to_skeletal_mesh()`

\# Commit the changes skeleton\_modifier.commit\_skeleton\_to\_skeletal\_mesh()

Copy full snippet(3 lines long)