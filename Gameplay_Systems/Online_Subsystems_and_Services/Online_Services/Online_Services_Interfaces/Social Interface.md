# Social Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/social-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/social-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:51:23

---

The **Online Services Social Interface** manages relationships between users. This includes:

-   Retrieving and viewing a player's friends list.
-   Sending friend invites.
-   Accepting/Rejecting friend invites.
-   Viewing a list of blocked players.
-   Blocking other players.

## API Overview

### Functions

The following table provides a high-level overview of the functions provided by the social interface:

| **Function** | **Description** |
| --- | --- |
| **View** |   |
| [`QueryFriends`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/QueryFriends) | Query the player's friends list. |
| [`GetFriends`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/GetFriends) | Retrieve a friends list cached by `QueryFriends`. |
| **Invite** |   |
| [`SendFriendInvite`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/SendFriendInvite) | Send a friend invite. |
| [`AcceptFriendInvite`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/AcceptFriendInvite) | Accept a friend invite. |
| [`RejectFriendInvite`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/RejectFriendInvite) | Reject a friend invite. |
| **Block** |   |
| [`QueryBlockedUsers`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/QueryBlockedUsers) | Query the blocked users list. |
| [`GetBlockedUsers`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/GetBlockedUsers) | Retrieve blocked users list cached by `QueryBlockedUsers`. |
| [`BlockUser`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/BlockUser) | Block a specified user. |
| **Event Listening** |   |
| [`OnRelationshipUpdated`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/ISocial/OnRelationshipUpdated) | Event triggered by updating friends list. |

### Primary Struct

The social interface communicates its functionality primarily through the [`FFriend`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/FFriend) struct in addition to the function specific structs for passing parameters and return values.

#### FFriend

| **Member** | **Type** | **Description** |
| --- | --- | --- |
| `FriendId` | `FAccountId` | Account ID of this friend. |
| `DisplayName` | `FString` | Display the name of this friend. |
| `Nickname` | `FString` | 
Local nickname for this friend.

Consult the documentation for your platform's online services for availability.



 |
| `Relationship` | `ERelationship` | Relationship to this friend. |

### Enumerated Classes

The [`ERelationship`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/UE__Online__ERelationship) enumerated class holds the relationship status between the local user and the online user represented by the `FFriend` struct through which it is accessed.

#### ERelationship

| **Value** | **Description** |
| --- | --- |
| `Friend` | Friend |
| `NotFriend` | Not a friend |
| `InviteSent` | Invite sent to a user. |
| `InviteReceived` | Invite received from a user. |
| `Blocked` | Local user has blocked this user. |

## Process Flow

### View Friends

Upon starting your game, the player views which friends are online. To accomplish this, `QueryFriends` caches the player's friends list with the social interface, then `GetFriends` retrieves the previously cached friends list for reading. The player can now view their friends list to decide whether to invite their friends to join a lobby and enter a game session together.

### Invite Friends

After playing with their friends and other online players, the player meets several other players they enjoy playing with. The player decides to send friend invites to two of these online players. `SendFriendInvite` sends a friendship invitation to a single provided player each time it is called. One of the online players sees the invitation and rejects it. The game calls `RejectFriendInvite` to reject the player's invitation.

Meanwhile, the second online player accepts the invitation. A call to `AcceptFriendInvite` accepts the player's invitation. This friendship acceptance triggers an `OnRelationshipUpdated` event for both the player who sent the invitation and the online player who accepted the invitation.

### Block Users

While playing with their new friend, the player meets another online player. This time, the player decides they do not wish to interact with this online player in the future. The player proceeds to block this online player. The player can see the online players they have blocked by querying their blocked list. `QueryBlockedUsers` caches the information in the interface and a subsequent call to `GetBlockedUsers` retrieves the list of blocked players. If the online player in question does not appear in this list, a call to `BlockUser` adds the online player to the player's blocked list.

Depending on your platform, the Invite and Block APIs may bring up a platform dialogue to perform the associated action. Consult the documentation for your particular platform for more information.

## Converting Code from Online Subsystem

The Online Services Social Interface is responsible for all code previously handled by the [Online Subsystem](/documentation/en-us/unreal-engine/online-subsystem-in-unreal-engine) [Friends Interface](/documentation/en-us/unreal-engine/online-subsystem-friends-interface-in-unreal-engine).

## More Information

### Header File

Consult the `Social.h` header file directly for more information as needed. The social interface header file `Social.h` is located in the directory:

```
`Engine\Plugins\Online\OnlineServices\Source\OnlineServicesInterface\Public\Online`
Copy full snippet
```
Engine\\Plugins\\Online\\OnlineServices\\Source\\OnlineServicesInterface\\Public\\Online

For instructions on how to obtain the UE source code, see our documentation on [Downloading Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).

### Function Parameters and Return Types

See the [Functions](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine#functions) section of the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) page for an explanation of function parameters and return types, including how to pass parameters and processing the results when functions return.