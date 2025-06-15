# Setting Up a Vertex Color Material for Mesh Painting

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-vertex-color-material-for-mesh-painting-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-a-vertex-color-material-for-mesh-painting-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:09

---

When you use the Vertex Color mode with mesh painting, the vertex color data is used with a material to color the mesh. To do this, you use the **Vertex Color** material expression in a material graph with some logic to effectively use this color data.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed3c26b3-4b23-4da7-9893-93ac7d098b01/vertexcolornode.png)

Vertex Color Material Expression.

There are many ways in which you can use this color-painted data with a Vertex Color material expression. The sections below demonstrate how to add vertex-painted color to an existing material to tint that color in some way. This is one way you can use the Vertex Color expression with your materials with the mesh painting system.

To learn more about vertex color materials and how you can use them to blend textures layers together for painting on a mesh, see [Setting Up a Texture Blended Material for Mesh Painting](/documentation/en-us/unreal-engine/setting-up-a-texture-blended-material-for-vertex-weights-painting-in-unreal-engine).

## The Mesh and its Material

The example mesh and its material below demonstrate how to integrate vertex color workflows into your existing materials.

|   |   |
| --- | --- |
| ![Base Static Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4fbeba16-8a88-4a0e-af4a-83385c256d62/base-static-mesh.png) | ![Base material applied to a static mesh.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53bb9ba3-47d6-49f0-a8ae-a8c0ff7857a2/base-material.png) |
| Base Static Mesh | Base material applied to the mesh. |

## Vertex Color Material Setup

To set up a paintable material that takes in painted vertex color to tint an existing base color in a material, add a **VertexColor** material expression that plugs the RGB color channel into the **A** input of a **Multiply** node.

![Simple Vertex Color Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/76bd6497-a7be-4a3b-a769-00b945fc8edb/vertex-color-example.png)

Next, plug the material logic for your Base Color (Albedo) into the **B** input of the **Multiply** node, and then plug the output of the Multiply into the **Main Material** node.

The material should look similar to the image below with its paintable vertex color setup.

![Example of a vertex color node in a material graph.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df340a29-4621-4871-a657-d2e4265e02d7/vertex-color-material-setup.png)

## Using a Vertex Color Material to Paint on a Mesh

When you switch to the **Mesh Paint** mode in the level viewport, select the **Vertex Color** tab in the mode toolbar.

![Vertex Color paint mode selection.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc22a92b-4ce1-490d-8481-2b852dfc3903/vertex-color-paintmode.png)

To get started, use this workflow:

1.  Use the **Select** tool to click on your mesh that has a material setup to use vertex color painting.
2.  Switch to the **Paint** tool and choose a **Paint Color** to apply to your mesh.
3.  Use the **Color View Mode** dropdown selection to inspect the painted colors, as needed.

With this change to your material, you can paint a color that tints the base material.