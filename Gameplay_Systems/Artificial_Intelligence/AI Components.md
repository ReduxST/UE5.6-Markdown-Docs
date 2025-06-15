# AI Components

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-components-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-components-in-unreal-engine)  
**Processed:** 2025-06-14 16:05:15

---

AI Components are a type of component that enable Pawns receive sensory like data from the environment, such as where noises are coming from or if the Pawn can see something.

## AI Perception Component

The **AIPerceptionComponent** is used to register as stimuli listener in the **AIPerceptionSystem** and gathers registered stimuli. **UpdatePerception** is called when component gets new stimuli (batched).

## Pawn Noise Emitter Component

A **PawnNoiseEmitterComponent** tracks noise event data used by **SensingComponents** to hear a Pawn. This component is intended to exist on either a Pawn or its Controller. It does nothing on network clients.

## Pawn Sensing Component

The Pawn SensingComponent encapsulates sensory (i.e. sight and hearing) settings and functionality for an Actor, allowing the Actor to see/hear Pawns in the world. It does nothing on network clients.