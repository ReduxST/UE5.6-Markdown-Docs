# nDisplay Configuration File Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:38:13

---

As of Unreal Engine 4.27, you can continue to import both `.cfg` and `.ndisplay` configuration files into your project's **Content Browser** and they will be converted to the new `.uasset` format.

You can export and use `.ndisplay` configuration files to launch a cluster. The `.ndisplay` files won't have tracking and other features that can only be configured in the **nDisplay Config Asset**.

We recommend using the [nDisplay 3D Config Editor](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine) for configuring your nDisplay cluster.

You define most aspects of the nDisplay system in a single configuration file. This file includes the computers that make up your network, the characteristics of the windows and viewports you want the Unreal Engine to render on each computer, the parts of the virtual world each viewport should render, the types of input devices you want to accept, and more.

This page describes all the settings available in the nDisplay configuration file.

The best way to get started understanding the nDisplay configuration file, and creating your own, is to start from the example configurations provided by the nDisplay plugin. If you've created your Project from the nDisplay template, you'll find these files in your Project folder, under `Content/ExampleConfigs`. If not, you can find these files in the Unreal Engine installation folder, under `Templates/TP_nDisplayBP/Content/ExampleConfigs`.

The structure of the nDisplay configuration file is directly tied to the different types of components it uses to render the visualization.

-   Each different type of component that you configure has its own line in the file, and is identified by a string ID that you assign. You use these string IDs when one configuration section needs to refer to another.
    
-   Many of the components that you configure in this file have defined positions (and often rotations) in virtual 3D space. Each object's position and rotation is relative to that object's *parent*. By default, the parent of all objects is the VR space origin: an arbitrary point in 3D world space where VR space is considered to start. You can also configure specific named transforms in 3D space, called scene\_nodes, which can act as parents for one or more components. This can help simplify the spatial layout of your screens, cameras and other components. To see how you can use scene\_nodes to build a hierarchy of 3D transforms that all start from the same point in virtual space, see the [Configuration File Scene Structure Example](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#configurationfilescenestructureexample) section below.
    
-   All parameters that refer to measurements in virtual 3D space or real-world physical space expect values in meters and degrees, unless otherwise indicated. This includes screens, scene nodes, cameras, and so on.
    
-   All parameters that refer to measurements in screen space expect values in pixels. This includes windows and viewports.
    

## Cluster Node Configurations

For each different instance of your Unreal Engine application that you'll use in your nDisplay network, you need to define a **cluster\_node** configuration. Each cluster\_node configuration must contain a reference to a **[window](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#windowconfigurations)** configuration section that defines the properties of the main application window.

The cluster\_node configuration also defines the hostname or IP address of the computer that will run that application instance. You may set up a different physical computer for each cluster\_node configuration, or you may have multiple cluster\_node configurations that run on the same host.

### Example configuration:

This example configures a primary node (one per network):

```
	`[cluster_node] id=node_front addr=192.168.0.1 window=wnd_LT sound=true port_cs=41001 port_ss=41002 master=true`

Copy full snippet
```
\[cluster\_node\] id=node\_front addr=192.168.0.1 window=wnd\_LT sound=true port\_cs=41001 port\_ss=41002 master=true

This example shows a non-primary cluster node:

```
	`[cluster_node] id=node_left addr=192.168.0.2 window=wnd_large sound=false`

Copy full snippet
```
\[cluster\_node\] id=node\_left addr=192.168.0.2 window=wnd\_large sound=false

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this cluster node configuration. |
| **addr** | Required |   | The IP address of the computer that will run this instance of Unreal Engine. This must be an IPv4 address. IPv6 is not supported. |
| **window** | Required |   | The name of the **[window](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#windowconfigurations)** configuration that defines the size and position of the main window for this instance of your Unreal Engine application. |
| **sound** | Optional | `false` | Determines whether this instance of Unreal Engine plays sound. Optional; default value is `false`. |
| **port\_cs** | Optional | `14001` | The port that the primary node uses to communicate with other nodes in the cluster for cluster synchronization. **port\_ss** is for swap synchronization; **port\_ce** is for cluster events. Optional; default values are `14001,` `14002`, and `14003`. |
| **port\_ss** | Optional | `14002` | The port that the primary node uses to communicate with other nodes in the cluster for swap synchronization. |
| **port\_ce** | Optional | `14003` | The port that the primary node uses to communicate with other nodes in the cluster for cluster events. |
| **master** | Optional | `false` | Determines whether this instance of Unreal Engine is the primary node of the cluster. Only one **cluster\_node** section can have this parameter set to `true`. |
| **gpu** | Optional |   | 
Determines the index of the GPU that this instance of Unreal should use for rendering.

Setting the GPU instance in this way is equivalent to using the `r.GraphicsAdapter` console variable.



 |

## Window Configurations

Each **window** configuration defines a set of properties for the main window of an instance of your Unreal Engine application. You use it to configure things like the starting size and placement of the window when nDisplay launches your application, and whether or not the window should take up the full screen.

You also provide one or more **[viewport](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#viewportconfigurations)** configurations, which identify specific areas within the main application window that nDisplay will fill with renderings of your scene.

### Example configuration:

This example configures an application window that contains a single viewport:

```
	`[window] id=wnd_one fullscreen=false WinX=0 WinY=0 ResX=640 ResY=480 viewports=vp_LT`

Copy full snippet
```
\[window\] id=wnd\_one fullscreen=false WinX=0 WinY=0 ResX=640 ResY=480 viewports=vp\_LT

This example configures an application window that contains four separate viewports:

```
	`[window] id=wnd_four fullscreen=false WinX=0 WinY=0 ResX=640 ResY=480 viewports="vp_LT,vp_RB,vp_LB,vp_RT"`

Copy full snippet
```
\[window\] id=wnd\_four fullscreen=false WinX=0 WinY=0 ResX=640 ResY=480 viewports="vp\_LT,vp\_RB,vp\_LB,vp\_RT"

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this window configuration. |
| **fullscreen** | Optional | `false` | Determines whether this window should run in fullscreen mode or not. If you set this value to `false`, you must provide the **WinX**, **WinY**, **ResX**, and **RexY** settings described below. |
| **WinX** | Optional | `0` | Specifies the X position of the top left corner of the application window on the desktop, in pixels of screen space from the left edge of the screen. |
| **WinY** | Optional | `0` | Specifies the Y position of the top left corner of the application window on the desktop, in pixels of screen space from the top edge of the screen. |
| **ResX** | Required | `0` | Specifies the horizontal size of the application window in pixels of screen space. When **fullscreen** is set to `false`, this value is required. When **fullscreen** is set to `true`, this value is ignored. |
| **ResY** | Required | `0` | Specifies the vertical size of the application window in pixels of screen space. When **fullscreen** is set to `false`. When **fullscreen** is set to `true`, this value is ignored. |
| **viewports** | Required |   | 
Refers to one or more **[viewport](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#viewportconfigurations)** configuration sections that define the areas of the main application window that nDisplay should fill with rendered views of the scene. If you specify more than one viewport, you must use a comma-separated list of **viewport** configuration section names, enclosed in quotes. See the `wnd_four` example under the **Example configuration** section above. The order of this list does not affect the visual order or placement of the viewports. The placement of the viewports within the parent window are defined in the named **viewport** configurations.

Make sure that the viewport definitions you use do not exceed the size of the window.



 |
| **postprocess** | Optional |   | Specifies the ID of one or more **[postprocess](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#postprocessconfigurations)** configuration sections that define post-processing operations you want to apply to the final generated output image before nDisplay renders it to the window. Optional; use this parameter only if you need to transform the final image before rendering it out. If you provide multiple postprocess configurations, nDisplay will apply their transformations in order. |

## Viewport Configurations

Each **window** configuration described above refers to one or more **viewport** configurations, each of which defines a rectangular area of the game window that nDisplay should fill with a rendered view of the scene.

Usually, a viewport starts at the upper left corner of the application window, and its width and height are set so that they fill the parent window. However, in some cases you may need to offset the viewport within its parent application window. For example, you might want to do this if you need to set up two projectors that partially overlap, or if you need one application window to host multiple separate viewports at different positions.

nDisplay supports **multi-GPU (mGPU)** for viewport rendering, so you can specify one GPU device to render a specific viewport and copy the frame to another GPU to display. For example in virtual production and in-camera VFX scenarios, the inner frustum can be entirely rendered on a second GPU thereby improving performance and hardware usage. On NVIDIA GPUs with [NVLink](https://www.nvidia.com/en-us/design-visualization/nvlink-bridges/), you can bypass the CPU and transfer memory directly from GPU to GPU. Without NVLink, any memory transfer will still be peer-to-peer (P2P) but might be slower as it has to go through the CPU over PCIe.

Add MaxGPUCount=2 to the custom command line arguments when you launch nDisplay either through the nDisplay Launcher or Switchboard to utilize mGPU.

### Example configuration:

```
	`[viewport] id=vp_LT X=0 Y=0 width=300 height=220 projection=proj_simple_LT`

Copy full snippet
```
\[viewport\] id=vp\_LT X=0 Y=0 width=300 height=220 projection=proj\_simple\_LT

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this viewport configuration. |
| **X** | Optional | `0` | The coordinates of the top left corner of the viewport, in screen space pixels, from the left edge of the main application window. Note that this value is relative to the top left corner of the application window, not relative to the top left corner of the screen itself. |
| **Y** | Optional | `0` | The coordinates of the top left corner of the viewport, in screen space pixels, from the top edge of the main application window. Note that this value is relative to the top left corner of the application window, not relative to the top left corner of the screen itself. |
| **width** | Required | `0` | The width of the rendered frame, in pixels. This should not be larger than the size of the game window that is set by the **size** parameter of any **window** configuration using this viewport. |
| **height** | Required | `0` | The height of the rendered frame, in pixels. This should not be larger than the size of the game window that is set by the **size** parameter of any **window** configuration using this viewport. |
| **projection** | Required |   | The name of the **[projection](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#projectionconfigurations)** configuration that defines the rendered view of the virtual world that should be drawn to this viewport. |
| **camera** | Optional |   | The ID of a **[camera](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#cameraconfigurations)** configuration section that you want to force this viewport to display. By default, viewports render the scene from the location of the **camera** section currently in use by nDisplay. However, you can use this parameter to override the default nDisplay camera and force this viewport to render the scene from the point of view configured in a different **camera** section. |
| **buffer\_ratio** | Optional | `1.0` | A value between `0` and `1` that scales the dimensions of the render target texture that nDisplay uses to render this viewport. Lowering this value effectively lowers the resolution of the image generated by nDisplay. This decreases the quality of the final image, but may make it faster to render. |
| **rtt** | Optional | `false` | Determines whether this viewport renders to a texture. |
| **gpu\_node** | Optional | 0 | The GPU device assigned to render the viewport and to copy the frames to the display-facing GPU. The default GPU is the first one installed in the computer. |
| **allow\_gpu\_transfer** | Optional | 1 | With this option enabled, every viewport will be transferred to every GPU. Disabling this option prevents the copy to the other GPU. |
| **share** | Optional |   | With this option enabled, nDisplay uses Texture Sharing for the viewport, sending and receiving textures from other applications. See [Texture Share](/documentation/en-us/unreal-engine/texture-share-in-unreal-engine) for more details. |

Typically, the first GPU installed and enabled in your computer is referenced as **0**, while the others are incrementally assigned **1**, **2**, ... , **n**. You can find the GPU device number provided by your OS in your computer's settings. For example on Windows, you can find your GPU device numbers in **Task Manager**:

1.  Open **Task Manager**.
2.  Switch to the **Performance** tab.
3.  The left side of the window shows every GPU you have in your machine and their device number.
    
    ![GPU numbers in Task Manager on Windows](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15220c52-eb5b-41b4-89d9-37af495ef35b/gpu_numbers_in_task_manager.png)
    
    A computer with one GPU has its GPU labelled GPU 0 in Task Manager.
    

## Projection Configurations

Each **viewport** configuration described above refers to a **projection** configuration, which is responsible for defining the rendered image that needs to be drawn in the viewport.

In most common situations, you will use the `simple` projection type, which renders the virtual world from the current camera's position using a frustum that is defined by a **screen** configuration section elsewhere in this nDisplay configuration file.

Other projection types, such as `mpcdi`, `easyblend`, `vioso`, and `domeprojection`, use other methods to define the rendered content for the viewport, and may introduce additional corrections or apply additional rendering techniques before rendering the image to the rectangular viewport. For example, the projection may squash, stretch, or distort the image so that it will look natural when displayed on a curved surface.

### Example configuration:

The following example shows the simplest possible use case, which routes the frustum defined by the screen configuration named `scr_LT` directly to the viewport without distorting or modifying the rendered image.

```
	`[projection] id=proj_simple_LT type=simple screen=scr_LT`

Copy full snippet
```
\[projection\] id=proj\_simple\_LT type=simple screen=scr\_LT

The following example shows how to use the `easyblend` projection type to render to a surface defined in a Scalable Display configuration file.

```
	`[projection] id=proj_easyblend_1 type="easyblend" file="D:\eb_data\ScalableData.pol_1" origin=easyblend_origin_1 scale=0.1`

Copy full snippet
```
\[projection\] id=proj\_easyblend\_1 type="easyblend" file="D:\\eb\_data\\ScalableData.pol\_1" origin=easyblend\_origin\_1 scale=0.1

The following example shows how to use the `mpcdi` projection type to render to a surface defined in an MPCDI configuration file.

```
	`[projection] id=proj_mpcdi_LT type="mpcdi" file="D:\rot90_flat.mpcdi" buffer="Mosaic" region="Monitor_R" origin=mpcdi_origin`

Copy full snippet
```
\[projection\] id=proj\_mpcdi\_LT type="mpcdi" file="D:\\rot90\_flat.mpcdi" buffer="Mosaic" region="Monitor\_R" origin=mpcdi\_origin

The following example shows how to use the `mpcdi` projection type to render to a curved surface defined by a specified `.pfm` geometry file, using an alpha blending map defined by a specified `.png` file.

```
	`[projection] id=proj_mpcdi_LT type="mpcdi" pfm="D:\geom_displayLeft1.pfm" alpha="D:\Left1blend.png" alpha_gamma=2 origin=mpcdi_origin`

Copy full snippet
```
\[projection\] id=proj\_mpcdi\_LT type="mpcdi" pfm="D:\\geom\_displayLeft1.pfm" alpha="D:\\Left1blend.png" alpha\_gamma=2 origin=mpcdi\_origin

The following example shows how to use the `vioso` projection type to render to a surface defined in a native VIOSO file.

```
	`[projection] id=proj_vioso_1 type="vioso" file="D:\left.vwf" origin=vioso_origin base="[1000 0 0 0] [0 1000 0 0] [0 0 1000 0] [0 0 1000 1]"`

Copy full snippet
```
\[projection\] id=proj\_vioso\_1 type="vioso" file="D:\\left.vwf" origin=vioso\_origin base="\[1000 0 0 0\] \[0 1000 0 0\] \[0 0 1000 0\] \[0 0 1000 1\]"

The following example shows how to use the `domeprojection` type to render to a surface defined by DomeProjection in a `.xml` calibration file.

```
	`[projection] id=proj_domeprojection_1 type=domeprojection file="D:\config.xml" origin=domeprojection_origin channel=0`

Copy full snippet
```
\[projection\] id=proj\_domeprojection\_1 type=domeprojection file="D:\\config.xml" origin=domeprojection\_origin channel=0

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this projection configuration. |
| **type** | Required |   | 
The type of projection that defines how nDisplay generates the rendered image it draws in the viewport. This accepts the following values:

-   `simple`: Renders to the viewport a frustum on the virtual world defined by a **screen** configuration section.
-   `easyblend`: Renders to the viewport a view of the virtual world that you have calibrated using tools from [Scalable Display Technologies](http://www.scalabledisplay.com/).
-   `mpcdi`: Renders to the viewport a view of the virtual world that you have calibrated using [MPCDI](https://vesa.org/vesa-standards/).
-   `vioso`: Renders to the viewport a view of the virtual world that you have calibrated using tools from [VIOSO](https://vioso.com/).
-   `domeprojection`: Renders to the viewport a view of the virtual world that you have calibrated using tools from [DomeProjection](https://www.domeprojection.com/).



 |

Projections where `type=simple` also accept the following additional parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **screen** | Required |   | The name of the **[screen](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#screenconfigurations)** configuration that defines the frustum of 3D space that the Unreal Engine application should render into this viewport. |

Projections where `type=easyblend` also accept the following additional parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **file** | Required |   | The path and file name of the Scalable Display calibration file (*.ol* or *.pol* extension) that defines the surface that this viewport will be projected on. |
| **origin** | Optional |   | The ID of a **scene\_node** configuration section that defines the starting point for the projection. This maps the frame of reference defined in the Scalable Display calibration file to the virtual space in your Unreal Engine Level. |
| **scale** | Optional | `1.0` | The scaling factor to use for the projection. This value depends on the units you used to calibrate EasyBlend. If you used meters, leave this value at `1.0`. For decimeters, use `0.1`. For centimeters, use `0.01`. For inches, use `0.0254`. |

Projections where `type=mpcdi` or `type=picp_mpcdi` also accept the following additional parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **origin** | Optional |   | The ID of a **scene\_node** configuration section that defines the starting point for the projection. This maps the frame of reference defined in the MPCDI calibration file (or the `.pfm` geometry file) to the virtual space in your Unreal Engine Level. |
| Option 1: Using an MPCDI file |   |   |   |
| **file** | Required |   | The path and file name of the `.mpcdi` file that defines the geometry of the surface that this viewport will be projected on. |
| **buffer** | Required |   | The ID of the buffer in the `.mpcdi` file that defines the projection area for this viewport. |
| **region** | Required |   | The ID of the region within the buffer set above that you want to render to. |
| Option 2: Using explicit data |   |   |   |
| **pfm** | Required |   | Specifies a `pfm` file that contains the geometry for the projection. |
| **scale** | Optional | `1.0` | Provides a scaling factor to use for the geometry. |
| **ue4space** | Optional | `false` | Indicates whether the geometry in your `.pfm` file is already expressed in the Unreal Engine coordinate system. |
| **alpha** | Optional |   | The path and file name of a `.png` file to use as an alpha blend map, which defines the intensity of the projection. Optional. |
| **alpha\_gamma** | Optional |   | If you use the `alpha` setting, you can use the `alpha_gamma` setting to provide a multiplier for the alpha gamma. Optional. |
| **beta** | Optional |   | If you use the `alpha` setting, you can also use the `beta` setting to provide the path and file name of the `.png` file to use as a beta blend map. This defines the black level adjustment. Optional. |

nDisplay currently supports only MPCDI version **1.0**, and only the **2D** and **A3D** (or **Advanced 3D**) profile types.

Projections where `type=vioso` also accept the following additional parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| file | Required |   | The path and file name of the VIOSO calibration file (`.vwf` extension) that defines the surface that this viewport will be projected on. |
| origin | Optional |   | The ID of a **scene\_node** configuration section that defines the starting point for the projection. This maps the frame of reference defined in the VIOSO calibration file to the virtual space in your Unreal Engine level. |
| base | Optional |   | The custom base matrix to convert the calibration space into UE coordinate system. |

Projections where `type=domeprojection` also accept the following additional parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| file | Required |   | The path and file name of the DomeProjection calibration file (`.xml` extension) that defines the surface that this viewport will be projected on. |
| channel | Required | 0 | The output mapped in the calibration file. One channel per display. |
| origin | Optional |   | The ID of a **scene\_node** configuration section that defines the starting point for the projection. This maps the frame of reference defined in the DomeProjection calibration file to the virtual space in your Unreal Engine level. |

Projections where `type=manual` also accept the following additional parameters to define the view rotation and frustum that nDisplay should render. You can configure the frustum using either matrices or angles.

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **rot** | Optional | `0,0,0` | The view rotation. Expressed as pitch, yaw, and roll values. For example, `rot="P=0,Y=0,R=0"`. |
| Option 1: Using matrices (monoscopic) |   |   |   |
| **matrix** | Required |   | If using monoscopic rendering, use this 4x4 matrix to define the view frustum. |
| Option 2: Using matrices (stereoscopic) |   |   |   |
| **matrix\_left** and **matrix\_right** | Required |   | If using stereoscopic rendering, use this pair of 4x4 matrices to define the view frustum of both the left eye and the right eye. For example, `matrix_left="[0.5 0 0 0] [0 0.999999 0 0] [1 0 0 1] [0 0 1 0]" matrix_right="[0.500001 0 0 0] [0 1 0 0] [-1 0 0 1] [0 0 1 0]"`. |
| Using angles |   |   |   |
| Option 3: Using a frustum (monoscopic) |   |   |   |
| **frustum** | Required |   | If using monoscopic rendering, use this property to define the angle to the left, right, top, and bottom of the frustum. For example, `frustum="l=0 r=15 t=10 b=-10"`. Values are set in degrees relative to the view vector. |
| Option 3: Using a frustum (stereoscopic) |   |   |   |
| **matrix\_left** and **matrix\_right** | Required |   | If using stereoscopic rendering, use these properties to define the angle to the left, right, top, and bottom of the frusta for both the left eye and the right eye. For example, `frustum_left="l=-15 r=0 t=10 b=-10" frustum_right="left=0 right=15 top=10 bottom=-10"`. Values are set in degrees relative to the view vector. |

Projections where `type=camera` do not accept any other additional parameters. You set up the camera for the projection policy at runtime using either the Blueprint or C++ API.

Projections where `type=mesh` and `type=picp_mesh` do not accept any other additional parameters. You set up the Static Mesh Component for the projection policy at runtime using either the Blueprint or C++ API.

## Screen Configurations

Each different output display that uses the `simple` projection type renders the scene from the current camera's position using a frustum that is defined by a rectangle with a defined size and placement in the 3D VR space. Each of these rectangles is defined by a **screen** configuration. Usually, each of these projection screens has the same dimensions in VR space as the physical screen that you'll use to render it.

The pivot point of a screen is always in its exact midpoint.

### Example configuration:

This definition describes a screen that is 3 meters by 3 meters screen, directly in front of its parent. Because the pivot point of the screen is at the center of the rectangle defined by the size parameter, we add a 1.5 meter offset on the Z axis to move the screen upward by half its height.

```
	`[screen] id=screen_front loc="X=1.5.Y=0,Z=1.5" rot="P=0,Y=0,R=0" size="X=3,Y=3" parent=screens`

Copy full snippet
```
\[screen\] id=screen\_front loc="X=1.5.Y=0,Z=1.5" rot="P=0,Y=0,R=0" size="X=3,Y=3" parent=screens

To define a screen on the left side of the viewer, we move it to the left (negative values on the Y axis), and rotate it around its local Y axis (yaw),

```
	`[screen] id=screen_left loc="X=0,y=-1.5,Z=1.5" rot="P=0,Y=-90,R=0" size="X=3,Y=3" parent=screens`

Copy full snippet
```
\[screen\] id=screen\_left loc="X=0,y=-1.5,Z=1.5" rot="P=0,Y=-90,R=0" size="X=3,Y=3" parent=screens

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this screen configuration. |
| **loc** | Optional | `0,0,0` | The location of the center of this screen in VR space, relative to its parent. |
| **rot** | Optional | `0,0,0` | The pitch (P), yaw (Y) and roll (R) angles of the screen's facing direction, in degrees, relative to its parent. |
| **size** | Required | `0,0` | The total size of the screen rectangle along its local X and Y axes, in meters. |
| **parent** | Optional |   | The name of a **[scene\_node](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#scenenodeconfigurations)** configuration that you want to act as the parent for this object. This parameter is optional. If you specify a parent, the values you set in the **loc** and **rot** parameters will be relative to the position of that parent. If you omit the parent, the values you set in the **loc** and **rot** parameters will be relative to the VR root. |
| **tracker\_id** | Optional |   | The name of a **[input](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#inputconfigurations)** configuration that defines a VR device you want to drive the position of the screen over time. Optional. If you omit this parameter, the screen's position will be static in VR space. |
| **tracker\_ch** | Optional |   | When you provide a **tracker\_id**, this parameter specifies the channel of that device that nDisplay will read tracking data from. |

## PostProcess Configurations

A **postprocess** configuration defines how the image generated for a window by an instance of the Unreal Engine should be post-processed before being rendered. nDisplay currently supports two types of post-process operations: `OutputRemap` and `TextureShare`.

With `OutputRemap`, you can control the way the 2D image, generated by nDisplay, maps to the 2D area of the application window. For example, you can translate, rotate, and scale parts of the output image so that they appear in different regions of the application window. To do this, you need to provide an .obj file that contains a planar geometry with a UV mapping set up. nDisplay will use the UV mapping that was set for your plane to determine how the output image is mapped to each part of the application window.

With `TextureShare`, you can receive a texture from another application and display it in the specified viewport. To do this, you need to define a postprocess with the name of the Texture Share item and the viewport that will display the texture.

### Example configuration:

The following example shows how to use the OutputRemap postprocess type with two .obj files:

```
	`[window] id=somewindow ... postprocess="pp_1, pp_2" 	[postprocess] id=pp_1 type="OutputRemap" file="remap_1.obj" 	[postprocess] id=pp_2 type="OutputRemap" file="remap_2.obj"`

Copy full snippet
```
\[window\] id=somewindow ... postprocess="pp\_1, pp\_2" \[postprocess\] id=pp\_1 type="OutputRemap" file="remap\_1.obj" \[postprocess\] id=pp\_2 type="OutputRemap" file="remap\_2.obj"

The following example shows how to use TextureShare to share the rendered frame for the **vp\_1** viewport to an external application, receive a texture from a third party source, and display it in the **vp\_ext** viewport.

```
	`[window] id=somewindow viewports="vp_1" fullscreen="false" … postprocess="pp_sharenode_ext" 	[viewport] id=vp_1 ... projection="proj_screen_1" share=true 	[viewport] id=vp_ext ... projection="" 		[postprocess] id=pp_sharednode_ext type="TextureShare" destination="vp_ext" source="thirdpartyapp_viewport_rendering"`
Copy full snippet
```
\[window\] id=somewindow viewports="vp\_1" fullscreen="false" … postprocess="pp\_sharenode\_ext" \[viewport\] id=vp\_1 ... projection="proj\_screen\_1" share=true \[viewport\] id=vp\_ext ... projection="" \[postprocess\] id=pp\_sharednode\_ext type="TextureShare" destination="vp\_ext" source="thirdpartyapp\_viewport\_rendering"

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this postprocess configuration. |
| **type** | Required |   | 
The type of post-processing you want to carry out. Currently supports the following types:

-   `OutputRemap`
-   `TextureShare`



 |
| OutputRemap configuration |   |   |   |
| **file** | Required |   | The path and file name of the `.obj` file that contains the UV mapping you want to use to remap the rendered image before drawing it to the application window. |
| TextureShare configuration |   |   |   |
| **destination** | Required |   | The name of the viewport that applies the texture share item received from the `source` application. |
| **source** | Required |   | The share name of the application sending the texture to nDisplay. |

## Camera Configurations

All instances in the nDisplay cluster render the scene from the same position in the virtual world. Each of these potential viewpoints is defined by a **camera** configuration line.

You can switch between these viewpoints at runtime. Each camera viewpoint can also be driven by a tracking device.

### Example configuration:

```
	`[camera] id=camera_static loc="X=0.Y=0,Z=1.7" tracker_id=VRPNTracking tracker_ch=0`

Copy full snippet
```
\[camera\] id=camera\_static loc="X=0.Y=0,Z=1.7" tracker\_id=VRPNTracking tracker\_ch=0

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this camera configuration. |
| **loc** | Optional | `0,0,0` | The location of this camera in VR space, relative to its parent. |
| **rot** | Optional | `0,0,0` | The rotation of this camera in VR space, relative to its parent. |
| **parent** | Optional |   | The name of a **[scene\_node](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#scenenodeconfigurations)** configuration that you want to act as the parent for this object. This parameter is optional. If you specify a parent, the values you set in the loc parameter will be relative to the position of that parent. If you omit the parent, the values you set in the loc parameter will be relative to the VR root. |
| **eye\_swap** | Optional | `false` | When rendering in stereoscopic mode, this property determines whether or not the images generated for the left and right eye are swapped. |
| **eye\_dist** | Optional | `0.064` | When rendering in stereoscopic mode, this property determines the inter-ocular distance to use for offsetting the images generated for the left and right eyes, in meters. |
| **force\_offset** | Optional | `0` | When rendering in *monoscopic* mode, this property allows you to simulate stereoscopic rendering by offsetting the camera to the position of the left or right eye (as defined by the **eye\_dist** property above). Use `-1` to force the camera to render from the left eye position, `0` to render from the camera's default position (no effect), or `1` to force the camera to render from the right eye position. |
| **tracker\_id** | Optional |   | The name of a **[input](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#inputconfigurations)** configuration that defines a VR device you want to drive the position of the camera over time. Optional. If you omit this parameter, the camera's position will be static in VR space. |
| **tracker\_ch** | Optional | `-1` | When you provide a **tracker\_id**, this parameter specifies the channel of that device that nDisplay will read tracking data from. |

## Scene Node Configurations

In your configuration file, you can define a hierarchy of scene nodes, each of which represents a transform in 3D space. Anything that you set up in the configuration file that requires a position and rotation in 3D space, such as a camera or a projection screen, can use one of these *scene\_node* configurations as its parent. This can help you to define the spatial relationships between all of the different components of the visualization system.

Like cameras, scene nodes can also be driven by VR tracking devices.

### Example configuration:

The following lines define a hierarchy of two nodes, where the child node has an offset of 2 meters in front of its parent.

```
	`[scene_node] id=vr_space_root loc="X=0.Y=0,Z=0" rot="P=0,Y=0,R=0" 	[scene_node] id=walls_front_group loc="X=2.Y=0,Z=0" rot="P=0,Y=0,R=0" parent= vr_space_root`

Copy full snippet
```
\[scene\_node\] id=vr\_space\_root loc="X=0.Y=0,Z=0" rot="P=0,Y=0,R=0" \[scene\_node\] id=walls\_front\_group loc="X=2.Y=0,Z=0" rot="P=0,Y=0,R=0" parent= vr\_space\_root

The following line shows a scene node that is configured to be driven by a VR tracking device:

```
	`[scene_node] id=cave_wand loc="X=0, Y=0,Z=1" tracker_id=CaveTracking tracker_ch=1`

Copy full snippet
```
\[scene\_node\] id=cave\_wand loc="X=0, Y=0,Z=1" tracker\_id=CaveTracking tracker\_ch=1

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this scene node configuration. |
| **loc** | Optional | `0,0,0` | The location of this scene node in VR space, relative to its parent. |
| **rot** | Optional |   | The pitch (P), yaw (Y) and roll (R) angles of the scene node's facing direction relative to its parent, in degrees. |
| **parent** | Optional |   | The name of another **[scene\_node](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#scenenodeconfigurations)** configuration that you want to act as the parent for this scene node. This parameter is optional. If you specify a parent, the values you set in the **loc** and **rot** parameters will be relative to the position of that parent. If you omit the parent, the values you set in the **loc** and **rot** parameters will be relative to the VR root. |
| **tracker\_id** | Optional |   | The name of a **[input](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#inputconfigurations)** configuration that defines a VR device you want to drive the position of the scene node over time. Optional. If you omit this parameter, the scene node's position and rotation will be static in VR space with respect to its parent. |
| **tracker\_ch** | Optional | `-1` | When you provide a **tracker\_id**, this parameter specifies the channel of that device that nDisplay will read tracking data from. |

## Input Configurations

You define an **input** section for each device that you need to provide input to the nDisplay system. For example, each **[camera](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#cameraconfigurations)** and each **[scene\_node](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#scenenodeconfigurations)** may optionally be driven by a VR tracking device that you set up in an **input** section and refer to in the **camera** or **scene\_node** configuration. Alternatively, you may want to set up trackers, controllers, and keyboards to send generic input events to the Unreal Engine input system, or bind their events and input values to generic nDisplay Blueprint nodes that you can respond to in your Project's gameplay scripts.

You can also use **[input\_setup](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#inputsetupconfigurations)** sections to control the way specific channels, buttons, or keys from these input devices are bound to specific types of input events and values within Unreal Engine.

For an overview of what you can do with nDisplay inputs, see [Live Link VRPN](/documentation/en-us/unreal-engine/live-link-vrpn-in-unreal-engine).

### Example configuration:

This configuration sets up nDisplay to get input from a VRPN location tracking device. Typically this kind of device is mounted to a camera or a viewer's head, or is held by a viewer. You can automatically drive the position of a camera or scene node from the trackerby referring to this **input** configuration in a **[camera](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#cameraconfigurations)** or **[scene\_node](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#scenenodeconfigurations)** configuration. Or, you can retrieve the value of this tracker in your Project's Blueprint code.

```
	`[input] id=CaveTracking type=tracker [[email protected]](/cdn-cgi/l/email-protection) loc="X=-1.5,Y=0,Z=3.4" rot="P-0,Y=0,R=0" front=X right=Y up=-Z`

Copy full snippet
```
\[input\] id=CaveTracking type=tracker addr=Tracker0@192.168.0.1 loc="X=-1.5,Y=0,Z=3.4" rot="P-0,Y=0,R=0" front=X right=Y up=-Z

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | A unique name for this input device configuration. |
| **type** | Required |   | 
The type of this VRPN input device:

-   `tracker` for a tracking device.
-   `analog` for a device that produces axis data.
-   `button` for a device that produces Boolean button data.
-   `keyboard` for a standard computer keyboard.



 |
| **addr** | Required |   | 

The address of the VRPN server that handles this particular device. The value must match the following format: `DEVICENAME@SERVER_ADDRESS:SERVER_PORT` where:

-   `DEVICENAME` is the VRPN name for this device.
-   `SERVER_ADDRESS` is the IPv4 address of the VRPN server.
-   `:SERVER_PORT` is the port the VRPN server listens on for incoming connections. This is optional. If you don't provide it, nDisplay uses port `3883` by default.



 |

Devices where `type=tracker` also accept the following additional parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **loc rot** | Optional | `0,0,0` `0,0,0` | Similar to other configuration sections, the **loc** and **rot** parameters specify position and rotation offsets in local space for this input device. However, for an input device, you typically use these offsets to adjust the root position of a tracking device in VR space to match the location you expect it to be in your scene node hierarchy. |
| **front right up** | Required |   | 
These parameters match each local axis of the tracker in Unreal (front, right, and up) with the corresponding axis in the tracker's coordinate system. Unreal uses a right-handed, Z-up coordinate system. If your tracker uses a different coordinate system, you can use these parameters to map the tracker's coordinate system to Unreal's. For example, the following line maps the Y axis of the tracker to the front (X) axis in Unreal; the X axis of the tracker to the right (Y) axis in Unreal, and the negative Z axis of the tracker to the up (Z) axis in Unreal: `front=Y right=X up=-Z`



 |

Devices where `type=analog` and `type=button` do not accept any additional parameters.

## Input Setup Configurations

Each **input\_setup** configuration section provides additional configuration parameters for a specified **[input](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#inputconfigurations)** device, typically to bind a channel or key from that device to a generic nDisplay Blueprint input node.

### Example configuration:

This configuration sets up the input device with ID controller so that when a button is pressed that generates an event on channel 0, an event is generated from the **Input >** N Display Events > **nDisplay Button 0** node in Blueprint.

```
	`[input_setup] id=controller ch=0 bind="nDisplay Button 0"`

Copy full snippet
```
\[input\_setup\] id=controller ch=0 bind="nDisplay Button 0"

This configuration is similar to the above, except that it binds an analog value (typically an axis from a controller) to an nDisplay analog value. You can use the **Input > N Display Events > nDisplay Analog 0** node in Blueprint to detect when that controller axis is used, or **Input > N Display Values > nDisplay Analog 0** to retrieve the value for the current frame.

```
	`[input_setup] id=test_axes ch=0 bind="nDisplay Analog 0"`

Copy full snippet
```
\[input\_setup\] id=test\_axes ch=0 bind="nDisplay Analog 0"

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **id** | Required |   | 
Refers to the ID of the **[input](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#inputconfigurations)** configuration that this **input\_setup** section configures. Note that unlike most other sections in the nDisplay configuration file, this **id** value does not provide an ID for the **input\_setup** section that contains it. Instead, it refers to the ID of an **input** section defined elsewhere in the file.



 |
| **ch** | Required |   | Determines the channel of the specified input device that will be bound to the event that you set in the **bind** setting. |
| **key** | Optional |   | Similar to **ch**, but used only for input devices where `type=keyboard`. |
| **bind** | Required |   | 

Determines the event in Unreal Engine that the channel or key specified above is bound to. This value can be the name of any Blueprint node that you see in the **Input** category, such as **F1**, **nDisplay F1**, **nDisplay Button 0**, **Gamepad Left Thumbstick X-Axis**, **Gamepad Face Button Top**, and so on. If the name contains a space, you must enclose it in double-quotes.



 |

## General Configuration

The **general** configuration line contains parameters that control the overall operation of the nDisplay cluster.

### Example configuration:

```
	`[general] swap_sync_policy=1`

Copy full snippet
```
\[general\] swap\_sync\_policy=1

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **swap\_sync\_policy** | Optional | `0` | 
Determines how output is synchronized over the network.

-   0: no synchronization (VSync=0).
-   1: Software swap synchronization (VSync=1).
-   2: NVIDIA swap lock (only for NVIDIA cards rendering with DirectX11 and DirectX12).



 |
| **ue4\_input\_sync\_policy** | Optional | `1` | 

Determines how native input into UE4 is replicated through the nDisplay network.

-   0: Native UE4 input is processed only by the primary node. No replication is done to other cluster nodes.
-   1: All native input that the primary node receives is replicated to all other cluster nodes as well.



 |

## NVIDIA Configuration

If you use a `swap_sync_policy` value of `2` in your **[general](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine#generalconfiguration)** configuration section, you can use the parameters in the **NVIDIA** section to tweak some specific hardware settings relating to frame lock.

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **sync\_group** | Optional | `1` | The sync group to use for frame locking. |
| **sync\_barrier** | Optional | `1` | The sync barrier to use for frame locking. |

## Network Configuration

The **network** configuration section provides settings that you can use to control timeouts and other settings related to network communication between nDisplay cluster nodes.

You can only have zero or one **network** section in your nDisplay configuration file.

### Example configuration:

```
	`[network] cln_conn_tries_amount=10 cln_conn_retry_delay=1000 game_start_timeout=30000 barrier_wait_timeout=5000`

Copy full snippet
```
\[network\] cln\_conn\_tries\_amount=10 cln\_conn\_retry\_delay=1000 game\_start\_timeout=30000 barrier\_wait\_timeout=5000

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **cln\_conn\_tries\_amount** | Optional | `10` | 
When a non-primary cluster node starts up, this setting determines the number of times the node will attempt to connect to the primary PC before it shuts down.



 |
| **cln\_conn\_retry\_delay** | Optional | `1000` | 

When a non-primary cluster node starts up, this setting determines the time interval between each successive attempt by the node to connect to its primary PC, in milliseconds.



 |
| **game\_start\_timeout** | Optional | `30000` | 

Sets a time interval that the Unreal Engine application on the primary node wait for all cluster nodes to be ready before it starts the first frame of the game loop and begins rendering to the main window, in milliseconds. This gives all your cluster nodes a chance to connect to the primary PC before rendering begins. During this time, the main window will be black. If, at the end of this time interval, any cluster node has not yet successfully connected to the primary PC, all instances in the cluster will shut down. You may need to raise this value if your cluster takes an unusually long time to initialize.



 |
| **barrier\_wait\_timeout** | Optional | `5000` | 

Sets the barrier timeout for the game and render threads, in milliseconds. This is a barrier timeout to synchronize both game and render threads among cluster nodes. It's used several times within each frame. In other words, this is used at runtime to detect situations where any node becomes unreachable. If this occurs, the state of the cluster state is determined to be invalid, and all nodes shut themselves down.



 |

The **cln\_conn\_tries\_amount** and **cln\_conn\_retry\_delay** settings work together to determine the maximum length of time your cluster nodes will try to connect to the primary node at startup. For example, suppose you have **cln\_conn\_tries\_amount** set to 10, and **cln\_conn\_retry\_delay** set to 1000 milliseconds. On startup, each node tries to connect to the primary PC. If that connection fails, it waits 1000 milliseconds to try again. If that attempt also fails, it waits another 1000 milliseconds. After ten successive failures, the cluster node quits automatically. As soon as a cluster node makes the connection to its primary PC, the count stops.

## Info Configuration

The **info** configuration line contains optional information about this configuration file: specifically, the latest version of nDisplay and Unreal Engine that this configuration file is known to be compatible with.

### Example configuration:

```
	`[info] version=22`

Copy full snippet
```
\[info\] version=22

### Parameters:

| Parameter | Required? | Default | Description |
| --- | --- | --- | --- |
| **version** | Required |   | 
The oldest version of Unreal Engine that is compatible with this configuration file.

The number should be understood as the point version that follows `4.`. For example, a value of 22 means that the file is compatible with version 4.22 of nDisplay and Unreal Engine.

Do not set this value by hand. The **nDisplay Launcher** sets it automatically. If you use a configuration file without a version, or where the version in the file is not supported by the current version Unreal Engine you are using, the **nDisplay Launcher** automatically attempts to update your configuration file to work with the latest version. If it succeeds, it saves the updated configuration to a new file and updates this value to the latest version.



 |

## Custom Configuration Parameters

You can include a **custom** configuration section to provide your own custom key-value pairs to your nDisplay cluster nodes. You can include as many parameters and values as you need on a `[cluster]` line. You can then retrieve these configuration values at runtime from the nDisplay Blueprint or C++ APIs.

### Example configuration:

```
	`[custom] stringParameter=myValue numberParameter=2`

Copy full snippet
```
\[custom\] stringParameter=myValue numberParameter=2

## Configuration File Scene Structure Example

To take a specific example, open the *wall\_flat\_3x2.cfg* sample file, which you'll find in your Unreal Engine installation folder under `Templates/TP_nDisplayBP/Content/ExampleConfigs`. This file defines six projection screens, each of which is to be rendered by a separate physical computer.

It also defines several scene\_nodes, which taken together create the following hierarchy:

![nDisplay example scene hierarchy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34164d8b-b05d-4e7b-b515-d8a220f8959b/ndisplay-scene-hierarchy.png "nDisplay example scene hierarchy")

The relative positions and rotations of the nodes in this hierarchy lay out the arrangement of the camera and the six screens in VR space so that the six projection screens are side-by-side, at a distance of 1 meter from the camera.

Note that the configuration implies a small space in between each adjacent pair of projection screens, to account for the edges of the monitors rendering the scene.