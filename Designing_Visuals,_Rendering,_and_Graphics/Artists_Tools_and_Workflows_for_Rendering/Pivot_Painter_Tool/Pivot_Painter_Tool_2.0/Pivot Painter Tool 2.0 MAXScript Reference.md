# Pivot Painter Tool 2.0 MAXScript Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pivot-painter-tool-2.0-maxscript-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pivot-painter-tool-2.0-maxscript-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:08

---

This page will cover the various properties of the Pivot Painter 2 3DS Max script. This tool is used to create very complex animations by storing pivot and rotational information about the model inside of its textures. This MAXScript can be used create complex hierarchies of animations all driven by Material's inside of Unreal Engine 4.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b78e9c0-c89b-4fab-bedd-a4ce0ed53d48/pivotpainter2.png)

## Prep Tools

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc7b81f2-5f77-43bb-9230-6f1d49e3a39b/preptools.png)

| Property | Description |
| --- | --- |
| **Detach Selected Model's Elements** | This will detach every element in an object as its own object. |
| **Preserve Custom Normals (Slow)** | 
This will duplicate the model as many times as there are model elements and then delete all but one element from each copy. This is to preserve the meshes custom normals.

This method can potentially be very time-consuming depending on the number of elements being detached since the model will be duplicated for each element there is. It is recommended to only use this is absolutely necessary.



 |
| Detach Elements Based on Penetration |   |
| **Pick Selected Obj** | Pick an editable polygon object without any modifiers applied. Do not pick the same object for both the "selection object" and the "model to process" options. (Note: The selection mesh cannot have any holes.) |
| **Pick Model to Proc** | Pick an editable polygon object without any modifiers applied. Do not pick the same object for both the "selection object" and the "model to process" options. (Note: The selection mesh cannot have any holes.) |
| **Detach Model Elements That Touch** | This will separate any elements that touch or penetrate the selection object's geometry into its own separate object. (Note: This tool will not work properly if the selection object has any holes.) |
| Generate New Pivot Points |   |
| **Pick Your Model Selection Set** | 

Use this drop-down to select your model selection set.

-   **Update**: Press this to get the latest selection sets from 3DS Max.
-   **Manage**: Press this to manage your selection sets.



 |
| **Pick Leaf Pivot Obj** | 

Choose whether you would like to construct your pivots based off of the knots in a spline or the vertices in an editable poly object. This will enable the button selections for **Pick Spline** or **Pick Mesh**

-   **Pick Spline**: Use this button to pick a spline from the scene viewport. The script will find the closest vertex pair between each model and each knot in the spline. Then it will move the object's pivot to the location of that vertex and orient the axis to match the model. The x-axis will point toward the center of the model from the desired vertex. The z-axis will point along the surface's normal. Processing time will increase as vertex counts rise. (Warning: Do not use the H list hotkey. The object must be picked from the viewport.) (Tip: For grass use a single or two-knot spline placed well below your grass to increase calculation speeds.)
-   **Pick Mesh**: Use this button to pick a mesh from the scene viewport. The script will find the closest vertex match between the model's pivot and model's vertices. Then it will orient the leaf's axis to the polygonal orientation and vertex position. Warning: Do not use the H list hotkey. The object must be picked from the viewport.) (Tip: For grass use a single or two-knot spline placed well below your grass to increase calculation speeds.)



 |
| **Num of Face Norms to Avg Near Pivot** | Enter a value to specify the number of face normals you want to average near a pivot point. This enables you to control the number of normals you're affecting or you can simply enable the **Average All** checkbox to include all available face normals nearest the pivot. |
| **Create New Pivots** | This will generate a new pivot point for every editable polygon object in the selection set. The pivot will rest on the model vertex closest to a knot in the selected spline or vertex in the chosen editable poly object. The x-axes of the pivots will be oriented toward the averaged center of the meshes. The meshes' bounds will also be recreated and aligned with the new pivot. |
| Recreate Bounding Boxes |   |
| **Process Selected Objects** | As a model changes from via sub-object manipulation, its bounding box expands to fix the model elements but does not re-align itself with the model's pivot point. This function recreates the object's bounding box so that it aligns with the model's basis vectors. It is necessary to have a correctly constructed bounding box to successfully utilize the axis tools in the processing section along with the vertex alpha painting tools. |

| Property | Description |
| --- | --- |
| **Update** | Press this to get the latest selection sets from 3DS Max. |
| **Manage** | Press this to manage your selection sets. |

| Property | Description |
| --- | --- |
| **Pick Spline** | Use this button to pick a spline from the scene viewport. The script will find the closest vertex pair between each model and each knot in the spline. Then it will move the object's pivot to the location of that vertex and orient the axis to match the model. The x-axis will point toward the center of the model from the desired vertex. The z-axis will point along the surface's normal. Processing time will increase as vertex counts rise. (Warning: Do not use the H list hotkey. The object must be picked from the viewport.) (Tip: For grass use a single or two-knot spline placed well below your grass to increase calculation speeds.) |
| **Pick Mesh** | Use this button to pick a mesh from the scene viewport. The script will find the closest vertex match between the model's pivot and model's vertices. Then it will orient the leaf's axis to the polygonal orientation and vertex position. Warning: Do not use the H list hotkey. The object must be picked from the viewport.) (Tip: For grass use a single or two-knot spline placed well below your grass to increase calculation speeds.) |

## Render Options

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/536f3961-fa84-4581-b81e-f2df4753e9ab/renderoptions.png)

| Property | Description |
| --- | --- |
| **Process The Selected Object Hierarchy** | Select your mesh and then press paint. This script will locate all the editable polygon meshes that are connected to the selected mesh via their shared hierarchy. (One can connect one object to another via the 3DS Max Link tool.) After locating the meshes the script will then alter the UV channel you've chosen to act as the basis for the ensuing textures which will be generated. The default texture contains model information like pivot location in the images RGB channels and an index in the alpha. The index can be used to locate the current meshes parent mesh. This is made simple Pivot Painter 2.0 Material Functions in Unreal Engine 4. |
| **UVs** |   |
| **Texture Coordinate Location** | 
Pivot Painter 2 creates textures that store model information. Those textures can then be referenced inside of Unreal. These models require UV coordinates to associate each element with a single pixel in the data textures. This drop-down allows you to specify where the coordinates are placed.

Any shaders referencing Pivot Painter 2 textures will have to use the coordinate index and that the order in which you select the assets determines how the UVs and textures are created. If you wish to bake out multiple sets of Pivot Painter 2 textures, a selection set should be formed and reused to select the models before pressing the **Paint** button again.



 |
| **Custom Textures** |   |
| **Texture 1 RGB** | 

Selection Options

-   **Do not render**: This option will prevent Texture 1 from being written. |
-   **Pivot Position (16-bit)**: Write HDR pivot position information to the RGB channels of a texture. This information needs to be decoded using the **ms\_PivotPainter2\_DecodePosition** function when referenced inside a shader.
-   **Origin Position (16-bit)**: Write HDR object bounds center point information to the RGB channels of the texture. This information needs to be decoded using the **ms\_PivotPainter2** function when referenced inside a shader.
-   **Origin Extents (16-bit)**: Store the maximum length of the model at every basis vector from the origin of the model; stored as three floats. The local values can be referenced directly but should use **ms\_PP2\_DecodeOriginExtent** when referenced in a shader.
-   **X Vector (8-bit)**: Stores the models X-axis basis vector. It needs to be decoded with **ms\_PivotPainter2\_DecodeAxisVector** when referenced in a material.
-   **Y Vector (8-bit)**: Stores the models Y-axis basis vector. It needs to be decoded with **ms\_PivotPainter2\_DecodeAxisVector** when referenced in a material.
-   **Z Vector (8-bit)**: Stores the models Z-axis basis vector. It needs to be decoded with **ms\_PivotPainter2\_DecodeAxisVector** when referenced in a material.



 |
| **Texture 1 Alpha** | 

Selection Options

Available 16-Bit Selection Options

-   **Parent Index (Int as float)**: Pivot Painter 2 enables users to re-create complex hierarchies within the Unreal Engine's material system. It does so by iteratively sampling points within a texture, reconstructing the hierarchy with the information that it gathers in the process. The "Parent Index" option enables us to read a pixel and then to pinpoint where its parent object's pivot information is located within the same texture. Referencing this data directly is considered advanced. In most cases, it is expected that you will process models with the default texture settings which can then be used with the **PivotPainter2FoliageShader** function. This function recreates hierarchies up to four levels deep and provides many of the animation controls that you would need while animating foliage. For those that are interested in creating their own complex networks, the data in this channel is an integer that should be decoded to float form before being referenced via **ms\_PivotPainter2\_UnpackIntegerAsFloat**. That information can then be used in **ms\_PivotPainter2\_ReturnParentTextureInfo** to return the UV location of the object's parent object. A **Is Child?** (see Note section below) output pin will return a black or white value indicating whether or not the pixel points to another pixel as its parent or if it points to itself (meaning that it is the root object). Explore the **PivotPainter2FoliageShader** function if you would like more information. The Render Options between Texture 1 and 2 are the same. Picking a 16-bit RGB option will show 16-bit Alpha options and hide the 8-bit Alpha options. Conversely, picking an 8-bit RGB option will show those and hide the 16-bit options.
-   **Number of Steps From Root**: This float value can be referenced without any additional decoding steps. It represents the number of steps that the current object is from being the root.
-   **Random 0-1 Value Per Element**: This will store a randomly generated 0-1 number per item and can be referenced without using additional decoding material functions.
-   **Bounding Box Diameter**: Store the local space diameter of the objects being processed as float values. This can be transformed into world space scale by multiplying the output by an output of the **ObjectScale** material function. |
-   **Selection Order (Int as float)**: The order in which objects were selected inside 3DS Max that is stored as an integer when this option is selected. Use **ms\_PivotPainter\_UnpackIntegerAsFloat** when referencing this information. Please see Content Examples **PivotPainter2** map for a sample use case.
-   **Normalized 0-1 Hierarchy Position**: When selected, the 3DS MAXScript will find the total depth of the hierarchy of the object selected, then find the object's depth within that hierarchy and then normalize the object's current depth by dividing it by the total depth. This information is stored as a 0-1 float value and does not need to be decoded.
-   **Object X Width**: This returns a float value that's equal to the total length of the object being processed in 3DS Max along its local X vector.
-   **Object Y Depth**: This returns a float value that's equal to the total length of the object being processed in 3DS Max along its local Y vector.
-   **Object Z Height**: This returns a float value that's equal to the total length of the object being processed in 3DS Max along its local Z vector.

Available 8-Bit Selection Options

-   **Normalized 0-1 Hierarchy Position**: When selected, the 3DS MAXScript will find the total depth of the hierarchy of the object selected, then find the object's depth within that hierarchy and then normalize the object's current depth by dividing it by the total depth. This information is stored as a 0-1 float value and does not need to be decoded.
-   **Random 0-1 Value Per Element**: This will store a randomly generated 0-1 number per item and can be referenced without using additional decoding material functions. |
-   **X Extent Divided by 2048 - 2048 Max**: This returns an 8-bit float value that's equal to the total length of the object being processed in 3DS Max along its local X vector. These values use **ms\_PivotPainter2\_Decode8BitAlphaAxisExtent** to decode the value. This format can represent values between 8-2048 in increments of 8.
-   **Y Extent Divided by 2048 - 2048 Max**: This returns an 8-bit float value that's equal to the total length of the object being processed in 3DS Max along its local Y vector. These values use **ms\_PivotPainter2\_Decode8BitAlphaAxisExtent** to decode the value. This format can represent values between 8-2048 in increments of 8.
-   **Z Extent Divided by 2048 - 2048 Max**: This returns an 8-bit float value that's equal to the total length of the object being processed in 3DS Max along its local Z vector. These values use **ms\_PivotPainter2\_Decode8BitAlphaAxisExtent** to decode the value. This format can represent values between 8-2048 in increments of 8.



 |
| **Texture 2 RGB** | 

Selection Options

-   **Do not render**: This option will prevent Texture 1 from being written.
-   **Pivot Position (16-bit)**: Write HDR pivot position information to the RGB channels of a texture. This information needs to be decoded using the **ms\_PivotPainter2\_DecodePosition** function when referenced inside a shader.
-   **Origin Position (16-bit)**: Write HDR object bounds center point information to the RGB channels of the texture. This information needs to be decoded using the **ms\_PivotPainter2** function when referenced inside a shader.
-   **Origin Extents (16-bit)**: Store the maximum length of the model at every basis vector from the origin of the model; stored as three floats. The local values can be referenced directly but should use **ms\_PP2\_DecodeOriginExtent** when referenced in a shader.
-   **X Vector (8-bit)**: Stores the models X-axis basis vector. It needs to be decoded with **ms\_PivotPainter2\_DecodeAxisVector** when referenced in a material.
-   **Y Vector (8-bit)**: Stores the models Y-axis basis vector. It needs to be decoded with **ms\_PivotPainter2\_DecodeAxisVector** when referenced in a material.
-   **Z Vector (8-bit)**: Stores the models Z-axis basis vector. It needs to be decoded with **ms\_PivotPainter2\_DecodeAxisVector** when referenced in a material.



 |
| **Texture 2 Alpha** | 

Selection Options

Available 16-Bit Selection Options

-   **Parent Index (Int as float)**: Pivot Painter 2 enables users to re-create complex hierarchies within the Unreal Engine's material system. It does so by iteratively sampling points within a texture, reconstructing the hierarchy with the information that it gathers in the process. The "Parent Index" option enables us to read a pixel and then to pinpoint where its parent object's pivot information is located within the same texture. Referencing this data directly is considered advanced. In most cases, it is expected that you will process models with the default texture settings which can then be used with the **PivotPainter2FoliageShader** function. This function recreates hierarchies up to four levels deep and provides many of the animation controls that you would need while animating foliage. For those that are interested in creating their own complex networks, the data in this channel is an integer that should be decoded to float form before being referenced via **ms\_PivotPainter2\_UnpackIntegerAsFloat**. That information can then be used in **ms\_PivotPainter2\_ReturnParentTextureInfo** to return the UV location of the object's parent object. A **Is Child?** (see Note section below) output pin will return a black or white value indicating whether or not the pixel points to another pixel as its parent or if it points to itself (meaning that it is the root object). Explore the **PivotPainter2FoliageShader** function if you would like more information. The Render Options between Texture 1 and 2 are the same. Picking a 16-bit RGB option will show 16-bit Alpha options and hide the 8-bit Alpha options. Conversely, picking an 8-bit RGB option will show those and hide the 16-bit options.
-   **Number of Steps From Root**: This float value can be referenced without any additional decoding steps. It represents the number of steps that the current object is from being the root.
-   **Random 0-1 Value Per Element**: This will store a randomly generated 0-1 number per item and can be referenced without using additional decoding material functions.
-   **Bounding Box Diameter**: Store the local space diameter of the objects being processed as float values. This can be transformed into world space scale by multiplying the output by an output of the **ObjectScale** material function.
-   **Selection Order (Int as float)**: The order in which objects were selected inside 3DS Max that is stored as an integer when this option is selected. Use **ms\_PivotPainter\_UnpackIntegerAsFloat** when referencing this information. Please see Content Examples **PivotPainter2** map for a sample use case.
-   **Normalized 0-1 Hierarchy Position**: When selected, the 3DS MAXScript will find the total depth of the hierarchy of the object selected, then find the object's depth within that hierarchy and then normalize the object's current depth by dividing it by the total depth. This information is stored as a 0-1 float value and does not need to be decoded.
-   **Object X Width**: This returns a float value that's equal to the total length of the object being processed in 3DS Max along its local X vector.
-   **Object Y Depth**: This returns a float value that's equal to the total length of the object being processed in 3DS Max along its local Y vector.
-   **Object Z Height**: This returns a float value that's equal to the total length of the object being processed in 3DS Max along its local Z vector.

Available 8-Bit Selection Options

-   **Normalized 0-1 Hierarchy Position**: When selected, the 3DS MAXScript will find the total depth of the hierarchy of the object selected, then find the object's depth within that hierarchy and then normalize the object's current depth by dividing it by the total depth. This information is stored as a 0-1 float value and does not need to be decoded.
-   **Random 0-1 Value Per Element**: This will store a randomly generated 0-1 number per item and can be referenced without using additional decoding material functions.
-   **X Extent Divided by 2048 - 2048 Max**: This returns an 8-bit float value that's equal to the total length of the object being processed in 3DS Max along its local X vector. These values use **ms\_PivotPainter2\_Decode8BitAlphaAxisExtent** to decode the value. This format can represent values between 8-2048 in increments of 8.
-   **Y Extent Divided by 2048 - 2048 Max**: This returns an 8-bit float value that's equal to the total length of the object being processed in 3DS Max along its local Y vector. These values use **ms\_PivotPainter2\_Decode8BitAlphaAxisExtent** to decode the value. This format can represent values between 8-2048 in increments of 8.
-   **Z Extent Divided by 2048 - 2048 Max**: This returns an 8-bit float value that's equal to the total length of the object being processed in 3DS Max along its local Z vector. These values use **ms\_PivotPainter2\_Decode8BitAlphaAxisExtent** to decode the value. This format can represent values between 8-2048 in increments of 8.



 |

## Vertex Alpha Painter

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f15dec8b-89e0-465c-a9ad-8a3c797245c5/vertexalphapainter.png)

| Property | Description |
| --- | --- |
| Alpha Channel Falloff Controls |   |
| **3D dist to piv multiplier** | This multiplies a distance calculation from the pivot to the current vertex. |
| **3D dist to piv contrast** | The contrast option is used as the exponent of a power function applied to a distance based on a gradient between the object's pivot point and the current vertex position. |
| **XYZ Multiplier** | Selectively increase and decrease the influence of local space gradients on X, Y, and Z. The gradient is formed by finding the distance between vertices and the object's center line, as defined by the object's pivot point and an axis direction. |
| **XYZ Contrast** | The exponent of a power function applied to the XYZ gradient results. |
| **Paint Current Selection** | This paints the editable polygon objects in the selection set using the parameters above. The objects that aren't collapsed editable polygon objects will be ignored. |
| **Solid Value Painting** |   |
| **Value** | Use any value between 0 to 1 to be used to paint the selected meshes a solid color. A value of 0 will be black with 1 being full white. |
| **Paint Selected Meshes a Solid Value** | Fill the vertex alpha with a value of zero. This value can be referenced in an Unreal shader to isolate or remove animation from certain elements. |
| Preview on Selected Objects |   |
| **Diffuse** | Click on the active viewport to view this new channel. |
| **Alpha** | Click on the active viewport to view this new channel. |
| **Color** | Click on the active viewport to view this new channel. |

## Package Model

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e812132-17b9-4cb1-8a1b-ce604bcda2a1/packagemodel.png)

| Property | Description |
| --- | --- |
| **Merge Selected Model's Normals** | Select several models that contain touching, open edges. This feature will average out their normals to form a continuous surface. |