# Transform and Property Tracks

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine)  
**Processed:** 2025-06-14 16:13:23

---

Sequencer contains various **Property Tracks** you can use to animate Actors' common property types. Using these tracks, you can animate properties such as Transform, Color, or Booleans. This guide provides an overview of the various Property Track types that exist in Sequencer.

#### Prerequisites

-   You have an understanding of [Sequencer](/documentation/en-us/unreal-engine/how-to-make-movies-in-unreal-engine) and its [Interface](/documentation/en-us/unreal-engine/sequencer-cinematic-editor-unreal-engine).

## Transform Track

One of the most commonly-used tracks in Sequencer is the **Transform track**. You can use this track to animate the movement of objects, cameras, and characters in your scene.

![sequencer transform track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e251b07e-523c-4e58-af52-398cf5583290/transformtrack.png)

### Creation

By default, whenever a [Static Mesh](/documentation/en-us/unreal-engine/static-meshes), [Skeletal Mesh](/documentation/en-us/unreal-engine/skeletal-mesh-assets-in-unreal-engine), or [Camera](/documentation/en-us/unreal-engine/cinematic-cameras-in-unreal-engine) is added to Sequencer, a Transform track will automatically be added under them.

To manually add a Transform track, click **Add Track (+)** on your [Actor Track](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine), and select **Transform**.

![add transform track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/faaa497c-31b1-458b-868e-b119d2dc20db/addtransform.png)

The automatic adding of the Transform track under certain tracks is enabled from the **Project Settings**, and can be customized to occur for other Actor class types under the [Track Setting Project Setting](/documentation/en-us/unreal-engine/cinematic-editor-and-project-settings-in-unreal-engine#projectsettings).

### Usage

Transform tracks can be expanded to view individual channels or axes. Selecting these channel or axis tracks and pressing **Enter** will allow you to place keyframes on those specific tracks.

![expand transform track channel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4872872-ebd9-428f-9c62-c63f83ed57bd/expandtransform.gif)

Channels and axes can also be disabled and removed from view if you don't need them. To do this, right-click the transform section and enable or disable channels under the **Active Channels** category. Removing any channel or axis will cause those tracks to not be evaluated by Sequencer and to not respond to [Auto Keying](/documentation/en-us/unreal-engine/sequencer-cinematic-toolbar-in-unreal-engine#autokey).

![transform track channels](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2551821-7f9f-4a3c-8daf-154307e09103/channels.png)

### Properties

The Transform track section contains properties to assist with improving control on your Transforms. Right-click a Transform track section and select Properties to view them.

![transform track properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5492a704-4148-4edf-89a7-c62e801d4687/transformproperties.png)

The **Use Quaternion Interpolation** option enables quaternion linear interpolation between transform keyframes. Quaternion interpolation helps reduce **Gimbal lock** and other Euler-based problems with rotations.

|   |   |
| --- | --- |
| ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b656f53-5216-4844-93cb-70638102691b/quat1.gif) | ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a137065-c1eb-4a22-9021-341f8fe39732/quat2.gif) |
| Use Quaternion Interpolation Disabled | Use Quaternion Interpolation Enabled |

**Show 3D Trajectory** contains options for drawing trajectory paths for the Transform track.

![show 3d trajectory](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dc1f53c-cce7-4962-9212-90445811b83e/trajectory.png)

These options include:

-   **Only When Selected,** which will only draw the trajectory when the object or track is selected.
-   **Always,** which will always draw the trajectory regardless of selection.
-   **Never,** which will never draw the trajectory.

Regardless of the chosen trajectory setting, the trajectory will always hide when [Game View](/documentation/en-us/unreal-engine/using-editor-viewports-in-unreal-engine#gameview) is enabled.

## Property Tracks

Sequencer supports the animating of various properties. Properties can be added to your [Actor Track](/documentation/en-us/unreal-engine/cinematic-actor-tracks-in-unreal-engine) in Sequencer by clicking **Add Track (+)** on your Actor and choosing one from the **Properties** category.

![sequencer property track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ea381420-00b9-41ca-8b38-e597324d88fc/addproperties.png)

### Boolean

Boolean tracks are used to animate boolean properties. Boolean tracks can only be set to enabled or disabled, and do not interpolate. The timeline will be colored **red** when set to disabled, and **green** when enabled.

![sequencer boolean track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f2f79937-9bf8-468e-b716-4fb4a50928dd/bool.png)

Booleans are also represented in the curve editor by values of **0** (disabled) and **1** (enabled).

### Integer

Integer tracks are used to animate integer properties and do not interpolate.

![sequencer integer track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/89a462c6-4c37-45ea-aeef-86aa85874050/integer.png)

### Float

Float tracks are used to animate scalar float properties. Float keyframes interpolate and can use custom tangents and curves.

![sequencer float track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8a28773-4fd0-4ab8-a5da-5139475fc124/float.png)

To assist with visualizing float value changes, you can enable float curves to be displayed in-line within a float track section.

![float track curve display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32f2bf11-3ed6-4d91-876e-2003eed24ba4/floatcurve1.png)

To enable the float track curve display, right-click on a float track section and select **Display > Show Curve**.

![float track curve display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c2dd9d8-3f92-4eb8-aa84-48cf9860b6ae/floatcurve2.png)

### Vectors

Sequencer supports animating Vector 2, 3, and 4 properties using their respective tracks. All Vector tracks interpolate and can have custom tangents and curves.

![sequencer vector track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c658e19d-724e-46f9-a5b7-18e32cf89f4d/vectors.png)

### Color

The Color track is used to animate color-specific properties in Sequencer, such as on lights or materials. The Color track supports interpolation and will also display the color set at each keyframe along the timeline so you can preview your colors at a glance.

![sequencer color track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb7b1ab1-01cf-4e46-9fae-5b6ef0167443/color.png)

To help with color selection, you can double-click a Color track keyframe to bring up the **Color Picker**. Once a color is selected, click the **OK** button and the keyframe will now be set to that color.

![sequencer color picker](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/22a53e3f-d36f-40d9-876f-b051e69424de/colorpicker.gif)

The Color track supports animating both **Color** and **Linear Color** spaces.

### String

The String track is used to animate different String values. String values do not interpolate between keyframes.

![sequencer string track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5b282f4c-b2ce-4196-8cf8-d2d3dfecd111/string.png)

### Enum

The Enum Track is used to animate different enumerated values. Enum values do not interpolate between keyframes.

![sequencer enum track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eac375df-6447-49a5-89b3-88940e5e787b/enum.png)

### Object

The Object Track is used to animate different Object and Asset values. Object values do not interpolate between keyframes.

![sequencer object track](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/82d56f2f-af29-40f5-9e49-633a37026cf8/object.png)

### UMG Properties

Sequencer supports animating properties from UI Elements in the [Creating User Interfaces](/documentation/en-us/unreal-engine/creating-user-interfaces-with-umg-and-slate-in-unreal-engine). The two main tracks used for UMG are the **Margin** and **Widget Transform Tracks**.

![sequencer umg ui property tracks](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/66f5a503-6bf3-4e7f-98bd-22cecc0a0d76/umg.png)

## Overridable Channels

Some properties can be overridden to output animation data other than normal keyframes or curves. For example, you can override float channels or individual X/Y/Z channels on transform axes to output random perlin noise. This can be useful to create procedural noise-based animation, rather than manually animating noise.

![sequencer animate noise](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a4618e5d-2b07-48e0-8b4e-1c7c9f57ddf9/override4.gif)

Currently only float/double and transform tracks support overridable channels.

To override a channel navigate either to a [Float Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#float) or an individual axis channel of a [Transform Track](/documentation/en-us/unreal-engine/cinematic-transform-and-property-tracks-in-unreal-engine#transformtrack), right-click the track and select **Override with Double Perlin Noise**.

![override with double perlin noise](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e28f7960-5cc2-4ce7-b8c9-ce4ed63a0138/override1.png)

You can modify noise parameters by right-clicking the track and navigating to **Double Perlin Noise Parameters**, where both the **Frequency** and **Amplitude** can be edited.

![double perlin noise parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b714ce0-9870-4871-9976-23c3b7ed6afc/override2.png)

Noise channels animate relative to a value of **0**. If you want your noise to animate between certain value ranges, such as between **100 - 200**, then you can create extra additive [Sections](/documentation/en-us/unreal-engine/creating-animation-keyframes-in-unreal-engine#sections), and convert those channels to noise. This way, you can have the base section at a specific value, and then noise will apply additively to that base.

![layer additive noise](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cae8954a-181b-4994-91b7-400fed010872/override3.png)

If you have overridden multiple channels within a section, you can right-click on the section and edit all noise parameters at the same time under the **Perlin Noise Channels** menu.

![change multiple noise properties](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/596a54da-53b9-4679-a643-92911369698f/override5.png)