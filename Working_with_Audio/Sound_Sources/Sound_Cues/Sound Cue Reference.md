# Sound Cue Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:51:32

---

In **Unreal Engine**, a **Sound Cue** is an audio asset that encapsulates complex sound design tasks within a node graph. Sound Cues provide audio designers freedom to dynamically change parts of a sound effect's design by arranging and modifying Sound Nodes to create complex and interesting audio output.

In the Sound Cue Editor, a list of Sound Node types is provided within the **Palette** panel. Selecting a node in the **Viewport** panel will display the node's properties in the **Details** panel.

![Sound Cue Editor Palette Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3176bcd-cc8f-4ec2-ad09-9d5a80706174/sound-cue-editor-palette-panel.png)

For more about working with Sound Cues, see the [Sound Cue Editor](/documentation/en-us/unreal-engine/sound-cue-editor-in-unreal-engine) and [Sound Cue Editor UI](/documentation/en-us/unreal-engine/sound-cue-editor-ui-in-unreal-engine) documentation.

## Named Parameters

In some Sound Nodes, you can declare a parameter by entering a new parameter name. When you enter a parameter name in a node, it will create a parameter with that name.

![Named Parameter Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/783eba73-914c-4095-a9d1-e9f18ba0992d/named-parameter-example.png)

You can name the parameter whatever you want. However, when you use an **Audio Component Function** to set the parameter's value, its **In Name** field must exactly match the Parameter Name you gave it.

You cannot set the values for a named parameter from within a Sound Cue. A recommended workflow would be:

-   Add a Sound Node.
-   Enter a name in the node **Parameter Name** field.
-   Call the relevant audio component function from within a Blueprint, or in code, using the appropriate Set \[Name\] Parameter function.
-   Add the same name to the **In Name** parameter. This will get the Sound Cue to respond as expected.

![Set Wave Parameter Blueprint Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fba3a6e-3bb9-4867-be4e-6182ac3861bf/set-wave-parameter-blueprint-example.png)

The table below shows the nodes that can use named parameters, and the corresponding parameter setting functions.

| Node Type | Corresponding Function |
| --- | --- |
| Branch | Set Boolean Parameter |
| Continuous Modulator | Set Float Parameter |
| Crossfade by Param | Set Float Parameter |
| SoundClass | Set Wave Parameter |
| Switch | Set Integer Parameter |
| Wave Param | Set Wave Parameter |

## Output Node

An **Output** node is required in every Sound Cue and works as an end point for the audio signal path in the node graph. The Output node's properties are relative and affect all of the audio output contained within the Sound Cue.

![Output Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48416cae-960f-4d1a-9110-b7298aee1731/output-sound-node.png)

| Property | Description |
| --- | --- |
| **Memory** |   |
| Prime on Load | If enabled, all connected Sound Waves will load into cache when this Sound Cue is loaded. |
| Disable Random Branch Culling | If enabled, all per-platform random node culling will be ignored. |
| **Sound** |   |
| Volume Multiplier | The base volume multiplier. |
| Pitch Multiplier | The base pitch multiplier. |
| Class | The **Sound Class** asset that this Sound Cue belongs to. |
| **Attenuation** |   |
| Override Attenuation | If enabled, the existing attenuation settings will be overridden with the provided values. See the [Attenuation Node](/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine#attenuationnode) section of this page for more information. |
| Attenuation Settings | This can be set to an existing **Sound Attenuation** asset to utilize that asset's settings. |
| **Effects** |   |
| 🞂 Source |   |
| Enable Bus Sends | If enabled, audio output will be sent to buses. |
| Source Effect Chain | The **Source Effect Preset Chain** asset to use for this Sound Cue. |
| Post-Effect Bus Sends | An array of buses to send audio output to if there are bus instances playing after the source effects are processed. |
| Pre-Effect Bus Sends | An array of buses to send audio output to if there are bus instances playing before source effects are processed. |
| 🞂 Submix |   |
| Enable Base Submix | If enabled, sound will route to the Master Submix by default or to the Base Submix if defined. If disabled, sound will route ONLY to the Submix Sends and/or Bus Sends. |
| Base Submix | The **Submix** asset to use for this Sound Cue. |
| Enable Submix Sends | Enables sending audio output to additional submixes. |
| Submix Sends | An array of submixes which receive a prescribed amount (see **Send Level**) of this Sound Cue's audio output. |
| **Voice Management** |   |
| Virtualization Mode | Sets virtualization behavior to determine if a sound may revive and how it continues playing when culled or evicted due to looping sound limitations. |
| 🞂 Priority |   |
| Subtitle Priority | The priority of the subtitle. Higher values will play instead of lower values. |
| Bypass Volume Scale for Priority | If enabled, bypasses volume weighting priority upon evaluating whether sound should remain active when max channel count is met. |
| Priority | This is used to determine whether sound can play or remain active if the channel limit is met. Higher values will play instead of lower values. Unless bypassed, value is weighted with the final volume of the sound to produce final runtime priority value. |
| 🞂 Concurrency |   |
| Override Concurrency | If enabled, the existing concurrency settings will be overridden with the provided values. This allows the **Concurrency Overrides** values to be modified. |
| Concurrency Set | An array of concurrency settings to observe (if override is set to false). Sound must pass all concurrency settings to play. |
| 🞂 Concurrency 🞂 Concurrency Overrides |   |
| Max Count | The maximum number of concurrent sounds allowed in this concurrency group. |
| Limit to Owner | If enabled, the concurrency settings are applied to the actor which played the sound. If the sound doesn't have an owning actor, it falls back to the global concurrency settings. |
| Resolution Rate | The concurrency resolution policy to use if max voice count is reached. |
| Retrigger Time | The amount of time (in seconds) to wait between different sounds. The sounds rejected from this will ignore virtualization settings. |
| Volume Scale | A ducking factor to apply per older voice instance, which compounds based on scaling mode, and optionally revives them as they stop according to provided attack/release times. |
| Volume Scale Mode | Designates how to scale voice volume based on the number of member sounds active in the group. |
| Duck Time | The amount of time (in seconds) to apply the ducking factor using the volume scalar. |
| Can Recover | If enabled, volume scaling can recover from the volume ducking behavior when concurrency group sounds stop. This is only available when **Volume Scale Mode** is set to **Default**. |
| Recover Time | The amount of time (in seconds) to recover from the volume scalar duck. This is only available when **Can Recover** is enabled. |
| Voice Steal Release Time | The amount of time (in seconds) to fade out if a sound is culled due to another sound in the group starting. |
| **Advanced** |   |
| Asset User Data | An array of user data stored with this asset. |
| **Developer** |   |
| Debug | If enabled, the attenuation shape is drawn when the sound is audible. For debugging purposes only. |
| Duration | The duration of the sound in seconds. |
| Max Distance | The maximum distance as determined by the attenuation settings. |
| Total Samples | The total number of samples (in the thousands). This is useful to analyze the relative size of a given asset. This value can also be viewed in the context menu that displays while hovering over a Sound Cue in the **Content Drawer**. |

## Attenuation Node

The **Attenuation** node controls volume for a sound based on the distance of the sound source from the listener.

The **Attenuation Settings** can be set to an existing **Sound Attenuation** asset or manually specified in the node's properties by enabling the **Override Attenuation** setting.

For an overview on attenuation and how it works, see the [Sound Attenuation](/documentation/en-us/unreal-engine/sound-attenuation-in-unreal-engine) documentation.

![Attenuation Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/831f3114-e43b-4de8-b735-98cbb8e71d27/attenuation-sound-node.png)

| Property | Description |
| --- | --- |
| **Attenuation** |   |
| Attenuation Settings | This can be set to an existing **Sound Attenuation** asset to utilize that asset's settings. |
| Override Attenuation | If enabled, the existing attenuation settings will be overridden with the provided values. |
| **Attenuation (Volume)** |   |
| Enable Volume Attenuation | Enables or disables distance-based volume attenuation. |
| Attenuation Function | The type of attenuation function to use: Linear, Logarithmic, Inverse, Log Reverse, Natural Sound, or Custom |
| Attenuation At Max (dB) | (For **Attenuation Function**: Natural Sound) The attenuation volume at the falloff distance in decibels. |
| Falloff Mode | (For **Attenuation Function**: Natural Sound) Controls whether to continue attenuating, go silent, or hold the last volume value when beyond falloff bounds. Only editable if **Attenuation At Max (dB)** is set to a value of greater than -60dB. |
| Attenuation Shape | The shape for a non-custom attenuation function: Sphere, Capsule, Box, or Cone |
| Inner Radius | (For **Attenuation Shape**: Sphere) The radius that defines where sound attenuation begins (or where a custom attenuation curve begins). Sounds played at a distance less than this radius will not attenuate. |
| Capsule Half Height | (For **Attenuation Shape**: Capsule) The attenuation capsule's half height. |
| Capsule Radius | (For **Attenuation Shape**: Capsule) The attenuation capsule's radius. |
| Extents | (For **Attenuation Shape**: Box) The attenuation box's extents. |
| Cone Radius | (For **Attenuation Shape**: Cone) The attenuation cone's radius. |
| Cone Angle | (For **Attenuation Shape**: Cone) The attenuation cone's angle. |
| Cone Falloff Angle | (For **Attenuation Shape**: Cone) The attenuation cone's falloff angle. |
| Cone Offset | (For **Attenuation Shape**: Cone) The attenuation cone's offset. |
| Falloff Distance | The distance over which the volume attenuates. |
| **Attenuation (Spatialization)** |   |
| Enable Spatialization | When enabled, allow the input sound to be positioned in 3D space. |
| Spatialization Method | 
The method used to spatialize the sound:

-   **Panning:** The standard panning method for spatialization (linear or equal power method, as defined in project settings).
-   **Binaural:** If available, use the binaural spatialization method (requires headphones and is enabled by plugins).



 |
| Binaural Radius | The minimum radius to swap to non-binaural audio when a sound starts playing. |
| Non-Spatialized Radius | The distance from the origin where a sound is non-spatialized (2D). This prevents near-field audio from flipping as audio crosses the listener's position. |
| 3D Stereo Spread | The world-space distance between left and right stereo channels when stereo assets are 3D spatialized. |
| Normalize 3D Stereo Sounds | When enabled, applies a -6 dB attenuation to stereo Assets that are 3D spatialized. This avoids clipping when Assets have a spread of 0.0 due to channel summing. |
| Spatialization Plugin Settings | An array of settings assets for spatialization plugins. As this is an array, multiple settings can be applied. |
| **Attenuation (Occlusion)** |   |
| Enable Occlusion | Enables real-time occlusion tracing. |
| Occlusion Trace Channel | The type of trace channel to use for audio occlusion checks. |
| Occlusion Low Pass Filter Frequency | The low-pass filter frequency (in Hz) that applies if the sound playing in this audio component is occluded. This will override the `LowPassFilterFrequency` specified in code or Blueprints. A frequency of `0.0` is the device sample rate and will bypass the filter. |
| Occlusion Volume Attenuation | The amount of volume attenuation to apply to occluded sounds. |
| Occlusion Interpolation Time | The amount of time in seconds to interpolate to the target **Occlusion Low Pass Filter Frequency** when a sound is occluded. |
| Use Complex Collision for Occlusion | Enables tracing against complex collisions when doing occlusion traces. |
| Occlusion Plugin Settings | An array of settings assets for occlusion plugins. As this is an array, multiple settings can be applied. |
| **Attenuation (Submix)** |   |
| Enables Submix Send | Enables submix sends based on distance. |
| Submix Send Settings | When this feature is enabled, the Submix Send Settings expand into a full set of parameters. |
| **Attenuation (Reverb)** |   |
| Enable Reverb Send | Enables adjusting reverb sends based on distance. |
| Reverb Send Method | 

The method used to control master reverb sends:

-   **Linear:** Reverb send based on linear interpolation between distance and send-level ranges.
-   **Custom Curve:** Reverb sending based on a supplied curve. This can be set directly in the **Details Panel** or to an external curve by clicking on the triangle beside the parameter name and using the expanded **External Curve** parameter options.
-   **Manual:** Reverb send level that uses the manual setting specified below. Useful for 2D sounds.



 |
| Reverb Min Send Level | The amount to send to master reverb when sound is located at a distance equal to the value specified. |
| Reverb Max Send Level | The amount to send to master reverb when sound is located at a distance equal to the value specified. |
| Reverb Min Send Distance | The minimum distance to send to the master reverb. |
| Reverb Max Send Distance | The maximum distance to send to the master reverb. |
| Reverb Plugin Settings | An array of settings assets for reverb plugins. As this is an array, multiple settings can be applied. |
| **Attenuation (Focus)** |   |
| Enable Listener Focus | This enables listener focus-based adjustments. |
| Focus Azimuth | The azimuth angle (in degrees) relative to the forward vector of the listener which defines the focus region of sounds. The sounds playing at an angle less than this will be in-focus. |
| Non Focus Azimuth | The azimuth angle (in degrees) relative to the forward vector of the listener which defines the non-focus region of sounds. The sounds playing at an angle greater than this will be out-of-focus. |
| Focus Distance Scale | The amount to scale the distance calculation for in-focus sounds. This can be used to make in-focus sounds seem closer or further away than they actually are. |
| Non Focus Distance Scale | The amount to scale the distance calculation for out-of-focus sounds. This can be used to make out-of-focus sounds seem closer or further away than they actually are. |
| Focus Priority Scale | The amount to scale the priority of sounds that are in-focus. |
| Non Focus Priority Scale | The amount to scale the priority of sounds that are not in-focus. |
| Focus Volume Attenuation | The amount to attenuate sounds that are in-focus. This can be overridden at the sound level. |
| Non Focus Volume Attenuation | The amount to attenuate sounds that are not in-focus. This can be overridden at the sound level. |
| Enable Focus Interpolation | This enables focus interpolation to smooth focus transition in and out. |
| Focus Attack Interp Speed | The scalar value used to increase interpolation speed upward to the target focus value. This option requires **Enable Focus Interpolation** to be enabled. |
| Focus Release Interp Speed | The scalar value used to increase interpolation speed downward to the target focus value. This option requires **Enable Focus Interpolation** to be enabled. |
| **Attenuation (Priority)** |   |
| Enable Priority Attenuation | Enables attenuation of sound priority based on distance. |
| Priority Attenuation Method | 

The method used to control priority attenuation:

-   **Linear:** Priority attenuation based on linear interpolation between distance and priority-attenuation ranges.
-   **Custom Curve:** Priority attenuation based on a supplied curve. This can be set directly in the **Details Panel** or to an external curve by clicking on the triangle beside the parameter name and using the expanded **External Curve** parameter options.
-   **Manual:** Priority attenuation based on the given **Attenuation Priority** value. This is useful for 2D sounds.



 |
| Priority Attenuation At Min Distance | The interpolated value to scale priority against when the sound is at the minimum priority attenuation distance from the closest listener. |
| Priority Attenuation At Max Distance | The interpolated value to scale priority against when the sound is at the maximum priority attenuation distance from the closest listener. |
| Priority Attenuation Min Distance | The minimum distance to attenuate priority. |
| Priority Attenuation Max Distance | The maximum distance to attenuate priority. |
| Attenuation Priority | (For **Priority Attenuation Method**: Manual) The priority level entered is static and does not change with distance. |
| **Attenuation (Air Absorption)** |   |
| Enable Air Absorption | Enables air absorption simulation by applying a filter with a cutoff frequency as a function of distance. |
| Min Distance Range | The minimum distance to apply an absorption low pass filter. Absorption frequency cutoff interpolates filter frequency ranges between **Min Distance Range** and **Max Distance Range**. |
| Max Distance Range | The maximum distance to apply an absorption low pass filter. Absorption frequency cutoff interpolates filter frequency ranges between **Min Distance Range** and **Max Distance Range**. |
| Low Pass Cutoff Frequency Min | The minimum range of the cutoff frequency (in Hz) for the low pass absorption filter. |
| Low Pass Cutoff Frequency Max | The maximum range of the cutoff frequency (in Hz) for the low pass absorption filter. |
| High Pass Cutoff Frequency Min | The minimum range of the cutoff frequency (in Hz) for the high pass absorption filter. |
| High Pass Cutoff Frequency Max | The maximum range of the cutoff frequency (in Hz) for the high pass absorption filter. |
| Enable Log Frequency Scaling | This enables perceptually linear frequency sweeping by applying a log scale to frequency values. |
| Absorption Method | 

The method used to map distance values to frequency absorption values:

-   **Linear:** The air absorption conforms to a linear distance function.
-   **Custom Curve:** The air absorption conforms to a custom distance curve. This can be set directly in the **Details Panel** or to an external curve by clicking on the triangle beside the parameter name and using the expanded **External Curve** parameter options.



 |
| **Attenuation (Source Data Override)** |   |
| Enable Source Data Override | Enables overriding WaveInstance data using source data override plugins. |
| Source Data Override Plugin Settings | An array of settings assets for source data override plugins. As this is an array, multiple settings can be applied. |

Stereo files play evenly on the left and right channels, and attenuate to allow volume fades between the Radius Min and Radius Max values, but they are not spatialized.

Sound Cues that do not contain an Attenuation node are not localized, and play consistently at the Sound Cue volume setting.

## Branch Node

The **Branch** node selects an input node based on the value of a named Boolean parameter of **True**, **False** or **Parameter Unset**.

Parameter Unset is the output that plays when the value of a named parameter has not been set. For example, if the parameter is saved as `Name` in the Branch node, but the user hasn't called `SetBooleanParam(Name, [true or false])`, the Sound Cue will use the Parameter Unset input pin, not the True or False pin.

For more information about named parameters, see the [Named Parameters](/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine#namedparameters) section of this page.

![Branch Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e265807-2d0a-459f-9c77-13955b8590b2/branch-sound-node.png)

| Property | Description |
| --- | --- |
| Bool Parameter Name | The name of the Boolean parameter that determines which input node is used. |

## Concatenator Node

The **Concatenator** node is used to play sounds sequentially (for example, creating a simple BGM playlist that plays through a series of specified tracks). While this node handles sequential playback, it will also add a small delay between each asset.

Initially, this node has two input pins. You may add more pins by clicking the **Add input** button on the node or remove pins by right-clicking them and selecting "Delete Input" from the context menu.

![Concatenator Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5c6c6f5-17ed-4794-9cee-1ec4d8281035/concatenator-sound-node.png)

| Property | Description |
| --- | --- |
| Input Volume | An array which stores the volume multiplier for each attached input sound. |

## Continuous Modulator Node

The **Continuous Modulator** node provides a way to control named parameters for volume and pitch modulation in real time. A typical example would be using the velocity of a vehicle to correspond to the pitch of an engine sound. This modulator needs to be hooked up in code or Blueprint to work, and does not function on its own within the Sound Cue Editor. However, you can change pitch and volume from within the Sound Cue Editor.

By setting maximum and minimum values, you can determine the range of randomization.

The pitch and volume of the input sound will default to a uniform distribution, but you can change them in the Sound Cue Editor to any other type.

For more information about named parameters, see the [Named Parameters](/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine#namedparameters) section of this page.

![Continuous Modulator Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f88320cc-12ba-4177-a09a-47723361e6e6/continuous-modulator-sound-node.png)

| Property | Description |
| --- | --- |
| **Pitch Modulation Params** |   |
| Parameter Name | The name of the sound instance parameter being used to manipulate pitch. |
| Default | The default pitch value used if no parameter is found. |
| Min Input | The minimum input pitch value. Values will be clamped to the `[MinInput, MaxInput]` range. |
| Max Input | The maximum input pitch value. Values will be clamped to the `[MinInput, MaxInput]` range. |
| Min Output | The minimum output pitch value. This value is scaled from the `[MinInput, MaxInput]` range to the `[MinOutput, MaxOutput]` range. |
| Max Output | The maximum output pitch value. This value is scaled from the `[MinInput, MaxInput]` range to the `[MinOutput, MaxOutput]` range. |
| Param Mode | 
The mode with which the parameter is applied:

-   **Normal:** Clamps input value to the range (MinInput, MaxInput), then maps to the range (MinOutput, MaxOutput).
-   **Absolute:** Same as Normal, except that the input value is treated as an absolute value.
-   **Direct:** Uses the input value directly, without scaling or reference to Min or Max input or output values.



 |
| **Volume Modulation Params** |   |
| Parameter Name | The name of the sound instance parameter being used to manipulate volume. |
| Default | The default volume value used if no parameter is found. |
| Min Input | The minimum input volume value. Values will be clamped to the `[MinInput, MaxInput]` range. |
| Max Input | The maximum input volume value. Values will be clamped to the `[MinInput, MaxInput]` range. |
| Min Output | The minimum output volume value. This value is scaled from the `[MinInput, MaxInput]` range to the `[MinOutput, MaxOutput]` range. |
| Max Output | The maximum output volume value. This value is scaled from the `[MinInput, MaxInput]` range to the `[MinOutput, MaxOutput]` range. |
| Param Mode | 

The mode with which the parameter is applied:

-   **Normal:** Clamps input value to the range (MinInput, MaxInput), then maps to the range (MinOutput, MaxOutput).
-   **Absolute:** Same as Normal, except that the input value is treated as an absolute value.
-   **Direct:** Uses the input value directly, without scaling or reference to Min or Max input or output values.



 |

## Crossfade by Distance Node

The **Crossfade by Distance** node provides the ability to fade between two or more input sounds based on the distance from the Sound Cue's origin to the listener.

For example, a gunshot heard at a distance will sound different from a gunshot up close. This node can calculate the distance the listener is from the shot and play the sound based on a short or long distance, or a mix of the two.

This node differs from the Attenuation node in that the sound will only play if it is within the minimum and maximum distance settings.

Sound Nodes can be connected directly to the Crossfade by Distance node inputs, but you can also add nodes between them for independent control per layer.

Initially, this node has two input pins. Add more pins by clicking **Add input**.

![Crossfade by Distance Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8db18fac-28bb-456c-9305-86753438434d/crossfade-by-distance-sound-node.png)

| Property | Description |
| --- | --- |
| **Cross Fade Input** |   |
| Fade in Distance Start | The distance from the listener's position at which the sound begins to be audible. |
| Fade in Distance End | The distance from the listener's position at which the sound reaches full volume. |
| Fade Out Distance Start | The distance from the listener's position at which the sound begins to fade out. |
| Fade Out Distance End | The distance from the listener's position at which the sound is no longer audible. |
| Volume | The maximum volume of the input sound. |

If you want to hear the sound up close, then setting **Fade in Distance Start** to 0 might be a good option.

These values can be set independently for each attached sound.

## Crossfade by Param Node

The **Crossfade by Param** node works similarly to the **Crossfade by Distance** node, except that the **Crossfade by Param** node provides a way for you to manipulate the value of a named parameter that controls the crossfade programmatically (with code or Blueprints).

Initially, this node has two input pins. You may add more pins by clicking the **Add input** button on the node or remove pins by right-clicking them and selecting "Delete Input" from the context menu.

For more information about named parameters, see the [Named Parameters](/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine#namedparameters) section of this page.

![Crossfade by Param Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f32298f-c586-4d30-9cde-68d8ccd27684/crossfade-by-param-sound-node.png)

| Property | Description |
| --- | --- |
| Param Name | The name of the parameter used to control the crossfade. |
| **Cross Fade Input** |   |
| Fade In Param Value Start | The parameter value at which the sound begins to be audible. |
| Fade In Param Value End | The parameter value at which the sound reaches full volume. |
| Fade Out Param Value Start | The parameter value at which the sound begins to fade out. |
| Fade Out Param Value End | The parameter value at which the sound is no longer audible. |
| Volume | The maximum volume of the input sound. |

If you want to hear the sound up close, then setting **Fade in Param Value Start** to 0 might be a good option.

The **Crossfade by Param** node does not support negative values.

### Crossfade by Param Example

Click image for full size.

The diagram above shows the expected volume change over time of two parameters based on the the given property values.

## Delay Node

The **Delay** node inserts a delay into the Sound Node chain to cause a pause before the input sound is passed to the output. The amount of the delay is a random value between the **Delay Min** and **Delay Max** values specified in the **Details** panel.

![Delay Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86572586-623c-403d-a6a4-1ac05456a06f/delay-sound-node.png)

| Property | Description |
| --- | --- |
| Delay Min | Sets the lower bound of time in seconds for the pause. |
| Delay Max | Sets the upper bound in seconds. |

## Dialogue Player Node

The **Dialogue Player** node is a way to set up a **Dialogue Wave** asset to be played under specific conditions.

Since Dialogue Waves are expected to be used purely for spoken dialogue, the Dialogue Player node requires that you specify both the speaker and the targets of the dialogue being played. This allows the Dialogue Wave to play the correct audio Asset depending on the specific context, such as plurality, gendered language, or for localization purposes.

![Dialogue Player Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52f20f84-1244-4e67-b849-6b8e8ec91e63/dialogue-player-sound-node.png)

| Property | Description |
| --- | --- |
| Dialogue Wave | The Dialogue Wave that the node will play. Click the dropdown to browse for the Asset you want to use. |
| Context | Who is speaking, and to whom. Note that this can only be used once a valid Dialogue Wave is entered. |
| Looping | When enabled, the dialogue will play on a loop. |

## Doppler Node

The **Doppler** node simulates a Doppler effect, in which a sound's pitch changes based on the source's movement in relation to the listener. The pitch will increase as the source approaches the listener and will decrease as the source moves away.

A common real world example of this is the sound of a passing ambulance's siren.

![Doppler Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e01982a-2e5d-4b0f-afb7-cae25fed41da/doppler-sound-node.png)

| Property | Description |
| --- | --- |
| Doppler Intensity | A multiplier value for how strongly the Doppler effect is heard. Increase the value to make the effect more pronounced. |
| Use Smoothing | When enabled, the node performs a smooth interpolation on the Doppler effect. |
| Smoothing Interp Speed | The speed at which the pitch scale is interpolated. |

## Enveloper Node

The **Enveloper** node creates an envelope where a sound's volume and pitch are manipulated over a specified time period via distribution curves. These curves can be edited using the embedded **Curve Editors**, or can be based on curves defined in an existing Float Curve Asset already in the **Content Browser**.

Optionally, the envelope can be set to loop a set number of times or even indefinitely.

You can use the properties in the **Modulation** category to randomize predefined values across set points on the envelope.

![Enveloper Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d244d3c8-cc30-4398-9e7b-3083214064f7/enveloper-sound-node.png)

| Property | Description |
| --- | --- |
| **Looping** |   |
| Loop Start | The time in seconds where the envelope's loop begins. |
| Loop End | The time in seconds where the envelope's loop ends. |
| Duration After Loop | The time in seconds it takes the envelope to fade out after the last loop is completed. |
| Loop Count | The number of times the envelope will loop if looping is enabled and the envelope is not set to loop indefinitely. |
| Loop Indefinitely | If enabled, the envelope will continue to loop indefinitely regardless of **Loop Count** value. |
| Loop | If enabled, the envelope will loop using the specified loop settings. |
| **Envelope** |   |
| Volume Curve | The distribution curve that defines the volume envelope. This can be set directly in the **Details Panel** or to an external curve by clicking on the triangle beside the parameter name and using the expanded **External Curve** parameter options. |
| Pitch Curve | The distribution curve that defines the pitch envelope. This can be set directly in the **Details Panel** or to an external curve by clicking on the triangle beside the parameter name and using the expanded **External Curve** parameter options. |
| **Modulation** |   |
| Pitch Min | The minimum pitch for the input sound. |
| Pitch Max | The maximum pitch for the input sound. |
| Volume Min | The minimum volume for the input sound. |
| Volume Max | The maximum volume for the input sound. |

## Group Control Node

The **Group Control** node controls which sounds are played based on the number of active sounds, while giving priority to the first available group.

Initially, this node has two input pins. You may add more pins by clicking the **Add input** button on the node or remove pins by right-clicking them and selecting "Delete Input" from the context menu.

![Group Control Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e34c73a-77f6-4cde-8619-6d14c2d1a8c0/group-control-sound-node.png)

| Property | Description |
| --- | --- |
| Group Sizes | The maximum number of Sound Wave sources allowed for each group, minus 1 (the first Sound Wave Node is node **0**). |

## Looping Node

The **Looping** node is used to loop sound indefinitely or a set number of times.

You can loop multiple audio files independently when used in conjunction with the **Mixer** node.

![Looping Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5c4380fa-23b5-442b-8e59-287358746d85/looping-sound-node.png)

| Property | Description |
| --- | --- |
| Loop Count | The number of times to loop the input sound. This can only be edited if the **Loop Indefinitely** option is disabled. |
| Loop Indefinitely | When enabled, loop indefinitely regardless of the **Loop Count** value. |

A **Looping** node should only be used for logical or procedural looping such as introducing a delay because these sounds will not play seamlessly. If you want a sound to loop seamlessly and indefinitely, use the **Looping** flag on the **Wave Player** node (see below) for the sound.

## Mature Node

With the **Mature** node, you can flag input nodes as intended for mature audiences. This node uses the value of `UEngine:bAllowMatureLanguage` to determine whether input nodes should be played.

Initially, this node has two input pins. You may add more pins by clicking the **Add input** button on the node or remove pins by right-clicking them and selecting "Delete Input" from the context menu.

![Mature Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8b73894-ffd3-41da-bf6f-2dfc225ccd5c/mature-sound-node.png)

## Mixer Node

The **Mixer** node defines how concurrent sounds in a Sound Cue are mixed together by providing volume control for each individual input.

Initially, this node has two input pins. Add more pins by clicking **Add input**.

![Mixer Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32616e53-0948-4536-a439-874cb43c88d8/mixer-sound-node.png)

| Property | Description |
| --- | --- |
| Input Volume | The list of volumes to use for each of the input sounds, allowing normalization with different source volumes. The topmost input is represented by index 0 and each additional input is incremented in order. |

## Modulator Node

The **Modulator** node is used to randomize volume and pitch modulation. You can set maximum and minimum values to determine the range of randomization. When the Sound Cue is triggered, it randomly selects a value within that range.

To set a consistent level for volume or pitch, set the same values for both the minimum and maximum values. This node can also be used to adjust relative volumes of multiple Sound Wave nodes contained within a Sound Cue.

If the **Modulator** node is used in combination with the **Looping** node, it will randomize on the each **Sound Cue** trigger and not on each individual loop.

![Modulator Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a3ee093e-8732-4c60-a9e0-6be1c839e142/modulator-sound-node.png)

| Property | Description |
| --- | --- |
| Pitch Min | Sets the minimum pitch for the input sound. |
| Pitch Max | Sets the maximum pitch for the input sound. |
| Volume Min | Sets the minimum volume for the input sound. |
| Volume Max | Sets the maximum volume for the input sound. |

## Oscillator Node

The **Oscillator** node is used to introduce continuous pitch and volume oscillation. This is useful when looping sounds to create a greater degree of ongoing movement.

By setting maximum and minimum values, you can determine the range of randomization.

![Oscillator Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca8dcb2a-5e85-44e4-8b4f-637105eee618/oscillator-sound-node.png)

| Property | Description |
| --- | --- |
| Modulate Volume | Enables volume modulation. |
| Modulate Pitch | Enables pitch modulation. |
| Amplitude Min | The minimum amplitude of the sine wave's modulation, centered around the value set by Center Min and Center Max. For example, an amplitude of 0.25 would oscillate between 0.75 and 1.25. |
| Amplitude Max | The maximum amplitude of the sine wave's modulation, centered around the value set by Center Min and Center Max. For example, an amplitude of 0.25 would oscillate between 0.75 and 1.25. |
| Frequency Min | The minimum frequency of the sine wave's modulation, with the value divided by two to equal to the hertz rate. For example, a frequency of 20 would oscillate at 10Hz. |
| Frequency Max | The maximum frequency of the sine wave's modulation, with the value divided by two to equal to the hertz rate. For example, a frequency of 20 would oscillate at 10Hz. |
| Offset Min | The minimum offset value into the sine wave, commonly called phase. The value entered here will be multiplied by 2π. |
| Offset Max | The maximum offset value into the sine wave, commonly called phase. The value entered here will be multiplied by 2π. |
| Center Min | Both Center Min and Center Max default to 0. Because the default is 0 (not 1), if the amplitude is .2, the sample will be multiplied between -.2 and .2 (instead of .8 and 1.2). |
| Center Max | See Center Min. |

## Quality Level Node

By default, there are no quality levels; the designer must add them to the Project Settings for the node inputs to populate. Once populated, node branching can be used to switch between various levels of SoundCue graph complexity. This provides a way for designers to use simpler SoundCue graphs for lower-powered platforms.

![Quality Level Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9886e3a8-b0e8-4fbf-bc7c-8848dbf910f6/quality-level-sound-node.png)

The **Quality Level** node uses `GameUserSettings AudioQualityLevel` (or the editor override) to choose which branch to play.

At runtime, this node will only load into memory the Sound Waves connected to the branch that is selected.

## Random Node

The **Random** node is used to randomly trigger a node from the list of connected input nodes. Weight values control the probability of a node being triggered relative to the other nodes connected to the Random node.

When an input node is selected randomly, the Sound Cue will play the entire data flow of that selected input.

Initially, this node has two input pins. You may add more pins by clicking the **Add input** button on the node or remove pins by right-clicking them and selecting "Delete Input" from the context menu.

![Random Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/acbdb0fe-782b-4db2-9a17-a8c213b66e15/random-sound-node.png)

| Property | Description |
| --- | --- |
| Weights | The list of weights for each input sound that determines the odds that a particular sound will be chosen. Each item in the Array can be assigned its own weight value. |
| Preselect at Level Load | If greater than 0, then upon each level load the specified number of inputs will be randomly selected and the rest will be removed. This can be used to cut down the memory usage of large randomizing cues. This setting does not apply during Play In Editor or Simulate; it applies only in game builds outside of Unreal Editor. |
| Should Exclude from Branch Culling | If set to true, this node will not be culled on load for platforms with a maximum amount of preloaded random branches set in the project settings. |
| Randomize Without Replacement | When enabled, the entire list of Sound Nodes will be exhausted before repeating a sound. |

## SoundClass Node

The **SoundClass** node provides a way to remap which **Sound Class** asset used with the input node.

For more information about named parameters, see the [Named Parameters](/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine#namedparameters) section of this page.

![SoundClass Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca9b115b-0cbe-48c8-a7d0-f38d9d3fdbad/soundclass-sound-node.png)

| Property | Description |
| --- | --- |
| Sound Class Override | The Sound Class Asset that will override the current Sound Class for the input node. |

## Switch Node

The **Switch** node selects an input node based on the value of a runtime integer parameter. The specified parameter must be declared in either code or Blueprints.

Initially, this node has four input pins. You may add more pins by clicking the **Add input** button on the node or remove pins by right-clicking them and selecting "Delete Input" from the context menu.

For more information about named parameters, see the [Named Parameters](/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine#namedparameters) section of this page.

![Switch Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b40cfa7-42b1-4785-aa57-9a784e18e52d/switch-sound-node.png)

| Property | Description |
| --- | --- |
| **Switch** |   |
| Int Parameter Name | The name of the integer parameter that determines which input is used. |

## Wave Param Node

The **Wave Param** node uses a named parameter to determine whether to play a different Sound Wave than the one feeding into the input pin. If the specified parameter is set to the name of a valid Sound Wave asset, that asset is played.

If an optional input node is connected and the named parameter is valid, the Wave Param will override the input node when the Sound Cue is played.

For more information about named parameters, see the [Named Parameters](/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine#namedparameters) section of this page.

A potential use for this node would be to play dynamic dialogue lines in between static blip sounds in order to simulate dialogue over a radio. In this way, the same Sound Cue can be reused to great effect.

![Wave Param Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e465f02d-cd01-470d-bf21-0521439ae5d2/wave-param-sound-node.png)

| Property | Description |
| --- | --- |
| Wave Parameter Name | The name of the Sound Wave asset to play. If the Sound Wave asset specified does not exist, then the input node is evaluated to determine which sound to play instead. |

## Wave Player Node

The **Wave Player** node contains a reference to a Sound Wave asset to be played with the Sound Cue.

![Wave Player Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05989665-9a36-4a3b-8ab5-c1b12bfd0f89/wave-player-sound-node.png) ![Looping Wave Player Sound Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8400c770-fce5-490f-a768-48416573dcbd/looping-wave-player-sound-node.png)

| Property | Description |
| --- | --- |
| Sound Wave | The Sound Wave Asset to use in this node. |
| Looping | When enabled, the Sound Wave will play on a loop. Additionally, the node type displayed in the Sound Node Graph will be changed to "Looping Wave Player." |

## Add Comment

Comments can be added anywhere on the Sound Cue. They do not affect the output, but instead are used to call attention to or explain details in the node arrangements or uses.

The comment appears at the top of the frame. There is no limit to the length of the comment.

![Add Comment Box](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7fbad4a8-47b6-4fbf-8145-e2a9b661d156/add-comment-box.png)

The comment frame's size can be changed by dragging the lines in the lower right corner and the position can be changed by dragging from anywhere else on the frame. Wherever positioned, it will appear behind the nodes.

If you move a comment box, it will bring any fully contained Sound Nodes along with it.

You can also add a comment by selecting multiple nodes, right-clicking a selected node, and then selecting **Create Comment from Selection** from the context menu.

## Examples

Below are examples of more complex Sound Cue arrangements. You can click on each image to expand it.

This Sound Cue plays one sound if a parameter is set to true, and another if it is set to false.

This Sound Cue changes the Sound Classes of the Sound Waves.

This Sound Cue mixes together Sound Waves with a variety of properties, including attenuation, randomization, looping, and delays.