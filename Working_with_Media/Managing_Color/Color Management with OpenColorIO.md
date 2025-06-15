# Color Management with OpenColorIO

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine)  
**Processed:** 2025-06-14 16:14:12

---

Unreal Engine 5 supports OCIO v2. For more information about the features included in OCIO v2, refer to the [OCIO documentation](https://opencolorio.readthedocs.io/en/latest/upgrading_v2/how_to.html).

[OpenColorIO](http://opencolorio.org/) (**OCIO**) is a color management system used primarily in film and virtual production. OCIO guarantees the colors of captured video remain consistent through the entire film pipeline. This pipeline includes initial camera capture, all the compositing applications that need to work with the captured media, and the final render.

**Unreal Engine** (UE) offers support for using OCIO to convert the colors of linear media in several ways:

-   When you use media sources like captured clips or live feeds in your project, you can apply color conversion to make those media sources match your computer-generated elements in UE.
    
-   You can use OCIO to apply color conversions to your Viewport and Play in Editor (PIE) windows. This means your reference frames in the editor will be consistent with your chosen color space.
    
-   You can re-apply another color conversion to the composited feed you output from [Composure](/documentation/en-us/unreal-engine/real-time-compositing-with-composure-in-unreal-engine). This helps make your CG elements and live frames blend more convincingly, while preserving the colors of the original shots faithfully.
    
-   You can use Displays and Views to apply color conversions to multiple physical or virtual display devices from the same OCIO configuration.
    
-   You can apply color space transformations to [nDisplay](/documentation/en-us/unreal-engine/rendering-to-multiple-displays-with-ndisplay-in-unreal-engine) renders on monitors and LED walls.
    
-   When you export a video through [Movie Render Queue](/documentation/404), you can apply a color space transformation to your output video or image sequence.
    

All OCIO features in the engine rely on an **OpenColorIO Configuration Asset**, which you use to manage the color profiles that you want to work with.

The OpenColorIO Configuration Asset references an OCIO configuration (`.ocio`) file, which contains detailed specifications about multiple color profiles and how to transform between them. UE currently supports OCIO v2. For more details on OCIO configuration files, refer to the [OpenColorIO v2 documentation](https://opencolorio.readthedocs.io/en/latest/index.html).

This page contains links to documentation about creating an OpenColorIO Configuration Asset and applying color transformations in the engine.

## Quick Start

This page guides you through creating an OpenColorIO Configuration Asset.

## Converting Colors in the Viewport

The Editor supports applying OCIO color conversions to the Level Viewport through **Viewport View Modes** and to Play in Editor mode through Blueprints. This page shows how to apply color transformations to the Level Viewport and Play in Editor mode.

## Converting Colors in Blueprints

This page describes how to use **Blueprints** to apply color transformations.

## Converting Colors in nDisplay

[nDisplay](/documentation/en-us/unreal-engine/rendering-to-multiple-displays-with-ndisplay-in-unreal-engine) supports applying OCIO color conversions to nDisplay renders for the entire cluster, the inner frustum, or individual cluster nodes. This can be useful for managing the color spaces of specific displays. This page explains how to use OCIO with nDisplay.

## Converting Colors in Movie Render Queue

[Movie Render Queue](/documentation/404) supports applying OCIO color conversions to media exports. This page shows how to set the color conversion in Movie Render Queue.

## Converting Colors in Composure

[Composure](/documentation/en-us/unreal-engine/real-time-compositing-with-composure-in-unreal-engine) supports applying OCIO color conversions to input and output media. This page explains how to apply color transformations in Composure.