# Groom Asset Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:26:27

---

The **Groom** system is designed to handle hair strands from imported groom Alembic `.abc` files. However, for scalability purposes, it also supports alternative geometry representations using cards and meshes. All of these geometric representations are managed within a single asset and component for ease of setup. The **Groom Asset Editor** manages most of the aspects of your groom, enabling you to modify various parts of the groom for how it's rendered, how it handles physics simulation, creating and managing levels of detail (LODs), and much more.

## Opening the Groom Asset Editor

The Groom Asset Editor is opened from the Content Browser by **double-clicking any Groom Asset**, or through the **right-click context menu of a Groom Asset**.

![Groom Asset in the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a5a4ebec-f872-4ef6-9f64-82a42c90906c/01-groom-asset-in-the-content-browser.png)

## Groom Asset Editor Interface

The Groom Asset Editor is comprised of these regions:

Click image for full size.

1.  [Viewport Display Options](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine#viewportdisplayoptions): Includes viewport options, view perspectives, view modes, debug views, and level of detail visualization.
2.  [Viewport](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine#viewport): Displays the groom asset with its assigned materials, level of details, and physics representation.
3.  [Details Panels](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine#detailspanels): Includes

## Viewport Display Options

The **Viewport Display Options** toolbar provides basic rendering and visualization options.

![The Viewport Display Option Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a434f4ac-537d-4019-b202-c23e68b2f7b6/03-viewport-display-options-toolbar.png)

### Viewport Options

The **Viewport Options** dropdown menu provides basic rendering options within the viewport. You can toggle real-time mode, change the field of view, and set the screen percentage for supersampling.

These options, and more, are accessed using the dropdown **arrow** in the viewport display options toolbar.

![Viewport Options Dropdown Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1d6604a-ca46-4749-bf08-999d8dd676ca/04-viewport-options-dropdown-menu.png)

### Perspectives

The **Perspectives** dropdown provides perspective and orthographic views; a perspective view that's a 3D window into the level, and orthographic views that are 2D viewports that look down on of the main XYZ axes.

![The Perspectives Viewport Dropdown Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e971e0d8-0618-429d-8fa8-dc10edf914e0/05-perspectives-dropdown.png)

### View Modes

The **View Modes** dropdown provides a number of visualization options common to all editor viewports, such as lighting, optimization, materials, and exposure value control for the viewport.

![The View Modes Dropdown Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d31e2da6-886b-448a-8ce0-7bda1177ee4f/06-view-modes-dropdown.png)

### Show

The **Show** dropdown provides Groom Asset Editor specific visualization options to help you see the type of data being processed in your scene, as well as diagnose errors or unexpected results for this groom.

![The Show Dropdown Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e111c61e-154b-4b86-a2f3-d250b07e8783/07-show-dropdown.png)

| Property | Description |
| --- | --- |
| **Guide** | Displays the guides used for simulation. |
| **Guide Influence** | Shows simulation clumps (all the strands influenced by one guide) in color visualization. |
| **UV** | Displays the UV along each strand. |
| **Root UV** | Displays the UV at the root of each strand. |
| **Root UDIM** | Displays the UDIM at the root of each strand. |
| **Dimension** | Displays the width/length variations of each strand. |
| **Seed** | Displays (in color) the random seed used per strand. |
| **Radius Variation** | Shows (in color) the size of the strands. Blue represents thinner strands. Yellow represents thicker strands. |
| **Tangent** | Displays tangents direction of each strand. |
| **Base Color** | Displays the base color stored per vertex. If base color is not exported from your modeling application with your groom, the strands will appear black. |
| **Roughness** | Displays the roughness stored per vertex. If the roughness is not exported from your modeling application with your groom, the strands will appear black. |
| **Hair CVs** | Displays hair strands CVs. |
| **Vis. Clusters** | Shows clusters of hair used for culling and level of detail purposes. |
| **Hair Groups** | Displays hair groups. |
| **Cards Guide** |   |

These are some example visualizations from the **Show** dropdown.

|   |   |   |   |
| --- | --- | --- | --- |
| ![Show Seed Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dea61b3e-fab5-4fa3-8a68-c511fed1a6a0/08-show-seed.png) | ![Show Hair CVs Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea2becb4-bc2a-492c-b665-845053627ac6/09-show-hair-cvs.png) | ![Show Vis. Clusters Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd36b465-bb31-4420-a2e6-ac005354d4da/10-show-vis-clusters.png) | ![Show Base Color Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2482d9d2-0ea3-44d3-a591-57602b88fea9/11-show-base-color.png) |
| Seed | Hair CVs | Vis.Clusters | Base Color |

### LODs

The LODs dropdown enables you to visualize levels of detail within the viewport automatically or by specifying a particular level.

![The LODs Dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c3974c2-81b4-493c-82a4-35951cbd229d/12-lods-dropdown.png)

Switch between LODs automatically based on the options specified in the [Level of Detail](/documentation/en-us/unreal-engine/groom-asset-editor-user-guide-in-unreal-engine#levelofdetail) panel when using the LODs Auto option. This option automatically switches LODs based on their screen size in the viewport. Alternatively, use the dropdown to select from the available levels of detail that have already been generated to see them represented regardless of screen size.

## Viewport

The **Viewport** is where you can view your imported Groom Asset with changes made in its different details panels, and use different visualization and debug view modes to inspect your groom.

## Details Panels

The Groom Asset Editor has several **Details** panels to set and configure a variety of attributes related to your groom.

![Groom Asset Editor Details Panels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98313ce1-ce76-4d1e-bfa2-ad03a58c652e/groom-editor-panels.png)

Explore the pages below to learn more about each of these Details panels:

| Details Panel | Description |
| --- | --- |
| [Level of Detail](/documentation/en-us/unreal-engine/setting-up-level-of-detail-for-grooms-in-unreal-engine) | Use this panel to configure the number of LODs your groom has and each of their properties. |
| [Interpolation](/documentation/en-us/unreal-engine/groom-interpolation-in-unreal-engine) | Use this panel to define how the groom's curves should move with respect to skinning and physics simulation. |
| [Strands](/documentation/en-us/unreal-engine/groom-strands-in-unreal-engine) | Use this panel to configure properties of your groom's strand geometry. |
| [Cards](/documentation/en-us/unreal-engine/setting-up-cards-and-meshes-for-grooms-in-unreal-engine) | Use this panel to configure and generate card geometry for your groom's LODs. These cards are generated and assigned per-LOD. |
| [Meshes](/documentation/en-us/unreal-engine/setting-up-cards-and-meshes-for-grooms-in-unreal-engine) | Use this panel to configure and generate mesh geometry for your groom's LODs. These can be generated and assigned per-LOD. |
| [Materials](/documentation/en-us/unreal-engine/groom-materials-in-unreal-engine) | Use this panel to assign materials to your groom. |
| [Physics](/documentation/en-us/unreal-engine/enabling-physics-simulation-on-grooms-in-unreal-engine) | Use this panel to set up your groom's physics simulation. |