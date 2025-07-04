# Supported Video Devices for Mixed Reality Capture

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/supported-video-devices-for-mixed-reality-capture-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/supported-video-devices-for-mixed-reality-capture-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:06

---

We have tested a limited number of video capture devices with the Mixed Reality Capture Framework (MRC). This is not to say that other video capture devices won't work, but below is a list of the devices that we've tested here at Epic Games.

**Webcams**

-   [Logitech C920](https://www.logitech.com/en-us/product/hd-pro-webcam-c920)
-   [Logitech C930e](https://www.logitech.com/en-us/product/c930e-webcam)

**USB Capture Dongles**

-   [Magewell USB Capture HDMI Gen 2](http://www.magewell.com/usb-capture-hdmi)¹

¹ While untested, it is likely that other Magewell USB capture products are just as compatible with MRC, such as their [Plus model](http://www.magewell.com/usb-capture-hdmi-4k-plus) (for 4K), and their SDI capture dongles (for broadcast hardware).

It is possible for advanced users to write a Media Framework plugin to support their own video capture device.