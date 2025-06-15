# Scripting in Unreal Engine for Maya Users

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-in-unreal-engine-for-maya-users](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-in-unreal-engine-for-maya-users)  
**Processed:** 2025-06-14 16:48:10

---

Unreal Engine provides several ways for you to script functionality for your projects. Some are ideal for gameplay at runtime while others are only useful to build in-editor tools. 

## Python Scripting

Python Scripting is ideal for production pipelines and interoperability between 3D applications, particularly those in the media and entertainment industry. Python is great for automating workflows within the Unreal Editor and cannot be used for runtime scripting. Python is integrated into a lot of features and workflows you would use in Unreal Engine.  

Python scripting can be used in Unreal Editor to do things like:

-   Construct larger-scale asset management pipelines or workflows that tie the Unreal Editor to other 3D applications that you use.
    
-   Automate time-consuming asset management tasks in the editor, like generating level of detail (lod) meshes for Static Meshes.
    
-   Procedurally lay out content in a level.
    
-   Control the editor from user interfaces that you create yourself in Python.
    

Python scripting is a plugin, which you can enable from the main menu under the **Edit** menu in the **Plugins** browser when you enable the **Python Editor Script Plugin** and **Editor Scripting Utilities**. 

To learn more about getting started using Python in Unreal Engine, see [Scripting the Unreal Editor Using Python](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-python). 

For Maya users, Python workflows are integrated into key areas with animation, control rig, and IK rigs. You can find more information about how to use Python in these workflows in the links below:

-   [Python Scripting for Animating with Control Rig](https://dev.epicgames.com/documentation/en-us/unreal-engine/python-scripting-for-animating-with-control-rig-in-unreal-engine)
    
-   [Python Scripting for Rigging with Control Rig](https://dev.epicgames.com/documentation/en-us/unreal-engine/control-rig-python-scripting-in-unreal-engine)
    
-   [Python Scripting in Sequencer](https://dev.epicgames.com/documentation/en-us/unreal-engine/python-scripting-in-sequencer-in-unreal-engine)
    
-   [Using Python with IK Rigs](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-python-to-create-and-edit-ik-rigs-in-unreal-engine)
    
-   [Using Python with the IK Retargeter](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-python-to-create-and-edit-ik-retargeter-assets-in-unreal-engine)
    

## Blueprint Visual Scripting

Unreal Engine includes a visual scripting language called **Blueprint**. This is a complete scripting system that uses a node-based interface to create in-editor tools and workflows, gameplay elements for characters and objects, trigger animations and sounds, and more. The system is extremely flexible and powerful as it provides designers a way to implement their concepts through a suite of tools that are generally only available to programmers. 

Blueprints are ideal for designers and artists who want to build out functionality without any coding experience. They are useful for fast prototyping, developing logic in a visual way, and Blueprint seamlessly integrates with the rest of Unreal Engine’s systems.

[![Blueprint Graph](https://dev.epicgames.com/community/api/documentation/image/c974ee4d-6d1c-4b60-a03e-f84770f777d5?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c974ee4d-6d1c-4b60-a03e-f84770f777d5?resizing_type=fit)

Example Blueprint graph.

 Here are handful of ways you can use Blueprints in the Editor or at runtime: 

-   Setup character movement and behavior for gameplay
    
-   Trigger animations and sounds to play
    
-   Create a user interface with UMG
    
-   Create in-editor tools with Editor Utility Widgets
    
-   Interaction with objects, such as opening doors.
    
-   Spawning enemies or other gameplay events
    
-   Adding logic to level, such as moving platforms.
    
-   And more!
    

With all this in mind, not every Blueprint is the same. There are several types to handle information and logic differently. These types include:

-   [Blueprint Class](https://dev.epicgames.com/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine):
    
    -   This type of Blueprint includes a viewport and node graph. It’s most useful for creators that want to add actors, such as player characters, enemies, weapon pick-ups, and so on that have logic applied to them.
        
-   [Data-Only Blueprint](https://dev.epicgames.com/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine):
    
    -   This is like a Blueprint Class but only with node graphs. It includes variables and components inherited from its parent. These Blueprints can only modify inherited properties, making them ideal for creating variations of a parent class. You can think of these like the relationship between Materials and Material Instances.
        
-   [Blueprint Interface](https://dev.epicgames.com/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine):
    
    -   This contains user-created functions you can use to share and send data between any Blueprints that use them. This is an asset you can create and reference in your Content Browser.
        
-   [Level Blueprint](https://dev.epicgames.com/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine):
    
    -   This is a specialized type of Blueprint that only exists in a loaded Level. It can act as a level-wide global event graph, such as triggering actors or other events, such as playing a Level Sequence.
        
-   [Animation Blueprint](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprints-in-unreal-engine):
    
    -   This is a specialized Blueprint that is built into the [Animation Modes](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) editor. They are used to control animation of a skeleton mesh during simulation or gameplay. The difference in this Blueprint’s node graph is that it’s set up to blend animation, control the bones of a skeleton, and create logic that defines the final pose to use per-frame.  
        

For more information on using Blueprints in your projects, see the following topics: 

-   [Blueprint Visual Scripting](https://dev.epicgames.com/documentation/en-us/unreal-engine/blueprints-visual-scripting-in-unreal-engine)
    
-   [Types of Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/types-of-blueprints-in-unreal-engine)
    

## Animation Blueprints

**Animation Blueprints** are part of the Animation Modes editor. These are a specialized type of Blueprint used to control and manage the animation of a skeletal mesh. It’s primarily used for characters used in gameplay whereby you can define complex animation behavior using Blueprint’s node-based scripting. While Animation Blueprints are generally used for real-time gameplay, you can use them to implement real-time animation effects, such as real-time physics, cloth simulation, or mesh deformation.

[![Blueprint Graph](https://dev.epicgames.com/community/api/documentation/image/c1593597-7512-4ea0-84f9-5eaec52f77a0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c1593597-7512-4ea0-84f9-5eaec52f77a0?resizing_type=fit)

Example character, Echo from the Valley of the Ancients sample project, and the Animation Blueprint that drives her animations through movement.

For more information on Animation Blueprints, see the Using Animations in Your Project section of this guide, or see [Animation Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-blueprint-editor-in-unreal-engine). 

## Editor Utility Widgets

**Editor Utility Widgets** enable you to build your own in-editor tools, planes, and interfaces using Blueprint visual scripting in order to streamline workflows. These utility widgets can access and manipulate editor data, such as actors, assets, and levels. Any utility widget you build is dockable, like any other panel in the Unreal Editor. 

**Editor Utility Widgets** are ideal for streamlining your workflows, automating repetitive tasks, managing assets, and manipulating content directly in a level. 

For more information on these and how you can start using them, see the following:

-   [Scripting the Unreal Editor Using Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-the-unreal-editor-using-blueprints)
    
-   [Editor Utility Widgets](https://dev.epicgames.com/documentation/en-us/unreal-engine/editor-utility-widgets-in-unreal-engine)
    
-   [Editor Utility Blueprints](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripted-actions-in-unreal-engine)
    

## Scriptable Tools System

The **Scriptable Tools** system provides functions and an editor mode to create custom interactive tools, with the goal being to make it possible for non-C++ programmers to build interactive tools in the editor. This plugin exposes the Interactive Tools Framework to Blueprint, providing creators and technical artists the means to design tools that behave similar to those found in the [Modeling mode](https://dev.epicgames.com/documentation/en-us/unreal-engine/modeling-mode-in-unreal-engine).

These may appear similar to Editor Utility Widgets, but it uses a non-modal dialog window containing a custom built user interface where you can do different kinds of editor scripting. While powerful and useful in its own right, as a non-modal dialog, there are limitations to what it can do. The Scriptable Tools is modal, meaning that no other tool can be active while it’s in use. This also means the editor state is more strictly managed. Scriptable tools can more efficiently capture the mouse, the user interface has more structure than utility widgets, and you can use the tools you create at runtime. 

Some use cases for Scriptable Tools are: 

-   Draw basic 3D geometry, such as lines and points.
    
-   Add property sets to tools through Blueprint and have them act as user-visible tool settings.
    
-   Create one or more 3D gizmos, control their positions, and respond to transform changes.
    
-   Pair scriptable tools with other features of the engine, such as [Procedural Content Generation](https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-content-generation--framework-in-unreal-engine) (PCG) and [Motion Design](https://dev.epicgames.com/documentation/en-us/unreal-engine/motion-design-in-unreal-engine).
    

For more information, see [Scriptable Tools System](https://dev.epicgames.com/documentation/en-us/unreal-engine/scriptable-tools-system-in-unreal-engine).

## Next Page

[

![Designing and Building Worlds in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/6d65385e-1db5-4dc2-b079-ebec8aaaa699?resizing_type=fit&width=640&height=640)

Designing and Building Worlds in Unreal Engine for Maya Users

An overview of Unreal Engine's design tools to build scenes for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/designing-and-building-worlds-in-unreal-engine-for-maya-users)