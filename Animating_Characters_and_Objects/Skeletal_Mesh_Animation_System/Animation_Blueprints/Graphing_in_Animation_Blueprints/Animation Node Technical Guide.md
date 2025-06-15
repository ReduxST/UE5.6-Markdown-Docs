# Animation Node Technical Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-node-technical-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-node-technical-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:21

---

**Animation nodes** are used inside of [Anim Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) to perform operations, such as working with [Animation Assets](/documentation/en-us/unreal-engine/animation-assets-and-features-in-unreal-engine), blending [Animation Poses](/documentation/en-us/unreal-engine/animation-pose-assets-in-unreal-engine), and manipulating a Skeletal Mesh's [bones](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine). A suite of animation nodes are included in **Unreal Engine**, but you can also create custom nodes to fit the needs of your project.

![example animation blueprint nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d43d7452-a9a7-4c02-921a-91794ec347ac/animnodeoverview.png)

To open an Animation Blueprint in your project's [source code editing IDE](/documentation/en-us/unreal-engine/setting-up-your-development-environment-for-cplusplus-in-unreal-engine), open the AnimBP in the [AnimBP Eitor](/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine), and click the **Parent Class** link in the top-left of the editor window.

![open an animation blueprint in your project's source code ide with the parent class instance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4002d7a-9a88-4e6b-8a3e-1a03dd68e38b/opennodeincode.png)

## Anatomy of an Animation Node

The two essential components of any Animation nodes are:

-   A [runtime struct](/documentation/en-us/unreal-engine/animation-node-technical-guide-in-unreal-engine#runtimenodecomponent) that performs the actual operations to generate an output pose.
-   An [editor-time container class](/documentation/en-us/unreal-engine/animation-node-technical-guide-in-unreal-engine#editornodecomponent) that handles visual aspects and functionality of the node within the graph, such as node titles and the context menu.

In order to add a new animation node, both of these must be created.

### Node Hierarchies

It is possible to create a hierarchy of nodes, but any non-abstract editor-time classes should contain exactly one runtime node.

Do not add additional nodes when deriving unless the parent was abstract and did not contain one.

See the `UAnimGraphNode_BlendListBase` node family for examples.

![example blend list base animation blueprint nodes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0964fb77-93e4-4e73-83b7-09cc70694550/blendlistbase.png)

## Runtime Node Component

The **runtime struct** is derived from `FAnimNode_Base` and is responsible for initialization, updating, and performing operations on one or more input poses to generate the desired output pose. It also declares any input pose links and any properties needed by the node to perform the desired operation.

### Pose Inputs

In the runtime node, pose inputs are exposed by creating properties of the type `FPoseLink` or `FComponentSpacePoseLink`. `FPoseLink` is used when working with poses in local space, such as blending animations. `FComponentSpacePoseLink` is used when working with poses in component space, such as applying skeletal controllers.

An Anim BP node can have a single pose input. The following are examples of animation nodes using a single pose input.

| **Node Classification** | **Code Example** | **Image** |
| --- | --- | --- |
| **Local Space** | 
**Local Space** pose input code implementation:

```
			`UPROPERTY(Category=Links) 			FPoseLink BasePose;`
Copy full snippet
```
UPROPERTY(Category=Links) FPoseLink BasePose;

 | ![Pose Input Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55622886-dceb-41ab-97f5-572593bb94e8/node_rotate_root_bone-base_pose_callout.png) |
| **Component Space** | 

**Component Space** pose input code implementation:

```
			`UPROPERTY(Category=Links) 			FComponentSpacePoseLink ComponentPose;`
Copy full snippet
```
UPROPERTY(Category=Links) FComponentSpacePoseLink ComponentPose;

 | 

![Pose Input Pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f867c1c2-ce44-4d8e-8b1b-d71a62ccc578/node_spring_controller-component_pose_callout.png)

Component Space pose input pins are blue.



 |

An Anim BP node can also have more than one pose input pin for nodes that blend between multiple animations:

| **Node Classification** | **Code Example** | **Image** |
| --- | --- | --- |
| **Blending Node** | 
**Base pose** and **Additive pose** input pin code implementation:

```
			`UPROPERTY(Category=Links) 			FPoseLink Base;  			UPROPERTY(Category=Links) 			FPoseLink Additive;`
Copy full snippet
```
UPROPERTY(Category=Links) FPoseLink Base; UPROPERTY(Category=Links) FPoseLink Additive;

 | ![Pose Input Pins](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e50574dc-8b29-4ee8-906e-c2981305bbd0/node_apply_additive_default-base_additive_callout.png) |

Once implemented into your custom Anim BP node, each of these properties will display a pose link input pin.

Properties of this type are always exposed as input pins. They cannot be optionally hidden or used only as editable properties in the **Details** panel.

### Properties and Data Inputs

You can assign any number of properties to an AnimBP that are used to perform the operations of the node. Similar to other properties, you can declare custom properties using the `UPROPERTY` macro.

| **Node Clasifcation** | **Code Example** | **Image** |
| --- | --- | --- |
| **Alpha Property Implementation** | 
**Alpha property** pin code implementation:

```
	`UPROPERTY(Category=Settings, meta(PinShownByDefault)) 	mutable float Alpha;`
Copy full snippet
```
UPROPERTY(Category=Settings, meta(PinShownByDefault)) mutable float Alpha;

 | ![Property Pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f885fbb-9af8-41ac-8f47-071bda287838/node_apply_additive_default-alpha_callout.png) |

Using special **metadata keys**, animation node properties can be exposed as **data inputs pins** to allow values to be passed to the node. The following are metadata keys you can use when create custom AnimBP nodes for your project.

| Metadata Key | Description |
| --- | --- |
| `NeverAsPin` | This key will hide property as a data pin in the AnimGraph and will only be editable in the node's **Details** panel. |
| `PinHiddenByDefault` | You can use this key to hide the property as a pin, by default. The property can then be exposed as a data pin in the AnimGraph. See the [Optional Pins](/documentation/en-us/unreal-engine/animation-node-technical-guide-in-unreal-engine#optionalpins) section for more information about exposing hidden pins in the AnimGraph. |
| `PinShownByDefault` | With this key you can expose a property as a data pin in the AnimGraph by default. |
| `AlwaysAsPin` | This key will always expose the property as a data point in the AnimGraph. |

### Optional Pins

For properties that are hidden, but exposable in the AnimGraph, using keys like `PinHiddenByDefault` or `PinShownByDefault`, you can expose properties in the node's **Details** panel, by navigating to the property and toggling **Expose As Pin** from the dropdown menu.

![Property Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16ca4739-92d4-45e8-a9ca-a165c1cd6c7c/node_options-alpha_pin_callout.png)

You can also hide property pins from the AnimGraph by **right-clicking** the pin you want to hide, navigating to the **Binding** option and toggling **Expose As Pin** from the dropdown menu.

![Property Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63dedcba-e729-4be6-b8fd-089c374930b1/node_options-alpha_pin_calloutb.png)

## Editor Node Component

The editor class is derived from `UAnimGraphNode_Base` and is responsible for visual elements like the node's title or adding context menu actions.

The editor-time class should contain an instance of your runtime node exposed as editable.

```
	`UPROPERTY(Category=Settings) 	FAnimNode_ApplyAdditive Node;`

Copy full snippet
```
UPROPERTY(Category=Settings) FAnimNode\_ApplyAdditive Node;

### Title

![Node Title](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54f45c49-8191-4951-891e-7d51a8ed082d/node_apply_additive_default-title_callout.png)

You can override the appearance of an Animation node's title elements in the AnimGraph, such as the text and background color, using the `GetNodeTitle` and `GetNodeTitleColor` functions.

For example, the `UAnimGraphNode_ApplyAdditive` node uses a gray background and displays "Apply Additive":

```
	`FLinearColor UAnimGraphNode_ApplyAdditive::GetNodeTitleColor() const 	{ 		return FLinearColor(0.75f, 0.75f, 0.75f); 	}  	FString UAnimGraphNode_ApplyAdditive::GetNodeTitle(ENodeTitleType::Type TitleType) const 	{ 		return TEXT("Apply Additive"); 	}`

Copy full snippet
```
FLinearColor UAnimGraphNode\_ApplyAdditive::GetNodeTitleColor() const { return FLinearColor(0.75f, 0.75f, 0.75f); } FString UAnimGraphNode\_ApplyAdditive::GetNodeTitle(ENodeTitleType::Type TitleType) const { return TEXT("Apply Additive"); }

### Tooltip

![Node Tooltip](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/672845cd-2aea-40d6-b2d0-0d590dd7d3d8/node_apply_additive_hover_callout.png)

When creating custom animation nodes you can create custom tooltips that are viewable in the AnimGraph by overriding the `GetTooltip` function:

```
	`FString UAnimGraphNode_ApplyAdditive::GetTooltip const 	{ 		return TEXT("Apply additive animation to normal pose"); 	}`

Copy full snippet
```
FString UAnimGraphNode\_ApplyAdditive::GetTooltip const { return TEXT("Apply additive animation to normal pose"); }

### Context Menu

When creating your own custom animation nodes, you can add node-specific options to the node's context menu, which is accessible by **right-clicking** the node in the AnimGraph. You can add context menu options to your custom animation nodes using the `GetContextMenuActions` function, which also is a function of all Blueprint nodes in Unreal Engine.

![Node Context Menu Entry](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d448d41-a17f-45c3-9060-17d3faa76c20/node_node_actions-context_callout.png)

For example, the `UAnimGraphNode_LayeredBoneBlend` node adds context-menu options for adding a **Add Blend Pin** or **Remove Blend Pin**:

```
	`void UAnimGraphNode_LayeredBoneBlend::GetContextMenuActions(const FGraphNodeContextMenuBuilder& Context) const 	{ 		if (!Context.bIsDebugging) 		{ 			if (Context.Pin != NULL) 			{ 				// we only do this for normal BlendList/BlendList by enum, BlendList by Bool doesn't support add/remove pins 				if (Context.Pin->Direction == EGPD_Input) 				{ 					//@TODO: Only offer this option on arrayed pins 					Context.MenuBuilder->BeginSection("AnimNodesLayeredBoneBlend", NSLOCTEXT("A3Nodes", "LayeredBoneBlend", "Layered Bone Blend")); 					{ 						Context.MenuBuilder->AddMenuEntry(FGraphEditorCommands::Get().RemoveBlendListPin); 					} 					Context.MenuBuilder->EndSection(); 				} 			} 			else 			{ 				Context.MenuBuilder->BeginSection("AnimNodesLayeredBoneBlend", NSLOCTEXT("A3Nodes", "LayeredBoneBlend", "Layered Bone Blend")); 				{ 					Context.MenuBuilder->AddMenuEntry(FGraphEditorCommands::Get().AddBlendListPin); 				} 				Context.MenuBuilder->EndSection(); 			} 		} 	}`

Copy full snippet
```
void UAnimGraphNode\_LayeredBoneBlend::GetContextMenuActions(const FGraphNodeContextMenuBuilder& Context) const { if (!Context.bIsDebugging) { if (Context.Pin != NULL) { // we only do this for normal BlendList/BlendList by enum, BlendList by Bool doesn't support add/remove pins if (Context.Pin->Direction == EGPD\_Input) { //@TODO: Only offer this option on arrayed pins Context.MenuBuilder->BeginSection("AnimNodesLayeredBoneBlend", NSLOCTEXT("A3Nodes", "LayeredBoneBlend", "Layered Bone Blend")); { Context.MenuBuilder->AddMenuEntry(FGraphEditorCommands::Get().RemoveBlendListPin); } Context.MenuBuilder->EndSection(); } } else { Context.MenuBuilder->BeginSection("AnimNodesLayeredBoneBlend", NSLOCTEXT("A3Nodes", "LayeredBoneBlend", "Layered Bone Blend")); { Context.MenuBuilder->AddMenuEntry(FGraphEditorCommands::Get().AddBlendListPin); } Context.MenuBuilder->EndSection(); } } }

## Derived Native Getters

You can create your own `UAnimInstance` derived class to achieve performance improvements . You can add new getters if there is a need for improved performance. You can set up a new getter following the steps below:

-   The getter functions must be tagged as **UFUNCTIONS**.
-   They must be **BlueprintPure**.
-   They must include the metadata **AnimGetter="True"**.

They must also define some specifically named parameters (this is also explained above the base anim getter functions in `AnimInstance.h`). That list of parameters includes :

| **Parameter** | **Description** |
| --- | --- |
| **int32 AssetPlayerIndex** | The getter acts on an asset player and an entry will be added to the editor per asset player available. |
| **int32 MachineIndex** | The getter acts on a state machine, an entry will be added per state machine. |
| **int32 StateIndex** | This also requires MachineIndex. The getter acts on a state, an entry will be added per state. |
| **int32 TransitionIndex** | This also requires MachineIndex. The getter acts on a transition, an entry will be added per transition. |

You can also use helper functions to get the actual nodes in your getters. These exist on the `UAnimInstance`:

| **Function** | **Description** |
| --- | --- |
| **GetStateMachineInstance(int32 MachineIndex)** | Gets the baked state machine instance. |
| **GetCheckedNodeFromIndex(int32 NodeIdx)** | Gets a node from an index, asserts if invalid. |
| **GetNodeFromIndex(int32 NodeIdx)** | As above, can return nullptr. |
| **GetRelevantAssetPlayerFromState(int32 MachineIndex, int32 StateIndex)** | Gets the highest weighted asset player in a state. |