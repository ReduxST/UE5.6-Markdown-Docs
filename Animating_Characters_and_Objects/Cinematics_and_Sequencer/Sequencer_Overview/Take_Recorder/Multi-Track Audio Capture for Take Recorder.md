# Multi-Track Audio Capture for Take Recorder

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-track-audio-capture-for-take-recorder-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-track-audio-capture-for-take-recorder-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:24

---

Multi-Track Audio Capture for Take Recorder **Take Recorder** provides options for recording audio. You can create multiple (up to 8) **Microphone Audio** sources in Take Recorder to record audio from multi-channel audio devices.

![Multi-track audio sources](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c46cb610-e878-4086-b378-bb902cd2ab7b/multi-track_audio_sources.png)

Each **Microphone Audio** source has an associated **Audio Input Device Channel** that designates the input channel on the selected audio device. Up to 8 channels are supported via the **Windows Audio Session API**. It is important to note that the audio device must have **Windows WDM multi-channel support** in order to have 8 channels available. There are third-party audio device manufacturers that offer Windows WDM multi-channel support.

See [Microphone Audio Recorder](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#microphoneaudiorecorder) and [Audio Input Device](/documentation/en-us/unreal-engine/take-recorder-in-unreal-engine#audioinputdevice) sections for more information about these audio settings.