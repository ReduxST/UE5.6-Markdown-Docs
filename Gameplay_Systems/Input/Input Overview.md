# Input Overview

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/input-overview-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/input-overview-in-unreal-engine)  
**Processed:** 2025-06-14 16:31:05

---

The **PlayerInput** Object is responsible for converting input from the player into data that Actors (like PlayerControllers or Pawns) can understand and make use of. It is part of an input processing flow that translates hardware input from players into game events and movement with PlayerInput mappings and InputComponents.

For an example of setting up Input, refer to the [Setup Input](/documentation/en-us/unreal-engine/setting-up-user-inputs-in-unreal-engine) documentation.

## Hardware Input

Hardware input from a player is straightforward. It commonly includes key presses, mouse clicks or mouse movement, and controller button presses or joystick movement. Specialized input devices that don't conform to standard axis or button indices, or that have unusual input ranges, can be configured manually by using the [Raw Input Plugin](/documentation/en-us/unreal-engine/rawinput-plugin-in-unreal-engine).

## PlayerInput

PlayerInput is a UObject within the PlayerController class that manages player input. It is only spawned on the client. Two structs are defined within PlayerInput. The first, **FInputActionKeyMapping**, defines an ActionMapping. The other, **FInputAxisKeyMapping**, defines an AxisMapping. The hardware input definitions used in both ActionMappings and AxisMappings are established in InputCoreTypes.

$ ActionMappings : Map a discrete button or key press to a "friendly name" that will later be bound to event-driven behavior. The end effect is that pressing (and/or releasing) a key, mouse button, or keypad button directly triggers some game behavior.

$ AxisMappings : Map keyboard, controller, or mouse inputs to a "friendly name" that will later be bound to continuous game behavior, such as movement. The inputs mapped in AxisMappings are continuously polled, even if they are just reporting that their input value is currently zero. This allows for smooth transitions in movement or other game behavior, rather than the discrete game events triggered by inputs in ActionMappings.

Hardware axes, such as controller joysticks, provide degrees of input, rather than discrete 1 (pressed) or 0 (not pressed) input. That is, they can be moved to a small degree or a large degree, and your character's movement can vary accordingly. While these input methods are ideal for providing scalable amounts of movement input, AxisMappings can also map common movement keys, like WASD or Up, Down, Left, Right, to continuously-polled game behavior.

### Setting Input Mappings

Input mappings are stored in configuration files, and can be edited in the Input section of Project Settings.

1.  In the Level Editor, select **Edit > Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/40c3eb43-e571-4b6f-a65e-5fd6390612a5/projectsettingsmenu.png)
2.  Click **Input** in the **Project Settings** tab that appears.
    

In this window, you can:

**Change the properties of (hardware) axis inputs:** ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b4c12d6c-e1d5-4fba-86c6-a0c0f128573d/axisconfig.png)

**Add or edit ActionMappings:** ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4e10af62-2520-465f-8029-e2e587182e2b/actionmappings.png)

**Add or edit AxisMappings:** ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9bcf9fea-f653-4602-971c-f5f41e157a63/axismappings.png) 

## InputComponent

**InputComponents** are most commonly present in Pawns and Controllers, although they can be set in other Actors and Level Scripts if desired. The InputComponent links the AxisMappings and ActionMappings in your project to game actions, usually functions, set up either in C++ code or Blueprint graphs.

The priority stack for input handling by InputComponents is as follows (highest priority first):

1.  Actors with "Accepts input" enabled, from most-recently enabled to least-recently enabled.
    
    If you want a particular Actor to always be the first one considered for input handling, you can re-enable its "Accepts input" and it will be moved to the top of the stack.
    
2.  Controllers.
3.  Level Script.
4.  Pawns.

If one InputComponent takes the input, it is not available further down the stack.

## Input Processing Procedure

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c6af466-56e1-4741-8134-5e2d6bccc247/inputflow.png)

### Example - Moving Forward

This example is taken from the First Person template provided with Unreal Engine.

1.  **Hardware Input from Player:** The player presses W.
2.  **PlayerInput Mapping:** The AxisMapping translates W to "MoveForward" with a scale of 1.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/03ba0597-1ae0-41cc-a6e8-d297dfc21021/axismappingw.png)
3.  **InputComponent Priority Stack:** Proceeding through the InputComponent priority stack, the first binding of the "MoveForward" input is in the AFirstPersonBaseCodeCharacter class. This class is the current player's Pawn, so its InputComponent is checked last.
    
    ```
                 `void AFirstPersonBaseCodeCharacter::SetupPlayerInputComponent(class UInputComponent* InputComponent)                  {                      // set up gameplay key bindings                      check(InputComponent);                      ...                      InputComponent->BindAxis("MoveForward", this, &AFirstPersonBaseCodeCharacter::MoveForward);                      ...                  }`
    Copy full snippet
    ```
    void AFirstPersonBaseCodeCharacter::SetupPlayerInputComponent(class UInputComponent\* InputComponent) { // set up gameplay key bindings check(InputComponent); ... InputComponent->BindAxis("MoveForward", this, &AFirstPersonBaseCodeCharacter::MoveForward); ... }
    
    This step could also be accomplished in Blueprints by having an InputAxis MoveForward node in the Character's EventGraph. Whatever this node is connected to is what will execute when W is pressed.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/27a6c980-367b-4ca0-8805-23a38f9e37be/inputmappingmoveforward.png)
4.  **Game Logic:** AFirstPersonBaseCodeCharacter's MoveForward function executes.
    
    ```
                `void AFirstPersonBaseCodeCharacter::MoveForward(float Value)                 {                     if ( (Controller != NULL) && (Value != 0.0f) )                     {                         // find out which way is forward                         FRotator Rotation = Controller->GetControlRotation();                         // Limit pitch when walking or falling                         if ( CharacterMovement->IsMovingOnGround() || CharacterMovement->IsFalling() )                         {                             Rotation.Pitch = 0.0f;                         }                         // add movement in that direction                         const FVector Direction = FRotationMatrix(Rotation).GetScaledAxis(EAxis::X);                         AddMovementInput(Direction, Value);                     }                 }`
    Copy full snippet
    ```
    void AFirstPersonBaseCodeCharacter::MoveForward(float Value) { if ( (Controller != NULL) && (Value != 0.0f) ) { // find out which way is forward FRotator Rotation = Controller->GetControlRotation(); // Limit pitch when walking or falling if ( CharacterMovement->IsMovingOnGround() || CharacterMovement->IsFalling() ) { Rotation.Pitch = 0.0f; } // add movement in that direction const FVector Direction = FRotationMatrix(Rotation).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } }
    
    Blueprint Implementation:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/18863233-adb8-4237-9109-cc453cb6f989/moveforward_blueprint.png)

## Touch Interface

By default, games running on touch devices will have two virtual joysticks (like a console controller). You can change this in your **Project Settings**, in the **Input** section, with the **Default Touch Interface** property. This points to a Touch Interface Setup asset. The default one, **DefaultVirtualJoysticks** is located in shared engine content (`/Engine/MobileResources/HUD/DefaultVirtualJoysticks.DefaultVirtualJoysticks`). There is also a Left Stick only version, **LeftVirtualJoystickOnly**, for games that do not need to turn the camera.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/14ada552-b89d-48eb-b8df-38b2dbd863b0/virtualjoystickssettings.png)

Note that you will need to check the **Show Engine Content** checkbox in the object picker **View Options** settings to see these.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1c75223b-5ad2-4865-b2c3-2e2751e83808/showenginecontent.png)

If you do not want any virtual joysticks, just clear the Default Touch Interface property. Additionally, you can force the touch interface for your game independent of the platform it is running by checking Always Show Touch Interface (or by running the PC game with -faketouches).

## Enhanced Input Plugin

For projects that require more advanced input features, like complex input handling or runtime control remapping, the experimental [Enhanced Input Plugin](/documentation/en-us/unreal-engine/enhanced-input-in-unreal-engine) gives developers an easy upgrade path and backward compatibility with the engine's default input system. This plugin implements features like radial dead zones, chorded actions, contextual input and prioritization, and the ability to extend your own filtering and processing of raw input data in an Asset-based environment.

## Getting Started

To configure your project to use Enhanced Input, enable the Enhanced Input Plugin. You can do this by opening the **Edit** dropdown menu in the editor and selecting **Plugins**. Under the **Input** section of the Plugin List, find and enable the Enhanced Input Plugin, then restart the editor.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/7e5ce11c-3718-4119-9fb9-c9511e1ea518/enableenhanceinput.png)

The plugin will become active after you restart the editor.

Once the editor has restarted, you can set your project to use Enhanced Input Plugin classes instead of the default Unreal Engine input handlers. Go to the **Edit** dropdown menu and choose **Project Settings**. From there, locate the **Input** section (under the **Engine** heading) and find the **Default Classes** settings. These will initially contain the standard PlayerInput and InputComponent classes.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6b973ded-c4d2-4fdf-83da-ac4252dd521e/defaultinputclasses.png)

To use Enhanced Input, change these settings to EnhancedPlayerInput and EnhancedInputComponent, respectively.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0e32a121-9f4b-4f35-8c20-c115bc545bff/enhancedinputclasses.png)

## Core Concepts

The Enhanced Input system has four main concepts: \* Input Actions are the communication link between the Enhanced Input system and your project's code. An Input Action can be anything that an interactive character might do, like jumping or opening a door, but could also be used to indicate user input states, like holding a button that changes walking movement to running. Input Actions are separate from raw input; an Input Action is not concerned with the specific input that triggered it, but does know its current state and can report an input value on up to three independent floating-point axes. As an example, a "pick up item" Action might only need an on/off state, indicating whether or not the user is trying to pick something up, while a "walk" Action might require two axes to describe the direction and speed at which the user is trying to walk.

\* Input Mapping Contexts map user inputs to Actions and can be dynamically added, removed, or prioritized for each user. You can apply one or more Contexts to a local player through its Enhanced Input Local Player Subsystem, and prioritize them to resolve collisions between multiple actions trying to consume the same input. A common example of this might be a single button that can open doors while the character is walking around in the world, or select an item while looking through the character's backpack. Whenever the character opens the backpack, you could add a "select item" Input Mapping Context that out-prioritizes the "open door" context, and then remove the "select item" context when the character closes the backpack. This would ensure that the user's inputs will be interpreted correctly based on the character's situation, and prevent the need to program code at the input-handling level with awareness of the door and backpack systems. Modifiers adjust the value of raw input coming from the user's devices. An Input Mapping Context can have any number of modifiers associated with each raw input for an Input Action. Common Modifiers including dead zones, input smoothing over multiple frames, conversion of input vectors from local to world space, and several others are included in the plugin; developers can also create their own Modifiers.

\* Triggers use post-Modifier input values, or the output magnitudes of other Input Actions, to determine whether or not an Input Action should activate. Any Input Action within an Input Mapping Context can have one or more Triggers for each input. For example, taking a photograph might require that the user hold down the Left Mouse Button for a quarter of a second while a separate Input Action for aiming the camera is active.

By combining these concepts, developers can quickly set up input systems ranging from simple to complex, and adjust these systems without having to change project code.

## Input Actions

Input Actions are the connection between the system and your project's code. You can create an Input Action by right-clicking in the **Context Browser**, expanding the **Input** option, and choosing **Input Action**. To trigger an Input Action, you must include it in an Input Mapping Context, and add that Input Mapping Context to the local player's **Enhanced Input Local Player Subsystem**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5eb431f5-cf04-465b-9f77-2a5bc6ec733e/buttoninputclass.png)

To make your Pawn class respond to a triggered Input Action, you must bind it to the appropriate type of **Trigger Event** in SetupPlayerInputComponent. The following sample code overrides SetupPlayerInputComponent to bind two Input Actions, MyInputAction and MyOtherInputAction, to handler functions:

```
 `// Make sure that we are using a UEnhancedInputComponent; if not, the project is not configured correctly.  if (UEnhancedInputComponent* PlayerEnhancedInputComponent = Cast<UEnhancedInputComponent>(PlayerInputComponent))  {     // There are ways to bind a UInputAction* to a handler function and multiple types of ETriggerEvent that may be of interest.      // This calls the handler function on the tick when MyInputAction starts, such as when pressing an action button.     if (MyInputAction)     {         PlayerEnhancedInputComponent->BindAction(MyInputAction, ETriggerEvent::Started, this, &AMyPawn::MyInputHandlerFunction);     }      // This calls the handler function (a UFUNCTION) by name on every tick while the input conditions are met, such as when holding a movement key down.     if (MyOtherInputAction)     {         PlayerEnhancedInputComponent->BindAction(MyOtherInputAction, ETriggerEvent::Triggered, this, TEXT("MyOtherInputHandlerFunction"));     }  }`
Copy full snippet
```
// Make sure that we are using a UEnhancedInputComponent; if not, the project is not configured correctly. if (UEnhancedInputComponent\* PlayerEnhancedInputComponent = Cast<UEnhancedInputComponent>(PlayerInputComponent)) { // There are ways to bind a UInputAction\* to a handler function and multiple types of ETriggerEvent that may be of interest. // This calls the handler function on the tick when MyInputAction starts, such as when pressing an action button. if (MyInputAction) { PlayerEnhancedInputComponent->BindAction(MyInputAction, ETriggerEvent::Started, this, &AMyPawn::MyInputHandlerFunction); } // This calls the handler function (a UFUNCTION) by name on every tick while the input conditions are met, such as when holding a movement key down. if (MyOtherInputAction) { PlayerEnhancedInputComponent->BindAction(MyOtherInputAction, ETriggerEvent::Triggered, this, TEXT("MyOtherInputHandlerFunction")); } }

Binding Input Actions with the Enhanced Input Plugin replaces the built-in input system's Action and Axis bindings; if you are using the Enhanced Input Plugin, you should only bind Input Actions. When binding Input Actions, you can choose between four different handler function signatures, as follows:

| Return Type | Parameters | Usage Notes |
| --- | --- | --- |
| void | `()` | Suitable for simple cases where you don't need any extra information from the Enhanced Input system. |
| void | `(const FInputActionValue& ActionValue)` | Provides access to the current value of the Input Action. |
| void | `(const FInputActionInstance& ActionInstance)` | Provides access to the current value of the Input Action, the type of trigger event, and relevant timers. |
| void | `(FInputActionValue ActionValue, float ElapsedTime, float TriggeredTime)` | Signature used when dynamically binding to a UFunction by its name; parameters are optional. |

Input Actions have built-in events that expose them to Blueprints Scripting; C++ developers do not have to create pass-through functions to give Blueprint Scripting developers access to Input Action events. A typical handler function might take the following form:

```
 `void AMyPawn::MyFirstAction(const FInputActionValue& Value)  {     // Debug log output to confirm that the handler function is running.     UE_LOG(LogTemp, Warning, TEXT("%s called with Input Action Value %s (magnitude %f)"), TEXT(__FUNCTION__), *Value.ToString(), Value.GetMagnitude());     // Use the GetType() function to determine Value's type, and the [] operator with an index between 0 and 2 to access its data.  }`
Copy full snippet
```
void AMyPawn::MyFirstAction(const FInputActionValue& Value) { // Debug log output to confirm that the handler function is running. UE\_LOG(LogTemp, Warning, TEXT("%s called with Input Action Value %s (magnitude %f)"), TEXT(\_\_FUNCTION\_\_), \*Value.ToString(), Value.GetMagnitude()); // Use the GetType() function to determine Value's type, and the \[\] operator with an index between 0 and 2 to access its data. }

For most use cases, using the void (const FInputActionValue&) signature is recommended. Binding Input Actions to handler functions enables the Pawn to respond to them depending on the specific way that they are triggered. The most common trigger types are likely to be Started for actions that happen once, immediately upon pressing a button, and Triggered for continuous actions that happen every frame while holding an input, but you can view the complete list at the API reference page for [ETriggerEvent](/documentation/404).

## Input Mapping Contexts

Input Mapping Contexts describe the rules for triggering one or more Input Actions. Its basic structure is a hierarchy with a list of Input Actions at the top level. Under the Input Action level is a list of user inputs that can trigger each Input Action, such as keys, buttons, and movement axes. The bottom level contains a list of Input Triggers and Input Modifiers for each user input, which you can use to determine how an input's raw value is filtered or processed, and what restrictions it must meet in order to drive the Input Action at the top of its hierarchy. Any input can have multiple Input Modifiers and Input Triggers. These will evaluate in order, using the output of each step as the input for the next.

To create an Input Mapping Context, right-click the **Context Browser**, expand the **Input** option, and choose **Input Mapping Context**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/56192189-d350-40a0-a7c9-53a654c9eece/buttoninputclass.png)

Populate your Input Mapping Context with all of the relevant Input Actions. For a simple project, you may be able to put all of your Input Actions into a single Input Mapping Context. More complex projects may work best with multiple Input Mapping Contexts, since a local player can have more than one active Input Mapping Context at a time. As an example, a character who can swim, walk, and drive vehicles might have an Input Mapping Context for common actions that are always available and always mapped to the same user inputs, and separate Input Mapping Contexts for each mode of travel. Developers could then place the vehicle-related Input Actions into a separate Input Mapping Context, which they can then add to the local player upon entering a vehicle, and remove from the local player upon exiting. Doing this helps to reduce bugs by ensuring that inappropriate Input Actions cannot run (and don't waste CPU cycles), and by avoiding input collisions when a user input is used for different Input Actions by mutually-exclusive Input Mapping Contexts. See the sections on Modifiers and Triggers for more details.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/125faf8d-2ba3-4ce6-80ad-8f56eae24db3/inputmapcontext.png)

This Input Mapping Context shows an Input Action for running, which can be activated by multiple inputs, including a gamepad's left thumbstick deflection, combining both axes into a single input. That input's raw value will go through a "dead zone" Input Modifier, and the resulting value will be sent to the "hold" Input Trigger to drive the "RunAction" Input Action.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c7b7203e-e9b3-4495-93c8-9a769c5b7a2d/spacebarhighlight.png)

There are a large number of input bindings available in the dropdown list. To select your input binding more quickly, press the small button to the left of the dropdown, and then press the key or button you want to bind.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d4517b0c-0c7f-46f5-a4ee-d3c7521b903a/fullmap.png)

This simple Input Mapping Context supports Input Actions for running and jumping. Once you have populated an Input Mapping Context, you can add it to the Local Player associated with the Pawn's Player Controller . Do this by overriding the PawnClientRestart function and adding a code block like this:

```
 `// Make sure that we have a valid PlayerController.  if (APlayerController* PC = Cast<APlayerController>(GetController()))  {     // Get the Enhanced Input Local Player Subsystem from the Local Player related to our Player Controller.     if (UEnhancedInputLocalPlayerSubsystem* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PC->GetLocalPlayer()))     {         // PawnClientRestart can run more than once in an Actor's lifetime, so start by clearing out any leftover mappings.         Subsystem->ClearAllMappings();          // Add each mapping context, along with their priority values. Higher values take priority over lower values.         Subsystem->AddMappingContext(MyInputMappingContext, MyInt32Priority);     }  }`
Copy full snippet
```
// Make sure that we have a valid PlayerController. if (APlayerController\* PC = Cast<APlayerController>(GetController())) { // Get the Enhanced Input Local Player Subsystem from the Local Player related to our Player Controller. if (UEnhancedInputLocalPlayerSubsystem\* Subsystem = ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PC->GetLocalPlayer())) { // PawnClientRestart can run more than once in an Actor's lifetime, so start by clearing out any leftover mappings. Subsystem->ClearAllMappings(); // Add each mapping context, along with their priority values. Higher values take priority over lower values. Subsystem->AddMappingContext(MyInputMappingContext, MyInt32Priority); } }

With your Input Mapping Contexts added, your Pawn is able to respond to any Input Action events you bound in SetupPlayerInputComponent, or that Blueprint Scripting users have set up. If events occur during gameplay that warrant changing the set of available Input Mapping Contexts, you can use ClearAllMappings, AddMappingContext, and RemoveMappingContext to update the set of available commands dynamically. Check the [IEnhancedInputSubsystemInterface](/documentation/404) API reference page for more information.

## Input Modifiers

Input Modifiers are pre-processors that alter the raw input values that Unreal Engine receives before sending them on to Input Triggers. The Enhanced Input Plugin ships with a variety of Input Modifiers to perform tasks like changing the order of axes, implementing "dead zones", converting axial input to world space, and several others. Each input associated with an Input Action within an Input Mapping Context will go through a user-defined series of Input Modifiers before proceeding to the Input Trigger (or Input Triggers) for that input. Input Modifiers are applied in the order they are listed, and the output value from each Input Modifier becomes the input value for the next. To see the complete list of Input Modifiers included with the Enhanced Input Plugin, check the [UInputModifier](/documentation/404) API reference page. If your project requires an Input Modifier that doesn't already exist, you can create your own UInputModifier class.

## Input Triggers

Input Triggers determine whether or not a user input, after passing through an optional list of Input Modifiers, should activate the corresponding Input Action within its Input Mapping Context. Most Input Triggers analyze the input itself, checking for minimum actuation values and validating patterns like short taps, prolonged holds, or the typical "press" or "release" events. The one exception to this rule is the "Chorded Action" Input Trigger, which requires another Input Action to be triggered. By default, any user activity on an input will trigger on every tick. To see the complete list of Input Triggers included with the Enhanced Input Plugin, check the [UInputTrigger](/documentation/404) API reference page. If you need an Input Trigger that the Enhanced Input Plugin does not provide, you can create your own UInputTrigger class.