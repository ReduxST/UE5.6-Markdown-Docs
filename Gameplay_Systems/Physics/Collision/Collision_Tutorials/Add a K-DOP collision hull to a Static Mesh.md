# Add a K-DOP collision hull to a Static Mesh

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-k-dop-collision-hull-to-a-static-mesh-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/add-a-k-dop-collision-hull-to-a-static-mesh-in-unreal-engine)  
**Processed:** 2025-06-14 16:04:48

---

### Steps

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2daad4b-624d-41b4-bef1-613c1b297249/colref_collisionmenu_kdop.png)

There are a series of menu options in the **Static Mesh Editor** under the **Collision** menu entry, named *##DOP*, these are the **K-DOP** simple collision generators. **K-DOP** is a type of bounding volume, which stands for *K discrete oriented polytope* (where K is the number of axis aligned planes). Basically it takes K axis-aligned planes and pushes them as close to the mesh as it can. The resulting shape is used as a collision hull. In the **Static Mesh Editor** K can be:

-   **10** - Box with 4 edges beveled - you can choose X- Y- or Z-aligned edges.
-   **18** - Box with all edges beveled.
-   **26** - Box with all edges and corners beveled.

See below for an example. This tool is quite handy for packages full of pipes, pillars, and railings:

![kdop_sizes.jpg](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0943730-fdad-4c5e-8dc3-cdc7cff298fa/kdop_sizes.jpg)