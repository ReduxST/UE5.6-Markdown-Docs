# Rundown Server

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-rundown-server-for-motion-design-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/setting-up-rundown-server-for-motion-design-in-unreal-engine)  
**Processed:** 2025-06-14 16:49:48

---

Controlling the Motion Design playout can be accomplished by combining two APIs. The **Rundown Server API** is used to load the rundown assets and the page’s templates, and contains an embedded [Remote Control](/documentation/en-us/unreal-engine/remote-control-for-unreal-engine) Preset (RCP).

The RCP for the corresponding page can be accessed and modified via the Remote Control API, then saved back in the rundown page for immediate or later playout.

## Architecture Overview

![Unreal Editor Rundown and Remote Control API process](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dc32c804-b74e-4fd4-bf98-b090645f96c1/unreal-editor-process.png)

## Project Configuration

### 1\. Set Up WebSocket Messaging Plugin in Server Mode

The Rundown Server API is exposed to WebSocket through the **WebSocket Messaging** bridge plugin. This plugin allows any internal message bus end points to be exposed through a WebSocket.

It can be enabled in the plugin browser by searching for **web socket**:

![web socket messaging](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/eb3b548e-773d-4f44-aaec-e4fc78bab0d4/websocket-messaging.png)

Once enabled, the plugin can be configured in **Project Settings > Json**.

![web socket plugin](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/15f9bf9a-5955-4913-a643-86dc1a0081f0/plugins-websocket-messaging.png)

Enter the desired listen port and configure the serialization to JSON.

### 2\. Enable Rundown Server

In the Editor settings:

![Motion Design Rundown settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/133cafac-671b-48fc-9178-71cb814cdfbc/motion-design-rundown.png)

Enable the auto start for the Rundown server on the next editor restart. Leaving the server name blank will use the computer’s name instead.

Alternatively, there is a console command to start the rundown server immediately: "MotionDesignRundownServer.Start \[ServerName\]". The server name is an optional argument.

Finally, the UE process can be launched with a command line argument: `-MotionDesignRundownServerStart[=ServerName]`.

If the server is running, the console command `MotionDesignRundownServer.Status` should provide some information about the status of the server.

### 3\. Set Up Remote Control

Follow the instructions on the [Remote Control API WebSocket Reference](/documentation/en-us/unreal-engine/remote-control-api-websocket-reference-for-unreal-engine) page.

![Remote Control Web Server plugin settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c700b70-f180-4a0f-95ad-5bb665a24256/plugins-remote-control.png)

**If using the http server**, it is binding to `localhost` by default, which may not be the adapter you need. To let it bind to any adapter, add the following lines to `DefaultEngine.ini`:

\[HTTPServer.Listeners\]

DefaultBindAddress=any

## Using WebSocket Messaging

The WebSocket Messaging plugin exposes all messages going through the [UE message bus](/documentation/en-us/unreal-engine/API/Runtime/Messaging/IMessageBus). Each internal message-bus message is wrapped in a .json message with additional routing information.

Anatomy of the a WebSocket Messaging bridge `message`:

| Field Name | Description |
| --- | --- |
| **`Sender`** | UUID of the sender. This identifies the sending endpoint in the messaging bus. |
| **`Recipients`** | List of UUID of the recipients. If empty, this is equivalent to a `broadcast` to all endpoints listening to the given message type. |
| **`MessageType`** | Corresponds to the UE structure of the message content. |
| **`Expiration`** | Unix time at which the message gets discarded. |
| **`Scope`** | Specifies the scope of propagation of the message (thread, process, network) in the message bus system. For the WebSocket, this is always `Network`. |
| **`Annotations`** | Optional message annotations. |
| **`Message`** | Content of the message. The structure of this content is determined by the `Message Type`. |

Example of a request `GetRundowns` and the response from the server:

| Client request | Server response |
| --- | --- |
| 
```
`{   "Sender": "F2DCD99C267C4F84B50CF091AA4ED608",   "Recipients": [     "139696A842C8861F52E756BB60AA8661"   ],   "MessageType": "/Script/AvalancheMediaEditor.AvaRundownGetRundowns",   "Expiration": 253402300799,   "Scope": "Network",   "Annotations": {},   "Message": {} }`
Copy full snippet
```
{ "Sender": "F2DCD99C267C4F84B50CF091AA4ED608", "Recipients": \[ "139696A842C8861F52E756BB60AA8661" \], "MessageType": "/Script/AvalancheMediaEditor.AvaRundownGetRundowns", "Expiration": 253402300799, "Scope": "Network", "Annotations": {}, "Message": {} }

 | 

```
`{   "Sender": "139696A842C8861F52E756BB60AA8661",   "Recipients": [     "F2DCD99C267C4F84B50CF091AA4ED608"   ],   "MessageType": "/Script/AvalancheMediaEditor.AvaRundown**Rundowns**",   "Expiration": 253402300799,   "TimeSent": 1660878367,   "Scope": "Network",   "Annotations": {},   "Message": {  **   "rundowns": [       "/Game/AvaRundown.AvaRundown",       "/Game/AvalancheExamples/ExampleRundown.ExampleRundown",       "/Game/AvalancheExamples/DemoRC.DemoRC"     ] **  } }`
Copy full snippet
```
{ "Sender": "139696A842C8861F52E756BB60AA8661", "Recipients": \[ "F2DCD99C267C4F84B50CF091AA4ED608" \], "MessageType": "/Script/AvalancheMediaEditor.AvaRundown\*\*Rundowns\*\*", "Expiration": 253402300799, "TimeSent": 1660878367, "Scope": "Network", "Annotations": {}, "Message": { \*\* "rundowns": \[ "/Game/AvaRundown.AvaRundown", "/Game/AvalancheExamples/ExampleRundown.ExampleRundown", "/Game/AvalancheExamples/DemoRC.DemoRC" \] \*\* } }

 |

The `message type` specifies the content of `Message`. In API terms, for the client, the `message type` is the command and the content of `Message` is the arguments of the command.

### Message Bus Handshake with Rundown Server

In order to get the UUID of the Rundown server on the message bus, which is then used as `Recipient` for the messages, a WebSocket client must broadcast a `ping` message to the WebSocket and listen for the pong reply to get the UUID of the server. In the message bus, the Rundown server is subscribed to the `AvaRundownPing` message and will reply to its sender with a `AvaRundownPong` message.

| Client request | Server response |
| --- | --- |
| 
```
`{   "Sender": "F2DCD99C267C4F84B50CF091AA4ED608",   "Recipients": [],   "MessageType": "/Script/AvalancheMediaEditor.AvaRundownPing",   "Expiration": 253402300799,   "Scope": "Network",   "Annotations": {},   "Message":     {         "bAuto": false      } }`
Copy full snippet
```
{ "Sender": "F2DCD99C267C4F84B50CF091AA4ED608", "Recipients": \[\], "MessageType": "/Script/AvalancheMediaEditor.AvaRundownPing", "Expiration": 253402300799, "Scope": "Network", "Annotations": {}, "Message": { "bAuto": false } }

 | 

```
`{         "Sender": "**69C67BCB4B61795764D1E596D9F01214**",         "Recipients": [ "F2DCD99C267C4F84B50CF091AA4ED608 ],         "MessageType": "/Script/AvalancheMediaEditor.AvaRundownPong",         "Expiration": 253402300799,         "TimeSent": 1661023146,         "Scope": "Network",         "Annotations": { },         "Message":         {                 "bAuto": false,                 "hostName": "TEST-SERVER-01"         } }`
Copy full snippet
```
{ "Sender": "\*\*69C67BCB4B61795764D1E596D9F01214\*\*", "Recipients": \[ "F2DCD99C267C4F84B50CF091AA4ED608 \], "MessageType": "/Script/AvalancheMediaEditor.AvaRundownPong", "Expiration": 253402300799, "TimeSent": 1661023146, "Scope": "Network", "Annotations": { }, "Message": { "bAuto": false, "hostName": "TEST-SERVER-01" } }

 |

The Pong message `Sender` field is the UUID of the Rundown server’s endpoint in the message bus system. This is then used as the `Recipients` field for all other messages from the Websocket client.

## Rundown Server API

Existing commands and response messages can be found in the source code here:

```
`Engine\Plugins\Experimental\Avalanche\Source\AvalancheMediaEditor\Private\Rundown\AvaRundownMessages.h`
Copy full snippet
```
Engine\\Plugins\\Experimental\\Avalanche\\Source\\AvalancheMediaEditor\\Private\\Rundown\\AvaRundownMessages.h

The path of the USTRUCT is the `MessageType` field of the WebSocket message, while the content is serialized in the `Message` field as previously shown.

The JSON serializer uses UStructToJsonObject, which will change the case of field names from the native struct definitions. see StandardizeCase in native code for details. As a general rule, in the JSON format, the first character of the field name will be lowercase. This is only true for JSON format, the concise Binary Object Representation (CBOR) keeps the field name’s case untouched.

### Editing the Page RCP with Remote Control API

![Remote Control API flowchart](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/823fee05-3447-49a7-8c85-31ef748a4b06/remote-control-api.png)

The `GetPageDetails` is used with `bLoadRemoteControlPreset` set to **true** to inject the page’s RC values into the managed RCP for that asset. The server response will include the following fields:

'remoteControlPresetName': '/Temp/Managed/ESPYS/Blueprint/Avalanche/9021',

'remoteControlPresetId': '984A4E0146010512D839538C0AF265FA',

These can be used with Remote Control API as the `PresetName` field.

The RC values are saved back in the page with the `UpdatePageFromRCP` request.

There is no API to modify the Page RC values directly. Doing that might break the RC controllers so it is not allowed by design. The only path to modify RC values is through the Remote Control API, which runs the controllers and all associated logic.