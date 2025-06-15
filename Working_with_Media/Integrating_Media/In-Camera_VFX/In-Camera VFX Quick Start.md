# In-Camera VFX Quick Start

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-quick-start-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/in-camera-vfx-quick-start-for-unreal-engine)  
**Processed:** 2025-06-14 16:30:48

---

This Quick Start page shows the process of setting up a project in Unreal Engine to work with in-camera VFX. At the end of this guide, you will:

-   Have a synchronized cluster of nDisplay nodes.
    
-   Have an inner and outer frustum for in-camera VFX.
    
-   Have a real-time camera tracking system integrated via Live Link XR.
    
-   Have a green screen inner frustum with chroma key markers that can be toggled on.
    
-   Be able to launch all clustered nodes and test on set.
    

## Step 1 - Set up Your Project for In-Camera VFX

The easiest way to set up an in-camera VFX project is to use the In-Camera VFX Example project.

1.  Open the **Epic Games Launcher**.
    
2.  In the **Samples** tab, find the [In-Camera VFX Example](https://www.fab.com/listings/1ccaf0a1-acce-4a3b-831e-a9cf4af35f6d) project.
    
3.  On the project page, click **Free**.
    
4.  Click **Create Project**.
    
5.  Specify the location on your machine to save the project and select **Create**.
    
6.  Launch **Unreal Engine** and open the **In-Camera VFX Example** project.
    

In the example project, under **Content > Maps**, you can see **Main** level. For learning about in-camera VFX with Unreal Engine, open the **Main** level. The example project and levels automatically enable the necessary plugins, provide helpful blueprints, configure additional settings, and include sample configuration files.

### Plugins

-   **Aja or Blackmagic Media Player:** Provides support for SDI capture cards.
    
-   **Camera Calibration** A tool for creating lens distortion profiles and nodal offsets.
    
-   **Color Correct Regions:** Color correction and shading constrained to a volume.
    
-   **ICVFX:** A plugin that enables a base suite of in-camera VFX plugins.
    
-   **Level Snapshots:** Store alternative layouts for convenient, non-destructive variations of the current level with filtering abilities.
    
-   **Live Link:** Unreal Engine's API for ingesting live data, such as motion capture and camera tracking.
    
-   **Live Link Over nDisplay:** The primary node receives Live Link data and redistributes the tracking data in an efficient and synchronized manner.
    
-   **Live Link XR:** Unreal Engine's API for ingesting live data from XR devices, such as Vive Trackers.
    
-   **Multi-User Editing:** Multiple editors can be in a shared session.
    
-   **Media Framework Utilities:** Utility plugins related to live video, timecode, and genlock on SDI capture cards.
    
-   **nDisplay:** Unreal Engine's technology for rendering on multiple displays.
    
-   **nDisplay Support for Level Snapshots:** Enables support for saving and restoring nDisplay Root Actor properties with Level Snapshots.
    
-   **OpenColorIO (OCIO):** Provides support for OpenColorIO.
    
-   **OSC:** Provides functionality to send and receive OSC messages between remote clients or applications.
    
-   **Remote Control API:** A suite of tools to control the Engine remotely through a REST API, WebSockets, and C++.
    
-   **Remote Control Web Interface:** Provides a remote web interface and UI builder for remotely controlling the Editor.
    
-   **Switchboard:** Application for launching instances of Unreal, nDisplay nodes, and other Virtual Production devices in a multi-user session.
    
-   **Timed Data Monitor:** Utilities to monitor inputs that can be time synchronized.
    
-   **Virtual Production Utilities:** Utility plugins useful for Virtual Production.
    

### nDisplay Root Actor

The [nDisplay Config Asset](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine) defines the relationship between the computers in the nDisplay cluster and the topology of the LED volume. The nDisplay Root Actor is an instance of the nDisplay Config Asset in the level, and is created by dragging the nDisplay Config Asset into the level.

Sample nDisplay Config Assets are included in the example project. You can find them in the Content Browser under nDisplayConfigs. For more information on the settings exposed in the nDisplay Root Actor, refer to [nDisplay Root Actor Reference](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine).

## Step 2 - Create LED Panel Geometry

This section provides an example of how to create a representation of a curved LED wall. Each LED Volume can be different, so modify these steps to match the dimensions and layout of your display.

These steps show how to create the geometry to represent the real-world LED panels.

In this example, a curved wall is created with two meshes. Each mesh is mapped to an nDisplay viewport. There are a few factors which define how an LED stage should be separated into meshes:

1.  **Angle:** The maximum ideal angle of curvature should be 90 degrees per mesh. A curve greater than 90 degrees per mesh can cause visual degradation. In addition, no single viewport (and therefore mesh) can cover more than 179 degrees.
    
2.  **Resolution:** UHD (3840 x 2160) is a sensible upper limit to render on a single GPU nDisplay viewport. For machines with multiple GPUs, you can have multiple viewports that span across a larger display resolution. Either way, separate your stage mesh based on the resolution of the LED panels in increments of the maximum resolution at which you want each machine and viewport to render. Refer to your LED manufacturer for details on your per-panel resolution.
    
3.  **Control:** You might want to separate control between the ceiling and side walls, if you only use ceiling panels for lighting and reflections and they never appear in-camera. This is especially true if the LED panels are different models and require different color management. Color management is controlled per viewport, so you must break out these different panels into their own meshes.
    

These are considerations for how to separate the topology into meshes (and therefore viewports). It is common for a single machine to render multiple viewports, such as a ceiling and a wall. The important thing is that they are separate viewports on the single node.

Each mesh should have two UV sets in a particular order. The first UV set is used for calculating the projection for the PICP\_Mesh projection policy for nDisplay. The second UV set is used to ensure that the chroma key tracking markers move appropriately across seams between two viewports.

Each square on this example mesh represents an LED panel that is 500mm x 500mm with 2.6mm pixel pitch.

Mesh representation of a curved LED wall. Click image to enlarge.

The meshes should be modeled in a position and orientation to match the real-world LED panels. In this example, they are modeled upright. The geometry should be modeled to scale in cm.

Create the UV sets with the following specifications:

-   The first UV set should be scaled to cover the entire UV space in the range 0-1. This UV set should be unfolded as evenly as possible to avoid stretching. The scaling can be non-uniform. Ensure there is no padding around the edges of the UVs, and that the UVs do not go beyond the range 0–1.
    
    ![First UV set for the mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1471fcc7-23fa-453f-ac73-f44f03273600/led-mesh-uv1.png "First UV set for the mesh")
-   The second UV set should have the UVs aligned so that they match at the same seams as the actual hardware configuration. They should also have the same aspect ratio as the meshes.
    
    ![Second UV set for the mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/154da20d-0b7c-4869-bfc9-67c6b0f9d13d/led-mesh-uv2.png "Second UV set for the mesh")

When the meshes are created, export the geometry from the 3D modeling software and import them into the Unreal project. [Download this example mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/f2754cf6-790d-4c65-9adf-b1c092252604/examplecurvedwallmesh_ndisplay.fbx) and drag the file to the **Content Browser** into the **Content/nDisplayConfigs/Meshes** folder to follow the steps in the next section.

Once the meshes are imported into your Unreal Project, enable **Use Full Precision UVs** on each mesh to prevent UV artifacts appearing. Follow these steps for each imported mesh:

1.  Double-click the imported mesh to open it in the Static Mesh Editor.
2.  In the **Details** panel under **LOD 0**, expand **Build Settings** and enable **Use Full Precision UVs**.
    
    ![Enable Use Full Precision UVs in the Details panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/211be2b5-528f-471b-ae41-f5fd6572c3db/use-full-precision-uvs.png "Enable Use Full Precision UVs in the Details panel")
3.  Click the **Apply Changes** button.
    
    ![Apply Changes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6dfd8498-bfa2-43db-9da0-b9361ef8f421/apply-changes.png "Apply Changes")
4.  Click **Save**.
5.  Close the Static Mesh Editor.

## Step 3 - Define the LED Screens in Your Project

You will need to customize the layout and geometry of the screens in the project to reflect what you have on set. These meshes should be in the same physical position and dimensions as your LED wall in the real world in relation to your tracking system. The tracking system used on set will have a zero point. These meshes should be placed in the same world coordinates as they relate to the tracking system. Work with your tracking provider to find out where the zero point is and measure relative to this zero point to find the offsets.

These examples do not use the loopback address 127.0.0.1, because its use cannot be combined with other non-loopback addresses, such as those belonging to other machines, in the same Switchboard configuration. Loopback may be used, but only in a simple configuration where it is the only address used, and every device is local to the machine running Switchboard. Mixing loopback and non-loopback addresses in a multi-machine setup leads to connectivity errors.

Follow these steps to modify and customize the layout and geometry of the screens in the engine:

1.  In the **Content Browser**, navigate to the **nDisplayConfigs** folder.
    
2.  Right-click in the folder to open the Create Asset menu and choose **nDisplay > nDisplay Config**.
    
    ![nDisplay Config in the Create Asset menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35d71abf-373f-4578-9eec-5b9fd024a8d7/ndisplay-config.png "nDisplay Config in the Create Asset menu")
3.  In the **Pick a starting point for your nDisplay Config** window that appeared, choose **Create New Config** and click **Finish**.
    
    ![Create New Config](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a6aabdc4-0cba-461c-93c1-8fabc76f64de/create-new-config.png "Create New Config")
4.  Name the new nDisplay Config Asset **NDC\_ICVFXQuickStart**.
    
    ![Name the new nDisplay Config Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a9d343c-c2c2-42cd-8cc1-f3cfa44c88ff/quickstart-config-asset.png "Name the new nDisplay Config Asset")
5.  Double-click the **NDC\_ICVFXQuickStart** Asset to open it in the **nDisplay 3D Config Editor**.
    
    ![Open the new Asset in the nDisplay 3D Config Editor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0828d91-5128-4de4-8618-a1765c078fce/quickstart-config-editor.png "Open the new Asset in the nDisplay 3D Config Editor")
6.  In the **Components** panel, right-click the **nDisplayScreen** Component and select **Delete** to remove the component from the list.
    
    ![Delete nDisplay Screen Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca6b5d52-a99c-46c6-9801-96c2375a91dc/delete-ndisplay-screen.png "Delete nDisplay Screen Component")
7.  Click **Add Component** and add two **Static Mesh** Components to the Components panel.
    
    ![Add two Static Mesh Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/46020b38-fb38-4c32-b772-c784536d930f/add-static-mesh-component.png "Add two Static Mesh Components")
8.  Name one of the Static Meshes **CurvedWall\_Left**, and in its **Details** panel assign **ExampleCurvedWallMesh\_nDisplay\_WallLeft** to its **Static Mesh** parameter. Name the other **CurvedWall\_Right**, and assign **ExampleCurvedWallMesh\_nDisplay\_WallRight** to its **Static Mesh** parameter.
    
    ![Name the Static Meshes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f2762ef-5154-4dbd-af95-4e1603f099c2/curved-wall-left-right.png "Name the Static Meshes")
9.  Select both **Static Mesh** Components and rotate them so they're curving towards the View Origin Component. You will not see a preview of the projections on the meshes until Projection Policies have been set in a later step.
    
    ![Place and rotate the Static Mesh Components](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1713007e-c397-4663-b190-4bbf0e927f0f/place-static-mesh-components.png "Place and rotate the Static Mesh Components")
10.  In the **Cluster** panel, click the **Add New** button and choose **Add New Cluster Node**.
    
    ![Add New Cluster Node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e35406d1-55df-4b95-a626-090ea6897697/add-new-cluster-node.png "Add New Cluster Node")
    
    If you are using the NVIDIA Quadro Sync II with NVIDIA Quadro GPUs, select the **Cluster** item in the **Cluster** panel and set **Type** to **Nvidia (2)**.
    
    ![Set Cluster Type to Nvidia 2](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7b885f94-bb76-419a-a5a5-3dee415444fc/cluster-type-nvidia2.png "Set Cluster Type to Nvidia 2")
11.  A **Cluster Node** represents a host computer. In the **Add New Cluster Node** window that appears:
    
    1.  Set **Host IP Address** to your computer's external IP address. You must use your computer's external IP address instead of the default localhost IP address 127.0.0.1, if you want to add more computers to your nDisplay cluster later, because you cannot use both loopback and non-loopback addresses in a multi-machine setup. These steps use the IP address 192.0.2.0 as an example.
    2.  Enable **Fullscreen** to achieve synchronization and genlock.
    3.  Click **Add**.
        
        ![Setting the Host IP Address](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ce62ab9-ee28-4ade-b85a-f2e1acf499fe/save-host-ip-address.png "Setting the Host IP Address")
12.  A **Cluster Node** is created and a new viewport is assigned to the node. Select the viewport in the **Cluster** panel to open its **Details** panel.
    
    ![Select the viewport in the Cluster panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/db9bc908-4cf4-4910-ae63-f9b59bf6f68d/cluster-node-vp.png "Select the viewport in the Cluster panel")
13.  In the **Details** panel, set **View Origin** to **DefaultViewPoint**. This allows the associated component to control the point of projection for the outer frustum.
    
    ![Set View Origin to Default View Point](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/39634d17-7a03-4635-b415-3c7829326e3b/view-origin-default-vp.png "Set View Origin to Default View Point")
14.  Under the **Projection Policy** section of the **Details** panel for the viewport, set **Type** to **Mesh** and select your **CurvedWall\_Left** mesh from the list. Only Static Mesh Components added to the Components panel will show in the mesh list.
    
    ![Set Projection Policy Type to Mesh and select a mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d260efdb-d5c7-41a8-9111-84f70054dc85/proj-pol-type-mesh.png "Set Projection Policy Type to Mesh and select a mesh")
15.  See the test scene appear on the mesh in the viewport and in the **Output Mapping** panel.
    
    ![Set the test scene](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d96dd52-c3a0-4803-9fe9-12944d213fb1/test-scene-mesh.png "Set the test scene")
16.  Create a viewport for the other wall mesh. Right-click the **Cluster Node** and choose **Add New Viewport**.
    
    ![Add a new viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38abf3e7-f7e8-42c4-9838-8aceac8ef267/node-add-new-vp.png "Add a new viewport")
17.  In the **Add New Viewport** window that appears:
    
    1.  Set **View Origin** to **DefaultViewPoint**.
    2.  Under **Projection Policy**, set **Type** to **Mesh**.
    3.  Under **Projection Policy**, set **Mesh** to **CurvedWall\_Right**.
    4.  Click **Add**.
    
    ![Setting up the other wall mesh viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7d3b3b39-077b-4102-8f2b-7205691ff043/mesh-curved-wall-right.png "Setting up the other wall mesh viewport")
18.  A second viewport is created and the test scene appears on the wall mesh in the viewport and in the Output Mapping panel.
    
    ![The second viewport](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e8c806ec-94a5-4a92-b098-d9f1d0fecf9d/2nd-viewport.png "The second viewport")
19.  In the **Components** panel, add an **ICVFXCamera** Component. This component will give you inner-frustum controls and capabilities.
    
    ![Add an in-camera VFX camera component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6da33a42-2997-4704-b1b0-fd649730e5fd/add-icvfx-camera.png "Add an in-camera VFX camera component")
20.  Select the created **ICVFXCamera** Component and manipulate it within the **Preview Viewport**. You will see an inner-frustum projection preview on your projection meshes.
    
    ![The inner-frustum projection preview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bce2b9b-522b-4818-8b77-0c8c65903123/projection-preview.png "The inner-frustum projection preview")
21.  **Compile** and **Save** the asset.
22.  Drag the **NDC\_ICVFXQuickStart** Asset into the level to create an [nDisplay Root Actor](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine) and preview the level in the cluster.
    
    ![Creating the nDisplay Root Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca72367d-c511-4ddc-b69e-979b8c7ec40b/create-ndisplay-root-actor_smaller.gif)
23.  **Save** the project.

This section showed how to create your own nDisplay Config Asset and set it up with the previously created meshes. An example nDisplay Config Asset is already included in the project with a quad mesh layout. You can find this asset in the **Content Browser** at **nDisplayConfigs/nDisplayBasicExample**.

## Step 4 - Launch Your Project with Switchboard

Diagram shows how nDisplay works with a network and display devices for in-camera VFX. Click image to enlarge.

In an nDisplay setup, there is a *primary* computer and a *cluster* of additional computers. The primary computer is the centralized location for managing and dispatching input information. The primary computer also ensures all PCs in the cluster are synchronized and receive input and data at the same time. For more information on an nDisplay setup, see [nDisplay Overview](/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine).

[Switchboard](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine) is an external application that allows a single operator to control nDisplay clusters. Switchboard has additional features such as advanced logging, system monitoring, and integration with external software to simultaneously trigger third-party motion capture software take recording with [Take Recorder](/documentation/en-us/unreal-engine/record-gameplay-in-unreal-engine).

Follow the steps below to launch the nDisplay cluster with Switchboard:

1.  In the toolbar, click the **Switchboard** button. If this is your first time launching Switchboard, a command prompt appears and installs required dependencies.
    
    ![Launch Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d756681-c086-4b90-9ae9-731ab4508260/launch-switch.png "Launch Switchboard")
2.  In the toolbar, click the three dots next to the **Switchboard** button and in the dropdown menu choose **Launch SwitchboardListener**. This companion application must be run on every machine in the cluster to be able to connect to Switchboard.
    
    ![Launch Switchboard Listener](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0b76b3f-3401-4f60-8ab4-43e7601b2761/launch-sb-listener.png "Launch Switchboard Listener")
3.  Create a new **Switchboard Configuration** for the project.
    1.  If this is your first time running Switchboard, the **Add New Switchboard Configuration** window appears when Switchboard launches.
    2.  If you have run Switchboard before, click **Configs > New Config** in the top left corner of the window to open the **Add New Switchboard Configuration** window.
4.  In the **Add New Switchboard Configuration** window:
    
    1.  Set **Config Path** to **ICVFXQuickStart**.
    2.  Set **uProject** to the location of the In-Camera VFX Example Project on your computer.
    3.  Set **Engine Dir** to the location of Unreal Engine 5.
    4.  Click **OK**.
    
    ![Add a new Switchboard config](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/327ffe13-e9ab-4bc6-8806-48ee328752a0/add-new-sb-config.png "Add a new Switchboard config")
5.  In Switchboard, set **Level** to **Main**.
    
    ![Set Switchboard Level to Main](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5a08dfd4-c13b-445c-8288-e2b2ce4a5488/sb-level-main.png "Set Switchboard Level to Main")
6.  Click **Add Device > nDisplay** to open the **Add nDisplay Device** window.
    
    ![Add an nDisplay device](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7be2605-618f-4d0e-ab20-4f384694b981/add-ndisplay-device.png "Add an nDisplay device")
7.  In the **Add nDisplay Device** window, click the **Populate** button to see a list of available nDisplay Config Assets from the project. Select the nDisplay Asset created in the previous section, **NDC\_InCameraVFXQuickStart**, and click **OK**.
    
    ![Add the QuickStart Asset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/30f25e04-d417-4582-9a14-0aaa879a05be/add-quickstart-asset.png "Add the QuickStart Asset")
8.  The cluster node appears under **nDisplay Devices**.
    1.  Click its **Connect to listener** button to connect to the Switchboard Listener.
        
        ![Click Connect to listener on the new node](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a95163d8-9619-4337-b043-c6bc56b5503c/new-ndisplay-node.png "Click Connect to listener on the new node")
    2.  Click its **Start Unreal** button to launch Unreal with the nDisplay renderer.
        
        ![Start Unreal button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8bb9e7af-4ff3-401a-9994-953416a9bc6c/start-unreal.png "Start Unreal button")
9.  When nDisplay launches, all windows are minimized on the computer and the nDisplay view appears.

## Step 5 - Join Multi-User Session

The Multi-User Editing system enables robust collaboration to support any type of change. Multiple operator machines in the same Multi-User session can perform different tasks and modify the scene in real-time. In an nDisplay setup, Multi-User is responsible for synchronizing changes across the various instances of Unreal Engine on the cluster nodes to ensure that creative updates to the scene appear immediately and simultaneously on the LED wall during a shoot.

Follow the steps below to connect your Unreal Editor to the nDisplay renderer through Multi-User.

1.  In Switchboard, click the **Stop Unreal** button on the nDisplay node.
    
    ![Stop Unreal button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f48488d9-011c-4014-9104-9bcbe96f1677/stop-unreal.png "Stop Unreal button")
2.  Click the **Settings** button to open the **Switchboard Settings** window.
3.  Under the **Multi User Server** section:
    1.  Set **Server Name** to **ICVFXQuickStart\_MU\_Server**.
    2.  Enable **Auto Join** so any Unreal instances or nDisplay nodes automatically attempt to connect.
    3.  Enable **Auto Launch**. The **Multi User Server Executable** will not start without it enabled.
        
        ![The Multi User Server settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0d22ccb8-f165-405d-af7b-a867742507f6/enable-auto-launch.png "The Multi User Server settings")
4.  Close the **Settings** window.
5.  Set **Multiuser Session** to **ICFVXQuickStart\_Session\_001**.
    
    ![Set the multi user session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/311e15c7-3882-42b9-b185-9b72e57de445/multi-user-session.png "Set the multi user session")
6.  Click the **Start Unreal** button next to the nDisplay node to relaunch it.
    
    ![Start Unreal button](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/17d7f48e-477d-4302-af4c-e2dea58d8d63/start-unreal.png "Start Unreal button")
7.  Wait for the nDisplay node to finish launching before going to the next step.
8.  In the Editor's **Toolbar**, click the **Browse** button to open the **Multi-User Browser**.
    
    ![Browse button in the Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93767960-e840-4cd3-8464-3666ee2691bf/browse-button.png "Browse button in the Toolbar")
9.  In the **Multi-User Browser**, double-click **ICVFXQuickStart\_Session\_001** to connect your Unreal Editor to the multi-user session started with nDisplay.
    
    If the Unreal Editor displays a message about in-memory changes and prevents you from joining your multi-user session, it means that something in your editor may have an unsaved change and your project doesn't match the current state of the project running with nDisplay. All projects joining a multi-user session should be in the exact same state. To fix this, make sure to save the project before launching nDisplay.
    
10.  The Multi-User Browser will now change to show you the session you are currently connected to and the Level each user has active. The Clients category will show you which nodes and Editor instances are connected. History will list transactions that have been made over a Multi-User session. Details will show more information about the currently selected transaction in the History category.
    
11.  Changes you make in the Editor are now transmitted to the nDisplay node. Move the **Default View Point** Component for **NDC\_ICVFXQuickStart** to see the nDisplay view update with the changes in the Editor.

## Step 6 - Use Live Link for Camera Tracking

Live Link is a framework in the Unreal Engine for ingesting live data, including cameras, lights, transforms, and basic properties. For in-camera VFX, Live Link plays a critical role in distributing the tracked camera information and can be enabled to work with nDisplay to carry the tracking information to each cluster node. Unreal Engine supports many camera-tracking partners through Live Link, such as Vicon, Stype, Mo-Sys, and Ncam, as well as several other professional tracking solutions. Live Link also supports XR devices such as Vive Trackers and Controllers as a Live Link source.

It's important for this step that you have a Live Link source available. This guide will show how to set up Live Link XR in your project so you can use a VR headset and controllers for tracking. You can use similar steps to enable other Live Link sources. Refer to [Live Link XR](/documentation/en-us/unreal-engine/livelinkxr-in-unreal-engine) for more details.

To track the inner camera frustum via Live Link XR with nDisplay:

1.  In Unreal Editor's **main menu**, choose **Window > Virtual Production > Live Link** to open the Live Link panel.
    
    ![The editor with Live Link highlighted in the Window dropdown](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb019b58-2270-4552-b957-098b7c52d890/image_15.png "The editor with Live Link highlighted in the Window dropdown")
2.  In the Live Link panel, click the **Add Source** button. In the dropdown, choose **Live Link XR Source**.
    
3.  In the **Connection Settings** panel that appears, enable **Track Controllers** and **Track HMDs** and click **Add**.
    
    ![The connection settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0b7aa7a8-1086-47b0-8026-5667e6e9989c/live-link-connection-settings.png "The connection settings")
4.  When the Live Link XR Source is added, connected XR devices appear under the XR section of the Subject panel.
    
    ![Connected XR devices](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f9c0d5b9-a955-4b3f-b0bd-6e96b8189d6d/connected-xr-devices.png "Connected XR devices")
5.  In the Subject panel, select the XR device you're using for tracking to open its Details panel. In the Details panel, enable **Rebroadcast Subject** to share the tracking data with other computers in the Multi-User Session.
    
6.  Click **Presets** and select **Save as Preset**.
    
7.  In the main menu, select **Edit > Project Settings**.
    
8.  In **Project Settings,** under **Plugins**, select **Live Link**.
    
9.  Add the Live Link preset to **Default Live Link Preset** to make the preset automatically apply when the project runs.
    
    ![Set the Default Live Link Preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4afa05f4-b12c-46a4-921e-9f15657b0697/default-live-link-preset.png "Set the Default Live Link Preset")
10.  In the **Outliner**, select **DemoDisplay3\_innerFrustum** to open its **Details** panel.
    
11.  Click **Add Component** and choose **Live Link Controller** to add a **Live Link Component Controller** to the Cine Camera Actor.
    
12.  In **DemoDisplay3\_innerFrustum**'s **Component** section, select **LiveLinkComponentController** to view its settings.
    
13.  Under **Live Link**, set the **Subject Representation** parameter to your Live Link Subject. In this example, the Live Link Subject is a SteamVR Controller.
    
    ![Set the Live Link Subject Representation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eec61810-b4e4-4eca-a5e4-994c57f06dba/live-link-subj-repres.png "Set the Live Link Subject Representation")
14.  Select the ICVFX Camera Component of the NDC\_ICVFXQuickStart Actor to open its Details panel. Set Cine Camera Actor to DemoDisplay3\_innerFrustum.
    
    ![Set the Cine Camera Actor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0794067-ab6d-4673-a955-4c53f08e919b/set-cine-camera-actor.png "Set the Cine Camera Actor")
15.  When you move the XR device, the camera in the editor mimics the movement. The inner frustum also appears in the nDisplay preview when the camera faces the meshes.
    
16.  Save the project.
    
17.  Restart the nDisplay cluster to see the changes in the nDisplay renderer.
    

## Step 7 - Enable Green Screen and Chroma Key

You can change what displays in the inner frustum on the LED panels from the virtual world to a green screen with chroma key markers.

Follow these steps to make the green screen visible and to modify the chroma key markers:

1.  In the **Outliner,** select **NDC\_ICVFXQuickStart**.
    
2.  In the **Details** panel, select the **ICVFXCamera** Component to view its settings.
    
3.  In the **Details** panel under **Chromakey**, enable **Enable Inner Frustum Chromakey**.
    
    ![Enable inner frustum chromakey](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/01284517-9f42-44be-a270-8b77ee7a3e0f/enable-inner-frustum-chromakey.png "Enable inner frustum chromakey")
4.  The inner frustum turns green and tracking markers are rendered on top.
    
    Click image for full size.
    
5.  Change the parameters in the **Chromakey** section to modify the color, marker placement, and custom marker alpha textures. For more details on the settings, refer to [nDisplay Root Actor Reference](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine).
    

This section showed how to enable chroma key for the inner frustum. An example nDisplay Config Asset with chroma key enabled is already included in the project with a quad mesh layout. You can find this asset in the **Content Browser** at **nDisplayConfigs/nDisplayExample\_Chromakey**.

## Step 8 - Add Light Cards

Light Cards can be found in the nDisplay plugin content. Light Card Actors should be spawned to a separate layer to take advantage of nDisplay's Light Card control features and parented to the Config Actor's outer frustum viewpoint for optimum effect.

Follow the steps below to add Light Cards to your project.

1.  In the **Content Browser**, click **Settings** and enable both **Show Engine Content** and **Show Plugin Content**.
    
    ![View Options for the Content Browser](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/07710803-12f4-4f71-909f-403ff115e904/content-browser-view-options.png "View Options for the Content Browser")
2.  In the **Sources** panel, open the **nDisplay Content/LightCard** folder.
    
    ![Open the nDisplay Content Lightcard folder](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3e180590-e960-418a-86eb-fbac42b74822/ndisplay-content-lightcard.png "Open the nDisplay Content Lightcard folder")
3.  Drag the Blueprint **LightCard** into your level. In the **Outliner**, parent the **LightCard** actor to **NDC\_ICVFXQuickStart**.
    
    ![Dragging a Lightcard into the level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc233b00-aafa-45e0-8bcd-b8004044068c/lightcard-quickstart.png "Dragging a Lightcard into the level")
    
    The splines visualise the position of the lat/long location of the Light Card. For a better projection to the outer frustum, place the **Light Card** Actor in the same location as the View Origin Component in the nDisplay Root Actor.
    
4.  In the main menu, choose **Window > Layers** to open the **Layers** panel.
    
    ![The Layers panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86362e47-b502-4efa-bfc0-87091e8d7962/layers-window.png "The Layers panel")
5.  In the **Layers** panel, right-click and choose **Create Empty Layer** from the dropdown. Name the Layer **ICVFXQuickStart\_LightCards**.
    
    ![Create and name a Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bb7eabca-68bf-4212-b21a-8b5aa5c9e533/lightcards-layer.png "Create and name a Layer")
6.  In the **Outliner**, select the **Light Card**. Right-click the **ICVFXQuickStart\_LightCards** layer and choose **Add Selected Actors to Selected Layers**.
    
    ![Add Lightcard Actors to the Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ba998203-2ee9-4e06-9d99-5c089f30352a/add-lightcard-actor.png "Add Lightcard Actors to the Layer")
7.  In the **Outliner**, select **NDC\_ICVFXQuickStart** to open its **Details** panel.
8.  In the **Details** panel under **Light Cards**, add an **Array element** to the **Layers** parameter.
    
    ![Add an Array element to the Layer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/102df4ff-7288-496e-881b-ebe647bafea6/add-array-element.png "Add an Array element to the Layer")
9.  Set the **Layer Array element** to **ICVFXQuickStart\_LightCards**.
    
    ![Set the Layer Array element to your Lightcard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3995b5ce-a201-4703-a233-303a04a44ef9/set-layer-array-element.png "Set the Layer Array element to your Lightcard")

For more details on the Light Card settings, refer to [nDisplay Root Actor Reference](/documentation/en-us/unreal-engine/ndisplay-root-actor-reference-for-unreal-engine).

## Step 9 - Shoot with Multi-Frustum

Multiple inner frustums can appear in the nDisplay Config Asset. In this step we'll add a second **ICVFXCamera** component to the NDC\_ICVFXQuickStart nDisplay Config Asset and set it up for multi-frustum shooting.

Follow the steps below to add another ICVFX Camera Component to the nDisplay Config Asset.

1.  Stop all nDisplay nodes before the next step.
2.  In the **Content Browser**, double-click the **NDC\_ICVFXQuickStart** Asset. Currently, there will already be an **ICVFXCamera** Component present in the **Components** panel.
    
    ![Open the Camera Component](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/55549d43-b4c7-41a4-b2f3-7e926bf6f0fe/icvfx-camera-component.png "Open the Camera Component")
3.  Click **Add Component** and add another **ICVFXCamera** Component. Ensure both are parented to the **Root Component** in the Component hierarchy. Name the two **ICVFXCamera** Components as follows:
    
    1.  **ICVFXCamera\_ACam**
    2.  **ICVFXCamera\_BCam**
    
    ![Naming the cameras](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d9aef804-2484-49e1-ab0a-ab0f231154a2/icvfx-acam-bcam.png "Naming the cameras")
4.  Select the new **ICVFXCamera** component and manipulate it in the viewport to see the multiple frustum projections.
    
    ![Manipulting the multiple frustums](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dfe6bedc-c5e5-4257-aa1a-152d626f203d/multiple-frustums-moving.gif)
5.  **Compile** and **Save** the nDisplay Config Asset.
6.  The nDisplay Root Actor created from this Asset automatically is updated with the second camera in the level.
7.  In the **Outliner**, select **NDC\_ICVFXQuickStart** to open its **Details** panel. In the **Details** panel under **In-Camera VFX**, expand **Inner Frustum Priority** and change the order of the cameras. The camera listed first is rendered on top of the other when they overlap.
    
    ![Demonstrating frustum priority](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3563a4d-9882-41e7-9fee-d84018aefbec/frustum-priority.gif)
8.  Add a new **CineCamera Actor** to your level to reference it from the **ICVFXCamera** component. Add a **LiveLinkComponentController** to the new **CineCamera Actor** and connect a **Live Link Subject** to the Component.

This section showed how to add another camera with its own inner frustum to the nDisplay Config Asset. An example nDisplay Config Asset with two cameras is already included in the project with a quad mesh layout. You can find this asset in the **Content Browser** at **nDisplayConfigs/nDisplayExample\_multiFrustum**.

## Step 10 - Apply OpenColorIO Configuration

This section shows how to create an **OCIO Configuration Asset** from a plugin content OCIO config file and assign it to the **nDisplay Root Actor** viewports.

Follow these steps to use an OCIO configuration in the project:

1.  In the **Outliner**, select **NDC\_ICVFXQuickStart** to open its Details panel.
2.  In the **Details** panel under **OCIO**, check **Enable Viewport OCIO**.
3.  Expand **All Viewports Color Configuration**.
    1.  Set **Configuration Source** to **ExampleOCIO**.
    2.  Set **Source Color Space** to **Utility - Raw**.
    3.  Set **Destination Color Space** to **Output -sRGB Monitor**.

![Set the destination color space settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bad67384-3a34-4c50-9b9a-2e184889390d/set-destination-color-space.png "Set the destination color space settings")

These steps showed how to add an OCIO configuration to the project. You can also set OCIO configurations per viewport and separately on the inner frustum. For more on how to do this, refer to [Color Management in nDisplay](/documentation/en-us/unreal-engine/color-management-in-ndisplay-in-unreal-engine).

## Step 11 - Control the Scene Remotely

The **Remote Control Web Interface** is a customisable web application that utilises the **Remote Control API**. This section shows how to create a **Remote Control Preset** and make changes to your level from a web browser interface.

Follow the steps below to create your own Remote Control Preset and Remote Control Web Application.

1.  In the **Content Browser**, right-click and choose **Remote Control > Remote Control Preset** to create a new **Remote Control Preset** Asset.
    
    ![Create a new Remote Control Preset](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d346002c-6813-44c5-9508-e17a55eecfd5/create-remote-control-preset.png "Create a new Remote Control Preset")
2.  Double-click the **Remote Control Preset** Asset to open the **Remote Control Panel**.
    
    ![The Remote Control Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4eb71cc1-a74d-4870-ac27-3363f8233e44/open-remote-control-panel.png "The Remote Control Panel")
3.  In the **Outliner**, select the actor **CR\_Mannequin\_Body** to open its **Details** panel.
4.  In the **Details** panel under the **Transform** section, click the **Expose** button to expose the **Location** and **Rotation** properties to the Remote Control API.
    
    ![Expose the Locaton and Rotation properties to the Remote Control API](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40b2333d-d344-4a09-84bc-5131c53f69c4/expose-rotation-location.gif)
5.  In the **Remote Control Panel**, click the **Launch Web App** button to launch a web browser that will connect to the **Remote Control Web Application**. On your local computer, the web app is accessible at **127.0.0.1:7000**.
    
    ![Launch the web browser to connect to the Remote Control Web Application](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7ad33147-f9d5-43b0-99ba-77fab1e66655/launch-web-app.png "Launch the web browser to connect to the Remote Control Web Application")
6.  In the **Remote Control Web Application**, switch the **Control** toggle to **Design** mode.
    
    ![Toggle between Control and Design](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e077c661-fd37-4ee9-a208-c5c48b149f0e/toggle-control-design.gif)
7.  Select the **Properties** tab.
8.  Click and drag **Relative Location** to the empty canvas. A blue circle in the **Properties** tab appears next to the property when a property has been added to the interface.
    
    ![Click and drg the Relative Location widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/10a5dfff-2061-4612-b9ac-abd69a09f290/drag-relative-location-widget.gif)
9.  Click and drag **Relative Rotation** to the same canvas.
10.  Select the **Relative Location Widget** in the canvas to open its settings.
11.  In the widget settings for **Relative Location**, set **Widget** to **Joystick** to change the look of the widget.
    
    ![Set the widget to joystick](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6aae1d1-4581-41f0-b1f4-954b4bfca410/set-widget-joystick.png "Set the widget to joystick")
12.  Select the **Relative Rotation Widget** to open its settings.
13.  In the widget settings for **Relative Rotation**, set **Widget** to **Sliders**.
14.  Toggle from **Design** mode to **Control** mode to lock the interface.
15.  With your Editor viewport visible, interact with the UI controls to see how it affects your level.
    
    ![Manipulating the Remote Control UI to affect your level](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8199c65f-4c9f-45ad-b45e-75c683ae5949/widget-effects-on-ui.gif)

## Step 12 - On Your Own

This guide covered setting up displays on LED screens, launching your project on multiple computers, and incorporating camera tracking into the project. Additional example nDisplay Config Assets are included in the project in the nDisplayConfigs folder that show how to set up your cluster in other configurations including with multi-node and mGPU.

Multi-display setups require syncing capabilities at both software and hardware levels. Not only should the generated content be ready at the same time on all PCs, using the same timing information for simulation, but the display swap (the changing out of the current image for the next image in the video card buffer) needs to also happen at the correct time to prevent tearing artifacts in the display. See [synchronization in nDisplay](/documentation/en-us/unreal-engine/synchronization-in-ndisplay-in-unreal-engine#gettingsynctowork) for information on setting up display sync and genlock on the machines to create a seamless view across the multiple displays.

In addition to synchronizing the displays, the engine's timecode and frame generation needs to match the input from the camera. See [Timecode and Genlock](/documentation/en-us/unreal-engine/timecode-and-genlock-in-unreal-engine) for steps on how to sync the timecode and genlock the engine between all the devices.

To be able to control the scene and displays during a film shoot, you can try several of the How-Tos for in-camera VFX:

-   On-stage scene modification in real-time with [Multi-User Editing](/documentation/en-us/unreal-engine/getting-started-with-multi-user-editing-in-unreal-engine).
-   Live compositing using [Composure](/documentation/en-us/unreal-engine/real-time-compositing-quick-start-for-unreal-engine).
-   Match the lighting and shadows between the real-world set and the environment displayed on the LED walls with [Color Correct Regions](/documentation/en-us/unreal-engine/color-correct-regions-in-unreal-engine).
-   Save and restore Actor states for each take with [Level Snapshots](/documentation/en-us/unreal-engine/level-snapshots-in-unreal-engine).
-   Calibrate the display of content on your LED wall for your camera with the [In-Camera VFX Camera Calibration](/documentation/en-us/unreal-engine/camera-color-calibration-for-in-camera-vfx-in-unreal-engine) guide.
-   Receive and monitor events from every machine in your network with [Stage Monitor](/documentation/en-us/unreal-engine/stage-monitor-with-unreal-engine).
-   Monitor, calibrate, and view incoming timed data with the [Timed Data Monitor](/documentation/en-us/unreal-engine/timed-data-monitor-in-unreal-engine).
-   Use motion blur effectively in your process shots with [Camera Motion Blur in nDisplay](/documentation/en-us/unreal-engine/camera-motion-blur-with-ndisplay-in-unreal-engine).
-   Color correct for only the displays and inner frustum with [Color Management in nDisplay](/documentation/en-us/unreal-engine/color-management-in-ndisplay-in-unreal-engine).

This guide walked through the basics of in-camera VFX projects. For an example of a real production project, refer to the [In-Camera VFX Production Test](/documentation/en-us/unreal-engine/in-camera-vfx-production-test-sample-project-for-unreal-engine).