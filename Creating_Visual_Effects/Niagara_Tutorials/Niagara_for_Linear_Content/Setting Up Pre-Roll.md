# Setting Up Pre-Roll

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-pre-roll](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-pre-roll)  
**Processed:** 2025-06-14 16:49:46

---

## Pre-Roll

Use **pre-roll warm up** to ensure simulations are ready before the Sequence begins.

There are many times when an FX element needs to already be visible on the first frame of a shot. Maybe it's the continuation of an explosion which happened in a previous shot, a missile trail, or a waterfall cascading over rocks.

There are a few ways we can handle pre-roll of Niagara Systems. There are pros and cons to each technique.

## Niagara System Warmup

Each system can define a **Warmup Time**. This tells Niagara to tick for a period of time before being rendered. As a result the system has performed a pre-roll before sequencer starts playing it.

Warmup can be defined inside the **Niagara system** or on the **Niagara system instance** in the level. Search for "warmup" on the component:

![Warmup settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/505ea5ce-9ca5-454a-a58c-2d80e2879b0d/warmupcomponentsettings.png)

## System Life Cycle Track

A similar method to the Warmup Time is to use the **System Life Cycle Track** to offset the system before the start of the shot. This method can be more intuitive as the start and end times for the system are clearly visible from Sequencer.

## Niagara Pre-Roll vs Engine Pre-Roll

Both the Warmup Time and System Life Cycle Track pre-roll methods suffer from the fact that only the Niagara System is performing the pre-roll. If there is anything in the world influencing the system, collisions or a parent transform for example, the pre-roll will not take it into account.

In the video below you'll notice that the 'rolling balls' do not collide against the cubes until the shot starts.

## MRQ: Use Camera Cut for Warm Up

The Movie Render Queue (MRQ) supports Warm Up when preparing to render a shot. The settings are inside the **Anti-aliasing** block. The setting you will need to activate is called **Use Camera Cut for Warm Up**. The nice thing about this mode is it will tick the engine, including Skeletal Meshes, providing a more accurate environment for Niagara to interact with.

![MRQ warm up](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11e2af03-ae6a-4b26-a45d-ca32daad715a/mrqwarmuptooltip.png)

## Movie Render Queue: Render Warm Up Frames

The MRQ considers there are two types of Warm Up: Engine Warm Up only and Render Warm Up. The cheaper option is to tick the engine only and do not waste time rendering frames that are not going to be needed. However, there are several cases where it is necessary to render the warm up frames so a Niagara System can function correctly.

The most obvious case is when using **Depth Map collisions**. For a depth map to exist, it must first be rendered. Without the Render Warm Up Frames option being active, GPU Depth Map collisions will not be able to operate properly.

Other use cases include any time you are querying the **GBuffer** for Scene Color etc.

In the Anti-aliasing settings block, activate the **Render Warm Up Frames** option.

The MRQ Warm Up is a powerful tool, but it is not possible to preview in editor. However, in many cases this may be the most reliable approach.