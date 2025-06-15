# UV Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine)  
**Processed:** 2025-06-14 17:02:32

---

The **UV Editor** provides the toolset and **Viewports** for creating and modifying UVs. Compared to the **Level Editor's** UV tools, the UV Editor delivers a more interactive 2D view with fine-grain editing of UVs. In addition, it provides options such as:

-   Merging edges
-   UDIM management
-   Multi-Asset workflow

Before using the UV Editor, it is essential to understand the unique aspects of [modeling in-engine](/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine) and the [common terminology](/documentation/en-us/unreal-engine/uvs-category-in-unreal-engine) associated with creating UVs.

|   |   |
| --- | --- |
| ![UV Editor Default UVs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99f8c2c2-e3ff-4d46-ae17-8742e77d5bc4/uv-editor-deformed-uv.png) | ![UV Editor Custom UVs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae2a8a44-48ef-4305-86f6-c60b5563b494/uv-editor-unifrom-uv.png) |
| UVs with Distorted Texture | UVs with Uniform Texture |

When opening the UV Editor, the initial UV map shown is pulled from your imported mesh, and meshes created in-engine have default UVs created.

## The Default Interface

The UV Editor interface consists of four core components:

Click image to expand.

1.  [Toolbar](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#toolbar)
2.  [Tools](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#tools)
3.  [2D Viewport](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#2dviewport)
4.  [3D Viewport](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#3dviewport)

## Accessing the UV Editor

You can access the UV Editor from the following:

-   Use the **UV** category in **Modeling Mode**.
-   **Right-click** your mesh within your **Level**.
-   **Right-click** your mesh in the **Content Browser**.

## Toolbar

| Action | Description |
| --- | --- |
| **Save** | Save your UV map. |
| **Browse** | Opens the location of the current mesh in the **Content Browser**. |
| **Apply** | Applies your UV changes to your original mesh. |
| **Channels** | Switch between UV maps for a mesh. Use the [Channel tool](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#channels) to create and edit UV maps. |
| **Display** | Control the look of your 2D Viewport. |

#### Display

Using the **Display** tab, you can toggle the visibility of the grid and rulers in the 2D Viewport. You can also set the background to visualize textures mapped to your UVs.

Click image to expand.

In addition, you can label UDIMs based on the location of your UV Islands or from Textures. You can manually apply UDIMs using the **Active UDIMs** plus icon.

When a background is enabled, it displays automatically for the 0-1 unit square. UDIMs must be set for the background to appear correctly in other unit squares.

## Tools

Use the UV Editor tools to create and manage the desired UV map(s) for your mesh. When creating new UVs, you can use the [AutoUV](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#autouv) tool, then the remaining tools to work out the details. For a manual start, use the [**Seam**](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#seam) tool.

You can adjust Texture resolution using the **Layout**, **AutoUV**, and **Unwrap** tools.

### Sew

The **Sew** tool connects two corresponding edges. When using the tool, the selected edge will be highlighted in red, and its counterpart edge in green. These highlighted edges will combine once you click the Sew tool, creating a new UV island.

![Sewing UVs in UV Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cb62f92-0b7b-4162-af07-be69d797e99c/uv-sew.gif)

If you receive the warning that no viable sew candidate edges are selected then the selected edge is already connected within the UV island or is a boundary edge.

### Split

Use the **Split** tool to separate the UV coordinates of your mesh manually. You can split along a given selection of the following:

-   **Bowtie vertices**
    
    -   This disconnects the UV topology from any bowtie vertices within the selection.
        
        These are vertices that join triangles by one point instead of an edge. It is unnecessary to select individual bowtie vertices for the tool to work. Selecting UV islands and then using the Split tool will disconnect any existing bowtie vertices.
        
-   **Edges**
    
    -   This disconnects the UV topology at the edge(s).
        
-   **Triangles**
    
    -   This slices out whole regions.
    

The thicker-saturated outline of your UVs indicates a [seam](/documentation/en-us/unreal-engine/uv-editor-in-unreal-engine#seam). Use this to identify if you properly split your selection.

### Layout

The Layout tool helps organize your UV islands into a 0-1 space or within their originating UDIM when **Preserve UDIMs** is enabled.

The process of laying out UVs into a UV space is called UV packing. There are three Layout Types to help pack your UVs:

| Layout Type | Description |
| --- | --- |
| **Transform** | Transform applies scaling and translation to all your UVs, regardless if particular islands are selected. Keeps the current layout of the UVs. These scale and translation controls are available in Stack and Repack. |
| **Stack** | Uniformly scale and translate each UV island individually to pack in a unit square with overlap. Stacking can be useful when two UV islands share the same texturing design, removing the need for replication. |
| **Repack** | Uniformly scale and translate UV islands collectively to pack in a unit square with no overlap. Unique to Repack is the Allow Flips setting. Enabling this feature can save space when packing UVs but can lead to issues for downstream operations. |

The tool operates on the current selection of islands or all islands if nothing is selected.

### Transform

The **Transform** tool provides explicit numerical input for scale and translation compared to the gizmo in the 2D Viewport.

You can perform rapid transformations using the **Quick Translate** and **Quick Rotate** options. For further precision, use the **Advance Transform** section, where you have the option to adjust the pivot.

**Translation Mode** decides how to position the UVs using either of the following options:

-   **Relative** moves elements respective to their current position.
-   **Absolute** moves elements based on the **Manual** input in the **Transform Origin**.

**Transform Origin** decides the UVs' pivot location, which controls the relative motion of the transforming UVs.

| Transform Origin Mode | Description |
| --- | --- |
| **Bounding Box Center** | Pivots around the center of all island bounding boxes. |
| **Origin** | Pivots using the global origin of 0,0. |
| **Individual Bounding Box Center** | Pivots around each island's bounding box center. |
| **Manual** | Pivots based on a user-specified point. |

Transformation operations are performed in order from top to bottom.

### Align

Line up existing UVs based on their edges, vertices, or islands.

To further assist you to adequately position UVs, the following options are available:

-   The **Alignment Anchor** controls what geometry the alignment is relative to when performed.
-   **Grouping Mode** controls how alignment considers grouping the selection to the alignment behavior.

### Distribute

You can adjust the spacing of UV vertices and islands.

![Distribute Tool in UV Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/631faf00-af56-45ad-8358-bd776557a710/distribute-tool.gif)

Similar to the Align tool, use the Distribute tool to help remove stretching and distortion in your UVs.

### Channels

You can manage UV maps by adding, copying, and deleting channels. **UV Channels** consist of differentiating UV maps for one mesh.

Multiple UV Channels provide the ability to layer textures on your mesh, as well as [baking lights](/documentation/en-us/unreal-engine/understanding-lightmapping-in-unreal-engine). For example, with the crate, you can have one channel for the wooden texture and another for a Decal with the wording, *"FRAGILE"*.

To learn more about UV Channels, refer to the [Using UV Channels With Static Meshes](/documentation/en-us/unreal-engine/using-uv-channels-with-static-meshes-in-unreal-engine) documentation.

### Seam

Using the **2D** or **3D Viewport**, you can interactively separate edges to create seams. You automatically develop seams when at least two vertices are selected.

In addition to cutting new seams, you can also sew seams together. Use the **Mode** option to switch between **Split** and **Sew**. You can separate and combine multiple edges before clicking **Complete** in the Viewport by double-clicking the second vertice.

Be mindful of where your seams appear. You typically want seams invisible to your audience unless it is the desired aesthetic. Knowing what parts of your asset are visible in the experience is essential in understanding where to create seams

![Visable Seam in Center Beam](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89bb0401-8acd-4edb-8e42-7808c0535382/seam-1.png)

![Discrete Seam](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e2799cd-dd5b-498c-8b6b-c134400cb9ca/seam-2.png)

### AutoUV

You can automatically unwrap and pack your UVs using **AutoUV**. This automation is helpful as a starting point for custom UV mapping or background assets needing a quick UV map.

There are three methods for control: **UVAtlas**, **XAtlas**, and **PatchBuilder**.

| Method | Description |
| --- | --- |
| **Patch Builder** | Supports large models, such as Nanite. This is the default option built in-engine. |
| **UV Atlas** | 
Use for organic objects, to minimize stretching.

Does not work on Linux.



 |
| **XAtlas** | Designed for light maps and mechanical meshes. |

In **Patch Builder** and **UV Atlas** mode, you can layout UVs based on predefined PolyGroups. In addition, you can automatically organize the specified PolyGroups into UDIMs.

To visualize the numbering of each UDIM, use the Display dropdown menu.

### Unwrap

The **Unwrap** tool recomputes UVs for existing UVs or PolyGroups, helping minimize stretched and squashed areas (distortion).

The tool operates on the current selection of islands or all islands if nothing is selected.

How your UVs automatically unwrap is determined by the **Unwrap Type**.

| Unwrap Type | Description |
| --- | --- |
| **ExpMap** | Performs a fast unwrap but is limited in reducing distortion. |
| **Conformal** | Reduces distortion compared to ExpMap, but is increasingly expensive on large islands. |
| **SpectralConformal** | Compared to the Conformal method reduces the distortion further but is more expensive to compute. Additionally has the option Preserve Irregularity to remove unnatural distortion due to mesh irregularity. |
| **Island Merging** | UV islands are merged into larger islands if it does not increase distortion beyond defined limits. |

If you are texturing a simple geometry such as a flat plane, then all unwrap types will give you approximately the same result. If you are working with a mesh that is not uniformly tessellated and has a complex shape, Spectral Conformal is the best option. It provides the least distortion; however, it computes slower.

## 2D Viewport

The 2D Viewport represents the 2D Space (also referred to as UV or Texture Space) for displaying your UV map. It is the primary Viewport for unwrapping and packing UVs. Unique to this Viewport are the UV selection types in the table below.

|   |   |   |   |   |
| --- | --- | --- | --- | --- |
| ![UV Editor Vertices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8faeb4a-44c4-4410-9e19-42cb68d9dcb2/select-verticies.png) | ![UV Editor Edges](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b87efb8-103c-4880-a3f0-8c7144219c5f/select-edges.png) | ![UV Editor Triangles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92bd61b1-23dd-43a3-a1ce-a31e80ff06c4/select-triangles.png) | ![UV Editor Islands](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89db15aa-1833-4de4-bee5-143ba11295f3/select-islands.png) | ![UV Editor Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efd6e805-f4dd-4449-b03f-fb81397e0ec5/select-mesh.png) |
| **Select Vertices** | **Select Edges** | **Select Triangles** | **Select Islands** | **Select Mesh** |

The Viewport grid consists of what's known as unit squares. The default unit square for UVs is 0-1. A texture map is placed in one unit square and UDIMs are numbered by each unit square used starting at 1001.

Click image to expand.

UDIMs are created horizontally to a max of 10 units before continually up to the next row, repeating the process if needed.

### Controls

You have the following navigation options in the 2D Viewport:

-   Scroll with the middle mouse button to zoom in and out.
    
-   **Right-click** to translate the grid.
    

Avoid using hotkeys associated with the Level Viewport.

The Translate Gizmo mimics the one used for Modeling Mode and reorients when re-clicking the UV after performing a rotation.

## 3D Viewport

Live view of your UVs on your 3D mesh. Unique to the 3D Viewport is the **Focus Camera**, which snaps to your current selection of UVs. You can use the hotkey **Alt + F** when the 3D Viewport is active.

### Controls

When **Orbit Camera** is enabled, you have the standard navigation controls in addition to pan, orbit, and zoom. **Fly Camera** has the same navigations along with game-style controls.

To learn more about these controls, refer to the [Viewport Controls](/documentation/en-us/unreal-engine/viewport-controls-in-unreal-engine) documentation.

There is also the option to adjust the **View Mode** from the default **Lit** option. To learn more, see [Viewport Modes](/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine).

## Next Steps

Now that you're familiar with the basics of the UV Editor, you can:

-   Begin UV mapping your geometry.
-   Learn about using [Textures](/documentation/en-us/unreal-engine/textures-in-unreal-engine) and creating [Materials](/documentation/en-us/unreal-engine/unreal-engine-materials).