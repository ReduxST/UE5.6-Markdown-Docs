# Pivot Painter Tool 1.0 Material Functions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/painter-tool-1.0-material-functions-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/painter-tool-1.0-material-functions-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:33

---

**Pivot Painter** Material Functions allow you to tap into the [Pivot Painter MAXScript](/documentation/en-us/unreal-engine/pivot-painter-tool-in-unreal-engine), which stores rotation information within the vertices of a mesh. This is a great way to handle dynamic motion on Static Meshes.

Although the data provided by Pivot Painter can be utilized without these functions, they do make the process much easier.

## Pivot Painter Functions

The following is a list of all the functions underneath the Pivot Painter category.

These functions are used to process and organize world position and angle information stored in the model's UVs by the Pivot Painter MAXScript.

### PivotPainter\_HierarchyData

This particular function is specifically designed to work with object hierarchies.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Max Dist for Parent Piv (Scalar)** | This value should match the value that was used in the MAXScript "Max Dist for Parent Piv" spinner while painting your asset. |
| Outputs |   |
| **Parent Piv Position** | Returns the pivot point information for each parent in world space. Children return the pivot point information of the parent they are attached to. |
| **Parent X Axis Vector** | Returns a normalized vector pointing down the parent's x-axis. |
| **Child Piv Position** | Return the pivot position information in world space for each child. Parents return a value of (0,0,0). |
| **Child X-Axis Vector** | Returns a normalized vector pointing down the parent's x-axis. |
| **Object Pivot Point** | Location of the object's pivot point. |
| **Object Orientation** | The orientation of the object. |
| **Object Scale** | The scale of the object. |
| **Object Black Mask** | (Currently non-functional) Returns a black value for surfaces that are painted black by the Pivot Painter tool. |

![HierarchyData](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6347b815-a361-421c-8319-755656c505f3/hierarchydata.png)

The outputs labeled "-----------------" exist as separators in the list and are not intended to be used.

### PivotPainter\_PerObjectData

This particular function is designed to work on a per-object basis.

| Item | Description |
| --- | --- |
| Outputs |   |
| **Pivot Position** | Returns the pivot point information for each element in world space. |
| **Child X-Axis** | Returns a normalized vector pointing down the element's X-Axis, which points from the pivot point toward the averaged center of the mesh. |
| **Random Value Per Element** | Returns a random value per element in the 0-1 range. |
| **Custom Alpha Values** | Returns the custom falloff values stored in the vertex alpha channel of the model. |
| **Object Scale** | Returns a scalar value that is equal to the object's uniform scale. |

![PerObjectData](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f70b0e34-03ca-4f52-9b6e-e27a64edb332/perobjectdata.png)

### PivotPainter\_PerObjectFoliageData

This function is designed to work specifically with individual foliage objects.

| Item | Description |
| --- | --- |
| Inputs |   |
| **Wind Vector (Vector4)** | Takes in the incoming vector for the wind's direction and magnitude. |
| **Optimized for Foliage Placement (StaticBool)** | Set to *true* if you processed the mesh using Pivot Painter with the "Optimize for Foliage Placement" option checked. Default is *false*. |
| **Optimized Vector (Vector3)** | Enter a local vector to be used as the element's rotation axis. This is only viable if the *Optimized for Foliage Placement* input is set to *true*. |
| Outputs |   |
| **Piv Position** | Returns the pivot point information for each element in world space. |
| **Element Rot Axis** | Returns a rotation axis for branches to be used with the "RotateAboutAxis" node. Leaves return the same information. Note: The angle is found by transforming a vector along the branch's x-axis from local to world space. Then the cross product is found between the wind direction and the transformed vector. |
| **Element X-Axis** | Returns a normalized vector pointing down the elements X-Axis. Which points from the pivot point toward the averaged center of the mesh. |
| **Random Value Per Element** | Returns a random value per element in the 0-1 range. |
| **Custom Alpha Values** | Returns the custom falloff values stored in the vertex alpha channel of the model. |
| **Normalized Wind Vector** | The vector for the wind direction and magnitude normalized to 0-1. |
| **Wind Speed** | Outputs wind speed multiplied by time multiplied by -1. |
| **Wind Strength** | Returns wind strength. The magnitude of the wind vector found by calculating distance from the wind vector to 0. |
| **Object Scale XYZ** | Returns a scalar value that is equal to the object's uniform scale. |
| **Uniform Object Scale** | Returns a scalar value that is equal to the object's uniform scale. |

![PerObjectFoliageData](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb75ecfa-4e0d-448a-9e39-fac7b7856ed8/perobjectfoliagedata.png)

### PivotPainter\_TreeData

The outputs starting with *tree* process the model's UV information as it would be stored by the Pivot Painter MAXScript. The outputs starting with *Leaf* process the UV information as it would be stored by the per-object pivot painting section of the script.

| Item | Description |
| --- | --- |
| Inputs |   |
| **WindVector (Vector3)** | This is the direction that the wind will be blowing. |
| **Max Dist for Parent Piv (Scalar)** | This value should match the value that was used in the max script "Max Dist for Parent Piv" spinner while painting your asset. |
| Outputs |   |
| **Branch Piv Position** | Returns the pivot point information for each branch in world space. Leaves return the pivot point information of the branch they are attached to. |
| **Branch Wind Rot Axis** | Returns a rotation axis for branches to be used with the "RotateAboutAxis" node. Leaves return the same information. Note: The angle is found by transforming a vector along the branch's x-axis from local to world space. Then the cross product is found between the wind direction and the transformed vector. |
| **Branch X-Axis Vector** | Returns a normalized vector pointing down the branches x-axis. This is not typically needed for foliage animations unless it is needed for custom vector calculations. |
| **Branch Flow Grad** | Returns a gradient value in the direction of the blowing wind. |
| **Branch Flow Grad 90 Deg** | Returns a gradient value across world space at a 90 degree angle to the wind. |
| **Leaf Piv Position** | Return the pivot position information in world space for each leaf. Branches return a value of (0,0,0). |
| **Leaf Rot Axis** | Returns a rotation axis for leaves to be used with the "RotateAboutAxis" node. Branches return (0,0,0). Note: The angle is found by transforming a vector along the leaf's x-axis from local to world space. Then the cross product is found between the wind direction and the transformed vector. |
| **Leaf X-Axis Vector** | Returns a normalized vector pointing down the branches x-axis. This is not typically needed for foliage animations unless it is needed for custom vector calculations. |
| **Leaf Mask** | Returns a white mask for leaves. All branches are black. |
| **Leaf Flow Grad** | Returns a gradient value in the direction of the blowing wind. |
| **Leaf Flow Grad 90 deg** | Returns a gradient value across world space at a 90 degree angle to the wind. |
| **Object Pivot Point** | Returns the pivot point location of the object. |
| **Object Orientation** | Returns the orientation of the object. |
| **Object Rotation Axis** | Returns the rotation axis for the object. |
| **Object Scale** | Returns the scale of the object. |
| **Object Flow Grad** | Gradient aligned with the wind vector at object level in world space. |
| **Object Flow Grad 90 deg** | Gradient aligned with the wind vector at object level in world space, rotated 90 degrees. |
| **WindStrength** | Returns wind strength. The magnitude of the wind vector found by calculating distance from the wind vector to 0. |
| **Normalized Wind Vector** | Returns a normalized wind vector with a magnitude between 0-1. |
| **WindSpeed** | Wind speed multiplied by time. |
| **Black Mask** | Returns a black value for surfaces that are painted black by the pivot painter tool. This mask only works in the vertex shader. |

![TreeData](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93af6959-87af-43ca-869b-adf9a847a921/treedata.png)

The outputs labeled "-----------------" exist as separators in the list and are not intended to be used.