# Remote Control API WebSocket Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-api-websocket-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-api-websocket-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:46:27

---

This page describes the WebSocket message types offered by the **Remote Control API**. A sample HTML file with JavaScript functions is provided at the end of this page to show how to use and test these WebSocket messages.

By default, the WebSocket port in the engine is 30020. Connect to the WebSocket server at `ws://127.0.0.1:30020` to start sending messages. You can change the WebSocket port for your project.

-   In the Editor's main menu, choose **Edit > Edit Project Settings…** to open the **Project Settings** window.
    
-   In the **Project Settings** window, select **Remote Control** in the **Plugins** section.
    
-   Change the field **Remote Control WebSocket Server Port** to the port that you want to use.
    

![Remote Control Plugin Settings](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18c99465-64ed-4cb0-ba6e-abc849c8ba82/image_0.png)

## WebSocket Messages

The Remote Control API uses the JSON format for its WebSocket messages. All WebSocket messages sent to the server must be JSON objects with the following properties:

| Property | Description |
| --- | --- |
| MessageName | 
Identifies the type of message to send. Options are:

-   HTTP
-   Preset.Register
-   Preset.Unregister



 |
| Parameters | Parameters for each message type. See the sections below for more details. |
| Id | Optional: A useful identifier for any deferred response from the server. |

### WebSocket Message Type - HTTP

Use this message type to call an HTTP route through a WebSocket message. See the [Remote Control API HTTP Reference](/documentation/en-us/unreal-engine/remote-control-api-http-reference-for-unreal-engine) for more information on HTTP routes that can be called.

Example JSON message:

```
	`{ 		"MessageName": "http", 		"Parameters": { 			"Url": "/remote/object/property", 			"Verb": "PUT", 			"Body": { 				"ObjectPath": "/Game/ThirdPerson/Maps/ThirdPersonMap.ThirdPersonMap:PersistentLevel.StaticMeshActor_1.StaticMeshComponent0", 				"propertyName": "StreamingDistanceMultiplier", 				"access": "READ_ACCESS" 			} 		} 	}`

Copy full snippet
```
{ "MessageName": "http", "Parameters": { "Url": "/remote/object/property", "Verb": "PUT", "Body": { "ObjectPath": "/Game/ThirdPerson/Maps/ThirdPersonMap.ThirdPersonMap:PersistentLevel.StaticMeshActor\_1.StaticMeshComponent0", "propertyName": "StreamingDistanceMultiplier", "access": "READ\_ACCESS" } } }

The WebSocket server sends back a JSON message with the response to the call:

```
	`{ 		"RequestId": -1, 		"ResponseCode": 200, 		"ResponseBody": { 			"StreamingDistanceMultiplier": 1 		} 	}`

Copy full snippet
```
{ "RequestId": -1, "ResponseCode": 200, "ResponseBody": { "StreamingDistanceMultiplier": 1 } }

### WebSocket Message Type - Preset.Register

Use this message type to subscribe to events emitted by a **Remote Control Preset**. Example JSON message:

```
	`{ 		"MessageName": "preset.register", 		"Parameters": { 			"PresetName": "MyPreset" 		} 	}`

Copy full snippet
```
{ "MessageName": "preset.register", "Parameters": { "PresetName": "MyPreset" } }

The following sections describe the events that are emitted by the preset and their JSON messages.

#### Remote Control Preset Event - PresetFieldsChanged

This message is sent any time someone modifies the value of a property exposed in the preset.

```
	`{ 		"Type": "PresetFieldsChanged", 		"PresetName": "MyPreset", 		"ChangedFields":  [ 			{ 					"PropertyLabel": "Relative Rotation (LightSource_0)", 					"ObjectPath": "/Game/ThirdPerson/Maps/ThirdPersonMap.ThirdPersonMap:PersistentLevel.DirectionalLight_0.LightComponent0", 					"PropertyValue":  { 						"Pitch": 346.4, 						"Yaw": 0, 						"Roll": 169.2 					} 			} 			] 		}`

Copy full snippet
```
{ "Type": "PresetFieldsChanged", "PresetName": "MyPreset", "ChangedFields": \[ { "PropertyLabel": "Relative Rotation (LightSource\_0)", "ObjectPath": "/Game/ThirdPerson/Maps/ThirdPersonMap.ThirdPersonMap:PersistentLevel.DirectionalLight\_0.LightComponent0", "PropertyValue": { "Pitch": 346.4, "Yaw": 0, "Roll": 169.2 } } \] }

#### Remote Control Preset Event - PresetFieldsAdded

This message is sent any time a property is exposed to the preset. The response only includes the group to which the property was added.

```
	`{ 		"Type": "PresetFieldsAdded", 		"PresetName": "MyPreset", 		"Description": { 			"Name": "MyPreset", 			"Path": "/Game/Presets/MyPreset.MyPreset", 			"Groups": [ 				{ 					"Name": "Lighting", 					"ExposedProperties": [ 						{ 							"DisplayName": "Light Color (LightSource_0)", 							"UnderlyingProperty": { 								"Name": "LightColor", 								... 							} 						} 					], 					"ExposedFunctions": [] 				} 			] 		} 	}`

Copy full snippet
```
{ "Type": "PresetFieldsAdded", "PresetName": "MyPreset", "Description": { "Name": "MyPreset", "Path": "/Game/Presets/MyPreset.MyPreset", "Groups": \[ { "Name": "Lighting", "ExposedProperties": \[ { "DisplayName": "Light Color (LightSource\_0)", "UnderlyingProperty": { "Name": "LightColor", ... } } \], "ExposedFunctions": \[\] } \] } }

#### Remote Control Preset Event - PresetFieldsRemoved

This message is sent any time a property or function is removed from the preset.

```
	`{ 		"Type": "PresetFieldsRemoved", 		"PresetName": "MyPreset", 		"RemovedFields": [ 			"Light Color (LightSource_0)" 		] 	}`

Copy full snippet
```
{ "Type": "PresetFieldsRemoved", "PresetName": "MyPreset", "RemovedFields": \[ "Light Color (LightSource\_0)" \] }

#### Remote Control Preset Event - PresetFieldsRenamed

This message is sent any time a property or function is renamed in the preset.

```
	`{ 		"Type": "PresetFieldsRenamed", 		"PresetName": "MyPreset", 		"RenamedFields": [ 			{ 				"OldFieldLabel": "Relative Rotation (LightSource_0)", 				"NewFieldLabel": "Directional Light Rotation" 			} 		] 	}`

Copy full snippet
```
{ "Type": "PresetFieldsRenamed", "PresetName": "MyPreset", "RenamedFields": \[ { "OldFieldLabel": "Relative Rotation (LightSource\_0)", "NewFieldLabel": "Directional Light Rotation" } \] }

### WebSocket Message Type - Preset.Unregister

Use this message type to unsubscribe from events emitted by a **Remote Control Preset**. Example JSON message:

```
	`{ 		"MessageName": "preset.unregister", 		"Parameters": { 			"PresetName": "MyPreset" 		} 	}`

Copy full snippet
```
{ "MessageName": "preset.unregister", "Parameters": { "PresetName": "MyPreset" } }

## Sample HTML/JavaScript File

1.  Save the following code in a file named **index.html**.
    
    ```
    	``<!DOCTYPE html> 	<html> 	<head></head> 	<body> 		<h3 id="status">Connection Closed</h3> 		<input id="in"></input> 		<button id="btn" onclick="sendMessage()">Register Preset</button> 		<div id="holder"></div> 		<script> 			// Variable to hold the WebSocket connection if it's successful. 			var connection = null;  			/** 			* This function sends a WebSocket message to subscribe to events emitted by a Remote Control Preset. 			* The Remote Control Preset is specified by the user in the HTML input field. 			*/ 			function sendMessage() { 				if (connection) { 					let input = document.getElementById("in"); 					const registerPayload = { 						"MessageName": "preset.register", 						"Parameters": { 							"PresetName": `${input.value}` 						} 					}; 					connection.send(JSON.stringify(registerPayload)); 				} 			}  			/** 			* This function is called every time the page loads. 			* It sets up a WebSocket connection and updates the page with "Connection Open" if the connection is successful. 			* Any message it receives from the WebSocket server, it converts from JSON to HTML elements and renders them on the page. 			* It also logs the full JSON message responses in the console. 			*/ 			window.onload = function() { 				console.log("Starting test") 				connection = new WebSocket('ws://127.0.0.1:30020'); 				connection.onopen = function () { 					document.getElementById("status").innerHTML = "Connection Open"; 				}; 				connection.onerror = function (error) {}; 				connection.onmessage = function (message) { 					if (message.data instanceof Blob) { 						reader = new FileReader(); 						reader.onload = () => { 							let holder = document.getElementById("holder"); 							let par = document.createElement("pre"); 							par.style = style="white-space: pre-line"; 							let json = JSON.parse(reader.result); 							let text = json.Type; 							par.innerHTML = text; 							holder.appendChild(par); 							console.log(reader.result) 						}; 						reader.readAsText(message.data); 					} else {} 				}; 				connection.onclose = function(event) { 				console.log("WebSocket is closed now."); 				}; 			} 		</script> 	</body> 	</html>``
    Copy full snippet
    ```
    <!DOCTYPE html> <html> <head></head> <body> <h3 id="status">Connection Closed</h3> <input id="in"></input> <button id="btn" onclick="sendMessage()">Register Preset</button> <div id="holder"></div> <script> // Variable to hold the WebSocket connection if it's successful. var connection = null; /\*\* \* This function sends a WebSocket message to subscribe to events emitted by a Remote Control Preset. \* The Remote Control Preset is specified by the user in the HTML input field. \*/ function sendMessage() { if (connection) { let input = document.getElementById("in"); const registerPayload = { "MessageName": "preset.register", "Parameters": { "PresetName": \`${input.value}\` } }; connection.send(JSON.stringify(registerPayload)); } } /\*\* \* This function is called every time the page loads. \* It sets up a WebSocket connection and updates the page with "Connection Open" if the connection is successful. \* Any message it receives from the WebSocket server, it converts from JSON to HTML elements and renders them on the page. \* It also logs the full JSON message responses in the console. \*/ window.onload = function() { console.log("Starting test") connection = new WebSocket('ws://127.0.0.1:30020'); connection.onopen = function () { document.getElementById("status").innerHTML = "Connection Open"; }; connection.onerror = function (error) {}; connection.onmessage = function (message) { if (message.data instanceof Blob) { reader = new FileReader(); reader.onload = () => { let holder = document.getElementById("holder"); let par = document.createElement("pre"); par.style = style="white-space: pre-line"; let json = JSON.parse(reader.result); let text = json.Type; par.innerHTML = text; holder.appendChild(par); console.log(reader.result) }; reader.readAsText(message.data); } else {} }; connection.onclose = function(event) { console.log("WebSocket is closed now."); }; } </script> </body> </html>
    
2.  Open the index.html file in your web browser. The page will say **Connection Open** if it was able to successfully connect to the WebSocket server.
    
    ![Screenshot of test HTML/JavaScript page](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b883d978-bf73-45ac-ae84-15e419260383/image_1.png)
3.  Enter the name of a **Remote Control Preset** in the input field and change the preset's fields.
    
4.  Open your browser's console log and verify that response messages were logged.