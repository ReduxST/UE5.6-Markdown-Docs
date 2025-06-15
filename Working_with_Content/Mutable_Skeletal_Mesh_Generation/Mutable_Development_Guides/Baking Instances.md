# Baking Instances

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/baking-instances-using-mutable-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/baking-instances-using-mutable-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:38

---

The main goal of Mutable is to build dynamic objects at runtime. It is also useful to be able to build these objects in the editor, and convert them to standard Unreal Engine assets (skeletal meshes, materials and textures). Some use cases for this are:

-   Production of marketing materials in other tools. From Unreal you can export these assets and import them into other content creation tools for the creation of cinematic videos and offline renders.
-   Debugging your object. You can examine a baked instance in standard Unreal Editor tools to better understand the effect of Mutable and try to pinpoint inefficiencies in your object.
-   Mutable as a production tool. Some projects use Mutable purely offline at game content creation time, generating final characters for their games.

## Baking an Instance

Instances can be baked using the **Bake Instance** button in any Mutable preview panel. These currently include the Customizable Object Editor and the Customizable Instance Editor.

The Bake Instance button is available in any Mutable Preview panel.

A window will pop up to select the target content folder for the generated resources, and a prefix for the asset names:

Select the target content folder to save your baked assets.

There are two additional checkboxes in this window:

-   **Export all used resources**: If checked, all the materials and textures used by the object will be baked in the target folder. Otherwise, only the assets that Mutable modifies are baked, and the original references to non-Mutable assets are used instead (i.e. textures used by object materials, but have no nodes connected to them). In other words, checking this box generates a fully self-contained object that doesn't use any shared resources from your project.
-   **Generate Constant Material Instances**: If checked, all the material instances in the baked skeletal meshes are constant instead of dynamic. They cannot be changed at runtime but they are lighter and required for UEFN.

The result is a set of Unreal assets in the target folder, including all levels of detail.

The results of baking out a character skeletal mesh.