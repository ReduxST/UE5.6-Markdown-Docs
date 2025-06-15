# IK Rig Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:45

---

The **IK Rig editor** is where you set up IK Rigs and retargeting for characters. With it, you can create different Solvers, adjust Bone settings, and preview your results.

This page provides an overview of this editor and how to create IK Rig Assets.

#### Prerequisites

-   IK Rigs require a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-actors-in-unreal-engine) in your project.

## Create IK Rig

To start creating IK Rigs, you must create an **IK Rig Asset**. To do this, click **Add (+)** in the **Content Browser**, then select **Animation > IK Rig**. A dialog window will open where you select the Skeletal Mesh you want to create the IK Rig for.

![create ik rig](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/915126ba-2526-4f34-a6a8-5cf94d9a1623/create.png)

After selecting the Skeletal Mesh, the IK Rig Asset will be created. Double-click it in the **Content Browser** to open it.

## Editor and Feature Overview

The IK Rig editor contains the following tools and options:

![ik rig editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8b60eb25-2211-4bd2-bec0-5c285bdd4bda/overview.png)

1.  The **Reset** button, which resets [IK Goals](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) to their default position.
2.  **Hierarchy**, which displays your Bones, IK Goals, and settings.
3.  **Solver Stack**, which displays the [IK Solvers](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine) being used on this Skeletal Mesh.
4.  **Viewport**, where you can select your Bones and manipulate IK Goals to preview the IK behavior.
5.  **IK Rig Output Log**, which displays debug information about your IK Rig. It displays warnings and errors indicating the current status of the rig.
6.  The **Details** panel displays properties for your selected item. **Preview Scene Settings** is where you can change the ambient viewport environment, such as lighting and background.
7.  The **Asset Browser** displays a list of [Animation Sequences](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) that you can preview along with your IK behavior to test its effects. **IK Retargeting** is where you specify Bone chains for use with an IK Retargeter asset if you are [retargeting](/documentation/en-us/unreal-engine/ik-rig-animation-retargeting-in-unreal-engine) this character using IK Rig.

### IK Goals

IK Goals are the manipulation and effector points for your IK chains, which you create in the IK Rig Editor. IK Goals are used in conjunction with [Solvers](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine) to modify an incoming pose to reach the goal locations.

To create IK Goals, first select the ending Bones in the IK chain you want to create. Typically, these would be the hand or foot Bones if you are creating IK along the arms or legs.

![create ik goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9427e9ad-9a85-482c-b534-8b851ab704e7/goal1.png)

Next, click **Add (+)** in the Hierarchy panel and select **New IK Goal**. If your IK Rig does not already have a Solver, then a dialog window will appear where you can select a Solver to associate with the new goal. For common IK setups, you can select **Limb IK**, then click **OK**.

![new ik goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc7dd2cb-5936-4cd2-a63f-3c32c08923db/goal2.png)

You can also right-click Bones in the Hierarchy panel to access the **Add (+)** menu.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34882247-5805-46b0-88fe-b4db7a2ea667/goal2b.png)

The goal and Solver-specific settings will now be created and be visible in the Viewport and Hierarchy.

![ik goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a7190c6-4c6b-4b6f-8c62-ada603fbefc2/goal3.png)

#### IK Goal Properties

When you select an IK Goal, you will see the following properties in the **Details** panel:

![ik goal details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3782d9ce-a537-4c77-9bf1-2ef25d2fc148/goal4.png)

| Name | Description |
| --- | --- |
| **Goal Name** | The name of the IK Goal object. |
| **Bone Name** | The name of the end Bone that the IK Goal is acting as the effector for. |
| **Position Alpha** | 
Blends the final location of the IK Goal from the position of the Goal bone in the input pose (**0**) to the Goal's own position (**1**).

![position alpha](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7de7ecc-bff3-4deb-a2d0-77c4a448c24a/goalpositionalpha.gif)

 |
| **Rotation Alpha** | 

Blends the final rotation of the IK Goal from the rotation of the Goal bone in the input pose (**0**) to the Goal's own rotation (**1**).

![rotation alpha](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7221f90f-0456-41c5-8c75-620eb0151e4a/goalrotationalpha.gif)

 |
| **Preview Mode** | 

Previews (in editor only) the goal in either **Additive** or **Absolute** modes. **Additive** is used when you want to ensure the IK behavior is relative to any incoming animation, whereas **Absolute** overwrites any incoming animation along the chain. Additive goal behavior can be achieved at runtime by setting your goals to **Manual Input** and **Additive** on the [IK Rig Anim Graph node](/documentation/en-us/unreal-engine/ik-rig-in-animation-blueprints-in-unreal-engine).

![preview mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc6d4018-43a0-4b5d-903b-2ffb3ca2111e/goalmode.gif)

 |
| **Transforms** | Contains the current transform information for the selected IK Goal. |
| **Size Multiplier** | 

Multiplies the size of the IK Goal relative to its base size from the [viewport settings](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#viewportsettings). Increase this if you have larger, non-human characters.

![size multiplier](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/62479ed9-ac0e-4a4d-844d-c2fb9b24a0ac/goalsize.gif)

 |
| **Thickness Multiplier** | 

Multiplies the line thickness of the IK Goal relative to its base thickness from the [viewport settings](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#viewportsettings) You may want to increase this if you have increased the **Size Multiplier**.

![thickness multiplier](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ea7fc37-67d5-4f8a-930c-b051d188aa2f/goalthick.gif)

 |
| **Expose Position** | Exposes position pins on the [IK Rig Animation Blueprint Node](/documentation/en-us/unreal-engine/ik-rig-in-animation-blueprints-in-unreal-engine) in order to affect the position of the IK Goal in [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine). |
| **Expose Rotation** | Exposes rotation pins on the [IK Rig Animation Blueprint Node](/documentation/en-us/unreal-engine/ik-rig-in-animation-blueprints-in-unreal-engine) in order to affect the rotation of the IK Goal in [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine). |

### Solvers

Different IK behaviors can be added to your IK Rig, which are called **Solvers**. Using Solvers, you can create a wide variety of IK effects, from simple three-bone chains to full-body multi-limb IK systems.

Visit the [Solvers](/documentation/en-us/unreal-engine/ik-rig-solvers-in-unreal-engine) page to learn more about the different Solvers you can add, and how to use them in your IK Rigs.

### Viewport Settings

When nothing is selected in the IK Rig editor, the **Details** panel will display the following Viewport settings:

![ik rig viewport settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77b6a706-a717-4960-9990-03c200081521/viewportsettings.png)

| Name | Description |
| --- | --- |
| **Preview Skeletal Mesh** | The Skeletal Mesh to run the IK solve on. You can change the assigned Skeletal Mesh here and the IK Rig system will attempt to run on the replacement. If the new Skeletal Mesh contains incompatible bone names or hierarchies, then the IK Rig will not function. You can reference the **IK Rig Output Log** for more information on any incompatibilities. |
| **Draw Goals** | Shows or hides [IK Goals](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) in the viewport. |
| **Goal Size** | The base size of IK Goals. |
| **Goal Thickness** | The base thickness of IK Goals. |

## IK Rig Example Setup

A common use-case for IK in Unreal Engine is to control foot alignment to uneven terrain, which requires manipulating the feet and hips of a character. The example below will walk you through setting up this IK Rig system for a humanoid character.

### Create Solvers

Start by creating a new Solver. To do this, click **Add New Solver** in the Solver Stack panel, then add the following Solvers:

-   **Set Transform**.
-   **Limb IK**.
-   **Limb IK** again.

![add new solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5550d7db-7254-4019-aef7-8326da24e3da/tut1.png)

The order in which you add the Solvers matters, because Solvers execute in sequence according to the number displayed next to their name. For this IK system, Limb IK should evaluate last.

You can drag Solvers within the Solver stack to change their order if needed.

![change solver order](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13db4575-8b9d-4391-ba6c-9fa9a892ff4a/tut2.gif)

### Create Goals

Due to the Solver types being used for this IK system, you will need to create [IK Goals](/documentation/en-us/unreal-engine/ik-rig-in-unreal-engine#ikgoals) for each Solver. To do this, select the pelvis and feet bones, right-click them, and select **New IK Goal**. Goals will be created at the location of each of these bones.

![create ik goal](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d7eecad0-9d6f-414c-ae74-5d4727bdaa90/tut3.gif)

You can optionally adjust the goals so they appear more prominently in the viewport by selecting them and editing their **Size** and **Thickness Multiplier** properties.

![ik goal size](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ede8dc6a-5aaf-40a5-a053-17f52eb41b1a/tut4.png)

### Connect Goals to Solvers

Each IK Goal must be connected to a Solver for it to correctly act as the effector for that Solver.

To do this, select both the **Solver** and the **IK Goal**, right-click the goal, and select **Connect Goal to Selected Solver**.

![connect goal to selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9bf1f99-0c24-48f1-93ad-d6bccdfaf3a0/tut5.gif)

Repeat this action for each goal and Solver so that all your goals are connected to their respective Solvers.

![connect goal to selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26ce8188-7c8a-450a-9caa-f79af3287b62/tut6.png)

### Set Solver Root

For some Solvers, like Limb IK, you must specify both a **goal** and a **root**. The root is typically the starting Bone of the IK chain. In this example, the **thigh** will be the root.

To set the root for a Solver, select both the **Solver** and the **Bone**, right-click the Bone, and select **Set Root Bone on Selected Solver**.

![set root bone on selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7be32a62-3b74-4d36-997b-d65355cca4a5/tut7.gif)

Repeat this action for both Limb IK Solvers so that both of them have their respective thigh Bones set as the root.

![set root bone on selected solver](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a179bf85-3c6a-461a-a70b-6ee95300b836/tut8.png)

### Final Result

You can now preview your IK system in the viewport by selecting IK Goals and manipulating them. Clicking **Reset** restores your Goals to their initial state.

![ik rig setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/feb10ebd-13b4-4ea4-8cfa-19d9e9bb4ebb/tut9.gif)