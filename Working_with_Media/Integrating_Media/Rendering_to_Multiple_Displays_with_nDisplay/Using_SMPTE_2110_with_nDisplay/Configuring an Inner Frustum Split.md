# Configuring an Inner Frustum Split

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/inner-frustum-split-for-smpte-2110-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/inner-frustum-split-for-smpte-2110-in-unreal-engine)  
**Processed:** 2025-06-14 16:30:59

---

This tutorial guides you through the configuration setup for an inner frustum split on a nDisplay ICVFX Camera using SMPTE 2110.

With SMPTE 2110 support, you can now dedicate an entire nDisplay render node to just the inner frustum. Unreal Engine provides the ability to render the Inner Frustum with even more hardware resources, across both multiple nodes as well as multiple GPUs (similar to a [Multi-Process](/documentation/en-us/unreal-engine/multi-process-rendering-with-unreal-engine) deployment), to produce the highest quality Inner Frustum possible. As new cameras increase in resolution and volumes increase in size, the system can scale with the needs of modern productions.

![Using multiple nodes for an inner frustum split on-set for an ICVFX shoot.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fc8d25fe-d198-46dc-84c4-1ed9ef193248/image_0.png)

Using multiple nodes for an inner frustum split on-set for an ICVFX shoot.

## Configuration

![A sample configuration diagram for an inner frustum split using nDisplay and SMPTE 2110.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/152d1151-b51a-4bfd-860d-fc44081cb7d4/image_1.png)

A sample configuration diagram for an inner frustum split using nDisplay and SMPTE 2110.

1.  Create an [nDisplay configuration](/documentation/404).
    
2.  Add a Node layout that reflects the deployment of your setup.
    
    ![Add a Node layout.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bc84689-6474-4034-90f2-c2b483197297/image_2.png)
    -   Nodes 1 and 2 render the wall and ceiling, respectively.
        
    -   Nodes 3 and 4 render the inner frustum tiles (0,0) and (0,1) respectively, and both have the **Headless Rendering** setting enabled (set this in their configuration accordingly), which means they render no (outer) viewports.
        
3.  Add an ICVFX Camera component.
    
    ![Add an ICVFX Camera component.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/57b815ba-5cad-4261-8451-e3d62888b9e5/image_3.png)
4.  Select the ICVFX Camera component and go to the **Details** panel.
    
    ![Enable Media and select Tiled as the Inner Frustum Type.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18c9a5d3-3dab-4dda-a23e-71b512fb0876/image_4.png)
    -   Enable **Media**, and set the **Inner Frustum Type** to **Tiled**.
        
    -   Use the **Tiled Split Layout** values to set the number of tiles in the horizontal (x) and vertical (y) directions.
        
        -   In this example, the total number of tiles to render is two (2) – two tiles horizontally and one vertically.
5.  Under the settings for **Tile Overscan** set the following properties to use overscan to improve tile blending:
    
    -   Enable **No Overscan for Edges**.
        
    -   Set the **Overscan Value** to 5% or higher.
        
        ![Set the Overscan Value](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0243fbfa-e1b3-403d-9e50-4455c7ec7db1/image_5.png)
6.  (Optional, see the [Tile Configuration Wizard](/documentation/en-us/unreal-engine/inner-frustum-split-for-smpte-2110-in-unreal-engine#tileconfigurationwizard) section below.) Under **Media Output Groups**, create a group for each set of nodes that will render Inner Frustum tiles. In this example, the first tile (0,0) will render on Node\_3 and the second tile will render on Node\_4 (1,0).
    
    ![Create groups for each set of nodes under Media Output Groups.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1dc624d6-ff2c-4d67-8311-893021549895/image_6.png)
7.  Select **NVIDIA Rivermax Output** as the Media Output. This means you can set up the SMPTE 2110 stream with the specified parameters.
    
    ![Set up the SMPTE 2110 stream parameters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/857b476c-27a6-46c6-94cf-0e7201d4c6f4/image_7.png)
    
    Most properties will be initialized by default.
    
    -   The **Resolution** is automatically set based on the tile layout, and you should not need to set specific values.
        
    -   Set the correct **Interface Address** and **Stream Address** for your network.
        
    -   You must set the **Frame Rate** higher than the rendering rate. If the bandwidth permits it, it should be at least twice as high.
        
    -   If you want to use GPU Direct, Unreal Engine supports it when **Frame Locking Mode** is set to **Block on Reservation** and **Alignment Mode** is set to **Frame Creation**, so set those values accordingly.
        
    -   Leave **Capture Synchronization** set to **None**.
        
8.  Under **Media Input Groups**, specify the nodes that will receive the inner frustum tiles.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/806b5750-294b-4e1a-b57c-2b2e6a2e100b/image_8.png)
    -   Create a **Media Input Group** for each group of outer viewports that will receive the inner frustum tiles.
        
        -   In this example, there are two tiles, and both should be visible by Node\_1 (wall) and Node\_2 (ceiling).
    -   Add the number of tiles to match the number configured to render in **Media Output Groups**. Each index is an inner frustum tile to deliver to the Nodes above.
        
    -   For each tile, specify the relevant tile coordinates, add an **NVIDIA Rivermax Source**, and match the stream settings of the Media Output groups.
        
        Some deployments might want to specify a different **Interface Address** or remove the wild card. Ensure the frame rate matches between input and output.
        
    -   GPUDirect is supported on input if the PCI-e root complex is the same.
        

## Media Tiles Configuration Wizard

You can use an automated workflow to configure your tiles, by means of the **Media Tiles Configuration** wizard. Its purpose is to simplify the process of configuring tiles, as much as possible.

Steps 6-8 in the configuration workflow above remain valid, and you can use them for manual split configuration.

The key features of the Media Tiles Configuration wizard are to:

-   Automatically generate input and output groups based on the tile layout.
    
-   Automatically configure pre-defined media parameters with default settings.
    
    -   The only pre-defined media are NVIDIA Rivermax and Shared Memory Media.
        
    -   Default parameters are pre-configured and ready to use.
        

To start the configuration wizard, click **Configure Tiles**.

![The Configure Tiles button starts the tile configuration wizard.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/758c426b-5143-4b4f-be90-1f5911e44597/image_16.png)

The Configure Tiles button starts the tile configuration wizard.

The configuration process starts with the layout configuration of the tiles.

![The Media Tiles Configuration wizard.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7f2e6712-324a-40d5-a576-6ec6b8b4bb4d/image_17.png)

The Media Tiles Configuration wizard.

1.  Select the tiles that represent the split layout you need for your setup, then click **Next**. For the example shown below, we split the inner frustum into two tiles horizontally, and therefore selected the **2x1** layout.
    
    ![Selecting a two-tile split layout.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5bfbafa2-ddfe-405b-956f-9da766385062/image_11.png)
2.  Specify your **Media Source** and **Media Output** types. The example below uses NVIDIA Rivermax for both.
    
    ![Specify your Media Source and Media Output.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/29bf92f4-d073-4559-85d5-1ad2995a26ad/image_12.png)
3.  Specify which nodes produce and send tiles, and which ones consume and receive tiles.
    
    This is a preliminary input and output configuration step. The next step has more flexibility.
    
    ![Specify your nodes.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9a7bc7d6-99b3-49b0-b6d7-4563d8df10b2/image_13.png)
4.  The tile mapping is pre-configured based on the data provided in the previous step. If necessary, you can manually map the tiles to nodes that will render them.
    
    In the example below, there are two tiles. The left one is mapped to **Node\_3**, the right one is mapped to **Node\_4**. For a simple example such as this, this is fine, but for more complex setups, you can click any tile and manually pick another node(s) to render it.
    
    ![Review your tile mapping.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/446076a0-8227-44b4-8b4c-3912d2774c13/image_14.png)
5.  Click **Finish** to complete the configuration process.
    

With the configuration wizard complete, the camera settings are updated with all the tiled media settings.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/347859bf-9b67-4263-9174-e95ebcf38b51/image_15.png)

NVIDIA Rivermax and Shared Memory Media are configured automatically by default. You can manually modify settings if needed, but in most cases the default settings should be sufficient.

The **Reset Media Input and Output to Default** button resets all the existing media input and output settings to the default pre-configured settings. You can use this to revert unsuccessful manual changes back to the original default settings.

## Multi-Process Inner Frustum Split

If you have a deployment with render nodes that have multiple (2 or more) GPUs, you might choose to combine a [Shared Memory/Multi Process](/documentation/en-us/unreal-engine/multi-process-rendering-with-unreal-engine) deployment with SMPTE 2110 and an inner frustum split. This means you can devote more resources to each viewport and inner frustum tile, while reducing the total number of render nodes required for the deployment.

In the following example, the same setup as in the previous example is laid out with 3 hosts instead of 4, with the outer viewports no longer sharing the same process/GPU:

-   Each viewport is rendered on its own Node/GPU on the same host, and the configuration uses both shared memory and SMPTE 2110 media.
    
-   Each inner frustum tile is rendered on its own node/GPU on the same host, and the configuration shares with SMPTE media only.
    

![The hosts and nodes for a multi-process inner frustum split using nDisplay and SMPTE 2110.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27e8c61f-36bd-497a-a4fd-47f78fc52442/image_9.png)

The hosts and nodes for a multi-process inner frustum split using nDisplay and SMPTE 2110.

![A sample configuration diagram for a multi-process inner frustum split using nDisplay and SMPTE 2110.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6d5902da-111b-4229-a3dc-a5a63b1f7a58/image_10.png)

A sample configuration diagram for a multi-process inner frustum split using nDisplay and SMPTE 2110.