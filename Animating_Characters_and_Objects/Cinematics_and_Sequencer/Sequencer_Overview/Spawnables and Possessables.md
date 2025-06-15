# Spawnables and Possessables

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics](https://dev.epicgames.com/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)  
**Processed:** 2025-06-14 16:51:51

---

In Sequencer, you can choose to either reference an Actor that currently exists in the scene, referred to as a **Possessable**, or spawn a new Actor, referred to as a **Spawnable**. This document provides an overview of these concepts and how you can use them in your scenes.

#### Prerequisites

-   You have an understanding of **[Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)** and its **[Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine)**.
    
-   You know how to create and use **[Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine)**.
    

## Possessable and Spawnables

### Possessable

You can possess Actors by adding existing Actors in a level to your sequence. The link is formed as a [soft object path](/documentation/en-us/unreal-engine/API/Runtime/CoreUObject/UObject/FSoftObjectPath). In most cases this might be an acceptable or even preferable workflow. If your scene requires a high degree of interaction with currently existing Actors in a **Level Sequence**, then possessing is likely the best choice for referencing Actors.

You can add any Actor to the sequence by selecting it or picking an Actor from the **Add Actor to Sequencer** list. You can also drag an Actor from the **Outliner** to an open space in **Sequencer**.

![Actor to sequencer possessable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9630b26-d1a8-4e69-bf89-a427c230b77d/add_actor_to_sequencer.png)

### Spawnable

In cases where your scene requires Actors that might be temporary for the duration of a scene, you can use **Spawnables**. By default, when a sequence with a Spawnable Actor starts, the Actor will be spawned. When the sequence ends, the Actor will be destroyed and removed. You can also explicitly control the frames during which the Actor is spawned and destroyed with the Spawn Track.

#### Create Spawnable

There are two methods for spawning Actors: dragging actors and adding an Actor.

If you have an existing Actor that isn't in **Sequencer** and you want to turn it into a **Spawnable**, add it to **Sequencer** as a **Possessable** and then convert the Actor into a **Spawnable**.

You can create a **Spawnable** by dragging it into Sequencer. Drag an Actor from the **[Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine)**, **[Outliner](/documentation/en-us/unreal-engine/outliner-in-unreal-engine)**, or **[Place Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine)** panels into an open area in Sequencer Outliner.

![Drag actor from Content Browser to Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/25d21887-ff31-4b04-9933-5d6c8f7cbf84/drag_actor_from_content_browser_to_sequencer.gif)

Drag actor from Content Browser to Sequencer

![Drag actor from Place Actors to Sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb880033-94cb-43d0-9d98-947951fc7bf7/drag_actor_from_place_actors_to_sequencer.gif)

Drag actor from Place Actors to Sequencer

To convert a **Possessable** to a **Spawnable**, follow these steps:

1.  Select the Actor that you want to spawn in the Viewport or from the Outliner.
    
2.  In Sequencer, click **Track > Add Actor to Sequencer > Add '{name of selected actor}'**. This action adds the Actor to Sequencer but it is not a Spawnable yet.
    
3.  Right-click the Actor in Sequencer and select **Convert to Spawnable**.
    

A Spawnable Actor can be converted back to Possessable. When this happens, the Actor is re-created in your level and the track binds to it, removing the Spawnable Actor.

#### Identify Spawnables in Sequencer

Once an Actor has been spawned, a **lightning bolt overlay** appears on the Actor in Sequencer and in the **Outliner**.

![Possessable and Spawnable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f5b3e90-3851-4193-ac57-b8e224ab9789/possessable_and_spawnable.png)

Possessable Actor Spawnable Actor

![Spawned actors in Outliner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64c107ce-b766-4536-9d1b-af61fc7c7d5f/spawned_actors_in_outliner.png)

Spawned actors in Outliner

## Spawnable Properties

Spawnable Actors have various properties that control their behavior and interactions with Sequencer. These properties can be accessed by right-clicking the Spawnable bound track and locating the **Spawnable** category.

| Property Name | Description |
| --- | --- |
| **Spawned Object Owner** | 
Specifies which Level Sequence owns the Actor, which also determines the automatic spawn behavior.

-   **This Sequence** is the default setting which causes the Actor to be spawned and destroyed for the duration of the current sequence only.
-   **Root Sequence** causes the Actor to spawn and despawn for the duration of the master sequence, if one is being used. This causes the Actor to be spawned and destroyed outside the bounds of the current sequence.
-   **External** causes the Actor to spawn at the start of the sequence, but it will not be destroyed at the end. You can instead destroy the Actor through Blueprints by using **[Sequencer Tags and Groups](/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine)**.



 |
| **Spawnable Level** | 

Specifies which Level the Actor will spawn into. This list is determined by what Levels exist in your **[Levels](/documentation/en-us/unreal-engine/levels-in-unreal-engine)** window.

You cannot specify the World Partition or Data Layers.



 |
| **Change Class** | This option provides a way to change which class is being spawned, while preserving any Sequencer tracks already added to this Spawnable. This does not preserve any non-Sequencer data such as object properties. |
| **Continuously Respawn** | When enabled, the Actor is checked every tick to ensure that it still exists (based on the status of the Spawn track). The Actor respawns in the event that an external destroy event did destroy it. |
| **Evaluate Tracks When Not Spawned** | When enabled, all tracks from this Actor will still be evaluated even if the Actor is not spawned. This is useful if the Actor requires any preprocessing before being spawned. |
| **Net Addressable** | When enabled, this Spawnable Actor will be spawned using a unique name that allows it to be referenced by the server and client. |
| **Save Default State** | Saves the current state of this Spawnable Actor. Typically, you don't need to click this as Unreal Engine will attempt to automatically save any changes to the Spawnable Actor. |
| **Convert to Possessable** | Converts the Actor to a Possessable Actor. When this occurs, the Actor is re-created in your Level and the Actor track binds to it, removing the Spawnable Actor. |

## Workflows

Spawnable Actors helps you create more organized scenes in terms of content organization and management.

### Lighting Scenes

Instead of placing several lights in your Level that have to be manually enabled or disabled per shot, you can add the required lights to your shot as Spawnable Actors. They will exist only for that shot and don't clutter your Level with unnecessary lights.

![Lighting scenes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f014e8c1-c3ff-4767-809d-e4b08ae66277/lighting_scenes.png)

This workflow can also be used for any temporary Actor, such as particles so that it can create an instance of it.