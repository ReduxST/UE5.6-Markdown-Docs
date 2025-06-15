# World Position Offset Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/world-position-offset-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-position-offset-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 17:05:09

---

The WorldPositionOffset category contains special functions for applying manipulating vertices of a mesh by using the world position offset input. These functions can be chained together for additive effects.

## SimpleGrassWind

The **SimpleGrassWind** function applies a basic wind operator to foliage, giving the ability to specify a weight map and wind strength. This is a non-directional wind that just gives a very general movement to foliage. This should be the last WPO node you add.

| Inputs | Description |
| --- | --- |
| **WindIntensity (Scalar)** | Controls how much the wind affects the mesh. |
| **WindWeight (Scalar)** | This is a grayscale map that controls how much the mesh's vertices will respond to the wind. |
| **WindSpeed (Scalar)** | This controls the speed of the wind. |
| **AdditionalWPO (Vector3)** | Takes in any additional world position offset networks or functions. |

![SimpleGrassWind](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1208094f-faec-413e-872e-8ffe1f5aece1/simple-grass-wind.png)

This is what the effect looks like in motion.

## SplineThicken

The **SplineThicken** function serves as a way to make very thin polygons look thicker at render time. This is perfect for cables, hair, grass, and other such objects.

Objects using this function should be extremely thin and have a normalized UV layout. Objects should be imported with "Remove Degenerate Triangles" disabled.

| Inputs | Description |
| --- | --- |
| **WidthBase (Scalar)** | This sets the width of a single polygon object at its base. |
| **WidthTip (Scalar)** | Sets the width of a polygon object at its tip. |
| **WorldPosition (Vector3)** | World Position takes in any existing world position offset functions and adds this function to them. |
| **UVs for Projection (Vector2)** | This is the texture coordinate to use in the expansion of the spline. |
| **UVs for Thickness (Vector2)** | This is the texture coordinate to use for the Thickness mapper if projecting from U, it will the Y component of the specified UV index for the thickness blending. |
| **UVs for texturing (Vector2)** | This is the UV channel for texturing. This must be the same UV channel you want to have the 3D-parallax correction. |
| **Expand U or V UV Channel (StaticBool)** | Sets whether to expand the mesh in U or V. Defaults to *true*, which is U. |
| **DriveNormalZ (Boolean)** | This will use DeriveNormalZ to make a perfectly round normal map. |
| **AngleCorrectedNormal (Boolean)** | Uses DerivedNormalZ to make perfectly round normal map. Requires a center tesselation vertex otherwise the value of Z will be 0 for the entire face, causing harsh lighting. |
| **AdditionalNormal (Vector3)** | This will add a texture normal to the normalmap transform. |
| **FlattenPixelNormal (Boolean)** |   |
| **UVs For NormalShading (Vector2)** |   |
| Outputs |   |
| **Normal** | The outgoing normal of the adjusted geometry. |
| **WorldPositionOffset** | This is the output that you can add to other world position offset calculations. |
| **UVs with Parallax** |   |

![Spline Thicken](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8366a711-dfc5-4746-b2d1-2cbd136308ec/spline-thicken.png)

## CameraOffset

The **CameraOffset** function is great to assist with depth sorting, as it allows you to move an object in camera space, either toward or away from the camera.

| Inputs | Description |
| --- | --- |
| **OffsetAmount (Scalar)** | Enter a negative or positive number to offset your model in the direction of the camera. Note that positive values will bring the model closer to the camera and cause rendering errors if the mesh greatly exceeds the models bounding box. |
| **Clamp Padding (Scalar)** | The amount of padding to prevent the clamped version of the offset value from clipping into the camera. |
| **WorldPosition (Vector3)** | Enter the model's vertex world position. The Default Value = World Position. |
| Outputs |   |
| **Clamped Camera Offset** | The Camera offset is clamped to avoid early camera intersections. Adjust the padding to change the amount of space reserved to avoid camera intersection. |
| **Camera Offset** | Either add this value to other World Position offset code or enter it directly into the world position offset master material to offset your mesh. |

![Camera offset graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62d93dfd-1cff-4d6f-b910-0a0cdcdfc4ea/camera-offset.png)

When the Offset parameter in this graph is overidden in the Material Instance Editor, the sphere is moved toward or away from the camera.

## ObjectPivotPoint

The **ObjectPivotPoint** function returns the object's pivot point in world space. This is not compatible with the pixel shader.

| Outputs | Description |
| --- | --- |
| **Object Pivot Location** | Returns the object's pivot point in world space. This only works with the vertex shader and is incompatible with the pixel shader. |

![Object Pivot Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e5ea297-e077-44e4-9136-30f321450714/object-pivot-graph.png)

This graph uses the **Object Pivot Point** function with some minimal logic to scale an object from its pivot point using a scalar parameter in the Material Instance Editor. You can see the result in the demonstration below:

## ObjectScale

The **ObjectScale** function returns the object's XYZ scale together and seperately. This is not compatible with the pixel shader.

| Outputs | Description |
| --- | --- |
| **Scale XYZ** | Returns a float3 value that is equal to the objects XYZ scale. This is not compatible with the pixel shader. |
| **Scale X** | Returns a scalar value that is equal to the object's X-scale. This is not compatible with the pixel shader. |
| **Scale Y** | Returns a scalar value that is equal to the object's Y-scale. This is not compatible with the pixel shader. |
| **Scale Z** | Returns a scalar value that is equal to the object's Z-scale. This is not compatible with the pixel shader. |

In the video below, the **ScaleXYZ** output is used as a multiplier for the Emissive input. When the size of the sphere is increased, the emissive value also increases and the sphere glows brighter.

## PivotAxis

The **PivotAxis** function creates a common pivot location on arbitrary axes. This is helpful for creating flag motion. Instead of using a single pivot point near the top of the flag, use a shared Z point and unique X and Y location data to create a more realistic connection along the object's width.

This shader node only supports uniform scaling. Also, the rotate about axis axis and the pivot axis/pos should not coincide.

| Inputs | Description |
| --- | --- |
| **Pivot Axis/Pos (Vector3)** | Enter a number to use as both your local axis line axis and position. If you would like to lock off your model, enter on its local z axis near its pivot enter (0,0,1). If you would like to lock of the top of the model, enter your model's height in as (0,0,model height). |
| Outputs |   |
| **Pivot** | This can be used as the pivot point in the rotate about axis node. |

## RotateAboutWorldAxis\_cheap

The **RotateAboutWorldAxis\_cheap** function cheaply rotates objects around world axes. Input the angle you would like to use and attach the output to world position offset.

| Inputs | Description |
| --- | --- |
| **Rotation Amount (Scalar)** | A value of one is equal to one full rotation. |
| **PivotPoint (Vector3)** | World space location of pivot point to rotate around. The default value is the model's pivot point. |
| **WorldPosition (Vector3)** | World space location of individual vertices. The WorldPosition node is typically used. |
| Outputs |   |
| **X-Axis** | Cheaply rotates the object around the world X-axis. |
| **Y-Axis** | Cheaply rotates the object around the world Y-axis. |
| **Z-Axis** | Cheaply rotates the object around the world Z-axis. |

The video below shows an example Material which rotates a cube about its own pivot point. Note how the axis of rotation changes when each of the three output pins are used.

## StaticMeshMorphTargets

The **StaticMeshMorphTargets** function unpacks morph target data that was added into a via 3ds Max's Morph Packer MAXScript.

| Outputs | Description |
| --- | --- |
| **Morph Target 1 Normals** | The surface normals that are associated with Morph Target 1. |
| **Morph Target 1 WPO** | World position offset for Morph Target 1. |
| **Morph Target 2 WPO** | World position offset for Morph Target 2. |

![StaticMeshMorphTargets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29fa003f-5369-47c0-828a-fcdce79ab12d/staticmeshmorphtargets.png)

## Wind

The **Wind** function provides separate outputs for wind strength, speed multiplied by time and a normalized wind vector.

| Inputs | Description |
| --- | --- |
| **WindActor (Vector4)** | This will take in a Wind actor (in development). At this time you may use a Vector4 to designate direction and strength of the wind. |
| Outputs |   |
| **Normalized Wind Vector** | The wind vector, normalized to 0-1 space. |
| **WindStrength** | Returns wind strength. The magnitude of the wind vector found by calculating distance from the wind vector to 0. |
| **WindSpeed** | Wind speed multiplied by time. |
| **WindActor** | Standard WindActor node. |

![Wind](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/325c73b4-a501-4c4a-8424-4f730b4be2e3/wind.png)