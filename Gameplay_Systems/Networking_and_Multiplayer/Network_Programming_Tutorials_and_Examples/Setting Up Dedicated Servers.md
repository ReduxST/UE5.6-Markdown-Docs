# Setting Up Dedicated Servers

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-dedicated-servers-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-dedicated-servers-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:30

---

## Overview

**Unreal Engine (UE)** uses the **client-server** model for network multiplayer games. One server acts as the **host** for the game while players connect to the host as **clients**. The true game state is moderated by the server, this is referred to as the server being the **authoritative host**. Players control their pawns with an **autonomous proxy**. The server **replicates** changes from each connected client to simulate the true game state for each connected client. Clients see a close approximation of the game, which is actually being played on the server.

### Dedicated Server

A **listen server** consists of a client hosting the game on their machine and acting as the server. Other clients connect to the hosting client and play the game on the hosting client's instance. In this model, the hosting client is the **authoritative host**. This gives them an advantage over the connected clients as they are actively playing in the true game state.

A **dedicated server** consists of a server that runs headlessly. This means that there are no clients playing directly in the dedicated server game instance. Every player comes from a connected, remote client. A headless server does not render any visuals and nobody is playing locally on the headless server.

This has several advantages over a listen server:

-   Smaller size
-   No unfair advantage for the host client
-   Focus on gameplay logic and moderating information from clients

A listen server is often acceptable for casual multiplayer and cooperative gaming, but dedicated servers are ideal for large-scale or competitive games.

This tutorial shows you how to build, cook, and test a dedicated server.

## Tutorial

This tutorial uses the **Lyra Starter Game** as a base for setting up the dedicated server and clients. Lyra provides multiplayer functionality out-of-the-box, which makes it an ideal choice as a sample game for this tutorial.

To follow the steps in this tutorial, your project needs to satisfy the following requirements:

-   You must use a source build of Unreal Engine. See our [Download Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine) page for more information.
-   You must use a C++ project that supports client-server multiplayer gameplay.

### Configure Lyra

Ensure that you have Generated Visual Studio project files for Lyra. Furthermore, make sure that you have switched the Unreal Engine version to your source build. Instructions for doing this can be found on the [Download Lyra for Engine Source Builds](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine#downloadinglyraforenginesourcebuilds) documentation page. Once you have done this, open Lyra in the **Unreal Editor** by navigating to your project source directory and opening `LyraStarterGame.uproject`.

There are a couple things that you need to change before building the dedicated server and client builds of the Lyra sample:

-   Set the **Server Default Map** to **L\_Expanse** so clients are taken directly to the map instead of the Lyra Main Menu.
-   Change the number of bots that spawn to 0 so bots do not immediately start attacking clients as soon as they connect to the server.

#### Set Server Default Map

1.  In the menu bar, navigate to **Edit > Project Settings...**. This opens a new **Project Settings** window.
2.  Use the table of contents on the left to find **Project > Maps & Modes**.
3.  Change **Default Maps > Advanced > Server Default Map** to **L\_Expanse**.
4.  Close the **Project Settings** window.

For more information about the maps available with Lyra, see the [Lyra Sample Game](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine#playingthegamesample) documentation.

#### Change Number of Bots

1.  Changing the number of bots requires you to edit one of Lyra's **assets**. To edit an asset, open the **Content Drawer**.
2.  Switch the directory to **Plugins**.
3.  Search for the `B_ShooterBotSpawner` blueprint. This is the blueprint you need to edit to change the number of bots that spawn.
4.  Open the `B_ShooterBotSpawner` blueprint. This opens a new window for this blueprint's settings.
5.  Under the **Teams** section, find the field **Num Bots to Create**.
6.  By default, this number is set to 3 so that when a game is started within the **Unreal Editor**, it starts a 2v2 elimination style game. Set **Num Bots to Create** to 0. This way you can see the clients connecting to the same dedicated server without the distraction of bot activity.
7.  In the top left corner of the window, there is a **Compile** button. Click **Compile** for the changes that you made to the blueprint to take effect.
8.  Close the blueprint window.

The initial project settings are now configured. Close the **Unreal Editor**.

If you are following this guide using Lyra, the `PROJECT_NAME` variable in file paths is `LyraStarterGame` for the Lyra Sample.

### Build

#### Server

You are ready to build the **Development Server** configuration for the **Lyra Starter Game** project.

1.  Navigate to your project's root directory in **File Explorer**.
2.  Right-click on your project's `*.uproject` file and select **Generate Visual Studio project files...**
3.  Open the generated `*.sln` Visual Studio solution file in **Visual Studio (VS)**.
4.  If your project does not already have one, create a `<PROJECT_NAME>Server.Target.cs` in the `<PROJECT_DIRECTORY>/Source` directory.
    -   See `LyraServer.Target.cs` for an example.
5.  Change the **Solution Configuration** to **Development Server**.
6.  From the menu bar, select **Build > Build Solution**. This builds the dedicated server for your project.
7.  After the build process successfully finishes, you can find the newly built files in `<PROJECT_DIRECTORY>/Binaries/Win64`, in particular, the executable `<PROJECT_NAME>Server.exe`.
    -   For Lyra, these are located in `LyraStarterGame/Binaries/Win64`, in particular, the executable `LyraServer.exe`.

#### Client

You have built the server and can now build the **Development Client** configuration for the **Lyra Starter Game**.

1.  With Visual Studio still open from the [Build Server](/documentation/en-us/unreal-engine/setting-up-dedicated-servers-in-unreal-engine#server) step, change the **Solution Configuration** to **Development Client**.
2.  If your project does not already have one, create a `<PROJECT_NAME>Client.Target.cs` in the `<PROJECT_DIRECTORY>/Source` directory.
    -   See `LyraClient.Target.cs` for an example.
3.  From the menu bar, select **Build > Build Solution**. This builds the client game for your project.
4.  After the build process successfully finishes, you can find the newly built files in `<PROJECT_DIRECTORY>/Binaries/Win64`, in particular, the executable `<PROJECT_NAME>Client.exe`.
    -   For Lyra, these are located in `LyraStarterGame/Binaries/Win64`, in particular, the executable `LyraClient.exe`.

### Cook

#### Server Content

You have now built both the dedicated server and the clients that connect to the server. If you try to run the server from VS, you get an error message stating that there are missing shaders. This is because you have not yet cooked the content. To cook the server content:

1.  Start the **Development Editor** either from VS or by navigating to `UnrealEditor.exe` in your project's directory.
2.  From the **Main Toolbar**, set **Platforms > Windows > Build Target** to **Server** and **Platforms > Windows > Binary Configuration** to **Development**.
3.  Run **Cook** from **Platforms > Windows > Content Management**.
4.  A dialogue box appears in the lower right corner indicating that the content is cooking. Click **Show Output Log** in this dialogue box to monitor the cooking process.
5.  If the process exits successfully, the output log shows **BUILD SUCCESSFUL**.
6.  To see the files that were created during the cooking process, navigate to `<PROJECT_DIRECTORY>/Saved/Cooked/WindowsServer`.
7.  Test that the server runs successfully by navigating to your project directory in the command prompt and execute `./Binaries/Win64/<PROJECT_NAME>Server.exe -log`
8.  Close the **Logging** window to shut down the dedicated server.

#### Client Content

To cook the client content:

1.  If the **Unreal Editor** is not already running, start the **Development Editor** either from VS or by navigating to `UnrealEditor.exe` in your project's directory.
2.  From the **Main Toolbar**, set **Platforms > Windows > Build Target** to **Client** and **Platforms > Windows > Binary Configuration** to **Development**.
3.  Run **Cook** from **Platforms > Windows > Content Management**.
4.  A dialogue box appears in the lower right corner indicating that the content is cooking. Click **Show Output Log** in this dialogue box to monitor the cooking process.
5.  If the process exits successfully, the output log shows **BUILD SUCCESSFUL**.
6.  To see the files that were created during the cooking process, navigate to `<PROJECT_DIRECTORY>/Saved/Cooked/WindowsClient`.
7.  Run the client by navigating to VS, changing the **Solution Configuration** to **Development Client**, and selecting **Run without Debugging**.
8.  A splash screen appears saying **Experience Still Loading...** The client is running successfully, but it is expecting to connect to a dedicated server, which is not running. Close the Lyra client window.

### Test

#### Start the Dedicated Server

In a terminal window, run the following command from your project's root directory:

```
	`./Binaries/Win64/<PROJECT_NAME>Server.exe -log`

Copy full snippet
```
./Binaries/Win64/<PROJECT\_NAME>Server.exe -log

This starts the dedicated server and a logging window pops up.

By default, a dedicated server listens on the localhost IP address (`127.0.0.1`) at port `7777`. You can change the port for your dedicated server by adding the command line argument `-port=<PORT_NUMBER>`. If you change the port that your server is using, you will also need to change the port when connecting the client to the server.

#### Connect Clients to Dedicated Server

In a terminal window, run the following command from your project's root directory:

```
	`./Binaries/Win64/<PROJECT_NAME>Client.exe 127.0.0.1:7777 -WINDOWED -ResX=800 -ResY=450`

Copy full snippet
```
./Binaries/Win64/<PROJECT\_NAME>Client.exe 127.0.0.1:7777 -WINDOWED -ResX=800 -ResY=450

This starts an instance of the client game. To illustrate two clients connected to the same dedicated server, start another client instance by repeating the same command:

```
	`./Binaries/Win64/<PROJECT_NAME>Client.exe 127.0.0.1:7777 -WINDOWED -ResX=800 -ResY=450`

Copy full snippet
```
./Binaries/Win64/<PROJECT\_NAME>Client.exe 127.0.0.1:7777 -WINDOWED -ResX=800 -ResY=450

You should now see two players in the game. You can also check the server log for confirmation that both players are connected to the server.

The `-WINDOWED`, `-ResX=<HORIZONTAL_RESOLUTION>`, and `-ResY=<VERTICAL_RESOLUTION>` command-line arguments set here are for convenience. This enables you to see both client windows easily on the same screen for testing purposes. For more information on the command-line arguments used here, see our [Command-Line Arguments](/documentation/en-us/unreal-engine/command-line-arguments-in-unreal-engine) page.

## Extend the Multiplayer Experience

This tutorial teaches you how to build, cook, and test a dedicated server on your local machine. The next steps include: providing a functioning frontend, expanding your game's gameplay, and providing a means for players to connect to your dedicated server over the internet.

### Lyra Sample

See the Lyra Sample for an example of a working game sample in Unreal Engine.

### Expand Gameplay

See the Network Multiplayer Quick Start Guide for more information about expanding your game's multiplayer gameplay.