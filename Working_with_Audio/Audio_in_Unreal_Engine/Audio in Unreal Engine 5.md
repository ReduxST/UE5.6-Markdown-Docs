# Audio in Unreal Engine 5

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-in-unreal-engine-5](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-in-unreal-engine-5)  
**Processed:** 2025-06-14 16:08:47

---

The **Audio Mixer** is Unreal Engine's fully-featured, multi-platform audio renderer. This powerful audio engine was first launched in Fortnite and was later added to Unreal Engine 4.24.

Since its initial release, the Audio Mixer has continued to evolve its legacy feature set, and has added next-generation audio rendering features that provide unprecedented control and flexibility to audio designers working on real-time experiences.

This overview covers the current legacy feature set, as well as the next-generation features added to Unreal Engine 5 (UE5).

### Legacy Features

The core of the Unreal Engine legacy audio features are Sound Cues, Sound Classes, and Sound Mixes. These features are supported in the new Audio Mixer to facilitate the migration of projects to the new audio engine.

#### Sound Cues

Sound Cues are Unreal Engine's legacy audio objects. Sound Cues are audio parameter graphs from which audio designers can play sound sources and manipulate various parameters, such as volume and pitch.

Sound Cues are not capable of sample-accurate control and do not support the creation of arbitrary digital signal processing algorithms. The workflow is mostly manual, forcing audio designers to create separate Sound Cues for every sound.

Lastly, the inability to handle sample-accurate timing and scheduling of audio causes the creation of procedural sound to become more challenging.

#### Sound Classes and Sound Mixes

Sound Classes represent a set of static parameters corresponding to specific sounds.

These are used to categorize sounds and apply a consistent set of parameters to the project. Due to their static nature, audio designers will often end up creating many similar Sound Classes to cover all the different use cases needed for a large project. Debugging Sound Classes can also become complex due to inheritance inconsistencies between parameters within Sound Classes, where some take precedence over others.

Sound Mixes provide audio designers the ability to modulate a set of audio parameters dynamically at runtime. This is useful in creating dynamic sounds that react to gameplay events and other conditions. Sound Mixes can also become challenging to debug as audio designers can add complexity by creating multiple instances of the same Sound Mix and combining them with Sound Classes.

### Sound Rendering in UE5

Many of the features developed for Audio Mixer expand on the legacy features found in Unreal Engine and address the challenges mentioned above. Other features were newly developed to give Unreal Engine capabilities similar to other professional audio authoring tools.

#### MetaSounds

Unreal Engine 5 introduces **MetaSounds**, a new high-performance audio system that provides audio designers with complete control over Digital Signal Processing (DSP) graph generation for sound sources. MetaSounds have feature parity with Sound Cues and include next-generation features that empower designers to create immersive audio experiences.

MetaSounds address the issues present in Sound Cues and serve as a replacement for Unreal Engine's default audio objects. Unlike Sound Cues, MetaSounds are fundamentally a Digital Signal Processing (DSP) rendering graph. They provide audio designers the ability to construct arbitrarily-complex procedural audio systems that offer sample-accurate timing and control at the audio-buffer level.

In addition to runtime audio rendering capabilities, MetaSounds support improved workflows for audio designers, including: building MetaSounds through composition (MetaSounds within MetaSounds), templatization support, and dynamic and static asset instancing.

MetaSounds also provide significant performance improvements over Sound Cues and offer a fully extensible API that can be used by third-party plugins.

#### Audio Modulation

In Unreal Engine's legacy audio feature set, the Sound Class defines static global parameters and applies them to sounds in groups, and Sound Mixes adjust those parameters dynamically at runtime. These parameters are hardcoded and static which limit their use during gameplay.

**Audio Modulation** is the evolution of these legacy classes and it liberates the concept of parameter control and modulation to a generic "parameter bus". Anything can be a modulation source and anything can be a modulation destination.

The parameter buses can have any number of modulation sources, including Blueprint classes, modulation mixes, and gameplay code. Modulation destinations are parameters that are being modulated and can be locally mapped from the parameter bus in multiple ways.

Audio Modulation Parameter Buses provide audio designers the ability to define their own parameter groups (Sound Classes) and control them however they want (Sound Mixes).

#### Quartz

**Quartz** is a feature set that brings sample accurate timing of audio events to Blueprints. Quartz handles the complexity of scheduling audio to play at precise times and is designed to support custom interactive and procedural music systems. Quartz also sends precise timing events back to Blueprints to support synchronized gameplay logic and visuals with audio.

#### Audio Analysis

**Audio Analysis** is a set of technologies that offers non-real-time and real-time audio analysis. These tools work with Niagara and Blueprint scripting and will provide integration into Unreal Engine 5's editor for the creation of UX and debug analyzers, as well as runtime audio analysis to drive gameplay and graphics.