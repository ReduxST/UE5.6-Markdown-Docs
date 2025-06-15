# Global Illumination

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/global-illumination-in-unreal-engine)  
**Processed:** 2025-06-14 16:26:05

---

**Global illumination** (sometimes referred to as indirect lighting and indirect illumination) simulates lighting interactions with geometry and material surfaces to add accurate lighting to scenes. Global illumination also takes into account absorption and reflectiveness of the materials in which it interacts.

Simulating the way in which light behaves in a 3D world is handled in one of two ways: using lighting that supports movement and interaction, or precomputed lighting that doesn't require scenes to be overly dynamic or interactive with lighting.

Unreal Engine provides multiple lighting paths to choose from for global illumination solutions, and often they are not exclusive to one another and can be seamlessly blended. For example, it is possible to have both dynamic lighting and baked lighting within the same scene.

For comparison, the list below highlights some of the benefits of choosing a precomputed or dynamic global illumination path for your project:

<table class="table" style="--columns-count: 2;"><tbody><tr><td><div><ul><li>Ideal for scenes where lighting doesn't need to change.</li><li>Performance costs are relative to the memory required to load and store the lightmap textures.</li><li>Quality and accuracy of results is set by the texture resolution of the lightmap texture being baked and applied to geometry.</li><li>Supports Static Mesh and BSP geometry by default.</li><li>Static Meshes require setting up a Lightmap UV to store lighting data.</li><li>Can be used in combination with dynamic lighting.</li></ul></div></td><td><div><ul><li>Ideal for times where lighting needs to change, such as turning a light on or off, or a time-of-day system.</li><li>Large, open-world environments present impractical requirements for baked lighting (even without a time-of-day system). Bake times, memory usage, texture storage and playback are considerable factors to use dynamic GI.</li><li>Performance costs can be significantly more expensive to calculate in real-time depending on the method being used.</li><li>Quality and accuracy is often traded with performance. Some Dynamic GI methods are limited by real-time usage.</li><li>Supports all geometry types by default.</li><li>Can be used in combination with precomputed lighting.</li></ul></div></td></tr></tbody></table>

## Precomputed Global Illumination

The light baking system in Unreal Engine computes lighting data on the CPU, or GPU, using the Lightmass Global Illumination system. This method of precomputing lighting is used to achieve high-quality results that aren't compromised by real-time limitations by storing the information in textures that are then applied to geometry. This method of lighting cannot be changed dynamically and is ideal for projects where lighting doesn't need to change, or for mobile projects where dynamic lighting is limited.

-   **CPU-based Lightmass** uses the CPU with a separate program called [Unreal Swarm](/documentation/en-us/unreal-engine/unreal-swarm-in-unreal-engine) to compute and generate lighting data. This method can use a single machine or distribute lighting data to build farms.
-   **GPU-based Lightmass** uses your current machine's NVIDIA GPU which supports DirectX 12 and ray tracing to compute and generate lighting data.

### Precomputed Global Illumination Methods

### Precomputed Global Illumination Supporting Topics

## Dynamic Global Illumination

The dynamic global illumination methods in Unreal Engine provide real-time scalable solutions for dynamic indirect lighting in your projects. This means being able to place, move, and light objects in the world without additional costs of baking lighting or having additional set up. Dynamic indirect lighting also means being able to accurately simulate time-of-day transitions or something as simple as turning a light on and off and having light bounce and reflect accurately.

![lumen-global-illumination](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/96f61b68-6220-473a-bcdb-1f20b956592d/lumentechdemo_1.png)

-   **Lumen** is a fully dynamic global illumination and reflection system that is designed for next-generation consoles. It is the default dynamic global illumination system and uses multiple ray tracing methods to solve global illumination and reflections at scale.
-   **Screen Space Global Illumination** (SSGI) is a post processing effect that generates global illumination for objects within the scene based solely on the current visible objects within the camera view. This is a low-cost and most effectively used in conjunction with existing precomputed or dynamic global illumination methods as an additive effect.
    
    This feature is deprecated. It may be removed in a future release.
    

### Dynamic Global Illumination Topics

%building-virtual-worlds/lighting-and-shadows/global-illumination/lumen:Topic% %building-virtual-worlds/lighting-and-shadows/global-illumination/lumen/TechOverview:Topic%