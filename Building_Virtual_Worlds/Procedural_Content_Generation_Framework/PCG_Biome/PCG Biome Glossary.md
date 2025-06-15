# PCG Biome Glossary

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-glossary-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-glossary-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:27

---

The PCG Biome Core and Sample Plugins are examples of how to use the [PCG Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-overview). This page provides definitions for many of the terms used in the documentation for this project.

Assembly (PCG)

PCG Data Asset, a PCG point data, created and exported from all static meshes and instanced static meshes found in a level using the **Asset Action > Create PCG Assets from Level(s)**.

Biome

A volume in space defined by a Biome Definition and a list of Biome Assets.

Biome Actors

Blueprint actors available with the Biome Core used to set up biomes in a world. This includes Biome Volumes/Splines and Biome Setups actors.

Biome Assets

A data asset containing asset properties to be spawned by Biome Core.

Biome Cache

3D Point Grid Structure used to store the biomes in the world.

Biome Core

Data-driven biome creation tool built with a systemic approach providing a fixed pipeline organized in logical sections with customizable steps. The PCG Biome Core plugin contains a collection of PCG Graphs and subgraphs used to procedurally generate Biomes.

Biome Core Runtime

Biome Core Runtime is a separate PCG Component and Graph, used for runtime generation of detailed assets around the camera.

Biome Sample

The PCG Biome Sample plugin contains a level, data assets and custom PCG graphs used to showcase procedural biome generation using Biome Core.

Child Points

All points created from the recursive transform step to spawn child assets.

Filter Graph

PCG Graph processing points and writing to a defined filter attribute from its logic or texture projection.

Filters

A list of filter graphs.

Generator

A data asset holding a Type, Priority and Generator Graph properties, referred to by Biome Assets entries.

Generator Graph

PCG Graph producing root points used for placing assets in the world.

Global parameters

Biome Core graph parameters impacting its global behavior. Includes filter graphs, debug cache display, biome blending range and optional biome map projection.

Hierarchical Generation

Subdivides the volume and processing into multiple grids of different size at which parts of a PCG graph executes. Hierarchical Generation speeds up local updates by distributing computing at different grid sizes and outputs data into separate actors that can be streamed in individually. For more information, see [Using PCG Generation Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-generation-modes-in-unreal-engine?application_version=5.5).

Injected Data

External data injected at different stages of the Biome Core to exclude or add points. Divided in different types based on their entry point within the pipeline: Exclusions, Typed, Specific, Custom biome data.

Partitioning

Subdivide the volume and processing into a grid to speed up local updates and divide outputs into separate actors that can be streamed in individually.

Root Points

All points provided by the generators and their graphs.

Runtime Assets

A data asset containing properties of assets to be spawned by Biome Core Runtime.

Runtime Hierarchical Generation

Generate at runtime grid cells based on streaming source or PCG generation source components using the generation radius of each grid size configured in the PCG Graph. Uses the same multi-level grid size approach as the Hierarchical Generation. For more information, see [Using PCG Generation Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-pcg-generation-modes-in-unreal-engine?application_version=5.5).

Transform Graph

PCG Graph taking points from a generator or parent transformed points to alter their properties. Used for child points generation and placement.