# Audio Gameplay Volumes Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-gameplay-volumes-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-gameplay-volumes-overview)  
**Processed:** 2025-06-14 16:08:41

---

![Audio Gameplay Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/329e838e-a5ff-4c14-b9f6-f25ccff105d9/audio_gameplay_volume.png)

## Audio Gameplay Volumes

The **Audio Gameplay Volumes** system is the next-generation approach to area-based sound processing, which allows sound designers to define physical regions that apply effects to sounds, relative to the listener's position.

For example, you can add reverb while the listener is inside a specific room to simulate sound waves bouncing within the space, or apply a low pass filter to sounds outside of a room to simulate the wall's muffling effect.

The legacy [Audio Volume](/documentation/en-us/unreal-engine/audio-volumes-in-unreal-engine) system can present challenges to audio designers, as each Audio Volume's functionality is fixed at runtime and cannot be extended without modifying engine code. Furthermore, all of the possible settings are provided on each Audio Volume and that can be cumbersome when often only a subset of the options available are needed. This system can also present a workflow challenge as each Audio Volume requires a separate **Actor** in the **Level**, which makes the system harder to integrate.

Designed as a replacement for the legacy system, this new approach leverages a plugin and component-based architecture to address many of the challenges of the legacy approach, while providing more flexibility to developers.

### Extensible

![Plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/52e58bcf-3754-41f1-8730-4f21f2f00f0c/plugin.png)

You can enable or disable the Audio Gameplay Volume plugin based on your project needs. Additionally, you can use the provided C++ API or the **Blueprint Interaction Interface** to extend functionality with new effects, positional player interactions, and more.

### Component-Based Architecture

![Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/504ac00c-3a0a-40cb-a2da-ea626f8cca9d/components.png)

Audio Gameplay Volumes are designed using a modular component approach. Each component contains a configurable behavior you can add to a Volume individually, or in combination with others, so you can create custom functionality for when a listener enters or exits the volume.

These components provide parity to the functionality found in the legacy Audio Volumes system, but with greater control as each feature set is its own component.

The behavior component types are:

-   **Attenuation**: Interpolates the audio's current volume (loudness) to a target volume (loudness). You can configure the effect to apply to sounds inside of the volume while the listener is outside, or the other way around.
-   **Filter**: Applies a low pass filter to the audio. You can configure the effect to apply to sounds inside of the volume while the listener is outside, or the other way around.
-   **Reverb**: Adds a reverb effect to the audio. When the listener enters the volume, this effect applies to all sounds regardless of whether they are inside or outside of the volume.
-   **Submix Override**: Adds a **Submix Effect Chain** to a **Sound Submix**. When the listener enters the volume, this effect applies to all sounds regardless of whether they are inside or outside of the volume.
-   **Submix Send**: Sends the audio to a **Sound Submix**. This effect applies to sounds inside of the volume, and can be configured to apply while the listener is either outside or inside.

Each component comes with a Priority value which determines which component is used in cases where the listener is inside multiple volumes that have a valid component of the same type.

### Improved Integration

![Place Volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1201b47-4233-4314-9e1f-582b46e8f16e/place_volume.png)

Audio Gameplay Volumes offer deep integration with Blueprints to give audio designers flexibility in how they want to implement the system. You can place volumes directly in a Level as stand-alone Actors, or add them as components to any Actor Blueprint.

You can implement custom collision checks within Blueprint Actors to simulate when a listener enters or exits the volume. In this way, manual location or transformation adjustments within the Level are unnecessary.

### Improved Workflow

In many projects, audio implementation tends to happen toward the end of the production cycle. This can make it challenging to implement a robust audio system that works seamlessly with other gameplay features. The Audio Gameplay Volume system takes this into consideration by providing the ability to attach Volume components to any Actor in a Level.

Furthermore, the user interface was streamlined to make it more intuitive for audio designers.

### Improved Performance

Volume processing and collision tests were moved out of the game thread and into the audio thread. This results in significant improvements to performance and allows you to extend the system without worrying about thread safety.

### Proxy Functionality

![Proxy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f504135a-dfe8-42f1-9105-4dde7872492a/proxy.png)

In addition to replacing and enhancing the legacy features, the Audio Gameplay Volume system offers new **Proxy** functionality. With Proxies, system functionality can be leveraged without a traditional Audio Gameplay Volume object.

There are two types of Proxies:

-   **Primitive**: Allows any static mesh to be used as a Volume with its own Enter and Exit events.
-   **Condition**: Allows functionality use when a particular condition is met without the need for a physical Volume.