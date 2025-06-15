# Audio Track

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-audio-track-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-audio-track-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:56

---

You can add [Sound Waves](/documentation/en-us/unreal-engine/sound-waves) and [Sound Cues](/documentation/en-us/unreal-engine/sound-cues-in-unreal-engine) using Seqeuncer's **Audio Track** to add sounds to your cinematics in Unreal Engine. Similar to other film editing software, the Audio Track provides controls for adjusting the volume, pitch, and crossfading sounds together.

This document provides an overview of the creation and usage of the audio track.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).
    
-   You have a basic understanding of [How to Import Audio Files](/documentation/en-us/unreal-engine/importing-audio-files) or your project already contains audio files.
    

## Create an Audio Track

To create a new Audio Track, open a **Level Sequence** in the [Sequencer Editor](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine), and use **Track** (**+**) to select **Audio Track**.

![add new audio track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ac798ac7-6af5-4087-824f-0d6ebd1c8595/addnewaudiotrack.png)

After creating an Audio Track in your Level Sequence you can add an audio section to the track at the location of your [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead), by clicking the **Audio** (**+**) dropdown on the track and selecting a [Sound Waves](/documentation/en-us/unreal-engine/sound-waves) and [Sound Cues](/documentation/en-us/unreal-engine/sound-cues-in-unreal-engine) asset.

![add audio asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66ae3c81-6241-4ce2-9dda-f9e5036dab20/addaudioasset.png)

You can also drag **Sound Waves** and **Sound Cues** from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) into your sequence, which will automatically create the Audio Track and add the sound.

![adding audio asset demo](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e410516c-bee7-492f-b740-fc900c4d3ed3/addaudiodemo.gif)

Additional audio clip sections can be added to the same audio track for linear playback. You can also add additional Audio Tracks for layered audio playback and blending, each with their own mixing and object binding properties.

![wroking with multiple audio assets and tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4641626a-c024-462f-a9fd-dc95c9481f3d/multiaudiotracks.png)

## Working With Audio Sections

Similar to most [Sequencer Sections](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#sections), **Audio Sections** can be edited by trimming, looping, and moving sections within the Sequencer Editor. Audio Sections can also be attached to other [Skeletal Meshes](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine), and [Object Actors](/documentation/en-us/unreal-engine/unreal-engine-actors-reference), in order to create dynamic [sound sources](/documentation/en-us/unreal-engine/sound-sources-in-unreal-engine) and [spatial sounds](/documentation/en-us/unreal-engine/spatialization-overview-in-unreal-engine).

### Editing Audio Sections

Like most sections in Sequencer, audio sections [can be edited](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#interactionanddisplay) in the following ways:

-   Dragging the left and right edges of an audio section will trim the **Start** and **End** times.
    
-   Dragging the end time past the duration of the clip will cause the sound to **Loop** for the trimmed duration.
    

![trimming audio assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0c90507d-3e4b-4d11-a762-d3ca2ae944a7/audiotrimming.gif)

Audio sections that have been trimmed or edited from their default lengths may not play correctly due to the **Platform Specific** codec settings. To fix this, you must ensure that **Sound Asset Compression Type** is set either to **Bink Audio** or **PCM**. This property is found within the Sound Wave Asset.

![codec settings compression audio](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e06783c-9a37-40a5-b155-bf568975e94a/codecsettings.png)

### Blending Audio Sections

Dragging the upper corner edges of an audio section will cause the volume to blend up and down for the duration of the blend.

![audio asset fade handles](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a826670-a889-4bcd-b57a-5165d9422401/audiofadehandles.gif)

Intersecting two or more sound sections will cause them to crossfade for the duration of the overlap. You can adjust the crossfade between the clips by clicking and dragging the fade handles on each clip independently.

![blandning audio assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2da74bea-57d6-4848-bdb4-a400c8bb7ff6/audioblending.gif)

For more information about blending techniques and properties you can use on audio sections, see the [Keyframe Blending](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#blending) documentation.

### Attaching Sounds

You can create spatial audio effects for more immersive and dynamic cinematic audio, such as 3D sound and distance falloff, by attaching Audio Tracks to characters and objects within the Level Sequence. To attach an audio track to a source within your level sequence, expand the Audio Track in the Sequence Editor's outline and select a source from the **Attach** property's drop-down menu.

![attach audio tracks to objects](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/010d8f09-4a2b-4793-b14a-682be6251bb0/attachobject.png)

You can only attach Audio Tracks to Actors that are currently referenced in your Level Sequence.

After attaching an Audio Track, you must specify an [Attenuation Mode](/documentation/en-us/unreal-engine/sound-attenuation-in-unreal-engine) for each audio clip in the track to drive its 3D audio behavior. To specify an Attenuation mode, right-click an audio section and navigate to the **Properties** section. Then select a mode from the **Attenuation** mode property's drop-down menu or **Create New Asset**.

If your Sound Wave or Cue asset already has a Sound Attenuation specified, then you do not need to specify a Sound Attenuation asset for the audio section.

![sound attenuation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05284c0a-55a2-4788-bb6a-9d156759337f/soundattenuation.png)

If you are unfamiliar with **Sound Attenuation** assets, the [Meerkat Seqeuncer Demo](/documentation/en-us/unreal-engine/meerkat-sample-project-for-unreal-engine) contains a Sound Attenuation asset for you to reference and use. Additionally you can reference the [Sound Attenuation](/documentation/en-us/unreal-engine/sound-attenuation-in-unreal-engine) page to learn more about it.

The Audio Track's Attach track can also be [keyframed](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine), so the audio source attachment can be changed at any point during playback. When you attach an Audio Track to multiple sources, selecting the **Attach** track will display a sound icon on all the attached sources. The sound icon will be highlighted **green** during playback or scrubbing when the audio is attached to that source.

![use keyframes to attach audio assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff0c2346-7bd9-427f-8308-ee5440e2d9a6/audioattachkeyframe.gif)

You can also create a dedicated Audio Track under any Actor added to Sequencer by clicking the Actor's **Track (+)** dropdown and selecting an audio asset from the **Audio** menu. This automatically attaches the sound source to that Actor.

![dedicated audio track for actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f8244406-4c31-4031-8309-2a11ca38ead4/dedicatedaudiotrack.png)

When creating a dedicated Audio Track for an Actor is Sequencer, the Audio Tracks attachment cannot be changed to any other Actor, which is denoted by the lack of an **Attach** track.

![no attach track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8346eb18-6b7b-4671-883d-0f844df58220/noattach.png)

### Attaching Sounds to Bones

If you are attaching an Audio Track to an Actor with a **Skeletal Mesh Component**, you can attach sounds to specific bones for more control over the audio source. After selecting the Skeletal Mesh Actor in the Audio Track's Attach Property, you can then specif the Skeletal Mesh Component and a specific Bone from the character's skeleton.

![select a bone to attach audio tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/776e9218-5845-407c-9865-0d1c270bd545/selectbone.png)

## Audio Track Properties

Once a sound asset is added to the Audio Track, it can be expanded to reveal the following keyframable tracks.

![audio track settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c735cbba-4bcb-4219-b472-ba8881b05ed1/keytracks.png)

| Name | Description |
| --- | --- |
| **Attach** | Set an actor within the Level Sequence to [attach the sound to](/documentation/en-us/unreal-engine/cinematic-audio-track-in-unreal-engine#attachingsounds) for the purposes of spatial audio. |
| **Pitch** | Set the Pitch value for the audio clip. Higher values increase the pitch, and lower values decrease the pitch. A value of `1` is the default pitch. |
| **Volume** | Set the Volume of the audio clip. Higher values increase the volume, and lower values decrease the volume. A value of `1` is the default volume. |

### Audio Section Properties

Right-clicking an audio section and navigating to the **Properties** menu will reveal the following properties.

![audio section properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf362bf6-8f2d-4bd4-8e5f-2807a97a51bd/audiosectionsettings.png)

| Name | Description |
| --- | --- |
| **Sound** | Set the [Sound Wave](/documentation/en-us/unreal-engine/sound-waves) or [Sound Cue](/documentation/en-us/unreal-engine/sound-cues-in-unreal-engine) asset for the Audio section. |
| **Start Frame Offset** | 
Set the number of frames to offset the start time of this audio section by. This value provides a similar effect to [Slip Editing](https://support.apple.com/en-ca/guide/final-cut-pro/ver1632d8e4/mac), as it is used to adjust the playable region of a sound without affecting the duration.

Holding the **Shift** key and dragging on the clip provides a shortcut to changing this property using your mouse.



 |
| **Looping** | Toggle if the audio section is able to loop or not. |
| **Suppress Subtitles** | When enabled, the display of subtitles will be suppressed, if subtitles are being used on the asset. |
| **Override Attenuation** | When enabled, the Sound Wave attenuation asset will be overridden with the attenuation specified in **Attenuation Settings**. |
| **Attenuation Settings** | Set a [Sound Attenuation](/documentation/en-us/unreal-engine/sound-attenuation-in-unreal-engine) asset to drive the 3D audio behavior for the audio section. |