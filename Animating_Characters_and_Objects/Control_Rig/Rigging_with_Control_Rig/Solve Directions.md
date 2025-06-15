# Solve Directions

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:36

---

Control Rigs are evaluated in several ways, called **solve directions**, which are created in the Control Rig Rig Graph. By using these tools to split the rig logic into multiple solve directions, or **solvers**, you can expand on the incoming data for a rig, which enables workflows such as rig sharing, baking animation back to your controls, and debugging this behavior.

This page provides an overview of the different solve directions available in Control Rig, how to use them, and the workflows these features enable.

#### Prerequisites

-   You have an understanding of the [Control Rig Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine).
    
-   You have an understanding of [Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine), and know [how to add Control Rig characters to Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-control-rigs-in-unreal-engine).
    

## Forwards Solve

[![forwards solve](https://dev.epicgames.com/community/api/documentation/image/ed514015-57a5-4b19-b97f-b3b49e299de7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ed514015-57a5-4b19-b97f-b3b49e299de7?resizing_type=fit)

Forwards Solve is the solve direction used for driving your skeleton with controls, variables, and other rig elements. It is the primary solve direction for Control Rig, as it is used when animating your Control Rig within Sequencer and Animation Blueprints.

By default, all Control Rig assets will include the Forwards Solve node in the Rig Graph. From this node, the logic you will be creating will be based on affecting the skeleton's bones through controls, variables, and other rig elements. In this way, your controls are behaving in a "forward" manner, where controls affect bones.

[![forward solve rig graph](https://dev.epicgames.com/community/api/documentation/image/55fe3aeb-794d-40e1-94af-1e8220271fc2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/55fe3aeb-794d-40e1-94af-1e8220271fc2?resizing_type=fit)

### Previewing Forwards Solve

Forwards Solve is the default preview mode within the [Viewport](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine). This can be verified by ensuring the solve direction [Toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine) button is set to **Forwards Solve**. Similar to AnimBP's, Forwards Solve will continuously execute regardless of your editor state within a level.

[![forwards solve](https://dev.epicgames.com/community/api/documentation/image/06f82d05-e023-4715-a3c1-9a47e80e825b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/06f82d05-e023-4715-a3c1-9a47e80e825b?resizing_type=fit)

Depending on which solve direction is active, then this will affect which execution lines are highlighted in the rig graph. For example, if Forwards Solve is active, then the execution lines from Backwards Solve will appear more transparent.

[![solve direction execution](https://dev.epicgames.com/community/api/documentation/image/8fccabf8-67ff-4edb-b690-653987be13a2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8fccabf8-67ff-4edb-b690-653987be13a2?resizing_type=fit)

## Backwards Solve

[![backwards solve](https://dev.epicgames.com/community/api/documentation/image/4d4a619d-c54c-4b62-b175-660d60038717?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4d4a619d-c54c-4b62-b175-660d60038717?resizing_type=fit)

Backwards Solve is the solve direction used for driving your controls from your skeleton. It is the **inverse** of Forwards Solve, and is used to bake animation from animation sequences onto a Control Rig in Sequencer.

In order to create Backwards Solve logic in your Rig Graph, you must create a **Backwards Solve** node. Right-click in the **Control Rig Graph** and select **Events > Backwards Solve**.

[![create backwards solve](https://dev.epicgames.com/community/api/documentation/image/043e68da-41ef-4046-88d1-ac5b4ee36999?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/043e68da-41ef-4046-88d1-ac5b4ee36999?resizing_type=fit)

From this node, the logic you will be creating will be based on affecting your controls from the bones in the skeleton. In this way, your controls are behaving in a "backward" manner, where bones affect controls.

[![backwards solve](https://dev.epicgames.com/community/api/documentation/image/7b661b52-f73f-4942-b975-346d929fb506?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7b661b52-f73f-4942-b975-346d929fb506?resizing_type=fit)

### Previewing Backwards Solve

You can preview Backwards Solve behavior in the the [Viewport](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine) by opening the solve direction **dropdown menu** in the [Toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine), then clicking **Backwards Solve**. This will cause the viewport to execute Backwards Solve logic from the Rig Graph, rather than Forwards Solve.

[![enable backwards solve](https://dev.epicgames.com/community/api/documentation/image/67788cb6-28f8-4e20-8cc1-e0036291e672?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/67788cb6-28f8-4e20-8cc1-e0036291e672?resizing_type=fit)

To better preview this inverse Control Rig behavior, you can navigate to the **Preview Scene Settings** panel in Control Rig and specify an animation to play on your character. Set **Preview Controller** to **Use Specified Animation**, then select an animation from the **Animation** property. You should now see your controls match the playing animation.

[![preview backwards solve](https://dev.epicgames.com/community/api/documentation/image/39dd2b0c-22a7-4a7f-80da-b9dd9d0d409b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/39dd2b0c-22a7-4a7f-80da-b9dd9d0d409b?resizing_type=fit)

When previewing Backwards Solve, the viewport will be outlined in a **yellow** border. This color and other colors can be changed in the **Control Rig Editor Preferences**.

[![solve viewport color preference](https://dev.epicgames.com/community/api/documentation/image/267038e7-f447-4937-97dd-740fa05b35a0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/267038e7-f447-4937-97dd-740fa05b35a0?resizing_type=fit)

### Bake Animation to Control Rig

The main use of Backwards Solve is to bake animation sequences to your Control Rig, in order to make further changes to an animation in Unreal Engine.

To do this, assuming you [have an animated character in Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-add-cinematic-animation-to-a-character-in-unreal-engine), right-click on the character track, select **Bake To Control Rig**, then select your **Control Rig Asset** you want to bake to.

[![bake to control rig](https://dev.epicgames.com/community/api/documentation/image/95c5a231-1740-447c-baa6-8df8e3b4fb02?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/95c5a231-1740-447c-baa6-8df8e3b4fb02?resizing_type=fit)

If your Control Rig asset does not use the Backwards Solve node in the Rig Graph, then the Control Rig will not be selectable in the **Bake To Control Rig** menu.

A dialog window will appear where you can specify options related to the bake operation:

[![bake options](https://dev.epicgames.com/community/api/documentation/image/2ebc77a2-882c-4f24-8348-b699d9957ab1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2ebc77a2-882c-4f24-8348-b699d9957ab1?resizing_type=fit)

| Name | Description |
| --- | --- |
| 
**Export Transforms**

 | 

Bakes transform data to controls.

 |
| 

**Export Curves**

 | 

Bakes **AnimCurve** data to controls. This includes AnimCurves when evaluating the Backwards Solve logic.

 |
| 

**Record in World Space**

 | 

Bakes in absolute world space coordinates.

 |
| 

**Evaluate All Skeletal Mesh Components**

 | 

Evaluates all skeletal mesh components when baking. Typically you may want to enable this if you are using a Blueprint with other Skeletal Mesh Components.

 |
| 

**Warm Up Frames**

 | 

The number of frames to evaluate before the baking process occurs. This is useful if there are post process Animation Blueprint effects that require additional time to settle before evaluation.

 |
| 

**Delay Before Start**

 | 

The number of Display Rate frames to delay before the baking process occurs. This is useful if there are post process Animation Blueprint effects you need to run repeatedly before evaluation.

 |
| 

**Reduce Keys**

 | 

Enable this to run a [Simplify](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine) process after the baking process occurs, which removes redundant keyframes based on a tolerance amount.

 |
| 

**Tolerance**

 | 

The higher the **Tolerance** value, the more the filtered curve is allowed to deviate from the original, which causes more keyframes to be removed if **Reduce Keys** is enabled.

 |

Click **Create** to bake the animation sequence to Control Rig. Once completed, you should now see a Control Rig track with keyframes along the timeline. These keyframes should correspond to the overall animation that you have baked from.

[![bake animation to control rig](https://dev.epicgames.com/community/api/documentation/image/0312a08d-3a9e-4b77-88f2-b61c7dbdfdb4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0312a08d-3a9e-4b77-88f2-b61c7dbdfdb4?resizing_type=fit)

You can also import an animation sequence directly as Control Rig keyframes by right-clicking on the **Control Rig Section**, then selecting an animation from **Import Anim Sequence Into This Sequence**. The animation will import relative to the Sequencer Playhead.

## Construction Event

[![setup event](https://dev.epicgames.com/community/api/documentation/image/6312736b-b8c3-403b-ac4f-c68c771da452?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6312736b-b8c3-403b-ac4f-c68c771da452?resizing_type=fit)

Similar to Blueprints, you can also create a **Construction Event**, which is used to execute preparation logic, such as initializing variables and setting initial positions on controls. It is executed once, at the post-initialization stage of the Control Rig.

In order to create Construction Event logic in your Rig Graph, you must create a **Construction Event** node. Right-click in the **Control Rig Graph** and select **Events > Construction Event**.

[![create setup event](https://dev.epicgames.com/community/api/documentation/image/3ec6b6cb-33ff-42a6-9a41-7a5569fde740?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3ec6b6cb-33ff-42a6-9a41-7a5569fde740?resizing_type=fit)

From this node, the logic you will be creating will be based on affecting the initial state of your rig elements. This can include things like defining the initial offset of your controls to their respective bones, which enables Rig Sharing. Additionally, you can define initial values for variables, or change the initial positions of bones.

[![setup event logic](https://dev.epicgames.com/community/api/documentation/image/80bf4137-e2ff-4fbd-a58b-d491a1cdcd06?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/80bf4137-e2ff-4fbd-a58b-d491a1cdcd06?resizing_type=fit)

### Spawn Rig Elements

One of the other main purposes of the Construction Event is to spawn rig elements during this initialization phase. This makes it possible to create procedural Control Rigs by spawning new [Controls, Bones, and Nulls](https://dev.epicgames.com/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine), and initialize them using Rig Graph logic.

To create a spawn node, right-click in the Rig Graph and click one of the **Spawn** nodes from the **Dynamic Hierarchy** category. The following nodes can be added:

[![spawn rig elements](https://dev.epicgames.com/community/api/documentation/image/4d0f1bba-98a9-407f-87b2-fe7f787493bf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4d0f1bba-98a9-407f-87b2-fe7f787493bf?resizing_type=fit)

| Name | Description |
| --- | --- |
| 
**Spawn Bone**

 | 

Creates a new [Bone](https://dev.epicgames.com/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine) in the hierarchy.

 |
| 

**Spawn Null**

 | 

Creates a new [Null](https://dev.epicgames.com/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine) in the hierarchy.

 |
| 

**Spawn Animation Channel**

 | 

Creates a new **Animation Channel** in the hierarchy. Animation Channels are a [type](https://dev.epicgames.com/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine) of **Control** that is used to provide an animation channel or custom attribute.

 |
| 

**Spawn Control**

 | 

Creates a new [Control](https://dev.epicgames.com/documentation/en-us/unreal-engine/controls-bones-and-nulls-in-control-rig-in-unreal-engine) in the hierarchy.

 |

When spawning **Animation Channels** or **Controls**, you will need to specify their property type. Do this by right-clicking the **Initial Value** pin and selecting a type from the **Wildcard** dropdown menu.

[![spawn control property type](https://dev.epicgames.com/community/api/documentation/image/060a9fb4-2d06-41b0-bd7f-03e9611209f3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/060a9fb4-2d06-41b0-bd7f-03e9611209f3?resizing_type=fit)

When connecting the Spawn node to the Construction Event, you should see the new element appear in the Hierarchy Panel, as well as in the Viewport as if it were created normally. All spawned element names are colored yellow to distinguish them from non-spawned elements.

[![spawn control hierarchy](https://dev.epicgames.com/community/api/documentation/image/13781c6f-920a-4788-b74c-3528561fc3b8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/13781c6f-920a-4788-b74c-3528561fc3b8?resizing_type=fit)

Spawn nodes currently only function with the Construction Event.

You can also right-click any spawned element and click **Select Spawner Node**, which frames the node used to spawn this element. This makes it easy to locate spawn nodes in a complex graph.

[![select spawner node](https://dev.epicgames.com/community/api/documentation/image/841a76c4-b14c-4365-b993-67e82a608421?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/841a76c4-b14c-4365-b993-67e82a608421?resizing_type=fit)

Unlike non-spawned elements, initial values and settings for spawned elements are read-only, and must be defined on the node, instead of in the Details panel. You can do this by expanding the Initial Value and Settings pins and editing the properties. You can also connect properties and variables to these to drive them from other logic sources.

[![spawn element properties](https://dev.epicgames.com/community/api/documentation/image/025b5ec5-09e8-4d78-b473-b84518436ecf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/025b5ec5-09e8-4d78-b473-b84518436ecf?resizing_type=fit)

There is a limit to the number of spawned elements you can create in a Control Rig, which can be reached if you are creating large rigs or using **For Loop** logic. By default this limit is set to **128**, and can be changed by enabling **Class Settings** and changing the **Procedural Element Limit** property.

[![procedural element limit](https://dev.epicgames.com/community/api/documentation/image/9de43142-83ff-4ede-a650-6a8f42770f64?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9de43142-83ff-4ede-a650-6a8f42770f64?resizing_type=fit)

### Previewing Construction Event

You can preview Construction Event behavior in the [Viewport](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine) by selecting the Solve Direction dropdown menu in the [Toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine), then clicking **Construction Event**. This causes the viewport to execute Construction Event logic from the Rig Graph, rather than Forwards Solve. Entering into this mode is useful for debugging your construction logic.

[![enable setup event](https://dev.epicgames.com/community/api/documentation/image/a2360cd3-dc47-493a-a2a0-e913137540f9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a2360cd3-dc47-493a-a2a0-e913137540f9?resizing_type=fit)

When Construction Event is enabled, you can also edit the initial locations of bones and nulls from the viewport.

[![edit initial rig location](https://dev.epicgames.com/community/api/documentation/image/523bfc18-ed31-4e74-ba02-68e6060e56df?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/523bfc18-ed31-4e74-ba02-68e6060e56df?resizing_type=fit)

When previewing Construction Event, the viewport will be outlined in a **red** border.

## Backwards and Forwards

[![backwards and forwards](https://dev.epicgames.com/community/api/documentation/image/9d99c9bf-4d4e-4b01-baa4-248997b85e4e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9d99c9bf-4d4e-4b01-baa4-248997b85e4e?resizing_type=fit)

The Backwards and Forwards preview mode executes the Backwards Solve, then the Forwards Solve rig logic. This results in behavior that mimics the [Bake Animation to Control Rig](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine) process within the viewport. Typically you will enable this mode if you want to debug the baking process to ensure your bones and controls are operating correctly.

You can preview Backwards and Forwards behavior in the [Viewport](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine) by selecting the Solve Direction dropdown menu in the [Toolbar](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-editor-in-unreal-engine), then clicking **Backwards and Forwards**. This will cause the viewport to execute both the Backwards and Forwards Solve logic sequentially from the Rig Graph.

[![backwards and forwards](https://dev.epicgames.com/community/api/documentation/image/66cd7318-65b9-43df-936e-a3ee72f71a23?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/66cd7318-65b9-43df-936e-a3ee72f71a23?resizing_type=fit)

When previewing Backwards and Forwards, the viewport will be outlined in a **blue** border.