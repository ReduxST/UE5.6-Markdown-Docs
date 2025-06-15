# Transforming Actors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:56

---

**Transforming** an Actor in **Unreal Engine** refers to moving, rotating, or scaling it (in other words, adjusting the position, orientation, and / or size of the Actor). This page describes how to perform each of these actions, as well as some of the commonly used keyboard shortcuts when working with Actors.

There are two ways to transform Actors in the Unreal Editor:

-   Manual transformation
    
-   Interactive transformation
    

In Unreal Engine, the vertical axis is the **Z axis**.

## Manual Transformation

You can do **manual transformation** through the Transform section of the **Details** panel. When you select one or more Actors in the **Level Viewport**, you can view and edit their **Location**, **Rotation**, and **Scale** in this section. Where applicable, this section also contains [Actor mobility](/documentation/en-us/unreal-engine/actor-mobility-in-unreal-engine) settings.

![Transform section in the Unreal Enigne](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8524a90d-dc0c-414e-89e9-825d4f235c78/details-panel-transform.png)

The Transform section of an Actor's Details panel, showing values for the Actor's Location, Rotation, and Scale.

Each **Transform** property has numeric entry fields for the X, Y, and Z axes. You can type specific values directly into these fields to adjust the selected Actors, or click inside a field and drag your mouse up or down to adjust that field's value.

If more than one Actor is selected, and their Location or Rotation has multiple values, the relevant fields will display *Multiple Values*. In this case, if you enter a number it will overwrite that value for all selected Actors. Note that this may cause the Actors to overlap.

![Multiple values in the Transform section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b46c85b5-f27e-4ae4-ade2-ba3714a0eaca/transform-multiple-values.png)

With multiple Actors selected, one or more Transform fields can have multiple values, as this example illustrates.

To reset an Actor's **Location**, **Rotation**, or **Scale** to their default values after you've made changes, click the **Reset to Default** button ( ![Reset to Default button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3790987d-fb31-44f5-a96b-2412ca389319/reset-to-default.png)).

You can lock the **Scale** fields by clicking the **Lock Scale** button ( ![Lock Scale button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87d95ead-53f2-4392-bac1-3007f1e3778f/lock-scale.png)). When locked, the values for each axis (X, Y, and Z) change in unison, which allows for uniform scaling and prevents distortion.

Transform properties default to *relative* coordinate space, which means the transform occurs relative to the Actor's parent. You can toggle between *relative* and *world* transforms by clicking the dropdown arrow next to a property label. *World* transforms occur relative to world coordinates instead of the Actor's parent. For more information, see the **World and Local Transformation Modes** section on this page.

## Interactive Transformation

You can do **Interactive transformation** directly inside the **Level Viewport**, using a visual tool called a **gizmo**. Sometimes, a gizmo can also be called a **widget**; in Unreal Engine, these terms mean the same thing.

A gizmo is made up of several parts that are color-coded according to which axis they affect:

-   Red represents the X axis.
    
-   Green represents the Y axis.
    
-   Blue represents the Z axis.
    

You can use transformation gizmos to move, rotate, or scale Actors.

Gizmos are more intuitive to use, but they can be less precise than entering coordinates manually. Use **grid snapping** for precise positioning when using gizmos. For more information, refer to the [Actor Snapping](/documentation/en-us/unreal-engine/actor-snapping-in-unreal-engine) page.

The gizmo takes different forms depending on what type of transformation is being performed: translation, rotation, or scale. You can choose which type of gizmo you want to use by clicking its icon in the **Level Viewport** toolbar, which is located in the upper-right section of the viewport, or by using keyboard shortcuts.

The Level Viewport toolbar is located in the upper-right section of the viewport. Click the image for full size.

![Shortcuts to transformation gizmos on the Level Viewport toolbar.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/457d98ac-1442-4a86-9256-1b1eb49f575c/viewport-toolbar-gizmos.png)

Left to right: Shortcuts to the Selection, Translation, Rotation, and Scaling gizmos in the Level Viewport toolbar.

With one or more Actors selected, you can toggle between the different types of gizmos by pressing the **Space Bar** on your keyboard.

You can toggle the visibility of transformation gizmos on and off from the Main Toolbar's **Settings** menu by enabling or disabling the **Show Transform Widget** option.

### Translation Gizmo

The **Translation** gizmo is a set of color-coded arrows pointing down the positive direction of each axis in the world. Use it to move an Actor along an axis, a plane, or freely.

Click an arrow and drag an arrow to move the selected Actor along that axis.

![Translating a cube along a single axis.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f5ff669-dcf8-4926-ac6a-fdfdcc713660/translate-single-axis.gif)

Translating a cube along a single axis.

To move an Actor along two axes simultaneously, click the square at the point where the two axes meet, then drag to move the Actor along the plane defined by the two axes (XY, XZ, or YZ).

![Translating a cube along a single plane.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c55343a3-f8e0-424b-b292-2d63bff48e70/translate-two-axes.gif)

Translating a cube along two axes (a single plane).

To move the Actor freely along all three axes, click and drag the white sphere at the point where all three axes intersect. You can also use the mouse wheel to move the Actor nearer or farther.

![Translating a cube along all three axes.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60505490-defe-4e74-8893-8ce0762d8427/translate-three-axes.gif)

Translating a cube along all three axes.

#### Duplicating an Actor Using the Translation Gizmo

To duplicate an Actor, hold down the **Alt** key, then click and drag a Translation gizmo arrow. This creates and moves a duplicate of the selected Actor, leaving the original unchanged at the starting position.

![Duplicating an Actor using the Translation gizmo.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8073589b-ef27-4175-9735-7fd1d7a0af2c/duplicate-actor.gif)

Duplicating an Actor using the Translation gizmo.

### Rotation Gizmo

The **Rotation** gizmo is a set of three color-coded arcs, each associated with one axis. When you drag one of the arcs, the selected Actor rotates around that axis. For this gizmo, the axis affected by any one of the arcs involved is the one perpendicular to the arc. For example, the arc aligned to the XY plane rotates the Actor around the Z axis.

![Rotating an Actor using the Rotation gizmo.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7eda8aa-301c-4b36-b9a8-47c9112db44b/rotate-actor.gif)

Rotating an Actor using the Rotation gizmo.

When you hover the cursor over a particular arc, that arc turns yellow, indicating that you can drag it to rotate the Actor. When you start to rotate the Actor, the gizmo changes shape to show only the axis around which the Actor is being rotated. The amount of rotation is displayed in real time to help you gauge your progress.

### Scale Gizmo

The **Scale** gizmo has handles that end in cubes. When you drag the gizmo by one of these handles, you scale the selected Actor only along the associated axis. The handles are color-coded by axis, similar to the **Translation** and **Rotation** gizmos.

![Scaling an Actor along a single axis.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61513a36-e159-448a-92a9-9ebf4f264859/scale-single-axis.gif)

Scaling an Actor along a single axis.

You can scale an Actor along two axes simultaneously in the same way you can use the **Translation** gizmo to move an Actor along a plane defined by two axes. Each axis is connected to each other axis with a line that forms a triangle. These triangles align with one of the three planes (XY, XZ, YZ). Dragging one of these triangles scales the Actor along both axes that define that plane. When the mouse hovers over one of these triangles, the associated handles turn yellow.

![Scaling an Actor along a single plane.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24921d68-c0d4-4fd2-b734-c5ab38139f63/scale-two-axes.gif)

Scaling an Actor along a single plane.

You can also scale an Actor along all three axes, thus maintaining its original proportions. If you hover the cursor over the cube where all three axes meet, all three handles turn yellow. Dragging by that center cube scales the Actor proportionally.

![Scaling an Actor proportionally.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/133d1241-6b3d-4303-8557-bfadc2f771e8/scale-three-axes.gif)

Scaling an Actor proportionally.

### World and Local Transformation Modes

When using the interactive transformation method, you can choose which reference coordinate system you want to use when performing the transformation. This means you can transform the Actor in accordance to either:

-   World space - that is, along the world axes, or
    
-   The Actor's local space - that is, along its local axes.
    

The example below shows the difference between world and local space, using a Static Mesh Actor.

|   |   |
| --- | --- |
| 
![Example transform in world coordinates](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d52d8265-c407-496c-9079-cded348f8281/coordinates-world-space.gif)

 | 

![Example transform in local coordinates](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8e1994b-e70e-482b-a4d3-f2b25ec29437/coordinates-local-space.gif)

 |
| World space: The translation gizmo's XYZ axes are the same as the world's XYZ axes. Dragging along the Z axis moves the cube up and down in relation to the floor. | Local space: The translation gizmo's XYZ axes use the cube's local coordinates. Dragging along the Z axis also moves the cube up and down, but at an angle. |

By default, the Unreal Editor starts out in world transformation mode. To switch to local transformation mode, click the **Globe** icon in the **Level Viewport** toolbar. The globe turns into a cube icon, indicating that you are now in local transformation mode. Click the cube to switch back to world coordinates.

![World / Local Coordinates toggle in the Level Viewport toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c47274b-35fc-49d7-be04-4f85b8556ae7/viewport-toolbar-coordinates.png)

The Globe icon indicates that transformations for the currently selected Actor use world space coordinates.

## Adjusting an Actor's Pivot Point

When transforming Actors, you typically perform your transforms from the base pivot of the Actor. If you have a transformation gizmo enabled, you can see the **pivot point** where the three axes of that gizmo intersect.

You can adjust the location of an Actor's pivot temporarily by middle-clicking on the sphere in the center point of the **Translation** gizmo and dragging to move the pivot. You can then transform the object around the new pivot point.

The pivot point can be inside or outside an Actor.

![Rotating an Actor around an external pivot point.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a1388bc-746c-4c51-a46c-92e95a07748b/external-pivot-point.gif)

In this example, the Static Mesh Actor rotates around an external pivot point.

The pivot jumps back to its original location as soon as you deselect that Actor. To make the pivot change permanent, after you adjust the pivot, right-click the Static Mesh and select **Pivot > Set as Pivot Offset**.

To reset the pivot to its default location, right-click the Static Mesh, then select **Pivot > Reset Pivot Offset**.

## Keyboard Shortcuts

Below are some of the common keyboard shortcuts when working with Actors.

| **Control** | **Tool or Action** |
| --- | --- |
| **W** | Selects the Move tool. |
| **E** | Selects the Rotate tool. |
| **R** | Selects the Scale tool. |
| **V** (hold down while using a translation gizmo) | Toggles vertex snapping. |
| **Left-click and drag** (on a transformation gizmo) | Moves, rotates, or scales the selected Actor, depending on the transformation gizmo that is currently active. |
| **Middle-click and drag** (on a pivot point) | Moves the pivot of the selected Actor. |
| **Ctrl + W** (on an Actor) | Duplicates the selected Actor at the same coordinates as the original. |
| **Alt + Left-click and drag** (on a translation gizmo) | Duplicates the selected Actor. |
| **H** (on an Actor) | Hides the selected Actor. |
| **Ctrl + H** | Shows all hidden Actors. |
| **Shift + E** (on a mesh Actor) | Selects all Actors with the same Static Mesh as the selected Actor. |
| **Ctrl + Left-click** (on an Actor) | Adds the Actor to the current selection of Actors. |