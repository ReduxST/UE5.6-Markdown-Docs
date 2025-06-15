# Virtual Texture Memory Pools

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-texture-memory-pools-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-texture-memory-pools-in-unreal-engine)  
**Processed:** 2025-06-14 17:03:21

---

The Virtual Texture system has two main types of GPU memory allocation: Page Table Memory and a Physical Memory Pool.

-   **Page Table Memory** provides indirection from texture coordinates to the texture data, and is allocated on demand. It can grow over time and generally is not released from memory unless all of its contents are released. There are no user controls for this memory type.
-   **Physical Memory Pool** contains the currently resident texture data, and is made up of a number of individual pools. Each texture format that the Virtual Texture system sees has its own associated memory pool. Each pool is allocated on the first instantiation of a virtual texture with the matching format. Each pool has a fixed size and cannot grow. Users can control the size of each pool.

This document describes how virtual texture physical memory pools can be defined and debugged.

## Understanding the Behavior of Physical Memory Pools

The physical memory pools are each made up of pages. Each page contains the data for one tile of virtual texture. The pool acts as a least recently used cache. As the Virtual Texture system requests a tile, it is streamed or rendered into an available page in the pool. If there are no available pages, then the page containing the least recently seen tile is evicted to make room for the new one.

If a view has more virtual texture tiles visible than can fit in the virtual texture memory pools, the system will not be able to render that view correctly. In those cases, the virtual texture memory pool sizes need to be tuned to match the data usage.

## Configuring the Physical Memory Pools

The Memory Pool Sizes for virtual texturing are set up in the **Project Settings** under **Engine > Virtual Texture Pool**. These settings contain two configuration arrays:

![Project Settings for Virtual Texture Memory Pools.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5153dfe0-5290-41be-979d-52465608aac2/project-settings-vt-memory-pools.png)

-   **Fixed Pools** are serialized settings that iterates from last to first and uses the first matching configuration it finds. These settings will persist between editor sessions.
-   **Transient Pools** are configurations detected at runtime and used by the Pool Auto Grow system. A virtual texture physical pool searches these configurations to find a match before searching the configuration settings in Pools. Transient Pools only persist for the current editor session, but they can be copied to the serialized pools as a good estimation of the fixed pool sizes that a cooked project needs.

The pool descriptions are stored in the **Fixed Pools** array setting with each description containing the **Texture Format** and **Tile Size**. The example below has a specific pool description for each of the listed texture formats: DXT1, DXT5, and BC5.

![Example of pool description with various texture formats.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7be6eaa-f3bc-4e4f-bdb2-b0d1619d9c32/vtmempools-fixedpools-textureformat-example.png)

You can further set up any Virtual Texture Memory Pool containing DXT1 textures to be 100 megabytes (MB) in size by expanding the index under **Fixed Pools** and setting **Size in Megabyte**, like the example below. The size of the memory pool is approximate, and the system allocates the largest pool size less than 100 MB that is square and fits an integer number of pages.

![Example setting the DXT1 virtual texture memory pool to 100 megabytes.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bdb9dab9-3ed3-4c38-840d-378ef3b3f64c/vtmempools-fixedpools-sizeinmb.png)

Formats that don’t have any corresponding entry in the configuration use the pool size from **Default Size in Megabyte**.

Alternatively, a default pool size can be expressed by defining an entry in **Fixed Pools** that doesn’t have a texture format assigned.

Some pools contain multiple layers, with each having its own format. This is true for most Runtime Virtual Texture setups. In this case, the pool description should have the **Format** array correctly specified. For example, a Runtime VIrtual Texture that uses the **Base Color, Normal, Roughness, Specular** type in a material uses two DXT5 textures to store the data. It would be setup as follows:

![Example of Fixed Pools entry set up to match the texture formats of a runtime virtual texture.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0b4ff94-afad-4aea-ad8c-6154f7535d5b/vtmempools-fixedpools-textureformat-rvtmaterial.png)

Fixed Pools configuration entries also have the following settings:

| Memory Pool Configuration Setting | Description |
| --- | --- |
| **Allow Size Scale** | Applies an additional scale factor to the pool memory size through the scalability console variables `r.VT.PoolSizeScale`. |
| **Enable Residency Mip Map Bias** | Enables behavior where a mipmap bias is applied to virtual textures when this pool is oversubscribed. |
| **Min Scaled Size in Megabyte** | Sets the lower limit of the size to allocate for the pool after the console variable value for `r.VT.PoolSizeScale` is applied. |
| **Max Scaled Size in Megabyte** | Sets the upper limit of the size to allocate for the pool after the console variable value for `r.VT.PoolSizeScale` is applied. |

Pool sizes increase to accommodate the highest pool residency when the setting **Pool Auto Grow in Editor** is enabled. When a pool is detected to be at 100% residency, its size is increased and a notification pop-up informs you of this change in the editor. The detected changes in settings for the automatically increased pool size are stored in the **Transient Pool** array configuration.

These settings are not persistent to the project settings between editor sessions and will be lost. This means if your project has oversubscribed pools and **Pool Auto Grow in Editor** is enabled, you may see the pools growing every time you start the editor. You can circumvent this by copying and pasting the entries between the **Transient Pool** settings and **Fixed Pools** settings to have them persist between editor sessions.

The setting **Pool Auto Grow in Editor** has no effect in a cooked build, but you can set `r.VT.PoolAutoGrow` to tune pool sizes in a cooked build.

## Residency of Physical Memory Pools

The current usage of the virtual texture memory pools is referred to as **Residency**. When a pool has all its pages allocated by tiles that are currently visible, residency is 100%.

At a residency of 100%, a pool is oversubscribed and will drop data for visible tiles. This leads to unwanted IO and screen flickering as texture data is repeatedly loaded and evicted from memory.

You can enable an on-screen notification to be shown when the memory pool is oversubscribed. Enable the notification with the console command `r.VT.Residency.Notify 1`.

![virtual texture pool oversubscribed notification](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d6fc199-f0c7-4293-95d9-013b068069d6/oversubscribed-notification.png)

This warning indicates you should either increase your memory pool sizes in the configuration file, or change your virtual texture or Material. See the section below for tips on resolving these types of issuesnote

### Residency MipMap Bias

If a pool has been configured with the `bEnableResidencyMipMapBias` setting enabled, a mipmap bias is set to reduce residency when it is oversubscribed. This prevents unwanted IO and screen flickering at the cost of rendering virtual textures with a reduced resolution.

This setting is useful if residency is very rarely oversubscribed and you don't want to allocate memory for the rare chance this could happen. The on-screen message for oversubscription includes any mipmap bias that is being applied.

The mipmap bias that comes from residency is global. The maximum current bias from all of the physical memory pools is applied to *all* virtual texture sampling.

## Physical Memory Pool Heads-Up Display

Setting a good memory pool size is important to monitor residency and reduce oversubscription from happening. You can use the onscreen heads-up display (HUD) to show the current residency of each virtual texture physical memory pool.

It is enabled with `r.VT.Residency.Show 1`.

![virtual texture pool residency level editor view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38fc443d-cb0a-46ee-9cde-abd9eef59e9b/residency-graph-level-editor.png)

Virtual texture physical memory pool HUDs display the current residency of each texture format and their allocated memory.

![virtual texture pool residency graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ca8640e-c516-4733-953d-f2571dd5a250/residency-graph.png)

Each graph on the screen represents one of the virtual texture physical memory pools. There are three line graphs:

-   **Red** is the current pool occupancy from 0-100%.
-   **Yellow** is the fixed pool occupancy from 0-100%.
-   This is the occupancy from pages that are marked as locked. There is usually one page locked for every virtual texture. A very large number of loaded virtual texture assets can reduce the available pool space even if the virtual textures are not visible.
-   **Green** is the mipmap bias being applied to keep residency below 100%.

## Debugging the Residency of Physical Memory Pool

The following are some areas to start debugging and checking content when virtual texture memory pools are oversubscribed.

### Pool Memory Sizes

When it comes to virtual texture pool sizes, you'll want to check the following:

-   Check that pool sizes are large enough to hold an expected full working set of virtual texture data.
-   The pool size should be bigger for pools that have larger page sizes. For example, a pool with texture format `PF_A32B32G32R32F` has a much bigger memory requirement than a pool with texture format `PF_DXT1`. Similarly, a pool that contains multiple layers has a bigger memory requirement.
-   When rendering a higher output resolution, pool sizes should be larger.
-   A higher resolution output generally requests more higher resolution mip tiles.
-   Larger tile sizes may require a bigger pool size.
-   The default tile size for [Streaming Virtual Textures](/documentation/en-us/unreal-engine/streaming-virtual-texturing-in-unreal-engine) is 128 texels. However, that can be overridden.
-   The tile size of [Runtime Virtual Textures](/documentation/en-us/unreal-engine/runtime-virtual-texturing-in-unreal-engine) can be up to 1024 texels. Larger tile sizes often incur wasted space in the pool.

### Oversubscription

One particular cause of oversubscription is the application of a negative mip bias when sampling virtual textures. Systematically sampling higher resolution mips requires more pool memory. Negative mip bias comes from explicitly setting mip level or bias on a Texture Sample node in the Material Graph.

Oversubscription can also come from unexpected sources, such as when sampling a texture with zero gradient because the UVs are invariant for a triangle or mesh. The material graph snippet below is an example of this. This specific case can be solved by using a Mip Value setting of "Ignore Input WorldPosition" on the Runtime Virtual Texture Sample node.

![virtual texture pool oversubscription material example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/691b9310-4da1-4abc-a29f-9692edd1ef50/oversubscription-material-example.png)

Use the console command `r.VT.DumpPoolUsage` to help locate any textures that are taking up more space in the pool than expected due to mip bias, or other issues. This command dumps out the number of pages that each virtual texture asset currently allocates in each memory pool. The dump is sorted by page count so that the first entries should be checked to see if they are reasonable.

Note that in the following dump, the first entry is significantly higher than the others. So, materials that reference `T_Ground_Sand_F_basecolor_CANYON` should be checked for any mip bias issues.

```
	`PhysicaPool: [0] DXT1 (136x136): 		T_Ground_Sand_F_basecolor_CANYON 1912 		T_Rock_Quarry_Y_RAOD 418 		ubulehofw_8K_Albedo 324 		pcciQ_4K_Albedo 248 		T_Rock_Cliff_D_RAOD 187 		noise_directional_3 115 		T_column_260_B_W 97 		T_column_260_B_goldA_RMAOO 97 		T_column_260_B_goldA_C 96`

Copy full snippet
```
PhysicaPool: \[0\] DXT1 (136x136): T\_Ground\_Sand\_F\_basecolor\_CANYON 1912 T\_Rock\_Quarry\_Y\_RAOD 418 ubulehofw\_8K\_Albedo 324 pcciQ\_4K\_Albedo 248 T\_Rock\_Cliff\_D\_RAOD 187 noise\_directional\_3 115 T\_column\_260\_B\_W 97 T\_column\_260\_B\_goldA\_RMAOO 97 T\_column\_260\_B\_goldA\_C 96