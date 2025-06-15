# Console Commands

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/console-commands-for-network-debugging-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/console-commands-for-network-debugging-in-unreal-engine)  
**Processed:** 2025-06-14 16:15:03

---

# Console Commands for Network Debugging

**Unreal Engine (UE)** includes several [console variables](/documentation/en-us/unreal-engine/console-variables-editor) and [commands](/documentation/en-us/unreal-engine/console-variables-cplusplus-in-unreal-engine) that are useful for debugging networked games.

## Networking

### Console Variables

Networking console variables customize how Unreal Engine’s networking and replication systems behave. Networking console variables begin with either the `net.` (networking) or `p.net.` (networked physics) prefixes.

| **Variable** | **Description** | **Arguments** |
| --- | --- | --- |
| `net.ActorChannelPool` | If enabled, actor channels are pooled to save memory and object creation cost. | 0: disabled, 1: enabled (default) |
| `net.AllowAsyncLoading` | 
Allow async loading of unloaded assets referenced in packets. If disabled, the client hitches and immediately loads the asset. If enabled, the packet is delayed while the asset is async loaded.

`net.DelayUnmappedRPCs` can be enabled to delay RPCs relying on async loading assets.



 | 0: disabled (default), 1: enabled |
| `net.AllowClientRemapCacheObject` | When enabled, allow clients to remap read-only cache objects and keep the same NetGUID. | false: disabled (default), true: enabled |
| `net.AllowEncryption` | If 1, the engine attempts to load an encryption Packet Handler component and fill in the Encryption Token parameter of the `NMT_Hello` message based on the `?EncryptionToken` URL command-line option and callbacks if non-empty. If 2, make the Encryption Token required (this is enforced server-side). | 0: disabled, 1: enabled (default), 2: required |
| `net.AllowPIESeamlessTravel` | If enabled, allow seamless travels in single-process Play In Editor (PIE). | false: disabled (default), true: enabled |
| `net.AllowReliableMulticastToNonRelevantChannels` | If enabled, allow reliable server multicasts to be sent to non-relevant actors as long as there is an existing actor channel. | 0: disabled, 1: enabled |
| `net.AllowRPCDoSDetectionBlocking` | Override whether RPC DoS Detection RPC blocking is enabled. | 0: disabled, 1: enabled |
| `net.AllowRPCDosDetectionKicking` | Override whether RPC DoS Detection kicking is enabled. | 0: disabled, 1: enabled |
| `net.AlwaysUpdateGuidReferenceMapForNetSerializeObjectStruct` | 

If enabled, entries in the GuidReferenceMap for NetSerialize struct properties with object properties will always be updated, not just when the Guid changes or goes null. This should prevent issues with old property data being applied when an unmapped actor reference in the struct is mapped.

This command also requires `net.TrackNetSerializeObjectReferences 1`.



 | false: disabled, true: enabled |
| `net.BitReader.EnsureOnOverflow` | If enabled, ensure that, if BitReader overflows, then `BitReader.LogFatalOnOverflow` takes precedence over this. | 0: disabled, 1: enabled |
| `net.BlockSend` | If enabled, block packet sends on `NetConnection`s. | 0: disabled (default), 1: enabled |
| `net.CheckNoLoadPackages` | If enabled, check the no load flag in `GetObjectFromNetGUID` before forcing a sync load on packages that are not marked `IsFullyLoaded`. | false: disabled, true: enabled |
| `net.CheckPushBPRepIndexAgainstName` | If enabled, validates that Blueprint generated values passed to `MarkPropertyDirtyFromRepIndex` match the actual property data. | false: disabled, true: enabled |
| `net.ClientToServerUnreliableRPCQueueSize` | Maximum number of unreliable RPCs queued for sending from the client to the server. If more RPCs are queued, then older ones are dropped. | `<VALUE>`: Number of RPCs (default 16) |
| `net.CloseTimingDebug` | Logs the last packet send/receive and TickFlush/TickDispatch times on connection close for debugging blocked send/recv paths. | 0: disabled (default), 1: enabled |
| `net.ContextDebug` | Debugging option to set a context string during replication. | 0: disabled (default), 1: enabled |
| `net.ControlChannelDestructionInfo` | If enabled, send destruction information updates via the control channel instead of creating a new actor channel. | 0: use actor channel (default), 1: use control channel |
| `net.CurrentHandshakeVersion` | The current, supported, stateless handshake protocol version. | `<INTEGER>`: Version (default 4) |
| `net.DebugAppendResolverAddress` | If this is set, all IP address resolution methods add the value of this Console Variable to the list of results. This allows testing resolution functionality across multiple addresses with the end goal of having a successful result. | `<STRING>`: Address (default "") |
| `net.DebugDraw` | Draw debug information for network dormancy and relevancy. | 0: disabled (default), 1: enabled |
| `net.DebugDrawCullDistance` | Cull distance for `net.DebugDraw` in world units. The maximum world units an actor can be away from the local view to draw its dormancy status. Zero disables culling. | `<FLOAT>`: Distance (default 0.0) |
| `net.DebugDualIPs` | If enabled, duplicate every packet received, then process with a new, deterministic IP to emulate receiving client packets from dual IPs. | 0: disabled (default), 1: enabled |
| `net.DebugInitialConnect` | If enabled, periodically log socket-level send stats client-side until a packet is successfully received to verify connection. | 0: disabled, 1: enabled (default) |
| `net.DebugInitialConnectLogFrequency` | The amount of time (in seconds) between initial connect debug logging. | `<FLOAT>`: Seconds (default 10.0) |
| `net.DelayUnmappedRPCs` | If enabled, delay received RPCs with unmapped object references until they are received or loaded. If disabled, RPCs execute immediately with null parameters. This can be used with `net.AllowAsyncLoading` to avoid null asset parameters during async loads. | 0: disabled (default), 1: enabled |
| `net.DelinquencyNumberOfTopOffendersToTrack` | The number of “Top Offenders” tracked by the PackageMap and GuidCache for queued actors and async loads, respectively. `net.TrackAsyncLoadingGUIDThreshold` and `net.TrackQueuedActorThreshold` still dictates whether or not any of these items are tracked. | `<INTEGER>`: Number (default 10) |
| `net.DeltaInitialFastArrayElements` | If enabled, send delta struct changelists for initial fast array elements. | false: disabled (default), true: enabled |
| `net.DisableBandwithThrottling` | If enabled, force IsNetReady to always return true. Not available in shipping builds. | 0: disabled (default), 1: enabled |
| `net.DisableIPv6` | If enabled, IPv6 will not resolve and its usage will be avoided when possible. | 0: disabled , 1: enabled (default) |
| `net.DisableRemapScriptActors` | If enabled, disable name remapping of compiled script actors for networking. | 0: disabled (default), 1: enabled |
| `net.DiscardTornOffActorRPCs` | If enabled, discard RPCs if the actor has been torn off. | false: disabled, true: enabled (default) |
| `net.DoHandshakeVersionFallback` | If enabled, perform randomized falling-back to previous version of the handshake protocol client-side upon failure. | 0: disabled (default), 1: enabled |
| `net.DoPacketOrderCorrection` | If enabled, try to fix “out of order” packet sequences by caching packets and waiting for the missing sequence. | 0: disabled, 1: enabled (default) |
| `net.DoPropertyChecksum` | If enabled and `ENABLE_PROPERTY_CHECKSHUMS` is defined, checksums of replicated properties are compared on client and server. | 0: disabled (default), 1: enabled |
| `net.DormancyEnable` | If enabled, use the network dormancy system to reduce CPU and bandwidth overhead for infrequently updated actors. | 0: disabled , 1: enabled (default) |
| `net.DormancyHysteresis` | The time (in seconds) the system waits before letting a channel become fully dormant. This can prevent churn when objects are going in and out of dormant more frequently than normal. | `<FLOAT>`: Seconds (default 0.0) |
| `net.DormancyValidate` | If enabled (value 1 or 2), validates that dormant actors do not change state while in a dormant state (on the server only). | 0: disabled (default), 1: validate on wake up, 2: validate each net update |
| `net.EnableCongestionControl` | If enabled, use the congestion control module. | 0: disabled (default), 1: enabled |
| `net.EnableDetailedScopeCounters` | If enabled, use detailed networking scope cycle counters. There are often lots of these, which can negatively impact performance. | false: disabled, true: enabled (default) |
| `net.EnableNetInitialSubObjects` | If enabled, set `bNetInitial` to true on new sub objects to make sure all replicated properties are replicated. | false: disabled, true: enabled (default) |
| `net.FilterGuidRemapping` | If enabled, remove destroyed and parent GUIDs from the unmapped GUID list. | 0: disabled, 1: enabled (default) |
| `net.ForceNetFlush` | 

If enabled, immediately flush the send buffer when written to. This helps trace packet writes.

May be unstable.



 | 0: disabled (default), 1: enabled |
| `net.HandshakeEnforceNetworkCLVersion` | If enabled, the stateless handshake enforces the network CL version, instead of the higher level netcode. | 0: disabled (default), 1: enabled |
| `net.HandshakeResendInterval` | Delay between resending handshake packets which we have not received a response for. | `<FLOAT>`: Time (default 1.0) |
| `net.IgnoreNetworkChecksumMismatch` | If enabled, the integrity checksum on package map objects is ignored. This can cause issues with out of sync data. | 0: disabled (default), 1: enabled |
| `net.InstantReplayProcessQueuedBunchesMillisecondLimit` | Time threshold for processing queued bunches during instant replays. If it takes longer than this in a single frame, wait until the next frame to continue processing queued bunches. For unlimited time, set this to 0. | `<INTEGER>`: Milliseconds (default 8) |
| `net.IpConnectionDisableResolution` | If enabled, any future IP connections do not use resolution methods. | 0: disabled (default), 1: enabled |
| `net.IpConnectionUseSendTasks` | If enabled, the IP connection calls the socket’s `SendTo` function in a task graph so that it can run off the game thread. | 0: disabled (default), 1: enabled |
| `net.IpNetDriverReceiveThreadPollTimeMS` | If `net.IpNetDriverUseReceiveThread` is enabled, the number of milliseconds to use as a timeout value for `FSocket::Wait` on the receive thread. A negative value means to wait indefinitely. `FSocket::Shutdown` cancels the indefinite wait. | `<INTEGER>`: Milliseconds (default 250) |
| `net.IpNetDriverReceiveThreadQueueMaxPackets` | If `net.IpNetDriverUseReceiveThread` is enabled, the maximum number of packets that can be waiting in the queue. Additional packets received are dropped. | `<INTEGER>`: Packets (default 1024) |
| `net.IpNetDriverUseReceiveThread` | If enabled, the IP Net Driver calls the socket’s `RecvFrom` function on a separate thread (not the game thread). | 0: disabled (default), 1: enabled |
| `net.IsPushModelEnabled` | If enabled, use push model mode. Push model networking mode allows game code to notify the networking system of changes rather than scraping. | false: disabled (default), true: enabled |
| `net.LogPendingGuidsOnShutdown` | If enabled, log pending GUIDs on shutdown. | false: disabled (default), true: enabled |
| `net.LogSkippedRepNotifies` | If enabled, log when the networking code skips calling a RepNotify client-side due to the property value not changing. | 0: disabled (default), 1: enabled |
| `net.LogUnhandledFaults` | 

Warning level for unhandled net faults.

Unhandled net faults might be deliberate depending on implementation.



 | 0: disabled, 1: enabled (log once), 2: enabled (log always) |
| `net.MagicHeader` | 

String representing binary bits that are prepended to every packet sent by the game.

Maximum length is 32 bits.



 | `<STRING>`: Bits string (default “”) |
| `net.MakeBpPropertiesPushModel` | If enabled, properties declared in Blueprints are forced to use push model mode. | false: disabled, true: enabled (default) |
| `net.MaxAggregateIPLogs` | 

Maximum number of IP addresses to include in aggregated pre-connection logging before such logging is disabled altogether.

Minimum is 1 and maximum is 128.



 | `<INTEGER>`: Number of IPs (default 16) |
| `net.MaxChannelSize` | 

Maximum number of network channels allowed across the entire server.

If non-positive, the connection `DefaultMaxChannelSize` is used.



 | `<INTEGER>`: Channels (default: 0) |
| `net.MaxClientGuidRemaps` | Maximum number of client resolves of unmapped network GUIDs per tick. | `<INTEGER>`: Number of Resolves (default: 100) |
| `net.MaxConnectionsToTickPerServerFrame` | 

Maximum number of channels that will have changes replicated to them per server update.

No effect when non-positive.



 | `<INTEGER>`: Number of Channels (default: 0) |
| `net.MaxConstructedPartialBunchSizeBytes` | Maximum size allowed for partial bunches. | `<INTEGER>`: Size of Bunch (default: 65536) |
| `net.MaxIPHitLogs` | 

Maximum number of times to individually log a specific IP pre-connection, before aggregating further logs.

Minimum is 0 and maximum is max value of `int32`.



 | `<INTEGER>`: Number of Logs (default: 4) |
| `net.MaxNetStringSize` | Maximum size for strings sent/received by the network code in bytes. | `<INTEGER>`: Number of bytes (default: 16777216) |
| `net.MaxNumberOfAllowedTArrayChangesPerUpdate` | Maximum number of allowed `TArray` changes per update. | `<INTEGER>`: Number of changes (default: 2048) |
| `net.MaxNumberOfAllowedTArrayDeletionsPerUpdate` | Maximum number of allowed `TArray` deletions per update. | `<INTEGER>`: Number of deletions (default: 2048) |
| `net.MaxPlayersOverride` | Maximum number of players. Overrides the standard maximum players count. Useful for testing full servers. | `<INTEGER>`: Number of players (default: 0) |
| `net.MaxRPCPerNetUpdate` | Maximum number of unreliable multicast RPC calls allowed per network update, additional ones are dropped. | `<INTEGER>`: Number of RPCs (default: 2) |
| `net.MaxSerializedNetExportGroups` | Maximum number of network export groups we would expect to receive in a bunch. | `<INTEGER>`: Number of groups (default: 65536) |
| `net.MaxSerializedNetExportsPerGroup` | Maximum number of network exports in each group we would expect to receive in a bunch. | `<INTEGER>`: Number of exports (default: 131072) |
| `net.MaxSerializedNetGuids` | Maximum number of network GUIDs we would expect to receive in a bunch. | `<INTEGER>`: Number of GUIDs (default: 2048) |
| `net.MaxSerializedReplayNetGuids` | Maximum number of network GUIDs we would expect to receive in replay export data. | `<INTEGER>`: Number of GUIDs (default: 32768) |
| `net.MaxSimultaneousObjectsWithRPCs` | Maximum number of objects that can have unsent RPCs at the same time. | `<INTEGER>`: Number of Objects (default: 4096) |
| `net.MinHandshakeVersion` | 

Minimum stateless handshake protocol version.

See `StatelessConnectHandlerComponent.h` for more information about `EHandshakeVersion`.



 | `<INTEGER>`: Handshake version (default: 4) |
| `net.Montage.Debug` | Print replication information about animation montages. | 0: no print (default), 1: print on client side |
| `net.NetFaultRecoveryLogQuotaChecks` | If enabled, debug logging for quota checks. Useful for debugging new network faults used with `RegisterCounterCategory`. | false: disabled, true: enabled |
| `net.NetGuidCacheHistoryEnabled` | 

If enabled, allows logging of `NetGUIDCache` history.

This can consume a large amount of memory that will not be freed until the cache is destroyed.



 | 0: disabled, 1: enabled |
| `net.NetPingDebugDump` | If enabled, dump `NetPing` ping values to the log every 5 seconds. | 0: disabled, 1: enabled |
| `net.NetPingEnabled` | Enable or disable the `NetPing` ping handling interface used for centralized ping tracking and ICMP/UDP ping. | 0: disabled, 1: enabled for client, 2: enabled for server and client, 3: enabled for server only |
| `net.NetPingICMPInterval` | Specify the interval (in seconds) for performing ICMP pings. | `<INTEGER>`: Time (default: 5) |
| `net.NetPingTimeoutDisableThreshold` | Number of times to send an ICMP/UDP ping when at a failure/timeout rate of 100% before giving up and disabling pings. | `<INTEGER>`: Number of attempts (default: 15) |
| `net.NetPingTypes` | 

A comma-delimited list of `EPingType` pings to enable, and (optionally) the `EPingAverageType` averaging to apply to the ping.

An example usage of this is: `net.NetPingTypes="RoundTrip=None,RoundTripExclFrame=PlayerStateAvg,ICMP=MovingAverage"`. See `NetPing.h` for more information about `EPingType` and `EPingAverageType`.



 | Comma-delimited list |
| `net.NetPingUDPInterval` | Specify the interval (in seconds) for performing UDP pings. | `<INTEGER>`: Time (default: 5) |
| `net.NetPingUDPPort` | Set the port used for pinging the `UDPQoS` ping type. | `<INTEGER>`: Port Number (default: 22222) |
| `net.NetServerMoveTimestampExpiredWarningThreshold` | Tolerance for `ServerMove` to warn when client moves are expired more than this time threshold behind the server. | `<FLOAT>`: Time (default: 1) |
| `net.OodleClientEnableMode` | 

When to enable compression on the client.

This setting overrides the `ClientEnableMode` engine configuration setting.



 | `<STRING>`: Mode (default: "") |
| `net.OodleMinSizeForCompression` | 

Minimum size that an outgoing packet must be for it to be considered for compression.

This does not count overhead for handler components which process packets after Oodle.



 | `<INTEGER>`: Size (default: 0) |
| `net.OodleNetwork.TimeGuardLimit` | Set the maximum number of `OodleNetworkHandlerComponent` timeguard logs. | `<INTEGER>`: Number of logs (default: 20) |
| `net.OodleNetwork.TimeGuardThresholdMS` | Threshold (in milliseconds) for the `OodleNetworkHandlerComponent` timeguard. | `<FLOAT>`: Time in MS (default: 0.0) |
| `net.OodleServerEnableMode` | 

When to enable compression on the server.

This setting overrides the `ServerEnableMode` engine configuration setting.



 | `<STRING>`: Mode (default: "") |
| `net.OptimizedRemapping` | Use optimized path to remap unmapped network GUIDs. | 0: disabled, 1: enabled |
| `net.PackageMap.DebugAll` | Debug `PackageMap` serialization for all objects. | 0: disabled, 1: enabled |
| `net.PackageMap.DebugObject` | Debug `PackageMap` serialization of the provided object. | `<STRING>`: Name of object (default: "") |
| `net.PackageMap.LongLoadThreshold` | Threshold time (in seconds) for printing long load warnings in object serialization. | `<FLOAT>`: Time in seconds (default: 0.2) |
| `net.PacketHandlerCRCDump` | If enabled, dump packet CRC’s for debugging for every `HandlerComponent`, incoming and outgoing. | 0: disabled, 1: enabled |
| `net.PacketHandlerTimeguardLimit` | Maximum number of `HandlerComponent` timeguard logs. | `<INTEGER>`: Number of logs (default: 20) |
| `net.PacketHandlerTimeguardThresholdMS` | Threshold (in milliseconds) for the `HandlerComponent` timeguard, incoming and outgoing. | `<FLOAT>`: Time in milliseconds (default: 0) |
| `net.PacketOrderCorrectionEnableThreshold` | Number of "out of order" packet sequences that need to occur before correction is enabled. | `<INTEGER>`: Number of sequences (default: 1) |
| `net.PacketOrderMaxCachedPackets` | 

Maximum number of packets to cache while waiting for missing packet sequences before treating missing packets as lost.

This number must be a power of 2.



 | `<INTEGER>`: Number of packets (default: `2^5 == 32`) |
| `net.PacketOrderMaxMissingPackets` | Maximum number of missed packet sequences that are allowed before treating missing packets as lost. | `<INTEGER>`: Number of sequences (default: 3) |
| `net.PartialBunchReliableThreshold` | If a bunch is broken up into this many or more partial bunches, send it reliable even if the original bunch was not reliable. Partial bunches are atomic and must all make it over to be used. | `<INTEGER>`: Number of partial bunches (default: 8) |
| `net.PingDisplayServerTime` | 

Show server frame time.

Not available in shipping builds.



 | 0: disabled, 1: enabled |
| `net.PingExcludeFrameTime` | If enabled, game frame times are subtracted from calculated ping to approximate actual network ping. | 0: disabled, 1: enabled |
| `net.PingUsePacketRecvTime` | 

Use the operating system or receive thread packet receive time for calculating ping.

This excludes frame time.



 | 0: disabled, 1: enabled |
| `net.ProcessQueuedBunchesMillisecondLimit` | 

Time threshold for processing queued bunches. If it takes longer than this in a single frame, wait until the next frame to continue processing queued bunches.

To use unlimited time, set to 0.



 | `<INTEGER>`: Time in milliseconds (default: 30) |
| `net.ProfilerUseComparisonTracking` | Use comparison tracking. | 0: disabled, 1: enabled |
| `net.PushModelSkipUndirtiedFastArrays` | If enabled, include fast arrays when skipping objects that we can safely see aren’t dirty. | false: disabled, true: enabled |
| `net.PushModelSkipUndirtiedReplication` | If enabled, skip replicating any objects that we can safely see aren’t dirty. | false: disabled, true: enabled |
| `net.PushModelValidateProperties` | If enabled, compare all push model properties and warn if they haven’t been properly marked dirty. | false: disabled, true: enabled |
| `net.PushModelValidateSkipUpdate` | If enabled, detect when we thought we could skip an object replication based on push model state, but we sent data anyway. | false: disabled, true: enabled |
| `net.QuantizeActorLocationOnSpawn` | If enabled, quantize location for newly spawned actors to a single decimal point of precision. | false: disabled, true: enabled (default) |
| `net.QuantizeActorRotationOnSpawn` | If enabled, quantize rotation for newly spawned actors to a single decimal point of precision. | false: disabled, true: enabled (default) |
| `net.QuantizeActorScaleOnSpawn` | If enabled, quantize scale for newly spawned actors to a single decimal point of precision. | false: disabled (default), true: enabled |
| `net.QuantizeActorVelocityOnSpawn` | If enabled, quantize velocity for newly spawned actors to a single decimal point of precision. | false: disabled, true: enabled (default) |
| `net.QueuedBunchTimeoutSeconds` | Time (in seconds) to wait for queued bunches on a channel to flush before logging a warning. | `<FLOAT>`: Time in seconds (default: 30) |
| `net.RandomizeSequence` | 

Randomize initial packet sequence.

This can help provide some obfuscation.



 | 0: disabled, 1: enabled |
| `net.RcvThreadShouldSleepForLongRecvErrors` | Whether or not the receive thread should sleep for `RecvFrom` errors which are expected to last a long time. | 0: don’t sleep (default), 1: sleep, 2: exit receive thread |
| `net.RcvThreadSleepTimeForWaitableErrorsInSeconds` | 

Time the receive thread sleeps when a waitable error is returned by a socket operation.

A value of 0 yields only if the platform supports it.



 | < 0: disabled, 0: yield (default), > 0: time to sleep |
| `net.RecreateSocketCooldown` | Minimum amount of time (in seconds) between socket recreation attempts. | `<INTEGER>`: Time in seconds (default: 10) |
| `net.RecreateSocketTimeoutThreshold` | Time (in seconds) without receiving a packet or without a send ACK before triggering socket recreation. | `<INTEGER>`: Time in seconds (default: 0) |
| `net.RecvMultiCapacity` | 

When `RecvMulti` is enabled, this is the number of packets it is allocated to handle per call.

Larger numbers are better, especially under a DDoS attack, but be aware of memory cost.



 | `<INTEGER>`: Number of packets (default: 2048) |
| `net.Reliable.Debug` | Print all reliable bunches sent over the network. | 0: no print (default), 1: print bunches as they are sent, 2: print reliable bunch buffer each net update |
| `net.ReliableRPCQueueSize` | Maximum number of reliable RPCs queued per object. This is in addition to the 256 that are in the send window. This is to support very large RPCs that split into smaller pieces. | `<INTEGER>`: Number of RPCs (default: 4096) |
| `net.RelinkMappedReferences` | Relink mapped references. | 0: disabled, 1: enabled (default) |
| `net.RepDriver.Enable` | 

Enable replication driver.

If disabled, fallback to legacy NetDriver implementation.



 | 0: disabled, 1: enabled (default) |
| `net.ReplicateCustomDeltaPropertiesInRepIndexOrder` | 

If enabled, custom delta properties are replicated in the property `RepIndex` order, which is typically in increasing property offset order. If disabled, custom delta properties replicate in the same order as they are added to the lifetime property array during the call to `GetLifetimeReplicatedProps`.

Custom delta properties are always serialized after regular properties.



 | false: disabled (default), true: enabled |
| `net.ReplicateOnlyBeginPlay` | Only allow property replication of actors that had BeginPlay called on them. | false: disabled (default), true: enabled |
| `net.Replication.DebugProperty` | Debug replication of property by name. This should be set to the partial name of the property to debug. | `<STRING>`: Name of property (default: "") |
| `net.RepMovement.DrawDebug` | Draw debug information for replicated movement. | 0: disabled (default), 1: enabled |
| `net.ReportGameTickFlushTime` | Record and report to the performance tracking system the processing time of the `GameNetDriver`’s `TickFlush`. | false: disabled (default), true: enabled |
| `net.ReportSyncLoads` | 

If enabled, the engine tracks objects loaded by the networking system and broadcasts `FNetDelegates::OnSyncLoadDetected` to report them.

By default, they are logged to the `LogNetSyncLoads` category.



 | false: disabled (default), true: enabled |
| `net.RequiredEncryptionNetDriverDefNames` | 

Comma-delimited list of `NetDriverDefinition`s where `IsEncryptionRequired` returns true when `net.AllowEncryption == 2`.

Specifying `net.RequiredEncryptionNetDriverDefNames="all"` enables this for all `NetDriverDefinition`s.



 | Comma-delimited list |
| `net.ReservedNetGuidSize` | Reserved size (in bytes) for NetGUID serialization, used as a placeholder for later serialization. | `<INTEGER>`: Size in bytes (default: 512) |
| `net.ResetAckStatePostSeamlessTravel` | 

If enabled, the server resets the ACK state of the package map after seamless travel.

Increases bandwidth usage, but may resolve some issues with GUIDs not being available on clients after seamlessly traveling.



 | 0: disabled (default), 1: enabled |
| `net.ReuseReplicatorsForDormantObjects` | 

If enabled, the server persists and attempts to reuse replicators for dormant actors and objects.

This can cut down on bandwidth by preventing redundant information from being sent when waking objects from dormancy.



 | false: disabled (default), true: enabled |
| `net.RPC.Debug` | Print all RPC bunches sent over the network. | 0: disabled, 1: enabled |
| `net.RPCDoSAnalyticsMaxRPCs` | The top `N` number of RPCs to include in RPC DoS analytics ranked by RPC rate per second. | `<INTEGER>`: Number of RPCs (default: 20) |
| `net.RPCDoSDetectionOverride` | 

Enable RPC DoS detection per-NetDriver.

Example usage: `net.RPCDoSDetectionOverride=GameNetDriver=1,BeaconNetDriver=0`. This command specifies that RPC DoS detection is enabled for `GameNetDriver` and disabled for `BeaconNetDriver`.



 | Comma-delimited list |
| `net.RPCDoSForcedRPCTracking` | 

Set a single RPC that, when encountered, forcibly enables RPC tracking. Limited to one RPC for performance.

You can also specify a random chance that encountering the RPC enables tracking and a length of time for leaving tracking enabled; otherwise, tracking disables on the next tick.

Example usage: `net.RPCDoSForcedRPCTracking=ServerAdmin,0.5,10`. This command specifies that there is a 50% chance that when the `ServerAdmin` RPC is encountered, tracking occurs; and, if tracking occurs, it lasts for 10 seconds.



 | `<STRING>`: Name of RPC (default: ""), or Comma-delimited list |
| `net.RPCDoSScopeDebugging` | If enabled, display debug information for RPC DoS Tick/Packet scopes. | 0: disabled (default), 1: enabled |
| `net.ShareInitialCompareState` | If enabled and `net.ShareShadowState` is enabled, attempt to share initial replication comparisons across connections. | 0: disabled (default), 1: enabled |
| `net.ShareSerializedData` | If enabled, use a shared serialization system for replication to reduce CPU usage when multiple clients need the same data. | 0: disabled, 1: enabled (default) |
| `net.ShareShadowState` | If enabled, work done to compare properties is shared across connections. | 0: disabled, 1: enabled (default) |
| `net.SkipDestroyNetStartupActorsOnChannelCloseDueToLevelUnloaded` | If enabled, an actor that is a `NetStartUpActor` associated with the channel is not destroyed when we receive a channel close with `ECloseReason::LevelUnloaded`. | false: disabled, true: enabled (default) |
| `net.SkipReplicatorForDestructionInfos` | If enabled, skip creation of object replicator in `SetChannelActor` when we know there is no content payload and we are going to immediately destroy the actor. | 0: disabled, 1: enabled |
| `net.SubObjects.CompareWithLegacy` | If enabled, collect the subobjects replicated by the `ReplicateSubObjects` method and compare them with the ones replicated via the actor’s registered list. If a divergence between the two is detected, an ensure is triggered. | false: disabled (default), true: enabled |
| `net.SubObjects.DefaultUseSubObjectReplicationList` | If enabled, actors and actor components replicate subobjects using the registration method by default. | false: disabled (default), true: enabled |
| `net.SubObjects.DetectDeprecatedReplicatedSubObjects` | If enabled, trigger an ensure if a `ReplicateSubObjects` function is still implemented in a class that is using the new registered subobjects list. | false: disabled (default), true: enabled |
| `net.SubObjects.LogAllComparisonErrors` | If enabled, log all errors detected by `net.SubObjects.CompareWithLegacy`. If disabled, only the first ensure triggered is logged. | 0: disabled (default), 1: enabled |
| `net.SupportFastArrayDelta` | If enabled, use fast array struct delta serialization. | 0: disabled, 1: enabled (default) |
| `net.TickAllOpenChannels` | 

If enabled, each net connection ticks all of its open channels every tick.

Enabling this can provide valuable debug information, but can degrade performance.



 | 0: disabled, 1: enabled |
| `net.TrackAsyncLoadingGUIDThreshold` | 

Any objects that take longer than this threshold (in seconds) to async load are tracked.

Use this command for debugging and analytics. For more information, see `FNetGUIDCache::ConsumeDelinquencyAnalytics`.



 | `<FLOAT>`: Time in seconds (default: 0) |
| `net.TrackAsyncLoadingGUIDThresholdOwner` | 

If the net connection’s owning player controller or pawn is waiting on async loads for longer than this threshold (in seconds), fire a CSV event to track it.

Use this command for debugging and analytics.



 | `<FLOAT>`: Time in seconds (default: 0) |
| `net.TrackDormantObjectsByLevel` | If enabled, the network object list maintains a set of dormant actors per connection per level. | false: disabled, true: enabled |
| `net.TrackNetSerializeObjectReferences` | 

If enabled, create small layouts for Net Serialize structs if they have object properties.

This can prevent some shadow state garbage collection crashes.



 | false: disabled (default), true: enabled |
| `net.TrackQueuedActorThreshold` | 

Any actor that spends longer than this threshold (in seconds) with queued bunches is tracked.

Use this command for debugging and analytics. For more information, see `UPackageMap::ConsumeDelinquencyAnalytics`.



 | `<FLOAT>`: Time in seconds (default: 0) |
| `net.TrackQueuedActorThresholdOwner` | 

If the net connection’s owning player controller or pawn has queued bunches for longer than this threshold, fire a CSV event to track it.

Use this command for debugging and profiling.



 | `<FLOAT>`: Time in seconds (default: 0) |
| `net.UnreliableRPCQueueSize` | Maximum number of unreliable RPCs queued per object. If more RPCs are queued, older ones are dropped. | `<INTEGER>`: Number of RPCs (default: 10) |
| `net.UseAdaptiveNetUpdateFrequency` | If enabled, `NetUpdateFrequency` is calculated based on how often actors actually send something when replicating. | 0: disabled (default), 1: enabled |
| `net.UseGranularNetworkTracking` | If enabled, the object list prints out highly detailed information about network memory usage. | 0: disabled (default), 1: enabled |
| `net.UsePackedShadowBuffers` | If enabled, `FRepLayout` generates shadow buffers that are packed with only the necessary net properties, instead of copying the entire object state. | 0: disabled, 1: enabled (default) |
| `net.UseRecvMulti` | If enabled and running on a Unix/Linux platform, multiple packets are retrieved from the socket with one syscall improving performance and also allowing retrieval of timestamp information. | 0: disabled (default), 1: enabled |
| `net.UseRecvTimestamps` | If enabled and if `net.UseRecvMulti` is enabled on a Unix/Linux platform, the kernel timestamp will be retrieved for each packet received providing more accurate ping calculations. | 0: disabled (default), 1: enabled |
| `net.ValidateReplicatedPropertyRegistration` | 

If enabled, warn if replicated properties were not registered in `GetLifetimeReplicatedProps`.

Disabled by default in shipping builds, enabled by default in all other builds.



 | 0: disabled,1: enabled |
| `net.VerifyMagicHeader` | 

If enabled, verify the magic header prior to processing a packet.

Use `net.MagicHeader` to set your magic header. Disable verification if transitioning to a new magic header while still supporting the old header.



 | 0: disabled (default), 1: enabled |
| `net.VerifyNetClientID` | If enabled, verify the packet `ClientID`. | 0: disabled, 1: enabled (default) |
| `net.VerifyNetSessionID` | If enabled, verify the packet `SessionID`. | 0: disabled, 1: enabled (default) |
| `net.VerifyShareSerializedData` | If enabled, verify shared serialization data during replication. | 0: disabled (default), 1: enabled |
| `net.WithArrayOnRepFix` | If enabled, attempt to prevent issues with arrays not receiving `OnRep` calls until their size changes if their archetypes have different values from instances in levels. | false: disabled (default), true: enabled |
| `p.net.ForceFault` | If enabled, force a server side input fault. | 0: disabled (default), 1: enabled |
| `p.net.ForceInputDrop` | 

If enabled, force the client to drop inputs.

Use this command for simulating desync.



 | 0: disabled (default), 1: enabled |
| `p.net.LerpTargetNumBufferedCmdsAggresively` | 

If enabled, aggressively linearly interpolate (LERP) toward `TargetNumBufferedCmds`.

Reduces server side buffering, but can cause more artifacts.



 | 0: disabled (default), 1: enabled |
| `p.net.MaxBufferedCmds` | Maximum number of buffered server side commands. | `<INTEGER>`: Number of commands (default: 16) |
| `p.net.MaxTargetNumBufferedCmds` | Maximum number of buffered inputs the server targets per client. | `<FLOAT>`: Number of inputs (default: 5) |
| `p.net.MaxTimeDilationMag` | Maximum time dilation that client uses to slow down / catch up with server. | `<FLOAT>`: Time in seconds (default: 0.01) |
| `p.net.TargetNumBufferedCmds` | Amount to increase `TargetNumBufferedCmds` when an input fault occurs. | `<FLOAT>`: Amount (default: 1.9) |
| `p.net.TargetNumBufferedCmdsAlpha` | Linear interpolation (LERP) strength for `TargetNumBufferedCmds`. | `<FLOAT>`: Strength (default: 0.005) |
| `p.net.TargetNumBufferedCmdsDeltaOnFault` | Amount to increase TargetNumBufferedCmds when an input fault occurs. | `<FLOAT>`: Amount (default: 1) |
| `p.net.TimeDilationAlpha` | Linear interpolation (LERP) strength for sliding client time dilation. | `<FLOAT>`: Strength (default: 0.1) |
| `p.net.TimeDilationEnabled` | If enabled, use client side time dilation. | 0: disabled (default), 1: enabled |

### Console Commands

| **Command** | **Description** | **Arguments** |
| --- | --- | --- |
| `net.ActorReport` | Print actor debug information for all actively replicating actors in the world. | None |
| `net.CreateBandwidthGenerator` | Create a bandwidth generator. | None |
| `net.DeleteDormantActor` | Delete all dormant actors. | None |
| `net.DisconnectSimulatedConnections` | 
Disconnect the provided number of simulated client connections.

Use `net.DisconnectSimulatedConnections 0` to disconnect all simulated client connections.



 | `<INTEGER>`: Number of connections |
| `net.DumpRelevantActors` | Dump information on relevant actors during the next network update. | None |
| `net.ForceOnePacketPerBunch` | 

If enabled, use AutoFlush on all connections and force a packet to be sent for every bunch created. This forces one packet per replicated actor.

This can help you find ordering bugs.



 | true: enabled, false: disabled |
| `net.GenerateConstantBandwidth` | Deliver a constant throughput every tick to generate the specified Kb/sec (Kilobits per second). | `<FLOAT>`: Bandwidth in Kb/sec |
| `net.GeneratePeriodicBandwidthSpike` | 

Generate a bandwidth spike of `<FLOAT>` Kb every `<INTEGER>` seconds.

To generate a bandwidth spike of 100 Kb every 5 seconds use the command: `net.GeneratePeriodicBandwidthSpike 100 5`.



 | `<FLOAT>`: Size in Kb, `<INTEGER>`: Time in seconds |
| `net.ListActorChannels` | List all open actor channels. | None |
| `net.ListNetGUIDExports` | List how many times each Net GUID has been exported. | None |
| `net.ListNetGUIDs` | List Net GUIDs for all actors. | None |
| `net.PackageMap.FindNetGUID` | 

Look up the object that is assigned the provided Net GUID.

Not available in test or shipping builds.

If you do not provide an argument, the system looks up all objects in the Net GUID cache.



 | `<INTEGER>`: Network GUID |
| `net.SimulateConnections` | Start a simulated NetDriver. | `<INTEGER>`: Number of connections |
| `net.TestObjRefSerialize` | 

Attempt to replicate an object reference to all clients.

Not available in test or shipping builds.



 | None |
| `NetEmulation.Off` | Turn off network emulation. | None |
| `NetEmulation.PktDup` | Specify a percentage chance of a sent outbound packet being duplicated. | Clamped value between 0 (no packets duplicated) and 100 (all packets duplicated). |
| `NetEmulation.PktEmulationProfile` | Apply a preconfigured emulation profile. | `<STRING>`: Name of profile |
| `NetEmulation.PktIncomingLagMax` | Specify a maximum amount of potential packet lag on the receiving end. | `<INTEGER>`: Time in milliseconds |
| `NetEmulation.PktIncomingLagMin` | Specify a minimum amount of potential packet lag on the receiving end. | `<INTEGER>`: Time in milliseconds |
| `NetEmulation.PktIncomingLoss` | Specify a percentage change that an inbound packet is discarded to simulate packet loss. | Clamped value between 0 (no packets dropped) and 100 (all packets dropped). |
| `NetEmulation.PktJitter` | Cause sent packets to have a variable, fluctuating latency by adding the value of NetEmulation.PktJitter to the range of possible packet lag times. | `<INTEGER>`: Time in milliseconds |
| `NetEmulation.PktLag` | 

Delay sending packets by the amount of time specified (in milliseconds).

Cannot be used with `NetEmulation.PktOrder`.



 | `<INTEGER>`: Time in milliseconds |
| `NetEmulation.PktLagMax` | Specify a maximum amount of potential packet lag on the sending end. | `<INTEGER>`: Time in milliseconds |
| `NetEmulation.PktLagMin` | Specify a minimum amount of potential packet lag on the sending end. | `<INTEGER>`: Time in milliseconds |
| `NetEmulation.PktLagVariance` | 

Causes packet lag to behave like a random variable instead of a constant lag time (in milliseconds).

If set, lag is a uniform random variable on the interval `[PktLag - PktLagVariance, PktLag + PktLagVariance]`.

Can only be enabled when `NetEmulation.PktLag` is enabled.



 | `<INTEGER>`: Variance |
| `NetEmulation.PktLoss` | Specify a percent chance an outbound packet is discarded to simulate packet loss. | Clamped value between 0 (no packet drop) and 100 (all packets dropped). |
| `NetEmulation.PktOrder` | Change the order of packets at random. This works by randomly selecting packets to be delayed until a subsequent call to `FlushNet`. | 0: disabled, 1: enabled |

## Iris

Iris is Unreal Engine’s next generation replication system. For more information about Iris, see the Iris Overview documentation. Iris console variables begin with the `net.iris.` (networking iris) prefix.

### Console Variables

| **Variable** | **Description** | **Arguments** |
| --- | --- | --- |
| `net.iris.AllowAsyncLoading` | 
If enabled, allow async loading when Iris replication is enabled.

`net.AllowAsyncLoading` must also be enabled.



 | false: disabled, true: enabled (default) |
| `net.iris.AllowPollPeriodOverrides` | If enabled, allow poll period overrides set in `ObjectReplicationBridgeConfig`. | false: disabled, true: enabled (default) |
| `net.iris.bWarnAboutStructPropertiesWithSuspectedNotReplicatedProperties` | If enabled, try to detect whether a struct replicated as a property might contain unannotated members. | false: disabled (default), true: enabled |
| `net.iris.CullNonRelevant` | If enabled, cull replicated actors that are not relevant to any client. | false: disabled, true: enabled (default) |
| `net.iris.DebugName` | Set a class or object name to break on. | `<STRING>`: Name (default "") |
| `net.iris.DebugRPCName` | Set an RPC name to break on. | `<STRING>`: Name (default "") |
| `net.iris.DeferEndReplication` | If enabled, calls to `EndReplication` are deferred until after state data is applied. | false: disabled, true: enabled (default) |
| `net.iris.DeltaCompressInitialState` | If enabled, compare the initial state with the default state when serializing. | false: disabled, true: enabled (default) |
| `net.iris.EnableDeltaCompression` | If enabled, delta compress replicated objects. | false: disabled, true: enabled (default) |
| `net.iris.EnableFilterMappings` | If enabled, honor filter mappings set in `ObjectReplicationBridgeConfig`. If filter mappings are enabled, objects may also be assigned the default spatial filter even if there aren’t any specific mappings. | false: disabled, true: enabled (default) |
| `net.iris.EnableForceNetUpdate` | If enabled, the system only allows `ForceNetUpdate` to skip the poll frequency of objects. If disabled, any `MarkDirty` object is immediately polled. | false: disabled (default), true: enabled |
| `net.iris.EnableRPCs` | If enabled, let Iris replicate and execute RPCs. | 0: disabled, 1: enabled (default) |
| `net.iris.ExecuteReliableRPCsBeforeOnReps` | If enabled and Iris is running in backwards compatibility mode, then reliable RPCs are executed before `OnRep` on the target object. | false: disabled (default), true: enabled |
| `net.iris.ForceFullCopyAndQuantize` | If enabled, a full copy and quantize is used. If disabled, the system only copies and quantizes dirty state data. | false: disabled (default), true: enabled |
| `net.iris.ForcePruneBeforeUpdate` | 

If enabled, verify the integrity of all tracked instances at the start of every update.

Not available in shipping builds.



 | false: disabled (default), true: enabled |
| `net.iris.IrisPreExportExistingNetTokensOnConnect` | If enabled, enqueue all existing Net Tokens for pre-export when a new connection is added. | false: disabled (default), true: enabled |
| `net.iris.LogReplicationProtocols` | If enabled, log all created replication protocols. | false: disabled (default), true: enabled |
| `net.iris.MinimumNumberOfFramesBetweenBaselines` | Minimum number of frames between creation of new delta compression baselines for an object. | `<INTEGER>`: Frames (default 60) |
| `net.iris.OnlyQuantizeDirtyMembers` | If enabled, only quantize members marked as dirty unless this is a new object. | false: disabled, true: enabled (default) |
| `net.iris.PushModelMode` | 

Set the push model mode for Iris networking.

This setting requires that you enable `net.IsPushModelEnabled` and `WITH_PUSH_MODEL > 0` to use push-based dirtiness in backward compatibility mode.



 | 0: disabled (runtime togglable), 1: enabled (not runtime togglable), 2: enabled (runtime togglable) (default) |
| `net.iris.ReplicationWriter.ValidateObjectsWithDirtyChanges` | If enabled, validate all objects marked as dirty. | false: disabled (default), true: enabled |
| `net.iris.SaturateBandwidth` | If enabled, saturate the bandwidth. | false: disabled (default), true: enabled |
| `net.iris.UseChangeMaskForTArray` | If enabled, use a change mask for individual elements in `TArray`s. When enabled and packet loss occurs, the received array may not reflect a state which was ever present on the sending side since the array won’t be replicated atomically. | false: disabled, true: enabled (default) |
| `net.iris.UseDormancyToFilterPolling` | If enabled, use dormancy to filter out objects that should not be polled. | false: disabled, true: enabled (default) |
| `net.iris.UseFrequencyBasedPolling` | If enabled, use frequency based polling. | false: disabled, true: enabled (default) |
| `net.iris.UseIrisReplication` | If enabled, use the Iris replication system. If disabled, replication is still available with Unreal Engine’s legacy replication system. | 0: disabled (default), 1: enabled |
| `net.iris.UseNativeFastArray` | If enabled, use `IrisNativeFastArray`. | false: disabled, true: enabled (default) |
| `net.iris.UsePrevReceivedStateForOnReps` | If enabled, `OnRep` uses the previous received state when doing `OnRep` and does not do any comparison. If disabled, copy the local state and compare before issuing `OnRep`. | false: disabled (default), true: enabled |
| `net.iris.UseSupportsStructNetSerializerList` | If enabled, structs in the `SupportsStructNetSerializerList` do not raise warnings even if the struct has a `NetSerialize`/`NetDeltaserialize`, but has no custom `NetSerializer`. | false: disabled, true: enabled (default) |
| `net.iris.WarnAboutDroppedAttachmentsToObjectsNotInScope` | If enabled, warn when attachments are dropped due to objects not in scope. | false: disabled (default), true: enabled |
| `net.iris.WarnAboutStructsWithCustomSerialization` | If enabled, warn when generating descriptors for structs with custom serialization. | false: disabled, true: enabled (default) |

### Console Commands

| **Command** | **Description** | **Arguments** |
| --- | --- | --- |
| `net.iris.DebugNetInternalIndex` | Specify an internal index to break on. | `<INTEGER>`: Internal Net Ref Index |
| `net.iris.DebugNetRefHandle` | Specify a NetRefHandle ID to break on. | `<INTEGER>`: Net Ref Handle |

## Check Console Variable State

You can check the state of a console variable by entering the name of the console variable into the console followed by a question mark (?). To check the state of all console variables, use `DumpCVars`. To check the state of all console commands, use `DumpCCmds`. If you only wish to see networking console variables, you can filter the console log by searching for `net.` console variables.