# Importing Materials Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-materials-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-materials-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:24

---

We're using reference images from **3DS Max** and **Maya** throughout this reference guide. Although there are other 3D modeling applications available for your use, this reference guide only covers 3DS Max and Maya.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.

Autodesk Maya Autodesk 3ds Max

## Supported Materials

Unreal's FBX pipeline supports the following materials:

*Surface* Anisotropic *Blinn* Lambert *Phong* Phone E

*Standard* Multi/Sub-Object

Only basic materials are supported by Unreal's FBX pipeline. Uncommon map (texture) types will not be imported.

## Material Naming

Unreal names materials in correlation with the originating application.

For Maya, the material name in Unreal Editor is transferred from the name of the shading engine applied to the mesh in Maya.

![mat_name_maya.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3d73763b-5a69-443c-8086-08d1d29adb2d/mat_name_maya.jpg)

For 3dsMax, the material name in Unreal Editor is transferred directly from the name of the material applied to the mesh in 3dsMax.

![mat_name_max.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7099f7f8-c310-462c-aeae-2952bd9d8098/mat_name_max.jpg)

## Material Ordering

If material order is important, content creators can specify imported material order by using the **\*\_skin##** naming convention.

For example, order can be established by naming materials accordingly:

-   `M_ExampleMesh_skin00`
-   `M_ExampleMesh_skin01`

## Importing Meshes with Multiple Materials

Unreal's FBX pipeline can import meshes with multiple materials.

Maya is pretty straightforward when it comes to the use of multiple materials on a mesh. You simply select the faces of the mesh you want to have the material applied to and then apply the material.

![mat_mult_maya.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d27b1eef-0983-4fde-bf91-c348fe67475c/mat_mult_maya.jpg) ![mat_mult_maya_result.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e1bc8a7-aa80-458e-ac88-4f6e0ad9fe8c/mat_mult_maya_result.jpg)

A material will be created in Unreal Editor for each material applied to the mesh in Maya, and the imported mesh will have material slots for each of these materials. When applied to the mesh, the materials will only affect the corresponding polygons of the mesh (just as they did in Maya).

In 3dsMax, multiple materials are handled by the use of a **Multi/Sub-Object** material. Each face of a mesh has a *Material ID* and each Standard material within the Multi/Sub-Object material is applied to the corresponding *Material ID*.

![mat_multi_max.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89ce9b76-af17-4443-91cc-c408c64291ae/mat_multi_max.jpg) ![mat_multi_max_result.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec66db19-8c8f-473d-aadd-ab5847f86753/mat_multi_max_result.jpg)

A material will be created in Unreal Editor for each of the Standard materials within the Multi/Sub-Object material and the imported mesh will have material slots for each of these materials. When applied to the mesh, the materials will only affect the corresponding polys of the mesh, just as they did in 3dsMax.

## Importing Textures

If the material has a texture assigned as either a diffuse or normal map in the 3D application, those textures will be imported into Unreal as long as the **Import Textures** setting is enabled.