# Debugging Guide

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-debugging-networked-games-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/testing-and-debugging-networked-games-in-unreal-engine)  
**Processed:** 2025-06-14 16:53:47

---

## Testing Networking Options In Unreal Editor

The **Unreal Editor** contains adjustable settings to help with testing multiplayer projects. These options include setting the **Number Of Players**, running multiple **Play windows**, and running a **Dedicated Server**.

To view these settings, launch the **Editor** and navigate to the **Toolbar**, then select the **Modes** drop-down button adjacent to the **Play** button.

For additional details on adjusting Multiplayer settings in the Editor, see [Testing Multiplayer](/documentation/en-us/unreal-engine/testing-multiplayer-in-unreal-engine)

## Multiplayer Options

### Launching a Dedicated Server

There are other alternatives to launching a multiplayer game. Follow the steps below to launch a separate Dedicated server instance.

1.  You may select **Advanced Settings** from the **Modes** drop-down arrow, or by navigating to **Editor Preferences** > **Level Editor** > **Play > Multiplayer Options**.
2.  From the **Multiplayer Options** section, navigate to the **Launch Separate Server** variable and click the box to enable its boolean to **true**.
3.  Click the drop-down menu adjacent to the **Play Net Mode** variable and select **Play Standalone**.

This will create a new server instance, however, other instances won't automatically connect to it.

### Connecting to Standalone Server instances

You can connect **Standalone instances** to the **Server** by using the command:

```
`open 127.0.0.1:<PORT>`
Copy full snippet
```
open 127.0.0.1:<PORT>

You can also use the [Session interface](/documentation/en-us/unreal-engine/online-subsystem-session-interface-in-unreal-engine). This creates an instance of the game running on a server that other clients can discover and join. This is useful for testing your project's connection flow.

If the **Play Net Mode** variable is set to **Play as Client**, you are not required to enable the **Launch Separate Server** variable, as it is not needed for a dedicated server instance to be launched.

When using **Play as Client** or **Play As Listen Server** in the **Net Mode options** of the editor, these instances are automatically connected directly to each other by IP address. This is the equivalent of running the `open 127.0.0.1:17777` command on a **Client** to connect to the **Server**.

This connection process does not use the **Session Interface**, therefore, the Server will not create an online multiplayer session, and Clients will not search and join this session. For most gameplay testing purposes, this won't make a difference. However, certain online features that rely on the session interface, such as voice chat, will not be available.

If the box adjacent to the **Run Under One Process** variable is enabled, then all Client and Server instances will share the same **tick rate** as the editor.

This is different behavior than running these instances separately. As an example, in **Standalone mode**, you can control the server's tick rate using the NetServerMaxTickRate config value located in the `BaseEngine.ini` file.

```
`[/Script/OnlineSubsystemUtils.IpNetDriver] NetServerMaxTickRate=30`
Copy full snippet
```
\[/Script/OnlineSubsystemUtils.IpNetDriver\] NetServerMaxTickRate=30

This may affect certain behavior which uses tick rate, such as calculating the bandwidth limit for a single net update.

When using **Play-In-Editor (PIE)** there are limitations to features such as [Server/Client traveling](/documentation/en-us/unreal-engine/travelling-in-multiplayer-in-unreal-engine). Your project will need to run in Standalone mode as a separate process outside of the editor to test these features.

If you're running instances under separate processes, one instance will be considered Play-In-Editor and the others will be Standalone. This may lead to varying behaviors when compared to uniformly running all instances as Play-In-Editor. or Standalone. For example, the `UEditorEngine::NetworkRemapPath` function will need to be called in order to add remove or PIE prefixes on static Actors whose paths are sent across the network.

## Debugging Multiple Client and Server Instances

Running multiple Client and Server instances has unique challenges, most especially understanding which instance you're attached to. You can mitigate these challenges by using breakpoints to assist in debugging a PIE instance.

In your code editor, you can add the following variables to your **Watch** window.

| Watch Variable | Use |
| --- | --- |
| `UnrealEditor-Engine!GPlayInEditorContextString` | Determines which instance you're currently stepping through. |
| NetDriver `ServerConnection` | On Clients, this will hold a reference to the `NetConnection` to the server. On the server, this value will be `Null`, allowing you to quickly check which instance you're in when debugging the replication system. |

Additionally, you can check an Actor's [Role](/documentation/en-us/unreal-engine/actor-role-and-remote-role-in-unreal-engine) property by placing a call to the function GetLocalRole() in a watch, or by calling it directly in code. The GetLocalRole function returns how much control the instance has over this Actor. If you're debugging issues within a Replicated Actor, then it will return one of three roles:

| Role | Description |
| --- | --- |
| `ROLE_Authority` | An Actor that exists on the server instance. |
| `ROLE_AutonomousProxy` | An Actor that is a Character or Pawn possessed by a local PlayerController on this client instance. |
| `ROLE_SimulatedProxy` | An Actor that exists on a client instance. |

## Profiling Networked Games

### Networking Insights

You can profile networked games using [Networking Insights](/documentation/en-us/unreal-engine/networking-insights-in-unreal-engine). This is a component of the **Unreal Insights** profiling tool that provides detailed information to help analyze, debug, and optimize a project's network traffic.

### Network Profiler

Unreal Engine also includes the [Network Profiler](/documentation/en-us/unreal-engine/using-the-network-profiler-in-unreal-engine), a legacy tool that offers a different view of a project's network traffic. While the information provided by the Network Profiler is less detailed than that of Networking Insights, it can still provide a high-level overview of your game's bandwidth usage as well as stats on individual Actors, Properties, or RPCs.

## Gauntlet Automation Framework

The [Gauntlet Automation Framework](/documentation/en-us/unreal-engine/gauntlet-automation-framework-in-unreal-engine) supports launching multiple sessions, such as a server and clients, and it can be an invaluable tool for testing and validating your multiplayer project.

There is a sample implementation of an automation script using Gauntlet for a multiplayer game in the **ShooterGame** project. It contains a ShooterGame automation C# that drives the tests, located in the `/Build/Scripts folder`, as well as the project's native test controller code, which is located in the `/Source/ShooterGame/Private` and `Public/Tests` directories.

## Functional Testing

UE includes the ability to set up and run [Functional Tests](/documentation/en-us/unreal-engine/functional-testing-in-unreal-engine) through the [Level Blueprint](/documentation/404). Your functional tests will initially be required to run on a single instance of your project. Afterward, you may run these tests in a multiplayer project. You can start the level containing the tests in a Client Instance, Dedicated Server, or a Listen Server Instance.

Setting up a functional test that runs across multiple instances, such as both the Client and the Server, is not currently supported. An example scenario where the desired functionality **will not** work is if the Server sets a Replicated Property to a new value, then the Client checks if this new replicated value was received.