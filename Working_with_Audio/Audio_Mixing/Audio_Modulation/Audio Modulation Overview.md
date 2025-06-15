# Audio Modulation Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-modulation-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-modulation-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:08:55

---

The **Audio Modulation** plugin provides dynamic control over floating-point audio parameters, such as volume and pitch, from the **Component** and **Blueprint** systems.

The Audio Modulation plugin is disabled by default. To enable it, follow these steps:

1.  Select **Edit > Plugins** to open the **Plugin** panel.
2.  Use the search bar to find the plugin.
3.  Enable the corresponding checkbox.
4.  Restart the Unreal Editor.

## Purpose

The Audio Modulation plugin provides:

-   A generic and flexible audio mixing system.
-   A set of auditioning and debugging tools.
-   Extensible Blueprint and C++ APIs.

## How It Works

Audio Modulation's workflow is similar to physically connecting a patch cable in hardware modulation. Conceptually, a modulation signal is carried via a connector from a source to a destination.

With Audio Modulation, those physical concepts apply to audio assets and components in Unreal Engine:

-   Connectors
    -   Control Buses
    -   Parameter Patches
    -   Modulation Generators
-   Sources (Modulators)
    -   Control Bus Mixes
    -   Parameter Patches
    -   Modulation Generators
-   Destinations (Modulation Destinations)
    -   Sound Waves
    -   MetaSound Sources
    -   Audio Components
    -   Synth Components
    -   Sound Classes
    -   Submixes
    -   Source Effects (BitCrusher and Chorus only)

Technically, the destination audio objects are not Modulation Destinations themselves; rather they **have** Modulation Destinations.

Once a connector links a modulator to a destination, the system works automatically and reacts in real time. Specifically, when a destination object instantiates, the destination object activates all of its connectors and modulators.

You can activate your connectors and modulators manually by instantiating them in Blueprint. Manual lifetime management may require more diligence, but it can be helpful when you want information passed through your modulation pipeline, regardless of any active Modulation Destinations.

For detailed information on Audio Modulation asset types, Blueprint API, and more, see the [Audio Modulation Reference Guide](/documentation/en-us/unreal-engine/audio-modulation-reference-guide-in-unreal-engine).

## Examples

See the following pages for implementation-specific details:

-   [Audio Modulation Quick Start Guide](/documentation/en-us/unreal-engine/audio-modulation-quick-start-guide) - A quick guide on getting started with Audio Modulation.
-   [Lyra Sample Game](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine) - A sample game project that features Audio Modulation.