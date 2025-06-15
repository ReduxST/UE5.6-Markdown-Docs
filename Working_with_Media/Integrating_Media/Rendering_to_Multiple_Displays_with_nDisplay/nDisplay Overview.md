# nDisplay Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine)  
**Processed:** 2025-06-14 16:38:18

---

Every nDisplay setup has a single *primary* computer, and any number of additional computers, called secondary nodes.

-   Each computer in the network runs one or more instances of your Unreal project either in -game or in packaged format.
    
-   Each Unreal Engine instance handles rendering to one or more display devices, such as screens, LED displays, or projectors.
    
-   For each display device an instance of Unreal Engine handles, it renders a viewport that shares the same view origin or viewpoint. By setting up these viewports so that their location in the 3D world matches the physical locations of the screens or projected surfaces in the real world, you give viewers the illusion of being present and immersed in the virtual world.
    
-   The primary node is also responsible for accepting input from spatial trackers and controllers through connections to Virtual-Reality Peripheral Networks (VRPNs) through Live Link, and replicating that input to all other connected computers.
    

![nDisplay network overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e90368fe-a7e3-458a-a49b-deafe1bf2205/ndisplay-setup.png "nDisplay network overview")

The image above shows a possible nDisplay network. Like all nDisplay networks, one of its PCs acts as the primary node. This primary node accepts input into the system from a VRPN server, which relays signals that come from spatial tracking devices and other controller devices. The network also contains several other PCs that run other instances of the Unreal Engine Project. Each of these secondary nodes drives one or more display projectors.

|   |   |
| --- | --- |
| 
 | 

**One application instance and host computer per display device.**  
This is the most straightforward way to set up a host for nDisplay. For each projector or physical display device you need, you set up one computer to handle rendering to that device. On that computer, you run one instance of Unreal Engine running your project. Typically, in this scenario, you'll set up that application instance to render a single view of the 3D scene into a single viewport.



 |
| 

 | 

**One application instance and host computer per multiple display devices.**  
With this option, you run a single instance of Unreal Engine per computer, but you set it up to render multiple views of the scene's 3D space. Using the Output Mapping tool, these separate viewports are then mapped into different areas of a large 2D canvas, referred to as the application window.

We recommend leveraging multi-display technologies from graphics card vendors such as [NVIDIA Mosaic](https://www.nvidia.com/en-gb/design-visualization/solutions/nvidia-mosaic-technology/) or [AMD Eyefinity](https://www.amd.com/en/technologies/eyefinity) to treat multiple connected displays as one display. This ensures that Unreal can render fullscreen on these aggregated screens for better display sync and performance. In this scenario, you can map all your viewports in this extended display canvas using the nDisplay Output Mapping tool.

For improved performance, you can also leverage a second GPU for viewport rendering. Once all pixels are copied and available on the display-facing GPU, they are composited in the application window and sent to the GPU outputs. For more details on using multiple graphics cards, refer to [Multi-GPU Support](/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine#multi-gpusupport).



 |

## nDisplay Components

nDisplay adds several components to the usual Unreal system architecture:

-   A Plugin that works inside the Unreal Engine. It communicates and synchronizes information between all the application instances that make up the cluster, ensures all instances render the same frame at the same time, ensures each display device renders the correct frustum of the game world, and more.
-   A shared configuration asset that contains all the settings nDisplay needs to start up the correct number of instances on the correct computers, each rendering the right points of view on the game's 3D world to produce the illusion of a seamless rendering across all display screens or projectors. See the [nDisplay 3D Config Editor](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine) for more information.

## Workflow

You need to tell nDisplay about the different computers you want to use in your network, the size and resolution of the screens or projectors those computers will render to, the spatial relationships between those screens in 3D space, and more. To do this, you create a configuration asset that expresses all of this information in a series of settings.

Typically, once your configuration asset is set up, you only have to modify it when the topology of your network changes: for example, when you need to change the computers you are rendering to, or if you change the physical arrangement of your screens and displays in the real world.

The general workflow for setting up your nDisplay cluster:

1.  Create a new nDisplay Config Asset in the Unreal Editor.
2.  Configure your nDisplay Config Asset in the nDisplay 3D Config Editor:
    1.  **Components**: Add your displays, cameras, and transforms to the root component.
    2.  **Cluster**: Create a representation of your cluster PC configuration, assign Viewports and GPU ID. Essentially adding PC's and Viewports.
    3.  **Output Mapping**: Effectively map Viewports to UE Application Windows. Assign Projection Policies and bind Viewports to Display, Screen, or Mesh Components.
3.  Drag the nDisplay Config Asset into the level viewport to create an nDisplay Root Actor and preview your project's content from the cluster's perspective.
    
4.  Launch your project onto your physical nDisplay setup with [Switchboard](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine).

To get started with a sample nDisplay configuration on your computer, follow the steps in the [nDisplay Quick Start](/documentation/en-us/unreal-engine/ndisplay-quick-start-for-unreal-engine).

The nDisplay Root Actor is not required to be in the level to launch the nDisplay cluster. If the nDisplay plugin is enabled for the project, you can specify the location of the nDisplay Configuration Asset (`.uasset` or `.ndisplay` file) in Switchboard or the nDisplay Configuration File (`.cfg` or `.ndisplay`) as a command-line argument. This method works in -game and Packaged modes.

If a config asset is already present as an Actor in your project, it will be ignored when you specify one externally using Switchboard or command line arguments.

## Failover

Every installed clustered system, either permanent or temporary, is exposed to some risk of failure. Failure can be because of hardware, software, or network issues. Failover refers to how systems can mitigate the risk of failure and recover from nodes failing without terminating the entire cluster.

The current implementation of failover in nDisplay addresses the network discoverable failures of the render nodes only. In other words, when a render node becomes unresponsive, whether because of a crash or because it loses its network connection, it is dropped from the cluster after a configurable timeout value.

### Enable Failover

To enable nDisplay Failover support, open the Cluster Details panel in the [nDisplay 3D Config Editor](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine) and set Failover Policy to Drop S-node on fail.

![Enable Failover Policy](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b47ce8f4-0042-4da0-8e0d-3265d498f617/enable-failover-policy.png)

When activated, this option causes render nodes to drop from the cluster should they exceed the timeout value. The timeout values used for failover can be found in the Network settings for the Cluster. Refer to [Changing nDisplay Communication Ports](/documentation/en-us/unreal-engine/changing-ndisplay-communication-ports-in-unreal-engine) for details on the Network settings.

![Network Settings for Cluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1f47bb1-8c11-47d0-bd6d-6a9ba0062c6b/network-settings.png)

If any of the nodes don't respond in time and a barrier is timed out, those nodes are considered as failed and will be dropped from the cluster when the failover policy is active.

## Multi-GPU Support

nDisplay supports multi-GPU (mGPU) for viewport rendering, so you can specify one GPU device to render a specific viewport and copy the frame to another GPU to display. For example, in virtual production and in-camera VFX scenarios, the inner frustum can be entirely rendered on a second GPU thereby improving performance and hardware usage.

On NVIDIA GPUs with NVLink, you can bypass the CPU and transfer memory directly from GPU to GPU. Without NVLink, any memory transfer will still be peer-to-peer (P2P) but might be slower as it has to go through the CPU over PCIe.

To enable mGPU in your nDisplay setup:

1.  Open your nDisplay Config Asset in the nDisplay 3D Config Editor.
2.  In the **Components** panel, select the Config Asset to open the Details panel and set **Configuration > Render Frame Settings > Multi GPU Mode** to **Enabled**.
3.  For viewport renders: In the nDisplay 3D Config Editor, select the viewport and in its Details panel set the GPUIndex field to the index of your GPU.
    
    ![GPU Index parameter in a viewport's details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9c95a66-ae40-422a-8a8c-ee6515b6f4ed/mgpu-setting.png)
    
    For inner frustum renders: In the nDisplay 3D Config Editor, select the ICVFX camera and in its Details panel set the GPUIndex field to the index of your GPU.
    
    ![GPU index setting in an ICVFX camera's details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08646dec-e3b6-4d0c-a457-c34f74e0606e/mgpu-setting-innerfrustum.png)
    
    Typically, the first GPU installed and enabled in your computer is referenced as **0**, while the others are incrementally assigned **1, 2, ... , n**. You can find the GPU device number provided by your OS in your computer's settings. For example on Windows, you can find your GPU device numbers in Task Manager: 1. Open Task Manager. 1. Switch to the Performance tab. 1. The left side of the window shows every GPU you have in your machine and their device number.
    
    ![Task manager window only showing one GPU, with the name GPU 0](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30e55dbf-b048-40b6-9f9c-c46aadacb1fc/gpu-0.jpg)
4.  In the [Switchboard](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine) settings under your nDisplay node, set *Number of GPUs* to match the number of GPUs in the nDisplay node.
    
    ![Switchboard settings number of GPUs set to 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fb97f04a-ca8b-437f-8110-52e582c89189/switchboard-set-number-of-gpus.png)

## Runtime Camera Control

Internally, nDisplay maintains a hierarchy of scene objects in virtual 3D space that you set up in the configuration file. For example, this scene hierarchy typically defines the position of a *camera*, and the positions of a set of *screens*—rectangles of 3D space that represent the real-world display screens or projection surfaces in the virtual world. The positions of these nDisplay scene objects are defined relative to a single *root* position that is always located at the origin (0,0,0) in virtual space.

When you run a Project with nDisplay enabled, the root of this virtual space is based on the position and rotation of a **DisplayClusterRoot** Component that is attached to a camera in your Level. Every frame, nDisplay uses the position and rotation of this root component as the starting point for the hierarchy of scene nodes that you set up in your configuration file.

By default, nDisplay creates a DisplayClusterRoot Component at startup and attach it to the default camera. The effect is that all devices and projectors in the whole nDisplay cluster automatically render the scene from the point of view of the active camera.

## Blueprint API

You can control the behavior of the nDisplay system in your game's runtime logic using its Blueprint APIs.

To get to the functions exposed in these APIs:

1.  For most nDisplay Blueprint functions related to cluster management, querying input devices, nDisplay rendering, and more, create a new **N Display > DisplayCluster Module API** node in your Blueprint.
2.  Drag from the **Out API** pin of your node, and look under the **Display Cluster** category:
    
    ![Display cluster blueprint API](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8ab566d3-ca56-4e28-bfac-0ce3771c9a28/display-cluster-blueprint-api.png)

## Extending nDisplay

nDisplay offers many features out of the box for controlling real-time, synchronized rendering across multiple computers and output devices. However, there are a wide variety of projection systems and display surfaces, and you may need to extend the nDisplay rendering system to support your own choice of technologies. If you are comfortable programming in C++, and you understand how nDisplay works in typical use cases, you can extend nDisplay to support additional display and calibration technologies by building on top of its extendable rendering API.

The nDisplay API breaks the rendering pipeline into a few major concepts:

-   The **DisplayClusterRenderingDevice**, which is essentially an extension of the native `IStereoRendering` Interface.
-   The **DisplayClusterPostProcess** is a group of six callbacks that you can use to apply post-processing to specific viewports.
-   The **DisplayClusterProjectionPolicy** is responsible for custom projection methods, such as supporting Scalable Display, VIOSO, DomeProjection, or MPCDI to render to curved and arbitrary surfaces, or doing a simple planar projection.
-   The **DisplayClusterRenderSyncPolicy** is used for a variety of synchronization methods, like **nvSwapLock**, vSync, or custom skip-frame sync for 24hz displays.

By creating your own specializations of the elements described above, you can customize the images produced by the nDisplay system to suit whatever projection or display technologies you work with, while still getting all the key benefits of the nDisplay clustering system, all without needing to modify the shipped Unreal Engine source code.

For a working model of how to set up implementations of these elements, see the source code for the `PicpProjection` and `PicpMPCDI` modules. You'll find these modules in the Unreal Engine source code, under `Engine/Plugins/Runtime/nDisplay/Source`.

You can provide your own custom key-value pairs to your nDisplay cluster. You can include as many parameters and values as you need in the Custom Parameters field located in the Config Asset's Details panel. You can then retrieve these configuration values at runtime from the nDisplay Blueprint or C++ APIs.

To add Custom Parameters:

1.  In the **3D Config Editor**, select **self** in the Components panel to open its **Details** panel.
2.  In the **Details** panel, expand the **Configuration** section and add elements to the **Custom Parameters** field.
    
    ![Adding Custom Parameters to your nDisplay cluster](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/093f8d72-8fbb-4035-9215-ae79918eea0a/custom-parameters.png)

## Supported Operating Systems

### Windows

All nDisplay tools and features are fully functional on Windows 10, 8.1, 8, and 7.

### Linux

nDisplay and its tools ecosystem now includes preliminary Linux support. This will benefit users running UE under various flavors of Linux distros, especially those in training and simulation, in a clustered setup environment.

#### Known Limitations on Linux

-   Custom Sync policies will exhibit some limitations due to existing graphics card drivers support.
-   Some Projection policies relying on other vendors will have to be validated.
-   Some rendering features, for example ray tracing, are not supported at the moment.