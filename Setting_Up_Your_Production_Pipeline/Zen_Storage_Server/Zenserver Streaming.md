# Zenserver Streaming

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-zenserver-streaming-to-play-on-target-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-use-zenserver-streaming-to-play-on-target-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:37

---

Before taking steps to stream data from the Zen Storage Server (Zenserver), ensure you enabled [Zenserver as Cooked Output Store](/documentation/en-us/unreal-engine/using-zen-storage-server-as-cooked-output-store-for-unreal-engine) per the directions on this page.

The purpose of using Zenserver streaming is to:

-   Allow for much faster staging and deployment.
    
-   Allow for more direct/efficient targeted workflows in the future by allowing us to cook to the same storage that the game loads from without large data transformations having to happen in between.
    

## Understanding Cook/Stage/Deploy

When using Zenserver as cooked output store and staging to container files (`*.pak`, `*.utoc`, `*.ucas`), you can visualize the content pipeline as follows:

The cooked data is written into Zenserver at high granularity by the cook phase, then read from Zenserver and written out into aggregated `.pak`/`.utoc`/`.ucas` files by the stage phase.

This avoids filesystem overheads with high file quantities while still retaining the same behavior for the runtime game on a target device. All of the data ends up as data on the local disk of the target platform, stored mostly in `.pak`/`.utoc`/`.ucas` files.

There is, however, an **opportunity to improve iteration further** by avoiding the data copying that comes from staging all cooked data into `.pak`/`.utoc`/`.ucas` files then copying data further to get those `.pak`/`.utoc`/`.ucas` files onto the target platform.

This is where you can make use of the network capabilities of Zenserver.

## Environment, Security, and Use Case

Before enabling Zenserver streaming, consider the network environment and the security implications of allowing access to Zenserver over the network.

Zenserver is an **unauthenticated** storage server. While authentication might be added in the future, it is currently targeted for use in a trusted environment like an office LAN or VPN, where every user who is able to reach Zenserver is permitted full read/write/delete access to its contents. We do not advise the use of Zenserver with remote access in public (such as the internet) or untrusted network environments, as this could lead to data leaks, data corruption/poisoning, or data loss for DDC, cooked output, or any other data stored within Zenserver.

Zenserver streaming is meant for use:

-   In trusted networks like home or office situations.
    
-   With non-shipping build configurations (debug, development, test).
    
-   When the distance between Zenserver (on your workstation) and the target platform (console or mobile device) is low.
    

For situations that don’t adhere to those use cases, we advise that you keep using the container (`.pak`/`.utoc`/`.ucas`) staging workflow and not use Zenserver streaming.

By default, Zenserver is set up to:

-   Only listen to requests from the local machine, not other machines on the network.
    
-   Only stay running as long as a process on the local machine wants to use it.
    

You need to change both of these details to use Zenserver streaming so that Zenserver is running and can be reached when the game is launched on your target platform (console or mobile). The way to change the default setup is described under [Enabling Zen Streaming](/documentation/en-us/unreal-engine/how-to-use-zenserver-streaming-to-play-on-target-in-unreal-engine#enablingzenstreaming) below.

When using Zenserver streaming, the content pipeline can be visualized as follows:

## Enabling Zenserver Streaming

If you have established that you are on a trusted network (as discussed above under [Environment, Security, and Use Case](/documentation/en-us/unreal-engine/how-to-use-zenserver-streaming-to-play-on-target-in-unreal-engine#environmentsecurityandusecase)), you should change configuration to allow Zenserver to be launched in a way that service requests from other machines on your network are recognized and keep running even if Unreal Editor is no longer running.

Both of these are controlled by means of Unreal Engine’s config, which influences how Zenserver is started up by Unreal Editor or other tools. Put the following into your project's `DefaultEngine.ini`:

DefaultEngine.ini

```
	`[Zen.AutoLaunch]  	LimitProcessLifetime=false  	AllowRemoteNetworkService=true`
Copy full snippet
```
\[Zen.AutoLaunch\] LimitProcessLifetime=false AllowRemoteNetworkService=true

These configuration lines (followed by a restart of your editor) will mean that Zenserver will be launched in a way that allows it to keep running after you close the editor, and continue to service network requests from other machines (such as your target platform).

## Network or USB Link Considerations

When using Zenserver Streaming, it is important that you make the Network or USB link between the workstation and the target platform as optimal as possible. That means:

-   Use a 1 Gbps or 10 Gbps wired ethernet connection when possible.
    
-   Use a USB 3.2 Gen2 (10 Gbps) cable for mobile devices that support USB 3 speeds.
    
-   Avoid the use of a WiFi network connection.
    

The requirements will depend on the details of your title and how heavily it makes use of I/O, so the information above is guidelines, not strict requirements. Internally, we have found 1 Gbps to be adequate in-game, and 10 Gbps to provide faster boot/load times when streaming from Zenserver.

## Staging Without Using Container Files

Once Zenserver is allowed to keep running and serve network requests from other machines, we can make use of it by staging without making use of pak/utoc/ucas files. Staging is the operation in the content pipeline that happens after cooking and before deploying. Staging is done by the Unreal Automation Tool (UAT), and can be manually invoked or invoked by buttons or menu use in-editor. When UAT staging is invoked:

1.  If it was passed the `-pak` argument, it will stage to container (`.pak`/`.utoc`/`.ucas`) files.
    
2.  If it was not passed the `-pak` argument, it will not stage to container (`.pak`/`.utoc`/`.ucas`) files.
    

When using Zenserver as a cooked output store, Zenserver streaming is used specifically when you stage **without** using container files.

## In Unreal Editor

By default, the **Play on Device** functionality built into Unreal Editor is configured to stage without using container (`.pak`/`.utoc`/`.ucas`) files.

You can check or confirm that configuration using the **Edit | Editor Preferences** menu sequence, then selecting the **Level Editor | Play** section. Within that section, you’ll find a **Play on Device** category that has a **Pack Files for Launch** setting:

![Pack Files for Launch setting](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dcd824c5-28b2-434b-a224-677fc82ac989/image_2.png)

To use Zenserver Streaming from the editor, this setting must be set to **Use loose files**. If this is configured correctly, you can use the mechanism described [here to launch on a target platform](/documentation/en-us/unreal-engine/launching-unreal-engine-projects-on-devices).

## In ushell

[ushell](/documentation/en-us/unreal-engine/how-to-use-ushell-for-unreal-engine) is a command line interface for Unreal Engine with brief commands and extensive tab completion. It can be found under `Engine/Extras/ushell`. Quick Start and documentation can be found in the Engine/Extras/ushell/README.txt.

When you have configured Zenserver as cooked output store, ushell’s `.stage` command automatically uses the non-container (or Zenserver streaming) workflow by default.

ushell

```
	`.cook game <platform>  	.stage game <platform>  	.deploy game <platform>  	.run game <platform>`
Copy full snippet
```
.cook game <platform> .stage game <platform> .deploy game <platform> .run game <platform>

If you enabled Zenserver as a cooked output store and want to stage to container files, you must pass a positional argument to the `.stage` command to explicitly request staging to container files.

ushell

```
	`.stage game <platform> development pak`
Copy full snippet
```
.stage game <platform> development pak

The 4th positional parameter of `pak` in the example above can be:

-   `pak`: Staged cook output data will be stored in container (`.pak`/`.utoc`/`.ucas`) files
    
-   `nopak`: Staged cooked output data will be stored as either loose files on the filesystem or in Zenserver if you enable **Zen as cooked output store**.
    
-   `zen`: Staged cook output data will be stored in Zenserver if you enable **Zen as cooked output store**, or emit an error if you did not enable it.
    
-   `auto`: (Default) Staged cook output data will be stored in Zenserver if you enabled **Zen as cooked output store**, or in container files if you did not enable it.
    

## In Your Development Environment / Debugger

Use of Zenserver streaming should be automatic from your development environment or debugger of choice. Upon launch, the game executable will look for the presence of the `ue.projectstore` file. If it is found, the game will attempt to connect to Zenserver to get cooked data.

The `ue.projectstore` file is a simple JSON-formatted file that includes information about hostname, port, and other identifiers that are necessary for the game to connect to Zenserver and start getting cooked data from it.

While the contents of the ue.projectstore file should be appropriate for almost all cases, if you have a need to override the connection parameters, you can pass one or more of these command line arguments to the game runtime to override what is specified in the `ue.projectstore` file:

ue.projectstore

```
	`-ZenStoreHost=<ip_or_hostname>  	-ZenStorePort=<host_port_number>  	-ZenStoreProject=<project_id>  	-ZenStorePlatform=<platform_id>`
Copy full snippet
```
\-ZenStoreHost=<ip\_or\_hostname> -ZenStorePort=<host\_port\_number> -ZenStoreProject=<project\_id> -ZenStorePlatform=<platform\_id>

## Validating that Zenserver Streaming is in Use

When using Zenserver streaming, you should be able to observe that your project’s `Saved/StagedBuilds/<Platform>` folder contains a `ue.projectstore` file and it (and its subfolders) do not contain either `*.uasset` or `*.pak`/`*.utoc`/`*.ucas` files.

Aside from the directory contents, when you have a game runtime (debug or development, not test), you can observe the "ZenServer streaming from …" text in the top left of the screen.

You can also issue the console command:

Console Command

```
	`zen.showgraphs 1`
Copy full snippet
```
zen.showgraphs 1

You’ll see an on-screen plot of the streaming throughput from Zenserver over time.