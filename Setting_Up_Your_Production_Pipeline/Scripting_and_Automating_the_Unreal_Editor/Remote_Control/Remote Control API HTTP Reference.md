# Remote Control API HTTP Reference

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-api-http-reference-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/remote-control-api-http-reference-for-unreal-engine)  
**Processed:** 2025-06-14 16:46:25

---

This page describes the HTTP endpoints offered by the Remote Control API, and details the format of the message body you need to include when you call each endpoint.

## GET remote/info

Use this endpoint to see all the HTTP routes available in the Remote Control API. The call returns a JSON payload with all the available HTTP routes and their descriptions.

### Example

Send the request with an empty request body. A successful request returns a 200 status with the following response body:

```
	`{ 		"HttpRoutes": [ 			{ 				"Path": "/remote/info", 				"Verb": "Get", 				"Description": "Get information about different routes available on this API." 			}, 			{ 				"Path": "/remote", 				"Verb": "Options", 				"Description": "Allows cross-origin http requests to the API." 			}, 			{ 				"Path": "/remote/batch", 				"Verb": "Put", 				"Description": "Allows batching multiple calls into one request." 			} 			... 		] 	}`

Copy full snippet
```
{ "HttpRoutes": \[ { "Path": "/remote/info", "Verb": "Get", "Description": "Get information about different routes available on this API." }, { "Path": "/remote", "Verb": "Options", "Description": "Allows cross-origin http requests to the API." }, { "Path": "/remote/batch", "Verb": "Put", "Description": "Allows batching multiple calls into one request." } ... \] }

## PUT remote/object/call

Use this endpoint to call a function exposed by a specified `UObject` that is currently in memory in the Editor: typically an Actor in the current Level or an Asset in your Project.

You can call any function that is callable from Blueprint. This includes any function defined in C++ with the `BlueprintCallable` specifier, or any function that is defined and implemented entirely in Blueprint.

When you call this endpoint, you must pass a JSON payload with the following properties:

| Property | Description |
| --- | --- |
| `objectPath` | 
The path that uniquely identifies the `UObject` you want to interact with. For more information on finding this path, see [About UObject Paths](/documentation/en-us/unreal-engine/remote-control-api-http-reference-for-unreal-engine#aboutuobjectpaths) below.



 |
| `functionName` | 

The name of the function you want to call from the specified `UObject`. If your function is defined in C++, its original name may not match the display name shown in Blueprint. In this case, use the function name defined in C++.



 |
| `parameters` | 

An object that defines the parameters you want to pass to the function.

-   The name of each property in this object should be the name of a parameter accepted by the function you call.

```
	``If your function is defined in C++, the original parameter name may not match the value you see in the Blueprint Editor. In this case, use the paramter name defined in C++. For example, in the code below, the second parameter needs to be specified as `bSweep` to match its C++ definition, although it is exposed in the equivalent Blueprint node as **Sweep**.``

Copy full snippet
```
If your function is defined in C++, the original parameter name may not match the value you see in the Blueprint Editor. In this case, use the paramter name defined in C++. For example, in the code below, the second parameter needs to be specified as \`bSweep\` to match its C++ definition, although it is exposed in the equivalent Blueprint node as \*\*Sweep\*\*.

-   The value of the property may be any simple value such as a number or a Boolean value. Or, if the function requires you to pass an object, you can provide a JSON object that encapsulates the properties of that object. The Remote Control system will use the values you provide to attempt to create a new object of the necessary type. For example, in the code below, the `NewLocation` is automatically used to create a new Vector.

You don't have to include a property in this object for every parameter the function accepts. For any parameter that you omit, the Web Remote Control system will construct a default object of the appropriate type.



 |
| `generateTransaction` | 

Defines whether or not the Editor should record this function call in the Project's transaction history. Setting this property to `true` has the following effects:

-   Any changes made by the function will be undoable. The Editor records an entry in the Project's **Undo History** panel for this function call. A user working in the Unreal Editor can then roll back the effect of the change. This entry is always under the name **Remote Call Transaction Wrap**, regardless of the function you call:
    
    ![Remote transactions listed in the Undo History](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f04b3c82-9460-4806-a8c7-e2905f21b661/remote-call-transaction-wrap.png "Remote transactions listed in the Undo History")
-   If you're in a [Multi-User Editing](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine) session, the change will be replicated to other connected users.
    



 |

The call returns a JSON payload that contains the return value of the function called, along with any other output parameters specified in the function's definition.

### Example

Request body:

```
	`{ 		"objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5", 		"functionName" : "SetActorLocation", 		"parameters" : { 			"NewLocation" : {"X" : 100, "Y" : 0, "Z" : 30},   // These values are used to create a new Vector 			"bSweep" : true 		}, 		"generateTransaction" : true 	}`

Copy full snippet
```
{ "objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5", "functionName" : "SetActorLocation", "parameters" : { "NewLocation" : {"X" : 100, "Y" : 0, "Z" : 30}, // These values are used to create a new Vector "bSweep" : true }, "generateTransaction" : true }

A successful request gives a `200` status with the following response body:

```
	`{ 		"SweepHitResult":{ 			"bBlockingHit":true, 			"bStartPenetrating":false, 			"FaceIndex":-1, 			"Time":0.338644, 			"Distance":170.822, 			"Location":{ "X":100, "Y":0, "Z":429.178 }, 			"ImpactPoint":{ "X":169, "Y":30, "Z":354 }, 			"Normal":{ "X":-1.51964e-11, "Y":4.01851e-8, "Z":1 }, 			"ImpactNormal":{ "X":-1.51964e-11, "Y":4.01851e-8, "Z":1 }, 			"TraceStart":{ "X":100, "Y":0, "Z":600 }, 			"TraceEnd":{ "X":100, "Y":0, "Z":100 }, 			"PenetrationDepth":0, 			"Item":-1, 			"PhysMaterial":"", 			"Actor":"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Bump_StaticMesh", 			"Component":"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Bump_StaticMesh.StaticMeshComponent0", 			"BoneName":"None", 			"MyBoneName":"None" 		}, 		"ReturnValue":true 	}`

Copy full snippet
```
{ "SweepHitResult":{ "bBlockingHit":true, "bStartPenetrating":false, "FaceIndex":-1, "Time":0.338644, "Distance":170.822, "Location":{ "X":100, "Y":0, "Z":429.178 }, "ImpactPoint":{ "X":169, "Y":30, "Z":354 }, "Normal":{ "X":-1.51964e-11, "Y":4.01851e-8, "Z":1 }, "ImpactNormal":{ "X":-1.51964e-11, "Y":4.01851e-8, "Z":1 }, "TraceStart":{ "X":100, "Y":0, "Z":600 }, "TraceEnd":{ "X":100, "Y":0, "Z":100 }, "PenetrationDepth":0, "Item":-1, "PhysMaterial":"", "Actor":"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Bump\_StaticMesh", "Component":"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Bump\_StaticMesh.StaticMeshComponent0", "BoneName":"None", "MyBoneName":"None" }, "ReturnValue":true }

In this case, the `SweepHitResult` is included in the return value because the original definition of the `SetActorLocation()` function in the `Engine/Source/Runtime/Engine/Classes/GameFramework/Actor.h` file defines it as an output parameter: that is, a non-const reference to a data value that is produced by the function call.

## PUT remote/object/property

Use this endpoint to access property values exposed by a specified UObject currently in memory in the Editor: typically an Actor or an Asset.

If the UObject you are accessing is an instance of a C++ class, this includes any class members defined in C++ as properties that are accessible to Blueprint, subject to the restrictions below.

If the UObject you are accessing is an instance of a Blueprint class, this includes any Blueprint variables owned by that class, subject to the restrictions below.

This endpoint can only access properties that meet certain criteria:

-   The property must be defined as `public`. It may not be `private` or `protected`.
-   It must not have any `BlueprintGetter` or `BlueprintSetter` functions defined. If it does, you must use those functions with the `remote/object/call` endpoint described above instead of trying to read or write the values directly using the `remote/object/property` endpoint.
-   If you are accessing the object in the Editor, the property must be set as `EditAnywhere`. In order to modify the value, the property must not be set as `EditConst`.
-   If you are accessing an object in `-game` mode or Play In Editor (PIE) mode, the property must be set as `BlueprintVisible`. In order to modify the value, the property must not be set as `BlueprintReadOnly`.

Depending on the way you construct your request message, you can:

-   Request all available properties exposed by the object, along with their current values.
-   Request the value of any property that offers at least read access.
-   Set the value of any properties that offer write access.

When you call this endpoint, you must pass a JSON payload with the following properties:

| Property | Description |
| --- | --- |
| `objectPath` | 
The path that uniquely identifies the `UObject` you want to interact with. For more information on finding this path, see [About UObject Paths](/documentation/en-us/unreal-engine/remote-control-api-http-reference-for-unreal-engine#aboutuobjectpaths) below.



 |
| `propertyName` | 

The name of the property you want to read or modify. If you omit this property in a call with `READ_ACCESS`, the response will list all readable properties available on the specified `UObject`.



 |
| `access` | 

Defines the kind of access request you are making for the property. This can be any of the following values:

-   `READ_ACCESS` specifies that you are making a request for the current value of a property, or for all properties on the specified `UObject`.
-   `WRITE_ACCESS` specifies that you want to set a new value for one or more properties, which you define in the `propertyValue` object.
-   `WRITE_TRANSACTION_ACCESS` is the same as `WRITE_ACCESS`, but records the property value change in the Project's transaction history. This is similar to the `generateTransaction` property of the `remote/object/call` endpoint. It has the following effects:
    -   The Editor handles the property modification exactly as if it had been done in the **Details** panel of the Unreal Editor. This may invoke additional code inside the Editor to handle pre-change and post-change events linked to that property.
    -   If you're in a [Multi-User Editing](/documentation/en-us/unreal-engine/multi-user-editing-in-unreal-engine) session, the change will be replicated to other connected users.
    -   This option makes the change undoable. If you set this property to `true`, the Editor records an entry in the Project's **Undo History** panel for this property change. A user working in the Unreal Editor can then roll back the effect of the change. This entry is always under the name **Remote Set Object Property**:
        
        ![Remote Set Object Property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3bf94f62-8b25-4caa-ba5f-972de7a44b33/remote-set-object-property.png "Remote Set Object Property")



 |
| `propertyValue` | 

When you make a request with `WRITE_ACCESS` or `WRITE_TRANSACTION_ACCESS`, you use this object to specify the properties you want to modify, and the new value you want to set for each of those properties.

This must be a JSON object in which the name of each field matches the name of a writeable property on the specified `UObject`, and the value of each field is the new value that you want to set for that property.



 |

The call returns a JSON payload that contains the information you requested, or the result of your write request.

### Examples

#### Reading all Properties

Request body:

```
	`{ 		"objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5", 		"access" : "READ_ACCESS" 	}`

Copy full snippet
```
{ "objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5", "access" : "READ\_ACCESS" }

A successful request gives a `200` status with the following response body:

```
	`{ 		"bStaticMeshReplicateMovement": false, 		"NavigationGeometryGatheringMode": "Default", 		"PrimaryActorTick": { 			"TickGroup": "TG_PrePhysics", 			"EndTickGroup": "TG_PrePhysics", 			"bTickEvenWhenPaused": false, 			"bCanEverTick": false, 			"bStartWithTickEnabled": true, 			"bAllowTickOnDedicatedServer": true, 			"TickInterval": 0 		}, 		"bHidden": false, 		"bOnlyRelevantToOwner": false, 		"bAlwaysRelevant": false, 		"bReplicateMovement": false, 		"bNetLoadOnClient": true, 		"bNetUseOwnerRelevancy": false, 		"bRelevantForLevelBounds": true, 		"bReplayRewindable": false, 		"bAllowTickBeforeBeginPlay": false, 		"bBlockInput": false, 		"bCanBeDamaged": false, 		"bFindCameraComponentWhenViewTarget": true, 		"bGenerateOverlapEventsDuringLevelStreaming": false, 		"bIgnoresOriginShifting": false, 		"bEnableAutoLODGeneration": true, 		"bIsEditorOnlyActor": false, 		"ReplicatedMovement": { 			"LinearVelocity": { "X": 0, "Y": 0, "Z": 0 }, 			"AngularVelocity": { "X": 0, "Y": 0, "Z": 0 }, 			"Location": { "X": 0, "Y": 0, "Z": 0 }, 			"Rotation": { "Pitch": 0, "Yaw": 0, "Roll": 0 }, 			"bSimulatedPhysicSleep": false, 			"bRepPhysics": false, 			"LocationQuantizationLevel": "RoundWholeNumber", 			"VelocityQuantizationLevel": "RoundWholeNumber", 			"RotationQuantizationLevel": "ByteComponents" 		}, 		"InitialLifeSpan": 0, 		"NetDormancy": "DORM_Awake", 		"SpawnCollisionHandlingMethod": "AlwaysSpawn", 		"AutoReceiveInput": "Disabled", 		"InputPriority": 0, 		"NetCullDistanceSquared": 2.25e+08, 		"NetUpdateFrequency": 100, 		"MinNetUpdateFrequency": 2, 		"NetPriority": 1, 		"SpriteScale": 1, 		"Tags": [] 	}`

Copy full snippet
```
{ "bStaticMeshReplicateMovement": false, "NavigationGeometryGatheringMode": "Default", "PrimaryActorTick": { "TickGroup": "TG\_PrePhysics", "EndTickGroup": "TG\_PrePhysics", "bTickEvenWhenPaused": false, "bCanEverTick": false, "bStartWithTickEnabled": true, "bAllowTickOnDedicatedServer": true, "TickInterval": 0 }, "bHidden": false, "bOnlyRelevantToOwner": false, "bAlwaysRelevant": false, "bReplicateMovement": false, "bNetLoadOnClient": true, "bNetUseOwnerRelevancy": false, "bRelevantForLevelBounds": true, "bReplayRewindable": false, "bAllowTickBeforeBeginPlay": false, "bBlockInput": false, "bCanBeDamaged": false, "bFindCameraComponentWhenViewTarget": true, "bGenerateOverlapEventsDuringLevelStreaming": false, "bIgnoresOriginShifting": false, "bEnableAutoLODGeneration": true, "bIsEditorOnlyActor": false, "ReplicatedMovement": { "LinearVelocity": { "X": 0, "Y": 0, "Z": 0 }, "AngularVelocity": { "X": 0, "Y": 0, "Z": 0 }, "Location": { "X": 0, "Y": 0, "Z": 0 }, "Rotation": { "Pitch": 0, "Yaw": 0, "Roll": 0 }, "bSimulatedPhysicSleep": false, "bRepPhysics": false, "LocationQuantizationLevel": "RoundWholeNumber", "VelocityQuantizationLevel": "RoundWholeNumber", "RotationQuantizationLevel": "ByteComponents" }, "InitialLifeSpan": 0, "NetDormancy": "DORM\_Awake", "SpawnCollisionHandlingMethod": "AlwaysSpawn", "AutoReceiveInput": "Disabled", "InputPriority": 0, "NetCullDistanceSquared": 2.25e+08, "NetUpdateFrequency": 100, "MinNetUpdateFrequency": 2, "NetPriority": 1, "SpriteScale": 1, "Tags": \[\] }

#### Reading a Single Property

Request body:

```
	`{ 		"objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5.StaticMeshComponent0", 		"propertyName" : "StreamingDistanceMultiplier", 		"access" : "READ_ACCESS", 	}`

Copy full snippet
```
{ "objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5.StaticMeshComponent0", "propertyName" : "StreamingDistanceMultiplier", "access" : "READ\_ACCESS", }

A successful request gives a `200` status with the following response body:

```
	`{ 		"StreamingDistanceMultiplier": 1 	}`

Copy full snippet
```
{ "StreamingDistanceMultiplier": 1 }

#### Writing Properties

Request body:

```
	`{ 		"objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5.StaticMeshComponent0", 		"access" : "WRITE_ACCESS", 		"propertyName" : "StreamingDistanceMultiplier", 		"propertyValue" : { 			"StreamingDistanceMultiplier" : 2 		} 	}`

Copy full snippet
```
{ "objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5.StaticMeshComponent0", "access" : "WRITE\_ACCESS", "propertyName" : "StreamingDistanceMultiplier", "propertyValue" : { "StreamingDistanceMultiplier" : 2 } }

A successful request gives a `200` status with an empty response body.

## PUT remote/object/thumbnail

Use this endpoint to retrieve the thumbnail image of an Asset in the **Content Browser**. The call returns a JSON payload that contains the thumbnail.

### Example

Request body:

```
	`{ 		"objectPath" : "/Game/Mannequin/Animations/ThirdPersonJump_Start.ThirdPersonJump_Start" 	}`

Copy full snippet
```
{ "objectPath" : "/Game/Mannequin/Animations/ThirdPersonJump\_Start.ThirdPersonJump\_Start" }

A successful request returns a 200 status with the thumbnail image in the response body:

![image alt text](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/dd24a586-0ac4-4e03-8e20-d83cee03b97c/image_0.png)

## PUT remote/search/assets

Use this endpoint to search for an Asset in the Asset Registry.

When you call this endpoint, you must pass a JSON payload with the following properties:

| Property | Description |
| --- | --- |
| Query | The text you want to match in an asset's name. Leaving this field an empty string returns all results. |
| Filter | 
A JSON object to specify how you want to filter the requested assets with the following optional properties:

-   **PackageNames:** Restricts the search to exact matches of the specified packages. The format of the value is an array of strings, such as \["/Game/MyFolder/MyAsset"\].
-   **ClassNames:** Restricts the search to exact matches of the specified class names. The format of the value is an array of strings.
-   **PackagePaths:** Restricts the search to any packages that contain the specified paths. For example, \["/Game/MyFolder"\] will only return assets with "/Game/MyFolder" in their asset path. The format of the value is an array of strings.
-   **RecursiveClassesExclusionSet:** When searching for matching classes recursively, you can specify any classes you want to exclude from the results. The format of the value is an array of strings.
-   **RecursivePaths:** A boolean specifying whether to search subfolders of the paths specified in PackagePaths.
-   **RecursiveClasses:** A boolean specifying whether to look at subclasses of classes specified in ClassNames.



 |

The call returns a JSON payload that contains the information you requested.

### Example

Request body:

```
	`{ 		"Query": "Cube", 		"Filter": { 			"PackageNames": [], 			"ClassNames": [], 			"PackagePaths": [], 			"RecursiveClassesExclusionSet": [], 			"RecursivePaths": false, 			"RecursiveClasses": false 		} 	}`

Copy full snippet
```
{ "Query": "Cube", "Filter": { "PackageNames": \[\], "ClassNames": \[\], "PackagePaths": \[\], "RecursiveClassesExclusionSet": \[\], "RecursivePaths": false, "RecursiveClasses": false } }

A successful request returns a 200 status with the following response body:

```
	`{ 		"Assets": [ 			{ 				"Name": "CubeMaterial", 				"Class": "Material", 				"Path": "/Game/Geometry/Meshes/CubeMaterial.CubeMaterial" 			}, 			{ 				"Name": "1M_Cube", 				"Class": "StaticMesh", 				"Path": "/Game/Geometry/Meshes/1M_Cube.1M_Cube" 			}, 			{ 				"Name": "1M_Cube_Chamfer", 				"Class": "StaticMesh", 				"Path": "/Game/Geometry/Meshes/1M_Cube_Chamfer.1M_Cube_Chamfer" 			} 		] 	}`

Copy full snippet
```
{ "Assets": \[ { "Name": "CubeMaterial", "Class": "Material", "Path": "/Game/Geometry/Meshes/CubeMaterial.CubeMaterial" }, { "Name": "1M\_Cube", "Class": "StaticMesh", "Path": "/Game/Geometry/Meshes/1M\_Cube.1M\_Cube" }, { "Name": "1M\_Cube\_Chamfer", "Class": "StaticMesh", "Path": "/Game/Geometry/Meshes/1M\_Cube\_Chamfer.1M\_Cube\_Chamfer" } \] }

## PUT remote/object/describe

Use this endpoint to see all the properties, functions, and other metadata about a UObject currently in memory in the Editor, such as an Actor or an Asset. The call returns a JSON payload that contains the information you requested.

### Example

Request body:

```
	`{ 		"objectPath": "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5" 	}`

Copy full snippet
```
{ "objectPath": "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5" }

A successful request returns a 200 status with the following response body:

```
	`{ 		"Name": "CubeMesh_5", 		"Class": "/Script/Engine.StaticMeshActor", 		"Properties": [ 			{ 				"Name": "StaticMeshComponent", 				"Description": "", 				"Type": "UStaticMeshComponent*", 				"ContainerType": "", 				"KeyType": "", 				"Metadata": {} 			}, 			{ 				"Name": "PrimaryActorTick", 				"Description": "Primary Actor tick function, which calls TickActor().\nTick functions can be configured to control whether ticking is enabled, at what time during a frame the update occurs, and to set up tick dependencies.\n@see https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Engine/FTickFunction/\n@see AddTickPrerequisiteActor(), AddTickPrerequisiteComponent()", 				"Type": "FActorTickFunction", 				"ContainerType": "", 				"KeyType": "", 				"Metadata": { 					"ToolTip": "Primary Actor tick function, which calls TickActor().\nTick functions can be configured to control whether ticking is enabled, at what time during a frame the update occurs, and to set up tick dependencies.\n@see https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Engine/FTickFunction/\n@see AddTickPrerequisiteActor(), AddTickPrerequisiteComponent()" 				} 			}, 			{ 				"Name": "bOnlyRelevantToOwner", 				"Description": "If true, this actor is only relevant to its owner. If this flag is changed during play, all non-owner channels would need to be explicitly closed.", 				"Type": "uint8", 				"ContainerType": "", 				"KeyType": "", 				"Metadata": { 					"ToolTip": "If true, this actor is only relevant to its owner. If this flag is changed during play, all non-owner channels would need to be explicitly closed." 				} 			}, 			... 		] 	}`

Copy full snippet
```
{ "Name": "CubeMesh\_5", "Class": "/Script/Engine.StaticMeshActor", "Properties": \[ { "Name": "StaticMeshComponent", "Description": "", "Type": "UStaticMeshComponent\*", "ContainerType": "", "KeyType": "", "Metadata": {} }, { "Name": "PrimaryActorTick", "Description": "Primary Actor tick function, which calls TickActor().\\nTick functions can be configured to control whether ticking is enabled, at what time during a frame the update occurs, and to set up tick dependencies.\\n@see https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Engine/FTickFunction/\\n@see AddTickPrerequisiteActor(), AddTickPrerequisiteComponent()", "Type": "FActorTickFunction", "ContainerType": "", "KeyType": "", "Metadata": { "ToolTip": "Primary Actor tick function, which calls TickActor().\\nTick functions can be configured to control whether ticking is enabled, at what time during a frame the update occurs, and to set up tick dependencies.\\n@see https://docs.unrealengine.com/latest/INT/API/Runtime/Engine/Engine/FTickFunction/\\n@see AddTickPrerequisiteActor(), AddTickPrerequisiteComponent()" } }, { "Name": "bOnlyRelevantToOwner", "Description": "If true, this actor is only relevant to its owner. If this flag is changed during play, all non-owner channels would need to be explicitly closed.", "Type": "uint8", "ContainerType": "", "KeyType": "", "Metadata": { "ToolTip": "If true, this actor is only relevant to its owner. If this flag is changed during play, all non-owner channels would need to be explicitly closed." } }, ... \] }

## PUT remote/batch

Use this endpoint to group multiple HTTP requests into a single remote call. The order of execution is determined by the order of the elements in the **Requests** array.

Each request element in the **Requests** array must be a JSON object with the following properties:

| Request Property | Description |
| --- | --- |
| RequestId | A unique ID to be able to match the request with the corresponding response. |
| URL | The request target, such as `/remote/object/describe`. |
| Verb | Options for the HTTP method are PUT, POST, GET, and DELETE. |
| Body | The data that is sent to the server. Not at all requests have a body. |

The call returns a JSON payload that contains an array of responses for the multiple requests. Each element in the array has the following properties:

| Response Property | Description |
| --- | --- |
| RequestId | A unique ID to match the response to the corresponding request. |
| ResponseCode | The status code of the response. A successful response returns the status 200. |
| ResponseBody | Payload containing any requested data. Not all responses have a response body. |

### Example

Request body:

```
	`{ 		"Requests" : [ 			{ 				"RequestId" : 1, 				"URL": "/remote/object/property", 				"Verb" : "PUT", 				"Body": { 					"objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5.StaticMeshComponent0", 					"propertyName": "StreamingDistanceMultiplier", 					"access" : "READ_ACCESS" 				} 			}, 			{ 				"RequestId" : 2, 				"URL": "/remote/object/property", 				"Verb" : "PUT", 				"Body": { 					"objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5.StaticMeshComponent0", 					"propertyName": "StreamingDistanceMultiplier", 					"propertyValue": { 						"StreamingDistanceMultiplier" : 2 					}, 					"access" : "WRITE_ACCESS" 				} 			}, 			{ 				"RequestId" : 3, 				"URL": "/remote/object/property", 				"Verb" : "PUT", 				"Body": { 					"objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5.StaticMeshComponent0", 					"propertyName": "StreamingDistanceMultiplier", 					"access" : "READ_ACCESS" 				} 			} 		] 	}`

Copy full snippet
```
{ "Requests" : \[ { "RequestId" : 1, "URL": "/remote/object/property", "Verb" : "PUT", "Body": { "objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5.StaticMeshComponent0", "propertyName": "StreamingDistanceMultiplier", "access" : "READ\_ACCESS" } }, { "RequestId" : 2, "URL": "/remote/object/property", "Verb" : "PUT", "Body": { "objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5.StaticMeshComponent0", "propertyName": "StreamingDistanceMultiplier", "propertyValue": { "StreamingDistanceMultiplier" : 2 }, "access" : "WRITE\_ACCESS" } }, { "RequestId" : 3, "URL": "/remote/object/property", "Verb" : "PUT", "Body": { "objectPath" : "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5.StaticMeshComponent0", "propertyName": "StreamingDistanceMultiplier", "access" : "READ\_ACCESS" } } \] }

A successful request returns the following response body with an array of responses for each request:

```
	`{ 		"Responses": [ 			{ 				"RequestId": 1, 				"ResponseCode": 200, 				"ResponseBody": { 					"StreamingDistanceMultiplier": 1 				} 			}, 			{ 				"RequestId": 2, 				"ResponseCode": 200, 				"ResponseBody": null 			}, 			{ 				"RequestId": 3, 				"ResponseCode": 200, 				"ResponseBody": { 					"StreamingDistanceMultiplier": 2 				} 			} 		] 	}`

Copy full snippet
```
{ "Responses": \[ { "RequestId": 1, "ResponseCode": 200, "ResponseBody": { "StreamingDistanceMultiplier": 1 } }, { "RequestId": 2, "ResponseCode": 200, "ResponseBody": null }, { "RequestId": 3, "ResponseCode": 200, "ResponseBody": { "StreamingDistanceMultiplier": 2 } } \] }

## PUT remote/object/event

This route is experimental. Enable it by adding the following console variable to your project's **DefaultEngine.ini** file.

```
	`[Console Variables] 	WebControl.EnableExperimentalRoutes = 1`
Copy full snippet
```
\[Console Variables\] WebControl.EnableExperimentalRoutes = 1

Use this endpoint to receive the object's next event, such as receiving an update when an object's property changes. The route will not return until the event has occurred.

The following events are currently supported:

-   ObjectPropertyChanged
    
-   PreObjectPropertyChanged
    

### Example

Request body:

```
	`{ 		"EventType": "ObjectPropertyChanged", 		"ObjectPath": "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5.StaticMeshComponent0", 		"PropertyName": "StaticMesh" 	}`

Copy full snippet
```
{ "EventType": "ObjectPropertyChanged", "ObjectPath": "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5.StaticMeshComponent0", "PropertyName": "StaticMesh" }

A successful request will not return until the event has occurred. When the StaticMesh property changes, a response with a 200 status will be returned with the following body:

```
	`{ 	"StaticMesh": "/Engine/EditorMeshes/ArcadeEditorSphere.ArcadeEditorSphere" 	}`

Copy full snippet
```
{ "StaticMesh": "/Engine/EditorMeshes/ArcadeEditorSphere.ArcadeEditorSphere" }

## About UObject Paths

Every Asset and Actor that the Unreal Editor has loaded in memory has a path that uniquely identifies it. These paths are mostly for internal use within the Editor, so they aren't directly exposed to you in a way that's easy to access. And, because they're determined programmatically according to internal rules, they aren't always easy to predict.

In general, these object paths follow the format:

```
	`/path/PackageName.ObjectName:SubObjectName.SubObject`

Copy full snippet
```
/path/PackageName.ObjectName:SubObjectName.SubObject

Programmers who work with the Engine in C++ may recognize this format as the same one accepted by functions like `FindObject()` and `StaticFindObject()`.

For example, to deconstruct an Actor path shown in the request examples above:

|   |   |
| --- | --- |
| `/Game/ThirdPersonBP/Maps/` | The path to the Asset in the Content Browser. |
| `ThirdPersonExampleMap.ThirdPersonExampleMap:` | The name of the package and the object it contains (for many Assets, these will be the same). |
| `PersistentLevel.CubeMesh_5.StaticMeshComponent0` | The path through a hierarchy of sub-objects to the object you want to affect. |

Although these paths are not easily exposed to view, the following sections describe some ways you can get at them.

### Paths in the Undo History

When you modify a UObject, you can view its path in the **Undo History** panel.

1.  Click the filter icon at the bottom right of the panel and enable **Show transactions details.**
    
    ![Show transactions details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4a2f03b4-4d96-4775-8be8-4ab53b798af9/transaction-details.png "Show transactions details")
2.  Make a minor change to the Asset or Actor you want to access, such as moving an Actor to a new location. This will record a new transaction in the **Undo History**.
    
3.  In the **Transaction Details** panel, hover over the entries in the **Modified objects and properties** column. The Tooltip contains the path to the highlighted object.
    
    ![Object path shown in the Tooltip](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d8792b86-b511-4006-a45f-c6407436db1d/object-path-tooltip.png "Object path shown in the Tooltip")

### Paths in the Editor Scripting Utilities

Depending on the types of tasks you want to carry out remotely, it may be helpful for your web application to be aware of the paths for the Actors available in the current Level, or for Assets that exist in the Content Browser. The **Editor Scripting Utilities** Plugin exposes some helpful functions for interacting with Assets and Levels that you can use to achieve this.

For example, to get a list of the paths for all Actors in the current Level, you can remotely call the `GetAllLevelActors` function exposed by the `EditorLevelLibrary` class in the `EditorScriptingUtilities` module. Send the following request body to the `remote/object/call` endpoint:

```
	`{ 		"objectPath" : "/Script/EditorScriptingUtilities.Default__EditorLevelLibrary", 		"functionName":"GetAllLevelActors" 	}`

Copy full snippet
```
{ "objectPath" : "/Script/EditorScriptingUtilities.Default\_\_EditorLevelLibrary", "functionName":"GetAllLevelActors" }

The `ReturnValue` field in the response body gives you an array of paths for all Actors in the Level. For example:

```
	`{ 		"ReturnValue": [ 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LightmassImportanceVolume_0", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.AtmosphericFog_1", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.SkySphereBlueprint", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.SphereReflectionCapture", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.NetworkPlayerStart", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.DocumentationActor1", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Linear_Stair_StaticMesh", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Bump_StaticMesh", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LeftArm_StaticMesh", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.RightArm_StaticMesh", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Ramp_StaticMesh", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh_5", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LightSource_0", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.PostProcessVolume_0", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.SkyLight_0", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Floor_1", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall7_4", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall9", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall10", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall11", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.TextRenderActor_1", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.MyBlueprint_5", 			"/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.ThirdPersonCharacter_167" 		] 	}`

Copy full snippet
```
{ "ReturnValue": \[ "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LightmassImportanceVolume\_0", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.AtmosphericFog\_1", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.SkySphereBlueprint", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.SphereReflectionCapture", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.NetworkPlayerStart", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.DocumentationActor1", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Linear\_Stair\_StaticMesh", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Bump\_StaticMesh", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LeftArm\_StaticMesh", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.RightArm\_StaticMesh", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Ramp\_StaticMesh", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.CubeMesh\_5", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LightSource\_0", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.PostProcessVolume\_0", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.SkyLight\_0", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Floor\_1", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall7\_4", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall9", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall10", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.Wall11", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.TextRenderActor\_1", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.MyBlueprint\_5", "/Game/ThirdPersonBP/Maps/ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.ThirdPersonCharacter\_167" \] }

For details on installing the **Editor Scripting Utilities** Plugin, see [Scripting and Automating the Editor](/documentation/en-us/unreal-engine/scripting-and-automating-the-unreal-editor).

During [Play in Editor (PIE)](/documentation/en-us/unreal-engine/playing-and-simulating-in-unreal-engine) mode, **UEDPIE\_X\_** is added as a prefix to the Map's name, where **X** is the PIE instance ID. Using the first returned value above as an example, the object path during PIE would be:

```
	`"objectPath" : "/Game/ThirdPersonBP/Maps/UEDPIE_0_ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LightmassImportanceVolume_0"`
Copy full snippet
```
"objectPath" : "/Game/ThirdPersonBP/Maps/UEDPIE\_0\_ThirdPersonExampleMap.ThirdPersonExampleMap:PersistentLevel.LightmassImportanceVolume\_0"

### Paths for Blueprint Function Libraries

To remotely call custom [Blueprint Function Libraries](/documentation/en-us/unreal-engine/blueprint-function-libraries-in-unreal-engine) with static methods, the object path must point to the [Class Default Object (CDO)](/documentation/en-us/unreal-engine/objects-in-unreal-engine), which is the one object that a UCLASS maintains. The following sections explain how to build the object path for C++ and Python objects.

#### C++

The object path to a CDO in C++ follows the format:

```
	`/Script/ModuleName.Default__ClassName`

Copy full snippet
```
/Script/ModuleName.Default\_\_ClassName

The table below describes how to find the values for ModuleName and ClassName for your Blueprint Function Library.

<table class="table" style="--columns-count: 2;"><tbody><tr><td>ModuleName</td><td>ModuleName is the name of the DLL that contains the class you are looking for. In your Visual Studio project, there is a <strong>.build.cs</strong> file with the same name as the module, which specifies how that module should be built as well as the module's dependencies.</td></tr><tr><td>ClassName</td><td>ClassName is the name of the class, which has a UCLASS macro.</td></tr></tbody></table>

#### Python

The object path to a CDO in Python follows the format:

```
	`/Engine/PythonTypes.Default__ClassName`
Copy full snippet
```
/Engine/PythonTypes.Default\_\_ClassName

ClassName is the name of the class, which has a `@unreal.uclass()` decorator.