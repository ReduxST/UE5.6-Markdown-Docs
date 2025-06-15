# Debugging Grooms

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-grooms-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/debugging-grooms-in-unreal-engine)  
**Processed:** 2025-06-14 16:19:20

---

This page contains information to help you debug and inspect grooms in Unreal Engine.

## Groom Debug Visualization Options

The Level Editor viewport options contain useful visualizations for inspecting different aspects of grooms. You can access these options with **Lit > Groom**.

![Groom visualization modes for debugging.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52a16821-01fe-485e-9a53-fff28fe67a98/groom-visualization-selection.png)

One example from the list of groom visualizations that is useful is **Instances**. With this visualization, you can inspect all visible instances' properties. The view shows each visible hair group and information about their LOD index, type of geometry, type of binding, simulation, RBF, and so on. For strands geometry, it also shows the number of active curves and points.

Click image for full size.

**Guides** is another useful visualization that displays the simulation guides for visible grooms.

Click image for full size.

To get a summary of all Groom assets, Groom Binding assets, and Groom Component memory footprint, you can use the console command `r.HairStrands.Dump`to output information to the log. This output contains information about consumed memory on the CPU and GPU for these assets. You can also get a summary of information with the **Memory** visualization mode.

Click image for full size.

## Groom Shadow Artifacts

Shadows cast by strands geometry are computed using voxelized curves by default. The default settings might not suit your use case and need to be adapted to your project using console variables. The strands are voxelized using a sparse voxel structure made of pages, which you can think of as "bricks" of voxels. When a groom is voxelized, the bricks are allocated to cover the groom. The size of these bricks adapts based on the distance to the grooms. If there are a lot of grooms in a level, or if the camera is really close to a large groom, it's possible to run out of pages.

You can increase the number of pages with the console variable `r.HairStrands.Voxelization.Virtual.VoxelPageCountPerDim`. Increasing this value can cause allocated memory to quickly rise up.

If the camera gets close to a groom, the voxel resolution may appear too low. You can increase the voxel resolution by reducing the voxel size with the console command `r.HairStrands.Voxelization.Virtual.VoxelWorldSize`.

You can visualize the groom voxels with the **Voxels** visualization mode. Hovering over the **Draw Pages** in the viewport shows the groom pages.

Click image for full size.

## Tuning Motion Vectors to Reduce Visible Artifacts

During rapid camera movement, you can have undesireable visible artifacts appear on hair strands. The console variable `r.HiarStrands.Visibility.WriteVelocityCoverageThreshold` is useful for tuning motion vector coverage of hair strands to get rid of these artifacts by defining the coverage threshold at which a pixel writes its hair velocity.

When tuning this value, at `0` (default), hair will always write its velocity. For any value greater than 0, hair writes its velocity only if the hair coverage for a given pixel is greater than this value.