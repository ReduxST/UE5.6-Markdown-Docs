# Multi-User Editing Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-editing-overview-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-editing-overview-for-unreal-engine)  
**Processed:** 2025-06-14 16:37:27

---

The Multi-User Editing workflow is built on a client-server model, where a single *server* hosts any number of *sessions*. Each session is a separate virtual workspace that any Unreal Editor instance on the same network can connect to in order to collaborate on the same Project content inside a shared environment.

![Multi-User Editing network server and clients](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fdc81fb1-62ba-4614-b47c-629f39fc7df6/multiuser-editing-overview.png "Multi-User Editing network server and clients")

While inside a session workspace, each user can interact with the Project content in any way made possible by their instance of Unreal Editor. For example:

-   Some users might work using a keyboard and mouse in a standard desktop PC setup — on different platforms, if needed.
    
-   Other users might choose to use the Editor's VR editing mode to visualize and work in the scene using a VR headset and controllers, or they might use a plugin like the [Virtual Camera](/documentation/en-us/unreal-engine/virtual-cameras-in-unreal-engine) to enter the same scene using a mobile device.
    

Whenever any connected user makes a change to a Level or saves an Asset in the Project, their instance of Unreal Editor automatically forwards information about that change to the server. The server is responsible for keeping track of all these change records, or **transactions**, and for sending out those transactions to all other connected clients. Each client then applies those same changes locally within its own environment. In this way, everyone's view of their current Level and of other Assets in the Project remains up to date with the latest changes.

## Synchronizing Transactions

The Multi-User Editing system chooses different strategies for synchronizing changes between connected clients depending on the type of Asset you're working with and the type of changes you make.

### Levels: Instant Sync

All changes that you make to the contents of a Level are synchronized immediately with all other computers in the session. If you add or remove Actors, move Actors from place to place, swap Materials, or change the properties of an Actor, all other users in the session will see those changes take effect immediately. Dragging a tool to move, rotate, or scale an Actor causes multiple transactions to occur while you're dragging. Other users see these changes happen even before you release your mouse.

For example, in the following video, when the user on the left makes changes by dragging Actors from place to place, the user on the right sees those changes reflected immediately in their Viewport, even before the drag is released. Similarly, when the user on the right rotates the object, the user on the left sees the changes immediately.

You only see the effects of other users' changes if you're in the same Editor mode: that is, if you're both in editing mode, or if you're both in one of the **Play In Editor (PIE)** or **Simulate** modes.

### Other Assets: Sync on Save

The Multi-User Editing system does not immediately synchronize most types of Assets in your Unreal Engine Project each time you make a change. This includes Asset types like Materials and Material Instances, Static Mesh Assets, Blueprint classes, and so on. In these cases, when you make changes to these Asset, you are the only one who sees the changes take effect in your environment immediately. When you save your changes, the Multi-User Editing system sends the transaction around to all other users in the session. 

In this case, the transaction is not just a record of the change, but the actual saved Asset. Each instance of the Editor that receives one of these updated packages immediately hot-reloads it, making the changes visible.

For example, in the following video, when the user on the left changes a Material, their changes are not immediately synchronized. However, when the user saves their changes to the Asset, the transaction is processed and the changes show up for the user on the right.

After you save your Asset, you automatically acquire a lock on it. In addition, while you have unsaved changes to some kinds of Assets, the Multi-User Editing system marks those Assets as dirty for other users. See [Avoiding Conflicts](/documentation/en-us/unreal-engine/multi-user-editing-overview-for-unreal-engine#avoidingconflicts) below.

### Sequencer: Playback Sync and Optional UI Sync

The Multi-User Editing system treats Level Sequences and Master Sequences like Levels: when any user makes a change to a Sequence such as adding or removing a track, or adding a new keyframe, it immediately synchronizes that change to all other users in the session. 

In addition, when one user plays a Sequence, the same Sequence plays immediately for all users that have that same Sequence open. Only the user who began playback will be able to stop it. After the Sequence has stopped, any user can restart playback.

You can also choose to have the Multi-User Editing system automatically open the Sequencer UI on all clients when one user opens it. Because the Multi-User Editing system synchronizes playback for all users that have the same Sequence open, enabling this UI synchronization option helps you make sure that all users see the same Sequence play back at the same time.

The following video shows how the Multi-User Editing system synchronizes Sequencer UI events, playback events, and editing events.

To enable UI sync for the Sequencer as shown above, use the `Concert.EnableOpenRemoteSequencer` console command. For details, see the [Console Commands](/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine#consolecommands) section of the [Multi-User Editing Reference](/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine).

The Multi-User Editing system synchronizes playback events, but different computers may play back the animations at different frame rates. Do not expect the results to be frame-accurate from one instance of Unreal Editor to another.

## Presence

The Multi-User Editing system offers a few different ways to see what the other users in your session are doing.

The presence information described in the following sections uses a display name and color to distinguish the connected users. Each user can customize these values using the **Display Name** and **Avatar Color** settings in their **Project Settings**. For details, see the [Multi-User Editing Reference](/documentation/en-us/unreal-engine/multi-user-editing-reference-for-unreal-engine#projectsettings).

### Location and Viewpoint

While you're working in the same Level as another user, you'll see an avatar that represents their position and viewpoint on the scene. As they interact with the scene, you'll also see lasers that indicate the objects highlighted by their mouse cursors or motion controllers.

For example, the following image shows avatars for two desktop users working in the same Level:

![Multi-User Editing desktop avatars](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/16b357d3-1f17-4874-87c4-c1e91d3a427f/multiuserediting-ov-presence-avatars.png "Multi-User Editing desktop avatars")

At any time, you can use the controls in the **Connected Clients** panel of the **Multi-User Browser** window to work with this presence information.

![Multi-User Editing Connected Clients panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b504def-2cd6-4554-b07e-bebf6a0cdbc0/ue5_01-connected-clients.png "Multi-User Editing Connected Clients panel")

| Icon | Description |
| --- | --- |
| ![Teleport to user's point of view](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f5d964de-4d73-46fd-b39d-69f4887170d8/multiuserediting-ov-presence-location.png "Teleport to user's point of view") | Teleport immediately to the same location and viewpoint as this user. |
| ![Toggle presence visibility](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2dbf8ff0-95e1-4064-a15c-622cbc2f24cf/multiuserediting-ov-presence-visibility.png "Toggle presence visibility") | Toggle displaying the avatar and laser pointers for this user. |

You can also click the **Level** listed for any connected user to switch to that Level and teleport immediately to that user's location and viewpoint.

### Session Change History

The **Multi-User Browser** window shows a list of all editing transactions that have occurred in the current session, and each time a user connected to or disconnected from the session.

![Session change history](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed3658f8-cff8-4c52-836c-037728173f65/ue5_02-multi-user-browser.png "Session change history")

### Asset Change History

You can also view the list of changes made to each individual Asset. Right-click an Asset in the Content Browser, and select **Multi-User > Asset History**. You'll get a list of all the transactions that modified this particular Asset.

![Asset change history](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ec2fd843-4248-4202-a96e-aedd28418012/ue5_03-asset-history.png "Asset change history")

## Avoiding Conflicts

When you allow multiple people work on the same content at the same time, they're likely to eventually try to change the same things at the same time. If you are too permissive about allowing this to happen, it can cause frustrations as people fight for control or lose the changes they make. On the other hand, if you are too strict, you may reduce people's ability to modify the things they need when they need to, which can slow down their work or block them entirely.

The Multi-User Editing system attempts to find a balance between these two extremes, preventing fighting and overwriting in the most common cases of contention between users.

### Locking Dragged Selections

While you're actively dragging a selection in the Level Viewport — for example, to move, rotate, or resize it — you have exclusive control over those Actors. If another user attempts to modify any of the same Actors, either by dragging it with a tool in the **Level Viewport** or by setting properties in the **Details** panel, their changes will be immediately reverted.

As soon as you stop your drag interaction, other users become free to work with those Actors again, even if you still have them selected.

### Locking Assets

If you want to prevent other users from modifying certain Assets, you can lock them. While an Asset is locked, only the user who locked it can save new modifications. Other users can still modify locked Assets locally in their own Project, but they can't save their modifications until the user who owns the lock unlocks it.

There are two ways to lock and unlock Assets:

-   Any time you begin modifying an unlocked Asset, you acquire a temporary lock on it until you save your changes.
    
-   You can also lock and unlock selected Assets without modifying them. Right-click them in the **Content Browser** and select **Multi-User > Lock Asset(s)** or **Multi-User > Unlock Asset(s)**.
    
    ![Lock and unlock Assets](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/555fe81d-bcfa-44b1-a45c-cac5b1ba8e35/ue5_04-lock-asset.png "Lock and unlock Assets")

You can tell locked and modified Assets by the overlay on the Asset's thumbnail in the **Content Browser**. Mouse over the Asset to see details about the user who owns a lock or who has modified an Asset:

![Asset locks and dirty flag](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae2fbc65-7b92-48fa-aa04-d70a5e1686d5/ue5_05-asset-details.png "Asset locks and dirty flag")

| Overlay | Description |
| --- | --- |
| ![Locked by you](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/81a14a75-50b1-4536-a688-222b34d9bcf8/ue5_06-locked-by-me.png "Locked by you") | White indicates that you locked the Asset. You can continue modifying at any time. Other users cannot modify this Asset until you save or unlock it. |
| ![Locked by someone else](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4b12e1b-cead-4832-ad41-8786f59c7d12/ue5_07-locked-by-other-user.png "Locked by someone else") | 
White with avatar indicates that another user has locked this Asset. You can still modify this Asset locally in your Project. If you do, you'll be notified that another user has it locked:

You won't be able to save your modifications and sync that change to others until the user who owns the lock releases it.



 |
| ![Modified but unsaved on another computer](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/752b662c-1fb1-44fe-95c6-b6abd17d0c25/ue5_08-modified-asset.png "Modified but unsaved on another computer") | 

Asterisk indicates the Asset is dirty (modified but unsaved) on another computer.

Only selected Asset types get marked with this icon. Be cautious about modifying Assets in this state — whoever saves their changes first gets a lock on the file and their change propagates to all other clients, potentially losing changes that others have made.



 |

### Undo and Redo

Each connected user has access only to their own history of operations. Within that history, each user can freely undo and redo their own actions, just as if they were working offline without being part of the session. However, a user cannot undo or redo any actions carried out by any other user in the session.

## Starting from a Common State

To avoid long delays and high bandwidth usage, the server in the Multi-User Editing system does not transfer the entire contents of your Project between connected users. Instead, it relies on exchanging lightweight transaction records when it needs to achieve instant synchronization, and only circulates Assets like Levels, Static Meshes, Blueprints, and so on when those Assets get modified and saved during the course of a session.

The only way to make sure that incoming transactions are applied in exactly the same way for every connected user, and therefore that every user's content is kept in sync with every other user's content, is to have every connected user *start* with exactly the same content in exactly the same state. That way, as the same list of transactions is applied to each client in the same order, the overall state of each user's content is guaranteed to remain synchronized.

The typical way to get all users to start with the same content is to use a source control system such as Perforce, Git, or SVN, and to make sure that each user synchronizes their local copy to the same changelist or revision as everyone else before they connect to a session together. See the [Multi-User Editing and Source Control](/documentation/en-us/unreal-engine/multi-user-editing-overview-for-unreal-engine#multi-usereditingandsourcecontrol) section below for more.

Using source control isn't an absolute requirement; you can use Multi-User Editing without an external source control system. However, in that case it is up to you to find a way to share your Project content within your organization such that all the users you need to work together are reliably able start with the exact same Project content.

### Session Validation

Every time a user attempts to connect to a session, the server checks certain attributes of their content and their working environment to see if they match the content the session was initially started with. If any of these checks fail, the server won't allow the user to join the session.

-   **Version of UE -** The server checks that the user trying to connect to the session is using the same version of Unreal Engine as the user who started the session. For example, if the user who started the session used version 5.0, and another user tries to join using version 4.27, the server won't allow the connection. This helps avoids problems caused by changes to Asset formats between different versions.
    
-   **Project name -** The server checks that the user trying to connect to the session has a Project open whose name matches the name of the Project that was used to create the session. If this check fails, the server assumes that the content in the two Projects can't be the same, and refuses the connection.
    
    ![Failure to join - invalid Project name](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69863c5d-974b-480a-be2c-ce23f6482734/ue5_10-failed-to-join-invalid-name.png "Failure to join - invalid Project name")
-   **Source control revision -** If the user who started the session was connected to a Source Control provider in the Unreal Editor, the server associates the changelist or revision of their Project with the session. When another user who has a Source Control provider active attempts to connect to that session, the server checks that their changelist or revision matches the one associated with the session. 
    
-   **Locally modified files -** If you are connected to a Source Control provider, and you have any locally modified files, the server will prevent you from creating new sessions and joining existing sessions. This avoids the possibility of having users on the same changelist but with different versions of certain Assets.
    

## Transactions and Persisting Changes

As you and your teammates work in a live session, the Editor applies transactions on top of your local Project content in a kind of virtual sandbox. Your Project files on disk are not actually modified at all as long as you remain in the session. The Multi-User Editing system takes care of keeping track of your changes, and shows you in the Unreal Editor the result of applying those transactions to your Project content.

At any time, any session participant can choose to **persist** the session changes: to take all the modifications made in the current session, and apply those changes back to their local files on disk. If you began your session while connected to a Source Control provider, you can also optionally check in those same changes in a new changelist or revision.

![Persist Session Changes from the Toolbar](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/86832746-6e6d-457a-81e8-fd0691e506e8/ue5_12-persist-session-changes.png "Persist Session Changes from the Toolbar")

If you leave a session without persisting changes, the Editor automatically reverts back to the state your Project was in before you started or joined the session. It hot-reloads all the Assets in your Project that you modified while in the session, discarding the session modifications. Although you no longer see your session changes after you leave the session, you don't lose the transactions entirely. Each session still retains the record of all its transactions, even when all its users have left. If you re-join the same session later, the Multi-User Editing system re-applies all those same transactions in your Editor.

If you leave a session *that you own* without persisting changes, you'll also be prompted to persist the changes. This helps avoid the possibility of leaving changes unsaved within the session by accident. Even if you dismiss this prompt, you won't lose the pending changes forever. You can rejoin the session anytime and persist the changes later. Even if the server shuts down, the session changes aren't lost; see the next section for details.

### Redundancy

The server retains each session until the user who created the session expressly deletes it, or until the server itself is shut down. Therefore, a crash or disconnection for any individual client, or even for all clients, never results in losing modifications. Users can simply reconnect to the server and pick up where they left off.

The server also protects itself against losing information due to unexpected shutdowns by saving its session records to disk.

-   If the server shuts down abnormally, then the next time you restart that server it will immediately restore all the sessions it had open at the state they were in when it shut down.
    
-   If you shut down the server cleanly, it archives all live sessions. You can restore the session from the archive later. See the next section for details.
    

## Multi-User Editing and Source Control

The Multi-User Editing system offers some features that are similar to source control systems, such as having a server that stores a history of transactions, or having users acquire locks on the Assets they work on to reduce contention. However, **Multi-User Editing is not a replacement for source control**.

Multi-User Editing is best used to augment a standard collaboration workflow in which you use a dedicated source control system such as Perforce, SVN, or Git to regularly record the changes you make to your Project.

If you're using Perforce, you can also consider using UnrealGameSync (UGS) to make this process easier. For details, see [the UGS documentation](/documentation/en-us/unreal-engine/unreal-game-sync-ugs-for-unreal-engine).

When you have such a version control system set up in your team, use Multi-User Editing for limited-time live collaborations on top of a specific, defined changelist.

-   At the start of each live session (a shoot, a day's work, a review meeting, or whatever applies to the work you do with your team), all participants decide on the changelist they'll start from. This is typically the latest revision. Everyone syncs to that revision.
    
-   At the end of the live session, one person commits those changes back to the team's usual source control system to preserve them.
    
-   After committing changes from a session back to source control, you can delete the session — you don't need it anymore.
    
-   Next time you need to work live with others, start a new session based on the latest changelist.
    

We don't recommend keeping a single Multi-User Editing session in use for a long period of time — that is, for days or weeks of work. Stop and commit your changes regularly to source control.

For more information about connecting the Unreal Editor UI to a Source Control provider, see [Collaboration in Unreal Engine](/documentation/en-us/unreal-engine/collaboration-and-version-control-in-unreal-engine).

## Launching in -game mode

If you use the `-game` command-line option to launch your project, you also need to include the `-messaging` option. This option enables the MessageBus system that the components of the Multi-User Editing system use to communicate with each other under the hood.

## Networking

When you join a session, your instance of Unreal Editor connects to the server via UDP, on port **6666**.

-   Each computer running the Unreal Editor that wants to connect to a server must be able to see the Private IP Address of that server's computer.
    
-   The server's computer must have port **6666** open to UDP traffic coming from the local network.
    

You should only expect this connection to work on a Local Area Network (LAN), or potentially if both endpoints are in the same Virtual Private Network (VPN). Do **not** expect to share your Unreal Editor sessions over an open Internet connection.

The instructions in the Getting Started page should be enough to get you up and running in a simple LAN. If you have trouble establishing connections between your clients and your server, you may be able to adjust the UDP Messaging settings for your Unreal Editor instances and your server. See [Advanced Multi-User Networking](/documentation/en-us/unreal-engine/advanced-multi-user-networking-in-unreal-engine).