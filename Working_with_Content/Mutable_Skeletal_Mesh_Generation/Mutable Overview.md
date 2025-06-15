# Mutable Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:47

---

## What is Mutable

**Mutable** is a toolset for Unreal Engine that generates dynamic skeletal meshes, materials and textures in editor or at runtime. It is designed to help artists and designers create character customization systems but can generate a variety of dynamic content, such as animals, props, and other skeletal mesh assets.

Mutable is designed to run efficiently for in-game use, however it is also useful as a content pipeline tool for projects that require the flexibility to create many skeletal mesh variations inside the Unreal Editor.

Mutable is designed to:

-   Support deep customization involving many parameters and texture layers.
    
-   Support complex mesh interactions.
    
-   Support texture effects that are not gpu-performant, such as wrapping projections and many planar projections.
    
-   Optimize memory usage
    
-   Reduce shader costs.
    
-   Reduce draw call count.
    

Using Mutable translates some of the CPU and memory cost at character generation time. Characters are generated in the background using some CPU resources and working memory and will use only the resources of a pre-generated Skeletal mesh once generated.

## Mutable Features

Mutable contains the following features:

### General

-   Flexible parameter systems connect customizable objects with multiple effects.
    
-   Splits customizable characters into multiple assets to facilitate concurrent artist work.
    

### Mesh

-   Removes hidden parts to maximize performance and avoid z-fighting.
    
-   Bakes morphs at character generation time.
    
-   Merges meshes to reduce draw calls.
    
-   Deforms meshes based on interactions between character parts.
    

### Textures

-   Bakes texture images at runtime combining multiple effects.
    
-   Supports multiple types of projectors: planar, cylindrical and wrapping.
    
-   Supports multiple texture blending modes: multiply, soft light, hard light, burn, dodge, etc.
    
-   Manages UV layouts to dynamically remove unnecessary texture parts.
    

### Animation And Physics

-   Combines animation graphs of multiple parts.
    
-   Merges and deforms collision physics assets together with the meshes.
    
-   Manages cloth simulation data at character generation.
    

### Performance

-   Flexible instancing of customized characters.
    
-   Supports LOD management at runtime.
    
-   Supports multiple states for adjusting character generation to different use cases.
    
-   Supports texture streaming with on-demand generation.
    

## Customizable Objects and Actors

The diagram below shows how meshes, textures, and materials are used for character customization. The system's main concepts are **CustomizableObject** assets, **CustomizableObjectInstance** assets, and Actors with special components using these assets.

[![Anatomy of a Customizable Object](https://dev.epicgames.com/community/api/documentation/image/a7bf8310-6f09-4f32-8181-fe89f1e74a78?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a7bf8310-6f09-4f32-8181-fe89f1e74a78?resizing_type=fit)

Anatomy of a Customizable Object

*Mutable uses CustomizableObject assets, CustomizableObjectInstance assets, and Actors with special components to create the final assets.*

### Customizable Objects

Customizable Objects are a new type of asset added to Unreal Engine and represent an object that can be customized using Mutable. It includes all the possible variations that can be applied to it. It defines the parameters that are controlled at runtime by the player or game code and how they affect the final objects.

You can create **Customizable Objects** from the **Content Drawer** or **Content Browser** using the **Add New** menu:

[![](https://dev.epicgames.com/community/api/documentation/image/5e3d7eba-b2a0-4306-9e3b-771d85c63073?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5e3d7eba-b2a0-4306-9e3b-771d85c63073?resizing_type=fit)

*Creating a Customizable Object.*

### Parameters

A Customizable Object contains several parameters that can be modified at runtime. There are several types of parameters:

-   **Slider parameters**: numeric parameters with decimals, ranging between 0.0 and 1.0. These are usually created explicitly by a [Node-Float-Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Float-Parameter) , and used for continuous effects like texture effects, or mesh morphs.
    
-   **Enumeration parameters**: represents an option in a predefined set of options. These may be created by a [Node-Object-Group](https://github.com/anticto/Mutable-Documentation/wiki/Node-Object-Group), to select a child object, or by the [Node-Enum-Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Enum-Parameter), to choose one option or multiple [Node-Switch](https://github.com/anticto/Mutable-Documentation/wiki/Node-Switch).
    
-   **Checkbox parameters**: represents two possibilities, either enabled or disabled. These are created by a [Node-Object-Group](https://github.com/anticto/Mutable-Documentation/wiki/Node-Object-Group) when the group type is "Toggle Each".
    
-   **Color parameters**: represents a color with alpha channel using a vector of four numeric float values, ranging between 0.0 and 1.0. These are created by the [Node-Color-Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Color-Parameter).
    
-   **Projector parameters**: represents a projector with a position that can be modified at runtime. These are created with the [Node-Projector-Parameter](https://github.com/anticto/Mutable-Documentation/wiki/Node-Projector-Parameter).
    

### Customizable Object Instance

The **Customizable Object Instance** is a new type of asset used with Mutable. It represents an instance of a CustomizableObject, a set of parameter values to apply to a CustomizableObject in order to create a customized asset. For example, if you have a CustomizableObject for Bandits, each unique bandit you create from it is a CustomizableObjectInstance.

To create an instance asset from a Customizable Object, right-click your Customizable Object and select **Create New Instance**:

[![](https://dev.epicgames.com/community/api/documentation/image/f495e5f7-33ab-4045-be1f-d906fcd58108?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f495e5f7-33ab-4045-be1f-d906fcd58108?resizing_type=fit)

*Creating a new Customizable Object Instance.*

## Mutable Editors

### Customizable Object Editor

Double-clicking a Customizable Object opens up the **Customizable Object Editor**:

[![](https://dev.epicgames.com/community/api/documentation/image/96347096-c3fb-42f2-9b3e-acb12c603607?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/96347096-c3fb-42f2-9b3e-acb12c603607?resizing_type=fit)

*The Customizable Object Editor.*

The interface contains the following panels:

-   **Source Graph**: Contains the blueprint nodes that define the CustomizableObject’s structure, including its LOD settings, mesh sections, meshes, textures, parameters and the effects that connect them.
    
-   **Object Properties**: Contains the general properties of the object.
    
-   **Node Properties**: Contains the properties of the selected node.
    
-   **Preview Instance Viewport**: Shows the 3D preview when an object is open and compiled.
    
-   **Preview Instance Parameters**: Shows the current parameters for the preview object. They can be directly modified here. It can also "Bake" the current instance into a set of standard Unreal Engine assets. See [Baking Instances](https://dev.epicgames.com/documentation/en-us/unreal-engine/baking-instances-using-mutable-in-unreal-engine) for more details.
    

The editor toolbar contains the following elements:

-   **Save**: Saves the current object.
    
-   **Compile**: Compile the current object with all of its children and update the preview. This is necessary to reflect changes in the graph. For more information about compiling and its options, see [Performance Tuning](https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-optimizing-and-debugging-in-unreal-engine).
    
-   **Compile Only Selected**: Compiles the current object and the previewed children only. This is useful for faster iteration when the customizable object is very large.
    
-   **Texture Memory Analyzer**: Opens a tool panel that shows the resulting textures of the preview object and its details, such as final size, format, and memory usage.
    
-   **Performance Analyzer**: Opens a tool panel that benchmarks the current object by generating many random instances and showing many relevant metrics like triangle count or generation time.
    

### Customizable Object Instance Editor

The Customizable Object Instance Editor is used to view and modify CustomizableObjectInstances. It has only two panels and are similar to the Preview and Node Properties panels in the Customizable Object Editor.

[![](https://dev.epicgames.com/community/api/documentation/image/c3edf89a-a5a8-4252-9ad8-c9b27e0cd851?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c3edf89a-a5a8-4252-9ad8-c9b27e0cd851?resizing_type=fit)

## Object Hierarchy

### Objects

Mutable organizes each Customizable Object into a hierarchy. Each object has a root node that connects to all other nodes. These nodes represent components, meshes, materials, textures, and parameters. Any object can have any number of child objects. A child can:

-   Add new meshes and mesh sections to the final object
    
-   Extend a mesh already present in another object
    
-   Remove part of the mesh in another object
    
-   Patch the textures of a material in another object
    
-   Activate user-defined Tags that can be used in sibling objects to apply different effects.
    

At the same time, child objects can have their own child objects in an unlimited hierarchy.

### Groups

Child objects can be organized in **Groups**. Groups define the logic between the object and its parent in regard to how the child objects are activated. For instance, all t-shirt children can be grouped with an object parameter that only lets the users select one of them at a time or none.

Here are two child objects connected through a Group:

[![](https://dev.epicgames.com/community/api/documentation/image/6210db20-73c3-4039-b40b-3132dd45cb7e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6210db20-73c3-4039-b40b-3132dd45cb7e?resizing_type=fit)

Each Group has a Group Type which can be one of the followings:

-   **Toggle**: the child objects appear as toggleable options.
    
-   **At least one Option**: a single child object must be selected.
    
-   **None or One**: a single child object can be selected.
    
-   **All options**: all the object’s children are active all the time. Behaves as if the children connect directly to the parent.
    

### Actor Components

A single CustomizableObject can generate multiple **Actor Components**. Parameters can affect multiple components at the same time but also can conditionally toggle them. To create multiple components see the [components nodes reference](https://github.com/anticto/Mutable-Documentation/wiki/Node-Reference#objects-components-and-mesh-sections).

### Reference Skeletal Mesh

Mesh Component nodes have a property called **Reference Skeletal Mesh**. This is a standard Unreal Engine SkeletalMesh and is used for the following reasons:

All the skeletal meshes generated for this component in CustomizableObject instances use the Reference Skeletal Mesh properties for everything that Mutable doesn't create or modify. This includes data such as LOD distances, Physics properties, Bounding Volumes, Skeleton, etc. When a CustomizableObject instance is being created for the first time the Reference Skeletal Mesh is used for each Actor Component. This can be disabled using the function "SetReplaceDiscardedWithReferenceMeshEnabled" from the class CustomizableObjectSystem. For more information see [Using Mutable from C++](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mutable-from-cplusplus-in-unreal-engine) and [Using Mutable from Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-mutable-from-blueprint-in-unreal-engine).

For this reason, projects usually use a simple or generic skeletal mesh as the Reference Skeletal Mesh. One option is to replace the Reference Skeletal Mesh with a Baked Skeletal Mesh generated in the editor, with the desired //generic// appearance. See [Baking Instances](https://dev.epicgames.com/documentation/en-us/unreal-engine/baking-instances-using-mutable-in-unreal-engine) for more information.

## Multiple Assets

A large CustomizableObject can be split into several assets. This is important when multiple users are working on the same data and for version control. There are 2 features to assist with this:

-   Child Objects can be selected as the parent of an Object Group in a different asset, instead of directly connecting them in a graph. See the [Object Group](https://github.com/anticto/Mutable-Documentation/wiki/Node-Object-Group) and [Child Object](https://github.com/anticto/Mutable-Documentation/wiki/Node-Child-Object) node reference for more information.
    
-   There are special diagram nodes to [export](https://github.com/anticto/Mutable-Documentation/wiki/Node-Export-Pin) and [import](https://github.com/anticto/Mutable-Documentation/wiki/Node-Import-Pin) connections from the graph in other assets.
    

This is useful for editor data, but it has nothing to do with data streaming in packaged games. Data streaming for packaged games happens regardless of whether the CustomizableObject is split into multiple assets or not.

## Object Interactions

Mutable has several features for handling object interactions. One is **Object Groups**, which create instance parameters that select only one child object from a set, so it is not possible to add more than one of them. An example of this is a group for character hats, that will let you select one hat or none, but never two hats.

Additionally, Mutable has a system for creating different variations of an object based on what other objects are added to an instance. For example, you have a character with several hair styles and hats. You may want to create variations for some of the hairstyles to be used when a type of hat is also present in the character. You can use the Mesh Section Variations and other Variation nodes for this.

Another example of object interaction is the selective removal of mesh fragments from one object using modifiers that exist in another object.

These two types of object interactions use the Tag system. You can define your own Tags and enable them when an object is active in an instance. The Mesh Section Node is where you can add tags. Then there are several nodes that act differently based on what tags are in a particular instance, like the Mesh Section Variation or the Clip Mesh With Mesh Modifier node.

## Texture Layouts

Mutable can merge meshes and mesh sections from several objects into a single mesh. It can also remove mesh fragments from existing meshes. When doing this, Mutable will modify the texture UV layouts to optimize memory usage, and minimize rendering commands. Mutable will do this automatically by default, but manual control of is available through several properties in the [Skeletal Mesh Node](https://github.com/anticto/Mutable-Documentation/wiki/Node-Skeletal-Mesh) and the [Table Node](https://github.com/anticto/Mutable-Documentation/wiki/Node-Table).

See [Texture Layouts](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-layouts) for more information.

## States

A State represents a specific use case in the game (like in-game, cloth customization, facial customization, etc.) and can be configured with a set of parameters that Mutable is going to have ready for modification. States are used to optimize instance updates. For example, one state can be optimized for face changes, another state for body changes, another state for tattoos, and another for only the things that can change during gameplay. Using states means that the character update time can be much faster when only changing the parameters that are optimized in the state that is selected for the character.

See the [States](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-customizable-states-in-mutable-with-unreal-engine) page for more information.

## Streaming

Mutable data streaming is important to reduce memory usage. A customizable character may have hundreds of options and customization parts. Without data streaming they would have to be loaded from disk to memory all at the same time and they would use many GBs of RAM and it would take a long time. Mutable streams only the parts that are being used, greatly reducing memory consumption and load times. In addition, a part is unloaded when it is no longer used.