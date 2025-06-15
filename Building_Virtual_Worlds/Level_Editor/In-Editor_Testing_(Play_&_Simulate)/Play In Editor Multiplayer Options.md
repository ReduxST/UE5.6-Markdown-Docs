# Play In Editor Multiplayer Options

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/play-in-editor-multiplayer-options-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/play-in-editor-multiplayer-options-in-unreal-engine)  
**Processed:** 2025-06-14 16:43:35

---

The **Play In Editor (PIE)** preview mode supports testing using multiple worlds, so you can test networked play. The editor spawns multiple worlds within the already loaded instance of Unreal Engine, which results in fast iteration time and allows you to debug Blueprints for each world.

## Setting up Networked Testing

In the **Play In** drop down menu in the **Level Editor Toolbar** or **Blueprint Editor Toolbar**, you can set how many client worlds to create when you begin a Play In Editor session. In addition, you can specify whether or not to run a dedicated server.

Click image for full size.

Using the **Number of Players** field, you can specify the total number of players you want to test.

Next, select the **NetMode** to use:

| **Option** | **Description** |
| --- | --- |
| **Play Standalone** | Creates a Standalone game. This option does not create a dedicated server. A server can be created by enabling **bLaunchSeparateServer**. |
| **Play as Listen Server** | Creates a session that acts as both a server and a client. Additional instances can be added depending on the number of clients. |
| **Play as Client** | Creates a session that acts as a client. A dedicated server is launched in the background. |

If the **Number of Players** field is set to 1, and the **NetMode** is set to **Play Standalone**, your Play In Editor session will test standalone, non-networked gameplay.

If the NetMode is set to **Play as Client**, a dedicated server world is launched, although there is no display or local player for the dedicated server. Using the dedicated server means that none of your clients will be running as a listen server. You can use the dedicated server to check for dedicated server only bugs, such as code that relies on a local player. A basic test configuration for Blueprints that have functionality that relies on servers and clients is to have the **Number of Players** set to 1, and **Play as Client** selected. This creates only one window to test play in, but it has the full functionality of a client connected to a dedicated server.

After setting these options, pick your preferred Play In Editor mode to begin testing gameplay. If you have more than one client world and select the Viewport display option for your Play In Editor session, one client world is shown in the viewport, and all others will be shown in new windows. The image below shows testing with 4 players and a dedicated server.

## Advanced Settings

The number of client worlds, as well as whether or not to use a dedicated server, can also be set in the [Level Editor - Play In Settings](/documentation/en-us/unreal-engine/play-in-editor-settings-in-unreal-engine) window. Here, you can also specify any command line options to be sent to the preview session.

| **Setting** | **Description** |
| --- | --- |
| **Launch Separate Server** | Launches a separate server even if the net mode doesn't require it. You can use this to test offline --> server workflows by connecting to a server from the offline game. |
| **Play Net Mode** | 
Sets the net mode used for Play In Editor session:

-   **Play Standalone**: Starts a standalone game. This will not create a dedicated server, nor automatically connect to one.
-   **Play As Listen Server**: Enables the Editor to act as both the server and the client. Additional clients can be opened depending on the number of clients.
-   **Play As Client**: Enables the Editor to act as a client. A dedicated server spawns behind the scenes to connect to.



 |
| **Run Under One Process** | Spawns multiplayer windows under a single instance of Unreal Engine. This loads much faster but is not as representative of a player's runtime environment, where each game instance would run in its own process. |
| **Show Server Debug Drawing by Default** | Draws debug rendering from the Dedicated Server during Play In Editor. |
| **Server Debug Drawing Tint Strength** | Controls the bias of the debug draw color towards the selected tint color. |
| **Server Debug Drawing Color Tint** | Selects the tint color of the server debug drawing. |
| **Enable Network Emulation** | 

Applies the selected network emulation settings when starting the game for the purpose of testing how your game handles network issues:

-   **Emulation Target**: Applies the emulation settings to the Server Only, Clients Only, or Everyone.
-   **Network Emulation Profile**: Applies a preset for incoming traffic and outgoing traffic. Options are Average, Bad, or Custom.
-   **Incoming traffic**: Applies settings that add latency and packet loss to all incoming packets. Can add minimum and maximum latency, as well as a percentage amount of packet loss.
-   **Outgoing traffic**: Applies settings that add latency and packet loss to all outgoing packets. Can add minimum and maximum latency, as well as a percentage amount of packet loss.



 |
| **Client** | 

Applies the selected client settings when starting the game:

-   **Play Number of Clients**: Opens a number of client windows. The first one will use the Play In Editor Modes options. The rest will use the Run Under One Process settings.
-   **Route Gamepad to Second Window**: Routes the gamepad input during a multiplayer session. If unchecked, then the first gamepad is attached to the first multiplayer window, the second to the second window, and so on. If checked, then the gamepad is routed to the second multiplayer window, allowing the first to be controlled by keyboard and mouse.
-   **Create Audio Device for Every Player**: Controls how many audio devices are created. If checked, a separate audio device is created for every player. This will render accurate audio for every player's perspective at the cost of CPU performance. If unchecked, a separate audio device is created for only the first two players.
-   **Client Fixed FPS**: Sets each client's framerate to an element in the list. Includes a Listen Server.



 |
| **Server** | 

Applies the selected server settings when starting the game:

-   **Server Port**: UDP port number used for game networking.
-   **Server Map Name Override**: Overrides the map launched by the server. Currently only used by the **PIE\_StandaloneWithServer** net mode.
-   **Additional Server Game Options**: Adds additional parameters that are passed to the server as URL parameters.
-   **Additional Server Launch Parameters**: Adds additional parameters that are passed to the server as arguments.
-   **Server Fixed FPS**: Sets the server to run at the specified framerate. Does not impact Listen Server.
-   **Multiplayer Viewport Size (in pixels)**: Spawns additional clients at the width and height specified. Useful when you need multiple clients but only want to interact with one window.



 |

## Debugging Blueprints

There is an additional drop down menu in the **Blueprint Editor** to select the world to debug when running a multiple world scenario:

The world selected in the world list filters the Actors in the Actor list. For example, with **All Worlds** selected, you will see Actors from every world in the other drop down list. By selecting only one of the worlds, you can see Actors from only that world instance.

This also affects break points. For example, setting the debug world to Client 1 will make it so that only breakpoints will trigger on Actors in Client 1's world.

You can see the client number for a preview window by looking at the window title. For example, in the networked play image above, one window is titled **LyraStarterGame Preview \[NetMode Client 1\]**.

When **All Worlds** is selected, any world can trigger break points.