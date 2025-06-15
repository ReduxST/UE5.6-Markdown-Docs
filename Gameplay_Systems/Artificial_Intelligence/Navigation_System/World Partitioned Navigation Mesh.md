# World Partitioned Navigation Mesh

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partitioned-navigation-mesh](https://dev.epicgames.com/documentation/en-us/unreal-engine/world-partitioned-navigation-mesh)  
**Processed:** 2025-06-14 17:05:07

---

## Overview

This document provides an overview of how to use a world-partitioned **Navigation Mesh** with Unreal Engine's **World Partition** system.

World Partition is an automatic data management and distance-based level streaming system that provides a complete solution for large world management. The system removes the need to divide large levels into sublevels by storing your world in a single persistent level separated into grid cells, and provides an automatic streaming system to load and unload those cells based on distance from a streaming source.

Learn more about the system by reading the [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) documentation.

## World-Partitioned Navigation Mesh

A World Partition Navmesh is split into several Navmesh chunk Actors that are loaded / unloaded like other world partitioned resources.

A World Partition Navmesh only makes sense in the context of a world partitioned map. To convert a map so it uses World Partition, refer to the [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) documentation.

Alternatively, you can create a world partitioned map by creating a new Level and selecting the Open World template.

## Runtime Generation

World Partition Navigation Meshes support all available generation modes: **Static**, **Dynamic Modifiers Only**, and **Dynamic**.

## Dynamic Modes

When using the Dynamic generation mode, the Navmesh tile generation will occur at runtime. However, navigation dirtiness (the need to rebuild the navigation) is ignored for objects that are loaded and unloaded which are part of the base Navmesh (see below). This prevents excessive dirtiness as a result of the loading and unloading of the world.

Dynamic tile building is limited to the loaded space when using a World Partition Dynamic Navmesh.

## Base Navigation Mesh and Data Layers

All runtime navigation generation modes use a **Base Navmesh**. This refers to the initial Navmesh that gets loaded via streaming as cells are loaded.

In Static mode, this Navmesh will not change. However, in the Dynamic modes, spawned Actors that are relevant to the navigation will dirty the Base Navmesh and trigger the rebuilding of navigation tiles.

### What is included in the Base Navmesh?

Navigation-relevant objects outside of Data Layers will be included in the Base Navmesh (i.e. baked in the initial Navmesh). In addition, any objects in editor Data Layers are also included.

Finally, any layers (including runtime Data Layers) in the Base Navmesh Data Layers list will also be considered in the Base Navmesh.

Learn more about World Partition Data Layers by reading the [Data Layers](/documentation/en-us/unreal-engine/world-partition---data-layers-in-unreal-engine) documentation.

## External Packaging

When building a World Partitioned Navmesh, the navigation data actor (ANavigationData) is externally packaged. This means that building a World Partitioned Navmesh does not dirty the main map.

For more information on external packaging see the [One File Per Actor](/documentation/en-us/unreal-engine/one-file-per-actor-in-unreal-engine) documentation.

## Create a World Partitioned Navigation Mesh

### 1 - Required Setup

1.  Create a new project from a template in the **Games** category. In this example, we selected the **Third Person** template.
    
    ![Create a new project](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aad401eb-52ee-4222-9d7e-6532f1d1a681/wp-navmesh-1.png)
2.  In the editor, click **File > New Level**. Select the **Open World** map type and click **Create**. Save the level.
    
    ![Create a new Open World level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8005f0e-bc42-4f2e-8cce-6eb4de0dc0b0/wp-navmesh-2.png)
    
    The Open World default map type is designed as a starting point for creating large open-world maps and has the following features enabled by default:
    
    -   World Partition
    -   One File Per Actor
    -   Data Layers
    -   Hierarchical Levels of Detail
3.  Go to the **World Settings** window and scroll down to the **World Partition** section.
    
    1.  Expand **Runtime Settings > Grids > Index \[0\]**.
        
    2.  Change the **Loading Range** value to **12800**. The smaller value will make it easier to visualize when the Navigation Mesh is loaded by World Partition.
        
    
    ![Create a new Open World level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/141cd89b-360c-4cbb-bc2d-4109f46801a7/wp-navmesh-2b.png)

#### Section Results

In this section, you created a new project with a level set up to use World Partition. In the next section, you will configure a Navigation Mesh so it works with World Partition.

### 2 - Configuring the Navigation Mesh to use World Partition

1.  Click **Settings > Project Settings** to open the **Project Settings** window.
    
    ![Click Settings > Project Settings to open the Project Settings window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ad7a46b-3756-4820-87af-c79a077fd50d/wp-navmesh-3.png)
2.  Click the **Navigation Mesh** category and scroll down to the **Runtime** section. Click the **Runtime Generation** dropdown and select **Static**.
    
    ![Click the Runtime Generation dropdown and select Static](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04f5de1b-4917-4817-bae3-0e1f6927337b/wp-navmesh-4.png)
3.  If your project has large worlds, you can limit memory utilization by going to the **Generation** section and enabling the **Fixed Tile Pool Size** checkbox, and adjusting the **Tile Pool Size**. The pool size will limit the memory size utilized by the Navigation Mesh.
    
    The number of tiles in the pool must be large enough to allow you to add: *The maximum number of tiles required to load the Navmesh Actors in the loading bubble at runtime.* The maximum number of tiles you want to visualize in the editor when loading parts of the world partitioned map.
    
    ![Click the Runtime Generation dropdown and select Static](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4625431-14a7-45d0-a970-218141906e2b/wp-navmesh-4a.png)
4.  Click **Add + > Volumes > NavMeshBoundsVolume** to add a **Navigation Mesh** volume actor to your level.
    
    ![Add a Navigation Mesh volume actor to your level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24468c77-d3b4-46bf-aca8-1956f41d186e/wp-navmesh-5.png)
5.  Select the **NavMeshBoundsVolume** actor in the **Outliner** window and go to the **Details** panel.
    
    1.  **Scale** the actor so it covers the playable space in the level.
        
    2.  Press **P** to see the navigation being built in the viewport.
        
    
    ![Select the NavMeshBoundsVolume actor in the Outliner window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a59f71be-9219-4f0e-b17f-004eda9d4561/wp-navmesh-6.png) ![Press P to see the navigation being built in the viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81c84850-3900-4b78-b600-f2de65ed684f/wp-navmesh-7.png)
6.  Select the **RecastNavMesh-Default** actor in the **Outliner** window and go to the **Details** panel. Scroll down to the **Generation** section and **enable** the **Is World Partitioned Navmesh** checkbox.
    
    ![Select the RecastNavMesh-Default actor in the Outliner window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6811ba74-09d8-4e07-afba-69416da9d27b/wp-navmesh-8.png) ![Enable the Is World Partitioned checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/33c42247-c513-4548-a3d7-9817c4119ddc/wp-navmesh-9.png)

#### Section Results

In this section, you added a Navigation Mesh Bounds volume to your level. You also configured the Navigation mesh to work with World Partition.

In the next section you will configure the editor to improve your workflow.

### 3 - Configuring the Editor

Since you are most likely working on a really big level, it is recommended that you disable automatic Navigation Mesh generation to improve your workflow.

To do so, follow these steps:

1.  Click **Edit > Editor Preferences** to open the **Preferences** window.
    
    ![Click Edit - Editor Preferences to open the Preferences window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0874a5a5-371a-48e5-b25a-c5582bed26a6/wp-navmesh-10.png)
2.  Scroll down to the **Level Editor** section and click the **Miscellaneous** category. Scroll down to the **Editing** category and disable the **Update Navigation Automatically** checkbox.
    
    ![Disable the Update Navigation Automatically checkbox](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2db5e1a-46d2-4f7f-b75d-26ff81fa2732/wp-navmesh-11.png)

#### Section Results

In this section, you configured your Navigation Mesh so it does not update automatically. This generally improves your workflow as you work with large worlds using World Partition.

In the next section, you will build the Navigation Mesh in your level.

### 4 - Building the Navigation Mesh

When working with a world partitioned map, some assets are usually loaded while others are unloaded. Because of this, building the entire Navigation Mesh requires a different process.

To build the Navigation Mesh in your level, follow these steps:

1.  Enter the following console command in the command line and press **Enter**: **n.bNavmeshAllowPartitionedBuildingFromEditor 1**
    
    ![Enter the command n.bNavmeshAllowPartitionedBuildingFromEditor 1](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a721613f-97f0-43b5-9d02-b6811a9493f3/wp-navmesh-12.png)
2.  Click **Build > Build Paths** to build the Navigation Mesh in your level.
    
    ![Click Build - Build Paths to build the Navigation Mesh in your level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71061b41-8a55-4cca-ada4-c6aa4ddf255d/wp-navmesh-13.png)
3.  In the **Build Navigation Settings** window, click **Ok** to build the Navigation Mesh. You also have the following options available:
    
    1.  **Verbose** \- Enable this checkbox if you want to see a more detailed log of the build process. You can find the output log named **WPNavigationBuilderLog.txt** in the **Saved > Logs** directory of your project.
        
    2.  **Clean Packages** - Enable this if you want to remove all world partitioned NavMesh actor packages from your project. This will not build the navigation.
        
    
    ![Build Navigation Settings options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d060622b-26c0-43f9-9cd7-2f130ada560c/wp-navmesh-14.png)
4.  Go to the **Outliner** window and notice that you now have four **NavDataChunk** Actors. These actors hold the navigation data loaded and unloaded by World Partition. The number of NavDataChunk Actors created depends on the size of the Data Chunk Grid (see section 6 for more details).
    
    ![Go to the Outliner window and notice that you now have four NavDataChunk Actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22dfcb4f-12f4-4c5e-ac1b-854fb0e246c3/wp-navmesh-14b.png)

#### Section Results

In this section, you learned how to build the navigation for your level. You also learned about the different Navigation Settings options and how NavDataChunk actors are created in your level.

In the next section, you will learn how to build navigation outside of the editor.

### 5 - Building the Navigation Mesh with the World Partition Navigation Data Builder

It is also possible to build a world partitioned static Navigation Mesh outside the editor by using the **WorldPartitionBuilderCommandlet** with the **WorldPartitionNavigationDataBuilder**.

Follow the instructions in the [World Partition](/documentation/en-us/unreal-engine/world-partition-in-unreal-engine) documentation, under the **World Partition Navigation Data Builder** section to learn how to do this.

### 6 - Additional settings for your Navigation Mesh

1.  Go to the **World Settings** window and scroll down to the **Navigation** section to find the **Navigation Mesh** settings for the level.
    
    The options are as follows:
    
    | Setting | Description |
    | --- | --- |
    | Navigation Data Chunk Grid Size | This defines the size of the data chunk actors loaded with each cell of World Partition. The smaller the number, the more granular the data. |
    | Navigation Data Builder Loading Cell Size | This defines the size of the loading cells used to load the Navigation data into memory. |
    
    Set the **Navigation Data Chunk Grid Size** to **25600**. This lower value better shows how the Navigation Mesh is loaded and unloaded by World Partition. This value should be adjusted based on your gameplay needs, loading range, and required granularity.
    
    ![Set the Navigation Data Chunk Grid Size to 25600](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/948667b4-fc8b-4321-a4eb-9c9807ef23fe/wp-navmesh-15.png)
2.  Click **Build > Build Paths** to build the Navigation Mesh in your level.
    
3.  Go to the **Outliner** window and notice that you have many more **NavDataChunk** actors in the level. This is expected as the Chunk Grid Size is smaller than before.
    
    ![There are many more NavDataChunk** **actors in the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea1cb7b7-f87f-41bb-9816-31e6738f2922/wp-navmesh-16.png)

#### Section Results

In this section, you learned how to change the Navigation Data Chunk Grid Size and how it affects the number of NavDataChunk actors that are created in your level.

In the next section, you will see how the Navigation Mesh is loaded and unloaded as the player traverses the level.

### 7 - World Partition Settings

In addition to the Navigation Mesh settings, you can also use the following World Partition settings to set up your map.

#### Use the Partition Actor Bounds

To set the Partition Actor to use its **bounds** (instead of its location) when checking if it should be loaded, follow these steps:

-   Go to the **World Settings** panel and scroll down to the **Runtime Settings** section.
-   Expand the **Advanced** options and click the **Place Partition Actors Using Location** dropdown.
-   Select **Disabled**.

![Click the Place Partition Actors Using Location dropdown and select Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5d220ca-4af0-4a08-95b4-5963046c8d6e/wp-navmesh-21.png)

This might be useful when using large landscape tiles with a small loading radius.

#### Force Garbage Collection

To force Garbage Collection after the level is streamed out, use the console command **LevelStreaming.ShouldReuseUnloadedButStillAroundLevels 0**.

This will remove the Navigation Actors that have been unloaded by World Partition. Otherwise, it might take some time for the unloaded Actors to be collected.

### 8 - Viewing your results

Follow these steps to view how the Navigation Mesh is loaded and unloaded with the World Partition cells.

1.  Enter the following Navigation Mesh Gameplay Debugger console commands in the command line and press **Enter**:
    
    1.  **ai.debug.nav.RefreshInterval 0.3**
        
    2.  **ai.debug.nav.DisplaySize 100**
        
    
    These commands adjust the display size and how frequently the Navigation Mesh visualization is updated.
    
    ![Enter the ai.debug.nav.DisplaySize 100 command](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9d59657-64ca-4ba9-9f8b-46d2a4a484b7/wp-navmesh-17.png)
2.  Press **Play** to start the game. Open the command line by pressing **tilde (~),** then enter the following World Partition debug commands:
    
    1.  **wp.Runtime.ToggleDrawRuntimeHash2D**
        
    2.  **wp.Runtime.ShowRuntimeSpatialHashGridLevel 2**
        
    
    These commands display which World Partition cells are loaded around the player.
    
    ![During gameplay you can see a display of which World Partition cells are loaded around the player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d12adc0-0559-4d1c-84ba-4f8b33acefdb/wp-navmesh-18.png)
3.  Press **single-quotation (')** to enable the **Gameplay Debugger** and press **zero** **(0)** to switch to the **Navigation** view. You can now see the Navigation Mesh loaded around the player.
    
    ![You can see the Navigation Mesh loaded around the player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7987a14c-1651-4770-88df-6d73e873c499/wp-navmesh-19.png)
4.  Move around the level and see how the Navigation Mesh is loaded as each World Partition cell is loaded around the player.
    
    ![Move around the level and see how the Navigation Mesh is loaded around the player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c562a77-55b2-486b-9eb2-8d9b294dec6b/wp-navmesh-demo-1.gif) ![Top view of the Navigation Mesh being loaded around the player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34947bad-e654-47a4-b75b-a82ba96c35c5/wp-navmesh-demo-2.gif)

#### Section Results

In this section, you learned how to visualize when the Navigation Mesh is loaded and unloaded by World Partition.