# Live Link VRPN

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-vrpn-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-vrpn-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:02

---

**Live Link** supports devices exposed through a [VRPN](https://github.com/vrpn/vrpn/wiki) server that has OpenVR support. VRPN provides an abstraction layer for VR peripherals so that they all appear to have the same data reports. Because of the nature of VRPN, you can have multiple **Live Link Subjects** that map to the same device.

## Getting Started

Follow these steps to set up your devices with **Live Link VRPN**.

1.  Start your VRPN server.
    
    The VRPN server must support OpenVR.
    
2.  Launch **Unreal Engine** and open your project.
    
3.  Enable the following plugins:
    
    1.  **Live Link**
        
    2.  **Live Link VRPN**
        
4.  Restart Unreal Engine.
    
5.  In Unreal Editor's **main menu**, choose **Window > Live Link** to open the **Live Link** window.
    
6.  Click **Add Source** and choose **Live Link VRPN Source**.
    
    ![Select the Live Link VRPN Source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/562a9a6a-f3ac-4842-a6a9-2dc0e05007ca/live-link-vrpn-source.png)
    
    A user-selected Live Link VRPN Source which shows the Connection Settings panel. These are the default settings.
    
7.  In the **Connection Settings** window:
    
    1.  Set **IPAddress** to the IP address and port number of the VRPN server. In this example, the VRPN server is running on the local computer using port 3884, so the text value is 127.0.0.1:3884.
        
    2.  Set **Local Update Rate in Hz** for the frequency to poll the VRPN server. The default is 120, and the max is 1000.
        
    3.  Set **Device Name** to the identifier used by the VRPN server for your device. It is better to use the serial number than the generic device identifier because the serial number won't change.
        
        In this example, the VRPN server uses the identifier openvr/controller/1GNGH850VE0304\_Controller\_Left for the left VR controller.
        
    4.  Set **Subject Name** to a friendly name. This will be the **Live Link Subject Name**. In this example, the subject name is LeftController\_VRPNTracker.
        
    5.  Set **Type** to one of the following:
        
        -   **Tracker**: Returns the position and orientation of the device as an Unreal Transform.
        -   **Analog:** Returns one or more analog axes in the 0 - 1 range, such as joystick or sliders from the device.
        -   **Dial**: Returns a float to represent the rotation, such as a dial from the device.
        -   **Button**: Returns an array of floats with 0 or 1 values.
    6.  Click **Add**.
        
        ![Adding the connection settings to the VRPN source](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9463df7-e0d4-495c-af45-1cef2991ba1c/add-connection-settings.png)
8.  A Live Link Subject with the given name appears under a **VRPN** section when the first data is received. In this example, the subject name is LeftController\_VRPNTracker.
    
    ![Live Link Subject in the VRPN section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4caaa76a-9472-4c2a-8fc0-9ab6dc444dc5/live-link-subject.png)
    
    If your Live Link VRPN Subject doesn't appear, refer to the [Troubleshooting](/documentation/en-us/unreal-engine/live-link-vrpn-in-unreal-engine#troubleshooting) section below for tips on how to make sure you're receiving data.
    
9.  **For Tracker type:** Select an **Actor** in the level and add a **LiveLinkComponentController** to it. Set **Subject Representation** to the Live Link VRPN Subject. In this example, the subject is LeftController\_VRPNTracker.
    
    ![Ading a Live Link Component Controller](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e59cf3fa-96b8-4396-92b0-f39a724f27b5/live-link-component-controller.png)
    
    **For the other types:** Since the other types are floats, use them in **Blueprints** to modify the scene.
    

## Reorienting Axis Mapping

Since VRPN doesn't enforce a standard axis mapping, Live Link provides controls for reorienting the axis mappings using Live Link preprocessors.

Follow these steps to change the axis mappings in Unreal Engine for your device.

1.  In the **Live Link** window, click on the **Live Link VRPN Subject**.
    
2.  Click **View Options > Show Subject Properties**.
    
3.  Next to **Pre Processors,** click the **Add (+)** button to add a Live Link preprocessor.
    
    ![Adding a Live Link Pre Processor](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df514073-f120-46c2-bcd2-f2b1f0655441/add-preprocessor-element.png)
4.  Set the Pre Processors element to **Transform Axis Switch** and expand the section.
    
    ![Expand the Transform Axis Switch section](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6f458da-1db9-46b2-9b4d-82cf38ce7c94/expand-transform-axis-switch.png)
5.  Change the **Front**, **Right**, and **Up Axes** to match the coordinate system of the device. Each VRPN server may have a different default axis mapping, and each device may have its own axis mapping. Refer to the documentation or configuration file for your VRPN server for details. In this example, the device uses -Z forward, +X right, and +Y up.
    
    ![Setting the axes](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/158a93f0-7f46-48c3-a2df-15558d65fe60/axis-settings.png)
6.  Once the axes are moving as expected, enable and set **Offset Position** or **Offset Rotation** to achieve the right orientation or position in the world, if necessary.
    
    ![Enabling Ofset Position and Offset Rotation](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5ff5e24f-2ced-45a4-9d7c-84369e42d168/enable-offsets.png)

## Troubleshooting

If your Live Link VRPN Subject doesn't appear when you add a Live Link Source, try the following tips to troubleshoot.

-   Make sure the IP address and port specified in Live Link match the VRPN server.
    
-   You can use the [LiveLinkXR](/documentation/en-us/unreal-engine/livelinkxr-in-unreal-engine) plugin on the same server to troubleshoot if the stream of data is correctly sent from VRPN.
    
-   In Live Link, select the Live Link VRPN Subject and click **View Options > Show Frame Data** to see what data Unreal Engine is receiving.
    

![The Show Frame Data View Option](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b1b6d40-5617-4a27-a80a-a98c8737756a/show-frame-data.png)