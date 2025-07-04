# Open World Tools Property Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/open-world-tools-property-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/open-world-tools-property-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:40:08

---

## Overview

This page contains a reference listing of properties you will find while working with the Open World Tools.

## Foliage Type

### Mesh

Click image for full size.

| Property | Description |
| --- | --- |
| **Mesh** | Defines which Static Mesh will be used. |
| **Component Class** | The component class to use for foliage instances. You can make a Blueprint subclass of FoliagedInstancedStaticMeshComponent to implement custom behavior and assign that class here. |
| **Override Materials** | Material overrides for foliage instances. |

### Placement

Click image for full size.

| Property | Description |
| --- | --- |
| **Z Offset** | Specifies a range from minimum to maximum of the offset to apply to a foliage instance's Z location. |
| **Align to Normal** | Whether foliage instances should have their angle adjusted away from vertical to match the normal of the surface they're painted on. If AlighnToNormal is enabled and RandowYaw is disabled, the instance will be rotated so that the +X axis points down-slope. |
| **Random Yaw** | If selected, foliage instances will have a random yaw rotation around their vertical axis applied. |
| **Random Pitch Angle** | A random pitch adjustment can be applied to each instance, up to the specified angle in degrees, from the original vertical. |
| **Ground Slope Angle** | Foliage instances will only be placed on surfaces sloping in the specified angle range from the horizontal. |
| **Height** | The valid altitude range where foliage instances will be placed, specified using minimum and maximum world coordinate Z values. |
| **Landscape Layers** | If a layer name is specified, painting on Landscape will limit the foliage to areas of Landscape with the specified layer painted. |
| **Collision with World** | If checked, an overlap test with existing world geometry is performed before each instance is placed. |

### Procedural

Click image for full size.

| Property | Description |
| --- | --- |
| **Collision Radius** | The CollisionRadius determines when two instances overlap. When two instances overlap a winner will be picked based on rules and priority. |
| **Shade Radius** | The ShadeRadius determines when two instances overlap. If an instance can grow in the shade this radius is ignored. |
| **Num Steps** | The number of times we age the species and spread its seeds. |
| **Initial Seed Density** | Specifies the number of seeds to populate along 10 meters. The number is implicitly squared to cover a 10m x 10m area. |
| **Average Spread Distance** | The average distance between the spreading instance and its seeds. For example, a tree with an AverageSpreadDistance 10 will ensure the average distance between the tree and its seeds is 10cm. |
| **Spread Variance** | Specifies how much seed distance varies from the average. For example, a tree with an AverageSpreadDistance 10 and a SpreadVariance 1 will produce seeds with an average distance of 10cm plus or minus 1cm. |
| **Seeds Per Step** | The number of seeds an instance will spread in a single step of the simulation. |
| **Distribution Seed** | The seed that determines placement of initial seeds. |
| **Can Grow in Shade** | If true, seeds of this type will ignore shade radius overlap tests with other types. |
| **Spawns in Shade** | Whether new seeds are spawned exclusively in shade. Occurs in a second pass after all types that do not spawn in shade have been simulated. Only valid when CanGrowInShade is true. |
| **Max Initial Age** | Allows a new seed to be older than 0 when created. New seed will be randomly assigned an age in the range\[0,MaxInitialAge\]. |
| **Max Age** | Specifies the oldest a seed can be. After reaching this age the instance will still spread seeds, but will not get any older. |
| **Overlap Priority** | When two instances overlap we must determine which instance to remove. The instance with a lower OverlapPriority will be removed. In the case where OverlapPriority is the same regular simulation rules apply. |
| **Procedural Scale** | The scale range of this type when being procedurally generated. Configured with the Scale Curve. |
| **Scale Curve** | Instance scale factor as a function of normalized age(i.e. Current Age / Max Age). X = 0 corresponds to Age = 0, X = 1 corresponds to Age = Max Age. Y = 0 corresponds to Min Scale, Y = 1 corresponds to Max Scale. |
| **External Curve** | For and external curve. |

### Instance Settings

Click image for full size.

| Property | Description |
| --- | --- |
| **Mobility** | Mobility property to apply to foliage components. |
| **Cull Distance** | The distance where instances will begin to fade out if using a PerInstanceFadeAmount Material node. 0 disables. When the entire cluster is beyond this distance, the cluster is completely culled and not rendered at all. |
| **Cast Shadow** | Controls whether the foliage should cast a shadow or not. |
| **Affect Dynamic Indirect Lighting** | Controls whether the foliage should inject light into the Light Propagation Volume. This flag is only used if CastShadow is true. |
| **Affect Distance Field Lighting** | Controls whether the primitive should affect dynamic distance field lighting methods. This flag is only used if CastShadow is true. |
| **Cast Dynamic Shadow** | Controls whether the foliage should cast shadows in the case of non precomputed shadowing. This flag is only used if CastShadow is true. |
| **Cast Static Shadow** | Whether the foliage should cast a static shadow from shadow casting lights. This flag is only used if CastShadow is true. |
| **Light Map Resolution** | Overrides the lightmap resolution defined in the static mesh. |
| **Collision Presets** | Select collision presets. You can set this data in Project Settings. |
| **Custom Navigable Geometry** | 
-   **No**: Primitive doesn't have custom navigation geometry, if collision is enabled then its convex/trimesh collision will be used for generating the navmesh.
-   **Yes**: If primitive would affect navmesh, DoCustomNavigableGeometryExport() should be called to export this primitive's navigable geometry
-   **Even if not Collidable**: DoCustomNavigableGeometryExport() should be called even if the mesh is non-collidable and wouldn't normally affect the navmesh
-   **Dont Export**: Don't export navigable geometry even if primitive is relevant for navigation (can still add modifiers).



 |
| **Cast Shadow as Two Sided** | Whether this foliage should cast dynamic shadows as if it were a two sided material. |
| **Receives Decals** | Whether the foliage receives decals. |
| **Use as Occluder** | If enabled, foliage will render a pre-pass which allows it to occlude other primitive, and also allows it to correctly receive DBuffer decals. Enabling this setting may have a negative performance impact. |

### Scalability

Click image for full size.

| Property | Description |
| --- | --- |
| **Enable Density Scaling** | Whether this foliage type should be affected by the Engine Scalability system's Foliage scalability setting. Enable for detail meshes that don't really affect the game. Disable for anything important. Typically, this will be enabled for small meshes without collision(e.g. grass) and disabled for large meshes with collision (e.g. trees). |

## Landscape Grass Type

### Grass Varieties

Click image for full size.

| Property | Description |
| --- | --- |
| **Grass Varieties** | Grass Varieties. |
| **Grass Mesh** | Grass Mesh. |
| **Use Grid** | If true, use a jittered grid sequence for placement, otherwise use a halton sequence. |
| **Placement Jitter** | Placement Jitter. |
| **Start Cull Distance** | The distance where instances will begin to fade out using a PerInstanceFadeAmount material node. 0 disables. |
| **End Cull Distance** | The distance where instances will have completely faded out when using a PerInstanceFadeAmount material node. 0 disables. When the entire cluster is beyond this distance, the cluster is completely culled and not rendered at all. |
| **Min LOD** | Specifies the smallest LOD that will be used for this component. If -1(default), the MinLOD of the static mesh asset will be used instead. |
| **Scaling** | Specifies grass instance scaling type. |
| **Scale X** | Specifies the range of scale, from minimum to maximum, to apply to a grass instance's X Scale property. |
| **Scale Y** | Specifies the range of scale, from minimum to maximum, to apply to a grass instance's Y Scale property. |
| **Scale Z** | Specifies the range of scale, from minimum to maximum, to apply to a grass instance's Z Scale property. |
| **Random Rotation** | Whether the grass instances should be placed at random rotation (true) or all at the same rotation(false). |
| **Align To Surface** | Whether the grass instances should be tilted to the normal of the landscape(true), or always vertical(false). |
| **Use Landscape Lightmap** | Whether to use the landscape's lightmap when rendering the grass. |

## Procedural Foliage Spawner

### Procedural Foliage Simulation

Click image for full size.

| Property | Description |
| --- | --- |
| **Random Seed** | The seed used for generating the randomness of the simulation. |
| **Tile Size** | Length of the tile (in cm) along one axis. The total area of the tile will be TileSize \* TileSize. |
| **Num Unique Tiles** | The number of unique tiles to generate. The final simulation is a procedurally determined combination of the various unique tiles. |
| **Foliage Types** | The types of foliage to procedurally spawn. |
| **Foliage Type Object** | The foliage type that will be spawned by the procedural foliage simulation. |