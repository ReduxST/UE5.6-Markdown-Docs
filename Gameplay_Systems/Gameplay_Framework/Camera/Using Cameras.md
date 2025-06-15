# Using Cameras

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cameras-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-cameras-in-unreal-engine)  
**Processed:** 2025-06-14 16:58:23

---

Blueprints C++

This Tutorial series covers working with and placing **Cameras** in Unreal Engine. A Camera can be used by itself and placed directly into a level or it can be a part of a Blueprint (for instance, to provide a perspective for the player when flying a plane, driving a car, or controlling a character).

## Creating and Placing a Camera Actor

1.  In the Editor, navigate to **Window > Place Actors > All Classes**, then place a Camera by dragging a **Camera Actor** into your level.
    
    ![placed-actors-panel-camera-actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f23c501-335d-4c54-9538-33e90cc72ac4/placeactors.png)
2.  You can use the Search Bar to find the Camera Actor directly, or You can right-click in the Level Viewport and use the context menu by selecting **Place Actor** then selecting the **Camera Actor**.
    
    ![placed-camera-actor-from-the-context-menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/50c7ab88-af73-4f3a-81f7-7239971df0c4/contextmenuplaceactors.png)
3.  When you select your Camera in the Level, in the Viewport, a picture-in-picture window appears, representing the viewing angle of the Camera. The upper-middle portion of the picture-in-picture window displays the Camera name. In its lower-left corner, there is a pin icon, which provides the option to "pin" the window (keep it on screen when clicking off the Camera) is represented by a pin icon in the lower left corner of the window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3223bcfc-4eeb-4d06-8e35-e55af6431fa9/cameraviewport.png)
4.  Select a Camera to populate the **Details** panel with settings that pertain to the Camera.
    
    ![camera-details-panel-display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/604956a1-4596-41cb-833a-f022f33cfb67/cameradetails.png)

This Tutorial series covers working with and placing **Cameras** [(ACameraActor)](/documentation/404) with C++ in Unreal Engine. A Camera can be used by itself and placed directly into a Level or it can be a part of a Blueprint (for instance, to provide a perspective for the player when flying a plane, driving a car, or controlling a character).

## Creating And Placing a Camera Actor

1.  Create a Camera with the [C++ Class Wizard](/documentation/en-us/unreal-engine/using-the-cplusplus-class-wizard-in-unreal-engine). Launch the wizard, enable the box to **Show All Classes**, and, in the Search bar, type **CameraActor** to select and create your new Camera Actor class.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/054e32f4-da8a-4ac6-999f-2d55dcacd5e4/addcameraactorcpp.png)
2.  In the **Sources** panel, navigate back to your C++ classes folder and create a Blueprint class of your Camera Actor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc5e2c5a-347c-4d43-b9f6-368327cef1a2/bp_examplecameraactor.png)
3.  When you select your Camera in the Level, in the Viewport, a picture-in-picture window appears, representing the viewing angle of the Camera. The upper-middle portion of the picture-in-picture window displays the Camera name. In its lower-left corner, there is a pin icon, which provides the option to "pin" the window(keep it on screen when clicking off the Camera) is represented by a pin icon in the lower-left corner of the window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/305fcdb9-a54a-4934-9eea-5e8dbb88d1e2/cameraviewport.png)
4.  Select a Camera to populate the **Details** panel with settings that pertain to the Camera.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69e0c6c9-d4c2-43dc-abe9-6f0f920f7af8/cameradetails.png)

## Camera Actor Details Panel Overview

The following table is an overview of each section in the **Details** panel for a Camera Actor.

| Property | Description |
| --- | --- |
| **Transform** | This category represents the location of the Camera in the world. |
| **Camera Settings** | This category you to modify the type of projection used by the Camera, field of view, aspect ratio, and post process blending. |
| **Auto Player Activation** | Specifies which Player Controller, if any, should automatically use this Camera when the controller is active. |
| **Film** | In this category, you can apply film effects such as Tint, Saturation, or Contrast. See also [Film](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#film). |
| **Scene Color** | Used to apply effects to the Camera. See also [Scene Color](https://www.fab.com/listings/017fabb0-78ac-400e-8c97-fafa226b73f0). |
| **Bloom** | Simulates the effects the eye perceives when viewing bright objects. See also [Bloom](/documentation/en-us/unreal-engine/bloom-in-unreal-engine). |
| **Light Propagation Volume** | Used to achieve Global Illumination (GI) in real-time. See also [Light Propogation Volumes](/documentation/en-us/unreal-engine/lighting-the-environment-in-unreal-engine). |
| **Ambient Cubemap** | Lights the scene from a provided image. See also [Ambient Cubemap](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#ambientcubemap). |
| **Auto Exposure** | This simulates the human eye adjusting to bright/dark areas. See also [Auto Exposure](/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine). |
| **Lens Flares** | Simulates the scattering of light when viewing bright objects through imperfections found in camera lenses. See also [Lens Flares](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#lensflare). |
| **Ambient Occlusion** | Approximates the attenuation of light due to occlusion. See also [Ambient Occlusion](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#ambientocclusion). |
| **Global Illumination** | Affects the indirect lighting contribution coming from Lightmass in order to alter a scene's brightness, color, or tint. See also [Global Illumination](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#globalillumination). |
| **Depth Of Field** | Applies a blur effect to a scene based on distance in front or behind a focal point. See also [Depth Of Field](/documentation/en-us/unreal-engine/depth-of-field-in-unreal-engine). |
| **Motion Blur** | Generates a Motion Blur effect that blurs objects based on its motion. See also [Motion Blur](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#motionblur). |
| **Misc** | Applies Blendables (screen overlays), sets Anti-Aliasing methods or Screen Percentage options for the Camera. See also [Blendables](/documentation/en-us/unreal-engine/blendables-in-unreal-engine), [Screen Percentage](https://www.fab.com/listings/017fabb0-78ac-400e-8c97-fafa226b73f0), or [Anti-Aliasing and Upscaling](/documentation/en-us/unreal-engine/anti-aliasing-and-upscaling-in-unreal-engine). |
| **Screen Space Reflections** | Alters the appearance of objects on the surface of Materials. Enabled by default. See also [Screen Space Reflection](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine#screenspacereflections). |
| **Activation** | Determines whether or not the Camera is automatically enabled. |
| **Tags** | Provides you with Tags to place on the Actor. |
| **Actor** | Displays information pertaining to the Camera Actor itself. |
| **Blueprint** | Allows you to turn the Actor into a Blueprint or add Events to the Level Blueprint for the Actor. |

For information on using Cameras for cinematic purposes, refer to [Cinematics and Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine) overview page. Additionally, the [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine) provides an excellent resource for a sample cutscene and how it was constructed.

Now that you have an understanding of how to place a Camera Actor in your level, the examples below provide some ways in which you can use the Camera, including how to use a Camera as a viewpoint for a player, how to use a Camera Component as part of an Actor class, how to use a Spring Arm Component with a Camera Component (typically used for creating Third Person perspectives), and how to switch between Cameras during gameplay.

## Implementation Guides