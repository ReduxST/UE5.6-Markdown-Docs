# Cinematic Depth of Field

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-depth-of-field-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-depth-of-field-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:04

---

The following depth of field methods provides a cinematic look that closely resembles photography and film for desktop and console platforms using the Deferred Shading renderer and Clustered Forward renderer.

## Cinematic

**Cinematic** DOF closely matches real-world cameras, similarly to Circle and Bokeh DOF, you can see circular-shaped Bokeh (out-of-focus areas) with sharp [High Dynamic Range](/documentation/en-us/unreal-engine/high-dynamic-range-display-output-in-unreal-engine) (HDR) content. This method uses a procedural Bokeh simulation that provides dynamic resolution stability and alpha channel support while being faster, scalable, and optimized for projects developing on desktops and consoles.

![Depth of Field Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f6cf3fb-259d-4211-9fba-2fe5bda60072/dof_cine_disabled.png)

![Cinematic Depth of Field](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e74c4893-eabb-48cc-b514-3843a8f753e9/dof_cine_enabled.png)

### Focus on the Shot's Subject

The key to achieving an aesthetically pleasing depth of field effect is all in how the subject(s) of the shot is focused. There are three core factors that affect setting up Depth of Field for any given shot:

-   Decide on the Lens **Focal Length** to use.
    
-   Choose an appropriate **Aperture** (f-stop number).
    
-   Choose a **Distance to your Subject(s)** from the camera.
    

Let's break down the elements that make up the camera and scene being captured to understand what's going on when we adjust these settings:

![Camera Elements Diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cda5fb6f-9634-4051-a422-b60a30c71c54/ue5_1-camera-elements-diagram.png)

1.  Points in the Scene
    1.  Red: Out of Focus
        
    2.  Blue: Perfectly in Focus
        
    3.  Green: Marginally in Focus
        
2.  Focus Distance to Shot's Subject (1. ii)
    
3.  Camera Lens
    
4.  Lens Diaphragm (measured in F-Stop)
    
5.  Lens Focal Length
    
6.  Filmback / Image Sensor
    
7.  Final Image Result

Take note that the rendered image on the right is inverted through the camera lens. Red is part of the background and more out of focus, and Green is part of the foreground and marginally out of focus.

Here we have the multiple points (1) representing objects captured by the camera to a defined **Focus Distance** (2), in this case, the blue subject. The **Aperture** (4) defines how blurred objects in the foreground and background will be that are not in focus, and, finally, the **Focal Length** (5) of the lens controls the field of view, or how zoomed in the image will be.

#### Aperture

The **Aperture** defines how sharp or blurred the foreground and background are based on the diameter of the **Diaphragm** which is controlled in f-stop.

![Camera Elements Aperture Diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/88a38445-714e-4510-a769-efb67c9d745c/cameraelements_aperturediagram.png)

1.  Camera Lens
    
2.  Lens Aperture Diaphragm measured in F-stop
    

This diagram demonstrates the **Diaphragm** (2) blocking light passing through the **Lens** (1). The size of the Aperture (or f-stop number) sets how much light passes through the Lens in turn controlling how much the foreground and background are blurred based on the Focus Distance of the shot.

Two elements make up the Aperture; the **F-stop** number and the **Diaphragm**.

![Camera Aperture Parts](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89956d56-0a7e-4a29-ac9c-1ea6c678db6c/ue5_1-camera-aperture-parts-1.png)

1.  The **Aperture** is the diameter of the opening through which light passes. The Aperture is defined by Focal Length divided by an **F-stop** number.
    
2.  The **Diaphragm** is a mechanical structure made up of multiple blades used to block light. It opens and closes based on the supplied F-stop.
    

The lens Aperture is defined by the diameter of the Diaphragm which decreases as the F-stop number increases controlling how shallow or deep the depth of field effect is. See [Focus Distance](/documentation/en-us/unreal-engine/cinematic-depth-of-field-in-unreal-engine#focusdistance) for a diagram showing this effect.

To demonstrate how the Aperture works, drag the slider to change the F-stop number between 1.4, 2.8, and 5.6. Smaller F-stop numbers create a shallower DOF with more background and foreground blur. Larger F-stops increase the depth of DOF with less blur.

Note that only the F-stop is being changed here, the Focus Distance and Focal Length remain constant at 7m and 75mm, respectively.

  ![Camera Element Aperture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ea092c8-1d2c-435f-af62-4cdb10186a7e/cameraelement_aperture_1_4.png) ![Camera Element Aperture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/70360590-ee0a-4433-a952-3a74db407aa0/cameraelement_aperture_2_8.png) ![Camera Element Aperture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7a024b97-a232-446f-aa76-ca4fecbce396/cameraelement_aperture_5_6.png)

Drag the slider to change the Aperture F-stop.

Normally when you would adjust the Aperture settings of a real camera, you'd have to also adjust the Exposure settings at the same time to maintain the same light intensity received by the filmback/image sensor. However, in Unreal Engine this is not a real camera, so adjusting the F-stop and Diaphragm does not control the light intensity.

#### Focal Length

The **Focal Length** is the distance from the center of the lens to the **Filmback** (or image sensor) measured in millimeters (mm).

![Focal Length Diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a268963-a489-403e-bd05-4593688c5dbe/cameraelements_focallengthdiagram.png)

1.  Camera Lens
    
2.  Focal Length
    

To demonstrate how this works, drag the slider to change the Lens Focal Length to be between 50mm, 75mm, and 100mm. Notice how effectively it changes the shot's Field of View (FOV); as the focal length increases, the FOV decreases. You can think of the focal length as being similar to zooming in with a camera, except when doing so, the out-of-focus areas of the shot in the background and foreground are becoming more pronounced. In the example below, you can see this when changing between a focal length of 50mm and 100mm; the shot appears mostly in focus throughout the foreground but when using a 100mm focal length, it's easier to see that the background is more out of focus and the foreground has a minimal amount of blur too.

Note that the diagram and example here are only changing the lens Focal Length; the Focus Distance and F-stop remain constant at 7m and f/2.8, respectively.

  ![Camera Elements Focal Length](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ce9a856-405c-425a-bd7d-878ee07302d5/cameraelements_focallength_50mm.png) ![Camera Elements Focal Length](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3037af21-e922-44d2-a5b4-7602425e9741/cameraelements_focallength_75mm.png) ![Camera Elements Focal Length](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40ebb7de-8a03-410c-8661-8e510f8bc1f2/cameraelements_focallength_100mm.png)

#### Focus Distance

The **Focus Distance** is the distance from the center of the camera lens to the subject of the shot that is put into focus, creating a focal plane. The closer the camera is to the subject, the more the background will end up out-of-focus.

![Focus Distance Diagram](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e12ee0a4-ba54-41f1-a3ff-39b0d3221e56/cameraelements_focusdistancediagram-1.png)

1.  Focal Points in the Scene
    1.  Red: Out of Focus
        
    2.  Blue: Perfectly in Focus
        
    3.  Green: Marginally in Focus
        
2.  Focus Distance to the Subject (1b)
    
3.  Camera Lens

This diagram demonstrates objects (1) that make up the scene; background, shot subject, and foreground. The distance from the Lens (3) to the focal subject (2) - in this case the blue dot - is the Focus Distance. Areas in the background and foreground are blurred depending on the F-stop used and the Lens Focal Length.

We can visualize the DOF Layers by using the **Show** dropdown in the **Viewport** to select **Advanced** \\> **Depth of Field Layers**. In this instance, Green represents the foreground objects, Black is the area where objects are focused, and Blue is part of the background.

![Rendered Scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67e83ea3-4f1f-4ea6-99dc-b262351c7959/ue5_1-1-depth-of-field-visualization-2.png)

![Depth of Field Layers Visualization](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a00b7038-a4f5-46a3-8eb9-efaab2a7f1d0/ue5_1-1-depth-of-field-visualization-1.png)

To demonstrate how this works, drag the slider to change the Focus Distance between 4m, 7m, and 10m. Adjusting the Focus Distance adjusts the Focal Plane (purple dotted line) in the scene, indicating where the in-focus region of the shot is. The blue reference point in the diagram uses the Character as the focal subject here, so as the camera shifts shot focus (black/gray area above) to different parts of the scene, objects in the foreground and background will shift too. Starting with 4m, the Police car in the foreground is in sharp focus and the character is out of focus in the background. The blue reference in the diagram indicates this with its focal point intersection in front of the filmback. At 7m, the character is completely in focus with background and foreground objects out of focus. At 10m, the construction barriers are in sharp focus and the character and a Police car are out of focus in the foreground. The blue reference in the diagram indicates this since the intersection point extends beyond the filmback. Through all these Focus Distance changes, the DOF effect increases or decreases depending on an object being in the foreground or background.

Note that only the Focus Distance is being changed here; the F-stop and Focal Length remain constant at f/1.4 and 75mm, respectively.

  ![Focus Distance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d5cdc7b4-8721-473a-a906-84e9b5430c22/focusdistance_4m-2.png) ![Focus Distance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/11b3f63e-42f3-4f40-b300-8ebb05a35bf6/focusdistance_7m-2.png) ![Focus Distance](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3491471c-323f-4372-a425-dc21a62c9a22/focusdistance_10m-3.png)

### Procedural Diaphragm Simulation

The job of Depth of Field is to apply focal importance to a subject(s) in your scene. Just as importantly, out-of-focus areas can be as important. Unreal Engine 4's depth of field simulates the lens diaphragm by enabling you to aesthetically control the shape of the Bokeh (out-of-focus areas) by adjusting the number and curvature of diaphragm blades.

![Depth of Field Shot](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e72a2b8-503b-4d9a-ab0d-84ab227f4849/dofshot3.png)

For performance reasons, the diaphragm simulation is only supported on Engine Scalability settings of Epic and Cinematic. Lower quality settings will fall back to circle Bokeh shapes of equal area to ensure similar behavior with auto exposure functionality, in turn disabling the diaphragm blade simulation.

#### Number of Diaphragm Blades

The **Diaphragm** (or Iris) is a mechanism made up of blades that can adjust to aesthetically inform the look of Bokeh shapes. Using a lower number of blades will result in a polygon-shaped diaphragm whereas a higher number of blades improves the curvature of the diaphragm to appear more natural with rounded out-of-focus Bokeh.

   ![Blades](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dd70693-8d53-4b7e-a4d2-27da34469ebf/blades_4-2.png) ![Blades](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5347f8d4-ef6b-4e87-8964-19ed80208c96/blades_5-2.png) ![Blades](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dbdb892-eb14-48b4-ba0a-61a76485b292/blades_8-2.png) ![Blades](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7269114-5558-409a-9d52-aa586e6ccb89/blades_16-2.png)

The number of diaphragm blades directly influences the shape of the Bokeh when the [Maximum Aperture](http://www.linktomaxaperturesectionofpage.com) is increased (minimum F-stop number is decreased).

   ![Diaphragm Zoomed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/67cbba1c-7160-446c-b290-f727d3ef8a7f/diaphragm_4_zoomed-1.png) ![Diaphragm Zoomed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5edac95-5b89-4da2-b053-55a228c9e641/diaphragm_5_zoomed-1.png) ![Diaphragm Zoomed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/edf70128-a4a6-4e3b-a9c9-246612d3924a/diaphragm_8_zoomed-2.png) ![Diaphragm Zoomed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4fb6d6c-b8f3-4b57-8840-98ad5f496c6b/diaphragm_16_zoomed-3.png)

#### Aperture and Max Aperture

The **Aperture** is the opening of the lens controlled by the diameter of the **Diaphragm** which is measured in **F-stops**. The amount of light allowed to pass through the lens is controlled by the size of the aperture. Adjusting the size of the aperture sets the focal plane to adjust how in-focus or out-of-focus areas outside of the focal region are.

The following chart shows the correlation between aperture size (f-stop number), max aperture (min f-stop number), and depth of field effects.

![Aperture Range](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/37e2965c-d764-4302-abf2-513c2ff007eb/aperturerange.png)

A larger aperture (lower f-stop number) has a shallow focal region, causing the foreground and background to become more out-of-focus. A small aperture (higher f-stop number) has a deeper focal region that includes more objects in focus in the foreground and background.

     ![Aperture Stop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b7de759-8e04-4ebb-bd57-dc6de3f8344f/aperturestop_1_4.png) ![Aperture Stop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9ec5d08e-f553-4a9b-94ec-9ae6c61386ec/aperturestop_2_0.png) ![Aperture Stop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35df655a-f7dc-4e59-9ab3-6ed9a0609162/aperturestop_2_8.png) ![Aperture Stop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/51c9b5db-9455-4821-98fb-106ee48e4d90/aperturestop_4_0.png) ![Aperture Stop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6f1e99cd-a7df-469b-ab1f-615e0b64c470/aperturestop_5_6.png) ![Aperture Stop](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4cb02440-b181-4879-b565-d1c60ec5d5b5/aperturestop_8_0.png)

Aperture F-stops: 1.4, 2.0, 2.8, 4.0, 5.6, 8.0

While the Aperture can be as small as you'd like, it can only ever be as large as the maximum size of the lens. The **Maximum Aperture** (measured in f-stop) defines how large the lens can be. This also defines the curvature of the blades that make up the diaphragm by limiting the size that the aperture can open; limiting the size of the aperture shortens the effective focal region which limits how out-of-focus areas can be.

   ![Max Aperture And Bokeh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/601c8c0e-043e-44d7-8e83-c5ef4835e7f6/maxapertureandbokeh_1_4.png) ![Max Aperture And Bokeh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59440c54-c5a9-4d91-8d42-8db193e0955a/maxapertureandbokeh_2_0.png) ![Max Aperture And Bokeh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de6b5203-7142-474c-a423-0c0a4cbef8fa/maxapertureandbokeh_2_8.png) ![Max Aperture And Bokeh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f93aa64e-9aaa-4e3b-8b71-d0737365c9ab/maxapertureandbokeh_4_0.png)

5 Diaphragm Blades with Different Max Aperture Values

In this example, the **Number of Diaphragm Blades** is set to 5. With a smaller Aperture, the blades of the diaphragm become more visible in the Bokeh shapes. Using a larger Aperture (f-stop is equal to minimal f-stop) the Bokeh shapes will begin to become circular.

In this example, a Cine Camera Actor is being used with the following values:

-   **Min F-Stop**: 1.4
    
-   **Max F-Stop**: 4.0
    
-   **Diaphragm Blade Count**: 5
    
-   **Current Aperture**: 1.4 - 4.0
    

With these values, the F-stop can only accept values between **1.4** and **4.0**. As the depth of field effect is deepened with a larger F-stop (smaller aperture), the diaphragm blades become more visible in the Bokeh shapes.

Keep in mind that the aperture is not controlling the light intensity. This choice has been made so that you don't have to continually adjust the exposure at the same time as with a real camera.

### Cinematic DOF Settings

#### Cinematic Camera

The following settings are specific to the [Cinematic Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine). Note that you have access to the Camera and Depth of Field settings as well.

| Property | Description |
| --- | --- |
| Filmback |   |
| **Sensor Width** | Sets the horizontal size of the filmback or digital sensor (measured in millimeters (mm)). |
| **Sensor Height** | Sets the vertical size of the filmback or digital sensor (measured in millimeters (mm)). |
| **Sensor Aspect Ratio** | Read-Only. Computed from Sensor dimensions. |
| Lens Settings |   |
| **Min Focal Length** | Sets the minimum focal length for the lens (measured in millimeters (mm)). |
| **Max Focal Length** | Sets the maximum focal length for the lens (measured in millimeters (mm)). |
| **Min FStop** | The maximum aperture for this lens. For example, 2.8 for an f/2.8 lens. This will also define the curvature of the blades of the diaphragm. |
| **Max FStop** | The minimum aperture for this lens. For example, 8.0 for an f/8.0 lens. |
| **Diaphragm Blade Count** | The number of blades that make up the diaphragm mechanism. |
| Focus Settings |   |
| **Focus Method** | 
Select the camera focus method to use: 

-   **None:** Disables DOF entirely.
    
-   **Manual:** Allows for specifying or animating exact focus distances.
    
-   **Tracking:** Locks focus on a specific object in the shot.
    



 |
| **Manual Focus Distance** | Set the manually-controlled focus distance. This is only available when the **Focus Method** is set to **Manual**. |
| **Draw Debug Focus Plane** | Enable to draw a translucent plane at the current focus depth. This enables a visual way to track where the focus is for the shot. |
| **Debug Focus Plane Color** | When this setting is enabled, it sets a color for **Draw Debug Focus Plane.** |
| **Smooth Focus Changes** | Enable this to use interpolation to smooth out changes in focus distance. When disabled, the focus changes will be instantaneous. |
| **Focus Smoothing Interp Speed** | Controls the interpolation speed when smoothing focus distance changes. This option is ignored if **Smooth Focus Changes** is not enabled. |
| **Focus Offset** | This adds offset to focus depth which can be used to manually tweak focus if the chosen focus method needs adjustment. |
| **Current Focal Length** | Controls the current focal length of the camera which controls the field of view (FOV) and zoom. |
| **Current Aperture** | Sets the current aperture size based on an f-stop number. Note that this setting only accepts values that are within the **Min FStop** and **Max FStop** range. |
| **Current Focal Distance** | Displays a read-only value that is used by the **Focus Settings**. |
| **Current Horizontal FOV** | Displays a read-only value that is used by **Current Focal Length** and **Filmback Settings**. |

#### Post Process Volume and Camera Actor

The following settings are available with the [Cine Camera Actor](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine), [Camera](/documentation/en-us/unreal-engine/movie-and-cinematic-cameras-in-unreal-engine), and [Post Process Volumes](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine).

| Property | Description |
| --- | --- |
| Camera Settings |   |
| **Shutter Speed (1/s)** | The camera shutter in seconds. |
| **ISO** | The camera sensor sensivity. |
| **Aperture (F-stop)** | Defines the opening of the camera lens. The aperture is 1/f-stop with a typical lens going down to f/1.2 (larger opening). Larger numbers will reduce the DOF effect. |
| **Maximum Aperture (minimum f-stop)** | Defines the maximum opening of the camera lens to control the curvature of the diaphragm. Set this to 0 to get straight blades. |
| **Number of Diaphragm Blades** | Defines the number of blades of the diaphragm within the lens. Values between 4 and 16 can be used. |
| Depth of Field Settings |   |
| **Focal Distance** | The distance in which the depth of field effect should be sharp. This value is measured in Unreal Units (cm). |
| **Depth Blur km for 50%** | Defines the distance at which the pixel is blurred with a radius half of the Depth blur Radius. This is particularly useful to emulate cheap atmospheric scattering. |
| **Depth Blur Radius** | Radius in pixels at 1080p resolution to apply according to distance from the camera to emulate atmospheric scattering. |

### Useful Console Variables for Optimization

The challenge of DOF is that it can vary depending on your content and how much importance has been given to the artistic direction of your game with DOF. With that in mind, the DOF implementation offers a variety of console variables ready to be customized per platform for developers to better control the performance budget allocated. 

Below are some console variables that can be useful for binding Cinematic DOF performance.

-   **r.DOF.Kernel.MaxBackgroundRadius:** The maximum size of the background blurring radius in horizontal screen space.
    
-   **r.DOF.Kernel.MaxForegroundRadius:** The maximum size of the foreground blurring radius in horizontal screen space.
    
-   **r.DOF.Scatter.MaxSpriteRatio:** The maximum ratio of scattered pixel quads as sprites. Useful to control DOFs scattering upper bound.
    

Note that these are a good starting point and additional console variables can be found under **r.DOF.**\*.

## Bokeh DOF Method (Legacy)

As of Unreal Engine 4.23, Bokeh DOF has been removed from Unreal Engine and the source code. If using 4.22 and 4.21, Bokeh DOF has been deprecated for the Deferred Desktop Renderer and the Forward Rendering path.

**Bokeh** DOF refers to the name of the shape that can be seen in photos or movies when objects are out of focus. This method renders a textured quad for each pixel using a user-specified texture to define a shape with which to reproduce the effect of a camera lens.

The implementation only uses half-resolution to perform this intensive effect. It attempts to save render performance in areas where the effect is not noticeable by using Adaptive Depth of Field. Bokeh DOF is more costly than other DOF methods available in Unreal Engine making this a prime candidate for cinematics and showcases where appealing visuals often outweigh any performance concerns in those situations.

![Depth of Field Disabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8e1604fb-32bd-43a5-b348-3febb1097e8b/dof_bokeh_disabled.png)

![Bokeh Depth of Field Enabled](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48919fdb-ef82-428e-a81f-48b8cda65e9f/dof_bokeh_enabled.png)

### Adaptive Depth of Field for Bokeh DoF

Bokeh DOF is rendered at quarter resolution (half resolution in each direction) by default for performance reasons. In most cases, the downsampling is barely noticeable, which is perfectly acceptable; however, in some situations, it can lead to artifacts and unwanted results. Adaptive Depth of Field resolves these types of artifacts where possible.

![Adaptive DOF without Downsampling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f7fc830e-3022-4c4d-a227-37c1a9e0d3d9/dof_adaptive_0.png)

![Adaptive DOF with Downsampling](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/076d16aa-abc7-4cca-8b5a-9341aced4fca/dof_adaptive_1.png)

The characters being blurred in the background appear blocky when using only the downsampled DOF technique. Also, some artifacts appear around the horns of the character in the foreground. Adaptive DOF eliminates these types of artifacts, and the background characters have a much smoother appearance.

Adaptive DOF can be visualized by using the **Adaptive Depth of Field** to show the flag in the Level Viewport under **Show** \\> **Visualize**. When enabled, an overlay is shown where the downsampled effect is being used (green) and where the full-resolution effect is being used (red). The regular scene color is shown where no blurring is being applied.

![Depth Of Field Adaptive Vesualize](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b1d1c70d-08b0-4b4c-9993-cd3c40904084/dof_adaptive_visualize.png)

In general, you want the Adaptive DOF to display all green. The more red shown by the visualization, the more expensive the scene is to render each frame.

![Adaptive DOF mostly optimized](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e39ded2-ccc7-4388-bf07-d59fd9cabdf3/dof_adaptive_good.png)

![Adaptive DOF unoptimized ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80cf0425-d71e-4593-bfd5-16f1ed813623/dof_adaptive_bad.png)

### Bokeh DOF Settings

The following settings are available with the Cine Camera, Camera, and Post Process Volumes, located under the Lens tab in the Depth of Field section.

| **Property** | **Description** |
| --- | --- |
| **Focal Distance** | The distance in which the depth of field effect should be sharp. This value is measured in Unreal Units (cm). |
| **Near Transition Region** | The distance in Unreal Units from the focal region on the side nearer to the camera over which the scene transitions from focused to blurred when using Bokeh or Gaussian DOF. |
| **Far Transition Region** | The distance in Unreal units from the focal region on the side farthest from the camera over which the scene transitions from focused to blurred when using Bokeh or Gaussian DOF. |
| **Scale** | An overall scaling factor for Bokeh-based blurring. |
| **Max Bokeh Size** | 
The maximum size (in percent of the view width) of the blur for the Bokeh-based DOF.

Note that performance scales with the size.



 |
| **Shape Texture** | 

A texture that defines the shape of the Bokeh when objects get out of focus.

Note that these cannot be blended with other Post Process Volumes.



 |
| **Occlusion** | Controls how much the blurred geometry extends beyond its usual silhouette and its opacity. A value of 0.18 gives a fairly natural occlusion result. A value of 0.4 may be necessary to solve layer color leaking issues. Very small values (less than 0.18) generally result in negating the blur effect, though can work well when objects are very near to the camera. |
| **Color Threshold** | Controls the threshold where adaptive DOF switches to using full resolution based on color. Smaller values cause more of the scene to use full-resolution processing. |
| **Size Threshold** | Controls the threshold where adaptive DOF switches to using full-resolution based on size. Larger values cause more of the scene to use full-resolution processing. |

## External Resources

-   [SIGGRAPH 2018 - "A Life of a Bokeh" by Guillaume Abadie](https://epicgames.box.com/s/s86j70iamxvsuu6j35pilypficznec04) (PowerPoint presentation ~150 Mb)
    
-   [Diaphragm (Optics)](https://en.wikipedia.org/wiki/Diaphragm_\(optics\))
    
-   [Aperture](https://en.wikipedia.org/wiki/Aperture)
    
-   [F-Number](https://en.wikipedia.org/wiki/F-number)
    
-   [Understanding Factors that affect Depth of Field](https://photography.tutsplus.com/articles/understanding-the-factors-that-affect-depth-of-field--photo-6844)