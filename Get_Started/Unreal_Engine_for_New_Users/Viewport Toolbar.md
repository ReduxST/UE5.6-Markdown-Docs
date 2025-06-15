# Viewport Toolbar

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar)  
**Processed:** 2025-06-14 17:03:04

---

When working in the Unreal Editor, there are Level Editor Modes that each have their own workflows, functionality, and toolbar that corresponds to this. This **Viewport Toolbar** is located above the editor viewport, they include quick-select tools and menu options that affect how you interact with objects, the level in general, and what you see there. These viewport toolbar options can change depending on which mode the level editor is currently using.

## Improved Viewport Toolbar versus the Legacy Viewport Toolbar

Unreal Engine 5.6 introduces the improved viewport toolbar that has a new layout that accommodates modern workflows. This viewport toolbar replaces the previous viewport toolbar entirely for the Level Viewport and any other asset editors that also have a viewport.

[![The improved level viewport toolbar in Unreal Engine 5.6 and later compared to the legacy viewport toolbar found in earlier versions of Unreal Engine.](https://dev.epicgames.com/community/api/documentation/image/1466b2a4-8d7a-4654-b425-eae11f07c257?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1466b2a4-8d7a-4654-b425-eae11f07c257?resizing_type=fit)

The improved level viewport toolbar in Unreal Engine 5.6 and later compared to the legacy viewport toolbar found in earlier versions of Unreal Engine.

This update to the viewport toolbar provides the following benefits: 

-   It has consistent locations for features ordered by logical categories, such as those for transforms, snapping, and view modes.
    
-   Unification of related tools and options that were previously located in high-level settings dropdowns.
    
-   Better overflow management for smaller viewports as quick-select elements and menu condense and collapse into an overflow menu.
    
-   Unique toolbars for Level Editor Modes and asset editors with their own specific controls.
    
-   User-customizable menus.
    
-   Better extensibility and customization with the \`ToolsMenu\` system.
    

## Viewport Toolbar Interface

The toolbar — whether it’s in the level editor or an asset editor — is located just above the viewport window.

[![Toolbar interface](https://dev.epicgames.com/community/api/documentation/image/697b0bce-0f56-4e4c-b98b-d805e5a50a15?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/697b0bce-0f56-4e4c-b98b-d805e5a50a15?resizing_type=fit)

The tools and settings are grouped into the following categories: 

The improved Viewport Toolbar is located at the top of any viewport as a separate toolbar above the viewport window. Its settings and tools are grouped into the following categories:

[![Toolbar settings grouped into 5 categories.](https://dev.epicgames.com/community/api/documentation/image/794446dd-254a-4d46-a5df-1043f0d44582?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/794446dd-254a-4d46-a5df-1043f0d44582?resizing_type=fit)

1.  [Transform and Snapping Tools](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar#viewport-toolbar-transform-amp-snapping-tools)
    
2.  [Camera-Related Tools](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar#viewport-toolbar-camera-settings)
    
3.  [View Mode and Show Flag Options](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar#viewport-toolbar-view-mode-and-show-flag-options)
    
4.  [Performance and Scalability Options](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar#viewport-toolbar-performance-and-scalability-tools)
    
5.  [Viewport-Related Options](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-toolbar#viewport-related-settings)
    

## Viewport Toolbar Transform & Snapping Tools

The **Transform** and **Snapping** tools make up most of the tools you’ll use to select and manipulate objects within the editor viewport. This includes tools for selection, snapping, space orientation, and quick-select options for the most common ones.

### Transform Tools

The **Transform** **tools** are a set of quick selection tools to move, rotate, and scale objects and set what space (local or world) these should operate in. These options are how you will interact with objects in the level. This part of the toolbar also includes a dropdown menu with additional transform-related options.

[![Viewport transform tools area.](https://dev.epicgames.com/community/api/documentation/image/96df7d16-0702-467e-bd22-c9fcb25f5fcc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/96df7d16-0702-467e-bd22-c9fcb25f5fcc?resizing_type=fit)

You can use these quick-select toolbar options to manipulate objects in the viewport:

[![Viewport quick-select transform tools.](https://dev.epicgames.com/community/api/documentation/image/f1869f64-4930-4e2e-8a9e-81a4a8978622?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f1869f64-4930-4e2e-8a9e-81a4a8978622?resizing_type=fit)

| Icon | Name | Keyboard Shortcut | Description |
| --- | --- | --- | --- |
| 
[![Transform tool select icon](https://dev.epicgames.com/community/api/documentation/image/85b86b76-d3aa-49db-892a-371a1df26c0e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/85b86b76-d3aa-49db-892a-371a1df26c0e?resizing_type=fit)



 | 

**Select Objects**

 | 

**Q**

 | 

Use this option to select objects within the viewport.

 |
| 

[![Select and transform icon](https://dev.epicgames.com/community/api/documentation/image/eb7f28ad-f90d-4bc3-9ca2-9530e73a3581?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eb7f28ad-f90d-4bc3-9ca2-9530e73a3581?resizing_type=fit)



 | 

**Select and Translate Objects**

 | 

**W**

 | 

Use this option to select objects and move them around the world using the translate gizmo. Use the gizmo to move objects along individual axes, dual axes, or on all three axes.

 |
| 

[![Select and rotate objects tool icon](https://dev.epicgames.com/community/api/documentation/image/f784e0e6-7a9c-4118-b42c-170e69783be7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f784e0e6-7a9c-4118-b42c-170e69783be7?resizing_type=fit)



 | 

**Select and Rotate Objects**

 | 

**E**

 | 

Use this option to select objects and rotate them using the rotate gizmo. Use the gizmos to rotate the selected object along individual axes.

 |
| 

[![Select and scale objects tool icon](https://dev.epicgames.com/community/api/documentation/image/ce649799-4ddb-4def-8131-07299be6a58e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ce649799-4ddb-4def-8131-07299be6a58e?resizing_type=fit)



 | 

**Select and Scale Objects**

 | 

**R**

 | 

Use this option to select objects and scale them using the scale gizmo. Use the gizmo to scale objects along individual axes, dual axes, or uniformly on all three axes.

 |

|  |  |  |
| --- | --- | --- |
| 
[![Transform tools video of object moving.](https://dev.epicgames.com/community/api/documentation/image/58f9bffb-feba-477e-9424-bd74da305bd8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/58f9bffb-feba-477e-9424-bd74da305bd8?resizing_type=fit)



 | 

[![Transform tools video of object rotating..](https://dev.epicgames.com/community/api/documentation/image/40fc8551-61c3-408d-a56b-837d943399d2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/40fc8551-61c3-408d-a56b-837d943399d2?resizing_type=fit)



 | 

[![Transform tools video of object rotating.](https://dev.epicgames.com/community/api/documentation/image/3833ed08-6bf6-4083-890b-c31fe6e9c650?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3833ed08-6bf6-4083-890b-c31fe6e9c650?resizing_type=fit)



 |
| 

**Move**

 | 

**Rotate**

 | 

**Scale**

 |

  You can click the **Coordinate Space** icon to toggle between World and Local space that affects how objects in the viewport are translated and rotated.

[![Coordinate space tool in toolbar.](https://dev.epicgames.com/community/api/documentation/image/dbbf9393-9b91-422b-a92b-dced9ffcce57?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dbbf9393-9b91-422b-a92b-dced9ffcce57?resizing_type=fit)

| Icon | Name | Keyboard Shortcut | Description |
| --- | --- | --- | --- |
| 
[![World space coordinates icon](https://dev.epicgames.com/community/api/documentation/image/48264079-12b4-49bf-b9bc-18961dcd3717?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/48264079-12b4-49bf-b9bc-18961dcd3717?resizing_type=fit)



 | 

**World Space Coordinates**

 | 

**CTRL + \`**

 | 

This icon is the coordinate system used for World Space (the entire level), with its origin being the center of the scene (the world grid). This coordinate system is fixed — you cannot transform it. Objects are translated and rotated in absolute units relative to the level’s origin and scale relative to the entire level.

 |
| 

[![Local space coordinates icon](https://dev.epicgames.com/community/api/documentation/image/e2a93a6c-9b8e-4add-8087-13396de886d0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e2a93a6c-9b8e-4add-8087-13396de886d0?resizing_type=fit)



 | 

**Local Space Coordinates**

 | 

**CTRL + \`**

 | 

This icon is the coordinate system used for Local (Object) Space with its coordinate system relative to the scene component to which the actor is attached. Every actor has a local space coordinate system within a scene relative to the actor’s pivot point. Use local space to translate or rotate an object relative to its parent.

 |

|  |  |
| --- | --- |
| 
[![Video of world space view and rotate.](https://dev.epicgames.com/community/api/documentation/image/d7730f74-afd2-416f-a399-8b42458991ec?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d7730f74-afd2-416f-a399-8b42458991ec?resizing_type=fit)



 | 

[![Video of local space move and rotate.](https://dev.epicgames.com/community/api/documentation/image/3c97e3c4-fd49-4c85-9876-42c1b9a11463?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3c97e3c4-fd49-4c85-9876-42c1b9a11463?resizing_type=fit)



 |
| 

**World Space Move and Rotate**

 | 

**Local Space Move and Rotate**

 |

  For more in-depth explanations of Unreal Engine’s coordinate system and coordinate spaces for transforming objects within a 3D space, see [Coordinate System and Spaces](https://dev.epicgames.com/documentation/en-us/unreal-engine/coordinate-system-and-spaces-in-unreal-engine).

#### Viewport-Related Transform Tools Menu

The **Transform** toolbar dropdown menu contains a list of transform options, coordinate spaces, and options for how the gizmo is displayed in the level editor viewport. Some options here, such as transform tool and coordinate system are available as quick-select options in the viewport toolbar.

[![Image of transform tools menu with checkbox options.](https://dev.epicgames.com/community/api/documentation/image/f6e938b4-dc21-40c2-aef8-1967a44c80ba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f6e938b4-dc21-40c2-aef8-1967a44c80ba?resizing_type=fit)

  The menu is broken down into the following categories:

| Menu Section | Name | Description |
| --- | --- | --- |
| 
[![Transform tools menu.](https://dev.epicgames.com/community/api/documentation/image/639a5271-4dc8-4d20-aad9-1b8a88ce9561?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/639a5271-4dc8-4d20-aad9-1b8a88ce9561?resizing_type=fit)



 | 

**Transform Tools**

 | 

Menu options to select the transform tool or coordinate space you want to use. These options are available as quick-select options in the viewport toolbar.

 |
| 

[![Transform tools menu, gizmo options.](https://dev.epicgames.com/community/api/documentation/image/eb4dfd7b-17b2-482e-8921-4ef206d36f76?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eb4dfd7b-17b2-482e-8921-4ef206d36f76?resizing_type=fit)



 | 

**Gizmo Options**

 | 

Menu options to change how you view and interact with the transform tools gizmo when objects are selected.

 |
| 

[![Transform tools menu, selection options.](https://dev.epicgames.com/community/api/documentation/image/cbf459d5-8ff2-4faf-9473-e8657d39b5ca?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cbf459d5-8ff2-4faf-9473-e8657d39b5ca?resizing_type=fit)



 | 

**Selection Options**

 | 

Menu options to change how you select objects in the viewport.

 |

### Snapping Tools & Snap Settings

The **Snapping** tools includes a set of quick selection tools for snap sizes and angles to move, rotate, and scale objects in incremental steps. The snap settings also include options for how objects should snap to other objects and surfaces. 

The **Snapping Settings** dropdown displays a list of optional toggles for how objects snap within the world.

[![Snapping tools menu.](https://dev.epicgames.com/community/api/documentation/image/e2d01b22-1869-4c72-87be-eb84ebecce31?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e2d01b22-1869-4c72-87be-eb84ebecce31?resizing_type=fit)

The toolbar includes quick-select snapping toggles and size / angle increments settings.

[![Snapping tools increment settings.](https://dev.epicgames.com/community/api/documentation/image/caeb84f3-337e-4aca-9e53-1b4f0e2c11a5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/caeb84f3-337e-4aca-9e53-1b4f0e2c11a5?resizing_type=fit)

When clicking on the values next to any quick-select snapping icon in the toolbar, you can use its dropdown to set a value, or select from available ones to use.

|  |  |  |  |
| --- | --- | --- | --- |
| 
[![Surface snapping setting options.](https://dev.epicgames.com/community/api/documentation/image/f82c1b0e-700d-4e4e-9214-1158e7cb7ba1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f82c1b0e-700d-4e4e-9214-1158e7cb7ba1?resizing_type=fit)



 | 

[![Snapping menu, grid snap options.](https://dev.epicgames.com/community/api/documentation/image/72d25b45-f481-4d9b-b3ad-9be1b82b5bf5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/72d25b45-f481-4d9b-b3ad-9be1b82b5bf5?resizing_type=fit)



 | 

[![Rotation angle snap increments.](https://dev.epicgames.com/community/api/documentation/image/542e6ef6-e14f-4443-95b3-2dad0de0fdd3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/542e6ef6-e14f-4443-95b3-2dad0de0fdd3?resizing_type=fit)



 | 

[![Snapping menu scaling options.](https://dev.epicgames.com/community/api/documentation/image/ef570fff-84c9-4a10-8ccc-7b2b2eab60b9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ef570fff-84c9-4a10-8ccc-7b2b2eab60b9?resizing_type=fit)



 |
| 

**Surface Snapping Settings**

 | 

**Grid Snap Sizes**

 | 

**Rotation Angle Snap Increments**

 | 

**Scaling Snap Sizes**

 |

#### Snap to Surfaces Settings

The **Surface Snapping** settings dropdown sets the snapping behavior of objects when you drag them around in the scene.

[![Surface snapping menu.](https://dev.epicgames.com/community/api/documentation/image/42a0465f-c761-4777-8353-54d6b2fcaa5d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/42a0465f-c761-4777-8353-54d6b2fcaa5d?resizing_type=fit)

The **Rotate to Normal Surface** setting toggles whether objects should align to the surface's normal direction they are being snapped to. For example, when an object, like the pillar below, is dragged along a curved surface, it aligns to the direction of the curved surface when this setting is enabled. When disabled, the pillar will always face in the direction it is oriented.

|  |  |
| --- | --- |
| 
[![Video clip of normal rotate to surface action.](https://dev.epicgames.com/community/api/documentation/image/9b6ddcf7-0d24-4b3f-938d-b83e32b289c7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9b6ddcf7-0d24-4b3f-938d-b83e32b289c7?resizing_type=fit)



 | 

[![Video of Rotate to surface in off mode.](https://dev.epicgames.com/community/api/documentation/image/ae4aad50-2ae8-402f-9c42-661a94c80ca6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ae4aad50-2ae8-402f-9c42-661a94c80ca6?resizing_type=fit)



 |
| 

**Rotate to Surface Normal: ON (default)**

 | 

  **Rotate to Surface Normal: OFF**

 |

## Viewport Toolbar Camera Settings

The **Camera Settings** contain options that affect the camera view for the viewport and the look of the scene.

[![Toolbar camera settings.](https://dev.epicgames.com/community/api/documentation/image/520a50af-f28e-4f26-9d4f-a13d5dcf8d93?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/520a50af-f28e-4f26-9d4f-a13d5dcf8d93?resizing_type=fit)

| Icon | Name | Description |
| --- | --- | --- |
| 
[![Camera perspective options](https://dev.epicgames.com/community/api/documentation/image/d713139c-3d33-4745-9478-3ed8a5589c85?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d713139c-3d33-4745-9478-3ed8a5589c85?resizing_type=fit)



 | 

**Camera Options**

 | 

A selection of options that affect the look of the viewport, its view, and includes the access to the high resolution screenshot tool.

 |
| 

[![Camera speed options icon](https://dev.epicgames.com/community/api/documentation/image/74dd8cd3-9c60-4a31-a054-f50f805255d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/74dd8cd3-9c60-4a31-a054-f50f805255d5?resizing_type=fit)



 | 

**Camera Speed Options**

 | 

Options that control the speed of the camera when moving through the world.

 |

### Camera Options Menu

You can click on the **Camera Options** dropdown menu that includes options to change the look of the viewport, switch between camera views for perspective and orthographic, set the viewport to a cinematic view, and more. The options available in this menu change depending on cameras placed in the level and whether you are using a perspective or orthographic view.

[![Camera toolbar menu.](https://dev.epicgames.com/community/api/documentation/image/5aceb983-41c9-4351-82b9-be17b704f28e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5aceb983-41c9-4351-82b9-be17b704f28e?resizing_type=fit)

  This menu is broken up into the following sections:

| Menu Section | Name | Description |
| --- | --- | --- |
| 
[![Camera perspective menu options.](https://dev.epicgames.com/community/api/documentation/image/c735cc7d-6476-4ac6-bc43-750f0585c67c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c735cc7d-6476-4ac6-bc43-750f0585c67c?resizing_type=fit)



 | 

**Perspective**

 | 

This camera view simulates how the human eye perceives the world. This camera view is the default view used for all viewports. The **View** options in this menu that affect field of view, near view plane, and far view plane are specific to the perspective camera view. 

 |
| 

[![Camera orthographic menu options.](https://dev.epicgames.com/community/api/documentation/image/dfc55278-77aa-4da5-bb6c-7b03f25f7ad4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dfc55278-77aa-4da5-bb6c-7b03f25f7ad4?resizing_type=fit)



 | 

**Orthographic**

 | 

This camera view uses a projection that maintains parallel lines, whereby objects appear to have the same scale regardless of their distance from the camera. This includes views for top, bottom, left, right, front, and back. 

 |
| 

[![Camera movement menu options.](https://dev.epicgames.com/community/api/documentation/image/136ae870-1351-4dd3-99f4-62ceb194bc00?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/136ae870-1351-4dd3-99f4-62ceb194bc00?resizing_type=fit)



 | 

**Movement**

 | 

Options to change how the viewport camera moves. You can pilot other actors in the scene and change the movement of the camera.

 |
| 

[![Camera view menu options.](https://dev.epicgames.com/community/api/documentation/image/44692a2a-f34b-4ff5-968a-27af2fba01a8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/44692a2a-f34b-4ff5-968a-27af2fba01a8?resizing_type=fit)



 | 

**View**

 | 

When the **Perspective** view is used, these options change the field of view, near view plane, and far view plane for how content is shown in the viewport.

 |
| 

[![Camera exposure menu options.](https://dev.epicgames.com/community/api/documentation/image/1b9d5570-c5fb-4d1d-9656-e31aedac0bed?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1b9d5570-c5fb-4d1d-9656-e31aedac0bed?resizing_type=fit)



 | 

**Exposure**

 | 

Override settings change the exposure value in the viewport. When Game Settings is disabled, you can use the text field to override the camera exposure for the viewport.

 |
| 

[![Camera viewport type menu options.](https://dev.epicgames.com/community/api/documentation/image/c826bb15-a4e3-48ca-b53b-a1ee0b0de7d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c826bb15-a4e3-48ca-b53b-a1ee0b0de7d5?resizing_type=fit)



 | 

**Viewport Type**

 | 

Choose a viewport layout to use. The **Cinematic Viewport** layout is tailored for cinematic workflows and adds the **Composition Overlays** options menu to the toolbar, where you can select different overlays for framing, masking, and composition.

 |
| 

[![Camera create menu options.](https://dev.epicgames.com/community/api/documentation/image/935ed14d-e65d-4510-9e2f-c9f7b4a10509?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/935ed14d-e65d-4510-9e2f-c9f7b4a10509?resizing_type=fit)



 | 

**Create**

 | 

Options to create camera actors in the world and scene bookmarks for camera views in the world.

 |
| 

[![Camera options menu choices.](https://dev.epicgames.com/community/api/documentation/image/5028b0ca-30a5-4c03-8430-c92a08d863e9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5028b0ca-30a5-4c03-8430-c92a08d863e9?resizing_type=fit)



 | 

**Options**

 | 

Toggleable settings that affect the viewport, such as game view that disables selection highlight and gizmos tools, or **Preview Selected Cameras** sets how large the preview window for a selected camera is in the bottom-right of the viewport.

 |

### Camera Perspective & Orthographic Views

You can use the **Camera Options** menu to select how content is displayed in the viewport. The default viewport uses the **Perspective** view, but you can select from a list of **Orthographic** views to use as well. 

[![Perspective and orthographic menu options.](https://dev.epicgames.com/community/api/documentation/image/cff6a187-1294-4660-bfac-cbb25452dc18?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cff6a187-1294-4660-bfac-cbb25452dc18?resizing_type=fit)

  Below is an example of different views in the viewport for both orthographic and perspective.

[![Orthographic and perspective views in 4 viewports.](https://dev.epicgames.com/community/api/documentation/image/caacf8be-a2af-40c6-9cc2-3560743cba74?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/caacf8be-a2af-40c6-9cc2-3560743cba74?resizing_type=fit)

### Movement Options

The **Movement** options section of the menu includes options for how you pilot actors using the viewport, and change camera movement in the viewport.

[![Camera movement options menu.](https://dev.epicgames.com/community/api/documentation/image/54670716-fa78-4da2-a267-987244d6a018?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/54670716-fa78-4da2-a267-987244d6a018?resizing_type=fit)

  This section of the menu includes the following settings:

| Setting Name | Description |
| --- | --- |
| Pilot |  |
| --- | --- |
| 
**Pilot \[Selected Actor\]**

 | 

Move the selected actor around using the viewport controls, and bind the viewport to the actor’s location and orientation.

 |
| 

**Stop Piloting Actor**

 | 

When piloting is enabled for an actor, this stops piloting of an actor with the current viewport. It unlocks the viewport’s position and orientation from the actor the viewport is currently piloting.

 |
| 

**Exact Camera View**

 | 

Toggles showing the exact camera view when using the viewport to pilot a camera.   


 |
| 

**Selected Piloted Actor**

 | 

Selects the currently piloted actor in the Outliner.

 |
| Camera Movement |  |
| --- | --- |
| 

**Camera Speed**

 | 

Set the camera speed for movement in the viewport. These options are available from the quick-select toolbar as well.

 |
| 

**Frame Selected**

 | 

Centers the viewport on the selected actor(s).

 |
| 

**Move Camera to Object**

 | 

Move the current camera to match the location and rotation of the selected object.

 |
| 

**Move Object to Camera**

 | 

Move the selected object to match the location and rotation of the current camera.

 |
| 

**Orbit Around Selection**

 | 

If enabled, the camera will orbit around the current selection in the viewport. 

 |
| 

**Link Ortho Camera Movement**

 | 

If enabled, all orthographic viewports are linked to the same position and move together. When disabled, they move independent of one another.

 |
| 

**Ortho Zoom to Cursor**

 | 

If enabled, orthographic viewport zooming centers on the mouse cursor’s position. When disabled, the zoom is around the center of the viewport.

 |

### View Options

The **View** options are available when the viewport is using the **Perspective** view. These options configure the viewing angle of the viewport camera, and at what distance content should be visible from this camera.

[![Image of menu options for field of view.](https://dev.epicgames.com/community/api/documentation/image/e0cc14a4-eb26-4b0e-87a7-07e1b7510d41?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0cc14a4-eb26-4b0e-87a7-07e1b7510d41?resizing_type=fit)

  This section includes the following settings:

| Setting Name | Description |
| --- | --- |
| 
**Field of View**

 | 

Sets the viewing angle of the viewport camera. This angle defines the extent of the world that is visible to the camera at any given time. The default is a **90 degree** viewing angle. Higher angles give you wider views to see more of the world but this skews the camera view. Lower angles show less of the world, feeling zoomed in, but the view of content is limited. 

 |
| 

**Near View Plane**

 | 

Sets the size of the plane used to clip through objects when the camera is close to a surface. Large values make the clip plane bigger to see through objects more easily. 

 |
| 

**Far View Plane**

 | 

Sets the far distance at which objects stop being rendered on screen.

This value does not affect objects that have Nanite enabled.



 |

In the example below, you can see how adjusting the field of view angle affectss your view:

|  |  |  |
| --- | --- | --- |
| 
[![Example field of view at 65 degrees.](https://dev.epicgames.com/community/api/documentation/image/1f9f86ec-5d0a-4b81-94bc-e598b1f3e822?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1f9f86ec-5d0a-4b81-94bc-e598b1f3e822?resizing_type=fit)



 | 

[![Example field of view at 90 degrees.](https://dev.epicgames.com/community/api/documentation/image/008005ee-07f9-41cc-bf25-ff45a6796c87?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/008005ee-07f9-41cc-bf25-ff45a6796c87?resizing_type=fit)



 | 

[![Example field of view at 120 degrees.](https://dev.epicgames.com/community/api/documentation/image/7f8ac9c9-e2b9-4644-aa48-fe2ec4c5e4b5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7f8ac9c9-e2b9-4644-aa48-fe2ec4c5e4b5?resizing_type=fit)



 |
| 

**Field of View: 65 Degrees**

 | 

**Field of View: 90 Degrees (Default)**

 | 

**Field of View: 120 Degrees**

 |

### Create Options

The **Create** options provide a way to place cameras and bookmarks in the world based on the current viewport location and orientation.

[![Options in the Create camera menu.](https://dev.epicgames.com/community/api/documentation/image/f3782511-7b30-423a-bbef-cbc4d8d722ab?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f3782511-7b30-423a-bbef-cbc4d8d722ab?resizing_type=fit)

  This section includes the following options:

| Setting Name | Description |
| --- | --- |
| Create Camera |  |
| --- | --- |
| 
**Camera Actor**

 | 

Spawn a Camera actor in the current location and orientation of the viewport. 

 |
| 

**Cine Camera Actor**

 | 

Spawn a Cine Camera actor in the current location and orientation of the viewport. 

 |
| Bookmarks |  |
| --- | --- |
| 

**Set Bookmark**

 | 

Choose a bookmark from the list to set with the current viewport location and orientation.

 |
| 

**Manage Bookmarks**

 | 

-   **Clear Bookmark**: Clears a specific bookmark that has been saved.
    
-   **Compact Bookmarks**: Attempts to move bookmark indices so they are continuous. For example, if you have bookmarks for 1, 2, and 4 slots bookmarked, this will attempt to move bookmark 4 to the bookmark 3 slot.
    
-   **Clear All Bookmarks**: Clears any saved bookmarks.
    

 |
| 

**Bookmarks List**

 | 

A list of any bookmarks that have been saved and what keyboard shortcut they are assigned to. 

 |

### General Options

The **Options** section of the menu includes general settings you can enable for the viewport. It also includes access to the **High Resolution Screenshot** tool, to capture still images from the viewport quickly.

[![General options menu items.](https://dev.epicgames.com/community/api/documentation/image/cbced124-5b07-408b-8002-b5c903fc3888?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cbced124-5b07-408b-8002-b5c903fc3888?resizing_type=fit)

  This section includes the following options:

| Setting Name | Description |
| --- | --- |
| 
**Allow Cinematic Control**

 | 

When enabled, this allows for cinematic (Sequencer) previews to play in this viewport. 

 |
| 

**Game View**

 | 

When enabled, the viewport shows the scene as it appears in the game — without editor widgets, selection highlights, or any other element usually only visible in the editor.

 |
| 

**Allow Camera Shakes**

 | 

When enabled, it allows for the camera shake previewer panel to apply shaking to this viewport. 

 |
| 

**Preview Selected Cameras**

 | 

When enabled, selecting a camera actor displays a live picture-in-picture preview from the camera’s perspective within the current editor viewport. This can be used to make adjustments to positioning, post processing, and other settings without having to possess the camera itself. The **Preview Size** value adjusts the size of this picture-in-picture preview window for the camera view.

 |
| 

**High Resolution Screenshot**

 | 

Opens the control panel dialog to take high resolution screenshots of the currently used viewport. 

 |

#### High Resolution Screenshot Tool

The **High Resolution Screenshot** tool is a dialog window you can use to capture still images of the current viewport window or you can use the **Crop** tool to select a part of the viewport to capture. It includes additional output options you can toggle on.

[![Menu options for the high resolution screenshot tool.](https://dev.epicgames.com/community/api/documentation/image/d71421b6-db23-4a72-921a-49f08ef093b6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d71421b6-db23-4a72-921a-49f08ef093b6?resizing_type=fit)

  For more information on using this tool, see [High Resolution Screenshot Tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/taking-screenshots-in-unreal-engine#highresolutionscreenshottool).

### Camera Speed Options

The **Camera Speed** dropdown menu includes options that affect the speed at which the camera can move around the world.

[![View of camera speed menu items.](https://dev.epicgames.com/community/api/documentation/image/1eafd4d4-829b-456f-957c-79ecd3eaa32b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1eafd4d4-829b-456f-957c-79ecd3eaa32b?resizing_type=fit)

| Setting Name | Description |
| --- | --- |
| 
**Camera Speed**

 | 

Sets the speed of the camera in first person mode. 

Hold either mouse button (LMB or RMB) and use the scroll wheel to adjust the camera speed up or down.



 |
| 

**Speed Scalar**

 | 

Multiplies the effective value of the camera speed slider, changing how quickly the slider changes camera speed.

 |
| 

**Distance Based Camera Speed**

 | 

When enabled, this scales the perspective camera speed based on the distance between the camera and its look-at position.

 |

## Viewport Toolbar View Mode and Show Flag Options

The **View Mode** and **Show Flag** options for the viewport enable different visualization modes and options to enable or disable elements being rendered in the viewport.

[![View of toolbar icons for view mode and show flag.](https://dev.epicgames.com/community/api/documentation/image/c4899c13-3ae2-4005-8b56-27fe35db5148?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c4899c13-3ae2-4005-8b56-27fe35db5148?resizing_type=fit)

| Icon | Name | Description |
| --- | --- | --- |
| 
[![Image of view mode button.](https://dev.epicgames.com/community/api/documentation/image/f0766fb7-158b-4a14-8048-ad3df941a661?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f0766fb7-158b-4a14-8048-ad3df941a661?resizing_type=fit)



 | 

**View Modes**

 | 

A listing of visualization modes to help see specific types of data being processed in your scene, such as lighting only, reflections, or buffer visualizations. These can help you diagnose and investigate specific issues for your project.

 |
| 

[![View of show flag icon.](https://dev.epicgames.com/community/api/documentation/image/430ec8dd-c966-4a01-a474-23a6557c6b0e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/430ec8dd-c966-4a01-a474-23a6557c6b0e?resizing_type=fit)



 | 

**Show Flags**

 | 

A list of engine features you can show and hide within the viewport. For example, you can disable all particle systems, individual post processing features, and more. 

 |

### View Modes

The **View Modes** dropdown menu includes many visualization options to select from. When selected, they apply to the current viewport only.

[![Image of the view modes dropdown menu items.](https://dev.epicgames.com/community/api/documentation/image/bde0afd1-bd7a-4d0a-bef7-c25a12056faf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bde0afd1-bd7a-4d0a-bef7-c25a12056faf?resizing_type=fit)

These are some examples of different view modes being applied to the viewport:

|  |  |  |
| --- | --- | --- |
| 
[![View of a set with the walls and actors lit.](https://dev.epicgames.com/community/api/documentation/image/239f8d7b-89ae-44e0-afd5-3227a17b3c93?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/239f8d7b-89ae-44e0-afd5-3227a17b3c93?resizing_type=fit)



 | 

[![View of a set with the walls and actors unlit.](https://dev.epicgames.com/community/api/documentation/image/b807627d-aa62-4fa0-b208-1c9421d354a0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b807627d-aa62-4fa0-b208-1c9421d354a0?resizing_type=fit)



 | 

[![View of a set with the walls and actors in light gradient..](https://dev.epicgames.com/community/api/documentation/image/d4d2155f-4b79-439c-a319-534ba3da84ed?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d4d2155f-4b79-439c-a319-534ba3da84ed?resizing_type=fit)



 |
| 

View Mode: Lit (default)

 | 

View Mode: Unlit

 | 

View Mode: Light Complexity

 |

For more information on using these view modes in your project workflows, see [View Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine).

### Show Flags

The **Show Flags** dropdown menu includes many options to toggle visibility of engine features, such as lighting, post processing, geometry types, and more.

[![Image of show flags menu items.](https://dev.epicgames.com/community/api/documentation/image/ef4daefe-6f46-470b-a4ce-e12f4e9f4a54?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ef4daefe-6f46-470b-a4ce-e12f4e9f4a54?resizing_type=fit)

For more information on using these show flags in your project, see [Viewport Show Flags](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-show-flags-in-unreal-engine).

## Viewport Toolbar Performance and Scalability Tools

The **Performance** and **Scalability Tool** menu includes options that affect the look and performance of content in the viewport. These tools are useful for approximating what content looks like on a particular platform, setting scalability for the project (to make it easier to work with), and looking at how the game can look with different scalability options. This can help you to set up your own scalability options for your project.

[![Image of scalability menu options on the toolbar.](https://dev.epicgames.com/community/api/documentation/image/fa566a50-d5ba-4818-ae19-f2a9ce25e56e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fa566a50-d5ba-4818-ae19-f2a9ce25e56e?resizing_type=fit)

### Realtime Viewport

The **Realtime Viewport** toggles whether the current viewport should update every frame.  

When disabled, the viewport only updates when you move around the scene. A warning icon is added to the viewport toolbar next to the performance and scalability dropdown menu. Clicking it restores realtime to the viewport.

[![Image of warning icon next to the realtime viewer.](https://dev.epicgames.com/community/api/documentation/image/31f43d66-398d-496a-818b-edcfb841382c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/31f43d66-398d-496a-818b-edcfb841382c?resizing_type=fit)

### Preview Platform

The **Preview Platform** rollout menu includes a variety of platform options to select from. Selecting platform and its target, triggers a shader recompile for the engine. Once completed, the viewport updates to display an approximation of what the scene would render like using this target. 

Each platform can have multiple targets depending on what rendering paths of the engine it supports.

[![Preview platform menu dropdowns.](https://dev.epicgames.com/community/api/documentation/image/8826a8b9-564d-40e8-97e9-e02427de813b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8826a8b9-564d-40e8-97e9-e02427de813b?resizing_type=fit)

This menu rollout includes the following options:

| Setting Name | Description |
| --- | --- |
| Preview Platform |  |
| --- | --- |
| 
**Disable Preview**

 | 

Disables any currently selected preview platform target and sets it back to the operating system's default preview. For Windows, this would be Windows with Shader Model 6 (SM6). 

 |
| 

**\[Platform Preview Select\]**

 | 

Choose from a list of platform targets to preview in the main editor viewport. Each platform can support multiple targets, such as Android with OpenGL and Vulkan preview options. Some platform preview options, such as console platforms, only become available when their SDKs are installed. 

 |

The scene below shows a comparison of the default viewport preview settings on WIndows compared to previewing the scene on Android in the viewport.

|  |  |
| --- | --- |
| 
[![Statue in a foyer, darker version image.](https://dev.epicgames.com/community/api/documentation/image/75f4d827-da28-49c9-a75b-8d14369a5050?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/75f4d827-da28-49c9-a75b-8d14369a5050?resizing_type=fit)



 | 

[![Statue in a foyer, better lighting.](https://dev.epicgames.com/community/api/documentation/image/9e0da18d-aa85-4426-a224-1295ae100db8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9e0da18d-aa85-4426-a224-1295ae100db8?resizing_type=fit)



 |
| 

**Windows with SM6**

 | 

**Android with Vulkan High**

 |

For more information, see [Mobile Previewer](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-mobile-previewer-in-unreal-engine).

### Viewport Scalability

The **Viewport Scalability** options include a rollout menu of common settings of the engine. You can change individual feature categories to be Low, Medium, High, Epic, or Cinematic, or you can select any of these quality options to set all categories to be Low, Medium, High, Epic, or Cinematic. Optionally, you can use **Auto** to configure the scalability options based on your system specifications and its performance.

[![Image of viewport scalability groups.](https://dev.epicgames.com/community/api/documentation/image/66609d7a-5753-470f-84d4-27dcc65c2d12?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/66609d7a-5753-470f-84d4-27dcc65c2d12?resizing_type=fit)

When the scalability options are set to anything other than the default, this warning icon appears in the toolbar. This is an indicator that what the game would look like running outside of the editor doesn’t reflect the options currently set in the scalability options. You can click this icon to reset the scalability options to their default settings.

[![Viewport scalability icon on the toolbar.](https://dev.epicgames.com/community/api/documentation/image/64d028d5-4b39-455a-807b-b50fc7a75ae1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/64d028d5-4b39-455a-807b-b50fc7a75ae1?resizing_type=fit)

For more information, see [Scalability](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-in-unreal-engine).

### Material Quality Level

The **Material Quality Level** rollout menu lists quality levels for Low, Medium, High, and Epic to choose from. You can use these to check any materials that use the **Quality Switch** node in a material. You can use these menu options to inspect only materials in the viewport. The material quality switches also work with the scalability options.

[![Material quality menu options.](https://dev.epicgames.com/community/api/documentation/image/5fba5d35-b1d9-4f62-8754-df69329a51d3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5fba5d35-b1d9-4f62-8754-df69329a51d3?resizing_type=fit)

### Screen Percentage

The **Screen Percentage** rollout menu includes information about the current screen percentage used in the viewport, and options to override screen percentage in the viewport. The summary in this menu provides specific information about the viewport and its current settings.

[![Image of the screen percentage menu options.](https://dev.epicgames.com/community/api/documentation/image/488a5724-5ad5-4f97-8cfc-073c0e7bb5fc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/488a5724-5ad5-4f97-8cfc-073c0e7bb5fc?resizing_type=fit)

## Viewport-Related Settings

The viewport **Settings** and **Overlay** menus assist with audio settings, mouse movement within the viewport, viewport layout options (for working with multiple viewports), and more.

[![Image of the settings and viewport-layout icons on the toolbar.](https://dev.epicgames.com/community/api/documentation/image/83261801-f15f-4a5a-b3ce-404267019998?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/83261801-f15f-4a5a-b3ce-404267019998?resizing_type=fit)

| Icon | Name | Description |
| --- | --- | --- |
| 
[![Viewport settings icon.](https://dev.epicgames.com/community/api/documentation/image/e7a69e83-6836-4373-841f-82d82eea97d6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e7a69e83-6836-4373-841f-82d82eea97d6?resizing_type=fit)



 | 

**Viewport Settings** 

 | 

A list of settings to control the volume of sounds in the level editor, configurable controls for interacting and traversing the scene in the level editor viewport, and more.

 |
| 

[![Viewport layout icon.](https://dev.epicgames.com/community/api/documentation/image/a6167bd2-db69-4da0-be2a-800b48f4dd0c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a6167bd2-db69-4da0-be2a-800b48f4dd0c?resizing_type=fit)



 | 

**Viewport Layout Options**

 | 

A list of viewport layouts to choose from when using more than one viewport.

 |

### Viewport Settings

The **Viewport Settings** menu includes options that affect controls and interactions with objects within the viewport, sound levels for audio playback, and quick access to the **Editor Preferences** you can configure for the viewport.

[![Viewport settings menu options.](https://dev.epicgames.com/community/api/documentation/image/b0103c4d-38fa-41a4-980d-446627bf3aa1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b0103c4d-38fa-41a4-980d-446627bf3aa1?resizing_type=fit)

| Settings Name | Description |
| --- | --- |
| Settings |  |
| --- | --- |
| 
**Level Editor Volume (dB)**

 | 

Sets the preview volume (in decibels) of audio placed in the level while working in the level editor.

 |
| Controls |  |
| --- | --- |
| 

**Mouse Sensitivity**

 | 

How fast the perspective camera moves through the world when using the mouse scroll wheel.

 |
| 

**Mouse Scroll Zoom Speed**

 | 

Sets the incremental speed at which the camera should move in a forward or reverse direction when using the mouse scroll wheel.

 |
| 

**Invert Middle Mouse Pan**

 | 

When enabled, the direction of the middle mouse panning in the viewport is inverted.

 |
| 

**Invert Orbit Axis**

 | 

When enabled, the Y-axis of the mouse movement when orbiting is inverted. 

 |
| 

**Invert Right Mouse Dolly**

 | 

When enabled, the direction of the right mouse dolly on the Y-axis in orbit mode is inverted.

 |
| 

**Scroll Gestures**

 | 

Set whether scroll gestures should use standard or natural scrolling when working in the **Perspective** and **Orthographic** viewports.

 |
| 

**Open Viewport Preferences**

 | 

Opens the advanced viewport settings of the **Editor Preferences**. There, you can configure settings for the look and feel, controls, grid snapping, and more. 

 |
| Cascade |  |
| --- | --- |
| 

**Cascade**

 | 

These settings only apply to the deprecated particle systems created with Cascade.

-   Enable Particle Systems LOD Switching: When enabled, Cascade particle systems will use distance level of detail (LOD) switching in perspective viewports.
    
-   **Toggle Particle System Helpers**: When enabled, Cascade particle systems show helper widgets in viewports.
    
-   **Freeze Particle Simulation**: When enabled, Cascade particle systems will freeze their simulation state.
    

  


 |

### Viewport Layouts and Sizing Settings

The **Viewport Layouts** includes a layouts window to select the type of viewport layout you prefer, and a quick-toggle to switch between a selected layout and maximized viewport screen.

[![Viewport layouts icon and ellipses on the toolbar.](https://dev.epicgames.com/community/api/documentation/image/c92f543d-ad68-4845-99c1-5a4739f37ba7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c92f543d-ad68-4845-99c1-5a4739f37ba7?resizing_type=fit)

The vertical ellipses menu includes different layout configurations you can choose from, including an option to use **Immersive View** with the selected viewport.

[![Viewport panes menu options in the toolbar.](https://dev.epicgames.com/community/api/documentation/image/8ed72bfe-c285-40f3-87ce-7ed1f060e74d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8ed72bfe-c285-40f3-87ce-7ed1f060e74d?resizing_type=fit)

The quick-toggle button switches between maximizing the currently selected viewport or switching to the selected layout configuration with multiple viewports displayed in the editor window.

[![Quick toggle menu icon on the toolbar.](https://dev.epicgames.com/community/api/documentation/image/9a56930a-df8c-48f8-9787-02d3f969e296?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9a56930a-df8c-48f8-9787-02d3f969e296?resizing_type=fit)

In this example, clicking the overlay toggle buttons will switch between the maximized and selected layout for the editor viewports.

### Viewport Toolbar Warning Indicators

When the interaction within a menu alters something critical that affects the viewport, such as a change that could cause visual or performative differences, actionable warning indicators appear in the viewport toolbar alongside the category they affect. This is helpful to indicate a change has occurred that can affect what you see in the viewport in some way.   

For example, when **Realtime Viewport** is disabled, the warning indicator can clue you into the fact that the viewport isn’t updating what you see, which can have unintended consequences.

When these indicators are shown, you can click them to rest the changed setting to its default state, in turn removing the warning.

[![Realtime viewport warning icon on the toolbar.](https://dev.epicgames.com/community/api/documentation/image/6165487c-14c4-4b98-9b30-485d798b92b0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6165487c-14c4-4b98-9b30-485d798b92b0?resizing_type=fit)

### Other Editor Viewports

The **Viewport Toolbar** is adapted to different modes of the level editor and to the individual asset editors it has. 

The sections below are some examples of these differences. 

### Level Editor Viewport Modes

The level editor can be put into different **Modes** to enable specialized editing interfaces and workflows for editing particular types of actors and geometry within the viewport. 

You can change the level editor mode using the dropdown selection menu in the main toolbar.

[![Menu of categories you can select via the selection tool.](https://dev.epicgames.com/community/api/documentation/image/362cc9db-7ea3-4eaf-9a42-980352a367e4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/362cc9db-7ea3-4eaf-9a42-980352a367e4?resizing_type=fit)

These modes change the primary behavior of the level editor viewport for a specialized task, such as moving and transforming assets in the world, sculpting landscapes, generating foliage, animating objects, and more.

| Level Editor Mode | Viewport Toolbar |
| --- | --- |
| 
**Selection (default)**

 | 

[![Default toolbar for level editor modes.](https://dev.epicgames.com/community/api/documentation/image/f5350e38-d61e-4a55-b06c-5183b3d1b172?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f5350e38-d61e-4a55-b06c-5183b3d1b172?resizing_type=fit)



 |
| 

**Animation**

 | 

[![Animation toolbar for level editor modes.](https://dev.epicgames.com/community/api/documentation/image/745169d6-bfd0-4a1e-a356-b57fb64337fd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/745169d6-bfd0-4a1e-a356-b57fb64337fd?resizing_type=fit)



 |
| 

**Modeling**

 | 

[![Modeling toolbar for level editor modes.](https://dev.epicgames.com/community/api/documentation/image/82d8d3c7-3c68-4e52-a126-06a9f774a8d6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/82d8d3c7-3c68-4e52-a126-06a9f774a8d6?resizing_type=fit)



 |

For more information on these editor modes, see [Level Editor Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-modes-in-unreal-engine).

### Asset Editors

Individual **Asset Editors** use a viewport toolbar adapted to their editors and functionality within. 

In this example, you can see a comparison of the legacy viewport toolbar to the improved viewport toolbar.

[![Legacy editor under current toolbar for comparison.](https://dev.epicgames.com/community/api/documentation/image/b360a888-6082-4c24-8259-82f6c5b092b0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b360a888-6082-4c24-8259-82f6c5b092b0?resizing_type=fit)

Below are examples of the different viewport toolbars you’ll see in different editors:

| Viewport Toolbar Location | Viewport Toolbar Representation |
| --- | --- |
| 
**Level Editor Selection Mode**

 | 

[![Level editor selection mode toolbar layout.](https://dev.epicgames.com/community/api/documentation/image/2d7724a0-88d3-4ec5-8e9e-0e1dea575479?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2d7724a0-88d3-4ec5-8e9e-0e1dea575479?resizing_type=fit)



 |
| 

**Static Mesh Editor**

 | 

[![Static mesh editor toolbar layout.](https://dev.epicgames.com/community/api/documentation/image/f305a46b-a887-4e5d-bf6e-2275323e4905?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f305a46b-a887-4e5d-bf6e-2275323e4905?resizing_type=fit)



 |
| 

**Material / Material Instance Editor**

 | 

[![Material instance editor toolbar layout.](https://dev.epicgames.com/community/api/documentation/image/87e81354-6902-40fa-8917-e3f573f1b96b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/87e81354-6902-40fa-8917-e3f573f1b96b?resizing_type=fit)



 |

### Asset Editor Preview Scene Settings

**Asset Editor** viewports use a preview scene to display their assets. This scene can give you an idea of how that asset will look in a lit environment. You can change properties of the scene using the **Preview Scene Settings**. 

You can access a portion of these settings from the viewport toolbar by clicking its menu.

[![Asset editor preview scene menu settings.](https://dev.epicgames.com/community/api/documentation/image/93b2c78b-9c28-405a-991b-759288e999ea?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/93b2c78b-9c28-405a-991b-759288e999ea?resizing_type=fit)

If you want to make additional changes to the scene in the viewport, select Preview Scene Settings from this menu to open the Preview Scene Settings panel, where you’ll have access to additional lighting, post process, and scene options.

[![The preview scene settings panel for more options.](https://dev.epicgames.com/community/api/documentation/image/2f818a57-040c-4815-afb3-243e070c92da?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2f818a57-040c-4815-afb3-243e070c92da?resizing_type=fit)

### Materials and Material Instances Viewport Toolbars

The **Material** and **Material Instance** editors display a limited viewport toolbar. Since these editors are previewing a material and how it renders on an object within an environment, viewport controls found in other editors simply aren’t necessary here.

[![Materials options icons on the toolbar.](https://dev.epicgames.com/community/api/documentation/image/ed6f986c-88ab-4124-b145-c6c7177e913f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ed6f986c-88ab-4124-b145-c6c7177e913f?resizing_type=fit)

The notable difference between these editors and others is that **Preview Mesh** options are included in the viewport toolbar. You can choose one of the provided shapes, or select a custom mesh from the **Content Browser** to preview the material.