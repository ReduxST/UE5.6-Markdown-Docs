# Pixel Streaming 2 Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/pixel-streaming-2-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/pixel-streaming-2-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:11

---

## Why Pixel Streaming 2?

From UE 5.5 onwards, we introduced a layer that makes it easier for Epic to maintain WebRTC internally since it is used in many parts of the engine and its peripherals. As the original Pixel Streaming plugin used WebRTC directly, the transition to use this new layer meant many parts of the plugin had to be adapted or rewritten.

We have decided to introduce a new plugin to provide a better transition phase for developers who have developed custom solutions on top of the PixelStreaming plugin. For now, both the original Pixel Streaming plugin and the Pixel Streaming 2 plugin will be shipped with Unreal Engine to give users time to migrate.

## Who is Impacted?

All users moving from Pixel Streaming plugin to the new Pixel Streaming 2 plugin should read this migration guide.

## What are the Impacts?

One of our primary goals when creating the new Pixel Streaming 2 plugin was to have minimal impact on the existing Pixel Streaming users.

In pursuit of that goal, we have kept the flow of getting up and running with Pixel Streaming the same, with all the same steps and launch arguments. However, there are a handful of Blueprint nodes, C++ public API, and functionality changes that users migrating to the new plugin should be aware of. The most noticeable change for users of the C++ API is that we removed all the WebRTC types.

## Compatibility

Pixel Streaming 2 is directly compatible with the existing [Pixel Streaming infrastructure](https://github.com/EpicGamesExt/PixelStreamingInfrastructure). We advise using the Pixel Streaming infrastructure branch corresponding to your Unreal Engine version. For the Unreal Engine 5.5 version of Pixel Streaming 2, you should use the UE5.5 branch of the Pixel Streaming Infrastructure.

## What Changed?

The following list includes some of the high-level changes you should be aware of when moving to Pixel Streaming 2:

-   All Blueprint nodes have a Pixel Streaming 2 version. If you are migrating your project, you must manually recreate and relink relevant nodes in your Blueprints. A redirector is not possible when the entire plugin name is changed.
-   We significantly changed the C++ API. Several files and members have been added, removed, or renamed.
-   The Pixel Streaming settings have changed. We added some new options, changed default values for some existing options, and deprecated legacy options.
    -   You can now set the Pixel Streaming settings from `.ini`, console, or command line. The setting priority order is `.ini` is overridden by command line, which is overridden by console.
-   Pixel Streaming Player functionality is included with Pixel Streaming 2, rather than requiring an additional plugin. See the [Setting Up a Pixel Streaming Player](/documentation/en-us/unreal-engine/pixel-streaming-2-overview-in-unreal-engine#settingupapixelstreamingplayer) section below for more information.

For an in-depth look at the low-level changes, including C++ public API, functionality, and flag changes, see the full document on the Pixel Streaming Infrastructure [here](https://github.com/EpicGamesExt/PixelStreamingInfrastructure/tree/master/Docs/pixel-streaming-2-migration-guide.md).

### Setting Up a Pixel Streaming Player

The Blueprint implementation for setting up a PixelStreamingPlayer component has changed significantly. The following steps outline an example implementation where the peer subscribes to the first streamer available:

1.  Enable the **Pixel Streaming 2** plugin.
2.  Create a new **Blueprint Class (Actor)**.
3.  Open the **Actor** and add the **Pixel Streaming Peer** component.
4.  Drag the **Pixel Streaming Peer** component into the **Event Graph**.
5.  Drag off the **Pixel Streaming Peer** node into empty space and create a **Connect** node.
6.  Connect the **BeginPlay** node's **Exec** output pin to the **Connect** node's **Exec** input pin.
7.  On the **Connect** node:
    1.  Connect the input **Exec** pin to **BeginPlay's** output **Exec** pin.
    2.  Enter "ws://localhost:80" into the **Url** value.
8.  In the **Components** panel, right-click the **Pixel Streaming Peer** component and add the **OnStreamerList** event to the **Event Graph**.
9.  Drag the **Pixel Streaming Peer** component into the **Event Graph** again.
10.  Drag off the new **Pixel Streaming Peer node** into empty space and create a **Subscribe** node.
11.  On the **Subscribe** node, connect the input **Exec** pin to **OnStreamerList's** output **Exec** pin.
12.  On the **OnStreamerList** node, drag off the **Streamer List** output and create a **Get (a ref)** node with index **0**.
13.  Connect the output of the **Get** node to the **Streamer Id** input of **Subscribe**.
14.  In the **Components** panel, select the **Pixel Streaming Peer** component.
15.  In the **Details** panel, set **Properties > Pixel Streaming Video Consumer** to **Pixel Streaming Media Texture**. This prompts you to create and save a new asset.
16.  Drag your **Blueprint Actor** into the level.
17.  Create a **Plane** object and use the transform tools to create a suitable display in your level.
18.  Drag your **Pixel Streaming Media Texture** from the **Content Browser** onto the **Plane** in the level. This automatically creates a Material and applies it to the object.
19.  Start a local Pixel Stream external to this project. Start the Signalling server and run the application with relevant Pixel Streaming arguments.
20.  Play your level. You should now see your external Pixel Stream displayed on the **Plane** in your scene.
    
    Click for full size.