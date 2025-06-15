# Render Resource Viewer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/render-resource-viewer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/render-resource-viewer-in-unreal-engine)  
**Processed:** 2025-06-14 16:46:47

---

The **Render Resource Viewer** is a tool that provides a snapshot in time — captured when the window opens — of where all GPU memory allocations are going and to what render resources. These include Vertex and Index buffers, and the types of assets they come from. This tool is useful for artists and developers to identify and understand which assets are making allocations. It also provides the information needed to optimize GPU memory and keep a project within its rendering budget.

![Render Resource Viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/895f40b3-1978-4087-9581-25c95832eceb/render-resource-viewer-interface-5-3.png)

This tool includes an interactive interface that:

-   Displays each render resource allocation with its name, size, type, flags, and owner.
-   Has a sortable and filterable table of allocations.
-   Provides information to identify and understand which assets are making the allocations.

## Open the Render Resource Viewer

You can open the **Render Resource Viewer** from the **Tools** menu.

![UE Main menu to launch Render Resource Viewer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c0d42896-ef6f-4c85-b4d8-5ffeb18ca12e/opening-rrv.png)

## Working with the Render Resource Viewer Interface

The Render Resource Viewer interface is made up of the following:

-   **Refresh Button**
    -   The viewer creates a snapshot in time when it is opened and doesn't automatically update in real-time. Use this button to refresh the list and create a new snapshot of GPU memory allocations.
        
        ![Render Resource Viewer Interface Refresh Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db2726ea-540d-44e9-8df9-5285c8a17ec5/render-resource-viewer-interface-refresh-5-3.png)
-   **Resource Filters**
    -   Each resource has some rendering flags. Use these resource checkboxes to show filtered entries relevant to your search. Choose from the following resources:
    -   **Resident:** Is accessible by the GPU, and not evicted (unused).
    -   **Transient:** Is only allocated during the duration of the render passes where it is active and it will share underlying memory with other resources in the frame. (This filter is unchecked by default.)
    -   **Streaming:** Is a streamable texture.
    -   **Render Target (RT):** Can be written to as a Render Target buffer by the GPU.
    -   **Depth Stencil (DS):** Can be written to as a Depth Stencil buffer by the GPU.
    -   **Unordered Access View (UAV):** Supports Unordered Access View which allows temporarily unordered read/write access from multiple GPU threads without generating memory conflicts.
    -   **Ray Tracing Acceleration Structure (RTAS):** Is a Ray Tracing Acceleration Structure.
        
        ![Render Resource Viewer Interface Filter By Flags](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4128fd93-cff5-4a76-bbcd-bc672c61967f/render-resource-viewer-interface-filterbyflags-5-3.png)
-   **Search Box**
    -   Searches text from both the **Resource Name** and **Owner** categories. For example, it can be hard to find all resources belonging to a skeletal mesh, but by searching its owner's path, you can see the total memory being used.
        
        ![Render Resource Viewer Interface Search Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5da25c0-48f2-4437-a84e-33d99ab8d7e7/render-resource-viewer-interface-search-5-3.png)
-   **Resource Totals**
    -   Displays the total number of entries and their combined size in the list. Changing the filtered flags and searching lists only the filtered results and their totals.
        
        ![Render Resource Viewer Interface Totals of all Resources](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b86f32ce-3dcf-4757-8954-c9a0595ede16/render-resource-viewer-interface-resourcetotals-5-3.png)
-   **Resource Table**
    -   The window includes listed information about a given resource occupying memory. In this window, you see the name of the resource, its type, size, and flags, and the owner of that resource. The Owner column provides the path name of the UObject the resource belongs to, including its LOD index.
        
        ![Render Resource Viewer Interface Resource List](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/763a5589-b75d-4b55-a604-bcd6ebee02d4/render-resource-viewer-interface-resourcewindow-5-3.png)

## Additional Notes

### Owner is None

When a resource has an owner as "None", it means the resource owner is not currently tracked. Currently tracked resources include static meshes, skeletal meshes, textures, and hair/groom assets. The list of tracked resources will continue to grow.

### Owner Paths and LOD Index

If the resource belongs to a mesh, the Owner path will also indicate the LOD index that mesh belongs to at the end of the path. For example, the Quinn mannequin included with some of the default templates in Unreal Engine has multiple levels of detail set up. When looking at the resource entry for this skeletal mesh, the path looks like `/Game/Characters/Mannequins/Meshes/SKM_Quinn.SKM_Quinn[LOD1]`.

### Browse to Asset in the Content Browser

You can find listed entries assets using either the hot key **CTRL + B** or right-clicking on them and selecting **Browse to Asset**. This opens the Content Browser to show their location. If there is no asset path associated with the **Owner** **column**, no action is taken.

![Right-click on an entry to browse to its asset in the Content Browser.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8372bac-b1f3-4846-ae32-73833e862e03/browstoasset.png)