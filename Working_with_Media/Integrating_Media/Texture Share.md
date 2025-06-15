# Texture Share

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-share-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/texture-share-in-unreal-engine)  
**Processed:** 2025-06-14 16:54:10

---

**Texture Share** efficiently sends and receives GPU data between processes by bypassing the CPU and its expensive memory-copy operation by keeping the data stored in GPU memory.

Examples of shared data include GPU textures, projection and camera matrices, and depth buffers. Texture Share supports synchronization mechanisms and thread barriers to ensure coherency between applications.

Texture Share can be integrated into your project through the following methods:

-   C++ SDK integrated with DirectX11 and DirectX12
    
-   Blueprints
    
-   Support for nDisplay
    

![Unreal sending its viewport to an external application to render as a texture on a rotating cube](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8d9f070-f75a-4f68-bd81-9956e474ea71/unreal_sharing_viewport.gif)

Example of Unreal Engine sharing the viewport with an external application. The application is using the viewport as a texture on a rotating cube.

## Sample Projects

Sample C++ projects are included with the engine source code in the folder **Engine/Source/Programs/TextureShare/Samples/ThirdParty**. There are examples for how to use both DirectX11 and DirectX12 with Texture Share. See the [Quick Start](/documentation/en-us/unreal-engine/texture-share-quick-start-for-unreal-engine) for details on how to get started with Texture Share.

## Sync Policies

There must be a sender and receiver for each interaction in Texture Share to share the GPU data. When the applications exchange data, the sender and receiver should use mirrored priorities for the send and receive operations.

For example, let Unreal Engine be the sender and a third party DirectX application be the receiver:

-   Unreal Engine would execute Send and then Receive.
    
-   The third party application would execute Receive and then Send.
    

Texture Share provides multiple options to synchronize at various stages of the exchange to control blocking behavior. The three stages are described in the following sections.

### Connection Sync Mode

**Connection Sync Mode** defines the synchronization policy when the client and server connect. The following table describes these policies.

| Option | Description |
| --- | --- |
| Default | 
This mode uses the module's global settings. Default connection sync policies are:

-   **Client:** SyncSession
-   **Server:** None



 |
| None | This mode does not block when the remote process connects to the texture shared mechanism. |
| SyncSession | This mode blocks until the remote process successfully connects and is ready to exchange data. |

### Frame Sync Mode

**Frame Sync Mode** defines the synchronization policy for generated frames. The following table describes these policies.

| Option | Description |
| --- | --- |
| Default | 
This mode uses the module's global settings. Default frame sync policies are:

-   **Client:** FrameSync
-   **Server:** FrameSync



 |
| None | This mode does not sync frames with the remote process and can skip frames. |
| FrameSync | This mode ensures both applications exchange frames without skipping. This mode guarantees frame indices are consistent between processes. |

### Texture Sync Mode

**Texture Sync Mode** defines the order of operations for reading and writing data when the texture sharing connection mechanism is established. The following table describes these policies.

| Option | Description |
| --- | --- |
| Default | 
This mode uses module global settings. Default texture sync policies are:

-   **Client:** SyncRead
-   **Server:** SyncRead



 |
| None | This mode skips pairing textures and does not block on the write operation from the remote process before reading. |
| SyncRead | This mode skips pairing textures but blocks waiting for the write operation to end in the remote process before reading. |
| SyncPairingRead | This mode blocks during texture pairing and blocks waiting for the write operation to end in the remote process before reading. |

## Using Texture Share with nDisplay

nDisplay supports Texture Share for sharing a viewport and displaying received textures on it. You can access the shared viewport texture from the viewport's **id**.

To display textures received from another application on an nDisplay viewport, use nDisplay's post processing to define the texture share item and assign it to an nDisplay window.

See the [nDisplay Configuration File Reference](/documentation/en-us/unreal-engine/ndisplay-configuration-file-reference-for-unreal-engine) for further details on sharing and receiving textures in nDisplay.

## Known Limitations

Texture Share is currently in beta. The following are known limitations of the feature.

-   Texture Share SDK currently only supports DirectX11 and DirectX12.
    
-   Maximum length of the Texture Share item name is 128 characters.
    
-   Maximum Texture Share items allowed per process is 100.
    
-   Maximum textures per Texture Share item is 10.
    

A Texture Share item is a container that has a pointer to the DirectX texture and auxiliary buffers such as projection, camera, and rotation matrices.