# Proxy Geometry Tool Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/proxy-geometry-tool-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/proxy-geometry-tool-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:45:09

---

## Reference

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0af92b3f-2d8d-426d-8cd0-dc1818fee2da/proxy_geo_rf_01.png "Proxy_Geo_RF_01.png")

In the following table you will find property descriptions for each of the settings that you will find in the Proxy Geometry Tool:

| **Property Name** | **Description** |
| --- | --- |
| **Screen Size** | Screen size of the resulting proxy mesh in pixels. |
| **Override Spatial Sampling Distance** | Override when converting mesh from proxy lod merging. Warning, large geometry with small sampling has very high memory costs. |
| **Material Settings** | Material simplification settings. |
| **Calculate Correct LOD Model** | Determines whether or not the correct LOD models should be calculated given the source meshes and transition size. |
| **Merge Distance** | Distance at which meshes should be merged together, this can close gaps like doors and windows in distant geometry. |
| **Unresolved Geometry Color** | Base color assigned to LOD geometry that can't be associated with source geometry. For example, doors and windows that have been closed by the Merge Distance. |
| **Transfer Distance Override** | Override search distance used when discovering Texture values for simplified geometry. Useful when non-zero Merge Distance settings generates new geometry in concave corners. |
| **Hard Edge Angle** | Angle at which a hard edge is introduced between faces. Note: Increases vertex count and may introduce additional UV seams. It is only recommended if not using Normal Maps. |
| **Normal Calculation Method** | Controls the method used to calculate the Normal for simplified geometry. |
| **Light Map Resolution** | Lightmap resolution size. |
| **Compute Light Map Resolution** | If ticked will compute the lightmap resolution by summing the dimensions for each mesh included for merging. |
| **Enable Volume Culling** | Allows culling volumes to exclude geometry. |
| **Allow Adjacency** | Whether to allow Adjacency buffers to tessellation in the merged mesh. |
| **Allow Distance Field** | Whether to allow distance field to be computed for this mesh. Disable this to save memory if your mesh will only rendered in the distance. |
| **Reuse Mesh Lightmap UVs** | Whether to attempt to reuse the source mesh's lightmap UVs when baking the Material or always generate a new set. |
| **Allow Vertex Colors** | Whether to allow Vertex Colors saved in the merged mesh. |
| **Generate Lightmap UVs** | Whether to generate lightmap UVs for the merged mesh. |

In the following table you will find description for each of the available Console Commands that can be used with the Proxy Geometry Tool: 

| **Command Name** | **Description** |
| --- | --- |
| **r.ProxyLODChartColorVerts** | 
Color verts by UV chart. Default off.  
0: Disabled.  
1: Enabled.



 |
| **r.ProxyLODCorrectCollapsedWalls** | 

Shall the ProxyLOD system attempt to correct walls with interpenetrating faces  
0: Disabled - Default.  
1: Enable, may cause cracks.



 |
| **r.ProxyLODMaterialInParallel** | 

Doing material work in parallel with mesh simplification.  
0: Disable.  
1: Enable - Default.



 |
| **r.ProxyLODMaxDilationSteps** | 

Limit the number of dilation steps used in gap filling for performance reasons. This may affect gap filling quality as bigger dilations steps will be used with a smaller max.  
0: Will disable gap filling.  
1: Default.- Default.



 |
| **r.ProxyLODMeshReductionModule** | Name of the Proxy LOD reduction module to choose. If blank it chooses any that exist. |
| **r.ProxyLODRemeshOnly** | 

Only remesh. No simplification or Materials.  
0: Disabled - will simplify and generate Materials.- Default.  
1: Enabled - will not simplify or generate Materials.



 |
| **r.ProxyLODSingleThreadSimplify** | 

Use single-threaded code path.  
0: Multithreaded. - Default.  
1: Single threaded.



 |
| **r.ProxyLODTransfer** | 

0: shoot both ways.  
1: preference for forward - Default.



 |
| **r.ProxyLODUseTangentSpace** | 

Controls the option to generate a Mikk-T space at each vertex. Default on. When this is disabled, a tangent space of (1,0,0) (0, 0, 1) (0,1,0) is added to each vertex for encoding the normal map.  
0: world space at each vertex.  
1: tangent space at each vertex - Default.



 |