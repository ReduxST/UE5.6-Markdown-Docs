# Online User Interface

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-user-interface-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-user-interface-in-unreal-engine)  
**Processed:** 2025-06-14 16:39:57

---

The **OnlineUser Interface** is the central repository for all cached information and metadata about users, both remote and local. This interface also provides reverse-lookup functionality, enabling developers to search for user IDs based on their display names or email addresses and map them back to Unreal Engine's native `FUniqueId` system.

## Retrieving and Examining User Metadata

To access user metadata, you must first request and cache that data from the online service. Call `QueryUserInfo` with a list of `FUniqueNetId` values for the users whose information you want, as well as the index of the local user making the request. This is an asynchronous process, and will call a delegate of type `OnQueryUserInfoComplete` when it finishes. After a successful query populates the cache with user information, the `GetAllUserInfo` function will return all collected data. If you have the `FUniqueNetId` of a specific user whose data you want, you can call `GetUserInfo` with that `FUniqueNetId` to get just that user's data.

## Mapping External User IDs

Most online services support searching for users by their display names or email addresses. The OnlineUser Interface mirrors this functionality with `QueryUserIdMapping`, which takes a display name or email address and attempts to map it, through the online service, to an `FUniqueNetId`. Since this procedure involves contacting the online service, it is asynchronous, and will call `FOnQueryUserMappingComplete` upon completion. Unlike most information requests, this function does not update a cache. Instead, when the operation is successful, the delegate's payload will contain the known display name or email address that was searched, and the resulting `FUniqueNetId` that the online service found.