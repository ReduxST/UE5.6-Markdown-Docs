# Space Conversion Nodes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-component-space-conversion-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-component-space-conversion-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:19

---

Animation Blueprint nodes on the **AnimGraph** calculate and generate new poses that drive animations in either the **Local Space** or a **Component Space**. Animation poses generated in **Local space** calculate bone transforms relative to the bones **parent bone**. Animation poses generated in **Component Space** calculate bone transforms relative to the [Skeletal Mesh Component](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) of your character.

![space conversion nodes overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5272723f-6dff-4128-a342-cc744055c264/overview.png)

The **Convert Spaces** nodes available in the **AnimGraph** of Animation Blueprints provides the ability to convert poses between **local** and **component** space.

When working with poses in an Animation Blueprint, most nodes will operate within Local Space, indicated with **white** pose input and output pins. However, certain [blend nodes](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine) and all [skeletal controls nodes](/documentation/en-us/unreal-engine/animation-blueprint-skeletal-controls-in-unreal-engine), operate in **Component Space**, indicated with **blue** pose input and output.

To use nodes that operate within Component Space, poses must first be converted to Component Space using the Local to Component conversion node.

![local to component space conversion node animbp animgraph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9cdb488c-5e68-4338-94af-14803e6662d9/localtocomponent.png)

After an animation pose has undergone component space operations, it must be converted back to local space in order to be usable by additional nodes, or provide a final pose for the output node.

![component to local space conversion node animbp animgraph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/319913e7-8bcb-4e4b-b4c5-7495910d9c16/componenttolocal.png)

Because there is a cost associated with each conversion **to** or **from** Component Space, it is best to group any nodes that operate in Component Space, to reduce the number of conversions needed.