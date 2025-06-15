# Unreal Editor and Features Overview for Maya Users

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-and-features-overview-for-maya-users](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-editor-and-features-overview-for-maya-users)  
**Processed:** 2025-06-14 16:56:04

---

If you’re moving from a full or partial Maya workflow to Unreal Engine, it can be challenging to translate familiar features that you rely on from one application to another. While both have similar functionalities in some areas, the ecosystem Unreal Engine provides and the way it’s organized differs from that of Maya in many ways.

This guide provides a walkthrough of how you would get started with Unreal Engine and its features and the Maya equivalents, where possible. The sections of this guide are broken up into many things you’d want to know as a first-time or casual user of Unreal Engine.

## What does it mean to make the switch to Unreal Engine from Maya?

[![](https://dev.epicgames.com/community/api/documentation/image/b6e4765f-3ed0-47fe-b4b3-c2ef97d191c0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b6e4765f-3ed0-47fe-b4b3-c2ef97d191c0?resizing_type=fit)

-   **An Unreal Engine Pipeline versus a Traditional Pipeline**
    
    -   In a traditional pipeline workflow, each department has its own assignment, such as lighting, look dev, rigging, character creation, and so on. When content is finished in one, it may go to the next to work on in isolation, which can lead to wasted time as the content each department generates can take time to get the right solution.
        
    -   Using a fully integrated Unreal Engine pipeline helps avoid round-trip workflows and import/export issues. It also makes collaboration between departments simpler when everyone is working in the same tool and in a WYSIWYG realtime editor.
        
-   **Realtime Scene Updates versus a Global Timeline**
    
    -   In Maya, you have the main timeline that represents the overall time in a scene. You can place keys and go to a specific time. In Unreal Engine, you work in real-time without a dedicated timeline. Instead, there are dedicated tools, like Sequencer, where you’ll view a timeline and set keys to animate objects in the scene.
        
-   **Working in Real-time versus Offline Rendering**
    
    -   In Maya, you can potentially wait minutes to hours for Arnold or V-Ray to render a single frame. In Unreal Engine, you can see the result in real-time.
        
-   **Unreal Engine offers seamless asset integration**
    
    -   FBX, Alembic, and USD import pipelines preserve your work from Maya for geometry, rigging, and animations.
        
-   **Built-in artist-friendly tools to replace traditional pipeline workflows**
    
    -   Unreal Engine includes a suite of tools to develop your projects from beginning to end. This can replace entire parts of a traditional offline pipeline with one that provides feedback in real-time as you make changes. There is no waiting to see the finished results.
        
    -   Unreal Engine also supports full animation workflow capabilities with Skeletal Mesh editing tools, rigging with Control Rig, the Animators Kit plugin, animation deformers, and more.
        
    -   With the engine’s material editor, post-process effects, particles and physics, you can create nearly any style and look for your project in an iterative and collaborative workflow with your teams.
        
    -   High-quality lighting systems with dynamic global illumination and reflections with cinematic quality shadowing that work without any additional setup.
        

## Maya and Unreal Engine Terminology

Before you dive completely into learning Unreal Engine, let’s take a moment and look at terminology you may be familiar with in Maya and how that applies to Unreal Engine. 

| Autodesk Maya | Unreal Engine |
| --- | --- |
| 
Scene File

 | 

Project

 |
| 

Channel Box / Attribute Editor

 | 

Details Panel

 |
| 

Outliner

 | 

Outliner / Animation Outliner

 |
| 

Referencing Characters / Assets

 | 

Instancing using the Content Browser

 |
| 

Timeline / Dope Sheet / Trax Editor

 | 

Sequencer

 |
| 

Scenes / Environment Sets

 | 

Levels

 |
| 

Animation Scene Files

 | 

Level Sequences

 |
| 

Graph Editor

 | 

Curve Editor

 |
| 

Hypershade

 | 

Material Editor

 |

## Topics

To learn about and familiarize yourself with Unreal Engine and it's features, explore the topics below. Ideally, you'd follow along with these in order from top to bottom, but each area can be explored and learned independently of other topic pages.

[

![Unreal Engine Interface and Navigation](https://dev.epicgames.com/community/api/documentation/image/ed24529a-e266-4568-984f-df7e0ade61ed?resizing_type=fit&width=640&height=640)

Unreal Engine Interface and Navigation

An overview of Unreal Engine's editor interface and navigation controls for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-engine-interface-and-navigation)[

![Importing Content into Unreal Engine from Maya](https://dev.epicgames.com/community/api/documentation/image/6af188d2-182a-420c-9da2-323bf113f719?resizing_type=fit&width=640&height=640)

Importing Content into Unreal Engine from Maya

An overview of importing content into Unreal Engine for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/importing-content-into-unreal-engine-from-maya)[

![Using Materials and Textures in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/709cd0c1-cc2e-43c7-bc6e-6789097e0210?resizing_type=fit&width=640&height=640)

Using Materials and Textures in Unreal Engine for Maya Users

An overview of Unreal Engine's Material System and Textures for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-materials-and-textures-in-unreal-engine-for-maya-users)[

![Lighting and Rendering in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/d847f373-1ce3-4c85-bdf7-dd02402ddf5c?resizing_type=fit&width=640&height=640)

Lighting and Rendering in Unreal Engine for Maya Users

An overview of Unreal Engine's lighting and rendering features for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/lighting-and-rendering-in-unreal-engine-for-maya-users)[

![Scripting in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/b6934f24-95ef-4d8f-b625-3aed82bed188?resizing_type=fit&width=640&height=640)

Scripting in Unreal Engine for Maya Users

An overview of Unreal Engine's scripting functionality for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-in-unreal-engine-for-maya-users)[

![Designing and Building Worlds in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/6d65385e-1db5-4dc2-b079-ebec8aaaa699?resizing_type=fit&width=640&height=640)

Designing and Building Worlds in Unreal Engine for Maya Users

An overview of Unreal Engine's design tools to build scenes for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/designing-and-building-worlds-in-unreal-engine-for-maya-users)[

![Animating in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/68f2ba45-2126-46b8-bcbe-7f4504d3c8c4?resizing_type=fit&width=640&height=640)

Animating in Unreal Engine for Maya Users

An overview of Unreal Engine's animation system and its core features as they relate to a Maya user.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/animating-in-unreal-engine-for-maya-users)[

![Using Cinematics and Sequencer in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/4995756c-734e-4d4e-bc41-d06db1e6cc3c?resizing_type=fit&width=640&height=640)

Using Cinematics and Sequencer in Unreal Engine for Maya Users

An overview of Unreal Engine's cinematic tool Sequencer for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cinematics-and-sequencer-in-unreal-engine-for-maya-users)[

![Additional Features and Resources of Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/d5ca4fff-ad01-4090-a9f1-e42fac0e9087?resizing_type=fit&width=640&height=640)

Additional Features and Resources of Unreal Engine for Maya Users

A brief overview of additional features of Unreal Engine and useful resources for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/additional-features-and-resources-of-unreal-engine-for-maya-users)