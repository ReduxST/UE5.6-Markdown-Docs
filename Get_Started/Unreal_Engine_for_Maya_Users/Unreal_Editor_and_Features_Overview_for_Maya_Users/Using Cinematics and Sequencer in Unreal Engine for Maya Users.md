# Using Cinematics and Sequencer in Unreal Engine for Maya Users

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cinematics-and-sequencer-in-unreal-engine-for-maya-users](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cinematics-and-sequencer-in-unreal-engine-for-maya-users)  
**Processed:** 2025-06-14 16:58:26

---

Unreal Engine contains robust cinematic tools enabling you to create animated and cinematic sequences where you can pilot cameras to create fly-throughs, animate characters, move and change properties for any actors in the scene, such as lights and other objects, and render out your sequences. **Sequencer** is at the core of a lot of workflows as a non-linear editing suite. It is the primary tool you’ll use to create animations and cinematic content in Unreal Engine. 

[![Sequencer](https://dev.epicgames.com/community/api/documentation/image/9c9ec300-00ea-44a5-b172-fca0ec090143?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9c9ec300-00ea-44a5-b172-fca0ec090143?resizing_type=fit)

To get started with Sequencer, see the following topics: 

-   [Sequencer Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview)
    
-   [Starting Out Topics for Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine)
    
-   **[Sequencer Editor Topics](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine#sequencer-editor)**
    
-   [Workflow Guides and Examples](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine#workflow-guides-and-examples)
    

## Key Benefits of Using Sequencer

-   **Real-Time Cinematics** where you can preview animations, lighting, and effects in real-time, drastically reducing iteration time compared to traditional offline rendering workflows.
    
-   **Non-Linear Timeline-Based Editing Capabilities** where you can layer and blend animations, audio, events, and camera cuts like in a video editing toolset.
    
-   **Fully Integrated with features of Unreal Engine** meaning that you can animate any property of any actor in a level with its common and unique properties, such as location, rotation, material changes, lighting and shadowing, and more.
    
-   **Camera System and Cuts** to allow for full control of cinematic cameras and its properties, such as field off view, depth of field, lens effects, and post process settings. You can add and switch between cameras using cut tracks for editing.
    
-   **Event Tracks and Gameplay Syncing** to trigger gameplay logic directly from Sequencer using Event Tracks, which can be useful to start playing audio, animations, and Blueprints during a cinematic.
    
-   **Audio Integration** to add, preview, and sync audio tracks directly with what is happening in the level.
    
-   **Export Options** for rendering sequences using Movie Render Queue or Movie Render Graph for high-quality offline output whereby you can capture stills, videos, or image sequences with motion blur and anti-aliasing applied.
    
-   **Quick Render Options** to render a scene from the viewport without needing to manually set up Movie Render Queue or Movie Render Graph to see the result of your work.
    
-   **Collaborative Workflows** where you can share sub-sequences across multiple levels or even projects enabling you to swap assets and animations without rebuilding the whole timeline.
    
-   **Engine Plugins** that provide additional tools and functionality to your workflow. Some tools simplify the process for working with specific types of content, such as the Media Viewer, or add non-gameplay-oriented editing for animation, like with the Animation Kit and its utilities and deformer control rigs.
    

## Sequencer Components and Features

The following is a list of different components you’ll use in Sequencer to create cinematics and animate objects.

| Unreal Engine Component | Description |
| --- | --- |
| 
**Sequencer Editor**

 | 

This is the main interface used to edit Level Sequence assets in order to create cinematic content using a timeline to create cinematics, cutscenes, animations, and scripted events.  

[![Level Sequence](https://dev.epicgames.com/community/api/documentation/image/06fcad87-f025-4a19-992d-659507b97d9d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/06fcad87-f025-4a19-992d-659507b97d9d?resizing_type=fit)



 |
| 

**Level Sequence Asset**

 | 

This is a foundational asset used to create cinematic content for games and traditional animation in Unreal Engine. These assets are tied to specific levels and actors within them. These assets contain cameras, characters, and other game objects that you can animate for playback during game or rendering output. These can also include sub-sequences and shots to create more dynamic and complex cinematics. 

For more information, see “Level Sequences” in [Sequences, Shots, and Takes](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine).

 |
| 

**Level Sequence Actor**

 | 

These are actors placed in a level that is a container for the Level Sequence asset. You can use it to manage playback options for the assigned Level Sequence.

For more information, see “Sequencer Asset and Actor” section of [Sequencer Overview](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-sequencer-movie-tool-overview).

 |
| 

**Shots**

 | 

These are individual sequences within a Level Sequence that you can use to create more complex cinematics. Each shot corresponds to its own Sequence asset, which can be used for different Level Sequences. 

For more information, see “Shots” in [Sequences, Shots, and Takes](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine).

 |
| 

**Curve Editor**

 | 

This is used to control the way objects are animated by modifying and fine-tuning keyframes. Within the graph, you can create new keyframes, edit tangents, and use built-in tools to adjust the animation curves. For more information, see Curve Editor.

[![Curve Editor](https://dev.epicgames.com/community/api/documentation/image/981a885e-3698-444d-8739-2715498c0125?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/981a885e-3698-444d-8739-2715498c0125?resizing_type=fit)

For more information, see [Curve Editor](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-curve-editor-in-unreal-engine).

 |
| 

**Tracks**

 | 

This is a timeline component that represents a specific property or behavior of an object that you want to animate and control over time using keyframes to specify values at specific times. Each track controls a property for an actor, such as its transform, visibility, animation, material, lighting, and more.  

For more information, see [Tracks](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequencer-track-list-in-unreal-engine).

 |
| 

**Render Output**

 | 

While Sequencer can be used to playback sequences in real-time during gameplay, it can also output images and video rendered at higher quality results when compared with traditional real-time rendering. With this rendering option, you can use additional settings and commands to significantly increase the quality, precision, and look for features like Lumen Global Illumination and Reflections, and improved motion blur with removed unwanted anti-aliasing artifacts.

The engine offers several ways you can output images, which you can learn about by seeing the following topics:

-   [Movie Render Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-pipeline-in-unreal-engine)
    
-   [Movie Render Queue](https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-pipeline-in-unreal-engine#movie-render-queue)
    
-   [Movie Render Graph](https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-pipeline-in-unreal-engine#movie-render-graph)  
    
-   [(Legacy) Render Movie Options](https://dev.epicgames.com/documentation/en-us/unreal-engine/old-render-movie-in-unreal-engine)
    

 |

## Constraints with Control Rigs

When animating, there may be cases where you need to attach elements together without causing a change in the Outliner or Control hierarchy. This kind of attachment is known as constraining. Constraints in Unreal Engine are broken up into different methods: **Position**, **Rotation**, **Scale**, **Parent**, and **LookAt**. With these, you can set options to control how these constraints operate, such as controlling the attachment offset and baking the constraint back to normal keyframes.

Constraints are established by creating a **Parent - Child** relationship between two or more objects. You can add Constraints to a mesh when using the level editor **Animation** mode.

For more information on their types and usage, see [Constraints](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-constraint-tools-in-unreal-engine). 

## Deformers

Animation deformers are a way to adjust and distort the surfaces of your skeletal meshes in Unreal Engine. The **Animator Kit** plugin adds a set of animator-friendly deformers that you can add to your meshes in Sequencer. 

The Animator Kit plugin includes several utility rigs and deformers that you can use. Below are some examples:

|  |  |  |
| --- | --- | --- |
|  | 
[![Lattice Deformer](https://dev.epicgames.com/community/api/documentation/image/e7438f44-423c-45a7-9010-e74b9dd45929?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e7438f44-423c-45a7-9010-e74b9dd45929?resizing_type=fit)



 | 

[![Camera Space Deformer](https://dev.epicgames.com/community/api/documentation/image/6cd46209-d8e2-4b81-b25f-2bd227f246d2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6cd46209-d8e2-4b81-b25f-2bd227f246d2?resizing_type=fit)



 |
| 

**Sculpt Deformer**

 | 

**Lattice Deformer**

 | 

**Camera Space Lattice Deformer**

 |

You can enable the Animator Kit from **Plugins** browser found in the main menu under the **Edit** menu.

For more information on using this plugin and Deformers, see [Getting Started with Deformers](https://dev.epicgames.com/community/learning/tutorials/wj6z/unreal-engine-getting-started-with-deformers-in-ue-5-5) learning course on the EDC.

## Transform Track

In Sequencer you can apply a **Transform** track to animate and move objects, cameras, and characters in your scene. When applied to an actor, such as a skeletal mesh, it can scale, rotate, and move the mesh. The Transform track is most helpful for gameplay animation because it moves the origin of the exported asset around, but is also useful for general animation workflows for linear content. Attaching it to the top node of a rig will have unintended consequences, like double transforms and things will explode as they are transformed.

Maya doesn’t have this concept of applying transforms to the rig in this way. For you to do so, you’d have to build overly complex logic into your rig and add a global scale that knows how to deal with specific features of the rig for face, body, hair, and others. Unreal simplifies this process making it a small part of your process to transform rigs and animations with minimal effort.

In this example below, you can see how applying a Transform track in Sequencer can reasonably scale the rig and mesh without causing it to break.

|  |  |
| --- | --- |
|  |  |
| 
**Scaling applied to the Actor in Unreal engine.**

 | 

**Scaling Applied to the Rig, which causes it to break.**

 |

To learn more about the usage of tracks and the transform track in Sequencer, see [Transform and Property Tracks](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine).

## Dockable Media Viewer

Often animators need to align their animations against existing reference footage. In Unreal Engine, you can dock a video file or Sequencer-driven Media Track next to the viewport where animation work is done. This mechanic allows docking media assets (images, media textures, live viewport textures) anywhere in the engine’s interface. Two A/B banks in either horizontal or vertical configurations help compare two sets of images. Zoom and pan controls can be used to further align content you place here.

This tool is a plugin for the engine. You can enable this tool for your project by going to the main menu > Edit menu and opening the **Plugins** browser. Search **“Media Viewer”** and enable it for the project. 

## Levels versus Level Sequences

In Unreal Engine, Levels and Level Sequences are fundamentally different but are used together in cinematic and gameplay workflows. 

-   A **Level** is a container that holds everything playable and editable in a real-time environment. This includes anything from geometry, lighting, cameras, sounds, logic, and more. This is where you’ll build the environment, place characters and props, and define gameplay through Blueprint, events, and triggers.
    
-   A **Level Sequence** is an asset used to create animations, cutscenes, or scripted events within a level using its actors. It uses the Sequencer editor to set up tracks to control when things happen within a level using a timeline. The timeline stores animated values with keyframes to trigger animations, camera cuts, Blueprint events, and more. Level Sequences can be used for creating cinematics, triggering scripted gameplay events, or playing pre-recorded camera moves and animations.
    

For more information, see the “Level Sequences” section of [Sequences, Shots, and Takes](https://dev.epicgames.com/documentation/en-us/unreal-engine/sequences-shots-and-takes-in-unreal-engine).

## Movie Render Pipeline

While Unreal Engine is primarily a real-time engine, its movie render pipeline includes offline images sequence and movie rendering solutions. For general workflows, you’ll create everything using its real-time workflows and tools. However, you can achieve higher quality results using its real-time features for rendering and lighting using offline output through Movie Render Queue or Movie Render Graph. These tools include settings and commands that greatly increase the quality, precision, and look for the engine’s lighting and rendering capabilities without worrying about balancing real-time performance with quality.

There are two tools you can use to interface with the movie render pipeline. Each offers different features to meet our project's needs. 

-   **Movie Render Graph** (MRG) is a graph-based interface where you can build logic to execute rendering operations.
    
-   **Movie Render Queue** (MRQ) is a tool where you can create presets and scripts to queue render processes and then export high-quality video and images.
    

For more information on using either of these render output options, see [Movie Render Pipeline](https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-pipeline-in-unreal-engine).

### Quick Render with Movie Render Queue

The **Quick Render** toolbar option enables you to quickly render the scene without manually configuring a queue or graph. It uses the current map and level sequence, the level sequence’s playback range, and the viewport’s look to generate frames.

The Quick Render dropdown menu includes options for what actions the Quick Render toolbar button should take and by what method it should use to do so. 

[![Quick Render Menu](https://dev.epicgames.com/community/api/documentation/image/eb48a964-426a-4c14-87e1-b6d8435cba1a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/eb48a964-426a-4c14-87e1-b6d8435cba1a?resizing_type=fit)

For more information on rendering out scenes, see [Movie Render Queue](https://dev.epicgames.com/documentation/en-us/unreal-engine/movie-render-pipeline-in-unreal-engine#movie-render-queue). 

## Next Page

[

![Additional Features and Resources of Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/d5ca4fff-ad01-4090-a9f1-e42fac0e9087?resizing_type=fit&width=640&height=640)

Additional Features and Resources of Unreal Engine for Maya Users

A brief overview of additional features of Unreal Engine and useful resources for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/additional-features-and-resources-of-unreal-engine-for-maya-users)