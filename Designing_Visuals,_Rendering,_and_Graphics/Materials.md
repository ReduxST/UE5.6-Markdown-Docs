# Materials

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials)  
**Processed:** 2025-06-14 16:57:00

---

**Materials** in Unreal Engine define the surface properties of the objects in your scene. In the broadest sense, you can think of a Material as the "paint" that is applied to a mesh to control its visual appearance.

In more technical terms, Materials tell the render engine exactly how a surface should interact with the light in your scene. Materials define every aspect of the surface including color, reflectivity, bumpiness, transparency, and so on. These calculations are done using data that is input to the Material from a variety of images (textures) and node-based **Material expressions**, as well as from various [property settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-properties) inherent to the Material itself.

## Getting Started

Material creation is a broad topic, and the node-based workflow allows you to create an almost infinite variety of surface types. Beginners are recommended to start with with the pages linked in this section. The Essential Material Concepts and Physically Based Materials pages introduce the theory and ideas that form the foundation of Material creation in Unreal. The Material Editor User Guide is a set of tool-based documentation that teaches practical aspects of using the Material Editor.

[

![Essential Material Concepts](https://dev.epicgames.com/community/api/documentation/image/465086e4-09bf-4c2e-b532-b4fa2ea14956?resizing_type=fit&width=640&height=640)

Essential Material Concepts

An introductory document on Materials in Unreal Engine.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/essential-unreal-engine-material-concepts)[

![Designing Visuals, Rendering, and Graphics](https://dev.epicgames.com/community/api/documentation/image/6f554451-3f4a-4cac-865e-432e405fa7a3?resizing_type=fit&width=640&height=640)

Designing Visuals, Rendering, and Graphics

Rendering subsystem including lighting and shadowing, materials and textures, visual effects, and post processing.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/designing-visuals-rendering-and-graphics-with-unreal-engine)[

![Physically Based Materials](https://dev.epicgames.com/community/api/documentation/image/98cd2fab-397a-494c-886f-168211c69201?resizing_type=fit&width=640&height=640)

Physically Based Materials

An overview of the primary physically based Material inputs and how best to use them.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine)[

![Material Editor Guide](https://dev.epicgames.com/community/api/documentation/image/72872fe1-0e78-4f46-ae0b-de38a93bf712?resizing_type=fit&width=640&height=640)

Material Editor Guide

Learn about Unreal Engine's node-based material editor to create materials which define the appearance and surface properties of objects in your scene.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide)[

![Material Properties](https://dev.epicgames.com/community/api/documentation/image/5dbfa075-4a29-4ade-a2fb-be1bb67ee3c3?resizing_type=fit&width=640&height=640)

Material Properties

An introductory document on Material Properties in Unreal Engine.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-properties)[

![Material Inputs](https://dev.epicgames.com/community/api/documentation/image/a4edb7ab-d5f9-470a-a063-02fccbdd4423?resizing_type=fit&width=640&height=640)

Material Inputs

An in-depth look at the various inputs available on a Material and how they are used.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine)[

![Material Data Types](https://dev.epicgames.com/community/api/documentation/image/788d85df-73c8-4402-91a7-1b01f76c9304?resizing_type=fit&width=640&height=640)

Material Data Types

An introduction to the four types of float data in the Material Editor





](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-data-types-in-unreal-engine)

## Substrate Material Framework

This system is experimental.

[

![Substrate Materials](https://dev.epicgames.com/community/api/documentation/image/830a4be5-131a-4465-b8e3-e929042f9b5a?resizing_type=fit&width=640&height=640)

Substrate Materials

Topics and reference about using the Substrate Materials framework.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/substrate-materials-in-unreal-engine)

## Material Workflow Concepts

Once you understand the basic principles behind Material creation, the documents in this section are strongly recommended as a next step. **Material Instances** and **Material Functions** are foundational topics in Material creation, and help you optimize your workflow to save time and avoid doing the same work twice. Material Instances allow you or other artists on your team to quickly and easily customize Materials to produce multiple variations (or instances) from a single parent Material. Material Functions allow you to package parts of a Material graph into a single node, and share it to a common library for reuse in other Materials.

[

![Instanced Materials](https://dev.epicgames.com/community/api/documentation/image/8500d1c4-e247-465e-befe-bd71fa4b563d?resizing_type=fit&width=640&height=640)

Instanced Materials

Hierarchical Material relationships help you alter the behavior and appearance of child Materials without recompiling the shader.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine)[

![Material Functions](https://dev.epicgames.com/community/api/documentation/image/a5357430-ca69-4609-99f0-7bfb088d9fa1?resizing_type=fit&width=640&height=640)

Material Functions

Snippets of Material that you can save in packages and reuse across multiple Materials.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-functions-in-unreal-engine)[

![Layered Materials](https://dev.epicgames.com/community/api/documentation/image/307ce731-a45d-4431-b3f7-69a28a6ffb84?resizing_type=fit&width=640&height=640)

Layered Materials

Two methods for layering Materials to create complex, unique surfaces.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/layering-materials-in-unreal-engine)

## Tutorials Index

The pages in this section are step-by-step, project based documents that walk you through some specific aspect of Material creation in Unreal. For example: [Animating UV Coordinates](https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-uv-coordinates-in-unreal-engine), or [Using Texture Masks](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-texture-masks-in-unreal-engine).

[

![Materials Tutorials](https://dev.epicgames.com/community/api/documentation/image/7b6fad41-753b-4d80-b468-7eba5b43c3b1?resizing_type=fit&width=640&height=640)

Materials Tutorials

Tutorials demonstrating various aspects of Material creation in Unreal Engine.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials-tutorials)

## Material Reference Pages

The [Material Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide) provides dozens of **Material Expressions** and **Functions**, each meant to perform some specific task in your Material graph. If you are looking for information about how and when to use a specific node, start with the pages linked below. The Material Expression and Function reference pages are organized according to their categories in the Materials palette — for example, Blends, Gradients, Math, Coordinates, and so on.

[

![Material Expressions Reference](https://dev.epicgames.com/community/api/documentation/image/19f5bf40-044b-4a54-9089-9393f1c5b6ad?resizing_type=fit&width=640&height=640)

Material Expressions Reference

Reference for all Material expressions available for use in the Material Editor.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-expressions-reference)[

![Material Functions Reference](https://dev.epicgames.com/community/api/documentation/image/988af5c5-c3df-4b78-8077-b40927165f81?resizing_type=fit&width=640&height=640)

Material Functions Reference

Reference pages for each of the default Material Functions, organized by category.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-functions-reference)[

![Material Editor UI](https://dev.epicgames.com/community/api/documentation/image/da269570-1d2e-412d-bc51-ee77f3c698e0?resizing_type=fit&width=640&height=640)

Material Editor UI

A breakdown of the Material Editor user interface.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-ui)[

![Material Instance Editor UI](https://dev.epicgames.com/community/api/documentation/image/6d514ff4-fd86-427c-8f64-6a30beaf3ce7?resizing_type=fit&width=640&height=640)

Material Instance Editor UI

Guide to using the Material Instance Editor for modifying MaterialInstanceConstants.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui)

## Additional Concepts and Tools

Materials pages that do not fit more precisely into another category are found below. Many of these are intermediate to advanced topics that allow you to progress beyond the basics of Material creation and begin to develop more sophisticated Materials for your projects.

[

![Bent Normal Maps](https://dev.epicgames.com/community/api/documentation/image/923612d3-788c-4afa-bbdc-f27abb43a0a4?resizing_type=fit&width=640&height=640)

Bent Normal Maps

An overview of using Bent Normal maps in Unreal Engine.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/bent-normal-maps-in-unreal-engine)[

![Bump Mapping Without Tangent Space](https://dev.epicgames.com/community/api/documentation/image/21c3b960-bbd3-40b0-b4d9-d72a535ef68a?resizing_type=fit&width=640&height=640)

Bump Mapping Without Tangent Space

How to achieve bump mapping from 3D procedural shaders where classic tangent space does not work.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/bump-mapping-without-tangent-space-in-unreal-engine)[

![Curve Atlases in Materials](https://dev.epicgames.com/community/api/documentation/image/3bd54120-e5b3-4bd2-8a41-0afab103dc26?resizing_type=fit&width=640&height=640)

Curve Atlases in Materials

Curve Atlases store a combination of Curve assets that enables you to access Curve Linear Color data through your Materials.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/curve-atlases-in-unreal-engine-materials)[

![Customized UVs](https://dev.epicgames.com/community/api/documentation/image/3d09138b-50ef-4526-a282-d21d77fdac5f?resizing_type=fit&width=640&height=640)

Customized UVs

Feature that allows running calculations in the vertex shader to increase performance over running them per-pixel.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/customized-uvs-in-unreal-engine-materials)[

![Material Analyzer](https://dev.epicgames.com/community/api/documentation/image/e7b26ff4-74eb-4afe-93cb-cc256e6fb240?resizing_type=fit&width=640&height=640)

Material Analyzer

This page describes how to locate and use the Material Analyzer tool.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-analyzer-tool)[

![Refraction Using Pixel Normal Offset](https://dev.epicgames.com/community/api/documentation/image/5955055a-160d-403c-aca4-d50835c0af04?resizing_type=fit&width=640&height=640)

Refraction Using Pixel Normal Offset

Overview of the Refraction Mode for Pixel Normal Offset in your Materials.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/refraction-using-pixel-normal-offset-in-unreal-engine)[

![Storing Custom Data in Materials Per-Primitive](https://dev.epicgames.com/community/api/documentation/image/0efaeddf-a1e7-40f9-8b12-fd53c6043459?resizing_type=fit&width=640&height=640)

Storing Custom Data in Materials Per-Primitive

An overview of the Custom Primitive Data workflow for storing custom data per primitive that's accessible through Blueprint.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/storing-custom-data-in-unreal-engine-materials-per-primitive)[

![Lit Translucency](https://dev.epicgames.com/community/api/documentation/image/fc766164-f7a1-4cbc-8463-ed04d625acd6?resizing_type=fit&width=640&height=640)

Lit Translucency

Explanation of how translucent surfaces are lit and cast shadows including self-shadows.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/lit-translucency-in-unreal-engine)