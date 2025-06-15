# Media Editor Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/media-editor-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/media-editor-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:35:26

---

When opening a **Media Player** asset, the **Media Editor** window will open presenting you with options for playing back and controlling different aspects of your **Media Source** assets. In the Media Editor, you can define the player Plug-in used for a Media Source, select between different audio/video tracks (if applicable) as well as define settings for the Media Player itself. The **Info** tab inside this editor will also display information about the type of media you are accessing which can be used to debug any potential playback problems. Please refer to each of the sections below for more information and a breakdown of the available options.

## Toolbar

![Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a536c8bf-abb1-45f6-aada-8ea045517161/01-toolbar_ue5.png)

The **Toolbar** section of the Media Editor enables you to control the playback of media.

You must first select a valid Media Source from the **Media Library** window that you want to play for the playback options to become available.

| Option | Description |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df813d9a-87b1-494e-9dab-bdc412d30eee/02-save-icon_ue5.png) | Saves this Media Player asset (**Ctrl+S**). |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b03651e2-09c2-44cb-9b3c-9f54ede30ee1/03-browse-icon_ue5.png) | Browse to the Media Player asset in the Content Browser (**Ctrl+B**). |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28d31dfe-1fdb-4f41-ba8d-6d44d58dc2dd/04-prev-icon_ue5.png) | Jump to previous item in the Playlist. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/05ec5cbe-6d00-4f93-b59c-191fa8e87375/05-rewind-icon_ue5.png) | Rewind the media source to the beginning. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14d0ad68-3496-464b-9981-2d4e0fc4d46a/06-reverse-icon_ue5.png) | Reverse playback of the selected media (clicking multiple times increases the seek speed). |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec5e7dcc-abc5-46f0-b151-9e9727122b01/07-play-icon_ue5.png) | Start/Resume media playback. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbc1106b-22e7-4ead-8461-c42f5683a698/08-pause-icon_ue5.png) | Pause media playback. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8867b58d-b076-4214-94b0-628ffc8268e8/09-forward-icon_ue5.png) | Fast forward media playback (clicking multiple times increases the seek speed). |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c51296b-488f-4795-b89d-88f314001ca1/10-next-icon_ue5.png) | Jump to the next item in the Playlist. |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de6d32c3-aae7-40b0-8468-693b8e56d780/11-close-icon_ue5.png) | Close the currently opened media. |

## Player Window

![Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1e33eeb4-78cb-485b-88f0-eeadb6cf6376/12-player-window_ue5.png)

The **Player Window** enables you to view the playback of your media as well as define **Playback Options**. When you open a Media Source and mouse over this window, you will see text overlays that display the name of the file (upper-left), the current player Plug-in being used (upper-right), the state of the media (lower-left), and the current horizontal, vertical fields of view and view rotation (lower-right), which is used for 360 videos.

At the top of the Player Window, there is a text field that displays the URL path (which you can use to Open directly in Blueprint with the **Open URL** Blueprint node). To the right of the URL field, a reload button can be used to reload the current media (similar to pressing the reload button on most web browsers and can be used to reload external URLs that link to the Internet). To the left of the URL field, via the drop-down menu, are the **Capture Devices** options.

### Capture Devices

![Capture Devices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c9cca56b-782f-4868-8cec-e49c3d95ec35/13-capture-devices_ue5.png)

The **Capture Devices** menu and options are available when you have a connected and [supported device](/documentation/en-us/unreal-engine/media-framework-technical-reference-for-unreal-engine) attached to your computer. These options enable you to test different audio and capture devices where the URL will update with the selected device. Capture Devices are slightly different the other Media Sources in that you can have multiple devices connected. You can use Blueprint (or C++) code to enumerate and filter for specific devices.

![Enumerate](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07f3e5e6-a6a3-4cc7-9a56-e794862c3fc4/14-enumerate-filter_ue5.png)

Above, in a Blueprint, you can search for enumerate or capture devices to see the list of optional enumerators.

In the example below, a sample setup using the **Enumerate Video Capture Devices** node is shown to filter for specified devices that we can use to obtain the URL to open.

![Enumerate Example](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6adead9-3a14-45f9-91f0-13acd4d89302/15-enumerate-video-capture-devices_ue5.png)

Please see the [Playing Live Video Captures](/documentation/en-us/unreal-engine/playing-live-video-captures-in-unreal-engine) page for more information.

### Playback Options

![Playback Options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/95ddb3ba-40f2-409a-89fb-77f8240fbed9/16-playback-options_ue5.png)

Also part of the Player Window is the **Playback Options** menu that contains several different options used to define how your media is played.

**Player**

| Option | Description |
| --- | --- |
| **Decoder** | This section enables you to define the player Plug-in used for media. Automatic is the default setting which will auto-select the appropriate player Plug-in based on the type of media. |

**Tracks**

| Option | Description |
| --- | --- |
| **Audio** | Enables you to set the default audio track associated with a media source (if multiple audio tracks are embedded with the media) or disable the audio track. |
| **Captions** | Enables you to define the default caption track for a selected media source (if tracks are embedded with the media). |
| **Subtitles** | Enables you to define the default subtitles track for a selected media source (if tracks are embedded with the media). |
| **Text** | Enables you to define the default text track for a selected media source (if tracks are embedded with the media). |
| **Video** | Enables you to set the default video track associated with a media source (if multiple video tracks are embedded with the media) or disable the video track. |

**Formats**

| Option | Description |
| --- | --- |
| **Audio** | Displays the available audio format tracks which you can select from (if applicable). |
| **Captions** | Displays the available caption format tracks which you can select from (if applicable). |
| **Subtitles** | Displays the available subtitle format tracks which you can select from (if applicable). |
| **Text** | Displays the available text format tracks which you can select from (if applicable). |
| **Video** | Displays the available video format tracks which you can select from (if applicable). |

**View**

| Option | Description |
| --- | --- |
| **Scale** | Change the video size to Fit (fit video in the Player Window), Fill (fill video in the Player Window) or Original Size (to use the original dimensions of the video). |
| **Show Text Overlays** | Toggles the display of any associated overlay assets with the selected media. |

## Media Library

![Media Library](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e1b7f2f2-1327-4b93-ae75-a0b4f6d3f8df/17-media-library_ue5.png)

The **Media Library** displays all of the Media Source assets within your project that you can open in the Media Editor. You can right-click on a source in this window to open up a context menu that you can use to edit the asset, open in the Media Editor, browse to the asset in the Content Browser or show the location of the Media File on your computer. This window also displays the type of each Media Source as well as their associated URL string.

## Playlist

![Playlist](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8cf36ffc-2f62-4a60-8c9e-d52f1dca2ff0/18-playlist-forward_ue5.png)

The **Playlist** section of the Media Editor not only displays all of the files contained within a Media Playlist but also enables you to create/save new Media Playlists assets inside your project. The arrows in the upper-right corner of the Playlist window function similar to the Toolbar's **Prev** and **Next** buttons and enable you to cycle through Media Sources in your playlist.

![Playlist section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6e1fa1a5-e28c-4ad2-bbec-8423464444b2/19-playlist-back_ue5.png)

Above, an active Media Playlist displays each of the Media Sources contained within it with the arrow marker pointing to the currently playing source.

Each Media Source (when active) has a local Media Playlist created inside the Media Editor. You can save the local Media Playlist as a new Media Playlist by clicking the **Save** icon.

![Unsave Playlist](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/674ed77c-b11c-4561-918f-07b0b26bd0a6/20-playlist-save-icon_ue5.png)

## Details / Info

![Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/58c1a57e-8349-49ec-9352-9932150257b9/21-details-window_ue5.png)

The **Details** panel provides options for controlling playback of the Media Player itself.

**Playback**

| Option | Description |
| --- | --- |
| **Play on Open** | When enabled will automatically start to play a Media Source when opening the source through Blueprint or C++. |
| **Shuffle** | When a Playlist is opened, if this option is enabled, the player will randomly select a source within the playlist rather than playback sequentially. |
| **Loop** | When enabled will loop a single Media Source or entire Media Playlist (looping Video Capture devices is not supported). |

**View Settings**

| Option | Description |
| --- | --- |
| **Horizontal Field of View** | Enables you to manually set the Horizontal FOV value for 360 videos. |
| **Vertical Field of View** | Enables you to manually set the Vertical FOV value for 360 videos. |
| **View Rotation** | Enables you to manually set the View Rotation for 360 videos. |

**Editor**

| Option | Description |
| --- | --- |
| **Affected by PIEHandling** | Enables you to set whether this player should stop when entering or exiting PIE. |

### Info Panel

![Info Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/159cad38-1226-468c-b5ad-368dd78b27ae/22-info-window_ue5.png)

The **Info** panel provides information about the selected Media Source that you can use for debugging purposes. This window displays the player Plug-in associated with the file, the number of video and audio streams and information about video and audio tracks such as the codec being used, sample rate and dimensions.

Any errors when trying to playback video will be displayed here, for example, if you attempt to load an unsupported format, it will list it in this window as **Not supported**. Additionally, you can use the **Copy to Clipboard** button to copy this information out which you can use to post to our official forums or [Answer Hub](https://answers.unrealengine.com/) pages to get help with and troubleshoot any playback issues.