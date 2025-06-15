# Tracks

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:27

---

In Sequencer, Actor properties and other elements are accessed by the adding of tracks to your timeline. Depending on the track's type, they can be used to organize your tracks, create keyframes, or enable other auxiliary functions.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).

## Track List

Below is a list of the main tracks you can add in Sequencer.

## Adding Tracks

Sequencer provides a variety of ways to add tracks to your timeline.

Clicking **Add Track (+)** in Sequencer's Outliner reveals the list of tracks to add to your sequence. Select any track here to add it to Sequencer.

![sequencer track list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bf8e3d72-858d-4180-b562-d7e5a78e65c7/addtrack1.png)

Right-clicking in the empty region of the outliner will also bring up the track list.

![sequencer track list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/235cc8c3-0b6c-4228-96da-f8f511a1dee0/addtrack2.png)

### Adding Actors

One of the most common track Sequencer uses is the [Object Binding Track](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine). These are tracks that bind to **Skeletal Meshes**, **Static Meshes**, **Effects**, **Blueprints**, **Components** and other objects in a Level.

You can add Actors to your sequence by navigating in the **Add Track (+)** menu to the **Actor To Sequencer** submenu. Here you can choose any Actor currently in your Level to add to your sequence, or you can also search for a specific Actor using the search bar.

![actor to sequencer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4d8d16a5-9a78-4a8d-b95e-14e1e2153cbd/addactor1.png)

If an Actor is already selected in your Level, then it will be listed at the top of the **Actor To Sequencer** list for convenience.

You can also drag Actors from other windows, like the [Outliner](/documentation/en-us/unreal-engine/outliner-in-unreal-engine) and add them into Sequencer.

![actor to sequencer drag drop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66ec803a-7711-4608-9a0b-be80f87c37ae/addactor2.png)

Actors can also be added as [Spawnables](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics) by dragging them from the [Content Browser](/documentation/en-us/unreal-engine/content-browser-in-unreal-engine) or [Place Actors](/documentation/en-us/unreal-engine/placing-actors-in-unreal-engine) panels.

![actor to sequencer content browser place actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db4b5bc2-2035-48c6-b2de-be8bddc02bb0/addactor3.png)

### Adding Components

Some tracks allow for components and other track types to be added under their main header track. This is done to access specific track functionality, such as transform, components, properties, and other similar features.

To add a component track, hover over the track and click **Add Track (+)** to view a list of tracks available for the selected track. Typically, this list will be filtered based on the types of tracks and components that track or Actor can support.

![add child track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19b0e828-1f69-4008-9353-990f4b343529/subtrack.png)

As you can with most menus in Unreal Engine, you can type to filter the results in the **Add Track (+)** menu, making it easier to locate a specific property, component, or other track to add.

![type to filter tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f58d4187-89d0-4575-a4dc-7439cc4594d4/subtrack2.gif)

## Organization

Most tracks have properties that allow for them to be edited and displayed in different ways. These properties are saved in Sequencer and can be shared with others working on your project.

### Renaming

To assist in organization, all top-level tracks and components can be renamed in Sequencer. You can rename a track by triple-clicking on the track text, or right-clicking and selecting **Rename**, or by pressing **F2**.

![rename track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/846535ea-5bcb-4bd1-8031-da16315a78c3/rename1.png)

When renaming a track bound to an Actor in the Level, the Actor in the level also renames.

![rename track renames actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed2fe149-92e2-4b52-8396-7b74e498a360/rename3.gif)

Most, but not all tracks can be renamed. Typically, you cannot rename a track if it is a property. However, some property tracks can be renamed, such as Transform.

![rename track restrict](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37b27ff9-b709-48cb-a67d-486b7916dcc8/rename2.png)

Tracks in Green can be renamed, tracks in Red cannot.

### Lock

Tracks can be locked to prevent keyframes on them and their subtracks from being edited. Right-click a track and select **Locked** to lock that track. When a track is locked, all keyable tracks under it will display with a red border denoting the lock state.

![lock track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/75687538-0d53-4d8e-80a3-5fced62bfe9a/locking.png)

### Pin

You can **Pin** tracks so that they will appear in a separate outliner section at the top of your Sequencer outliner. Right-click a track and select **Pinned** to pin that track.

![pin track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/abd9a356-f54e-4c38-b199-738bc4aeb88a/pinning.png)

Only one track can be pinned within each sequence.

### Mute

Muting tracks causes them to become inactive and to not display any of their properties or keyframe results from Sequencer. Right-click a track and select **Mute** to mute that track.

![mute track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a228143-f9cc-4662-8de2-6ff09f9b0825/mute.png)

If the **[Object Binding Track](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine)** is muted, it will also hide the Actor in the viewport.

### Solo

When you **Solo** a track, all other tracks will be muted, allowing for the soloed track to be viewed in isolation. Right-click a track and select **Solo** to solo that track.

![solo track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d88f0ed-0fbb-41b1-bd43-f1e183aaad87/solo.png)

Soloing and muting are editor-only operations and do not impact the Level at runtime, unless you are previewing through **[Play In Editor](/documentation/en-us/unreal-engine/in-editor-testing-play-and-simulate-in-unreal-engine)**.

### Reordering

Tracks can be reordered in the outliner by dragging them above or below each other. Visual cues appear when dragging to indicate where the track will be placed.

![reorder tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/049c63b2-826f-49b3-a383-15e46955e5e4/dragdrop.gif)

## Search and Filter

You can search and filter for specific track names using Sequencer's search field. Typing the full or partial name of a track will filter out tracks that do not match that name and will include child tracks as part of its search.

![search track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0280f56-393a-43f1-b8ee-7cef53410e34/search.png)

Clicking the **Filters** button will also reveal a list of common track types that you can filter for.

![filter track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5aab50dc-9e6e-44f8-874d-2735fd6ecad1/filter.png)

When a filter is applied, the **Filter** button will indicate with a red dot.

![filter indication](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5719c24b-6416-4c52-904f-42c29be71d74/filter2.png)