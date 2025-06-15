# Locomotion

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/locomotion-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/locomotion-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:19

---

In **Unreal Engine** character **Locomotion** is built on the foundation of [character object](/documentation/en-us/unreal-engine/setting-up-a-character-in-unreal-engine), [movement](/documentation/en-us/unreal-engine/movement-components-in-unreal-engine), and [animation](/documentation/en-us/unreal-engine/animation-assets-and-features-in-unreal-engine) playback. This foundation is supported with Locomotion tools that you can use to synchronize character movement behavior with reactive and dynamic animations.

This document provides an overview of the character Locomotion tool in Unreal Engine.

## Root Motion

By enabling **Root Motion**, a character's movement can be driven by an animation sequence using motion data from the Root Bone. Animations with their Root Motion enabled, create more realistic and grounded movement behaviors and interactions within levels.

![root motion enabled animation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bd6394cb-998c-4176-98b9-5884b45ef264/recursiverootmotion.gif)

Read about how you can drive a Character's movement with animation playback using Root Motion in the following documentation.

## Pose Warping

You can enable **Pose Warping** to dynamically adjustment a character's animated poses to align with character movement, using [Root Motion](/documentation/en-us/unreal-engine/locomotion-in-unreal-engine#root%20motion). With Pose Warping, you need fewer individual animations to reach the same level of animated-movement coverage as before. This reduces the dependency on animation-dictated gameplay, and allows animation and gameplay tuning to evolve side by side during development.

![pose warping demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e2e75a6-0481-4e61-9858-192998ae5fe0/posewarpdemo.gif)

Read about Pose Warping and an example implementation in the following documentation.

## Motion Warping

With **Motion Warping**, you can dynamically warp windows of a character's animation to align with [Root Motion](/documentation/en-us/unreal-engine/locomotion-in-unreal-engine#root%20motion) or to align with assigned **Warp Targets**. With this feature, you can rely less on the manual creation and fine tuning of animations to fit specific object interactions, and apply logic to bend base animations to fit pre-established conditions.

![motion warping animation to warp target](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d1de273-031b-4eec-b1fd-26354909b503/motionwarpingresult.gif)

In the following documentation you can read more about Motion Warping and follow along with an example workflow.

## Distance Matching

With **Distance Matching** you can use a calculated distance value, to or from, a target to drive Animation Sequences. Distance Matching can align animation playback with character speed, reducing the need for manual animation tuning when altering character behaviors.

![distance matching animation pose selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77797fbd-dc86-4964-8248-446942d09332/lyradistancematchingdemo.gif)

Read about Distance Matching and see an example workflow in the documentation below.