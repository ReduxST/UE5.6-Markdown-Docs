# In-Camera VFX Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:44

---

**In-Camera VFX** is an exciting new methodology for shooting real-time visual effects during a live action film shoot. This technique relies on a mixture of LED lighting, live camera tracking, and real-time rendering with off-axis projection to create a seamless integration between foreground actors and virtual backgrounds. Its primary goal is to remove the need for green screen compositing to produce final pixel results in camera. One of the challenges of producing high- quality, real-time visual effects is synchronizing the technology to execute everything simultaneously.

**Unreal Engine** supports this technique through multiple systems such as nDisplay, Live Link, Multi-User Editing, and Remote Control. This documentation covers the features needed for this workflow, and what to consider when creating your set for an in-camera VFX shoot.

![A set using in-camera VFX within a LED volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10cb0f39-7e14-4154-aff3-c13f9d7ba0bf/image_0.png)

A set employing in-camera VFX within a LED volume. The arrows mark the camera's inner frustum, which is rendered from the camera's perspective.

The image above shows a set employing in-camera VFX within an immersive **LED volume**. The picture-in-picture indicated on the main LED wall shows the camera view, called the **inner frustum** render of the camera. This inner frustum represents the field of view (FOV) from the camera's perspective based on the current lens focal length. The image shown in the inner frustum tracks with the physical camera as the camera moves within the scene, always displaying what the virtual equivalent of the camera should be seeing in the Unreal Engine environment. When viewed through the real world camera, the system creates a parallax effect that gives the impression of shooting at a real world location, utilizing the full virtual 3D world as opposed to using a flat background plate.

Content displayed on the LED volume outside of the camera's FOV is called the **outer frustum**. This outer frustum turns the LED panels into a dynamic light and reflection source for the physical set because they surround the set with the virtual world and illuminate it as if it were a real world location. The outer frustum remains static when the camera moves. This mimics how lights and reflections do not move with the camera in the real world. Each shot setup can be placed at the desired location within the Unreal Engine environment and dictate what the outer frustum renders to light the scene on stage.

## LED Panels

The LED stage design and its intended use is integral to the in-camera VFX setup. The number of panels in an LED volume that are needed and how they are laid out drives the rest of the hardware setup. LED panels can be placed in an arc pattern around the actor to provide better ambient lighting and reflections. It is also useful for providing an LED ceiling to contribute to the ambient lighting and reflections on the overall scene. Productions that intend to create a fully virtual environment may require at least a 270-degree enclosed volume to achieve accurate set lighting and reflections. If a substantial part of the set is a physical build, and the virtual world is only needed for a portion of the set, such as for set windows, then a one-sided or curved wall can be considered. Other factors, including production budget, physical space constraints, and, in some cases, the availability of panels from the manufacturer, may also impact the LED stage design.

![A view of the cabinets behind the LED volume](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/427ec713-1a7b-4acc-ab57-b6e0537c34e5/image_1.png)

An LED Volume is made up of an array of cabinets that can be arranged in any configuration. This image shows the back of an LED volume.

An LED volume is made up of a cluster of **cabinets**. Each cabinet has a fixed resolution that can range from a very low resolution, such as 92x92 pixels that can be used for outdoor signs, to 400x450 pixels for ultra-high-resolution indoor displays. The physical size of each cabinet can vary from manufacturer to manufacturer.

The **LED processor** is the hardware and software that combines multiple cabinets into an array that displays a single image. You can arrange the cabinets in any configuration inside the canvas that the LED processor drives. On a large LED stage, there could be ten or more LED processors driving a seamless LED wall.

**Pixel pitch** describes the density of the pixels in a cabinet and correlates with its overall resolution. The pixel pitch is typically described in millimeters and represents the distance between each LED light. The closer the LEDs are together—the lower the pitch—the higher the pixel density. A higher pixel density means a noticeable increase in resolution and quality—and higher cost for each cabinet.

A cabinet with a lower pixel pitch does not ensure it will be the correct product for your production, as other factors, such as viewing angle, color shift, color consistency, and heat dissipation, must also be considered. You can consult a professional LED systems integrator to determine the best product for your production.

![A moiré pattern on the LED wall](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f839c627-9ff3-4a0c-87cc-3a2e7b264b6d/image_2.png)

You can see the optical artifact, the moiré pattern, appearing on the LED wall in the left side of this image.

The combination of the distance from the screen, pixel pitch, and camera sensor size will help you determine how far away you should shoot your subject from the LED wall without seeing any visible artifacts. One visual artifact that is present when shooting on LEDs is the **moiré pattern**. A moiré pattern is a common optical artifact that appears when the display system and camera sensor pixels are slightly offset. Moiré patterns can appear when the camera's focus plane aligns with the LED panels in 3D space. It is recommended to have the camera's focus placed either in front or behind the LED surface so that the image is slightly out of focus. Moiré patterns can also appear more commonly at severe angles to the LED surface. Try to maintain a perpendicular angle of the camera to the LED's surface where possible.

## Hardware

An example hardware layout with three render nodes. Click image for full size.

In-Camera VFX can require a complex network of connected devices with various functions on a film set. The diagram shows an example hardware layout for a set with three LED panels. The table below explains the roles of the various machines in the setup. For details on specific hardware to consider for your in-camera VFX production, see [In-Camera VFX Recommended Hardware](/documentation/en-us/unreal-engine/recommended-hardware-for-in-camera-vfx-in-unreal-engine).

| Device | Description |
| --- | --- |
| Master Clock | The Master Clock is the heartbeat of the system. It ensures that all devices that receive or record data are in sync throughout the shoot. |
| Network | It is highly recommended to have a protected LAN with high throughput for all the machines. |
| nDisplay Render Nodes | Each render node drives a part of the LED volume. This means each node requires an NVIDIA GPU along with an NVIDIA Quadro II Sync card. |
| UE Primary | This station is the primary operator workstation where stage setup is typically configured. It also runs additional applications for launching the nDisplay cluster, the Remote Control Web Application, and the Multi-User server. |
| UE Editor—(Tech Art) | This workstation is in the Multi-User session for an artist to make creative real-time scene adjustments while a more stage-oriented operator keeps things running on the primary machine. |
| UE Record | This workstation records the camera, lights, and prop changes during the shoot using Take Recorder. |
| UE Composite | This workstation renders live composites in Composure. It is optional for the setup. |
| UE VR Scouting | This workstation has a VR headset and scouts the environment during a shoot. This can be useful on set both during the film shoot and separately. |
| Perforce Proxy | The Perforce Proxy is an on-site fast connection to the outside Perforce server. |
| Remote Control Web App | This is a web app written with HTML, CSS, and JavaScript frameworks that can remotely control the scene from a tablet or device with a web browser. |
| Camera Tracking | Camera tracking can involve optical, feature, or mechanical tracking to derive the camera's 3D position. This setup can include a small PC or server provided by the tracking company. |
| Camera | This is the Digital Cinema Camera on set and can be paired with the camera-tracking system. |
| Video Village | This is the center for video playback and review. |

## Camera Tracking

![On-stage shot of the camera used for an in-camera VFX production](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2eb8824b-62f5-4127-a9d9-56c74c90a648/image_4.png)

Camera tracking is needed to relay the position and movement of the camera from the real world to the virtual world. With this technology, the correct perspective of the production camera is rendered relative to the virtual environment. There are several different methods available for camera tracking with in-camera VFX.

Some of the most common methods for camera tracking include:

-   **Optical Tracking:** Optical tracking systems leverage specialized IR-sensitive cameras to track either reflective or active IR markers, in order to determine the location of the production camera.
    
-   **Feature Tracking:** Instead of tracking the custom markers that optical tracking systems use, feature tracking involves identifying specific image patterns of real-world objects as the tracking source.
    
-   **Inertial Tracking:** Inertial Measurement Units (IMUs) contain a gyroscope and accelerometer to determine the position and orientation of the camera. IMUs are frequently used with both optical and feature-tracking systems.
    

Using multiple sources for measuring the camera position and orientation, such as optical tracking combined with inertial tracking, is recommended for in-camera VFX. Multiple sources can enhance the overall camera-tracking data compared to using any single technique.

### Live Link

Live Link is a framework in the Unreal Engine for ingesting live data, including cameras, lights, transforms, and basic properties. For in-camera VFX, Live Link plays a critical role in distributing the tracked camera information and can be enabled to work with nDisplay to carry the tracking information to each cluster node. Unreal Engine supports many camera-tracking partners through Live Link, such as Vicon, Stype, Mo-Sys, and Ncam, as well as several other professional tracking solutions. For more information, see [Live Link Plugin](/documentation/en-us/unreal-engine/live-link-in-unreal-engine).

### Camera Calibration

Creating accurate compositions from CG renders and live video requires a virtual camera in Unreal Engine that accurately simulates the physical camera used to capture the real-world video footage. The virtual camera's position and orientation must closely match that of the physical camera, and its tracking information must match the video feed's exact timing to ensure each video frame is accurately synced to the position of the camera for each moment in time.

The Camera Calibration plugin provides users with simplified tools and workflows to calibrate a camera and lens in the Editor. This calibration process generates the data necessary to accurately align the virtual camera with the physical camera's position in space, and to model the lens distortion of the physical camera. The plugin introduces the Lens File asset type which encapsulates all of the calibration data for the camera and lens.

The Camera Calibration plugin also includes a robust lens-distortion pipeline that takes the calibrated distortion data and applies an accurate post-process effect to the CG render. The distortion post-process effect can be applied directly to a [Cinecamera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine), which can be used in [Movie Render Queue](/documentation/404), or to the CG layers of [Composure](/documentation/en-us/unreal-engine/real-time-compositing-with-composure-in-unreal-engine).

The plugin's tools and framework are extensible and flexible to support a wide range of lenses and workflows.

For more information, refer to [Camera Calibration](/documentation/en-us/unreal-engine/camera-lens-calibration-in-unreal-engine).

## Timecode and Genlock for In-Camera VFX

On an in-camera VFX film set, it is very important to have highly accurate synchronization between all devices. Each device, such as the camera, computers, and tracking systems, has an internal clock. Even though two devices may be exactly the same, their internal clocks will not be in sync with each other. This can cause problems in the resulting display, such as tearing, if they are not unified. Genlocking with nDisplay prevents these issues. For more information on synchronization and genlock in nDisplay, see [Synchronization in nDisplay](/documentation/en-us/unreal-engine/synchronization-in-ndisplay-in-unreal-engine).

In addition to synchronizing the displays, the engines' timecode and frame generation need to match the input from the camera. See [Timecode and Genlock](/documentation/en-us/unreal-engine/timecode-and-genlock-in-unreal-engine) for steps on how to sync the timecode and genlock the engine between all the devices.

When constructing an environment for in-camera VFX, it is important to note that nDisplay has certain limitations that need to be taken into consideration. Screen spaced effects such as SSGI, SSAO, SSR, vignetting, eye-adaptation, and bloom should be avoided. Since the nature of these effects are screen spaced, there can be issues with borders between two clustered nodes in the nDisplay system.

## Multi-User Editing for In-Camera VFX

![Two images that show perspectives of someone in VR Scouting and from the camera in a Multi-User session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bcf68317-61aa-49b9-b37a-2d6a8be4fe1f/image_5.png)

The left image is the view from a machine dedicated to VR Scouting in a Multi-User session. The right image shows the LED wall displaying the camera's perspective and the representation of the user VR Scouting.

The **Multi-User Editing** system enables robust collaboration to support any type of change. The primary operator machine is in charge of scene modifications and updates the nDisplay render machines live. You can have multiple operator machines in the same Multi-User session that can perform different tasks and modify the scene in real-time. Examples of machines are ones dedicated to VR Scouting and live compositing with Composure. One machine runs the Multi-User server, and all others machines connect to the server. Any scene changes from these machines are then sent as transactions from the server to all the other machines. Conceptually, any action that can be *undone* in the engine is transacted and sent through the Multi-User server.

For information on adding Multi-User Editing to your project, follow the instructions in [Getting Started with Multi-User Editing](/documentation/en-us/unreal-engine/getting-started-with-multi-user-editing-in-unreal-engine). When automatic server discovery is not possible in your network, follow the steps in [Advanced Multi-User Networking](/documentation/en-us/unreal-engine/advanced-multi-user-networking-in-unreal-engine).

## Live Compositing

![An in-camera VFX set showing the green screen in the camera's view but still using the LED walls for lighting and reflections](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0ed1f3e4-5325-4649-8688-0fcb0727a528/image_6.png)

A set with the green screen visible only in the camera's view. The outer frustum still displays the renders from the Unreal Engine environment for lighting and reflections.

For shots that can't quite be achieved as in-camera finals, the system provides a fallback option. The inner frustum can be easily changed to a green screen with adjustable tracking markers. The outer frustum can continue to display renders from the Unreal Engine environment.

![Two images of the shot with green screen and after compositing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b353c4fb-403d-4214-8af8-4ed4271c4e99/image_7.png)

Since this set used the LED walls in the outer frustum for ambient lighting and reflections, you can see the real world reflections visible in both the motorcycle and the actor's glasses even though the background in the final shot is composited.

Using a green screen only in the camera's FOV minimizes the amount of green screen required for a given shot. Less green screen means less green spilling onto the actors and set. Continuing to display renders from the Unreal Engine environment on the outer frustum allows the production to still take advantage of the real world lighting and reflection capabilities of in-camera VFX. Both contribute to improved green-screen elements for compositing.

Green-screen shots also benefit from live compositing, which allows filmmakers and performers to get a fuller sense for what the final shot is going to be as opposed to the classic sea of green. These comps can also be very valuable as preview shots for editorial.

**Composure** is Unreal Engine's framework for real-time compositing. With this suite of features, you can include live video feeds, AR compositing, green-screen keying, garbage mattes, color correction, and lens distortion in your shots. Composure is a flexible system where you can extend and create your own material effects. For more, see [Composure](/documentation/en-us/unreal-engine/real-time-compositing-with-composure-in-unreal-engine).

## Remote Control for In-Camera VFX

Since there can be so many machines involved in an in-camera VFX shoot, controlling the scene in real time from a web app can be useful on set. For example, you can change the color correction, lighting, and virtual actor positions from the web app. Included in the In-Camera VFX Example Project is a sample Remote Control Preset and Web Application to show how you can incorporate this technology into your production workflow. In addition to using the Remote Control Presets, you can also use the UI builder to customize the controls to suit your project's requirements. For more information about Remote Control in Unreal Engine, refer to [Remote Control](/documentation/en-us/unreal-engine/remote-control-for-unreal-engine).

![A production remotely controlling the scene with a web app to change the background](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b9714db-3a43-414a-ac6f-a751ff571b3d/image_8.png)

A remote control can be helpful on set to adjust the scene for the shot. In this set, a web app was used to change the sky during the shoot.

## Color Considerations

Ensuring color consistency between shots is important during an in-camera VFX shoot. It is good practice to verify the final image by looking through the live action camera, and to test with the LED panels displaying the outer frustum as a light source.

Follow these best practices to ensure consistency between shots:

-   All cameras do not produce the same outputs. Using different cameras between shots can cause the color in the resulting captures to be different. Avoid this by using the same cameras throughout a film shoot with a LED volume.
    
-   Test live action assets on stage with the visuals on the LED volume as a light source. Light from the LED panels can have a different effect on stage elements from other lights.
    
-   Ensure that the tonemapper is disabled so content from the engine does not have a tone curve and is in linear sRGB color space as input to the LED panels. The tonemapper can be disabled using the console command **ShowFlag.Tonemapper 0**.
    

### OpenColorIO

[OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine), or OCIO, is a color management system used primarily in film and virtual production. OCIO guarantees that the colors of captured video remain consistent through the entire film pipeline. This pipeline includes from initial camera capture, through all the compositing applications that need to work with the captured media, all the way to the final render.

OCIO is available as a plugin in Unreal Engine. When the plugin is enabled, you can apply OCIO profiles to the Editor, or to individual displays with nDisplay. Refer to [Color Management in nDisplay](/documentation/en-us/unreal-engine/color-management-in-ndisplay-in-unreal-engine) for more information.

## Stage Monitor

When operating a stage in a live environment, multiple machines running instances of **Unreal Engine 4** work in tandem and rely on each other. Operators may use some instances to render on a LED wall, some could be used to modify the scene in the Editor, and others may be used for compositing. With **Stage Monitor**, you can receive reports of different events from all these instances of UE4 and be able to troubleshoot any issues in the setup.

For more information, refer to [Stage Monitor](/documentation/en-us/unreal-engine/stage-monitor-with-unreal-engine).

## Timed Data Monitor

Unreal Engine can ingest a variety of data types from multiple sources at the same time. For example, in Virtual Production, the engine can receive captured frames from the camera on SDI as well as the position and orientation of the camera from the tracking system through Live Link. The **Timed Data Monitor** is a solution to configure and visualize how all this incoming timed data relates to each other and the engine's time.

For more information, refer to [Timed Data Monitor](/documentation/en-us/unreal-engine/timed-data-monitor-in-unreal-engine).

## Level Snapshots

**Level Snapshots** enable you to save a particular configuration of the **Actors** in the **World Outliner** of your Level and instantly restore your scene to that state. This can dramatically streamline complex setups and avoid duplication and management of multiple variations of the same Level for different scenarios. Level Snapshots are especially useful for Virtual Production, as they enable users to reset virtual environments to their starting position between takes as well as track per-shot changes that may occur during a shoot while preserving the base starting point of the Level.

You'll want to use a combination of Source Control and Level Snapshots to version both the Assets and Actors in your project. For more details on how to use Level Snapshots, see [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine).

## In-Camera VFX Example Project and Template

This page provided an overview of the technologies and hardware needed for in-camera VFX. To become more familiar with the workflow, the [In-Camera VFX Example](https://www.fab.com/listings/1ccaf0a1-acce-4a3b-831e-a9cf4af35f6d) project is available with a sample scene and a base level to start your in-camera VFX project with. See the [In-Camera VFX Quick Start](/documentation/en-us/unreal-engine/in-camera-vfx-quick-start-for-unreal-engine) for steps on how to modify the example project for a different LED volume and run the necessary programs on all the machines. If you are aleady familiar with using In-Camera VFX, the [In-Camera VFX Template](/documentation/en-us/unreal-engine/in-camera-vfx-template-in-unreal-engine) provides a basic set-up with all the tools and assets to create a project from the beginning.

## In-Camera VFX Production Test

The [In-Camera VFX Production Test](https://www.fab.com/listings/17ce3d9c-0843-48ff-96d6-3f49a7163dbd) is a Virtual Production sample available in Fab that uses Unreal Engine and an LED Volume to feature traveling vehicle shots, multi-camera setups, and multi-user setup for making quick changes between takes. This sample was created in collaboration with filmmakers' collective [Bullitt](https://bullittbranded.com/). The team produced final pixels in-camera over four days on [NantStudios](https://www.nantstudios.com/)' LED stage in Los Angeles.

For more information on the production and the technologie used, refer to [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine).