# FBX Content Pipeline

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-content-pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/fbx-content-pipeline)  
**Processed:** 2025-06-14 16:23:20

---

Unreal Engine supports a variety of file formats for importing content into your project.

FBX is a flexible file format that is owned by Autodesk and provides interoperability between digital content creation (DCC) applications. Some applications such as Autodesk Motionbuilder support the format natively. While others such as Autodesk Maya, Autodesk 3ds Max, and Blender support the format using FBX plugins.

The advantages of the Unreal FBX Import pipeline over other importing methods are:

-   Using a single file format for Static Mesh, Skeletal Mesh, animation, and morph targets.
-   Importing multiple LODs and Morphs/Blendshapes in one import operation.
-   Importing Material and Texture assets, and automatically applying them to Static Meshes.

The Unreal Engine FBX import pipeline uses **FBX 2020.2**. Using a different version during export may result in incompatibilities.