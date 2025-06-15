# Referencing the Player in Sequencer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-reference-the-player-in-unreal-engine-cinematics](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-reference-the-player-in-unreal-engine-cinematics)  
**Processed:** 2025-06-14 16:29:14

---

When making cinematic content in Sequencer, it may not be clear how to add and animate the player character in the same way you [add other objects or actors](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine) in the scene. This document provides the recommended workflow for referencing the player character as a proxy, then binding it to the actual player at runtime.

#### Prerequisites

-   You have a controllable player character in your project. For this document, the [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) is used as an example.
-   You are familiar with [animating skeletal meshes in Sequencer](/documentation/en-us/unreal-engine/how-to-add-cinematic-animation-to-a-character-in-unreal-engine).
-   You are familiar with using [Blueprints](/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine).

## Reference a Proxy Player

While the PlayerStart Actor is the spawn point for the player, this is not a useful or appropriate Actor to use in Sequencer, as it does not include the player mesh or object being spawned.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e45c7891-9ae7-40d1-ac4e-fb4c4407270f/proxy1.png)

Because of this, you should instead create a proxy (substitute) Actor to animate with instead. One way this can be done is by creating a [spawnable](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics) reference of the player **Character Blueprint**. To do this, navigate in the **Content Browser** to the Character Blueprint Asset and drag it into Sequencer.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/365240f6-d35a-4937-a585-5c23a672ab8a/proxy2.gif)

This creates a spawnable Actor based on the player Character Blueprint in your Sequence. It is a temporary Sequencer-only character, which can be useful to not pollute your level with proxy references.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/524b5ae7-aa2e-4311-a865-b383057a4c57/proxy3.png)

You can now animate and create content on this proxy character in your cinematic sequence.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23ee0bae-66ec-4ebd-8b38-b515dacd6794/proxy4.gif)

## Rebind Proxy to Actual Player

Once your content is ready, the proxy character must be replaced with the actual player before the sequence plays.

### Create Player Tag

To make finding the proxy character to replace easier, assign a [Tag](/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine) to the character track. To do this, right-click the track and select **Tags**, then type a tag name in the **Add Tag** menu and press **Enter**. This creates a tag on the character track.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a5b44cf-f1f8-4474-baca-cef9521a6edc/rebind1.png)

### Blueprint Setup

Next, open your Level Blueprint by clicking **Level Blueprint** in the **Level Toolbar** and selecting **Open Level Blueprint**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b876643-a26b-4a58-aadc-fe6ff219ed8c/rebind2.png)

Reference your sequence in Blueprints by selecting the **Level Sequence Actor** in your level, then right-click in the **Event Graph** and select **Create a Reference to Level Sequence**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ce8b18cf-7134-437a-8d38-f2a536577993/rebind3.png)

Create the following logic:

1.  Create a **Get Player Pawn** node, which gets the current actual player during runtime. This is the actor that replaces your proxy character.
2.  Drag off the Level Sequence reference and create a **Set Binding by Tag** node, which is used to change the binding of an object or Actor on a track by tag name. On this node, do the following:
    
    -   Connect your **Level Sequence** reference to **Target**.
    -   Set **Binding Tag** to the tag name you created earlier on the proxy character track.
    -   Connect **Get Player Pawn** to **Actors**.
    -   Ensure **Allow Bindings from Asset** is **disabled**. If **enabled**, the proxy actor remains and won't be overridden, resulting in both the player pawn and the proxy actor bound to the track.
    
3.  After binding, **Play** the sequence.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02e48f1b-7ba8-4da2-bc2c-be20e188a4cf/rebind4.png)

## Results

When executing this logic, you should see the player correctly animating in your cinematic sequence.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/792d7b3e-f717-4bf6-82cb-8db48f08e826/results.gif)