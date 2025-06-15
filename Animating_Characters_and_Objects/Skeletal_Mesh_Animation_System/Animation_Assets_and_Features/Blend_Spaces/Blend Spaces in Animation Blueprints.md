# Blend Spaces in Animation Blueprints

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-spaces-in-animation-blueprints-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-spaces-in-animation-blueprints-in-unreal-engine)  
**Processed:** 2025-06-14 16:10:11

---

**Blend Spaces** are used in Unreal Engine by placing nodes in the [AnimGraph](/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine) of [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine) which take input data to drive the blending of the samples used in the **Blend Graph**. They can also be created directly in the AnimGraph without needing a pre-existing Blend Space.

This page provides an overview of the different types of Blend Space nodes in Animation Blueprints, and how to use them.

#### Prerequisites

-   You have created and have an understanding of [Animation Blueprints](/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine).
-   You have created a [Blend Space](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine) or [Aim Offset](/documentation/en-us/unreal-engine/aim-offset-in-unreal-engine).

## Blend Space Player

**Blendspace Players** are nodes which reference a currently existing Blend Space Asset. They contain data pin inputs for both axes, or one axis if using a [1D Blend Space](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#1d). The node outputs the resulting pose based on those inputs.

![blendspace player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b51d5d4-e7e3-4580-b534-cf2aa9a01dcd/player1.png)

Aim Offsets can also be used as players.

### Creation and Usage

Blendspace Players can be created in any of the following ways:

By right-clicking in the AnimGraph and selecting your Blend Space from the **Blend Spaces** category. Ensure it contains the **Blendspace Player** prefix.

![create blendspace player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9994291-3c4c-4485-8152-156c5cc8b8a1/playercreation1.png)

By dragging the Blend Space Asset from the Asset Browser or Content Browser into the AnimGraph.

![create blendspace player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2c62ea8-44e7-4ac0-90a5-35332fc14496/playercreation2.png)

Double-clicking a Blendspace Player will open that Asset in a separate window, if the Blend Space is assigned.

![open blendspace player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c0d0c13-512f-4f59-a625-6cdcdf23848b/openplayer.gif)

### Properties

Selecting the Blendspace Player will reveal the following properties relevant to the Blend Space in the **Details** panel.

![blendspace player settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d25abe81-742e-4229-8196-178627d056eb/playerproperties.png)

| Name | Description |
| --- | --- |
| **Coordinates** | The Axes or Axis (if 1D) of the Blend Space. |
| **Play Rate** | The speed of the playing samples in the Blend Space. Setting this to negative values will cause the samples to play in reverse. |
| **Loop** | Enabling this will cause the samples to repeat playing indefinitely. When disabled, this will cause the final frame of the sample to be held. |
| **Reset Play Time when Blend Space Changes** | Resets the normalized time of the playing samples if the **Blend Space** property changes. |
| **Start Position** | The start time for all the samples in the Blend Space. This is in normalized time, so it must be a value between **0** and **1**. |
| **Blend Space** | The Blend Space Asset to use. |
| **LOD Threshold** | Controls the maximum Level of Detail (LOD) that this node is permitted to run on. For example, if you set this to **2**, it will enable until **LOD2**, but disables once the component's LOD becomes **3**. A value of **\-1** will cause the node to always execute, regardless of LOD. This property only appears for **Aim Offset** and **Aim Offset Players**. |

## Blend Space Graph

While Blendspace Players are nodes that reference currently existing Blend Spaces, **Blend Space Graphs** are nodes that contain Blend Spaces within the Animation Blueprint. Using them, you can create bespoke Blend Spaces for your Animation Blueprint, diverge them from other assets, and edit sample logic.

![blend space graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d2c7cf1-8b6b-49d4-a6d2-ea153d87d275/animgraph1.png)

Aim Offsets can also be used in this manner.

### Creation

To create this Blend Space type, right-click in the AnimGraph and select **Blend Space** from the Blend Spaces category. You can also select a pre-existing Blend Space Asset by selecting it, ensuring the prefix says **Blendspace**. Doing this will import (instead of referencing) the Blend Space, in which you can diverge it from the original.

![create blend space graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4af56843-4efd-483f-90d8-34526afa8dde/animgraph2.png)

### Usage

As Blend Space Graphs are meant to be created and managed within your Animation Blueprint, you can open the Blend Space interface by double-clicking on the Blend Space entry in the **My Blueprint** panel. From here, you can [add samples](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#addinganimationstothegraph), [define your axis values](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#definingaxisnamesandranges), and [edit other properties](/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine#assetdetails) just like a Blend Space asset.

![add samples to blend space graph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b23b1850-200b-454d-a695-e04f5a97c596/animgraph3.gif)

Each sample in the blend space contains its own sub-graph, which can be viewed by double-clicking it. In this way, you can assign more features to a sample by creating additional logic.

![blend space sample animgraph](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40b2a1e7-ca8a-4fd2-9e84-f00902a7fb0a/animgraph4.png)

## Blend Space Evaluator

**Blendspace Evaluators** are Blend Space nodes that have the times of all their samples' times controlled externally, rather than play automatically. This time control is a normalized (0 - 1) float value that determines the point at which the pose is sampled.

![blend space evaluator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18422d85-37ec-4f58-b2b6-0e31e725787e/evaluator1.png)

To create this Blend Space type, right-click in the AnimGraph and select **Blendspace** **Evaluator** from the Blend Spaces category. You can also select a pre-existing Blend Space Asset by selecting it, ensuring the prefix says **Blendspace Evaluator**.

![create blend space evaluator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/345f64f3-b4ce-4c22-8584-9c0a291a476b/evaluator2.png)

By default, the Blendspace Evaluator teleports to the provided time and does not advance time, which causes root motion or Animation Notifies to not evaluate. Disabling **Teleport to Normalized Time** will restore this functionality.

![blend space evaluator settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca9b63e6-f7ea-4815-8ca9-9f51f2b1129b/evaluator3.png)