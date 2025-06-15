# SMPTE 2110 Media IO Workflows

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/smpte-2110-media-io-workflows-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/smpte-2110-media-io-workflows-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:20

---

This guide provides instructions for: setting up a basic streaming output, and receiving the stream on a local network using SMPTE 2110 with Nvidia Rivermax.

Because Rivermax-SMPTE 2110 video streaming support is built on top of the Media IO framework, you can use it the same way you can already use serial digital interface (SDI) video streaming in and out of the engine.

## Configure the Output Stream

You can make Unreal Engine’s viewport available to the network by multicasting it over a SMPTE 2110 stream, which can be received by another instance of Unreal Engine on another machine.

Once you have configured it, this example stream will be 4k30 (3840 x 2160) using the RGB10 pixel format.

1.  Enable the **NVIDIA Rivermax Media Streaming and Media Framework Utilities** plugin.
    
2.  Open the MediaCapture panel.
    
    -   In the menu, select **Window > Virtual Production > Media Capture**,
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3c153903-4bcd-4722-9b03-bde472173565/image_0.png)
3.  Create a Rivermax Media Output asset.
    
    -   Right-click in the Content Browser, then select **Media > Rivermax Media Output**
4.  Configure the output to multicast on a Rivermax-enabled interface with the desired options.
    
    -   Alignment Mode: Select **Alignment Point** and **Do Continuous Output** to generate an output similar to SDI, meaning:
        
        -   Your output stream will align to specific points in time, like reference genlock signals.
            
        -   Your output stream will always output a frame at the desired frame rate even if no new frame is available.
            
    -   Frame locking: Use **Block on Reservation** to avoid dropping frames. This also makes the engine run at the presentation rate, 30fps.
        
    -   Settings: Adjust your settings to correspond to the desired stream configuration, based on your local network.
        
        -   The network interface used will be the first one matching `*.*.*.107`.
            
        -   The multicast group is `225.1.1.1 on port 60000`.
            
5.  Select your newly configured asset in the Media Capture panel and start capturing.
    
    ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b2eb107f-d412-4642-95e3-747b4f00e8c9/image_1.png)
    
    Select your Rivermax Media Output asset by name in the Media Capture panel.
    

Your viewport is now available for any 2110 compatible device on the local network. You can confirm network bandwidth usage by your stream using the Windows Task Manager Performance tab.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93893cc3-e8da-41b4-af0b-55ddc696f190/image_2.png)

Network bandwidth usage in the Windows Task Manager for your stream source.

If you don’t see any activity in Task Manager, make sure that **View > Update Speed** is not set to **Paused**.

## Configure to Receive the Stream

You can use a Rivermax Media Source to receive 2110 streams from other instances of Unreal Engine as well as from other external sources. You can configure Unreal Engine on another machine on your network to receive the stream on any interface matching `*.*.*.108`.

1.  Create a Rivermax Media Source asset.
    
    -   Right-click in Content Browser, and select **Media > Rivermax Media Source**.
2.  Configure your media source for the stream you want to receive.
    
    -   **Player Mode:** Use Latest mode as there is no synchronization between your instances.
        
    -   Resolution will be auto detected from the stream.
        
    -   Match the other settings to the configuration of your output stream.
        
        ![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/36a2d7b5-427b-437e-899d-bee2cccf8393/image_3.png)
        
        The settings for the Rivermax Media Source asset.
        

Once configured, you can directly preview the stream in the asset editor by clicking **Open** in the menu bar at the top.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cbbe0f29-baf3-4f88-af81-fda77db08ae3/image_4.png)

Your stream output, shown in the asset editor of the receiving instance of Unreal Engine.

You can confirm stream bandwidth using the Task Manager and performance tab, and see what your network interface is receiving:

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/cf6f7974-b8e8-4873-a578-2f0ac899e764/image_5.png)

Network bandwidth usage in the Windows Task Manager for your stream receiver.