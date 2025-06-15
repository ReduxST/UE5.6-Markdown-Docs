# World Partition Builder Commandlet Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partition-builder-commandlet-reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partition-builder-commandlet-reference)  
**Processed:** 2025-06-14 17:05:03

---

**World Partition** introduces a builder commandlet framework through the **UWorldPartitionBuilderCommandlet** and the **UWorldPartitionBuilder** base class.

These commandlets are used to automate batch processes and generate or modify data in World Partition Levels. Large worlds will not have to be loaded all at once to do things like generating HLODs, AI Nav Data, or resave a large number of Actors.

## World Partition HLODs Builder

HLODs are generated using the **World Partition HLODs Builder** commandlet. Running this commandlet creates the HLOD Actors for your World Partition cells according to the generation settings you specified in your HLOD Layers.

[![](https://dev.epicgames.com/community/api/documentation/image/537014c7-7420-4405-b726-13b1d6b1a869?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/537014c7-7420-4405-b726-13b1d6b1a869?resizing_type=fit)

Command: `UnrealEditor.exe "C:\Users\user.name\Documents\Unreal Projects\MyProject\MyProject.uproject" "/Game/ThirdPersonBP/Maps/OpenWorldTest" -run=WorldPartitionBuilderCommandlet -AllowCommandletRendering -builder=WorldPartitionHLODsBuilder`

For more information about using Hierarchical Levels of Detail (HLODs) in World Partition and using the WorldPartitionHLODsBuilder commandlet, see the [World Partition - Hierarchical Level of Detail](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partition---hierarchical-level-of-detail-in-unreal-engine) documentation.

## World Partition MiniMap Builder

The **World Partition MiniMap Builder** commandlet generates or updates the minimap that displays in the WorldPartition Editor window.

[![](https://dev.epicgames.com/community/api/documentation/image/7d7a5535-2837-4a31-b683-91b63b22ac3d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7d7a5535-2837-4a31-b683-91b63b22ac3d?resizing_type=fit)

Command: `UnrealEditor.exe "C:\Users\user.name\Documents\Unreal Projects\MyProject\MyProject.uproject" "/Game/ThirdPersonBP/Maps/OpenWorldTest" -run=WorldPartitionBuilderCommandlet -AllowCommandletRendering -builder=WorldPartitionMiniMapBuilder`

## World Partition Rename Duplicate Builder

The **World Partition Rename Duplicate Builder** commandlet automates the process of renaming or duplicating an existing World Partition Level and all its actors.

[![](https://dev.epicgames.com/community/api/documentation/image/0ec62a45-95ad-4eec-a248-c24dba10a1bf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0ec62a45-95ad-4eec-a248-c24dba10a1bf?resizing_type=fit)

Command: `UnrealEditor.exe "C:\Users\user.name\Documents\Unreal Projects\MyProject\MyProject.uproject" "/Game/ThirdPersonBP/Maps/OpenWorldTest" -run=WorldPartitionBuilderCommandlet -SCCProvider=None -builder=WorldPartitionRenameDuplicateBuilder -NewPackage=/Game/ThirdPersonBP/Maps/NewPackage`

This will create a duplicate World Partition Level of the **OpenWorldTest** map named **NewPackage** and leave the original map untouched.

To rename your World Partition map rather than make a copy, add the `-Rename` argument.

## World Partition Resave Actors Builder

The **World Partition Resave Actors Builder** commandlet resaves all Actors of a World Partition Level and supports a class filter to resave only a subset of Actors.

[![](https://dev.epicgames.com/community/api/documentation/image/60a6118d-5d44-4f3c-95d3-f037c13c8443?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/60a6118d-5d44-4f3c-95d3-f037c13c8443?resizing_type=fit)

Command: `UnrealEditor.exe "C:\Users\user.name\Documents\Unreal Projects\MyProject\MyProject.uproject" "/Game/ThirdPersonBP/Maps/OpenWorldTest" -run=WorldPartitionBuilderCommandlet -SCCProvider=None -builder=WorldPartitionResaveActorsBuilder`

When you execute the above example, all of the Actor's packages in the OpenWorldTest level are resaved.

You can use the `-ActorClass` argument to specify only a subset of Actors to be resaved. For example, adding `-ActorClass=StaticMeshActor` will resave only the Static Mesh Actors in the specified Level.

## World Partition Foliage Builder

In a World Partition map, the default Instanced Foliage Grid Size for Foliage Instances is 256 meters. The **World Partition Foliage Builder** commandlet is used to change the Instanced Foliage Grid Size for existing World Partition level.

[![](https://dev.epicgames.com/community/api/documentation/image/a1a4085f-2876-4b9b-9c0e-c14d26bcafc8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a1a4085f-2876-4b9b-9c0e-c14d26bcafc8?resizing_type=fit)

Command: `UnrealEditor.exe QAGame Playground.umap -run=WorldPartitionBuilderCommandlet -Builder=WorldPartitionFoliageBuilder -NewGridSize=Value`

For more information on using Foliage Mode with World Partition, see the [Foliage Mode](building-virtual-worlds/open-world-tools/foliage-mode) documentation.

## World Partition Navigation Data Builder

The **World Partition Navigation Data Builder** commandlet rebuilds the navmesh in your World Partition Level.

[![](https://dev.epicgames.com/community/api/documentation/image/da8f9db3-b787-4776-8b04-ad55bcda2bd3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/da8f9db3-b787-4776-8b04-ad55bcda2bd3?resizing_type=fit)

Command: `UnrealEditor.exe "C:\Users\user.name\Documents\Unreal Projects\MyProject\MyProject.uproject" "/Game/ThirdPersonBP/Maps/OpenWorldTest" -run=WorldPartitionBuilderCommandlet -AllowCommandletRendering -builder=WorldPartitionNavigationDataBuilder -SCCProvider=None`

This commandlet takes the following arguments:

| Optional Argument | Description |
| --- | --- |
| 
**\-SCCProvider**

 | 

Specifies which source control provider to use. To run without source control, specify `-SCCProvider=None`.

 |
| 

**\-Verbose**

 | 

Displays verbose logging.

 |
| 

**\-Log**

 | 

Outputs log to a specific file.

 |
| 

**\-CleanPackages**

 | 

Wipes all navigation data packages instead of building them.

 |

## World Partition Smart Object Collection Builder

The World Partition Smart Object Collection Builder commandlet rebuilds the smart object collection from all the smart object components in your World Partition Level.

[![](https://dev.epicgames.com/community/api/documentation/image/11c6ad85-fa39-4f31-8920-6246f9f691fe?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/11c6ad85-fa39-4f31-8920-6246f9f691fe?resizing_type=fit)

Command: `UnrealEditor.exe "C:\Users\user.name\Documents\Unreal Projects\MyProject\MyProject.uproject" "/Game/ThirdPersonBP/Maps/OpenWorldTest" -run=WorldPartitionBuilderCommandlet -builder=WorldPartitionSmartObjectCollectionBuilder`

When you execute the above example, all of the Smart Object Collection in the OpenWorldTest level are rebuilt. You can use the `-SCCProvider` argument with this commandlet to specify which source control provider to use.

## World Partition PCG Builder

The **World Partition PCG Builder** commandlet loads the level completely, waits for async processes to complete such as static mesh builds, then schedules generation on matching PCG components. When all generation is complete the process saves the World Partition level and exits.

[![](https://dev.epicgames.com/community/api/documentation/image/985b6069-74e6-4761-8167-23a23e410709?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/985b6069-74e6-4761-8167-23a23e410709?resizing_type=fit)

Command Line: `UnrealEditor.exe "C:\Users\user.name\Documents\Unreal Projects\MyProject\MyProject.uproject" "/Game/ThirdPersonBP/Maps/OpenWorldTest" -Unattended -AllowCommandletRendering -run=WorldPartitionBuilderCommandlet -Builder=PCGWorldPartitionBuilder -IncludeGraphNames=PCG_GraphA;PCG_GraphB`

Console Command: `pcg.BuildComponents -IncludeGraphNames=PCG_GraphA;PCG_GraphB`

This commandlet takes the following arguments:

| Optional Argument | Description |
| --- | --- |
| 
**\-IncludeGraphNames**

 | 

Includes a list of graph names in the generation, separated by `;`. If provided, the system will schedule generation of all PCG components with the first graph assigned, then the same for the second graph, and so on. If omitted then PCG components will not be filtered by graph.

 |
| 

**\-GenerateComponentEditingModeLoadAsPreview**

 | 

Components that are saved with the Editor Mode **Load As Preview** will be considered for generation when this argument is used.

 |
| 

**\-GenerateComponentEditingModeNormal**

 | 

Generates components with Editing Mode set to **Normal**. By default only components that are saved with the Editing Mode **Load As Preview** are generated.

 |
| 

**\-GenerateComponentEditingModePreview**

 | 

Generates components with Editing Mode set to **Preview**. By default only components that are saved with the Editing Mode **Load As Preview** are generated.

 |
| 

**\-IgnoreGenerationErrors**

 | 

Submits the result to source control, regardless of errors (but the errors are still reported and the job status will still be Failed). This can be used to keep the job online even in the presence of errors, but should be used with caution. By default, any error that occurs while a component is generating will be registered with the builder and will fail the build job, and the results will not be submitted.

 |
| 

**\-IncludeActorIDs**

 | 

Includes a list of unique actor IDs separated by `;`. If provided only PCG components on matching actors will be generated. Particularly useful for debugging a single component/actor.

 |
| 

**\-OneComponentAtATime**

 | 

Schedules generation of one component at a time and wait for each generation to finish before scheduling a new component. Useful while debugging to ensure async processes are not interfering with each other.

 |
| 

**\-PCGBuilderSettings**

 | 

Specifies a **PCGBuilderSettings** asset to use when setting up the builder commandlet. All commandlet arguments override the arguments set in the PCGBuilderSettings asset.

 |
| 

**\-IterativeCellLoading**

 | 

Processes the world using a specific cell size to avoid loading everything at once. Loaded components generate and save. They are then unloaded and the builder moves to a different cell. This is useful for large worlds where loading the whole world causes memory issues.

 |
| 

**\-IterativeCellSize**

 | 

Overrides the default cell size when using **IterativeCellLoading**. Default is `25600`.

 |
| 

**\-Unattended**

 | 

Avoids initializing the Editor UI, runs in console instead.

 |
| 

**\-AllowCommandletRendering**

 | 

Initializes rendering subsystem. Useful because PCG has some functionality that utilizes the GPU.

 |
| 

**\-AutoSubmit**

 | 

Attempts to submit the result to source control, if available.

 |
| 

**\-AssetGatherAll**

 | 

Builds the full asset registry for all assets in the project. Required if the builder needs to access assets not referenced in the level.

 |