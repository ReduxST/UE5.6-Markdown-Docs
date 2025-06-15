# Saving and Restoring Session Archives

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-restoring-session-archives-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/saving-and-restoring-session-archives-in-unreal-engine)  
**Processed:** 2025-06-14 16:47:46

---

At any time, you can have the Multi-User Editing server save all of the transactions made in a single session into an archive on disk. Later, you can use this archive to create a new session that contains all the same changes.

The instructions on this page show how to save a session to an archive, and to restore the archive to an active session later.

You'll use the controls in the **Multi-User Browser** to do this. You can open this panel by choosing **Window > Developer Tools > Multi-User Browser** from the main menu, or by activating the Toolbar button for Multi-User Editing. For more, see the [Quick Start](/documentation/en-us/unreal-engine/getting-started-with-multi-user-editing-in-unreal-engine).

## Saving a Session to an Archive

Follow the instructions in this section to save an active session to an archive on disk.

### Steps

1.  Select the session you want to archive in the **Multi-User Browser**.
    
2.  Click the **Archive** icon in the Toolbar, or right-click the session and choose **Archive** from the context menu.
    
    ![Archive icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/181ab807-77d1-4c7c-8378-3a9b61432fb1/01-archive-icon.png "Archive icon")
3.  Immediately below your session name, give the archive a descriptive name, then click the checkbox icon.
    
    ![Name the session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/819bb94e-cb6c-4e55-9788-975de13ea496/02-archive-name.png "Name the session")

### End Result

Your new archive appears in the list of sessions. It's distinguished from active sessions by its box icon, and by its lighter grey text.

![An archived session in the list of sessions](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b9a8315f-6008-4750-8baf-c22ab4376e65/03-session-list-new-archive.png "Archived session in the list of sessions")

The server saves session archives in the `Engine\Programs\UnrealMultiUserServer\Saved\MultiUser` folder under your Unreal Engine installation folder.

## Restoring an Archived Session

Follow the instructions in this section to restore an archive back to an active session that you can join to resume editing.

### Steps

To restore a session from an archive:

1.  Make sure you have the same server running that you used to host the original session. Each server is responsible for saving its own sessions to archives locally on its own computer. That means that each server can only restore sessions that it archived.
    
2.  Make sure that you have the same Project open that was originally used to create the session, and make sure the state of the Project's content matches the original state of the archived session.
    
    Remember that when you restore an archived session, just like when you join an existing session, your Project content on disk must match the state that the Project content was in at the time the session was originally created.
    
3.  Select the archive you want to restore in the **Multi-User Browser**.
    
    ![Select an archive in the sessions list](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/172f973c-fef2-4ac8-9904-5fa320324949/04-select-to-restore-archive.png "Select an archive in the sessions list")
4.  Click the **Restore** icon in the Toolbar, or double-click the archive, or right-click the archive and choose **Restore** from the context menu.
    
    ![Restore icon](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e88f720-4ccf-494e-8420-f2398d7ec2ff/05-restore-icon.png "Restore icon")
5.  Set the name of the new session that you want to create from the transactions stored in the archive, then click the checkbox icon.
    
    ![Name the new session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35528b4b-1619-41da-81b6-549506edd6ae/06-restored-session-new-name.png "Name the new session")\]
    

### End Result

The Multi-User Editing system starts a new session, owned by you, and immediately joins you to the session. The History will show the full record of all the transactions made while the session was live. As you work, you'll continue adding new transactions on top of this existing history.

![Restored session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/199064f8-387c-4dad-a267-847968247a85/07-history-of-sessions.png "Restored session")