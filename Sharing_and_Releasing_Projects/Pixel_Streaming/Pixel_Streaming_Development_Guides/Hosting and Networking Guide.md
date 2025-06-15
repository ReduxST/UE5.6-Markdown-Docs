# Hosting and Networking Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine)  
**Processed:** 2025-06-14 16:28:29

---

Even without prior experience developing or deploying web services, you should be able to get the Pixel Streaming setup described in the [Overview](/documentation/en-us/unreal-engine/overview-of-pixel-streaming-in-unreal-engine) and [Quickstart Guide](/documentation/en-us/unreal-engine/getting-started-with-pixel-streaming-in-unreal-engine) pages to work within a simple local area network. However, if you try to deploy your service over more complex networks or over the open Internet, or if you want to redesign the user experience and connection flow, you might need to rethink your setup.

The signalling server, web server, and matchmaker server that accompany Pixel Streaming are a reference implementation only. We do not view them as being a complete solution for all cases, rather, we encourage you to modify them for your own purposes. To this end, we provide the signalling server, web server, and matchmaker in the newly made [Pixel Streaming Infrastructure(external website)](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/) so they can be freely distributed as per the Unreal Engine [EULA](https://www.unrealengine.com/en-US/eula/publishing) (see Distribution and sublicensing of Examples).

For more information regarding the Pixel Streaming front end and web servers, please refer to the [Pixel Streaming Infrastructure](https://github.com/EpicGamesExt/PixelStreamingInfrastructure) page.

## STUN and TURN Servers

In order for the Signaling and Web Server to be able to negotiate a direct connection between the Unreal Engine application and the browser, each party needs to send the other its own IP address. The browser needs to be able to access the IP address sent by the UE5 application, and vice-versa.

Within a simple local area network, each endpoint can usually assume that the other party can access it using the private IP address known to its own network card. Over the open Internet, across subnets, or when network address translation (NAT) services intervene between the browser and the UE5 application, this is not usually the case. Instead, each party needs to find out its own publicly visible IP address by querying a server that implements the STUN (Session Traversal Utilities for NAT) protocol. After the STUN server tells each endpoint its publicly visible IP address, the Signaling and Web Server can continue brokering their direct connection.

![Pixel Streaming with STUN and TURN servers](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6a044148-2c21-46ab-b3c7-60e7a1163203/cloud-stun-turn-5.png "Pixel Streaming with STUN and TURN servers")

Alternatively, you can use a TURN server to relay the media stream between the UE5 application and the browser. With the TURN protocol, the TURN server connects to both the UE5 application and to the browser. The UE5 application sends all of its streamed data to the TURN server, which forwards the data on to the browser. In this case, there is no direct connection between the UE5 application and the browser. If you need to support mobile devices over wireless carrier networks or clients on secured enterprise networks, you may have no choice but to use a TURN server. Mobile and enterprise networks often prevent clients from successfully connecting using the WebRTC protocol.

The STUN and TURN protocols together, along with the ability to fall back from one server to another, make up the ICE (Interactive Connectivity Establishment) framework.

You can find several [open-source implementations](https://github.com/coturn/coturn) of STUN and TURN servers on the Internet. There are even [public STUN servers](https://gist.github.com/mondain/b0ec1cf5f60ae726202e) that you can use for free instead of hosting your own, although you should exercise caution when using a service that you are not hosting yourself. Because of the throughput and bandwidth involved in relaying media through the TURN protocol, public TURN services are rarely available for free.

For convenience, the `SignallingWebServer/platform_scripts/` folder contains scripts to run **CoTURN** on Windows, Linux, and Mac. CoTURN is a free and open source STUN / TURN server that is production ready. We have removed the STUN and TURN reference servers we shipped in the past as these were not production-grade.

To set up Pixel Streaming to use ICE connections, you need to set the host names of the STUN and TURN servers you want to use in the **peerConnectionOptions** configuration parameter for the Signaling and Web Server. For details on how to format this parameter, and how to supply it, see the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference#signallingserverconfigurationparameters).

In addition, if you're hosting your own STUN or TURN server, you must make sure that the IP address and port you specify for it in the **peerConnectionOptions** parameter are visible on the open Internet.

## Multiple Player Endpoints

You may want all users to be in the same Unreal Engine session, but not have exactly the same ability to control that session.

For example, you might want to create an experience like a presentation, where the presenter has full control over the Unreal Engine from their browser, but other users are only able to view the stream. Or, you may want to create customized sets of controls for different users, so that they can cooperate to control different aspects of the experience in real time.

For these kinds of scenarios, you can have one Unreal Engine instance running with one stack of web services, but create different player HTML pages on the Signaling and Web Server:

![Multiple player pages](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d70243d6-fbdc-482d-8c08-e3b56b0089c4/cloud-multi-player-5.png "Multiple player pages")

In this scenario, you could customize each different HTML player page and its JavaScript environment to expose only the controls you want. Then, each class of users would need to request a different URL from the Signaling and Web Server. For example, maybe the presenter loads `http://yourhostname/presenter.html` and other users load `http://yourhostname/attendee.html`.

For more details on how to customize the player page, see [Customizing the Player Web Page](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference).

## Multiple Full Stacks with Matchmaking

The Matchmaker is being deprecated from Unreal Engine 5.5 onward. For users who require the matchmaker, you can use previous versions of the Pixel Streaming infrastructure; however, we advise you to develop your own solutions going forward as the feature is now unsupported and may cease to function at some point in the future.

Instead of having all users connect to the same stream, you may want each person to end up in their own interactive experiences. To do this, you can run a separate stack of Pixel Streaming components for each user, and direct each user to a separate Signaling and Web Server to start a connection.

You can set up each stack of Pixel Streaming components on a separate host, or you can put more than one stack on the same host as long as you configure the port settings for the components within each stack so that they all communicate over different ports. See the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference) for details on these port settings.

If you plan to run multiple instances of the Unreal Engine using Pixel Streaming on the same computer, remember many consumer-level graphics cards such as the NVIDIA GeForce line can only run a maximum of eight encoders at the same time (as of 2024). Professional-grade cards such as the Quadro and Tesla do not have the same limitation.

To help set up this kind of configuration, the Pixel Streaming system can use a matchmaker server that tracks which Signaling and Web Servers are available, and whether they are being used by a client connection.

![Multiple full stacks with a Matchmaker Server](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/df1de745-99ea-45eb-b1a0-e655a39d3ef1/cloud-multi-server-5.png "Multiple full stacks with a Matchmaker Server")

Instead of each client needing to connect to its own Signaling and Web Server URL, they first connect to the Matchmaker Server. The Matchmaker takes care of redirecting each requester to its own Signaling and Web Server, which sets up the peer-to-peer connection between the client and its UE5 application. As long as that connection is active, the Matchmaker Server will not redirect any new incoming browser connections to the same Signaling and Web Server.

The Pixel Streaming system includes a reference implementation for a Matchmaker Server, under the `PixelStreamingInfrastructure/Matchmaker/` folder. You can use this server as-is; or, you can customize the `matchmaker.js` file to fit your needs, as long as you handle the same messages from the Signaling and Web Server.

To set up the Matchmaker Server:

1.  Before you start your Signalling and Web Server, start the Matchmaker Server by running its `run.bat` file. By default, the server listens for HTTP connections from clients on port **90**, and it listens for connections from Signalling and Web Servers on port **9999**. You can override those settings by providing the following configuration parameters on the command line:
    
    | Parameter | Description |
    | --- | --- |
    | **\--HttpPort** | Defines the port the Matchmaker Server listens to for incoming HTTP connections from browsers. |
    | **\--MatchmakerPort** | Defines the port the Matchmaker Server listens to for incoming status messages from Signaling and Web Servers. |
    
    For example:
    
    \\> node cirrus --HttpPort 88 --MatchmakerPort 9988
    
2.  Set the following configuration parameters for the Signalling and Web Server:
    
    | Parameter | Description |
    | --- | --- |
    | **\--UseMatchmaker** | Set this parameter to `true` to make the Signalling Web Server send its current status to the Matchmaker Server. |
    | **\--MatchmakerAddress** | The IP address of the Matchmaker Server this Signalling and Web Server will connect to. |
    | **\--MatchmakerPort** | The port this Signalling and Web Server will use when it needs to send messages to the Matchmaker Server. Make sure this value matches the **\--MatchmakerPort** value you set for the Matchmaker Server. |
    | **\--PublicIp** | The publicly visible IP address of the Signalling and Web Server. When the Matchmaker Server redirects a user to this Signalling and Web Server, it sends them to this IP address. Therefore, it has to be visible to the connecting browser. |
    | **\--HttpPort** | The port that the Signalling and Web Server listens to for HTTP connections. When the Matchmaker Server redirects a user to this Signalling and Web Server, it sends them to this port. |
    
    For instructions on how you can set these parameters, see the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference).
    

## Scaling on Demand

If you want to use a strategy like the one described above, where a separate full stack serves each incoming client connection, you might not want to have a preset number of Unreal Engine applications running. If you have fewer users than servers, you'll be wasting resources; conversely, if you have fewer servers than users, people may need to wait until a connection is free. Instead, you might want to spin up a new server instance each time a client tries to connect.

With the components of the Pixel Streaming system and the optional Matchmaker Server, you should have all the pieces you need to set up a dynamically-scaling hosting system like this. However, for now, this level of cloud deployment is up to you to set up on your own cloud service provider.

## What is the SFU?

A Selective Forwarding Unit (SFU) is a server which intelligently routes media streams between participants.In Pixel Streaming the role of the SFU is to receive stream data from the Unreal Engine application and deliver it to the recipients peers (typically connected web browsers), optionally subsetting the data to adapt to the prevailing network conditions of each recipient peer.

When using the SFU Pixel Streaming implements the simulcast strategy for adapting stream bandwidth. In the simulcast strategy, the Unreal Instance generates multiple streams at different resolutions. The SFU then selects which quality variant of the stream to transmit to the recipient based on the recipient's network conditions.

At this time the SFU feature of Pixel Streaming is experimental.

![SFUSetup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/694c8555-19bd-4842-97d9-d68be0aee528/sfusetup.png "SFU UE Setup")

## When to Use an SFU

An SFU enables a one-to-many stream where there can be more peers connected than would be typically available if all the peers were connected to the Pixel Streaming application in a peer-to-peer fashion. The use of an SFU is often appropriate when your Pixel Streaming application requires multiple connected recipients and those recipients are in varying network conditions that call for different quality stream quality levels (for example, lower bitrates, resolutions, or framerates).

## SFU Configuration

Configuration of the SFU can be achieved by modifying the `config.js` file found in `PixelStreamingInfrastructure/SFU/`.

The SFU is configured by default to provide three quality levels: one full, one half, and one quarter resolution streams. This configuration can be changed using `-SimulcastParameters=` (See the Pixel Streaming reference for details).

If you create more than eight simulcast streams you may hit up against limits when using the H.264 hardware encoders on consumer GPUs that often have a limit of eight encoding sessions. In Pixel Streaming 2, any streams beyond the 8th will automatically switch to software encoders. This is unique to Nvidia hardware.

## Host Machine Hardware Capabilities

If you choose to use a service provider such as Amazon (AWS) or Microsoft Azure to host your Unreal Engine application and Pixel Streaming web services, you may have a choice between multiple different tiers of hosts with different hardware capabilities. Keep in mind that the capabilities of the host may affect the quality of the stream that you can offer.

For example, if you opt for hosts with less powerful GPUs or less memory, you may not be able to get the maximum video quality possible in your streams.