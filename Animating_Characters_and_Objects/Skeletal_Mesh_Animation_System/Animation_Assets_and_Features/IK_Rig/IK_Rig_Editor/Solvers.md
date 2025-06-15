# Solvers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:46

---

IK Rig supports a variety of IK Solvers to affect a wide range of Bone hierarchies. They are used to create the Inverse Kinematic solution to rotating and positioning Bones in a chain. Multiple Solvers can also be used at the same time to further customize the IK effect.

This page provides an overview of the different Solvers you can add within the IK Rig editor, and their properties.

#### Prerequisites

-   You have created and opened an IK Rig Asset. See the [IK Rig Editor](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine) page for how to do this.
-   You are familiar with how to create [IK Goals](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals).

## Creating Solvers

The primary way to create Solvers is by clicking **Add New Solver** in the **Solver Stack** panel, then selecting a **Solver**.

![add new solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c33dc3ea-77c9-4994-beb5-812c15b0b897/create1.png)

If a Solver does not already exist in your IK Rig, then creating an **IK Goal** will also prompt you to create a Solver, which automatically binds to that goal. Click the **Solver Type** dropdown menu to select a Solver.

![add default solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92e701e3-679f-441e-a55c-20526c76db58/create2.png)

## Solver Usage

All IK Solvers require either a **root Bone**, **IK Goal**, or both to be specified. These two starting and ending Bones will complete the IK chain for that Solver.

![root bone goal bone](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/618d4aa8-c30f-48d7-92c4-aea932331efc/example.png)

1.  The root Bone at the start of the hierarchy chain.
2.  The goal, or effector Bone at the end of the hierarchy chain. This is driven by an [IK Goal](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoal).

### Connecting to Bones and Goals

To set the root Bone to a Solver, select the **Bone** in the **Hierarchy** and the **Solver** from the **Solver Stack**, then right-click on the **Bone** and select **Set Root bone on Selected Solver**.

![set root bone on selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1dfd7e9-c925-429c-8d04-119a5f9400c8/connect2.gif)

If your Solver requires an IK Goal, connect it by selecting the **goal** from the **Hierarchy** and the **Solver** from the **Solver Stack**, then right-click on the **goal** and select **Connect Goal to Selected Solver**.

![connect goal to selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0672a19b-68de-428e-bc34-51262429432d/connect1.gif)

Once Bones and goals are connected to a Solver, selecting the Solver will highlight those objects within the Hierarchy, as well as in the Viewport.

![bone highlight](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e35fe38-c83a-4801-b68d-b51c776094b9/create3.png)

### Multiple Solvers

Multiple Solvers can also be added to the Solver Stack, which provides extra functionality for your IK Rigs. The order of multiple Solvers will matter, as they evaluate in sequence, denoted by the number next to their name.

![multiple solvers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abf0bda7-821a-4eb4-90a2-77c22c25aa69/multiple1.png)

For example, in most leg IK setups, you may want to ensure that the **Set Transform Solver** on the hips evaluates first, before the Limb IK leg chains. This is so the legs can properly compensate for the movement of the hips beforehand.

![solver order of execution](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35270a5e-c9b8-467e-b2d9-04d820388db5/multiple2.png)

Solvers can be rearranged by dragging them up and down in the Solver Stack.

![rearrange solvers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86c91014-a072-42df-9694-6ecc44da98eb/multiple3.gif)

### Excluding Bones

Bones within an IK chain can be excluded from the hierarchy, causing them to be ignored by all Solvers. This can be useful to correct bad poses, or to simplify a complex chain.

To exclude Bones, select all the **Bones** to be excluded, then right-click on them and select **Exclude Selected Bone From Solve**. Excluded Bones are denoted with a different icon.

![exclude selected bone from solve](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9c6855e1-40dc-426f-99ed-50d5eeaa7912/excluded1.png)

You can re-include excluded Bones by right-clicking them and selecting **Include Selected Bone In Solve**.

## Solver Types

The following is a list of the different Solvers you can use in IK Rig.

### Body Mover

The **Body Mover Solver** will translate and rotate the root Bone based on the location of other connected IK Goals, which are typically the feet. Using Body Mover allows IK Rig to generate large-scale, gross movement of the body resulting in a more natural final pose

#### Setup

Body Mover requires a root Bone and at least two IK Goals to be connected. However, it can support several goals if the character is quadrupedal or multi-legged.

#### Usage

Body Mover is mainly intended for ground alignment, and should be used as the first Solver paired with other Solvers, such as [Limb IK](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine#limbik) or [Full Body IK](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine#fullbodyik).

For example, on its own, Body Mover does not produce correct looking results as an IK Solver.

![body mover solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ddea3dd-fc77-4ef7-a7e0-891381819261/bodymover1.gif)

However, once other IK Solvers are set up to evaluate after it, and with appropriate settings applied, then Body Mover will function more naturally.

![body mover solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bbc70f46-9d81-4deb-8375-91c16b2f431f/bodymover2.gif)

#### Settings

Selecting the Body Mover Solver will reveal additional settings in the Details panel.

![body mover settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b93bcf66-d0d0-490f-8a3f-df44a3df34f1/bodymover3.png)

These settings are used to control the degree of movement exerted on both position and rotation axes, including their channels. In certain cases it may be necessary to adjust these properties to provide a more natural looking pose.

For example, on humanoid characters, setting **Rotation Alpha** to **0** will resolve the character leaning unnaturally towards the offset goal.

![body mover fix rotation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea4e4fd8-d591-4172-b4c9-8fc6e6afba43/bodymover4.gif)

However, on quadrupedal or multi-legged creatures, it may be more natural to keep this root rotation and not change any settings.

![body mover spider](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89800902-717b-4e1d-b5a1-8d6bb4630ad0/bodymover5.gif)

#### Goal Settings

Selecting a **Goal Setting** located underneath a goal assigned to the Body mover solver will reveal additional properties in the **Details** panel.

![body mover goal settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77852fdf-ca5a-40f7-9baa-384c9790453a/bodymover6.png)

**Influence Multiplier** is used to increase or decrease the amount of influence this goal exerts on the Body Mover solver, and can be useful if you want a goal to have more influence compared to others.

### Limb IK

Limb IK provides a cheaper-performance single-chain IK Solver. Typically you will want to use this for individual limbs, such as arms and legs.

#### Setup

Limb IK requires a root Bone and a single IK Goal to function. It follows typical IK rules in that you specify the starting bone (root), and an ending bone (goal). This Solver requires at least three Bones in the chain, in order to work correctly.

In most cases, you should specify the **shoulder** or **arm** as the root, and the **hand** as the goal. For legs, you should specify the **upper leg** or **thigh** as the root, and the **foot** as the goal.

![limb ik](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8160fe6-bd9d-46a6-b142-7befb9b86e4a/limbik1.png)

#### Settings

Selecting **Limb IK** from the Solver Stack panel will reveal additional properties in the **Details** panel. These properties are only valid if your Limb IK chain is made up of more than 3 Bones. So if you are using Limb IK for a normal humanoid **Thigh > Leg > Foot** solve, then these properties will not affect its behavior.

![limb ik settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2797d42a-5b46-4470-b58c-9d76b4165624/limbik2.png)

| Name | Description |
| --- | --- |
| **Root Bone** | The root Bone assigned to this Limb IK solver. |
| **Reach Precision** | This value controls the accuracy threshold of the effector reaching the goal's position. Lower numbers are more accurate and higher numbers are less accurate. |
| **Hinge Rotation Axis** | The normal plane for the solver chain. |
| **Max Iterations** | Increasing this value will cause the joint chain to better converge on the goal location, but increases the CPU cost of the Limb IK chain. |
| **Enable Limit** | Enables rotational limits on the joint chain between the root and effector. |
| **Min Rotation Angle** | If **Enable Limit** is enabled, this forces at least this input angle between the parent and child bone. |
| **Average Pull** | Enables an average pull distribution along the joint chain. |
| **Pull Distribution** | Manual control of the weight of the pull distribution along the chain if **Average Pull** is disabled. Lower numbers favor the effector, and higher numbers favor the root. |
| **Reach Step Alpha** | Moves the end effector towards the target and limits displacement. |
| **Enable Twist Correction** | Enables twist correction along the solver chain by comparing the orientations of bones along the chain. |
| **End Bone Forward Axis** | Which axis to favor if **Enable Twist Correction** is enabled. |

### Full Body IK

Full Body IK (FBIK) is a fully-featured multi-goal IK solver that supports Bone limits, stiffness, and preferred angles. This Solver is useful if you want to create a large-scale IK system for multiple goals, with each of them exerting natural influence upon the whole body.

#### Setup

A root Bone and at least one IK Goal must be connected for Full Body IK to function. However, unlike Limb IK, multiple goals may be added to allow the skeleton to reach for multiple locations simultaneously.

![full body ik multiple goals](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49c51de1-2208-4fe3-a46a-1691e01d11b2/fbik1.gif)

#### Usage

FBIK differs from other solvers in that you can create settings for any of the Bones affected by the Solver. This is so you can further refine the movement of a specific Bone within the FBIK chain.

To create a Bone setting, select the **Full Body IK Solver**, then right-click a **Bone** you want to create settings for and select **Add Settings to Selected Bone**.

![full body ik bone settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3aed254-ac71-4dc6-97fb-4fdb273bd4f4/fbik2.png)

Selecting the Bone setting in the Hierarchy will reveal the following Bone settings in the Details panel:

![full body ik bone settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b88c4b94-582e-421b-b05a-990264fa5674/fbik3.png)

| Bone Setting | Description |
| --- | --- |
| **Stiffness** | 
**Rotation** and **Position Stiffness** properties are used to control how much a bone in the IK chain can be affected by goals and effectors. Use these properties to change the degree to which the pelvis bone will be affected by the movement of the controls. A value of **0** results in completely free movement, whereas a value of **1** completely locks the bone from movement.

In this humanoid example, the pelvis bone is specified as the root Bone for the FBIK chain, however in its base state it is rotating too aggressively. Increasing the **Stiffness** properties resolves this.

![fbik stiffness](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d1be251-2dad-484a-ac46-2d115376ba02/fbik4.gif)

 |
| **Limits** | 

**Limits** can be used to limit the range of, or completely lock, the rotation of bone axes along the IK chain. Each axis can be set to the following:

-   **Free**, which allows for the bone to move freely.
-   **Limited**, which only allows movement within a specified range. If this is chosen, then the **Min/Max** properties are used to define the range of movement.
-   **Locked**, which disables movement along that axis.

Using limits can help with correcting unnatural joint movement. For example, these limits can be used to correct the unnatural ankle rotation issue. A value of **\-50** is set for **Min Z** and **40** for **Max Z**, and the **Z** axis is set to **Limited**.

![fbik limits](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd6a8a68-f255-4344-8efd-329b1606f735/fbik5.gif)

 |
| **Preferred Angles** | 

**Preferred Angles** can be used to prioritize joints rotating along a specific axis to reach the effector. In some cases they can be used to resolve rigid issues in joint rotation. Enabling **Use Preferred Angles** will cause the rotation to reference the **Preferred Angles**.

The Preferred Angle properties you specify depend on the type of character, and its joint structure. For this example, the mannequin's knee should be bending more along the **Z axis**, therefore the **Z** property is increased.

![preferred angles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0023cc5-87e8-4243-976c-9043c21dbb99/fbik6.gif)

 |

#### Settings

Selecting the Full Body IK Solver reveals the following properties in the Details panel:

![fbik settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/453615a9-8dce-4458-8812-be63c0011915/fbik7.png)

| Name | Description |
| --- | --- |
| **Iterations** | Increasing this value will cause the effectors to converge on their goal locations, but increases the CPU cost of the FBIK chain. The addition of **Stiffness**, a high **Mass Multiplier**, and **Rotation Limits** can all affect the convergence rate and may require more adjustments to this value. |
| **Mass Multiplier** | 
This is a global value that affects how much the bones resist rotations and translations. Typical values range between **0.0** and **10.0**, with **0.0** being completely loose and **10.0** being very stiff. Increasing this value also requires you to increase **Iterations** in order to achieve convergence.

Increasing Mass Multiplier can resolve severe convergence problems within FBIK, which occur most commonly with larger characters. In general, the larger your character is, the higher this number should be.

![mass multiplier twitching fix](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c695007-93a2-4153-830a-bb8190d06e28/massmultiplier.gif)

 |
| **Min Mass Multiplier** | Keep this value as low as possible as long as the Solver provides stable results. Lower values improve the convergence of the chain. |
| **Allow Stretch** | Enabling this will cause bones along the IK chain to translate to reach their effector. **Position Stiffness** values affect this result, where higher stiffness will cause less stretching. |
| **Root Behavior** | 

Controls the translation behavior of the root Bone. You can select the following options:

-   **Pre Pull** limits the translation of the root by the average motion of the goals. This helps achieve better convergence so that all goals are reached.
-   **Pin to Input** locks the translation and rotation of the root. This also cancels any Bone settings applied to the root Bone.
-   **Free** allows the Bone to move freely or according to any bone setting. This setting requires more iterations to be set to achieve convergence when compared to **Pre Pull**.



 |
| **Start Solve from Input Pose** | When enabled, the Solver is reset each tick to start from the current input pose. If disabled, then the incoming animated poses are ignored and the solver starts from the results of the previous solve. |

#### Goal Settings

Selecting a **Goal Setting** located underneath a goal assigned to the Full Body IK Solver will reveal additional properties for that goal in the **Details** panel.

![fbik goal settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4143a52-92b4-471f-ba94-0285e142caf0/fbik8.png)

| Name | Description |
| --- | --- |
| **Strength Alpha** | This property affects the strength of this effector's influence on the IK chain. Lower numbers will cause this IK Goal to not pull the chain towards it as strongly, causing other goals to take priority. |
| **Pull Chain Alpha** | When enabled by setting the value greater than **0.0**, the FBIK solver will partition the skeleton into "chains" which extend from the effector to the nearest skeleton hierarchy divergence. Using this can improve results for sparse bone chains, but cause undesirable results for more complex constrained bone chains. |
| **Pin Rotation** | Blends the effector bone rotation between the rotation of the effector transform (**1.0**), and the rotation of the input bone (**0.0**). |

### Pole Solver

The Pole Solver provides **Pole Vector** controls for a single Bone chain, which is used to orient middle joints to face an IK Goal, like elbows or knees. Typically this Solver should be used in conjunction with other Solvers, such as [Limb IK](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine#limbik).

#### Setup

Pole Solvers differ from other solvers in that you must specify both a root and end Bone. This is done by right-clicking on the root and end bones and selecting **Set Root / End Bone on Selected Solver**. In this example, the upper arm is set as the root, and the hand is set as the end.

![pole solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/144fc7e9-25c8-4626-b83a-2829de7f8b94/pole1.png)

An IK Goal must also be used which will act as the Pole Vector. In most cases you must create it for the first child bone of the root.

For example, in a simple three-bone chain, the IK Goal must be created on the first child Bone of the root. This would place it on the middle joint.

![pole solver three bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b795cafd-0948-4e22-bf6a-c9dd41a7c4e5/pole2.png)

In longer chains, the first child will not be the middle joint, making the IK Goal located closer to the root.

![pole solver five bones](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff4686d8-fa04-4025-ba2e-3d7de678e170/pole3.png)

Once the root, end, and goal is specified, you can manipulate the IK Goal to preview the Pole Solver.

![pole solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2ecbc7e-ef45-4b64-8384-9ce1f5f0e6bd/pole4.gif)

#### Usage

In most cases you should pair the Pole Solver with another Solver, with the Pole Solver executing last. In this example it is being paired with an IK Limb Solver.

![pole solver with other solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c137815-41ca-4e78-9c0a-17acaca6abc8/pole5.gif)

### Set Transform

Set Transform will translate and rotate a bone to match a goal. No IK system is involved as this Solver simply translates and rotates a single Bone and any children. In most cases this Solver should be paired with others to achieve a more complex IK effect.

#### Setup

This Solver only requires a single IK Goal to be connected, which is used as the transform point.

![set transform solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8372d34e-71f6-447f-bb61-fc4889af59ec/transform1.png)

#### Usage

Typically you may want to pair this Solver with other solvers, with Set Transform executing first. In this example, **Set Transform** on the hips is being paired with **Limb IK** on the legs.

![set transform solver multiple](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17faaca8-9067-4929-9c6a-1d058fca2f3e/transform2.gif)