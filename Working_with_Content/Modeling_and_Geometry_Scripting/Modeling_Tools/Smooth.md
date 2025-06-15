# Smooth

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/smooth-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/smooth-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:18

---

The **Smooth** tool softens the edges of surfaces by moving vertices towards the averaged location of their neighbors. This operation is helpful to use when a mesh has jagged edge artifacts.

![Jagged Cobble](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/403f8f4b-dd49-42e6-8088-fabbecc4d173/jagged-cobble.png)

![Smooth Cobble](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f59b4e4-d34e-4b2f-b38c-477f4ddc205f/smooth-cobble.png)

## Accessing the Tool

You can access the Smooth tool from the following:

-   The **Deform** category in **Modeling Mode**. To learn more about Modeling Mode and how to access it, see [Modeling Mode Overview](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
-   The **Editing Tools** tab in the **Skeleton Editor**. To learn more, see [Skeleton Editing](/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).

## Using Smooth

How you smooth your mesh is set by the **Smoothing Type** property. Each smoothing type has options to adjust the smoothing amount.

The **Fast Iterative** and **Fast Implicit** smoothing types have a vertex weight map option to adjust specific areas of your mesh. You must first create the weight map layer in the [Attribute Edit](/documentation/en-us/unreal-engine/edit-attributes-tool-in-unreal-engine) tool. The comparison images above use a weight map to create the cobblestone effect. To learn more about creating weight maps, see [Paint Maps Tool](/documentation/en-us/unreal-engine/paint-maps-tool-in-unreal-engine).

Sometimes, your mesh can seem to have disappeared when using the Smooth tool. Your mesh has not disappeared but has significantly smoothed and shrunken in size. This change in size happens based on the resolution (number of triangles) of your mesh and values used with the **Iterative Smoothing Options**.

To avoid this issue, do one of the following:

-   Increase the number of triangles the mesh has with the **Remesh** tool (you must cancel the current tool session to do this).
-   Lower the **Smoothing Per Step** setting under the **Iterative Smoothing Options**.
-   Lower the **Steps** settings under **Iterative Smoothing Options**.

Once you are done using the tool, accept or cancel the changes in the [Tool Confirmation](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine#tools,undohistory,andacceptingchanges) panel.

### Hotkeys

| **Key Command** | **Operation** |
| --- | --- |
| **F** | Zooms into the location of the mesh. |
| **ESC** | Cancels the changes and exits the tool. |
| **Enter** | Accepts the tool changes. |