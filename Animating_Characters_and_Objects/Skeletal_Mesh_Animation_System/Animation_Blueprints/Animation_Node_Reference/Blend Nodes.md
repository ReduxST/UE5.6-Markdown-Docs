# Blend Nodes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine)  
**Processed:** 2025-06-14 16:06:15

---

In the **AnimGraph** of a character's **Animation Blueprint** you can use **blend nodes** to blend multiple source animation poses together to create new animation poses.

![animation pose blending example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c3841815-bda9-4767-a17a-6c438343944f/blenddemo.gif)

With each blend node you can input multiple animation poses using the node's **pose input pins**, to generate a blended pose that will be accessible from the node's **output pose pin**.

![input and output pin nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c94ab60-8333-460d-9271-f2bf4702d66a/inputandoutput.png)

Some Blend Nodes can accept and blend more than two animation poses, with these nodes you can **right-click** the node in the **AnimGraph** and select **Add Blend Pin** to add another pose input pin.

![add blend pin to blend nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8cad01c1-26bd-4f48-ac7e-b6ecc2c89cf9/addblendpin.png)

You can also remove additional pose input pins by **right-clicking** the specific input pin you want to remove and selecting **Remove Blend Pin** from the context menu.

While using blend nodes, you can control the degree of blending with an **Alpha value**. You can manually assign a blend node's alpha value, by selecting the variable input node, or the alpha property in the node's details panel, and entering a value. You can also assign a blend node's alpha by connecting an alpha variable node to the alpha input pin in the **AnimGraph**. An alpha value of zero will typically favor the primary pose, while a value of 1 will favor the secondary pose.

![alpha pin on blend nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77410535-d3c1-4357-b028-ec123948f04f/alphapin.png)

Using more advanced blend nodes that can incorporate additional animation data, you can create unique animation blending results in your project. Here you will find a reference to the available blend nodes you can use to blend animation poses in **Unreal Engine**.

## Blend Nodes

Categorized with a gray title color, standard blend nodes perform simple blends of animation poses based on node specific parameters. Here you can reference a list of the standard blend nodes that you can use in your project to blend animation poses in the **AnimGraph**

### Apply Additive

Both the **Apply Additive** and the **Apply Mesh Space Additive** nodes add an additive pose to a base-normal animation pose, based on an alpha value.

![apply addivite animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/056be207-7c65-435c-9086-7b47d5bf5bbb/applyadditive.png) ![apply mesh space additive animation blend mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28fd9409-e580-4931-af17-526959899d5c/applymeshspace.png)

Using the nodes input pins, you can connect a **base** pose and an **additive** pose with which to apply.

**Apply Additive** nodes are also affected by the [LOD](/documentation/en-us/unreal-engine/skeletal-mesh-lods-in-unreal-engine) Threshold system. You can adjust the LOD level threshold that the blend occurs in the **Apply Additive** and **Apply Mesh Space Additive**'s **Details** panel.

In addition, you can use a **Make Dynamic Additive** node, to negatively blend additive animation poses. With this node, you can subtract the additive pose from the base pose to create an output pose.

![make dynamic additive animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/765ea187-5f0b-46d5-9c22-9169dfd8e6c3/makedynamic.png)

In the Make Dynamic Additive node's details panel you can also enable the node to operate in the **Mesh Space**.

### Blend

The standard Blend node is a simple combination of the two input poses that scales the weight of which input is prioritized based on an alpha value from the **Alpha** input pin.

![blend animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1965895-716f-4618-96ed-4c35b1994577/blend.png)

You can connect animation poses to the **A** and **B** input pins, and control the degree of blending between the poses with the **Alpha** pin.

### Blend Bone by Channel

With a **Blend Bone by Channel** blend node you can specify individual bones, in which to apply specific blending transforms.

![blend bone by channel animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82644d87-6012-4b05-a83c-f271f7e13941/blendbone.png)

In the Blend Bone by Channel's **Details** panel you can add a **Bone Definitions** section with **(+) Add**. After creating a definition, you can define a source bone to pull transform data from, and a Target bone to apply the blend. You can also define what aspects of the transform you want to incorporate in the blend, such as **Translation**, **Rotation** and **Scale** by toggling the available properties. In addition you can define in what **Transform Space** the transform data is being calculated, such as **World Space**, **Component Space**, **Parent Bone Space** and **Bone Space**.

The present alpha value will facilitate the weight of the blend.

### Blend Multi

With a Blend Multi node, you can blend more than two blend poses, between a range of alpha values.

![blend multi animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7091a90-363d-49ec-ab66-36b731a129e9/blendmulti.png)

In the Blend Multi's **Details** panel you can also toggle the node to behave as additive with the **Additive Node** property.

## Function Blend Nodes

Categorized with a green title color, function blend nodes perform more advanced calculation-based blends of animation poses based on node specific parameters. Here you can reference a list of the function based blend nodes that you can use in your project to blend animation poses in the **AnimGraph**.

### Blend Poses by bool

The **Blend Poses by bool** node performs a time-based blend between two poses using a **Boolean** value as the trigger. When the Boolean reads **true**, the pose connected to the **True Pose** input pin is used; when the Boolean is **false**, the **False Pose** is used. Each pose has a float value **Blend Time** that is used to control how long it will take to blend into the pose.

![blend poses by bool animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82a7200a-38d7-4465-80af-bf29367d43fb/blendposesbool.png)

In the **Details** panel, you can toggle the **Blend Time** pins to be visible in the AnimGraph as well as set the [Transition Type](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine).

### Blend Poses by int

The **Blend Poses by int** node performs a time-based blend between any number of poses using an integer value as the key. For each input integer value, the pose associated with that value's input pin is used. For instance, when the integer is set to 0, the pose connected to **Blend Pose 0** is used. Each pose has a float value **Blend Time** that is used to control how long it will take to blend into the pose.

![blend poses by int integer animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53cf67f4-e3ab-4449-b8cb-9bfbe5cb3bc0/blendposesint.png)

In the **Details** panel, you can toggle the **Blend Time** pins to be visible in the AnimGraph as well as set the [Transition Type](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine).

### Blend Poses by Enumeration (Enum)

The **Blend Poses by Enum** node performs a time-based blend between poses using an **Enumeration** (**Enum**) value as the key. A default pose can be used, and additional poses can be added for the values identified within the enum connected through the **Active Enum Value** pin. Additionally, each pose has a float value **Blend Time** that is used to control how long it will take to blend into the pose.

![blend poses by enum enumeration animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6501cfa5-9a31-47ae-90b8-df5c78ad95e7/enum.png)

In the **Details** panel, you can toggle the **Blend Time** pins to be visible in the AnimGraph as well as set the [Transition Type](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine).

### Layered blend per bone

With the **Layered blend per bone** node you can blend between any number of dynamic blend poses based on a defined set of bones.

![layered blend per bone animation blend node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17ec8638-9c3d-4134-a08c-0a2cd1e10b39/layeredblendperbone.png)

In the **Details** panel of the Layered blend per bone node, you can define the blend mode as either a **Branch Filter** or a **Blend Mask**.

![blend mode in layered blend per bone animation blend node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a78fa39-747b-4593-9d1e-9bb2399de1ba/blendmode.png)

You can enable the **Mesh Space Rotation Blend** and **Mesh Space Scale Blend** properties to control whether the **Rotation** and **Scale** blending occurs in the **Mesh Space** or **Local Space**.

With the **Curve Blend Options** property you can set the curve blend behaviors from a set list to control how the animation layers blend together. Here you can reference a list of the available **Curve Blend Options**.

![curve blend option in layered blend per bone animation blend node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8a04c37-8945-4b20-a5a0-8af1fa8046e0/curveblendoption.png)

| Blend Option | Description |
| --- | --- |
| **Override** | Overrides the pose to the last pose that contains a valid curve value. |
| **Do Not Override** | Does not override the pose. Best used when the desired previous pose doesn't have a curve value. |
| **Normalize by Weight** | Normalizes the pose blend by the **sum** of all blend weights. |
| **Blend by Weight** | Blends the poses by blend weight **without** normalizing. |
| **Use Base Pose** | Uses the **Base Pose** for all curve values. |
| **Use Min Value** | Selects the **highest** curve value from all connected poses and uses it to blend. |
| **Use Max Value** | Selects the **lowest** curve value from all connected poses and uses it to blend. |

You can also enable the **Blend Root Motion Based on Root Bone** property to incorporate the per-bond blend weight of the **root bone** when lending [Root Motion](/documentation/en-us/unreal-engine/root-motion-in-unreal-engine).

#### Branch Filter

With the **Branch Filter** option, you can define an **Index** of bones the blend will affect.

![layer setup indexes in layered blend per bone animation blend node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7445fb2e-8fc1-4aa3-a387-a1c03075a735/indexes.png)

After adding an element to the **Branch Filters** property, you can input a bone as the **Bone Name** to use as a reference point to control localized animation blending. Using the **Blend Depth** property, you can control the wight the blend has on the children bones of the **Bone Name**.

| Value | Example | Description |
| --- | --- | --- |
| **Positive** | ![postive blend depth value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29ed16c6-f0ed-4599-ab53-f69e32aa4acf/positive.gif) | Positive **Blend Depth** values will offset the weight by the same number of bones and taper the weight through the chain to the **Bone Name**. For example, a **Blend Depth** of 2 will apply a blend weight of 1 to the next child bone and a blend weight of .5 to the **Bone Name**. |
| **Zero** | ![zero blend depth value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3168f1df-e20c-49d8-b14d-5269eca3ac72/zero.gif) | A **Blend Depth** of 0 will apply a blend weight of 1 to the **Bone Name** and all connected child bones. |
| **Negative** | ![zero blend depth value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7195616c-e2ea-4c97-a40c-aebc943bf292/negative.gif) | Negative **Blend Depth** values will disable any **Blend Poses** and favor the **Base Pose**. Lesser values than -1 will offset the weight by the same number of bones and taper the disabled blend weight through the chain to the **Bone Name**. For example, a **Blend Depth** of -2 will apply a blend weight of -1 to the next child bone and a blend weight of -.5 to the **Bone Name**. |

#### Blend Mask

With the **Blend Mask** option, you can define the character's [Blend Masks](/documentation/en-us/unreal-engine/blend-masks-and-blend-profiles-in-unreal-engine) as reference points to control the blending between the **Base Pose** and the **Blend Poses**.

![blend masks in layered blend per bone animation blend node details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4be10b78-709c-433b-81c7-bc922c8d4bf2/blendmask.png)

## Inertialization

**Inertial blending** is a high-performance alternative to traditional animation crossfading that produces natural transitions as a post-process. Once an inertial blend is activated, the source pose is no longer evaluated at all. By contrast, traditional blending evaluates both source and target poses for the duration of the transition to combine them into a blended pose.

![inertialization example animations](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16cfb6a4-c347-418c-bb23-3e2b4f5ca33a/inertb.gif)

To use inertial blending, you can add an **Inertialization** or **Dead Blending** node to the **AnimGraph** after the source animation blend you want inertially blended. Each node approaches inertial blending using different methods.

![inertialization nodes animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b9d99e4-af51-49fe-abf8-2cfa8fc00501/inertialnodes.png)

Both the Inertialization and Dead Blending node tracks the animation pose motion and changes within **Animation Curves**, so that the motion can continue moving toward the target animation when an inertial blend is activated. These nodes are activated by any **inertial blend requests** connected to its **Source** input pose pin. [State Machine Transitions](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#requestfromstatemachinetransitions), [Blend Nodes](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#requestfromblendnodes), [Linked Anim Graphs and Linked Anim Layers](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#requestfromlinkedandlayeredanimgraphs), can all trigger inertial blends. The Inertialization or Dead Blending node must be connected after the source of the inertial blend request, but does not have to be immediately adjacent. Deferring an Inertialization or Dead Blending node closer to the **Output Pose** node can help reduce or eliminate standard blends from your graph and improve your animation system's performance. A single Inertialization or Dead Blending node can handle many inertial blend requests. When processing multiple inertial blend requests, the **minimum requested blend duration** will be used.

![Inertialization overview example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/664b0c21-c770-469e-921a-e794faf1be0a/inertializationoverview.png)

If your AnimGraph contains a Inertialization request but is missing an Inertialization or Dead Blending node, a runtime error will be logged in the **Message Log** panel.

When authoring animations and graphs with inertial blending in mind, it's best to begin transitions while the outgoing animation is still in motion. There is no need to return to a neutral pose, as inertial blending will handle smooth and natural easing to a rest position. Short blends work best since inertial blending is a **post-process** for easing motion toward a target animation. Inertial blends can be interrupted with other inertial blends, but try to avoid scenarios that could cause continuous interruptions because animation quality can degrade.

#### Using Multiple Inertial Blends

You can place multiple Inertialization or Dead Blending nodes in your graph as needed, and each will handle inertial blend requests from their source pose. This means you can perform inertial blending in different spaces. For example, you may want to create separate Inertialization or Dead Blending nodes that operate on your character's upper and lower body separately, followed by a **Layered Blend per bone** node to blend them together into a final pose.

#### Additive Inertial Blending

You can also use inertial blending with additive poses by inserting an Inertialization or Dead Blending node before applying to the base pose. For final pose fixups, you will generally apply an inertial blend before any IK, which effectively does inertial blending in IK space.

A Source pose stops being evaluated once inertial blending begins. As a result, [Animation Notifies](/documentation/en-us/unreal-engine/animation-notifies-in-unreal-engine) from the source animation [Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) will no longer trigger after inertial blending begins. You may need to refactor existing game logic and Anim Notifies to be compatible with Inertialization.

### Inertialization Node vs Dead Blending

There are two kinds of inertial blend nodes available in Unreal Engine; the Inertialization node and the Dead Blending node.

| Inertialization Node | Dead Blending Node |
| --- | --- |
| ![inertilization animation blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd81dcdc-4b63-4b02-85de-6f0790533422/inertialization.png) | ![dead blending aniamtion blueprint node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3f935d4d-20fe-4aa1-881e-9002d31efeb7/deadblendnode.png) |
| The Inertialization node records the offset between the incoming and outgoing animations and fades this out to prevent the pose from popping. | 
The Dead Blending node tries to predict future poses of the outgoing animation and blends these with the incoming animation.

This node is an experimental node, and therefore we do not recommend shipping projects that rely on its functionality.



 |

In general the Dead Blending node tends to perform better, in particular when transitioning between animations with large pose differences, but it can sometimes produce more stiff movements. It also takes into account transition blend curves, which are ignored by the Inertialization node.

#### Initialization Node Reference

Here you can reference a list of the Inertializtion nodes properties and a description of their function.

![inertilization node settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8bd9886-f790-4236-92d8-0518d844122b/inertializationsettings.png)

| Property | Description |
| --- | --- |
| **Blend Profile** | Optionally set a default Blend Profile to use when no blend profile is supplied by the source node with the inertial blend request. You can set a Blend Profile using the drop-down menu. |
| **Filtered Curves** | Set a list of animation curves that should not use inertial blending. These curves will instantly change when inertial blending. To filter a curve, use (**+**) to add a new array to the property, then set the curve by typing the curve's name in the provided **Index** field. |

#### Dead Blend Node Reference

Here you can reference a list of the Dead Blend nodes properties and a description of their function.

This node is an experimental node, and therefore we do not recommend shipping projects that rely on its functionality.

![dead blending node settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/751d7157-5ff8-46c1-8c0f-00dcd04eba68/deadblendingsettings.png)

| Property | Description |
| --- | --- |
| **Always Use Default Blend Settings** | When enabled, the default blend settings will be used rather than those coming from the source node providing the inertial blend request. |
| **Default Blend Duration** | Set a default blend duration to use when the source node providing the inertial blend request does not specify a blend duration, or when the **Always Use Default Blend Settings** property is enabled. |
| **Default Blend Profile** | Set a default blend profile to use when the source node providing the inertial blend request does not specify a blend profile, or when the **Always Use Default Blend Settings** property is enabled. You can set a blend profile using the drop-down menu. |
| **Mode** | Set the default blend mode to use when the source node providing the inertial blend request does not specify a blend mode, or when the **Always Use Default Blend Settings** property is enabled. You can set a blend mode using the drop-down menu and selecting one of the provided curves. |
| **Default Custom Blend Curve** | Optionally set a default blend curve to use in conjunction with the blend mode when the source node providing the inertial blend request does not specify a blend curve, or when the **Always Use Default Blend Settings** property is enabled. You can set a blend curve using the drop-down menu and selecting a curve asset from your project. |
| **Blend Time Multiplier** | Set a blend time multiplier that can be used to scale the overall lend durations coming from the inertial blend request. |
| **Linearly Interpolate Scales** | When enabled, bone scales will be linearly interpolated. This is slightly more performant and consistent with the rest of Unreal Engine but visually gives the appearance of the rate of change of scale being affected by the overall size of the bone. |
| **Filtered Curves** | Set a list of animation curves that should not use inertial blending. These curves will instantly change when inertial blending. To filter a curve, use (**+**) to add a new array to the property, then set the curve by typing the curve's name in the provided **Index** field. |
| **Filtered Bones** | Set a list of bones from the character's Skeleton that should not use inertial blending. The motion from these bones will instantly change when inertial blending. To filter a bone, use (**+**) to add a new array to the property, then select the bone from the Skeleton hierarchy using the drop-down menu in the provided **Index** field. |
| **Extrapolation Half Life** | Set the average half-life of decay in seconds to use when extrapolating the animation. To get the final half-life of decay this value will be scaled by the amount to which the velocities of the animation being transitioned from are moving toward the animation being transitioned too. |
| **Minimum Extrapolation Half Life** | Set the minimum half-life of decay in second to use when extrapolating the animation. This will be used when the velocities of the animation being transitioned from are very small or moving away from the animation being transitioned too. |
| **Maximum Extrapolation Half Life** | Set the maximum `half_life` of decay in seconds to use when extrapolating the animation. This will dictate the longest decay duration possible when velocities of the animation being transitioned from are small and moving towards the animation being transitioned too. |
| **Maximum Translation Velocity** | Set the maximum velocity to allow for extrapolation of bone translations, in centimeters per-second. Smaller values may help prevent the pose from breaking during blending but too small values can make the blend less smooth. The default value is `500.0`. |
| **Maximum Rotation Velocity** | Set the maximum velocity to allow for extrapolation of bone rotations in degrees per second. Smaller values may help prevent the pose from breaking during blending but too small values can make the blend less smooth. The default value is `360.0`. |
| **Maximum Scale Velocity** | Set the maximum velocity to allow for extrapolation of bone scales. Smaller values may help prevent the pose from breaking during blending but too small values can make the blend less smooth. The default value is `4.0`. |
| **Maximum Curve Velocity** | Set the maximum velocity to allow for extrapolation of curves. Smaller values may help prevent extreme curve values during blending but too small values can make the blending of curves less smooth. The default value is `100.0`. |
| **Preallocate Memory** | When enabled the Dead Blending node will pre-allocate memory, rather than allocate and deallocate memory when blending becomes active and inactive. This property can improve performance, but causes larger memory usage, in particular when you have multiple Dead Blending nodes in an Animation Graph that are not all used at once. |
| **Show Extrapolations** | When enabled, the Dead Blending node will output a pose that matches the extrapolation. A debug drawing will be rendered that shows what the extrapolation of the animation being generated looks like. |

### Request from Blend Nodes

In the **Details** panel of any inertialization compatible node, you can set the **Transition Type** property to **Inertialization**, to activate an inertial blend request. To use inertial blending, the Inertialization node must be placed in the animation graph anywhere after the blend node making the inertial blend request.

![inertial blend request from blend node transition type](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/00bffebb-f7c5-40aa-b045-43259e3d661c/transitiontype.png)

### Request from State Machine Transitions

A Inertial Blend request can be made by a [State Machine](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine)'s transition logic. In the **Details** panel of a [Transition Rule](/documentation/en-us/unreal-engine/transition-rules-in-unreal-engine), you can set the **Blend Logic** property to **Inertialization**, to activate an inertial blend request.

![inertial blend request from state machine transition rule](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4170412-42a7-4bca-8f85-7e947c39c566/statemachine.png)

### Request from Linked and Layered AnimGraphs

Inertialization properties can also be defined in an [Animation Layers](/documentation/en-us/unreal-engine/editing-animation-layers) or from a [Linked Anim Graph](/documentation/en-us/unreal-engine/animation-blueprint-linking-in-unreal-engine). After selecting a Graph from the **My Blueprints** panel you can find the **Graph Blending** section of properties in the **Details** panel. An Animation Layer can blend **in** or **out**, but only via **inertial blending**. An **Inertialization** or **Dead Blending** node must be placed anywhere after the **Linked Anim Layer** node that links this Animation Blueprint. A negative value means the blend time will be determined by the other incoming or outgoing Animation Layer.

![inertial blend request from anim layer blend linked anim graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78caa876-d4d8-44f8-91a7-13adf0c5e2a2/animlayerblend.png)