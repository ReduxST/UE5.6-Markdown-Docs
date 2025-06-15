# Sequencer Playlists

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-playlists-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-playlists-in-unreal-engine)  
**Processed:** 2025-06-14 16:48:26

---

For broadcasts, live events, or timing-critical playback, you may find it necessary to trigger different sequences to play at arbitrary times. You can do this using **Sequencer Playlists**, where you can prepare sequences and trigger them to play during a virtual production session.

This document provides an overview of how to use Sequencer Playlists.

#### Prerequisites

-   Sequencer Playlists is a [Plugin](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine) that must be enabled prior to use. Navigate in the Unreal Engine menu to **Edit > Plugins**, locate **Playlists** in the **Virtual Production** section, and enable it. You will need to restart the editor afterward.
    
    ![enable playlits plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56ae4646-df5d-4466-abdb-1110192e15da/plugin.png)
    
-   Your project already contains some [Level Sequences](/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview) that you can reference in your playlist.

## Overview

To start using Sequencer Playlists, navigate to the main Unreal Engine menu and click **Window > Virtual Production > Playlists**. This will open the **Playlists** panel.

![open playlists panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0849ec6d-0fed-44e6-abd8-020279d232ca/overview1.png)

The **Playlists** panel contains the following interface:

![playlists panel interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/572b812f-7d52-4c33-a92a-ba3bb8505810/overview2.png)

1.  The **Toolbar**, where you can **Save**, **Load**, and **create new playlists**.
2.  The name of the current playlist and a short description. You can name a playlist by **Saving** it, and you can edit the description by clicking on the playlist description field.
3.  Adds a **Sequencer item** to the playlist. When one is added, you need to specify the **Sequence** you want to play in the main dropdown menu of the item.
4.  The **Playlist**, which displays the list of Sequences added to the playlist. The following properties can also be set on each item:
    
    -   **Offset**, which controls the start and end trim of the Sequence, when played.
    -   **Hold**, which holds the first frame of the Sequence until it is played. This is done by creating a second instance of the Sequence with its **Time Scale** property set to **0**.
    -   **Loop**, which enables the Sequence to loop when triggered. If looping is enabled, then you must also set the number of times to loop before stopping.
    
5.  **Play Mode**, which enables a more streamlined overlay for your items, making it easier to select **Play** and **Stop** for each Sequence.
6.  **Playback Controls**, which contains the following buttons:
    
    -   **Play All**: Starts playing all playlist items at the same time.
    -   **Stop All**: Stops all playlist items.
    -   **Reset All**: Stops all playlist items and re-holds the first frame for any Sequences that have **Hold** enabled.
    

Hovering your cursor over a Sequence item also reveals additional buttons and properties.

![sequence item interface](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/012e1d21-e626-4f12-8a17-e83c463d9898/overview3.png)

1.  **Playback Controls**, where you can **Play**, **Stop**, and **Reset** this Sequence.
2.  **Settings** for this Sequence, which contains the following:
    
    -   **Playback Controls**.
    -   **Playback Speed**, which controls the playback rate of the Sequence when triggered.
    -   **Mute**, which disables this Sequence from being triggered when clicking **Play All**. This Sequence can still be triggered directly by clicking **Play**.
    -   **Remove from Playlist**, which deletes this Sequence from the playlist.
    

## Workflow Example

The main purpose of Sequencer Playlists is to add pre-created Sequences to a "playlist" so that you can trigger them to play as [Subsequences](/documentation/en-us/unreal-engine/cinematic-subscequences-track-in-unreal-engine) during the playback or recording of another Sequence. In most cases, this is during recording with [Take Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine).

### Create and Populate Playlist

Click the **Add (+) Item** button to start adding Sequences to your playlist.

![create playlist item](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/47f56390-541f-4c80-8337-8ab0b20bcc30/create1.png)

Next, assign a Sequence to the item by clicking the **dropdown menu** and selecting a **Sequence**.

![assign sequence to item](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a0a175a7-1a93-455a-8fa2-4ebb3c8d45e0/create2.png)

Continue to add and assign Sequences to your Playlist until you are satisfied with your list.

![populate playlist with items](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/601dd397-0802-4b15-b7fe-53b6c424efbd/create3.png)

### Trigger Playlist Playback

To trigger the playback of your entire playlist, click **Play All**. This will open a new pending Sequence, if one was not open already, and play all Sequences indefinitely until you stop the playback. Playlist Subsequences will be stored in a folder called **Playlist - (Your Playlist Name)**.

![trigger playlist playback](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ba6b5bf-703c-44fa-8020-ceae094a4ada/trigger1.gif)

The most typical use-case for Playlists will be triggering them during a **Take Recorder** session. During recording, you can trigger your sequences to play at different times by clicking on each Sequence's playback controls. Sequences can be started, stopped, and reset multiple times during the recording and playback process.

![trigger during take recorder session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f45f81c9-829f-4c10-b25e-8a2e9eff8940/trigger2.gif)

You can also enable **Play Mode**, which will enable a more streamlined overlay for your items, making it easier to select Play and Stop for each Sequence.

![play mode easier selection](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4acaf85d-206a-4e44-a32d-9770e8bfeead/trigger3.gif)

### Saving and Managing Playlists

You can save Sequence Playlists by either clicking **Save**, or by opening the Save **dropdown menu** to clicking **Save Playlist As**. Saved playlists are stored in the **Content Browser** as **SequencerPlaylist Assets**.

![save playlist](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8266466-ef00-4019-a9d7-b30ec9ab4311/manage1.png)

Clicking **Load** will display a list of all playlists in your project. Selecting one will load it as the current playlist.

![load playlist](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/076a46ba-38b0-4e2a-9271-0efe835ff00e/manage2.png)

You can clear your current playlist and start over by clicking **Create New Playlist**.

![create new playlist](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a820f372-f717-4637-a7c3-ad25d96979ee/manage3.png)