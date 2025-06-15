# Water Debugging and Scalability Options

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/water-debugging-and-scalability-options-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/water-debugging-and-scalability-options-in-unreal-engine)  
**Processed:** 2025-06-14 17:04:01

---

The [Water system](/documentation/en-us/unreal-engine/water-meshing-system-and-surface-rendering-in-unreal-engine) contains its own commands useful for displaying relevant information in the Level Viewport for debugging purposes, for providing visualizations, and for setting scalability options for your project.

## Water Level Stats

While working in the Editor, you can open the **console** with the **backtick** (\`) key and enter one of the stat commands to display information about the Water system in your currently loaded level.

### Stat Water

Use the command `stat water` to toggle display of CPU statistics about the water-related functions used in the current scene.

![Statistical data about the water system displayed on screen.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae49fde4-e5a5-4219-a696-994314e0f105/command-stat-water.png)

| Stat Name | Description |
| --- | --- |
| **IsUnderwater Test** | The cost of the function, testing how many times it's called per frame and how much it costs (max/average). This test function is used to detect whether to activate the underwater post process or not. |
| **WaterBody\_ComputeWaterInfo** | The cost of the function used throughout the engine to compute water-related information. It's useful for checking frame time since if many queries are done by gameplay systems, physics, or other systems, there can be significant time added to the frame. |
| **WaterBody\_ComputeWaterDepth** | Runs as part of the `WaterBody_ComputeWaterInfo` function to compute data on the water depth. |
| **WaterBody\_ComputeWaveHeight** | Runs as part of the `WaterBody_ComputeWaterInfo` function to compute data on the water height. |
| **WaterBody\_ComputeLandscapeDepth** | Runs as part of the `WaterBody_ComputeWaterInfo` function to compute data on the landscape depth. |

The stats for `WaterBody_ComputeWaterDepth`, `WaterBody_ComputeWaterHeight`, and `WaterBody_ComputeLandscapeDepth` do not provide information you can act on. Each of them is part of the `WaterBody_ComputeWaterInfo` stat, and are some of the most expensive parts of its function. Instead, get a better sense of what's happening by using [Unreal Insights](/documentation/en-us/unreal-engine/unreal-insights-in-unreal-engine) to profile your scene.

### Stat WaterMesh

The command `stat watermesh` displays information about [Water Meshing and Surface Rendering](/documentation/en-us/unreal-engine/water-meshing-system-and-surface-rendering-in-unreal-engine). You can act on the statistics in this display by adjusting some settings and assignments on different parts of the water used in your Level.

![Statistical data about the water meshes being rendered on screen.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72c602ed-6710-4316-9723-a1689e9b6fd1/command-stat-water-mesh.png)

| Stat Name | Description |
| --- | --- |
| **Vertices Drawn** | Displays the number of vertices drawn for all Water Bodies in the current view. |
| **Tiles Drawn** | 
Displays the total number of visible tiles based on the current water mesh's Tile Size, Tile Extents, and how close the camera is to them.

Use `r.Water.WaterMesh.ShowTileBounds 1` in conjunction with this stat to understand how the mesh is divided into tiles and how they relate to this stat.



 |
| **Draw Calls** | 

The total number of draw calls to draw water this frame. The lower the number, the lesser the cost on the CPU.

The tiles with an identical material are usually merged into a single draw call, thus you'll see a lower **Number of Drawn Materials** than those compared to **Tiles Drawn**.



 |
| **Number of Drawn Materials** | The number of different water materials drawn in this frame. For example, if you are using various Water Bodies with a different water material on them, there will be more drawn materials per frame. By contrast, if all Water Bodies share the same material, fewer materials are being drawn giving you less draw calls per frame. |

## Debugging Console Commands

The following console commands are useful for debugging the Water system in your Levels.

| Variable Name | Description | Default Value |
| --- | --- | --- |
| `r.Water.WaterMesh.ShowTileGenerationGeometry` | Displays the geometry used for intersecting the water grid and generating water mesh tiles. | 0 |
| `r.Water.WaterMesh.ForceRebuildMeshPerFrame` | Forces rebuild of the entire water tile mesh every frame. | 0 |
| `r.Water.WaterMesh.Enabled` | Sets whether the water mesh should be rendered or not. This affects both rendering and the water mesh tile generation. | 0 |
| `r.Water.WaterMesh.ShowWireframeAtBaseHeight` | When rendering in wireframe, it shows the water tile mesh with no displacement. | 0 |
| `r.Water.WaterMesh.EnableRendering` | Sets whether all water rendering from within the scene proxy should be turned off. | 1 |
| `r.Water.WaterMesh.ShowLODLevels` | Shows the levels of detail as concentric rings around the camera position at height 0 in the Level. | 0 |
| `r.Water.WaterMesh.ShowTileBounds` | 
Shows the tile bounds of the water mesh tiles as colored by `r.Water.TileBoundsColor`.

By default, tiles are colored by Water Body type or transition type:

-   **Red:** River
-   **Green:** Lake
-   **Blue:** Ocean
-   **Yellow:** River to Lake Transition
-   **Purple:** River to Ocean Transition



 | 0 |
| `r.Water.WaterMesh.TileBoundsColor` | Sets the colors of water mesh tile bounds when visualized using `r.Water.ShowTileBounds`. When set to 0, colors represent the level of detail (LOD) transitions. When set to 1, colors are representative of Water Body types. | 1 |
| `r.Water.WaterMesh.ShowWireframe` | Forces wireframe rendering for water. | 0 |
| `r.Water.VisualizeActiveUnderwaterPostProcess` | Shows which Water Body is currently being picked up for underwater post process when set to 1. When set to 2, it provides additional information about the Water Data Query performed at the camera location, which is useful for debugging water data queries. | 0 |
| `r.Water.OverrideWavesTime` | Force the time used for waves if values are greater than or equal to 0. | \-1 |
| `r.Water.FreezeWaves` | Freezes time for waves. | 0 |
| `r.Water.OceanFallbackDepth` | Depth to report for the ocean when no terrain is found under the query location. This depth value is not used when set to 0 or less. | 3000 |
| `r.Water.DebugBuoyancy` | Enables debug drawing for water interactions. | 0 |
| `r.Water.WaterInfo.ForceUpdateWaterInfoNextFrames` | Force the water info texture to regenerate on the next N frames. A negative value will force update every frame. | 0 |

### Tile Bounds and their Colors

Use the console command `r.Water.WaterMesh.ShowTileBounds 1` to display colored boxes for different types of water mesh tiles currently used in the Level.

Choose one of the following for how Tile Bounds are displayed:

-   **0** is disabled.
-   **1** is by Water Body type.
-   **2** is by level of detail.
-   **3** is by density index.

![Example scene with water bodies and their tile bounds color.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2c85e76-0af5-4350-86aa-85d33571aa44/debugging-water-tile-bounds.png)

An example scene showing Water Tile Bounds colored by their Water Body and transition type.

By default, tiles are colored by Water Body type and their transition between other water bodies:

-   **Red:** River
-   **Green:** Lake
-   **Blue:** Ocean
-   **Yellow:** River to Lake Transition
-   **Purple:** River to Ocean Transition

### Visualizing Active Underwater Post Processing

Use the console command `r.Water.VisualizeActiveUnderwaterPostProcess` to display information in the Level Viewport about the underwater post process currently overlapped by the camera.

When set to **1**, basic debug information is provided about the currently used underwater post process.

![Debug information displayed on screen about the current underwater post process.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8dcc3fae-e9a1-406f-9b29-50b390fdf499/underwater-post-process-debugging-1.png)

When set to **2**, additional information is displayed about the Water Data Query performed at the camera's location.

![Additional debug information displayed on screen about the current underwater post process.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a36e5524-8508-4d7b-9e9b-91670aae8ecf/underwater-post-process-debugging-2.png)

## Scalability Console Commands

The following console commands are useful for setting scalability options of the Water system in your Levels and projects.

| Variable Name | Description | Default Value |
| --- | --- | --- |
| `r.Water.WaterMesh.LODCountBias` | Adds the value to the LOD Count of each Water Mesh Component. Negative values lower the quality (lower density of water mesh), whereas higher values increase quality (higher density of water mesh). | 0 |
| `r.Water.WaterMesh.TessFactorBias` | Adds the value to the tessellation factor of each Water Mesh Component. Negative values lower the overall density (resolution), or the vertex grid. Higher values increase the density (resolution) of the Water Mesh Component. | 0 |
| `r.Water.WaterMesh.LODMorphEnabled` | Sets whether to use smooth LOD morphing for transitions between different levels of detail. Disabling this may cause popping between LOD levels but will skip the calculations in the vertex shader, making water cheaper in the scene. | 1 |
| `r.Water.WaterMesh.LODScaleBias` | Adds the value to the LOD Scale of each Water Mesh Component. Negative values lower the overall density (resolution), or the vertex grid and make the LODs smaller. Higher values increase the density (resolution) and make LODs larger. Smallest allowed value is -0.5, which will make the inner LOD as small and optimized as possible. | 0 |
| `r.Water.WaterMesh.PreAllocStagingInstanceMemory` | Pre-allocates staging instance data memory according to historical max, which reduces the overhead when the array needs to grow but may use more memory. | 0 |
| `r.Water.UseSplineKeyOptimization` | Whether to cache spline input keys for Water Bodies. | 1 |
| `r.Water.EnableUnderwaterPostProcess` | Controls whether the underwater post process is enabled. If the camera never intends to go below the surface, this should be disabled. | 1 |
| `r.Water.EnableShallowWaterSimulation` | Controls whether the shallow water fluid sim is enabled. | 1 |
| `r.Water.ShallowWaterMaxDynamicForces` | The maximum number of dynamic forces that are registered with the water fluid sim at a time. | 6 |
| `r.Water.ShallowWaterMaxImpulseForces` | The maximum number of impulse forces that are registered with the water fluid sim at a time. | 3 |
| `r.Water.ShallowWaterRenderTargetSize` | The size for the square shallow water fluid sim render target. Effective dimensions are Size x Size. | 1024 |
| `r.RayTracing.Geometry.Water` | Include water in ray tracing effects. | 0 |
| `r.Water.WaterSplineResampleMaxDistance` | The maximum distance between the sample segments and the spline when converting the water spline shapes to polygons. As distance decreases, the number of vertices increases, the physics shapes are more accurate, and the water mesh tiles match more closely, but the computational cost also increases. | 50 |

### Water Body Spline Resampling Max Distance

The Lake Water Body collision components (and water mesh tile generation) is based on their spline evaluation. Both Lake and Ocean Water Body splines go through a transformation process into polygons and are processed in order to see which water mesh tiles they cover. The polygonization is an iterative process where the spline is resampled as long as the distance between the sampled spline segments are too far from the original spline. This leads to a higher number of points in sections with high curvature, and a lower number of points in straighter sections.

Use the console variable `r.Water.WaterSplineResampleMaxDistance` to adjust the distance. By default 50 centimeters is used. Higher values use fewer vertices which in turn means fewer collision components to match the lake spline's shape. If using a lower value, there will be significantly more vertices generated.

Set `r.Water.WaterMesh.ShowTileGenerationGeometry 1` to view the generated tile geometry.

|   |   |   |
| --- | --- | --- |
| 
 | 

 | 

 |
| Max distance of 50 cm (Default) is a good middle ground. | Max distance of 400 cm has fewer vertices. | Max distance of 10 cm has significantly more vertices. |

Click on an image to enlarge it.

From our experience developing Fortnite and using large worlds with water, we recommend 50 as a good middle ground that approximates most normally-sized lakes correctly. If you lower the distance too low, the physics shape won't match enough, which might cause some water tiles to be missing.

When adjusting this console variable, you must modify something on the water spline, such as moving a spline point slightly) to see the result.