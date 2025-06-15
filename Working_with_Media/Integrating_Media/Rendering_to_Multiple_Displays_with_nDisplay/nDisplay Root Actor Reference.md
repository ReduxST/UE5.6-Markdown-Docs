# nDisplay Root Actor Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:38:23

---

With the **nDisplay Root Actor**, you can modify its settings while the nDisplay cluster is launched and rendering on all the nodes. This allows you to quickly make changes to the nDisplay renders without needing to modify the nDisplay configuration through the **nDisplay 3D Config Editor**.

Typically, once you create your nDisplay topology, you won't need to modify it. Since the nDisplay Root Actor is an instance of the **nDisplay Configuration Asset**, the nDisplay Root Actor settings cover the cases where you'll want to change how the nDisplay renders look on specific nodes without changing the configuration asset itself.

To create the nDisplay Root Actor, drag the nDisplay Config Asset into the level. This creates a preview of the nDisplay Cluster in the project so you can see how your content looks in your clustered rendering setup.

This page covers all the settings you'll want to use on the nDisplay Root Actor while you're either previewing in the Editor, or in the live environment with your physical nDisplay cluster.

## nDisplay Root Actor Settings

To access the nDisplay Root Actor's settings, select your nDisplay Root Actor in the **World Outliner** to open its **Details** panel.

The following sections describe the settings for the nDisplay Root Actor.

### Viewports

| Parameter | Description |
| --- | --- |
| **Viewport Screen Percentage Multiplier** | 
This parameter defines the resolution for the viewport. 1.0 means full resolution.

In complex and large clustered rendering setups, we recommend lowering this value to improve the Editor's frame rate during preview. Lowering the value lowers the resolution of what's displayed.



 |
| **Viewport Screen Percentage** | 

Dropdown section that shows all viewports in the nDisplay cluster. Set the Viewport screen percentage per viewport. The **Viewport Screen Percentage Multiplier** is combined with the per-viewport screen percentage setting to determine the resolution.

This is especially useful for viewports that are used only for lighting during in-camera VFX shoots. You will typically want to lower the resolution for the ceiling displays, unless you need high quality reflections from them in your scene.



 |
| **Viewport Overscan** | 

With Viewport Overscan enabled, the Engine will render a larger frame than specified for the viewport, to achieve continuity across displays when using post-processing effects. See [Overscan Support](/documentation/en-us/unreal-engine/ndisplay-overscan-in-unreal-engine) for more details on what is supported with overscan in nDisplay.

Expand the dropdown to show all viewports in the nDisplay cluster, and change overscan settings per viewport. See Viewport Overscan Settings Per Viewport below for the per-viewport options.



 |
| **Freeze Viewports** | Freezes rendering for viewports displaying the outer frustum. Disabling this option can help to improve performance. |
| **Content Hidden from Entire Cluster** | 

Content added to the arrays here will not show up on any display in the cluster, and will not appear in the inner frustum if it's enabled. Content can be added by specifying [Layers](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine), or Actors individually.

This is useful for cases when you need an Actor in your project but don't want it displayed through nDisplay. For example, if you're using an Actor for tracking during an in-camera VFX shoot and don't want it displayed but need it for compositing with Composure.



 |
| **Content Hidden from Viewports** | Content added to the arrays here will not show up on the outer frustum, but will appear in the inner frustum if it's enabled. Content can be added by specifying [Layers](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine), or Actors individually. |

#### Viewport Overscan Settings Per Viewport

| Parameter | Description |
| --- | --- |
| **Enable** | Enable or disable overscan for the viewport. |
| **Mode** | 
Specify the units for overscan. Options include:

-   Percentage
-   Pixels



 |
| **Adapt Resolution** | 

When enabled, the resolution of the rendering output increases based on the settings below.

When disabled, the rendering output is scaled from the original resolution of the viewport to reach the size in the settings below.

This option is enabled by default.



 |
| **Left** | If overscan is enabled, increases the resolution for the **left** side of the render by this amount. Units are in pixels or percent, depending on which **Mode** is selected. |
| **Right** | If overscan is enabled, increases the resolution for the **right** side of the render by this amount. Units are in pixels or percent, depending on which **Mode** is selected. |
| **Top** | If overscan is enabled, increases the resolution for the **top** of the render by this amount. Units are in pixels or percent, depending on which **Mode** is selected. |
| **Bottom** | If overscan is enabled, increases the resolution for the **bottom** of the render by this amount. Units are in pixels or percent, depending on which **Mode** is selected. |

### In-Camera VFX

| Parameter | Description |
| --- | --- |
| **Enable Inner Frustum** | 
Enable this option if you want to use the inner frustum with your nDisplay setup. Disabling this option overrides the [inner frustum settings](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#icvfxcamcomp) on the individual ICVFX cameras.

When you have multiple cameras, disabling this option disables the inner frustum for all of them.



 |
| **Inner Frustum Priority** | This list determines which camera's inner frustum is rendered on top, when you have multiple ICVFX cameras and their inner frustums overlap on the display. The priority is determined by the order of the list, with the first camera as the highest priority. |

### Color Grading

This section describes the specific settings available for color grading in nDisplay. See [Color Management in nDisplay](/documentation/en-us/unreal-engine/color-management-in-ndisplay-in-unreal-engine) for more information on how to use color grading in your project.

| Parameter | Description |
| --- | --- |
| **Enable Entire Cluster Color Grading** | 
When enabled, applies the color grading settings from the **Entire Cluster** section to all the nDisplay viewports and inner frustums.

The color grading is only applied to nDisplay renders. It will not change the color of the project in the Editor, or the renders from [Movie Render Queue](/documentation/404).



 |
| **Entire Cluster** | Expand the section to view the color grading options. See [Color Correction](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorcorrection) for details on the color grading options exposed. |
| **Per-Viewport Color Grading** | Refer [Per-Viewport Color Grading](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#per-viewportcolorgrading) for details. |

#### Per-Viewport Color Grading

You can apply color grading settings to an individual viewport or to groups of viewports. Add an Array element and modify the settings described in the following table to apply color grading to specific viewports.

| Parameter | Description |
| --- | --- |
| **Enable Viewport Color Grading** | 
When enabled, applies the color grading settings from the **Color Grading** section to all viewports defined in **Apply Color Grading to Viewports**.

The color grading is not applied to inner frustums that appear on the nodes, if they're enabled. To apply color grading only to an inner frustum, see the [Color Grading](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#innerfrustumcolorgrading) section of the ICVFX Camera settings.



 |
| **Include Entire Cluster Color Grading** | 

When enabled, applies the color grading settings defined in **Entire Cluster** before applying the settings defined in the **Color Grading** section to the specific viewport.

When disabled, the color grading settings defined in **Entire Cluster** will not be applied to the viewport. The settings defined in **Color Grading** will still be applied to the viewport if **Enable Viewport Color Grading** is enabled.



 |
| **Color Grading** | Expand the section to view the color grading options. See [Color Correction](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorcorrection) for details on the color grading options exposed. |
| **Apply Color Grading to Viewports** | 

The color grading settings can be applied to multiple viewports. Add an Array element for each viewport to which you want to apply these color grading settings.

The list of viewports shown in the dropdown is the same as the list defined in the nDisplay Config Asset.



 |

### OCIO

This section describes the specific settings available for color management with OpenColorIO (OCIO) in nDisplay. See [Color Management in nDisplay](/documentation/en-us/unreal-engine/color-management-in-ndisplay-in-unreal-engine) for more information on how to use OpenColorIO in your project.

| Parameter | Description |
| --- | --- |
| **Enable Viewport OCIO** | 
When enabled, applies the OCIO configuration to all nDisplay viewports.

The configuration is not applied to inner frustums that appear on the nodes, if they're enabled. To apply an OCIO configuration only to an inner frustum, see the [OCIO](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#ocio_params) section of the ICVFX Camera Component settings.

The OpenColorIO configuration set here is only applied to nDisplay renders. It will not change the color of the project in the Editor, or the renders from [Movie Render Queue](/documentation/404).

If you already have an OCIO configuration applied to your project, this will override those settings on the nDisplay viewports.



 |
| **All Viewports Color Configuration** | Expand this section to set the **Configuration Source**, **Source Color Space**, and **Destination Color Space**. See [Color Management with OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more details on using OpenColorIO in your project. |
| **Per-Viewport OCIO Overrides** | You can apply OCIO settings to an individual viewport or groups of viewports. Add an Array element and modify the settings described in Per-Viewport Array Elements to apply color grading to specific viewports. |

#### Per-Viewport OCIO Overrides Array Elements

| Parameter | Description |
| --- | --- |
| **Enable Per-Viewport OCIO** | 
When enabled, applies the OCIO configuration from the **Viewport OCIO** section to all viewports defined in **Apply OCIO to Viewports**.

If you already have an OCIO configuration applied to your project or all your nDisplay viewports, this will override those settings on the nDisplay viewports defined in **Apply OCIO to Viewports**.

The configuration is not applied to inner frustums that appear on the nodes, if they're enabled. To apply OCIO configurations only to an inner frustum, see the [OCIO](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#ocio_params) section of the ICVFX Camera Component settings.



 |
| **Viewport OCIO** | Expand this section to set the **Configuration Source**, **Source Color Space**, and **Destination Color Space**. See [Color Management with OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more details on using OpenColorIO in your project. |
| **Apply OCIO to Viewports** | 

The OCIO settings can be applied to multiple viewports. Add an Array element for each viewport to which you want to apply these OCIO settings.

The list of viewports shown in the dropdown is the same as the list defined in the nDisplay Config Asset.



 |

### Light Cards

| Parameter | Description |
| --- | --- |
| **Enable Light Cards** | When enabled, all Light Cards defined in Light Cards Content will be displayed in the nDisplay viewports. |
| **Blending Mode** | 
There are two modes for how Light Cards are rendered when the inner frustum overlaps them:

-   **Lightcard Over Frustum:** The Light Card renders on top of the inner frustum when they overlap.
-   **Lightcard Under Frustum:** The Light Card is hidden by the inner frustum when they overlap.



 |
| **Light Cards Content** | Light Cards can be added by specifying [Layers](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine), or Actors individually. |

### Editor Preview

| Parameter | Description |
| --- | --- |
| **Enable Editor Preview** | 
When enabled, a preview of the Unreal Project appears on the nDisplay Root Actor's meshes in the Level Viewport. The Color Management options and other settings defined in the nDispay Root Actor will appear in the preview.

This option is enabled by default. We recommend disabling this option when you're not previewing in the Level Viewport and need to improve performance.



 |
| **Preview Screen Percentage** | This parameter defines the value by which the preview texture's resolution is scaled. |
| **Enable Post Process** | When enabled, post process settings are applied to the nDisplay preview in the Level Viewport. |
| **Freeze Editor Preview** | When enabled, the viewport renders for the nDisplay preview freezein the Level Viewport. |
| **Enable Camera Frustums** | When enabled, visualizations for the inner frustum appear with the ICVFXCamera as the origin. |
| **Camera Frustum Distance** | This parameter defines the maximum distance where the inner frustum can be rendered. |
| **Preview Node** | This parameter defines which nodes you want to preview in the Level Viewport. Options are **None**, **All**, or specific Cluster Nodes in your nDisplay cluster. |
| **Render Mode** | 

This parameter defines the Render Mode for the nDisplay cluster preview. Options include:

-   Mono
-   Stereo: Side By Side
-   Stereo: Top Bottom

See [Stereoscoping Rendering in nDisplay](/documentation/en-us/unreal-engine/stereoscopic-rendering-with-ndisplay-in-unreal-engine) for more details on the options.



 |
| Advanced |   |
| **Tick Per Frame** | This parameter defines the time interval between updates for the preview in the Editor. |
| **Viewports Per Frame** | 

This parameter defines how many viewports are rendered per frame for the preview in the Editor. If this parameter is set to less than the number of viewports in the cluster, then the number of preview viewports specified in this parameter are updated each frame.

For example, if Viewports Per Frame is 1 and your cluster has 2 viewports (VP0, VP1), then the preview viewports are updated over multiple frames: VP0 on frame 0, VP1 on frame 1, VP0 on frame 2, and so on.

If Viewports Per Frame is set to a number greater than the number of viewports in the cluster, then all the preview viewports are updated once per frame. For larger clusters, updating every viewport in the preview can be expensive, so you can adjust this parameter to improve performance in the Editor.



 |
| **Preview Texture Max Size** | This parameter defines the maximum dimension of textures for preview. By default, the value is 2048. When you have large preview viewports, you can use less memory by changing this value. |

## In-Camera VFX Camera Component Settings

To access the nDisplay Root Actor's ICVFX Camera Component settings:

-   Select your nDisplay Root Actor in the **World Outliner** to open its **Details** panel.
-   In the nDisplay Root Actor's **Details** panel, select the **ICVFX Camera Component** in the Components section to open its **Details** panel.

The following sections describe the settings for the ICVFX Camera Component of the nDisplay Root Actor.

### In-Camera VFX

| Parameter | Description |
| --- | --- |
| **Enable Inner Frustum** | When enabled, shows the inner frustum from this ICVFX camera in the nDisplay cluster. |
| **Cine Camera Actor** | When you assign a Cine Camera Actor to this parameter, that camera is used to render the inner frustum instead of the default nDisplay camera. |
| **Inner Frustum Screen Percentage** | This parameter defines the percent multiplier for the resolution of the inner frustum. 1.0 is the same as full resolution. |
| **Inner Frustum Overscan** | Refer to [Inner Frustum Overscan](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#innerfrustumoverscan) for more details. |
| **Soft Edge** | 
These parameters define how much of the edges are feathered. You can set the **Top and Bottom**, and the **Sides** of the edges separately.

It can be useful to feather the inner frustum's edges so its hard line doesn't appear in a reflection during an in-camera VFX shot.



 |
| **Inner Frustum Border** | These parameters create a border around the inner frustum. You can set Border Width and Border Color to customize the border's appearance. |
| **Inner Frustum Rotation** | This rotation offset is applied to the inner frustum. |
| **Inner Frustum Offset** | This translation offset is applied to the inner frustum. |
| **Mipmapping** | 

When the inner frustum is smaller, in terms of LED wall pixels, than the resolution you configure nDisplay to render, mipmaps can be generated to create a nicer small inner frustum. Generating mipmaps for the inner frustum might affect performance slightly.

To use mipmapping on your inner frustum, enable **Auto Generate Mips**. You can choose which mips sampler filter to use:

-   Nearest
-   Bi-linear
-   Tri-linear
-   Default (from Texture Group)

**Auto Generate Mips** and the **Tri-linear** sampler filter are selected by default for the ICVFX camera.



 |
| **Camera Motion Blur** | See [Camera Motion Blur](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#cameramotionblur) for more. |
| **Content Hidden from Inner Frustum** | Any Actors added here will not display in the inner frustum. Content can be added by specifying [Layers](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine), or Actors individually. |

#### Inner Frustum Overscan

You can specify inner frustum overscan per direction. For in-camera-VFX scenarios, this feature can be useful for extending the inner frustum in specific directions to accommodate the latency of moving cameras or reducing the rendered size of the frustum if it's partially obscured by the set. Its resolution can optionally auto-adapt to maintain the same visual quality. Refer to [Overscan Support](/documentation/en-us/unreal-engine/ndisplay-overscan-in-unreal-engine) for details on which features work with overscan.

| Parameter | Description |
| --- | --- |
| **Estimated Overscan Resolution** | 
This parameter displays the resolution that is being sent to the output, which may or may not be scaled. When you change the overscan settings below, this resolution reflects the changes.

For example, if the render target resolution is 3840 x 2160, and **Overscan Multiplier** is set to 2, then **Estimated Overscan Resolution** will be 7680 x 4320.



 |
| **Inner Frustum Resolution** | This parameter displays the resolution of the render target, which is defined in the nDisplay Config Asset. When Adapt Resolution is enabled, this resolution reflects the aspect ratio changes made by the overscan settings below. |
| **Enable Inner Frustum Overscan** | When enabled, overscan is applied to the inner frustum. |
| **Adapt Resolution** | 

When enabled, the resolution of the render target changes based on the overscan settings below.

When disabled, the rendering output is scaled from the original resolution of the viewport to reach the size in the settings below.

This option is disabled by default.



 |
| **Overscan Multiplier** | Multiplies the field of view for the ICVFX camera by this value. This can increase the overall size of the inner frustum to help provide a buffer against latency when moving the camera. |
| **Overscan Units** | 

Specify the units for overscan. Options include:

-   Percentage
-   Pixels



 |
| **Left** | If overscan is enabled, increases the resolution for the left side of the render by this amount. Units are in pixels or percent, depending on which Overscan Units is selected. |
| **Right** | If overscan is enabled, increases the resolution for the right side of the render by this amount. Units are in pixels or percent, depending on which Overscan Units is selected. |
| **Top** | If overscan is enabled, increases the resolution for the top of the render by this amount. Units are in pixels or percent, depending on which Overscan Units is selected. |
| **Bottom** | If overscan is enabled, increases the resolution for the bottom of the render by this amount. Units are in pixels or percent, depending on which Overscan Units is selected. |

#### Camera Motion Blur

The settings for specifying motion blur in the nDisplay render. Refer to [Camera Motion Blur](/documentation/en-us/unreal-engine/camera-motion-blur-with-ndisplay-in-unreal-engine) for how to set up your projects to work with motion blur.

| Parameter | Description |
| --- | --- |
| **Motion Blur Mode** | 
Specify the motion blur mode for the inner frustum and how it corrects for the motion of the camera. Blur due to camera motion will be incorrectly doubled in the physically exposed image if there is already camera blur applied to the inner frustum.

There are three modes:

-   **ICVFX Camera Blur Off:** Subtracts blur due to motion of the ICVFX camera relative to the nDisplay root, but preserves blur from both object motion and movement of the nDisplay root, which can be animated to represent vehicular motion through an environment.
-   **ICVFX Camera Blur On:** Allows blur from camera motion. This option should not normally be used for camera shooting, but may be useful for diagnostic purposes.
-   **All Camera Blur Off:** Subtracts blur due to all global motion of the ICVFX camera, but preserves blur from object motion.

**ICVFX Camera Blur Off** is selected by default.



 |
| **Translation Scale** | This parameter defines how much translation should be scaled for generating motion blur. |
| 

**Motion Blur Settings Override**



 |   |
| **Enable Settings Override** | If enabled, override the overall motion blur settings that would otherwise come from the current post-process volume or CineCamera. |
| **Amount** | This parameter defines the strength of the motion blur. |
| **Max** | This parameter defines the max distortion caused by motion blur, specified by screen width percentage. |
| **Per Object Size** | 

This parameter defines the minimum projected screen radius for a primitive to be drawn in the velocity pass. This parameter is specified in terms of screen width percentage. The smaller the number, the more draw calls there are.

The default value is **4%**.



 |

### Inner Frustum Color Grading

| Parameter | Description |
| --- | --- |
| All Nodes |   |
| **Enable All Nodes Color Grading** | 
When enabled, applies the color grading settings from the **Color Grading** section to the inner frustum.

The color grading is only applied to nDisplay renders.



 |
| **Include Entire Cluster Color Grading** | When enabled, applies the color grading settings from the [Entire Cluster](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#entirecluster) section of the nDisplay Root Actor to the inner frustum. |
| **Color Grading** | Expand the section to view the color grading options. See [Color Correction](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorcorrection) for details on the color grading options exposed. |
| Per-Node Color Grading |   |
| **Enable Per-Node Color Grading** | 

When enabled, applies the color grading settings from the **Color Grading** section to the inner frustum when it appears on the cluster nodes defined in **Apply Color Grading to Nodes**.

The finest granularity of control for the inner frustum in the nDisplay cluster is per-node. This is because the inner frustum can be shared across multiple viewports when mGPU is enabled.

The color grading is only applied to nDisplay renders.



 |
| **Include Entire Cluster Color Grading** | When enabled, applies the color grading settings from the [Entire Cluster](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#entirecluster) section of the nDisplay Root Actor to the inner frustum when it appears on the cluster nodes defined in **Apply Color Grading to Nodes**. |
| **Include All Nodes Color Grading** | When enabled, applies the color grading settings from the [All Nodes](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine#allnodes) section of the ICVFX Camera Component to the inner frustum when it appears on the cluster nodes defined in **Apply Color Grading to Nodes**. |
| **Color Grading** | Expand the section to view the color grading options. See [Color Correction](/documentation/en-us/unreal-engine/color-grading-and-the-filmic-tonemapper-in-unreal-engine#colorcorrection) for details on the color grading options exposed. |
| **Apply Color Grading to Nodes** | 

The color grading settings can be applied to multiple cluster nodes. Add an Array element for each cluster node to which you want to apply these color grading settings.

The list of cluster nodes shown in the dropdown is the same as the list defined in the nDisplay Config Asset.



 |

### OCIO

| Parameter | Description |
| --- | --- |
| **Enable Inner Frustum OCIO** | 
When enabled, applies the OCIO configuration from the **All Nodes Color Configuration** section to the inner frustum.

If you already have an OCIO configuration applied to your project, this will override those settings for the inner frustum.

The OCIO configuration is only applied to nDisplay renders.



 |
| **All Nodes Color Configuration** | Expand this section to set the **Configuration Source**, **Source Color Space**, and **Destination Color Space**. See [Color Management with OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more details on using OpenColorIO in your project. |
| **Per-Node OCIO Overrides** | 

The OCIO settings can be applied to multiple cluster nodes. Add an Array element for each cluster node to which you want to apply these OCIO settings.

The list of cluster nodes shown in the dropdown is the same as the list defined in the nDisplay Config Asset.

The finest granularity of control for the inner frustum in the nDisplay cluster is per-node. This is because the inner frustum can be shared across multiple viewports when mGPU is enabled.



 |

#### Per-Node OCIO Overrides

| Parameter | Description |
| --- | --- |
| **Enable Per-Node OCIO** | 
When enabled, applies the OCIO configuration from the **Inner Frustum OCIO** section to the inner frustum when it appears on the cluster nodes defined in **Apply OCIO to Nodes**.

If you already have an OCIO configuration applied to your project or to the inner frustum for all cluster cluster nodes, this will override those settings for the inner frustum when it appears on the cluster nodes defined in Apply OCIO to Nodes.

The OCIO configuration is only applied to nDisplay renders.



 |
| **Inner Frustum OCIO** | Expand this section to set the **Configuration Source**, **Source Color Space**, and **Destination Color Space**. See [Color Management with OpenColorIO](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more details on using OpenColorIO in your project. |
| **Apply OCIO to Nodes** | 

The OCIO configuration can be applied to multiple cluster nodes. Add an Array element for each cluster node to which you want to apply these settings.

The list of cluster nodes shown in the dropdown is the same as the list defined in the nDisplay Config Asset.



 |

### Chromakey

| Parameter | Description |
| --- | --- |
| **Enable Inner Frustum Chromakey** | 
When enabled, turns the entire inner frustum the solid color set in **Chromakey Color** and applies **Chromakey Markers** if they're enabled.

This setting is typically used to apply a green screen and tracking markers to the display during an in-camera VFX shoot. Since only the inner frustum changes, the outer frustum can continue to be used for reflections while filming.



 |
| **Chromakey Color** | This parameter defines the color used for chroma keying. |
| 

**Chromakey Markers**



 |   |
| **Enable Chromakey Markers** | When enabled, tracking markers are generated and applied to the inner frustum's chroma key content. |
| **Marker Color** | This parameter defines the color of the tracking marker. |
| **Marker Tile RGBA** | This parameter defines the texture used for the tracking marker. A texture with a plus icon is assigned by default. |
| **Marker Scale** | This parameter defines the size of the tracking marker. |
| **Marker Tile Distance** | This parameter defines the distance between tracking markers. |
| **Marker Tile Offset** | This parameter defines an offset applied to the tracking markers' default location. |
| 

**Custom Chromakey**



 |   |
| **Use Custom Chromakey** | 

When enabled, only turns the content defined in **Custom Chromakey** to the **Chromakey Color** and applies **Chromakey Markers** when the content appears in the inner frustum. The content is hidden in the outer frustum and will only appear in the inner frustum.

This setting is for green screen halo.



 |
| **Custom Chromakey Content** | Content can be added by specifying [Layers](/documentation/en-us/unreal-engine/layers-panel-in-unreal-engine), or Actors individually. |
| **Post Process Blur** | 

You can choose to apply a blur to the content defined in **Custom Chromakey** Content.

There are three modes you can set **Post Process Blur** to:

-   None
-   Gaussian
-   Dilate

For **Gaussian** and **Dilate**, you can set the **Kernel Radius** and **Scale** to change the look of the effect.



 |

### Texture Replacement

| Parameter | Description |
| --- | --- |
| **Enable Viewport Texture Replacement** | 
When enabled, replaces the inner frustum view with the texture defined in **Source Texture**. The texture moves with the camera.

The replacement won't be visible if the entire inner frustum is used for chroma keying.



 |
| **Source Texture** | The texture applied to the inner frustum when **Enable Viewport Texture Replacement** is checked. |
| **Use Texture Crop** | When enabled, only uses the rectangle defined in **Texture Crop** of the **Source Texture**. |
| 

**Texture Crop**



 |   |
| **Texture Crop Origin** | Defines the upper left corner of the rectangle using the **X** and **Y** parameters. |
| **Texture Crop Size** | Defines the width and height of the rectangle from the starting point using the **W** and **H** parameters. |