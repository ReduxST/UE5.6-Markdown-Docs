# In-Camera VFX Depth of Field Compensation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-depth-of-field-compensation-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-depth-of-field-compensation-for-unreal-engine)  
**Processed:** 2025-06-14 16:30:39

---

## Introduction

### The challenge with DOF on an LED wall

Managing Depth of Field (DOF) on an LED wall for In-Camera VFX (ICVFX) is a long-standing challenge. This is due in part to the fact that two DOFs are present, one from the virtual camera rendering using nDisplay on the LED wall, and the other from the physical camera. With these two cameras, matching Focus, Iris, and Zoom, the resulting image is inaccurate and blurrier than would otherwise be expected, and there is a break in the continuity between physical and virtual props and set dressing.

![A depth of field continuity break between physical and virtual elements.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fcf8bfb7-a215-43e6-b55f-a54e34b84f82/image_1.png)

In other scenarios, to mitigate the extra blurring effect, DOF is sometimes disabled leading to a lack of depth in the virtual background, or arbitrary adjustments are applied to the focus distance and aperture to attempt to achieve an desired accurate or creative result. These methods can result in non-accurate depth of field falloff and send confusing lens data downstream into post production.

![Correcting the depth of field continuity break.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a06b07d4-db95-4ab2-87bb-26bb77fda440/image_2.png)

### ICVFX Depth of Field Compensation

The ICVFX Depth of Field Compensation feature provides a simple and effective method to achieve accurate DOF for LED wall virtual production, with full creative control, whilst retaining contiguous DOF falloff between the physical and virtual set.

This feature is new and experimental; it has been rigorously tested and visually verified by the virtual production team, the level of accuracy it achieves has been shown to provide enormous value on set. Supporting both spherical and anamorphic lenses, the compensation works by adjusting the Circle of Confusion (CoC, or amount of blur) of each pixel, based on the camera's distance to the wall and the pixel's depth in the scene. The compensation dynamically adjusts based on the real world camera’s focus distance, aperture and focal length.

## ICVFX DOF Compensation: How to use the feature

![An In Camera VFX shoot in progress.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/969a7268-a440-4ce5-8f43-cb383b617914/image_3.png)

### Prerequisites

#### Camera tracking and LED wall mesh

The main parameter the DOF compensation feature relies on is the camera’s distance to the LED wall, therefore camera tracking is required along with an nDisplay wall mesh matching the real world LED wall.

#### Matching camera parameters

It is also important that the ICVFX camera component or its assigned Cine Camera actor, share the same focus distance, aperture and focal length parameters (sometimes referred to as focus/iris/zoom or "FIZ") as the real world camera and lens. The Cine Camera actor must also share the same sensor size, and squeeze factor is also required for anamorphic lenses. This is best achieved with a lens encoding system and a well calibrated lens file, giving you a fully dynamic real time compensation, capable of compensation throughrack focuses!

However, without such a system, it is possible to enter all the parameters manually, just be sure to update the parameters each time the lens FIZ values are adjusted by the camera team. The blade count for the aperture is also important to achieve a complementary Bokeh.

#### Engine settings

Lastly, ensure the minimum engine scalability setting for Post Processing is set to Epic, otherwise the render will be utilizing legacy DOF which is not physically accurate.

Prerequisites in summary:

-   Camera tracking
-   Reasonably accurate LED wall mesh
-   Lens encoding (ideal but optional)
-   Lens file (ideal but optional
-   All Cine Camera actor settings must match the real world camera
    -   Focus distance
    -   Aperture (Iris)
    -   Focal length (zoom)
    -   Sensor size
    -   Squeeze factor
    -   Aperture blade count
-   Minimum engine scalability: Epic

### Location

The ICVFX Depth of Field Compensation feature is located on the ICVFX Camera Component of the nDisplay Config actor.

![ICVFX Depth of Field settings under the ICVFX Camera Component.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e2eea92-77b5-4518-9992-f8bb45c64d33/image_4.png)

### Controls

The two main controls are:

1.  Enabling the feature
    
2.  Depth of Field Gain
    

![Main ICVFX Depth of Field controls.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27ec5d6b-6aef-4730-b460-6d07826172bf/image_5.png)

Enabling the feature immediately compensates for DOF on the LED wall using the nDisplay render. You can also observe this compensation on the nDisplay Config actor preview render.

The **Depth of Field Gain** property is the main creative control, as it defines how shallow the depth of field is. A value of 1 is default and represents a match with the real world lens. A gain value higher than 1 (max 4) will make the DOF falloff more shallow. For example if you want a DOF which is twice as shallow then set the gain to 2. Gain values lower than 1 will make the DOF less shallow, i.e lower gain numbers increase the depth of field. For example, to halve how shallow the DOF is then set the DOF gain to 0.5. This works all the way down to a value of 0, at which point there is no DOF in the rendered LED wall content.

![Additional ICVFX Depth of Field controls.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0582f5a-a547-41e7-9157-8a779a68061b/image_6.png)

Other controls include the **Automatically Set Distance to Wall** and **Distance to Wall Offset** properties. As this feature is experimental, the development team wanted to include controls to allow users to tinker and experiment, however these are not required to be altered for regular intended use. The Automatically Set Distance to Wall property is enabled by default and is responsible for providing a dynamic update of the compensation based on the camera’s position.

The Distance to Wall Offset property simply adds or subtracts a number from the distance to wall parameter. This can be used to artistically control the blur on the objects closer to the wall without changing the falloff. Bear in mind that defocusing the virtual objects at the wall depth, can in turn produce a double blur and break the transition from physical to virtual set, **but in the end if a shot looks correct through the monitor then it is!**

Lastly there is the **Compensation LUT** (look up table) property. Not to be confused with any color correction, this LUT defines the non-linear depth based adjustment to the circle of confusion required for DOF compensation. This can be left as default, but it was added to allow for further experimentation where it is felt to be required.

### Workflow Improvements

Improvements have been made to the way the Cine Camera actor and ICVFX Camera Component interact, such that changes to focus distance, aperture, focal length, and other lens parameters can be made on either actor/component and will be instantly reflected on the other. This means that these often used settings are now accessible from the nDisplay Config actor details panel.

The ICVFX Stage app also includes controls for the ICVFX Depth of Field compensation. This provides remote control on set for enabling and disabling compensation, adjusting the distance to wall offset and controlling the DOF Gain. When no lens encoding system is present, from the app it is possible to control all of the Cine Camera actor lens parameters, including focal length, aperture, focus distance, and its associated settings.

![The ICVFX Stage app on a tablet.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/742bd615-d7f0-45cd-b131-cf18b613009b/image_7.png) ![Controlling ICVFX Depth of Field Compensation from a tablet.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/19b51138-a649-4fc9-aeef-9d28ba5457ab/image_8.png)

## ICVFX Depth of Field Compensation: Caveats

### Bokeh

Bokeh rendered on the wall will appear slightly softer when compared with the bokeh produced in the lens. Therefore in scenarios where the focus distance is closer to the camera with a larger aperture leading to a very shallow depth of field, it may be worth setting the DOF gain to lower values, including 0. In our tests, in this limited scenario, DOF gain 0 provided more accurate Bokeh when compared with a reference image.

### Convert T-stop to F-stop

The Unreal engine Cine Camera actor expects F-stop values to be entered, therefore if your lens is in T-stops you will want to convert to F-stop for the most accurate results. However you may find very good results using the T-stop value without conversion, so don’t sweat it.

### Asymmetric Frustum Overscan

It’s worth also noting that the asymmetric frustum over scan settings can in some extreme situations impact the DOF, therefore adjust the DOF gain accordingly.

### Virtual Foreground Objects

It is not possible to compensate for virtual objects rendered on the wall that are between the Cine Camera actor and nDisplay Config actor, so you may wish to disable these for best results and rely on physical set props to provide foreground elements instead.

### Anamorphic Frustum Resolution

Lastly, the lens squeeze factor parameter increases the horizontal resolution of the frustum, so be sure to optimize content with this in mind. In situations where this has not been possible, a good work-around would be to reduce the frustum resolution multiplier or reduce the height of the frustum resolution based on the squeeze factor (for example, squeeze factor of 1.8 would require that you divide the vertical resolution by 1.8)