# nDisplay Multi-User Technical Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-multi-user-technical-reference-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/ndisplay-multi-user-technical-reference-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:15

---

When launching [multi-user editing sessions](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine) using [nDisplay](/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine), **Unreal Engine** automatically creates a local server to host multiple editor users simultaneously.

In the following document you can read about the multi-user server connection logic for launching virtual production projects using **nDisplay** in Unreal Engine.

## Multi-User Connection Logic

When launching a virtual production project using nDisplay for the first time, you can use the [Quick Launch tool](/documentation/en-us/unreal-engine/ndisplay-quick-launch-local-tool-in-unreal-engine) to automatically launch a local server multiple users can connect to.

When launching your project using nDisplay for a second time, Unreal Engine automatically reconnects to the existing local server and reuses the existing multi-user editing session if the editor is already operating in a session. If the editor is not operating in an nDisplay multi-user editing session, Unreal Engine creates a new multi-user editing session on the local server.

You can also build your own custom multi-user server to host an nDisplay multi-user editing session, that multiple users can connect to locally or using a network connection.

When attempting to join a network-based multi-user server, Unreal Engine checks if the editor is already in a multi-user editing session. If the editor is operating in an editing session, Unreal Engine joins the generated multi-user server and session. If the editor is not already operating within an nDisplay multi-user editing session, Unreal Engine closes the local multi-user server, ignores the network-based multi-user server, and launches a new server locally.

You can use the following diagram to better understand the Unreal Engine Multi-User (**MU**) connection behavior:

![flowchart showing a visual diagram of how unreal engine connects to servers and m u editing sessions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/da777fd8-98ba-4683-983c-11bed3be2e66/flowchart.png)

For more information about getting started using multi-user editing sessions, refer to the [Multi-User](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine) documentation.

For more information about launching virtual projects using nDisplay, see the [nDisplay](/documentation/en-us/unreal-engine/ndisplay-overview-for-unreal-engine) documentation.