# PCG Biome Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-quick-start-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-quick-start-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:31

---

The PCG Biome Core and Sample Plugins are examples of how to use the [PCG Framework](/documentation/en-us/unreal-engine/procedural-content-generation-overview) with features like Attribute Set Tables, Feedback loops, Recursive Sub-graphs and [Runtime Hierarchical Generation](/documentation/404).

## Base Requirements

This section covers the base requirements and all steps required to get the PCG Biome Core working in a world.

## Enabling Plugins

The PCG Biome Core and Sample are two distinct plugins. The PCG Biome Core plugin is stand alone, only contains what is required for the biome creation tool to work and has a dependency on the PCG Framework and PCG Geometry Script Interop plugins. The PCG Biome Sample plugin is a content example showcasing the biome creation tool, it can be enabled in any project and has a dependency on the PCG Biome Core plugin.

To enable the plugins, open the Plugins settings and enable the PCG Biome Core to access the tool or alternatively enable the PCG Biome Sample to access both the tool and the content example. For more information on enabling plugins, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

## Resources

To access all the content related to both PCG Biome Core and Sample plugins, the **Show Engine Content** and **Show Plugin Content** content browser settings must be enabled. Open the **Settings** menu in the **Content Browser** and click the checkbox next to both options.

![PCG Biome Quick Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2fad55e-6beb-45b8-b4b7-dc9fb70c9f66/pcg-biome-quick-start-image-18.png "PCG Biome Quick Start") ![PCG Biome Quick Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08e0abeb-22c6-47b2-a190-6bb05726f5f6/pcg-biome-quick-start-image-2.png "PCG Biome Quick Start")

Content Browser paths:

`/All/EngineData/Plugins/PCGBiomeCore`

`/All/EngineData/Plugins/PCGBiomeSample`

Disk paths:

`..\Engine\Plugins\Experimental\PCGBiomeCore\`

`..\Engine\Plugins\Experimental\PCGBiomeSample\`

### PCG Biome Core Content

All the base blueprint classes are located in: `/All/EngineData/Plugins/PCGBiomeCore/Blueprints`

The **BP\_PCGBiomeCore** is the main blueprint class pre configured with a PCG Component that refers to the BiomeCore PCG graph and holds a Box Collision component as its Volume.

The BiomeCore PCG Graph located at the plugin's root is the source and main graph to execute all logic for the Biome Core to work. It contains multiple subgraphs with their own nested subgraphs. All of these separate subgraphs are stored under the "Core" folder.

BiomeCore Graph: `/Script/PCG.PCGGraph'/PCGBiomeCore/BiomeCore.BiomeCore'`

The tool relies on multiple **Data Assets**, pre-made classes with specific structures to generate content. Those assets are **BiomeDefinitions**, **BiomeAssets** and **BiomeGenerators**. They are located in their respective folders and `../Setup` sub-folders. The default assets of each type are also available for testing and debugging.

### PCG Biome Sample Content

The **BiomeSampleLevel** world is located in: `/All/EngineData/Plugins/PCGBiomeSample/Maps`

The world contains the pre-configured BP\_PCGBiomeCore, Biome Setup, Volume and Spline actors making it the best starting point to learn how to set up the tool and understand it.

The Sample contains multiple Biomes, Generators and Assets as well as custom structures and data assets classes inheriting from the base Biome Core classes. All in their respective BiomeSample folders and `../Setup` sub-folders.

Additionally, the PCG Biome Sample plugin contains extra data including a BiomeMap texture, tiled Flow and SunExposure texture2Darray located in the Tiles folder as well as example PCG assemblies, meshes and filter graph instances.

## World Setup

This is a step by step quick start guide to use the biome creation tool from scratch followed by instructions on how to add new biomes and assets.

1.  Create a new level or open an existing world. The PCG Biome Core works with [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) using partitioned and non-partitioned levels.
    
2.  Add a new Landscape of the desired world scale through the Landscape Editor mode. If starting from the Open World template or any existing level with an existing landscape, no action is required.
    
    The presence of a landscape is **optional** when working with the PCG Biome Core.
    
3.  Add OR drag and drop a **BP\_PCGBiomeCore** actor to the level. The provided BP\_PCGBiomeCore blueprint class is located here: `/Script/Engine.Blueprint'/PCGBiomeCore/Blueprints/BP_PCGBiomeCore.BP_PCGBiomeCore'`
    
4.  Adjust the BP\_PCGBiomeCore actor's Volume component scale to the desired world coverage. The tool uses this volume to constrain its generation and output. For best performances, the volume should be carefully adjusted to fit the landscape or environment including height. The default scale is 1024 x 1024 x 256 meters.
    
5.  Select the "**BiomeCore**" PCG component of the **BP\_PCGBiomeCore** actor in the level and click on **Generate** to initialize the generated state for live updates. At this stage, it is normal for nothing to appear in the level.
    

Before continuing to setting up the [Biomes, Generators and Assets](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-quick-start-guide-in-unreal-engine#biomes,generatorsandassetssetup), validate the previous steps with the following:

-   Add OR drag and drop a **DefaultBiomeVolume/Spline actor** within the BP\_BiomeCore volume.
    
    **Expected result:** An automatic refresh will occur and debug cubes meshes will be spawned on the landscape surface constrained within the DefaultBiomeVolume/Spline and BiomeCore volume.
    
    If no refresh occurred or no debug cube spawned, verify that the BiomeCore PCG component was triggered once using the **Generate** button (step 5 above), that the DefaultBiomeVolume/Spline actor resides inside the BiomeCore volume and overlaps the landscape surface.
    
-   After adding the DefaultBiomeVolume/Spline, the Biome Cache debug display can be enabled to validate the biome coverage and creation. The BiomeCore PCG component contains all global parameters. To view the biome cache, override and enable the "**Debug - Display Biome Cache**" option. For more information about the biome cache, see [Biome Cache](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#biomecache).
    
    **Expected result:** An automatic refresh will occur to display the cache voxels. The default undefined biome color is black and the preconfigured DefaultBiomeVolume/Spline actor biome color is white. White cache voxels should appear where the DefaultBiomeVolume/Spline has been placed.
    
    If the biome cache is not displayed, make sure the BiomeCore PCG component was triggered once using the **Generate** button (step 5 above) and that the option is overridden and enabled on the Biome Core PCG component. If the entire cache is colored black, move the DefaultBiomeVolume/Spline actor inside the BiomeCore volume.
    
-   Remove the DefaultBiomeVolume/Spline from the world after validating that the BiomeCore is working as expected.
    

## Biomes, Generators and Assets Setup

Once the original world setup is done and validated, proceed with the following steps to create a new biome with its definition and assets:

1.  Add OR drag and drop a new **BP\_PCGBiomeVolume** or **BP\_PCGBiomeSpline** actor in the world within the Biome Core actor volume and overlapping the landscape surface. The blueprint classes are available here:
    
    BP\_PCGBiomeVolume: `/Script/Engine.Blueprint'/PCGBiomeCore/Blueprints/BP_PCGBiomeVolume.BP_PCGBiomeVolume'`
    
    BP\_PCGBiomeSpline: `/Script/Engine.Blueprint'/PCGBiomeCore/Blueprints/BP_PCGBiomeSpline.BP_PCGBiomeSpline'`
    
2.  Create a set of new Data Assets for Biome Definitions, Generators and Assets. Data Assets can be added from content browser ADD button, through right click menu - data asset OR duplicated from existing assets of the same class.
    
3.  **Biome Definition:** Add a new Data Assets in the project's content folder of **class BiomeDefinitionTemplate** and set its **BiomeName**, **BiomeColor**, **BiomePriority** properties.
    
    These properties define your biome, the definition asset can be shared and re-used in multiple biome volumes and spline, in a world or across multiple worlds but its settings must be unique compared to other Biome Definitions assets. The BiomeColor will be displayed when enabling the debug display for the Biome Cache.
    
    ![PCG Biome Quick Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5843c452-a87f-4f6d-b950-536f31f4313a/pcg-biome-quick-start-image-9.png "PCG Biome Quick Start")
    
    To learn more about Biome Definitions, see [Biome Definition](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#biomedefinition).
    
4.  **Biome Generator:** Add a new Data Assets in the project's content folder of **class BiomeGeneratorTemplate** and set its **GeneratorType**, **GeneratorPriority** and **GeneratorGraph** properties.
    
    These properties define your generator, the generator asset can and should be shared and re-used in multiple assets, it provides the initial point data from the linked GeneratorGraph PCG Graph on which to assign assets and spawn.
    
    ![PCG Biome Quick Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab219843-930d-4676-a792-8e5ff33acde3/pcg-biome-quick-start-image-10.png "PCG Biome Quick Start")
    
    The **GeneratorGraph** is a PCG Graph OR PCG Graph Instance which outputs its point data created by sampling the world, landscape or any desired logic. To get started copy the **BiomeGenerator\_Template** graph here:
    
    `/Script/PCG.PCGGraph'/PCGBiomeCore/BiomeGenerators/Graphs/BiomeGenerator_Template.BiomeGenerator_Template'`
    
    To learn more about biome generators, see [Generator](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#generator).
    
5.  **Biome Asset:** Add a new Data Assets in the project's content folder of **class BiomeAssetTemplate** then add a new biome asset array entry and set its **Generator**, a mandatory reference to the biome generator data asset created above and a Mesh, the visual to spawn.
    
    The biome assets array is the collection of assets to process and spawn. Each entry contains multiple properties to configure and assets sharing the same generator reference are distributed randomly on to the generated points. The biome asset list can also be shared and re-used in multiple biomes.
    
    ![PCG Biome Quick Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6135ec76-0da1-4711-a76b-ff32199fd29b/pcg-biome-quick-start-image-12.png "PCG Biome Quick Start")
    
    To learn more about Biome Assets, see [Biome Assets and Structures](/documentation/en-us/unreal-engine/procedural-content-generation-pcg-biome-core-and-sample-plugins-reference-guide-in-unreal-engine#biomeassetsandstructures).
    
6.  Assign the Biome Definition and Asset for the BP\_PCGBiomeVolume added to the world in step 1.
    
    ![PCG Biome Quick Start](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f56fb09d-8991-4a98-ae2f-49f05ff4d82d/pcg-biome-quick-start-image-13.png "PCG Biome Quick Start")

Following these steps, an automatic refresh will occur and a new biome constrained within the BP\_PCGBiomeVolume and the Biome Core Volume will spawn the defined asset(s).

Once this initial configuration is done, the biome can be extended with more generators and assets. Any number of biomes can be created using the same process and co-exist within the same world or across multiple worlds, refer to the BiomeSampleLevel within the PCGBiomeSample plugin for a complete setup.

In this image, the biome has been configured with multiple assets referencing and sharing only 2 custom generators, one for trees and one for rocks.

After adding several more biomes of higher priority with their respective assets using overlapping BP\_PCGBiomeSpline actors and a 64m biome blending range.