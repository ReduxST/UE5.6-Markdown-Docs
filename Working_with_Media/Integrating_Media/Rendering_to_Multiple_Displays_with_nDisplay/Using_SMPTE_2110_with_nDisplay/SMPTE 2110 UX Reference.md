# SMPTE 2110 UX Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/smpte-2110-ux-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/smpte-2110-ux-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:21

---

This page provides a guide to the UX for SMPTE 2110 with NVIDIA Rivermax in Unreal Engine.

## Settings

### Project Settings

You can configure the following settings in your **Project Settings** under **Plugins - NVIDIA Rivermax**.

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/97637b77-4c2f-4f88-8d98-455b9eef1407/image_0.png)

Settings for the NVIDIA Rivermax plugin.

| **Setting** | **Description** |
| --- | --- |
| **Time Source** | 
This setting controls the clock source (timing reference) of the Rivermax library. **PTP:** On Windows, when using a BlueField-2 card, you can configure Rivermax’s clock to be PTP, handled by the DPU on the NIC. **System:** When used, Rivermax will use system time for its clock **Engine:** When used, Rivermax will use Unreal Engine’s time returned by `FPlatformTime::Seconds`.



 |
| **PTP Interface Address** | Only used for PTP Time Source. This is the interface address where PTP is coming from. |

### Assets

The following sections describe asset types for NVIDIA Rivermax, which you can create and access in the Content Browser.

The Media Source Details panel settings are shared for all capture cards, so some of the settings will be nonfunctional. Check carefully what settings are appropriate for your Rivermax capture card.

#### Rivermax Media Source

![Rivermax Media Source settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f1f6befd-4722-433e-904b-4a79cce122d7/image_1.png)

Rivermax Media Source settings.

Use the Rivermax media source settings to configure a stream you want to receive in Unreal Engine. Here’s a description of each setting:

| **Setting** | **Description** |
| --- | --- |
| **Options** |   |
| **Resolution** | 
**If enabled**, the resolution entered will be compared against the incoming video stream. If it doesn’t match, errors will be logged. **If not enabled**, media will automatically adjust to the incoming stream detecting its resolution using RTP headers.



 |
| **Frame Rate** | The frame rate of the video stream. |
| **Pixel Format** | 

The pixel format of the video stream. A subset of the formats supported in the 2110-20 standard are supported in Unreal Engine.

![Supported pixel formats](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/004f358d-dc1f-4610-a19e-d9ca60dd96a8/image_6.png)

When using 10 bit streams, make sure to disable the **Receivers Apply OCIO** feature, otherwise you might encounter issues with clipping.



 |
| **Interface Address** | This is the IP address of the network interface you want to use. That is, the IP address where the video stream will be coming in. Wildcards (`*` and `?`) are supported so the system can reuse configurations from different machines with different interface IPs. |
| **Stream Address** | This is the IP address the stream is read from. This is usually a multicast address to which the sender is broadcasting. |
| **Port** | The port number the stream is sent to. |
| **Video** |   |
| **Deinterlacer** | This property is not supported for Rivermax. Leave it set to **None**. |
| **Interlace Field Order** | This property is not supported for Rivermax. Leave it set to the default setting. |
| **Override Source Encoding** | Only use this property if you are not using OCIO Encoding. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. |
| **Override Source Color Space** | Only use this property if you are not using OCIO Encoding. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. |
| **Video - Color Conversion Settings** |   |
| **Configuration Source** | Use this property to define your OCIO configuration. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. |
| **Transform Source** | Use this property to define your OCIO transform source. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. |
| **Transform Destination** | Use this property to define your OCIO transform destination. See the [OCIO documentation](/documentation/en-us/unreal-engine/color-management-with-opencolorio-in-unreal-engine) for more information. |
| **Video - Advanced** |   |
| **Use GPU Direct** | When enabled and if supported, sample memory will go directly from the network card memory to GPU memory, bypassing system memory. Currently globally disabled using a CVAR because of performance problems when receiving more than one stream. |
| **Synchronization** |   |
| **Time Synchronization** | This property must be enabled to use Rivermax. When enabled, media sources rely on ptp/frame time data to synchronize incoming streams. Rivermax synchronizes based on the frame number. |
| **Frame Delay** | Leave at 0. Rivermax always uses the latest frame. |
| **Time Delay** | This property is not supported for Rivermax. It should always be grayed out. |
| **Synchronization - Advanced** |   |
| **Just in Time Rendering** | Enabling this option defers the processing of the media source’s pixels to the last possible point in the current frame pipeline, which provides more time for pixels to arrive from external sources and be rendered in the current frame on the playback device. This is always on by default, and is the only type of rendering Rivermax media support. |
| **Framelock** | Enable to ensure the frame number of the sender to match the frame number of the receiver. For the Rivermax source and output to match, this property must be enabled, but see below about using [third-party media sources](/documentation/en-us/unreal-engine/smpte-2110-ux-reference-in-unreal-engine#streamingfrommediaservers). |
| **Sample Evaluation Type** | For use with Rivermax, you must set this property to Timecode. |

##### Streaming from Media Servers

Using Rivermax, you can stream media from external sources such as Media Server. When streaming from external sources, you have the option to not use framelocking, and instead have your external media source use timecode-based synchronization. If the external media source encodes a timestamp into RTP headers, then you can disable the **Framelock property**, and select the **Timecode** option for the **Sample Evaluation Type** property. The streamed media will then be synchronized based on the RTP timestamp.

When you stream media from external sources such as Media Server, you can choose to apply color conversion on reception.

-   You can use the Override Source Encoding and Override Source Color Space properties if you aren't using OCIO.
-   You can apply OCIO color conversion which overrides the above settings.

#### Rivermax Media Output

![Rivermax Media Output settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/08c9a2f1-934e-4496-8e3c-aa187390346b/image_2.png)

Rivermax Media Output settings.

| **Setting** | **Description** |
| --- | --- |
| **Output** |   |
| **Alignment Mode** | 
Controls the timing of the output frame scheduling. The options are:

-   **Alignment Point:** In this mode, you use Rivermax time to schedule the timing of the output frames (‘alignment’ point) based on ST2059. Each frame will be scheduled to be sent on these alignment points.
-   **Frame Creation:** In this mode, the scheduler will start scheduling each frame when one has been created. Then, at the specified frame interval it will activate to send another one. If none is available, it will wait for the next one and send it out right away. This is useful for ICVFX streaming in nDisplay to reduce latency when sending Inner Frustum render to other nodes.



 |
| **Do Continuous Output** | Only supported when the **Alignment Mode** is using the **Alignment Point** method. Use this option to constantly output a frame on each alignment point even if no frame is available to send. In that case, the previous frame is repeated. If this option is disabled and no frame is available at a given alignment point, it is skipped and the scheduler tries again at the next alignment point. |
| **Frame Locking Mode** | 

Only supported when the **Alignment Mode** is using the **Alignment Point** method. Options control what happens when a frame is captured:

-   **Free Run:** If there is no space in the presentation queue, it is dropped.
-   **Block on Reservation:** If there is no space in the presentation queue, the RHI thread is blocked until there is space in the queue. If the engine is running faster than the configured output stream (60fps vs 24fps for example), the engine is locked to the presentation frame rate.



 |
| **Presentation Queue Size** | Size of the queue of frames to be sent out. The bigger the number, the more latency you will have between the frame being sent and the frame being rendered. This defaults to double buffering but you can increase it to tolerate bigger hitches. |
| **Do Frame Counter Timestamping** | Only applicable when **Alignment Mode** is using the **Frame Creation** method. It converts the engine’s frame number generated when a frame was created, and uses that as the timestamp for this sample. Use it in conjunction with the Framelock player mode of RivermaxMediaSource in a UE-UE setup, mainly for nDisplay. |
| **Advanced** |   |
| **Number of Texture Buffers** | Base MediaCapture settings controlling textures pre-allocated by MediaCapture. |
| **Settings** |   |
| **Resolution** | 

If **enabled**, the captured texture size will be validated against the desired output resolution. If it doesn’t match, it will error out. If **disabled**, output stream resolution will be configured based on the incoming captured texture automatically.



 |
| **Frame Rate** | The frame rate of the video stream. |
| **Pixel Format** | 

The pixel format of the video stream. A subset of the formats supported in the 2110-20 standard are supported in Unreal Engine.

![Supported pixel formats](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/004f358d-dc1f-4610-a19e-d9ca60dd96a8/image_6.png)

When using 10 bit streams, make sure to disable the **Receivers Apply OCIO** feature, otherwise you might encounter issues with clipping.



 |
| **Interface Address** | This is the IP address of the network interface you want to use. That is, the IP address where the video stream will come from. Wildcards (`*` and `?`) are supported so the system can reuse configurations from different machines with different interface IPs. |
| **Stream Address** | This is the IP address the stream is sent to. This is usually a multicast address where it will be broadcasted to. To really differentiate multicast groups, the address should be made different, not only the port. |
| **Port** | The port number the stream is sent on. |
| **Video** |   |
| **Use GPUDirect** | When enabled and if supported, sample memory will go directly from GPU memory to the network card memory, bypassing system memory. |

#### Rivermax Custom Timestep

You can configure the Engine’s custom timestep from a MediaProfile or from the project settings, and you can now use Rivermax.

![Rivermax Custom Timestep settings.](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4aac0e95-8026-4941-86f6-c3fe0f2a2814/image_3.png)

Rivermax Custom Timestep settings.

The custom timestep uses the same alignment method as the Rivermax output when using the Alignment Point method. This means that you can genlock the Engine for a specific frame rate and align it based on the ST2059 alignment point formulas.

The custom timestep requires the PTP clock, because it uses the Time Source settings configured in Rivermax’s project settings, and it is aligned with standard genlock signals that might be used by other devices.