# Storage and Replication

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-storage-and-replication-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/mutable-storage-and-replication-in-unreal-engine)  
**Processed:** 2025-06-14 16:37:56

---

As explained in the [Mutable Overview](/documentation/en-us/unreal-engine/mutable-overview-in-unreal-engine), Customizable Object assets contain all the data to generate all possible combinations of an object. One single combination is represented by a Customizable ObjectI nstance asset, which contains only a reference to a Customizable Object and the values for each of the parameters it exposes.

There are 2 use cases for this data:

-   **Persistent storage**: for example to store in disk when an instance is created in the editor for a fixed NPC, or in-game, when a player customizes its character and the game wants to save it for another session.
-   **Transient usage**: for instance if you want to transmit it through the network from a client to the server or to other clients.

The requirements are slightly different in each case.

## Persistent Storage

In this case, you need the instance parameters to be valid even if the Customizable Object changes (it is extended, patched or updated) from session to session. For this reason you need this data to be as portable as possible.

If the Customizable Object changes it may be one of the following:

-   A new parameter is added. In which case, not having it would set it to the default value in the Customizable Object, which should be set to something reasonable.
-   A parameter is removed. No problem here, only some useless data to be removed.
-   A parameter changes name. The CustomizableO bject parameters have a UID that can be used to be able to adapt data in this case.
-   The values of an enum parameter change. This is similar to a parameter change, since there are UIDs for each of the possible values that can be used to match the new object.

Most projects choose to implement their own data structures and storage to implement this description, and they feed it to Customizable Object Instances from game code, but for in-editor creation the Customizable Object Instance asset handles the parameters in this way.

## Transient usage

In this case, you want the data to be as small as possible. If the Customizable Object is not going to change, you can use the **Compact Descriptor**. This assumes that the number of parameters and their order is not going to change. Also, default parameters values are not serialized.

This is important because it allows the description to be more than 100x smaller in some cases. If you have 100 players and each of them can find each other, there are 10,000 potential transmissions happening, without even accounting for in-game changes to instances. If the description is 1KB instead of 100KB, you can save a lot of bandwidth each game.

`void FCustomizableObjectInstanceDescriptor::SaveDescriptor(FArchive& Ar, bool bUseCompactDescriptor)`