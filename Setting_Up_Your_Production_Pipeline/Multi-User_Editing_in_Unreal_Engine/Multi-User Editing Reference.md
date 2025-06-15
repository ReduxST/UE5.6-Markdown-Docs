# Multi-User Editing Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:37:28

---

This page contains information about requirements, settings, command-line parameters, and console commands for the **Multi-User Editing** system.

## Project Settings

### Multi-User Editing settings

When you have the **Multi-User Editing Plugin** activated in your Project, you'll have access to the following settings in the **Project Settings** window, under **Plugins > Multi-User Editing**.

| Setting | Description |
| --- | --- |
| **Client Settings** |   |
| **Enable Multi-User Toolbar Button** | 
When enabled, the Toolbar in the main Unreal Editor window contains a button that provides shortcuts for carrying out common Multi-User Editing tasks:

-   ![Join](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7189c045-f5c4-41e5-8a28-35cda6e51d00/02-multiuserediting-ref-iconjoin.png "Join"): When you're disconnected, and you have a default server name or session name set below, click **Join** to join that default session.
-   ![Browse](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9f0f4a8f-47ad-417c-b03f-0b8d242d9f2f/03-multiuserediting-ref-iconbrowse.png "Browse"): When you're disconnected, and you don't have a default server name or session name set below, click **Browse** to launch the **Multi-User Browser** so you can find and join a session manually.
-   ![Leave](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed49c94e-4ede-47a6-b1be-acc0c939b51d/04-multiuserediting-ref-iconleave.png "Leave"): When you're connected to a session, you can click **Leave** to disconnect.
-   ![Cancel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4178b03-0234-4628-952d-dc86d6d5d7ba/05-multiuserediting-ref-iconcancel.png "Cancel"): When you're connecting to a session, you can click **Cancel** to cancel connection.

You can also use the down arrow next to the Toolbar button at any time to access the **Multi-User Browser**, to open the **Project Settings** window to this page, or to start a Multi-User Server on your computer.



 |
| **Auto Connect** | Enable this setting to make the Unreal Editor immediately attempt to connect to the **Default Server URL** and **Default Session Name** set below each time you open this Project. |
| **Default Server URL** | 

Sets the name of the server that the Multi-User Editing system tries to connect to when you have the **Auto Connect** setting enabled or when you click the **Join** button in the Toolbar.

This must be the hostname of the computer running the server, as it appears in the **Session Browser** window.



 |
| **Default Session Name** | 

Sets the name of the session that the Multi-User Editing system tries to connect to when you have the **Auto Connect** setting enabled or when you click the **Join** button in the Toolbar.

If a session with that name doesn't exist yet on the default server, the server will start a new session.



 |
| **Default Session to Restore** | If you want to restore a saved session when you have the **Auto Connect** setting enabled or when you click the **Join** button in the Toolbar, enter the name of that saved session. |
| **Default Save Session As** | If you want the Multi-User Editing system to save the session it opens when you have the **Auto Connect** setting enabled or when you click the **Join** button in the Toolbar, enter the name you want that session to saved as. |
| **Display Name** | Sets the name that identifies you in all presence information visible to other users. |
| **Avatar Color** | Sets the color that the Multi-User Editing system associates with you in all presence information visible to other users. |
| **Desktop Avatar Actor Class** | 

Sets the class that the Multi-User Editing system uses to represent you in other users' Level Viewports when you're using a standard keyboard and mouse to interact with the Unreal Editor.  
If you want to change the default avatar, you can derive your own Blueprint class from the built-in **DesktopPresence** class and customize your class to meet your needs.



 |
| **VRAvatar Actor Class** | 

Sets the class that the Multi-User Editing system uses to represent you in other users' Level Viewports when you're using the VR Editing system to work in the Level using a VR headset and controllers.  
If you want to change the default avatar, you can derive your own Blueprint class from the built-in **VRPresence** class and customize your class to meet your needs.



 |
| **Client Settings — Advanced** |   |
| **Server Port** | 

When you launch the Multi-User Editing server from the Unreal Editor, this setting specifies the port the server should listen to for multicast traffic.

If you have also specified a port for the unicast endpoint IP address in your UDP messaging settings, the **Server Port** value you set here takes precedence. See also [Advanced Multi-User Networking](/documentation/en-us/unreal-engine/advanced-multi-user-networking-in-unreal-engine).



 |
| **Discovery Timeout** | If a previously discovered server does not respond to a message within this time span, it is considered stale and removed from the list in the **Multi-User Browser**. |
| **Session Tick Frequency** | Determines how frequently this instance of Unreal Editor processes session updates. |
| **Latency Compensation** | Determines how much compensation this instance of Unreal Editor should apply when treating incoming transactions that involve time-sensitive operations such as Sequencer playback. |
| **Endpoint Settings** |   |
| **Enable Logging** | 

Determines whether this instance of Unreal Editor should log detailed information about the current session. You can find these logs in your Project's `Saved/Logs/Concert` subfolder.

Activating this option can consume large amounts of disk space in a short time.

If you disable logging after you previously had it enabled, you'll need to remove those log files yourself in order to recover the disk space.



 |
| **Purge Processed Message Delay** | Determines how long this instance of Unreal Editor should wait before removing from memory any messages about the session state that it has already processed. |
| **Remote Endpoint Timeout** | If a remote instance of Unreal Editor does not respond to a message within this time span, it is considered stale and removed from the current session. |

### Multi-User Transactions Settings

You'll also have access to the following settings under **Plugins > Multi-User Transactions**.

Avoid adjusting these settings until you have used the Multi-User Editing system extensively with the default values, and you have a good understanding of how it works. Altering these settings can affect the stability of the Multi-User Editing system.

| Setting | Description |
| --- | --- |
| **Transaction Settings** |   |
| **Snapshot Transactions Per Second** | The number of transactions the Multi-User Editing system sends per second while you are interacting with a tool or control that synchronizes changes instantly with other clients — for example, while dragging an Actor in the Level Viewport, or while dragging a slider in an Actor's **Details** panel. |
| **Include Object Class Filters** | While this list is empty, the Multi-User Editing system automatically sends transactions for modifications to all class types. If you instead want to synchronize modifications only for specific classes, you can specify those classes in this list. The values that appear in this list by default are ones that have been tested and judged to be stable enough to expose. |
| **Exclude Transaction Class Filters** | 
If you want to restrict the Multi-User Editing system from synchronizing modifications to certain classes, you can specify those classes in this list. Any transaction that involves a change to an object with one of these excluded classes won't be synchronized.  
This list takes priority over the **Include Object Class Filters** list above.

By default, this list includes Landscape classes. Any modifications you make to a Landscape are not synchronized until you save the Level that contains that Landscape.



 |
| **Allowed Transient Properties** | 

Contains a list of transient class properties that are always synchronized, even if they would normally be filtered out. The default entries synchronize Actor visibility in the Editor. You can remove these default entries from the list if you want different users working in the same Level to be able to show and hide different sets of Actors.

If you need to change these values, make your changes directly in the `[/Script/ConcertSyncCore.ConcertSyncConfig]` section of the `Saved/Config/<platform>/Engine.ini` file rather than in the UI.



 |
| **Transaction Settings — Advanced** |   |
| **Interactive Editor Hot Reload** | 

Determines how Unreal Editor should handle the situation when it needs to replace an already loaded Asset with a different version of the same Asset. This happens when another user connected to your session modifies and saves an Asset. It also happens when you leave a session without persisting changes, and the Editor needs to replace content that was modified during the session with the content you initially had before you joined the session.

Leave this setting disabled to have the newly loaded content immediately replace the content you already had loaded. Enable this setting if you want to be prompted whether to reload each modified Asset.



 |
| **Show Presence in PIE** | Determines whether other users' presence information should be shown while you are in a **Play In Editor (PIE)** session. |
| **Package Settings** |   |
| **Exclude Package Class Filters** | Determines what saved packages will not propagate to the Multi-User server. You can filter by the package path and by a specific asset class. For example, adding **/Game/Maps/**\* to **Content Paths** will prevent anything saved in **/Game/Maps/** from propagating to the Multi-User server. |

## UnrealMultiUserServer Command-line Parameters

The [Getting Started](/documentation/en-us/unreal-engine/getting-started-with-multi-user-editing-in-unreal-engine) page shows how to launch the server component of the Multi-User Editing system from inside the UI of the Unreal Editor. However, you can also launch this server from the command line on any computer that has Unreal Engine installed.

If you run the server from the command line, you don't need to have your Project on that computer. The server only records transactions and modified Assets; it has no dependency on having the entire Project content available. Only the computers that join a session need to have copies of the Project content.

You'll find the Multi-User Editing server in your Unreal Engine installation folder, at `Engine/Binaries/<platform>/UnrealMultiUserServer.exe`. When you launch it, you can provide the following optional parameters on the command line to control its behavior.

| Parameter | Description |
| --- | --- |
| **\-ConcertSession=** | 
If specified, the server creates a new session with this name when it starts up. For example:  
`-ConcertSession=DemoSession`



 |
| **\-ConcertProject=** | 

If you've specified a **\-ConcertSession**, then the server will use the value of **ConcertProject** as the name of the Unreal Engine Project associated with the session. It will only permit connections from Unreal Editor instances that are running a Project with the same name. For example:  
`-ConcertProject=MyUprojectName`



 |
| **\-ConcertVersion=** | 

If you've specified a **\-ConcertSession**, then the server will use the value of **ConcertVersion** as the version of the Unreal Engine associated with the session. It will only permit connections from Unreal Editor instances that are built with the same version. For example:  
`-ConcertVersion=4.22.0-123456`

To get this version number, open the Unreal Editor and choose **Help > About Unreal Editor...** from the main menu.



 |
| **\-ConcertRevision=** | 

If you've specified a **\-ConcertSession**, then the server will use the value of **ConcertRevsion** as the base source control changelist associated with the session. It will only permit connections from Unreal Editor instances that are have Source Control active, and that have the same revision of the content checked out, with no local modifications. For example:  
`-ConcertRevision=4725058`



 |
| **\-ConcertIgnore** | 

Add this value to the command line if you want to prevent the Multi-User Editing server from validating that connecting Unreal Editor instances match the Project name, Engine version, and content source control changelist associated with each session.

Although it can sometimes be useful to permit clients to connect despite minor discrepancies in their Project content, you should avoid relying on this setting for your typical workflow in order to avoid any unexpected behavior that may be caused by your content being out of sync on different clients.



 |
| **\-ConcertClean** | 

Add this value to the command line if you want the server to remove all existing session files from its temporary storage directory when it starts up.

This removes all saved sessions.



 |
| **\-ConcertSaveSessionAs=** | 

If you've specified a **\-ConcertSession**, then the server uses the **ConcertSaveSessionAs** value to define the name it uses to save the session data in the event that it shuts down before the session has been deleted. Specifying the name in this way is equivalent to setting the **Session Data Management > Save Session As** value when you create a new session in the Unreal Editor UI.  
Once the session has been saved and the server shut down, you can start the server again with the **ConcertSessionToRestore** parameter to restore the state of that session.



 |
| **\-ConcertSessionToRestore=** | If you've specified a **\-ConcertSession**, then you can use this parameter to restore a session that this server previously saved with the specified name instead of creating a new session. |

## Unreal Editor Command-line Parameters

If you launch the Unreal Editor from the command line, you can use the following parameters to control the behavior of the Multi-User Editing system. These parameters set default values for some of the settings listed under [Project Settings](/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine#projectsettings) above.

| Parameter | Description |
| --- | --- |
| **\-ConcertAutoConnect** | Enables the **Auto Connect** setting for your Project. Immediately after starting up, the Unreal Editor will attempt to connect to the default server and session configured for it. You can pre-set this default session configuration in the **Project Settings**, or specify them on the command line using the parameters below. |
| **\-ConcertServer=** | Sets the value of the **Default Server URL** setting for your Project. |
| **\-ConcertSession=** | Sets the value of the **Default Session Name** setting for your Project. |
| **\-ConcertSaveSessionAs=** | Sets the value of the **Default Save Session As** setting for your Project. |
| **\-ConcertSessionToRestore=** | Sets the value of the **Default Session to Restore** setting for your Project. |
| **\-ConcertDisplayName=** | Sets the value of the **Display Name** setting for your Project. |

## Console Commands

This section lists the Unreal Engine console commands that affect the Multi-User Editing system.

| Command | Description |
| --- | --- |
| `Concert.DefaultConnect` | If you've set up a **Default Server URL** and a **Default Session Name** in your Project Settings, and if you're not already connected to a Multi-User Editing session, this console command immediately tries to connect you to the default server and session. |
| `Concert.Disconnect` | Disconnects you from the session you're currently connected to, if any. |
| `Concert.EnableOpenRemoteSequencer` | 
Anytime a user with this setting enabled opens a Level Sequence or Master Sequence in the Sequencer UI, the Multi-User Editing system automatically opens the Sequencer UI for all other users in the same session who also have this setting enabled, and loads the same Sequence.  
This setting is disabled by default. Use `Concert.EnableOpenRemoteSequencer 1` to enable it, or `Concert.EnableOpenRemoteSequencer 0` to disable it.



 |
| `Concert.EnablePresence` | When you have this setting enabled, you'll see an Actor in the Level Viewport that represents the current position and point of view of each other user working in the same Level that has a **Desktop Avatar Actor Class** or **VRAvatar Actor Class** set in their Project Settings. |
| `Concert.EnableSequencePlayer` | 

By default, the Multi-User Editing system only synchronizes Sequencer playback events between Unreal Editor instances that have the same Sequence open in the Sequencer UI.  
If you also want to synchronize Sequencer playback events to Unreal Editor instances that are running in `-game` mode, enable this setting.  
This setting is disabled by default. Use `Concert.EnableOpenRemoteSequencer 1` to enable it, or `Concert.EnableOpenRemoteSequencer 0` to disable it. You must enable it for each Unreal Editor instance that you start with the `-game` argument that you want to respond to those playback events.

Remember that if you use the `-game` option when you launch the engine, you also need to include the `-messaging` option.



 |
| `Concert.OpenBrowser` | Opens the **Multi-User Browser** window. Equivalent to choosing **Window > Developer Tools > Multi-User Browser** from the main menu or choosing **Session Browser** from the down arrow next to the Multi-User Editing button in the Toolbar. |
| `Concert.OpenSettings` | 

Opens the **Project Settings** window to the **Plugins - Multi-User Editing** page. Equivalent to choosing **Multi-User Settings** from the down arrow next to the Multi-User Editing button in the Toolbar.  
For details on these settings, see [Project Settings](/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine#projectsettings) above.



 |