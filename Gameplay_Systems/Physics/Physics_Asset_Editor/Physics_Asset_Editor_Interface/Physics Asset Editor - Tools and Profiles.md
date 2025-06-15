# Physics Asset Editor - Tools and Profiles

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---tools-and-profiles)  
**Processed:** 2025-06-14 16:42:38

---

The **Tools** and **Profiles** tabs enable you to choose how [Bodies](/documentation/en-us/unreal-engine/physics-bodies-in-unreal-engine) are generated and allow for custom profiles for default properties of assigned bodies and constraints.

![The Tools and Profiles tabs enable you to choose how Bodies are generated and allow for custom profiles for default properties of assigned bodies and constraints](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ccaed45-6781-4752-a6c8-c79f1b779215/tools-and-profiles.png)

## Tools Tab

The **Tools** tab enables you to perform batch edits of your Physics Asset. It includes being able to add, generate or re-generate bodies for the entire skeleton or selected bodies in the [Skeleton Tree](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree).

![The Tools tab enables you to perform batch edits of your Physics Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b76dbfb-2671-4ebe-800c-0929eb7c3988/tools.png)

### Body Creation Settings

The following options are available when creating or editing primitive shapes, sizes, and more for bodies:

![The following options are available when creating or editing body](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e14c2fa-1405-4e56-9bb4-9cfbc2f6d63b/body-creation-settings.png)

| Property | Description |
| --- | --- |
| **Min Bone Size** | Bones that are shorter than this value will be ignored for body creation. |
| **Primitive Type** | 
The geometry type that should be used when creating bodies.

-   Box
-   Capsule
-   Sphere
-   Tapered Capsule (Cloth Only)
-   Single Convex Hull
-   Multi Convex Hull



 |
| **Vertex Weighting Type** | 

How vertices are mapped to bones when approximating them with bodies.

-   Any Weight
-   Dominant Weight



 |
| **Auto Orient to Bone** | Whether to automatically orient the created bodies to their corresponding bones. |
| **Walk Past Small Bones** | Whether to skip small bones entirely (rather than merge them with the adjacent bones). |
| **Create Body for All Bones** | Forces the creation of a body for each bone. |
| **Disable Collisions by Default** | Whether to disable collision of body with other bodies on creation. |
| Advanced Properties |   |
| **Min Weld Size** | Bones that are smaller than this value will be merged for body creation. |
| **Hull Accuracy** | When creating convex hulls, the target accuracy of the created hull. |
| **Max Hull Verts** | When creating convex hulls, the maximum verts that should be created. |

### Constraint Creation Settings

The following options are available when creating or editing the constraints of bodies:

![The following options are available when creating or editing constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88872519-f7cb-4dd0-8e73-8943c27198d0/constraint-creation-settings.png)

| Property | Description |
| --- | --- |
| **Create Joints** | Whether to create constraints between adjacent created bodies. |
| **Angular Constraint Mode** | 
The type of angular constraints to create between bodies.

-   **Free**: No constraint against this axis.
-   **Limited**: Limited freedom along this axis.
-   **Locked**: Fully constraint against this axis.



 |

#### Body Generation Options

Once the properties have been set for the **Body Creation** and **Constraint Creation** categories, any selected bodies, constraints, or bones will display an action to add, generate, or re-generate bodies.

![Body Generation Option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e080d300-e338-4b4b-b7f2-95e0a9ea07ca/tools-body-button.png)

| Button |   |
| --- | --- |
| !\[All physics bodies and constraints will be re-created\] (all-bodies.png) | All physics bodies and constraints will be re-created. |
| ![This button will enable all bodies and constraints to be recreated using the new settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28d713d0-d6b6-4f28-be2b-c97a438a9218/generate-all-bodies.png) | When a constraint is selected, this button will enable all bodies and constraints to be recreated using the new settings. |
| ![Selected bodies will be replaced along with their constraints using the new settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27891159-683c-4b57-a945-37eacff5331d/regenerate-bodies.png) | Selected bodies will be replaced along with their constraints using the new settings. |

## Profiles Tab

The Physics Asset **Profiles** tab enables you to view, select, and edit a collection of settings for **Physical Animations** and **Constraints** that can be saved to profiles which can then be assigned to the selected bodies or constraints in the [Skeleton Tree](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---skeleton-tree).

![Profiles Tab](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8041d822-6ccb-420a-8be1-cf215bc82ab4/profiles.png)

For additional information, see the [Using Profiles for Bodies and Constraints](/documentation/en-us/unreal-engine/using-profiles-for-bodies-and-constraints-in-unreal-engine) page.

### Current Profile

The **Current Profile** drop-down is where you'll find any new or existing profiles that have been created. When the profile is selected, options to remove it from the list of profiles, and assign or unassign it from the selected bodies or constraints will become available.

![The Current Profile drop-down is where you'll find any new or existing profiles that have been created](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f360ff8-66c1-4cd6-ae96-01a98f6e3c56/current-profile.png)

| Option | Description |
| --- | --- |
| **New** | Creates a new profile that has properties set and can be assigned to bodies or constraints. |
| **Delete** | Removes the custom profile when it is set as the **Current Profile** selection. |
| **Assign** | Assigns the selected bodies or constraints to the **Current Profile** selection. |
| **Unassign** | Unassigns the selected bodies or constraints from the **Current Profile** selection. |

Some options are available for the Current Profile by clicking the **arrow** drop-down.

![Some options are available for the Current Profile by clicking the arrow drop-down](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/714eaf4f-9fc9-4636-b5c7-cd3478f957c7/current-profile-menu.png)

| Option | Description |
| --- | --- |
| **Duplicate** | Copies the currently set profile. |
| **Set Current Constraint Profile** | Select from the currently created profiles the one to be used as the Current Profile to assign, unassign, or delete. |

#### Current Profile Assignment

When bodies or constraints are assigned a profile, there are a couple of places where you can check the status of the assignment:

-   From the Details panel
-   From the [Graph](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---constraints-graph)

In the **Details** panel, the **Current Profile** being used for the selected body will be listed. When there isn't a profile assigned, it will be listed as **None**.

![Current Profile Assignment](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/228315d6-382a-46da-8e3c-1ab7481ef591/current-profile-assignment.png)

|   |   |
| --- | --- |
| ![Unassigned Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af995b13-fe25-4655-bd95-d7b68018b75c/current-profile-none.png) | ![Assigned Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/638556d3-36ea-4c52-b182-724960417921/current-profile-name.png) |
| Unassigned Profile | Assigned Profile |

In the [Graph](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---constraints-graph), the selected bodies and their constraints will be displayed. The shading of the bodies and constraints will be based on which the profile is selected as the **Current Profile**.

![The shading of the bodies and constraints will be based on which profile is selected as the Current Profile](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91bbc6af-7ee5-45e9-899f-8bb60f6a4158/profile-assignment.png)

For example, the Graph is showing the selected body and constraints, while the Profiles tab is showing the Current Profile for Physical Animation set to **MyPhysicalAnimation\_Profile** which is assigned to two of the four bodies in the Graph. When the Current Profile selected is assigned to a node, it will have an unshaded fill color, and when the node is not assigned that profile, it will appear shaded. The constraints displayed all appear with their fill color since the Current Profile for Constraints is set to **None**.

For additional information about the nodes in the Graph, see the [Constraints Graph](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine---constraints-graph) page.

#### Physical Animation Profiles

When Bodies are selected and assigned a Physical Animation profile, the following options will become available:

![Physical Animation Profiles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7e8080d-5aa6-4a42-a719-86ad696e353a/physical-animation-settings.png)

| Property | Description |
| --- | --- |
| **Is Local Simulation** | Whether the drive targets are in the world or local space. |
| **Orientation Strength** | The strength used to correct orientation error. |
| **Angular Velocity Strength** | The strength used to correct angular velocity error. |
| **Position Strength** | The strength used to correct linear position error. Only used for non-local simulation. |
| **Velocity Strength** | The strength used to correct linear velocity. Only used for non-local simulation. |
| **Max Linear Force** | The max force used to correct linear errors. |
| **Max Angular Force** | The max force used to correct angular errors. |

#### Constraint Profiles

When Constraints are selected and assigned a Constraints Profile, the following options will become available:

Click the image to view the full size.

For additional information, visit the [Constraints Reference](/documentation/en-us/unreal-engine/physics-constraint-reference-in-unreal-engine) page.

### Thumbnail

Control how the thumbnail image for the Physics Asset should appear in the **Content Drawer**. You can control the Pitch, Yaw, and Zoom of the thumbnail.

![Control how the thumbnail image for the Physics Asset should appear in the Content Drawer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/83527955-be1b-42ea-b5b7-28ebd1c58392/thumbnail-settings.png)

When the Thumbnail pitch, yaw, and zoom values are adjusted the thumbnail in the **Content Drawer** will update in real-time.

![When the Thumbnail pitch yaw and zoom values are adjusted the thumbnail in the Content Drawer will update in real time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edc4dd5f-d639-4efd-a457-e1434a1b7288/content-drawer-thumbnail.png)

### Physics

The following options are available that will apply to all assigned profiles.

![The following options are available that will apply to all assigned profiles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b99d9982-0d2d-4193-b603-013bf655ace1/physics-settings.png)

| Property | Description |
| --- | --- |
| **Not for Dedicated Server** | If true, skips instancing bodies for the PhysicsAsset on dedicated servers. |