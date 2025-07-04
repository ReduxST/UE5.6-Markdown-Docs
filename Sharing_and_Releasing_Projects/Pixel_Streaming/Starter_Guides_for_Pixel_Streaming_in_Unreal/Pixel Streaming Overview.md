# Pixel Streaming Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-pixel-streaming-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/overview-of-pixel-streaming-in-unreal-engine)  
**Processed:** 2025-06-14 16:41:05

---

People typically experience your Unreal Engine application on the same device that runs the gameplay logic and renders the game world to the screen, regardless of whether you build for a desktop platform, mobile OS, or console. Multiplayer networked games may distribute parts of the gameplay logic among multiple instances of the application, but each individual instance still does the work of rendering the game world locally for its own player. Even when you use the HTML5 deployment option to create a version of your Project that can run inside a Web browser, the game logic and rendering still happens locally within each user's Web browser.

With Pixel Streaming, however, you run your Unreal Engine application remotely, on a computer that users probably never see. For example, this could be a physical desktop somewhere inside your organization, or a virtual machine provided by a cloud hosting service. Unreal Engine uses the resources available to that computer — CPU, GPU, memory, and so on — to run the game logic and render every frame. It continuously encodes this rendered output into a media stream, which passes through a lightweight stack of Web services. Users can then view that broadcast stream in standard Web browsers running on other computers and mobile devices.

![Rendering in the cloud with Pixel Streaming](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c8de4280-f44a-436a-a4cb-bd2b8f51e2a0/cloud-simplified-1.png "Rendering in the cloud with Pixel Streaming")

The result for the user is just like watching a video stream from a service like YouTube or Netflix, except for two things:

-   Instead of playing back a pre-recorded video clip, the stream is playing back the rendered frames and audio generated by Unreal Engine in real time.
-   Users can control the experience from their browsers, sending keyboard, mouse, and touch events, plus custom events emitted from the player Web page, back to Unreal Engine.

## Benefits

Using the Pixel Streaming system offers several possible benefits:

-   It makes mobile devices and lightweight Web browsers capable of displaying better-quality graphics than otherwise possible. They can show complex scenes at high resolutions, using rendering features that are only possible when rendering in a native desktop application with a powerful GPU.
    
-   The user doesn't need to download large executables or content files in advance, and doesn't need to install anything. The only thing the user needs to download is the media stream as it plays.
    
-   You can support multiple platforms without creating and distributing multiple separate packages. You package your application once for Windows, Linux, or Mac and people can use any platform to experience your content. Users can view the stream in any modern browser that supports the WebRTC connection model, which includes Google Chrome and Mozilla Firefox on desktop, iOS, and Android platforms. (See the [Pixel Streaming Reference](/documentation/en-us/unreal-engine/unreal-engine-pixel-streaming-reference) for details.)
    
-   The Pixel Streaming system contains a minimal number of components that are relatively easy for anyone to set up inside a local network. However, it's powerful enough for teams with experience in deploying web services to use as a basis for creating custom cloud-hosted platforms.
    
-   Pixel Streaming uses the WebRTC peer-to-peer communication framework for the lowest possible latency between the user and the Unreal Engine application.
    

## Architecture

The following image summarizes the components of a simple Pixel Streaming setup:

![Pixel Streaming architecture](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f0cabf11-f2a2-4708-a347-f49264c33a52/cloud-architecture-5.jpg "Pixel Streaming architecture")

### Components

1.  **Pixel Streaming plugin:** This plugin runs inside Unreal Engine. It encodes the final results of every rendered frame using video compression, packs those video frames along with the game audio into a media stream, and sends that stream to one or more connected browsers over direct peer-to-peer connections.
    
2.  **Signalling and Web Server:** The Signalling and Web Server is responsible for negotiating connections between browsers and the Pixel Streaming plugin and for providing browsers with the HTML and JavaScript environment that plays back the media stream.
    

### Connection Process

1.  When you start up all the Pixel Streaming components, the Pixel Streaming plugin running inside Unreal Engine first establishes a connection to the Signalling and Web Server.
    
2.  A client connects to the signaling server, which serves it an HTML page that contains a player widget and control code written in JavaScript.
    
3.  When the user starts the stream, the signaling server negotiates the establishment of a direct connection between the client browser and the Unreal Engine application.
    
    For this connection to work, the browser and the Unreal Engine application need to know each other's IP address. If both are running on the same network, they are typically visible to each other directly at their own IP addresses. However, network address translation (NAT) services running between the two endpoints may change the externally visible IP address of either party. Resolving this usually involves the use of a STUN or TURN server, which tells each component what its externally visible IP address is. For details, see the [Hosting and Networking Guide](/documentation/en-us/unreal-engine/hosting-and-networking-guide-for-pixel-streaming-in-unreal-engine).
    
4.  As soon as the connection between the client and the Unreal Engine application is established, the Pixel Streaming Plugin starts streaming media directly to the browser. Input from the client is sent by the player page's JavaScript environment directly back to the Unreal Engine application.
    
5.  The Signalling and Web Server maintains its connection to the browser and to the Unreal Engine application even after the media stream starts playing, so that it has the ability to handle disconnections initiated by the browser.
    

For step-by-step instructions on setting up the architecture shown above, see [Getting Started](/documentation/en-us/unreal-engine/getting-started-with-pixel-streaming-in-unreal-engine).