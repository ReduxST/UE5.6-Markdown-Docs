# Lighting and Rendering in Unreal Engine for Maya Users

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/lighting-and-rendering-in-unreal-engine-for-maya-users](https://dev.epicgames.com/documentation/en-us/unreal-engine/lighting-and-rendering-in-unreal-engine-for-maya-users)  
**Processed:** 2025-06-14 16:33:31

---

Unreal Engine’s lighting and rendering features prioritize real-time workflows optimized for games and interactive environments where there is often a balance between performance and quality over offline rendered workflows. This means you can see results while working in the editor without waiting to render a complete scene when using an offline-rendered workflow.

Even so, while the engine prioritizes real-time workflows where you get what you see, there is support for features and workflows that more closely align with offline workflows to push quality of the final rendered image further. This includes using image output through features like Movie Render Queue or Movie Render Graph in conjunction with ray tracing features or the standalone Path Tracer.

## Unreal Engine’s Lighting System

Unreal Engine’s lighting is primarily driven by these components:

-   **Global Illumination**:
    
    -   **Lumen Global Illumination** is a real-time global illumination and reflections system. It provides options that work with a broad range of hardware. For higher quality results, use Lumen with [Hardware Ray Tracing](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-technical-details-in-unreal-engine#hardware-ray-tracing) for high quality reflections.
        
-   **Shadowing**:
    
    -   **Virtual Shadow Maps** deliver consistent, high-resolution shadowing that works with film-quality assets and large, dynamically lit open worlds and is supported by Nanite Virtualized Geometry and Lumen Global Illumination. Virtual shadow maps are on by default in projects that support DirectX 12.
        
-   **Render Settings**:
    
    -   **Post Process Volumes** include a lot of rendering settings that can affect the rendering of a scene globally or in isolated parts of a level. This includes settings for depth of field, bloom, exposure, color grading, reflections, and many other feature areas.
        
-   **Placeable Lights**:
    
    -   There are a variety of light types you can place to achieve different results. This includes directional lights, sky light, point and spot lights, and area lights.
        
-   **Environment Lighting**:
    
    -   There are a variety of world lighting features to define the look and feel of the world. These include features for volumetric clouds and atmosphere rendering, and fog.
        

### Placing and Using Different Types of Lights

Unreal Engine provides different types of lights to create nearly any type of lighting scenario that works with small and large scale scenes. These include large lights for multiple sun or moon representation down to small scale lights for medium and small-sized interior or exterior spaces.

The table below is a list of the types of lights Unreal Engine includes and their equivalences in Maya:

| Unreal Engine | Maya | Description |
| --- | --- | --- |
| 
**Directional Light**

 | 

Directional Light

 | 

Used for sunlight / moonlight. Infinite, parallel light rays

 |
| 

**Point Light**

 | 

Point Light

 | 

Emits light in all directions from one point

 |
| 

**Spot Light**

 | 

Spot Light

 | 

Cone-shaped light. Good for flashlights, stage lights, etc

 |
| 

**Rect Light**

 | 

Area Light

 | 

Rectangular soft light. Great for tvs, windows, etc.

 |
| 

**Sky Light**

 | 

Environment Light

 | 

Captures ambient lighting and sky reflections (usually paired with cubemaps/HDRIs).

 |

These are examples of Unreal Engine’s Point, Spot, and Rect lights. 

|  |  |  |
| --- | --- | --- |
| 
[![](https://dev.epicgames.com/community/api/documentation/image/713ba615-36a2-49bc-b6b6-df383d63f0dc?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/713ba615-36a2-49bc-b6b6-df383d63f0dc?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/f55ee753-3a64-45f6-983c-7fe5794e4ec8?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f55ee753-3a64-45f6-983c-7fe5794e4ec8?resizing_type=fit)



 | 

[![](https://dev.epicgames.com/community/api/documentation/image/43f4ea4c-1aba-4abe-aa88-b1107db93743?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/43f4ea4c-1aba-4abe-aa88-b1107db93743?resizing_type=fit)



 |
| 

**Point Light**

 | 

**Spot Light**

 | 

**Rect Light**

 |

Below are some quick notes you can use while working with lighting in the engine: 

-   **Quick Placement of Lights at cursor location**:
    
    -   In the Viewport, press **L** to place a Point light at the cursor location.
        
        -   Use the right-click context menu to select “**Replace selected actor with**” to choose another light type to swap it out with.
            
-   **Directional Lights**:
    
    -   You can have up to two Directional lights in the scene. For example, this can be multiple suns or sun and moon.
        
        -   Each of the Directional lights must have a different **Atmosphere Sun Light Index** set in their actor settings.
            
    -   Use **Right Shift + L** while dragging the mouse cursor to change the Directional light’s position for Index 0.
        
    -   Use **Right Shift + Right Ctrl + L** while dragging the mouse cursor to change the Directional light’s position for Index 1.
        
-   **Light Mobility**:
    
    -   Each type of actor, whether it be Lights or objects in the scene, can have a mobility set that determines how they are treated by the different lighting paths for dynamic and precomputed lighting. While light mobility may not be a needed factor unless you’re developing your project with baked lighting in mind, it’s worth noting that this exists and can affect how objects interact with different lighting paths in Unreal Engine.
        
-   **Sky Lighting and HDRIs**:
    
    -   You should use a Sky Atmosphere, Directional light, and Sky Light to achieve realistic looking lighting for environment scenes.
        
    -   HDRIs can be assigned to any Sky Light actor that has **Real Time Capture** enabled in its settings. Alternatively, you can create a material and apply an HDRI to a large skysphere as a background.
        

For the purposes of making it simpler to work in complex scenes and environments with lots of lights, you can use the **Light Mixer** panel to change properties of lights more simply than selecting individual lights or groups of lights to make adjustments to from the Outliner panel in the Unreal Editor. 

You can enable the Light Mixer panel as a dockable panel from the main menu under the **Windows** menu.

[![Light Mixer](https://dev.epicgames.com/community/api/documentation/image/ccff8bbb-5ce0-4c79-b19d-7bd4e57b88ee?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ccff8bbb-5ce0-4c79-b19d-7bd4e57b88ee?resizing_type=fit)

For more information on Lighting and its components in Unreal Engine, see the following topics: 

-   [Light Types and Their Mobility](https://dev.epicgames.com/documentation/en-us/unreal-engine/light-types-and-their-mobility-in-unreal-engine)
    
-   [Lumen Global Illumination and Reflections](https://dev.epicgames.com/documentation/en-us/unreal-engine/lumen-global-illumination-and-reflections-in-unreal-engine)
    
-   [Virtual Shadow Maps](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine)
    
-   [Shadowing](https://dev.epicgames.com/documentation/en-us/unreal-engine/shadowing-in-unreal-engine)
    
-   [Light Mixer](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-light-mixer-in-unreal-engine)
    

### Post Process Volumes

In Unreal Engine, **Post Process Volumes** are placeable volumes whereby you can configure rendering settings that affect the look and feel of an area. These can be isolated areas within the volume or globally applied to everywhere in the level. 

With a placed Post Process Volume you can change settings for color grading, depth of field, bloom, reflections, and more. You can also use Materials with post processing to create more specific effects. 

For the purposes of making color grading more approachable and tweakable in your scene, you can use the **Color Grading** panel in conjunction with any actor that has post process settings integrated into them, such as the already named post process volume, cine camera actor, and camera actors.

You can enable the Color Grading Panel as a dockable panel from the main menu under the **Windows** menu.

[![Color Grading Panel](https://dev.epicgames.com/community/api/documentation/image/49d3f1ae-c3c9-440c-9f91-79cbdaf59051?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/49d3f1ae-c3c9-440c-9f91-79cbdaf59051?resizing_type=fit)

For more information on Post Processing in Unreal Engine, see the following topics: 

-   [Post Process Effects](https://dev.epicgames.com/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine)
    
-   [Post Process Materials](https://dev.epicgames.com/documentation/en-us/unreal-engine/post-process-materials-in-unreal-engine)
    
-   [Color Grading and the Filmic Tonemapper](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine)
    
-   [Color Grading Panel](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-grading-panel-in-unreal-engine)
    
-   [Depth of Field](https://dev.epicgames.com/documentation/en-us/unreal-engine/depth-of-field-in-unreal-engine)
    

### Environment Lighting Features

Any environment you have is generally made up of a light source, atmosphere, and clouds. Unreal Engine includes a suite of features that enables you to build out environments to feel part of a larger world, whether you build to that scale or not. The lighting system in the engine supports all of these features in a drag-and-drop fashion to get you started.

[![Cloud And Sky Examples](https://dev.epicgames.com/community/api/documentation/image/afe0297a-4dd4-4b49-8b87-e096dd96fe1f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/afe0297a-4dd4-4b49-8b87-e096dd96fe1f?resizing_type=fit)

For the purposes of making environment lighting more approachable and simpler to adjust, the **Environment Light Mixer** panel includes all these actor’s Details panels in one place. You can even open this panel directly and add the actors to the scene that make up these elements of the environment to start adjusting them immediately.

You can enable the Environment Light Mixer panel as a dockable panel from the main menu under the **Windows** menu.

[![Environmental Light Mixer](https://dev.epicgames.com/community/api/documentation/image/8348c4a9-6e09-4337-b19b-264863df92b3?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8348c4a9-6e09-4337-b19b-264863df92b3?resizing_type=fit)

For more information on using these lighting components that make up large environments, see the following topics: 

-   [Environment Light Mixer](https://dev.epicgames.com/documentation/en-us/unreal-engine/environment-light-mixer-in-unreal-engine)
    
-   [Environmental Light with Fog, Clouds, Sky and Atmosphere](https://dev.epicgames.com/documentation/en-us/unreal-engine/environmental-light-with-fog-clouds-sky-and-atmosphere-in-unreal-engine)
    
-   [Sky Atmosphere Component](https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-atmosphere-component-in-unreal-engine)
    
-   [Volumetric Cloud Component](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine)
    
-   [Volumetric Cloud Material](https://dev.epicgames.com/documentation/en-us/unreal-engine/volumetric-cloud-material-in-unreal-engine)
    
-   [Sky Lights](https://dev.epicgames.com/documentation/en-us/unreal-engine/sky-lights-in-unreal-engine)
    
-   [Exponential Height Fog](https://dev.epicgames.com/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine)
    
-   [Local Fog Volumes](https://dev.epicgames.com/documentation/en-us/unreal-engine/local-fog-volumes-in-unreal-engine)
    

## Time of Day System with Day Sequence

For those looking for something that is quicker to setup and apply for your scene as a starting point, the Day Sequence plugin includes a time-of-day system that is fully drag-and-drop into a scene (like the example below), or you can use a more customizable version of Day Sequence to tailor it to your project.

For more information on using the built-in time of day system, see [Setting Up A Time Of Day With Day Sequence](https://dev.epicgames.com/documentation/en-us/unreal-engine/day-sequence-time-of-day-plugin-for-unreal-engine).

## Next Page

[

![Scripting in Unreal Engine for Maya Users](https://dev.epicgames.com/community/api/documentation/image/b6934f24-95ef-4d8f-b625-3aed82bed188?resizing_type=fit&width=640&height=640)

Scripting in Unreal Engine for Maya Users

An overview of Unreal Engine's scripting functionality for Maya users.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/scripting-in-unreal-engine-for-maya-users)