# Audio

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:08:59

---

## Audio

### Dialogue

| **Section** | **Description** |
| --- | --- |
| **Dialogue Filename Format** | 
The format string to use when generating the filename for contexts within dialogue waves.

This must generate unique names for your project.

Available format markers:

-   **{DialogueGuid}**: The GUID of the dialogue wave. Guaranteed to be unique and stable against Asset renames.
    
-   **{DialogueHash}**: The hash of the dialogue wave. Not guaranteed to be unique or stable against Asset renames, however may be unique enough if combined with the dialogue name.
    
-   **{DialogueName}**: The name of the dialogue wave. Not guaranteed to be unique or stable against Asset renames, however may be unique enough if combined with the dialogue hash.
    
-   **{ContextId}**: The ID of the context. Guaranteed to be unique within its dialogue wave. Not guaranteed to be stable against changes to the context.
    
-   **{ContextIndex}**: The index of the context within its parent dialogue wave. Guaranteed to be unique within its dialogue wave.
    



 |

### Audio

| **Section** | **Description** |
| --- | --- |
| **Default Sound Class** | The `SoundClass` assigned to newly created sounds. |
| **Default Media Sound Class** | The `SoundClass` assigned to media player Assets. |
| **Default Sound Concurrency** | The `SoundConcurrency` assigned to newly created sounds. |
| **Default Base Sound Mix** | The `SoundMix` to use as base when no other system has specified a Base Sound Mix. |
| **VOIP Sound Class** | Sound class to be used for the VOIP audio component. |
| **VOIP Sample Rate** | 
Sample rate used for Voice Over IP (VOIP).

VOIP audio is resampled to the application's sample rate on the receiver side.

You can choose from the following options:

-   **Low 16000 Hz**
    
-   **Normal 24000 Hz**
    



 |
| **Maximum Concurrent Streams** | Defines how many streaming sounds can be played at the same time (if more are played, they will be sorted by priority). |
| **Global Min Pitch Scale** | The value to use to clamp the minimum pitch scale. |
| **Global Max Pitch Scale** | The value to use to clamp the maximum pitch scale. |

### Mix

| **Section** | **Description** |
| --- | --- |
| **Master Submix** | 
The default submix through which all sounds are routed to.

The root submix that outputs to audio hardware.



 |
| **Reverb Submix** | The submix through which all sounds set to use reverb are routed. |
| **Default Audio Buses** | Array of `AudioBuses` that are automatically initialized when the `AudioEngine` is initialized. |
| **Base Default Submix** | The default submix the audio engine uses when no submix is specified during a Submix Send. |
| **EQ Submix (Legacy)** | The submix through which all sounds set to use the legacy equalizer (EQ) system are routed |

### Quality

| **Section** | **Description** |
| --- | --- |
| **Quality Levels** | The quality levels of the audio. |
| **Allow Play when Silent** | Allows sounds to play at 0 volume. |
| **Disable Master EQ** | Disables master EQ effect in the audio DSP graph. |
| **Allow Center Channel 3DPanning** | Enables the surround sound spatialization calculations to include the center channel. |
| **Num Stopping Sources** | 
The maximum number of sources to reserve for "stopping" sounds.

A "stopping" sound applies a fast fade in the DSP render to prevent discontinuities when stopping sources.



 |
| **Panning Method** | 

The method to use when doing non-binaural or object-based panning.

You can choose from the following options:

-   **Linear**
-   **Equal Power**



 |
| **Mono Channel Upmix Method** | 

The upmixing method for mono sound sources.

Defines how mono channels are upmixed to stereo channels.

You can choose from the following options:

-   **Linear**
-   **Equal Power**
-   **Full Volume**



 |

### Debug

| **Section** | **Description** |
| --- | --- |
| **Debug Sounds** | A list of sounds that should only be packaged in non-shipping builds, typically intended for debugging purposes. |