# Multi-User Server User Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-server-user-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/multi-user-server-user-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:31

---

A user interface was added to the **Multi-User Server** to inspect the running status of the server live. This enables operators and ICVFX stage managers to inspect, monitor, and diagnose problems during Multi-User Server operation.

This has benefits over the console server, which only provided a stream of connection information over a console command, and did not provide contextual information about the running server operation.

The console server is still available for operation on headless computers, or on computers where running a UI is not possible. For example, a Linux server or containerized operation.

## Building the Multi-User Server

The Multi-User Server program needs to be built in order to run. If you are using precompiled binary builds, the server should be pre-built, and available upon launching the Engine. If you are building Unreal Engine from Source, we recommend you use **UnrealGameSync** to build compiled versions of the server for both console and UI versions.

In UnrealGameSync you can build the server during the normal sync operation by enabling the options **Compile UnrealMultiUserServer** and **Compile UnrealMultiUserSlateServer**. The latter is the name of the new UI based server.

1.  Click **Options** in the bottom-right corner of the UnrealGameSync interface and select **Customize Commands.**
    
    ![Customize Build UnrealGameSync](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0dbfddbd-f742-45a5-92a8-d9550fc68b68/ugs-customize-build.png)
2.  In the Modify Build Steps dialog, enable the checkbox next to **Compile UnrealMultiUserServer** and **Compile UnrealMultiUserSlateServer.**
    
    ![Modify Build Steps UnrealGameSync](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c56c1d81-11e0-47c5-b3b1-9461b55e9ee8/ugs-modify-build-steps.png)

## Enable the Multi-User Editing Plugin

To use the Multi-User Server, you must enable the **Multi-User Editing** plugin in your project.

1.  In the Editor go to **Edit** > **Plugins** to open the Plugin Browser.
    
2.  Search for "Multi-User" and enable the **Multi-User Editing** plugin.
    
    ![Enable Multi-User Editing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bab08d3f-7eb3-418b-a468-c28b26323cbb/enable-multi-user-plugin.png)
3.  Restart the Unreal Editor before you proceed.
    

## Change Settings to Launch UI Mode

After you enable the plugin you need to change the default server mode in the Multi-User Project Settings to make the plugin launch in UI mode.

1.  In the **Window** menu select **Multi-User Browser** to open the plugin interface.
    
    ![Enable Multi-User Editing](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e7863723-6d03-4375-9c9b-1ecc6dd86f91/multi-user-browser-settings.png)
2.  Click the **Settings** gear icon in the upper-right corner of the **Multi-User Browser** window. This will open the Multi-User Editor plugin settings.
    
3.  Under **Client Settings**, change the **Server Type** property to **Slate** mode.
    
    ![Enable Slate UI mode](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f1020c0-c26e-40f1-836e-fec314084eb4/server-type-slate.png)

### Switchboard Support

Launching the Multi-User Server in UI mode is also supported in Switchboard. The Switchboard application launches Multi-User Server in UI Mode by default.

You can change this behavior by adjusting the global settings in the **Switchboard Settings** menu.

1.  In the Switchboard application menu go to **Settings** > **Settings**.
    
    ![Switchboard Settings Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6daa9665-388e-463a-af3b-683a1961a725/switchboard-settings-menu.png)
2.  Scroll down to the **Multi User Server** section.
    
3.  Uncheck the box next to **Launch Multi-user server in UI mode** to disable the user interface version. Switchboard will now launch Multi-User Server sessions in Console mode.
    
    ![Switchboard Settings Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f52ef24e-6d61-4af7-ab67-1f541c0f7cab/switchboard-settings-panel.png)

## Running the Multi-User Server

You can run a new server from the **Multi-User Browser** Editor panel, or from **Switchboard**.

### From Multi-User Browser

When the Multi-User Browser panel is open, the plugin will automatically search for available servers on the network.

You can launch a new server by clicking the **Launch a Server** button in the middle of the window, or the server icon on the left side of the toolbar.

![Launch Multi-User Server](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca4ae13f-a01e-48dd-b9f3-112b8e849172/launch-multi-user-server.png)

The Multi-User Server UI opens in a new window.

![Launch Multi-User Server](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1618c943-5439-429b-8f45-1e9d41c73d63/multi-user-server-interface-sm.png)

### From Switchboard

In the Switchboard application click the **Multi-user Server** launch icon in the bottom-left corner of the window.

![Launch Multi-User Server in Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56acc855-8785-4cea-b01d-a5f174eef8b5/launch-multi-user-server-switchboard.png)

## Multi-User Server UI Overview

The Multi-User Server interface contains three regions.

![Multi-User Server UI](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d44e1741-3a3f-4a80-88c3-f7e62c988054/multi-server-ui-annotated.png)

1.  Menu bar and Tabs.
2.  Sessions and Client information panels.
3.  Command Console and Output Log.

### Menu bar and Tabs

#### Window

The Window menu displays a context-sensitive list of browser windows available within the current UI tab (Sessions, Clients, or Active Session). You can use this list to restore windows that were previously closed.

![Window Menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6805a87c-efc9-4d28-83f1-921e27b4873d/window-menu.png)

#### Debug

Under **Debug** > **View App Icons** you can summon an information key that describes all the icons in the Multi-User Server interface.

![Multi-User Server Icon Key](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5742e444-b5df-4ac0-b87c-f28b35d13f49/multi-user-icon-key.png)

#### Tabs

Beneath the menu bar is a row of tabs which enable you to switch between the various UI panels in the Multi-User Server. The **Sessions** and **Clients** tabs are displayed by default. If you double-click an **Active** or **Archived Session**, a new tab panel will open containing detailed information about that session.

![Multi-User Server UI Tabs](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c13041c7-b80d-431f-a138-f38c5c643e6f/server-interface-tabs.png)

### Command Console and Output Log

The Multi-User Server has an Output Log where you can review logs for information relevant to the operation of the server. You can find errors, warnings, and general diagnostic information that may assist you in troubleshooting the Multi-User Server operation.

![Output Log Filters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/371a55f4-51bf-463a-9dd7-4549ce65bf92/console-and-output-log.png)

Several options are available under the Filters drop-down menu to limit which Output Log entries are visible.

This interface also has a Command Console where you can modify various Console Variables that affect the operation of the Multi-User Server.

## Sessions Information Tab

Similar to the existing Multi-User Browser available in the Unreal Editor, the Multi-User Server has a Sessions Panel where you can examine running and archived sessions.

![Sessions information panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b670c945-6607-4bd3-9005-cb6c3c4b0cd8/sessions-panel.png)

### Toolbar Icons

When an Active or Archived session is selected, you can perform three actions from the toolbar in the Sessions tab.

| Icon | Description |
| --- | --- |
| ![Restore Session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/af8dfbd8-7652-462b-a616-e20373b5f91c/restore-selected.png) | Restore the selected session. |
| ![Archive Session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d2002a8a-562b-4d77-a95b-6fc3b35c8004/archive-selected.png) | Archive the selected session. |
| ![Delete session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d1299533-18b0-4fa1-b344-aa173c369d8a/delete-selected.png) | Delete the selected session if permitted. |

### Active Sessions

All **Active Sessions** on the server are listed here, with summary information about their Server, Project name, Unreal Engine Version, and the Last Modified date. If you right-click an active session you can Archive, Rename, or Delete that session from the context menu.

![Active Session context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/362ced32-e0dc-4417-8e5f-85570eac495c/active-session-context-menu.png)

You can **double-click** an active session to inspect that session in greater detail in a new tab.

### Archived Sessions

All **Archived Sessions** on the server are listed here with the same summary information as above. If you right-click an archived session, you can Restore, Rename or Delete that session from the context menu.

![Archived Session context menu](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecc18b41-3a89-4277-8f38-d1e44f14646e/active-session-context-menu.png)

You can double-click an archived session to inspect it in a new tab.

## Active Session Tab

You can double-click any active session in the Sessions Information Panel to display more information about that session. Information about the session opens in a new tab bearing the name of the session. The information panel of an Active Session has four regions.

![Active Session Panel](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/71d4f255-536c-499c-8dbb-17fa5f592d3a/active-session-panel.png)

1.  Connected Clients
2.  Session History
3.  Transaction Details
4.  Session Content

### Connected Clients

From an active session tab, you can click the **Connected Clients** button to inspect the clients currently connected to that session. The Connected Clients button will take you to the main **Clients** tab, with the content filtered to display only the active connections in that specific session. You can clear the filter and show all clients by using the gear icon in the Clients tab.

### Session History

Once open, the active session tab displays a chronological history of all the individual transactions that occurred during that session. This panel also displays a brief summary of the operation and the Client where the changes originated.

![Session History](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a1224490-3b36-48fb-a5da-a91141999e07/session-history.png)

You can use the search bar to look for specific transactions in the history timeline. Several display filters are available under the gear icon.

![History Filters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/500c2c45-cec5-41be-8e03-aba579dc92f5/history-filters.png)

### Transaction Details

You can select any individual transaction in the Session History and expand the Details section to expose more information about the changes that were made in that transaction.

![Transaction Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e80c6476-48e9-4e25-87c1-b76646fdcc1f/transaction-details.png)

Under **Modified objects and properties** you can hover the mouse over one of the listed items and a tooltip will display precisely which Asset was modified.

### Session Content

![Session Content](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ed0f18a6-76e6-4c29-9843-0832a1a063aa/session-content.png)

The **Session Content** panel lists any changes made to the contents of the project. When new packages are added, they are listed with a plus icon to the left of the package name. This icon changes to a check sign when the package is saved.

## Clients Information Tab

The Clients information tab displays network information about the Multi-User server, and a record of any clients that have participated in a session on that server.

### Clients Table

The Clients table keeps track of all clients that have participated in the server, both connected and disconnected. Clients that are currently connected to an active session in the Multi-User server will display a green swatch in the bottom-left corner of the table. When a client disconnects from the server, the swatch turns gray.

![Clients table](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/592f5c98-ea71-4b8d-b3b3-14daef715acc/clients-table.png)

The client table provides a summary view of the active network data that each client is sending and receiving. You can use the search bar to retrieve information about specific clients. You can also see detailed connection information about a specific client by right-clicking in the corner of the client and selecting one of the options in the context menu.

![Client table Display options](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d22ea1c5-8549-4a3d-a120-46ab26da6866/client-table-display-options.png)

-   **Open Log:** Opens a new tab in which you can view log events related to this client.
-   **Network Graph:** Displays a real time graph of the client's network activity.
-   **Outbound segment table:** An itemized record of all transactions initiated by the client.
-   **Inbound segment table:** An itemized record of all transactions received by the client.

These tables provide information about the active data being sent or received by the client.

| Item | Description |
| --- | --- |
| Sent | Total data sent by the client. |
| Received | Total data received by the client. |
| RTT | Round trip time in milliseconds. |
| Inflight | Current inflight data, waiting to be acknowledged by the receiver. |
| Lost | Information about packet loss. |

This information is extremely useful when diagnosing passible packet loss in high throughput situations. You can identify connections that are unstable, or may be unreachable due to network congestion or configuration.

### Packages Column

The Packages column on the right side of the server window displays package transfer information between clients. This view provides insights about the current transfer of large data to other clients. For example, Level Snapshot data or GPU Lightmass bakes.

![Packages column](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3492326-a051-42fc-901f-6e468903fc5c/packages-column.png)

The time at which the package was sent, size, and revision information is visible. The green checkmark in the **State** column indicates that the package was acknowledged by the receiver to be completely transferred, and therefore should exist on the node. When **Enhanced Logging** is enabled, you can also click the checkmark to determine the exact message that was used to send the package.

### Enhanced Logging

Enhanced logging is available in the the **Server Log** panel at the bottom of the **Clients** tab. Click **Enable logging** in the middle of the Server Log panel to enable Enhanced Logging.

![Enable Enhanced Logging](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4606127b-9a2d-473d-b4ea-997a67439082/enable-enhanced-logging.png)

Enhanced logging displays a detailed view of the current transfer of message between the Multi-User Server and its Clients. It is an inspection of the types of messages transmitted. By default all message types are visible, along with the time it was sent, who sent it, where it was sent, and whether it was acknowledged by the client.

Various filters are available to the left of the search bar in the Server Log panel. Click the dropdown caret icon to display the filters.

![Server Log Filters](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/680ee78d-0f92-43c6-abca-17383b63f751/server-log-filters.png)

Once enhanced logging is enabled in a server, you cannot turn it off. Logging information is written to a CSV file found in the same directory as your server log files. Long sessions can generate very large CSV files, so you should only enable this feature when troubleshooting issues.

## Muting and Deleting Transactions

The Multi-User Server application has the capability for users to edit existing session data, enabling you to mute or delete transactions that were generated by clients. This feature is a useful way to identify and eliminate transactions that may be causing problems with user operation.

### Archiving a Session

To use this feature, you must create an archived copy of the session you wish to edit, and open that archived session in the Multi-User Server. **Right-click** an Active Session in the Sessions tab and select **Archive** in the context menu. Double-click the archived session to open its information panel.

![Archive Session](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/a8c0dda2-7110-40d5-b3c0-3a5a4857bdc0/archive-session.png)

Once the archived session is open, you can select any transaction and mute or delete it.

### Deleting a Transaction

To delete a transaction, right-click it in the archived session and select **Edit** > **Delete** from the context menu.

![Delete Transaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f6dd80a-311a-4e00-9966-04a69cf5b471/delete-transaction.png)

Note that deleting a transaction is destructive and cannot be undone. Muting transactions can achieve a similar effect, but enables you to unmute at a later time. If there is any chance you will want to recover the transaction later, consider muting instead.

### Muting a Transaction

If you mute a transaction in an archived session, that transaction is not replayed when clients rejoin the session after it is unarchived. Muted transactions appear as dimmed entries in the transaction history. To mute a transaction right-click it in the transaction history and select **Mute** from the context menu.

![Mute Transaction](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/016007f6-8013-4b83-b70a-1b507429702e/mute-transaction.png)

This workflow yields essentially the same results as deleting transactions. However you can always unmute transactions at a later time, whereas deleted transactions cannot be recovered. Muting is the recommended workflow for either temporarily or permanently disabling a transaction.

#### Dependency Analysis

When you attempt to mute a transaction, a warning dialog appears to inform you that by muting a transaction there is some risk of disrupting downstream dependencies.

![Mute Transaction Warning](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/13acebe3-3df3-41d3-9cf4-307c9d5d2ddc/caution-muting.png)

Since some transactions may depend on earlier transactions, muting or deleting always requires a dependency analysis on the transaction history. This process is automatic, and will find transactions that relate to one another. Dependency analysis is not infallible, and in some cases it is indeterminate whether or not a transaction depends on another. In those cases you are given the option to include or exclude the transaction. In most cases it is best to err on the side of caution.