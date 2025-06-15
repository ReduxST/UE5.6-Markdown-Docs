# AndroidFileServer

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/androidfileserver-settings-in-the-unreal-engine-project-settings](https://dev.epicgames.com/documentation/en-us/unreal-engine/androidfileserver-settings-in-the-unreal-engine-project-settings)  
**Processed:** 2025-06-14 16:05:57

---

## AndroidFileServer

### Packaging

| **Setting** | **Description** |
| --- | --- |
| **Use AndroidFileServer** | Enable the AndroidFileServer plugin. |
| **Allow Network Connection** | Allow FileServer connection using the network. |
| **Security Token** | Optional security token required to start FileServer (leave empty to disable). |
| **Include in Shipping** | Embed FileServer in Shipping builds. |
| **Allow External Start in Shipping** | Allow FileServer to be started in Shipping builds with UnrealAndroidFileTool. |
| **Compile AFSProject** | Compile standalone AFS project. |

### Deployment

| **Setting** | **Description** |
| --- | --- |
| **Use Compression** | Enable compression during data transfer. |
| **Log Files** | Log transferred files. |
| **Report Stats** | Report transfer rate statistics. |

### Connection

| **Setting** | **Description** |
| --- | --- |
| **Connection Type** | 
Defines how to connect to the file server. You can choose from the following options:

-   **USB Only**
-   **Network Only**
-   **USB and Network Combined**



 |
| **Use Manual IP Address?** | Defines whether to use manual IP address instead of automatic query from device. Use only for single-device deploys. |
| **Manual IP Address** | IP address of the device to use. |