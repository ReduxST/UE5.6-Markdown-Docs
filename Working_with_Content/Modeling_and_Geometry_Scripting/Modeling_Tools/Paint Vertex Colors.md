# Paint Vertex Colors

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/paint-vertex-colors-tool-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/paint-vertex-colors-tool-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:31

---

The **Paint Vertex Colors** tool adds color values to the vertices of a mesh (including nanite meshes). The painted values are stored in the R, G, B, and A channels. You can use the tool for many workflows, such as:

-   Editing imported vertex colors
    
-   Creating textures (using the **Vertex Color** node)
    
-   Making masks
    

[![Paint Vertex Colors Tool](https://dev.epicgames.com/community/api/documentation/image/be27773f-f37f-4828-b4ba-b029ec49261e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/be27773f-f37f-4828-b4ba-b029ec49261e?resizing_type=fit)

To visualize vertex colors outside of the tool, from the **Viewport** toolbar, click **Show > Advance > Vertex Colors**. However, the visibility feature does not work on Nanite-enabled meshes.

## Asset and Instance Vertex Colors

The Paint Vertex Colors tool is similar to the **Mesh Paint Mode**. However, the tool only adds vertex colors to the static mesh asset and does not create unique vertex colors for static mesh instances. Instances of a static mesh asset share the same vertex data, making the Paint Vertex Colors tool available for Nanite geometry. To learn more about Nanite and its supported features, see [Nanite Virtualized Geometry.](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine)

To perform instance vertex painting (vertex colors stored on the component in the level), use the **Mesh Paint Mode**. To learn more, see [Mesh Paint Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/mesh-paint-mode-in-unreal-engine).

| Color Type | Description |
| --- | --- |
| 
**Asset Vertex Colors**

 | 

Vertex colors stored on the asset. All instances of the asset share the same data set. Usable on nanite meshes.

 |
| 

**Instance Vertex Colors**

 | 

Unique vertex colors are created per instance of an asset. Usable in the Mesh Paint Mode only. You cannot use it for Nanite-enabled meshes as per-component vertex colors are not supported.

 |

Although instance color vertex data is not available, you can establish unique vertex colors for an asset using the following:

-   Storing data in individual R, G, B, or A channels
    
-   Setting [PolyGroup layers](working-with-content/modeling-and-geometry-scripting/modeling-mode/understanding-polygroups)
    

## Accessing the Tool

[![Paint Vertex Colors Tool](https://dev.epicgames.com/community/api/documentation/image/26a5f158-85cf-406c-8181-c92fc287e544?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/26a5f158-85cf-406c-8181-c92fc287e544?resizing_type=fit)

You can access the **Paint Vertex Colors** tool from the following:

-   **Modeling Mode** ****\>** Deform** category. To learn more, see [Modeling Mode Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).
    
-   **Skeleton Editor** ****\>** Editing Tools **\> Skin**** category. To learn more, see [Skeleton Editing](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editing-in-unreal-engine).
    

## Using Paint Vertex Colors

You paint vertex colors using the brush options in the **Action** section.

| Action | Description |
| --- | --- |
| 
**Paint Vertices**

 | 

Paint vertices of hit triangles with a smooth falloff. You can adjust additional settings, such as brush size and flow, in the Brush section.

 |
| 

**Paint Triangles**

 | 

Fill any painted triangles by setting all three vertices to the same color. You can adjust additional settings, such as brush size and flow, in the Brush section.

 |
| 

**Flood Fill Connected**

 | 

Fill any triangles connected to the brushed triangles. You can adjust additional settings, such as brush size and flow, in the Brush section.

 |
| 

**Flood Fill Groups**

 | 

Fill any PolyGroups connected to the brushed triangles. You can adjust additional settings, such as brush size and flow, in the Brush section.

 |
| 

**Poly Lasso**

 | 

Paint any triangles inside polygonal or freehand Lassos drawn in the viewport.

 |

The **Secondary Brush** provides additional operations for your **Action** selection.

| Secondary Brush | Description |
| --- | --- |
| 
**Erase**

 | 

Paint the color set in the **Erase Color** property. The default value is (1, 1, 1, 1).

 |
| 

**Soften**

 | 

Blend any split color values at painted vertices.

 |
| 

**Smooth**

 | 

Blend vertex colors with nearby vertex colors.

 |

For greater painting control, such as bounding to UV seams and painting front-facing vertices, use the **Filters** section.

The **Paint Color** and **Blend Mode** sections control how your colors appear. You can also use the **Channel Filters** section to visualize your colors and store values in individual channels.

The tool consists of **Quick Actions** and **Utility** sections to help create an efficient vertex painting workflow. These sections consist of the following properties.

| Property | Description |
| --- | --- |
| 
**Paint all**

 | 

Fill all vertex colors with the value set in Paint Color. Current values set in Channel Filter apply.

 |
| 

**Erase all**

 | 

Fill all vertex colors with the value set in Erase Color. Current values set in Channel Filter apply.

 |
| 

**Fill black**

 | 

Fill all vertex colors with the value (0,0,0,1). Current values set in Channel Filter apply.

 |
| 

**Fill white**

 | 

Fill all vertex colors with the value (1,1,1,1). Current values set in Channel Filter apply.

 |
| 

**BlendAll**

 | 

Average the current color values at each vertex with split colors, so there are no split vertices or seams in the color value.

 |
| 

**Fill Channels**

 | 

Set all selected channels to a fixed value.

 |
| 

**Invert Channels**

 | 

Invert channel values.

 |
| 

**Copy Channel to Channel**

 | 

Copy a color value from a source channel to all selected channels.

 |
| 

**Swap Channel**

 | 

Switch values between two channels.

 |
| 

**Copy Weight Map**

 | 

Copy values from a weight map into vertex color channels.

 |
| 

**Copy to other LODs**

 | 

Copy current values to any LODs defined on the mesh.

 |
| 

**Copy to High Res LOD**

 | 

Copy current values to a specific LOD defined on the mesh.

 |

Once you are done using the tool, you can accept or cancel the changes in the [Tool Confirmation](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine) panel.

You can use the **Bake Vertex Colors** tool to copy your vertex color data to another static mesh. However, the more the vertex positions differ, the less accurate the vertex colors will be.

### Hotkeys

| Hotkey | Description |
| --- | --- |
| 
**Shift + G**

 | 

Pull color value at the cursor location.

 |
| 

**Shift + Click**

 | 

Erase color. Click and hold to continuously erase. Use the **Erase Color** property to set the color that appears when erasing.

 |
| 

**\[ or S**

 | 

Decreases the size of the brush by 0.025 with each key press. Holding the Shift key will decrease the size by 0.005 each key press.

 |
| 

**\] or D**

 | 

Increases the size of the brush by 0.025 with each key press. Holding the Shift key will increase the size by 0.005 each key press.

 |
| 

**F**

 | 

Zooms into the location of the brush.

 |
| 

**Enter**

 | 

Accept tool changes.

 |
| 

**ESC**

 | 

To cancel the changes and exit the tool.

 |