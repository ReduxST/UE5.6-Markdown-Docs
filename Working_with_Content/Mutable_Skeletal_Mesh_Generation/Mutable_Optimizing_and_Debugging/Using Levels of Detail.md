# Using Levels of Detail

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-levels-of-detail-in-mutable-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-levels-of-detail-in-mutable-in-unreal-engine)  
**Processed:** 2025-06-14 16:59:30

---

There are many reasons to use Levels of Detail (LODs) in Mutable:

-   Memory usage
-   Processor performance
-   Loading time

In Mutable you can take advantage of the procedural construction of characters to optimize even further by creating specific diagrams for each LOD. In this way, you can have objects such as the base character body follow the usual LOD optimization by simply lowering the polycount and texture sizes on each LOD. You can also go beyond this and define different construction processes for each LOD using cheaper operations as the object is further away.

As an example, imagine a character bracelet. In the top LOD used during close-ups, the bracelet has its own mesh and complex materials with physics animation. For the second LOD, the bracelet may be simplified by replacing it with a rigid mesh with a single material directly skinned to the arm bone. The third LOD may be just a texture patch on the arm (if the bracelet is big enough). In the fourth LOD it may disappear completely. You can define all these cases in different diagrams using the same parameters, so if the bracelet color was customizable, you could see it change on every LOD.

## Defining the Levels of Detail of a Component

You can define the LODs using several different nodes in the graph. The most important node is the [Mesh Component](https://github.com/anticto/Mutable-Documentation/wiki/Node-Mesh-Component) node. The number of LODs defined in this node limits the maximum LODs that can be defined in the component.

For example, the [Add To Mesh Component](https://github.com/anticto/Mutable-Documentation/wiki/Node-Add-To-Mesh-Component) node only generate as many LODs as its parent [Mesh Component](https://github.com/anticto/Mutable-Documentation/wiki/Node-Mesh-Component) node. If an LOD pin has no connections, the LOD will not have geometry unless automatic LODs are used.

LOD properties that control how LODs are selected are standard Unreal Engine properties. They are copied from the Reference SkeletalMesh object and you can set them up there. Please note that this means that the Reference SkeletalMesh object must have LODs.

You can also find more LOD settings in the **Object Properties** tab.

## Automatic Levels of Detail

Since customizable objects may become very large, you can use the Auto LOD Strategy field in the Mesh Component node to simplify the generation of LODs without having to multiply all the nodes. See the [Mesh Component](https://github.com/anticto/Mutable-Documentation/wiki/Node-Mesh-Component) node reference for more information.