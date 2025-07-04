# Replay System

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-replay-system-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/using-the-replay-system-in-unreal-engine)  
**Processed:** 2025-06-14 17:01:52

---

**Unreal Engine (UE)** features a **Replay** system which can record gameplay for later viewing. This feature is available in all games, from live, multiplayer games played on dedicated servers, to single-player games, and even including Play-In-Editor sessions. At a high level, the Replay system works by using a `DemoNetDriver` to read data drawn from the built-in replication system, similar to how a `NetDriver` operates in a live, networked gameplay environment. Even if a project doesn't have a multiplayer mode, any project set up to replicate data is compatible with the Replay System without the need for further modification.

The way this works involves the `DemoNetDriver` passing network data to a Replay Streamer, which handles the process of filtering and storing the data. When viewing a replay, a `DemoNetDriver` will have access to all of the replicated information that was available during live play (as well as special data fields designated as relevant only to replays) so that it can reconstruct the events of the game from this data.

## Replay System Functionality

The basic functions of the replay system are to start or stop recording a demo, or play back a previously-recorded demo. While in playback mode, the Replay system supports commands to pause, change the playback speed, or jump to a specific point in time. More advanced usage of the system can include adding text tags (usually meta tags or the names of players involved in the game) to a replay, or querying existing replays based on text tags or version information present. The Replay system can be used from C++ code, mainly via the `UGameInstance` and `UWorld` classes, or with console commands or command-line arguments.

| Function Or Variable Name | Equivalent Console Command | Effect |
| --- | --- | --- |
| `UGameInstance::StartRecordingReplay` | "demorec (ReplayName)" | Begins recording a replay. If the (ReplayName) parameter is not supplied, the replay system can generate a name on its own. |
| `UGameInstance::StopRecordingReplay` | "demostop" | Stops a replay currently being recorded. |
| `UGameInstance::PlayReplay` | "demoplay (ReplayName)" | Plays the named replay. |
| `UDemoNetDriver::GotoTimeInSeconds` | "demoscrub (ReplayTime)" | Jumps to the provided time (in seconds) in the replay. |
| `UWorld::Pauser` (variable) | "demopause" | The World's `DemoNetDriver->ServerConnection` has an `OwningActor` variable. Setting `Pauser` to that value will pause the replay. Setting it back to `null` will resume the replay. The "demopause" console command will automatically set or clear that variable. |
| `WorldSettings->DemoPlayTimeDilation` (variable) | "demospeed (ReplaySpeed)" | Speeds up or slows down playback by setting the time-scaling factor. A value of 1.0 is normal speed. |
| `AGameMode::bHandleDedicatedServerReplays` (variable) | N/A | Setting this variable to `true` causes dedicated servers to record games automatically. |

## DemoNetDriver and Streamers

The `DemoNetDriver` is a specialized network driver that passes replicated data to **Streamers**, which record the information for later playback. For details on the features of the `DemoNetDriver` and the Streamers included with the Engine, please see the [DemoNetDriver and Streamers](/documentation/en-us/unreal-engine/demonetdriver-and-streamers-in-unreal-engine) page.

## Backward Compatibility

Backward compatibility is supported by the Replay system, starting in version 4.13. This means you can make modifications to a build, such as adding or removing replicated properties, and still load and view replays that were recorded with the original build. In most cases, this is handled automatically, as the Replay system will skip over old replicated fields that have been removed, or use defaults for new replicated fields that have been added. Note that structures with `NetSerialize` overridden will require these differences in data format to be handled manually.

To this end, `FArchive` now provides the `EngineNetVer` and `GameNetVer` functions, which identify the engine and game version, respectively, enabling you to adjust replay data as it comes in so that it fits with your current build. The delegate `GetLocalNetworkVersionOverride` in `FNetworkVersion` can be bound to a function that returns a `uint32` version number of your choosing. In case exact matches are not required for compatibility, `FNetworkVersion` has a delegate called `IsNetworkCompatibleOverride` that can be overridden to perform the comparison between two version numbers and decide if they are compatible.