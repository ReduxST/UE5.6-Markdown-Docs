# Sequencer Toolbar Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:23

---

This page provides a reference for Sequencer's Toolbar.

![sequencer toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2adaab77-90dc-4d2f-a1fb-63a97683ce88/toolbar.png)

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

## World

Sequencer's World menu contains options relating to the current Level, session, and the level sequence name.

![world menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3cc7b25b-b009-49fd-bfba-9da9db8dfc25/world1.png)

The **Actors** options category lists the running sessions that Sequencer can bind to, and provides you the option to switch your binding between them.

In this example you can see there are now two sessions being run: **Editor** and **Simulate**. You have the option to switch between them which causes Sequencer to bind to that realm instead.

![world menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c88fab45-c6ab-4eb6-a42f-3d2ec00212ce/world2.png)

**Auto Bind to PIE** and **Simulate** enable the automatic binding of Sequencer to their respective realms when they begin to run.

## Create Camera

Clicking the **Create Camera** button will automatically create a **[Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)** and a **[Camera Cut Track](/documentation/en-us/unreal-engine/cinematic-camera-cut-track-in-unreal-engine)** with a binding to the new camera. Your viewport will also begin piloting the camera, which will prepare you to start framing your shot.

![sequencer create camera](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0102a220-d3d3-419f-9525-12774b088ede/createcamera.gif)

You can specify if this camera is spawnable or posessable by toggling **Create Spawnable Camera** in the **[Editor Preferences and Project Settings](/documentation/en-us/unreal-engine/cinematic-editor-and-project-settings-in-unreal-engine)** window.

## Render

Clicking the Render button will open the **[Render Movie](/documentation/en-us/unreal-engine/old-render-movie-in-unreal-engine)** Settings dialog box, from which you can render your sequence as a series of images.

![sequencer render](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/744dbadd-88fc-42a0-b567-7f2f14117f7a/renderbutton1.png)

If you have enabled the **[Movie Render Queue](/documentation/404)** (MRQ) plugin, then the button will have a dropdown menu from which you can choose between launching the new MRQ tool or the legacy rendering tool.

![sequencer mrq button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c2c90c3-954c-41a1-a77b-e8e9e1b17a9e/renderbutton2.png)

## Director Blueprint

Clicking the Director Blueprint button opens the Sequence Director window, from which you can see your sequence's **[Event Track](/documentation/en-us/unreal-engine/cinematic-event-track-in-unreal-engine)** events.

![sequencer director](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3ac204cf-ecb7-4f4b-b6c4-9fdbdd473bcd/directorbutton.png)

## Actions

The Actions button displays a dropdown menu with the following tools, commands, and options:

![sequencer actions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2f46974-ed65-48fc-88f7-3fa60cd9e6cf/actionsbutton.png)

| Name | Description |
| --- | --- |
| **Save As...** | Saves the current sequence and provides the option to select a different name. |
| **Import...** | Imports an FBX animation file to the selected Actor. If no Actor is selected then the importer will attempt to apply the animation to the entire sequence. Visit the **[Importing and Exporting FBX files](/documentation/en-us/unreal-engine/import-and-export-cinematic-fbx-animations-in-unreal-engine)** page for more information. |
| **Export...** | Exports a selected Actor to an FBX file. If no Actor is selected then the entire sequence will be exported. Visit the **[Importing and Exporting FBX files](/documentation/en-us/unreal-engine/import-and-export-cinematic-fbx-animations-in-unreal-engine)** page for more information. |
| **Open Director Blueprint** | Opens the Director Blueprint for this sequence, from which Event Track logic can be accessed. |
| **Open Binding Tag Manager** | Opens a tool from which you can create Tags. These tags are applied to Actors which allows them to be identified in a Blueprint to perform special functions. Visit the **[Sequencer Tags and Groups](/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine)** page for more information. |
| **Open Sequencer Group Manager** | Opens a tool that displays custom groups and the tracks applied to them. Visit the **[Sequencer Tags and Groups](/documentation/en-us/unreal-engine/cinematic-tags-and-groups-in-unreal-engine)** page for more information. |
| **Restore Pre-Animated State** | Snaps all Actors back to their default editor positions. Playing or scrubbing the sequence will snap them back to their Sequencer-determined positions. |
| Transform |   |
| **Transform Selection** | 
Opens a tool you can use to modify keyframes and sections relative to the playhead time. You can move keys in a positive and negative numerical direction, or multiply and divide their relative distance from the playhead.

![sequencer transform selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9de51f2-3353-4b49-bd43-e29deecce8a2/transformselection.png)

 |
| **Stretch/Shrink** | 

Opens a tool used for adding and removing time in your sequence relative to the playhead time.

![sequencer stretch shrink](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb411456-1df1-43b1-ba4a-f72f37a7c9ea/stretchshrink.png)

 |
| **Translate Left** | Moves a selected keyframe 1 frame to the left relative to the sequence's frame rate. |
| **Translate Right** | Moves a selected keyframe 1 frame to the right relative to the sequence's frame rate. |
| **Trim or Extend Section Left** | Trims or extends a selected track's section from its left/start point to the playhead location. If no track is selected, then all sections will be trimmed or extended. |
| **Trim or Extend Section Right** | Trims or extends a selected track's section from its right/ending margin to the playhead location. If no track is selected, then all sections will be trimmed or extended. |
| **Bake Transform** | Selecting this will bake a selected Actor's transform in world space. Any existing attachment or transform tracks will be disabled. This behavior can be changed by locating the **Disable Sections After Baking** preference in the **[Editor Preferences and Project Settings](/documentation/en-us/unreal-engine/cinematic-editor-and-project-settings-in-unreal-engine)** window. If you disable it, any existing tracks overwritten during the bake will be deleted. |
| **Sync Sections using Source Timecode** | Synchronizes sections with the first selected section using its source timecode. |
| Selection Range |   |
| **Set Selection Start** | Sets the start point of a custom timeline selection range to the playhead time. |
| **Set Selection End** | Sets the end point of a custom timeline selection range to the playhead time. |
| **Clear Selection Range** | Removes the selection range. |
| **Select Keys in Selection Range** | Selects all keyframes within the selection range. Does not select sections. |
| **Select Sections in Selection Range** | Selects all sections within the selection range. Does not select keyframes. |
| **Select All in Selection Range** | Selects all keyframes and sections within the selection range. |
| Advanced |   |
| **Fix Actor References** | Attempts to automatically fix broken Actor bindings by matching the object binding name with an Actor in the Level with the same name. |
| **Rebind Possesable References** | Rebinds all posessable Actors in the current sequence to ensure they're using the most robust referencing mechanism. |
| **Networking** | Lists options for emulating the current sequence in a Client or Server context. |
| **Volatile** | Signifies that this sequence can change dynamically at runtime or during the game. This property must be set if any procedural changes will be made to the source sequence data in game. |
| **Blocking Evaluation** | Enables the sequence to fully evaluate and apply its state every time it is updated. |

## View Options

The View Options button displays a dropdown menu with the following tools, commands, and options:

![sequencer view options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/491be97c-ffb7-4284-bc3a-ab15e123bd75/viewbutton.png)

| Name | Description |
| --- | --- |
| **Pilot Camera** | Toggles the piloted camera between the viewport camera and the camera cut track camera. |
| **Auto Scroll** | 
Enables automatic panning in Timeline view to keep the playhead in view when playing.

![sequencer auto scroll](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8073c66-d8ef-44b0-a36f-42c936d9ceaf/autoscroll.gif)

 |
| **Range Slider** | 

Toggles the display of the bottom timeline region between a Maya-style range slider and a second timeline bar.

![sequencer range slider](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75abaafc-fd7d-448f-aa3e-f1f2dbca37b8/rangeslider.png)

 |
| **Selected Nodes Only** | Automatically filters tracks when enabled to list only tracks or sub-tracks matching the selected Actor. |
| **Combined Keyframes** | Shows or hides a preview of a track's keyframes when collapsed. |
| **Channel Colors** | 

Enables the visualization of common colors for transform axes in the Timeline view. Red = X, Green = Y, and Blue = Z.

![sequencer channel colors](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9503a32-ce3a-4f92-b517-27cbfd8544aa/channelcolors.png)

 |
| **Pre/Post Roll** | Toggles the display of the pre-roll and post-roll visualization for sections. |
| **Zero Pad Frame Numbers** | Applies the selected amount of digit padding to the displayed time. Only applies when you are displaying time as frames. |
| Organize and Sort |   |
| **Expand/Collapse Nodes** | Expands or collapses a selected track. |
| **Expand/Collapse Nodes and Descendants** | Expands or collapses a selected track, including all sub-tracks. |
| **Expand All Nodes** | Expands all tracks and sub-tracks in the sequence. |
| **Collapse All Nodes** | Collapses all tracks in the sequence. |
| **Sort All Nodes** | Sorts all tracks by type, then alphabetically within the types. |
| **Show Marked Frames Globally** | Makes marked frames in a sub-sequence visible to its parent or sibling sequence. |
| **Clear Global Marked Frames** | Sets all marked frames in all sub-sequences to not display. |

## Playback Options

The Playback Options button displays a dropdown menu with the following tools, commands, and options:

![sequencer playback options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c23294d4-611b-4bc4-b45b-5dfbd012afc0/playbackbutton.png)

| Name | Description |
| --- | --- |
| **Start** | Sets the start time of the sequence. |
| **End** | Sets the end time of the sequence. |
| **Playback Speed** | Displays options for previewing the current sequence's playback at different speeds. |
| **Playback Range Locked** | Locks the start and end times of the sequence and prevents editing. |
| **Game View (Clean Playback Mode)** | Automatically enables Game View whenever the sequencer is being played. |
| **Rerun Construction Scripts** | Enables the construction script from Blueprint Actors to run every tick. This also requires you to enable the **Run Construction Script in Sequencer** property in the Blueprint's Class Settings. |
| **Async Evaluation** | Enables a single asynchronous evaluation once per frame. When disabled, this forces a full blocking evaluation every time the sequence is evaluated. This should be enabled for sequences that run in real time. |
| **Evaluate Sub Sequences in Isolation** | Isolates a sub-sequence or a shot from the master sequence when viewing it. This will disable any tracks or content that may be propagating from the master sequence, as well as disable the shot range preview. |
| **Keep Cursor in Playback Range While Scrubbing** | 
Clamps the playhead within the start and end regions of the sequence when scrubbing.

![sequencer clamp scrub](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73f192b7-455c-4898-9008-cdb81fb0bf5c/clampscrub.gif)

 |
| **Link Curve Editor Time Range** | 

Synchronizes the Curve Editor's view with Sequencer's timeline.

![sequencer sync view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d1ad248-6d27-4436-8d5c-8bf4fa0fc4b0/cesync.gif)

 |
| **Jump Frame Increment** | Sets the number of frames to jump when pressing Shift + Left / Right Arrows to jump forward and backward in the timeline. |

## Keyframe Options

The Keyframe Options button displays a dropdown menu with the following options:

![keyframe options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/134ab17a-eff4-4ed8-8f29-a70d97bb7dc3/keyframebutton.png)

| Name | Description |
| --- | --- |
| **Key All** | All transform channels will be keyframed when a value is changed and if auto key is enabled. |
| **Key Group** | All axes within a channel will be keyframed when a value is changed and if auto key is enabled. |
| **Key Changed** | Only the axis that changes will be keyed if auto key is enabled. This is the default behavior. |
| **Cubic (Auto)** | When a new keyframe is created, the tangents will be automatically managed and smoothed during changes. This is the default behavior. |
| **Cubic (User)** | When a new keyframe is created, the tangents will be user controlled and will not change if the keyframe is adjusted. |
| **Cubic (Break)** | When a new keyframe is created, the tangents will use cubic interpolation and broken to allow for individual edits to in/out angles. |
| **Linear** | When a new keyframe is created, the tangents will use linear interpolation. |
| **Constant** | When a new keyframe is created, the tangents will use stepped interpolation meaning they retain the previous keyframe's value until the next keyframe. |

## Auto Key

The Auto Key button enables Auto Key mode which automatically creates keyframes when channels or properties are changed.

![sequencer auto key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e74ad7a1-948f-4ecd-8672-bf8357353cd2/autokey.gif)

Auto Key will only add keyframes if the track already contains at least one keyframe.

## Edit Options

The Edit Options button displays options for automatic behavior when manipulating Sequencer-bound and Level-bound actors.

![sequencer edit options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3906aa4f-6127-4a96-aae8-c9cfb79795e8/editbutton.png)

| Name | Description |
| --- | --- |
| **Allow All Edits** | Enables interaction with both Sequencer-bound and Level-bound Actors. Both edit operations occur in their respective realms (Sequencer or Level). |
| **Allow Sequencer Edits Only** | 
Manipulating any Level-bound Actor will automatically add the Actor to the current sequence under a folder named: Autotracked Changes.

![allow sequencer edits only](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fcae60d-79a8-40bb-a05c-6cb54060ee17/seqedits.gif)

 |
| **Allow Level Edits Only** | Disables all interaction with Sequencer. You cannot set any keyframes and any edits can only occur in the Level. |

## Snapping

The Snapping button enables the ability to have your keyframes or playhead marker snap to increments or other keyframes within the timeline.

The Snapping dropdown menu contains options for customizing the snapping behavior.

![sequencer snapping](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c094ee47-f4b7-425b-a53e-109d0ca71d13/snappingbutton.png)

| Name | Description |
| --- | --- |
| Key Snapping |   |
| **Snap to the Interval** | 
Snaps keyframes to time intervals when moving along the timeline.

![snap keys time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38602111-f17c-43b1-998a-2383745e868e/snapkeyinterval.gif)

 |
| **Snap to Keys and Sections** | 

Snaps keyframes to other keys, or the start and end of sections when moving along the timeline.

![snap keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2fcaab7-4d1d-41d9-8ba1-651b7b7868ab/snapkeykeys.gif)

 |
| Section Snapping |   |
| **Snap to the Interval** | 

Snaps sections to time intervals when scaling or moving sections in the timeline.

![snap sections time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c6be63e1-89e0-4321-8dac-8be9948d4fc1/snapsectionsinterval.gif)

 |
| **Snap to Keys and Sections** | 

Snaps sections to other keys, or the start and end of sections when moving along the timeline.

![snap sections keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/badebc4f-2948-473d-a914-fb5f934d3d27/snapsectionskeys.gif)

 |
| Keys and Sections Snapping |   |
| **Snap Keys and Sections to the Playback Range** | 

Clamps key and section placement to within the playback range.

![clamp keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70b187f9-ab0b-4e16-b20b-9706d5ff27ea/snapkeysrange.gif)

 |
| Play Time Snapping |   |
| **Snap to the Interval While Scrubbing** | 

Snaps the playhead marker to time intervals while scrubbing.

![snap playhead time](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5fb58799-88cf-4ccc-bd6f-56eec64e0488/snapplayheadinterval.gif)

 |
| **Snap to Keys While Scrubbing** | 

Snaps the playhead marker to other keys, or the start and end of sections while scrubbing.

![snap playhead keys](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/346d7b84-5550-4884-9158-1c323ce4cee6/snapplayheadkeys.gif)

 |
| **Snap to the Pressed Key** | 

Pops the playhead marker to a keyframe when clicked. This can also be done when holding Shift and clicking the keyframe if this option is disabled.

![pop playhead key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/53bca1c0-aedf-4ecd-a0c3-bcbb1ff9836e/snapplayheadselectkey.gif)

 |
| **Snap to the Dragged Key** | 

Keeps the playhead maker at the same time as the keyframe when dragging the keyframe along the timeline.

![snap playhead dragging](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e668371-e967-4629-a524-965ecd8db0bd/snapplayheaddragkey.gif)

 |
| Curve Snapping |   |
| **Snap Curve Key Values** | 

Toggles value snapping in the Curve Editor.

![snap curve key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dec813e7-f77d-4365-971f-b81b0a86f8bb/snapcurvekey.gif)

 |

## Frames Per Second

The Frames Per Second (FPS) menu displays options for specifying the frame rate of a sequence, the unit of time to be used, and other timing-related options.

![sequencer fps](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/575dca9a-fd52-4dd6-ab01-8ebcb7ca1a77/seqfps.png)

| Name | Description |
| --- | --- |
| **Show Time As** | 
Specifies the unit of time to display in your sequence to Frames, Seconds, or Timecode. This affects all time displays in your sequence.

![show time as](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1655c797-9470-4844-bffa-3fa254d87c28/showtimeas.gif)

 |
| **Clock Source** | 

Directs Sequencer to advance time in one of the following ways:

-   Tick uses the default mechanism for how the engine advances time.
-   Platform uses system time.
-   Audio uses the audio clock and is useful for keeping audio and visuals in sync.
-   Timecode uses the absolute timecode if one is being used.
-   Relative Timecode advances relative to the timecode when you press play.



 |
| **Lock to Display Rate at Runtime** | Locks the playback of this sequence to the chosen FPS display rate. |
| **Advanced Options** | 

Opens a window in which you can specify different tick intervals for your sequence.

![advanced time properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a63f7249-a446-4a75-a398-88da4b92b0aa/advtime.png)

 |

## Curve Editor

The Curve Editor button displays the Curve Editor tab, which can be used to fine-tune your keyframes and tangents.

Visit the **[Curve Editor](/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine)** page to learn more about it.

![sequencer curve editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d803bbc-e555-4cf9-a619-d1820fe03e76/curveeditorwindow.png)

## Breadcrumbs

The breadcrumbs area of the toolbar displays the name of the current sequence. When using master sequences and shots, it can be used to navigate between your shots and the master sequence.

Use the forward and backward buttons to navigate through your view history, or use the folder button to navigate through all shots in a tree view.

![sequencer breadcrumbs navigate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c81e4d4-31ba-4d08-b429-eb67dca2b959/navcrumbs.gif)