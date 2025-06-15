# Physics-Based Animation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-driven-animation-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-driven-animation-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:53

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8243c15b-2ff3-49eb-9c4f-ff87480e9483/physicsblend.png)

This document covers how to apply physics-driven animation to your characters and Skeletal Meshes. The concept is that you can blend in the result of a simulation along with your keyframed animation to have a naturally simulated feel for characters that need to exhibit a "ragdoll" effect.

An example of this concept in action can be seen in the [Content Examples](/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine) project, within the map named PhysicalAnimation.umap. In this map, we have a series of Skeletal Meshes to which animation has been applied. In each one, we can also interact in some way and see physics animation take over the existing motion.

Be aware that the use of physics on a Skeletal Mesh in any form requires that the mesh have a Physics Asset set up and applied to it. Please see the associated documentation for the [Physics Asset Tool (PhAT)](/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine).

Skeletal Meshes are used in this example for overall simplicity. The same techniques can be applied to a Character or Pawn, simply by utilizing the **Set All Bodies Simulate Physics** and **Set All Bodies Below Physics Blend Weight** nodes within the Animation Blueprint's Event Graph, rather than on a simple Blueprint Actor's Event Graph, as we do in this example.

## Setup

There are many ways to apply physics to a character and our example shows only a few possibilities. In our approach, the two primary tools you will need are the Set All Bodies Simulate Physics and Set All Bodies Below Physics Blend Weight nodes, which will generally be placed within your character's Animation Blueprint Event Graph.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b738e05-2170-4a7d-8a7e-033d40714aa2/physicsweghtnodes.png)

### Set All Bodies Below Simulate Physics

The purpose of the Set All Bodies Below Simulate Physics node is to recursively activate Physics Asset bodies on a Skeletal Mesh to begin simulating physics starting at a given bone and moving recursively down the bone chain. For example, if you tell the left clavicle to start simulating, then all of the bones descending from that in the skeletal hierarchy will simulate as well, resulting in a limp or ragdolling arm. Simply put, you can think of this node as an on/off switch to begin or stop simulating physics from a given bone.

### Set All Bodies Below Physics Blend Weight

This node simply controls how much influence the Physics Asset will have over the animated Skeletal Mesh. At a value of 1.0, the given bone and all those below it are completely driven by physics. At a value of 0.0, the Skeletal Mesh has returned to its original keyframe animation. Often, you will want to drive this node at each tick so that you can smoothly animate the Physics Blend Weight value.

## Hit-Based Reaction Overview

Hit-based physics reactions are a common use case for simulation on characters, such as when a character is struck by a projectile. At a high-level, this requires that you:

-   Get the name of the bone that was hit. This can be done via a trace for instant-effect weapons, or within a projectile class where applicable.
-   Transfer that bone name into the Character's Animation Blueprint for the Event Graph to use, generally through a Set All Bodies Below Simulate Physics node. This activates the simulation system.
-   Control the Physics Blend Weight property via a Set All Below Physics Blend Weight node. Generally, you want to quickly animate this going up to 1.0 and then back down to 0.0 so that the physics reaction blends in and then back out. This would generally be done within the Animation Blueprint's Event Graph.
-   Once the reaction is complete and the Physics Blend Weight returns to 0, you should use the Set All Bodies Below Simulate Physics node once more to deactivate the simulation.

You can see an example of this technique in Example 1.2 of the PhysicalAnimation.umap level, found within the Content Examples project.