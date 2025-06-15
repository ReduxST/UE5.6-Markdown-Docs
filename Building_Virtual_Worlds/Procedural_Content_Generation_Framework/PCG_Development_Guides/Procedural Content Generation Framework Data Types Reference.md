# Procedural Content Generation Framework Data Types Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-framework-data-types-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation-framework-data-types-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:44:21

---

Data in the **Procedural Content Generation (PCG) Framework** is divided into the following types:

-   [Spatial Data](/documentation/en-us/unreal-engine/procedural-content-generation-framework-data-types-reference-in-unreal-engine#spatialdata)
-   [Composite Data](/documentation/en-us/unreal-engine/procedural-content-generation-framework-data-types-reference-in-unreal-engine#compositedata)
-   [Attribute Sets](/documentation/en-us/unreal-engine/procedural-content-generation-framework-data-types-reference-in-unreal-engine#attributesets)

## Spatial Data

Spatial data contains references to two-dimensional (2D) or three-dimensional (3D) space and can represent volumes, heightfields, splines, and point data.

### Volumes

Volumes are a type of spatial data that represents 3D shapes that is often used for boolean set operations or sampling directly from the level using the Volume Sampler node.

### Surfaces

Surfaces are a type of spatial data that represents data that is 2D, such as Landscapes, which are mapped to the XY plane, or the Surface Sampler node that generates points on a 2D plane and projects them onto a 3D shape.

### Lines

Lines are a type of spatial data that represents Spline and Landscape Spline components. This data reads the spline's key points with tangents and point scales. The Landscape Spline is projected vertically and always applies at the surface even if the spline is offset from the Landscape. This data type is referenced in the PCG graph using the Get Spline Data and Spline Sampler nodes.

### Points

Point Clouds are a type of spatial data that represents a collection of points representing surfaces or volumes in 3D space with associated bounds. The bounds allow the points to represent shapes in different dimensions.

For example, a 3D sphere can be sampled to points, with the point size determining how closely the sphere shape is respected by the points.

Additionally, each point is given a Density value that is constrained to a value between zero and one. Together, these points along with their density values represent a floating-point function in space. PCG graph nodes often create and manipulate sampling density values in space before subsequently taking the samples.

Points can contain the following information:

| **Data** | **Description** |
| --- | --- |
| **Transform** | Translation, Rotation, and Scale information. |
| **BoundsMin and BoundsMax** | Minimum and maximum extents of the volume represented by the point. |
| **Color** | Four channel color value per point. |
| **Density** | Floating point representation of a point's falloff in relation to other points in a given sampling. Used to determine sampling density. |
| **Steepness** | Softness of the volume represented by a point. Each point has 3D bounds and represents a region of space. The Steepness value on each point gives control over the shape of its influence. |
| **Seed** | Consumed by random number generators during various operations. This can be manipulated to control how randomness is expressed and is computed from the position in order to be world-position consistent. |

## Composite Data

Composite data is the result of set operations, such as union, intersection, and set difference.

You can chain set operations together as multiple operations before converting the result back to explicit data and applying the result.

## Attribute Sets

Attribute sets are user-defined variables and stored in the PCG graph as Metadata. These variables can be manipulated using various attribute operation nodes and consumed by nodes.

A common example of this is to drive node settings found by expanding out the advanced pins on the node and connecting an attribute to the exposed pins.

The available Attribute inputs on the Transform Points node.

Attributes can be inspected in the Attributes List window, part of the PCG Node Graph interface. For more information on using the PCG Framework, see [Procedural Content Generation Overview](/documentation/en-us/unreal-engine/procedural-content-generation-overview).