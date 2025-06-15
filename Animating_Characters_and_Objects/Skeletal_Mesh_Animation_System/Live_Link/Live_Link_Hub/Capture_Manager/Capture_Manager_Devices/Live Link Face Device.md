# Live Link Face Device

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-face-device](https://dev.epicgames.com/documentation/en-us/unreal-engine/live-link-face-device)  
**Processed:** 2025-06-14 16:33:48

---

The **Live Link Face** device enables the ingest of takes directly from a connected iOS device running the [Live Link Face App](https://dev.epicgames.com/documentation/en-us/metahuman/live-link-face-app). When using this device, make sure the LiveLink Face application is running in the foreground (is active).

Although the Live Link Face application is available on Android devices for real time animation in MetaHuman Animator, it does not support capture for offline processing.

[![Device Details Live Link Face](https://dev.epicgames.com/community/api/documentation/image/edf08bf3-7bc9-4f99-a953-b0194ce711c4?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/edf08bf3-7bc9-4f99-a953-b0194ce711c4?resizing_type=fit)

-   **Display Name**: The name of the device as it will appear in the **Devices** list.
    
-   **Ip Address**: The IP address of the device on the network.
    
-   **Port**: The port of the device on the network.
    
-   **Connect**: Tokens that can be extracted from the folder and file name of the audio file to identify the take.
    

Live Link Hub and the mobile device must be able to connect across the network; make sure your network settings, firewalls, VPNs, and so on are set to allow this connection.

## Capturing Data

It is possible to trigger recording in the Live Link Face app from the Live Link Hub Live Data layout. This will pass **Session**, **Slate**, and **Take** information to the app.

[![Capturing Data](https://dev.epicgames.com/community/api/documentation/image/ef98c442-6304-4a68-9d88-aebc4133aaac?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/ef98c442-6304-4a68-9d88-aebc4133aaac?resizing_type=fit)

This will trigger recording on all connected Live Link Hub devices; it is not possible to trigger a specific device.