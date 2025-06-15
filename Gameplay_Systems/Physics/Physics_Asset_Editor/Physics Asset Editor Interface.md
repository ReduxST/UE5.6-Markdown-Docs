# Physics Asset Editor Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:40

---

The **Physics Asset Editor** is a tool used for working [Physics Assets](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine) inside of Unreal Engine. This editor allows for the visualization and control over the body and constraint hierarchy associated with a Skeletal Mesh. In this editor, you can create [Bodies](/documentation/en-us/unreal-engine/physics-bodies-in-unreal-engine) and [Constraints](/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine) that are used for collision and simulation of your Skeletal Mesh ragdoll.

![The Physics Asset Editor is a tool used for working Physics Assets inside of Unreal Engine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4e52cfb-5b1c-45ee-87ab-55333304022f/physics-asset-editor-v2.png)

Please refer to each section below for a breakdown of the Physics Asset Editor user interface:

## 1\. Toolbar

The [Toolbar](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) inside the Physics Asset Editor provides you with options for saving any changes made to your Physics Asset or locating it in the Content Drawer. You can set a **Preview Mesh** and/or a **Preview Animation** for this particular Physics Asset, **Create Assets** to use with your mesh, **Enable / Disable Collision** for selected bodies, and use the **Simulation** settings under the **arrow** dropdown menu for testing the Physics Assets ragdoll. On the far right of the Toolbar is the **Editor Toolbar** which enables you to switch between the different [Animation Tools](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) in Unreal Engine.

## 2\. Skeleton Tree

The [Skeleton Tree](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree) shows the skeletal hierarchy of the current Skeleton asset and is where you create bodies and constraints.

## 3\. Constraints Graph

The [Constraints Graph](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---constraints-graph) enables you to have a visual representation of the skeletal hierarchy bodies that are constrained to another body. From this graph, you can create your constraints by pulling off the main body node (left) and selecting a new body to constrain or even navigate the skeleton tree by double-clicking the end body to jump down the tree to the next set of bodies and constraints. You can also see which [Physical Animation and Constraints Profiles](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles) are assigned based on the currently selected one in the Profiles panel.

## 4\. Viewport

The [Viewport](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) enables you to preview the changes you make, like the position of the physics bodies. You can also preview a simulation of the bodies as a physics ragdoll. From the Viewport, you can change lighting modes, show or hide the bones, bodies, and constraints of your skeleton, and even set your Skeletal Mesh to automatically rotate around on a turntable allowing you to view it from all angles.

## 5\. Asset Details / Preview Scene Settings

The [Details](/documentation/en-us/unreal-engine/level-editor-details-panel-in-unreal-engine) panel, which is similar to the Main Editor panel, is primarily used for modifying the properties of added elements like bodies or constraints. For example, when adding a body or constraint to the Skeleton, clicking on it in the Skeleton Tree or Viewport will populate the Details panel with options related to how the body or constraint functions.

The [Preview Scene Settings](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) panel enables you to quickly assess what your assets will look like in multiple environments and light scenarios without having to set up these scenes within your level. Several different settings can be defined and applied from Skeletal Meshes and specified animations to play along with lighting and **Post Process** effects all within each of the [Animation Tools](/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) inside of the Editor.

## 6\. Tools and Profiles

The [Tools](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles#toolstab) panel displays the options available for selected physics bodies when generating them or choosing to regenerate them. These are the same options available when creating a Physics Asset from the Content Drawer. Otherwise, these are the default settings that will be used when a Skeletal Mesh is imported and **Create Physics Asset** is enabled.

The [Profiles](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles#profilestab) panel enables you to create profiles that can be reused for **Physical Animations** and **Constraints**. These profiles enable you to set default settings that can be quickly assigned to other bodies or constraints.