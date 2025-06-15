# Audio Volumes

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-volumes-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/audio-volumes-in-unreal-engine)  
**Processed:** 2025-06-14 16:09:06

---

With the **Audio Volume Actor**, you can define areas within a Blueprint map that can be used to process sounds, then use these settings to apply reverb effects, set volumes, define the zones affected, emulate occlusion on a sound, and define the shape of the sound volume.

## Transform

The **Transform** settings change the location, rotation and scale. Use these settings to ensure that the audio volume encompasses the area in which you want sound to be processed.

![The Transform Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9fbc242a-85fe-466f-8b7f-fc9d26ff454e/01-audio-volume-transform-settings.png)

-   **Location:** Determines the location of the origin of the audio volume.
-   **Rotation:** Determines the rotation of the audio volume.
-   **Scale:** Determines the scale (size) of the audio volume.

## Audio Volume

The **Audio Volume** settings define which volume's settings are used when there are overlapping volumes.

![The Audio Volume Settings ](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/85199898-5102-4fb8-b998-ea39198d2c06/02-audio-volume-settings.png)

-   **Priority:** Determines the priority of the audio volume, which is used to ensure that in the case of overlapping or *nested* volumes, the correct volume is applied. The higher the number used, the higher the priority. When two overlapping volumes have the same priority, no priority is used.
-   **Enabled:** Toggles audio volume on or off.

In the image below, a small area is nested inside a larger one. Each space has its own audio volume (note the yellow volume outlines around the two spaces) for defining the different reverbs and ambient zone settings.

![Nested Audio Volumes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a0865ff-10f6-416c-8c65-9deadbdc04fb/03-nested-audio-volumes.png)

If the listener is within the smaller space, they are inside both of the audio volumes, so it's necessary to define how the audio engine chooses which audio volume to use. When audio volumes overlap, the one with the higher priority is used by the audio engine.

In this case, it would make sense to set the larger audio volume to 1, and the smaller to 2. This way, when inside of the smaller space, the appropriate reverb and ambient zone settings are used.

## Reverb

You can use the **Reverb** settings to turn audio volume on or off, select a reverb preset for use when activated, and define the volume of the reverb signal and the fade time between reverb settings.

![Audio Volume Reverb Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04b0d7e8-e47f-49db-bb22-d3d472d64cea/04-reverb-settings.png)

-   **Apply Reverb:** Enables or disables the reverb effect assigned below.
-   **Reverb Effect:** Determines the Reverb Effect asset that will be used. There are a number of reverb presets included within the engine content, or you can create your own reverb effect assets within the Content Browser.
-   **Reverb Plugin Effect:** Determines the Reverb Plugin Effect that will be used. If you're using a third-party audio plugin (such as Google Resonance), select the reverb effect that the plugin will use from the dropdown menu options.
-   **Volume:** Set the volume level for the reverb effect. The default setting is 0.5.
-   **Fade Time:** The time (in seconds) it takes to interpolate from the current reverb settings to the new ones as you enter and leave audio volumes. Determines the transition times between areas within a Level — there is a balance to be struck between how responsive the system is and how much movement the settings have to make to reach the new values. For example, if you were moving from a space with very little reverb to one with very long reverb times, then you might want to use longer transition times to avoid abrupt changes when moving between spaces. A move between spaces with similar reverb settings could transition more quickly.

## Brush Settings

**Brush settings** define the overall shape of the audio volume, and set the initial size of the volume (before the scaling values from above are applied).

![Audio Volume Brush Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82fe75e1-b425-4e92-9549-34eafee7b8e4/05-brush-settings.png)

Select the **Brush Shape** for the audio volume that would provide best coverage for the area. The remaining settings below Brush Shape change based on the shape chosen.

You can use **Geometry Editing mode** to alter any of the shapes provided to create bespoke (customized) shapes that better fit specific areas within your Level. Some brush shapes can be set to hollow, and while this *can* work (for instance, when the audio volume only has an effect between the interior and exterior walls), it is not recommended for general audio use. The **Brush Editor** was primarily designed to build geometry for level designers, so some of the available shapes may be impractical for audio use.

## Brush Shapes

Click the **Brush Shape** dropdown menu to display and select from a list of built-in shapes:

![Brush Shapes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01fb016a-49ed-4bb3-8fd2-5b6fd17ffb50/06-brush-shapes-dropdown-menu.png)

### Box (CubeBuilder)

The default shape, this shows up as **CubeBuilder** in the dropdown menu. This shape produces a cube-shaped audio volume.

![Box Brush Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/699655be-6fc8-40be-b0d8-ec687de5a3f2/07-cube-shaped-audio-volume.png "Audio Volume with a Box Shape")

For the Box Brush shape, the following options are available:

-   **X, Y, Z:** Determines the initial size of the box-shaped audio volume when it is first created. These values are then scaled according to the values of the Scale property above.
-   **Wall Thickness:** Only active when the Hollow option is enabled, and determines the thickness of the walls if the audio volume is set to be hollow.
-   **Hollow:** Determines whether the audio volume is hollow. This is an inherited feature from the parent volume class and is not recommended for general audio use.
-   **Tessellated**: Determines whether extra internal faces are generated for each cube face.
-   **Display Shaded Volume**: Displays the brush with a shaded volume when checked.
-   **Shaded Volume Opacity Value**: A value between 0–1 to set opacity for the shaded volume.

### Cone (ConeBuilder)

Select **ConeBuilder** in the dropdown menu to produce a cone-shaped audio volume.

![Cone Brush Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f4db9f33-735b-43f0-b8d3-d9a27079ec32/08-cone-shaped-audio-volume.png "Audio Volume with a Cone Shape")

The following options are available for this shape:

-   **Z:** Determines the initial height of the cone, from base to tip. It is then scaled according to the Z value within the Scale property under Transform settings.
-   **Cap Z:** Only active when the Hollow option is enabled. It determines the height of the inner cone.
-   **Outer Radius:** The initial radius of the cone-shaped audio volume, which is then scaled according to the X and Y values of the Scale property under Transform settings. This allows you to produce non-symmetrical cones.
-   **Inner Radius:** Only active when the Hollow option is enabled. It determines the radius of the inner cone.
-   **Sides:** Determines the number of sides of the cone, which in turn affects how closely the base approximates a circle.
-   **Hollow:** Determines whether the audio volume is hollow. This is an inherited feature from the parent volume class and is not recommended for general audio use.
-   **Align to Side**: Enables or disables aligning the brush to a face.
-   **Display Shaded Volume**: Displays the brush with a shaded volume when checked.
-   **Shaded Volume Opacity Value**: A value between 0–1 to set opacity for the shaded volume.

### Curved Stair (CurvedStairBuilder)

Select **CurvedStairBuilder** in the dropdown menu to produce a curved-stair-shaped audio volume. This shape is inherited from the parent volume Class. While it can be used for audio, it may not be practical.

![Curved Stair Brush Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/48df0d50-1ee5-4e9b-b705-25ddf0f6dea5/09-curved-stair-shaped-audio-volume.png "Audio Volume with a Curved Stair Shape")

The following options are available for this shape:

-   **Inner Radius:** Determines the initial inner radius of the curved-stair audio volume. This value is scaled according to the X and Y values of the Scale property above.
-   **Step Height:** Sets the initial height of the steps within the curved-stair audio volume. This value is scaled according to the Z value of the Scale property above.
-   **Step Width:** Determines the width of the steps within the curved stair audio volume.
-   **Angle of Curve:** The angle of the total curve of the curved stair audio volume.
-   **Num Steps:** The number of steps within the curved stair audio volume.
-   **Add to First Step:** The amount the volume should drop below the level of the first step.
-   **Counter Clockwise**: Determines whether the stair curves clockwise or counter-clockwise.
-   **Display Shaded Volume**: Displays the brush with a shaded volume when checked.
-   **Shaded Volume Opacity Value**: A value between 0–1 to set opacity for the shaded volume.

### Cylinder (CylinderBuilder)

Select **CylinderBuilder** in the dropdown menu to produce a cylinder-shaped audio volume.

![Cylinder Brush Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/facda089-da54-4a1f-8e08-f86ec62837ba/10-cylinder-shaped-audio-volume.png "Audio Volume with a Cylinder Shape")

The following options are available for this shape:

-   **Z:** Determines the initial height of the cylinder. It is then scaled according to the Z value within the Scale property under Transform settings.
-   **Outer Radius:** The initial radius of the cylinder-shaped audio volume, which is then scaled according to the X and Y values of the Scale property under Transform settings. This allows you to produce non-symmetrical cylinders.
-   **Inner Radius:** Only active when the Hollow option is enabled. It determines the radius of the inner cylinder.
-   **Sides:** Determines the number of sides the cone has, which in turn affects how closely the base approximates a circle.
-   **Hollow:** Determines whether the audio volume is hollow. This is an inherited feature from the parent volume class and is not recommended for general use.
-   **Align to Side**: Enables or disables aligning the brush to a face.
-   **Display Shaded Volume:** Displays the brush with a shaded volume when checked.
-   **Shaded Volume Opacity Value:** A value between 0–1 to set opacity for the shaded volume.

### Linear Stair (LinearStairBuilder)

Select **LinearStairBuilder** in the dropdown menu to produce a linear-stair-shaped audio volume.

This shape is inherited from the parent volume Class. While it can be used for audio, it may not be practical.

![Linear Stair Brush Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29eab72b-838f-46ba-8c5e-29c85afd10ba/11-linear-stair-shaped-audio-volume.png "Audio Volume with a Linear Stair Shape")

The following options are available for this shape:

-   **Step Length:** Determines the initial length (depth) of the steps within the linear-stair audio volume. This value is scaled according to the X value of the Scale property above.
-   **Step Height:** Determines the initial height of the steps within the linear-stair audio volume. This value is scaled according to the Z value of the Scale property above.
-   **Step Width:** The width of the steps within the curved stair audio volume. This value is scaled according to the Y value of the Scale property above.
-   **Num Steps:** The number of steps within the curved stair audio volume.
-   **Add to First Step:** The amount the volume should drop below the level of the first step.
-   **Display Shaded Volume:** Displays the brush with a shaded volume when checked.
-   **Shaded Volume Opacity Value:** A value between 0–1 to set opacity for the shaded volume.

### Sphere (TetrahedronBuilder)

Select **TetrahedronBuilder** in the dropdown menu to produce a spherical audio volume.

![Sphere Brush Shape](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0f6e46e4-4abc-4db4-b241-dd9a506358bd/12-spherical-audio-volume.png "Audio Volume with Spherical Shape")

The following options are available for this shape:

-   **Radius:** Determines the initial radius of the sphere. It is then scaled according to the X, Y, and Z values within the Scale property under Transform settings. This allows you to produce non-symmetrical spheres.
-   **Tessellation:** Sets the number of iterations the audio volume will use to calculate the sphere shape, which influences how closely the base approximates a sphere.
-   **Display Shaded Volume:** Displays the brush with a shaded volume when checked.
-   **Shaded Volume Opacity Value:** A value between 0–1 to set opacity for the shaded volume.