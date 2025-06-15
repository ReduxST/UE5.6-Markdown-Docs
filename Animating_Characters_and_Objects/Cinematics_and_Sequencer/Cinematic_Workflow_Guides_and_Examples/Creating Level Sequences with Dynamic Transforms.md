# Creating Level Sequences with Dynamic Transforms

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-level-sequences-with-dynamic-transforms-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-level-sequences-with-dynamic-transforms-in-unreal-engine)  
**Processed:** 2025-06-14 16:17:37

---

If your project requires cinematics or other **Level Sequence** content that takes place in more than one location, it may be beneficial to use Sequencer's **Transform Origin** features to dynamically change the location of the animation at runtime. By default, all Sequencer transforms are relative to the world origin (0, 0, 0). However, by using Transform Origin, you can make transforms relative to any transform, or even to an Actor's transform.

This document provides instructions on how to bind Transform Origin to an Actor to change the location of Sequencer content.

#### Prerequisites

-   You are familiar with creating content with Sequencer. Refer to these pages for more information:
    
    -   [Create Camera Animation](/documentation/en-us/unreal-engine/how-to-animate-cinematic-cameras-in-unreal-engine)
    -   [Apply Animation to a Character](/documentation/en-us/unreal-engine/how-to-add-cinematic-animation-to-a-character-in-unreal-engine)

## Level Sequencer Setup

To start, create a [Level Sequence Actor](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) in your Level. Select it, and in the **Details** panel do the following:

1.  Enable **Override Instance Data**.
2.  Assign the **Level Sequence Actor** to **Transform Origin Actor**.

![assign transform origin actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ca5a075-624d-4fea-a025-8a9c0124a3eb/setup1.png)

Which Actor to assign to Transform Origin Actor is arbitrary and depends on the context of your scene. For example, if you have a scene where characters are interacting with an object, like a table, then it may be better to assign the table as the Transform Origin Actor.

Depending on your use-case, you may want to assign the Transform Origin Actor first, before creating any Sequencer content in Unreal Engine. If you create content first and then assign a Transform Origin Actor with a non-zero location, your content will move relative to that Actor. In other words, your current Sequencer transforms do not compensate when assigning the Transform Origin Actor.

## Content Setup

Next, [create content in your sequence](/documentation/en-us/unreal-engine/creating-level-sequences-with-dynamic-transforms-in-unreal-engine#prerequisites), aligning your Sequencer content to the Transform Origin Actor. In this example, the Mannequin character walks to the same location as the Level Sequence Actor.

![create cinematic content aligned to transform origin actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/113c27a8-5c4a-408e-ad90-41f50c321a54/content1.gif)

You can now move the Transform Origin Actor and see your animation change location when playing.

![move transform origin actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d623f0b-b197-4d2c-a44b-8738a6af2a53/content2.gif)

## Results

Changing the location of the Transform Origin Actor affects all transforms and animations within the sequence. This makes it possible to dynamically change where a scene takes place.

![dynamic scene location](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99a1c3a7-e875-474c-a656-7aef902b486b/content3.gif)

All objects within a [Root Sequence](/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine) also receive Transform Origin offsets.

## Animated Transform Origin

Transform Origins also correctly adjust Sequencer content if the origin Actor is animated. In this example, the boat Actor is set as the Transform Origin Actor, causing the character and any other transformed actors in the sequence to follow the animation of the boat during runtime.

![animated transform origin actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38598d5b-d0cb-4bca-9753-39381eac0de7/boat.gif)