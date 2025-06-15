# AJA Media Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/aja-media-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/aja-media-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:05:24

---

This page describes the options and settings exposed on AJA Media Framework objects.

## Supported AJA Cards and Software

The AJA Media Source and AJA Media Output have been tested with the following cards, using **Version 15.2** or later of the AJA Desktop Software:

-   **Corvid 88**
    
-   **Corvid 44 12G**
    
-   **Corvid 44 12G BNC**
    
-   **Corvid 44**
    
-   **Corvid 44 BNC**
    
-   **KONA 4** (4K bitfile is supported, UFC bitfile is not supported)
    
-   **KONA 5** (Both `KONA 5 (4K)` and `KONA 5 (8K)` bitfiles are supported)
    
-   **KONA HDMI**
    
-   **Io 4K Plus**
    

Other devices and SDK versions may or may not work as expected.

## AJA Media Source

Each AJA Media Source asset you create exposes the following Configuration dropdown menu settings and Details panel settings.

### AJA Media Source Configuration Dropdown Settings

The settings described here are available in the Configuration dropdown menu accessible at the top of the AJA Media Source Details panel.

![AJA Media Source Configuration dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/26a8d2e6-df63-4385-9576-8d249e1c84e3/aja-source-dropdown.png "AJA Media Source Configuration dropdown menu")

| **Setting** | **Description** |
| --- | --- |
| **Device** | Sets the AJA device that this Media Source will use to bring video into Unreal Engine. If you have multiple cards or devices attached to your computer, you can choose which one to use here. |
| **Source** | Sets the port or SDI connection on the specified device that this Media Source will use to bring video into Unreal Engine. Note that only single-link connections are supported. |
| **Resolution** | Sets the resolution of the incoming video feed. Note that this must match the actual video feed exactly. |
| **Standard** | Sets whether the incoming video feed is progressive or interlaced. Note that this must match the actual video feed exactly. |
| **Frame Rate** | Sets the number of video frames per second in the incoming feed. Note that this must match the actual video feed exactly. |

### AJA Media Source Details Panel Settings

The settings in the Details panel shown under **AJA** > **Configuration** are always greyed-out, as they are set through the Configuration dropdown menu. The values for these settings are shown as a reference. Depending on the specific Media Source asset, some of the reference fields might not apply.

The Media Source Details panel settings are shared for all capture cards, so some of the settings will be nonfunctional. Check carefully what settings are appropriate for your AJA capture card.

![AJA Media Source Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a9dfa515-4269-491e-b9c2-9cfd19f5bcce/aja-source-details.png "AJA Media Source Details panel")

| **Setting** | **Description** |   |   |
| --- | --- | --- | --- |
| **AJA** |   |   |   |
| **Configuration** | Provides access to the Configuration dropdown, and shows a summary of the settings. |   |   |
| **Configuration - Media Connection** |   |   |   |
| **Device** | Shows the AJA device that this Media Source will use to bring video into Unreal Engine. Includes subfields for the **Device Name** and the **Device Identifier**. Read-only. |   |   |
| **Protocol** | Shows the communication protocol. Read-only. |   |   |
| **Transport Type** | Shows the transport type. Read-only. |   |   |
| **Quad Transport Type** | Shows the Quad transport type, when applicable. Read-only. |   |   |
| **Port Identifier** | Shows the port. Read-only. |   |   |
| **Configuration - Media Mode** |   |   |   |
| **Frame Rate** | Shows the number of video frames per second in the incoming feed. Note that this must match the actual video feed exactly. Read-only. |   |   |
| **Resolution** | Shows the resolution of the incoming video feed. Note that this must match the actual video feed exactly. Read-only. |   |   |
| **Standard** | Shows whether the incoming video feed is progressive or interlaced. Read-only. |   |   |
| **Device Mode Identifier** | Shows the mode identifier for the AJA device. Read-only. |   |   |
| **Timecode Format** | Specifies the type of timecode that accompanies the video signal. |   |   |
| **Capture with Auto Circulating** | 
Captures video, audio, and ancillary data at the same time. This may decrease your transfer performance, but it guarantees that all data for each frame will be synchronized together. If you experience problems with latency, you can try disabling this option.



 |   |   |
| **Ancillary** |   |   |   |
| **Capture Ancillary** | Determines whether Unreal Engine captures ancillary metadata that accompanies the video signal. |   |   |
| **Ancillary - Advanced** |   |   |   |
| **Max Num Ancillary Frame Buffer** | Sets the maximum number of frames of ancillary data Unreal Engine will store in memory at any given time. If the input video jumps or hitches, you can try raising this value. |   |   |
| **Audio** |   |   |   |
| **Capture Audio** | Determines whether Unreal Engine captures audio from the Media Port. |   |   |
| **Audio Channel** | Specifies the audio channel that contains the signal you want Unreal Engine to capture. |   |   |
| **Audio - Advanced** |   |   |   |
| **Max Num Audio Frame Buffer** | Sets the maximum number of frames of audio data Unreal Engine will store in memory at any given time. If the input video jumps or hitches, you can try raising this value. |   |   |
| **Video** |   |   |   |
| **Capture Video** | Determines whether the Unreal Engine captures video from the Media Port. |   |   |
| **Color Format** | Determines the order of the color channels that make up each pixel in the input video, and the number of bits in each channel. |   |   |
| **Deinterlacer** | 

You can select how an incoming interlaced stream should be processed. Options are:

-   None (default)
-   Blend Deinterlacer
-   Bob Deinterlacer
-   Discard Deinterlacer



 |   |   |
| **Interlace Field Order** | The order in which interlace fields should be copied. Options are: Top Field First and Bottom Field First. |   |   |
| **Override Source Encoding** | Enable this field to override the source encoding. Select the override encoding from the dropdown menu. |   |   |
| **Override Source Color Space** | Enable this field to override the source color space. Select the override color space from the dropdown menu. |   |   |
| **Video - Color Conversion Settings** |   |   |   |
| **Configuration Source** | Use this property to define your OCIO configuration. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. |   |   |
| **Transform Source** | Use this property to define your OCIO transform source. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. |   |   |
| **Transform Destination** | Use this property to define your OCIO transform destination. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. | **Video - Advanced** |   |
| **Max Num Video Frame Buffer** | Sets the maximum number of frames of video data Unreal Engine will store in memory at any given time. If the input video jumps or hitches, you can try raising this value. |   |   |
| **Debug** |   |   |   |
| **Log Drop Frame** | When enabled, Unreal Engine prints a message to its output log every time it detects a dropped frame in the input feed. |   |   |
| **Burn Frame Timecode** | When enabled, the engine embeds the timecode of each frame into the captured video. You can use this to check that the timecode for each frame of input matches the values you're expecting. See [Timecode Texel Encoding](/documentation/en-us/unreal-engine/timecode-and-genlock-in-unreal-engine#timecodetexelencoding). |   |   |
| **Synchronization** |   |   |   |
| **Time Synchronization** | Determines whether users want to synchronize Media based on the engine's timecode. A prerequisite for the Timecode Sample Evaluation Type and Frame Delay setting. |   |   |
| **Frame Delay** | This setting depends on whether time synchronization is enabled or not. It is used to find the right frame based on the engine’s timecode and is calculated based on the player/media source frame rate. For example: If the Player is at frame #2 and you set the value of Frame Delay at 1 Frame, the Media Player will display an older frame (2 - Frame Delay = 1) on the screen, despite frame #2 also being available. |   |   |
| **Time Delay** | This setting is used when you aren't using time synchronization, similarly to Frame Delay it is taken into account when the engine selects the frame to display. |   |   |
| **Synchronization - Advanced** |   |   |   |
| **Just in Time Rendering** | Enabling this option defers the processing of the media source’s pixels to the last possible point in the current frame pipeline, which provides more time for pixels to arrive from external sources and be rendered in the current frame on the playback device. |   |   |
| **Framelock** | This option does not function for AJA sources, and will be ignored if enabled. |   |   |
| **Sample Evaluation Type** | 

Latest - Displays the received sample as soon as possible. This does not use any of the time-based synchronization techniques and shows the latest available frame. PlatformTime - The displayed sample is synchronized based on the platform time. Timecode - Synchronize based on the timecode. Requires a timecode provider set either in the Media Profile or the Project settings.

Determines whether the Unreal Engine outputs only the fill image, or both the fill and key images. When you set this to **Fill Only**, only the fill image is output to the **Source** set below. When you set this to **Fill and Key**, the fill image is output to the **Source**, and the key is output to the **Key Source**.



 |   |   |

## AJA Media Output Settings

Each AJA Media Output object you create exposes the following Configuration dropdown menu settings and Details panel settings.

### AJA Media Output Configuration Dropdown Settings

The settings described here are available in the Configuration dropdown menu accessible at the top of the AJA Media Output Details panel.

![AJA Media Output Configuration dropdown menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/126aa34b-d4e4-4051-9d71-c53ab192c07d/aja-output-dropdown.png "AJA Media Output Configuration dropdown menu")

| Setting | Description |
| --- | --- |
| **Output Type** | 
Latest - Displays the received sample as soon as possible. This does not use any of the time-based synchronization techniques and shows the latest available frame. PlatformTime - The displayed sample is synchronized based on the platform time. Timecode - Synchronize based on the timecode. Requires a timecode provider set either in the Media Profile or the Project settings.

Determines whether the Unreal Engine outputs only the fill image, or both the fill and key images. When you set this to **Fill Only**, only the fill image is output to the **Source** set below. When you set this to **Fill and Key**, the fill image is output to the **Source**, and the key is output to the **Key Source**.



 |
| **Device** | Sets the AJA device that this Media Source will send its video feed to. If you have multiple cards or devices attached to your computer, you can choose which one to use here |
| **Destination** | Sets the port or SDI connection on the specified **Device** this Media Source will send video to. |
| **Resolution** | 

You can select how an incoming interlaced stream should be processed. Options are:

-   None (default)
-   Blend Deinterlacer
-   Bob Deinterlacer
-   Discard Deinterlacer



 |
| **Standard** | Sets whether the output feed produced by this Media Output is progressive or interlaced. |
| **Frame Rate** | Sets the number of frames per second in the video feed produced by this Media Output. |
| **Key Source** | Sets the port that receives the key images from the Unreal Engine. Only available when the **Output Type** is set to **Fill and Key**. |
| **Reference** | 

Configures the source of the timing for the internal clock on the AJA card. The card uses this to determine when it should send each frame of video output.

-   **Free Run -** Uses the card's internal clock.
    
-   **External -** Synchronizes the card's internal clock with the genlock signal that arrives on its reference pin from an external source.
    
-   **Input -** Synchronizes with the video signal from the input port that you specify in the **Sync Source** setting below. 
    



 |

### AJA Media Output Details Panel Settings

The settings in the Details panel shown under **AJA** > **Configuration** are always greyed-out, as they are set through the Configuration dropdown menu. The values for these settings are shown as a reference. Depending on the specific Media Output asset, some of the reference fields might not apply.

The Media Source Details panel settings are shared for all capture cards, so some of the settings will be nonfunctional. Check carefully what settings are appropriate for your AJA capture card.

![AJA Media Output Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/94b2de5f-de23-418e-b2bf-9292775ad063/aja-output-details.png "AJA Media Output Details panel")

| Setting | Description |
| --- | --- |
| **AJA** |   |
| **Configuration** | Provides access to the **Configuration** dropdown. |
| **Media Configuration** | Shows a summary of the configuration settings selected in the **Configuration** dropdown. |
| **Media Configuration - Media Connection** |   |
| **Device** | Shows the AJA device that this Media Output will send its video feed to. Includes subfields for the **Device Name** and the **Device Identifier**. Read-only. |
| **Protocol** | Shows the communication protocol. Read-only. |
| **Transport Type** | Shows the transport type. Read-only. |
| **Quad Transport Type** | Shows the Quad transport type, when applicable. Read-only. |
| **Port Identifier** | Shows the port. Read-only. |
| **Media Configuration - Media Mode** |   |
| **Frame Rate** | Shows the number of frames per second in the video feed produced by this Media Output. Read-only. |
| **Resolution** | Shows the resolution of the video feed produced by this Media Output. Read-only. |
| **Standard** | Shows whether the output feed produced by this Media Output is progressive or interlaced. Read-only. |
| **Device Mode Identifier** | Shows the mode identifier for the AJA device. Read-only. |
| **Output Type** | Shows the output type. Read-only. |
| **Key Port Identifier** | Shows the physical port on the card where the engine outputs the Key signal. Read-only. |
| **Output Reference** | Shows the source of the timing for the internal clock on the AJA card. Read-only. |
| **Output Port Identifier** | Shows the physical port where the engine outputs the video signal. Read-only. |
| **Output** |   |
| **Output with Auto Circulating** | 
When enabled, the Unreal Engine buffers its output frames before sending them to the AJA card. This may improve the smoothness of the video signal, at the cost of some latency. Leave this option disabled to minimize latency, at the risk of seeing interruptions in the output signal.



 |
| **Timecode Format** | Determines whether Unreal Engine should embed timecode in the output feed, and which timecode format it should use. |
| **Pixel Format** | 

Determines the order of the color channels that make up each pixel, and the number of bits in each channel.

If you want to output the alpha, set the **Output Type** setting to **Fill and Key**, and use the **Key Source** to send the alpha to an output port on your AJA card.



 |
| **Output Audio** | Enable to send the engine’s audio alongside the video signal on the output. |
| **Audio Buffer Size** | The number of samples to buffer before sending them on the wire. |
| **Num Output Audio Channels** | Determines how many audio channels are output on the card. Must be greater than the number of audio channels used in the engine. |
| **Audio Sample Rate** | The number of audio samples per second sent on the wire. The value must match the engine’s audio sample rate. |
| **Output Audio on Audio Thread** | (Experimental - Only works in PingPong mode) If enabled, audio is sent to the capture card on the audio thread, rather than on the capture thread. |
| **Output - HDR** |   |
| **EOTF** | Determines the mathematical function the engine uses to convert the digital signal into brightness. |
| **Gamut** | Determines the range of colors the output can display. |
| **Output - Advanced** |   |
| **Output in 3GLevel B** | Enable to configure the card to convert your outgoing video signal into Level B, instead of using Level A. |
| **Invert Key Output** | When doing Key and Fill output, this controls whether or not to invert the values in the Key signal. Useful when the key receives video where the alpha is inversed, and you need to correct it before sending it out. |
| **Number of AJA Buffers** | 

Sets the number of buffers used to transfer each frame image from the main thread memory to the AJA card. Lower values are more likely to cause missed frames as it waits for each transfer to complete; larger numbers are more likely to increase latency.



 |
| **Interlaced Fields Timecode Need to Match** | When producing an interlaced video feed, this setting determines whether the timecode values for both fields in a single interlaced frame need to match. |
| **Output Interlace as Progressive** | When producing interlace output, enable this to send out interlace frames as if they were a progressive signal. (Experimental / Debugging) |
| **Use Multithreaded Scheduling** | Enable to write out the video frames in the capture card’s buffers on a different thread, which can help with performance when outputting at 4k / 8k. |
| **Number of Texture Buffers** | 

Sets the number of buffers used to transfer each frame image from the GPU to main thread memory. Lower values are more likely to cause a bottleneck on the GPU side as it waits for each transfer to complete; larger numbers are more likely to increase latency.



 |
| **Synchronization** |   |
| **Wait for Sync Event** | 

When this option is disabled, and you don't already have the Unreal Engine genlocked to an input signal, the engine runs at the fastest frame rate it can manage and provides all the frames it generates to the AJA card. Each time the card is ready to output a new frame, it selects one of the frames generated by the Engine.

When this option is enabled, the Unreal Engine does not generate any new frames of output until the AJA card is ready to accept the new frame. The effect is similar to genlock, but instead of locking the Unreal Engine's frame rate to an input signal, it locks the Engine's frame rate to the output timing of the AJA card.

This option is most useful when you don't already have an input signal that you can lock the Unreal Engine's frame rate to, but you want to ensure that the Engine is producing only one output frame for every frame in the output video feed.

Do not enable this option if you already have the Unreal Engine genlocked to an input feed using a custom time step.



 |
| **Debug** |   |
| **Log Drop Frame** | When enabled, Unreal Engine prints a message to its output log every time it detects a dropped frame in the input feed. |
| **Burn Frame Timecode** | When enabled, the engine embeds the timecode of each frame in the output signal. See [Timecode Texel Encoding](/documentation/en-us/unreal-engine/timecode-and-genlock-in-unreal-engine#timecodetexelencoding). |