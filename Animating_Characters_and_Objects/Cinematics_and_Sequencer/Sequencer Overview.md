# Sequencer Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview)  
**Processed:** 2025-06-14 16:57:06

---

Sequencer gives users the ability to create in-game cinematics through its specialized multi-track editor. By creating Level Sequences, adding tracks, and creating keyframes you can manipulate objects, characters, and cameras.

This page provides an overview of Sequencer Actors, Level Sequence Assets, and the primary features of Sequencer.

## Sequencer Asset and Actor

Sequencer in Unreal Engine consists of 2 main parts: a **Level Sequence Asset** and a **Level Sequence Actor**.

The **Level Sequence Asset** is located in the Content Browser and contains Sequencer's data. This includes tracks, cameras, keyframes, and animations. This is assigned to a **Level Sequence Actor** in order to bind its data to a Level.

![level sequence asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/49c55c39-b51a-4afd-bef4-9d18ac8a6cdb/seqasset.png)

The **Level Sequence Actor** is located in the Level and is the container for the **Level Sequence Asset**. You can select it to view its details in the **Details** panel.

![level sequence actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b22525d-4df0-43c8-b131-f13bc74eaf10/seqactor.png)

| Name | Description |
| --- | --- |
| **Open Level Sequence** | Opens the Sequence Editor for the currently bound level sequence asset. |
| **Level Sequence** | The currently bound level sequence asset. |
| Playback |   |
| **Auto Play** | The sequence will automatically play when the actor is created. |
| **Loop** | Loop options for the sequence. Don't Loop will cause the sequence to play once and finish. Loop Indefinitely will cause the sequence to loop forever. Loop Exactly... will expose a numerical time entry where you can specify the amount of times the sequence will loop, then finish. |
| **Play Rate** | The speed of the sequence to play. Does not affect Time Dilation. |
| **Start Offset** | The amount of time in seconds the sequence should start relative to the start time. |
| **Random Start Time** | Starts playing the sequence at a random point between the start and end time. Enabling this will disable Start Offset. |
| **Restore State** | Restores all actors to their previous state before the sequence started. |
| **Pause at End** | The sequence will pause upon reaching the end, keeping all actors in their final positions in the sequence. |
| Cinematic |   |
| **Disable Movement Input** | Disables translation input from the player pawn for the duration of the sequence. |
| **Disable Look At Input** | Disables rotation input from the player pawn for the duration of the sequence. |
| **Hide Player** | Disables the player pawn's visibility for the duration of the sequence. |
| **Hide Hud** | Hides all Heads Up Display (HUD) elements for the duration of the sequence. |
| **Disable Camera Cuts** | Disables the Camera Cuts track, causing the sequence to not take control of the camera. |

### Sequencer Creation

There are several ways you can create and assign your Level Sequences.

One of the quickest ways is to click the **Cinematics** dropdown in the Level Editor's main toolbar and select **Add Level Sequence**. This will prompt you to create a new **Level Sequence Asset** in the Content Browser. Give it a name and click **Save**. Once created, your Level will now contain a **Level Sequence Actor** with a reference to the newly created **Level Sequence Asset**.

![create level sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1d6815f-65de-4be6-a34c-12aa1a6f0025/createseq1.png)

An alternate way of creating and assigning your sequence is to click **Add/Import > Animation > Level Sequence** in the **[Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine)**. This will also prompt you to create a new **Level Sequence** Asset.

![create level sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7daae85b-71bd-4dac-96ce-3200ab4fb471/createseq2.png)

Once the sequence Asset has been created, navigate to the **[Place Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine)** panel and drag in a **Level Sequence Actor** from the **Cinematic** category.

![add sequence actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ef55f7d-04a9-4377-9ceb-9212cb22a8a6/addseqactor.png)

Then bind your Level Sequence Asset to the Level Sequence Actor by dragging and dropping the Asset onto the Level Sequence property.

![bind level sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13eccbc8-8bc4-4310-8e25-8807301543a0/assignseq.png)

## Sequencer Editor

The Sequencer tab contains the Sequencer Editor, which provides a user interface for creating cinematic content.

![sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22ae54fc-a86f-43f5-ac3f-2ddb470a0c40/seqwindow.png)

There are various ways you can open this window.

One way is to click the **Cinematics** dropdown in the Level Editor's main toolbar and select your sequence from the list. Your sequence must be assigned to a Level Sequence Actor within your Level for it to appear here.

![open sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27e7df6e-1aad-466f-80d9-38d8e35ac7a2/openseq1.png)

Another way is by clicking the Level Sequence Actor's **Open Level Sequence** button in the **Details** panel.

![open sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7267cf70-3ca5-443e-ace7-e66661698fba/openseq21.png)

Or by double-clicking the **Level Sequence** property icon in the **Details** panel.

![open sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/210a5858-20ab-4311-bce6-359f321cf86b/openseq2.png)

You can also open it by double-clicking the Level Sequence Asset in the **Content Browser**.

![open sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a06b9f6-1bba-4de6-99f3-32b4e6c39b8a/openseq3.png)

When opening a sequence from the Content Browser, you must currently have a Level opened in which this sequence is being referenced. Otherwise the contents will be unbound.

Finally, you can open it by navigating to the main menu bar and clicking **Window > Cinematics > Sequencer**.

![open sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ab4eb42-618f-43de-92cc-d60dc63dd662/opensec4.png)

Visit the **[Sequencer Editor](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine)** page for more information on the Sequencer editor.

## Sequencer Features

The following pages detail the primary animation and movie-making features of Sequencer.