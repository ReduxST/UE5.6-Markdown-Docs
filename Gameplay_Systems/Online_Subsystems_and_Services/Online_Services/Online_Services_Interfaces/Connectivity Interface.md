# Connectivity Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/connectivity-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/connectivity-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:01

---

The **Online Services** **Connectivity Interface** provides you with tools to determine whether your game is connected to your platform's backend online services.

## API Overview

### Functions

The following table provides a high-level overview of the functions provided by the Connectivity Interface:

| **Function** | **Description** |
| --- | --- |
| [`GetConnectionStatus`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IConnectivity/GetConnectionStatus) | Retrieve the connection status for the provided online service. |
| [`OnConnectionStatusChanged`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IConnectivity/OnConnectionStat-) | The event triggered when an online service connection status changes. |

### Enumerated Classes

Online service connection status is represented by the [`EOnlineServicesConnectionStatus`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/UE__Online__EOnl-) enumerated class.

#### EOnlineServicesConnectionStatus

| **Value** | **Description** |
| --- | --- |
| `Connected` | Connected to the online services. |
| `NotConnected` | Not connected to the online services. |

## Connection Status

`GetConnectionStatus` returns the current connection status for the provided online service. Some online services consist of multiple underlying microservices. Use the name of one of these microservices as a parameter for `GetConnectionStatus` to determine the particular microservice's connection status. If you don't specify an online service parameter, `GetConnectionStatus` returns `EOnlineServicesConnectionStatus::Connected` only if all underlying microservices are connected.

You can bind `OnConnectionStatusChanged` to events to inform you when the connection status of an online service or one of its microservices changes.

The organization of an online service and the accessibility of its particular microservices varies by platform. Consult your platform's online services documentation for more information.

## More Information

### Header File

Consult the `Connectivity.h` header file directly for more information as needed. The Connectivity Interface header file `Connectivity.h` is located in the directory:

```
`Engine\Plugins\Online\OnlineServices\Source\OnlineServicesInterface\Public\Online`
Copy full snippet
```
Engine\\Plugins\\Online\\OnlineServices\\Source\\OnlineServicesInterface\\Public\\Online

For instructions on how to obtain the UE source code, see our documentation on [Downloading Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).

### Function Parameters and Return Types

Refer to the [Functions](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine#functions) section of the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) page for an explanation of function parameters and return types, including how to pass parameters and processing the results when functions return.