# PCG Biome Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:32

---

The PCG Biome Core and Sample Plugins are examples of how to use the [PCG Framework](/documentation/en-us/unreal-engine/procedural-content-generation-overview) with features like Attribute Set Tables, Feedback loops, Recursive Sub-graphs and [Runtime Hierarchical Generation](/documentation/404).

## Reference

### Core Graph Overview

The BiomeCore graph is the brain of the biome creation tool and where all processing is made using the PCG Framework.

The main processing steps are shown below, in order:

1.  Biome Cache is computed from all Biome Actors and optional Biome Texture projections.
    
2.  Generator graphs, referenced by Biome Assets within the world, are processed and bound by the biome cache, producing a unique root point data per generator used.
    
3.  Biomes are applied to the generated root points data. A Root Asset Table is built from all assets of all biomes within the world. The Root Asset Table attributes are assigned to each point based on the biome, generator type, subtype and weighting.
    
4.  At this step, Priority based Difference between each Generator root point data set is performed. The Generator Priority property determines the order of operation and can be optionally bypassed.
    
5.  Filters are applied using the PCG Graphs provided by the Root Points Filters global parameter of the Biome Core actor. The template Biome Assets class has options to control the filtering behavior per-asset entry and can be extended if desired.
    
6.  Recursive transforms are applied per asset using their transform graph and child asset reference. Through this hierarchy of asset reference, child points data can be created for each root point and limited with the maximum depth global parameter.
    
7.  Spawning of static meshes and actors. Including support for property overrides, assemblies and collision presets.
    
8.  Output data to Biome Core Runtime, can be enabled in the global parameters. All assets marked as used for runtime gen are exported. Meshes also can be optionally sampled offline to provide points to the Biome Core Runtime at minimal cost.
    

### High Level Concepts

#### Biome Cache

The **Biome Cache** is a grid of PCG points used to store biome definition data spatially in the world.

-   Biome definition colors associated with biome volumes, biome splines and biome textures are projected and stored into this 3D Grid to identify each biome in world space.
    
-   Because the Biome Cache is a 3D structure, verticality is supported - such as stacking biomes on top of each other or underground caves - 2D is still possible, by providing tall column-like points.
    
-   The cache resolution is controlled by the **Biome Cache Cell Size** vector parameter of the Biome Core PCG Component.
    
-   Each point in the cache can only store a single biome color value at a time.
    
-   **Biome prioritization** - which biome wins over other overlapping biomes - happens when storing the biome colors into the biome cache.
    
-   The cache is initialized from the Biome Core actor bounds, and if a landscape is found it uses its surface to remove cells from the grid as an optimization.
    
    \* Volumes and Spline can define biomes in a world without landscape, generators should sample geometry using world ray hit query in this case.
    
    \* Optionally, a biome texture can be projected to the cache if a landscape is present.
    
-   When generating points using surface samplers in generator graphs, the biome cache is used as a **bounding shape** to avoid sampling the landscape or other surfaces in parts of the world where the biomes are not using the generators.
    
-   Finally, the cache is used to resolve biomes before matching biome assets from the Root Asset Table to the points produced by the generator graphs.
    

#### Root Asset Table

**Root Assets** are at the top level of the asset hierarchies. They are provided by data assets assigned to Biome Setups, Volumes or Splines and contain properties such as generator, mesh, transform, bounds, rendering and collision options.

These assets properties are stored in a PCG Attribute Set table called the **Root Asset Table**. Each entry in the table is identified using its unique **AssetID** attribute.

Once generated points produced by generator graphs have been assigned a biome from the Biome Cache, they are given an AssetID attribute corresponding to their entry in the Root Asset Table.

This root asset table setup simplifies and optimizes the point attributes layout by avoiding to assign directly all the properties from an asset to each generated point. Once a point is assigned its AssetID, this is the only attribute it needs to hold. Other attributes are easily accessed when needed, from the Root Asset Table.

#### Generators

The Generators are the root points providers and mandatory for the system to work.

**Biome Generator data assets** are required to provide: the **Generator Type** as a unique name identifier, the **Generator Graphs** which are run by the Biome Core to output points on which Biome Assets will be assigned to and a **Generator Priority**.

The **Generator Graphs** are standalone PCG graphs built for any kind of needs with any custom logic, all they need to do is provide points. PCG graph instances of Generator Graphs are fully supported and should be used for easy customization from the graph parameters without having to build new custom graphs for each similar case. It is recommended to start from **BiomeGenerator\_Template** graph here: `/Script/PCG.PCGGraph'/PCGBiomeCore/BiomeGenerators/Graphs/BiomeGenerator_Template.BiomeGenerator_Template'`

The **Generator Priority** is used for layering. It impacts the priority-based difference to order the layering of multiple generators against each other. Lower priority values indicate a higher priority. The difference by priority between generated point data is done after assets have been assigned to each point, allowing access to the mesh bounds during these difference operations. The difference by priority can be bypassed optionally within the BiomeGenerator asset by enabling the GeneratorAllowOverlap option.

Each **Biome Assets** entry has a reference to a Generator. This link is necessary to define which point data the asset will be assigned to. Biome Assets can also be mapped to generator subtypes which is covered in the advanced setup section.

Examples:

-   Generate points for trees and rocks from landscape sampling with different graph instance parameter values while sharing the same source graph. The rocks generator is set with priority 0 and trees with priority 1. The trees will be automatically removed when their bounds overlap with rocks.
    
-   Generate points for spawning POI assemblies in flat areas over static meshes by sampling the geometry surface using World Ray Hit Query.
    
-   Produce points near the border of a lake or river spline and reproject them onto the landscape.
    
-   Create points for Niagara systems or Sounds volumes matching the biome.
    

#### Biome and Asset Mapping

Biomes are created from the Biome Definition and Biome Assets. Both data assets are required for a biome to exist in the world, and Biome Generators are required to assign the assets onto root points.

The mapping between biome definitions and assets occurs within the Biome Core execution. For each unique Biome Definition found in BiomeVolumes, Splines or Setup actors in the world, the list of all Biome Assets referenced within all actors sharing the same Biome Definition is gathered and associated to the specific biome during processing.

The Root Asset Table is built with all Biome Assets and the Biome they belong to which can then be properly filtered and mapped to the generated points within the biome.

A few contextual examples:

-   A single Biome Volume with a unique biome definition and multiple assets result in a unique biome for this volume.
    
-   Multiple Biome Volumes and Splines with the same biome definition but with different asset lists result in a single biome with a single common asset list.
    
-   A Biome Setup actor with a unique biome definition, multiple assets and multiple volumes or splines sharing the same biome definition: The Biome Setup class was made to provide a single global source of configuration, this means that you can build your biome using a single setup actor and only add a reference of its biome definition to other biome volumes or splines. When using the optional Biome texture projection, a Biome Setup Actor per biome texture color is required.
    

In the BiomeSampleLevel, a ConiferousForest `BP_PCGBiomeSetup` actor is used to globally define the ConiferousForest biome (blue). The `BP_PCGBiomeVolume` in the level refers to the same Biome Definition while the BiomeMap texture used (optional) has a large section with the exact same biome color. In both cases, the BiomeSetup contains the assets list and both inputs produce the ConiferousForest biome.

It is possible and recommended to create Child Blueprint Classes of pre-configured Biome Setups, Volumes and Splines for a project. This allows quick and easy re-use of Biomes in the same or across multiple worlds as well as an easy way to adjust content globally.

#### Priority Based Difference

Generators are processed individually and their output - the root points - can be layered against each other using the Generator Priority value set within the Generators Assets. The layering occurs when each point data is processed within the BiomeCoreDifferenceByPriority feedback loop. Ordered from the most important (smallest generator priority value), to the least important (highest generator priority value).

Within the feedback loop graph, a binary difference is applied sequentially between the incoming data of the current iteration and Remaining Points from previous loop iterations. Upon loop completion, no points will overlap unless the generators had identical priority values or the GeneratorAllowOverlap option was enabled. Input point bounds are matching the assigned asset mesh/assembly bounds and can be overridden within the asset options for better control.

The layering between the higher generator priority Rocks (in red) removes overlapping Trees.

The layering has been bypassed using the GeneratorAllowOverlap option, resulting in overlapping rocks and trees.

#### Filtering

Additionally to layering from the priority-based difference, both root and child points can be filtered from a fully customizable list of compute graphs or texture projections. By default, the Biome Core actor is configured with Height, Density and Water Distance filters. Biome Assets Filter Options have ranges exposed for each of these default filters.

The Density filter is based on density set from generator, transform or filter graphs on the points' `$Density` property, this means that any computation writing to `$Density` can be used. The Height filter uses the points `$Position.z` property while the Water Distance filter is working with the distance between points at or below the defined water level and the remaining points.

The filtering steps for root and child points in the Biome Core are using the dynamic graph feature which allows the graph being executed to be parameterized, in this case with an array of dynamic subgraphs for even more flexibility. For information on how to define the filters array, create filter graphs and customize filter options structure, see [Filters](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#filters).

The Biome Sample example is set up with extra texture projection filters and custom Filter Options. The two provided textures, Flow and Sun Exposure, are both 2D texture arrays projected per-tile and then filtered from their respective min/max values set within each asset.

Debug display of the flow map projection.

When filtering an asset from 0 to 0.33 from the flow map projection.

When filtering an asset from 0.66 to 1 from the flow map projection.

#### Recursion and Transform

Screenshot of BiomeCore\_ChildTransformLoop subgraph calling itself.

In Biome Core, Root Assets can have Child Assets. **Child assets** share the same asset type as their parents and can themselves have children, forming a hierarchy of assets. Contrary to the Root Assets, child assets are not generated using **generator graphs**. They use their parent points as input and generate their final points using Transform graphs.

All assets of all hierarchy levels, including the root assets, support Transform graphs execution to alter their input points.

Transform graphs are simple PCG graphs assigned to assets, they take point data from their parent as input, either from the Generator Graph of a root asset or from the Transform Graph output of a parent asset.

Starting from their input points they can do any operation provided by the PCG framework, like duplicate, copy points, sampling and project points. This is particularly useful when placing Child assets.

Executing the placement of all child assets in a hierarchy is achieved using the new **recursive subgraph** feature of PCG in UE 5.4. The process can be described as follows.

For any given set of point, by asset:

-   Run the transform graph over the set of points to duplicate and/or alter their position (the child placement pattern)
    
-   Apply scale/bounds
    
-   Apply Self Pruning (optional)
    
-   Assign Mesh/Material/MeshPropertyOverrides/Assembly/Actor attributes for final asset spawning
    
-   Output the points for spawning
    
-   Resolve potential Child Assets from the current asset
    
-   **Feed resulting points and child assets to the same subgraph**. This is where the recursion takes place, the process will run indefinitely until no child asset, no input/parent point is found or the **Max Child Asset Depth** property of the BiomeCore PCG Graph is reached.
    

In order to control the performance of the recursive generation, a limit is in place to control the number of parent points allowed to emit child points. This limit is controlled by the **Child Input Points Rate Multiplier** property of the Biome Core Graph.

Important to note, an asset can emit multiple child assets at the same level of recursion. When sharing the same parent, child assets distribution is weighted using their weight property.

#### Spawning

Once the points have their final transforms and mesh/actor/assembly attributes they are ready for the Actor and Mesh spawning step.

The spawning step is relatively simple, and comprises the 3 following method that can be used non exclusively:

1.  In case of **Actor** spawning, an actor is spawned for each point, using a SoftClassPath point attribute indicating which actor class to spawn.
    
2.  For **Static Meshes** the Mesh SoftObjectPath attribute is used to specify the mesh to be spawned by each point using ISM Components. A list of property overrides is also supported to apply various StaticMesh component properties per point:
    
    -   bUseDefaultCollision
        
    -   bCastShadow
        
    -   bCastHiddenShadow
        
    -   DetailMode
        
    -   InstanceStartCullDistance and InstanceEndCullDistance
        
    -   WorldPositionOffsetDisableDistance
        
    -   bIncludeInHLOD
        
    -   bVisible
        
    -   bAffectDistanceFieldLighting
        
3.  The **Assembly Instancer** spawning path is used to spawn assemblies or PCG Data Assets (a pre-generated PCG point cloud with mesh attributes to be spawned as a single asset).An extra **Copy Points** step is needed to copy the PCG Data Assets point clouds to their final location before going through the regular Static Mesh Spawner output. Static Mesh property overrides are not yet supported when using this assembly spawning path.
    

#### Output to Biome Core Runtime

The **output to runtime generation** is an optional step that outputs data from the Biome Core graph, to be used by the BiomeCoreRuntime graph, for runtime generation of detailed assets around the camera.

This feature showcases the **graph to graph** communication capabilities of PCG and can be described as follows:

-   PCG Data from the graph is passed through the Output node to be serialized into the BiomeCore PCG Component.
    
-   Other graphs can access this data using a **Get PCG Component Data** node.
    
-   In the case of the BiomeCoreRuntime, the data from the BiomeCore graph/component is accessed at runtime, when BiomeCoreRuntime is executed.
    
-   Multiple data sets can be exported and serialized simultaneously by a graph, using multiple named pins. When accessing the data from a different graph using the **Get PCG Component Data** node, an Expected Pins array must be provided, with pin names matching the Output pin names of the graph providing the data.
    

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56b65bde-dbb7-4c81-a899-177d270fce5a/pcg-biome-reference-image-18.png "PCG Biome Reference")

Data exported from BiomeCore using multiple pins.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4eb0f4e-f320-490f-876e-4c2d967f0b07/pcg-biome-reference-image-19.png "PCG Biome Reference")

And the corresponding Get PCG Component Data node in BiomeCoreRuntime.

BiomeCoreRuntime main features are:

-   Spawning points on the landscape through runtime sampling
    
-   Spawning points on meshes spawned by BiomeCore
    
-   Using BiomeCore points as influences to attract or repulse runtime generated points
    

To support these features, 4 separate point data sets are precomputed by BiomeCore every time it runs, using the **BiomeCore\_PrepareRuntimeData** subgraph:

-   BiomePoints are the points from the BiomeCache, at that point the Biome Cache is updated using the final asset points location and biome color, to account for the Biome Blending jittering process. BiomeCoreRuntime uses the cache to resolve biome information and decide which asset to spawn.
    
-   InfluencePoints are the points from BiomeCore acting as Influences, which uses the **InfluenceType** property under the RuntimeOptions section of the BiomeAsset)
    
-   Instances Points are used as the target location for the meshes that receive runtime details
    
-   Meshes Points are generated in local space using a Mesh Sampler process, which uses the **ExportPoints** property under the RuntimeOptions section of the BiomeAsset.
    

BiomeCache before Biome Blending.

BiomeCache after Biome Blending.

The runtime generation of detailed assets using this data is described in the [BiomeCore Runtime](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#biomecoreruntime) section.

For more information on the runtime hierarchical generation feature of the PCG Framework, see [Runtime Hierarchical Generation](/documentation/404).

#### Injected Data

Injected data in the Biome Core is a term defining external data sent to the system at different key steps to add manual, semi-manual and more artistic control. There are 4 main injected data types: **Exclusions**, **Typed**, **Specific** and **Custom Biome** data. All injected data inputs are contained within the blue comment boxes in the BiomeCore PCG graph. All injected data types have pre-made blueprint classes and can be extended.

##### Exclusions

Binary exclusions from a volume, primitives or spline to remove generated points overlapping those exclusion data. Ideal to isolate an area for manual placement such as POIs, buildings or for specific art/gameplay needs.

The exclusion searches for actors with tags "PCG\_BiomeExclusion" using components tagged with "BiomeExclusion" for volumes, primitives and closed splines or components tagged with "BiomePath" if it's an open spline.

Example:

In the image below preconfigured BP\_PCGBiomeExclusionVolume and Spline were added in the lower right quadrant resulting in empty space. The yellow open spline path is removing trees along the spline volume, based on its control points scale property.

##### Typed Biome Data

Points injected into the pipeline, in parallel with the generators before applying biomes and assets to the points.

These injected points come from manually placed Typed Biome Data actors - a blueprint class with a Generator Type property, a PCG component and PCG graph - outputting points marked with the referenced generator. As these injected points behave as points from a generator, assets assigned to that generator are required in the Biome Assets list. When using shared generators references across multiple biomes/assets, the selected assets to spawn on the Typed point output will vary depending on the biome the actor is placed in.

Example:

A Typed Biome actor using Trees as its Generator Type. A tree spawns at this position, the selected asset is based on the biome definition and biome assets. The resulting spawned mesh/actor will vary automatically depending on the biome.

In the Biome Sample level, if the Typed Biome Data references the Shared\_Trees generator, it can spawn a cactus in the Desert biome, a deciduous tree in the Broadleaf Forest biome or a spruce in the Coniferous biome automatically.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11be662b-ef97-4c0d-8c72-7ebdeb012539/pcg-biome-reference-image-24.png "PCG Biome Reference")

Cactus in Desert biome

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/864e1cea-bab5-4b40-8a32-00aa12bb0251/pcg-biome-reference-image-25.png "PCG Biome Reference")

Deciduous tree in Broadleaf Forest biome

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f7d6682-4a18-4bf9-a183-fa644e12a057/pcg-biome-reference-image-26.png "PCG Biome Reference")

Spruce in Coniferous biome

##### Specific Biome Data

Points injected into the pipeline, alongside the other points after applying biome and assets but before recursive transforms and spawning. They are defined with an Asset set on the Specific Biome Data actors - a blueprint class with an Asset variable, a PCG component and PCG graph - outputting points marked with the specific asset they represent.

The advantage of using specific biome data actors is to precisely control from a PCG graph with a specific logic which assets should spawn and benefit from the data asset structure, transform graph, filtering, spawning from Biome Core in optimized ISM and potentially sent to runtime biome core.

Example:

A Specific actor is set with BirchTree01 Asset. The exact BirchTree01 mesh and recursive child assets will spawn on this point no matter where it is placed, in any biome.

The Biome Sample level has 2 examples, one specific actor spawning a single tree asset and the crop field generator actor. The latter has its own custom PCG graph logic using splines and projection, its own set of asset references assigned to the output points then transformed, filtered and spawned by the Biome Core. It is a separate tool with its output gathered and handled by the Core system.

##### Custom Biome Data

The Custom Biome data is stand-alone with its own independent custom logic and output. Its point data output is injected near the very end of the pipeline just before spawning and output to the Biome Core Runtime. As it is fully custom and stand-alone, it can produce artifacts on its own like spawning meshes while outputting data to the Biome Core to benefit from global spawning. It can also output data for any other graphs non-related to Biome Core. When passing its output to Biome Core for spawning its points, the points must have the attributes required for spawning, mainly the “Mesh” soft object path.

Examples:

-   A custom cavern tool is built from PCG Graph logic, blueprints and a set of variables. The cavern actor must hold its own trigger box, gameplay actors and spawners while all meshes can be spawned by the Biome Core.
    
-   A level instance actor containing a manually created cabin is both an exclusion data for the biome and custom data as it generates surroundings from a set of meshes and actors to be spawned by the Biome Core.
    

## Inputs

### Biome Actors and Setup

Biome Actors are made of blueprint classes available with the Biome Core and are used to set up biomes in a world. This includes Biome Volumes/Splines and Biome Setups actors.

Blueprint classes can be found here:

`/Script/Engine.Blueprint'/PCGBiomeCore/Blueprints/BP_PCGBiomeVolume.BP_PCGBiomeVolume'` `/Script/Engine.Blueprint'/PCGBiomeCore/Blueprints/BP_PCGBiomeSpline.BP_PCGBiomeSpline'` `/Script/Engine.Blueprint'/PCGBiomeCore/Blueprints/BP_PCGBiomeSetup.BP_PCGBiomeSetup'`

#### Biome Volume and Spline

Biome Volume and Spline actors are the easiest way to get started with the Biome Core. Once set up they can be scaled or reshaped (spline), duplicated, instanced throughout the world and exported as child blueprint classes to re-use in multiple worlds while having a single source class to work on.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f526dfd-d8bf-48ef-8507-2d5a2baa84f1/pcg-biome-reference-image-28.png "PCG Biome Reference")

Properties:

1.  **Actor transforms and components**: Actor transforms (position, rotation, scale) are supported. The spline shape can be customized and new control points can be added in the world directly, the spline must remain a closed spline. For volumes, the "BiomeVolume" box collision component can be modified.
    
2.  **Definition**: reference to the Biome Definition data asset to identify the biome this actor represents with a color, name and a priority. It is mandatory to assign the Biome Definition to each biome volume/spline.
    
3.  **Assets array**: reference to the Biome Asset - the list of assets to process and spawn within this biome. As this property is an array, multiple Biome Assets can be added for ease of use and categorization or for sharing the same asset in different biomes. If another biome volume, spline or setup sharing the same definition exists in the world with its Assets array already configured, it is not required to replicate the same list.
    
4.  **Runtime Assets**: reference to the Biome Asset data asset that will be used for this biome within the Biome Core Runtime generation. These are optional and are only needed when using the Biome Core Runtime.
    
5.  **ZExtents**: defines the height of the biome when using a Biome Spline actor. A very large value would mean this biome is applied in 2D across the BiomeCore volume height, while a small value would require the spline to be adjusted against the surface.
    

#### Biome Setup

Biome Setup actors are used to globally define a biome within a world. It is useful when considered as the source of the biome setup - definition + assets - and is required when working with the optional BiomeMap texture projection. They can also be exported to child blueprint classes and re-used in other worlds for a single source of truth and easier world setup.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e15152c8-54ba-42dc-9139-526d78c52a48/pcg-biome-reference-image-29.png "PCG Biome Reference")

Properties:

1.  **Definition**: reference to the Biome Definition data asset to identify the biome this actor represents with a color, name and a priority. It is mandatory to assign the Biome Definition to each biome setup.
    
2.  **Assets array**: reference to the Biome Asset data asset - the list of assets to process and spawn within this biome. As this property is an array, multiple Biome Assets can be added for ease of use and categorization or for sharing the same asset in different biomes. Since the biome setup can be considered as global, biome volumes, splines do not require any assets when paired with biome setup actors referencing the same Biome Definition.
    
3.  **Runtime Assets**: reference to the Biome Asset data asset that will be used for this biome within the Biome Core Runtime generation. These are optional and are only needed when using the Biome Core Runtime.
    

### Biome Definition

Biome Definition Templates are **PrimaryDataAsset** classes inheriting from **BiomeDefinitionTemplate**.

Examples of BiomeDefinitionTemplate and their corresponding structure can be found here:

`/Script/Engine.Blueprint'/PCGBiomeCore/BiomeDefinitions/Setup/BiomeDefinitionTemplate.BiomeDefinitionTemplate'` `/Script/Engine.UserDefinedStruct'/PCGBiomeCore/BiomeDefinitions/Setup/BiomeDefinition.BiomeDefinition'`

It is mandatory to refer to a Biome Definition asset in each Biome Volume/Spline/Setup actor to define which biome they represent.

Base BiomeDefinition Structure properties:

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4288a844-8d0f-4394-9ad2-62bd44d50b12/pcg-biome-reference-image-30.png "PCG Biome Reference")

-   **BiomeName**: Used to identify the biome when debugging and inspecting the Biome Core. Has no actual impact on generation.
    
-   **BiomeColor**: A unique color (RGB) to identify the biome and match generated points to assets entries in the Root Asset Table. Biomes must have a unique color.
    
-   **BiomePriority**: the priority specific to the biome when overlapping biomes are inserted into the biome cache. Lower values mean higher priority.
    

### Biome Assets and Structures

BiomeAsset Templates are **PrimaryDataAsset** classes inheriting from BiomeAssetBaseTemplate. To be compatible with BiomeCore, subclasses of **BiomeAssetBaseTemplate** must provide an **array of structures** named **BiomeAssets**.

Examples of BiomeAssetBaseTemplate and their corresponding structures can be found here:

`/Script/Engine.Blueprint'/PCGBiomeCore/BiomeAssets/Setup/BiomeAssetTemplate.BiomeAssetTemplate'` `/Script/Engine.UserDefinedStruct'/PCGBiomeCore/BiomeAssets/Setup/BiomeAsset.BiomeAsset'`

`/Script/Engine.Blueprint'/PCGBiomeCore/Runtime/BiomeRuntimeAssetTemplate.BiomeRuntimeAssetTemplate'` `/Script/Engine.UserDefinedStruct'/PCGBiomeCore/Runtime/BiomeRuntimeAsset.BiomeRuntimeAsset'`

`(BiomeSample Plugin)` `/Script/Engine.Blueprint'/PCGBiomeSample/BiomeAssets/Setup/BiomeSample_BiomeAssetTemplate.BiomeSample_BiomeAssetTemplate'` `/Script/Engine.UserDefinedStruct'/PCGBiomeSample/BiomeAssets/Setup/BiomeSample_BiomeAsset.BiomeSample_BiomeAsset'`

BiomeAsset structures generally have several substructures used to categorize properties. It is easy to create different types of BiomeAsset Templates, sharing one or more substructures, based on project needs.

Base BiomeAsset Structure properties:

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a7729641-2cca-47f9-8686-2c36b144ac0f/pcg-biome-reference-image-31.png "PCG Biome Reference")

-   **Enabled**: Used to disable an asset without removing it from the assets array.
    
-   **Weight**: When assets sharing a common generator graph are assigned to the generated points, the weight property is used to affect the probability of the asset being chosen.
    
-   **Generator**: reference to a BiomeGenerator asset, used to provide a PCG graph responsible for producing PCG Points.
    
-   **GeneratorSubType**: optional, a comma separated list of generator subtypes used to select the generator output(s) to be used.
    
-   **TransformGraph**: optional, reference to a PCG graph consuming the points from the generator and transforming them before spawning the asset.
    
-   **Mesh**: reference to a Static Mesh asset
    
-   **Assembly**: reference to a PCG Data Asset
    
-   **Actor**: reference to an actor class
    
-   **ChildAssets**: array of BiomeAssets to be spawned as children of this asset. ChildAssets use their Transform Graph to generate their relative position to the parent.
    
-   **DebugOptions**: BiomeAsset\_DebugOptions substructure
    
    -   **Isolate**: when true, only assets that are isolated are spawned
        
    -   **ShowBounds**: draws wireframe bounds of the points associated with the asse
        
-   **AssetOptions**: BiomeAsset\_AssetOptions substructure
    
    -   **OverlapWithChildren**: when false, the point bounds will be used as difference to remove the child assets overlapped by the current asset.
        
    -   **ForceAssetScale**: Applies the scale property to the points regardless of the scale applied by the Transform Graph. Leave false if the scale is to be controlled by the transform graphs.
        
    -   **ExtentsMultiplier**: By default the points bounds are computed from the composed bounds of the asset's Mesh/Actor/Assembly. This property acts as a multiplier over the computed bounds and will affect the results of the differences with points from other generators/ child assets and self pruning operations. Useful for tree assets when the canopy bounds are too large compared to the trunk.
        
    -   **Translation/Rotation/Scale**: Offset applied to the Actor/StaticMesh/Assembly, used to compensate for pivot placement, useful in cases where assets of different size/orientation share the same generator.
        
    -   **OrientUpward**: Progressively blends asset orientation from the generator to Z up. (i.e landscape normal for surface sample based generators)
        
    -   **SelfPrune**: Applies a self pruning operation over the generated points, using the asset computed bounds with the Extents multiplier factor applied, to cleanup overlapping points.
        
    -   **SelfPruningExtentsMultiplier**: an extra multiplier applied to the points extents for self pruning exclusively. Allows for control over the bounds used during the self pruning without affecting other operations using the asset bounds.
        
-   **MeshOptions**: BiomeAsset\_MeshOptions substructure
    
    -   **Material**: Optional, single material applied as an override to the Static Mesh material.
        
    -   **AllowCollision**: When true, the asset will use the collision preset from the Static Mesh. When false, the NoCollision preset is used.
        
    -   *\*Visible*: Translates to the similarly named property of the static mesh component.
        
    -   **CastShadow**: Translates to the similarly named property of the static mesh component.
        
    -   **CastHiddenShadow**: Translates to the similarly named property of the static mesh component.
        
    -   **AffectDistanceFieldLighting**: Translates to the similarly named property of the static mesh component.
        
    -   **DetailMode**: Translates to the similarly named property of the static mesh component. (0 to 3 = Low to Epic)
        
    -   **StartCullDistance/EndCullDistance**: Translates to the similarly named properties of the static mesh component.
        
    -   **WorldPositionOffsetDisableDistance**: Translates to the similarly named property of the static mesh component.
        
    -   **IncludeInHLOD**: Translates to the similarly named property of the static mesh component.
        
-   **AssemblyOptions**: BiomeAsset\_AssemblyOptions substructure
    
    -   **AllowCollision**: When true, the asset will use the collision presets from the Assembly/PCG Data Asset Static Meshes. When false, the NoCollision preset is used.
-   **FilterOptions**: BiomeAsset\_FilterOptions substructure
    
    -   **DensityMin/Max**: Points with Density values outside this range will be discarded.
        
    -   **HeightMin/Max**: Points with Position.Z values outside this range will be discarded.
        
    -   **WaterDistanceMin/Max**: Points Below the water level configured in BiomeFilter\_WaterDistance\_Level\_Inst are considered below the water, a Distance node is used to compute the 3D distance of the points above the water to the closest point below the water. Points within the WaterDistanceMin/Max range will be kept.
        
-   **RuntimeOptions**: BiomeAsset\_RunTimeOptions substructure
    
    -   **ExportPoints**: Enables sampling of the asset's static mesh, and exports the assets locations in world space to generate points at runtime for additional details covering the static mesh.
        
    -   **MeshSamplingRadius**: Controls the number of points generated by the Mesh Sampler
        
    -   **NormalOffset**: Used to remove points generated by the Mesh Sampler based on their normal orientation.
        
    -   **ScaleMultiplier**: Used to scale points generated by the Mesh Sampler
        
    -   **ZMin/ZMax**: Controls the minimum and maximum height range of points generated by the Mesh Sampler.
        
    -   **InfluenceType**: Controls if the asset adds or removes runtime generated details around them.
        
    -   **InfluenceRadius**: Radius around the asset points within which the InfluenceType is applied
        

### Generator

Biome Generator Templates are **PrimaryDataAsset** classes inheriting from **BiomeGeneratorTemplate**.

Examples of BiomeGeneratorTemplate and their corresponding structure can be found here:

`/Script/Engine.Blueprint'/PCGBiomeCore/BiomeGenerators/Setup/BiomeGeneratorTemplate.BiomeGeneratorTemplate'` `/Script/Engine.UserDefinedStruct'/PCGBiomeCore/BiomeGenerators/Setup/BiomeGenerator.BiomeGenerator'`

It is mandatory to refer to a Biome Generator asset in each Biome Asset entry to define which root point data they belong to. Child assets do not require generator reference unless they are used as both root and child assets.

Base BiomeGenerator Structure properties:

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4444c61-ba51-4916-a84a-1a1c43def87b/pcg-biome-reference-image-32.png "PCG Biome Reference")

-   **GeneratorType**: Unique name used to identify the generator. All generators must have a unique name and can be reused in multiple assets of multiple biomes.
    
-   **GeneratorPriority**: the priority used when layering the point data through the Priority Based Difference feedback loop. Lower values mean higher priority. Generators with identical values won't impact each other if overlapping.
    
-   **GeneratorAllowOverlap**: when enabled, the layering process through the Priority Based Difference is completely bypassed. All points produced by the generator will be kept and wont impact any other generator points data during this process.
    
-   **GeneratorGraph**: mandatory PCG Graph or PCG Graph Instance reference which will be executed to produce the root points.
    
-   **GeneratorSpatialNoiseSettings**: an optional SpatialNoiseSettings asset reference exported from a spatial noise PCG node through the PCG graph. When present, this spatial noise setting controls the weighted distribution of assets instead of using the random point seed.
    

### Transform

Transform Graphs are taking points from a generator or parent transformed points as input to alter them before the spawning step.

These graphs are optional for root assets but most of the time are mandatory for child assets, since without a transform graph, a child will spawn at the same location as its parent. Usage of graph instances to parameterize and control the behavior of transform graphs per asset is recommended, but using graphs directly works as well.

A few simple Transform graphs are provided by BiomeCore, the most interesting examples are **BasicSecondaries** and **DuplicatePattern**.

`/Script/PCG.PCGGraph'/PCGBiomeCore/Transforms/BasicSecondaries.BasicSecondaries'` `/Script/PCG.PCGGraph'/PCGBiomeCore/Transforms/DuplicatePattern.DuplicatePattern'`

**BasicSecondaries** creates a few points around each input point and projects them onto the landscape.

The process works as follows:

1.  Get the Input Points.
    
2.  Build a 2D grid of points using a CreatePointsGrid node.
    
3.  Remove the corner points of the grid to make it more circular.
    
4.  Copy the grid to each of the input points using CopyPoints.
    
5.  Randomly remove 50 percent of the copied points.
    
6.  Apply Random transformations to the points.
    
7.  Scale the points based on their distance from the center of each grid.
    
8.  Project the result on the landscape.
    

BasicSecondaries Transform Graph

BasicSecondaries Transform Graph applied to 2 generations of child assets (Red/Green)

**DuplicatePattern** uses the Duplicate Point node to achieve a rotating star shape:

1.  Reset the input points rotation.
    
2.  Duplicate the input points 9 times, rotate each copy by 36 degrees around the z axis.
    
3.  Duplicate each of the 9 copies 10 times, foreach copy, rotate by 10 degrees around Z, translating along the local X axis, and scaling down the point by 80 percent.
    
4.  Project to the landscape.
    

DuplicatePattern TransformGraph

DuplicatePattern Transform Graph applied to 2 generations of child assets (Red/Green)

DuplicatePattern Transform Graph applied to the 1st generation of child Assets (red), BasicSecondaries applied to the second Generation (Green)

### Filters

Root and child points can be filtered from a customizable list of Filters in the BiomeCore\_Filters PCG graph or an instance of it. Each filter entry in the filters array has a FilterGraph, FilterAttribute, FilterRangeMinAttribute and FilterRangeMaxAttribute. Each FilterGraph is processed sequentially from the order they appear in the Filters list through a feedback loop during the BiomeCore execution.

The filter graphs to process are set globally in the BiomeCore graph parameters - **Root Points Filters** and **Child Points Filters**. By default, the Biome Core is set up to use BiomeCore\_Filters\_Inst which filters by Height, Density and WaterDistance.

BiomeCore graph params root and child points filters reference:

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c1a4fbe-7fd4-4c8b-b63e-ac9bea87c11b/pcg-biome-reference-image-38.png "PCG Biome Reference")

BiomeCore\_Filters\_Inst list and properties for each entry:

BiomeCore filters graphs can be located here:

`/Script/PCG.PCGGraph'/PCGBiomeCore/Core/BiomeCore_Filters.BiomeCore_Filters'` `/Script/PCG.PCGGraphInstance'/PCGBiomeCore/Core/BiomeCore_Filters_Inst.BiomeCore_Filters_Inst'`

BiomeSample filters are extended to showcase how to customize the list and include texture projection filters, files can be located here:

`/Script/PCG.PCGGraphInstance'/PCGBiomeSample/Setup/BiomeSample_Filters_Inst.BiomeSample_Filters_Inst'` `/Script/PCG.PCGGraphInstance'/PCGBiomeSample/Filters/BiomeFilter_Flow_Projection.BiomeFilter_Flow_Projection'` `/Script/PCG.PCGGraphInstance'/PCGBiomeSample/Filters/BiomeFilter_SunExposure_Projection.BiomeFilter_SunExposure_Projection'`

The dynamic feedback loop processes over all incoming root and child points data by iterating over the FilterGraphs set in the Filters array. The remaining points left from the current iteration becomes the input of the next, progressively culling points based on asset filter options.

Processing steps:

1.  Incoming point data to process for the current loop iteration. The first iteration starts with all points, then each next iteration receives points remaining from the previous one until all filters have been processed.
    
2.  Dynamic FilterGraph set in the Filters array entries. It is expected to process and write to the set FilterAttribute on all points. This graph is optional when filtering simple point properties such as $Density or $Position but a filter graph can also override these properties if needed (for example, apply a spatial noise as a multiplication over incoming point $Density).
    
3.  Filters points by range using the FilterAttribute within the FilterRangeMinAttribute and FilterRangeMaxAttribute values set in each Asset Filter Options.
    
4.  Outputs all remaining points left after the filtering to the feedback Points output pin. These will be the next iteration's incoming points to work on, or the final output of the filtering process once all iterations have been completed.
    

## Advanced Setup

### Biome Core Graph Parameters

Overview of the global parameters exposed as Graph Parameter Overrides on the BiomeCore PCG Component:

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f830e488-0e9e-4f81-8b7f-1c042e22a6bf/pcg-biome-reference-image-41.png "PCG Biome Reference")

#### Biome Blending Range

Applies a jittering to the points produced by generators before assigning them a biome color from the Biome Cache. This is a global jittering value that is applied on all generated points.

Biome Blending Range value of 0

Biome Blending Range value of 2500

#### Debug Display Biome Cache

Displays a visual representation of the Biome Cache, including biome colors and cache cell size.

#### Biome Cache Cell Size

Configures the cache resolution.

-   Value is in cm.
    
-   Large z values can be used to produce a 2D cache.
    
-   Smaller cell size values will yield more cells and more precise biome definition at the expense of performance.
    

Cache cell size value 3200, 3200, 1024000

Cache cell size value 3200, 3200, 3200

Cache cell size value 800, 800, 1600

#### Max Child Asset Depth

Controls the maximum level of recursion to reach when spawning child assets.

-   A value of 0 will disable child assets spawning entirely.
    
-   Can be used as a performance vs. detail level trade-off when iterating on high level Biome placement or for producing optimized content for different platforms.
    
-   Child Assets can refer to themselves, potentially creating infinite recursion. The Max Child Asset Depth parameter prevents this situation from happening.
    
-   More details in the [Recursion and Transform](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#recursionandtransform) section.
    

Max Child Assets Depth value of 0

Max Child Assets Depth value of 1

Max Child Assets Depth value of 2

#### Child Input Points Rate Multiplier

Limits the number of points allowed to emit child assets.

Child Input Points Rate Multiplier value of 1

Child Input Points Rate Multiplier value of 10

Child Input Points Rate Multiplier value of 100

#### Output Data for Runtime Generation

Enables serialization of BiomeCore graph output data to the BiomeCore PCG component, for use by the BiomeCoreRuntime PCG Graph. Disabled by default for performance, enabled in Biome Sample to showcase BiomeCore Runtime.

-   Also enables sampling of asset meshes used by the BiomeCoreRuntime.
    
-   See the [Spawning and Output to BiomeCore Runtime](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#spawning) sections.
    

#### Bypass Global Filters

Skips the global point filtering step. See the [Filtering](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#filtering). section of this document.

### Biome Texture Projection

As an optional way to layout biomes in a world, a Biome texture can be used and co-exist with Biome Volumes or Splines. As this approach is global to the BiomeCore actor in the world, a Biome Texture Projection Instance graph needs to be assigned to the BiomeCore. For each color in the texture, a Biome Definition using the same color must be provided by Biome Actors in the world.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/74ff29e0-5116-4ebb-b3d2-07b6e924385d/pcg-biome-reference-image-54.png "PCG Biome Reference")

The Biome Sample level showcases this approach. The BiomeSample\_BiomeTextureProj\_Inst has been set up to support textures and 2D texture array projection with different tiling and uv coordinates options.

Biome Core currently requires a landscape for the biome cache initialization to produce cache points that can receive the biome texture data.

Files are located here:

Generic texture projection source graph: `/Script/PCG.PCGGraph'/PCGBiomeCore/Core/BiomeCore_ProjectTexture.BiomeCore_ProjectTexture'`

BiomeSample instance: `/Script/PCG.PCGGraphInstance'/PCGBiomeSample/Setup/BiomeSample_BiomeTextureProj_Inst.BiomeSample_BiomeTextureProj_Inst'`

BiomeSample graph instance properties.

Once set up, the texture on the left is projected on the biome cache points, binding biome definitions to the texture colors.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/779eac3d-a3d8-4917-ba78-86613be0784c/pcg-biome-reference-image-56.png "PCG Biome Reference") ![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01dded6a-162d-42af-aa62-07a2dbd0b2c3/pcg-biome-reference-image-57.png "PCG Biome Reference") ![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6cd7bcbb-c66b-41a2-b36c-f644ec42f912/pcg-biome-reference-image-58.png "PCG Biome Reference")

### Generator SubTypes

Generators have a unique GeneratorType, mapping the assets to the generated points per biome. Generator Graphs can optionally output multiple point data - Generator SubTypes.

Subtypes are useful for multiple use cases and can greatly reduce the amount of Generator Graphs needed to create a rich and complex biome. Any advanced interaction between points of different assets is better handled by generator subtypes as the BiomeCore pipeline does not allow access to points from other generators during the process. The only interaction between different generators point data happens during the Priority based Difference layering.

Use cases examples:

-   Generate points on landscape for trees and create subtypes based on the landscape layer weights, as seen in the images above. This allows landscape paint layers to impact the biome result while using a single generator by distributing assets based on the painting to add overall visual complexity while maintaining simple inputs and less processing.
    
-   Separate points from a single generator to be used by different assemblies or meshes depending on the slope angle.
    
-   Duplicating points within the generator to apply a specific transform to spawn actors such as Niagara systems, sound, decals, or even gameplay items.
    

To help create generator subtypes in generator graphs, a premade PCG subgraph is available in the BiomeCore to filter data based on an attribute and produce two separate outputs. This subgraph can also be chained or used in loops to create more than two separate subtypes.

The premade PCG subgraph is located here:

`/Script/PCG.PCGGraph'/PCGBiomeCore/BiomeGenerators/Graphs/BiomeGenerator_SubGeneratorSetup.BiomeGenerator_SubGeneratorSetup'`

In the following image, the landscape surface is sampled with its layer weights, then subtypes are created for each layer (Land, Mountain, Shore) using the subgraph.

Once the generator graph is outputting subtypes, it is mandatory to specify to which generator subtype(s) the Assets should be assigned using their GeneratorSubType property. An asset can be assigned to multiple subtypes at once using a comma separated list.

In the case of the landscape painting example displayed above, the Broadleaf Forest assets in Biome Sample are assigned different subtypes based on each landscape paint layer. The spruce trees spawn on Shore and Mountain layers while all other assets spawn on Shore and Land, resulting in spruce trees appearing only where the Mountain layer was painted using a single generator.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18a7817a-a5ed-45fc-8ffa-5bdb071f2b1e/pcg-biome-reference-image-62.png "PCG Biome Reference")

### Partitioning and Hierarchical Generation

The BiomeCore PCG Component is non partitioned by default, but the BiomeCore Graph has been built with partitioning in mind.

-   Partitioning can be enabled by toggling on the **Is Partitioned** option on the BiomeCore PCG Component. By default, the generation will be partitioned in chunks of 256x256 meters, according to the PCG World Actor's Partition Grid Size setting.
    
-   Advanced **Hierarchical generation** can be enabled as well, by enabling both **Is Partitioned** on the PCG Component and **Use Hierarchical Generation** option in the BiomeCore PCG graph settings. In that mode, the Biome Cache and Root Asset Table are generated at the Unbounded level (once for the entire world) and the rest of the generation is partitioned in chunks of 256x256 meters, using Grid Size nodes at multiple points in the graph.
    

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26ba89a9-daa2-4c3e-a97f-b58b0319dc13/pcg-biome-reference-image-63.png "PCG Biome Reference") ![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/84278b68-d6b2-4226-92e0-c3e728f105a6/pcg-biome-reference-image-64.png "PCG Biome Reference")

Options used to enable Graph Partitioning and Hierarchical Generation.

Selecting the BP\_PCGBiomeCore PCG Component in the inspection tree view highlights the nodes executed at the Unbounded level.

In editor, enabling Partitioning or Runtime Hierarchical Generation increases the time needed for a full regeneration, but makes partial updates of the biomes faster, such as when manipulating Biome Volumes or Biome Splines in the world.

Partitioning the PCG Component is also recommended when using BiomeCore for producing games using WorldPartition levels, to enable streaming of PCG Partition Actors at runtime.

## BiomeCore Runtime

BiomeCoreRuntime debug display: Points from the Biome Cache as consumed by BiomeCoreRuntime and output points with their biome colors displayed.

### Overview

BiomeCore Runtime is a separate PCG Component and Graph, used for runtime generation of detailed assets around the camera. It consumes data pre-generated by BiomeCore and leverages Runtime Hierarchical Generation to generate a large quantity of PCG Points at runtime.

#### Enabling Runtime Generation

To preview runtime generation in editor, enable the **Treat Editor Viewport as Generation Source** option of the PCGWorldActor:

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb6a6002-0acf-46c6-934c-6e5fcaae314e/pcg-biome-reference-image-67.png "PCG Biome Reference")

Doing so will generate points and spawn assets around the camera. Note that when in a PIE session or cooked build, the player location is automatically used as a runtime generation source.

#### Runtime Assets

Assets used by the runtime generation are a simplified type of Biome Asset, assigned to the BiomeActors such as Setups, Splines and Volumes. Only one runtime asset is currently supported per BiomeActor, containing an array of weighted assets.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bda7aa7-db1e-47d7-afe5-399cd46991f8/pcg-biome-reference-image-68.png "PCG Biome Reference")

MountainForest RuntimeAsset assigned to the MountainForest Biome Setup Actor.

MountainForest RuntimeAsset properties.

#### Runtime Hierarchical Generation Setup

Runtime Hierarchical generation is enabled using the following settings:

In the BiomeCore Runtime Component: the **Generation Trigger** is set to `Generate At Runtime` and the **Is Partitioned** property is set to \`True .

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b605ad62-4ea4-42a5-b8a8-2994c5a0df51/pcg-biome-reference-image-70.png "PCG Biome Reference")

In the BiomeCoreRuntime Graph settings: The **Use Hierarchical Generation** property is set to `true` and the **Higen Default Grid Size** is set to `Unbounded`, meaning that any node placed before a Grid Size node will execute only once, at the unbounded grid level.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7317316-c2f5-4fbc-aa16-f6307e830a13/pcg-biome-reference-image-71.png "PCG Biome Reference")

Also in the Graph Settings, the radius parameter used to control the generation distance is defined per grid size. For Grid Size 400 it is currently set at 1600 cm. Increasing this value will generate details farther away, and increase the number of Runtime Partition Actors to process.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36fff286-d9b5-4458-82f6-d40067a80c45/pcg-biome-reference-image-72.png "PCG Biome Reference")

The hierarchical generation of BiomeCoreRuntime operates at two levels:

-   The **Unbounded level**, for operations that need to happen once for the entire level.
    
-   A grid of runtime partition actors at the **400 cm Grid Size level** for operations that need to be updated frequently around the camera.
    

### Graph Parameters

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/219a4e68-dce0-4554-a34f-e661bc9cd5b6/pcg-biome-reference-image-73.png "PCG Biome Reference")

The two following properties are exposed as Graph Parameters:

-   Biome Blending Range: BiomeCore Runtime supports basic blending of runtime assets. The blending distance is controlled by this parameter.
    
-   Display Points: Used to display points spawned by BiomeCore Runtime and points from the Biome Cache colored using their individual biome color.
    

DisplayPoints option turned on: shows points colored using their associated biome.The biome blending is visible between the red and blue biomes.

### Graph Overview

The description of the data exported by BiomeCore and used as Inputs by BiomeCore Runtime is located here in the [Output to Biome Core Runtime](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#outputtobioemcoreruntime) section of this document.

#### Inputs

-   Meshes Points are produced from sampling BiomeCore asset meshes.
    
-   Instances Points are the target location to place the meshes points in the world.
    
-   InfluencePoints are points from BiomeCore acting as local Influences to increase or reduce the amount of points generated on the landscape.
    
-   BiomePoints are the points from the BiomeCache, representing the biome locations in the world.
    

#### Sampled Meshes Points Placement in Worlds

In the **BiomeCore Runtime CopyPoints Loop subgraph**, Meshes points are copied at their corresponding locations in the world, represented by the instance points. This process is executed in a grid of partition actors, at the **400 cm Grid Size level**.

Red wireframe cubes representing the 400 cm partition actors, Large axis gizmos represent the target Instances points, small gray points are the sampled meshes points copied at each instance point location.

#### Landscape Surface Sampler and BiomeAssets Influence

A surface sampler runs on the landscape surface in each 400 cm partition actor. A spatial noise is applied as density to the result, Influence points are added and subtracted to the final density, depending on their InfluenceType value.

Spruce trees Influence (RemoveGrass)

Cactus trees influence (AddGrass)

Final density value

Final Result

#### Compute Biome Weights and Blending

For each 400 cm partition actor, points from the Biome Cache are gathered within a range specified by the Biome Blending Range.The cache points are partitioned using their color property, the number of points for each individual biome color is used to compute the relative weight of each biome for the partition actor.

The biome colors are distributed to the points generated in each partition actor according to the computed relative weight values.

For instance, if during the first step the biome points gathered around the partition actor represent 3 biomes in a proportion of 33 percent each, the final points generated by the partition actor will respect that proportion, so that 33 percent of them will get assigned to Biome A, 33% to Biome B and 33 percent to Biome C.

Using the Display Points Graph Property: Biome Blending Range Value of 400 cm

Using the Display Points Graph Property: Biome Blending Range Value of 800 cm

Using the Display Points Graph Property: Biome Blending Range Value of 1600 cm

Using the Display Points Graph Property: Biome Blending Range Value of 3200 cm

#### Resolving Biome Assets

Similarly to what is done in the main Biome Core graph, a table of asset properties is built from the Runtime Assets found in the level's Biome Actors. This table contains the assets weight, mesh path, material path, scale and biome color. This part of the graph is generated at the Unbounded grid level, meaning that it's done once instead of per partition actor and that its output is available to all smaller grid levels.

Inspection of the asset table output, processed by the BiomeCoreRuntime Component, at the Unbounded grid level.

Finally, using the points and assets color values, asset properties are added to the points using a Match And Set Attributes node before the final mesh spawning step.

![PCG Biome Reference](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e61f336b-aab7-4a1f-bf38-0700f5a1b4c6/pcg-biome-reference-image-89.png "PCG Biome Reference")

Output of BiomeCore Runtime.