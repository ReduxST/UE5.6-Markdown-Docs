# Apply Animation to a Character

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-add-cinematic-animation-to-a-character-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-add-cinematic-animation-to-a-character-in-unreal-engine)  
**Processed:** 2025-06-14 16:28:34

---

This page provides a beginner's overview of how to animate Skeletal Meshes in Sequencer, and is intended for those who are new to Sequencer and Unreal Engine.

#### Prerequisites

-   You have read through the [Sequencer Basics](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) page and have already created and opened a **Level Sequence** in your Level.
-   Your project contains a [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine) and [Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine). If not, you can create a project using the [Third Person template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine), which provides sample Skeletal Meshes and animations.

## Adding a Character to Sequencer

Start by adding a character to your Level. Do this from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) by navigating to your asset and dragging it into your Level.

![add skeletal mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24ecb7e8-c4bb-40fc-ad1a-35e96e4b2940/addchar1.png)

Next, with your sequence open and the character selected, click **Add Track (+)** and select **Actor to Sequencer > Add 'SKM\_Manny2'**. This will add a track referencing the character into your sequence.

![character add sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7174834d-7c6b-4baa-8bf9-82d17b7ef9e2/addchar2.png)

When the Skeletal Mesh track is added to the sequence, it [automatically adds](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine#automatictrackcreation) commonly used tracks for this Actor. In this example, [Animation](/documentation/en-us/unreal-engine/cinematic-animation-track-in-unreal-engine) and [Transform](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine) tracks are automatically created.

## Applying Animation to a Character

Click **Add Animation (+)** on the Animation track. This will list all available animations that are compatible with your character's skeleton. Select one of these animations to add it to your sequence.

![add animation sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a25d3666-78b7-40a7-ad6b-ca210b110074/addanim.png)

Once the animation is added, click **Play** to preview the sequence. If the animation is intended to continue past the current endpoint, you can drag the edge of the clip to extend it.

![play character animation sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55d8e9d4-35c7-4d5d-937d-26019a937bc2/play.gif)