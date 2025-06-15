# TCP Messaging

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/tcp-messaging-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/tcp-messaging-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:53:38

---

## TCP Messaging

### Transport

| **Setting** | **Description** |
| --- | --- |
| **Enable Transport** | Defines whether the TCP transport channel is enabled. |
| **Listen Endpoint** | 
The IP endpoint to listen for incoming connections.

The format is `IP_ADDRESS:PORT_NUMBER`. Leave blank to disable listening.



 |
| **Connect to Endpoints** | 

The IP endpoints to try to establish outgoing connection to.

Use this setting to connect to a remote peer.

The format is `IP_ADDRESS:PORT_NUMBER`.



 |
| **Connection Retry Delay** | 

Delay time between attempts to re-establish outgoing connections that become disconnected or fail to connect.

`0` disables reconnection.



 |