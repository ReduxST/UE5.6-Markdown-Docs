# Coordinate System and Spaces

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/coordinate-system-and-spaces-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/coordinate-system-and-spaces-in-unreal-engine)  
**Processed:** 2025-06-14 16:16:19

---

## Coordinate System

Unreal Engine (UE) uses the [Cartesian coordinate system](https://en.wikipedia.org/wiki/Cartesian_coordinate_system) to represent positions in three-dimensional [Euclidean space](https://en.wikipedia.org/wiki/Euclidean_space). In the Unreal Editor the coordinate system is left-handed and uses a Z-up axis. Points are determined by their position along three coordinate axes: the X-axis, Y-axis, and Z-axis. These coordinate values set the position of actors and the direction they face for your project. There are a variety of different ways that these axes can be oriented in relation to one another. The orientation and values of the axes depend on the type of coordinate space you are in.

If you are importing assets from other software such as Maya, Houdini, ZBrush, Blender, or 3ds Max, you must be aware of the handedness and orientation of the coordinate system used in Unreal Engine. Other software systems use different up-axes and handedness that you might need to take into consideration.

*Three-dimensional cartesian coordinate system with the origin and coordinate axes.*

### Axes

In the Unreal Editor, and all illustrations in this documentation section, the following colors are associated with the coordinate axes:

-   X-axis: Red
    
-   Y-axis: Green
    
-   Z-axis: Blue
    

UE's Z-up, left-handed coordinate system is defined as follows:

-   The Z-axis determines how far up and down along a vertical line an actor is located.
    
    -   Positive values are upwards.
        
-   The Y-axis determines how far to the left or right an actor is located.
    
    -   Positive values are to the right.
        
-   The X-axis determines how far forward or backward an actor is located.
    
    -   Positive values are forward.
        

There is a special point in the coordinate system known as the origin. The origin is where the coordinate axes intersect and is represented by the point with coordinates (0, 0, 0). To learn more about the origin and how it's used to set a point's location, see the gif above and this page's [Coordinate Space](https://dev.epicgames.com/documentation/en-us/unreal-engine/coordinate-system-and-spaces-in-unreal-engine) section.

You can use the Orthographic Viewports to visualize the direction of the axes and set coordinate values. To learn more, see [Using Editor Viewports](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine).

|   |   |   |   |
| --- | --- | --- | --- |
| 
[![View Perspective](https://dev.epicgames.com/community/api/documentation/image/98f57112-38d2-443a-9feb-d3e024df2a8a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/98f57112-38d2-443a-9feb-d3e024df2a8a?resizing_type=fit)



 | 

[![View Front](https://dev.epicgames.com/community/api/documentation/image/2dd463a2-2a21-46e9-8de8-46fa9edf8d64?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2dd463a2-2a21-46e9-8de8-46fa9edf8d64?resizing_type=fit)



 | 

[![View Side](https://dev.epicgames.com/community/api/documentation/image/2a0c1d0a-8377-495c-a2af-cf9d05ff91e2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2a0c1d0a-8377-495c-a2af-cf9d05ff91e2?resizing_type=fit)



 | 

[![View Top](https://dev.epicgames.com/community/api/documentation/image/6de1f391-7d77-45fe-b759-a26f5357c3bd?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6de1f391-7d77-45fe-b759-a26f5357c3bd?resizing_type=fit)



 |
| 

Perspective (3D)

 | 

Front (X-Axis)

 | 

Side (Y-Axis)

 | 

Top (Z-Axis)

 |

UE is referred to as a left-handed coordinate system because the cross product and the coordinate axes follow the left-hand rule and Z-up because positive values along the Z-axis are located in the upward direction.

To illustrate, you could point your left index finger in the direction of the positive X-axis. Then point your left middle finger in the direction of the positive Y-axis. Now, the positive Z-axis points in the direction of your thumb. The following image shows what this looks like:

[![Left Hand Rule](https://dev.epicgames.com/community/api/documentation/image/e0210fee-8b01-478b-82ca-1a49556c1778?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e0210fee-8b01-478b-82ca-1a49556c1778?resizing_type=fit)

Visualization of Left Hand Rule

*Left-hand rule for the cross product of vectors.*

The three coordinate-axes are also sometimes referred to as the:

-   X-axis: abscissa
    
-   Y-axis: ordinate
    
-   Z-axis: applicate
    

To locate the point (2, 1, -3) in UE coordinate space, follow these steps:

-   Measure 2 unit steps along the positive X-axis.
    
-   Measure 1 unit step along the positive Y-axis.
    
-   Measure 3 unit steps along the negative Z-axis.
    

The following video illustrates this process step-by-step:

-   Travel 2 units forward in the positive X direction.
    
-   Travel 1 unit right in the positive Y direction.
    
-   Travel 3 units down in the negative Z direction.
    

For more information about units in UE, see the [Units of Measurement](https://dev.epicgames.com/documentation/en-us/unreal-engine/units-of-measurement-in-unreal-engine) documentation.

*Steps to locate the point (2, 1, -3) in Unreal's coordinate system.*

### Transform and Control Axes

The following image is a scene from the Third Person Template included with Unreal Engine. The selected object in the center of the scene is located at the origin of world space. In the lower left-hand corner of the Viewports in the Unreal Editor is a gizmo icon depicting the positive direction of the axes relative to the direction you are viewing. You can use this to visualize the coordinate system in Unreal Engine.

[![World Space Origin](https://dev.epicgames.com/community/api/documentation/image/116100d2-2c12-44e1-8a7d-491e1a4c3fad?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/116100d2-2c12-44e1-8a7d-491e1a4c3fad?resizing_type=fit)

World Space Origin

*Unreal Engine scene with gizmo indicating an object's position in world space.*

The transformation gizmo in the center of the scene is positioned with the same orientation as the gizmo icon in the bottom-left corner of the Viewport. The matching orientation is because you are viewing the selected actor in world space. In addition, the transformation controls in the editor are color-coordinated to match the axes.

|   |   |   |
| --- | --- | --- |
| 
[![Trans Widget](https://dev.epicgames.com/community/api/documentation/image/840c51a3-95bd-4248-a653-83e077c452f0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/840c51a3-95bd-4248-a653-83e077c452f0?resizing_type=fit)



 | 

[![Transform Rotate](https://dev.epicgames.com/community/api/documentation/image/7a46e7ac-5809-45f9-8d35-cbc5e628ecac?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7a46e7ac-5809-45f9-8d35-cbc5e628ecac?resizing_type=fit)



 | 

[![Trans Scale Widget](https://dev.epicgames.com/community/api/documentation/image/02d19911-4eec-49be-95fd-1d496264c0d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/02d19911-4eec-49be-95fd-1d496264c0d5?resizing_type=fit)



 |
| 

Move Tool (W)

 | 

Rotate Tool (E)

 | 

Scale Tool (R)

 |

The image above represents the common transform gizmos in the Level Editor. However, additional specialized gizmos exist in the various editors and level modes.

To learn more about using the various controls for adjusting the position of actors, including the pivot point, see [Transforming Actors](https://dev.epicgames.com/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine).

### More Information

For more information about coordinate systems, see the following resources:

-   [Wolfram MathWorld - Coordinate System](https://mathworld.wolfram.com/CoordinateSystem.html)
    
-   [Wikipedia - Coordinate System](https://en.wikipedia.org/wiki/Coordinate_system)
    

## Coordinate Spaces

Each coordinate space has its own coordinate system and origin. The intersection of the axes equals the origin point of that particular coordinate space, which is represented by the coordinates (0,0,0) within that coordinate space's coordinate system. The values of the axes increase or decrease based on the origin and direction of the transformation.

### World Space

**World space** is the coordinate system used for your entire level. Its origin is the center of the scene (the world grid). This coordinate system is fixed - you cannot transform it. Use world space to translate or rotate an object in absolute units relative to the level's origin and scale relative to the entire level.

The image below shows what happens when you select the blue cube. The coordinate axis gizmo is now located at the pivot point of the cube. The coordinate axes of the gizmo are still pointing in the same direction as the coordinate axes for world space. You can see this in two different ways.

-   One way is by noticing that the coordinate axes of the gizmo centered on the blue cube point in the same directions as the coordinate axes in the lower left-hand corner.
    
-   Another, simpler way is the globe icon near the top-right corner of the Viewport indicates that you are viewing this object with respect to world space.
    

[![World Space Cube](https://dev.epicgames.com/community/api/documentation/image/5abdb047-6fb8-4373-9809-14dd9629ed3b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5abdb047-6fb8-4373-9809-14dd9629ed3b?resizing_type=fit)

World Space centered on Cube

*View the blue cube with respect to world space.*

### Local Space

**Local space** is the coordinate system relative to the [scene component](https://dev.epicgames.com/documentation/en-us/unreal-engine/components-in-unreal-engine) to which the actor is attached. The space is also known as object space. Every actor has a local space coordinate system within a scene relative to the actor's pivot point. An actor's pivot point is where the three local coordinate axes for the actor intersect and represent the origin of local space. Use local space to translate or rotate an object relative to its parent.

|   |   |
| --- | --- |
| 
World Space

 | 

Local Space

 |
|  |  |
| 

Transform tools align to the world grid.

 | 

Transform tools align to the rotation of the selected actor.

 |

If you click on the globe icon in the upper right corner, the gizmo centered on the blue cube changes, and the globe icon changes to a cube icon with axes. This icon indicates that you are viewing the object with respect to local space. Now, the X- and Y- coordinate axes of the gizmo centered on the blue cube do not point in the same directions as those in the lower left-hand corner.

[![Local Space Cube](https://dev.epicgames.com/community/api/documentation/image/549fd7fc-6eac-4710-abbd-08bcda7fa8bc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/549fd7fc-6eac-4710-abbd-08bcda7fa8bc?resizing_type=fit)

Local Space centered on Cube

*View the blue cube with respect to local space.*

To temporarily change the location of an actor's pivot, choose from the following:

-   **Middle-click** on the sphere in the center point of the translation gizmo and drag to move the pivot.
    
-   Hover the cursor over where you want to set the pivot point on an actor and use the shortcut **ALT + MMB** (Middle Mouse Button).
    

You can permanently change the pivot point from the following:

-   Perform one of the actions above and then right-click the actor and select **Pivot > Set as Pivot Offset**.
    
-   The [Edit Pivot tool](https://dev.epicgames.com/documentation/en-us/unreal-engine/edit-pivot-tool-in-unreal-engine).
    

To learn more about adjusting pivot points, see [Transforming Actors](https://dev.epicgames.com/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine).

### Screen Space

**Screen space** is the projection of the three-dimensional world space onto the two-dimensional screen that constitutes the player's vision. You can pull screen space coordinates from specific cameras in your scene.

[![Screen Space](https://dev.epicgames.com/community/api/documentation/image/e592df61-56a4-44a1-8b34-67289ca54d05?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e592df61-56a4-44a1-8b34-67289ca54d05?resizing_type=fit)

Actor within Screen Space

*Play in Editor (PIE) session of the Third Person Template*

To help visualize the placement of actors in screen space, pilot the cameras or pawns in your scene. To pilot, right-click the object and select **Pilot**.

### UV Space

UVs are a parameterization (U,V) of a 3D surface mesh into a normalized (0-1) 2D space. In other words, they represent coordinates in 2D space that translate to vertices on your 3D model. The space is represented horizontally as U and vertically as V, thus the name UV coordinates. Also known as 2D or texture coordinates.

The **2D Viewport** of the [UV Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine) (pictured below) represents the UV space for displaying your UV map. It is the primary Viewport for unwrapping and packing UVs. The space is also known as 2D or texture space.

[![UV Space](https://dev.epicgames.com/community/api/documentation/image/9bbda4cf-f315-4be6-a4f7-89fc3305da93?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9bbda4cf-f315-4be6-a4f7-89fc3305da93?resizing_type=fit)

### Instance and Particle Space

**Instance and particle space** is the coordinate system relative to an [instanced static mesh (ISM) component](https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine) or [particle emitter](https://dev.epicgames.com/documentation/en-us/unreal-engine/key-concepts-in-niagara-effects-for-unreal-engine) to which a mesh is attached. Essentially, this coordinate system provides per instance transform.

In the video, the ISM component consists of mesh instances (copies) of the cube asset. The component transforms all instances as one based on the actor's pivot point. When the component is double-clicked, the pivot point moves to the selected instance.

The following applies when using the **Transform** or **TransformPosition** material nodes to convert positions or vectors of mesh instances or particle meshes.

-   **Local Space** refers to the coordinate system for the instanced static mesh component or particle emitter.
    
-   **Instance and Particle Space** refers to the coordinate system for the individual instance or particle. You can convert each instance's transformation from instance and particle space to local space.
    

The instance and particle space for non-mesh particles (Niagara and Cascade) is the same as local space.

To learn more about these material nodes, see [Vector Operation Material Expressions](https://dev.epicgames.com/documentation/en-us/unreal-engine/vector-material-expressions-in-unreal-engine).