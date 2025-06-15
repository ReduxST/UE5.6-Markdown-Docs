# Landscape Splines

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-splines-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-splines-in-unreal-engine)  
**Processed:** 2025-06-14 16:32:38

---

**Landscape Splines** are a flexible system for creating any linear feature that needs to conform to a Landscape, and can even push and pull the terrain to better facilitate building these features. They are created and edited using the spline tool in the Landscape tool.

The Spline tool is best used to make streets or paths in the environment, but in general, it can be used for any mesh that must conform to the terrain, such as cobblestone walls or long straight rows of corn.

## Creating a Spline

1.  Under the **Manage** tab, select **Splines**.
    
    ![Spline Tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54751bd4-6115-4e32-8163-bcfbed810bd7/landscape_splinetool.png "Spline Tool")
2.  Press **Ctrl + Left-click** to set your spline's first control point. The control point's sprite looks like a sculpted, Landscape mountain.
    
    ![A Spline control point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3a0aa523-33f7-4a3b-aa79-8e1f3ecf247f/control_point.jpg)
3.  Press **Ctrl + Left-click** again to create another control point and connect it to the first point by a spline segment. The selection changes to the new control point so that you can repeat this action and add more control points.
    
    ![A second spline control point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c19942c-5822-4afa-8b4b-94d7e2fa9e7f/short_spline.jpg "A second spline control point")
    
    Alternatively, you can use **ALT + Left Mouse Button (LMB) Drag** to create a new spline control point and segment. Select an existing control point and **ALT+LMB Drag** in the direction you want to place the new point. If you select the point at either end of the spline, **ALT+LMB Drag** adds a new segment and extends the spline. As you drag the point, you will see what the new segment will look like in the viewport.
    

### Joining and Splitting Splines

To join two splines, select one spline and then **Ctrl + Left-click** on the other.

To split a spline, press **Ctrl + Left-click** on a segment. This splits the segment at that point and inserts a new control point.

In addition to **Ctrl + Left-click**, you can use **ALT+LMB Drag** to split a spline. Select a spline point on either side of the segment and **ALT+LMB Drag** the cursor towards an existing segment to split the path.  
If **Use Auto Rotate Control Point** is enabled, after you release the cursor, the spline point auto-rotates to maintain a smooth spline.

![Enabling Auto Rotate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c6243a5-6fa1-42f9-82cb-325eac4ae4d5/enable_autorotate.png)

### Adding a Static Mesh Actor to a Spline

1.  In the **Content Browser**, find and select the Static Mesh asset that you want to use with your spline.
    
2.  Click on a spline control point on your Landscape.
    
3.  In the Level Editor's **Details** panel, in the **Landscape Spline** section, next to **Select all connected**, click the **Segments** button. This ensures that the Static Mesh is added to all the spline's segments.
    
    ![All Segments button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ea44172-0789-40ea-9fb2-fa1ae8d23e51/landscape_splineallsegments.png)
4.  In the **Landscape Spline Meshes** section, under **Spline Meshes**, if there is no element, click the plus icon (![Plus Sign](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ca85873-0b9a-4c2f-982e-3785d5ca254a/04-plus-sign.png "Plus Sign")) to add one.
    
    ![Add Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2afe0b0b-a66c-4954-a64f-64254c7da733/landscape_splinemeshadd.png)
5.  Expand the element you just added. Next to **Mesh**, click the Assign arrow icon (![Assign](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c56b2a4-3202-4758-a148-5974df78feb9/icon_assign_left_16x.png)) to assign the selected Static Mesh.
    
    ![Mesh Added](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d8916d8-6298-4f0d-895c-2c74b8566ab6/landscape_splinemeshadded.png)

You can also assign a Static Mesh to an individual control point by selecting that control point and assigning the Static Mesh in the **Details** panel, in the **Mesh** section.

## Editing a Spline

Spline control points respond as you would expect to the translation and rotation tools, but the scale tool brings up a different tool, spline tangents.

![Segment tangent scale tool](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46967d6e-afb9-4328-bd8a-3db290d8ee10/segment_scale.jpg)

If a segment is selected, it shows the tangents at each end of the segment, and if a control point is selected, it shows the tangents of all connected segments. You can adjust the scale of the tangent by dragging the end of it, which alters how curved the segment of spline is.

## Applying Splines to the Landscape

The **Apply Splines to Landscape** button modifies the Landscape heightmap and layer weightmaps with the spline information. The heightmap is raised or lowered to fit the spline, with a smooth cosine-blended falloff on either side. This is controlled by the width and falloff properties of the spline control points, and the **Raise/Lower Terrain** option on the individual spline segments. The Texture layer that is painted (if any) is specified in the **Layer Name** property of the individual spline segments, and the painting is affected by the spline width and falloff settings in the control points.

## Spline Properties

The properties of the selected control points or segments are displayed in the Level Editor's **Details** panel.

### Control Point Properties

| Property | Description |
| --- | --- |
| **Location** | Position of the control point relative to the Landscape. |
| **Rotation** | Rotation of the control point, and controls the direction of the tangent of any attached spline segments. |
| **Width** | Width of the spline, and shown as solid lines. Affects all connected segments. |
| **Side Falloff** | The width of the cosine-blended falloff region on either side of the spline, and shown as dotted lines. |
| **End Falloff** | Control point at the end of a spline with only one attached segment. The length of the cosine-blended falloff region smoothly ends the spline segment. |
| **Layer Name** | Name of the painted blendmask layer when applying the spline to the Landscape. |
| **Raise Terrain** | Raises the Landscape to match spline when applying the spline to the Landscape. Good for roads on embankments. |
| **Lower Terrain** | Lowers the Landscape to match spline when applying the spline to the Landscape. Good for rivers and ditches. |

### Spline Segment Properties

#### Landscape Spline Segment

| Property | Description |   |
| --- | --- | --- |
| **Connections** | Settings specific to the two control points attached to the segment. | 
**Connections Sub-Properties**:

-   **Tangent Len**: Scale of the tangent at this point, and controls the segment curve. Negative tangents cause the segment to connect to the back of the control point.
-   **Socket Name**: Overrides the Static Mesh's assigned Material with a different Material for the spline.



 |
| **Layer Name** | Name of the painted blendmask layer when applying the spline to the Landscape. |   |
| **Raise Terrain** | Raises the Landscape to match spline when applying the spline to the Landscape. Good for roads on embankments. |   |
| **Lower Terrain** | Lowers the Landscape to match spline when applying the spline to the Landscape. Good for rivers and ditches. |   |

#### Landscape Spline Meshes

| Property | Description |   |
| --- | --- | --- |
| **Spline Meshes** | The meshes applied to the spline. Multiple meshes will be applied in random order controlled by the random seed. | 
**Spline Meshes Sub-Properties (per mesh used)**:

-   **Mesh**: The Static Mesh applied to the spline.
-   **Material Overrides**: Socket on the control point connected to the end of the segment.
-   **Center H**: Determines whether to horizontally center the mesh on the spline or use the mesh's origin.
-   **Offset**: Offsets the mesh from the spline (units are in mesh-space, unscaled by the spline).
-   **Scale to Width**: Determines whether to scale the mesh to fit the spline width or to use the mesh as-is.
-   **Scale**: Multiplier to the size of the mesh. If **Scale to Width** is enabled, the **Scale** specified here is relative to the spline width. Otherwise, it is relative to the mesh's natural size.
-   **Forward Axis**: Chooses the forward axis of the **Spline Mesh**.
-   **Up Axis**: Chooses the Up axis of the **Spline Mesh**.



 |
| **Collision Profile Name** | Name of the Collision Profile to use with this spline. |   |
| **Cast Shadow** | Enables the casting of shadows by the mesh. |   |
| **Random Seed** | Controls the application order of multiple spline meshes to the spline. |   |
| **Max Draw Distance** | Max Draw Distance for all the meshes used in the spline. |   |
| **Translucency Sort Priority** | Sets the sort priority of translucent objects. Ignore if your meshes are not translucent. The default priority is zero. |   |
| **Hidden in Game** | Hides the Static Meshes in game. |   |
| **Place Spline Meshes in Streaming Levels** | Determines whether spline meshes should be placed in Landscape proxy streaming levels or the spline's level. Default is True. |   |

## Controls Reference

| Controls | Operation |
| --- | --- |
| **Left Mouse Button** | Selects a control point or segment. |
| **Shift + Left Mouse Button (LMB)** | Selects multiple control points or segments. |
| **Ctrl + A** | Selects all control points connected to the currently selected control points and/or all segments connected to the currently selected segment. |
| **Ctrl + LMB** | 
-   Adds a new control point, and automatically connects to any selected control points.
-   With a control point or multiple control points selected, creates a segment joining any selected control points to the new control point.
-   With a segment selected, splits the segment at that point and inserts a new control point.



 |
| **ALT + LMB Drag** | 

-   With a control point selected, adds a new control point and translates it in the direction of the drag.
-   Splits the path when dragged through an existing segment.
-   Adds a new segment when dragged away from either end of the spline.



 |
| **Del** | Deletes the selected control points or segments. |
| **R** | Automatically calculate rotation for selected spline control points. |
| **T** | Automatically flip the tangents for the selected control points / segments. |
| **F** | Flips selected spline segments (only affects meshes on the spline). |
| **End** | Snaps the selected control points to the Landscape below. |