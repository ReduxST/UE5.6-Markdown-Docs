# Using Nanite with Landscapes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-nanite-with-landscapes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-nanite-with-landscapes-in-unreal-engine)  
**Processed:** 2025-06-14 17:00:20

---

Nanite is Unreal Engine's virtualized geometry system. Nanite uses an internal mesh format and rendering technology to render pixel scale detail and high object counts. Nanite's compressed data format provides support for high detail meshes and fine-grained streaming with automatic level of detail.

You can use Nanite on your Landscape to improve performance with Nanite rendering, especially with regard to Virtual Shadow Maps. In-editor performance while the non-Nanite Landscape is in use is not representative of the runtime performance of the Nanite-enabled Landscape in your project until Nanite meshes are fully rebuilt. End users of your product should expect no visual improvement or downgrade since the source data is identical.

For more information on Nanite and its advantages, see [Nanite Virtualized Geometry](/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine).

Sometimes, parts of your landscape may use standard rendering, or Nanite meshes might not be fully updated. This is expected behavior. To make such issues disappear, save or cook your project.

## Technical Considerations

Nanite Landscapes stream on top of the existing Landscape data streaming since both Nanite and non-Nanite data are necessary at runtime. Non-Nanite Landscape data is required for Runtime Virtual Textures, water rendering, and more.

This means twice the amount of data is streamed. One set of data for Nanite streaming and another set for texture streaming. Enabling Nanite causes both sets of data to reside in memory.

Hierarchical Level of Detail (HLOD) and Landscape proxy streaming behaves identically to non-Nanite Landscapes.

## Enable Nanite on a Landscape

To use Nanite with your Landscape terrain, select your Landscape and use the **Details** panel to check the box next to **Enable Nanite**.

To use Nanite with your Landscape terrain:

-   Select your Landscape in the Viewport.
-   In the **Details** panel, find **Enable Nanite**, and check the box next to it.

Enable Nanite on your Landscape in the Details panel.

There are two ways to build the Nanite mesh representation from Landscape data:

-   In the Landscape's **Details** panel, go to the **Nanite** section, and click **Rebuilt Data**.
    
    Or
    
-   Use the **Build** menu to select **Build Nanite Only**.
    

The build time for the Landscape depends on the size of the Landscape and the number of tiles. When complete, you can view the Nanite geometry using the Nanite visualization modes.

If Landscape Actors show the following viewport message:

A Nanite error message.

Their Nanite meshes are not up-to-date (for example, after a sculpt operation).

Rebuilding the Nanite data or saving the Landscape proxy mesh removes the message.

## Nanite Skirts

Nanite Landscape relies on standard Nanite techniques for LODs and vertex decimation. The resulting mesh won't use a regular grid topology unless the camera gets very close to it, but will contain more vertices where necessary to retain shape. Because of this, the borders between Landscape Proxy Actors have vertices that might not be evenly distributed on each side of the border. At large distances this can introduce seam artifacts, which appear as tiny holes through the landscape. These are usually small enough to be corrected by temporal anti-aliasing.

You can use the Nanite Skirt enable option to avoid seams.This functionality expands the Nanite landscape mesh by an additional row/column of vertices at the edges of the mesh and move those new vertices down by an amount specified by the **Nanite Skirt Depth**:

Enable the Nanite Skirt option on your Landscape in the Details panel.

This causes neighboring Nanite Landscape meshes to criss-cross each other and prevent seam artifacts from appearing.

## Useful Console Commands

The following console variables are useful when you're working with Nanite-enabled Landscapes:

| **Console Command** | **Description** |
| --- | --- |
| **Landscape.RenderNanite** | 
Enables Nanite rendering for Landscapes.

The default value is 1.



 |
| **Landscape.Nanite.LiveRebuildOnModification** | 

Triggers a rebuild of the Nanite representation whenever a modification is performed.

This function is Experimental.

The default value is 0.



 |
| **Landscape.Nanite.MultithreadedBuild** | 

Enables rebuilding of Nanite-enabled Landscape meshes using multiple processor threads to improve performance when working with several Landscape components.

The default value is 1.



 |

When you're editing Nanite-enabled Landscapes, we recommend that you keep the live rebuilding of Nanite meshes toggled off (`Landscape.LiveRebuildNaniteOnModification 0`), as this might decrease performance significantly. Landscape rendering relies on non-Nanite Landscapes until the Nanite mesh is rebuilt and up-to-date. Unreal Engine uses that version for rendering until it is fully rebuilt, so the editing experience is identical to working with non-Nanite Landscape actors.