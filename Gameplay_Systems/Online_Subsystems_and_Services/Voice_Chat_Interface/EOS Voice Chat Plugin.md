# EOS Voice Chat Plugin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/voice-chat-with-epic-online-services](https://dev.epicgames.com/documentation/en-us/unreal-engine/voice-chat-with-epic-online-services)  
**Processed:** 2025-06-14 17:03:34

---

With the **EOS Voice Chat** plugin, developers can leverage the **Epic Online Services** (EOS) Voice Interface to add voice communication to their products, including using the familiar IVoiceChat and IVoiceChatUser interfaces from the engine's **Online Subsystem** (OSS). In addition, developers who were previously using VivoxVoiceChat can easily migrate to the EOS backend.

## Setup

The EOS Voice Chat plugin implements the IVoiceChat and IVoiceChatUser interfaces. To begin, open the **Plugin Browser** from the editor's **Edit** menu, then find and enable the plugin.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ae43e0d8-ec0d-4342-bbe2-85f769d7377d/enableeosvoicechat.png)

Once you have enabled the plugin in your project, you can integrate it through the **Lobbies** method, or the **Trusted Server** method. These methods are not mutually exclusive; you can mix them together to gain the benefits and capabilities of each method.

Although both methods are based on the way that EOS works, you will not need to program with the EOS SDK directly. However, you can read the [EOS Voice Interface](https://dev.epicgames.com/docs/services/en-US/Interfaces/Voice/index.html) documentation if you want to gain a better understanding of how it works. While reading, bear in mind that IVoiceChat **Channels** are equivalent to EOS **Rooms**, and the two terms should be considered interchangeable.

## Integrating with the EOS Voice Interface

The two main integration methods, Lobbies, and Trusted Server offer different capabilities. We recommend that you consider which works better for your project, or if a mixed approach is best. With the Lobbies method, the system will automatically join voice chat through EOS without the `IVoiceChatUser::JoinChannel` function, and you will receive an IVoiceChatUser instance from EOS. The Trusted Server method requires you to call the `IVoiceChatUser::JoinChannel` function with credentials from a trusted server, but along with this requirement comes the ability to choose which channels to join or leave. This method also gives you control over your IVoiceChat and IVoiceChatUser instances, rather than requiring you to use an instance that EOS provides. You can mix the two integration methods if you would like the OnlineSubsystemEOS plugin to manage lobby voice channels for you automatically, while you manually manage trusted server channels with the IVoiceChat and IVoiceChatUser interfaces. Mixed integration method developers can also reuse the IVoiceChatUser instance from the Lobbies method with the channels that the user has joined through the Trusted Server method.

To get started, you will need to configure your application on the [EOS Developer Portal](https://dev.epicgames.com/docs/services/en-US/DevPortal/index.html). If you are using the Lobbies integration method, you will also need to enable the **OnlineSubsystemEOS** plugin in your project.

### Using the Lobbies Method

The Lobbies method leverages EOS to handle most of the work involved in joining a channel. This means that if you are using this integration method, you do not need to implement the usual IVoiceChat flow for initializing, connecting, logging in, and joining a channel, because EOS will do this for you.

After setting up OnlineSubsystemEOS with your project, you will be able to join and host EOS lobby sessions. Follow these steps to enable automatic joining of the corresponding voice channels:

1.  Navigate to the EOS Developer Portal and configure your application by enabling voice support.
    
2.  Set `FOnlineSessionSettings::bUseLobbiesVoiceChatIfAvailable` to `true` when creating lobby sessions.
    
3.  Call `FOnlineSubsystemEOS::GetVoiceChatUserInterface` to get an IVoiceChatUser interface instance associated with a given local user.
    

Once the user has logged into EOS, you can get an instance of the IVoiceChatUser interface with the `GetVoiceChatUserInterface` function. Although you do not need to manage channels, you can use this to interact with the other aspects of the system, such as the user's selected input and output devices, or their list of blocked players. Use this interface instance to register event notification callbacks. As long as the user stays logged in, the OnlineSubsystemEOS plugin will automatically join and leave the associated voice channels for any lobbies the user joins or leaves. As this happens, EOSVoiceChat will broadcast `OnVoiceChatChannelJoined` and `OnVoiceChatChannelExited` delegates in response.

The OnlineSubsystemEOS plugin will automatically update the EOS Voice Chat plugin with information about lobby sessions, including notifications about creating, destroying, joining, and leaving them. The EOS Voice Chat plugin broadcasts the `OnVoiceChatChannelJoined` and `OnVoiceChatChannelExited` delegates in response to these events.

### Using the Trusted Server Method

For situations that favor manual channel management, you will need to use the Trusted Server integration method. As an example, if you use a party system that is not built on EOS Lobbies, creating channels for your party requires this method. The Trusted Server method provides greater control over the user's channel connections, but it requires users to retrieve login credentials from a trusted server in order to join a channel.

#### Trusted Server Engine Configuration

If you are reusing an IVoiceChatUser interface instance from a Lobbies integration, then you can skip this section.

If you are not using a Lobbies integration, or if you want to use a separate IVoiceChatUser interface instance, then you will need to add the following section to your `Engine.ini` file and populate with information about your product:

```
	`[EOSVoiceChat] 	ProductId= 	SandboxId= 	DeploymentId= 	ClientId= 	ClientSecret=`

Copy full snippet
```
\[EOSVoiceChat\] ProductId= SandboxId= DeploymentId= ClientId= ClientSecret=

Fill out each line with the appropriate value for your product. You can find these values by opening your product on the EOS Developer Portal. EOSVoiceChat uses these values to create an EOS [Platform Interface](https://dev.epicgames.com/docs/services/en-US/Interfaces/Platform/index.html) instance.

#### Code Flow

If you are working with the Trusted Server integration method, observe the same [code flow](/documentation/en-us/unreal-engine/voice-chat-interface-in-unreal-engine#codeflow) as described in the [Voice Chat Interface](/documentation/en-us/unreal-engine/voice-chat-interface-in-unreal-engine) documentation. If your project uses both integration methods, and you are reusing one or more IVoiceChatUser instances from OSS EOS for trusted server channels, these requirements do not apply; the Lobbies integration handles most of the IVoiceChat flow (including instance lifespan management) automatically, and provides a logged in IVoiceChatUser instance.

##### Joining a Channel

Although your code does not need to interface with the EOS SDK, the process of joining a channel will ultimately go through the EOS Voice Interface. If you would like to gain a greater understanding of that system, we recommend reading the [documentation](https://dev.epicgames.com/docs/services/en-US/Interfaces/Voice/index.html#voiceflowwithatrustedserver) for it on the EOS documentation site.

Joining a channel requires a client base URL and a participant token from your trusted server. Provide this information to EOS Voice Chat by filling in an `FEOSVoiceChatChannelCredentials` struct and serializing it to JSON, similar to the sample below:

```
	`// Create an FEOSVoiceChatChannelCredentials data structure. 	FEOSVoiceChatChannelCredentials ChannelCredentials; 	// Set the client base URL from the trusted server; this will vary from session to session. 	// The URL should look like "wss://example-of-url-us-east-1.rtcp.on.epicgames.com". 	ChannelCredentials.ClientBaseUrl = ClientBaseUrlFromTrustedServer 	// Set the participant token from the trusted server. 	ChannelCredentials.ParticipantToken = ParticipantTokenFromTrustedServer;  	// Call JoinChannel with the FEOSVoiceChatChannelCredentials data structure. 	VoiceChatUser->JoinChannel(ChannelName, ChannelCredentials.ToJson(), ...);`

Copy full snippet
```
// Create an FEOSVoiceChatChannelCredentials data structure. FEOSVoiceChatChannelCredentials ChannelCredentials; // Set the client base URL from the trusted server; this will vary from session to session. // The URL should look like "wss://example-of-url-us-east-1.rtcp.on.epicgames.com". ChannelCredentials.ClientBaseUrl = ClientBaseUrlFromTrustedServer // Set the participant token from the trusted server. ChannelCredentials.ParticipantToken = ParticipantTokenFromTrustedServer; // Call JoinChannel with the FEOSVoiceChatChannelCredentials data structure. VoiceChatUser->JoinChannel(ChannelName, ChannelCredentials.ToJson(), ...);

### Mixing the Lobbies and Trusted Server Methods

The Lobbies and Trusted Server integration methods are fully compatible with each other. If you want to gain the advantages of both methods, you can either reuse the IVoiceChatUser interface from the Lobbies method to join, leave, and interact with your trusted server channels, or you can create separate interface instances.

## Testing and Debugging

### Console Commands

| Command | Description |
| --- | --- |
| `eosvoicechat list` | Lists all EOSVoiceChat instances along with their instance ID, debug name (which is useful for telling them apart), and number of created user interfaces. |
| `eosvoicechat info instanceid=<instanceid>` | Dumps the current state of the instance and all associated user interfaces to the log. |
| `eosvoicechat initialize instanceid=<instanceid>` | Initializes this instance. |
| `eosvoicechat uninitialize instanceid=<instanceid>` | Uninitializes this instance. |
| `eosvoicechat connect instanceid=<instanceid>` | "Connects" this instance. This should always succeed on EOS Voice Chat, as EOS Voice handles connections per-channel. |
| `eosvoicechat disconnect instanceid=<instanceid>` | Disconnects this instance. |
| `eosvoicechat createuser instanceid=<instanceid>` | Creates a new IVoiceChatUser interface. |
| `eosvoicechat releaseuser instanceid=<instanceid>` | Releases an IVoiceChatUser interface created with `createuser`. |
| `eosvoicechat createsingleuser instanceid=<instanceid>` | This is a convenience method for non-splitscreen games. You can create a single user interface and avoid passing `UserIndex=<UserIndex>` in commands that require it. |
| `eosvoicechat input setvolume instanceid=<instanceid> userindex=<userindex> volume=<volume>` | 
Sets the volume of the input device.

Takes a float value between `0.0` and `2.0` where:

-   `0.0` is fully attenuated.
-   `1.0` is no change in volume.
-   `2.0` is double volume.



 |
| `eosvoicechat input mute instanceid=<instanceid> userindex=<userindex>` | Mutes the input device. |
| `eosvoicechat input unmute instanceid=<instanceid> userindex=<userindex>` | Unmutes the input device. |
| `eosvoicechat input listdevices instanceid=<instanceid> userindex=<userindex>` | Lists the available input devices. |
| `eosvoicechat input setdevice instanceid=<instanceid> userindex=<userindex> deviceid=<deviceid>` | Selects a specific input device. You can get a list of valid `deviceid` values from the `listdevices` command. |
| `eosvoicechat input setdefaultdevice instanceid=<instanceid> userindex=<userindex>` | Reverts to using the default input device. |
| `eosvoicechat output setvolume instanceid=<instanceid> userindex=<userindex> volume=<volume>` | 

Sets the volume of the output device.

Takes a float value between `0.0` and `2.0` where:

-   `0.0` is fully attenuated.
-   `1.0` is no change in volume.
-   `2.0` is double volume.



 |
| `eosvoicechat output mute instanceid=<instanceid> userindex=<userindex>` | Mutes the output device. |
| `eosvoicechat output unmute instanceid=<instanceid> userindex=<userindex>` | Unmutes the output device. |
| `eosvoicechat output listdevices instanceid=<instanceid> userindex=<userindex>` | Lists the available output devices. |
| `eosvoicechat output setdevice instanceid=<instanceid> userindex=<userindex> deviceid=<deviceid>` | Selects a specific output device. You can get a list of valid `deviceid` values from the `listdevices` command. |
| `eosvoicechat output setdefaultdevice instanceid=<instanceid> userindex=<userindex>` | Reverts to using the default output device. |
| `eosvoicechat login instanceid=<instanceid> userindex=<userindex> playername=<playername>` | Logs a user in on this interface. The `playername` parameter is the stringified EOS Product ID of the user. |
| `eosvoicechat logout instanceid=<instanceid> userindex=<userindex>` | Logs a user out from this user interface. |
| `eosvoicechat channel join instanceid=<instanceid> userindex=<userindex> channelname=<channelname> channeltype=<channeltype>` | Joins a named channel. This command will not query a trusted server for the client base URL or participant token; it will use the `InsecureClientBaseUrl` from the configuration file, and a generated participant token. See `FEOSVoiceChatUser::InsecureGetJoinToken`. The `channeltype` parameter is optional. There is a feedback channel named "echo" that is helpful for single user testing. |
| `eosvoicechat channel leave instanceid=<instanceid> userindex=<userindex> channelname=<channelname>` | Leaves a named channel. |
| `eosvoicechat channel transmit instanceid=<instanceid> userindex=<userindex> channelname=<channelname>` | Transmits only to a specific, named channel. |
| `eosvoicechat channel transmitall instanceid=<instanceid> userindex=<userindex>` | Transmits to all channels. |
| `eosvoicechat channel transmitnone instanceid=<instanceid> userindex=<userindex>` | Transmits to no channels. |
| `eosvoicechat player mute instanceid=<instanceid> userindex=<userindex> playername=<playername>` | Mutes the named remote player. Although you cannot hear them, they can still hear you. To stop sending input to them also, see the block command. |
| `eosvoicechat player unmute instanceid=<instanceid> userindex=<userindex> playername=<playername>` | Unmutes the named remote player. |
| `eosvoicechat player block instanceid=<instanceid> userindex=<userindex> playername=<playername>` | Blocks the named remote player, rendering you inaudible to each other. |
| `eosvoicechat player unblock instanceid=<instanceid> userindex=<userindex> playername=<playername>` | Unblocks the named remote player. |
| `eosvoicechat player setvolume instanceid=<instanceid> userindex=<userindex> playername=<playername> volume=<volume>` | 

Sets the volume of the name remote player.

Takes a float value between `0.0` and `2.0` where:

-   `0.0` is fully attenuated.
-   `1.0` is no change in volume.
-   `2.0` is double volume.



 |

### Log Output

The `LogEOSVoiceChat` log category contains all log output coming from the EOSVoiceChat plugin itself, including the above console commands, while the `LogEOSSDK` log category contains log output coming from the underlying EOS SDK. Changing the verbosity level of the `LogEOSSDK` log category will also update the log verbosity setting on the EOS SDK [Logging Interface](https://dev.epicgames.com/docs/services/en-US/Interfaces/Logging/index.html), so the two are always in sync.