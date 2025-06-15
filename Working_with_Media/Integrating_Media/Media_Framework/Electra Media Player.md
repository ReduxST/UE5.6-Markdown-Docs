# Electra Media Player

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/electra-media-player-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/electra-media-player-in-unreal-engine)  
**Processed:** 2025-06-14 16:21:52

---

![Media streaming inside Unreal Engine using the Electra Media Player](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/952c4b09-05a2-4a78-86cb-0aaac8d6be7c/player_image.png)

Electra Media Player is a media player plugin for Unreal Engine, designed primarily for streamed media hosted on the Internet.

Electra supports the following media types:

-   live streams and static video-on-demand streams in MPEG, DASH, or HLS formats
-   Internet radio streams encoded in mp3 (ISO 11172-3 MPEG audio layer 3) and delivered using Icecast or Icycast
-   static `.mp4`, `.mkv`, and `.mp3` files from the Internet, local network, and local files

Electra is supported on the following platforms:

-   Windows 10 or later
-   macOS
-   iOS 13.0 or later
-   Android 5.1 or later
-   Playstation 4
-   Playstation 5
-   Xbox One/S/X
-   Xbox Series X
-   Nintendo Switch

The maximum playable video resolution and frame rate, as well as the supported codecs, depends on the platform. See the respective platform documentation for their specifications.

## Supported Codecs

Electra Media Player supports media files and streams encoded with the following codecs.

### Video

| Media Type | Stream Protocol or Container | Availability |
| --- | --- | --- |
| H.264 / AVC (ISO/IEC 14496-10) | DASH, HLS, mp4, mkv | Only using platform OS |
| H.265 / HEVC (ISO/IEC 23008-2) | DASH, HLS, mp4, mkv | Only using platform OS |
| VP8 | DASH, mp4, mkv, webm | Using platform OS or additional plugin |
| VP9 | DASH, mp4, mkv, webm | Using platform OS or additional plugin |

### Audio

| Media Type | Stream Protocol or Container | Availability |
| --- | --- | --- |
| AAC (LC, HE, HEv2) (ISO/IEC 14496-3) | DASH, HLS, mp4, mkv | Using platform OS |
| MPEG layer 3 (ISO 11172-3) | HLS, mp4, mp3 | Using additional plugin |
| Opus | DASH, mp4, mkv, webm | Using additional plugin |
| FLAC | mp4, mkv | Using additional plugin |

### Subtitles

| Media Type | Stream Protocol or Container | Availability |
| --- | --- | --- |
| tx3g | DASH, mp4 | Using subtitle plugin |
| TTML / IMSC1 | DASH | Using subtitle plugin |
| wvtt | DASH, mp4 | Using subtitle plugin |

## Additional Codecs

Additional plugins for Electra are available in the Plugin Manager. To learn about installing plugins, see [Working with Plugins](/documentation/en-us/unreal-engine/working-with-plugins-in-unreal-engine).

## Supported Media Formats

Video, audio, and subtitles are encoded into a media elementary stream with one of the supported and appropriate codecs. Any combination of media elementary streams is then packaged into a supported container format (typical file extensions being `.mp4`, `.mkv`, or `.ts`).

Not every type of elementary stream can be placed into every container, such as in the following examples:

-   If you try to place VP9 video into an MPEG transport stream, it will be placed into a private stream that is not necessarily recognized by media players.
-   H.264 cannot be placed into a webm container. The webm container is exactly the same as the Matroska/mkv container, but webm artificially restricts the codecs to VP8, VP9, Opus and Vorbis. Other codecs are not permitted with webm.

For internet streaming, container files are split into short segments and video is typically provided in different resolutions and bitrates to allow for seamless switching between quality levels based on the user's current network bandwidth. This is handled by the DASH and HLS protocols.

Every supported container file however can be streamed from the internet, but if the network bandwidth is not able to sustain the data rate of the file playback will eventually start to stall for buffering.

Media files are not progressively downloaded or stored. Data is consumed as it arrives. Therefore, files containing multiple elementary streams need to have data from each stream interleaved in short intervals. For example, if a file has all the data for a video elementary stream first, followed by all the data for audio elementary stream, then the file cannot be played back. This would require random access into the file, which is the opposite of linear data streaming.

## Media format restrictions

Only media streams with supported codecs and container files can be played. If a media file contains multiple streams (tracks), streams of a supported codec will be played and unsupported streams will be ignored.

Some video decoders on the target platform have limitations for resolution, framerate, profile, level, or a combination of those properties. This means that it is possible for the same media file to play the video stream on one platform and be ignored on another platform, depending on these limitations.

### Encrypted Media

Encryption of media streams is supported with DASH and HLS only. Any `.mp4`, `.mp3`, `.ts`, `.mkv`, or `.webm` files that use encryption cannot be played back.

Encryption must follow ISO/IEC 23001-7. Both "cenc" and "cbcs" schemes are supported. For HLS, full segment encryption (AES-128 PKCS#7) is supported as well.

Custom DRM systems can be implemented using plugins.

### Unsupported Features

Some features of DASH and HLS are not supported by Electra as they are rarely used.

#### DASH

-   The most commonly used profiles for Live and On-demand streaming are supported.
-   Full profile and some profiles that include certain features (even if not actually used by the presentation) are not supported.
-   Profiles requiring transport streams are not supported.
-   Of the different segment addressing types, is not supported.

#### HLS

-   All segment types (`mp4` derivatives, MPEG TS and packed audio (`aac` and `mp3`)) are supported.
-   Subtitles are not currently supported, but support is planned for a future release.
-   The following playlist tags are not supported:
    -   `#EXT-X-I-FRAMES-ONLY`
    -   `#EXT-X-PART-INF`
    -   `#EXT-X-PART`
    -   `#EXT-X-BITRATE`
    -   `#EXT-X-DATERANGE`
    -   `#EXT-X-SKIP`
    -   `#EXT-X-PRELOAD-HINT`
    -   `#EXT-X-RENDITION-REPORT`
    -   `#EXT-X-I-FRAME-STREAM-INF`
    -   `#EXT-X-SESSION-DATA`
    -   `#EXT-X-SESSION-KEY`
    -   `#EXT-X-INDEPENDENT-SEGMENTS` (this is implicitly assumed as this is a requirement for Electra)
    -   `#EXT-X-VERSION` (not evaluated, up to version 12 is supported)
    -   `#EXT-X-SESSION-KEY` (license keys are not prefetched)
-   The following tags are recognized and partially used to aid playback, but are not yet fully supported:
    -   `#EXT-X-SERVER-CONTROL`
    -   `#EXT-X-CONTENT-STEERING`
-   The following optional tags are supported:
    -   `#EXT-X-DEFINE`
    -   `#EXT-X-GAP`

#### Support for older HLS streams

Many of the attributes that can appear with a playlist tag are optional, and can be absent in older playlists. To determine if an elementary stream can be played back, Electra needs to know its codec and (for video) the resolution and frame rate. If these tags are absent, Electra assumes that video is present in H.264, high profile level 4.0, and audio is present as stereo LC-AAC.

If there are several variant streams, they will be assigned one of the most commonly used resolutions, starting with 1080p for the variant with the highest bandwidth attribute. Assigned resolution will decrease for each additional variant in descending bandwidth order. Framerate is assumed to be no better than 30 frames per second (fps). Warnings will be logged to the console if any such assignments have been made since they are probably incorrect and could lead to malfunctioning playback.

Electra does not load each variant stream's playlist and then a random media segment from each list to probe the actual media content as this would take a very long time and delay playback start. Electra assumes that all relevant variant stream information, like `CODECS`, `RESOLUTION`, and `FRAME-RATE` (if higher than 30 fps) are given and are correct. Selection of variant streams is based entirely on this information.

This requirement is also true for DASH, but with DASH these attributes are mandatory and therefore have to exist.

For maximum compatibility of newly created HLS streams, you must follow the [Apple guidelines](https://developer.apple.com/documentation/http-live-streaming/hls-authoring-specification-for-apple-devices).