# Pixel Streaming Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference)  
**Processed:** 2025-06-14 16:57:04

---

This page describes options, settings, and command-line parameters exposed by the various parts of the Pixel Streaming system.

Many of the settings and parameters below have changed or been removed in the new Pixel Streaming 2 plugin. Please refer to the [Pixel Streaming 2 Overview](/documentation/en-us/unreal-engine/pixel-streaming-2-overview-in-unreal-engine) document for more information.

## Supported Graphics Hardware

The computer that runs the Unreal Engine application with the Pixel Streaming plugin must have one of the following types of graphics hardware:

-   NVIDIA GPU hardware that supports Hardware-Accelerated Video Encoding (NVENC). See the [matrix of supported devices](https://developer.nvidia.com/nvidia-video-codec-sdk#NVENCFeatures) from NVIDIA.
    
-   AMD GPU hardware that supports the [Advanced Media Framework (AMF)](https://gpuopen.com/gaming-product/advanced-media-framework/).
    
-   Macintosh hardware that supports the use of the VideoToolbox framework.
    

If you receive the error message **No compatible GPU found, or failed to load their respective encoder libraries** when you try to use the Pixel Streaming Plugin, it is very likely that your GPU does not support NVENC or AMF.

## Supported Operating Systems

The Pixel Streaming Plugin supports Windows, Linux, and Mac platforms. OSX is not supported.

However, the Pixel Streaming Plugin and the accompanying Signalling and Web Server have only been tested on Windows 10, Ubuntu 18.04/20.04, and MacOS Ventura 13.5.1. They have not been tested on any other operating systems, including Windows 7 or 8.

## Supported Client Browsers

Pixel Streaming playback works on any modern browser that supports the WebRTC protocol. For example, it has been tested and is known to work in recent versions of the following browsers without additional configuration:

-   Google Chrome (desktop and mobile)
-   Microsoft Edge (desktop)
-   Mozilla Firefox (desktop and mobile)
-   Apple Safari (desktop and mobile)

Other browsers such as Microsoft Edge and Opera may require add-ons or plugins, and may not work on all systems.

## Supported Encoders

| Encoder | Acceleration | Encoding Speeds at 1080p/4K | Benefits | Quality at low bitrate | CPU/GPU usage per peer. |
| --- | --- | --- | --- | --- | --- |
| H.264 | GPU (NVIDIA, AMD, or Apple M series processor) | ~8.97ms/~24.17ms | Fast encoding/decoding speed. Widely supported across many devices at hardware level. | Blocky | One GPU encoding session per peer, up to the GPU's encoding session limit. |
| VP8 | CPU | ~10.5/~25ms | Produces a better image quality at a lower bitrate. | Average | CPU performance scales linearly with peers. |
| VP9 | CPU | ~15ms/~50ms | Has highest image quality at lowest bitrates, compared to other encoders. | Good | CPU performance scales linearly with peers. |
| AV1 | GPU (NVIDIA Ada Lovelace or newer) | ~8.98ms/~15.8ms | Has the highest image quality at the lowest bitrates, compared to other encoders. | Best | One GPU encoding session per peer, up to the GPU's encoding session limit. |

With a 1080p stream, as bitrate increases above 20mbps the quality of all encoders would be similar. The encoding speeds listed here are estimates and were taken on an RTX 3060 and an AMD 3900X, with exception for AV1 which was tested on an NVIDIA RTX 6000 Ada. We recommend using the AV1 codec if your encoding hardware supports it as it achieves higher quality video at lower bitrates.

## Default Network Ports

The components of the Pixel Streaming system communicate using the default ports specified below. You'll need to make sure that these ports are open on the host that runs each of these components.

| Component | Ports |
| --- | --- |
| `Signalling Server host` | 
-   **80** - for all HTTP requests coming from clients.  
    To change this value, set the **\--httpPort** parameter for the Signalling Server.
-   **443** - for all HTTPS requests coming from clients, when the Signalling Server is running in HTTPS mode.  
    To change this value, set the **\--httpsPort** parameter for the Signalling Server.
-   **8888** - for all incoming connection requests from the Unreal Engine application.  
    To change this value, set **both** the **\--streamerPort** parameter for the Signalling Server **and** the **\-PixelStreamingPort** parameter for the UE4 application.



 |
| `Matchmaker Server host` | 

-   **90** - for all HTTP requests coming from clients.  
    To change this value, use the **\--httpPort** parameter for the Matchmaker Server.
-   **9999** - for all messages sent by the Signalling Server.  
    To change this value, set **both** the **\--matchmakerPort** parameter for the Matchmaker Server **and** the **\--matchmakerPort** parameter for the Signalling Server.



 |
| `SFU Ports` | 

-   **8889**\- Opens connection between the Signalling Server and the SFU.



 |

## Pixel Streaming Console Commands and Launch Arguments

This section contains console commands and launch arguments that are useful for applications that use Pixel Streaming.

### Required Launch Arguments

The following launch arguments must be specified when launching an Unreal Engine application that uses Pixel Streaming:\\

| Command Line Argument | Description |
| --- | --- |
| `-PixelStreamingIP=<value>` or `<domain>` | Specifies the IP address or domain name of the computer running the Signalling and Web Server. |
| `-PixelStreamingPort=<value>` | Specifies the port that the Signalling and Web Server is listening on for incoming communications from the Unreal Engine application. The Signalling and Web Server uses the default value of `8888`. |
| `-PixelStreamingURL=<value>` | 
Only required if `-PixelStreamingIP` and `-PixelStreamingPort` are not present. If used replaces both `-PixelStreamingIP` and `-PixelStreamingPort.`

This must include the websocket protocol too. For example: `ws://127.0.0.1:8888` or `wss://127.0.0.1:8888`.



 |

A typical Pixel Streaming application launch is as follows:

```
`MyPixelStreamingApplication.exe -PixelStreamingIP=127.0.0.1 -PixelStreamingPort=8888`
Copy full snippet
```
MyPixelStreamingApplication.exe -PixelStreamingIP=127.0.0.1 -PixelStreamingPort=8888

Or:

```
`MyPixelStreamingApplication.exe -PixelStreamingURL="ws://127.0.0.1:8888"`
Copy full snippet
```
MyPixelStreamingApplication.exe -PixelStreamingURL="ws://127.0.0.1:8888"

### Unreal Engine Launch Arguments

The following arguments are not specific to Pixel Streaming. However, many Pixel Streaming applications may find them useful, particularly in cloud deployments.

| Command Line Argument | Description |
| --- | --- |
| `-RenderOffscreen` | 
Run the Unreal Engine application headless, without any visible rendering at all on the local computer. The application will not display any windows, and will not render in full screen. You can use this parameter in conjunction with -ForceRes to stop the Unreal Engine from automatically adjusting resolution based on the resolution of the primary display.

If you omit this parameter, the Unreal Engine application window will be rendered normally. If this application window is ever minimized, the Pixel Streaming video and input capture will stop working. We therefore recommend always including this parameter, unless you need to be able to see the rendered output from the Unreal Engine application locally on the same computer while it is running.



 |
| `-ForceRes` | When combined with -ResX and -ResY this will force the Unreal Engine to a specified resolution. This is useful in a cloud deployment where there typically is no display resolution. |
| `-ResX=<value>` | Sets the width component of the resolution that the Unreal Engine application should launch with. |
| `-ResY=<value>` | Sets the height component of the resolution that the Unreal Engine application should launch with. |
| `-AudioMixer` | 

Forces the Unreal Engine to use software mixing for audio, this may be required if an audio device is not present..



 |
| `-Unattended` | Suppresses the generation of dialog boxes in the event that an error is encountered. This is helpful when running Unreal Engine offscreen or in a container as messages boxes can hang indefinitely in those scenarios. |
| `-StdOut` and `-FullStdOutLogOutput` | The combination of these two flags produces the maximum logging output, which is useful when debugging or viewing live logs in an SSH terminal. |

## Optional Console Command Launch Arguments

You can specify the following settings at runtime as console variables or at launch as program arguments.

The system provides defaults for each setting that will be used when these settings are not specified. Most users will have no need to change these settings. In fact, many of these values are controlled by WebRTC internally and overriding them will likely result in worse performance.

### Pixel Streaming Plugin Configuration

Changing the following settings will configure the Pixel Streaming Plugin.

| Console Variable | Command Line Argument | Default Value | Description |
| --- | --- | --- | --- |
| `PixelStreaming.HUDStats` | `-PixelStreamingHudStats` | `false` | Whether to show PixelStreaming stats on the in-game HUD. |
| `PixelStreaming.DisableLatencyTester` | `-PixelStreamingDisableLatencyTester` | `false` | Disables the ability to trigger latency tests that pass through the Pixel Streaming Plugin pipeline. |
| `PixelStreaming.KeyFilter` | `-PixelStreamingKeyFilter=<values>` | `""` | A comma separated list of keys to ignore from streaming clients. For example, "W,A,S,D" might be used to filter out the default movement keys. |
| `PixelStreaming.UseMediaCapture` | `-PixelStreamingUseMediaCapture` | `false` | Use Media Capture from MediaIOFramework to capture frames rather than Pixel Streamings internal backbuffer sources. This can be preferred in some scenarios. |
| N/A | `-AllowPixelStreamingCommands` | `false` | Whether the user should be able to send console commands via the `emitConsoleCommand` javascript. |
| N/A | `-PixelStreamingHideCursor` | `false` | Whether to hide the UE application cursor. |

### Encoder Configuration

Changing the following settings will configure the underlying video encoders that the Pixel Streaming Plugin uses.

| Console Variable | Command Line Argument | Default Value | Description |
| --- | --- | --- | --- |
| `PixelStreaming.Encoder.Codec` | `-PixelStreamingEncoderCodec=<value>` | `H264` | Specified encoder used for Pixel Streaming. Supported encoders are: "H264, "AV1", "VP8", "VP9" |
| `PixelStreaming.Encoder.TargetBitrate` | `-PixelStreamingEncoderTargetBitrate=<value>` | `-1` | Target bitrate (bps). Setting this ignores the bitrate WebRTC wants (not recommended). Set to -1 to disable. |
| `PixelStreaming.Encoder.MaxBitrateVBR` | `-PixelStreamingEncoderMaxBitrate=<value>` | `20000000` | 
Max bitrate (bps).

Does not work in CBR rate control mode with NVENC.



 |
| `PixelStreaming.Encoder.DumpDebugFrames` | `-PixelStreamingDebugDumpFrame=<value>` | `false` | Dumps frames from the encoder to a file on disk for debugging purposes. |
| `PixelStreaming.Encoder.MinQuality` | `-PixelStreamingEncoderMinQuality=<value>` | `-1` | 0-100, higher values result in better quality but higher bitrate. |
| `PixelStreaming.Encoder.MaxQuality` | `-PixelStreamingEncoderMaxQuality=<value>` | `-1` | 0-100, higher values result in better quality but higher bitrate. |
| `PixelStreaming.Encoder.RateControl` | `-PixelStreamingEncoderRateControl=<value>` | `"CBR"` | PixelStreaming video encoder RateControl mode. Supported modes are "ConstQP", "VBR", "CBR". Note: CBR is the only one we recommend. |
| `PixelStreaming.Encoder.EnableFillerData` | `-PixelStreamingEnableFillerData=<value>` | `false` | Maintains constant bitrate by filling with junk data. Note: Not required with CBR and MinQP = -1. |
| `PixelStreaming.Encoder.Multipass` | `-PixelStreamingEncoderMultipass=<value>` | `"FULL"` | How many passes the encoder does per frame. See the NVENC docs for more details. Supported modes are `"DISABLED"`, `"QUARTER"`, `"FULL"` |
| `PixelStreaming.Encoder.MaxSessions` | `-PixelStreamingEncoderMaxSessions` | `-1` | Sets the maximum number of concurrent hardware encoder sessions for Pixel Streaming (-1 means impose no limit). |
| `PixelStreaming.Encoder.H264Profile` | `-PixelStreamingH264Profile=<value>` | `"BASELINE"` | 

H264 profile used by the encoder. Supported modes are `"AUTO"`, `"BASELINE"`, `"MAIN"`, `"HIGH"`, `"HIGH444"`, `STEREO`, `SVC_TEMPORAL_SCALABILITY`, `PROGRESSIVE_HIGH`, `CONSTRAINED_HIGH`.

Baseline is the only profile guaranteed to be supported by WebRTC capable devices on the receiving side.



 |

### WebRTC Configuration

Changing the following settings will configure the WebRTC library that the Pixel Streaming Plugin uses internally.

| Console Variable | Command line argument | Default | Description |
| --- | --- | --- | --- |
| `N/A` | `-LogCmds="LogPixelStreamingWebRTC <LogLevel>"` | `Log` | Specifies the log level of WebRTC. This is useful for debugging WebRTC. Helpful log levels are: Log, Verbose, VeryVerbose |
| `PixelStreaming.WebRTC.DegradationPreference` | `-PixelStreamingWebRTCDegradationPreference=<value>` | `"MAINTAIN_FRAMERATE"` | Degradation preference is WebRTC's strategy to destructively adapt the bitrate (changing resolution/dropping frames) when changing the encoder bitrate/QP is not sufficient. |
| `PixelStreaming.WebRTC.MaxFps` | `-PixelStreamingWebRTCMaxFps=<value>` | `60` | The maximum FPS WebRTC will try to capture/encode/transmit. |
| `PixelStreaming.WebRTC.StartBitrate` | `-PixelStreamingWebRTCStartBitrate=<value>` | `10000000` | 
Start bitrate (bps) that WebRTC will try to begin the stream with.

Value must be between Min and Max bitrates.



 |
| `PixelStreaming.WebRTC.MinBitrate` | `-PixelStreamingWebRTCMinBitrate=<value>` | `100000` | 

Minimum bitrate (bps) that WebRTC will not request below.

Be careful not to set this value too high, otherwise WebRTC will just drop frames.



 |
| `PixelStreaming.WebRTC.MaxBitrate` | `-PixelStreamingWebRTCMaxBitrate=<value>` | `100000000` | 

Maximum bitrate (bps) that WebRTC will not request above.

Be careful not to set this value too high, as a local (ideal) network will actually attempt to reach this value.



 |
| `PixelStreaming.WebRTC.DisableReceiveAudio` | `-PixelStreamingWebRTCDisableReceiveAudio` | `false` | 

Disables receiving audio from the browser into UE.

If audio is not required can improve latency in some cases.



 |
| `PixelStreaming.WebRTC.DisableTransmitAudio` | `-PixelStreamingWebRTCDisableTransmitAudio` | `false` | 

Disables transmission of UE audio to the browser.

If audio is not required can improve latency in some cases.



 |
| `PixelStreaming.WebRTC.DisableAudioSync` | `-PixelStreamingWebRTCDisableAudioSync` | `true` | 

Disables the synchronization of audio and video tracks in WebRTC.

This improves latency if synchronization is not required.



 |
| `PixelStreaming.WebRTC.MinPort` | `-PixelStreamingWebRTCMinPort` | `49152` | Sets the minimum usable media port for the WebRTC port allocator. |
| `PixelStreaming.WebRTC.MaxPort` | `-PixelStreamingWebRTCMaxPort` | `65535` | Sets the maximum usable media port for the WebRTC port allocator. |
| `PixelStreaming.WebRTC.PortAllocator.Flags` | `-PixelStreamingWebRTCPortAllocatorFlags` | `""` | Sets the WebRTC port allocator flags. Flags are specified as comma separated. Supported values are: DISABLE\_UDP, DISABLE\_STUN, DISABLE\_RELAY, DISABLE\_TCP, ENABLE\_IPV6, ENABLE\_SHARED\_SOCKET, ENABLE\_STUN\_RETRANSMIT\_ATTRIBUTE, DISABLE\_ADAPTER\_ENUMERATION, DISABLE\_DEFAULT\_LOCAL\_CANDIDATE, DISABLE\_UDP\_RELAY, ENABLE\_IPV6\_ON\_WIFI, ENABLE\_ANY\_ADDRESS\_PORTS, DISABLE\_LINK\_LOCAL\_NETWORKS |
| `PixelStreaming.WebRTC.DisableFrameDropper` | `-PixelStreamingWebRTCDisableFrameDropper` | `false` | Disables the WebRTC internal frame dropper which can be useful if frames are being dropped in cases like LAN streaming. |
| `PixelStreaming.WebRTC.VideoPacing.MaxDelay` | `-PixelStreamingWebRTCVideoPacingMaxDelay` | `-1.0` | Enables the WebRTC-Video-Pacing field trial and sets the max delay (ms) parameter (values below zero are discarded). |
| `PixelStreaming.WebRTC.VideoPacing.Factor` | `-PixelStreamingWebRTCVideoPacingFactor` | `-1.0` | Enables the WebRTC-Video-Pacing field trial and sets the video pacing factor parameter. Larger values are more lenient on larger bitrates. |
| `PixelStreaming.WebRTC.FieldTrials` | `-PixelStreamingWebRTCFieldTrials` | `""` | Sets the WebRTC field trials string. Format: "TRIAL1/VALUE1/TRIAL2/VALUE2/". |
| `PixelStreaming.DecoupleFramerate` | `-PixelStreamingDecoupleFramerate` | `""` | Enables Decoupled mode, allowing WebRTC and application FPS to stream at different rates. Pixel Streaming will try to stream at a fixed rate. If your application can not render at the target rate, it will send duplicate frames. |

## Signalling Server Configuration Parameters

There are two ways you can set these parameters:

-   On the command line, when you start the Signalling and Web Server by running `start_with_stun.bat`. In this case, prefix each parameter name with `--` (two dashes), then follow it with a space, then the value you want to set. For example: `--player_port 81`.
-   In a configuration file. By default, the Signalling and Web Server looks for a file named `config.json` in the same folder. In this case, set each parameter and the value you want to set for it as a key-value pair in the JSON object defined in the file. If you've already started the Signalling and Web Server at least once, see the parameters [here](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master/SignallingWebServer).

For a full list of arguments for the Signalling Server, see the relevant page on the Pixel Streaming Infrastructure [here](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master/SignallingWebServer).

## Matchmaker Server Command-Line Parameters

Provide these parameters on the command line when you start the Matchmaker Server by running its `run.bat` file, or when you start it by running `node.exe matchmaker.js`.

| Parameter | Description |
| --- | --- |
| `--httpPort <value>` | 
Sets the port number that the Matchmaker listens to for HTTP connections from clients.  
The default value is `90`.



 |
| `--matchmakerPort <value>` | 

Sets the port number that the Matchmaker listens to for incoming messages from Cirrus signalling servers.  
The default value is `9999`.



 |

## SFU Server Parameters

| Parameter | Description |
| --- | --- |
| `--PublicIP=<value>` | The public IP address that your SFU server will use. |