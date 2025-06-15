# Device Properties

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/device-properties-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/device-properties-in-unreal-engine)  
**Processed:** 2025-06-14 16:20:40

---

**Device Properties** represent the physical properties of an input deviceThese include properties such as light color display or haptic trigger resistance. You can activate device properties by:

-   Using the **Input Device subsystem**.
-   Adding to an existing [Force Feedback Asset](/documentation/en-us/unreal-engine/force-feedback-in-unreal-engine) in the Device Properties category.
-   Using a **Burst Gameplay Cue Notify Blueprint**.

The list of devices is populated by a config file so third-party vendors can add their own devices as an option. By default, Unreal has console support. You can see these config settings in the editor by navigating to **Project Settings** > **Input** > **Platform Settings** > (**Platform**) > **Hardware**.

For example, a PlayStation5 can have a DualSense or a DualShock4 as an option.

![Device Property Overview](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/04e05deb-1f77-46a0-b4d9-43f87f1de118/devicepropertyoverview.png)

You can make your input triggers have haptic resistance based on the type of weapon you have, or change light color over time for special effects, and other gameplay possibilities.

You can use the Input Device Subsystem in Blueprints or C++. The system features:

-   The capability to create controller input functionality such as getting the "Most recently used hardware device".
-   A listener to the `OnInputHardwareDeviceChanged` delegate to make a responsive User Interface on a PC or Console for when a user changes input devices, such as changing from a keyboard to a controller, without having to use the [Common UI](/documentation/en-us/unreal-engine/common-ui-plugin-for-advanced-user-interfaces-in-unreal-engine) plugin.

## The Lifetime of Device Properties

Device Properties have a simple lifetime that you can customize with exposed virtual functions. Each device property has a **duration**, which work in the same manner as a Force Feedback effect's duration attribute. Properties are **activated**, **evaluated**, **applied**, and then reset once they have reached their duration.

| Function | Description |
| --- | --- |
| `Evaluate Device Property` | 
Override the `EvaluateDeviceProperty()` function to change the data on your device property. The function is called every tick and gives access to the current duration so you can get state changes such as the value of curve types over time.

See the `UColorInputDeviceCurveProperty::EvaluateDeviceProperty` class Implementation for a simple example in C++, or the `B_TeamColor_DeviceProperty` Blueprint located in the [Lyra Game sample](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine).



 |
| `Apply Device Property` | Override this function to change how the internals of your property are being passed along to the platform code. |
| `Reset Device Property` | Called when the duration of your device property is reached. You can use this function as a chance to reset any state changes you may have made to your device property, such as resetting the light color back to what it was when it was first applied. |

## How To Use Input Devices

Once you know what input device property you want to use, you can **activate** it with the ***Input Device Subsystem.*** When you activate a device property, you are given an **Input Device Property Handle**. This handle can be used to get the current state of the property from the Input Device Subsystem, as well as remove or reset it if needed.

When you want to activate a property, you have a few options that are configurable from the `FActivateDevicePropertyParams` struct.

| Struct Property | Description |
| --- | --- |
| User Id | The Platform User ID of the owning player whose input device you want to set |
| Device Id | The Input Device ID to activate this property on. If this is not explicitly set, then the default device of the given User Id will be used. |
| Looping | If true, then this property should loop once its lifetime is over. |
| Ignore Time Dilation | If true, then this property will ignore any time dilation when it is being evaluated. |
| Play while paused | Should this property be applied, even if the game is paused? |

#### C++

You can manually activate input device properties with the Input Device Subsystem in C++.

**ManualExample.h**

```
	`| // In the header file... 	// An Instanced device property. Use this if you want to be able to edit the properties in the details panel 	UPROPERTY(EditDefaultsOnly, Instanced, BlueprintReadOnly, Category = "Input Devices") 	TObjectPtr<UInputDeviceProperty> DevicePropertyInstance; 	  	// Or you can use a subclass if you don't have any properties you want to change in the details panel. 	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Input Devices") 	TSubclassOf<UInputDeviceProperty> DevicePropertyClass; |`
Copy full snippet
```
| // In the header file... // An Instanced device property. Use this if you want to be able to edit the properties in the details panel UPROPERTY(EditDefaultsOnly, Instanced, BlueprintReadOnly, Category = "Input Devices") TObjectPtr<UInputDeviceProperty> DevicePropertyInstance; // Or you can use a subclass if you don't have any properties you want to change in the details panel. UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = "Input Devices") TSubclassOf<UInputDeviceProperty> DevicePropertyClass; |

**ManualExample.cpp**

```
	`| // In the cpp file... 	#include "GameFramework/InputDeviceSubsystem.h" 	#include "GameFramework/InputDeviceProperties.h" 	  	**void** ApplyProperties() 	{ 		**const** FPlatformUserId UserId = GetOwningUserId(); 	  		**if** (UserId.IsValid()) 		{ 			**if** (UInputDeviceSubsystem* InputDeviceSubsystem = UInputDeviceSubsystem::Get()) 			{     					FActivateDevicePropertyParams Params = {}; 					Params.UserId = UserId; 	  					// By default, the device property will be played on the Platform User's Primary Input Device. 					// If you want to override this and set a specific device, then you can set the DeviceId parameter. 					//Params.DeviceId = <some specific device id>; 				  					// Uses the given instanced property and modifies it. Use this carefully 					FInputDevicePropertyHandle Handle = InputDeviceSubsystem->ActivateDeviceProperty(DeviceProp, Params); 	  					// Spawns a new instance of this device property class and uses that 					FInputDevicePropertyHandle Handle = InputDeviceSubsystem->ActivateDevicePropertyOfClass(DeviceProp, Params);     		 }  		} 	} 	 |`

Copy full snippet
```
| // In the cpp file... #include "GameFramework/InputDeviceSubsystem.h" #include "GameFramework/InputDeviceProperties.h" \*\*void\*\* ApplyProperties() { \*\*const\*\* FPlatformUserId UserId = GetOwningUserId(); \*\*if\*\* (UserId.IsValid()) { \*\*if\*\* (UInputDeviceSubsystem\* InputDeviceSubsystem = UInputDeviceSubsystem::Get()) { FActivateDevicePropertyParams Params = {}; Params.UserId = UserId; // By default, the device property will be played on the Platform User's Primary Input Device. // If you want to override this and set a specific device, then you can set the DeviceId parameter. //Params.DeviceId = <some specific device id>; // Uses the given instanced property and modifies it. Use this carefully FInputDevicePropertyHandle Handle = InputDeviceSubsystem->ActivateDeviceProperty(DeviceProp, Params); // Spawns a new instance of this device property class and uses that FInputDevicePropertyHandle Handle = InputDeviceSubsystem->ActivateDevicePropertyOfClass(DeviceProp, Params); } } } |  

See the LyraWeaponInstance.cpp from the [Lyra Game Sample](/documentation/en-us/unreal-engine/lyra-inventory-and-equipment-in-unreal-engine) for an example where device properties are applied as weapons are equipped and unequipped.

#### Blueprints

You can make your own Blueprints using Device Properties to create custom gameplay experiences. For example, using the `B_TeamColor_DeviceProperty` variable located in the [Lyra Game Sample](/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine), we set the light color of the controller to match your team color (red or blue).

![Lyra Device Property](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/360bc213-efa2-465e-8971-8af3ebaad96d/lyrabpdevice.png)

Lyra Game Sample example of the Device Property system using a Blueprint script.

Blueprints code can only use a subclass type to avoid harmful object referencing. This means that you will need to make a specific device property blueprint for these use cases.

Call the function `RemoveDevicePropertyHandles()` on the subsystem if you want to manually remove an input device property.

#### Force Feedback Asset

You can activate device properties by adding to an existing [Force Feedback Asset](/documentation/en-us/unreal-engine/force-feedback-in-unreal-engine) that you want to be applied to the player. To do this by navigate to the **Details** > **Device Properties** category.

![Force Feedback Details](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/311093fe-8f6b-4bd5-a108-bd4a64390c2a/ffdetails.png)

#### Burst Gameplay Effect Cue

You can specify input device properties that you wish to have activated when a **Gameplay Cue Notify Burst** is applied by navigating to the **Details** > **GCN Effects** \> **Burst Effects** \> **Burst Device Property Effect** \> **Device Properties** category.

![Burst Gameplay Effect](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6914c5f-7fd7-4217-b884-9c0a4e12b62c/burstgameplay.png)

## Debugging

To display information on the screen about what device properties are currently active. Press tilde(~) to open the console and use the console command

```

	`| showdebug DeviceProperty |`

Copy full snippet
```
| showdebug DeviceProperty | ![Debug Device Property Command](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9e69c2df-0830-4a6a-b2e0-7d3086895958/debugdeviceprop.png)

Typing the showdebug deviceproperty command to console.

This command displays debug information on the viewport about what device properties are currently active. It displays what flags were used when the device was activated, the Input Device ID it is being applied to, and how long it has been activated.

![Device Propery Debug Display](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bc00c004-fbb0-41c9-8f87-c102cb731ff9/debugdisplay.png)

## Creating New Hardware Properties

The `UInputDeviceProperty` in the `Engine` module provides an abstraction for the lower-level `FInputDeviceProperty` struct declared in the `ApplicationCore` module. The `FInputDeviceProperty` is passed to the platform code, which is where the implementation of each property is handled.

When a new development kit is released, you can add support for it with different input device properties by overriding the `SetDeviceProperty()` function on the `IInputDevice` or `IInputInterface` for that hardware.

If you are adding a new subclass of `FInputDeviceProperty`, then you will want to ensure that it is not device specific and can be referenced anywhere in the engine without breaking any NDA. If you have a project-specific piece of hardware, then declare it in your project code.