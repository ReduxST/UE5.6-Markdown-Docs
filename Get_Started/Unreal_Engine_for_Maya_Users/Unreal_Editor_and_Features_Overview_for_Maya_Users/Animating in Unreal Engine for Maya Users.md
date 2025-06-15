# Animating in Unreal Engine for Maya Users

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-in-unreal-engine-for-maya-users](https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-in-unreal-engine-for-maya-users)  
**Processed:** 2025-06-14 16:06:05

---

Unreal Engine has a suite of animation tools and editors to create characters and object runtime animation systems, rendered cinematic content, and author new animation content directly from within the engine and in real-time so you can see all your changes immediately.

For Maya users, Unreal Engine approaches animation in a real-time environment with interactive content tailored for games using state-driven logic, and interactive experiences to be “played” by the user, and not just playback. Even though Unreal Engine’s environment is tailored for this type of development, it doesn’t mean you have to make this type of experience. You can adapt offline workflows to a fully real-time environment that emphasizes collaboration, and instant feedback for lighting and materials, all while making you more efficient in the moment with the choices you can make without long turnaround times to render out a scene.  

This section of the guide will draw comparisons between Maya and Unreal Engine concepts, familiarize you with the primary components of animation in Unreal Engine, give you an overview of workflows for creating animations in the engine or using imported content, and point you towards some additional animation tools to familiarize yourself with. 

## Key Concepts Comparison

Below is a list of Maya concepts and how they translate to Unreal Engine.

| Maya | Unreal Engine |
| --- | --- |
| 
Joints and Skeleton

 | 

Skeletons

 |
| 

Rigging

 | 

Skeletons

 |
| 

Skinning

 | 

Skeletal Mesh

 |
| 

Keyframe Animation

 | 

Imported Animation Asset

 |
| 

Animation Exports (OBJ, FBX, etc)

 | 

Animation Sequences

 |
| 

Blend Shapes and Driven Keys

 | 

Morph Targets, Blend Spaces and Animation Curves

 |
| 

Animation Layers / Non-Linear Animation (NLA)

 | 

Anim Layers

 |
| 

Graph Editor

 | 

Sequencer Curves and Anim Graph

 |
| 

IK, FK, and HumanIK

 | 

Control Rig, Real-Time IK, and Non-Real Time IK Retargeting

 |
| 

Trax Editor (non-linear editing)

 | 

Animation Montages and Sequencer

 |
| 

Physics / Dynamics

 | 

Physics-Based Animation System

 |

## Animation Components

The following is a list of different components in Unreal Engine you’ll use to animate objects and work with animations you’ve imported or created in the editor.

| Unreal Engine Component | Description |
| --- | --- |
| 
**Skeleton and Skeletal Mesh**

 | 

The Skeleton is used to define bones (sometimes called joints) in a Skeletal (skinned) mesh. These bones, in some ways, mimic a real biological skeleton due to their position and control over how characters mesh deforms.

Skeletons are used to store and associate animation data, the overall skeletal hierarchy, and Animation Sequences. Skeletons can be shared among different skeletal meshes and animations.

Skeletal meshes contain the visual mesh of the character or object that uses a Skeleton to store bone data that is used to animate it. Skeletal meshes play animations and construct logic to control the character’s behavior in real-time.

For more information, see the following topics:

-   [Skeletal Meshes](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine)
    
-   [Skeletal Mesh Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-editor-in-unreal-engine)
    
-   [Skeleton Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeleton-editor-in-unreal-engine)
    

 |
| 

**Animation Sequence**

 | 

This is an animation asset that contains animation data that can be played on a Skeletal mesh to animate it. These animation sequences contain keyframes that specify position, rotation, and scale of the Skeleton assigned to the skeletal mesh at specific points in time. By blending between keyframes during sequential playback, the Skeleton’s motion animates the character.

Animation Sequences are tied to specific Skeleton assets, enabling animations to be shared across any skeletal meshes that use the same Skeleton asset.

For more information, see the following topics: 

-   [Animation Sequences](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sequences-in-unreal-engine)
    
-   [Animation Sequence Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-sequence-editor-in-unreal-engine)
    

 |
| 

**Blend Space**

 | 

These are assets that allow multiple animations or poses to be blended by plotting them onto either a one or two-dimensional graph. This graph can then be referenced within an Animation Blueprint where the blending can be controlled by gameplay input or other variables. With Blend Spaces, virtually any type of blending arrangement can be used for your animations.

Blend spaces can be thought of as interactive sliders or driven keys that use a visual grid to smoothly interpolate between animations based on inputs. While these are commonly used for smooth blending between idle / walk / run cycle animations they can also take speed and direction into account. 

For more information, see [Blend Spaces](https://dev.epicgames.com/documentation/en-us/unreal-engine/blend-spaces-in-unreal-engine).

 |
| 

**Control Rig**

 | 

This is a suite of animation tools for you to rig and animate characters directly in-engine, making it possible to bypass the need to rig and animate in external tools. With Control Rig, you can create and rig custom controls on a character, animate in Sequencer, and use a variety of other animation tools to aid your workflow. 

For more information, see [Control Rig](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-in-unreal-engine).

 |
| 

**Modular Control Rigs**

 | 

This is a digital animation rig that has been created by combining a series of pre-built Control Rig assets called Modules. A Module is a Control Rig component that represents a part of the character body, such as an arm, leg, or spine, that can be used to automatically create a set of controls and rig the part of the body, enabling it to receive animation data. Modules can be connected together to form a complete animation rig for articulation to drive a skeleton.

For more information, see [Modular Control Rigs](https://dev.epicgames.com/documentation/en-us/unreal-engine/modular-control-rigs-in-unreal-engine).

 |
| 

**Curve Editor**

 | 

Use this editor to modify and fine-tune keyframes of your animated objects. The curve editor’s graph is where you can edit existing keyframes or create new ones, edit tangents, and use its built-in tools to adjust your animation curves. Curves assets can be used across other editors in the engine, such as Niagara, but is used extensively with Sequencer to work with animation. 

[![](https://dev.epicgames.com/community/api/documentation/image/f537fad4-3638-4720-9b64-92b1cc4adddf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f537fad4-3638-4720-9b64-92b1cc4adddf?resizing_type=fit)

-   [Curve Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine)
    
-   [Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)
    
-   [Keyframing in Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine)
    

 |
| 

**Sequencer**

 | 

This is a cinematic editor for animating characters, cameras, properties, and other actors over time. It has a non-linear editing environment where you can create and modify tracks and keyframes along a timeline. 

For more information, see the following topics: 

-   [Cinematics and Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine)
    
-   [Sequencer Basics](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)
    
-   [Sequencer Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine)
    
-   [Sequencer Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview)
    

 |
| 

**Animation Mode**

 | 

The Level Editor can be put into different modes that serve different purposes, such as sculpting and painting terrain, modeling geometry, or animating. The level editor’s **Animation** mode provides a way for you to animate level actors and components directly in the level using Sequencer all while working in a realtime environment where WYSIWYG. 

The animation mode includes the following tools for Control Rigs: 

-   Constraint Tools
    
-   Poses Tools
    
-   Tweens Tools
    
-   Motion Trail Tool
    
-   And more!
    

[![Animation Mode](https://dev.epicgames.com/community/api/documentation/image/beae5fdd-ed0c-469c-9c66-8dfbca027f6d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/beae5fdd-ed0c-469c-9c66-8dfbca027f6d?resizing_type=fit)

For more information: see the following topics: 

-   [Level Editor Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/level-editor-modes-in-unreal-engine)
    
-   [Animation Mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editor-mode-in-unreal-engine)
    
-   [Sequencer Basics](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine)
    
-   [Control Rig](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-in-unreal-engine)
    
-   [Constraints](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine)
    
-   [Unreal Fest 2024 “Making Your Animation Unreal”](https://www.youtube.com/watch?v=PDz4bvP2MG0)
    
    -   Note that this demonstration is using Unreal Engine 5.5.
        

 |
| 

**Animation Blueprint**

 | 

These are specialized Blueprints that control the animation of a skeletal mesh during simulation or gameplay. Animation graphs are edited inside the Animation Blueprint Editor, where you can blend animation, control the bones of a skeleton, or create logic that defines the final animation pose for a skeletal mesh to use per frame. 

For more information, see the following topics: 

-   [Animation Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine)
    
-   [Animation Blueprint Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine)
    
-   [Graphing in Animation Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/graphing-in-animation-blueprints-in-unreal-engine)
    

 |
| 

**State Machine**

 | 

These are modular systems you can build inside of Animation Blueprints in order to define certain animations that can play and when they can play. Primarily, this type of system is used to correlate animations to movement states of your characters, such as idling, walking, running, and jumping.

With them, you can create “states” defined by animations that play during these times and create various types of transitions to control when to switch to other animation states. This makes it simpler to create complex animation blending without having to use an overly complicated Animation Graph.

[![State Machine](https://dev.epicgames.com/community/api/documentation/image/6f8625e3-e815-4dc0-b915-657d11a2d147?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6f8625e3-e815-4dc0-b915-657d11a2d147?resizing_type=fit)

For more information, see [State Machines](https://dev.epicgames.com/documentation/en-us/unreal-engine/state-machines-in-unreal-engine).

 |

## Additional Animation Tools

Unreal Engine includes many tools and systems to enable you to fully animate your project within the engine. Below are some highlights of additional tools, systems, and things you should consider when animating in Unreal Engine.

### Animation Retargeting

**Animation Retargeting** is a feature that allows for animations to be reused between multiple characters that use the same **Skeleton** asset but may have vastly different proportions. This eliminates the need to create entirely new animations as you can share your animation assets between them. 

There are two ways in which you can use retargeting for animations: 

-   The Skeleton of the character you’re retargeting uses the same Skeleton asset for which the animations were created for.
    
-   The Skeleton of the character you’re retargeting does not use the same Skeleton asset. Instead, you’ll use a Rig to pass the skeleton’s bone information to the other.
    

In the example below, there are three characters using the same Skeleton asset but all have different proportions to one another. Before retargeting, the Skeletons become deformed to the Skeleton despite their proportions. After retargeting, the character proportions are preserved for each character.

[![Animation Retargeting](https://dev.epicgames.com/community/api/documentation/image/9cd1be91-15dc-4ad2-a2eb-26ead86a7ff1?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9cd1be91-15dc-4ad2-a2eb-26ead86a7ff1?resizing_type=fit)

For more information, see the following topics: 

-   [Animation Retargeting](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-retargeting-in-unreal-engine)
    
-   [Using Retargeted Animations](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-retargeted-animations-in-unreal-engine)
    

### Physics-Based Animation

UE uses physics simulations (ragdolls, clothing, dynamic hair) to enhance realism

Can blend seamlessly with keyframe animations, a functionality more robots than typical Maya workflows.

Physic-driven animation blends the result of a simulation along with your keyframed animation to create naturally simulated feel for characters that need to exhibit a “ragdoll” effect or have elements that aren’t keyframed like hair, cloth, or chains simulate without being specifically animated.

*Example of physics-based animation from the Content Examples sample project.*

Physics-based animation does require you to set up a Physics asset for each character, enabling them to react with other surfaces that have collision set up. 

For more information, see the following topics: 

-   [Physics-Based Animation](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-driven-animation-in-unreal-engine)
    
-   [Physics Asset Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine)
    
-   [Content Examples](https://dev.epicgames.com/documentation/en-us/unreal-engine/content-examples-sample-project-for-unreal-engine)
    

### Layered Control Rigs

Layered Control Rigs is a system that leverages Control Rigs on top of many other workflows without the need to bake the data down to edit characters, which ultimately can lead to a destructive workflow as you make changes. Layer Controllers make it possible to blend and layer different control rigs together in Sequencer, adding the backwards solve in the control rig live onto the clip in Sequencer. Previously to edit an animation, you’d have to assign a control rig to your skeletal mesh in Sequencer, bake out the keys and have it play live.

For more information, see the EDC learning course [Layered Control Rigs - Deep Dive](https://dev.epicgames.com/community/learning/tutorials/Op78/unreal-engine-fortnite-layered-control-rigs-deep-dive). Additionally, you can download the [Content Examples](https://www.fab.com/listings/4d251261-d98c-48e2-baee-8f4e47c67091) project from Fab. The level “Animation\_ControlRig” includes several demonstrations of Layered Control Rigs and use cases that you can explore.

### Control Rig Backwards Solve

Control Rigs are evaluated in a couple of ways called solve directions. These are created in the Control Rig graph, and they split the rig logic into multiple solve directions, or solvers, with which you can expand on the incoming data for the rig. This enables workflows such as rig sharing, baking animation back to your controls, and debugging behavior. 

The primary use for Backwards Solve is to bake animation sequences to your control rig in order to make further changes to the animation within Unreal Engine. Backwards solve can also be useful for making refining edits to existing animations or motion capture data you’ve imported into the engine and then baking those changes in. 

For more information, see the “Backwards Solve” section of [Solve Directions](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-forwards-solve-and-backwards-solve-in-unreal-engine#backwards-solve).

### Animation Kit Plugin

The **Animator Kit** is a plugin that adds animator-friendly deformers and utility rigs to your project. These are just like adding any Control Rigs through Sequencer. 

You can enable this plugin from the main menu by going to **Edit > Plugins** and searching “Animator Kit.”

This plugin includes the following Control Rigs you and use in Sequencer:

-   Utility Rigs
    
    -   BlendParent
        
    -   3Node
        
    -   ChainSim
        
    -   SingleCim
        
    -   SplinePath
        
-   Deformers
    
    -   Sculpt Deformer
        
    -   Lattice Deformer (2x2x2, 3x3x3, and 4x4x4)
        
    -   Camera Space Lattice
        

For more information on using this plugin and Deformers, see [Getting Started with Deformers](https://dev.epicgames.com/community/learning/tutorials/wj6z/unreal-engine-getting-started-with-deformers-in-ue-5-5) learning course on the EDC.

## Additional Notes For Animating in Unreal Engine

-   **Root Motion**
    
    -   In Unreal Engine, characters are composed of many components and movement is often handled by the character’s [Movement Components](https://dev.epicgames.com/documentation/en-us/unreal-engine/movement-components-in-unreal-engine) with animation playback layered on top to communicate the visual feedback of motion. Root motion animations can drive character movement with animation data to create more grounded movement within a level. Examples of animations that would rely on root motion are ones that would move the character away from its root position, like jumping forward or backward, or performing a complicated action like a combination sword move.
        
    -   For more information, see [Root Motion](https://dev.epicgames.com/documentation/en-us/unreal-engine/root-motion-in-unreal-engine).
        
-   **Animation Compression**
    
    -   This is the process of transforming animation data from Animation Sequence assets in order to lower the overall animation file sizes and memory cost. With compression, the tradeoff is project performance, especially when scaling projects across multiple hardware targets with varying specifications. Animations with minimal movement benefit more so than ones with a lot of movement as there can be a noticeable drop in quality. It’s important to tailor the kind of compression you implement based on the type of quality loss your project can afford.
        
    -   For more information, see [Animation Compression](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-compression-in-unreal-engine).
        
-   **Live Link**
    
    -   This provides a common interface for streaming and consuming animation data from external sources, like Maya, into Unreal Engine. It provides a way for you to edit animations externally while seeing a preview of your work inside of Unreal Engine in real-time. This is really useful for motion capture systems and workflows.
        
    -   For more information, see [Live Link](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-in-unreal-engine).
        

## Next Page

[

![Using Cinematics and Sequencer in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/4995756c-734e-4d4e-bc41-d06db1e6cc3c?resizing_type=fit&width=640&height=640)

Using Cinematics and Sequencer in Unreal Engine for Maya Users

An overview of Unreal Engine's cinematic tool Sequencer for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cinematics-and-sequencer-in-unreal-engine-for-maya-users)