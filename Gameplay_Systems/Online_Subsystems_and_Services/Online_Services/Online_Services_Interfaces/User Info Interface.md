# User Info Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/user-info-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/user-info-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:57:55

---

The **Online Services User Info Interface** provides you with tools to retrieve user information from an online service such as Steam or Epic Online Services for display in your game. This includes a player's:

-   Platform Profile.
-   Display Name.
-   Avatar.

## API Overview

### Functions

The following table provides a high-level overview of the functions provided by the User Info Interface:

| **Function** | **Description** |
| --- | --- |
| **User Information** |   |
| [`QueryUserInfo`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserInfo/QueryUserInfo) | Query user info for the list of account IDs. |
| [`GetUserInfo`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserInfo/GetUserInfo) | Retrieve the user info for the account ID previously cached by `QueryUserInfo`. |
| **User Avatar** |   |
| [`QueryUserAvatar`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserInfo/QueryUserAvatar) | Query user avatars for the list of account IDs. |
| [`GetUserAvatar`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserInfo/GetUserAvatar) | Retrieve the user avatar for the account ID previously cached by `QueryUserAvatar`. |
| **Platform UI** |   |
| [`ShowUserProfile`](/documentation/en-us/unreal-engine/API/Plugins/OnlineServicesInterface/Online/IUserInfo/ShowUserProfile) | Show the profile UI for the provided account ID. |

## Access User Info

Accessing user information with the User Info Interface works similarly to the other [Online Services Interfaces](/documentation/en-us/unreal-engine/online-services-interfaces-in-unreal-engine).

`QueryUserInfo` caches the list of user display names associated with their corresponding account ID with the interface. `QueryUserInfo` requires you to provide the list of user account IDs for which you want to access display names as parameters. To access each user's display name, call `GetUserInfo` using their account ID.

## Access User Avatar

The workflow defined in the [Access User Info](/documentation/en-us/unreal-engine/user-info-interface-in-unreal-engine#accessuserinfo) section applies to accessing a user's avatar as well. `QueryUserAvatar` caches the information with the interface. `GetUserAvatar` retrieves each avatar individually.

## Platform User Profile

`ShowUserProfile` brings up the platform service's profile user interface for the provided user. Platform service profiles are specific to the platform on which the user is currently playing your game. Consult your platform service's documentation for more information on the profile user interface.

## More Information

### Header File

Consult the `UserInfo.h` header file directly for more information as needed. The User Info Interface header file `UserInfo.h` is located in the directory:

```
`Engine\Plugins\Online\OnlineServices\Source\OnlineServicesInterface\Public\Online`
Copy full snippet
```
Engine\\Plugins\\Online\\OnlineServices\\Source\\OnlineServicesInterface\\Public\\Online

For instructions on how to obtain the UE source code, see our documentation on [Downloading Unreal Engine Source Code](/documentation/en-us/unreal-engine/downloading-source-code-in-unreal-engine).

### Function Parameters and Return Types

See the [Functions](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine#functions) section of the [Online Services Overview](/documentation/en-us/unreal-engine/overview-of-online-services-in-unreal-engine) page for an explanation of function parameters and return types, including how to pass parameters and how to process the results when functions return.