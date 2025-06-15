# Simulation Blank Template

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/simulation-blank-template-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/simulation-blank-template-in-unreal-engine)  
**Processed:** 2025-06-14 16:50:34

---

The **Simulation Blank** template is an **Empty World** Level template enriched with simulation-specific settings and functionality. It consists of an empty environment with the following features and characteristics:

-   A flat Static Mesh as the ground/floor.
    
-   A [SunSky](/documentation/en-us/unreal-engine/geographically-accurate-sun-positioning-tool-in-unreal-engine) system with Earth-specific settings:
    
    -   North offset compatible with the GeoReferencing plugin conventions.
        
    -   A directional light with realistic Sun properties (**Intensity**, **Source Angle**), casting far shadows that leverage the [Virtual Shadow Maps](/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine) system (requires enabling the **DirectX 12 (SM6. Experimental)** option under **Project Settings > Platforms - Windows** and a compatible graphics card).
        
-   [Volumetric clouds](/documentation/en-us/unreal-engine/volumetric-cloud-component-in-unreal-engine), with a natural-looking material.
    
-   [Exponential Height Fog](/documentation/en-us/unreal-engine/exponential-height-fog-in-unreal-engine).
    
-   Stars (note that these are for cosmetic purposes only, and do not accurately represent realistic star positioning for any given real-world location).
    
-   A global Post-Process Volume with **Exposure** settings corresponding to human vision.
    
-   A [Georeferencing](/documentation/en-us/unreal-engine/georeferencing-a-level-in-unreal-engine) Actor to locate the environment on Earth.
    

The Geographic location of the UE origin in the SunSky and Georeferencing Actors has been set to 73W, 45N. You'll have to adapt it to your actual environment location if needed.

This template also comes with a custom `BP_SimGameMode` Blueprint that defines a specific `BP_SimPlayerController` and `BP_SimfloatingPawn`. These Blueprints are provided as an example of how to enhance the default features of the base Controller and Pawn classes and are explained below.

## The Simulation Player Controller (BP\_SimPlayerController)

This controller comes with some key shortcuts to allow the following player actions at runtime:

-   Navigate freely with a floating Pawn spawned on play (`BP_SimfloatingPawn`).
    
-   Alternate between this floating Pawn and a Pawn that already exists in the Level.
    
-   Control the time of day.
    
-   Display a profiling and stats widget.
    
-   Display the Geospatial location status bar.
    

The following keyboard shortcuts are available:

| **Key** | **Action** |
| --- | --- |
| Pawn controls |   |
| **Enter** | Alternate between the Floating Pawn and a pre-existing Level Pawn. |
| **Tab** | When controlling a Level Pawn, switch to the next controllable Pawn. |
| **Shift + Tab** | When controlling a Level Pawn, switch to the previous controllable Pawn. |
| **1 - 6** | Direct shortcut to control a specific Level Pawn. If there are more than 6, use the **Tab** key. |
| Time of Day controls |   |
| **End** | Decrease the current Time of Day. |
| **Page Down** | Increase the current Time of Day. |
| **Insert** | Smoothly transition the Time of Day to a Dawn value. |
| **Home** | Smoothly transition the Time of Day to a Noon value. |
| **Page Up** | Smoothly transition the Time of Day to a Dusk value. |
| Widget controls |   |
| **P** | Show / Hide the Profiling Widget. |
| **G** | Show / Hide the Geospatial Widget. |

### Geospatial Widget

Click image for full size.

The **Geospatial Widget** is a status bar displaying your current location on Earth in different coordinate systems:

-   Projected CRS.
    
-   Geographic CRS (Lat/Long).
    
-   Geocentric (ECEF).
    

To learn more, refer to the [Georeferencing a Level](/documentation/en-us/unreal-engine/georeferencing-a-level-in-unreal-engine) page.

### Profiling Widget

Click image for full size.

The **Profiling Widget** is a debug utility to profile the performance of your application.

The left button stack will show or hide different performance counters, which you can also access by their associated `stat counterName` console command. The widget displays the most common and useful ones:

-   FPS
    
-   Unit
    
-   Engine
    
-   SceneRendering
    
-   Game
    
-   GPU
    

Since profiling is heavily linked to the number of frames per second (FPS), the second column of buttons is where you can enable or disable vertical sync (VSync) or cap FPS to 30 or 60 FPS if desired.

## The Simulation Floating Pawn (BP\_SimfloatingPawn)

The Simulation Floating Pawn is an improved version of the Unreal Engine default Pawn, with the added capability to control the maximum navigation speed using the **mouse wheel**. This helps when dealing with large environments.

**Clicking** the mouse wheel will reset to the default speed.