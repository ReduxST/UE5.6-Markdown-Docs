# Networking Requirements for the Collab Viewer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/networking-requirements-for-the-collab-viewer-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/networking-requirements-for-the-collab-viewer-in-unreal-engine)  
**Processed:** 2025-06-14 16:38:38

---

This page describes some of the network requirements and considerations involved in getting multiple computers to connect together into the same runtime design review session using the Collab Viewer Template.

## Connecting over a Local Area Network

The instructions in the [Quick Start](/documentation/en-us/unreal-engine/collab-viewer-template-quick-start-in-unreal-engine) page show how to connect multiple computers that are running within a simple local area network. You should have no problems connecting in this scenario as long as:

1.  All computers are connected to the same network.
2.  All computers have the standard Unreal Engine networking port **7777** open for communication within that network.
3.  No intermediate network components, such as routers or network address traversal (NAT) services, are set up to block the connection.

If you have problems connecting, please contact your network administrator.

## Connecting Across Networks

If you need to have computers join a session across multiple sub-nets or over the open Internet, you will almost certainly need to do some extra network configuration. The exact steps you'll need to follow depend on your network configuration. However, in general:

-   Your server host needs to be visible to all clients from a specific IP address. This may involve setting up NAT traversal rules on your router and opening your firewall to external communications on port 7777.
-   Do not expect automatic server detection to work outside of the same network. Clients will need to manually specify the IP address of the server they want to connect to.

To avoid latency and lags, the Collab Viewer is best used locally within the same network.

## Bandwidth Requirements

Because the Collab Viewer Template only replicates lightweight data across the network, such as the 3D transforms of the users in the session and their laser pointers, network bandwidth usage should be relatively low. If you need exact measurements, you can profile how the template performs on your network using the [Network Profiler](/documentation/en-us/unreal-engine/using-the-network-profiler-in-unreal-engine).

## Other Resources

For additional information on how networking works in the Unreal Engine, see the documentation in the [Networking and Multiplayer](/documentation/en-us/unreal-engine/networking-and-multiplayer-in-unreal-engine) section.