# Transition Rules

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:57

---

## Transition Setup

To control which states can blend to another, you can create **transitions**, which are links between states that define the structure of your State Machine.

![transition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53ca9323-4c54-4442-9333-7635fd18821c/trans1.png)

To create a transition, drag from a state border to another state. In this example the **Idle state** is connected bi-directionally to the **Run state**, which is a common setup for basic locomotion State Machines. Transitions are single-direction, so if two states are intended to transition back and forth, you need to create a transition for each direction.

![create transition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/091220b1-f2be-4e05-a733-d7975d2ece23/trans2.gif)

You can also rebind existing transition logic by selecting a transition node and dragging it to a different state. You can rebind multiple transition nodes at once by dragging the transition arrow to a new binding.

![create transition](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34a2203c-dbe0-443b-96a5-b8895ea34917/trans3.gif)

## Transition Rules

While transitions control the structure of inter-state blending, **transition rules** control when a state can transition. In other words, it is not enough to simply define a transition, you must also define how and when the transition happens.

Transition rules are automatically created when you create a transition. Like states, you can see and access them from either the My Blueprint panel, or by double clicking the **transition icon** in the State Machine graph.

![transitions in my blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1a50865-d9ce-4aee-a9e7-d7d0ff3ff8af/trans3.png)

Within transition rules, you can create any variety of blueprint logic for checking and comparing, all with the purpose of outputting a boolean (true or false) value. A **true** value is used to determine whether the state can transition to the next state.

For example, when transitioning from idle to run, and then back to idle, the logic might look like this. In this example, a bool variable is being used to provide the transition rule. When returning to the default state, the inverse of the bool is used.

![transition rule example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/394c32ef-3d05-449a-a743-c4748617baab/transrule1.png)

Transition rules are typically informed by the movement component and other character variables. To learn more about how to get common properties for a controllable character, refer to the [How to Get Animation Variables](/documentation/en-us/unreal-engine/how-to-get-animation-variables-in-animation-blueprints-in-unreal-engine) page.

Once your variables are correctly set up with the intended logic, meeting the conditions of those variables during gameplay causes the transition to occur.

![transition example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dbbc258c-540a-45fd-9675-fccb70539437/transrule2.gif)

### Transition Functions

Within the transition rule graph, you can use the following specialized transition-only functions to augment your logic:

| Name | Image | Description |
| --- | --- | --- |
| **Current State Time** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc601ac8-8354-4a76-801e-7b11af43b12e/function1.png) | 
Gets the current elapsed time (in seconds) of any currently active state within this State Machine. This output provides information similar to the **activity indicator** in State Machines.

![elapsed function time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db4f5a02-ba7a-45d8-a8e9-b26a6a03386e/function6.png)

 |
| **Get Current State Name** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fca6531b-dffc-4c03-b942-88e27a799dea/function2.png) | Gets the name of the currently active state within this State Machine. |
| **Get Relevant Anim Time** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf40d15e-554f-45ff-80ea-13d98e14d131/function3.png) | 

Gets the current elapsed time (in seconds) of the most relevant animation within the state this transition is going to.

Because states can potentially have multiple animations with equal relevance, you can disable those animations from being checked and used in relevant-related functions. To do this, open the state graph, select the animation nodes you want to exclude (sequence players, blend spaces, aim offsets, or similar), and enable **Ignore for Relevancy Test** from the **Details** panel.

![ignore for relevancy test](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c8f138d-2bf7-4259-8c7b-47aea22ccee0/function7.png)

 |
| **Current Time** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/180345cf-0dc3-4bfd-b021-7a34f3661dda/function5b.png) | Gets the current elapsed time (in seconds) of an animation from the preceding state. This function is useful if you want to reference a specific animation directly, rather than by relevance. |
| **Get Relevant Anim Time Remaining** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df6dc349-da42-4dcf-9d71-a97746bacaf2/function4.png) | Gets the current time remaining (in seconds) of the most relevant animation within the state this transition is going to. |
| **Time Remaining** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2978c472-8d96-46a7-b23c-65776c6c700d/function5.png) | Gets the current time remaining (in seconds) of an animation within the state this transition is going to. This function is useful if you want to reference a specific animation directly, rather than by relevance. |

### Animation Notify Functions

There are also several [Animation Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine) functions that you can use within the transition graph. You can add these functions by right-clicking in the transition graph and locating **Was Anim Notify…** functions.

![notify functions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/926fc44f-5f07-4850-b657-01ca354c6215/notifyfunction1.png)

| Name | Description |
| --- | --- |
| **Was Anim Notify Name Triggered…** | Returns **true** if a [Skeleton Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#skeletonnotify), specified by name, was triggered in the previous tick. |
| **Was Anim Notify State Active…** | Returns **true** if a [Notify State](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#notifystate), specified by class, was active in the previous tick. |
| **Was Anim Notify Triggered…** | Returns **true** if a [Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#notify), specified by class, was active in the previous tick. |

The main differentiators between the notify function checks are if they are searching:

-   **In any state**, which searches for the notify in all active State Machines.
-   **In the source state**, which searches for the notify in the previously active state (the state being transitioned from).
-   **In the State Machine**, which searches for the notify in a specific State Machine.

### Transition Interrupt

While transitioning, if another state becomes active, then the transition will "interrupt" and transition to that new state instead. When this interruption occurs, you can link certain [Animation Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine) to the interruption. This makes those notifies execute when the interruption occurs.

To set up transition interruption notify behavior, select the transition and locate the **Transition Interrupt** properties in the **Details** panel.

![transition interrupt](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/60c20ba3-f172-4ec8-8723-40d917ff588b/interrupt1.png)

You can specify either a **Notify** or **Notify State Class** to link to the interruption. If a **Notify State** is used, then the interruption executes both the **start** and **end** notify events in sequence on subsequent frames.

The other properties can be referenced in the [Montage Notify](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine#montagenotify) page.

## Transition Blend Types

There are three main types of state transition blending you can use when deciding how you want states to transition: **Standard Blend**, **Inertialization**, or **Custom**. You can choose any of these types by selecting the transition and locating the **Blend Logic** property in the **Details** panel.

![transition blend types](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73476ce5-6579-4a89-a702-96896e81ea71/blend1.png)

### Standard Blend

Standard Blend is the default transition option and contains settings for duration, curve, and other basic controls. You can locate and adjust these settings by selecting the transition and locating the **Blend Settings** category in the **Details** panel.

![standard blend](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c1cf7a3a-6cc8-4676-92f4-21cbfbed44e7/blend2.png)

| Name | Description |
| --- | --- |
| **Transition Crossfade Sharing** | You can use this dropdown menu to share **Blend Settings** properties between different transitions. To create a new shared setting, click **Promote to Shared**, type in the name of the setting, and press **Enter**. You can now access this setting on other transitions. The settings are completely shared, so editing settings for one transition affects all others. |
| **Duration** | The length of time, in seconds, that the transition takes. |
| **Mode** | The curve type to use when blending with this transition. Holding **Ctrl + Alt** on each of the options will display a preview of the curve shape. |
| **Custom Blend Curve** | If **Mode** is set to **Custom**, then this is where you specify a custom created Curve Asset to use as the curve shape, when blending with this transition. |
| **Blend Profile** | You can optionally specify a [Blend Profile](/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine#blendprofiles) here, if you want certain bones to blend faster than others during this transition. |

### Inertialization

Rather than simply blending from one state to another, **Inertialization** can be used where the animation velocity and acceleration occurring at the time of the switch to the new animation are used to carry forward the motion. Refer to the [Inertialization](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#inertialization) document for more information.

If you are using inertialization as a blend type, you must also ensure that the **Inertialization node** is used in the Anim Graph. It must be placed after your State Machine evaluates.

![inertialization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5963ac55-65d3-4061-bd52-0a47d413ec73/inertia1.png)

Inertialization does not produce good results on all transitions, depending on the animations used in the states bordering them. Some general rules to keep in mind when using interialization blending are:

-   Keeping your blend duration short, less than 0.4 seconds is best.
-   When the poses are extremely different, do not use inertialization.

### Custom

Custom blends are blends you can graph and customize in their own Anim Graph layer, with its duration and curve shape determined by the [standard blend settings](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine#standardblend).

When **Blend Logic** is set to **Custom**, you can either click **Edit Blend Graph** next to the dropdown menu, or double click the custom blend graph in **My Blueprint** to open the graph.

![custom blend type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e5d8e2f-eb2f-4136-9911-0a266267ecb8/customblend1.png)

Within a custom blend graph, you can use the following special functions to read transition time and state weight information to inform your graph:

| Name | Image | Description |
| --- | --- | --- |
| **State Weight** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e422c44-7cd5-4cc1-bb43-9fd86dada33a/customblend2.png) | Gets the blend weight of the preceding state. This number gradually decreases from **1** to **0** over the transition duration. |
| **Get Transition Time Elapsed** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f11fea71-15ae-4a93-a88c-4908d6ab9265/customblend3.png) | Gets the elapsed time in seconds of a specified transition. |
| **Get Transition Time Elapsed (ratio)** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a88b17d-5027-4fb3-8529-1f4f7e086375/customblend4.png) | Gets the elapsed time as a ratio of the crossfade duration for a specified transition. In other words, this number gradually increases from **0** to **1** over the transition duration. |
| **Get Transition Crossfade Duration** | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1782ba0-cae7-4fd0-a123-541e9fddcfe3/customblend5.png) | Gets the crossfade duration of a specified transition. This is the number used in the **Blend Settings > Duration** property. |

With custom blends, you can create a wide variety of blending logic. As a simple example, you can replicate a [standard blend](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine#standardblend) by using a normal **Blend** node with the **Get Transition Time Elapsed (ratio)** function.

![custom blend example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1fcf606-9200-48cf-86d2-dfa347e840f0/customblend6.png)

## Transition Properties

Transitions contain the following properties:

![transition properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfa3c4d3-a117-4aad-8d00-04542a72a566/properties.png)

| Name | Description |
| --- | --- |
| **Priority Order** | The priority order of this transition. If multiple transitions are true at the same time, the one with the smallest priority is chosen. |
| **Bidirectional** | 
This setting is unsupported and currently does not function.



 |
| **Blend Logic** | What [transition blend type](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine#transitionblendtype) to use. |
| **Transition Rule Sharing** | You can use this dropdown menu to share the **Transition graph** between different transitions. To create a new shared setting, click **Promote to Shared**, type in the name of the setting, and press Enter. You can now access this setting on other transitions. Graphs are completely shared, so editing the graph for one transition affects all others. |
| **Automatic Rule Based on Sequence Player in State** | When enabled, the transition node will try to start the transition automatically based on the most relevant asset player node's remaining time and the **AutomaticRuleTriggerTime** property's value, ignoring internal time. This property can be useful to blend between state transitions more dynamically, by beginning blends sooner, during the first animation's playback. |
| **AutomaticRuleTriggerTime** | Here you can set when to begin the automatic transition rule, when the **Automatic Rule Based on Sequence Player in State** property is also enabled. The value set for this property, in seconds, is relative to the time remaining on the relevant asset player. Values less the `0.0` will use the blend out's cross fade duration to automatically transition the animation out (`AnimiationLength - CrossFadeDuration`). Values greater than or equal to `0.0` will use this value, in seconds, to manually set the time when the transition out is triggered (`AnimationLength - AutomaticRuleTriggerTime`). |
| **Sync Group Name to Require Valid Markers Rule** | If you specify a [Sync Group](/documentation/en-us/unreal-engine/animation-sync-groups-in-unreal-engine) name here, then this transition is only used if the current state contains animations with valid Sync Markers. Normal transition rules still apply. |
| **Transition Crossfade Sharing** | You can use this dropdown menu to share **Blend Settings** properties between different transitions. To create a new shared setting, click **Promote to Shared**, type in the name of the setting, and press **Enter**. You can now access this setting on other transitions. The settings are completely shared, so editing settings for one transition will affect all others. |
| **Duration** | The length of time, in seconds, that the transition takes. |
| **Mode** | The curve type to use when blending with this transition. Holding **Ctrl + Alt** on each of the options will display a preview of the curve shape. |
| **Custom Blend Curve** | If **Mode** is set to **Custom**, then this is where you specify a custom created Curve Asset to use as the curve shape, when blending with this transition. |
| **Blend Profile** | You can optionally specify a [Blend Profile](/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine#blendprofiles) here, if you want certain bones to blend faster than others during this transition. |
| **Transition Interrupt** | Contains settings for [transition interrupts](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine#transitioninterrupt). |
| **Start Transition Event (Custom Blueprint Event)** | Creates a [Skeleton Notify](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine#skeletonnotifies) with the name used in the **Custom Blueprint Event** field. This notify executes when this transition starts. As with normal Skeleton Notifies, you can access the event by creating it in the Animation Blueprint's **Event Graph**. |
| **End Transition Event (Custom Blueprint Event)** | Creates a Skeleton Notify with the name used in the **Custom Blueprint Event** field. This notify executes when the transition ends. |
| **Interrupt Transition Event (Custom Blueprint Event)** | Creates a Skeleton Notify with the name used in the **Custom Blueprint Event** field. This notify will execute when the transition [interrupts](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine#transitioninterrupt). |