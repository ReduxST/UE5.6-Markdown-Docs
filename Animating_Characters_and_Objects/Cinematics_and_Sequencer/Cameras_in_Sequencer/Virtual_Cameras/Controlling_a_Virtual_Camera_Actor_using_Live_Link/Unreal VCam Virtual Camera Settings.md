# Unreal VCam Virtual Camera Settings

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-vcam-virtual-camera-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/unreal-vcam-virtual-camera-settings)  
**Processed:** 2025-06-14 16:57:39

---

The **Virtual Camera** settings are located on the left side of the Unreal VCam app. This menu includes options to control the different camera, lens, and exposure settings of the virtual camera in your scene.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dcecf54-6193-457a-ad01-e2f46b97178d/vcamcamerasettings.png)

The menu includes the following settings:

| **Icon** | **Dial Name / Action** | **Description** |
| --- | --- | --- |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c91e41b-d726-46c9-a9cf-e87b19a26bc1/lenssettings.png) | **Lens Settings** | Set virtual camera parameters including lens size, focus, iris, and more. |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/80efd205-737c-4370-bcfe-8af7369dca6c/focussettings.png) | **Focus Settings** | Set the virtual camera’s focus mode and focus distance. |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/865f58b1-1e0f-40c8-b362-ae1663648fd0/filmbacksettings.png) | **Filmback Settings** | Configurable settings for the virtual camera's image sensor. |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c9fa883-8ece-4426-9726-1a5e4f7cc750/isosettings.png) | **ISO and Exposure Compensation Settings** | Configurable settings for how the virtual camera's exposure is handled. |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/23e3b680-7c0a-44cb-97b0-db7727d020e5/nearclipsettings.png) | **Near Clip Plane Settings** | Set the distance from the camera where polygons no longer render. |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/569fcda9-8e90-4b50-a183-2ba2422dab8d/masksettings.png) | **Mask / Overlay / Reticle Settings** | Set what type of aspect ratio mask, grid overlay, and reticle are used with the virtual camera. |

### Lens Settings

The **Lens** settings include virtual camera presets for lenses, focus, and iris settings.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/550f01e2-6f88-479c-af55-ba740e763080/lenssettingsinterface.png)

#### Lens Preset and Focal Length

When in **Lens Mode**, you can adjust between configurable presets for common focal lengths and iris. You can also set the iris and dial-in the focus distance manually.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f4e2074-f163-425e-b23b-4b48ccc4cbaf/lenspreset.png)

You can configure Lens presets in the **Project Settings** under **Cinematic Camera > Lens Presets**. Here, you can add your own, alter, or remove any existing presets.

| **Dial Name / Action** | **Description** |
| --- | --- |
| **Left Dials** |   |
| **Lens Preset** | 
Select from a list of presets for focal lengths and irises. Some presets include the Focal Length dial. Lens presets include:

-   12mm Prime f/2.8
-   12mm Prime f/2.8
-   12mm Prime f/2.8
-   30mm Prime f/1.4
-   50mm Prime f/1.8
-   85mm Prime f/1.8
-   105mm Prime f/2
-   200mm Prime f/2
-   24-70mm Zoom f/2.8
-   70-200mm Zoom f/2.8
-   Universal Zoom

Lens presets are set up in the Project Settings in the **Cinematic Camera** category. You can add new presets and edit existing ones.



 |
| **Focal Length** | Sets the length of the lens (in millimeters). Longer lengths lead to higher magnification with a narrower angle of view. Shorter lengths have lower magnification and a wider angle of view. (Only available on some Lens Presets.) |
| **Right Dials** |   |
| **Focus Distance** | Sets the distance (in meters) from the virtual camera lens where objects are in focus. |
| **Iris** | Controls the amount of light (in f-stops) by making the aperture wider (low f-stop) or narrower (high f-stop). |

#### Using Pinch to Zoom

Pinching in and out with two fingers on the center of the virtual camera screen zooms in and out within the range of your currently selected lens. If your lens is a prime that has a set focal length and cannot zoom, pinch to zoom does nothing.

### Focus Settings

The **Focus** settings contain options for configuring how the virtual camera focuses on objects.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b5e52df5-b4d1-44c9-bd60-11dabef1f1a8/focussettingdials.png)

| **Icon** | **Dial Name / Action** | **Description** |
| --- | --- | --- |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8d3bc129-6c84-4761-aed5-ed3128acb411/focussettings.png) | **Focus Method** | 
Choose how you want the virtual camera to apply focus in the scene:

-   **Do Not Override** removes the ability to change the focus distance dial in any menu and causes the **Post Process Volume** settings to persist
-   **Manual** lets you manually adjust the focus using the **Focus Distance** dial to set the distance from the camera to the subject
-   **Tracking** locks focus on specific actors in the shot
-   **Disable** stops all depth of field from happening



 |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4cbd8878-cf61-48c8-930f-2d50c8cf6cde/focussettings.png) | **Focus Distance** | Specifies the distance (in meters) from the virtual camera lens to the point where objects appear in focus. |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ebb7814-f1ad-4cd6-a232-e995ec71f71f/pickactor.png) | **Pick Actor to Track** | Use this to pick an actor in the scene to focus on. When in **Tracking** mode, the selected actor always remains in focus, and its distance from the camera drives the Focus Distance. When in **Manual** mode, the Manual Focus Distance is set to the distance to this target, but it does not track the selected actor ifthe camera or target moves. |
| ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7324dc94-b482-4c86-ac15-d83454c415d5/togglefocuspeaking.png) | **Toggle Focus Peaking** | Toggles a visual reference in the scene where the focus distance is currently set. |

#### Using Tap to Focus

You can select a focus target by double tapping on that actor in the scene. A yellow focus indicator appears to confirm where you have tapped. Tap to focus is available even if you are not in **Focus Mode.**

The behavior of tap to focus differs based on your current mode:

-   In **Manual Focus**, tapping an actor sets the manual focus distance to the distance to the tapped actor. This value does not update if the actor or camera moves.
    
-   In **Tracking Focus**, tapping an actor sets the tracking focus target and lock focus distance to the tapped point on the selected actor or skeletal mesh socket. If the actor/socket or camera moves, focus adjusts to keep the point in focus.
    

Only actors with collision (or physics assets in the case of skeletal actors) can be detected with tap to focus.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9a25133-bb7c-4e2f-beab-f8262e0275b9/taptofocus.png)

#### Using Tracking Focus

You can track an actor in the scene and maintain the virtual camera's focus on it by using the **Pick Actor to Track** option in the HUD or by using **Tap to Focus**.

To use Tracking Focus:

1.  In the **Lens settings** menu, navigate to the **Focus** settings. Here, **Focus Method** is selected by default with its adjustable dials present on screen.
    
2.  Drag the **left dial** to **Tracking**.
    

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a1aa4bb-96e0-4a94-bb41-cd978d15e15e/trackingfocusdial.png)

While holding and looking at your device, double-tap on an actor in the scene. Alternatively, point the virtual camera **Reticle** at the object you want to keep focused on. Tap the **Pick Actor to Track** icon in the left menu. Once you've done this, look at the **Right** dial and you'll see the **Tracking Offset** along with the **Name** of the focused asset/skeletal mesh socket below.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b8fa65b2-5591-4f7a-aa51-fafc54ef6dc3/trackingfocusoffset.png)

When using the Tracking focus method, use the right dial for **Tracking Focus Offset** to dial-in the focus on the subject. When tracking a Skeletal Mesh actor, the target point moves to the closest socket for focus, which may not always be the exact spot you're wanting to focus on.

#### Using Focus Peaking

You can use the **Focus Peaking** toggle to see exactly where the focus distance is in the scene. A red outline represents the focal distance. **Focus Peaking** is useful for quickly seeing where the focus distance is in the scene to dial it in. The outlined area expands and contracts to show the **depth of field** based on your current **iris**. To dial in the focus, use the **Focus Distance** dial on the right side of the app.

### Filmback Settings

**Filmback** describes the dimensions of the frame for the digital imaging sensor. This size determines what the camera sees through its viewfinder. The filmback determines frame size, depth of field, resolution, and more.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/73988fd4-2719-44de-a94a-b5277e912471/filmbacksettingsinterface.png)

There standard presets are:

-   16:9 Film
    
-   16:9 Digital Film
    
-   16:9 DSLR
    
-   Super 8mm
    
-   Super 16mm
    
-   Super 35mm
    
-   35mm Academy
    
-   35mm Full Aperture
    
-   35mm Vista Vision
    
-   IMAX 70mm
    
-   APS-C (Canon)
    
-   Full Frame DSLR
    
-   Micro Four Thirds
    

The examples below are using the **30mm Prime f/1.4** Lens Preset.

<table class="table" style="--columns-count: 4;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f69c9a7d-7c05-4fa2-ad4b-a267edc6ccfd/16x9film.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">16:9 Film</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e207ea8-1076-44be-80d4-26c69687b411/16x9dslr.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">**16:9 DLSR**</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a246a0ba-aeb3-48ad-ad2a-cbef50ce11af/super16.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Super 16mm</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89065d45-e5d5-4c94-9964-ca7c655ac52c/imax70.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">IMAX 70mm</p></td></tr></tbody></table>

You can configure Filmback presets in the Project Settings under **Cinematic Camera > Filmback Presets**. Here, you can add your own, alter, or remove any existing presets.

### ISO, Iris, Shutter Speed and Exposure Compensation Settings

The **Exposure** settings control how bright or dark the image is.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9d905353-d45b-428a-b9b0-30439e0eefb5/isosettingsinterface.png)

| **Dial Name / Action** | **Description** |   |
| --- | --- | --- |
| **Left Dials** |   |   |
| **ISO** | Sets the sensitivity of the camera's sensor. Lower numbers have a lower sensitivity to light, which makes the image darker. Higher numbers have a higher sensitivity to light, which makes the image brighter. When not set to **Auto Exposure**, the ISO is dependent on what f-stop the camera iris is set to. |   |
| **Iris** | Sets the diameter (measured in f-stops) of the aperture's opening. This controls the amount of light that is allowed to pass through the lens of the camera. It also has an effect on depth of field. For more information, see [Cinematic Depth of Field](/documentation/en-us/unreal-engine/cinematic-depth-of-field-in-unreal-engine). |   |
| **Right Dials** |   |   |
| **Exposure Compensation** | Applies a compensation (measured in stops) to override exposure to brighten or darken the frame. Lower numbers give a higher exposure, which makes the result brighter. Higher numbers give a lower exposure, which makes the result darker. |   |
| **Shutter Speed** | Adjusts the camera’s "exposure time" (measured in fractions of a second). Slower shutter speeds result in a brighter image. Faster speeds result in a darker image. Unlike a physical camera, shutter speed on the Virtual Camera only affects exposure and not motion blur. |   |

#### Using Zebra Striping

Tapping the **Zebra striping** button from **Exposure Mode** or the top quick action buttons toggles zebra striping. When enabled Zebra Striping marks areas of the frame that are over-exposed.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/addf9e95-10a4-4745-b205-59b92faa4f57/zebrastriping.png)

### Near Clip Plane

The **Near Clip Plane** sets the distance (measured in centimeters) from the camera that polygons no longer render. This option is useful when you want to not render objects blocking the view but also continue to render their shadows and interaction with the scene.

In the example below, the virtual camera is using a longer lens to capture the subject, but the view is partially obstructed by a plant. Using the near clip plane, Unreal doesn't render any geometry within the set distance from the camera.

### Mask, Overlay, and Reticle Settings

The **Mask / Overlay / Reticle** settings include optional visual guides for the virtual camera viewfinder. This includes grids, safe zones, different reticles, and mattes to mask off different aspect ratios.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ef4d8071-1a14-4faf-91f3-edd8e50ecf6e/maskoverlayinterface.png)

Each of the groups for overlays, reticles, and masks include their own **Opacity** dial. You can use this to set how opaque or transparent each is. At 0, they are not visible, at 0.5 they're partially transparent, and at 1.0 they're fully opaque.

<table class="table" style="--columns-count: 3;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/885f8d82-d9c9-41df-a086-d107dc0f0a75/opacity0.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Opacity = 0 (Overlay Grid Not Visible)</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/982069ec-0fbc-481b-9d29-6e71d4363dd2/opacity05.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Opacity = 0.5 (Overlay Grid Partially Transparent)</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4885c5f0-5740-4f03-9e04-36676f0e1cce/opacity1.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Opacity = 1 (Overlay Grid Opaque)</p></td></tr></tbody></table>

#### Overlay Selections

Use the **Overlay** dial to choose the type of grid to overlay on the virtual camera viewfinder.

You can choose from the following options:

<table class="table" style="--columns-count: 4;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fbe4b70b-be66-4678-9ec9-5ac67b2769d3/ruleofthirds.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Rule of Thirds</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df2c7d7d-de18-4ec5-a99b-3d1911faab6c/quadsymmetry.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Quad Symmetry</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/400de91e-3fb3-4855-8e61-8af7b2d2ad97/safezones.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Safe Zones</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f37278a-b9bf-4767-bbd6-0685d462a7a5/opacity0.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Hidden</p></td></tr></tbody></table>

#### Reticle Selections

You can use the **Reticle** dial to choose the design for the center of the frame used to aim what the virtual camera is looking at.

You can choose from the following options:

<table class="table" style="--columns-count: 5;"><tbody><tr><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cc889c74-511b-4edc-a12b-f3282a304667/dot.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Dot</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e526523-fa1f-45ca-9599-4927ca96b24a/circle.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Circle</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/867b19d8-ea40-46ee-8450-79823f3c9d42/cross.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Cross</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/771c61a5-9c4b-456d-a88c-29111a2e3138/splitcircle.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Split Circle</p></td><td><img src="https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ae2ccdd-2c6d-4811-a2fd-acb4da6b432b/hidden.png" alt="image alt text" loading="lazy"><p class="figure-caption is-separated">Hidden</p></td></tr></tbody></table>

#### Mask Selections

You can use the **Mask** dial to choose from the presets for different size aspect ratio mattes in the virtual camera viewfinder. The mask presets include common industry standards.

You can choose from:

-   9:16 (0.562)
    
-   1:1
    
-   4:3 (1.333)
    
-   3:2 (1.5)
    
-   16:9 (1.778)
    
-   1.85:1 (1.85)
    
-   2:1
    
-   2.39:1 (2.39)
    
-   2.4:1 (2.4)
    
-   2.76:1 (2.76)
    
-   Custom
    

Below is an example of the mask presets overlaying the virtual camera viewfinder:

If none of the included presets fit your requirements, you can use the **Custom** option to define your own masked area. When selected, a new dial appears on the right side of the screen. Drag the dial to the left to make the mask smaller, drag the dial to the right to make the mask larger. The mask can fill the tops and bottoms of the frame or the sides of the frame.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/87d90127-0585-4a72-8974-5316e6b2e34c/maskpresets.png)