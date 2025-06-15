# PCG Biome Core Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-overview-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-overview-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:29

---

The PCG Biome Core and Sample Plugins provide examples of how to use the [PCG Framework](/documentation/en-us/unreal-engine/procedural-content-generation-overview) with features like Attribute Set Tables, Feedback loops, Recursive Sub-graphs and [Runtime Hierarchical Generation](/documentation/404). This section contains the definition of the PCG Biome Core and Sample plugins, the tool features list, to dos for future updates and known issues.

For more information on the Procedural Content Generation (PCG) Framework, see [Procedural Content Generation Framework](/documentation/en-us/unreal-engine/procedural-content-generation-overview).

## What is the PCG Biome Core

The PCG Biome Core is a data-driven biome creation tool made of native PCG Framework nodes, graphs and making use of data assets. The tool has been built with a systemic approach providing a fixed pipeline, organized in logical sections with customizable steps.

It serves as an example to learn about the PCG Framework and leverages features such as Attribute Set Tables, Feedback loops, Recursive Sub-graphs and [Runtime Hierarchical Generation](/documentation/404).

It can be used by productions to get started in their world creation tool set and copied, modified or extended for specific needs and requirements without any or with minimal programming support.

The plugin itself is labeled as experimental and will evolve through future updates while relying on the PCG Framework and standard UE functionality that is Beta or Ready for Production. If used in production, it is recommended to copy the plugin to prevent future releases from breaking existing content.

The PCG Biome Core plugin is standalone, containing only what is required for the tool to work such as base data assets, structures, blueprint classes and PCG graphs. For more information on enabling plugins, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

## What is the PCG Biome Sample

The PCG Biome Sample is a content example showcasing the PCG Biome Core tool. It consists of the BiomeSampleLevel, a world with a pre-configured BiomeCore, multiple Biomes with their Assets and different inputs such as a Biome Volume, Biome Spline, Biome Texture and other Injected Data, a specific CropField generator and a stand alone actor.

The Biome Sample plugin can be enabled in any project using the Plugin settings. It depends on the Biome Core plugin and its own content. The Biome Sample is a guide and a reference on how to set up the Biome Core without having to load a separate project.

## Feature List

The PCG Biome Core contains the following features:

-   Data-driven, can be copied, modified or extend for any productions needs.
    
-   PCG native nodes only, no custom code, no custom Blueprint element.
    
-   Fixed pipeline organized in logical sections with customizable steps using PCG Graphs and Data Assets.
    
-   Unlimited user defined biomes.
    
-   Classes, Structures, Data Assets, Graphs ready to use.
    
-   AttributeSet table containing biome asset properties gathered and built dynamically from all data assets references.
    
-   Biome Cache to abstract biome inputs in 3D space.
    
-   Biomes can be spatially defined from volumes, splines and/or texture.
    
-   Biome priority sorting.
    
-   Biome global blending.
    
-   Support for manual or semi-manual interactions through exclusions and injected data.
    
-   Meshes, PCG Data Assets/Assemblies and Actors spawning.
    
-   Points bounds from meshes with support for custom bounds scaling.
    
-   Layering of generated points with overlap managed by generator priority and accurate bounds.
    
-   Multiple Generator subtypes support to better control asset distribution within a biome (i.e using landscape layer weights painting).
    
-   Global Root and Children point filtering from customizable compute and/or texture projection filter graphs (height, density, flow, and more).
    
-   Per-asset recursive hierarchical transform and spawning with support for multiple children per recursion level.
    
-   Recursion max depth and ratio controls.
    
-   Static Mesh property overrides per asset entry (cast shadow, collisions, and more).
    
-   Transforms offsets and scale per asset entry.
    
-   Runtime Hierarchical Generation details spawning on landscape and meshes.
    

## To Do

**Per-Biome blending range:** allow specific per-biome blending range instead of the current global blending range on each biome core actor.

**Assembly hierarchy and tags support:** add more advanced control over transforming and filtering assemblies from their inner hierarchy and tags similar to what was showcased by the Electric Dreams sample.

**Landscape patches workflow:** prevent potential feedback loops between landscape refreshes and PCG updates when spawning actors with landscape patches components.

## Known Issues

-   Child assets are not respecting exclusions and biome bounds.
    
-   Child assets overlapping with root and child asset from different hierarchy branches.
    
-   Difference by generator priority occurs prior filtering, leading to points being removed preemptively.