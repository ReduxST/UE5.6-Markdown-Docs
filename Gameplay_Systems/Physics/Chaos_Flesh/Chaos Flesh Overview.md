# Chaos Flesh Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-flesh-overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-flesh-overview)  
**Processed:** 2025-06-14 16:12:36

---

## Introducing the Chaos Flesh System

The **Chaos Flesh** system provides high-quality, real-time simulation of deformable (soft) bodies in Unreal Engine. Unlike rigid body simulation, the shape of soft bodies can change during simulation based on their properties.

The system supports the simulation of Static and Skeletal Meshes with various parameters - giving artists unprecedented control over the end result. We designed the system to primarily focus on the simulation of a character's muscle deformation during skeletal animation.

The Chaos Flesh system achieves high performance by simulating low-resolution geometry at runtime, along with cached results from an offline simulation of high-resolution cinematic-quality geometry.

## Simulating Soft Bodies in Real-Time

Artists can use the Chaos Flesh system to explore physically-based tetrahedral simulations within the Unreal Engine. The system creates real-time simulations of low-resolution geometry, along with cached results from high-resolution cinematic-quality geometry.

You can manage the Chaos Flesh through the **Dataflow** asset authoring system to generate deformation setups for the Chaos simulator. The Dataflow node-based editor provides controls for automatically generating tetrahedral geometry from closed Static and Skeletal Mesh surfaces, as well as tools to define internal simulation properties.

Simulations are managed through a connected **Solver Actor**. The standalone Actor allows for the simulation within the local space of a Skeletal Mesh, with the results visualized through a surface deformer on the Skeletal Mesh Actor. The Solver Actor exposes controls for the following:

-   Managing sub-stepping.
-   Threading models.
-   Global properties of the simulation.

### Technical Implementation

#### Tetrahedral Meshing tools

To begin simulating soft bodies, you must first convert an object's surface representation, such as a triangulated Static or Skeletal Mesh, into a volumetric representation of the same object. The Chaos Flesh system converts a Static or Skeletal Mesh into its equivalent tetrahedral geometry representation for use during simulations.

The Chaos Flesh system comes with the following methods for generating tetrahedral geometry from closed Skeletal and Static Mesh geometry:

-   The first method generates tetrahedral volumes by using iso-surface stuffing.
-   The second method generates tetrahedral volumes by using the **Tetrahedral Meshing in the Wild (TetWild)** algorithm.
-   The third method uses a custom algorithm to generate radial tetrahedral geometry.

#### Tetrahedral Simulation

The Chaos Flesh system uses its generated tetrahedral geometry to run a physically-based simulation in real-time.

The system uses kinematic constraints to bind the tetrahedral geometry to the Skeletal Mesh to match its animation. In addition, the system uses weak constraints to bind the tetrahedral geometry to the simulation vertices.

Using the system, you can set per-particle simulation properties, such as damping and mass values. In addition, the system comes with limited local space simulation support and provides uniform incompressibility and rest state adjustment settings.

#### World Solver Interactions

The Chaos Flesh simulations can interact with the environment in real-time. The system uses ray casts to detect environmental interactions against its tetrahedral (complex) geometry.

The system comes with Blueprint support which provides artistic control over one-way environmental collisions, as well as input animations that can drive constraint positions.

In addition, the system can detect convex and analytic collisions against rigid bodies in the world solver. This allows for more complex simulations as the soft bodies can collide with other simulating rigid bodies in real-time.

You can also configure the game tick order to set deformable simulations before or after the world solver.

#### Rendering Features

While the tetrahedral mesh is a good volumetric structure for simulation, it is usually not an ideal surface for rendering. Since the primary concern is making the rendering surface look good, the system transfers the simulation results onto an optimized surface for rendering.

The Chaos Flesh system also has the ability to visualize its tetrahedral geometry within the editor for debugging purposes. In addition, it comes with a Skeletal Mesh deformer visualization.

Nanite meshes are also supported via Nanite displacement map deformations on static geometry.

#### Caching the Simulation

Flesh simulations can be computationally expensive to run in realtime. For this reason, the Chaos Flesh System comes with the ability to cache its simulation results for smoother run-time playback.

You can use Sequencer to scrub the cached geometry results of any simulation, and render the simulation through **Get Take** and **Movie Render Queue (MRQ)**.

You can learn how to use the Chaos Flesh system by following the [Chaos Flesh](https://dev.epicgames.com/community/learning/tutorials/BEby/unreal-engine-chaos-flesh) tutorial on the Epic Developer Community.