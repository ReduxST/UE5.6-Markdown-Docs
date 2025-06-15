# Cine Camera Actor

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:59

---

The **Cine Camera Actor** is a specialized **[Camera Actor](/documentation/en-us/unreal-engine/camera-actors-in-unreal-engine)** with additional settings that replicate real-world film camera behavior. You can use the **[Filmback](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#filmback)**, **[Lens](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#lenssettings)**, and **[Focus](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#focussettings)** settings to create realistic scenes, while adhering to industry standards.

## Create a Cine Camera Actor

There are several ways to add a **Cine Camera Actor** to your level: [Place Actors](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#placeactors), [Quick add](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#quickadd), and **[Sequencer](/documentation/en-us/unreal-engine/cinematics-and-movie-making-in-unreal-engine)**.

### Place Actors

To use Place Actors:

1.  From the main menu, go to **Window** and select **Place Actors**.
2.  In the **Cinematic** section, drag a **Cine Camera Actor** into your level.
    
    ![Place Cine Camera Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/523360f9-392a-44f6-9d18-d2dcc261b7fd/place_cine_camera_actor.png)

### Quick Add

To use Quick Add:

1.  In the **Main Toolbar**, click **Quickly add to the project**.
2.  Select **Cinematic** from the drop down menu.
3.  Select **Cine Camera Actor**.

![Quick add a Cine Camera Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/59b55c10-5495-449d-9e1f-61e61fbe4a0e/quick_add_cine_camera.png)

### Sequencer

If you are using **Sequencer**, you can create a **Cine Camera Actor** by clicking the **Camera** button in Sequencer's toolbar. This action creates a temporary **[Spawnable](/documentation/en-us/unreal-engine/spawn-temporary-actors-in-unreal-engine-cinematics)** Cine Camera Actor in your current sequence. The created Cine Camera Actor becomes the current camera cut.

You can specify whether or not to create the camera as a spawnable in the Sequencer **[Editor Preferences](/documentation/en-us/unreal-engine/cinematic-editor-and-project-settings-in-unreal-engine)**, using the **Create Spawnable Cameras** preference.

## Usage

The **Cine Camera Actor** has a few primary functions to aid your viewport filming experience.

### Piloting

Similar to most other actors, the **Cine Camera Actor** can **Pilot** the preview of your camera's perspective and behavior from the [Viewport](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine). You can pilot any actor in your level using this piloting method.

To pilot the **Cine Camera Actor**,

1.  Right-click on the camera in the Viewport.
2.  Select **Pilot CineCameraActor**.

![camera pilot menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f4bda2a-3e4f-4b93-9c81-dd34058614f8/pilot_camera.png)

You should be aware of the three components of the Camera Pilot menu:

1.  Indicators which camera is being piloted.
2.  Stop piloting the camera (eject icon). Unlocks the **Viewport's** position and orientation from the actor that the Viewport is currently piloting. This action exits the camera pilot mode but keeps the camera selected.
3.  Camera icon indicates the exact camera view when using **Viewport** to pilot a camera (use the keyboard **Ctrl + Shift + C** to toggle as well).

You can use the keyboard shortcut of **Ctrl + Shift + P** of the selected camera to jump into pilot mode.

### Picture-in-Picture Display

When you have selected a **Cine Camera Actor**, a **Picture-in-Picture** (PIP) window appears in the bottom right corner of the **Viewport**. This window displays a preview of the camera's view and lists information about the camera's name, [filmback](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#filmback), and other properties.

![Camera Viewport Picture-in-Picture](pip.png)

When you've selected multiple **Cine Camera Actors**, multiple PIP windows with their respective views appear in the **Viewport**. The PIP isn't displayed when you are piloting a camera.

You can pin a PIP window so that it remains visible even when the camera is not selected. To pin a PIP window, click the **Pin** button in the bottom-left corner of the picture-in-picture window. To unpin a PIP, click the pin icon again.

![picture in picture pin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ad17305-ed7d-48f1-89d6-c2b9d96dc181/pin_pip.png)

You can customize or disable the PIP in Unreal Engine's **[Editor Preferences](/documentation/en-us/unreal-engine/unreal-editor-preferences)**.

To adjust a PIP's appearance:

1.  Go to **Edit > Editor Preferences**.
2.  Scroll down to **Level Editor**.
3.  Locate **Preview Selected Cameras** and **Camera Preview Size**.

Picture-in-picture settings provide options for which camera actor is active and the size of the PIP window.

| Name | Description |
| --- | --- |
| **Preview Selected Cameras** | When enabled, selecting a camera actor displays a live **Picture-in-Picture** Preview from the camera's perspective within the current Viewport. You can use this to tweak camera positioning, post-processing, and other settings without having to take control of the camera itself. This feature may reduce performance when enabled. Defaults to enabled. |
| **Camera Preview Size** | Change the size of the PIP preview when the **Preview Selected Camera** is enabled. Defaults to 5.0. |

### Post Processing

All **Cine Camera Actors** have their own **[Post Processing](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine)** layer that is enabled when piloting them. Post processing provides options for additional camera effects to be displayed and adjusted, such as **[Bloom](/documentation/en-us/unreal-engine/bloom-in-unreal-engine)**, **[Exposure](/documentation/en-us/unreal-engine/auto-exposure-in-unreal-engine)**, **[Vignetting](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine)**, **[Color Grading](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine)**, and more.

![cine camera post process comparison](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4148be5e-3819-423f-a31a-859d666be522/post_process_comparison.png)

Comparing cine camera post process. No post processing. Temp set to 15,000 and Vignette Intensity set to 0.8.

For more information on the post-processing effects available in Unreal Engine, see the **[Post Processing](/documentation/en-us/unreal-engine/post-process-effects-in-unreal-engine)** page.

## Properties

**Cine Camera Actor** have the following settings: **[Look at Tracking Settings](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#lookattracking)**, **[Camera Options](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#cameraoptions)**, **[Filmback](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#filmback)**, **[Lens Settings](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#lenssettings)**, **[Focus Settings](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#focussettings)**, and **[Crop Settings](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#cropsettings)** settings.

### Look at Tracking

You can use the **Cine Camera Actor** to track other actors using the **Look at Tracking** settings. Enabling this feature overrides the camera's rotation and modifies it to aim towards a specified actor.

![camera look at tracking](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/209973b6-e587-4d53-bbbe-133462f16245/look_at_tracketing.gif)

To enable camera tracking:

1.  In the **Details** panel of the selected camera, go to the **Current Camera Settings** category, and locate the **Lookat Tracking Settings**.
2.  Enable **Enable Look at Tracking**.
3.  Set the **Actor to Track** property to the actor you want the camera to look at. You can select an actor to track by either searching through the drop down list (1), using the Select Actor from Viewport (2), or Pick Actor from scene (3) options.
    
    ![Selecting actors to track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dc0ffc1-7dc1-4bd1-8bb5-c83b5d9b09ce/actor_to_track_property.png)

The **Look at Tracking** feature also contains the following properties for further customization:

| Name | Description |
| --- | --- |
| **Enable Look at Tracking** | Enables the **Look at Tracking** feature on this camera. |
| **Draw Debug Look at Tracking Position** | 
Enables a debug locator cube to show what the camera is tracking. This yellow cube is useful if you are using it in conjunction with **Relative Offset**.

![Draw debug look at tracking position](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5d9664d-04c1-4ef4-a7f5-09e7e6a765f0/draw_debug_look_at_tracking_position.png)

 |
| **Look at Tracking Interp Speed** | 

The speed that the camera updates its tracking of the object. The default value of 0 makes the camera track instantly, and numbers greater than 0 adds an increasingly large delay to the camera's tracking.

![look at tracking speed](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3dd878fb-4ed9-44fe-9972-fa71f5ff923b/look_at_tracking_interp_speed.gif)

 |
| **Actor to Track** | Specifies the actor that the camera is tracking. You can keyframe this property in Sequencer, allowing the camera to change its tracked target over time. If no actor is specified, the camera instead tracks the world origin (0, 0, 0). |
| **Relative Offset** | 

Specifies a positional offset to apply to the tracked actor relative to its local space. This is useful for controlling specific framing of a tracked actor.

![look at tracking offset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/90c4e691-5a99-45ed-b253-8cf1058bea52/relative_offset.gif)

 |
| **Allow Roll** | With this feature enabled, the camera can be rolled on the X-axis. If disabled, the camera tracking overrides any data on the X-axis. |

### Camera Options

You have additional camera setting options that provide control for black bars, Pawn influence, post-process blending, position and orientation locking when using head-mounted displays, and field of view adjustments for LOD.

| Name | Description |
| --- | --- |
| **Constrain Aspect Ratio** | Enables the drawing of black bars which preview the **Sensor Dimension** and its base aspect ratio. |
| **Use Pawn Control Rotation** | If the camera is being used as a component on a Pawn, then enabling this causes the pawn's rotation to influence the camera component. |
| **Post Process Blend Weight** | Blends the influence of the camera's **[Post Process](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#postprocessing)** layer between fully on and off. A weight of 1 causes it to be fully enabled, and 0 causes it to fall through to other layers. |
| **Lock to Hmd** | Locks the camera's position and orientation to a connected head-mounted display, when a VR headset is connected for **[XR Development](/documentation/en-us/unreal-engine/getting-started-with-xr-development-in-unreal-engine)**. |
| **Use Field Of View for LOD** | When enabled, the camera's field of view influences what level of detail the object should display, instead of relying on camera distance only. This fixes issues caused by low-quality objects that are rendered from far away cameras, and that are zoomed in on the subject. |

### Filmback

**Filmback** parameters provide options to select from real-world camera body presets (Filmback), emulate sensor dimensions, and display aspect ratio.

| Name | Description |
| --- | --- |
| **Filmback** | 
The **Filmback** property contains a list of real-world preset **[Camera Bodies](https://en.wikipedia.org/wiki/Camera)** to choose from. These presets affect the **Sensor Width** and **Sensor Height** properties in order to emulate the selected camera body. The camera's base field of view and aspect ratio are also affected by these settings.

![Filmback presets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d8eda2a-c5d2-4e39-a9b9-afe898ff9a04/filmback_presets.png)

 |
| **Sensor Width/Height** | The Sensor Width and Height properties emulate the dimensions of your film or **[Digital Sensor](https://en.wikipedia.org/wiki/Image_sensor_format)** in millimeters. These values automatically change whenever a new **Filmback** preset is selected. |
| **Sensor Aspect Ratio** | This property displays your current aspect ratio computed from the selected sensor's dimensions. This value cannot be changed manually, because it is intended for read-only reference. |

### Lens Settings

Lens parameters offer options to select real-world preset camera lenses, set focal length, F-stop, specify the squeeze factor for anamorphic lenses, and control the diaphragm (blade).

| Name | Description |
| --- | --- |
| **Lens Settings** | The **Lens Settings** property contains a list of real-world preset **[Camera Lenses](https://en.wikipedia.org/wiki/Camera_lens)** to choose from. These presets affect the **Focal Length**, **FStop**, and **Diaphragm** properties to emulate the selected lens. |
| **Min/Max Focal Length** | The minimum and maximum **Focal Length** range for the camera. Setting these affects the value range of the camera's **Current Focal Range** property, that is used to emulate **[Zoom Lenses](https://en.wikipedia.org/wiki/Zoom_lens)**. To achieve the effect that emulates **[Prime Lenses](https://en.wikipedia.org/wiki/Prime_lens)**, which are not designed to be zoomable, set both of these properties to the same value. |
| **Min/Max FStop** | The minimum and maximum **[Aperture](https://en.wikipedia.org/wiki/Aperture)** range for this camera. |
| **Squeeze Factor** | Squeeze factor for anamorphic lenses. |
| **Diaphragm Blade Count** | 
Controls the **[Diaphragm](https://en.wikipedia.org/wiki/Diaphragm_%28optics%29)** (blade) count on the camera lens. The number of diaphragms on a lens correlates to the shape of the **Bokeh** effect. Lower numbers cause bokeh to appear more square, and higher numbers cause it to appear more rounded.

![camera diaphragm](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d02b081f-20e0-454b-b0fc-b16b3e3d4ad6/diaphragm.png)

 |

### Focus Settings

The **Focus settings** feature includes manual focus distance controls, actor tracking with the option to offset, debugging focus, and several focus parameters.

| Name | Description |
| --- | --- |
| **Focus Method** | 
Focus Method controls the depth of field and focus settings that contains the following options:

-   **Do Not Override**: Disables the camera-influencing depth of field.This still provides depth of field from other sources, such as from a post-process volume.
-   **Manual**: Enables depth of field and controls the focus, relative to the camera position, using the **[Manual Focus Distance](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#manualfocusdistance)** property.
-   **Tracking**: Enables depth of field and controls the focus by tracking actors using the **Tracking Focus Settings** properties.
-   **Disable**: Disables depth of field entirely and does not allow any depth-of-field influence from other sources.



 |
| **Manual Focus Distance** | Manually controls the focus distance relative to the camera's position in centimeters. This is a type-aware field, so you can input **5m** and it converts the value to **500cm**. You can use the eyedropper to pick an object from the Viewport and snap your camera's focus to it. To use it, click the button, and then left-click the object in your viewport. This property only appears if **Focus Method** is set to **Manual**. |
| **Actor to Track** | Uses an actor as the focus point for the camera's depth of field. This is enabled only if **Focus Method** is set to **Tracking**. |
| **Relative Offset** | A positional offset to apply to the tracked actor relative to its local space. This is enabled only if **Focus Method** is set to **Tracking** and is useful for fine-tuning the focus point on tracked actors. |
| **Draw Debug Tracking Focus** | Enables a debug locator cube to show where the depth of field is focused if **Focus Method** is set to **Tracking**. This is useful if you are using it in conjunction with **Relative Offset**. |
| **Draw Debug Focus Plane** | Enables a camera-oriented transparent plane for previewing your focus point. |
| **Debug Focus Plane Color** | Specifies the color of the **Debug Focus Plane** with RGBA values. |
| **Smooth Focus Changes** | Enables focus distance changes to be automatically interpolated over time, instead of instantaneously. |
| **Focus Smoothing Interp Speed** | The speed of focus-change interpolation if **Smooth Focus Changes** is enabled. Lower numbers are slower, and higher numbers are faster. |
| **Focus Offset** | Offsets the focus point relative to the position of the tracked actor, if **Tracking** focus is being used. Positive numbers increase the distance from the camera, and negative numbers decrease the distance. If **Manual** focus is enabled, the focus point instead uses the **[Manual Focus Distance](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine#manualfocusdistance)**. |
| **Current Focal Length** | The focal length property of the camera, which is limited based on the focal length range defined by the **Min/Max Focal Length** properties in **Lens Settings**. |
| **Current Aperture** | The aperture or **FStop** property of the camera, which is limited based on the FStop range defined by the **Min/Max FStop** properties in **Lens Settings**. |
| **Current Focus Distance** | A read-only property that displays the final focus distance output based on either the **Manual** or **Tracking** focus, including any additional offsets applied to them. |
| **Current Horizontal FOV** | A read-only property that displays the final horizontal field of view based on a combination of the camera's **Focal Length** and **Sensor Dimensions**. |

### Crop Settings

You have the option to choose camera cropping settings, including No Crop, various aspect ratios, and Custom.

| Name | Description |
| --- | --- |
| **Crop Settings** | You can set the camera cropping to **No Crop**, **1.33 (4:3)**, **1.77 (16:9)**, **2.39**, and **Custom…**. Defaults to **No Crop**. |
| **Cropped Aspect Ratio** | Relationship between width to height. Changing this value sets the **Crop Settings** to custom. Defaults to 0.0. |

## Cine Camera Scene Capture Plugin

**Cine Camera Scene Capture** plugin adds the capability to apply scene capture to Cine Camera Component.

The functionality of **Cine Capture Component** is similar to **Scene Capture**, except most settings related to camera settings are controlled by **Cine Camera Component** or **Cine Camera Actor**. Similar to Scene Capture, you must select scene capture settings such as render target to be rendered to.

### Set Up Cine Capture Component

To set up the Cine Capture Component, you must first enable the CineCameraSceneCapture plugin.

To enable the plugin:

1.  Go to **Edit > Plugins**.
2.  In the search bar, enter **CineCameraCapture**.
3.  Enable the plugin and restart Unreal Engine.

With the plugin enabled, your project is ready for scene capture.

To capture a scene:

1.  Create a **Cine Camera Actor** by dragging one from the **Place Actors panel**.
2.  In the **Details panel**, click the **Add** button and find the **Cine Capture Component 2D**.
3.  While still in the **Details panel**, drag the **CineCaptureComponent** under your **CineCameraActor**. The parent-child relationship is required as it relies on the settings being propagated from the **Cine Camera Component**.
4.  In the **Scene Capture** section, set a **Render Target** by selecting **Render Target** from the **Texture Target**.
5.  Specify an output folder and click the **Save button**.
6.  In your output folder, double click the **Texture Render Target** to open the editor.

### Cine Capture Component Properties

The Render Target Highest Dimension and Follow Scene Capture render path settings provide options for controlling render target size and optimizing scene captures.

| Name | Description |
| --- | --- |
| **Render Target Highest Dimension** | Controls the render target size. The aspect ratio depends on the sensor width and height specified by Filmback settings of **Cine Camera Component**. If the sensor width is 35mm, sensor height is 20mm, and Render Target highest dimension is 1000, then render target dimensions would be \[1000, 571\] with the lowest dimension calculated (1000/(35/20)) = 571. |
| **Follow Scene Capture Render path** | Enables optimizations available to scene captures. These optimizations try to reuse certain visual effect buffers generated by other views. If you experience visual difference between Cine Camera Actor and the results of Cine Camera Capture, you might find the results comparable if you disable this setting. |

### OCIO

You can apply OCIO transformations to Cine Camera captures. For more information, see **[Color Management with OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine)**.