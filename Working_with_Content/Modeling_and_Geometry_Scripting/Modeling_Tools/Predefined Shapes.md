# Predefined Shapes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/predefined-shapes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/predefined-shapes-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:09

---

You can create a new mesh using the **Create** category in **Modeling Mode**. The category provides a selection of predefined primitives to use as a starting base. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

## Using Predefined Shapes

You can choose between nine shapes, represented in the table below.

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3851b42-5b12-4919-85c6-18adb53ab20d/box-shape.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33843521-6731-4869-a86a-7d6aac055e16/sphere-shape.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b59aad60-fa70-4060-9aad-7f7bda8f0f52/cylinder-shape.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/794749b4-744e-4200-914e-6568813aac63/cone-shape.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67fccf71-2dd9-4756-8af0-26427f706273/torus-shape.png) |
| Box | Sphere | Cylinder | Cone | Torus |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4022c1cd-dd38-4e0d-9c2d-d367a0e1236c/arrow-shape.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1f769b9-4746-41d1-b8ab-ca19a494c433/rect-shape.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33e2b5d3-de01-43b3-b0ee-74458a937cf9/disc-shape.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/adf8ba31-0959-41a7-b35c-2798dd02172a/stairs-shape.png) |   |
| Arrow | Rectangle | Disc | Stairs |   |

You can select your desired shape and drag it into the scene for placement. After placing your mesh, you can still adjust the tool settings in the [Tool Properties](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#accessingmodelingmode) panel. Once you have your desired settings, click **Accept**.

## Tool Settings

You use the **Tool Properties** panel to control settings such as the output type, dimensions, and material.

As with other Modeling Mode tools, parameter values are remembered when reopening the tool.

### Output Type

The **Output Type** sets the type of mesh you create. You can choose between the following types:

-   **Static mesh**
-   **Dynamic mesh**
-   **Volume**

You can update the mesh type at any stage of the modeling process by various tools, such as **Convert** and **Transfer**, found in the **Transform** category.

To learn more about these output types and asset management, refer to the [Working with Meshes](/documentation/en-us/unreal-engine/working-with-meshes-in-unreal-engine) documentation.

### Shape

You can adjust the dimensions and subdivisions of your mesh under the **Shape** setting. Each shape has specific options.

In addition, you can configure the PolyGroups of your new mesh using the **PolyGroup Mode** setting. The Polygroup Mode has the following grouping options:

|   |   |   |
| --- | --- | --- |
| ![Generate PolyGroups per Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2125bb8-4a65-4a46-93ea-26e363af786e/per-shape.png) | ![Generate PolyGroups per Face](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3ebb066-18ed-44be-b0cc-f5f0a19c3e89/per-face.png) | ![Generate PolyGroups per Quad](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/238127b0-663c-45a5-97bd-e5038dbca9ea/per-quad.png) |
| **Per Shape** | **Per Face** | **Per Quad** |
| Outputs the entire mesh as a single group. | Automatically divide the mesh into recognizable face groups. | Automatically divide the mesh into a group for each quad. |

To learn more about PolyGroups, refer to the [Understanding PolyGroups](/documentation/en-us/unreal-engine/understanding-polygroups-in-unreal-engine) documentation.

### Positioning

You can position your mesh in your level based on your scene or the ground plane.

Choosing **On Scene** from **Target Surface** positions your mesh based on the surface normal of the geometry your cursor resides over.

If you set [Collision Presets](/documentation/en-us/unreal-engine/setting-up-collisions-with-static-meshes-in-unreal-engine#simulatingphysicsandcollisionpresets) to **No Collision** for any object in your level, then **On Scene** will not detect the object.

Choosing **Ground Plane** positions your mesh in the level with the Z-axis set to 0.

You can adjust the pivot location to the base, top, or center. You can visualize the position of the pivot by the cursor placement, highlighted in the table below.

|   |   |   |
| --- | --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75417428-5168-41f5-804c-01c4b721453f/base-pivot.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc857b31-b1fd-4c45-9db7-a0a22fecea08/centered-pivot.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/807c94d0-9fe0-4cfb-8430-2b0b7f9a30ae/top-pivot.png) |
| Base | Centered | Top |

### Material

You can select the appropriate **Material** for your mesh. You can also set the **UV Scale** and enable **Show Wireframe**.

![Applying a material to your mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc28cd8d-38f0-42ea-9903-16832b39b478/material-setting.png)