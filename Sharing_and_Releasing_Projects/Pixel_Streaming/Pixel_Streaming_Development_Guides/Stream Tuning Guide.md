# Stream Tuning Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/stream-tuning-guide](https://dev.epicgames.com/documentation/en-us/unreal-engine/stream-tuning-guide)  
**Processed:** 2025-06-14 16:52:44

---

We made the default Pixel Streaming configuration to balance image quality, latency, and resiliency of the stream under the assumption that it will be deployed on the internet and consumed by users in a variety of network conditions. If this assumption matches your use case then you should not need to modify your Pixel Streaming configuration. However, Pixel Streaming is a flexible technology and can be used in many other use cases. This guide intends to inform the reader about how quality, latency, and resiliency are achieved in Pixel Streaming while additionally giving guidance about cases where optimizing for either image quality, latency, or resiliency is more important than a balanced stream.

## WebRTC

The balancing of image quality, latency, and resiliency in Pixel Streaming is largely handled by a technology called WebRTC. WebRTC is widely used in video conferencing and real time streaming, examples include Facebook Messenger, Discord, Amazon Chime, and Google Stadia. WebRTC is designed to facilitate low latency, fault tolerant, multimedia data transmission between multiple participants.

In the case of Pixel Streaming the WebRTC participants are the Unreal Engine application using the Pixel Streaming plugin and some number of WebRTC capable clients, typically web browsers. WebRTC does not have modes or predefined configurations for specific use cases, due to the wide variety of use cases it has. Instead WebRTC will try to balance quality, latency, and resiliency against network conditions and resource constraints.

However, we have exposed a number of parameters in Pixel Streaming that allow users who have specific requirements around image quality, latency, and resiliency to favor one of those.

Note that any prioritization of one of these does impact the other two, it is your decision if these tradeoffs are acceptable in your use case. In the following sections we will give guidance on how to:

1.  [Maintain image quality despite network conditions](/documentation/en-us/unreal-engine/stream-tuning-guide#maintainimagequalitydespitenetworkconditions)
2.  [Achieve the lowest possible latency](/documentation/en-us/unreal-engine/stream-tuning-guide#achievethelowestpossiblelatency)
3.  [Make the stream resilient to poor network conditions](/documentation/en-us/unreal-engine/stream-tuning-guide#makethestreamresilienttopoornetworkconditions)

## Image Quality

The image quality of the video stream is ultimately determined by how much compression is used when the Unreal Engine imagery is encoded before being transmitted by WebRTC. This compression occurs inside the Pixel Streaming application and by default is entirely controlled by WebRTC.

### WebRTC Encoder Bitrate Adaptation

WebRTC will repeatedly determine the available network bandwidth between the Pixel Streaming application and the WebRTC client, calculate a suitable bitrate value, and then update the video stream encoder with that latest bitrate estimate. The video stream encoder will then use that bitrate as an upper bound and will not produce an encoded image that exceeds that bitrate.

This system produces highly compressed images (that is, blocky and pixelated) when network conditions are poor and less compressed images when network conditions are capable of playing a high quality video stream. In other words, this system adapts the compression of the video stream based on network conditions.

### Maintain Image Quality Despite Network Conditions

Due to Pixel Streaming now supporting multiple video codecs (each with different QP ranges), we have changed the older “QP” parameter to a new “Quality” parameter in 5.5. This new parameter will automatically scale to the correct QP range depending on the selected codec, allowing ease of use and easier understanding/control of your stream quality.

Furthermore, the old QP parameter was “lower value = higher quality”. With the new Quality parameter, a higher value = higher quality.

To maintain image quality, use `-PixelStreamingEncoderMinQuality=N` and `-PixelStreamingEncoderMaxQuality=N` (where N is an integer between 1 and 100, inclusive).

We elaborate on the meaning of Quality and the tradeoff using this parameter introduces below.

Ultimately the only factor truly determining the image quality of the video stream is the compression performed by the video stream encoder. The compression of any given frame is measured using a metric called the "quantization parameter" (QP).

In Pixel Streaming the codecs we use have a varying QP range unique to each codec, as show below:

-   H264: 0-51
-   AV1: 0-255
-   VP8: 0-63
-   VP9: 0-63

Larger QP values result in more aggressive quantization, yielding smaller file sizes but potentially lower quality, whilst smaller QP values preserve more detail but increase file size.

By default we do not restrict this QP range, which means the video stream encoder can select an appropriate QP based on the target bitrate that WebRTC has passed it. However, in the case where we have an application that must never produce poor imagery (for example, a luxury product configurator) then we may wish to restrict the QP range that the encoder can use.

The Pixel Streaming Quality parameter will automatically scale each codec's respective QP value to the correct range, relative to the Quality parameter value. For example, setting Quality to 60, will set a QP value of 20 for H264.

If MaxQuality is restricted such that the bitrate produced exceeds network conditions or the -PixelStreamingWebRTCMaxBitrate then the streamed frame rate will be reduced as frames are dropped.

You can control the Pixel Streaming video encoder Quality with a launch argument by using:

-   `-PixelStreamingEncoderMinQuality=`
-   `-PixelStreamingEncoderMaxQuality=`

Typically, MinQuality is the only parameter you will need to change to bound the image quality. The MinQuality suitable for your application requires some experimentation as it depends on how compressible your application visuals are (particularly in the presence of movement). However, in our experience a MinQuality of 60 is acceptable for most users that want to put an upper bound on how much compression they are willing to accept.

Transmitted bitrate and Quality can be tracked using the in-page `settings"/"stats panel` that Pixel Streaming ships with or by using `chrome://webrtc-internals` in Chromium-based browsers or about:webrtc in Firefox.

The following images illustrate the impact that MaxQuality has on image quality and bitrate:

     ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4ef76ee3-aae8-43ce-9c3a-1f4fa9bbaaa2/quality1.jpg) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ab2d2f04-0f35-486d-8f4b-997242b7d99d/quality21.jpg) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec1d4af2-6b75-430b-8769-2eba27785eec/quality41.jpg) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78427385-66be-4e6e-afe2-c221fbd7579f/quality60.jpg) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ceab5771-d266-4bbb-a024-72bc7980c1c6/quality80.jpg) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7a8c0e2-3f6b-4eae-955a-3b849375927c/quality90.jpg)

**MaxQuality impact on image quality and bitrate**

We highlight that the relationship between Quality and bitrate is logarithmic, meaning the change in Quality, for example a change between a Quality of 96 and 95, represents a much larger difference in bitrate than a change in Quality between 61 and 60.

### Latency

Latency in Pixel Streaming is controlled by a combination of factors, some in your control, and some not. While you cannot control the end user's device hardware, the public internet, or the speed of light; there are, however, a number of other factors you can control that impact Pixel Streaming's latency. We highlight these factors in the following section.

#### Achieve the Lowest Possible Latency

To minimize latency you may want to adjust the following factors; however, be aware that some of these adjustments can impact stream quality and resiliency.

| Latency Factors | Guidance |
| --- | --- |
| Selected video encoder. | The VP8 / VP9 software encoders can introduce more latency than the hardware accelerated H.264 encoders. |
| Geographic location of your application. | Host the Pixel Streaming application as geographically close to the target users as possible. This may require hosting in multiple regions. |
| The hardware you use to host your application. | We recommend hardware that supports hardware accelerated H.264 encoding on the GPU. Additionally, we recommend profiling your application on your target CPU to ensure usage is not at 100% as this can stall the WebRTC transmission thread. |
| Maximum bitrate and resolution. | Reducing resolution and maximum bitrate can reduce data transmission and encoding complexity, which makes encoding, packetization, and decoding faster. This latency reduction is usually not worth the tradeoff in quality. |
| Synchronization of audio and video. | If you are willing to accept audio / visual desync then you can improve latency with `-PixelStreamingWebRTCDisableAudioSync` which will transmit audio and video in separate streams. |
| Disable audio. | If you don't need audio, save bandwidth by disabling its transmission with `-PixelStreamingWebRTCDisableReceiveAudio` and `-PixelStreamingWebRTCDisableTransmitAudio`. |
| Disable motion blur or scene complexity. | Disabling motion blur or any effect that increases visual complexity can, in some scenes, significantly decrease encoding complexity, thus resulting in a lower bitrate. |

In general, the biggest latency reductions will come from geographic proximity and the quality of the network between the Pixel Streaming application and the user.

### Resiliency

In this context resiliency is how stable the stream is in the presence of packet loss, network jitter, and data corruption. WebRTC already has a number of internal, dynamically adjusted, mechanisms it uses to manage stream resiliency. For example, WebRTC can increase the size of its "jitter buffer" that it uses to store received packets to compensate for network delays and retransmissions, at the cost of increased latency. While the jitter buffer is not directly controllable, there are other factors we can control during video stream encoding to increase stream resiliency through data redundancy.

#### Make the Stream Resilient to Poor Network Conditions

Video stream resiliency in Pixel Streaming can be increased by adjusting the following:

| Resiliency Factors | Guidance |
| --- | --- |
| Encoder keyframe interval | 
Sending keyframes allows the stream and decoder to recover after heavy data loss. The interval keyframes are sent on can be controlled using `-PixelStreaming.Encoder.KeyframeInterval`.

Keyframes do take more bandwidth than normal frames, so if packet loss is occurring due to network saturation sending more keyframes may not help.



 |
| Encoder intraframe refresh | 

Video stream recovery information can be encoded across multiple frame slices. This information makes the stream more resilient in the presence of data loss; however, this does take more bandwidth for the entire stream and introduces a scanline type artifact when stream recovery occurs.

This option is only available on NVIDIA GPUs at this time, and you can enable it in Pixel Streaming using `-NVENCIntraRefreshPeriodFrames=N` and `-NVENCIntraRefreshCountFrames=M` (where N is how many frames before sending intraframe refresh again and M is how many frames to encode with intraframe refresh data This option is removed in Pixel Streaming 2).



 |

Generally, stream resiliency is mostly impacted by network quality and the amount of data transmitted. Therefore, if it is acceptable for your Pixel Streaming application to trade decreased quality for increased resiliency, then reducing the amount of data transmitted by leaving the Quality range unrestricted or by reducing your application resolution are also viable options.

### Coupled and Decoupled Mode

In Pixel Streaming, coupling refers to the WebRTC and application frame rates being tied to one another. To enable decoupled mode, run your application with `-PixelStreamingDecoupleFramerate`. There are different use cases in which your stream may benefit from being coupled;

#### Coupled Mode

In Coupled mode, Pixel Streaming will attempt to stream frames at whatever rate your UE application is running at. This mode should be preferred in cases where the UE application is hitting consistent and stable frame rates and latency is critical.

#### Decoupled Mode

In Decoupled mode, Pixel Streaming will attempt to stream frames at a fixed rate, e.g. 60 FPS. If your UE application is not able to render at the target frame rate then Pixel Streaming will send duplicate frames. This mode can be used in cases where latency is not as critical but the application is suffering from inconsistent frame rates and this is causing the stream to hitch.

#### Considerations

Although Decoupled mode can offer improvements in the event of inconsistent application FPS, it’s important to note that Decoupled mode will introduce 1-2 frame latency in all use cases, regardless if the frame rate is consistent or not. This means that for most use cases, it’s recommended to stick with Coupled mode.

### Optimizing Your Application for Pixel Streaming

The following are additional suggestions we have to optimize your application for Pixel Streaming:

-   The presence of color banding artifacts can be greatly reduced by adding a post process introducing film grain into your scene, however; bandwidth will be increased.
-   If you can afford extra latency and you are not supporting multiple peers per Pixel Streaming application then you may wish to experiment with the VP8/VP9 software encoders using `-PixelStreamingEncoderCodec=` as they produce better quality encodings for the same bitrate as the H.264 encoders.
-   To achieve many Pixel Streaming applications running on a single GPU (multi-tenancy) your application will have to be profiled heavily or you may have to accept a reduced frame rate/resolution.
-   If you intend to run your application at scale in the cloud, it will be much simpler and cheaper if your Unreal application is built for Linux due to the greater support of Linux by technologies like Kubernetes.

## Achieving Optimum Performance in One-to-One Streams

A one-to-one use case is the simplest and most common form of Pixel Streaming, in which one user connects to one instance of Pixel Streaming. For more details on Pixel Streaming configurations, see the [Hosting and Networking Guide](/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine)

Before discussing the optimum setup for one-to-one streaming, we must define metrics to consider when devising the best Pixel Streaming experience. Of most interest are:

-   Latency (between the user and the streamed experience);
-   Video quality (that the user receives);
-   Stream robustness to varying network conditions (whether we can handle some lost packets and recover quickly).

### Latency

To achieve optimal latency, you should use the following architecture: **direct peer-to-peer** (no SFU or media server), and the Pixel Streaming instance should be as geographically close to the user as possible.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/973b0aa7-bafc-4b49-b42d-17acb39da2bd/latency.jpg)

The diagram above illustrates the optimal Pixel Streaming configuration for low latency. The end user is directly connected to the Pixel Streaming instance over UDP.

### Considerations

-   This requires the UE instance to be reachable over the public internet on UDP.
-   This requires the end user to have a network configuration that allows them to communicate over UDP with an unknown IP address. In WebRTC terms, this requires a STUN server between the two machines so that NAT can be overcome and public IPs exchanged.
-   For users who cannot do this, a TURN (relay) server can be used, but their latency **WILL** be worse than P2P users.
-   This configuration **will not work** in the case where multiple WebRTC peers need to view the same stream at variable qualities (for more details, refer to the documentation about [SFU configurations](/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine#whatisthesfu)).

### Video Quality

In a video-first WebRTC experience, such as Pixel Streaming, video quality is perhaps the most powerful tuning parameter we have for our experience. No one wants a blocky or pixelated experience; however, we also want to offer a consistent and stable experience to a wide range of users on varying networks. To achieve this, we need to consider the following:

-   What is the minimum acceptable resolution of the experience?
-   What is the minimum acceptable bitrate at that resolution?
-   Is visual quality, robustness, or latency more important?

Increasing video quality increases the required bitrate of our experience, making the experience less robust and more susceptible to freezes if packets are lost or increased latency as jitter buffers grow to account for small but critical retransmitted packets.

Therefore, we must carefully consider the minimum video quality that will result in a successful experience. Additionally, once this minimum quality is determined it is important to bound the streaming quality to not exceed this upper limit, except after careful field trials with users.

It’s important to make data-driven decisions based on deploying some experiments to the users and measuring key metrics such as packet loss, jitter buffer delay, and bitrate.

However, in the absence of any data, a starting point may be:

-   A 1080p video stream; ( -ResX=1920, -ResY=1080, -ForceRes, -Renderoffscreen )
-   10 megabit/s maximum encoding quality; ( -PixelStreamingWebRTCMaxBitrate=10000000 );
-   Key frames sent only as needed; ( PixelStreamingEncoderKeyframeInterval=0 )

## Robustness

Video stream robustness can be increased through the following techniques:

-   Reducing the maximum bitrate;
-   Adding redundant information during encoding; ( `-PixelStreamingEncoderIntraRefreshPeriodFrames=300 -PixelStreamingEncoderIntraRefreshCountFrames=5` )
-   Ensuring the negotiated offer/answer contains [Flex-FEC](https://datatracker.ietf.org/doc/html/rfc8627) (e.g., Chrome, Firefox) and is using -PixelStreamingWebRTCEnableFlexFec. However, beware that this will use more bitrate.

You can tune these metrics around how important robustness is for the experience and driven by how often users experience periods of freezes and jitter buffer growth.

## General Speed Recommendations

Although the speed recommendations vary based on how you are tuning the experience, some general guidelines for an H.264 video in a 1080p stream are as follows.

User network connections:

-   **10-20 megabit/s:** Will experience good visual quality;
-   **1.5-10 megabits/s:** On the low end, a user may experience some noticeable changes in visual quality as the network fluctuates (e.g., pixelation during movement that clears up when video is still);
-   **0.5-1.5 megabit/s:** The user will have a pixelated experience;
-   **0-0.5 megabit/s:** Likely unusable.

These depend on the target for video quality, latency, and robustness.

### Factors Contributing to Poor Quality Stream

Several factors can contribute to a poor quality stream. However, some of the most common factors are:

-   Maximum achievable network speed on the user side is too low for the target video quality;
-   The user is in a poor network and experiences intermittent/bursty packet loss;
-   Geographic proximity to the streaming instance (extra latency can make packet loss more likely, which can lead to reductions in stream quality as WebRTC attempts to stabilize the streaming experience by reducing bitrate);
-   The default video quality of the experience is too high for the user’s network connection, and the jitter buffer grows as packets are lost, causing the bitrate to reduce during an initial period of stream adaptation;
-   TURN/relay servers introduce latency and an extra point of packet loss (UDP) or packet retransmission (TCP);
-   Media server/SFU introduces latency and an extra point of packet loss;
-   Misconfigured media server/SFU introduces abstraction around bitrate and control messages that are not passed back to the Pixel Streaming instance. Thus, the streaming source is never updated with feedback needed to adjust the experience to a usable state for the connected peer.

## WebRTC Optimization Triangle

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/24953e9e-a5e4-435e-a574-ea912ab18b2f/balanceddiagram.png)

In some streaming scenarios, the stream settings may need to be optimized to better cater for the desired outcome.

Latency, video quality, and stream robustness are the three parameters of most interest that the stream providers can optimize to adjust the stream to suit their needs. This will require limiting one or sometimes both other parameters, as they are ultimately tied together due to network restrictions.

By default, Pixel Streaming is trying to offer the best balance between these configurations, adjusting to the user’s connection, as shown in the diagram above.

### Optimizing for Low Latency at the Cost of Quality and Robustness

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/63139f43-c4da-451e-8c2d-3b0dc1ba34f6/lowlatencydiagram.png)

In a local streaming case, for example, VCam Pixel Streaming, it might be beneficial to optimize the stream for low latency and trade out robustness and video quality. This can be achieved via these parameters:

```
`-PixelStreamingEncoderTargetBitrate=10000000 -PixelStreamingWebRTCDisableFrameDropper -PixelStreamingWebRTCVideoPacingFactor=100`
Copy full snippet
```
\-PixelStreamingEncoderTargetBitrate=10000000 -PixelStreamingWebRTCDisableFrameDropper -PixelStreamingWebRTCVideoPacingFactor=100

In this example, we are locking the bitrate to target 10 megabit/s despite the network conditions, disabling frame dropping to always send a frame despite congestion, and setting a lenient value in the video pacer to accept this large amount of packets. This allows us to send packets without delay despite network conditions, ensuring minimal latency. This configuration would not be advisable over the internet, where the network speed is more restricted, and dropping frames and pacing packets helps achieve a smooth experience in varying network conditions.

### Optimizing for Quality at the Cost of Latency and Robustness

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7de40a9e-3b20-460f-ac82-9723a529a91f/qualitydiagram.png)

In a different streaming scenario, where the stream provider targets a certain visual fidelity no matter what, for example, for a luxury product configurator, it might be beneficial to optimize for quality and trade out latency and robustness. This can be achieved by using the following configuration:

```
`-PixelStreamingEncoderMinQuality=70`
Copy full snippet
```
\-PixelStreamingEncoderMinQuality=70

This configuration limits the maximum compression the encoder will produce (lower values result in less compressed images), directly translating to a guaranteed minimum video quality. However, if the consumer’s network connection cannot handle this bitrate, they will experience freezing and added latency.