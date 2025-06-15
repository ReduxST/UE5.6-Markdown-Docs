# Sequencer Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine)  
**Processed:** 2025-06-14 16:48:21

---

The **Sequencer Editor** is the main interface you can use to edit [Level Sequences assets](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview), in order to create cinematic content in **Unreal Engine**.

The following document provides an overview of the Sequencer Editor's user Interface, tools, and properties.

![sequencer editor overview with highlights](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0385f35-7654-4a22-8cf2-29c52af494d8/reference.png)

1.  [Toolbar](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#toolbar)
    
2.  [Outliner](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#outliner)
    
3.  [Timeline](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#timeline)
    
4.  [Playback Controls](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playbackcontrols)
    

## Toolbar

The Sequencer Editor Toolbar contains a suite of tools, options and settings you can use to interface with Level Sequence assets.

![sequencer toolbar overview with highlights](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6548a68-c39e-4813-a86d-bcc3435b2ba9/toolbar.png)

| Name | Icon | Description |
| --- | --- | --- |
| [**World**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#world) | ![sequencer world](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6da800c5-ac0b-4221-be99-46b54b97c101/world.png) | Lists information on the current world context, Level Sequence Actor, and playback realm. It contains options for specifying whether you want your sequence to autobind to Play In Editor (PIE), Simulation, or other runtime sessions. |
| **Save** | ![sequencer save](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcdc6efe-7504-4736-94f5-e1f3c18f2461/save.png) | Saves the current sequence and any subscenes or shots. |
| **Find in Content Browser** | ![sequencer find](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/481b63f0-0f85-476f-ba58-de4f915b4492/findcb.png) | Locates the current sequence's Level Sequence asset in the Content Browser. |
| [**Create Camera**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#createcamera) | ![sequencer camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/54b58f96-97ff-4d1a-9736-58c85306c71b/camera.png) | Creates a new **[Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)**. A new **[Camera Cut Track](/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine)** will also be created and will reference this camera if one had not already been created. |
| [**Render**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#render) | ![sequencer render](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7eac4bb0-6a97-425f-91bf-6525f2ba63dc/render.png) | Opens the **[Render Movie](/documentation/en-us/unreal-engine/old-render-movie-in-unreal-engine)** Settings dialog, or the **[Movie Render Queue](/documentation/404)** if its plugin is enabled. |
| [**Director Blueprint**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#directorblueprint) | ![sequencer director](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/035043f2-1c81-4702-87c1-ecf7eb0f24e6/directorbp.png) | Opens the Director Blueprint for this sequence, from which **[Event Track](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine)** logic can be accessed. |
| [**Actions**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#actions) | ![sequencer actions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dd93a97-b1a9-4387-a0fb-5cd340855b79/actions.png) | Lists various sequence editor actions such as saving, import/export, baking, and selection editing. |
| [**View Options**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#viewoptions) | ![sequencer view options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0c54027-46a3-40f3-95a6-d37c6e02ae20/view.png) | Lists various sequence view options. |
| [**Playback Options**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#playbackoptions) | ![sequencer playback options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ed3e7f8-cdbd-4db3-8e32-a95fcf156bf5/playback.png) | Lists various playback options such as playrate, start/end times, and playhead behavior. |
| [**Keyframe Options**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#keyframeoptions) | ![sequencer keyframe options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b355a3e-0537-4bb6-9a7c-06dea1b42ea1/keying.png) | Lists settings for Auto Key transform keyframing behavior, and what default tangents are created. |
| [**Auto Key**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#autokey) | ![sequencer autokey](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f43a7934-3788-4240-81f9-5b3e690dabd6/autokey.png) | Enables Autokey mode, where keyframes are automatically created whenever a property or transform changes. |
| [**Edit Options**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#editoptions) | ![sequencer edit options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f88d5966-d12f-456e-b68d-b42c47f5f85a/edits.png) | Lists settings for how edits from the Details panel are interpreted by Sequencer when using Auto Key. |
| [**Snapping**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#snapping) | ![sequencer snapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf9bcac0-a58c-4b7d-af09-3980701537fc/snapping.png) | Enables snapping. The dropdown menu next to this lists options for setting snapping rules for keyframes, sections, and the timeline. |
| [**Frames Per Second**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#framespersecond) | ![sequencer fps](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b6143003-e8c7-4691-8073-a1aa7a907a9b/playbackoptions.png) | Lists settings for various Frames Per Second (FPS) targets at runtime. Also contains options to enable the runtime to lock to the chosen frame rate. |
| [**Curve Editor**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#curveeditor) | ![sequencer curve editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cb20f62f-b240-4866-b002-a4e877935026/curveeditor.png) | Opens the **[Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine)** which is used for fine tuning of animation keyframes and tangents. |
| [**Breadcrumbs**](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#breadcrumbs) | ![sequencer breadcrumbs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71bc0052-2c09-4e95-b39f-0da845c77cbc/breadcrumbs.png) | Displays the current sequence name, and is used to navigate master sequences and shots. |
| **Lock** | ![sequencer lock](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6800fc89-5a29-488a-9d3a-df3470cfbaf3/lock.png) | Locks the entire sequence to prevent editing. |

Refer to [Sequence Editor toolbar](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine) for more information about Sequencer's toolbar.

## Outliner

The Sequencer Editor's Outliner contains a list of the Level Sequence asset's tracks, as well as tools to add, filter, and search for tracks. Tracks can represent Actors attached to your Level Sequence such as Cameras, Characters, Audio, and Effects.

![sequencer outliner overview with highlights](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4b7c398-296a-4b1b-b8ea-f260ff89b0fd/outlinerarea.png)

Refer to [Sequencer Tracks](/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine) for more information about different types of tracks.

## Timeline

The Sequencer's Timeline is a non-linear editing environment that represents the entire playable region of your Level Sequence asset. The Timeline includes horizontal regions for each Track, and can include assets, keyframes and timeline controls.

The playback range of your Level Sequence asset is contained within **Start** (Green) and **End** (Red) markers. The current location of your playback is indicated by the [Playhead](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#playhead).

![sequencer overview with highlights](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97a9b9f5-af32-4f8d-b88d-8e1dff6b079b/timelinearea.png)

### Navigation

To navigate your Level Sequence asset in the Sequencer Editor, you can [pan](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#panning) and [zoom](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine#zooming) within the timeline.

#### Panning

You can pan your Timeline view vertically, to see additional track regions, by dragging the right-side scrollbar up and down.

![sequencer vertical pan scroll bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1cc31cd5-33c2-4c82-b18a-5373dfc5d214/pan1.png)

You can pan and zoom the Timeline view horizontally, to see different content in the playback, using the **Range Slider** at the bottom of the timeline.

Dragging the middle area of the slider pans, while dragging the left/right margins will zoom your view.

![sequencer horizontal pan bar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7422a168-544d-4ccc-9fe2-bc98f03f52c9/pan2.gif)

The Range Slider is enabled by default and can be disabled from the **View Options** dropdown in the Sequencer toolbar.

Image

Holding the right mouse button and dragging along the timeline enables panning horizontally and vertically.

![sequencer freeform pan right click](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d040cfe-efcc-4500-b963-6eb72c698d6b/pan3.gif)

Scrolling will pan the timeline up and down, while holding **Shift** and scrolling the mouse wheel will pan the timeline left and right.

![sequencer horizontal and vertical shift pan scroll wheel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c51fb79d-7793-4a93-83d8-1c65e9c661ff/pan4.gif)

#### Zooming

You can zoom in the timeline by holding **CTRL** and scrolling the mouse wheel.

![horizontal scrolling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef7af46a-dc8b-4434-8bcb-072701cf3de6/zoom1.gif)

By holding **ALT** + **Shift** and clicking and dragging left and right with the Right Mouse Button, you can free-form zoom.

![horizontal scrolling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/080a0263-7314-414c-86c2-ff93b05ad61f/zoom2.gif)

By holding **CTRL** and dragging along the time bar to the **right**, you can define a zoom region. Holding **CTRL** and dragging the time bar to the **left** resets the zoom back to full.

![horizontal scrolling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e81f163-f7ba-4d1c-b152-bd60023870dd/zoom3.gif)

The zoom pivot is relative to the playhead by default and can be changed by locating the **Zoom Position** preference in the **Level Sequence Editor** section of the **Editor Preferences**.

If your zoom and timeline framing have overextended, you can reset your zoom and timeline framing by pressing the **Home** key, which also resets the bounds of the range slider.

![home button horizontal zoom scrolling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6c96e9b3-fa87-4c08-a008-bf5b319a8621/zoom4.gif)

### Playhead

The playhead displays the current time in the sequence and is one of the main controls for timeline interactions. During playback it will move across the timeline at the specified playrate and can be stopped in place by pausing.

![sequencer playhead](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cab99f89-0af8-4fa4-b036-4702498b3e7a/playhead.png)

You can **Left Mouse Button** (**LMB**) drag the playhead to change the current time in the sequence, and preview changes in the viewport. This is commonly referred to as "scrubbing".

![sequencer scrubbing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d513885a-ea3a-4717-90b2-9fce04763f39/scrubbing.gif)

**Middle Mouse Button** (**MMB**) dragging causes the playhead to change to the selected position without causing the sequence to evaluate. This technique is used to change time, without changing property values and can be used to create same-value keyframes quickly. When manipulating the playhead in this way, it will change its color to **yellow**, to indicate the sequence is not evaluating.

![sequencer middle mouse button keyframing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a0c4508-85a1-445f-bc04-aaee6bf80d82/playheadmmb.gif)

The current time of the playhead is displayed and can be manipulated from the sequence outliner. You can press **CTRL + T** to focus selection to this field and type in a new time value.

![sequencer playhead values](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dfc3f3d-02a6-4149-8ad1-e88fb63a266e/playheadvalue.png)

You can also right-click the playhead or anywhere on the time bar to reveal additional options.

![sequencer timeline playhead context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/154f5f25-4795-4725-b16e-3019d7945a61/playheadmenu.png)

| Name | Description | Hotkey |
| --- | --- | --- |
| **Set Start Time** | Set the start time of the sequence to the current position of your cursor. | **\[** |
| **Set End Time** | Set the end time of the sequence to your cursor. | **\]** |
| **Set Selection Start** | Set the start point of a custom timeline selection range to your cursor. | **i** |
| **Set Selection End** | Set the endpoint of a custom timeline selection range to your cursor. | **o** |
| **Clear Selection Range** | Remove the selected range. |   |
| **Add Mark** | Create a custom timeline mark at the current playhead time. | **m** |
| **Delete All Marks** | Remove all custom marks from the sequence. |   |
| **Locked** | When enabled, all marks will be locked, which prevents marks from being edited allowing you to scrub the timeline slider freely. |   |

The Playhead time indicator can display with an **asterisk** (\*) if the current time is on a sub-frame or in-between frame. This can happen if [snapping](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#snapping) is disabled.

![sequencer sub frames asterisk](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c12ea62c-8e03-4117-92fa-1ee738e15507/asterix.png)

### Selection Ranges

Selection ranges are custom regions you can define in a sequence to assist with timeline selection and playback.

To create a selection range, right- click a point in the timeline bar and set a **Start** and **End Selection Range**.

![sequencer selection range start end](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b461382-2762-4095-a554-b998ad99051c/selectionrange1.png)

The selection range handles can be adjusted similarly to the start and end times of the sequence.

![sequencer selection range manipulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/44b9093a-fa48-47f5-83b1-2b6d6ce1ca23/selectionrange2.gif)

You can also set the playback of the sequence to loop within the section range.

![sequencer selection range playback](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d016f256-4df8-4cca-81a2-ae7aca6eef0f/selectionrange3.gif)

Selection ranges can also be used to select keyframes and sections within them by clicking the **Actions** toolbar button and selecting **Select Keys in Selection Range** or **Select Sections in Selection Range**.

![sequencer selection range settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9747df55-701c-4a8c-a6d5-6c5143101f50/selectionrange4.png)

To remove a selection range, right-click the time bar and select **Clear Selection Range**.

### Custom Frame Marks

Custom frame marks are points you can add to call attention to areas or provide annotation for your sequence.

To create a mark, right-click a point in the timeline bar and select **Add Mark**.

![sequencer add mark option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/efee818d-c4d3-4b46-8f53-32931704c1d3/marks1.png)

Frame Marks can be selected and multi-selected in the Sequencer Timeline in order to edit their location.

![sequencer marks manipulation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/68e11b3c-2a9c-444b-b7c3-1ff9196261ef/marks3.gif)

To edit a mark, right-click the mark flag in the Sequencer Timeline to access its context menu. Here you can customize its properties such as **Frame Number, Label,** and **Color**.

![sequencer mark properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22c7b946-194e-4bbb-bdbe-89ad3721734b/marks2.png)

Use these properties to observe and set Custom Frame Mark behavior when creating cinematics in the Sequencer Editor:

| Property | Description |
| --- | --- |
| **Marked Frame** | Sets or reference the **frame number** the mark is located in your Level Sequence. |
| **Label** | Sets a name for the Custom Frame Mark. The value set will be visible in the Sequencer Timeline at the top of the Mark flag. |
| **Comment** | Adds comments associated with the custom mark. |
| **Color** | Sets a custom color for the Mark flag in the Sequencer Timeline. |
| **Is Determinism Fence?** | 
When enabled, the Mark is treated as a **Determinism Fence**, which ensures that all Sequencer Components are evaluated at the Mark's location in the Sequencer Timeline.

Determinism Fences cannot be crossed with a single evaluation, and force the evaluation to be conducted in two separate parts, ensuring an accurate evaluation of all present Sequencer components.

It is recommended to add Marks, with the **Is Determinism Fence** property enabled, to important frames in your Level Sequence, in order to ensure accurate playback at runtime.



 |
| **Add Mark** | 

Creates a new custom mark at the timecode your cursor is at.

Only one custom mark can exist per level sequence frame.



 |
| **Delete Mark** | Deletes the currently selected mark. |
| **Delete All Marks** | Deletes all custom marks within the level sequence asset. |

## Playback Controls

The playback controls can be found in the bottom-left corner of Sequencer and function similarly to standard media playback applications.

Buttons for toggling playing, pausing, and other playback-related functions are found here.

![sequencer add mark option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e788de4-9325-4800-b61a-1ede57750e3e/playbackcontrols.png)

| Icon | Description |
| --- | --- |
| ![sequencer record button take recorder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d44388e7-308a-4a11-b837-c0e32c5f9d8f/recordbutton.png) | 
Records the motion of a selected actor in the Sequencer Outliner, using **Take Recorder**.

In order to use this playback control, you must install the Take Recorder plugin. For more information, see the [Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine) documentation.



 |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2e9e8298-9fea-4304-89d8-4ab30d621f28/playbackbracketin.png) | Sets the start time of the sequence to the current location of the playhead. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cef7a6c2-15f4-480e-85be-7e39d15679d9/playbackgotofront.png) | Jumps to the start of the sequence. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19142988-17d9-4b47-89d4-70a698c97e7a/playbackprevkey.png) | Jumps to the previous keyframe in the selected track. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/876344c6-9a79-4360-8764-b7fb5e9996c6/playbackstepback.png) | Jumps to the previous frame. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f3f92730-6d7b-4d93-a419-5315a7f80694/playbackreverse.png) | Plays or pauses the sequence in reverse from the current position of the playhead. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e94dbb20-c1f5-45a5-aa42-6261bd4d8c2c/playbackplay.png) | Plays or pauses the sequence from the position of the playhead. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a92a45d-3386-4606-b5d5-242d16af5050/playbackstepforward.png) | Jumps to the next frame. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7a57b82-d8a1-4300-acc0-dac09b04e2a3/playbacknextkey.png) | Jumps to the next keyframe in the selected track. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fdc2ac8-e46d-4fef-816e-d8ffc0fbc1ea/playbackgotoend.png) | Jumps to the end of the sequence. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/757f148c-02ec-4759-9d7f-ec4c076ea963/playbackbracketout.png) | Sets the end time of the sequence to the current location of the playhead. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f60cd1a5-a178-4cda-8955-c106ea919108/playbackloop.png) | Toggles between looping and no looping. Selection range looping is added if selection ranges are being used in the timeline. |