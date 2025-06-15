# Unreal Engine’s Systems and Workflows Overview for Unity Developers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engines-systems-and-workflows-overview-for-unity-developers](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engines-systems-and-workflows-overview-for-unity-developers)  
**Processed:** 2025-06-14 16:57:14

---

## Introduction

This page provides a high-level overview of Unreal Engine's major systems and workflows, and how they compare to Unity's commonly-used editors, tools, and asset types. This document is designed to help Unity developers understand how to accomplish familiar workflows in Unreal Engine. You can find out more about each feature by following the links in each section.

This page references tools and features based on versions **Unreal Engine 5.5.4** and **Unity 6 (6000.0.30f1)**. Feature references might be different in other versions of either engine.

## Gameplay

### Physics

[![](https://dev.epicgames.com/community/api/documentation/image/826652a3-7cb1-42e7-8c45-229eff90c49b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/826652a3-7cb1-42e7-8c45-229eff90c49b?resizing_type=fit)

For a more detailed overview of the features that come with Chaos Physics, see the [Physics](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/ModelingComponents/Physics) documentation.

#### Physics Engine

Unreal Engine comes with **Chaos Physics**, a light-weight physics simulation solution built from the ground up to meet the needs of next-generation games. Chaos Physics comes with many features such as destruction, networked physics, rigid body physics, vehicles, and more.

Unity’s default physics engine for 3D games is NVIDIA PhysX, which comes with many similar features to Chaos Physics.

#### Chaos Destruction

The **Chaos Destruction** system is a collection of tools within Unreal Engine that can be used to achieve cinematic-quality levels of destruction in real time. In addition to great-looking visuals, the system is optimized for performance, and provides more control for artists and designers over content creation.

The Chaos Destruction system utilizes **Geometry Collections**, a type of asset built from one or more Static Meshes, including those nested in Blueprints. These Geometry Collections can be fractured to achieve real-time destruction.

The system provides unprecedented control over the fracturing process by using an intuitive non-linear workflow. The user can create multiple levels of fracturing, as well as selective fracturing on parts of the Geometry Collection, for greater artistic control. Users can also define the Damage Thresholds per cluster that will trigger a fracture.

You can learn more about Chaos Destruction by reading the [Chaos Destruction](https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-destruction-in-unreal-engine) documentation.

#### Networked Physics

Networking, or replication in games, refers to the ability to communicate gameplay information between multiple machines over an internet connection. Unreal Engine features a robust networking framework that helps developers streamline the creation of multiplayer games.

**Networked physics** is part of the networking framework and enables physics-driven simulations to work in a multiplayer environment. In Unreal Engine, physics replication refers to Actors with replicated movement that simulate physics. These simulations run inside the local client (player’s machine) during gameplay.

You can learn more about Chaos Destruction by reading the [Networked Physics](https://dev.epicgames.com/documentation/en-us/unreal-engine/networked-physics) documentation.

#### Rigid Body Dynamics

Chaos Physics provides many features for **rigid-body dynamics**. This includes collision responses, tracing, physics constraints, and damping and friction. 

##### Collision

In Unreal Engine, collision is built into most actor components that use the physics engine. The collision settings for an actor can be modified by going to the Collision section in the Details panel. For instance, you can enable Simulation Generates Hit Events to allow the object to fire Hit events that you can access through blueprints or code to detect collisions. This is similar to handling collision in Unity by using OnCollisionEnter in C# or Visual Scripting. 

For more information on setting up collisions for your actors, see the [Collision](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Plugins/GameplayCameras/Nodes/Collision) documentation.

##### Traces with Raycasts

The Chaos Physics system comes with a variety of **tracing methods**. Traces offer a method of gathering external information to an actor. This information can then be used at runtime to react to changing gameplay conditions.

There are different options available when running a trace. You can use different trace types such as **line**, **sphere**, **box**, or **capsule** traces. You can also trace for single or multiple hits, and even trace for specific object types or collision channels.

The tracing system in Unreal is similar to Unity’s raycasting system.

For more information on tracing, see the [Traces with Raycasts](https://dev.epicgames.com/documentation/en-us/unreal-engine/traces-with-raycasts-in-unreal-engine) documentation.

#### Chaos Cloth

**Chaos Cloth** provides accurate and performant cloth simulation for games and real-time experiences. The system comes with extensive user controls, along with physical reactions such as wind, to achieve a specific artistic vision. In addition, Chaos Cloth also comes with a powerful Animation Drive system, which deforms a cloth mesh to match its parent’s animated Skeletal Mesh.

Chaos Cloth also provides machine learning cloth simulation. This system results in higher fidelity simulation compared to a traditional physics-based model by using a trained dataset that can be used in real-time to produce results that were previously only achievable with offline simulation.

For more information on Chaos Cloth, see the [Chaos Cloth](https://dev.epicgames.com/documentation/en-us/unreal-engine/cloth-simulation-in-unreal-engine) documentation.

#### Chaos Vehicles

**Chaos Vehicles** is Unreal Engine’s lightweight system for performing vehicle physics simulations. This system provides more flexibility to the user by simulating any number of wheels per vehicle. You can also configure any number of forward and reverse gears as well for added customization.

Chaos Vehicles can be configured for complex vehicle simulations. You can add any number of aerofoil surfaces that provide downforce or uplift at specific locations in the chassis. These can simulate vehicle spoilers, or even aircraft wings or rudders. Each of these control surfaces can be manipulated via roll, pitch, and yaw.

For more information on Chaos Vehicles, see the [Chaos Vehicles](https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-vehicles) documentation.

#### Fluid simulations

Unreal Engine includes a set of built-in tools for simulating 2D and 3D fluid effects in real time. These systems use physically-based simulation methods to produce realistic effects for things such as fire, smoke, clouds, rivers, splashes, and waves breaking on a beach.

The toolset is designed as an open platform for experimentation by utilizing simulation stages, reusable modules, and robust data interfaces.

For more information on fluid simulations, see the  [Fluid Simulation](https://dev.epicgames.com/documentation/en-us/unreal-engine/fluid-simulation-in-unreal-engine)  documentation.

### Artificial Intelligence

[![](https://dev.epicgames.com/community/api/documentation/image/768288d4-16e5-496e-a8cb-c7419f25309e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/768288d4-16e5-496e-a8cb-c7419f25309e?resizing_type=fit)

Unreal Engines comes with a variety of systems to create and manage AI Agents (NPCs) during gameplay.

#### Simulating AI Agents at Scale

**MassEntity** is a gameplay-focused framework designed for high performance, data-oriented simulations. MassEntity can be used for efficient management and rendering of large numbers of entities on-screen.

For more information on this, see the [MassEntity](https://dev.epicgames.com/documentation/en-us/unreal-engine/mass-entity-in-unreal-engine) documentation.

#### Simulating AI Agent Behavior

Unreal Engine comes with AI Agent functionality in the following categories: Perception and stimuli, decision-making, world navigation, and environment interactions. Each category has one or more systems that help you achieve your desired results.

##### Perception and Stimuli

In the area of **perception and stimuli**, Unreal Engine comes with the [Pawn Sensing](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/AI/Components/PawnSensing), [Pawn Noise Emitter](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/Audio/Components/PawnNoiseEmitter), and AI Perception [AI Components](https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-components-in-unreal-engine).

**AI Perception** can be used to define and handle what senses an AI Agent has access to. The AI Perception Component is a type of component that can be added to a pawn's AIController Blueprint from the components window and is used to define what senses to listen for, the parameters for those senses, and how to respond when a sense has been detected.

You can also use several different functions to get information about what was sensed, what Actors were sensed, or even toggle a particular type of sense.

For more information on this, see the [AI Perception](https://dev.epicgames.com/documentation/en-us/unreal-engine/ai-perception-in-unreal-engine) documentation.

##### Decision-Making

In the area of **decision-making**, Unreal Engine comes with Behavior Trees and State Trees. These assets hold the logic that AI Agents use to make decisions during gameplay.

**Behavior Tree assets** contain a decision graph with a variety of nodes containing logic the AI Agent can execute. The tree begins at the root and executes certain nodes based on data stored in a **[Blackboard asset](https://dev.epicgames.com/documentation/en-us/unreal-engine/API/Runtime/AIModule/BehaviorTree/Blackboard)** or other data coming from the Agent itself. Behavior trees offer an intuitive way to visualize how AI Agents make decisions and can be configured to be reusable and flexible.

For more information on this, see the [Behavior Trees](https://dev.epicgames.com/documentation/en-us/unreal-engine/behavior-trees-in-unreal-engine) documentation.

**StateTree** is a general-purpose hierarchical state machine that combines the Selectors from behavior trees with States and Transitions from state machines. StateTree can be used to create highly performant logic that stays flexible and organized.

For more information on this, see the [State Tree](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/StateTree) documentation.

##### World Navigation

In the area of **world navigation**, Unreal Engine comes with a fully-featured navigation system for AI Agents.

The **Navigation System** provides efficient pathfinding capabilities to AI Agents in your project. You can create a **Navigation Mesh Actor** in your level to build and map out the navigation for your Agents. You can also use [Navigation Mesh Modifiers](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-how-to-modify-the-navigation-mesh-in-unreal-engine) and [Custom Navigation Areas](https://dev.epicgames.com/documentation/en-us/unreal-engine/custom-navigation-areas-and-query-filters-in-unreal-engine) to affect the cost of traversing certain areas - actively influencing how the AI Agents choose their optimal navigation path to their target. 

In addition, the system comes with two [avoidance systems](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-avoidance-with-the-navigation-system-in-unreal-engine) - Reciprocal Velocity Obstacles and Detour Crowd Manager to help AI Agents avoid dynamic elements in their environment and each other.

For more information on this, see the [Navigation System](https://dev.epicgames.com/documentation/en-us/unreal-engine/navigation-system-in-unreal-engine) documentation.

##### Environment Interactions

In the area of **environment interactions**, Unreal Engine comes with Smart Objects.

**Smart Objects** are objects placed in a level that AI Agents and Players can interact with. These objects contain all the information needed for those interactions. Smart Objects are part of a global database and use a spatial partitioning structure. This means that they can be queried at runtime by using filters such as search area around the Agent and Gameplay Tags.

For more information on this, see the [Smart Object](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/SmartObject) documentation.

#### Machine Learning

To craft more complex AI solutions where AI agents can learn and adapt, Unreal Engine offers the Learning Agents plugin which can be used to train AI agents by using algorithms like Reinforcement Learning. This is the Unreal Engine equivalent of Unity’s MLAgents package.

For more information on this, see the [Learning Agents](https://dev.epicgames.com/documentation/en-us/unreal-engine/BlueprintAPI/LearningAgents) documentation.

## Animating Characters and Objects

[![](https://dev.epicgames.com/community/api/documentation/image/11977485-e378-4b2c-a54a-35f390fd4481?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/11977485-e378-4b2c-a54a-35f390fd4481?resizing_type=fit)

**Animation Blueprints** are Unreal Engine's equivalent to Unity's Animator Controllers. Animation blueprints include an **animation graph** and a standard blueprint event graph, providing a means for defining parameters and scripting complex animation behaviors and logic in a single point of entry.

For more information on this, see the [Animation Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine)  documentation.

If you prefer to organize animations with a state machine, you can create **State Machine** nodes in your animation graph, then double-click them to open their own specialized sub-graphs. You can then create new states, conduits, and state aliases, and create connections between them. Each state contains its own animation graph that controls the state's output and connections control the transitions between them.

For more information on this, see the [State Machines](https://dev.epicgames.com/documentation/en-us/unreal-engine/state-machines-in-unreal-engine) documentation.

**Blend Spaces** define a graph of animations that blend based on parameters. For example, a 2D blendspace can blend forward, backward, left, and right walking animations based on a character's velocity and facing.

For more information on this, see the [Blend Spaces](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine) documentation.

Unity uses the Timeline tool to animate cinematic sequences. The **Sequencer Editor** is Unreal Engine's equivalent to Unity's Timeline and provides an interface similar to a nonlinear editor for coordinating animations, effects, and camera movements. You can use Sequencer to define Level Sequences, which represent cinematics, or stand-alone animations for characters and objects. 

For more information on authoring sequences, see the [Sequencer Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine) documentation.

Unreal Engine also includes the **Control Rig System** which can be used to rig skeletal meshes for animation directly in the editor. With Control Rig, you can create and rig custom controls on a character, animate them in the Sequencer, and use a variety of other animation tools to aid your animating process.

For more information on rigging in Unreal Engine, see the [Control Rig](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-in-unreal-engine) documentation.

To capture and export image and video sequences within the Unreal Editor, you can use the **Movie Render Queue**. This is the equivalent of the Unity Recorder tool. Movie Render Queue can be used to render and export frame-by-frame sequences, in-game images, or video recordings with lossless quality.

For more information on Movie Render Queue, see the [Rendering High Quality Frames with Movie Render Queue](https://dev.epicgames.com/documentation/en-us/unreal-engine/rendering-high-quality-frames-with-movie-render-queue-in-unreal-engine) documentation.

## Gameplay Framework

[![](https://dev.epicgames.com/community/api/documentation/image/523d9bbf-4a02-4cd7-aae6-873d3d388a46?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/523d9bbf-4a02-4cd7-aae6-873d3d388a46?resizing_type=fit)

The **Gameplay** **Framework** in Unreal Engine is a collection of classes that provides you with a modular foundation upon which you can build your gameplay experience, such as **game** **mode**, **player state**, **controllers**, **pawns**, and **cameras**.

In Unity, similar structures are handled by components such as CharacterController and MonoBehaviour scripts attached to GameObjects to define behaviors. 

For more information on leveraging Gameplay Framework, see the [Gameplay Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/gameplay-framework-in-unreal-engine) documentation.

## Input

The **Enhanced** **Input System** is designed to handle player input across multiple devices, including keyboards, gamepads, and touchscreens. 

You can define Input Actions (for actions like jumping and shooting) and Input Axes (for continuous inputs like movement or camera rotation). These actions and axes can be bound to specific keys, buttons, or even touch gestures, providing a high degree of customization.

 To get started with the Enhanced Input System, you can create Enhanced Input Assets from the Content Browser by pressing the **\+ Add** button, and selecting **Input**. These assets can be configured to define the key bindings and inputs for your game.

You can bind these actions and axes to player input events in your game logic. The system can be used to manage different input schemes (e.g., keyboard vs. gamepad) and provides a way to define complex control schemes.

Unity developers might be familiar with the Unity Input System, similar in functionality to the Enhanced Input System in Unreal Engine. In Unreal Engine, 

For more information on defining input in your project, see the [Enhanced Input](https://dev.epicgames.com/documentation/en-us/unreal-engine/enhanced-input-in-unreal-engine) documentation.

## World Creation and Design

[![](https://dev.epicgames.com/community/api/documentation/image/3396481b-b1a7-4d7c-8a5c-bc0c3543c0db?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3396481b-b1a7-4d7c-8a5c-bc0c3543c0db?resizing_type=fit)

The functionality for building worlds in Unreal Engine is divided into different editor modes in the Level Viewport.  

### Modeling and Level Prototyping

The **Modeling** mode provides similar functionality to Unity’s ProBuilder extension, with extensive vertex, edge, face, and UV editing tools similar to what you would use in a modeling program.

You can activate the Modeling mode by clicking the Modes dropdown menu in the Viewport, and select Modeling.

For more information on the modeling in Unreal Engine, see the [Modeling Mode Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine) documentation.

### Creating a Terrain / Landscape

The **Landscape** mode provides similar functionality to Unity’s Terrain system. You can use the Landscape mode to create a landscape and shape it by using a tool suite similar to Unity’s Terrain system, such as raise, lower, and flatten.

You can activate the Landscape mode by clicking the Modes dropdown menu in the Viewport, and select Landscape.

To learn more about this, see the [Landscape Quick Start Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/landscape-quick-start-guide-in-unreal-engine) documentation. Additionally, see the Landscape Outdoor documentation to learn about creating terrain for large, open, outdoor environments. 

### Foliage

The **Foliage** mode is similar to Unity’s Terrain system for adding and managing foliage. In Foliage Mode, you can paint trees, grass, and other vegetation into your level, adjusting properties like density, height, and rotation of each piece.

One key difference from Unity's terrain system is that Unreal Engine’s Foliage mode can be used to paint foliage on any object, not just the landscape. This mode provides an intuitive way to populate your world with natural elements while giving you control over how they appear across the landscape or any surface in your level.

You can activate the Foliage mode by clicking the Modes dropdown menu in the Viewport, and select Foliage.

To learn more about this, see the [Foliage mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/foliage-mode-in-unreal-engine) documentation. Additionally, the [Open World Tools](https://dev.epicgames.com/documentation/en-us/unreal-engine/open-world-tools-in-unreal-engine) documentation can be used to learn more about procedurally filling large spaces with Static Mesh assets to create outdoor spaces that feel natural and alive.

### Procedural Content Generation (PCG)

The **Procedural Content Generation** **Framework (PCG)** is a toolset for creating procedural content inside Unreal Engine. PCG can be used by artists and designers to build fast, iterative tools and content of any complexity ranging from asset utilities, such as buildings or biome generation, up to entire worlds.

PCG is designed for extensibility and interactivity, providing integration into existing world building pipelines, effectively blurring the lines between procedural and traditional workflows.

For more information on creating procedural content in Unreal Engine, see the [Procedural Content Generation Framework](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation--framework-in-unreal-engine) documentation.

### Water System

The **Water System**  can be used to create rivers, lakes, and oceans that all interact and work together with your Landscape terrain using a spline-based workflow.

Unity developers might be familiar with the Water System available for projects using HDRP. The Water System in Unreal Engine is scalable to fit projects of all sizes and it supports all platforms.

For more information on enabling water in your levels, see the [Water System](https://dev.epicgames.com/documentation/en-us/unreal-engine/water-system-in-unreal-engine) documentation.

## Visuals and Rendering

[![](https://dev.epicgames.com/community/api/documentation/image/2cd41f3a-28b7-4fa6-bebe-f42f58b642f5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2cd41f3a-28b7-4fa6-bebe-f42f58b642f5?resizing_type=fit)

Unity uses the Scriptable Render Pipeline system (SRP) and provides templates like the High Definition Render Pipeline (HDRP). Unreal Engine has a unified, robust, and highly customizable render pipeline. This means that device support, functionality, and the feature set is not split among templates.

In Unreal Engine, you can use the **Scalability settings** to change the visual fidelity of your game. To learn more about this, see the [Scalability Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/scalability-reference-for-unreal-engine) documentation.

### Light sources

Lighting workflows in Unreal Engine are similar to those in Unity. You can add or remove lights to levels, and you have various types of light sources that you can use like Directional, Point, and Spot lights.

By going to **Create > Light**, you can choose the shape of the light source you want to add to your level. This will create a new object. To learn more about light types and how to use them, see the [Light Types and Their Mobility](https://dev.epicgames.com/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine) documentation.

### Sky Light

The **Sky Light** captures the distant parts of your level and applies that to the scene as a light. This means the sky's appearance and its lighting/reflections will match, even if your sky is coming from the atmosphere, or layered clouds on top of a skybox, or distant mountains. 

A new level in Unreal Engine by default has a **Lighting** folder in the **Outliner** panel. This folder contains a default set of lighting objects, like a DirectionalLight, ExperimentalHeightFog, and a SkyLight. To learn more about this,  see the [Sky Lights](https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine) documentation.

### Lumen Global Illumination and Reflections

**Lumen** is Unreal Engine’s fully dynamic global illumination and reflections system that is designed for next-generation devices, and it is the default global illumination and reflections system. This means that light bounces and interacts with surfaces, creating natural-looking lighting instantaneously without the need to bake lighting using precomputed workflows. 

To learn more about using dynamic global illumination and reflections in your project, see the [Lumen Global Illumination and Reflections](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine) documentation.

### Post-Processing

In Unity, post-processing is handled through Volumes. After creating a GameObject with a Volume component, you can assign a post-processing profile, and set whether it’s global or local. 

In Unreal Engine, post-processing is primarily handled using placed volumes. However, it can be applied in these other ways. Overall, post-processing works in a similar fashion where you can override default values.

| Ways of applying post-processing | Description |
| --- | --- |
| 
Project settings

 | 

By default, Unreal Engine applies a set of post-processing effects to your game based on the Scalability settings. These settings are applied project-wide unless overridden.

You can change the default post-processing effects that apply globally to the project by going to **Project Settings > Engine > Rendering**.

 |
| 

Camera component

 | 

Each camera component has its own set of overridable post-processing settings. These work on a per-camera basis, meaning that cameras that do not override any settings will apply the default effects defined in the Project Settings or use values applied to a placed volume.

 |
| 

Post Process Volume

 | 

A Post Process Volume can be added to a level by going to **Add > Volume**. This creates a new level actor that overrides the default post-processing settings, much like the Volume component in Unity.

These volumes can apply post processing when the player camera is within the volume, or they can apply any overrides globally to the entire level when their **Infinite Extent (Unbound)** setting is enabled. This works in similar fashion to the **Global Mode** option in Unity’s Volume framework.

 |

### Materials

Unity uses Shader Graph to define new shaders. Unreal Engine's equivalent is the **Material system**. Shaders and materials in Unreal Engine are distinct from each other in the following ways:

1.  A shader is a low-level construct in C++ that defines a base shading model, such as Lit, Unlit, Clear Coat, or Hair. This determines the inputs for the shader, such as Metallic or Translucent, and how they each react to light.
    
2.  A material is a logical graph of texture inputs, formulas, and instructions that are fed into a shader, representing a single object's surface qualities and specific expression of that shader.
    

To create a material, right-click anywhere in the **Content Browser** and click **Create Basic Asset > Materials**. The Material Editor displays a blank graph with the Main Material node. 

Click the **Main** **Material** node to display its properties in the **Details** panel. You can select different shaders with the **Shading Model** setting.

In situations where you want to apply a unique material to more than one mesh, we recommend using **Material Instances**. These are parameterized versions of materials that you can use to create variety and uniqueness without incurring additional costs. 

Each material instance uses either a material or another material instance as its parent (or “master” material) to make edits. Any nodes that have been parameterized in the master material are accessible in the **Instanced Material Editor**. These exposed parameters can be used to create endless variations from a single source material to create color variations, apply different textures, increase or decrease details, and more. 

Using material instances is more efficient when you use a master material and its child materials to drive variation. 

To create a material instance, right-click a material in the **Content Browser**, then click **Create Material Instance**.

To learn more about materials and material instances, see the [Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-materials) documentation and [Creating and Using Material Instances](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-and-using-material-instances-in-unreal-engine) documentation. Additionally, to learn more about the Material Editor, see the [Material Editor Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-material-editor-user-guide) documentation.

### Nanite

Nanite is Unreal Engine’s virtualized geometry system which uses an internal mesh format and rendering technology to render pixel scale detail and high object counts. It focuses on only the detail that can be perceived and no more.

Nanite provides various benefits to projects, like multiple orders of magnitude increase in geometry complexity, higher triangle and object counts than what has been possible before in real-time. Frame budgets are no longer constrained by polycounts, draw calls, and mesh memory usage.

For more information on Nanite and how to leverage it in your projects, see the [Nanite Virtualized Geometry](https://dev.epicgames.com/documentation/en-us/unreal-engine/nanite-virtualized-geometry-in-unreal-engine) documentation.

## Audio

Unity uses an audio source framework wherein each audio source in your game's world has a single voice associated with it. Unity uses Mixers to apply audio channel settings to these sources.

Unreal Engine's **MetaSounds** plugin is an audio generation system that can be used for complete control over a **Digital Signal Processing (DSP)** graph within a visual scripting environment similar to Blueprint.

To learn more about this, see the [MetaSounds](https://dev.epicgames.com/documentation/en-us/unreal-engine/metasounds-in-unreal-engine) documentation.

To mix audio, we recommend using the **Audio Modulation** plugin, which provides dynamic control over audio parameters, such as volume and pitch, from Unreal Engine's Blueprint or Component systems.

To learn more about this, see the [Audio Modulation Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-modulation-overview-in-unreal-engine) documentation.

**Sound** **Cues** are audio objects that encapsulate complex sound design tasks in a node graph. They can be used to dynamically change parts of a sound effect's design by arranging and modifying sound nodes, creating complex audio output.

To learn more about sound cues, see the [Sound Cue Reference](https://dev.epicgames.com/documentation/en-us/unreal-engine/sound-cue-reference-for-unreal-engine) documentation.

For a thorough overview of Unreal Engine’s audio systems, see the [Working with Audio](https://dev.epicgames.com/documentation/en-us/unreal-engine/working-with-audio-in-unreal-engine) page.

## Visual Effects

[![](https://dev.epicgames.com/community/api/documentation/image/450bcafe-3789-4991-a414-22d41cd2a37d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/450bcafe-3789-4991-a414-22d41cd2a37d?resizing_type=fit)

**Niagara Particle Systems** are Unreal Engine's equivalent to Unity's Particle Systems and the VFX Graph. You can create Niagara Emitters to build single particle emitters, or Niagara Systems to composite together multiple emitters into a more complex visual effect. When you create a new system or emitter asset, you can use an existing Niagara emitter as a template. 

The Niagara editor's System Overview graph provides a similar interface for editing particles as Unity's particle system editor. Niagara emitters and systems are made up of modular components that can handle a wide variety of behaviors or events. Each module you add increases the complexity of your particle system and adds new parameters to configure.

For more information on this, see the [Creating Visual Effects](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-visual-effects-in-niagara-for-unreal-engine) documentation.

The **Niagara** **Fluids** plugin can be used to add smoke, fire, explosions, water, splashes, and more physically plausible effects to your projects.

For more information on this, see the [**Niagara Fluids**](https://dev.epicgames.com/community/learning/paths/mZ/unreal-engine-niagara-fluids) documentation.

## User Interface

The **Unreal Motion Graphics** editor, or **UMG**, is Unreal Engine's equivalent to Unity's UI Toolkit and UI component library. UMG provides a WYSIWYG editor for building UIs from a variety of widgets, including buttons, text elements, and numerous containers and grids.

To create a new UI, create a new **Widget Blueprint** in the **Content Browser**. When you open a Widget Blueprint, it opens the UMG editor and displays a blank grid with a **Palette** panel of widgets on the left and a Details panel on the right. A button in the upper-right corner switches between the **Designer** and **Graph** views.

Use the Designer view to arrange widgets inside your Widget Blueprint. Click and drag widgets from the Palette panel into your graph, and use the **Hierarchy** to change the draw order. Widgets lower in the list display on top. Enable the **Is Variable** checkbox in a widget's Details panel to expose it to your UI's script.

As the name suggests, any Widget Blueprint you create can be used as a widget inside other Widget Blueprints. These appear in your palette under the **User Created** category. You can then use Widget Blueprints both for whole menus and HUDs, as well as for re-useable components like buttons or progress bars.

To learn more about this, see the [UMG UI Designer Quick Start Guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/umg-ui-designer-quick-start-guide-in-unreal-engine) documentation. Additionally, see the [Creating User Interfaces](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-user-interfaces-with-umg-and-slate-in-unreal-engine) documentation for more information on building and displaying UI.

## Saving and Loading

The ability to quit the game and then resume where a player has left off is a part of most modern games. Depending on the type of game you are making, you may only need a few basic pieces of information saved, like the last checkpoint the player reached, or more detailed information.

Unity developers might be familiar with PlayerPref which can be used to store player preferences between game sessions, or a variety of Asset Store packages that provide saving and loading functionality. These features are built-in to the Unreal Engine.

For more information on adding the ability to save and load game sessions in Unreal Engine, see the [Saving and Loading Your Game](https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-loading-your-game-in-unreal-engine) documentation.

## High Level Feature Comparison between Engines

This section provides a general overview of what some features and tools are named and used for in Unity and Unreal Engine. 

| Purpose | Unreal Engine | Unity |
| --- | --- | --- |
| User Interface (UI) |  |  |
| --- | --- | --- |
| 
Creating UI

 | 

Unreal Motion Graphics (UMG)

 | 

UI Toolkit

 |
| World Building |  |  |
| --- | --- | --- |
| 

Creating landscapes of all shapes

 | 

Landscape mode

 | 

Terrain system

 |
| 

Adding foliage to a landscape

 | 

Foliage mode

 | 

Terrain system’s foliage

 |
| 

Building level blockouts

 | 

Modeling mode

 | 

ProBuilder

 |
| 

Creating water surfaces and underwater effects

 | 

Water System

 | 

Water System

 |
| 

Procedurally generating worlds and tools

 | 

Procedural Content Generation (PCG)

 | 

Third-party tools

 |
| Optimization |  |  |
| --- | --- | --- |
| 

Profiling suite for identifying performance issues.

 | 

  Tracing

 | 

  Profiler

 |
| Gameplay |  |  |
| --- | --- | --- |
| 

Handling player input

 | 

Enhanced Input System

 | 

Input System

 |
| 

Visual scripting

 | 

Blueprint Editor

 | 

Visual Scripting (formerly known as Bolt)

 |
| 

Scripting and programming languages supported

 | 

C++ (programming)

 | 

C# (scripting)

 |
| 

Physics engine

 | 

Chaos Physics

 | 

NVIDIA PhysX

 |
| 

Saving and loading game data

 | 

SaveGame Objects

 | 

PlayerPrefs / Custom solutions

 |
| Artificial Intelligence |  |  |
| --- | --- | --- |
| 

State machine for crafting AI states

 | 

StateTree

 | 

Third-party tools

 |
| 

Creating areas for AI where they can navigate

 | 

Navigation System

 | 

NavMesh

 |
| Animation |  |  |
| --- | --- | --- |
| 

Handling animation data

 | 

Animation Blueprints

 | 

Animator Controller

 |
| 

Creating animation sequences

 | 

Sequencer editor

 | 

Timeline

 |
| 

Rigging 3D characters

 | 

Control Rig

 | 

Third-party tools

 |