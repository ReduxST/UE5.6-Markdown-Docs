# Constraints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:00

---

When animating, there may be cases where you need to attach elements together without causing a change in the Outliner or Control hierarchy. This kind of attachment is known as **constraining**. Constraints in Unreal Engine are broken up into different methods: **Position**, **Rotation**, **Scale**, **Parent**, and **LookAt**. With these methods, you can set options to control how these constraints operate, such as controlling the attachment offset and baking the constraint back to normal keyframes.

This document provides an overview of constraining in Sequencer, and the different workflows for each constraint method.

#### Prerequisites

-   You have created a **Control Rig Asset**. Refer to the [Control Rig Quick Start](/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine) page for information on how to do this.
-   Constraints when animating are accessed through the [Animation Mode](/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine) panel, therefore you need to enable **Animation Mode**.
-   Constraining is mainly dependent on using Control Rig within **Sequencer**, therefore you need a [basic knowledge](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) of Sequencer.

## Create a Constraint

Constraint information, as well as the workflow for adding constraints, is located in the Animation panel when [Animation Mode](/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine) is enabled.

![constraint section in animation panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2757924a-9bdc-4cfe-9ea6-208371fe1e52/create1.png)

Constraints are established by creating a **Parent - Child** relationship between two or more objects. To create a new constraint, first select your Controls you want to constrain (child), then click **Add Constraint (+)** and select a constraint type. Your cursor changes to an eyedropper tool you can use to select the object to constrain to (parent) in the Viewport.

![create constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31ab3b07-c793-4df7-b951-a8cbadf5c328/create2.gif)

Constraining is not limited to Control Rig elements, you can constrain any object or Actor. Additionally, Actors can be constrained without needing Sequencer to be open.

After creating your constraint, you can view its keyframe information in Sequencer for the constrained Control. Most constraints will also create compensating keyframes, which maintains the current visual position of the child when the constraint activates. These compensating keyframes are linked to the constraint keyframe, and follow it if you change the timing.

![constraint keyframe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82185aee-9837-4377-aa27-f848ef4606ec/create3.gif)

## Constraint Usage

Your constraints can also be viewed in the Animation Panel's **Constraints** section, when selecting the constrained Control. Here you can create new constraint keyframes, edit the properties of the constraint, and bake the constraint back to normal keyframes.

![constraint select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f71dd667-35d7-4eed-b167-c69056550013/manage1.png)

If you have more than one constraint applied to an object, they also appear here too. When you play or scrub the sequence, each constraint indicates its status by highlighting when it becomes active or inactive.

![constraint switching](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf02d51b-3e73-4a51-aac9-2fc930c34c46/manage2.gif)

The buttons for a constraint entry provide the following functionality:

| Button | Description |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec71bd73-5f2b-4663-9ff7-c22dbdbfa6cc/button1.png) | 
Creates an active keyframe for the constraint at your current time in Sequencer. If the constraint is already active, then a deactivate keyframe is created instead. Compensating keyframes are also created to maintain the same world position on the constrained object

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceeb0117-3a7f-4b3e-b38e-5ac04aa7cfb3/manage4.gif)

 |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4fc207b-8fd7-48e0-98e7-0b79f43694f9/button2.png) | 

If you have multiple constraints on the same object, these buttons move the constraint up or down on the list. Constraints in Unreal Engine are hierarchical and override other constraints higher on the list (only if the constraints animate the same channels). New constraints always take priority over older ones and are placed lower on the list.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df7a2ee2-42e7-4ca0-b0b7-d0d776d0ff9e/manage6.gif)

Because constraints can be overridden, it is not always necessary to deactivate other constraints. For example, since [Parent Constraints](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#parentconstraint) animate all transform channels of a control, simply activating one is enough to essentially deactivate all others, so long as the one activated is higher priority. In this example, although both constraints are active, only the **root** constraint is providing the constraint effect due to it being lower in the list and higher priority

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2c4ca48-40af-41c8-9aa3-d93070014484/manage5.png)

 |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9df41bfe-39a7-46eb-b276-866f7070cff9/button3.png) | Removes this constraint. |

Right-clicking on a constraint entry reveals a context menu where you can edit properties specific to that constraint type, [bake](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#bakeconstraint) the constraint, and set [compensating keyframes](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#compensatekeyframes).

![constraint properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b8a5de6-2a66-464d-ab7b-d9185cd81d1e/manage3.png)

### Bake Constraint

Once you have finalized animating with constraints, you can bake the final result to keyframes. This can be useful if you want to revert to normal keyframe animation to make further edits without constraint considerations.

To bake your selected Controls, right-click a constraint entry and select **Bake**.

![bake constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e420da5d-7e13-4021-bf5a-057d67af4a31/bake1.gif)

### Compensate Keyframes

When animating, there may be cases where the constraint exhibits a noticeable pop when it activates or deactivates. This commonly happens if you adjust the pose of the parent after the constraint has been created, which breaks the visual matching that the original compensating keyframes were providing.

![constraint pop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16f83f57-839b-4959-b31e-cbd45ed7d7e4/compensate1.gif)

To resolve this, select the offending Controls, right-click the constraint, and select **Compensate Key**. You must also ensure that the Sequencer **Playhead** is on the same time as the constraint keyframe that you want to fix. This will re-create new compensating keyframes for the new location of the parent object.

![fix constraint pop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14648b9d-2e5b-4e1a-8137-71b9889d62dc/compensate2.gif)

While **Compensate Keys** can be used to resolve errors with single constraints, **Compensate All Keys** can also be used to re-create all compensating keyframes for every constrained Control in the sequence, regardless of selection or Playhead position.

### Dynamic Offset

By default, you can keyframe the constrained object in addition to the constraint affecting it. If you want to disable this option and not allow the child object to animate, right-click the constraint and disable **Dynamic Offset**. This locks the position of the constrained object at its current transform, and it will now only move if the parent object moves.

![dynamic offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/418052cc-071f-4fea-80fa-f58da74d377f/dynamicoffset.gif)

### Constraints Manager

As you constrain many objects in your Level Sequence, it may become more difficult to manage and view your constraints. You can use the **Constraints Manager Actor** as a way to view and manage all constraints within a Level.

When you create any constraint for the first time, the **Constraints Manager Actor** automatically creates within your level, and selecting it consolidates all used constraints into a single list. This makes it easier to view and manage large numbers of constraints on several objects at the same time.

![constraints manager](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1fcc8285-7690-4afe-b7e3-6b2ad7f2286d/manager1.png)

## Constraint Types

The following constraint types can be created when clicking **Add Constraint (+)**:

![constraint types](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e74cfd05-44ee-4d70-9291-83f51519b810/types1.png)

-   [Translation Constraint](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#translationconstraint)
-   [Rotation Constraint](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#rotationconstraint)
-   [Scale Constraint](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#scaleconstraint)
-   [Parent Constraint](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#parentconstraint)
-   [LookAt Constraint](/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine#lookatconstraint)

### Translation Constraint

**Translation Constraints** constrain an object along translation axes only. It follows the parent position but not its rotation or scale.

![translation constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc3878db-7efb-4aac-97c1-df76cce0e2c9/types2.gif)

If **Maintain Offset** is disabled from the constraint context menu, then the constrained object follows the parent object position in absolute coordinates, instead of relative to when the constraint was made.

![translation constraint maintain offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3310994-274c-4989-a6cd-31561178ae53/types3.gif)

### Rotation Constraint

**Rotation Constraints** constrain an object along rotation axes only. It follows the parent rotation but not its translation or scale.

![rotation constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/badac4c8-32cd-48cd-ba3c-44261484912d/types4.gif)

If **Maintain Offset** is disabled from the constraint context menu, then the constrained object follows the parent object rotation in absolute coordinates, instead of relative to when the constraint was made.

![rotation constraint maintain offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07ef5720-70c6-4d3f-81a5-96989e8c799a/types5.gif)

### Scale Constraint

**Scale Constraints** constrain an object along scale axes only. It follows the parent scale but not its translation or rotation.

![scale constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b919c1b-f768-4343-8acd-2cbb285ecf96/types6.gif)

If **Maintain Offset** is disabled from the constraint context menu, then the constrained object follows the parent object scale in absolute coordinates, instead of relative to when the constraint was made.

![scale constraint maintain offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4c221a96-478a-4e95-85a2-dd9534e6b111/types7.gif)

### Parent Constraint

**Parent Constraints** constrain an object along all axes and channels to a parent as if it were attached hierarchically.

![parent constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c735c805-be61-432e-b0db-c2976784bc84/types8.gif)

By default, scale is not included in a Parent Constraint. To include it, right-click on the constraint entry and enable **Scaling**.

![enable scale in parent constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5be7bf9e-baf8-4a65-8138-18b2ce2d0fc7/types9.gif)

Similar to the other constraint types, disabling **Maintain Offset** causes the constrained object to follow the parent transform in absolute coordinates, instead of relative to when the constraint was made.

### LookAt Constraint

**LookAt Constraints** constrain an object along rotation axes only by aiming at the parent location.

![aim constraint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/040b2a1d-c896-4e14-9392-9fb9883d843a/types10.gif)

You can set the aim direction for the child object by right-clicking the constraint entry and editing the **Axis** properties.

![aim axis](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4d0a87c-b4f1-436b-9c5d-3d4d017050c7/types11.png)

Unlike other aim-type attachments, the LookAt Constraint does not use up vectors. Instead, you can animate the **roll** axis to manually control how you want the roll to behave. This can also be useful to eliminate rotation flipping problems, which are common in other aim-type attachments.

![aim constraint roll no flip](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/12eb31b5-b56e-4ce7-a372-26489cc07fab/types12.gif)