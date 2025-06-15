# Changing nDisplay Communication Ports

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/changing-ndisplay-communication-ports-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/changing-ndisplay-communication-ports-in-unreal-engine)  
**Processed:** 2025-06-14 16:12:28

---

## Network Configuration

The **Network** configuration section provides settings that you can use to control timeouts and other settings related to network communication between nDisplay cluster nodes.

To access the Network settings:

1.  Open your nDisplay Config Asset in the [nDisplay 3D Config Editor](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine).
2.  In the **Cluster** panel, select **Cluster** to open its **Details** panel.
3.  In the **Details** panel, edit the **Network** configuration settings.
    
    Click image to expand.
    

### Parameters

| Parameter | Default | Description |
| --- | --- | --- |
| Connect Retries Amount | 300 | When a non-primary cluster node starts up, this setting determines the number of times the node will attempt to connect to the primary PC before it shuts down. |
| Connect Retry Delay | 1000 | When a non-primary cluster node starts up, this setting determines the time interval after each unsuccessful attempt by the node to connect to its primary PC, in milliseconds. |
| Game Start Barrier Timeout | 18000000 | 
Sets a time interval that the Unreal Engine application on the primary node waits for all cluster nodes to be ready before it starts the first frame of the game loop and begins rendering to the main window, in milliseconds.

This gives all your cluster nodes a chance to connect to the primary PC before rendering begins. During this time, the main window will be black. If, at the end of this time interval, any cluster node has not yet successfully connected to the primary PC, all instances in the cluster will shut down.

You may need to raise this value if your cluster takes an unusually long time to initialize.



 |
| Frame Start Barrier Timeout | 30000 | The waiting time for all nodes to be ready to start frame processing on the game thread. |
| Frame End Barrier Timeout | 1800000 | The waiting time for when all nodes finish frame processing on the game thread. |
| Render Sync Barrier Timeout | 1800000 | 

Sets the barrier timeout for the render thread, in milliseconds. This is a barrier timeout to synchronize render threads among cluster nodes. It's used several times within each frame.

In other words, this is used at runtime to detect situations where any node becomes unreachable. If this occurs, the state of the cluster state is determined to be invalid, and all nodes shut themselves down.



 |

The **Connect Retries Amount** and **Connect Retry Delay** settings work together to determine the maximum length of time your cluster nodes will try to connect to the primary node at startup. For example, suppose you have **Connect Retries Amount** set to 10, and **Connect Retry Delay** set to 1000 milliseconds. On startup, each node tries to connect to the primary PC. If that connection fails, it waits 1000 milliseconds to try again. If that attempt also fails, it waits another 1000 milliseconds. After ten successive failures, the cluster node quits automatically. As soon as a cluster node makes the connection to its primary PC, the count stops.

## nDisplay Communication Ports

The nDisplay system communicates between hosts over four TCP/IP ports:

-   41001 for the Cluster Sync
-   41002 for the Render Sync
-   41003 for the JSON Cluster Events
-   41004 for the Binary Cluster Events

You need to make sure you have these ports open on all computers.

If you want to change the port numbers yourself, you can do so in the following locations.

-   **Runtime synchronization ports:** The primary node uses two ports to synchronize data with the other nodes in the cluster. To set these two ports, go to the [Cluster's settings](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine#cluster).
-   **Cluster event ports:** The primary node always uses the same port to exchange cluster events with connected clients. This includes both other nodes in the nDisplay cluster, and any external applications that you write to send and retrieve cluster events. To set this port, go to the [Cluster's settings](/documentation/en-us/unreal-engine/ndisplay-3d-config-editor-in-unreal-engine#cluster).
-   **Switchboard and SwitchboardListener ports:** Switchboard and SwitchboardListener both need to be configured to use the same communication port. You can specify this in the [Switchboard settings](/documentation/en-us/unreal-engine/switchboard-settings-reference-for-unreal-engine). In addition, you'll have to start the SwitchboardListener application on each host yourself, with the port argument. For example: SwitchboardListener.exe -port=2980