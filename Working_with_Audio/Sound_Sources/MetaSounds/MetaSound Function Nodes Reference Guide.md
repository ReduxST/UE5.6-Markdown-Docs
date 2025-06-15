# MetaSound Function Nodes Reference Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/metasound-function-nodes-reference-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/metasound-function-nodes-reference-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:35:59

---

MetaSound **Function** nodes come in many types and provide the functionality required to play audio files, mix sounds, apply filters and effects, and more. This document contains a list of function nodes with detailed information on each.

For more detailed information on the features available in MetaSounds, see [MetaSounds Reference Guide](/documentation/en-us/unreal-engine/metasounds-reference-guide-in-unreal-engine).

## General

### BPM To Seconds

![BPM To Seconds](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/766900e0-73ff-499b-bcc6-8a41a29c8b3f/general_bpm_to_seconds.png)

The **BPM To Seconds** node calculates a beat time in seconds from the given beats per minute (BPM), beat multiplier, and divisions of a whole note.

#### BPM To Seconds Inputs

| Input | Description |
| --- | --- |
| **BPM** | The input target BPM. |
| **Beat Multiplier** | The multiplier value to apply to the BPM. |
| **Division of Whole Note** | The divisions of a whole note. |

#### BPM To Seconds Outputs

| Output | Description |
| --- | --- |
| **Seconds** | The output beat time in seconds. |

### Envelope Follower

![Envelope Follower](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad1e6458-0352-4ef8-a15c-626d322f57e5/general_envelope_follower.png)

The **Envelope Follower** node outputs an envelope from an input audio signal.

#### Envelope Follower Inputs

| Input | Description |
| --- | --- |
| **In** | The input audio signal. |
| **Attack Time** | The attack time (in seconds). |
| **Release Time** | The release time (in seconds). |
| **Peak Mode** | 
The following-method of the envelope follower:

-   **MS**: Envelope follows a running Mean Squared of the audio signal.
-   **RMS**: Envelope follows a running Root Meat Squared of the audio signal.
-   **Peak**: Envelope follows the peaks in the audio signal.



 |

#### Envelope Follower Outputs

| Output | Description |
| --- | --- |
| **Envelope** | The output envelope value (block rate). |
| **Audio Envelope** | The output envelope value (audio rate). |

### Flanger

![Flanger](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef536cf4-0ef6-4e0f-bfcc-24f27e5b8bde/general_flanger.png)

The **Flanger** node applies a flanger effect to the input audio.

#### Flanger Inputs

| Input | Description |
| --- | --- |
| **In Audio** | The input audio signal to apply the flanger effect to. |
| **Modulation Rate** | The Low-Frequency Oscillator (LFO) rate that varies the delay time (in Hz). This value is clamped at block rate. |
| **Modulation Depth** | The LFO amplitude (strength) that scales the delay time. |
| **Center Delay** | The center delay amount (in milliseconds). |
| **Mix Level** | The balance between original and delayed signal. The value should be between 0 and 1.0. For example, a value of 0.5 uses equal amounts of each signal and a value greater than 0.5 uses more delayed signal than non-delayed signal. |

#### Flanger Outputs

| Output | Description |
| --- | --- |
| **Out Audio** | The output audio signal with the flanger effect applied. |

### Get WaveTable From Bank

![Get WaveTable From Bank](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22f98b23-4f5c-4341-ac5c-bed3a922ced4/general_get_wavetable_from_bank.png)

The **Get WaveTable From Bank** node retrieves (or generates an interpolated) WaveTable from a given WaveTable Bank asset.

#### Get WaveTable From Bank Inputs

| Input | Description |
| --- | --- |
| **WaveTableBank** | The WaveTable Bank asset to retrieve or generate an interpolated WaveTable from. |
| **TableIndex** | The index of the WaveTable to retrieve. If set between two whole values, the WaveTables located at the two closest indices are mixed together. The value will be adjusted to loop if it is set beyond the range of the WaveTable Bank. For example, if the WaveTable Bank has 3 indices, a value of 3.0 will retrieve the WaveTable at index 0. |

#### Get WaveTable From Bank Outputs

| Output | Description |
| --- | --- |
| **Out** | The retrieved WaveTable. |

### InterpTo

![InterpTo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/144bc0cc-d5c1-4f7d-95d6-5ae2955912d4/general_interpto.png)

The **InterpTo** node interpolates between the current value and a target value over a specified time.

#### InterpTo Inputs

| Input | Description |
| --- | --- |
| **Interp Time** | The time to interpolate from the current value to the target value. |
| **Target** | The value to interpolate to. |

#### InterpTo Outputs

| Output | Description |
| --- | --- |
| **Value** | The current value. |

### RingMod

![RingMod](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/963f1612-e05e-41d2-92c1-2db7d8d50bcf/general_ringmod.png)

The **RingMod** node performs ring modulation with a carrier signal and a modulator signal.

#### RingMod Inputs

| Input | Description |
| --- | --- |
| **In Carrier** | The carrier audio signal. |
| **In Modulator** | The modulator audio signal. |

#### RingMod Outputs

| Output | Description |
| --- | --- |
| **Out Audio** | The modulated audio signal. |

### Wave Player

![Wave Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6cb3117-7e86-4d67-9c16-213141214f78/general_wave_player.png)

The **Wave Player** node is used to play a Sound Wave asset. There are multiple versions of this node in order to support several different channel configurations, such as Mono, Stereo, Quad (4.0), 5.1, and 7.1.

#### Wave Player Inputs

| Input | Description |
| --- | --- |
| **Play / Stop** | The Play and Stop triggers start and stop the Wave Player playback at a sample-accurate moment in time. |
| **Wave Asset** | The Sound Wave asset played by the Wave Player during playback. This asset uses the same real-time decoders as all other sound sources in Unreal Engine. |
| **Start Time** | The time within the Sound Wave asset to begin playing the audio file. This is also referred to as seek time. |
| **Pitch Shift** | The Pitch Shift to use for the Wave Player. This is defined in units of semitones to account for the non-linear nature of frequency scaling. |
| **Loop** | Whether the Wave Player will loop the audio file or stop when it's finished. This can be toggled at any time during playback from the graph. |
| **Loop Start** | The Loop Start indicates at which point in time the Wave Player will loop the audio file. |
| **Loop Duration** | The Loop Duration represents the total time the loop will play. Any value other than -1 sets the end point of the loop to the sum of the Loop Start and Loop Duration values, while a value of -1 loops the entire audio file. |

#### Wave Player Outputs

| Output | Description |
| --- | --- |
| **On Play** | Triggers when the Wave Player's Input Play pin is triggered. |
| **On Finished** | Triggers when the Wave Player finishes playing the audio file. This pin will trigger on the same sample point where the audio file finishes playing. |
| **On Nearly Finished** | Triggers on the audio rendering block before the audio file is expected to finish playback. This is commonly used to loop back and pick a new audio file variation for the Wave Player. |
| **On Looped** | Triggers on the sample where a sound looped based on the looping settings. |
| **On Cue Point** | 
Triggers when a cue point has been parsed in the Wave Player. Cue points are metadata embedded in audio wave files on import.

Cue points are often used by sound designers to trigger events or loop points in their audio at exact points in time. With this feature, sound designers can procedurally trigger MetaSound behavior based on embedded data in the imported audio wave file.

This pin is executed with sample accuracy, but the integer and label associated with the cue point is read at the block rate. Cue points in the audio wave file that are closer together than the block rate of the MetaSound will only trigger on the last cue point in that block.



 |
| **Cue Point ID** | The ID of the cue point as parsed from the imported audio wave file. |
| **Cue Point Label** | The label of the cue point as parsed from the imported audio wave file. |
| **Loop Percent** | The current location in the audio wave file within the given loop region. |
| **Playback Location** | The current location in the audio wave file as a fraction of the total length of the audio wave file. |
| **Out X** | The X channel output of the input Sound Wave asset. |

In the case of mono file playback, the audio in the right and left channels are up-mixed using mono-channel duplication.

### WaveShaper

![WaveShaper](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c76e8bd7-fa74-4a23-a4a6-81b399d1fa28/general_waveshaper.png)

The **WaveShaper** node applies a non-linear shaping to the input audio signal.

#### WaveShaper Inputs

| Input | Description |
| --- | --- |
| **In** | The input audio signal to apply the non-linear shaping to. |
| **Amount** | The amount of the non-linear wave shaping to apply. |
| **Bias** | The DC offset to apply before wave shaping. |
| **OutputGain** | The amount of gain to apply after processing. |
| **Type** | The type of algorithm to use to process the audio: **Sine**, **Inverse Tangent**, **Hyperbolic Tangent**, **Cubic Polynomial**, or **Hard Clip** |

#### WaveShaper Outputs

| Output | Description |
| --- | --- |
| **Out** | The output audio signal with the non-linear shaping applied. |

## Array

**Array** functions provide options to manipulate arrays within a MetaSound. Each of these functions have different versions which allows them to support arrays of several common data types, including: Bool, Float, Int32, String, Time, Transmission:Address, AudioBusAsset, WaveTableBankAsset, and WaveAsset.

### Concatenate

![Concatenate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0a490af9-dcf7-4b13-a189-af1248743e44/array_concatenate.png)

The **Concatenate** node concatenates two arrays on a given trigger.

#### Concatenate Inputs

| Input | Description |
| --- | --- |
| **Trigger** | The trigger on which to concatenate the input arrays. |
| **Left / Right Array** | The input arrays. |

#### Concatenate Outputs

| Output | Description |
| --- | --- |
| **Array** | The concatenated array. |

### Get

![Get](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c1e7f2b-9ff3-4f83-a02e-7274c90ed625/array_get.png)

The **Get** node retrieves an element from an array at the given index.

You can use the **Get Last Index** node instead to access the last index of an array.

#### Get Inputs

| Input | Description |
| --- | --- |
| **Trigger** | The trigger on which to retrieve the specified array element. |
| **Array** | The array from which to retrieve an element. |
| **Index** | The index of the element to retrieve. |

#### Get Outputs

| Output | Description |
| --- | --- |
| **Element** | The value of the retrieved element. |

### Num

![Num](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/99ff0705-125d-425b-a432-1911f4c2e2d0/array_num.png)

The **Num** node returns the number of elements in the given array.

#### Num Inputs

| Input | Description |
| --- | --- |
| **Array** | The array whose elements will be counted. |

#### Num Outputs

| Output | Description |
| --- | --- |
| **Num** | The number of elements in the given array. |

### Random Get

![Random Get](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0962e4e5-d155-4a58-b568-2cd73e7cf9fc/array_random_get.png)

The **Random Get** node randomly retrieves elements from an input array. Optionally, an array of weights can be supplied to adjust the randomness.

#### Random Get Inputs

| Input | Description |
| --- | --- |
| **Next** | The trigger on which to get the next random value in the array. |
| **Reset** | The trigger on which to reset the randomization seed for the array. |
| **In Array** | The input array from which to randomly retrieve elements. |
| **Weights** | (Optional) An input array of weights used to define the probability of each entry retrieved. If not provided, an even probability for all elements is assumed. If this array is shorter than the input array, it is repeated to match the size. |
| **Seed** | The seed used for the random shuffle. The default value of -1 will use the current time. |
| **No Repeats** | The number of elements to track to avoid repeating in a row. For example, a value of 2 prevents this node from repeating the last two selected elements. |
| **Enabled Shared State** | If enabled, this node's state is shared across instances of this MetaSound to avoid playing the same exact variations at the same time. |

#### Random Get Outputs

| Output | Description |
| --- | --- |
| **On Next** | Triggers when the Next input is triggered. |
| **On Reset** | Triggers when the Shuffle input is triggered or if the array is auto-shuffled. |
| **Value** | The randomly-selected value from the input array. |

### Set

![Set](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b02f804-5ac8-469a-8b22-d1a15ce3946b/array_set.png)

The **Set** node sets the value of a specified index in a given array.

#### Set Inputs

| Input | Description |
| --- | --- |
| **Trigger** | The trigger on which to set value in the array. |
| **Array** | The array in which a value will be set. |
| **Index** | The index to set in the target array. |
| **Value** | The value to which the selected index is set. |

#### Set Outputs

| Output | Description |
| --- | --- |
| **Array** | The array after the setting operation is completed. |

### Shuffle

![Shuffle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad207466-ce3c-4b1b-bfd9-208d428f5394/array_shuffle.png)

The **Shuffle** node outputs elements from a shuffled array.

#### Shuffle Inputs

| Input | Description |
| --- | --- |
| **Next** | The trigger on which to get the next value in the shuffled array. |
| **Shuffle** | The trigger on which to shuffle the array manually. |
| **Reset Seed** | The trigger on which to reset the random seed stream. |
| **In Array** | The array from which to shuffle and output elements. |
| **Seed** | The seed used for the random shuffle. The default value of -1 uses the current time. |
| **Auto Shuffle** | If enabled, automatically shuffles when the array has been read completely. |
| **Enabled Shared State** | If enabled, the state is shared across instances of this MetaSound. |

#### Shuffle Outputs

| Output | Description |
| --- | --- |
| **On Next** | Triggers when the Next input is triggered. |
| **On Shuffle** | Triggers when the Shuffle input is triggered or if the array is auto-shuffled. |
| **On Reset Seed** | Triggers when the Reset Seed input is triggered. |
| **Value** | The value of the currently-selected element. |

### Subset

![Subset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8ff7c39-576d-42d5-8a80-49e021de9df0/array_subset.png)

The **Subset** node returns a subset of an input array.

#### Subset Inputs

| Input | Description |
| --- | --- |
| **Trigger** | The trigger on which to generate a subset. |
| **Array** | The input array from which to get a subset. |
| **Start / End Index** | The first and last indices to include in the subset. |

#### Subset Outputs

| Output | Description |
| --- | --- |
| **Array** | The subset of the input array. |

## Debug

### Get Wave Info

The **Get Wave Info** node returns the info from the Wave Asset.

#### Get Wave Info Inputs

| Input | Description |
| --- | --- |
| **Wave** | The input Wave Asset. |

#### Get Wave Info Outputs

| Output | Description |
| --- | --- |
| **Duration** | The duration of the Wave Asset (in seconds). |
| **Name** | The name of the Wave Asset. |
| **Path** | The full path of the Wave Asset. |

### Print Log

![Print Log](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc3f5860-0040-404d-ad59-d50f7747fb75/debug_print_log.png)

The **Print Log** node is used to record values to the Output Log on a given trigger for debugging purposes. There are multiple versions of this node in order to support several common data types, including: Bool, Float, Int32, and String.

#### Print Log Inputs

| Input | Description |
| --- | --- |
| **Trigger** | The trigger on which to write the set value to the log. |
| **Label** | The label to attach to the value logged. |
| **Value To Log** | The value to record to the log when triggered. |

## Delays

### Delay

![Delay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/77d4b8dd-884b-493f-b6a1-49dc00b1cdb6/delays_delay.png)

The **Delay** node provides a mono buffer delay that supports dry level, wet level, and feedback. For multi-channel buffer delay, use the **Stereo Delay** node.

#### Delay Inputs

| Input | Description |
| --- | --- |
| **In** | The audio signal to apply delay to. |
| **Delay Time** | The amount of time to delay the audio (in seconds). |
| **Dry Level** | The level for the unprocessed (dry) signal |
| **Wet Level** | The level for the processed (wet) signal. |
| **Feedback** | The amount of feedback to use. |
| **Max Delay Time** | The amount of feedback to use. |

#### Delay Outputs

| Output | Description |
| --- | --- |
| **Out** | The delayed audio signal. |

### Delay Pitch Shift

![Delay Pitch Shift](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d74f05d8-705f-4f50-881f-ba318c1779fe/delays_delay_pitch_shift.png)

The **Delay Pitch Shift** node pitch shifts the audio buffer using a delay-based doppler-shift method. This allows for pitch shifting without changing the length of the audio file by using an internal delay buffer. The pitch will shift but the sound will not speed up or slow down.

#### Delay Pitch Shift Inputs

| Input | Description |
| --- | --- |
| **In** | The audio buffer to process. |
| **Pitch Shift** | The amount of pitch shift (in semitones) to apply. |
| **Delay Length** | The amount of delay (between 10 and 100 milliseconds) to apply. Changing this value can reduce artifacts in certain pitch shift regions. |

#### Delay Pitch Shift Outputs

| Output | Description |
| --- | --- |
| **Out** | The processed audio buffer. |

### Diffuser

![Diffuser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82de584c-1d1a-4f75-8974-10bb7be280d7/delays_diffuser.png)

The **Diffuser** node applies diffusion to the incoming audio.

#### Diffuser Inputs

| Input | Description |
| --- | --- |
| **Input Audio** | The audio to apply diffusion to. |
| **Depth** | The number of filters to use to diffuse the audio (between 1 and 5). This will not update while running. |
| **Feedback** | The amount of feedback to use on each diffuser (between 0 and 1). |

#### Diffuser Outputs

| Output | Description |
| --- | --- |
| **Output Audio** | The diffused audio. |

### Grain Delay

![Grain Delay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc747003-597d-4428-827c-fe440ae1c7c5/delays_grain_delay.png)

The **Grain Delay** node performs delayed audio granulation on a given audio buffer by sampling it into "grains" and playing them after a set delay.

#### Grain Delay Inputs

| Input | Description |
| --- | --- |
| **In Audio** | The audio buffer to be grain delayed. |
| **Grain Spawn** | The trigger on which to spawn a new grain of audio. |
| **Grain Delay** | The delay (in milliseconds, between 0 and 2000) of the next spawned grain. |
| **Grain Delay Range** | The range delta (in milliseconds) used to randomize the delay in relation to the central Grain Delay value. |
| **Grain Duration** | The duration (in milliseconds) of the next spawned grain. |
| **Grain Duration Range** | The range delta (in milliseconds) used to randomize the duration in relation to the central Grain Duration value. |
| **Pitch Shift** | The pitch value (in semitones) to change the grain pitch of all rendering grains. |
| **Pitch Shift Range** | The pitch shift delta (in semitones) used to randomize the pitch shift in relation to the central Pitch Shift value. |
| **Grain Envelope** | The type of envelope to use for the grains: **Gaussian**, **Triangle**, **Downward Triangle**, **Upward Triangle**, **Exponential Decay**, or **Exponential Attack** |
| **Max Grain Count** | The maximum number of grains to render at a time (between 1 and 100). |
| **Feedback Amount** | The amount of feedback of each grain. If feedback is applied, the grain delay will feed its audio output back into itself. |

The **Max Grain Count** input is CPU intensive, so setting it to high values can reduce performance and introduce clipping.

#### Grain Delay Outputs

| Output | Description |
| --- | --- |
| **Out Audio** | The grain-delayed audio buffer. |

### Stereo Delay

![Stereo Delay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39e9d2dc-ef54-4299-841a-fc9e7044a859/delays_stereo_delay.png)

The **Stereo Delay** node provides multi-channel buffer delay. Like the **Delay** node, which provides mono buffer delay, this node supports dry level, wet level, and feedback, but also supports additional delay modes.

#### Stereo Delay Inputs

| Input | Description |
| --- | --- |
| **In Left / Right** | The input audio signals (left / right channels) to apply delay to. |
| **Delay Mode** | 
The delay method to use:

-   **Normal**: The left input mixes with the left delay output and feeds to the left output.
-   **Cross**: The left input mixes with the right delay output and feeds to the right output.
-   **Ping Pong**: The left input mixes with the left delay output and feeds to the right output.



 |
| **Delay Time** | The amount of time to delay the audio (in seconds). |
| **Delay Ratio** | The ratio of delay to apply to the left and right channels. This means channels can have different delay amounts. For example, a value of -1 applies no delay to the left channel while fully delaying the right channel, which can be useful for stereo channel decorrelation. |
| **Dry Level** | The level for the unprocessed (dry) signal |
| **Wet Level** | The level for the processed (wet) signal. |
| **Feedback** | The amount of feedback to use. |

#### Stereo Delay Outputs

| Output | Description |
| --- | --- |
| **Out Left / Right** | The output audio signal (left / right channels). |

## Dynamics

### Compressor

![Compressor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14470962-6d71-4a04-92f1-f6387da7bd6d/dynamics_compressor.png)

The **Compressor** node lowers the dynamic range of an input audio signal.

#### Compressor Inputs

| Input | Description |
| --- | --- |
| **Audio** | The audio signal to compress. |
| **Ratio** | The ratio of gain reduction to apply. For example, a value of 1 produces no gain reduction and a value greater than 1 produces gain reduction. |
| **Threshold dB** | The amplitude threshold (in decibels) above which gain will be reduced. |
| **Attack Time** | The amount of time it takes for audio above the Threshold (dB) to reach its compressed volume level. |
| **Release Time** | The amount of time it takes for audio below the Threshold (dB) to return to its original volume level. |
| **Lookahead Time** | The amount of time it takes to delay the compressed signal behind the analyzed input signal. |
| **Knee** | A decibel value that determines how hard or soft the gain reduction blends. A value of 0 dB provides no blending. |
| **Sidechain** | (Optional) An external audio signal to control the compressor with. If unset, the input audio signal is used. |
| **Envelope Mode** | 
The envelope-following method the compressor will use for gain detection:

-   **MS**: Envelope follows a running Mean Squared of the audio signal.
-   **RMS**: Envelope follows a running Root Meat Squared of the audio signal.
-   **Peak**: Envelope follows the peaks in the audio signal.



 |
| **Analog Mode** | If enabled, use Analog Mode for the compressor's envelope follower. |
| **Upwards Mode** | If enabled, an upwards compressor is used instead of the standard downwards compressor. |
| **Wet/Dry** | The ratio between the processed (wet) and the unprocessed (dry) signal. For example, a value of 0 is fully dry and a value of 1 is fully wet. |

#### Compressor Outputs

| Output | Description |
| --- | --- |
| **Audio** | The output audio signal with the compressor effect applied. |
| **Gain Envelope** | The amount of gain applied to the signal. |

### Decibels to Linear Gain

![Decibels to Linear Gain](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2a796d11-e400-4c50-97d3-87a63db8fde7/dynamics_decibels_to_linear_gain.png)

The **Decibels to Linear Gain** node converts a logarithmic (dB) gain value to a linear gain value.

#### Decibels to Linear Gain Inputs

| Input | Description |
| --- | --- |
| **Decibels** | The input logarithmic (dB) gain value. |

#### Decibels to Linear Gain Outputs

| Output | Description |
| --- | --- |
| **Linear Gain** | The output linear gain value. |

### Limiter

![Limiter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc8de412-134e-4735-9315-e1457689eb36/dynamics_limiter.png)

The **Limiter** node prevents a signal from going above a given threshold.

#### Limiter Inputs

| Input | Description |
| --- | --- |
| **Audio** | The input audio signal to be limited. |
| **Input Gain dB** | The amount of gain (in decibels) to apply to the input before limiting. |
| **Threshold dB** | The amplitude threshold (in decibels) above which gain will be reduced. |
| **Release Time** | The time it takes for audio below the threshold to return to its original volume level. |
| **Knee** | The knee mode determines if the gain reduction blends are **Hard** or **Soft**. |

#### Limiter Outputs

| Output | Description |
| --- | --- |
| **Audio** | The limited audio signal. |

### Linear Gain to Decibels

![Linear Gain to Decibels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb8020f0-7195-4975-8a01-993270db13e9/dynamics_linear_gain_to_decibels.png)

The **Linear Gain to Decibels** node converts a linear gain value to a logarithmic (dB) gain value.

#### Linear Gain to Decibels Inputs

| Input | Description |
| --- | --- |
| **Linear Gain** | The input linear gain value. |

#### Linear Gain to Decibels Outputs

| Output | Description |
| --- | --- |
| **Decibels** | The output logarithmic (dB) gain value. |

## Envelopes

MetaSounds provide **Envelope** nodes so audio designers can change aspects of their sounds over time. With the exception of the **WaveTable Envelope** and **Evaluate WaveTable** nodes, each type of Envelope node has two different versions to support Audio (audio-rate) and Float (block-rate) data types.

Audio designers can customize their curve values using the various curve values contained within the nodes. For attack-time values, a curve value of less than 1.0 is a logarithmic curve (which rises quickly at first and slower near the end), and a value greater than 1.0 is an exponential curve (rises slower at first and more quickly near the end). Decay and release curves have the opposite behavior. Values of 1.0 for these curves are linear curves.

### AD Envelope

![AD Envelope](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ee8c8d4-3943-4798-bd4f-cb0f0f22359b/envelopes_ad_envelope.png)

The **AD Envelope** node generates an attack-decay envelope value output when triggered.

This node provides an additional option for looping the Attack-Decay curve similarly to a Low Frequency Oscillator (LFO) or Wave Generator. When paired with a **Map Range** node, this can be used to great effect in a variety of applications.

#### AD Envelope Inputs

| Input | Description |
| --- | --- |
| **Trigger** | The trigger on which to start the attack phase of the envelope generator. |
| **Attack Time** | The amount of time (in seconds) to reach the maximum envelope value (1.0). |
| **Delay Time** | The amount of time (in seconds) to reach the minimum envelope value (0.0). |
| **Attack Curve** | The exponential curve factor of the attack phase. For example, a value of 1.0 produces linear growth, a value less than 1.0 produces logarithmic growth, and a value greater than 1.0 produces exponential growth. |
| **Decay Curve** | The exponential curve factor of the decay phase. For example, a value of 1.0 produces linear decay, a value greater than 1.0 produces logarithmic decay, and a value less than 1.0 produces exponential decay. |
| **Looping** | If enabled, the envelope will loop. |

#### AD Envelope Outputs

| Output | Description |
| --- | --- |
| **On Trigger** | Triggers when the envelope is triggered. |
| **On Done** | Triggers when the envelope finishes or loops back if looping is enabled. |
| **Out Envelope** | The output value of the envelope. |

### ADSR Envelope

![ADSR Envelope](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a83d0e2-25e4-4ce1-97b2-8b2e62d92324/envelopes_adsr_envelope.png)

The **ADSR Envelope** node generates an attack-decay-sustain-release envelope value output when triggered. This node is similar to the **AD Envelope** node, but it requires a separate release trigger for the release phase of the envelope to begin.

#### ADSR Envelope Inputs

| Input | Description |
| --- | --- |
| **Trigger Attack** | The trigger on which to start the attack phase of the envelope generator. |
| **Trigger Release** | The trigger on which to start the release phase of the envelope generator. |
| **Attack Time** | The amount of time (in seconds) to reach the maximum envelope value (1.0). |
| **Delay Time** | The amount of time (in seconds) to reach the minimum envelope value (0.0). |
| **Sustain Level** | The sustain level of the envelope. |
| **Release Time** | The release time of the envelope. |
| **Attack Curve** | The exponential curve factor of the attack phase. For example, a value of 1.0 produces linear growth, a value less than 1.0 produces logarithmic growth, and a value greater than 1.0 produces exponential growth. |
| **Decay Curve** | The exponential curve factor of the decay phase. For example, a value of 1.0 produces linear decay, a value greater than 1.0 produces logarithmic decay, and a value less than 1.0 produces exponential decay. |
| **Release Curve** | The exponential curve factor of the release phase. For example, a value of 1.0 produces linear release, a value greater than 1.0 produces logarithmic release, and a value less than 1.0 produces exponential release. |

#### ADSR Envelope Outputs

| Output | Description |
| --- | --- |
| **On Attack Triggered** | Triggers when the envelope attack phase is triggered. |
| **On Decay Triggered** | Triggers when the envelope decay phase is triggered. |
| **On Sustain Triggered** | Triggers when the envelope sustain phase is triggered. |
| **On Release Triggered** | Triggers when the envelope release phase is triggered. |
| **On Done** | Triggers when the envelope is finished. |
| **Out Envelope** | The output value of the envelope. |

### Crossfade

![Crossfade](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1f97009e-81a9-4a5a-985f-97c4fc88d436/envelopes_crossfade.png)

The **Crossfade** node blends between inputs linearly using a provided block-rate float parameter. There are multiple versions of this node to support different input counts (between 2 and 8).

#### Crossfade Inputs

| Input | Description |
| --- | --- |
| **Crossfade Value** | The value which represents the current blend between the provided inputs. For example, a value of 0.5 for input values of 2 and 4 will result in an output of 3. |
| **In X** | The input corresponding with position X. |

#### Crossfade Outputs

| Output | Description |
| --- | --- |
| **Out** | The value produced from the crossfade. |

### Evaluate WaveTable

![Evaluate  WaveTable](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c834fea2-acf3-4430-8ebd-904a5081b918/envelopes_evaluate_wavetable.png)

The **Evaluate WaveTable** node outputs the value of a WaveTable at a given input phase, allowing you to use the WaveTable as a curve in the graph.

#### Evaluate WaveTable Inputs

| Input | Description |
| --- | --- |
| **WaveTable** | The WaveTable to evaluate. |
| **Input** | The input to evaluate the WaveTable with. This value is clamped to a range of 0.0 to 1.0. |
| **Interpolation** | The method to use to interpolate between WaveTable values: **None (Step)**, **Linear**, or **Cubic** |

#### Evaluate WaveTable Outputs

| Output | Description |
| --- | --- |
| **Output** | The current interpolated value. |

### WaveTable Envelope

![WaveTable Envelope](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e8241bd-b501-41a4-91fd-9c6d772d4c27/envelopes_wavetable_envelope.png)

The **WaveTable Envelope** node reads through the given WaveTable over the given duration.

#### WaveTable Envelope Inputs

| Input | Description |
| --- | --- |
| **WaveTable** | The WaveTable to read. |
| **Play** | The trigger on which to play the envelope. |
| **Stop** | The trigger on which to stop the envelope. |
| **Pause** | The trigger on which to pause the envelope. |
| **Duration** | The duration (in seconds). |
| **Mode** | 
Determines what value the envelope completes on and if it loops:

-   **Loop**: Interpolates the last and first values in the WaveTable and restarts interpolation of the envelope on completion.
-   **Hold**: Holds the last value in the table if playback elapses beyond the WaveTable's length.
-   **Unit**: Interpolates the last value in the table with 1.0 if playback elapses beyond the WaveTable's length.
-   **Zero**: Interpolates the last value in the table with 0.0 if playback elapses beyond the WaveTable's length.



 |
| **Interpolation** | 

Determines how the envelope interpolates between WaveTable values:

-   **None (Step)**: No interpolation between values. The lowest value is used.
-   **Linear**: Linearly interpolates between values.
-   **Cubic**: Cubically interpolates between values.



 |

#### WaveTable Envelope Outputs

| Output | Description |
| --- | --- |
| **OnFinished** | Triggers when the envelope is finished. |
| **Out** | The output value. |

## External IO

### Audio Bus Reader

![Audio Bus Reader](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a50de5e4-46a1-44fe-b112-0311011150ab/external_io_audio_bus_reader.png)

The **Audio Bus Reader** node outputs audio data from an Audio Bus asset. There are two versions of this node to support different channel amounts (either 1 or 2).

#### Audio Bus Reader Inputs

| Input | Description |
| --- | --- |
| **Audio Bus** | The Audio Bus asset to read data from. |

#### Audio Bus Reader Outputs

| Output | Description |
| --- | --- |
| **Out X** | The audio output for channel X. |

### Wave Writer

![Wave Writer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/889ed21b-726d-47b3-a676-664c4fe09e49/external_io_wave_writer.png)

The **Wave Writer** node writes audio signals to disk. There are multiple versions of this node to support different channel amounts (between 1 and 8).

The file is rendered at 48,000 Hz and is saved to the **Saved > AudioCaptures** folder.

#### Wave Writer Inputs

| Input | Description |
| --- | --- |
| **Filename Prefix** | The filename prefix used for the output file. |
| **Enabled** | If enabled, this node will write audio signals to disk. |
| **In X** | The audio input corresponding with channel X. |

## Filters

### Biquad Filter

![Biquad Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7901a180-a095-4a14-905e-75f3d47dba58/filters_biquad_filter.png)

The **Biquad Filter** node provides a simple two-pole biquad filter that supports a variety of configurations.

#### Biquad Filter Inputs

| Input | Description |
| --- | --- |
| **In** | The audio to be biquad filtered. |
| **Cutoff Frequency** | The value of the cutoff frequency. |
| **Bandwidth** | When applicable, controls the bandwidth value of the current filter type. |
| **Gain (dB)** | The gain (in decibels) applied to the band when in Parametric mode. |
| **Type** | The type of biquad filter to use. |

#### Biquad Filter Outputs

| Output | Description |
| --- | --- |
| **Out** | The biquad-filtered audio. |

### Bitcrusher

![Bitcrusher](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e44b9d7a-c5bd-4895-a1fb-54f24b831f8d/filters_bitcrusher.png)

The **Bitcrusher** node downsamples and lowers the bit-depth of an incoming audio signal.

#### Bitcrusher Inputs

| Input | Description |
| --- | --- |
| **Audio** | The audio signal to bitcrush. |
| **Sample Rate** | The sampling frequency to downsample the audio to. |
| **Bit Depth** | The bit resolution to reduce the audio to. |

#### Bitcrusher Outputs

| Output | Description |
| --- | --- |
| **Audio** | The bitcrushed audio signal. |

### Dynamic Filter

![Dynamic Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f22f9f10-db69-4c9c-b426-2f21fff3aa0b/filters_dynamic_filter.png)

The **Dynamic Filter** node filters a band of audio based on the strength of the input signal.

#### Dynamic Filter Inputs

| Input | Description |
| --- | --- |
| **Audio** | The audio signal to filter. |
| **Sidechain** | (Optional) An external audio signal to control the filter with. If not set, the input audio signal is used. |
| **FilterType** | The filter shape to use: **Bell**, **Low Shelf**, or **High Shelf** |
| **Frequency** | The center frequency of the filter. |
| **Q** | The filter's Q, or resonance, which controls the steepness of the filter. |
| **Threshold dB** | The amplitude threshold (dB) above which gain is reduced. |
| **Ratio** | The amount of gain reduction to apply. A value of 1 applies no reduction and a higher value provides more reduction. |
| **Knee** | A decibel value that determines how hard or soft the gain reduction blends. A value of 0 dB provides no blending. |
| **Range** | The maximum gain reduction allowed (in decibels). A negative value applies compression and a positive value flips it into an expander. |
| **Gain (dB)** | The amount of make-up gain (in decibels) to apply. |
| **AttackTime** | The amount of time (in seconds) it takes the audio above the threshold to reach its compressed volume level. |
| **ReleaseTime** | The amount of time (in seconds) it takes for the audio below the threshold to return to its original volume level. |
| **EnvelopeMode** | The envelope-following method the compressor uses for gain detection. |
| **AnalogMode** | If enabled, analog mode is used for the compressor's envelope follower. |

#### Dynamic Filter Outputs

| Output | Description |
| --- | --- |
| **Audio** | The filtered audio signal. |

### Ladder Filter

![Ladder Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/694d8a18-55e3-4f0f-84a3-545b75459811/filters_ladder_filter.png)

The **Ladder Filter** node provides a virtual analog filter that has a pleasing and classic rolloff and resonance.

#### Ladder Filter Inputs

| Input | Description |
| --- | --- |
| **In** | The audio to be processed by the ladder filter. |
| **Cutoff Frequency** | The value of the cutoff frequency. |
| **Resonance** | The value of the filter resonance. |

#### Ladder Filter Outputs

| Output | Description |
| --- | --- |
| **Out** | The ladder filtered audio. |

### Mono Band Splitter

![Mono Band Splitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58428da0-db47-4d9e-ada6-6df5a92507b6/filters_mono_band_splitter.png)

The **Mono Band Splitter** node splits incoming audio into separate frequency bands. There are multiple versions of this node to support different input and output counts (between 2 and 5).

#### Mono Band Splitter Inputs

| Input | Description |
| --- | --- |
| **In** | The base audio input channel. |
| **Filter Order** | The steepness of the crossover filters: **Two Pole**, **Four Pole**, **Six Pole**, or **Eight Pole** |
| **Phase Compensate** | If enabled, each band is phase-compensated so they can be summed back together correctly. |
| **Crossover X** | The frequency of the crossover filters from **Band X** to the next. |

#### Mono Band Splitter Outputs

| Output | Description |
| --- | --- |
| **Band X Out** | The audio output corresponding to channel X. |

### One-Pole High Pass Filter

![One-Pole High Pass Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8b43ab8-60e1-44d1-8563-1094dd3bfa5c/filters_one-pole_high_pass_filter.png)

The **One-Pole High Pass Filter** node is a computationally cheap filter useful for a number of simple applications, such as simulating occlusion.

#### One-Pole High Pass Filter Inputs

| Input | Description |
| --- | --- |
| **In** | The audio signal to be filtered. |
| **Cutoff Frequency** | The value of the cutoff frequency. |

#### One-Pole High Pass Filter Outputs

| Output | Description |
| --- | --- |
| **Out** | The filtered audio signal. |

### One-Pole Low Pass Filter

![One-Pole Low Pass Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/feff0f12-ba13-4520-9538-116c83fb03af/filters_one-pole_low_pass_filter.png)

The **One-Pole Low Pass Filter** node is a computationally cheap filter useful for a number of simple applications, such as simulating air absorption

#### One-Pole Low Pass Filter Inputs

| Input | Description |
| --- | --- |
| **In** | The audio signal to be filtered. |
| **Cutoff Frequency** | The value of the cutoff frequency. |

#### One-Pole Low Pass Filter Outputs

| Output | Description |
| --- | --- |
| **Out** | The filtered audio signal. |

### Sample And Hold

![Sample and Hold](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ca2484d-f9b1-4bf8-9397-f6225d745232/filters_sample_and_hold.png)

The **Sample And Hold** node outputs a single value of the input audio signal when triggered.

#### Sample And Hold Inputs

| Input | Description |
| --- | --- |
| **Sample And Hold** | The trigger on which to sample and hold the input audio. |
| **In** | The audio signal to sample. |

#### Sample And Hold Outputs

| Output | Description |
| --- | --- |
| **On Sample And Hold** | Triggers when the Sample and Hold input is triggered. |
| **Out** | The sampled audio signal. |

### State Variable Filter

![State Variable Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc0a44f6-95bd-4489-99dc-d13c83524e57/filters_state_variable_filter.png)

The **State Variable Filter** node provides a virtual analog filter used in many synthesis applications.

#### State Variable Filter Inputs

| Input | Description |
| --- | --- |
| **In** | The audio to be processed by the filter. |
| **Cutoff Frequency** | The value of the cutoff frequency. |
| **Resonance** | The value of the filter resonance. |
| **Band Stop Control** | The control value applied to the band stop output. |

#### State Variable Filter Outputs

| Output | Description |
| --- | --- |
| **Low Pass Filter** | The low pass filter output. |
| **High Pass Filter** | The high pass filter output. |
| **Band Pass** | The band pass filter output. |
| **Band Stop** | The band stop filter output. |

### Stereo Band Splitter

![Stereo Band Splitter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7add9e6e-f409-4609-9f70-587ac4e2de3d/filters_stereo_band_splitter.png)

The **Stereo Band Splitter** node splits incoming audio into separate frequency bands. There are multiple versions of this node to support different input and output counts (between 2 and 5).

#### Stereo Band Splitter Inputs

| Input | Description |
| --- | --- |
| **In L / R** | The base audio input channels. |
| **Filter Order** | The steepness of the crossover filters: **Two Pole**, **Four Pole**, **Six Pole**, **Eight Pole** |
| **Phase Compensate** | If enabled, each band is phase-compensated so that they can be summed back together correctly. |
| **Crossover X** | The frequency of the crossover filters from **Band X** to the next. |

#### Stereo Band Splitter Outputs

| Output | Description |
| --- | --- |
| **Band X L / R** | The audio output corresponding to channel X (in the left / right channel). |

## Generators

MetaSounds have several audio-rate generators which provide options for frequency modulation.

With the exception of the **Noise** node, all of these nodes support sync triggering which resets their phase. When combined with an audio-rate trigger repeat or a threshold trigger, this can create many unique synthesis effects.

### Additive Synth

![Additive Synth](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0cf86e74-d59b-437d-9823-70f50f07a964/generators_additive_synth.png)

The **Additive Synth** node synthesizes audio by adding given sinusoids together.

#### Additive Synth Inputs

| Input | Description |
| --- | --- |
| **Base Frequency** | The sinusoid frequency the harmonics are based on. The value is clamped from 0.0 to the Nyquist frequency. |
| **HarmonicMultipliers** | An array of harmonic multipliers applied to the base frequency. The number of sinusoids used depends on the size of this array. The values are clamped from 0.0 to a maximum so the resulting frequency won't go above the Nyquist frequency. |
| **Amplitudes** | The array of sinusoid amplitudes. The values are clamped to a range of 0.0 to 1.0 |
| **Phases** | The array of sinusoid phases (in degrees). The values are clamped to a range of 0.0 to 360. |
| **Pan Amounts** | The array of pan amounts (using equal power law). For example, a value of -1.0 is fully left and a value of 1.0 is fully right. |

#### Additive Synth Outputs

| Output | Description |
| --- | --- |
| **Out Left / Right Audio** | The synthesized audio output (left / right channels). |

### Low Frequency Noise

![Low Frequency Noise](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab5fde0a-6996-4933-8df4-5f45bfa6071c/generators_low_frequency_noise.png)

The **Low Frequency Noise** node produces random values at a set frequency and smoothly interpolates between them to add periodic variation to a signal.

#### Low Frequency Noise Inputs

| Input | Description |
| --- | --- |
| **Rate** | The rate (Hz) of each new value. This is clamped to block rate. |
| **Seed** | The seed used for the random shuffle. The default value of -1 uses the current time. |
| **Reset Seed** | The trigger on which to reset the seed. |
| **Sync** | The trigger on which to reset the phase of the generator. |
| **Interpolation** | The method to use to interpolate between values: **None**, **Linear**, or **Cubic** |
| **Rate Jitter** | A percentage to randomly modify (+/-) the **Rate** by. This value is clamped between 0.0 and 1.0. |
| **Step Limit** | A percentage to limit the next random number in sequence to. This value is clamped between 0.0 and 1.0. |
| **Min Value** | The minimum output value. |
| **Max Value** | The maximum output value. |

#### Low Frequency Noise Outputs

| Output | Description |
| --- | --- |
| **Out** | The scaled output based on the **Min Value** and **Max Value**. |
| **Normalized** | The normalized output. |

### Low-Frequency Oscillator (LFO)

![LFO](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dacec5bd-667a-4c13-aca3-cfc3597bbb0c/generators_lfo.png)

The **LFO** node provides a low-frequency oscillator which you can use to create a variety of audio effects, such as phasing, vibrato, and tremolo.

#### LFO Inputs

| Input | Description |
| --- | --- |
| **Frequency** | The frequency (Hz) of the LFO (clamped at block rate). |
| **Shape** | The wave shape of the LFO: **Sine**, **Saw**, **Triangle**, or **Square** |
| **Min / Max Value** | The minimum / maximum output values. |
| **Sync** | Resets the phase of the generator. You can use this in conjunction with other nodes to get audio-rate phase synced generators. |
| **Phase Offset** | The phase offset (in degrees, between 0 and 360). |
| **Pulse Width** | The pulse width (between 0 and 1). |

#### LFO Outputs

| Output | Description |
| --- | --- |
| **Out** | The output value of the LFO (clamped at block rate). |

### Noise

![Noise](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f4c22ce-b52d-453c-9eca-99a869d101ba/generators_noise.png)

The **Noise** node generates either pink or white noise.

#### Noise Inputs

| Input | Description |
| --- | --- |
| **Seed** | The seed for the random number generator. The default value of -1 uses the current time. |
| **Type** | The type of noise to generate: **Pink Noise** or **White Noise** |

#### Noise Outputs

| Output | Description |
| --- | --- |
| **Audio** | The generated noise output. |

### Perlin Noise

![Perlin Noise](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f59f323d-3f70-448b-bcd6-6b6661608fdb/generators_perlin_noise.png)

The **Perlin Noise** node evaluates one-dimensional Perlin value noise to add natural roughness to a signal. This node has two versions to support different data types (Audio or Float).

#### Perlin Noise Inputs

| Input | Description |
| --- | --- |
| **X** | The input value to the Perlin function. By default, the internal clock (in seconds) will be used. |
| **Layers** | The number of octaves of noise to sum. |
| **Seed** | The seed used for the random shuffle. The default value of -1 uses the current time. |
| **Min Value** | The minimum output value. |
| **Max Value** | The maximum output value. |

#### Perlin Noise Outputs

| Output | Description |
| --- | --- |
| **Output** | The scaled output based on the **Min Value** and **Max Value**. |
| **Normalized** | The normalized output. |

### Saw

![Saw](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69bbfd0e-4891-47c3-9578-5589661cf949/generators_saw.png)

The **Saw** node emits an audio signal of a saw wave with the given properties.

#### Saw Inputs

| Input | Description |
| --- | --- |
| **Enabled** | If enabled, the oscillator produces a signal. |
| **Bi Polar** | If enabled, the output is bi-polar (-1, 1). Otherwise, the output is uni-polar (0, 1). |
| **Frequency** | The base frequency of the oscillator (in Hz). |
| **Modulation** | An audio-rate input to modulate the base frequency. |
| **Sync** | Resets the phase of the generator. You can use this in conjunction with other nodes to get audio-rate phase synced generators. |
| **Phase Offset** | The phase offset (in degrees, between 0 and 360). |
| **Glide** | The amount of glide (smooth interpolation over time) used when changing frequencies. For example, a value of 0.0 will produce no glide and a value of 1.0 produces lots of glide. |
| **Type** | 
The generator type used to make the saw wave:

-   **Poly Smooth**: Generates a smooth version of the saw wave.
-   **Trivial**: Uses a basic implementation to generate a saw wave.



 |

#### Saw Outputs

| Output | Description |
| --- | --- |
| **Audio** | The saw wave audio signal. |

### Sine

![Sine](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a2e5c4ad-9371-4bc8-a08f-d222b94f2211/generators_sine.png)

The **Sine** node emits an audio signal of a sinusoid with the given properties.

#### Sine Inputs

| Input | Description |
| --- | --- |
| **Enabled** | If enabled, the oscillator produces a signal. |
| **Bi Polar** | If enabled, the output is bi-polar (-1, 1). Otherwise, the output is uni-polar (0, 1). |
| **Frequency** | The base frequency of the oscillator (in Hz). |
| **Modulation** | An audio-rate input to modulate the base frequency. |
| **Sync** | Resets the phase of the generator. You can use this in conjunction with other nodes to get audio-rate phase synced generators. |
| **Phase Offset** | The phase offset (in degrees, between 0 and 360). |
| **Glide** | The amount of glide (smooth interpolation over time) used when changing frequencies. For example, a value of 0.0 will produce no glide and a value of 1.0 produces lots of glide. |
| **Type** | 
The generator type used to make the sinusoid:

-   **2D Rotation**: Rotates around the unit circle to generate the sine wave.
-   **Pure Math**: Uses the standard math library to generate the sine wave (most expensive method).
-   **Bhaskara**: Uses the Bhaskara technique to approximate the sine wave.
-   **Wave Table**: Uses a wave table to generate the sine wave.



 |

#### Sine Outputs

| Output | Description |
| --- | --- |
| **Audio** | The sinusoid audio signal. |

### Square

![Square](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c5389e93-cd51-43b9-9e8b-9a2f565a0ed8/generators_square.png)

The **Square** node emits an audio signal of a square wave with the given properties.

#### Square Inputs

| Input | Description |
| --- | --- |
| **Enabled** | If enabled, the oscillator produces a signal. |
| **Bi Polar** | If enabled, the output is bi-polar (-1, 1). Otherwise, the output is uni-polar (0, 1). |
| **Frequency** | The base frequency of the oscillator (in Hz). |
| **Modulation** | An audio-rate input to modulate the base frequency. |
| **Sync** | Resets the phase of the generator. You can use this in conjunction with other nodes to get audio-rate phase synced generators. |
| **Phase Offset** | The phase offset (in degrees, between 0 and 360). |
| **Glide** | The amount of glide (smooth interpolation over time) used when changing frequencies. For example, a value of 0.0 will produce no glide and a value of 1.0 produces lots of glide. |
| **Type** | 
The generator type used to make the square wave:

-   **Poly Smooth**: Generates a smooth version of the Square wave.
-   **Trivial**: Uses a basic implementation to generate a Square wave.



 |
| **Pulse Width** | The relative pulse width of the square wave. |

#### Square Outputs

| Output | Description |
| --- | --- |
| **Audio** | The square wave audio signal. |

### SuperOscillator

![SuperOscillator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16375648-10bc-4eee-8f6e-1f9e3865954c/generators_superoscillator.png)

The **SuperOscillator** node generates audio using multiple internal oscillators. You can detune each internal oscillator evenly or randomly using **Detune** and **Entropy**. It supports all of the features of basic oscillator nodes, with the addition of a built-in limiter to keep the amplitude in check when there are higher voice counts. This node has two versions to support different channel configurations (Stereo or Mono).

#### SuperOscillator Inputs

| Input | Description |
| --- | --- |
| **Enabled** | If enabled, the oscillator produces a signal. |
| **Limit Output** | If enabled, the output volume will be limited. |
| **Voices** | The number of oscillators to use. This value is clamped between 1 and 16. |
| **Frequency** | The base frequency (Hz) of the oscillator. |
| **Modulation** | The modulation frequency. |
| **Detune** | The max pitch offset (in semitones). Only oscillators beyond the 2nd are detuned. |
| **Entropy** | This value controls how evenly the voices are distributed in pitch. This value is clamped between 0.0 and 1.0. |
| **Blend** | The volume (dB) of detuned voices relative to the primary voice. |
| **Glide** | The amount of glide (smooth interpolation over time) used when changing frequencies. For example, a value of 0.0 will produce no glide and a value of 1.0 produces lots of glide. |
| **Pulse Width** | The width of the square segment of the wave. This is only used for **Square** waves. |
| **Width** | The stereo width of the oscillators. This value is clamped between 0.0 and 1.0. |
| **Type** | The shape of the oscillator: **Sine**, **Saw**, **Triangle**, or **Square** |

#### SuperOscillator Outputs

| Output | Description |
| --- | --- |
| **Audio** | The output audio signal. |

### Triangle

![Triangle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e52dd0b9-8133-4134-a997-86b18a06f7ea/generators_triangle.png)

The **Triangle** node emits an audio signal of a triangle wave with the given properties.

#### Triangle Inputs

| Input | Description |
| --- | --- |
| **Enabled** | If enabled, the oscillator produces a signal. |
| **Bi Polar** | If enabled, the output will be bi-polar (-1, 1). Otherwise, the output will be uni-polar (0, 1). |
| **Frequency** | The base frequency of the oscillator (in Hz). |
| **Modulation** | An audio-rate input to modulate the base frequency. |
| **Sync** | Resets the phase of the generator. You can use this in conjunction with other nodes to get audio-rate phase synced generators. |
| **Phase Offset** | The phase offset (in degrees, between 0 and 360). |
| **Glide** | The amount of glide (smooth interpolation over time) used when changing frequencies. For example, a value of 0.0 will produce no glide and a value of 1.0 produces lots of glide. |
| **Type** | 
The generator type used to make the triangle wave:

-   **Poly Smooth**: Generates a smooth version of the Triangle wave.
-   **Trivial**: Uses a basic implementation to generate a Triangle wave.



 |

#### Triangle Outputs

| Output | Description |
| --- | --- |
| **Audio** | The triangle wave audio signal. |

### WaveTable Oscillator

![WaveTable Oscillator](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87710e7a-8e96-42c0-b0da-59675ffc1d9a/generators_wavetable_oscillator.png)

The **WaveTable Oscillator** node reads through the given WaveTable at the provided frequency.

#### WaveTable Oscillator Inputs

| Input | Description |
| --- | --- |
| **Play** | The trigger on which to play the oscillator (block rate). |
| **Stop** | The trigger on which to stop the oscillator (block rate). |
| **WaveTable** | The WaveTable to read. |
| **Freq** | The number of times to sample one period of the WaveTable per second. This frequency should be set between -20000 Hz and 20000 Hz. |
| **Sync** | The trigger on which to restart playback of the WaveTable on the trigger boundary (sample rate). |
| **Phase Modulator** | The audio source to be used for the modulating oscillation phase of the provided WaveTable. A value of 0 produces no phase modulation and a value of 1 produces a full table length (360 degrees) of phase shift. |

#### WaveTable Oscillator Outputs

| Output | Description |
| --- | --- |
| **Out** | The output audio buffer. |

### WaveTable Player

![WaveTable Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5254fbfe-29ca-4fb0-9c93-b46ad232a6e9/generators_wavetable_player.png)

The **WaveTable Player** node reads through a WaveTable Bank entry at a given index.

#### WaveTable Player Inputs

| Input | Description |
| --- | --- |
| **Play** | The trigger on which to play the oscillator (block rate). |
| **Stop** | The trigger on which to stop the oscillator (block rate). |
| **Sync** | The trigger on which to restart playback of the WaveTable on the trigger boundary (sample rate). |
| **Bank** | The WaveTable Bank to play from. |
| **Index** | The index of the WaveTable in the WaveTable Bank to play. |
| **Pitch Shift** | How much to shift the pitch of the given WaveTable. |
| **Loop** | If enabled, the WaveTable will loop. |

#### WaveTable Player Outputs

| Output | Description |
| --- | --- |
| **Mono Out** | The output audio buffer (in mono). |
| **On Finished** | Triggers when the WaveTable Player finishes playing the WaveTable. |

## Math

MetaSounds come with a variety of nodes that perform basic math operations on the given inputs.

Operations on Audio data types are executed at a per-sample level.

### Abs

![Abs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d1a002a-eaef-49e6-8145-0c47a9b02068/math_abs.png)

The **Abs** node returns the absolute value of a given input. For example, an input value of -2.0 will output 2.0. This node has different versions which support several common data types, including: Audio, Float, Int32, and Time.

### Add

![Add](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/894a9a8b-b451-4fe0-ba63-a9b80826601d/math_add.png)

The **Add** node performs addition operations on provided inputs. This node has different versions which support several common data types, including: Audio, Float to Audio, Float, Int32, and Time.

### Clamp

![Clamp](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ea5e67d-617a-4dc4-8843-54c8fce949c3/math_clamp.png)

The **Clamp** node returns the clamped value of the input within the given value range. This node has different versions which support several common data types, including: Audio, Float, and Int32.

#### Clamp Inputs

| Input | Description |
| --- | --- |
| **In** | The input value to clamp. |
| **Min / Max** | The min / max value to clamp the input value to. |

#### Clamp Outputs

| Output | Description |
| --- | --- |
| **Value** | The clamped value. |

### Divide

![Divide](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fdcdba3-23dd-4bd6-9ea3-ccf137327687/math_divide.png)

The **Divide** node performs division operations on provided inputs. This node has different versions which support several common data types, including: Float, Int32, and Time by Float.

### Filter Q To Bandwidth

![Filter Q To Bandwidth](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d98cc58-9b13-4269-a1dc-685e73487c60/math_filter_q_to_bandwidth.png)

The **Filter Q To Bandwidth** node converts a given Q (quality-factor) parameter for filter control to a bandwidth value.

### Linear To Log Frequency

![Linear To Log Frequency](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2ce7a0a-e04b-4956-ab5b-f3b03412c882/math_linear_to_log_frequency.png)

The **Linear To Log Frequency** node converts a linear space input value to a log-frequency output.

#### Linear To Log Frequency Inputs

| Input | Description |
| --- | --- |
| **Value** | The linear input value to map to a log frequency output. |
| **Min / Max Domain** | The min / max domain for the input value. The input and output values are clamped to this domain. |
| **Min / Max Range** | The min / max positive range for the output frequency (Hz) value. The input and output values are clamped to this range. |

#### Linear To Log Frequency Outputs

| Output | Description |
| --- | --- |
| **Frequency** | The output frequency (Hz) that is the log frequency of the input value. |

### Log

![Log](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ccfd8041-cc5d-433e-a904-c011ebbaf08e/math_log.png)

The **Log** node calculates the float-base logarithm of another float.

### Map Range

![Map Range](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af8ace1c-13c1-4a40-bc65-9e9f04c24e13/math_map_range.png)

The **Map Range** node maps an input value in a given input range to a given output range. The results can also be clamped. This node has different versions which support several common data types, including: Audio, Float, and Int32. These nodes are analogous to the **Blueprint Map** Range nodes.

The Audio version of this node does a per-sample mapping. This is useful when mapping audio-rate signals to audio-rate modulation parameters, such as Frequency Modulator in FM synthesis.

#### Map Range Inputs

| Input | Description |
| --- | --- |
| **In** | The input value to map. |
| **In Range A / B** | The minimum and maximum input value range. |
| **Out Range A / B** | The minimum and maximum output value range. |
| **Clamped** | If enabled, the input will be clamped to the specified input range. |

#### Map Range Outputs

| Output | Description |
| --- | --- |
| **Out Value** | The mapped output value. |

### Max

![Max](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54f45c13-e1f5-4b9b-8a5e-29a3742c4c5b/math_max.png)

The **Max** node returns the higher value (max) of A and B. This node has different versions to support several common data types, including: Audio, Float, and Int32.

#### Max Inputs

| Input | Description |
| --- | --- |
| **A / B** | The input values to compare. |

#### Max Outputs

| Output | Description |
| --- | --- |
| **Value** | The higher value (max) of A and B. |

### Min

![Min](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90092c97-0881-4be2-9394-c158fd303734/math_min.png)

The **Min** node returns the lower value (min) of A and B. This node has different versions which support several common data types, including: Audio, Float, and Int32.

#### MinInputs

| Input | Description |
| --- | --- |
| **A / B** | The input values to compare. |

#### Min Outputs

| Output | Description |
| --- | --- |
| **Value** | The lower value (min) of A and B. |

### Modulo

![Modulo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d00fd07-8542-45d5-bb29-13b21187b51f/math_modulo.png)

The **Modulo** node returns the remainder of a division operation of two given Int32 values.

### Multiply

![Multiply](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e940030e-b693-411f-8214-3607039098ba/math_multiply.png)

The **Multiply** node performs multiplication operations on provided inputs. This node has different versions which support several common data types, including: Audio by Float, Audio, Float, Int32, and Time by Float.

This node can be used to provide ring-modulation type effects and audio-rate amplitude modulation.

### Power

![Power](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d44bac82-06f9-45b8-ab17-bf250fa02c00/math_power.png)

The **Power** node raises a given Float to the power of another Float.

### Subtract

![Subtract](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4470336f-9492-4fff-afc1-9e7919c745f1/math_subtract.png)

The **Subtract** node performs subtraction operations on provided inputs. This node has different versions which support several common data types, including: Audio, Float, Int32, and Time.

## Mix

MetaSounds provide two node types to create audio mixes, the **Mono Mixer** node and the **Stereo Mixer** node. These nodes have different versions which support between 2 and 8 input audio buffers, which are combined into a single buffer by using the input channel's corresponding gain values and summing them together.

The gain values are not clamped so they can be used for attenuating and inverting the audio signal.

These nodes are useful for mapping audio-rate buffers to different ranges for modulating various audio-rate-capable parameters.

### Mono Mixer

![Mono Mixer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ced6533c-1048-4ab0-90b6-9b219fe00c04/mix_mono_mixer.png)

### Stereo Mixer

![Stereo Mixer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01e2e47c-1812-4aac-af96-a4e123809f3c/mix_stereo_mixer.png)

## Music

### Frequency To MIDI

![Frequency To MIDI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a749f18-fe8c-46dc-a603-2b8bfdceb2f8/music_frequency_to_midi.png)

The **Frequency To MIDI** node converts a frequency value (in Hz) to a standard MIDI scale note value (where middle C is 60).

#### Frequency To MIDI Inputs

| Input | Description |
| --- | --- |
| **Frequency In** | The input frequency value (in Hz). |

#### Frequency To MIDI Outputs

| Output | Description |
| --- | --- |
| **Out MIDI** | The output MIDI note value. |

### MIDI Note Quantizer

![MIDI Note Quantizer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f8fd716-4443-4f1f-abfb-f018af229f56/music_midi_note_quantizer.png)

The **MIDI Note Quantizer** node quantizes a MIDI note to the nearest note that matches the provided criteria.

#### MIDI Note Quantizer Inputs

| Input | Description |
| --- | --- |
| **Note In** | The MIDI note to quantize. |
| **Root Note** | The MIDI note to treat as the root. For example, a value of 0 equals C, a value of 1 equals C#/Db, and so on. The octave does not matter. Additionally, all values less than 0 clamp to 0. |
| **Scale Degrees** | An array containing a set of notes (in ascending order) representing half steps. The array must start with 0.0 to represent the root note and the highest value in the array must represent the root note in a higher octave, such as 12.0 for a single octave range or 24.0 for a two octave range. |

#### MIDI Note Quantizer Outputs

| Output | Description |
| --- | --- |
| **Note Out** | The quantized note. |

### MIDI To Frequency

![MIDI To Frequency](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/332edcb7-ddde-41f2-a3d9-d83016740a7d/music_midi_to_frequency.png)

The **Frequency to MIDI** node converts a standard MIDI scale note value (where middle C is 60) to a frequency value (in Hz). This node has two different versions which support Float and Int32 data types respectively.

You can use this node to musically control generators that take frequencies (in Hz) as an input. Additionally, the Float version can take fractional MIDI note values, which can be useful for microtonality and custom tuning.

#### MIDI To Frequency Inputs

| Input | Description |
| --- | --- |
| **MIDI In** | The input value which represents a MIDI note value. |

#### MIDI To Frequency Outputs

| Output | Description |
| --- | --- |
| **Out Frequency** | The output frequency value (in Hz). |

### Scale to Note Array

![Scale to Note Array](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c02b1209-995b-4333-a480-496543bfd4cd/music_scale_to_note_array.png)

The **Scale to Note Array** node returns an array of floating-point numbers representing notes of the selected scale.

This node can be useful when creating procedural music by using the **Chord Tones Only** toggle to switch between full scale and chord tones.

#### Scale to Note Array Inputs

| Input | Description |
| --- | --- |
| **Scale Degrees** | The preset scale to get the notes for. |
| **Chord Tones Only** | If enabled, a subset of the scale representing chord tones is returned. For example, scale degrees of 1, 3, 5, and 7. |

#### Scale to Note Array Outputs

| Output | Description |
| --- | --- |
| **Scale Array Out** | The array representation of the scale as half-steps above the root. The set is inclusive at both ends (starting at 0.0f and ending at 12.0f). |

## Random

![Random](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9649ad26-058b-4f71-a80d-237ba8d6e785/random_random.png)

MetaSounds provide several **Random** nodes categorized by their output value type, including Bool, Float, Int, and Time. These nodes output a random value from their input type and a seed.

Using the Reset trigger with an identical seed will produce the same results. This is useful to get randomized repetition.

#### Random Inputs

| Input | Description |
| --- | --- |
| **Next** | The trigger on which to generate the next random value. |
| **Reset** | The trigger on which to reset the random sequence with the supplied seed. |
| **Seed** | The seed value to use for the randomization. The default value of -1 uses a random seed. |
| **Min / Max** | The inclusive range of the random value. |

#### Random Outputs

| Output | Description |
| --- | --- |
| **On Next** | Triggers when the Next input is triggered. |
| **On Reset** | Triggers when the Reset input is triggered. |
| **Value** | The randomly generated value. |

## Spatialization

### ITD Panner

![ITD Panner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1b996224-cec1-4094-9f0d-e9d0c7dcb3d9/spatialization_itd_panner.png)

The **ITD Panner** node pans an input audio signal using an interaural time delay method.

#### ITD Panner Inputs

| Input | Description |
| --- | --- |
| **In** | The input audio to spatialize. |
| **Angle** | The sound source angle (in degrees). A value of 90 degrees is front, 0 degrees is right, 270 degrees is behind, and 180 degrees is left. |
| **Distance Factor** | The normalized distance factor (0.0 to 1.0) to use for Interaural Level Difference (ILD) calculations. A value of 0.0 is near and a value of 1.0 is far. The further away the input audio is, the less difference in levels (gain) between the ears. |
| **Head Width** | The width (in centimeters) of the listener's head. |

#### ITD Panner Outputs

| Output | Description |
| --- | --- |
| **Out Left / Right** | The audio output (left / right channel). |

### Mid-Side Decode

![Mid-Side Decode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e3c60e1-46e3-402e-8da8-9b60da13c0f2/spatialization_mid-side_decode.png)

The **Mid-Side Decode** node converts a stereo signal with mid and side channels to left and right channels.

#### Mid-Side Decode Inputs

| Input | Description |
| --- | --- |
| **In Mid / Side** | The audio channels to convert. |
| **Spread Amount** | The amount of stereo spread. A value of 0.0 produces no spread, a value of 0.5 is the original signal, and a value of 1.0 is fully wide. |
| **Equal Power** | If enabled, an equal power relationship between the input audio channels will be maintained. |

#### Mid-Side Decode Outputs

| Output | Description |
| --- | --- |
| **Out Left / Right** | The output audio channels. |

### Mid-Side Encode

![Mid-Side Encode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/006660c4-0459-4406-958a-3d9d5c4411e5/spatialization_mid-side_encode.png)

The **Mid-Side Encode** node converts a stereo signal with left and right channels to mid and side channels.

#### Mid-Side Encode Inputs

| Input | Description |
| --- | --- |
| **In Left / Right** | The audio channels to convert. |
| **Spread Amount** | The amount of stereo spread. A value of 0.0 produces no spread, a value of 0.5 is the original signal, and a value of 1.0 is fully wide. |
| **Equal Power** | If enabled, an equal power relationship between the input audio channels is maintained. |

#### Mid-Side Encode Outputs

| Output | Description |
| --- | --- |
| **Out Mid / Side** | The output audio channels. |

### Stereo Panner

![Stereo Panner](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e34f73f-1d34-41c3-85c0-ebe19a7438ad/spatialization_stereo_panner.png)

The **Stereo Panner** node pans an input audio signal to left and right outputs.

#### Stereo Panner Inputs

| Input | Description |
| --- | --- |
| **In** | The input audio signal to pan. |
| **Pan Amount** | The amount to pan the audio signal (-1.0 is fully left, 1.0 is fully right). |
| **Panning Law** | 
The panning law to use:

-   **Equal Power**: The power of the audio signal is constant while panning.
-   **Linear**: The amplitude of the audio signal is constant while panning.



 |

#### Stereo Panner Outputs

| Output | Description |
| --- | --- |
| **Out Left / Right** | The output audio signal (left / right channels). |

## Triggers

### Trigger Accumulate

![Trigger Accumulate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/260a2493-ed7a-4e34-a743-fd3144f85600/triggers_trigger_accumulate.png)

The **Trigger Accumulate** node triggers once all connected input triggers have been triggered at least once. There are multiple versions of this node in order to support different input counts (between 1 and 8).

This node is can be useful to detect when multiple **Wave Player** nodes to finish before triggering the On Finished Output trigger.

#### Trigger Accumulate Inputs

| Input | Description |
| --- | --- |
| **In X** | The trigger input(s). |
| **Auto Reset** | The trigger on which the accumulation on this node is reset. |

#### Trigger Accumulate Outputs

| Output | Description |
| --- | --- |
| **Out** | Triggers when all input triggers have been accumulated. |

### Trigger Any

![Trigger Any](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2760eaa-4e5d-4253-a1ba-83083917f8c8/triggers_trigger_any.png)

The **Trigger Any** node triggers once any of the connected input triggers activate. This node has different versions which support different input counts (between 2 and 8).

This is a useful node when you want to have many different trigger sources execute another node's input.

#### Trigger Any Inputs

| Input | Description |
| --- | --- |
| **In X** | The trigger input(s). |

#### Trigger Any Outputs

| Output | Description |
| --- | --- |
| **Out** | Triggers when any input trigger is triggered. |

### Trigger Compare

![Trigger Compare](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acff386f-52c1-4d98-8b37-61784334b8e7/triggers_trigger_compare.png)

The **Trigger Compare** node triggers either true or false based on comparing connected inputs. This node has different versions which support several common data types, including: Bool, Float, and Int32.

#### Trigger Compare Inputs

| Input | Description |
| --- | --- |
| **Compare** | The trigger on which to compare A and B. |
| **A / B** | The values to compare. |
| **Type** | The type of comparison to make: **Equals**, **Not Equals**, **Less Than**, **Greater Than**, **Less Than Or Equals**, or **Greater Than Or Equals** |

#### Trigger Compare Outputs

| Output | Description |
| --- | --- |
| **True / False** | Triggers with the resulting trigger after making the comparison. |

### Trigger Control

![Trigger Control](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/314682e2-7837-4fce-b25f-8dc448819895/triggers_trigger_control.png)

The **Trigger Control** node provides controls to allow or block trigger signals from passing through to the output.

#### Trigger Control Inputs

| Input | Description |
| --- | --- |
| **Trigger In** | The input trigger to control. |
| **Open** | The trigger on which to allow the input trigger to pass through. |
| **Close** | The trigger on which to block the input trigger to pass through. |
| **Toggle** | The trigger on which to toggle the open/closed state of this node. |
| **Start Closed** | If enabled, the node will start in a closed state. |

#### Trigger Control Outputs

| Output | Description |
| --- | --- |
| **Trigger Out** | The output trigger that passes through if the node is open. |

### Trigger Counter

![Trigger Counter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3f65374-b293-4922-b300-a20f149ca317/triggers_trigger_counter.png)

The **Trigger Counter** node counts the connected input trigger activations.

This node is useful for sequencing array inputs and a large number of other procedural use cases.

#### Trigger Counter Inputs

| Input | Description |
| --- | --- |
| **In** | The input trigger for which to count activations. |
| **Reset** | The trigger on which to reset the counter to zero and the value back to the start value. |
| **Start Value** | The value to start with on initialization and when reset. |
| **Step Size** | The value to add to the current value for each input trigger. This can be negative. |
| **Reset Count** | The number of input triggers to count before automatically resetting. If the value is set to 0, the node won't automatically reset. |

#### Trigger Counter Outputs

| Output | Description |
| --- | --- |
| **On Trigger** | Triggers when the input trigger is triggered and the count is updated. |
| **On Reset** | Triggers when the input reset is triggered or if the counter automatically resets. |
| **Count** | The current trigger count. |
| **Value** | The current value. |

### Trigger Delay

![Trigger Delay](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cd16bf16-b2d6-48a2-ab38-6192a1c7174c/triggers_trigger_delay.png)

The **Trigger Delay** node executes a trigger after a given delay time from the most recent execution of the input trigger.

This node is similar to the **Trigger Pipe** node, but differs by only considering the most recent trigger execution. This means that additional triggers that happen within the delay time will reset the timer and cause the output trigger to be delayed again.

#### Trigger Delay Inputs

| Input | Description |
| --- | --- |
| **In** | The input trigger to delay. |
| **Reset** | The trigger on which to reset the delay and clear the execution task, if it is pending. |
| **Delay Time** | The amount of time to delay the trigger (in seconds). |

#### Trigger Delay Outputs

| Output | Description |
| --- | --- |
| **Out** | The delayed output trigger. |

### Trigger Filter

![Trigger Filter](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a51181d-6bf7-4d86-b8a8-cb7b19080356/triggers_trigger_filter.png)

The **Trigger Filter** node responds to a trigger by randomly activating one of the two output triggers.

#### Trigger Filter Inputs

| Input | Description |
| --- | --- |
| **Trigger** | The trigger on which to randomly activate an output trigger. |
| **Reset** | The trigger on which to reset the random sequence with the provided seed. |
| **Seed** | The seed value to use for the randomization. A value of -1 will use a random seed. |
| **Probability** | The probability that a particular output trigger will get activated. For example, a value of 0.0 is always heads, a value of 1.0 is always tails, and 0.5 is equal odds. |

#### Trigger Filter Outputs

| Output | Description |
| --- | --- |
| **Heads / Tails** | The possible output triggers. |

### Trigger On Threshold

![Trigger On Threshold](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55121e7a-b727-490c-a557-2ef7d5ac5e2f/triggers_trigger_on_threshold.png)

The **Trigger On Threshold** node operates as an edge detector and triggers when the input audio crosses a given threshold value while moving in the specified direction. This node has different versions which support several common data types, including: Audio, Float, and Int32.

If set to Rising Edge, a trigger is output when the signal crosses the threshold with a positive slope. This is useful when paired with a generator node and connected to another generator's sync trigger input.

#### Trigger On Threshold Inputs

| Input | Description |
| --- | --- |
| **In** | The input audio signal. |
| **Threshold** | The threshold at which to trigger output. |
| **Type** | The type of trigger threshold: **Rising Edge**, **Falling Edge**, or **Abs Threshold** |

#### Trigger On Threshold Outputs

| Output | Description |
| --- | --- |
| **Out** | The output threshold trigger. |

### Trigger On Value Change

![Trigger On Value Change](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61544e03-1695-4f56-a348-7a91345fb8f1/triggers_trigger_on_value_change.png)

The **Trigger On Value Change** node triggers when a given value changes. This node has different versions which support several common data types, including: Bool, Float, and Int32.

#### Trigger On Value Change Inputs

| Input | Description |
| --- | --- |
| **Value** | The input value to watch. |

#### Trigger On Value Change Outputs

| Output | Description |
| --- | --- |
| **Trigger** | The output trigger. |

### Trigger Once

![Trigger Once](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46c0a4eb-d6b8-4502-9961-e75a1749e087/triggers_trigger_once.png)

The **Trigger Once** node triggers the first time an input trigger is activated and ignores all other occurrences, unless reset.

#### Trigger Once Inputs

| Input | Description |
| --- | --- |
| **Trigger In** | The input trigger. |
| **Reset** | The trigger on which to open the node and allow another trigger through. |
| **Start Closed** | If enabled, the node is closed when playback begins. |

#### Trigger Once Outputs

| Output | Description |
| --- | --- |
| **Trigger Out** | The output trigger. |

### Trigger Pipe

![Trigger Pipe](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc7253a7-4abb-4857-85b0-c5b1331d06d3/triggers_trigger_pipe.png)

The **Trigger Pipe** node delays execution of all input trigger signals by the given delay.

This node is similar to the **Trigger Delay** node, but does not reset the timer upon receiving additional triggers.

#### Trigger Pipe Inputs

| Input | Description |
| --- | --- |
| **In** | The input trigger to delay. |
| **Reset** | The trigger on which to reset the trigger delay and clear any pending execution tasks. |
| **Delay Time** | The time to delay the input trigger (in seconds). |

#### Trigger Pipe Outputs

| Output | Description |
| --- | --- |
| **Out** | The delayed output trigger. |

### Trigger Repeat

![Trigger Repeat](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a9df4da-3e06-4f02-9abb-10ccd6ada847/triggers_trigger_repeat.png)

The **Trigger Repeat** node emits a trigger periodically at a given sample-accurate and arbitrarily-precise rate.

#### Trigger Repeat Inputs

| Input | Description |
| --- | --- |
| **Start / Stop** | The triggers on which to start or stop executing periodic output triggers. |
| **Period** | The period to trigger (in seconds). |

#### Trigger Repeat Outputs

| Output | Description |
| --- | --- |
| **RepeatOut** | The periodically generated output trigger. |

### Trigger Route

![Trigger Route](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1ae33b4c-5901-4208-a053-9251a3350d77/triggers_trigger_route.png)

The **Trigger Route** node routes different input values to a single output value. This node has multiple versions for different input counts (between 2 and 8) and for each supported data type, including: Audio, Bool, Float, Int32, and Time.

#### Trigger Route Inputs

| Input | Description |
| --- | --- |
| **Set X** | The input triggers which initialize the routing. The default option is 0. |
| **Value X** | The input value to route to the output when triggered by its corresponding trigger. |

#### Trigger Route Outputs

| Output | Description |
| --- | --- |
| **On Set** | Triggers when any of the input triggers are set. |
| **Value** | The output value set by an activated input trigger. |

### Trigger Select

![Trigger Select](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d56f092a-4070-4908-8ca8-3f67b9cac326/triggers_trigger_select.png)

The **Trigger Select** node passes triggers through to the currently selected output trigger. This node has multiple versions for different input counts (between 2 and 8).

#### Trigger Select Inputs

| Input | Description |
| --- | --- |
| **In** | The trigger to pass through. |
| **Index** | The output index to trigger. If the provided value is out of range, it will be ignored. |

#### Trigger Select Outputs

| Output | Description |
| --- | --- |
| **Out X** | The output trigger at index X. |

### Trigger Sequence

![Trigger Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57f24e4b-0c6f-4b0f-aaa4-11154daff460/triggers_trigger_sequence.png)

The **Trigger Sequence** node responds to input triggers by sending the next output trigger in a sequence. This node has multiple versions which provide different numbers of output triggers (between 2 and 8).

#### Trigger Sequence Inputs

| Input | Description |
| --- | --- |
| **In** | The input trigger. |
| **Reset** | The trigger on which to reset the sequence back to 0. |
| **Loop** | If enabled, the sequence automatically loops back to 0 once all triggers have been activated. |

#### Trigger Sequence Outputs

| Output | Description |
| --- | --- |
| **Out X** | The trigger outputs in sequence. |

### Trigger Toggle

![Trigger Toggle](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1eb65b1d-9423-4ea0-89c0-e3e4fd256457/triggers_trigger_toggle.png)

The **Trigger Toggle** node toggles a Bool value on or off.

#### Trigger Toggle Inputs

| Input | Description |
| --- | --- |
| **On / Off** | The trigger on which to toggle the Bool output on or off. |
| **Init** | The initial states of the Bool. |

#### Trigger Toggle Outputs

| Output | Description |
| --- | --- |
| **Out** | Triggers when the Bool is toggled. |
| **Value** | The current Bool value. |

## Value

![Value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7dcb9b8-e330-45c6-8013-0f6dc66541f2/value_value.png)

The **Value** node sets a variable value on a trigger. This node has different versions for each of the supported data types, including: Bool, Float, Int32, and String.

#### Value Inputs

| Input | Description |
| --- | --- |
| **Set** | The trigger on which to write the set value to the output. |
| **Reset** | The trigger on which to reset the value to the initial value. |
| **Init Value** | The value to initialize the output value to. |
| **Target Value** | The value to set the output to when triggered. |

#### Value Outputs

| Output | Description |
| --- | --- |
| **On Set** | Triggers when the value is set. |
| **On Reset** | Triggers when the value is reset. |
| **Output Value** | The current output value. |