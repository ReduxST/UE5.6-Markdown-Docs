# Using Grooms with Mutable

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-grooms-with-mutable-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-grooms-with-mutable-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:20

---

## Requirements

To use [Grooms](/documentation/en-us/unreal-engine/hair-rendering-and-simulation-in-unreal-engine) with Mutable you need to toggle on the **Grooms Extensions For Mutable** plugin in your **Project Settings**.

Once enabled, you will see a new pin appear on existing **Object** nodes.

## Usage

Grooms can be added to any Skeletal Mesh Component tagged by Mutable (see [Node Mesh Component](https://github.com/anticto/Mutable-Documentation/wiki/Node-Mesh-Component)). Groom Components are dynamically created as children of the tagged Skeletal Mesh Component.

To use Grooms, follow the steps below:

1.  Create a new Groom Constant node and specify which component you want it to bound to using the Component Name.
    
2.  In the **Node Properties** panel, specify the **Groom** and **Binding** assets. The Binding asset must have the same Skeletal Mesh as the one in the bound Skeletal Mesh Component as the **Target Skeletal Mesh**. Other properties are automatically copied to the dynamically created Groom Component.
    
3.  Connect the new node to an **Object** node. Notice that the Groom Constant nodes can be conditionally activated using Group nodes.
    

## Current Limitations

-   Modifier nodes can not be applied to Mesh Components bound by grooms.
-   A Mutable generated Skeletal Mesh must have the same number of LODs as the Source Skeletal Mesh in the Binding Asset.