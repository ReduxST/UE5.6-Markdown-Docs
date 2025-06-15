# Common User Plugin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/common-user-plugin-in-unreal-engine-for-lyra-sample-game](https://dev.epicgames.com/documentation/en-us/unreal-engine/common-user-plugin-in-unreal-engine-for-lyra-sample-game)  
**Processed:** 2025-06-14 16:14:25

---

# Common User Plugin

The **Common User** plugin provides a common interface between C++, Blueprint Scripting, and the [Online Subsystem](/documentation/en-us/unreal-engine/online-subsystem-in-unreal-engine) (**OSS**) or other online backends. It is distributed as part of the Lyra Starter Game and as a standalone plugin that can be used in any project.

## Design Philosophy

OSS was designed to be a generic interface for accessing platform-specific functions such as login, authentication and multiplayer sessions. It provides a standard interface that can be called from general Unreal Engine code to do a variety of operations. Because it is a generic and flexible library, it does not provide direct support for the high level flow of a typical gameplay session. Common User is an optional plugin that provides utility functions that help support features like an engagement screen, game controller handling, and hosting multiplayer games.

The features of Common User are exposed using [Engine Subsystems](/documentation/en-us/unreal-engine/programming-subsystems-in-unreal-engine) that can be called from C++ or Blueprint. The Lyra Starter Game provides an example of how to use these features and integrate them into a game. Common User works with the existing OSS in addition to other systems like the experimental **Online Services Interface**. Because it is defined in a game plugin, it can be modified or subclassed to work with proprietary online systems.Common User will be updated to support many game-related online features such as Leaderboards and Achievements. It currently provides support for the core operations(Login, Authentication, and Sessions) required to ship a commercial multiplayer game on multiple platforms.

## Installing the Plugin

To install the plugin into your game:

1.  Acquire the content and source code of the Lyra Starter Game from our **Unreal Engine Github**, or the Learn Tab on the Unreal Engine Launcher.
    
    Common User is not designed to be used in a Blueprint-only project.
    
    If you have access to platforms that are not included in the public release of the engine, you will need to use the version of the sample that includes those platforms.
    
2.  Navigate to the `c:Lyra/Plugins` folder located on your system, then copy the CommonUser folder into your game project's folder.
    
3.  In the editor, navigate to the Toolbar and click **Edit > Plugins**, then from the Plugin browser search for and enable the **Common User** plugin.
    
    ![common-user-plugin-setup](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bac3748f-ccd5-4316-8959-2b29bcfb74d2/commonuserplugin.png)
    
    You will need to enable any platform-specific online service plugins required for your project.
    
4.  Recompile your project to enable the subsystems.
    
5.  Observe the `.ini` files located in the `c:Lyra/Config` and the `c:Lyra/Platforms/PlatformName/Config` folders, then copy any values that you wish to use with your own .ini files.
    
    The settings and comments located in the Lyra config files can be used as a general guide for setting up your own project config settings, and the in-editor **Project Settings** can be used to commit some of the changes. See the [Lyra Scalability and Device Profiles](/documentation/en-us/unreal-engine/scalability-and-device-profiles-in-lyra-sample-game-for-unreal-engine) for more information.
    
6.  Blueprints will now have access to the Common User subsystems. To enable support for C++, you need to add CommonUser to the PrivateDependencyModuleNames section of your ModuleName.Build.cs file.
    
    See [Unreal Engine Modules](/documentation/en-us/unreal-engine/unreal-engine-modules) for additional documentation.
    

## Using the Online Services Plugin

By default, the Common User plugin uses the existing [Online Subsystem](/documentation/en-us/unreal-engine/online-subsystem-in-unreal-engine) plugin.

The Online Subsystem plugin is actively being replaced by the Online Services plugin (OSSv2) which provides improvements in asynchronous commands and error handling.

The [Online Services](/documentation/en-us/unreal-engine/online-services-in-unreal-engine) plugin is a beta feature, therefore the initial release of the Common User plugin does not use it by default. To swap the plugin to use the new interface, you can modify the `CommonUser.Build.cs` and change the `bUseOnlineSubsystemV1` boolean to the value of false, then navigate to the game's `Config/DefaultEngine.ini` config file, and add the following line.

```
`[/Script/Engine.OnlineEngineInterface] bUseOnlineServicesV2=true`
Copy full snippet
```
\[/Script/Engine.OnlineEngineInterface\] bUseOnlineServicesV2=true

This enables the build dependencies required to use the new interface. To use [Online Services EOS](/documentation/en-us/unreal-engine/online-services-eos-plugins-in-unreal-engine), you need to disable Online Subsystem EOS in any config file containing the section `[OnlineSubsystemEOS]`.

For example, in the `Lyra/Config/Custom/EOS/DefaultEngine.ini` file, you should set the `bEnabled` boolean value to `false`.

```
`[OnlineSubsystemEOS] bEnabled=false`
Copy full snippet
```
\[OnlineSubsystemEOS\] bEnabled=false

Using the beta Online Services plugin is recommended for games that are designed to be compatible with future releases of the engine. If you are developing a custom online backend or plan to use EOS as your primary backend, then you can enable Online Services support.

## Lyra and Common User

Lyra interacts with the Common User plugin in both C++ and Blueprint. Below are some examples of how Lyra uses the systems provided by this plugin:

-   The CommonGame C++ plugin includes classes like the **CommonGameInstance**(`UCommonGameInstance`). A game-specific GameInstance subclass can inherit from the CommonGameInstance class to integrate with features of the CommonUser and CommonUI plugins. You can use the code inside the class as an example of how to integrate your project with a different UI system.
    
-   The **LyraFrontEndStateComponent**(`ULyraFrontendStateComponent`) accesses the CommonUser subsystems directly from source code. This class is part of the logic that uses CommonUI to display the platform-specific **Press Start** screen (**W\_LyraStartup**) before the main menu(**W\_LyraFrontEnd**) is shown.
    
-   Multiple Widgets like **W\_LyraStartup** access the CommonUserSubsystem directly and use functions or async nodes to handle user operations.
    
-   The **LyraUserFacingExperienceDefinition**(`ULyraUserFacingExperienceDefinition`) class describes how to launch a game session with menu options that are standard with a multiplayer FPS. It is used by Widgets like **W\_HostSessionScreen** to create a session description that is passed into the CommonSessionSubsystem to host or join a game session.
    

The Lyra Starter Game is designed to be a working example of the [Epic Online Services](/documentation/en-us/unreal-engine/online-subsystem-eos-plugin-in-unreal-engine) (EOS) subsystem. By default, Lyra uses the Null subsystem, which only supports multiplayer in the editor or on local area networks. To enable support for EOS, you can either use the LyraGameEOS target when creating a packaged build or add the following option to your command line:

```
`-customconfig=EOS`
Copy full snippet
```
\-customconfig=EOS

This will load the EOS-specific config files from your `c:Lyra/Config/Custom/EOS` directory. These config files should be modified to use the EOS identifiers specific to your project.

# Plugin Subsystems

## Common User Subsystem

The **Common User Subsystem** (`UCommonUserSubsystem`) is designed to handle the user login, authentication, and permission check operations. These operations are required to use features like saved games that are tied to a player's profile. In an online-enabled game, user login is the first step that occurs because it is required before other online features will work. The Common User Subsystem handles initializing OSS interfaces like [Identity](/documentation/en-us/unreal-engine/online-subsystem-identity-interface-in-unreal-engine), and provides access for other Subsystems or Gameplay code. This subsystem defines the enumerations and structures used to describe the state of an individual user. In the table below, you can observe the important types used throughout the system:

| System Type Name | Description |
| --- | --- |
| ECommonUserOnlineContext | An Enumeration that identifies which lower level online system should be used for an operation. Blueprints and high-level C++ code will generally use the default context (Game) which combines information from multiple sources. On platforms like consoles that have their own authentication layer, the Platform context can be used to explicitly access it. The Service context can then be used to explicitly access services like EOS that work on top of the platform layer to provide features like crossplay. |
| UCommonUserInfo | An Object that is used to store the state of each individual user that is being managed by the system. Each user has their own Unique Net Id which is used to identify that user in classes like the PlayerState. In a single player game there will only be one User Info, but in a local multiplayer game there can be multiple User Info Objects that correspond to a platform-specific user(or a guest on platforms that do not support multiple local users.) |
| ECommonUserInitializationState | Describes the overall Login/Initialization state of a user. This state is modified as a user goes through the login steps described in the User Initialization Flow section below. |
| ECommonUserPrivilege | An Enumeration that describes the different capabilities and actions that users may perform as part of a Gameplay session. |
| ECommonUserAvailability | Describes the general level of availability for a privilege or other feature. For example, if the user has authenticated their account but the internet connection is currently offline, the availability of the privilege CanPlayOnline would be set to CurrentlyUnavailable. |

### User Initialization Flow

Logging in and authenticating a user is a complex, multi-step, and platform-specific process that takes a few seconds to perform. Below are the order of steps involved in the User Initialization flow:

1.  The person that wants to play the game needs to be identified as a user. On platforms like PC and Mobile, this happens before the game has started and the user's identity is sent from a launcher process. On platforms like consoles that support multiple logged in local users, an engagement screen(Press Start) must be used to identify the physical controller that the player wants to use to play the game.
    
2.  The user needs to be logged in and authenticated by using the platform interfaces. In some cases this happens automatically for the first identified user, while in other cases a platform-specific screen needs to be shown that explicitly maps a physical controller to a platform user.
    
3.  The privileges for that user need to be queried to determine if they are allowed to play the game. These privileges include platform-specific checks for valid software licenses or banned accounts.
    
4.  An initialization state of LoggedInLocalOnly is reached. The user is able to play the game locally and will have full access to profile-related operations like save games. However, they may not be able to play online or use other network privileges. To complete online initialization additional steps are required.
    
5.  The user may need to be logged in and authenticated a second time, possibly with a different online service.
    
6.  A different set of privileges for that user needs to be specifically queried for online play. This may include checking for active subscriptions and age restrictions.
    
7.  After passing the second set of privilege checks, the user is fully initialized for online play (LoggedInOnline) and is able to create or join multiplayer sessions.
    
8.  At any step in the process, a user can be forcibly logged out by the platform. This may require the game to be restarted because profile actions like save games are no longer available. In many cases this will require restarting the entire initialization flow.
    

A primary goal of the Common User Subsystem is to provide you with the functionality that allows individual games to ignore the complexity involved in this process.

### Requesting User Initialization

A state machine is built into the Common User subsystem that keeps track of which step a user is on during the initialization process. There are multiple methods you can use for starting this process.

| User Initialization Method | Description |
| --- | --- |
| Initialize for Local Play Login for Online Play | These Blueprint nodes can be placed in the Event graph of a Widget or other Blueprint to request a local-only or online login for a specific local player and physical controller. This is the simplest setup and it will activate the complete exec pin when initialization has succeeded or failed. |
| OnUserInitializeComplete | A delegate that can be bound from either Blueprint or C++ and is activated whenever a user completes initialization. |
| TryToInitializeUser | A function used to start a more advanced initialization process that will eventually execute the OnUserInitializeComplete delegate. |
| Listen for Login Key Input | A function used to create an initial engagement screen(Press Start) or allow the capability to add controllers in local multiplayer. This is achieved by registering a temporary input handler that listens for certain controller buttons or keyboard keys, then calls TryToInitializeUser with the correct parameters. |
| LoginLocalUser | A function that can be called from C++ if you want to manage the initialization manually.. |

These functions are used in the Lyra menu widgets(**W\_LyraStartup**) and C++, to show an explicit engagement screen on multi-user platforms, or attempt to automatically log in user\_0 on controller\_0 for PC and Mobile platforms. This is done by calling the ShouldWaitForStartInput function, however if you are creating a single player game, you may want to always show an engagement screen. An explicit login for online play is requested in widgets like **W\_ExperieceSelectionScreen** that can start online sessions.

There is no controller parameter for this online login because the user should have already completed local initialization.

### Other Operations

The Common User Subsystem provides other useful functions that you can use to query or change information for a particular user. You can look at the blueprint functions using the Common User Subsystem or read the CommonUserSubsystem.h file for details.

| Common User Subsystem Function | Description |
| --- | --- |
| OnHandleSystemMessage | A delegate that can be bound to display error messages related to online functions. The UCommonGameInstance class in Lyra shows a simple error popup, and SendSystemMessage can be used to trigger this UI from gameplay code. |
| OnUserPrivilegeChanged | A delegate that can be bound to handle any privilege change for a user. This is used to provide game-level handling for cases like losing network connectivity. |
| GetUserInfoForLocalPlayerIndex GetUserInfoForPlatformUserIndex GetUserInfoForUniqueNetId | The main method of querying information about a user. They return CommonUserInfo objects that can be queried for their network id, display nickname, and privileges. |
| GetOnlineIdentity GetOnlineSubsystem | A lower-level wrapper function that can be used by gameplay code or other subsystems to access the cached interface data. These functions are specific to the online interface being used. |

## Common Session Subsystem

The **Common Session Subsystem**(**UCommonSessionSubsystem**) is designed to provide a simple interface to access online features that include creating, searching, and joining online Gameplay sessions. The OSS [Session Interface](/documentation/en-us/unreal-engine/online-subsystem-session-interface-in-unreal-engine) provides platform-independent wrappers for operations that can interact with a platform's native matchmaking interface and a cross platform system like EOS. Depending on the game and platform, a multiplayer session may be physically hosted by a dedicated server or by a player who is also playing the game. Player-hosted(listen) servers are run on a console or user-owned PC that must be accessed by using a form of Peer-to-Peer(P2P) NAT traversal(like EOS). The goal for all multiplayer gameplay sessions is to connect two instances of the game together so they can use all features of the [Unreal Engine Networking](/documentation/en-us/unreal-engine/networking-overview-for-unreal-engine) system. However, before connecting the two instances, intermediate structures(known as Lobbies or Sessions depending on the situation) need to be created and queried.

### Requesting Session Initialization

There are multiple methods that you can use to initialize a session using the Common Session Subsystem but the table below lists the basic options available:

| Initialization Method | Description |
| --- | --- |
| HostSession | Can be called with a Host Request that describes the specific Gameplay mode and map that will be loaded. This can be used to create a single player session that does not register with the online backend, so your UI does not need to understand the difference between them. Once the session has been created, the specified map will be loaded and gameplay will begin. |
| FindSessions | Can be called to ask an online system for a list of joinable sessions that match the search request.It takes a Request(`UCommonSession_SearchSessionRequest`) and a SearchingPlayer (`APlayerController`) parameter to look for public matchmaking games that satisfy the provided arguments. The OnSearchFinished delegate implemented on the Request object will be called when the search is completed and the search result objects (which are filled in on the request object) can be used to join a session. |
| JoinSession | Takes a search result object and attempts to connect and join that multiplayer session. If successful, the game will connect to that peer or dedicated server and attempt to join the game as a network client. |
| QuickPlaySession | Starts the process to look for any existing public sessions that match the host parameters and will join them if possible. This method combines the other three initialization functions and is called with a host request. If joining a session is not possible, then it will start a new session. CommonSessionSubsystem provides a basic implementation, but games can override quickplay-related functions in a game-specific subclass if needed. |

Lyra interacts with the Common Session subsystem in several Widget Blueprints:

| Widget Blueprint | Description |
| --- | --- |
| W\_ExperienceSelectionScreen | Handles quick play in addition to choosing to either host or search for sessions. |
| W\_SessionBrowserScreen | Handles searching and joining existing sessions. |
| W\_HostSessionScreen | Allows specifying the hosting rules and creating a new local or multiplayer session. |

These Widgets rely on assets from the LyraUserFacingExperienceDefinition class located in your `c:Lyra/Source/LyraGame/GameModes` directory. This class defines the types of specific Maps and Gameplay modes that can be used in the game. The Lyra source code also includes checks to ensure that sessions are properly cleaned up in memory when a player leaves a game or has login failures.

Both the CommonSession Subsystem and Lyra are designed to search and create P2P hosted sessions that use the EOS [Lobby interface](https://dev.epicgames.com/docs/services/en-US/GameServices/Lobbies/index.html) (when support is enabled as described above.) It works with the local sessions that are created while testing [multiplayer in the editor](/documentation/en-us/unreal-engine/play-in-editor-multiplayer-options-in-unreal-engine) with the [Null subsystem](/documentation/404). To enable full support for other online backends In the initial release of the plugin, you may need to change some of the options passed to the internal session objects like FOnlineSessionSearch.