# Animation Slots

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine)  
**Processed:** 2025-06-14 16:07:38

---

As you create more complex Animation behavior for your characters, it may be necessary to create proxy areas in your Animation Blueprint where you can insert one-off animations. This can be accomplished by using **Slots**, which are nodes that you can add to your Animation Blueprint at various points to layer and play animations into. Slots are mainly used together with [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine), however they can also be used with [Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine).

This document provides an overview of how to create and use Animation Slots in your Animation Blueprint, Montages, and Sequencer.

#### Prerequisites

-   You are familiar with how to [graph within Animation Blueprints](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine).

## Overview

The main purpose of Slots is to provide a place in the Anim Graph to insert animations into your Animation Blueprint. This can be useful when using [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) as a way to insert one-off animations, such as shooting or interacting with objects. Slots can also be used together with blending nodes to separate playback to only occur on certain Bones on your character, such as upper body or arms.

For example, in this setup, Slots are used in the following two ways:

![slot example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f5df33d-ac9e-4c73-87e7-bf73cffac32d/overview.png)

1.  A **Full Body Slot** is used after the main locomotion [State Machine](/documentation/en-us/unreal-engine/state-machines-in-unreal-engine), which can insert animations in an overriding manner. This Slot can be used for full-body object interaction or emote gestures.
    
2.  An **Upper Body Slot** is used together with a [Layered blend per bone](/documentation/en-us/unreal-engine/animation-blueprint-blend-nodes-in-unreal-engine#layeredblendperbone) node to remove animation on the lower body so that only the upper body is affected. This Slot can be used for weapon reloading, shooting, or other similar animations which can work correctly regardless of your character's locomotion state.
    

## Creating and Managing Slots

Slots are created and managed from the **Anim Slot Manager**, which is a panel that can be opened from the **Animation Blueprint**, **Skeleton**, or **Animation Sequence** Editors. To open the panel, in any one of those editors, go to **Window > Anim Slot Manager** from the main menu.

![anim slot manager](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/670e6952-5e92-4323-9787-1fa2d3a3c4d9/create1.png)

By default, all Skeletons come with a starting Slot named **DefaultSlot**. To add a new Slot, click **Add Slot (+)**, type in a name for the Slot, then press **Enter**.

![create new slot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48fba9a6-7b28-42a8-9d44-10f2b8d15525/create2.png)

Regardless of the animation editor you are in, Slots are stored on the [Skeleton](/documentation/en-us/unreal-engine/skeletons-in-unreal-engine) Asset, therefore, when you are creating or changing Slots, you are also editing the Skeleton. Clicking **Save** in the Anim Slot Manager will save the Skeleton when you make any Slot changes.

Right-clicking in the Anim Slot Manager or on Slot entries will show the following context menu commands:

![slot context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7341b836-60d6-415c-bc63-12cde209c377/create3.png)

| Name | Description |
| --- | --- |
| **Set Slot Group to** | Moves the selected Slot to a different [Slot Group](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine#slotgroups), if one is available. |
| **Rename Slot** | Renames the selected Slot. |
| **Delete Slot** | Deletes the selected Slot. |
| **Add Slot** | Creates a new Slot. |
| **Add Group** | Creates a new [Slot Group](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine#slotgroups). |

## Using Slots

Before you start using Slots, you must first ensure they are added to your [Animation Blueprint](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).

In the Anim Graph, right-click and add the **Slot 'DefaultSlot'** node.

![create default slot node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/20c3af92-ceb7-41d9-b436-82e9ba26cf76/usage1.png)

By default, newly created Slot nodes will use **DefaultSlot**. To change this, select the node and set the **Slot Name** property in the **Details** panel to your desired Slot.

![change slot name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5db97211-51d9-4d3a-9e1d-75731065c53b/usage2.png)

Slots are designed to support incoming source pose links so that the Slot passes through the incoming pose if animations are not being inserted into it. The Slot only begins to override the incoming animation with its own once animation starts playing on the Slot.

Once an incoming source pose is overridden, it will no longer evaluate. You can change this to ensure the incoming animation keeps evaluating by enabling **Always Update Source Pose** in the Slot's **Details** panel.

![always update source pose](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd2d2b51-e202-4be3-b0d5-759d388084d4/usage3.png)

### In Animation Montages

[Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) require Slots in your Anim Graph to function, as they exclusively play animation using Slots. In this example, an Animation Montage will apply this animation to the **Upper Body Slot**.

![slots in montages](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/968ecf33-b920-47cf-bb34-ab19f27577b7/montage1.png)

To change or add Slots to the Montage, click the Slot dropdown menu on the Slot track to view the following commands:

![change slot in montage](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d031aea3-11c0-4d1c-98ac-40bccc1a3088/montage2.png)

| Name | Description |
| --- | --- |
| **Slot name** | Exposes a menu where you can change the current Slot. If this is the topmost Slot track, then selecting a Slot that is part of a different [Slot Group](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine#slotgroups) will change the Montage's Slot Group. |
| **New Slot** | Adds a new Slot Track using a pre-existing Slot. |
| **Delete Slot** | Deletes the Slot. |
| **Duplicate Slot** | Duplicates the Slot track and its contents into a new Slot track. |
| **Preview Slot** | If you have more than one Slot track, enabling this will cause the contents of this Slot to preview in the Viewport. |
| **Slot Manager** | Opens the [Slot Manager](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine#creatingandmanagingslots) panel. |

A single Montage can play animations on multiple Slots at the same time, but they must be within the same [Slot Group](/documentation/en-us/unreal-engine/animation-slots-in-unreal-engine#slotgroups).

Refer to the [Animation Montage](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine) page for more information on using Animation Montages.

### In Sequencer

Slots can also be used in [Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine), which is Unreal Engine's cinematic and movie-making tool. Using Slots in Sequencer enables inserting cinematic animation within an Animation Blueprint, so that your characters can benefit from its additional logic.

Slots are used for animations in the [Animation Track](/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine). To set an animation to play from a Slot, right-click an animation section and navigate to **Properties > Slot Name**. Enter the name of the Slot you want to insert this animation into.

![slots in sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47ae6ce1-ff77-449c-9fbe-c7004560ad39/sequencer1.png)

A common use-case for using Slots in Sequencer is to blend cinematic and gameplay animation together. Refer to the [Blending Gameplay and Sequencer Animation](/documentation/en-us/unreal-engine/blend-gameplay-animation-to-cinematic-animation-in-unreal-engine) page to learn more.

## Slot Groups

In addition to Slots, you can also create Slot groups to organize and control Slot playback within [Animation Montages](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine).

A **DefaultGroup** Slot group will already exist on your Skeleton. To create another Slot group, click **Add Group (+)** in the **Anim Slot Manager**, type in a name for the Slot group, then press **Enter**.

![slot groups](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8f9e620-0d07-49ba-afe0-a114885b93ec/groups1.png)

An existing Slot can be moved to a different Slot group by right-clicking it and selecting **Set Slot Group to**.

![change slot group](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f89f06d-4822-4593-bf77-ad53f7328f1f/groups2.png)

Slot groups are not just organizational. When you play a montage that uses a Slot in the same group as one that's already running, it stops the active one. This automatic behavior allows for montages to be interrupted. For example, a weapon reloading montage could be interrupted to play an ability or melee attack montage. If both montages are playing animations on Slots within the same group, then the most recent montage will interrupt the previous.

To learn more about using Slot groups in Animation Montages, refer to the [Animation Montage](/documentation/en-us/unreal-engine/animation-montage-in-unreal-engine#slotsandslotgroups) page.