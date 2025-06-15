# Ambient Sound Actor User Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ambient-sound-actor-user-guide-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ambient-sound-actor-user-guide-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:32

---

Unreal Engine streamlines the process by which you can produce or modify ambient sounds through the use of the **Ambient Sound Actor**. When a **Sound Wave** or **Sound Cue** asset is placed in a level, an Ambient Sound Actor with that sound asset is created. The Ambient Sound Actor has several properties which are covered on this page that will allow you to modify how players receive the sound.

For more information on importing files as [Sound Waves](/documentation/en-us/unreal-engine/importing-audio-files) or modifying files through [Sound Cues](/documentation/en-us/unreal-engine/sound-cue-editor-in-unreal-engine), refer to their respective pages for additional documentation.

## Ambient Sound Actor

![The Ambient Sound Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d274246-f668-4e9c-b6b2-7ff9f647cb42/01-ambient-actors.png)

The Ambient Sound Actor can be used for many purposes such as ambient looping sounds as well as non-looping sounds. Generally, the Ambient Sound Actor conforms to the real world where the closer you are to a sound, the louder it will appear. By comparison, a sound that is normally loud, may appear soft if it is further away.

If the Ambient Sound Actor is set to **Auto Activate**, it will immediately begin to play once it is created (at the beginning of play or on spawn), even if the player is not in a position to hear it.

The sound asset the Ambient Sound Actor points to will only play once per trigger unless specified as **Looping** in the Sound Wave or defined as part of a Sound Cue asset.

You can add an Ambient Sound Actor to your level in several ways:

1.  Select the Ambient Sound Actor from the **Place Actors** panel in the **All Classes** tab and drag it into your level as seen below.

![Add an Ambient Sound Actor From the Place Actors Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc247070-5ec6-4313-82e7-ec8b59d7d341/02-drag-ambient-sound-from-place-actors-panel.png)

1.  Right-click in your level and select **Place Actor** from the context menu.

![Add an Ambient Sound Actor From the Context Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ee2e9df6-be62-4167-9d24-4f801312de64/03-place-actor-from-level.png)

1.  Open the **Actor** menu in the Menu bar and select **Place Actor**.

![Add an Ambient Sound Actor From the Actor Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37dcade2-d013-46dc-a2bf-4518c2824d7e/04-place-actor-from-the-actor-menu.png)

1.  Drag a Sound Wave or Sound Cue from the **Content Browser** into your level.

![Drag a Sound From the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d4096e8-0ad8-4cae-9e0b-2c5a26721580/04-drag-a-sound-from-the-content-browser-into-the-level.png)

### Sound Properties

An Ambient Sound Actor has no function without an associated sound asset. You can assign a sound asset from the **Details** panel by selecting an asset from the **Sound** setting's drop-down menu or by highlighting a sound asset in the **Content Browser** and clicking the ![Arrow Button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6ce67607-8d16-4aa0-a6f7-ba205690e97e/05-sound-actor-arrow.png) button.

Click image for full size.

Once a Sound Cue asset has been assigned as the associated sound, the **Edit** option will become available so that you can open the Sound Cue asset up for editing inside the **Sound Cue Editor**. Optionally, instead of assigning a sound asset, you can select the **New** option which will create a new Sound Cue asset and will open it in the **Sound Cue Editor** for editing.

The **Play** and **Stop** options allow you to preview the assigned sound inside the editor and will play and stop playing the sound respectively.

Click image for full size.

Additional options inside the **Sound** section of the **Details** panel are defined below.

| Property | Description |
| --- | --- |
| **Sound** | Points to a Sound Wave or Sound Cue asset. |
| **Volume Multiplier** | Modifier applied to set the overall Volume of the sound. |
| **Pitch Multiplier** | Modifier applied to set the overall Pitch of the sound. |
| **Is UI Sound** | Whether or not the sound asset plays when the game is paused. |
| **Low Pass Filter Frequency** | Enable to set the frequency (in Hz) of the low pass Filter. A frequency of 0.0 is the device sample rate and will bypass the filter. |
| **Priority** | Enable to override the priority of selected sound with the value provided. |
| **Play Multiple Instances** | If true, the Audio Component plays multiple sound instances at once. |
| **Source Effect Chain** | Determines a chain of source effects to apply to the sounds playing on the Audio Component. |

### Attenuation Properties

Attenuation is the ability of a sound to decrease in volume as the player moves away from it. It works using two radii: **MinRadius** and **MaxRadius**. As you move from the sound's origin through the MinRadius, the volume of the sound is at 100%. As you move within the space between the MinRadius and the MaxRadius, the volume level is adjusted based on the **Distance Algorithm**. Outside of the MaxRadius, the volume of the sound is at 0%.

It is advisable to use **Sound Attenuation** objects whenever possible, if for no other reason than to give broad control over the settings for many Actors.

For additional information on Attenuation, please refer to the [Attenuation Overview](/documentation/en-us/unreal-engine/sound-attenuation-in-unreal-engine) page.

![Sound Actor Attenuation Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e52bb40c-3520-4072-a778-f0da05e12e3a/08-sound-actor-attenuation-properties.png "Sound Actor Attenuation Properties")

The options under the **Attenuation** section that can be modified inside the **Details** panel are defined below:

| Property | Description |
| --- | --- |
| **Allow Spatialization** | Enables or disables spatialization of the audio component. |
| **Override Attenuation** | Uses the asset's Attenuation settings or the Attenuation Override's settings. |
| **Attenuation Settings** | Points to and uses the settings assigned inside a SoundAttenuation asset. |

When **Override Attenuation** is checked, the ability to modify settings on the following sections becomes available:

| Section | Description |
| --- | --- |
| **Attenuation (Volume)** | Properties in this section define how the sound's volume will attenuate as the listener moves away from it. |
| **Attenuation (Spatialization)** | Properties in this section define how the sound will spatialize in the game world. |
| **Attenuation (Occlusion)** | Properties in this section control real-time occlusion tracing. |
| **Attenuation (Submix)** | Properties in this section control sending sound sources to a submix. |
| **Attenuation (Reverb)** | Properties in this section define the relationship between the sound's distance from the listener and the amount of reverb that is applied to the sound. |
| **Attenuation (Focus)** | Properties in this section control some additional processing that you can use to the 'focus behavior' of sounds. |
| **Attenuation (Priority)** | Properties in this section control attenuation of sound priority based on distance. |
| **Attenuation (Air Absorption)** | Properties in this section define the behavior of the algorithm that attempts to model the effect air absorption has on the sound. |

### Modulation Properties

![Sound Actor Modulation Properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/156ee75e-04a6-4ae3-82ce-34cdd0c1c85b/09-sound-actor-modulation-properties.png "Sound Actor Modulation Properties")

The **Modulation** settings define what settings to use for **Volume**, **Pitch**, **Highpass** and **Lowpass** modulation. There are three options available:

-   **Disable**: Disables modulation routing.
-   **Inherit**: The Audio Component inherits modulation settings from its parent Sound.
-   **Override**: Ignores inherited settings and allows you to set the base value, enable or disable modulation and set the modulation source for each parameter.

For additional information on Modulation, please refer to the [Overview of Audio Modulation in Unreal Engine](/documentation/en-us/unreal-engine/audio-modulation-in-unreal-engine) page.

## Adding Audio Components To Blueprints

Inside a **Blueprint**, in the **Component** panel, select the **Add Component** button and select the **Audio** component.

![Add Audio Component in a Blueprint](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c83bb0ff-347f-4989-8dca-64a1cb2ed92d/10-add-audio-component-in-a-blueprint.png "Adding an Audio Component Inside a Blueprint")

The **Audio** component can be referenced through Blueprints and many of its settings can be altered by using different types of functions.

![Connecting Audio Component to a Function in the Graph Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/066f2c85-a8aa-41df-bbef-5149075e8b78/11-audio-component-functions.png "Connecting Audio Component to a Function in the Graph Editor")

The **Audio** component does have a unique event which can be used. This **OnAudioFinished** event allows you to fire off events when the audio is finished playing or is stopped prematurely with a **Stop** function.

## Audio Volumes

For an added level of control, you can include **Audio Volumes** in conjunction with **Ambient Sound Actors**. For more information on how to use an Audio Volume, refer to the [Audio Volumes](/documentation/en-us/unreal-engine/audio-volumes-in-unreal-engine) page.

Making changes to an Audio Volume will not work in real time inside the editor. You will need to rebuild the geometry of the level that contains the edited volume in order for your changes to take effect.