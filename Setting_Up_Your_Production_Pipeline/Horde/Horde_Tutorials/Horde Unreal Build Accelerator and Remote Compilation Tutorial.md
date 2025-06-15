# Horde Unreal Build Accelerator and Remote Compilation Tutorial

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-unreal-build-accelerator-and-remote-compilation-tutorial-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/horde-unreal-build-accelerator-and-remote-compilation-tutorial-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:25

---

## Introduction

Horde implements a platform for generic remote execution workloads, allowing clients to leverage idle CPU cycles on other machines to accelerate workloads that would otherwise be executed locally. With Horde's remote execution platform, you can issue explicit commands to remote agents sequentially, such as "upload these files", "run this process", "send these files back", and so on.

**Unreal Build Accelerator (UBA)** is a tool included with Horde that implements lightweight virtualization for third-party programs (such as C++ compilers), allowing it to run on a remote machine - requesting information from the initiating machine as required. The remotely executed process behaves as if it's executing on the local machine, seeing the same view of the file system and so on, and files are transferred to and from the remote machine behind the scenes as necessary.

[Unreal Build Tool (UBT)](/documentation/en-us/unreal-engine/unreal-build-tool-in-unreal-engine) can use UBA with Horde to offload build tasks to connected agents, spreading the workload over multiple machines.

UBA only supports Windows in Unreal Engine 5.5. Support for Mac and Linux are planned for a future release.

## Prerequisites

-   Horde Server and one or more Horde Agents (see the [Horde Installation Tutorial](/documentation/en-us/unreal-engine/horde-installation-tutorial-for-unreal-engine)).
-   A workstation with a UE project under development.
-   Network connectivity between your workstation and Horde Agents on port range 7000-7010.
-   The default `Anonymous` authentication method enabled (see below for more details)

## Steps

1.  On the machine initiating the build, ensure your UE project is synced and builds locally.
2.  Configure UnrealBuildTool to use your Horde Server by updating `Engine/Saved/UnrealBuildTool/BuildConfiguration.xml` with the following:
    
    ```xml
         `<?xml version="1.0" encoding="utf-8" ?>      <Configuration xmlns="https://www.unrealengine.com/BuildConfiguration"> 		          <BuildConfiguration> 				              <bAllowUBAExecutor>true</bAllowUBAExecutor>          </BuildConfiguration> 		          <Horde> 				              <Server>http://{{ SERVER_HOST_NAME }}:13340</Server> 		 				              <WindowsPool>Win-UE5</WindowsPool>          </Horde> 		          <UnrealBuildAccelerator> 				              <bLaunchVisualizer>true</bLaunchVisualizer>          </UnrealBuildAccelerator> 		      </Configuration>`
    Copy full snippet
    ```
    <?xml version="1.0" encoding="utf-8" ?> <Configuration xmlns="https://www.unrealengine.com/BuildConfiguration"> <BuildConfiguration> <bAllowUBAExecutor>true</bAllowUBAExecutor> </BuildConfiguration> <Horde> <Server>http://{{ SERVER\_HOST\_NAME }}:13340</Server> <WindowsPool>Win-UE5</WindowsPool> </Horde> <UnrealBuildAccelerator> <bLaunchVisualizer>true</bLaunchVisualizer> </UnrealBuildAccelerator> </Configuration>
    
    Replace `SERVER_HOST_NAME` with the address associated with your Horde server installation.
    
    -   `BuildConfiguration.xml` can be sourced from many locations in the filesystem, depending on your preference, including locations typically under source control. See [Build Configuration](/documentation/en-us/unreal-engine/build-configuration-for-unreal-engine) in the UnrealBuildTool documentation for more details.
3.  Compile your project through your IDE as normal. You should observe log lines such as:
    
    ```
         `[Worker0] Connected to AGENT-1 (10.0.10.172) under lease 65d48fe1eb6ff84c8197a9b0      ...      [17/5759] Compile [x64] Module.CoreUObject.2.cpp [RemoteExecutor: AGENT-1]`
    Copy full snippet
    ```
    \[Worker0\] Connected to AGENT-1 (10.0.10.172) under lease 65d48fe1eb6ff84c8197a9b0 ... \[17/5759\] Compile \[x64\] Module.CoreUObject.2.cpp \[RemoteExecutor: AGENT-1\]
    
    This indicates work is being spread to multiple agents. If you enabled the UBA visualizer, you can also see a graphical overview of how the build progresses over multiple machines.
    
    For debugging and tuning purposes, it can be useful to force remote execution all compile workloads. To do so, enable the following option in your `BuildConfiguration.xml` file or pass `-UBAForceRemote` on the UnrealBuildTool command line:
    
    ```xml
     `<UnrealBuildAccelerator>      <bForceBuildAllRemote>true</bForceBuildAllRemote>  </UnrealBuildAccelerator>`
    Copy full snippet
    ```
    <UnrealBuildAccelerator> <bForceBuildAllRemote>true</bForceBuildAllRemote> </UnrealBuildAccelerator>
    
    It is not recommended to run a Horde Agent on the same machine as the Horde Server for performance reasons.
    
    When using Horde's build automation functionality, be mindful of mixing pools of agents for UBA and pools of agents for build automation. Agents used for build automation typically have higher requirements and are a more scarce resource than compute helpers.
    

## Enabling Authentication

When using the anonymous authentication mode, there's no authentication and every user has full access to perform remote compilation. This is only recommended during a testing phase and you should switch to either `Horde` or `OpenIdConnect` as soon as possible. Once you do that, additional permissions must be granted to the so called compute cluster. By default, a cluster called `default` is already defined.

Horde jobs utilizing remote compilation are automatically granted access via an injected token that's set as an environment variable for each job step (`UE_HORDE_TOKEN`).

Below is an updated global config with a `default` cluster and `AddComputeTasks` granted for letting UBT and UBA schedule remote compilation. To see what claims are available to your users, open `/api/v1/user/claims` as a logged in user.

```
`{   // ...   "plugins": {     // ...     "compute": {       // ...       "clusters": [         {           "id": "default",           "namespaceid": "horde.compute",           "acl": {             "entries": [               {                 "claim": { "type": "http://epicgames.com/ue/horde/user", "value": "jane.smith" },                 "actions": ["AddComputeTasks"]               }             ]           }         }       ]     }   } }`
Copy full snippet
```
{ // ... "plugins": { // ... "compute": { // ... "clusters": \[ { "id": "default", "namespaceid": "horde.compute", "acl": { "entries": \[ { "claim": { "type": "http://epicgames.com/ue/horde/user", "value": "jane.smith" }, "actions": \["AddComputeTasks"\] } \] } } \] } } }