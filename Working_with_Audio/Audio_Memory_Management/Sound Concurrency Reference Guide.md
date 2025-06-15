# Sound Concurrency Reference Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sound-concurrency-reference-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/sound-concurrency-reference-guide)  
**Processed:** 2025-06-14 16:51:27

---

Playing too many sounds at the same time can result in high resource consumption and poor performance. **Sound Concurrency** assets are one of the primary tools you can use to handle that problem. With a Sound Concurrency asset, you can limit how many sounds play simultaneously and what to do when that limit is reached. You can assign these rules to individual sounds, groups of sounds, or all sounds within a project.

### Creating Sound Concurrency Assets

You can create a Sound Concurrency by clicking the **Add** button in the **Content Browser** and selecting **Audio > Sound Concurrency**.

### Editing Sound Concurrency Assets

![Details Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9df54e47-7802-48d7-8161-7e9f93eee444/details_panel.png)

You can edit the properties of the Sound Concurrency by double-clicking it in the **Content Browser**, or by right-clicking it and selecting **Edit…** from the context menu. A **Details** panel for the asset will appear.

#### Details

##### Concurrency

| Property | Description |
| --- | --- |
| **Max Count** | The maximum number of concurrently active sounds allowed in this group before the **Resolution Rule** takes effect. |
| **Limit to Owner** | If enabled, limits these concurrency rules to each actor that plays the sound. |
| **Resolution Rule** | 
Sets the behavior to follow when **Max Count** has been reached:

-   **Prevent New**: Prevent any new sounds from starting.
-   **Stop Oldest**: Stop the oldest playing sound.
-   **Stop Farthest Then Prevent New**: Stop the farthest sound. If all sounds are the same distance, prevent new sounds from starting.
-   **Stop Farthest Then Oldest**: Stop the farthest sound. If all sounds are the same distance, stop the oldest sound instead.
-   **Stop Lowest Priority**: Stop the lowest priority sound. If all sounds have the same priority, stop the oldest sound instead.
-   **Stop Quietest**: Stop the quietest sound.
-   **Stop Lowest Priority Then Prevent New**: Stop the lowest priority sound. If all sounds have the same priority, prevent new sounds from starting.



 |
| **Retrigger Time** | The wait time (in seconds) between playing sounds. The sounds rejected by this setting ignore virtualization settings. |

All active components count towards **Max Count**, not just actively playing sounds. This can affect systems that can remain active without playing any audio, such as synthesizers. It can also affect **Source Buses** as they take up two spots within your **Max Count**: one for the original source and one for the bus. This is true even if the source is set to **Output to Bus Only** because it is still an active component.

##### Volume Scaling

| Property | Description |
| --- | --- |
| **Can Recover** | If enabled, allows volume scaling to recover to its default value after all sounds in the group have stopped playing. |
| **Volume Scale** | The scaling factor (ducking) applied to older sounds, which compounds based on the **Volume Scale Mode**. |
| **Volume Scale Mode** | 
Sets the volume scaling behavior to use based on the attributes of the active sounds in the group:

-   **Default**: Scale older sounds more than newer sounds.
-   **Distance**: Scale distant sounds more than closer sounds.
-   **Priority**: Scale lower priority sounds more than closer sounds.



 |
| **Duck Time** | The time (in seconds) to duck using the **Volume Scale**. |
| **Recover Time** | The time (in seconds) to recover from volume scaling. |

To avoid thrashing sounds, **Volume Scale** is applied after **Stop Quietest** rules are evaluated.

##### Voice Stealing

| Property | Description |
| --- | --- |
| **Voice Steal Release Time** | The fade-out time (in seconds) used if a sound is stopped due to another sound in the group starting. |

### Setting Sound Concurrency Assets

#### In Project Settings

![Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e859cca4-2007-4593-ad0c-cc99bfdd19a1/project_settings.png)

You can set a Sound Concurrency as the default for all sound sources in the **Project Settings**.

To assign a project default Sound Concurrency:

1.  Go to **Edit > Project Settings…** to open the **Project Settings** panel.
2.  On the left side of the panel, click **Audio** under the Engine heading.
3.  Click the **Default Sound Concurrency** dropdown and select the Sound Concurrency to use.

#### On Source Assets

![Concurrency Set](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f42de647-692b-4435-9554-7b148c6041ba/concurrency_set.png)

You can also set Sound Concurrency assets directly on sound source assets, such as **MetaSounds**, **Sound Cues**, and **Sound Waves**.

To assign a Sound Concurrency to a sound source:

1.  Open the sound source's **Details** panel.
2.  Find **Voice Management > Concurrency > Concurrency Set** in the **Details** panel
3.  Click the **Add** button to add an index to the **Concurrency Set**.
4.  Click the dropdown for the new index and select the Sound Concurrency to use.

You can use the same Sound Concurrency across multiple sound source assets. If you do so, the properties and state of the Sound Concurrency are shared between the sources.

You can specify multiple Sound Concurrency assets within a **Concurrency Set**. The source must fulfill all of the rules in the set before it can play.

If a **Concurrency Set** has multiple Sound Concurrency assets with fulfilled rules that stop active sounds, one sound per group will be stopped to make room for the new sound.

![Override Concurrency](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f91a237-dcf2-477d-9a99-53303b6529d3/override_concurrency.png)

You can also enable the **Override Concurrency** option and use the properties under **Concurrency Overrides** to specify behavior for an individual sound asset without creating a Sound Concurrency asset.