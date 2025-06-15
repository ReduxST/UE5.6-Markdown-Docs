# NDisplay Workflows

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-workflows-for-smpte-2110-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-workflows-for-smpte-2110-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:27

---

This guide provides instructions for setting up SMPTE 2110 using NVIDIA Rivermax to work with nDisplay, specifically when working with in-camera VFX (ICVFX) and an LED wall.

### nDisplay ICVFX Camera Streaming

The integration of media sharing and offscreen rendering provides a way for you to leverage SMPTE 2110 media sources and outputs to make your clusters perform more optimally. You can move the render of each ICVFX camera to its own machine, and then use SMPTE 2110’s multicast capabilities to deliver those camera streams to other nodes that depend on them.

This means you can dedicate render nodes to rendering cameras, which generally scales better than rendering all the inner frustums on all render nodes. With this configuration, you are not changing the way UE sends pixels to the wall. A synchronization card is still used by compositor nodes to send their output synchronously. However, render nodes dedicated to rendering inner frustums don’t need a synchronization card. Also, in this configuration PTP timing isn’t used for the SMPTE 2110 stream shared between instances of UE.

[![SMPTE ST 2110 ICVFX camera streaming.](https://dev.epicgames.com/community/api/documentation/image/ce403646-0c46-4c4e-874b-8a13e09bd53e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ce403646-0c46-4c4e-874b-8a13e09bd53e?resizing_type=fit)

SMPTE ST 2110 ICVFX camera streaming.

Here’s an example of how you can configure a cluster of three nodes and two ICVFX cameras. This example starts from an existing stage configuration to show the process of converting it to leverage these new additions.

#### Node Configuration

1.  In the **Content Browser**, search for then open your nDisplay configuration. This example is named **NDC\_MyStage**:
    
    [![image alt text](https://dev.epicgames.com/community/api/documentation/image/a0627833-258a-4a5c-8424-3c0d5f28cbd4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a0627833-258a-4a5c-8424-3c0d5f28cbd4?resizing_type=fit)
    
    This configuration has 3 nodes driving the wall, and each of them renders a set of viewports. These won’t be modified.
    
    | Node | Viewports |
    | --- | --- |
    | 
    Node\_1
    
     | 
    
    VP\_W1
    
     |
    | 
    
    Node\_2
    
     | 
    
    VP\_W2
    
     |
    | 
    
    Node\_3
    
     | 
    
    VP\_C1 VP\_C2
    
     |
    
2.  It also has two ICVFX cameras. For each of them, click **+Add,** then select **Add New Cluster Node** to create a node you will use to render that camera.
    
    [![Add button options](https://dev.epicgames.com/community/api/documentation/image/2bb43ea7-31db-4279-b193-3cf1a0197ab2?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2bb43ea7-31db-4279-b193-3cf1a0197ab2?resizing_type=fit)
    
    For each node:
    
    -   Give it a name that identifies the camera to render for.
        
    -   Disable **Adjust Cluster Node Position to Prevent Overlap**.
        
    -   Disable **Add Viewport to New Cluster Node**.
        
    -   Set the desired host IP.
        
    -   Enable Headless Rendering.
        
    -   Configure the graphics adapters if your system has more than one.
        
3.  When fully configured, your **Add New Cluster Node** dialog box should resemble the following image.
    
    [![Add New Cluster Node dialog box options](https://dev.epicgames.com/community/api/documentation/image/a9e39a7f-0121-4e9a-a672-3d159aa3fd35?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/a9e39a7f-0121-4e9a-a672-3d159aa3fd35?resizing_type=fit)
    
4.  When you are done creating the nodes, your cluster should resemble the following image:
    
    [![Cluster nodes](https://dev.epicgames.com/community/api/documentation/image/1a60db6f-75dd-4566-a49b-2beea21cc981?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1a60db6f-75dd-4566-a49b-2beea21cc981?resizing_type=fit)
    

#### Media Configuration–ICVFX Camera A Output

Once you have configured nodes dedicated to rendering the camera frustums, continue and configure the media sharing.

1.  In your stage outliner, select **ICVFXCameraA**.
    
    [![Select ICVFXCameraA](https://dev.epicgames.com/community/api/documentation/image/8903798d-4afe-45a5-a9df-09449d4bbd79?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8903798d-4afe-45a5-a9df-09449d4bbd79?resizing_type=fit)
    
2.  In the **Details** panel, find the **Media** section:
    
    [![Media section in the Details panel](https://dev.epicgames.com/community/api/documentation/image/dc794adb-5279-4144-9fea-f0e31f65251f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/dc794adb-5279-4144-9fea-f0e31f65251f?resizing_type=fit)
    
3.  Check the **Enable** checkbox.
    
4.  Add a **Media Output Group**. Here, you are configuring which node will render this inner frustum and how it will be shared.
    
5.  The node you want to render this camera is **Node\_CamA** for **ICVFXCameraA**. If you want to configure ICVFXCameraB, select Node\_CamB instead.
    
6.  Configure the **MediaOutput type** to be **Nvidia Rivermax Output** to share it using ST 2110. Some settings here are important:
    
    -   Set **Alignment Mode** to **Frame Creation**, which means that your output will start streaming the rendered frustum as soon as it’s available, always respecting the configured frame interval of the stream.
        
    -   Set **Frame Locking** mode to be **Block On Reservation**, to make sure you are sharing every frame rendered.
        
    -   Enable **DoFrameCounterTimestamp**. This embeds Unreal Engine’s frame number in the video stream, and will be used by the receiving nodes to know which samples correspond to what frame.
        
    -   Enforcing **Resolution** isn’t required, because UE will detect the frustum size automatically once it is captured.
        
    -   **Frame Rate** is important. The 2110 standard, like SDI, transfers a video frame over the whole frame interval. If you configure your 2110 video stream at 24 fps, each frame takes 41ms to be entirely received by listeners. To minimize latency, and depending on the available bandwidth of your network card, configure your frame rate to be faster than the rate your cluster is presenting. This means that for a cluster running at 24 fps, you should stream out the inner frustum faster than this. Using 48, 60, or an even faster frame rate is preferable, but take into consideration bandwidth usage.
        
    -   For the **Interface Address**, use wildcards to make the configuration as flexible as possible to work on different machines with different IPs.
        
    -   For the **Stream Address**, pick a unique multicast address to avoid two inner frustums streaming on the same address. If that occurs, receivers won’t be able to distinguish them. In the example shown here, CameraA will use 225.1.1.10 and CameraB will use 225.1.1.11.
        
    -   **Capture Synchronization** isn’t needed here since this stream isn’t going to the wall.
        

Your output configuration should resemble the following image:

[![SMPTE 2110 nDisplay ICVFX output settings configuration.](https://dev.epicgames.com/community/api/documentation/image/e132b198-3acb-4418-84f0-a9770efa7cf0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/e132b198-3acb-4418-84f0-a9770efa7cf0?resizing_type=fit)

SMPTE 2110 nDisplay ICVFX output settings configuration.

#### Media Configuration–ICVFX Camera A Input

Now that the output side of the ICVFXCameraA render is configured, you can work on the reception side. Here, you will configure which nodes will receive the shared render and how they will receive it.

1.  First, add a **Media Input Group**.
    
2.  Add **Cluster Nodes** to receive this output. In this case, you want all nodes that are driving the wall (Node\_1, Node\_2, Node\_3).
    
3.  To receive the shared render using ST 2110, configure the **Media Source** to be **Rivermax Media Source**. Some settings need to be set up correctly for low-latency framelocking to work.
    
    -   For **Player Mode**, use **Framelock** to have receivers wait for an expected frame every render. Using the embedded frame number, receiving instances of UE can match video samples with the current frame number. If a frame hasn’t arrived yet, the receiving instances will wait for it with the expectation that it will arrive.
        
    -   You can use the **Use Zero Latency** option to have the receiver UE instances wait for a frame number matching the current one with no added latency. Depending on the content, this might not be achievable, so you have the option to add a frame of latency to get more margin waiting for the inner.
        
    -   The **Resolution** doesn’t need to be enforced because it will be auto-detected by the receiver UE instances when the stream is received.
        
    -   Configure the **Frame Rate** with the same rate you used for the output.
        
    -   For the **Interface Address**, use wildcards again because this will be used by multiple nodes of the cluster and they won’t have the same interface IP.
        
    -   Configure **Stream Address** and **Port** match the output configuration.
        
    -   You can enable **GPU Direct**, however make sure that the GPU and DPU (Mellanox card) are on the same root complex. If they aren't, the 2110 packets can be lost especially if there are multiple input streams.
        
    -   To fully enable GPU Direct on input, set `Rivermax.GPUDirectInput=1` on Unreal Engine startup or before starting the Rivermax stream.
        

You input configuration should resemble the following image:

[![SMPTE 2110 nDisplay ICVFX input settings configuration.](https://dev.epicgames.com/community/api/documentation/image/188516e0-66cc-4e89-9afa-c1002aa729c0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/188516e0-66cc-4e89-9afa-c1002aa729c0?resizing_type=fit)

SMPTE 2110 nDisplay ICVFX input settings configuration.

Your ICVFXCameraA is now configured to be shared from one render node to the cluster. Media settings should look like this:

[![SMPTE 2110 nDisplay ICVFX media settings configuration.](https://dev.epicgames.com/community/api/documentation/image/f85f05e0-ee5f-405b-a4f0-feb65384298d?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/f85f05e0-ee5f-405b-a4f0-feb65384298d?resizing_type=fit)

SMPTE 2110 nDisplay ICVFX media settings configuration.

#### Media Configuration–ICVFX Camera B

When you are done configuring ICVFXCameraA, you can configure ICVFXCameraB which will use mostly the same settings except for the following details:

1.  Media Output Groups
    
    -   The **Cluster Node** rendering ICVFXCameraB will be Node\_CamB.
        
    -   The **Stream Address** must be different. Use 225.1.1.11, but keep the same **Port** number.
        
2.  Media Input Groups
    
    -   The **Stream Address** is the only setting you must change to match the output configuration, in this example 225.1.1.11.
        

You can use a faster frame rate for your 2110 streams to reduce latency. This comes at a higher bandwidth cost, so take that into account based on your network configuration. If there are other devices using bandwidth on the same network, you must also consider them too.

Example bandwidth usage:

-   4k24 RGB10
    
    -   ~6.3Gb/s
        
-   4k48 RGB10
    
    -   ~12.6Gb/s
        
-   8k24 RGB10
    
    -   ~25Gb/s
        
-   8k48 RGB10
    
    -   ~50Gb/s
        

### nDisplay ICVFX Camera Streaming and Synchronous Output (Experimental)

#### Requirements

The other nDisplay area you can update is about how you send your renders to the LED wall. Instead of sending streams from the GPU, you can now send ST 2110 streams directly from the network card. By providing a common PTP time reference to each node, you can framelock and synchronize each stream going to the wall, instead of relying on a synchronization card.

This requires:

-   A master clock generating PTP.
    
-   A switch that supports ST 2110 streams.
    
-   A compliant Nvidia network card, such as the ConnectX-6 BlueField-2 card.
    
-   The LED processor must also be able to receive ST 2110 streams.
    

[![SMPTE ST 2110 ICVFX synchronous camera streaming.](https://dev.epicgames.com/community/api/documentation/image/0ea24f60-e8cd-4e2f-bf41-d2dd9f49b7af?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/0ea24f60-e8cd-4e2f-bf41-d2dd9f49b7af?resizing_type=fit)

SMPTE ST 2110 ICVFX synchronous camera streaming.

When configured in this way, all your nodes are configured as headless or offscreen. You don’t need to have mosaic configured or deal with EDID settings anymore, since you are not streaming using the GPU. However, the PTP time reference going to each node needs to be valid all the time.

For this configuration to work, **the optional section about PTP setup mentioned in the deployment phase is mandatory.**

#### Configuration Basics

In terms of nDisplay configuration, this feature doesn’t change how you configure the ICVFX camera streaming. Instead, this feature leverages the media output configuration you can set at the node level to stream out the final back buffer rendered by a given node. You must also configure the framelocking.

When configuring each node’s window size, depending on the LED processor receiving the streams, there might be constraints on this. If the same processor receives two streams, you might need to make each stream the same size. Here's how to enforce that constraint for the same example cluster described previously.

[![The 3 node streams in their original configuration.](https://dev.epicgames.com/community/api/documentation/image/4682da36-13fc-441d-89b0-596870863ea6?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4682da36-13fc-441d-89b0-596870863ea6?resizing_type=fit)

The 3 node streams in their original configuration.

In the example, you have three nodes to send out, Node\_1, Node\_2 and Node\_3. As you don’t have resolution constraints, you can make the nodes window as tight as possible to send the minimum amount of pixels required. In this case, you will set Node\_1 and Node\_2’s window to the same size by adding a constraint. Consider them as using the same LED processor. The Node\_3 stream won’t have this constraint and won’t have the same window size.

#### Node Configuration–Node\_1 and Node\_2

Begin with the Node\_1 and Node\_2 configurations. In the original configuration:

-   Node\_1 used a full-screen node with a window size of 7680x2160 with a viewport of 2640x1408.
    
-   Node\_2 used a full-screen node with a window size of 3840x2160 with a viewport of 3344x1408.
    

[![The original example configuration settings of Node_1.](https://dev.epicgames.com/community/api/documentation/image/ef142ad8-28de-4857-b8ac-4849c9b5b663?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ef142ad8-28de-4857-b8ac-4849c9b5b663?resizing_type=fit)

The original example configuration settings of Node\_1.

[![The Node_1 stream in the VP_W1 viewport using the original example settings.](https://dev.epicgames.com/community/api/documentation/image/1255125c-d965-4834-a54d-4b03a05f681f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1255125c-d965-4834-a54d-4b03a05f681f?resizing_type=fit)

The Node\_1 stream in the VP\_W1 viewport using the original example settings.

[![The Node_2 stream in the VP_W2 viewport using the original example settings.](https://dev.epicgames.com/community/api/documentation/image/356a6fc5-da51-4003-bac7-eeec624bbf8c?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/356a6fc5-da51-4003-bac7-eeec624bbf8c?resizing_type=fit)

The Node\_2 stream in the VP\_W2 viewport using the original example settings.

1.  Since viewport VP\_W2 is the largest, make the settings for Node\_1 and Node\_2 identical, and use VP\_W2’s size of 3344x1408.
    
2.  Enable the **Headless Rendering** setting to set both nodes offscreen, and disable the **Fullscreen** setting.
    

[![The modified settings for both Node_1 and Node_2.](https://dev.epicgames.com/community/api/documentation/image/201cb1ce-f877-46de-b1db-c49ad3bd571a?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/201cb1ce-f877-46de-b1db-c49ad3bd571a?resizing_type=fit)

The modified settings for both Node\_1 and Node\_2.

[![The Node_1 stream in the VP_W1 viewport after changing the settings.](https://dev.epicgames.com/community/api/documentation/image/452cf5fa-3e31-48b1-afa8-8c7790a42b92?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/452cf5fa-3e31-48b1-afa8-8c7790a42b92?resizing_type=fit)

The Node\_1 stream in the VP\_W1 viewport after changing the settings.

[![The Node_2 stream in the VP_W2 viewport after changing the settings.](https://dev.epicgames.com/community/api/documentation/image/1e32373e-f1ed-484a-96bb-29f63a3737ba?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/1e32373e-f1ed-484a-96bb-29f63a3737ba?resizing_type=fit)

The Node\_2 stream in the VP\_W2 viewport after changing the settings.

This change added some extra pixels to Node\_1's stream to match the dimensions of Node\_2’s stream. When viewports are not all equal, it’s important to consider how they are organized per node to minimize wasted bandwidth.

Now, configure the media output of each node. Media can be configured at the node level (final backbuffer) and the viewport level. It’s important to do this configuration on the node to send the final composited and warped result.

1.  Select Node\_1 and find its Media section:
    
    [![Node 1 Media section](https://dev.epicgames.com/community/api/documentation/image/3a5eb1f2-7ddf-4c87-9d59-58dd8a44f348?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/3a5eb1f2-7ddf-4c87-9d59-58dd8a44f348?resizing_type=fit)
    
2.  Enable **Media** configuration:
    
    [![Enable Media configuration](https://dev.epicgames.com/community/api/documentation/image/6482fa7f-b2e6-47ef-b3dd-14f6e966670f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/6482fa7f-b2e6-47ef-b3dd-14f6e966670f?resizing_type=fit)
    
3.  Add a **Media Output**:
    
    [![Add a Media Output](https://dev.epicgames.com/community/api/documentation/image/d91878c3-de40-48fa-a13a-3859001cd345?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d91878c3-de40-48fa-a13a-3859001cd345?resizing_type=fit)
    
4.  Configure the Media Output to be **NVIDIA Rivermax Output** and configure the settings accordingly:
    
    -   **Alignment Mode: AlignmentPoint**. You need to align your output with Genlock by using PTP time reference so you need your output to send at known alignment points.
        
    -   **Do Continuous Output: True**. If a frame was not rendered in time, your output must continue and repeat the previous frame.
        
    -   **Frame Locking Mode: Block on Reservation**. You want to stream all rendered frames.
        
    -   **Presentation Queue Size: 2**. Double buffering is ideal to minimize latency.
        
    -   **Number of Texture Buffers: 3**. There are no hard requirements for this one.
        
    -   **Resolution: Unchecked**. You don't need to enforce a resolution. Leaving it unchecked will create a stream using the size of the node’s back buffer.
        
    -   **Frame Rate:** *Project dependent*. The example uses 24fps but your project might use a different setting.
        
    -   **Pixel Format: RGB10**. This can vary for your project and the receiver (LED Processor) must support that format.
        
    -   **Interface Address: 10.69.70.***. In this example, all nodes are in the subnet 10.69.70.* to facilitate changing which machine is rendering each node. Using a wildcard on the last octet means the selected node is able to resolve to its local interface address.
        
    -   **Stream Address**: *Unique Node\_1 stream address*. For this example, use **225.1.2.1** here and increment the last octet for each node to have a unique multicast address per node. Make sure the multicast group used here is not already used on your network to avoid collisions.
        
    -   **Port: 50000**. This example uses 50000 for all nodes and only the multicast address changes.
        
    -   **Use GPUDirect: FALSE**. This isn’t supported for framelocked ST 2110 output at the moment.
        
    
    [![Configured Media Output settings](https://dev.epicgames.com/community/api/documentation/image/7c9418b9-c605-43f0-9f35-13b32ce4c20f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/7c9418b9-c605-43f0-9f35-13b32ce4c20f?resizing_type=fit)
    
5.  Configure the **Capture Synchronization** to use **Rivermax (PTP)**. This enables a mechanism enforcing framelocking across the cluster by using an ethernet synchronization barrier leveraging a common PTP time reference for the whole cluster.
    
    -   **Margin (ms): 5**. Use the default value. This is a time margin referenced when the node is about to enter the capture sync barrier, just before queuing a frame for presentation. If it detects that it’s too close to the next alignment point (by the margin), it delays entering the barrier.
        
    -   **Barrier Timeout (ms): 3000**. Use the default value. This is a timeout to exit the barrier when all nodes haven’t joined before the timeout period ends.
        
    
    [![Configured Capture Synchronization settings](https://dev.epicgames.com/community/api/documentation/image/75740c82-d626-4159-9804-368421d3b1ab?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/75740c82-d626-4159-9804-368421d3b1ab?resizing_type=fit)
    

The Node\_1 configuration is now complete, and its settings should look like this:

[![The Node_1 Media settings for the nDisplay ICVFX camera streaming and synchronous output example.](https://dev.epicgames.com/community/api/documentation/image/b11129f3-32fd-446a-8311-588e7500eece?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/b11129f3-32fd-446a-8311-588e7500eece?resizing_type=fit)

The Node\_1 Media settings for the nDisplay ICVFX camera streaming and synchronous output example.

Now that the Node\_1 configuration is complete, proceed to configure Node\_2. Its configuration should be identical to Node\_1's, except for the **Stream Address**, which needs to be **unique**.

1.  Configure the Node\_2 settings to be identical to Node\_1.
    
2.  Set the Node\_2 **Stream Address** to use 225.1.2.2.
    

Here’s the final configuration of Node\_2:

[![The Node_2 Media settings for the nDisplay ICVFX camera streaming and synchronous output example.](https://dev.epicgames.com/community/api/documentation/image/380164cb-6566-4c84-aace-4fec2a519f6b?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/380164cb-6566-4c84-aace-4fec2a519f6b?resizing_type=fit)

The Node\_2 Media settings for the nDisplay ICVFX camera streaming and synchronous output example.

#### Node Configuration–Node\_3

Proceed to configure Node\_3. In the original example described above, there was a gap between the two viewports.

[![The original example viewports setup showing the gap between them.](https://dev.epicgames.com/community/api/documentation/image/acb6485b-f9e9-4e34-966c-7ca32826d2eb?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/acb6485b-f9e9-4e34-966c-7ca32826d2eb?resizing_type=fit)

The original example viewports setup showing the gap between them.

To reduce wasted space, you can configure the viewports to eliminate the gap.

[![The viewports configured to eliminate the gap.](https://dev.epicgames.com/community/api/documentation/image/bd282c0b-d53a-4545-b449-4817c7c346b7?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/bd282c0b-d53a-4545-b449-4817c7c346b7?resizing_type=fit)

The viewports configured to eliminate the gap.

Then, as you did for Node\_1 and Node\_2, configure this node to be headless and adjust its window size to be the minimum required to contain both viewports.

1.  Instead of using 7680x2160, set the **Window Size** to 6336x1408.
    
2.  Enable **Headless Rendering**.
    

[![The modified Node_3 settings.](https://dev.epicgames.com/community/api/documentation/image/d5fbe83c-21a5-4f1f-9360-c3bdd005d975?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/d5fbe83c-21a5-4f1f-9360-c3bdd005d975?resizing_type=fit)

The modified Node\_3 settings.

[![The Node_3 stream showing in the VP_C1 and VP_C2 viewports.](https://dev.epicgames.com/community/api/documentation/image/daf0543e-9903-4777-9d21-d02b7a0f08e0?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/daf0543e-9903-4777-9d21-d02b7a0f08e0?resizing_type=fit)

The Node\_3 stream showing in the VP\_C1 and VP\_C2 viewports.

Next, configure the Node\_3 media output configuration. Again, the settings will be the same as for Node\_1 and Node\_2 except for the stream address, which needs to be unique in the cluster.

1.  Configure the Node\_3 settings to be identical to Node\_1 and Node\_2.
    
2.  Set the Node\_3 **Stream Address** to use 225.1.2.3.
    

With this configuration complete, your cluster now uses 5 multicast groups:

1.  225.1.1.10:50000 : ICVFXCameraA
    
2.  225.1.1.11:50000 : ICVFXCameraB
    
3.  225.1.2.1:50000 : Node\_1
    
4.  225.1.2.2:50000 : Node\_2
    
5.  225.1.2.3:50000 : Node\_3
    

Here’s the final configuration of Node\_3:

[![The Node_3 Media settings for the nDisplay ICVFX camera streaming and synchronous output example.](https://dev.epicgames.com/community/api/documentation/image/5e907378-7437-48ad-a391-f14461e220b9?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/5e907378-7437-48ad-a391-f14461e220b9?resizing_type=fit)

The Node\_3 Media settings for the nDisplay ICVFX camera streaming and synchronous output example.