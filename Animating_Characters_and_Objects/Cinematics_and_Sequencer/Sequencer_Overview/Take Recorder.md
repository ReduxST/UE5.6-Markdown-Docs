# Take Recorder

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:29

---

**Take Recorder** records gameplay animation, live performances, and other sources into Unreal Engine directly. By recording and managing takes into Sequencer, you can achieve a highly iterative workflow in your virtual production.

## Common Uses

Some of the main use cases and features of **Take Recorder** are:

-   **Animation Recording**: Record animations and motions of characters or objects in the game world. This provides you with a way to create custom animations by manipulating the characters directly in the level.
-   **Camera Recording**: Capture camera movements, angles, and focal lengths. This is useful for creating dynamic camera shots for in-game and non-game cinematics.
-   **Sequencer** Integration: Seamlessly integrates with Unreal Engine's **[Sequencer](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview)**, which is the timeline-based cinematic editing tool. This integration can use recorded takes directly in Sequencer for further editing and compositing.
-   **Multiple Takes**: Create multiple takes for the same scene or action. This gives you the flexibility to experiment with different variations or performances without having to re-record everything from scratch.
-   **Non-Destructive Workflow**: Non-destructive workflow ensures that your original animations and gameplay data remain untouched, which gives you the capability to make changes and adjustments without losing previous recordings.
-   **Metadata Support**: Store metadata alongside recorded takes. This metadata can include character names, shot descriptions, and other relevant information, which helps organize and manage your recordings.
-   **Performance Capture Support**: For advanced setups, Take Recorder supports performance capture solutions like Motion Capture (MoCap) systems, which record high-quality character animations with external hardware.
-   **Real-time Recording**: Depending on your hardware and setup, Take Recorder can operate in real-time, enabling immediate feedback on the recorded performance during gameplay.

## Prerequisites

-   **Take Recorder** is a [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) that must be enabled prior to use. From the main menu, go to **Edit > Plugins**, locate **Take Recorder**, and click the checkbox to enable it. This requires Unreal Engine to restart in order for the plugin to be enabled. This plugin is required for Take Recorder to work.
-   To record animation from motion capture and other live performances, you can optionally enable **[Live Link](/documentation/en-us/unreal-engine/live-link-in-unreal-engine)**. From the main menu, go to **Edit > Plugins**, locate **Live Link**, and click the checkbox to enable it. This requires Unreal Engine to restart in order for the plugin to be enabled.
-   You also need a project with a playable character and actors to record. Alternatively, use a project created using the [Third Person Template](/documentation/en-us/unreal-engine/third-person-template-in-unreal-engine) template.

## Opening Take Recorder

To start using **Take Recorder**, click **Window > Cinematics > Take Recorder** to open the Take Recorder panel. Take Recorder opens a new empty sequence if one is not open already. The new sequence's time display is set to a timecode matching Take Recorder's time display.

## Interface Overview

There are four main sections of the **Take Recorder** user interface:

![Take Recorder UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f20dcb47-0048-48a4-8c2a-3021452491e2/take_recorder_ui.png)

1.  **[Toolbar](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#toolbar)**: The **Take Recorder** toolbar contains several buttons and toggles which control Sequencer integration, takes browsing, option displays, and **[user/project settings](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#user/projectsettings)**.
2.  **[Slate](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#slate)**: The Slate section shows information on the pending take and timecode. Specify the take name, take number, set a marker frame, adjust frames per second (fps), add a description about the take, and set recording speed. The **Start Recording** button is located here and initiates the recording of the take.
3.  **[Sources](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#sources)**: The Sources section contains options to specify the sources to record into your sequence. Sources can be captured from any actor in the Level as well as Live Link sessions, other sequences, a microphone, or World states.
4.  **[Details](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#details)**: The Details section contains user and project settings for **Take Recorder**, as well as settings for your sources.

### Toolbar

The **Take Recorder** toolbar contains buttons and toggles for controlling Sequencer integration, takes browsing, and option displays.

| Name | Icon | Description |
| --- | --- | --- |
| **Clear Pending Take** | ![Clear Pending Take](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc719ea8-8cb5-44fe-a5bd-05967fd8315d/clear_pending_take_icon.png) | Revert the currently opened sequence to an empty pending sequence. Removes any sequences specified in the **Record to Sequence** button. |
| **Review Last Recording** | ![Review Last Recording](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/657cc839-a70c-487c-beb0-76d8ac22cf45/review_last_recording_icon.png) | Open the most recent sequence that was recorded. Does not become clickable until after a recording has been created. |
| **Record to Sequence** | ![Record to Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a9dec89-e009-444d-9478-b8d37808713d/record_to_sequence_icon.png) | 
Open a dropdown menu from which you can specify another sequence to record your take into. Clear it by clicking the Clear Pending Take button.

![Record to sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7cf7a056-7257-49b7-aa51-2052985efcb2/record_to_sequence.png)

 |
| **Takes Browser** | ![Takes Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf0c1535-06d5-40de-a992-a25c85ca1d05/take_browser_icon.png) | 

Open a Content Browser window for navigating to your saved takes. When using the columns view mode, take-related metadata information is displayed.

![Take Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/343e82fc-97ec-468b-a328-d3773b6c3685/take_browser.png)

 |
| **Show / Hide Sequence** | ![Show / Hide Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3b9ec814-d53e-4cce-a40e-f0f124844abd/show-hide_sequence_icon.png) | Show or hide the Level Sequence that is used for setting up this take. |
| **Settings** | ![Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13e73fa3-8cfb-4d65-8d88-91ac3f75e2f3/settings_icon.png) | Show or hide project and user settings in the Take Recorder's details area. |
| **Return** | ![Return](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52b09228-6aa0-4922-aa7e-b3d0fa42d7ba/return_icon.png) | Return to the pending take sequence, when reviewing a previous take. This feature is accessible while reviewing a previous recording. |
| **Slate Info Lock** | ![Slate Info Lock](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bafa91b9-fd65-4c0b-86b5-92b9bb8c773c/state_info_lock_icon.png) | Lock or unlock the ability to modify a slate, when reviewing a previous take.This feature is accessible while reviewing a previous recording. |
| **Start New Recording** | ![Start New Recording](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e2ce8fcd-3c9c-480b-8c11-d0a005eb1fcd/start_new_recording_icon.png) | Start a new recording using the current selected take as a base. This feature is accessible while reviewing the last recording. |

### Slate

The **Slate** area displays information on the current pending take, the current time, and recording functions. Set custom names and numerical entries for your slate and take number by clicking the **Slate** or **Take** text fields and modifying the text. The same can be done by clicking the **\\** field in the slate body.

**Take Recorder** isn't running when the panel is initially loaded. The current timecode shows the current time from the running timecode provider, which defaults to UE's timecode provider. See **Recording Clock Source** in the [Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#takerecorder) section for timecode options.

To start a new recording, click the red **Record button** in either the Take Recorder window or in Sequencer playback controls. Sequencer's record button starts recording any selected actor into the current sequence, and does not require the Take Recorder window to be open. Click the button again or press the Esc key to stop the recording and save the current take.

![Take Recorder buttons](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d49ab518-bb91-452e-8da1-b0be64b68630/record_buttons.png)

1.  **Take Recorder** window record button.
2.  **Sequencer** record button.

During a recording session, click the **Add Marked Frame** button to add custom markers to the current time of the recording.

![Customer markers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/92d8e25b-f9fc-4a5f-b9be-820cc09557b0/custom_markers.png)

Click the **Frames Per Second** (fps) menu for a dropdown list of different frame rates to select for your pending take.

![Frames Per Second (fps)](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da22fd14-d7b8-421a-b663-f55d9e69a2b6/fps.png)

Change the recording speed and overall time dilation of the engine by editing the **Record Speed** number. This is useful when recording to a populated sequence by making the animation play at a slower speed, ensuring you can observe and match the animation at a more comfortable pace.

![Record Speed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/65729b9b-5b3f-448f-906e-2df5071b8e90/record_speed.png)

#### Warnings

**Take Recorder** provides warning information if you don't have a valid source to record from or if you try to name a take the same as a previously recorded take.

If you do not have a valid source to record from, the Record button is replaced with an invalid source icon. Ensure you have selected a recordable source before attempting any recordings.

![Invalid source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6749bbe6-be57-41c1-bf87-f8adc4a22c50/invalid_source_icon.png)

If you try to use the same take number from a previous take, the **Take Recorder** warns you that a take with the same number already exists and tells you where the previous take is. If you click that warning, it automatically changes the take number to the next available take number.

### Sources

The **Source** section is where you specify recording sources. Sources are listed here and can be enabled or disabled from the recording. When a source is enabled, the toggle icon is orange. When it is disabled, the toggle icon is gray.

![Enabled and disabled sources](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73e38df2-5c6a-4146-bd34-8ff5062c12b4/sources.png)

1.  Enabled source
2.  Disabled source

Each source also has a color bar at the far right end in the **Source** panel. The color of each source corresponds to the recorded subsequence.

**Take Recorder** only records a source **if** the source has both: The source has a recorder **and** a corresponding track that Sequencer can play back.

For example, any track that can be keyframed can be recorded. If a property of an actor cannot be keyframed, it cannot be recorded.

To add a source, click **+Source** and choose from a list of available sources. You can choose from:

-   **[Any Actor](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#anyactor)** in the level
-   **[Camera Cuts](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#cameracuts)**
-   **[Level Sequences](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#levelsequences)**
-   **[Live Link](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#livelink)**
-   One or more **[microphones](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#microphones)**
-   **[Nearby Spawned Actors](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#nearbyspawnedactors)**
-   A **[Player](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#player)** actor
-   **[World](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#world)** / **[Level assets](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#levelvisibility)**

![Add Source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2b5ad77-78d0-4825-a455-3921eaadcd04/add_source.png)

Add a source to **Take Recorder** by dragging an actor from the **[Outliner](/documentation/en-us/unreal-engine/outliner-in-unreal-engine)** into the **Source panel**.

| Source | Description |
| --- | --- |
| **Any Actor** | 
The **Take Recorder Source** records an actor from the World's properties. Records the properties of the actor and the components on the actor and safely handles new components being spawned and the actor being destroyed. Selecting **Any Actor** as a source creates an actor source with the following details.

-   **Source Actor**: The actor being referenced in the world. Record Type: Specify to record the actor as a **[Spawnable or Possessable](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)**.
    -   **Project Default**: Sets the record type to either possessable or spawnable depending on your project's default settings (default setting). See the value (true or false) in the Record to Possessable field in [Take Recorder settings](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#userandprojectsettings).
    -   **Possessable**: Overrides the Take Recorder settings and records the take assets as a possessable.
    -   **Spawnable**: Overrides the Take Recorder settings and records the take assets as a spawnable.
-   **Record Parent Hierarchy**: Whether or not to also include the parent hierarchy if this actor is attached to a parent.
    -   If this is **disabled** and you are recording to a **posessable actor**, then the resulting transforms are in local space, since this actor is still attached to the parent.
    -   If this is **disabled** and you are recording to a **spawnable actor**, then the resulting transforms are in global space since the actor is a spawned copy and not attached to anything.
-   **Reduce Keys**: When enabled, this executes a [Simplify](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#simplify) operation on all keyframes after recording finishes.
-   **Recorded Properties**: A list of default properties for this actor and Components that can be enabled or disabled. Disabling a property does not include it as a track when recording finishes.
-   **Include Animation Names**: An array where you specify Bone or [Curve](/documentation/en-us/unreal-engine/animation-curves-in-unreal-engine) names to include in the recording. If you fill this array with any entries, only those Bones or Curves are included. For example, if you specify "root", then only the root bone is recorded.
-   **Exclude Animation Names**: An array where you specify Bone or Curve names to exclude from recording.

![Source for Any Actor panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e4b9a929-2ce4-4d5c-b891-b126f781abae/source_any_actor.png)

 |
| **Camera Cuts** | If **Camera Cuts** is added as a source, **Take Recorder** records all active cameras during the session. Any time the active camera is changed, a new camera actor and camera cut section is created. |
| **Level Sequence** | 

Selecting a **Level Sequence** as a source provides other sequences to be played during your recording session. Specify any number of sequences to play from the details area of this source. Playback of sequences only is supported during recording within gameplay or simulation sessions.

-   **Level Sequences to Trigger**: Option to select one or more Level Sequences.

![Source for Level Sequence](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/711c6211-df20-4868-8a99-c262d8a5fa4d/source_level_sequence.png)

 |
| **Level Visibility** | The **Level Visibility** source records the visibility states of all Levels at the start of the recording. It does not record any level change, only the visible states. It does not record any changes during the recording session. |
| **Live Link** | 

**Live Link** connects to any currently active Live Link sessions. The Live Link session must be specified in the **Subject Name** details field. Select a live link session directly by navigating to **Add Source (+) > From Live Link**.

-   **Reduce Keys**: when enabled, this executes a [Simplify](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine#simplify) operation on all keyframes after recording finishes.
-   **Subject Name**: Name of subject to record.
-   **Save Subject Settings**: Toggle to Save subject settings while using Live Link. If you want to retain preprocessor, translations, and interpolations settings with your Live Link actor, enable this option.
-   **Use Source Timecode**: Toggle to use the subject's timecode or the system time while recording.
    -   If this option is enabled, the Live Link subject's timecode is used even if it doesn't match UE's timecode.
    -   If this option is disabled, data is keyed on the LiveLink thread and not the game thread. A key is stamped for every sample that arrives using the engine's time. No timecode track is created, so the relationship between the source's timecode and the recorded level sequence is lost.
-   **Discard Samples Before Start**: If enabled, UE discards Live Link samples with a timecode that occurs before recordings if **[Start at Current Timecode](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#startatcurrenttimecode)** is enabled.

![Source for Live Link](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1bb9134c-2a68-4ba3-9421-62842bf38132/source_live_link.png)

 |
| **Microphone Audio** | 

**Microphone Audio** permits your device's microphone to be recorded during the recording session. Upon completion, **Take Recorder** creates a sound file is created upon completion containing your recorded audio. The details area contains settings for audio recording, track name, and the recording directory.

-   **Audio Gain**: Gain in decibels to apply to recorded audio.
-   **Replace Recorded Audio**: Replace existing recorded audio with any newly recorded audio. Enabled by default.
-   **Audio Input Device**: Current selected channel from the Details panel for this source.
-   **Audio Source Name**: Name of the audio source
-   **Audio Track Name**: Name of the recorded audio track
-   **Audio Asset Name**: Name of the audio asset. Supports any of the following format specifiers that are substituted when at recording time:
    -   **{day}**: Day of the timestamp for the start of the recording.
    -   **{month}**: Month of the timestamp for the start of the recording.
    -   **{year}**: Year of the timestamp for the start of the recording.
    -   **{hour}**: Hour of the timestamp for the start of the recording.
    -   **{minute}**: Minute of the timestamp for the start of the recording.
    -   **{second}**: Second of the timestamp for the start of the recording.
    -   **{take}**: Take number.
    -   **{slate}**: Slate string.
-   **Audio Sub Directory**: Name of the subdirectory audio is saved in. Leave this field empty to place in the same directory as the sequence base path. Supports any of the following format specifiers that are substituted at recording time:
    -   **{day}**: Day of the timestamp for the start of the recording.
    -   **{month}**: Month of the timestamp for the start of the recording.
    -   **{year}**: Year of the timestamp for the start of the recording.
    -   **{hour}**: Hour of the timestamp for the start of the recording.
    -   **{minute}**: Minute of the timestamp for the start of the recording.
    -   **{second}**: Second of the timestamp for the start of the recording.
    -   **{take}**: Take number.
    -   **{slate}**: Slate string.

![Source for microphone audio](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f19dc11-9402-4eed-b2c0-393cfa223fa1/source_microphone_audio.png)

 |
| **Nearby Spawned actors** | 

The **Nearby Spawned Actors** source records all spawned actors located within a specified radius from the camera's location. The details panel includes options for defining the range and specifying filters. If you are using filters, then only the filtered actors are added to the take. Only actors that spawn during a gameplay session are added. Actors that have already spawned are not affected.

-   **Spawn Proximity**: Proximity to the current camera that an actor must be spawned in order to be recorded as a spawnable. If Proximity is set to 0cm, all spawned actors are recorded.
-   **Filtered Spawned Actors**: Only recorded actors that are listed in the Filter Type list. Defaults to disabled.
-   **Filter Types**: Type filter to apply to spawned actors.

![Source for nearby spawned actors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b05e61f6-91da-4876-98ef-a709ce5988f5/source_nearby_spawned_actors.png)

 |
| **Player** | The **Player** source records the Player's controlled actor. Using this source might be useful if your player is dynamically spawned and does not exist as an actor in the Level until gameplay starts. |
| **World** | If **World** is added as a source, everything in the Level is recorded (defaults to true). Particles that are created using **Spawn Emitter** functions are only captured when using this source. |

You can save your source list as a preset and reuse it later. To save your source list:

1.  Click the **Presets button** next in the Source panel.
2.  Select **Save As Preset**.
3.  The **Save Take Preset** window appears and prompts you for the **Path** location (folder where this preset is saved) and the **Name** of the preset.
4.  Click the **Save button** to save your preset.

![Save Source presets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e344de3-8f13-4361-bb01-e32eba469ef4/source_presets.png)

The **Presets** menu lists any saved presets.

Remove all sources from the list or revert to your preset's selection by clicking the **Revert** button. A warning message appears confirming if you are sure you want to revert changes. Click Yes if you want to discard your changes.

![Remove all sources](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b118d8c0-dfd0-457d-a7d0-dae16330abc6/remove_all_sources.png)

### Details

The details area of **Take Recorder** contains project properties and settings for your sources as well as the Take Recorder. Enable it by clicking the **Settings** button in the toolbar. When you specify default settings for sources here, they propagate to the source. Individual sources can still be customized from the project.

![Take Recorder's Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b5120bf-9df0-4940-9ae7-890901a79f9d/details_panel.png)

Example of Audio Sub Directory for the Microphone Audio Recorder properties overriding the Audio Sub Directory of the Microphone Audio Source in the Take Recorder Details panel.

#### User and Project Settings

The following **user/project settings** is found by enabling the Show/Hide general user/project settings button (gear icon in upper right corner).

##### Take Recorder

| Name | Description |
| --- | --- |
| **Root Take Save Dir** | Root directory in which to save recorded takes. Click the ellipsis icon (three dots) to select a different folder. |
| **Take Save Dir** | 
A sub-directory relative to the root that further organizes saved takes. Supports any of the following format tokens that are substituted when a take is recorded:

-   **{day}**: Day of the timestamp for the start of the recording.
-   **{month}**: Month of the timestamp for the start of the recording.
-   **{year}**: Year of the timestamp for the start of the recording.
-   **{hour}**: Hour of the timestamp for the start of the recording.
-   **{minute}**: Minute of the timestamp for the start of the recording.
-   **{second}**: Second of the timestamp for the start of the recording.
-   **{take}**: Take number.
-   **{slate}**: Slate name.



 |
| **Default Slate** | Project's default name for slates. |
| **Recording Clock Source** | 

Clock source to use when recording. Select from the following options:

-   **Tick**: Uses the default world tick delta for timing. This mode responds to world and actor pause states, but can be susceptible to accumulation errors.
-   **Platform**: Uses the platform's clock for timing. This mode does not respond to world and actor pause states.
-   **Audio**: Uses the audio clock for timing. This mode does not respond to world and actor pause states.
-   **Relative Timecode**: Uses the time relative to the timecode provider for timing. This mode does not respond to world and actor pause states.
-   **Timecode**: Uses the current timecode provider for timing. This mode does not respond to world and actor pause states.
-   **Play Every Frame**: A debugging mode where each frame is held for **Sequencer.SecondsPerFrame** for many wall-clock seconds before advancing to the next frame. This mode does not respond to world and actor pause states and time dilation. Audio is not synchronized.
-   **Custom**: Custom clock source created and defined externally.



 |
| **Start at Current Timecode** | If enabled, recording begins at the current date's timecode depicted in your slate. Otherwise, the recording begins at time 0. |
| **Record Timecode** | If enabled, this writes timecode metadata into every track section for every actor. This information is viewed by right-clicking a track section and navigating to **Properties > Section > Section Range Start/End**. |
| **Record Sources Into Sub Sequences** | If enabled, each source is recorded into a separate sequence and embedded in the Root Sequence that is linked to them via Subscenes track. If disabled, all sources are recorded into the Root Sequence and you cannot swap between various takes of a specific source using the Sequence Take UI. You can still do this by copying and pasting between sequences. |
| **Record to Possessable** | If enabled, records all actors to possessable type tracks instead of spawnables. This is overwritten per actor source. |
| **Default Tracks** | Specify actor classes and their components so that those components always be captured during a recording session. |
| **Show Notifications** | 

Shows or hides Take Recorder notifications before and during recording.

![Recording notification before recording starts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba4eee42-2456-47e7-b56f-87196283117d/show_notifications.png)

 |

##### Movie Scene Take Settings

Specify your project's names for Hours, Minutes, Seconds, Frames, Sub Frames, and Slates. This affects the names of tracks created in the **Takes Track** for your actors.

| Name | Description |
| --- | --- |
| **Hours Name** | Defaults to TCHour. |
| **Minutes Name** | Defaults to TCminute. |
| **Seconds Name** | Defaults to TCSecond. |
| **Frames Name** | Defaults to TCFrame. |
| **Sub Frames Name** | Defaults to TCSubframe. |
| **State Name** | Defaults to TCSlate. |

##### Microphone Audio Recorder

| Name | Description |
| --- | --- |
| **Audio Source Name** | Name of the audio source. Used to set the name of the source. Accepts **{channel}** token which will be replaced with the assigned channel number from the **Audio Input Device** channel menu. Note that in order to ensure this name is unique, UE may append the channel number if no {channel} token is present. |
| **Audio Track Name** | Name of the recorded audio track. |
| **Audio Asset Name** | 
Name of the audio asset. Supports any of the following format specifiers that are substituted when at recording time:

-   **{day}**: Day of the timestamp for the start of the recording.
-   **{month}**: Month of the timestamp for the start of the recording.
-   **{year}**: Year of the timestamp for the start of the recording.
-   **{hour}**: Hour of the timestamp for the start of the recording.
-   **{minute}**: Minute of the timestamp for the start of the recording.
-   **{second}**: Second of the timestamp for the start of the recording.
-   **{take}**: Take number.
-   **{slate}**: Slate string.



 |
| **Audio Sub Directory** | 

Name of the subdirectory audio is saved in. Leave this field empty to place in the same directory as the sequence base path. Supports any of the following format specifiers that are substituted at recording time:

-   **{day}**: Day of the timestamp for the start of the recording.
-   **{month}**: Month of the timestamp for the start of the recording.
-   **{year}**: Year of the timestamp for the start of the recording.
-   **{hour}**: Hour of the timestamp for the start of the recording.
-   **{minute}**: Minute of the timestamp for the start of the recording.
-   **{second}**: Second of the timestamp for the start of the recording.
-   **{take}**: Take number.
-   **{slate}**: Slate string.



 |

##### Audio Input Device

| Name | Description |
| --- | --- |
| **Use System Default Audio Device** | Option to use system selected audio devices. When enabled, Take Recorder falls back to the audio device selected in the host operating system. |
| **Audio Input Device** | If the **Use System Default Audio Device** toggle is disabled, select any available audio device on the host computer. Used to set the physical channel of the audio device to use when recording audio for this source. |
| **Audio Input Buffer Size** | The size of the buffer, in samples, that will be used to buffer audio as it is captured. Larger buffers prevent data over-runs but consume more memory. |

##### Animation Recorder

| Name | Description |
| --- | --- |
| **Animation Track Name** | The name of the recorded animation track. |
| **Animation Asset Name** | The name of the saved Animation Sequence. |
| **Animation Sub Directory** | The name of the subdirectory that Animation Sequences are saved to. If this is empty, then sequences are saved in the Root Take Save Dir. |
| **Remove Root Animation** | If enabled, Skeletal Meshes move based on a Transform track. If disabled, motion occurs on the root bone in the Animation Sequence. |
| **Timecode Bone Method** | 
Controls for recording [Timecode on Skeletal Meshes](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#recordtimecode).

-   **All**: Records Timecode metadata on every bone in the Skeleton as an [Animation Attribute](/documentation/en-us/unreal-engine/fbx-attributes-in-unreal-engine).
-   **Root**: Records Timecode metadata on the top-most bone in the Skeleton hierarchy. In most cases, this is the "root" bone.
-   **User Defined**: Records Timecode metadata on the bone specified in the Bone Name property.



 |

##### World Recorder

| Name | Description |
| --- | --- |
| **Record World Settings** | Whether to record the World Settings actor in the sequence. Some projects use this to attach world sound effects. |
| **Autotrack Actors** | Adds bindings and tracks for all actors that are not explicitly recorded. |

##### User Settings

| Name | Description |
| --- | --- |
| **Maximize Viewport** | Enables [Immersive Mode](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine#immersivemode) during a recording. |
| **Countdown** | After pressing the Record button, Take Recorder counts down the amount of time in seconds listed here before it starts the recording session. |
| **Engine Time Dilation** | Amount of time dilation to apply to the recording session. |
| **Stop at Playback End** | Recording stops upon reaching the end time of the sequence. On new sequences the end time defaults to 5 seconds. |
| **Remove Redundant Tracks** | By default, Take Recorder records all possible tracks from sources. When this option is enabled, only tracks with changes are kept by the recording. |
| **Reduce Keys Tolerance** | Tolerance to use when reducing keyframes created during a recording. Higher numbers cause more keyframes to be removed if they contain values differences within the tolerance. |
| **Save Recorded Assets** | Automatically saves recorded sequences and subscenes upon completing a recording. These assets are lost if they are not saved. |
| **Auto Lock** | Locks the take to prevent editing after the recording session ends. The take is unlocked by toggling the lock button in the **[Sequencer Toolbar](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine)**. |
| **Auto Serialize** | 
Stores capture data as it's recorded, as opposed to all at once at the end of the recording.

This is an experimental feature and should be used at your own risk, as it has not been tested fully.



 |
| **Preset Save Location** | Directory in which to save source preset files to. |

### Record Timecode

**Take Recorder** can record Timecode metadata. It provides controls for recording Timecode relative to the Scene, individual actors, and Skeletal Mesh bones.This is useful for changing performances relative to other performances within the same take, while maintaining other Timecode values.

For cameras and non-Skeletal Mesh actors, recorded Timecode information is displayed under a **Take Track** in the Subsequence.

![Example of timecode metadata](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ff5b650-b9e9-4c5a-a6e6-b44f2f9d874e/timecode_example.png)

After recording, view Skeletal Mesh Timecode data within the [Animation Sequence](/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine) timeline under the **Attributes** track.

### Reviewing Subscenes and Assets

Double-click the **subscene** section to open an actor's sequence and view the recorded keyframes, such as transform and animation.

![Open SubScene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5bc7c14-d8b9-469a-b4a6-998b78aeca9a/open_subscene.png)

## Editing Takes

There are two ways to unlock a take before or after a recording in order to edit the recorded data: disable **Auto Lock** or unlock the sequence.

If you know you want to edit a take after recording it, disable Auto Lock before recording.

1.  In **Take Recorder**, Show the **[user/project settings](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#userandprojectsettings)** (gear icon).
2.  In the User Settings, disable **Auto Lock**.
3.  Complete a take recording.
4.  Review the take in **Sequencer** and note that none of the recorded sources are grayed out and edit as necessary.

If you need to edit a take after recording it, unlock it by clicking the **Lock button** in **Sequencer**.

![Unlock the sequence to edit recorded data](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cef18a24-91dc-4b34-ab37-2fc66b4ade8d/lock_animation_button.png)