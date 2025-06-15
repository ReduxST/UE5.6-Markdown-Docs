# Audio Glossary

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-glossary-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-glossary-in-unreal-engine)  
**Processed:** 2025-06-14 16:08:44

---

Adaptive differential pulse-code modulation (ADPCM)

An audio codec that converts analog signals into digital information by quantizing the differences between the actual analog signal and a predicted signal.

Air Absorption

As sound travels through the air, high frequencies are absorbed more than lower frequencies. The amount of this absorption can vary with temperature and humidity. In UE, Air Absorption can be modeled under a sound's Attenuation settings to create a more realistic decay as a Listener moves away from a Source.

Ambient Sound Actor

An actor that can be placed directly into the Level Editor and contains an Audio Component.

Ambisonics

A spherical audio format that involves placing an array of coincident soundfield or ambisonic microphones during the recording process. Raw ambisonic recordings, also known as B-format, must be decoded to be used. UE supports FuMA and Ambix first-order ambisonic formats.

Amplitude

The relative strength of sound waves (transmitted vibrations) that is perceived as loudness or volume. Amplitude is measured in decibels (dB), which refers to the sound pressure level or intensity.

Attack Time

Refers to how quickly an effect or process is applied to a signal. This is often represented in milliseconds (ms).

Attenuation

A decrease in the volume and quality of a sound. In UE, Sound Attenuation can be set on any sound and includes options for Distance Attenuation, Air Absorption, Spatialization, Reverb, Occlusion, Focus, Priority, and Submix Sends.

Audio Bus

An asset type that operates similarly to a patch cable by providing a signal path that combines individual audio signals into a single asset. Audio Buses function similarly to Sound Submixes but do not have a graph, are not audible by default, and cannot have digital signal processing (DSP) effects applied to them directly.

Audio Component

Attaches to an Actor to provide a sound source.

Audio Gameplay Volume

An extensible, modular component approach for area-based sound processing. This system is intended to replace Audio Volumes.

Audio Gameplay Volume Proxy

A component type used to interact with the Audio Gameplay Volume system without a traditional Audio Gameplay Volume object.

Audio Mixer

The Audio Mixer is the multi-platform audio renderer in UE.

Audio Modulation

An audio engine system for controlling audio parameters from Blueprint and Component Systems. This system is intended to replace Sound Class Mixes.

Audio Synesthesia

A plugin that exposes automatically extracted audio metadata for gameplay scripting with Blueprint. This feature can be used to drive animations, effects, and other elements tightly coupled to sounds.

Audio Volume

A Volume actor that can be placed in the level Editor to control effects on sound objects inside and outside of a spatialized area. This system is intended to be replaced by Audio Gameplay Volumes.

AudioLink (API)

An API that connects Unreal Audio Engine to external software, such as other audio engines.

Band Pass Filter (BPF)

A filter that passes frequencies within a given range and attenuates frequencies outside of that range.

Binaural Audio

Audio that has been recorded in such a way as to consider the position of a person's ears and shoulders or has been synthesized using HRTFs (Head Related Transfer Functions). It is intended to be more realistic but requires headphones for accurate playback.

Bink Audio

A performance-oriented audio codec that is capable of perceptually lossless 10:1 compression with decode speeds closer to ADPCM than MP3 or Vorbis.

Bit Crusher

An audio effect that produces distortion by reducing the resolution or bandwidth of digital audio data.

Bit Depth

The number of bits per sample in a digital signal. Audio files with higher bit depths will have a higher resolution. The audio engine supports importing 16-bit files on all editor platforms, and supports 24-bit files on Windows.

Bit Rate

The amount of bits a digital audio file contains per second. It's most commonly used to convey the quality of compressed audio formats, such as MP3. For example, a 320 Kbps bit rate recording is processed at 320,000 bits per second.

Codec

A device or computer program that encodes or decodes a data stream or signal. The term codec is a portmanteau of coder/decoder.

Compression Format

Any digital audio format that reduces the amount of data from the recorded signal. Compression formats may be lossy or lossless.

Compressor

Reduces the overall dynamic range of a piece of audio by detecting when it exceeds a specified threshold and then attenuating it by a specified amount (the ratio).

Control Bus

A modulation source that can be added to an audio source or effect. Assets sent to the same Control Bus can be modulated as a group by using a Control Bus Mix.

Control Bus Mix

An array of mix stages used to drive values utilized by Control Buses.

Convolution Reverb

A type of reverberation effect that uses digital recordings of physical spaces or other reverb effects, known as impulse responses, to recreate the reverb.

Delay

An audio signal processing technique that records an input signal to a storage medium and then plays it back after a set period of time.

Digital Signal Processing (DSP)

Any computation manipulation applied to a digital signal, such as audio or video signals. DSP is often applied to audio analysis or to create audio effects, such as delay or reverb.

Dry Level

The volume of the unprocessed audio before any effects or processing

Envelope Follower

Follows the amplitude shape of the incoming signal and sends out a control value based on that shape.

Equalization (EQ)

The process of adjusting the volume of different frequency bands within an audio signal.

Filter

Audio filters are designed to amplify or attenuate a specific range of frequencies. Filters can be used for noise reduction, color, or effect. Low-pass, high-pass, and band-pass are common types of filters.

Foley

The art of performing sound effects to match movement in a film or interactive experience. Footsteps and cloth movement sounds are common examples of foley.

Frequency

The rate at which a vibration occurs that constitutes a wave, either in a material (as in sound waves) or in an electromagnetic field (as in radio waves and light). Frequency is measured in Hertz (Hz). An audio frequency or audible frequency is a periodic vibration whose frequency is in the band audible to the average human (20-20,000Hz). It is the property of sound that most determines pitch.

Gain

The amount of amplification applied to a signal by any process that increases its strength. Gain can be measured linearly or in decibels (dB).

High-Pass Filter (HPF)

Passes Frequencies above a given Cutoff Frequency to pass through while attenuating frequencies below it.

Limiter

A type of compressor with a very high ratio. A limiter is often used to control spikes in loudness in an audio signal and prevent unwanted distortion.

Listener

A microphone-like decisive that "hears" sound from a particular point. In UE, this is on the Camera by default.

Low-Pass Filter (LPF)

Passes Frequencies below a given Cutoff Frequency to pass through,while attenuating frequencies above it.

MetaSound

A high-performance audio system that provides audio designers with complete control over a digital signal processing (DSP) graph for the generation of sound sources.

Modulation Destination

Any endpoint that provides a modifiable float value to an audio source or effect.

Modulation Parameter

A modulation parameter provides context for how a value associated with a Control Bus is displayed, mixed, and transformed to and from unit and normalized (unitless) \[0.0, 1.0\] values. For example, the Volume Default Modulation Parameter has a default value of 1.0f in normalized space (0 dB in unit space), and when mixed multiplicatively, this leads to no change in the output.

Modulation Source

Any source that modulates a parameter.

Non-Spatialized Audio

Sound that is not panned in respect to the listener's position. Music, UI sounds, and narration are often non-spatialized.

Ogg Vorbis

An open-source audio compression format developed as a replacement for proprietary digital audio encoding formats, such as MP3, VQF, and AAC.

One-shot

A non-looping sound.

Panning

The processes in which a sound source is positioned in a stereo or surround field.

Phase

Audio waveforms are cyclical; that is, they proceed through regular cycles or repetitions. Phase is defined as how far along its cycle a given waveform is. The phase measurement is given in degrees, with 360 degrees being one complete cycle.

Pulse-code modulation (PCM)

An audio codec that converts analog signals into digital information by sampling and quantizing an analog signal.

Quartz

An audio engine system for sample-accurate scheduling of audio events.

Release Time

Refers to how quickly a signal returns to an unprocessed state after an effect or process has been applied to a signal.

Reverberation (Reverb)

The persistence of a sound after the sound is produced. Reverb is created when a sound is reflected off of a surface causing reflections to build up and they decay as the reflections are absorbed by the surfaces of the objects around it. Reverb is often characterized as "echo"; however, the effect can be much more subtle. Reverb provides acoustic information about the size and shape of a space we're in. The Unreal Engine has a Reverb Effect asset type, a simple Reverb Submix Effect, and a Convolution Reverb effect.

Sample Rate

The number of samples per second taken from a continuous signal to make a discrete or digital signal.

Semitone

The smallest interval used in classical Western music, which is equal to a twelfth of an octave or half a tone.

Sound Class

An organizational asset type for grouping multiple sounds together. Sound Classes contain some routing options required for sending sounds to the Master Reverb Submix.

Sound Class Mix

An asset type that a user can use to group multiple sounds together and then alter the parameters of all relevant Sound Waves at once. This is intended to be replaced by the Audio Modulation system.

Sound Concurrency

Defines the limits of how many sounds a given group can play simultaneously and what to do when that limit is reached. The primary cost for an audio engine is decoding and rendering sound sources, so one of the primary tools for reducing CPU cost is limiting the number of sounds that can play simultaneously.

Sound Occlusion

Simulates the effect of sound reduction in high-frequency content or amplitude due to object interference between a source and a listener. An example is hearing a person talking in the room next to the one you're in. In UE, occlusion can be set in the Sound Attenuation settings.

Sound Submix

A digital signal processing (DSP) graph used to mix audio generated from individual sounds into a single output buffer and efficiently apply effects to multiple sound sources simultaneously.

Sound Wave

A fundamental audio asset that is created upon importing an audio file into the editor. Sound Waves can be added to Audio Components, MetaSound Graphs, and Sound Cues.

Soundscape

A system that procedurally generates ambient sounds as the player moves around a level.

Source

The origin of a sound.

Source Bus

Mixes together multiple Sources into a single audio buffer, which can be used as a Source within the Level. Source buses function similarly to an aux bus in a mixer.

Source Effect

A digital signal processing (DSP) effect, such as flanger or delay, which can be added to a Source Effect Preset Chain to define a sequence of per-source effects. Source effects function similarly to an insert effect on a mixing console.

Spatialization

The simulation of location-based sound phenomena such as orientation, attenuation, propagation, obstruction, and reverb.

Stinger

A short musical phrase that's played on top of the music to signal a game event to the player. Stingers are often played when a goal is reached, a player dies, or treasure is found.

Voice

An active sound source. The maximum number of concurrent voices can be managed in the Project Settings.

WaveTables

WaveTables store periodic wave data in lookup tables and provide a way to perform wavetable synthesis and sampling in MetaSounds.

Wet Level

The volume of the processed audio after any effects or processing.