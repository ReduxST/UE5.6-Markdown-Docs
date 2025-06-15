# Control Rig in Animation Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-in-animation-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-in-animation-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:40

---

**Control Rigs** can be referenced within [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) in order to build animation blueprint logic that interacts with controls and variables. Typically you may want to use Control Rigs in this way to achieve procedural gameplay control of certain Control Rig features, such as ground alignment or other arbitrary contact points.

#### Prerequisites

-   You have created a **Control Rig Asset** for a **Skeletal Mesh**. See the **[Control Rig Quick Start](/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine)** page for information on how to do this.
    
-   You have created an **Animation Blueprint Asset** for the same Skeletal Mesh. See the **[Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine)** page for information on how to do this.
    

## Control Rig Blueprint Node

Control Rig content is accessed within Animation Blueprints by using the **Control Rig node**. You can add this node by right-clicking in the **Anim Graph** and selecting **Misc > Control Rig**. Ensure the source output is connected to the result pose by connecting the pins.

![control rig animation blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e6ec6519-f343-4370-8fcf-39cdd095ff71/node.png)

Next, you need to assign the appropriate **Control Rig Class**. To do this, select the node, navigate to the **Details** panel, and select the Control Rig from the **Control Rig Class** property dropdown menu.

![control rig animation blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e59a5788-632d-433b-a36f-786762204680/class.png)

### Properties

The Control Rig Animation Blueprint node has the following specific properties:

| Name | Description |
| --- | --- |
| **Set Initial Transform From Mesh** | Overrides the initial transforms from the Control Rig with the initial transform from the Skeletal Mesh. |
| **Reset Input Pose to Initial** | Enabling this causes the pose to reset to the initial pose prior to evaluation. |
| **Transfer Input Pose** | Enables bone transform information to be read by the Control Rig node when data is connected to its **Source** pin. |
| **Transfer Input Curves** | Enables [Animation Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) information to be read by the Control Rig node when data is connected to its **Source** pin. |
| **Transfer Pose in Global Space** | 
Enables the incoming pose to be evaluated in **Global** space, as opposed to **Local** space if this is disabled.

Transferring a pose in global space guarantees a global pose match, while local space ensures a match of the local transforms. In general, transforms only differ if the skeleton hierarchy differs between the Control Rig skeleton and the Animation Blueprint skeleton. Disabling this can also improve performance.



 |
| **Input Bones to Transfer** | A list of bones to transfer when data is connected to its **Source** pin. When bones are added to this list, only those bones are transferred. If no bones are listed, then all bones are transferred. |
| **Input** | 

If the Control Rig contains **Variables**, they can be exposed as pins on the node by enabling **Use Pin**, or controlled by [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) by selecting a curve from the Use Curve dropdown menu if the variable is a **Float**.

Transform input data for all Controls can also be exposed here by enabling **Use Pin** on the control entry.



 |
| **Control Rig Class** | The Control Rig class to use for this node. |

## Accessing Variables and Controls

The primary interaction with the Control Rig node is by manipulating **Controls** or **Variables** exposed on the node. You can then connect them to logic that drives their values or transforms.

Variables can be exposed by ensuring they are instance-editable by clicking the **Eye** next to it in the Control Rig **My Blueprint** panel. Next, in the **Animation Blueprint**, select the **Control Rig node** and enable **Use Pin** on the **Variable** entry. You should now see the Variable exposed as a pin on the node.

![control rig animation blueprint variable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/729fee3f-ca7e-472a-9c05-1e2d2bf530db/exposevar.png)

For **Float** type variables, you can instead specify for those to be driven with [Animation Curves](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) by clicking the dropdown menu next to **Use Curve** and selecting an **AnimCurve**.

![control rig animation blueprint animation curve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4364ed4-23f9-4c6e-84d5-81dedc9f6812/usecurve.png)

By default, all controls from the Control Rig Class are listed in the Control Rig node's **Input** property and can be exposed by enabling **Use Pin**. This exposes transform data for that control.

![control rig animation blueprint controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3f4a05b-4b88-4013-aea2-12f23716b096/exposectrl.png)