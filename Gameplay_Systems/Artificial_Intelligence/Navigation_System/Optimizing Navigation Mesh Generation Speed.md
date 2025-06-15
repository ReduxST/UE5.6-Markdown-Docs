# Optimizing Navigation Mesh Generation Speed

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/optimizing-navigation-mesh-generation-speed-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/optimizing-navigation-mesh-generation-speed-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:34

---

The latest version of this guide can be found in your local installation of Unreal Engine under the following directory: `Engine\Source\Runtime\NavigationSystem\DevDocs\How To Optimize Navmesh Generation.md`

## Overview

Unreal Engine's **Navigation System** provides pathfinding capabilities to Artificial Intelligence Agents. To find a path between a start location and a destination, a **Navigation Mesh** is generated from the collision geometry of the world.

The Navigation Mesh is divided into tiles which are used to rebuild localized parts of the Navigation Mesh at runtime.

The Navigation System provides a variety of settings that advanced users can use to modify the way navigation is computed in the Level. This guide provides recommendations to optimize the generation speed of the Navigation Mesh.

## Use the Highest Cell Size and Cell Height Possible

The **Cell Size** and **Cell Height** properties define the size of the voxels used to generate the Navigation Tiles. The smaller the voxels, the more precision is gained and the more accurate the navigation will be around obstacles. However, the smaller the voxels, the more processing is required when rebuilding the Navigation Mesh at runtime.

For this reason, it is important to balance the size of the cells (voxels) with the amount of navigation precision needed in your project.

Follow these steps to adjust the Cell Size and Cell Height properties of your Navigation Mesh:

1.  Click **Settings > Project Settings** to open the **Project Settings** window.
    
    ![Open the Project Settings window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/91d2c8f9-9c40-4a00-a64a-3c823980b24f/navigation-generation-project-settings-1.png)
2.  Go to the **Navigation Mesh** section and scroll down to the **Generation** section. You can increase the **Cell Size** and **Cell Height** values to improve generation speed. Note that increasing the Size and Height values will decrease the Navigation Mesh precision in your level.
    
    ![Open the Project Settings window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fd66983a-1b5b-408c-ae0b-57b0d568e494/navigation-generation-project-settings-2.png)
3.  Alternatively, you can adjust individual Navigation Meshes inside your Level by selecting the **RecastNavMesh-Default** Actor in the **Outliner** and going to the **Details** panel.
    
    ![Select the NavMesh Actor in the World Outliner window](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f5fa7b6-7356-49ec-88f8-5be713ab678b/navigation-generation-select-navigation-mesh.png)
4.  In this example the **Cell Size** was changed from **19** to **64**. Notice how precision is reduced and the Navigation Mesh is less accurate around the objects in the level. The new Cell Size of 64 prevents navigation generation between the wall and the box (see the arrow in the image below).
    

![Tile Size is 19](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4e87b83-a7e3-4f41-a3b1-c881781221e5/navigation-generation-cell-size-change-1.png)

![Tile Size is 64](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b39417cd-7269-40c2-909d-0c22abab92c6/navigation-generation-cell-size-change-2.png)

### Recommendation

Make the cells as large as possible while maintaining the required precision for your Agents.

In the example above, setting the **Cell Size** to 64 caused the path between the wall and the box to be removed. If this path is needed for your Agent, you can either continue to adjust **Cell Size** until a path is generated or move the box further from the wall.

## Limit the Tile Size

The Navigation Mesh is divided into tiles which are used to rebuild localized parts of the Navigation Mesh at runtime. Since each tile is built from cells, rebuilding a Navigation Tile will result in the recreation of all its cells with the new collision information.

Larger tiles contain more cells and are more expensive to rebuild than smaller tiles. However, when processing a tile, the system also processes the contiguous cells on the edges of the tile. You should consider this overhead cost when setting the size of your tiles, as there can be situations where the overhead cost of processing many smaller tiles is greater than the cost of rebuilding a single large tile.

### Recommendation

The **Tile Size** should be set between **32** to **128 cells** per side. This will provide the best performance when rebuilding tiles at runtime.

In the previous example the **Cell Size** was set to **64**. In that case, the **Tile Size UU** should be set between **2048** (64*32) and **8192** (64*128).

![Set the Tile Size UU](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f7973b9-9289-42a2-92ee-596c659e473c/navigation-generation-tile-size-change.png)

## Use Simplified Collision for Your Meshes

The Navigation System uses each object's collision data to generate the Navigation Mesh. Simpler object collision results in faster processing compared to higher triangle count collision data.

### Recommendation

Use **Simple Collision** when possible for Static Meshes. The lower the triangle count used in the collision mesh, the faster the generation will be.

## Reduce the Number of Objects That Affect the Navigation Mesh

By default, Blueprint Actors and Static Meshes in your Level affect navigation. The number of objects that affect a Navigation Tile has a direct impact on the cost of generating that tile.

### Recommendation

Smaller objects that should not affect the Navigation Mesh should be configured so they don't affect navigation. Select your Actor in the Level and go to the **Details** panel. Scroll down to the **Collision** section and **disable** the **Can Ever Affect Navigation** checkbox.

![Disable navigation on your Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0c38436-4586-4ec9-ba3c-1ae6a4589d46/navigation-generation-disable-navigation.png)

This setting should be disabled for any Actor that should not affect the Navigation Mesh, such as moving objects in inaccessible areas of the Level.

If possible, you should avoid affecting large tile areas or multiple tiles at the same time.

## Useful Developer Tools to Manage Navigation Generation

### Locking and Unlocking the Navigation Mesh Generation at Strategic Times

It is possible to stop the automatic generation of the Navigation Mesh before loading many assets that might affect it. You can unlock the generation once all the assets have completed loading. This method prevents the Navigation System from rebuilding the same tile several times.

To lock the Navigation Mesh generation, set your navigation system's **bInitialBuildingLocked** to **True.** To unlock the generation, call the function **ReleaseInitialBuildingLock()**. Once unlocked, the Navigation Mesh will rebuild all the tiles marked as dirty by the loaded assets. To prevent this, you can call **DefaultDirtyAreasController.Reset()** before unlocking the generation.

### Enable Multi-threaded Navigation Mesh Generation

You can control multi-threaded Navigation Mesh generation by setting the **MaxSimultaneousTileGenerationJobsCount** property in the Navigation System. Note that this is limited by the total number of worker threads in **FRecastNavMeshGenerator::Init()**.

### Use Dynamic Obstacles with Full Dynamic Navigation Mesh Generation

You can mark Static Meshes and other Actors in your Level as **Dynamic Obstacles**. Dynamic Obstacles mark the Navigation Mesh surface where generation needs to be rebuilt. This prevents the entire Navigation Tile from being rebuilt.

Using this method is less costly than generating the full Navigation Tile and should be used when a Navigation Mesh surface is not needed on top of moving obstacles.

![Set your Static Mesh to be a Dynamic Obstacle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0102b162-9516-4432-bd36-03b14334d60c/navigation-generation-dynamic-obstacle.png)

### Use Data Chunk Streaming for Static Navigation Meshes Loaded in Sublevels

If the only changes to the Navigation Mesh come from loading and unloading sublevels, you can set the Navigation Mesh Generation Method to **Static** and use **NavMesh Data Chunk Streaming**, instead of using a dynamic Navigation Mesh.

With this method, the Navigation Mesh will be fully built in the editor and only the relevant parts will be loaded in and out at runtime.