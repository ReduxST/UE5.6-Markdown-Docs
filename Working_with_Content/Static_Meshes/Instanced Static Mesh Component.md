# Instanced Static Mesh Component

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:14

---

In Unreal Engine, you use **actors**, such as static mesh actors, to fill levels. Static mesh actors make up most of what you see in a level, such as copies of walls, floors, or books on a shelf. Each static mesh actor has an inherent performance cost that increases with each new actor.

To reduce performance and workflow costs, you can use the engine's instancing features. For repeated meshes, the Instance Static Mesh (ISM) component helps efficiently group identical static meshes into one actor.

This overview discusses the use of ISMs for optimization and the various tools for creating and editing the component type. For an overview of the tools to create ISMs, see the [Creating and Editing ISM](/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine#creatingandeditingisms) section on this page.

The Valley of the Ancient sample project uses ISMs extensively to build the world in an optimized way with different static meshes placed together (known as kitbash) rather than unique pieces.

To learn more about the Valley of the Ancient sample project and how to download it to explore its use of ISMs, see the [Valley of the Ancient Sample](/documentation/en-us/unreal-engine/valley-of-the-ancient-sample-game-for-unreal-engine) document.

## Prerequisite Knowledge

We recommend understanding the following topics before continuing with the page:

-   [Unreal Engine Terminology](/documentation/en-us/unreal-engine/unreal-engine-terminology)
    
    -   Specifically componet, actor, level, and Blueprint
-   [Assets](/documentation/en-us/unreal-engine/assets-and-content-packs-in-unreal-engine)
    
-   [Static Mesh Actor](/documentation/en-us/unreal-engine/static-mesh-actors-in-unreal-engine)
    
-   [Draw Calls](https://stage.edc-dev.net/documentation/en-us/unreal-engine/guidelines-for-optimizing-rendering-for-real-time-in-unreal-engine#drawcalls)
    

## Instanced Static Mesh

An ISM is a component that contains a group of identical static meshes. Each static mesh within the component represents an instance (copy) of the static mesh asset.

You can use ISMs as a performance and creative workflow technique for repeating meshes. The method combines draw calls (a lookup cost for assets that happens every frame) of identical static meshes. The use of an ISM reduces the memory usage of `UObjects`. For example, on the GPU, a primitive uses roughly ten times more memory than a basic instance (672 bytes vs 64 bytes). As a design workflow, you can automate the generation of repeated meshes or assemble the instances to create a new mesh.

|   |   |
| --- | --- |
|  |  |
| Static Mesh Component Stats | Instanced Static Mesh Component Stats |

Stat comparison of 200 non-nanite books as individual static mesh actors and as a single actor with an instanced static mesh component.

With any project it is important to understand your target platforms and performance budget. To learn more about optimization and stat commands, see [Guidelines for Optimizing Rendering for Real-Time](/documentation/en-us/unreal-engine/guidelines-for-optimizing-rendering-for-real-time-in-unreal-engine) and [Stat Commands](/documentation/en-us/unreal-engine/stat-commands-in-unreal-engine).

### Details Panel

An instanced static mesh is a component of an actor. You can view the hierarchy in the **Details** panel. The type of actor depends on which tool you use to create an ISM. Learn more about selecting and creating an ISM in the [Creating and Editing ISMs](/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine#creatingandeditingisms) section on this page.

In addition, you can view and modify the following in the Details panel:

-   The static mesh asset applied to a component of the actor.
    
-   The number of instances inside a component.
    
    -   Includes the option to add, delete, or duplicate instances.
-   The material used by all instances generated by the component.
    
-   Custom data per instance. To learn more, see the [Custom Data](/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine#customdata) section of the page.
    
-   Levels of Details (LODs). To learn more, see the [Hierarchical Instanced Static Mesh](/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine#hierarchicalinstancedstaticmesh) section on this page.
    
-   Instance culling distance. To learn more, see [Visibility and Occlusion Culling](/documentation/en-us/unreal-engine/visibility-and-occlusion-culling-in-unreal-engine).
    
-   Additional properties commonly found in the panel. To learn more, see [Level Editor Details Panel](/documentation/en-us/unreal-engine/level-editor-details-panel-in-unreal-engine).
    

Instanced static mesh component highlighted in the Details panel and corresponding settings.

If you click an individual component instance, only the transform properties are available in the Details panel. This limited option is because the component shares all other properties, such as [materials](/documentation/en-us/unreal-engine/unreal-engine-materials), to create a single efficient component.

## Differences between an Instanced Static Mesh and Static Mesh

When you drag a **static mesh asset** into the Level Editor, a **static mesh actor** referencing the asset is automatically created. Each static mesh in an actor is referenced through a component. By default, when dragging a static mesh asset into a level a **static mesh component** is applied.

The table below shows the difference between a **static mesh component** and an **instanced static mesh component**.

| **Static Mesh Type** | **Behavior** |
| --- | --- |
| **Static Mesh Component** | Single static mesh representation with its own transform, material, and collision. |
| **Instanced Static Mesh Component** | 
Represents multiple instances of the assigned static mesh, which all share the same material and collision properties.

This component is commonly used to render the same static mesh more efficiently with different transforms. Many properties, such as collision, materials, and shadows, are component-level only and cannot be edited per instance.



 |

|   |   |
| --- | --- |
|  |  |
| Static Mesh Component | Instanced Static Mesh Component |

An actor can consist of multiple ISM components and static mesh components. Similar to repeated identical static mesh actors placed in a level, it is more efficient to use an ISM instead of duplicating a static mesh component in an actor.

## Hierarchical Instanced Static Mesh

Traditionally, **hierarchical instanced static meshes** (HISMs) uniquely applied levels of details (LODs) per instance, while an ISM applied LODs to the overall component bounds. Now, you can use LODs per instance for an ISM.

LODs are an array of the same mesh at different triangle counts depending on its screen space in the viewport. A reduced triangle count helps decrease the compute time, increasing optimization. You can adjust LOD properties for an ISM and HISM component in the Details panel. To learn more about LODs, see [Creating and Using LOD](/documentation/en-us/unreal-engine/creating-and-using-lods-in-unreal-engine).

There are some differences between a HISM and ISM to keep in mind. However, the implementation of an ISM over a HISM depends on your project and requires testing. To understand your project's performance needs, see [Testing and Optimizing Your Content](/documentation/en-us/unreal-engine/testing-and-optimizing-your-content).

Here are some differences to keep in mind:

-   HISMs can be better if you have 1000s of instances that don't move. In that case, a static hierarchy is used to accelerate the culling and LOD process.
    
    -   If you have many instances that are not completely static, errors can arise in your project using HISMs.
-   ISMs does not have the static hierarchy and so has to cull and LOD each instance on the GPU, which can be expensive on lower powered platforms.
    
-   If you want LODs to match a static mesh behavior, you can't rely on a HISM because it does groups of instances. HISM is most useful where the individual LOD is not very important. For example, meshes with few triangles.
    
-   If your project only uses Nanite then ISM is always the choice since Nanite has its own culling and LOD system. Use HISMs when appropriate for projects using Nanite and fallback meshes.
    

This page refers to ISM and HISM as instanced static mesh except where needed to distinguish the two.

## Instancing Systems

Unreal Engine provides systems that apply instance optimization to meshes. The use of these systems, such as Nanite, depends on your project and target platform.

| System | Description |
| --- | --- |
| **Dynamic Instancing** | Draw calls are reduced by combining static mesh draws that have identical materials and meshes. To learn more, see [Mesh Drawing Pipeline](/documentation/en-us/unreal-engine/mesh-drawing-pipeline-in-unreal-engine). |
| **Nanite** | Virtualized geometry system in which frame budgets are no longer constrained by polycounts, draw calls, and mesh memory usage. You can reference a Nanite-enabled mesh in an ISM and HISM component. To learn more, see [Nanite Virtualized Geometry](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine). |
| **Procedural Content Generation** | Framework for spawning instances to procedurally spawn content. To learn more, see [Procedural Content Generation](/documentation/en-us/unreal-engine/procedural-content-generation--framework-in-unreal-engine). |
| **Niagara** | System for creating visual effects. You can instance particle meshes at render. To learn more, see [Niagara Renders](/documentation/en-us/unreal-engine/render-module-reference-for-niagara-effects-in-unreal-engine). |

Instanced static meshes help create an efficient pipeline and ensure you aren't breaking the engine's auto-instancing. You can also create ISMs with nanite-enabled meshes.

  

## Working with ISMs

An ISM's primary function is to increase your project's performance. Creating a forest is incredibly slow if you make a copy of each mesh individually. With in-engine batch tools, you can save workflow and compute time by placing multiple grouped instances simultaneously.

### Prefabrication

Grouping identical static meshes into a component is a valuable workflow for designing an optimized level. ISMs can help complete a level design, such as placing background props in environments or repeating instances of architecture to create a tower.

This type of prefabrication differs from the workflow of merging meshes to create a new static mesh asset in that each instance is identical, selectable, and updating one instance updates all instances. To create prefabrication instances, see [Creating and Editing ISMs](/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine#creatingandeditingisms) section of the page.

### Custom Data

With an ISM, you can use **Custom Primitive Data** and **Per Instance Custom Data** to reduce draw calls further by passing data without generating a new **dynamic material instance** per mesh. Both data sets are available in the Details panel. You can read the data into a material and manipulate it using Blueprints.

-   **Custom Primitive Data:** Additional float data stored on a primitive. To learn more, see [Storing Custom Data in Materials Per-Primitive](/documentation/en-us/unreal-engine/storing-custom-data-in-unreal-engine-materials-per-primitive).
    
-   **Per Instance Custom Data:** Additional float data per instance. To learn more, see [Deterministic Replacement for Material Per Instance Random for nDisplay](https://dev.epicgames.com/community/learning/tutorials/wdMm/unreal-engine-deterministic-replacement-for-material-perinstancerandom-for-ndisplay).
    

You can profile your project to understand performance bottlenecks and potential areas to incorporate ISMs. To learn more, see [Unreal Insights](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine).

  

## Creating and Editing ISMs

The following are various in-engine tools for creating and editing ISMs.

When selecting multiple unique static meshes to group into a single actor, an instanced static mesh component is created per unique static mesh asset.

  

### Instance Selection

You can use the following methods to select instances of an ISM:

-   The console command `TypedElements.EnableViewportSMInstanceSelection`. Where true (1) is the default value.
    
-   Under the **Instances** section of the **Details** panel.
    
-   The [ISM Editor](/documentation/en-us/unreal-engine/instanced-static-mesh-component-in-unreal-engine#ismeditor).
    

### Blueprints

The **Blueprint Visual Scripting system** is a node-based scripting interface. You can use a Blueprint actor to add an ISM or HISM and then incorporate logic, such as spawning books on a shelf. To learn more about creating Blueprints, see [Introduction to Blueprints](/documentation/en-us/unreal-engine/introduction-to-blueprints-visual-scripting-in-unreal-engine).

To add an ISM to a Blueprint actor, follow these steps:

1.  Open your Blueprint actor. To learn how to create and open a Blueprint class, see [Creating Blueprint Classes](/documentation/en-us/unreal-engine/creating-blueprint-classes-in-unreal-engine).
    
2.  Click **\+ Add** in the **Components** tab.
    
3.  Search "Instanced" and choose your preferred instanced component.
    
4.  In the **Static Mesh** category of the **Details** panel, add your static mesh asset.
    
5.  In the **Instance** category of the Details panel, click the **+** icon to add an instance.
    

The static mesh should now appear in the Blueprint Viewport.

For an example of using instanced static mesh components in a script, see the [Blueprint Solution For Instanced Static Meshes](https://dev.epicgames.com/community/learning/tutorials/wdMm/unreal-engine-deterministic-replacement-for-material-perinstancerandom-for-ndisplay) section of the Deterministic Replacement tutorial.

### Merge Actors

The **Merge Actors** tool consists of various methods for combining static mesh actors. One option is the **Batch** method, which groups static meshes to create ISMs.

To batch actors, follow these steps:

1.  Select your desired actors.
    
2.  From the [menu bar](/documentation/en-us/unreal-engine/level-editor-in-unreal-engine#menubar), select **Actor > Merge Actors > Merge Actors Settings**.
    
3.  Change the method to **Batch** and adjust settings as needed.
    
4.  Click **Merge Actors**.
    

Batch method for creating instanced static mesh components.

After defining your preferred settings, you can run the command again by selecting the **Batch** option from the **Merge Actor** dropdown instead of **Merge Actors Settings**.

  

To learn more about the tool, see [Merge Actor](/documentation/en-us/unreal-engine/merging-actors-in-unreal-engine).

### Foliage Mode

**Foliage Mode** is a toolkit for placing static mesh and actor foliage to populate large environments quickly. You can use the **Static Mesh Foliage** to create HISMs while you paint.

Painting instanced static mesh components using the Foliage tool.

To learn more, see [Foliage Mode](/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine).

### Packed Level Actor

Another way to batch actors is using the level-instancing workflow. This workflow creates a packed level actor from Blueprints and is helpful for creating prefabricated objects.

The Valley of the Ancient sample project created ISMs from the Create Packed Level Actor tool.

To create a packed level actor, follow these steps:

1.  Select the desired actors.
    
2.  Right-click the selection to open the context menu and click **Level > Create Packed Level Actor**.
    
3.  Choose the pivot type and actor.
    
4.  Click **Ok**.
    
5.  Name the level and click **Save**.
    
6.  Name the Blueprint and click **Save**.
    

Actors are automatically grouped into a HISM when you use this method. To edit the component's properties, open the Blueprint actor.

To learn more about packed level actors, see [Level Instancing](/documentation/en-us/unreal-engine/level-instancing-in-unreal-engine).

### Modeling Mode Tools

The Modeling editor mode, known as **Modeling Mode**, is a toolkit for creating and editing meshes. The editor mode includes tools for instanced static meshes. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

#### Harvest Instances Tool

You can use the **Harvest Instances** tool to select a set of static mesh actors and batch them to create an ISM or HISM component. To access the Harvests Instances tool, click the **XForm** category in **Modeling Mode**.

#### Pattern Tool

The **Pattern** tool creates a mesh from pattern techniques and can output it as an ISM. You can tile one or more selected meshes along a line, grid, or circle oriented on a movable 3D plane. Various parameters are available for each tiling pattern, including interpolating translation, rotation, scale, and jitter. The tool can help build repeating objects, and scatter meshes for your environment. The tool consists of the following output types: single actors, dynamic mesh, and instanced static mesh.

To access the Pattern tool, click the **XForm** category in **Modeling Mode**.

#### ISM Editor

The **ISM Editor** selects instances of an ISM component and performs transformations. You can also add, replace, and delete instances. To access the ISM Editor, click the **XForm** category in **Modeling Mode**.

When you replace an instance with a new static mesh asset, a second ISM component is added.