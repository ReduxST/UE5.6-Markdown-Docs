# Physics Asset Editor - Skeleton Tree

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree)  
**Processed:** 2025-06-14 16:42:37

---

![The Skeleton Tree panel in the Physics Asset Editor shows the skeletal hierarchy of the current Skeleton asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b2de95f-d542-4f9e-8993-fdb147091a5c/skeleton-tree.png)

The **Skeleton Tree** panel in the [Physics Asset Editor](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine) shows the skeletal hierarchy of the current [Skeleton](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree) asset, along with additional assets like the collision bodies, primitives, and constraints. Within it, you can perform the following actions:

-   Select and view specific bones in the skeletal hierarchy with their attached bodies and constraints.
-   Create and edit bodies, primitives, and constraints, which can be simulated in the Viewport to see the results of ragdoll animations, constraints, and collision interaction.
-   Create preview assets, which are temporarily attached assets; these are good for previewing how a weapon will look on a character, for example.

## Interface Breakdown

![Interface Breakdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ed7bb1c-0051-4ff3-8d61-ae67ffa67988/skeleton-tree-interface.png)

1.  [Search Line](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree#searchline)
2.  [Bone Hierarchy List](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree#bonehierarchylist)
3.  [Skeleton Options](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree#skeletonshow/hideoptions)

### Search Line

![The Search line allows for quick filtering of the Skeletal hierarchy by filtering out the hierarchy to only include names based on the entered text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85de11bc-02b1-4ec4-88db-0d4b8d6034a3/search-line.png)

The **Search** line allows for quick filtering of the Skeletal hierarchy by filtering out the hierarchy to only include names based on the entered text.

![Pelvis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16c1d1c6-92e5-4a33-b616-0bfa1889d1f6/search-example.png)

Above, we have filtered the hierarchy to include any Bone Names, Bodies, or Constraints that include the text Pelvis in them.

### Bone Hierarchy List

![Bone Hierarchy List](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74068bd0-4b13-4228-a507-622666fe23d8/bone-hierarchy-list.png)

This window shows all the Bones, Bodies, Constraints, Primitives, and Preview Objects currently used by the selected Physics Asset. Inside this window is where you can add and assign collision Bodies, Primitives, Constraints, and Preview Objects. Most of the adjustments made in the Bone Hierarchy list are handled through right-click context menus where the menu options vary based on the object you right-click on (see the context menu sections below).

### Selection Context Menus

Within the Bone Hierarchy list, when you right-click on a Bone, Body, Primitive, or Constraint, you access context menus specific to the selection made.

Below are the available context menus and their relative options.

#### Bone Context Menu

When right-clicking on a Bone, you will see the following context menu:

![You will see the following context menu by clicking on the bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f51934e-eb2f-45b1-9931-fd781b5bfaa8/bone-context-menu.png)

| Option | Description |
| --- | --- |
| **Copy Selected Bone Names** | Copy the selected bone names to the clipboard. |
| **Reset Selected Bone Transforms** | Reset the transforms of the selected bones. |
| **Add Preview Asset** | Opens a menu of all eligible assets that can be temporarily attached to a bone for previewing purposes. For instance, if you want to see what a certain piece of armor would look like attached to a bone, this is the option you would use. Note, however, that this is not a permanent attachment and will only be visible while previewing. |
| **Remove All Attached Assets** | Removes all attached assets from the Skeleton and the mesh. |
| **Add/Replace Bodies** | Adds or replaces bodies for the selected bones using the current generation settings found in the [Tools](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles#toolstab) tab. |
| **Add Shape** | Adds shapes to the body. |
| **Select All Bodies** | Selects all bodies in the Skeleton Tree. |
| **Select Simulated Bodies** | Selects all simulated bodies in the Skeleton Tree. |
| **Select Kinematic Bodies** | Selects all kinematic bodies in the Skeleton Tree. |
| **Select All Constraints** | Selects all constraints in the Skeleton Tree. |

#### Body Context Menu

When right-clicking on a Body, you will see the following context menu:

![You will see the following context menu by clicking on the body](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5bb4dba-0fff-4382-943e-57a01f187bfd/body-context-menu.png)

| Option | Description |
| --- | --- |
| **Regenerate Bodies** | Regenerates the selected bodies using the current generation settings found in the [Tools](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles#toolstab) tab. |
| **Add Shape** | Adds shapes to this body. A Box, Sphere, or Capsule shape can be selected. |
| **Collision** | 
Adjust collision between bodies.

-   **Weld**: Weld the currently selected bodies together.
-   **Enable Collision**: Enable collision between the currently selected bodies.
-   **Enable Collision All**: Enable collision between the currently selected bodies and all bodies.
-   **Disable Collision**: Disable collision between the currently selected bodies.
-   **Disable Collision All**: Disable collision between the currently selected bodies and all bodies.



 |
| **Constraint selected bodies** | Create a constraint between all selected bodies as children and the last selected body as parent. |
| **Constraints** | Create a constraint between the selected body and one selected from the hierarchy list. |
| **Physics Type** | The type of physics to use for this body; kinematic or simulated. |
| **Physical Material** | Select a Physical Material to apply to all bodies. |
| **Copy Selected Bodies/Constraints To Clipboard** | Copy the bodies/constraints of the currently selected object to clipboard. |
| **Paste Bodies/Constraints From Clipboard** | Paste the previously selected bodies/constraints from clipboard. |
| **Copy Properties** | Copy the properties of the currently selected object to the next selected object. |
| **Paste Properties** | Past the properties of a previously selected object to the currently selected object. |
| **Delete** | Delete the currently selected body. |
| **Delete All Bodies Below** | Delete all bodies below the currently selected body in the Skeleton Hierarchy Tree. |
| **Mirror** | Find the body on the other side and duplicate its constraints and body. |
| **Assign** | Assigns the selected bodies to the current physical animation profile. |
| **Unassign** | Unassigns the selected bodies from the current physical animation profile. |
| **Copy Collision From Static Mesh** | Copy convex collision from a specified Static Mesh. |
| **Select All Bodies** | Selects all bodies in the Skeleton Tree. |
| **Select Simulated Bodies** | Selects all simulated bodies in the Skeleton Tree. |
| **Select Kinematic Bodies** | Selects all kinematic bodies in the Skeleton Tree. |
| **Select All Constraints** | Selects all constraints in the Skeleton Tree. |

#### Primitive Context Menu

When right-clicking on a Primitive, you will see the following context menu:

![You will see the following context menu by clicking on the primitive](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ca744b4-3568-4ba3-b73e-3a5f8104fb13/primitive-context-menu.png)

| Option | Description |
| --- | --- |
| **Rename** | Rename selected primitives. |
| **Duplicate** | Duplicate selected primitives. |
| **Delete** | Delete selected primitives. |
| **Select All Bodies** | Selects all bodies in the Skeleton Tree. |
| **Select Simulated Bodies** | Selects all simulated bodies in the Skeleton Tree. |
| **Select Kinematic Bodies** | Selects all kinematic bodies in the Skeleton Tree. |
| **Select All Constraints** | Selects all constraints in the Skeleton Tree. |

#### Constraint Context Menu

When right-clicking on a Constraint, you will see the following context menu:

![You will see the following context menu by clicking on the constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db56fe5f-ed30-4c92-a760-66e24f202f73/constraint-context-menu.png)

| Option | Description |
| --- | --- |
| **Snap** | Snap the selected constraint to Bone. |
| **Reset** | Resets the constraint to the default state. |
| **Axes and Limits** | 
Edit axes and limits of this constraint.

-   **Cycle Constraint Orientation**: Cycles constraint orientation between different cardinal axes.
-   **Cycle Active Constraint**: Cycles whether each constraint axis is active in isolation.
-   **Lock Swing**: Set swings 1 or 2 to be locked or limited.
-   **Lock Twist**: Set twist to be locked or limited.



 |
| **Convert** | 

Convert constraint to various presets.

-   Ball & Socket
-   Hinge
-   Prismatic
-   Skeletal



 |
| **Copy Selected Bodies/Constraints To Clipboard** | Copy the bodies/constraints of the currently selected object to clipboard. |
| **Paste Bodies/Constraints From Clipboard** | Paste the previously selected bodies/constraints from clipboard. |
| **Copy Properties** | Copy the properties of the currently selected object to the next selected object. |
| **Paste Properties** | Past the properties of a previously selected object to the currently selected object. |
| **Delete** | Delete the currently selected constraint. |
| **Assign** | Assigns the selected constraints to the current physical animation profile. |
| **Unassign** | Unassigns the selected constraints from the current physical animation profile. |
| **Copy Collision From Static Mesh** | Copy convex collision from a specified Static Mesh. |
| **Select All Bodies** | Selects all bodies in the Skeleton Tree. |
| **Select Simulated Bodies** | Selects all simulated bodies in the Skeleton Tree. |
| **Select Kinematic Bodies** | Selects all kinematic bodies in the Skeleton Tree. |
| **Select All Constraints** | Selects all constraints in the Skeleton Tree. |

#### Preview Asset Context Menu

A **Preview Asset** is an asset, such as a Static Mesh or Skeletal Mesh, that has been temporarily attached to a bone or socket for previewing purposes.

When right-clicking on a Preview Asset, you will see the following context menu:

![You will see the following context menu by clicking ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26b1375a-eded-4229-9a32-5bc3c9b3ea65/preview-asset-context-menu.png)

| Option | Description |
| --- | --- |
| **Add Preview Asset** | Opens a menu of all eligible assets that can be temporarily attached to a bone for previewing purposes. For instance, if you want to see what a certain piece of armor would look like attached to a bone, this is the option you would use. Note, however, that this is not a permanent attachment and will only be visible while previewing. |
| **Remove All Attached Assets** | Deletes all Preview Assets currently on the mesh. |

### Skeleton Show/Hide Options

The Skeleton Options window enables you to show or hide Bones, Bodies, Constraints, and Primitives.

![The Skeleton Options window enables you to show or hide Bones Bodies Cinstraints and Primitives](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f20721d1-a989-4c95-82af-4f39ddd37c9a/show-hide-options.png)

| Option | Description |
| --- | --- |
| **UpperBodyMask** | Selects the blend profile for editing. |
| **LowerBodyMask** | Selects the blend profile for editing. |
| **FastFeet** | Selects the blend profile for editing. |
| **LeftFingersMask** | Selects the blend profile for editing. |
| **UpperBodyLowerBodySplitMask** | Selects the blend profile for editing. |
| **Clear** | Clears the selected blend profile. |
| **Add Time Blend Profile** | Adds a new time blend profile for this skeleton. |
| **Add Weight Blend Profile** | Adds a new weight profile for the skeleton. |
| **Add Blend Mask** | Adds a new blend mask for the skeleton. |
| **Filtering Flattens Hierarchy** | Whether to keep the hierarchy or flatten it when searching for tree items. |
| **Hide Parents When Filtering** | Whether to show parent items grayed out or hide them entirely when filtering. |
| **Show Bodies** | Display bodies in the tree view. Bodies are a collection of primitive shapes used for collision. |
| **Show Simulated Bodies** | Show all simulated bodies in the Skeleton Tree. |
| **Show Kinematic Bodies** | Show all kinematic bodies in the Skeleton Tree. |
| **Show Constraints** | Display constraints in the tree view. Constraints are used to control how bodies can move in to one another. |
| **Show Primitives** | Display primitive shapes (spheres, boxes, capsules, etc.) in the tree view. |
| **Show Constraints on Parent Body** | Display constraints on both the parent and child body. |
| **Show All Bones** | Show every bone in the skeleton. |
| **Show Mesh Bones** | Show bones that are used in the mesh. |
| **Show LOD Bones** | Show bones that are used in the LOD (level of detail) being displayed. |
| **Show Weighted Bones** | Show bones that have vertices weighted to them. |
| **Hide Bones** | Hide all bones (sockets and attached assets will still be listed). |