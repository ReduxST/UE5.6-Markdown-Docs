# Physics Asset Editor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-in-unreal-engine)  
**Processed:** 2025-06-14 16:42:34

---

[![The Physics Asset Editoris specifically designed to manipulate Physics Assets for Skeletal Meshes.](https://dev.epicgames.com/community/api/documentation/image/a96cdd69-d962-4621-a9b5-10b2104129ff?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a96cdd69-d962-4621-a9b5-10b2104129ff?resizing_type=fit)

The **Physics Asset Editor** is an integrated editor that is part of the [Animation Editors](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) in Unreal Engine. It is specifically designed to manipulate **Physics Assets** for **Skeletal Meshes**.

[![A Physics Asset is used to define the physics and collision used by a Skeletal Mesh](https://dev.epicgames.com/community/api/documentation/image/2150e1b4-7ff7-4441-86ff-d238f5ad82bf?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2150e1b4-7ff7-4441-86ff-d238f5ad82bf?resizing_type=fit)

A Physics Asset is used to define the physics and collision used by a Skeletal Mesh. These contain a set of rigid bodies and constraints that make up a single ragdoll, which is not limited to humanoid ragdolls. They can be used for any physical simulation using bodies and constraints. Because only a single Physics Asset is allowed for a Skeletal Mesh, they can be turned on or off for many Skeletal Mesh components.

|  |  |
| --- | --- |
| 
[![A humanoid character](https://dev.epicgames.com/community/api/documentation/image/1946a5fa-e730-4710-bbe2-3eac5b0b3650?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1946a5fa-e730-4710-bbe2-3eac5b0b3650?resizing_type=fit)



 | 

[![The Buggy from demo](https://dev.epicgames.com/community/api/documentation/image/fb5088ee-17af-4d60-926f-cbb309b38c98?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fb5088ee-17af-4d60-926f-cbb309b38c98?resizing_type=fit)



 |
| 

Character Physics Asset

 | 

Vehicle Physics Asset

 |

A Physics Asset can be set up for any Skeletal Mesh for simulation. These are two examples of their usage; a humanoid character and the Buggy from Epic's demo Vehicle Game.

## Creating Physics Assets

There are two ways that Physics Assets can be created for your Skeletal Meshes:

-   On import by having **Create Physics Asset** enabled.
    
    [![On import by having Create Physics Asset enabled](https://dev.epicgames.com/community/api/documentation/image/d21ea5db-eb58-4505-884c-6fb8c4246e8c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d21ea5db-eb58-4505-884c-6fb8c4246e8c?resizing_type=fit)
    
-   By creating a Physics Asset using the **Content Drawer** and selecting a Skeletal Mesh to use.
    
    [![Use the Content Drawer and select a Skeletal Mesh](https://dev.epicgames.com/community/api/documentation/image/4eb5b371-6570-40cf-8140-388634299283?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4eb5b371-6570-40cf-8140-388634299283?resizing_type=fit)
    
    The first time the Physics Asset is selected, a window to set how bodies and constraints should be generated will open:
    
    [![A window to set the how bodies and constraints should be generated](https://dev.epicgames.com/community/api/documentation/image/ccebd597-6b84-4d4b-996d-323f26663ce4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ccebd597-6b84-4d4b-996d-323f26663ce4?resizing_type=fit)
    

## Opening the Physics Asset Editor

The **Physics Asset Editor** can be opened in several different ways:

-   By double-clicking the **Physics Asset** in the **Content Drawer**.
    
    [![By double-clicking the Physics Asset in the Content Drawer](https://dev.epicgames.com/community/api/documentation/image/19c7f4c4-9093-4882-a544-566cbbf1c5de?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/19c7f4c4-9093-4882-a544-566cbbf1c5de?resizing_type=fit)
    
-   By using the right-click context menu and selecting **Edit...**.
    
    [![By using the right-click context menu and selecting Edit](https://dev.epicgames.com/community/api/documentation/image/7ab55578-2f1a-4fa5-ad5e-834f505940ef?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7ab55578-2f1a-4fa5-ad5e-834f505940ef?resizing_type=fit)
    
-   By selecting the **Physics** tab in the [Animation Editors](https://dev.epicgames.com/documentation/en-us/unreal-engine/animation-editors-in-unreal-engine) selection tabs.
    
    [![By selecting the Physics tab in the Animation Editors selection tabs](https://dev.epicgames.com/community/api/documentation/image/1d334f3f-5360-47a2-b090-883530325097?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1d334f3f-5360-47a2-b090-883530325097?resizing_type=fit)
    
    The dropdown menu next to the **Physics** tab can be used to select any Physics Asset located in the **Content Drawer** that is using the currently opened Skeletal Mesh.
    
    [![The dropdown menu can be used to select any Physics Asset](https://dev.epicgames.com/community/api/documentation/image/fde6e522-b13e-4e35-b865-9731dd567542?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/fde6e522-b13e-4e35-b865-9731dd567542?resizing_type=fit)
    

## Essentials

[

![Physics Bodies](https://dev.epicgames.com/community/api/documentation/image/1f4892db-bc7d-44ce-9b6d-3feebfd3ba4a?resizing_type=fit&width=640&height=640)

Physics Bodies

Describes how to use Physics Bodies (Body Instance) for physics simulation.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-bodies-in-unreal-engine)[

![Physics Constraints](https://dev.epicgames.com/community/api/documentation/image/81a1c49b-6015-4f53-a065-752969cab06f?resizing_type=fit&width=640&height=640)

Physics Constraints

Constraining physics objects together and to the world.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-constraints-in-unreal-engine)

## Tutorials

[

![Physics Asset Editor Tutorials](https://dev.epicgames.com/community/api/documentation/image/9c01e529-3aa5-4581-a893-d45061c0a2e5?resizing_type=fit&width=640&height=640)

Physics Asset Editor Tutorials

Landing page for the Physics Asset Tool how-to section.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/physics-asset-editor-tutorial-directory-for-unreal-engine)