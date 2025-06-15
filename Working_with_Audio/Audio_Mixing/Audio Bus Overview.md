# Audio Bus Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-bus-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-bus-overview)  
**Processed:** 2025-06-14 16:08:34

---

In **Unreal Engine**, **Audio Buses** combine sound sources into a single signal path.

You can use the combined audio signal in two primary ways:

-   Use the signal to perform audio-rate modulation on parameters or other signals. For example, use it to dynamically control digital signal process (DSP) effect parameters (known as sidechaining).
-   Output the mixed audio signal from a point in space. In particular, using the rendered output, create speakers or other audio-producing objects within your Level.

### Creating Audio Buses

To create an Audio Bus:

1.  In the **Content Browser**, click the **Add** button.
2.  Select **Audio > Mix > Audio Bus**.

![Audio Bus Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8a408f4-f9ea-4c6f-9bc3-575b33661a89/audio_bus_details.png)

To edit an Audio Bus, you can double-click it in the **Content Browser** or right-click it and select **Edit** from the context menu. Then, in the **Details** panel that appears, set the number of **Audio Bus Channels** you want to use.

If you send audio to an Audio Bus with a different channel configuration, it will be mixed accordingly. For example, sending a mono source to a stereo Audio Bus will upmix to stereo.

### Sending Audio to Audio Buses

![Audio Bus Project Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7ac4fcd-a48d-47b6-a214-8cb90ef57116/audio_bus_project_settings.png)

You have to start an Audio Bus before it can receive audio. Set the **Default Audio Buses** in the [**Project Settings**](/documentation/en-us/unreal-engine/audio-settings-in-the-unreal-engine-project-settings) to have the specified Audio Buses start automatically.

You can also start an Audio Bus manually by using the **Start Audio Bus** Blueprint node. Similarly, you can stop an Audio Bus by using the **Stop Audio Bus** Blueprint node.

![Source Details Bus Sends](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0752a55e-7e9d-4e8e-a2ba-03b4bd160126/source_details_bus_sends.png)

You can set an Audio Bus to send audio to in the **Details** panel for your source asset (such as a **Sound Wave**, **Sound Cue**, or **MetaSound Source**). Under **Effects > Source**, click the **Add (+)** button for **Post-Effect Bus Sends** or **Pre-Effect Bus Sends** to add a bus send that will occur before or after an optionally provided **Source Effect Chain**.

![Source Details Audio Bus](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da43d907-e893-47eb-a743-db3a807230c8/source_details_audio_bus.png)

Expand the new bus send index to set the **Audio Bus** and the **Send Level**.

You can change the **Source Bus Send Level Control Method** (in combination with the other related properties) to send based on distance or a custom curve.

![Source Details Submix](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc8a6e43-8ca9-4081-9471-3efb9c78e10f/source_details_submix.png)

If you want the original source audio to be inaudible (by only sending it to the Audio Bus), you can disable **Enable Base Submix** and **Enable Submix Sends** under **Source > Submix** in the **Details** panel.

### Audio-Rate Modulation with Audio Buses

![Source Effects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccce9ec2-d83b-4801-b2f9-009991ab70a8/source_effects.png)

Modulation is the process of using a signal to alter other audio signals or parameters of a sound. You can modulate at an audio rate using Audio Buses.

By default, two **Source Effect Preset** classes allow for audio-rate modulation with an Audio Bus:

-   **Filter**: The Audio Bus signal controls the filter frequency cutoff.
-   **Ring Modulation**: The Audio Bus signal is multiplied by the input signal.

To create a Source Effect Preset:

1.  In the **Content Browser**, click the **Add** button.
2.  Select **Audio > Effects > Source Effect Preset**.
3.  Choose from the list of classes available in the **Pick Source Effect Class** window.

![Filter Preset Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f04d7078-ca9c-45fe-8775-0ce6314b8b04/filter_preset_details.png)

You can set the Audio Bus you want to modulate with in the **Details** panel for the Source Effect Preset.

After you create a Source Effect Preset, you must add it to a **Source Effect Preset Chain**.

To create a Source Effect Preset Chain:

1.  In the **Content Browser**, click the **Add** button.
2.  Select **Audio > Effects > Source Effect Preset Chain**.

![Source Effect Chain Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e0125c8-d638-42e2-93d8-639c66eb17e4/source_effect_chain_details.png)

You can set the Source Effect Presets you want to use in the Source Effect Preset Chain's **Details** panel.

![Source Effect Chain Set](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9da53f4d-b9c0-4116-983c-14b0455daac4/source_effect_chain_set.png)

After you configure a Source Effect Preset Chain, you can set it in the **Source > Source Effects Chain** property in a source's **Details** panel. The Source Effects Preset Chain specified will take effect after any bus sends in the **Pre-Effect Bus Sends** and before any bus sends in the **Post-Effect Bus Sends**.

### Outputting Audio from Audio Buses

By default, Audio Buses are not audible. To output Audio Bus audio, you must use a **Source Bus** or **MetaSound Source**.

#### Source Buses

A Source Bus renders the output of an Audio Bus. Source Buses can use sound source features, such as spatialization, attenuation, and concurrency resolution. They can even output audio to other Audio Buses and Source Buses.

Source Buses only support **Mono** or **Stereo**. Use a MetaSound Source to support additional channel configurations.

To create a Source Bus:

1.  In the **Content Browser**, click the **Add** button.
2.  Select **Audio > Source > Source Bus**.

![Source Bus Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/64b5a747-33c2-4cca-ace4-06e94636bc7d/source_bus_details.png)

Set the Audio Bus you want to render in the Source Bus **Details** panel. Additionally, you can select the number of **Source Bus Channels** and the **Source Bus Duration**.

If the **Source Bus Duration** is set to 0, the Source Bus will play indefinitely. Use any positive value to create a one-shot sound source that will stop after the duration.

#### MetaSound Sources

You can also render Audio Bus audio by using a MetaSound Source. On the MetaSound graph, use an **Audio Bus Reader** node to read in Audio Bus data, then attach it to the corresponding outputs.

In addition to mono and stereo, you can produce quad, 5.1, and 7.1 audio with a MetaSound Source by setting the **Output Format** accordingly.

For more information on MetaSounds, see the [MetaSounds documentation](/documentation/en-us/unreal-engine/metasounds-in-unreal-engine).

### Audio Buses vs. Submixes

Audio Buses are comparable to **Submixes** but differ in several important ways:

-   They don't have graphs.
-   Their audio is not audible by default.
-   They provide a way to define spatialization behavior.
-   They can't have DSP effects applied to them directly.
-   They only use CPU resources when receiving source audio.

See [Submixes Overview](/documentation/en-us/unreal-engine/overview-of-submixes-in-unreal-engine) for more information on Submixes.