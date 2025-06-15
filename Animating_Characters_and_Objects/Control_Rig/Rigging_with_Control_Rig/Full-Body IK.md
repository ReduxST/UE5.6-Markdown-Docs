# Full-Body IK

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-full-body-ik-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-full-body-ik-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:38

---

Use Control Rig's Full Body Inverse Kinematic (FBIK) feature to construct rigs in Control Rig with a high degree of control and flexibility. The overall solver method is built on a **Position Based IK** framework, which enables faster rig performance, per-bone settings, preferred angles, squash and stretch, and more. FBIK is designed to act as a procedural adjustment tool within Control Rig, such as for ground alignment, or arm reaching behavior.

This document provides an overview of how to create the FBIK node, and its various features.

#### Prerequisites

-   FBIK is a node within the [**Control Rig Graph**](/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine#riggraph), therefore you should have an understanding of the Control Rig Editor.
-   You must enable the **FullBodyIK** plugin. To do this, navigate in the Unreal Editor menu bar to **Edit > Plugins** and locate **FullBodyIK**. Ensure the plugin is enabled and restart the editor.
    
    ![full body ik plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f22d319-df61-431f-b1e7-f3d3c6ea7402/plugin.png)
    
-   You must have created a Control Rig asset for a character and know how to create controls. See the **[Control Rig Quick Start](/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine)** page for information on how to do this.

## Creation and Setup

FBIK is achieved within Control Rig by creating the FBIK node, then assigning bones and effectors to the appropriate pins.

To start, right-click in the Control Rig graph, and in the context menu select **Hierarchy > Full Body IK**. This will create the Full Body IK node. Connect the node to the **[Forwards Solve](/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine#forwardssolve)** node.

![create full body ik control rig node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/387734ef-8d2a-46b5-a261-b56195616e30/createnode.png)

### Rig Graph Setup

Next, set the **Root** bone property on the Full Body IK node. In typical full-body setups, this will likely be the hips or pelvis bone.

![full body ik root bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ad4b04a-900a-44fe-9bb4-dafdb6f728cf/rootbone.png)

Create and add your chosen controls for the FBIK system. Typically these controls correspond to the limbs you want to affect, and are based on the primary ending bone of the chain. In this example, controls are created for the head, hands, and feet.

![full body ik controls](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abfbbc7b-a20a-4c31-aedd-a52b37a6ea3b/addcontrols.png)

### Effector Setup

You will need to add an effector pin for each control added to the graph. To do this, click the **Add (+)** button next to the **Effectors** property. Effectors will need to be created for each control.

![full body ik effectors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/521ea796-e08d-4aa9-a29c-25ded275ed10/addeffectors.png)

Expanding one of the Effectors entries will reveal its properties. Within each Effector you will set the corresponding **Bone** value for the control, then connect the Transform pins from the corresponding **Get Transform** node.

![full body ik effectors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0a9dae6-bb04-44f8-895e-2715afb1f098/connecteffectors.png)

Connect each effector to their corresponding Get Transform nodes in the same way until all effectors and controls are connected.

![full body ik effectors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/013953e4-7029-43d5-851c-18ee166ca5d6/connecteffectors2.png)

### Setup Result

You should now have a basic FBIK setup for your character. You can manipulate the controls within the Control Rig viewport to see the results.

![full body ik setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9ae2ff6-1f25-4aed-8a21-9c4c3539914e/fbikpass1.gif)

## Bone Settings

Depending on your setup, the base FBIK behavior may not behave as intended. This might be because certain bone settings are not enabled. **Bone Settings** are properties within the Full Body IK node, and are used to control the behavior of each bone that FBIK is affecting.

Bone Settings are added to the Full Body IK node by clicking the **Add (+)** button next to **Bone Settings**, then specifying the bone you wish to affect in the **Bone** property. Each bone setting only affects a single bone, so you may want to add multiple bone settings depending the specific problem you are experiencing with your rig.

![full body ik bone settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05d5542c-cc86-4890-8810-0a4227df04ce/bonesettingsadd.png)

In a humanoid example, the following issues are visible:

-   The hips are rotating and translating too aggressively.
    
    ![fbik hips pelvis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3683dd19-43fa-44bc-a558-0350cad8a195/problemhips.gif)
    
-   The legs are not bending enough, having a stiff appearance.
    
    ![fbik legs bend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4557f777-1b82-4e8c-ae45-3eb17a0d5fe1/problemlegs.gif)
    
-   The ankle is rotating too far upward, causing an unnatural pose.
    
    ![fbik ankle bend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08cc5de0-ca6d-4e0a-ab59-10c78b88a881/problemankle.gif)
    

**Bone Settings** can be used to resolve issues like these, in order to support your preferred IK setup.

### Rotation and Position Stiffness

**Rotation** and **Position Stiffness** properties are used to control how much a bone in the IK Chain can be affected by controls and effectors. Use these properties to change the degree to which the pelvis bone will be affected by the movement of the controls. A value of **0** results in completely free movement, whereas a value of **1** completely locks the bone from movement.

![fbik stiffness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4c0a89c-9747-43ae-87d2-88d6ff121723/stiffness1.png)

In the humanoid example, the pelvis bone is specified as the bone setting, and a value of **0.8** is set for both **Rotation** and **Position Stiffness**. In this case, some movement is still preferable.

![fbik stiffness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a84892a-5747-4a01-9020-94e9942e5aa6/stiffnessfix.gif)

### Preferred Angles

Preferred Angles can be used to prioritize joints rotating along a specific axis to reach the effector. In the humanoid example, they can be used to resolve stiffness issues in the legs and knees.

Near the bottom of the Bone Settings are properties for **Preferred Angles**. You must also ensure **Use Preferred Angles** is enabled in order to use these Preferred Angles.

![fbik preferred angles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03e6f884-a06d-44e5-a92c-40f8418b464c/preferred1.png)

The Preferred Angle properties you specify depend on the type of character, and its joint structure. For this example, the mannequin's knee should bend along the **Z axis** in a positive direction, therefore a value of **45** should be set on the **Z** property.

![fbik preferred angles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/321f0974-5454-497a-8a5c-e4818b2b22cd/preferredfix.gif)

### Limits

**Limits** can be used to limit the range of, or completely lock, the rotation of bone axes along the IK chain. These settings are located between the Stiffness and Preferred Angles properties.

![fbik limits](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/571d5f1e-1067-4d05-80a4-df1d01f99bf2/limits1.png)

Each axis has settings that allow for the following limits:

-   **Free**, which allows for the bone to move freely.
-   **Limited**, which only allows movement within a specified range. If this is chosen, then the **Min/Max** properties are used to define the range of movement.
-   **Locked**, which disables movement along that axis.

In the humanoid example, these limits can be used to correct the unnatural ankle rotation issue. A value of **\-70** is set for **Min Z** and **70** for **Max Z**, and the **Z** axis is set to **Limited**.

![fbik limits](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f086f889-9890-4dc7-8c74-1e196829685c/limitsfix.gif)

## Excluding Bones

Depending on the needs of your rig, there may be cases where you want to exclude bones from the FBIK solve. This can be useful when correcting unnatural-looking poses, or when simplifying FBIK behavior.

![fbik excluded bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/21b259f3-e755-4d13-81d7-98ec3789a7ae/exclude1.png)

Excluding bones is recommended rather than exclusively using Bone Settings to set bones to be fully stiff or locked.

To exclude a bone, click the **Add (+)** button next to **Excluded Bones**, and select a bone from the dropdown menu to exclude.

![fbik excluded bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/435b57cc-9370-424f-9913-02a8ccb3b3e1/exclude2.png)

## Node Reference

The following is a list of all the pins and settings on the Full Body IK node.

| Name | Description |
| --- | --- |
| **Root** | The root bone for the FBIK chain. |
| Effectors |   |
| **Bone** | An endpoint bone for the IK chain, which corresponds to a control. |
| **Transform** | The transform to use to control the end-point bone. Typically this is provided by a **Get Transform** node linked to a control that shares the same transform information as the end-point bone. |
| **Position Alpha** | This property weighs the ability for the effector or bone to reach the target's **position**. When set to **1**, the effector does its best to reach the target transform. When set to **0**, the effector remains at the input pose. |
| **Rotation Alpha** | This property weighs the ability for the effector or bone to reach the target's **rotation**. When set to **1**, the effector does its best to reach the target transform. When set to **0**, the effector remains at the input pose. |
| **Strength Alpha** | This property affects the strength of this effector's influence on the IK chain. When set to **0**, the effector will not pull the chain towards it and other effectors will take priority. |
| **Pull Chain Alpha** | When enabled by setting the value greater than 0.0, the FBIK solver will partition the skeleton into "chains" which extend from the effector to the nearest skeleton hierarchy divergence. Using this can improve results for sparse bone chains, but cause undesirable results for more complex constrained bone chains. |
| **Pin Rotation** | Blends the effector bone rotation between the rotation of the effector transform (**1.0**), and the rotation of the input bone (**0.0**). |
| Bone Settings |   |
| **Bone** | The specified bone these settings are applied to. This can be any bone in the hierarchy between the **Effectors** and the **Root**. |
| **Rotation/Position Stiffness** | The amount of stiffness to apply to a bone's rotation or translation property. A value of **0** allows for free movement, whereas a value of **1** will completely lock down the bone. |
| **XYZ Limit Setting** | 
The type of allowed movement on the selected bone's axis.

-   **Free** allows for the bone to move freely.
-   **Limited** allows movement within a specified range. If this is chosen, then the **Min/Max** properties are used to define the range of movement.
-   **Locked** disables movement along that axis.



 |
| **Min/Max XYZ** | If **Limited** is set as a **Limit Setting**, the Min/Max XYZ properties are used to specify the range of movement allowed. |
| **Use Preferred Angles** | Enables the use of **Preferred Angles**. |
| **Preferred Angles** | Specifies how much the Bone should rotate, in each axis, as the chain is compressed. |
| Settings |   |
| **Iterations** | Increase this value until the effectors converge on their desired goal locations. Increasing this value also increases the CPU cost of the FBIK chain. The addition of **Stiffness**, a high **Mass Multiplier** and **Rotation Limits** can all affect the convergence rate and may require more adjustments to this value. |
| **Mass Multiplier** | This is a global value that affects how much the bones resist rotations and translations. Typical values range between **0.0** and **5.0**, with **0.0** being completely loose and **5.0** being very stiff. Higher **Mass Multiplier** values require more iterations to achieve convergence. |
| **Allow Stretch** | Enabling this will cause bones along the IK chain to translate to reach their effector. Position Stiffness values affect this result, where higher stiffness will cause less stretching. |
| **Root Behavior** | 

Sets the behavior of the solver root. You can select from the following options:

-   **Pre Pull**, which translates the root and all children by the average motion of the stretched effectors to help achieve better convergence when reaching far distances.
-   **Pin to Input**, which locks the translation and rotation of the root bone to the input pose and overrides any bone settings applied to the root. This can be useful for low-distance, partial-body setups.
-   **Free**, which makes the root bone behave like other bones in the chain, allowing it move freely or according to any bone settings applied to it.



 |
| **Start Solve from Input Pose** | When enabled, the solver is reset each tick to start from the current input pose. If disabled, incoming animated poses are ignored and the solver starts from the results of the previous solve. |
| Debug |   |
| **Draw Scale** | Multiplier that controls size of debug lines. |
| **Draw Debug** | Enable this to show all affected bones along the IK chain for this FBIK node. |