# Logging

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/logging-for-networked-games-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/logging-for-networked-games-in-unreal-engine)  
**Processed:** 2025-06-14 16:34:21

---

## Logging for Networked Games

**Client** and **Server** logs are important for identifying and debugging networking issues. While many networking logs fall into the **LogNet** category, we recommend checking log categories that are more closely related to specific systems to provide greater insight into any issues.

These categories are not enabled by default and have varying amounts of verbosity that you may need to adjust to gain information about the behavior you're experiencing. The list below provides some recommended categories:

| Category | Description |
| --- | --- |
| **LogNetTraffic** | Logs all network traffic when this log variable is set to VeryVerbose. |
| **LogNetPackageMap** | Logs information related to how NetGUIDs are Sent, Received, and Acknowledged. |
| **LogNetVersion** | Logs information related to Property Replication and RepNotify functions that are used by FRepLayout and FObjectReplicator. |
| **LogNetFastTArray** | ^ |
| **LogNetDormancy** | ^ |
| **LogRep** | ^ |
| **LogRepTraffic** | ^ |
| **LogRepProperties** | Logs information related to the sending and receiving of replicated properties. |
| **PacketHandlerLog** | Logs information on the packet handler and its components. These components have their own sub-categories. For example, LogDTLSHandler, OodleNetworkHandlerComponentLog, and LogHandshake. |
| **LogDemo** | Logs information on recording and playing back replays. Each replay streamer has a related log category: LogLocalFileReplay, LogSaveGameReplay, LogNullReplay, and LogMemoryReplay. |

You can enable these log categories and adjust their verbosity by the following methods:

### Command-Line Argument

Pass the `LogCmds` command line argument:

```
`-LogCmds="<LOG_CATEGORY> <LOG_VERBOSITY>"`
Copy full snippet
```
\-LogCmds="<LOG\_CATEGORY> <LOG\_VERBOSITY>"

For example, to set `LogNetTraffic` to `VeryVerbose`:

```
`-LogCmds="LogNetTraffic VeryVerbose"`
Copy full snippet
```
\-LogCmds="LogNetTraffic VeryVerbose"

### Console Command

Use the `Log` console command:

```
`Log <LOG_CATEGORY> <LOG_VERBOSITY>`
Copy full snippet
```
Log <LOG\_CATEGORY> <LOG\_VERBOSITY>

For example, to set `LogNetTraffic` to `Verbose`:

```
`Log LogNetTraffic Verbose`
Copy full snippet
```
Log LogNetTraffic Verbose

### Engine Configuration

Set them in your project's `DefaultEngine.ini.`:

```
`[Core.Log] <LOG_CATEGORY1>=<LOG_VERBOSITY1> <LOG_CATEGORY2>=<LOG_VERBOSITY2> ...`
Copy full snippet
```
\[Core.Log\] <LOG\_CATEGORY1>=<LOG\_VERBOSITY1> <LOG\_CATEGORY2>=<LOG\_VERBOSITY2> ...

For example, to set multiple categories to different verbosities:

```
`[Core.Log] LogNetPackageMap=Log LogNetTraffic=Verbose LogRep=VeryVerbose`
Copy full snippet
```
\[Core.Log\] LogNetPackageMap=Log LogNetTraffic=Verbose LogRep=VeryVerbose

## Helpful Errors

When reading logs, the following list can be useful for determining what kind of error occurred.

<table class="table" style="--columns-count: 2;"><tbody><tr><td><strong>UEngine::BroadcastNetworkFailure</strong></td><td>Printed when a net driver encounters some major error. The log line will include the failure type, the error string, and the description of the net driver that encountered the error. You can see a list of the possible network failures with brief descriptions in the ENetworkFailure enum in EngineBaseTypes.h.</td></tr><tr><td><strong>UNetConnection::Close</strong></td><td>A description of the connection being closed.</td></tr><tr><td><strong>UActorChannel::Close</strong></td><td>A LogNetTraffic category that will include the channel index, the Actor for that channel, and the reason it was closed. Checking the logs around these lines can help provide some indication as to why a connection or Actor channel was closed.</td></tr></tbody></table>

The command-line argument `-LogTrace=<PARTIAL_LOG_LINE>` performs stack traces from partial log message strings. For example: `-LogTrace=UNetConnection::Close` will produce a stack trace whenever `UNetConnection::Close` is printed to the logs. The command-line argument `-DumpRPCs` provides the capability to dump RPCs and their parameters, which can be useful for tracking what RPCs are being sent and their parameters.

LogTrace and DumpRPCs both require **NetcodeUnitTest** to be enabled.