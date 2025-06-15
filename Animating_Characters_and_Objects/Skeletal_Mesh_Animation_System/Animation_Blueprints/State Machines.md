# State Machines

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/state-machines-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/state-machines-in-unreal-engine)  
**Processed:** 2025-06-14 16:52:06

---

**State Machines** are modular systems you can build in **Animation Blueprints** in order to define certain animations that can play, and when they are allowed to play. Primarily, this type of system is used to correlate animations to movement states on your characters, such as idling, walking, running, and jumping. With State Machines, you will be able to create **states**, define animations to play in those states, and create various types of **transitions** to control when to switch to other states. This makes it easier to create complex animation blending without having to use an overly complicated Anim Graph.

This document provides an overview of how to create and use State Machines, states, and transitions in Animation Blueprints.

#### Prerequisites

-   State Machines are created within [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine), therefore you should have an understanding of how to use Animation Blueprints and their [interface](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine).
-   Your project contains a character with a movement component so that you can build states that react to input. The [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) can be used if you do not have one.

## Creation and Setup

State Machines are created within the [Anim Graph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#animgraph). To create one, right-click in the **Anim Graph** and select **State Machines > Add New State Machine.** Connect it to the **Output Pose**.

![add new state machine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ddbd59bf-8e71-405b-8b5d-a7bbc3284178/create1.png)

State Machines are subgraphs within the Anim Graph, therefore you can see the State Machine graph within the **My Blueprint** panel. Double-click it to open the State Machine.

![new state machine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9236cc22-6ff0-44af-9ab6-7b942c63a7a7/create2.png)

You can also double-click the State Machine node in the Anim Graph to open it.

### Entry Point

All State Machines begin with an **entry** point, which is typically used to define the **default state**. In most common locomotion setups, this would be the character idle state.

To create the default state, click and drag the **entry** output pin and release the mouse, which will expose the context menu. Select **Add State**. This will create the new state and connect it to the entry output, making this state active by default.

![state entry point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6941aa29-6a13-492e-91c9-5fe1f4fea3aa/create3.png)

## States

States are organized sub-sections within a State Machine that can transition to and from each other regularly. States themselves contain their own Anim Graph layer, and can contain any kind of animation logic. For example, an idle state may just contain a character's idle animation, whereas a weapon state may contain additional logic for shooting and aiming. Whatever logic is used, the purpose of a state is to produce a final animation or pose unique to that state.

### Creating States

States can be created in the following ways:

-   Right-click in the State Machine graph and select **Add State**.
    
    ![add state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/806171ce-c486-4230-aea9-7e922030e4e1/state1.png)
    
-   Click and drag off of the border of a state (or entry output), then release the mouse and select **Add State**. This will also connect it to the previous state with a [transition](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine#transitions).
    
    ![drag add state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85ec3324-7fcd-4767-8d6a-e075928e5301/state2.png)
    
-   Drag an **Animation Asset** into the State Machine graph from the **Content Browser** or **Asset Browser**. This also adds the animation to the state and connects it to its **Output Pose**.
    
    ![drag and drop add state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b0d40ed6-a6e0-4856-8c3e-c62e2bf52ad7/state3.png)
    

State Machines can have as many states as needed, and they also display as subgraphs under the State Machine.

![states in my blueprint panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb6652e2-96d2-43ea-b06b-16e4fdedcb77/state4.png)

### Editing States

To view the internal operation of a state, you can either double-click it in the **My Blueprint** panel, or double-click the node itself in the **State Machine** graph. This will open the state.

![open state](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b86d6fed-a785-4aa8-af6e-1267fa7e7c92/stateedit1.png)

Like Anim Graphs, states contain a final **Output Pose** node to connect your animation logic to. When the state is active, this logic will execute. When a different state is active, this logic will no longer execute. In this idle state example, an idle animation is connected to the Output Pose. When this state is active, this resulting animation will play.

![state preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7937ce53-3aed-49c9-942a-b0cc8be0ac8e/stateedit2.gif)

### State Properties

When a state is selected, you can view and edit the following properties in the **Details** panel.

![state properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3226347-5e4b-404d-9fc9-ad9cb3bee844/state5.png)

| Name | Description |
| --- | --- |
| **Name** | The name of the selected state. |
| **Entered State Event (Custom Blueprint Event)** | 
Creates a [Skeleton Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#skeletonnotify) with the name used in the **Custom Blueprint Event** field. This notify will execute when the state becomes active and starts to transition. As with normal Skeleton Notifies, you can access the event by creating it in the Animation Blueprint's **Event Graph**.

![entered state custom blueprint event](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89f3b6ab-3a06-4bce-9106-986beaed14ad/state6.png)

 |
| **Left State Event (Custom Blueprint Event)** | Creates a Skeleton Notify with the name used in the **Custom Blueprint Event field**. This notify will execute when starting to blend to another state. |
| **Fully Blended State Event (Custom Blueprint Event)** | Creates a Skeleton Notify with the name used in the **Custom Blueprint Event field**. This notify will execute when this state is fully blended to. |
| **Always Reset on Entry** | 

**Enabling** this will cause all animations within this state to re-initialize to their default values. In most cases, this means the following:

-   Sequence players will restart at the animation start time.
-   Properties will initialize at their default values.

If **disabled**, then all animations and their properties will maintain their previous playback state and other properties upon leaving and then returning to this state. In other words, the animations will "pick up where they left off".



 |

## Transitions

To control which states can blend to another, you can create **transitions**, which are links between states that define the structure of your State Machine.

![transition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53ca9323-4c54-4442-9333-7635fd18821c/trans1.png)

To create a transition, drag from a state border to another state. In this example the **Idle state** is connected bi-directionally to the **Run state**, which is a common setup for basic locomotion State Machines. Transitions are single-direction, so if two states are intended to transition back and forth, you need to create a transition for each direction.

![create transition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/091220b1-f2be-4e05-a733-d7975d2ece23/trans2.gif)

You can also rebind existing transition logic by selecting a transition node and dragging it to a different state. You can rebind multiple transition nodes at once by dragging the transition arrow to a new binding.

![create transition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34a2203c-dbe0-443b-96a5-b8895ea34917/trans3.gif)

To learn more about **transitions** and **transition rules**, refer to the [Transitions](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine) page.

## Conduits

While ordinary transitions can be used for 1-to-1 transitions between states, **conduits** can be used to create 1-to-many, many-to-1, or many-to-many transitions. Because of this, conduits serve as a more advanced and shareable transition resource.

To create a conduit, right-click in the State Machine graph and select **Add Conduit**.

![add conduit](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd62a748-00ab-4879-aec5-84cf54454265/conduit1.png)

There are several ways you can use conduits. One example might be to use them to diverge your State Machine's entry point. You can then use transitions from the conduit to select which state should start as the default. This example can be useful when re-initializing a State Machine if you were overwriting it with another animation, such as an [Animation Montage](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine).

![conduit connections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42b3d2a3-36e1-42b5-91f3-e15c81ed746a/conduit2.png)

The above example requires **Allow Conduit Entry States** to be enabled in the [State Machine Details panel](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine#statemachineproperties).

Conduits contain their own [transition rules](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine#transitionrules), which can be located by double-clicking on the conduit node, or by opening the conduit graph from the My Blueprint panel. By default, conduit transitions rules will return false. In most cases you may just want to enable **Can Enter Transition**, and create transition rule logic on the individual transitions in and out of the conduit.

![allow conduit passthrough](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95150b41-9e7b-4dd4-8c1b-27c1ac6a17b4/conduit3.png)

Refer to the [Transition Rules](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine) page for more information on transitions and transition rules.

## State Alias

As you build more complicated State Machines with many states and ways to transition between them, you may want to use **state aliases** to improve your graph. State aliases are shortcut-type nodes you can add to your State Machine to reduce line clutter, consolidate transitions, and improve the readability of your graph.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d1a4ab6-6b6e-4024-aef2-d3c5e666eb5c/alias_off.png) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85c570f0-ce51-469d-b80c-90bcfc226378/alias_on.png) |
| State Machine with no alias usage | State Machine using aliases |

To create a state alias, right-click in the **State Machine** graph and select **Add State Alias**.

![add state alias](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8038c620-018b-486e-a104-c7e14042b007/alias1.png)

State aliases work by defining which states can transition into it, then connecting the alias to other states using the normal transition method. Click the state alias node, and in the **Details** panel you can observe the following:

-   Each state within your State Machine is listed as a property. If you enable that state, it causes that state to adopt the transitions and rules that you make from the alias to other states. In other words, this is where you define which states are "coming into" the alias.
-   Enabling **Global Alias** makes all states come into the alias. Although you can enable all listed states which causes the same behavior, enabling Global Alias will also include any new states created later.
    
    Global Alias is best used in a limited way with single-frame input and finite-duration states, such as interaction, attacks, or other similar animations. Using Global Alias for states with indefinite lengths may require additional complicated logic between all other state transitions to ensure your other states are not always transitioning to it.
    

![alias properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2d17cc99-9029-43ed-a3b2-3a74aee78384/alias2.png)

### Alias Example

In this example, a somewhat simple State Machine requires the **land** and **locomotion** states to transition to both the **jump** and **fall loop** states. Four transitions in total are being used, each with their own transition rules.

![before alias example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/066a8acd-a515-48ee-a4c3-099441363bf9/alias3.png)

State aliases can be used to clean up this graph. To achieve the same effect, you can do the following:

-   Create a state alias and transition it to both the **fall loop** and **jump** states.
-   Select the state alias and enable **locomotion** and **land**.

![after alias example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/125ae541-1887-4c94-a5e8-20cb8a16fbaf/alias4.png)

Because state aliases consolidate transitions from all enabled states, using state aliases means that these states share the same transition rules and properties. If you want certain transitions to have different rules, blend durations, or other properties, then you should create unique transitions for those states instead.

## State Machine Properties

State Machines contain the following properties in the **Details** panel.

![state machine properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7850809d-fc86-46c0-a6e3-ac2dbe547450/properties.png)

| Name | Description |
| --- | --- |
| **Name** | The name of the selected State Machine. |
| **Max Transitions Per Frame** | This number defines how many transitions or **decisions** can occur in a single frame or tick. If your state machine has many states and transitions where more than one transition can be true at a given time, you may want to set this number to **1**. This makes it so that only one decision can be made at a time, preventing competing decisions and transitions. |
| **Skip First Update Transition** | 
When a State Machine becomes [relevant](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine#nodefunctions), it initializes into the default state connected to the **Entry** point. At that point, normal State Machine processes begin and any valid transitions are taken.

-   If this property is enabled, then any non-default states that are valid transition targets upon initialization will be immediately transitioned to.
-   If disabled, then any valid transition targets will blend normally.

This is to allow for any non-default states to behave as if they were the default state, if that is desired behavior. For example, if you have a simple idle and run State Machine, where **idle** is the default state and can transition to **run**. If **Skip First Update Transition** is enabled, and if the run transition rule is **true** at the time of the State Machine's initialization, then run will be initialized and blended to 100% immediately.



 |
| **Reinitialize on Becoming Relevant** | Enabling this reinitializes the first entered state when the State Machine becomes relevant. This setting operates similarly to the per-state property **Always Reset on Entry**, but only resets the first initialized state entered. |
| **Create Notify Meta Data** | When using [Animation Notify Functions](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#animationnotifyfunctions) in your transition rules, enabling this allows for all relevant data to be sent to these notify functions. If this is disabled, then none of the notify functions will work. |
| **Allow Conduit Entry States** | Enabling this allows [conduits](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine#conduits) to be used as entry states, allowing for variable default states depending on the conduit's transition rules. |