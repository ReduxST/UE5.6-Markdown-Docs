# Dataprep Import Customization

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-import-customization-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/dataprep-import-customization-in-unreal-engine)  
**Processed:** 2025-06-14 16:18:41

---

When Datasmith imports a scene into Unreal Engine, it does its best to preserve the geometry, materials, and scene hierarchy that you created in your source application. However, when you build 3D models in specialized applications for purposes other than real-time rendering, the scenes are often not prepared in a way that makes sense for a real-time rendering engine like Unreal. For example, this is often the case for models you create in applications like Rhino for the primary purpose of manufacturing or extruding physical parts, scenes you create in Revit or an IFC-compliant application for the primary purpose of documenting a construction project, scenes you create with procedurally generated elements in Cinema 4D, and so on.

You can always import the raw scene data, then make use of the tools offered by Unreal Editor to adjust your Assets and Actors after the import is complete. However, this has some limitations. For example, you may need to repeat these steps when you reimport the scene to pick up changes made in the source application or when you reimport a different scene with the same settings.

You can use the Visual Dataprep system to create reusable import "recipes" that reorganize, clean, merge, and modify scene elements before creating the final Assets and Actors in your Unreal Engine Project. You can create a recipe once, then reuse it each time you need to import a scene. You can also reuse the same recipe to import different source files, and even reuse it across different Projects. This effectively allows you to create your own standardized set of Asset import pipelines that match the needs of your content.

With the Visual Dataprep system, you can build common data preparation tasks like these into the import process:

-   Replacing Materials used in your source scene with high-quality Materials made specifically for real-time visualization.
-   Identifying unnecessary geometry and removing it from the scene.
-   Merging geometry together to reduce the number of separate objects in the scene.
-   Creating Levels of Detail to render complex geometry more efficiently.
-   Creating collisions for Objects that need collision meshes to work in your runtime experience, such as floors and walls.

As you get started with Visual Dataprep, you will discover some other operations that you can use to prepare reusable dataprep recipes for real-time scenes.

## Get Started

## Tutorials

## Reference