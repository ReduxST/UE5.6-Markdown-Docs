# Using Materials and Textures in Unreal Engine for Maya Users

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-materials-and-textures-in-unreal-engine-for-maya-users](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-materials-and-textures-in-unreal-engine-for-maya-users)  
**Processed:** 2025-06-14 16:59:50

---

The **Material** system in Unreal Engine offers a node-based material editor whereby you connect textures, math operations, parameters, and expressions to create the look of a surface. The material system optimizes and renders materials in real-time.

For a Maya user, this workflow would be most similar to how you build out materials in Hypershade but with some key differences.

[![Unreal Editor Material System](https://dev.epicgames.com/community/api/documentation/image/02334e9d-f2d3-4183-a6a4-c2a84a1a9431?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/02334e9d-f2d3-4183-a6a4-c2a84a1a9431?resizing_type=fit)

The materials in Unreal Engine are built using: 

-   A Node-based material editor that is streamlined for real-time previewing and workflows.
    
-   Physically-Based Rendering (PBR) that emphasizes realism through defined property inputs like Base Color, Metallic, Roughness, Specular, and Normal Maps.
    
-   Real-time feedback with changes to materials in the preview viewport with real-time lighting and reflections.
    
-   Parameter-driven workflows with Material Instances to make adjustments to materials through overrides without need to recompile the parent material.
    

## A Material’s Defining Attributes

A material’s defining attributes for how it’s rendered, and reacts to lighting and surfaces in Unreal Engine is determined by its properties, material inputs, and material graph logic. 

### Material Properties and Material Inputs

In the Material Editor, the **Details** panel is where you’ll set up the defining attributes of a material. There are three primary properties you’ll need to consider for the type of material you are making. These properties define the inputs on the main material node you’ll use to set up the look of your material in the material graph.

[![Unreal Editor Material Properties](https://dev.epicgames.com/community/api/documentation/image/cbcb6eb1-1a21-4619-9eb4-cfab201eaf29?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/cbcb6eb1-1a21-4619-9eb4-cfab201eaf29?resizing_type=fit)

-   The **Material Domain** defines what the material can be used for in your project. For example, a 3D surface, user interface, post processing, light functions, or decals.
    
-   The **Blend Mode** defines how the material blends with the surrounding background colored pixels. For example, this can be opaque, translucent, masked, along with other types of blending options.
    
-   The **Shading Model** defines how the material interacts with light, determining their visual appearance and lighting behavior of surfaces. For example, Cloth and Hair shading models use different material inputs to achieve realism for their surfaces compared to the Default Lit shading model. Some shading models add more complexity and performance cost to their materials.
    

With these material properties set, you can build out a material using the available inputs on the main material node in the material graph. The list of inputs is directly attributed to which domain, blend mode, and shading model is set for the material you are developing. For most materials created in Unreal Engine, you’ll use the following:

Below is an example of the different inputs on the Main Material Node when changing just the **Blend Mode** to use different outputs.

|  |  |  |
| --- | --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/75958f4d-4aa3-4d01-905a-8ce839813389?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/75958f4d-4aa3-4d01-905a-8ce839813389?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/109c6139-20dc-4ec2-8d03-07061b7efa7d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/109c6139-20dc-4ec2-8d03-07061b7efa7d?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/d8d1dffb-8077-43e8-81df-d644a6a069fc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d8d1dffb-8077-43e8-81df-d644a6a069fc?resizing_type=fit)



 |
| 

**Material Domain**: Surface

**Blend Mode**: Opaque

**Shading Model**: Default Lit

 | 

**Material Domain**: Surface

**Blend Mode**: Translucent

**Shading Model**: Default Lit

 | 

**Material Domain**: Surface

**Blend Mode**: Masked

**Shading Model**: Default Lit

 |

Below are some common input names used with Maya’s Hypershade materials and their equivalence in Unreal Engine. This also includes their typical type of source input for each of these inputs in Unreal Engine when defining logic in the material graph.

| Maya Hypershade Material Inputs | Unreal Engine Material Inputs | Typical Source Type | Material Input Description |
| --- | --- | --- | --- |
| 
**Color**

 | 

**Base Color** 

 | 

Texture or Color

 | 

The main diffuse color of a surface.

 |
| 

**Reflectivity**

 | 

**Metallic**

 | 

Scalar or Texture

 | 

Defines if the surface is metal (1) or non-metal (0) in appearance.

 |
| 

**Roughness**

 | 

**Roughness**

 | 

Scalar or Texture

 | 

Controls the smoothness of the surface from smooth (0) to rough (1).

 |
| 

**Reflectivity**

 | 

**Specular**

 | 

Scalar or Texture

 | 

Controls the reflective intensity of a non--metallic surface from non-reflective (0) to reflective (1).

 |
| 

**Bump** / **Normal**

 | 

**Normal**

 | 

Normal Map Texture

 | 

Applies surface detail using texture maps.

 |
| 

**Emission** / **Emission Color** / **Incandescence**

 | 

**Emissive Color**

 | 

Color or Texture

 | 

Controls the intensity of self-illumination from a surface.

 |
| 

**Transparency** / **Translucence**

 | 

**Opacity**

 | 

Scalar or Texture

 | 

Controls how translucent the surface is from fully transparent (0) to opaque (1).

 |
| 

**Ambient Color**

 | 

**Ambient Occlusion**

 | 

Texture

 | 

Controls the intensity of indirect shadows.

 |

For more information and examples of using these material properties and their inputs in materials, see the following topics: 

-   [Material Blend Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-blend-modes-in-unreal-engine)
    
-   [Material Shading Models](https://dev.epicgames.com/documentation/en-us/unreal-engine/shading-models-in-unreal-engine)
    
-   [Material Inputs](https://dev.epicgames.com/documentation/en-us/unreal-engine/material-inputs-in-unreal-engine)
    
-   [Material Properties](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-properties)
    

### Material Graph

The **Material Graph** is the node-based editor where you’ll connect textures, expressions, math operations, and values together to define the look of a surface. Materials can be as simple or complex as you need to define a surface.

[![Unreal Editor Material Graph](https://dev.epicgames.com/community/api/documentation/image/4ab7dc62-ed81-463f-902c-2004ba824089?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4ab7dc62-ed81-463f-902c-2004ba824089?resizing_type=fit)

The common node types you’ll use are: 

-   **Texture Sample**
    
    -   This node uses texture assets, such as color maps and normal maps.
        
-   **Constants**
    
    -   These are single-value numbers useful for controlling scalar properties, such as input values on a Linear Interpolate node, or plugging directly into the main material node’s inputs for Metallic, Roughness, or Opacity.
        
-   **Math Nodes**
    
    -   These are mathematical operations for Add, Multiply, Subtract, Divide, Linear Interpolate (Lerp), Power, Clamp, etc.
        
-   **Utility Nodes**
    
    -   These are nodes to help build logic with other nodes in the graph. These include expressions for Fresnel, Camera Vector, World Position, Texture Coordinates, etc.
        

For more information on using logic in the material graph and general functionality here, see the following topics: 

-   [Using the Main Material Node in the Material Graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-main-material-node-in-unreal-engine)
    
-   [Placing Material Expressions and Functions](https://dev.epicgames.com/documentation/en-us/unreal-engine/placing-material-expressions-and-functions-in-unreal-engine)
    
-   [Material Expressions Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-expressions-reference)
    

## Additional Notes for Materials and Textures

Below are some high-level overviews of subjects related to material development in Unreal Engine. For more in-depth overviews of these concepts and applications, see their linked documentation pages. 

### Materials versus Material Instances

Unreal Engine’s material system is built with customization and parameterization in mind for real-time rendering and lighting. One way of optimizing working with materials is to use Material Instancing as a means to customization of parameters without affecting the original material it’s derived from. 

So, if a **Material** is the primary asset that defines how the surface of an object looks and interacts with lighting, a **Material Instance** uses attributes and parameters of the parent or base material to override these values to create variety and customization. This can also be more cost efficient than using individual materials for all objects.

|  |  |
| --- | --- |
| 
[![Unreal Editor Material Editor](https://dev.epicgames.com/community/api/documentation/image/c3ba2dcc-71c9-42a7-be8b-b7ffc325a25e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c3ba2dcc-71c9-42a7-be8b-b7ffc325a25e?resizing_type=fit)



 | 

[![Unreal Editor Material Instance Editor](https://dev.epicgames.com/community/api/documentation/image/a30fc690-73f7-4920-92be-51fc43f0d8f8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a30fc690-73f7-4920-92be-51fc43f0d8f8?resizing_type=fit)



 |
| 

**Material Editor**

 | 

**Material Instance Editor**

 |

You can break down the characteristics of Materials and Materials Instances in the following ways:

| Material Characteristics | Material Instance Characteristics |
| --- | --- |
| 
Created using a node-based editor.

 | 

Uses an editor driven by exposed parameters that can be overridden from the base material.

 |
| 

Contains all possible feature inputs of a material, such as color, metallic, roughness, opacity, etc.

 | 

Provides access only to exposed parameters from the base material that can be overridden.

 |
| 

Changes to the material require it to be recompiled before the changes can be previewed.

 | 

Provides real-time feedback for changing parameters whereby they do not require the material to be recompiled.

 |
| 

The material graph can have any level of complexity to achieve its visual requirements.

 | 

Access to only exposed parameters means this improves performance and workflow efficiency.

 |
| 

Changing this material affects all objects that use it.

 | 

Changing this material instance affects only the objects that use it, making them ideal for creating multiple similar-looking surfaces that start from the same base parent with similar features.

 |

The best time to think about using a material instance in conjunction with a material is when you only need to customize details and adjust parameters, such as the color of the materials, its textures, scaling, and so on. You should create new base materials when you need to define new visual behavior and style (like opaque versus translucent) requires new logic to be set up in the material graph. 

Materials generally require a higher initial setup time and are less performance-friendly than using a material instance for materials with similar properties and attributes. 

For more information on using Materials with Material Instances in your project, see the following topics: 

-   [Instanced Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/instanced-materials-in-unreal-engine)
    
-   [Material Instance Editor Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-instance-editor-ui)
    
-   [Creating and Using Material Instances](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine)
    

### Textures

Like in Maya, textures are image maps you apply to input attributes of the material you’re creating, such as base color, normal, roughness, to define the surface details. In Unreal Engine, there is more importance placed on physically based rendering concepts and real-time feedback when developing your materials. 

When you import textures, you can open them in the **Texture Asset Editor** where you can see information about them, configure their settings, and make some adjustments.

[![Unreal Editor Texture Asset Editor](https://dev.epicgames.com/community/api/documentation/image/9e3ff60f-4c10-402d-a0ef-470cff129949?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9e3ff60f-4c10-402d-a0ef-470cff129949?resizing_type=fit)

Unreal Engine's Texture Asset Editor

You can do the following to optimize and work more efficiently with textures in Unreal Engine: 

-   Create and adjust textures using third-party tools before importing them.
    
-   Use channel packing techniques to combine multiple grayscale textures for material inputs like roughness, metallic, and ambient occlusion, into single RGB textures. This can optimize performance by referencing a single texture instead of several different textures.
    
-   The engine automatically uses texture compression for textures, but understanding how to leverage this can improve visual fidelity and performance.
    
-   Be mindful of texture sizes. For real-time performance, it’s ideal to rely on power-of-two (128, 512, 1024, etc.) dimensions for textures. Non-power-of-two textures don’t use the Texture Streaming system of the engine, which can lead to visual artifacts at distances.
    

For more information on using textures in Unreal Engine, see the following topics: 

-   [Using Textures in Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/textures-in-unreal-engine)
    
-   [Texture Asset Editor Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-asset-editor-in-unreal-engine)
    

### Substrate Material Framework

Unreal Engine’s **Substrate Material Framework** is an approach to authoring materials that replaces the fixed suite of shading models and blend modes with a more expressive and modular framework. Material authoring is the same as with the standard material system, however, you are no longer bound to having individual materials that use a single shading model and blend mode. You can seamlessly blend them in this workflow to create unique materials with richer complexity.

[![Unreal Engine Substrate Material](https://dev.epicgames.com/community/api/documentation/image/6b730c6b-133d-409e-8000-51a85c913920?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6b730c6b-133d-409e-8000-51a85c913920?resizing_type=fit)

For more information on using Substrate in your projects and material creation workflows, see [Substrate Material Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-substrate-materials-in-unreal-engine).

### Physically Based Rendering with Materials

Unreal Engine uses **Physically Based Rendering** (PBR) for shading and rendering that accurately simulates the behavior of light interacting with surfaces. This provides physically plausible light interactions to create realistic and — more importantly — predictable visuals under different lighting conditions, such as direct sunlight versus interior lighting, or even photo-realistic surfaces versus stylized effects from hand-painted to cel-shaded looks. 

The key principles to think about when working with PBR materials in Unreal Engine are: 

-   **Realistic Lighting Interactions** where surfaces respond accurately and predictably to different lighting setups, whether it’s natural (exterior) or artificial lighting (interior).
    
-   **Consistency** with materials to look correct across different scenes and lighting scenarios.
    
-   A **Simplified Workflow** whereby artists define materials by their physical properties instead of arbitrary values, which can reduce the guesswork of shading and lighting adjustments in a real-time environment with instant feedback in the scene.
    

For more information, see [Physically Based Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/physically-based-materials-in-unreal-engine).

## Next Page

[

![Lighting and Rendering in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/d847f373-1ce3-4c85-bdf7-dd02402ddf5c?resizing_type=fit&width=640&height=640)

Lighting and Rendering in Unreal Engine for Maya Users

An overview of Unreal Engine's lighting and rendering features for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/lighting-and-rendering-in-unreal-engine-for-maya-users)