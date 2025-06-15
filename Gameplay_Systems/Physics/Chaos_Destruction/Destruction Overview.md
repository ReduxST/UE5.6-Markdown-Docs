# Destruction Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/destruction-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/destruction-overview)  
**Processed:** 2025-06-14 16:20:00

---

![alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f642f6c4-3984-49a5-ae00-c0886f62e54c/city-chaos-destruction-small.gif)

The **Chaos Destruction** system is a collection of tools that can be used to achieve cinematic-quality levels of destruction in real time. In addition to great-looking visuals, the system is optimized for performance, and grants artists and designers more control over content creation and the fracturing process by using an intuitive nonlinear workflow.

The system allows artists to define exactly how geometry will break during the simulation. Artists construct the simulation assets using pre-fractured geometry and utilize dynamically-generated rigid constraints to model the structural connections during the simulation. The resulting objects within the simulation can separate from connected structures based on interactions with environmental elements, like [Physics Field](/documentation/en-us/unreal-engine/physics-fields-in-unreal-engine) and collisions.

The destruction system relies on an internal clustering model which controls how the rigidly attached geometry is simulated. Clustering allows artists to initialize sets of geometry as a single rigid body, then dynamically break the objects during the simulation. At its core, the clustering system will simply join the mass and inertia of each connected element into one larger single rigid body.

The destruction system uses on a new type of asset called a **Geometry Collection** as the base container for its geometry and simulation properties. A Geometry Collection can be created from static and skeletal mesh sources, and then fractured and clustered using UE5's **Fracture Mode**.

At the beginning of the simulation a connection graph is initialized based on each fractured rigid body's nearest neighbors. Each connection between the bodies represents a rigid constraint within the cluster and is given initial strain values. During the simulation, the strains within the connection graph are evaluated. These connections can be broken when collision constraints or field evaluations apply an impulse on the rigid body that exceeds the connections limit. Physics Fields can also be used to decrease the internal strain values of the connections, resulting in a weakening of the internal structure.

For large-scale destruction simulations, Chaos Destruction comes with a new **Cache System** that allows for smooth replay of complex destruction at runtime with minimal impact on performance.

Chaos Destruction easily integrates with other Unreal Engine systems, such as [Niagara](/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine) and [Audio Mixer](/documentation/en-us/unreal-engine/audio-engine-overview-in-unreal-engine), to spawn particles or play specific sounds during the simulation.