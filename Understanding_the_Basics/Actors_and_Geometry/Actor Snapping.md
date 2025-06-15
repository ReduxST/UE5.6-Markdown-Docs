# Actor Snapping

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-snapping-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/actor-snapping-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:37

---

**Snapping** is a feature that allows you to easily position an Actor by aligning it with a grid or another object. When snapping is enabled, the Actor will jump to fixed positions when transformed.

**Unreal Engine** implements snapping in several different ways:

-   Surface snapping
    
-   Grid snapping
    
-   Vertex snapping
    

## Surface Snapping

**Surface snapping** makes Actors align to the floor or another surface. Enable surface snapping from the **Level Viewport** toolbar: click the **Surface Snapping** button, then enable the **Surface Snapping** option.

Click image for full size.

Surface Snapping button and options in the Level Viewport toolbar.

After you enable surface snapping, you can also set the following options:

| Option | Description |
| --- | --- |
| **Rotate to Surface Normal** | If enabled, Actors will automatically rotate to match the alignment of the surface they snap to. |
| **Surface Offset** | Modify this value to configure the distance between the Actor and the surface it snaps to. |

If you select an Actor and press the **End** key, the Actor snaps to the nearest surface - for example, your Level's floor plane.

## Grid Snapping

When **grid snapping** is enabled in Unreal Engine, an Actor will move, rotate, or scale in increments of a specific value. For example, if your translation snapping value is set at 10 units, you can only move Actors in 10 unit increments.

Unreal Engine uses a separate grid for each transformation:

-   The **Drag Grid** allows for snapping to a 3-dimensional implicit grid within the Level.
    
-   The **Rotation Grid** provides for incremental rotation snaps.
    
-   The **Scale Grid** forces the Scale gizmo to snap to additive increments, but can be set to percentage values in the Editor Preferences (see the Snapping Preferences section below).
    

|   |   |   |
| --- | --- | --- |
| 
Click image for full size.



 | 

Click image for full size.



 | 

Click image for full size.



 |
| Drag Grid | Rotation Grid | Scale Grid |

Each snapping grid is activated by clicking its icon in the **Level Viewport** toolbar. When a grid is active, its icon will be highlighted. You can change each grid's increments from the dropdown to the right of its activation button.

### Snapping Preferences

The settings for the Drag Grid, Rotation Grid, and Scale Grid can all be configured from within the **Editor Preferences** panel, along with additional options for snap behavior. To access these preferences, from the main menu, select **Edit > Editor Preferences > Viewports**, then scroll down to the **Snap** category.

Click image for full size.

Grid Snapping preferences in the Unreal Engine Editor Preferences.

You can set the following options:

| Option | Description |
| --- | --- |
| **User Power of Two Snap Size** | Enable this option to use power of 2 grid settings (1, 2, 4, 8, 16…) instead of decimal grid sizes. |
| **Enable Grid Snapping** | If enabled, Actor location will snap to the grid. This is the same as the toggle button on the Level Viewport toolbar. |
| **Enable Rotation Snapping** | If enabled, Actor rotation will snap to the grid. |
| **Enable Scale Snapping** | If enabled, Actor scale (size) will snap to the grid. |
| **Use Percentage Based Scaling** | Enable this option to use Unreal Engine's legacy multiplicative (percentage) scaling instead of the current additive method. |
| **Enable 2D Layer Snapping** | This enables an additional option in the Level Viewport toolbar you can use to snap objects to a 2D layer if your project requires it. The default layers are Foreground, Default, and Background. You can customize these by clicking Edit Layers from the drop-down. |
| **Decimal Grid Sizes** | Use this array to customize snapping grid sizes. These values display in the Level Viewport's toolbar. |
| **Decimal Grid Intervals** | This setting controls the decimal interval between grid reference lines in orthographic viewports. |
| **Pow 2Grid Sizes** | If you enabled the User Power of Two Snap Size, use this array to customize power-of-2 snapping grid sizes. |
| **Pow 2Grid Intervals** | This setting controls the power-of-2 interval between grid reference lines in orthographic viewports. |
| **Common Rot Grid Sizes** | Use this array to customize the Common rotation grid intervals. These values display in the Level Viewport's toolbar, under the Rotation Grid Snap dropdown. |
| **Divisions Of 360Rot Grid Sizes** | Use this array to customize the Divisions of 360 rotation grid intervals. These values display in the Level Viewport's toolbar, under the Rotation Grid Snap dropdown. |
| **Scaling Grid Sizes** | Use this array to customize scaling grid intervals. These values display in the Level Viewport's toolbar. |

## Vertex Snapping

**Vertex snapping** is a feature you can use to snap one object to another object by using the polygonal vertices of their respective meshes. Vertices are the points where two or more edges meet..

To use vertex snapping, hold down the **V** key while using the translation gizmo. While you hold down the **V** key, as soon as you start moving an object, you will see the polygon vertices you can snap that object to. This is especially useful when used in conjunction with pivot adjustment: you can snap the pivot directly to a vertex, then use that as a means to snap the object to a vertex on another object.

The video below demonstrates how to snap two pipes together precisely using this technique. Note also where the two Static Meshes' pivot points are located.

This technique is useful for walkways, walls, doors, or any other object that needs to be placed precisely in relation to another object.