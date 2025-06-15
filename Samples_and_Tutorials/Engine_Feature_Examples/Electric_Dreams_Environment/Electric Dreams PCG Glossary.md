# Electric Dreams PCG Glossary

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary)  
**Processed:** 2025-06-14 16:21:55

---

The Electric Dreams Environment sample project uses several specialized terms to refer to different structures that are used in the Procedural Content Generation framework. This page contains many of these terms along with definitions and additional information to familiarize you with the language used in the documentation for this project.

Assembly

An **Assembly** is a group of actors and visuals combined to create a single asset. Assemblies in the context of Electric Dreams use Quixel assets combined in Level Instances or Packed Level Actors which are created and placed manually around the level. Assemblies are used as source content in [PCG Graphs](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary?application_version=5.5#pcggraph) and PCG Assemblies with the help of the Level to PCG asset utility.

Attribute

An **Attribute** is user-defined, additional metadata of a specific type that can override node parameters, or be associated with points, and used for attribute operations within the [PCG Graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary?application_version=5.5#pcggraph). An attribute can be created in the graph using the **Create Attribute** node or within custom [PCG Elements](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary?application_version=5.5#pcgelement).

The supported types for attributes are currently limited to:

-   transform
    
-   vec2
    
-   vec3
    
-   vec4
    
-   float
    
-   double
    
-   int32
    
-   int64
    
-   bool
    
-   string
    
-   name
    
-   rotator
    
-   quaternion
    

PCG Assembly

A **PCG Assembly** is an assembly that is procedurally generated with the PCG framework. A PCG Assembly can be constructed in multiple ways through a set of operations in a [PCG Graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary?application_version=5.5#pcggraph) and customized by changing their inputs, such as a component or exposed parameters. These operations range from spawning individual meshes and actors to full, handcrafted assemblies.

PCG Element

A **PCG Element** is a node used within a [PCG Graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary?application_version=5.5#pcggraph). Elements can be created through C++ code or in data using the PCG Blueprint Element class.

PCG Graph

The **PCG Graph** is the central piece of PCG. A graph describes work through a series of operations performed in the form of a data-flow graph. A PCG Graph can be used inside another graph as a subgraph.

PCG Settings

**PCG Settings** are the node settings, including its class and set properties.

Point Data

**Point Data** represents points in 3D space with associated bounds, defined properties, and attributes. This is the most common PCG data type for operations.

Point Properties

Point **Properties** are sets of predefined properties found on all points in PCG [Point Data](https://dev.epicgames.com/documentation/en-us/unreal-engine/electric-dreams-procedural-content-generation-glossary?application_version=5.5#pointdata). Properties can be used in attribute operations. Properties must be prefixed with the dollar sign ($), for example, `$Density`, `$Position.x`, `$Rotation.forward`.

These properties are:

-   **Transforms**: A transform consisting of a Location (vec3), Rotation (Rotator) and Scale (vec3).
    
-   **Density (float)**: A point density function maximum value ranging from 0 to 1. This value is used in multiple operations such as differences, unions, noise, and filtering.
    
-   **BoundsMin/Max (vec3)**: Point bounding volume as min and max.
    
-   **Color (vec4)**: Point color value.
    
-   **Steepness (float)**: A value ranging from 0 to 1 representing the slope of the point's density function. At steepness 1, the density function returns the maximum density within the point's bounds and returns 0 outside. At steepness less than 1, the density function returns maximum density value linearly interpolated down to 0, centered on the point's bounds min/max.
    
-   **Seed (int64)**: Point seed computed from point position, node seed, and component seed.
    

Spatial Data

**Spatial Data** exists in space and can represent:

-   Three-dimensional (3D) volumes.
    
-   Two-dimensional (2D) surfaces, such as heightfields and textures.
    
-   One-dimensional (1D) lines, such as splines and point clouds.