# Implementing your Character

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/implementing-your-character-in-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/implementing-your-character-in-unreal-engine)  
**Processed:** 2025-06-14 16:29:58

---

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/78d716bf-1177-478f-b0eb-15ba165eb9a7/41-result.png)

This is what you'll see at the end of this section.

## Goals

The purpose of this section is to show you how to implement your First Person Shooter character.

## Objectives

By the end of this tutorial section, you will be able to:

-   Make a New Character
-   Set Up Axis Mapping
-   Implement Character Movement Functions
-   Implement Mouse Camera Control
-   Implement Character Jumping
-   Add a Mesh to Your Character
-   Change the Camera View
-   Add a First Person Mesh to Your Character

## Steps

-   2.1 - Making a New Character
-   2.2 - Setting up Axis Mapping
-   2.3 - Implementing Character Movement Functions
-   2.4 - Implementing Mouse Camera Control
-   2.5 - Implementing Character Jumping
-   2.6 - Adding a Mesh to Your Character
-   2.7 - Changing the Camera View
-   2.8 - Add a First Person Mesh to Your Character

## 2.1 - Making a New Character

During this step, you are going to make a new character in the **Unreal Engine** (UE) using the engine's **Character** base class. The Character class (derived from the **Pawn** class) has built-in functionality for bipedal movement such as walking, running, and jumping.

### Adding a Character Class

Although you can manually add `.h` and `.cpp` files to your **Visual Studio** (VS) solution, it is good practice to use the **C++ Class Wizard** to add new classes to your project.

By using the C++ Class Wizard, the engine creates header and source templates that set-up UE specific macros for you.

1.  Launch your **FPSproject** in UE (if you have not already done so).
    
2.  Click the **Tools** in the **Main** menu panel, select **New C++ Class...**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2c23b0a7-ddd3-47f7-89d1-2cba8fce6fe2/01-new-cpp-class.png)
3.  The **Choose Parent Class** window appears. Select **Character** as the parent class, and click **Next**.
    
    Click for full image.
    
4.  Name the new class **FPSCharacter** then click **Create Class**.
    
    Click for full image.
    

### Verifying the Character Class

1.  In the **Solution Explorer** of VS, expand **FPSProject > Source > FPSProject**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/697227d2-900a-4f92-b271-e3c4c4cc27ac/04-expand-fpsproject.png)
2.  Click the `FPSCharacter.cpp` to open the implementation file for your **FPSCharacter** class.
    
3.  Add the following code in the `void AFPSCharacter::BeginPlay()` function (under `Super::BeginPlay();`). With the help of this, you will verify that `FPSCharacter` class is being used:
    
    FPSCharacter.cpp
    
    ```
        `check(GEngine != nullptr);      // Display a debug message for five seconds.      // The -1 "Key" value argument prevents the message from being updated or refreshed.     GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));`
    Copy full snippet
    ```
    check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));
4.  `FPSCharacter.cpp` should now look like the following:
    
    FPSCharacter.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.                  #include "FPSCharacter.h"      // Sets default values     AFPSCharacter::AFPSCharacter()     {         // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;      }      // Called when the game starts or when spawned     void AFPSCharacter::BeginPlay()     {         Super::BeginPlay();          check(GEngine != nullptr);          // Display a debug message for five seconds.          // The -1 "Key" value argument prevents the message from being updated or refreshed.         GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));          }      // Called every frame     void AFPSCharacter::Tick(float DeltaTime)     {         Super::Tick(DeltaTime);      }      // Called to bind functionality to input     void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)     {         Super::SetupPlayerInputComponent(PlayerInputComponent);      }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick(float DeltaTime) { Super::Tick(DeltaTime); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); }
5.  Save the `FPSCharacter.cpp` file in Visual Studio.
    
6.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
    Up until now, you have been compiling your project using the editor's **Build** button. During this step, you are going to gain experience compiling code using Visual Studio's build feature. To compile your code from inside Visual Studio, right-click on **FPSProject** and select **Build** to compile your project.
    
7.  To compile your code using the VS, right-click on **FPSProject** in **Solution Explorer** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4b395cf5-09f3-43f0-8f01-fd5071626c65/05-build-project.png)
    
    Before doing this step, make sure disable **Enable Live Coding** in the Unreal Engine.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ad43a38b-0e14-4b3a-8e71-16e03a4b4e7e/06-disable-live-coding.png)
    
    If you are using the default setup of VS, you should have a dialogue box near the bottom of the program (likely below where you've been editing code). When you click Build, some dialogue should appear in that box while it processes, and it should then hopefully say it was built successfully. If the build failed, don't stress! Just retrace your steps and make sure your code matches what you've listed here and in [Setting up your Project](/documentation/en-us/unreal-engine/setting-up-your-project-in-unreal-engine).
    
8.  After the build finishes, open Unreal Editor to verify that your newly compiled **FPSCharacter** class is visible in the **Content Browser**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aa8db647-1074-4cf3-a71c-4a27cb2fc37c/07-character-content-browser.png)

### Extending your C++ FPS Character Class to Blueprints

Now is a good time to extend the C++ FPS Character class to Blueprints (like you did with the FPSProject Game Mode in the [Setting up your Project](/documentation/en-us/unreal-engine/setting-up-your-project-in-unreal-engine). Please feel free to go to [C++ and Blueprints](/documentation/en-us/unreal-engine/cpp-and-blueprints-example) reference page to learn more about extending C++ classes to Blueprints.

1.  Right-click the **FPSCharacter** class in **Content Browser** to open the **Action** menu.
    
2.  Click the **Create Blueprint class based on FPSCharacter** to open the **Add Blueprint Class** dialog menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/38c99854-4e7e-4bd6-a761-1d45a94761a9/08-create-derived-bp-class.png)
3.  Name your new Blueprint Class **BP\_FPSCharacter** and choose the **Blueprints** folder before clicking the **Create Blueprint Class** button.
    
    Click for full image.
    
4.  You should have a newly created **BP\_FPSCharacter** Blueprint Class located inside of the **Blueprints** folder.
    
    Click for full image.
    
5.  Make sure to **Save** your **BP\_FPSCharacter** Blueprint before closing the **Blueprint Editor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/69213094-1d82-4f6f-bd22-ad768af1e366/27-compile-save.png)

### Setting the Default Pawn Class

Now that you have successfully extended your newly modified Game Mode to Blueprints, you will need to set your project to use `BP_FPSCharacter` as the default **Pawn** in this step.

1.  Click the **Edit** in the **Main** menu panel, select **Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/61fa0155-7a1b-41dc-ae61-e1056645496e/11-open-project-settings.png)
2.  Under the **Project** heading on the left side of the **Project Settings** tab, click on **Maps & Modes**.
    
3.  Expand the **Selected GameMode** section, and select **BP\_FPSCharacter** in the **Default Pawn Class** dropdown menu.
    
    Click for full image.
    
4.  Close the **Project Settings** menu.
    
5.  Click the **Play** button in the **Level Editor Toolbar**. "We are using FPSCharacter." should now be displayed in red text below "Hello World, this is FPSGameMode!" for five seconds in the upper left corner of the viewport.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3aa6e27a-c412-46b0-ae19-ef00d3dcc38f/13-verifying-result.png)
    
    If you are unable to move, you are using FPSCharacter as your Pawn correctly! Your new Character doesn't have any movement controls yet, so you will not be able to move around in the level.
    
6.  Before going to the next step, press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

## 2.2 - Setting up Axis Mapping

In general, Axis Mappings enable mapping keyboard, mouse, and controller inputs to a "friendly name" that can later be bound to game behavior (such as movement). Axis Mappings are continuously polled, allowing for seamless movement transitions and smooth game behavior. Hardware axis (such as controller joysticks) provide degrees of input, rather than discrete input (for example, 1 pressed vs. 0 not pressed). While controller joystick input methods are effective at providing scalable movement input, Axis Mappings can also map common movement keys (like **WASD** or arrow keys) to continuously-polled game behavior.

If you want to learn more about Player Input before moving forward with this step, please refer to the [Player Input and Pawns](/documentation/en-us/unreal-engine/quick-start-guide-to-player-input-in-unreal-engine-cpp) tutorial. During this step, you are going to get your new Character to move around the map by setting up the input axis mappings for the **WASD** keys.

### MoveForward Axis Mapping

1.  Click the **Edit** in the **Main** menu panel, select **Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ff68a190-7842-494e-a37a-04c0a60b1419/11-open-project-settings.png)
2.  Under the **Engine** heading on the left side of the **Project Settings** tab, click **Input**.
    
3.  Under the **Bindings** section, click the plus sign next to **Axis Mappings**.
    
4.  Click the arrow to the left of **Axis Mappings**.
    
5.  Type **MoveForward** into the text field that appears.
    
6.  In the dropdown menu, select **W** from the **Keyboard** dropdown list.
    
7.  Your input settings should now look like the following:
    
    Click for full image.
    
8.  Click the plus sign next to **MoveForward**.
    
9.  In the second dropdown menu, select **S** from the **Keyboard** dropdown list.
    
10.  Type **\-1.0** in the **Scale** field next to **S**.
    
11.  Your input settings should now look like the following:
    
    Click for full image.
    

### MoveRight Axis Mapping

1.  Under the **Bindings** section, click the plus sign next to **Axis Mappings**.
    
2.  Type **MoveRight** into the text field that appears.
    
3.  In the dropdown menu, select **D** from the **Keyboard** dropdown list.
    
4.  Your input settings should now look like the following:
    
    Click for full image.
    
5.  Click on the plus sign next to **MoveRight**.
    
6.  In the second dropdown menu, select **A** from the **Keyboard** dropdown list.
    
7.  Type **\-1.0** in the **Scale** field next to **A**.
    
8.  Your input settings should now look like the following:
    
    Click for full image.
    
9.  Now that you have set your Movement Axis Mappings, go ahead and close the **Project Settings** menu.
    

## 2.3 - Implementing Character Movement Functions

In this step, you are going to set-up our Player Input Component and implement the following functions in the **FPSCharacter** class:

-   `MoveForward`
-   `MoveRight`

### Movement Function Interfaces

Now that you have set-up Axis mappings for your **FPSCharacter**, you can switch to your project in VS.

1.  In `FPSCharacter.h`, add the following function declarations below `SetupPlayerInputComponent`, under `public` access specifier:
    
    FPSCharacter.h
    
    ```
        `// Handles input for moving forward and backward.     UFUNCTION()     void MoveForward(float Value);       // Handles input for moving right and left.     UFUNCTION()     void MoveRight(float Value);`
    Copy full snippet
    ```
    // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value);
    
    The `UFUNCTION` macro (located above each of these functions) makes the engine aware of these functions so that they can be included in serialization and other engine functionality.
    
2.  `FPSCharacter.h` should now look like the following:
    
    FPSCharacter.h
    
    ```
       `// Copyright Epic Games, Inc. All Rights Reserved.               #pragma once               #include "CoreMinimal.h"     #include "GameFramework/Character.h"     #include "FPSCharacter.generated.h"               UCLASS()     class FPSPROJECT_API AFPSCharacter : public ACharacter     {         GENERATED_BODY()               public:         // Sets default values for this character's properties         AFPSCharacter();               protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;               public:         // Called every frame         virtual void Tick( float DeltaTime ) override;                   // Called to bind functionality to input         virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;                   // Handles input for moving forward and backward.         UFUNCTION()         void MoveForward(float Value);                   // Handles input for moving right and left.         UFUNCTION()         void MoveRight(float Value);               };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); };

### Movement Function Implementations

In a typical FPS control scheme, the character's movement axes are relative to the camera. "Forward" movement means "the direction that the camera is pointing" and "right" means "to the right of the direction that the camera is pointing". You are going to use the `PlayerController` to get the character's control rotation. Also, your `MoveForward` function will ignore the pitch component of the control rotation and restrict your input to the XY plane so as to guarantee that your character will move along the ground while you are looking up or down.

1.  In `FPSCharacter.cpp`, add the following lines to the `SetupPlayerInputComponent` function under `Super::SetupPlayerInputComponent(PlayerInputComponent);`.
    
    FPSCharacter.cpp
    
    ```
        `// Set up "movement" bindings.     PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);     PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);`
    Copy full snippet
    ```
    // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);
    
    An `InputComponent` is a component that defines how to handle input data. An `InputComponent` can be attached to an actor that wants to receive input.
    
2.  Below `SetupPlayerInputComponent` function definition, add the following `MoveForward` function definition in `FPSCharacter.cpp`.
    
    FPSCharacter.cpp
    
    ```
        `void AFPSCharacter::MoveForward(float Value)     {         // Find out which way is "forward" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);         AddMovementInput(Direction, Value);     }`
    Copy full snippet
    ```
    void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); }
3.  Below `MoveForward` function definition, add the following `MoveRight` function definition in `FPSCharacter.cpp`.
    
    FPSCharacter.cpp
    
    ```
        `void AFPSCharacter::MoveRight(float Value)     {         // Find out which way is "right" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);         AddMovementInput(Direction, Value);     }`
    Copy full snippet
    ```
    void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); }
4.  `FPSCharacter.cpp` should now look like the following:
    
    FPSCharacter.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.                        #include "FPSCharacter.h"               // Sets default values     AFPSCharacter::AFPSCharacter()     {         // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;               }               // Called when the game starts or when spawned     void AFPSCharacter::BeginPlay()     {         Super::BeginPlay();                   check(GEngine != nullptr);                      // Put up a debug message for five seconds.          // The -1 "Key" value argument prevents the message from being updated or refreshed.           GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));                  }               // Called every frame     void AFPSCharacter::Tick( float DeltaTime )     {         Super::Tick( DeltaTime );               }               // Called to bind functionality to input     void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)     {         Super::SetupPlayerInputComponent(PlayerInputComponent);                   // Set up "movement" bindings.         PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);         PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);     }               void AFPSCharacter::MoveForward(float Value)     {         // Find out which way is "forward" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);         AddMovementInput(Direction, Value);     }               void AFPSCharacter::MoveRight(float Value)     {         // Find out which way is "right" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);         AddMovementInput(Direction, Value);     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr); // Put up a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); } void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); }

### Testing Character Movement

It is now time to compile and test your newly implemented character movement functions.

1.  Save the **FPSCharacter** header `.h` and implementation `.cpp` files in VS.
    
2.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
3.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1603999c-a084-4cde-b6e0-6f18b869f1aa/05-build-project.png)
4.  After the build finishes, open your **FPSProject** in the Unreal Editor.
    
5.  Click the **Play** button in the **Level Editor Toolbar**. You can now move forward, backward, left, and right using **WASD** keys.
    
6.  Before going to the next step, press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

## 2.4 - Implementing Mouse Camera Control

During this step, you are going to add the ability for your character to look around and steer with the mouse.

### Turn Axis Mapping

1.  Click the **Edit** in the **Main** menu panel, select **Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d377f802-9795-4d79-b335-9b7159cfd335/11-open-project-settings.png)
2.  Under the **Engine** heading on the left side of the **Project Settings** tab, click **Input**.
    
3.  Under the **Bindings** section, click the plus sign next to **Axis Mappings**.
    
4.  Click the arrow to the left of **Axis Mappings**.
    
5.  Type **Turn** into the text field that appears.
    
6.  In the dropdown menu, select **Mouse X** from the **Mouse** dropdown list.
    
7.  Your input settings should now look like the following:
    
    Click for full image.
    

### Look-up Axis Mapping

1.  Under the **Bindings** section, click the plus sign next to **Axis Mappings**.
    
2.  Type **LookUp** into the text field that appears.
    
3.  In the dropdown menu, select **Mouse Y** from the **Mouse** dropdown list.
    
4.  Type **\-1.0** in the **Scale** field next to **Mouse Y**.
    
5.  Your input settings should now look like the following:
    
    Click for full image.
    
6.  Close the **Project Settings** menu.
    

### Implementing Input Handling

Now it is time to add code to handle mouse input for turning and looking up. The `Character` base class defines the two necessary functions for us, namely:

-   `AddControllerYawInput`
-   `AddControllerPitchInput`
    
    If you want to perform additional processing, such as adding support for sensitivity or axis inversion, you could provide your own functions to adjust the input values before passing them to function. In this case however, you will bind your inputs directly to the `AddControllerYawInput` and `AddControllerPitchInput` functions.
    

1.  Add the following lines to the `SetupPlayerInputComponent` function in `FPSCharacter.cpp`.
    
    FPSCharacter.cpp
    
    ```
        `// Set up "look" bindings.     PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);     PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);`
    Copy full snippet
    ```
    // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);
2.  The `SetupPlayerInputComponent` function should now look like the following:
    
    FPSCharacter.cpp
    
    ```
        `// Called to bind functionality to input     void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)     {         Super::SetupPlayerInputComponent(PlayerInputComponent);                   // Set up "movement" bindings.         PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);         PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);                   // Set up "look" bindings.         PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);         PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);     }`
    Copy full snippet
    ```
    // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput); }

### Testing Mouse Camera Control

1.  Save the **FPSCharacter** implementation file in VS.
    
2.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
3.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8fe46e64-148e-4bc2-9765-cc99a186dc86/05-build-project.png)
4.  After the build finishes, open your **FPSProject** in the Unreal Editor.
    
5.  Click the **Play** button in the **Level Editor Toolbar**. You can now control the camera with your mouse.
    
6.  Before going to the next step, press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

## 2.5 - Implementing Character Jumping

In general, Action Mappings deals with inputs for discrete events, they allow you to map inputs to a "friendly name" that can later be bound to event-driven behavior. The end effect is pressing and/or releasing a key, mouse button, or keypad button directly triggers game behavior. During this step, you are going to add the ability for your character to jump by setting up the input action mapping for the space bar.

### Jump Action Mapping

1.  Click the **Edit** in the **Main** menu panel, select **Project Settings**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/afbab465-502c-4480-83d9-571690e8abae/11-open-project-settings.png)
2.  Under the **Engine** heading on the left side of the **Project Settings** tab, click **Input**.
    
3.  Under the **Bindings** section, click the plus sign next to **Action Mappings**.
    
4.  Click the arrow to the left of **Action Mappings**.
    
5.  Type **Jump** into the text field that appears.
    
6.  In the dropdown menu, select **Space Bar** from the **Keyboard** dropdown list.
    
7.  Your input settings should now look like the following:
    
    Click for full image.
    
8.  Close the **Project Settings** menu.
    

### Implement Input Handling

If you look inside the header file `.h` for the `ACharacter` base class, you will notice that there is built-in support for character jumping. Character jumping is tied to the `bPressedJump` variable, so all you need to do is set that boolean to `true` when the jump action is pressed, and `false` when the jump action is released. You will need to add the following two functions to accomplish this:

-   `StartJump`
-   `StopJump`

Go back to Visual Studio to add code to your `FPSCharacter` class.

1.  In `FPSCharacter.h`, add the following function declarations, under `public` access specifier:
    
    FPSCharacter.h
    
    ```
        `// Sets jump flag when key is pressed.     UFUNCTION()     void StartJump();               // Clears jump flag when key is released.     UFUNCTION()     void StopJump();`
    Copy full snippet
    ```
    // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump();
2.  `FPSCharacter.h` should now look like the following:
    
    FPSCharacter.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.               #pragma once               #include "CoreMinimal.h"     #include "GameFramework/Character.h"     #include "FPSCharacter.generated.h"               UCLASS()     class FPSPROJECT_API AFPSCharacter : public ACharacter     {         GENERATED_BODY()               public:         // Sets default values for this character's properties         AFPSCharacter();               protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;               public:         // Called every frame         virtual void Tick( float DeltaTime ) override;                   // Called to bind functionality to input         virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;                   // Handles input for moving forward and backward.         UFUNCTION()         void MoveForward(float Value);                   // Handles input for moving right and left.         UFUNCTION()         void MoveRight(float Value);                   // Sets jump flag when key is pressed.         UFUNCTION()         void StartJump();                   // Clears jump flag when key is released.         UFUNCTION()         void StopJump();     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump(); };
3.  In `FPSCharacter.cpp`, add the following function definitions to the bottom of the page:
    
    FPSCharacter.cpp
    
    ```
        `void AFPSCharacter::StartJump()     {         bPressedJump = true;     }       void AFPSCharacter::StopJump()     {         bPressedJump = false;     }`
    Copy full snippet
    ```
    void AFPSCharacter::StartJump() { bPressedJump = true; } void AFPSCharacter::StopJump() { bPressedJump = false; }
4.  Add the following lines to the `SetupPlayerInputComponent` function to bind your Jump action to the newly written functions:
    
    FPSCharacter.cpp
    
    ```
        `// Set up "action" bindings.     PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AFPSCharacter::StartJump);     PlayerInputComponent->BindAction("Jump", IE_Released, this, &AFPSCharacter::StopJump);`
    Copy full snippet
    ```
    // Set up "action" bindings. PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &AFPSCharacter::StartJump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &AFPSCharacter::StopJump);
5.  `FPSCharacter.cpp` should now look like the following:
    
    FPSCharacter.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.                        #include "FPSCharacter.h"               // Sets default values     AFPSCharacter::AFPSCharacter()     {         // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;               }               // Called when the game starts or when spawned     void AFPSCharacter::BeginPlay()     {         Super::BeginPlay();                   check(GEngine != nullptr);                        // Display a debug message for five seconds.          // The -1 "Key" valueargument prevents the message from being updated or refreshed.           GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));                  }               // Called every frame     void AFPSCharacter::Tick( float DeltaTime )     {         Super::Tick( DeltaTime );               }               // Called to bind functionality to input     void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)     {         Super::SetupPlayerInputComponent(PlayerInputComponent);                   // Set up "movement" bindings.         PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);         PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);                   // Set up "look" bindings.         PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);         PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);                   // Set up "action" bindings.         PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AFPSCharacter::StartJump);         PlayerInputComponent->BindAction("Jump", IE_Released, this, &AFPSCharacter::StopJump);     }               void AFPSCharacter::MoveForward(float Value)     {         // Find out which way is "forward" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);         AddMovementInput(Direction, Value);     }               void AFPSCharacter::MoveRight(float Value)     {         // Find out which way is "right" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);         AddMovementInput(Direction, Value);     }               void AFPSCharacter::StartJump()     {         bPressedJump = true;     }               void AFPSCharacter::StopJump()     {         bPressedJump = false;     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" valueargument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput); // Set up "action" bindings. PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &AFPSCharacter::StartJump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &AFPSCharacter::StopJump); } void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); } void AFPSCharacter::StartJump() { bPressedJump = true; } void AFPSCharacter::StopJump() { bPressedJump = false; }

### Testing Character Jumping

It is now time to compile and test your newly implemented character movement functions.

1.  Save the **FPSCharacter** header `.h` and implementation `.cpp` files in VS.
    
2.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
3.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8716e88e-49fe-4d9f-bdbc-61e2059d21f6/05-build-project.png)
4.  After the build finishes, open your **FPSProject** in the Unreal Editor.
    
5.  Click the **Play** button in the **Level Editor Toolbar**. You can now move forward, backward, left, and right using **WASD** keys.
    
6.  Before going to the next step, press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

## 2.6 - Adding a Mesh to your Character

Download and extract the sample mesh from the following link:

-   [Sample Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/ac9c23fb-66b6-4958-b1bb-67f0f557695a/genericmale.zip)

During this step, you will give the character a skeletal mesh. The Character class creates a SkeletalMeshComponent object for you by default, so all it needs to know is which SkeletalMesh asset to use.

### Importing a Skeletal Mesh

1.  Navigate to the **Content Browser** and open **Content** folder.
    
2.  Right-click inside the file window of the **Content Browser** to open the **Import Asset** dialog window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d675602b-77d1-4e0c-9503-f491420f84ba/21-fbx-import-option-1.png)
3.  Click **'Import to /Game...'** to open the **Import** dialog window.
    
4.  Locate and select the `GenericMale.fbx` mesh file in folder, where you have downloaded this file.
    
5.  Click **Open** to begin importing the mesh to your project.
    
6.  In the **Content Browser**, the **FBX Import Options** dialog windows appears. Click **Import All** to add your mesh to the Project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/bacc3e7c-2a58-46cc-8fa1-9e1ba764e33e/21-fbx-import-options.png)
7.  Click the **File** in the **Main** menu panel to save your imported mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/695742c7-0c72-40bc-90db-6850a24f68b4/22-save-all.png)

### Setting up a Third Person Mesh

1.  Double-click the **BP\_FPSCharacter** Blueprint Class icon in **Content > Blueprints** to open it in the **Blueprint Editor**.
    
    If you see a note about this Blueprint being a data only blueprint, click **Open Full Blueprint Editor**.
    
2.  Click the **Mesh** component in the **Components** tab.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/31baa892-b827-4a57-a9cf-ff387f3482cd/23-mesh-component.png)
3.  Navigate to the **Details** panel and scroll to the **Mesh** (right-side of screen, or under **Window > Details**).
    
4.  Open dropdown window under the **Skeletal Mesh** and select the **GenericMale** skeletal mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/28629840-3577-422b-a461-cc55f17f0520/24-select-skeletal-mesh.png)
5.  Scroll to the **Transform** section in the **Details** panel and align the `SkeletalMeshComponent` to the `CapsuleComponent` by setting its **Location** options to **X = -5.0; Y = 0.0; Z = -88.0**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f6cb2d5e-8474-4d5f-a097-1ce4e333827d/25-set-location-options.png)
6.  Click the **Viewport** in the **Blueprint Editor** to preview the Skeletal Mesh. It should look like the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8f534ef4-eb5c-401c-86ce-df1961680fb5/26-viewport.png)
    
    Verify that the skeletal mesh is inside the `CapsuleComponent` and that the mesh is facing the same direction as the `ArrowComponent`. Properly orienting the skeletal mesh component will ensure that your character moves through the world in the right way.
    
7.  Make sure to **Compile** and **Save** the **BP\_FPSCharacter** Blueprint before closing the **Blueprint Editor**.
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/93f26103-d7b1-470b-8e81-3fa0a6dad1c3/27-compile-save.png)

### Verifying the New Mesh in PIE Mode

It is now time to view your newly added mesh in-editor.

1.  Click the **Play** button in the Level Editor Toolbar. You should be able to see your character's shadow as you move around.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35a75b19-7716-4695-ba3c-2f9c127157a1/28-pawn-with-shadow.png)
    
    If you want to see your character's mesh inside the editor's Viewport, press the **F8** key to eject yourself from your pawn. After pressing the **F8** key, you'll be able to move your camera freely through the Level. To move your camera, hold the left mouse button down while moving the mouse at the same time.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/32943f73-c01a-4bac-9418-8481c31f0511/29-freely-moving-camera.png)
2.  Press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

## 2.7 - Changing the Camera View

At the end of the previous step, the default camera was positioned inside the mesh's neck. During this step, you're going to set-up an FPS camera that you can use to adjust the camera's properties (such as location and field of view). Before you get started, you need to expand your list of included files in `FPSCharacter.h`. This will allow your code to access more camera-related functions, and will ultimately allow you to manipulate your camera placement.

1.  Open your Visual Studio project, and navigate to `FPSCharacter.h`.
    
2.  Include the following header files to `FPSCharacter.h`.
    
    FPSCharacter.h
    
    ```
        `#include "Camera/CameraComponent.h"     #include "Components/CapsuleComponent.h"`
    Copy full snippet
    ```
    #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h"

### Attaching a Camera Component

1.  Open `FPSCharacter.h` to add the following code, under `public` access specifier:
    
    FPSCharacter.h
    
    ```
        `// FPS camera.     UPROPERTY(VisibleAnywhere)     UCameraComponent* FPSCameraComponent;`
    Copy full snippet
    ```
    // FPS camera. UPROPERTY(VisibleAnywhere) UCameraComponent\* FPSCameraComponent;
2.  `FPSCharacter.h` should now look like the following:
    
    FPSCharacter.h
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.           #pragma once           #include "CoreMinimal.h"     #include "GameFramework/Character.h"     #include "Camera/CameraComponent.h"     #include "Components/CapsuleComponent.h"     #include "FPSCharacter.generated.h"                UCLASS()     class FPSPROJECT_API AFPSCharacter : public ACharacter     {         GENERATED_BODY()           public:         // Sets default values for this character's properties         AFPSCharacter();           protected:         // Called when the game starts or when spawned         virtual void BeginPlay() override;           public:              // Called every frame         virtual void Tick( float DeltaTime ) override;               // Called to bind functionality to input         virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;               // Handles input for moving forward and backward.         UFUNCTION()         void MoveForward(float Value);               // Handles input for moving right and left.         UFUNCTION()         void MoveRight(float Value);               // Sets jump flag when key is pressed.         UFUNCTION()         void StartJump();               // Clears jump flag when key is released.         UFUNCTION()         void StopJump();               // FPS camera         UPROPERTY(VisibleAnywhere)         UCameraComponent* FPSCameraComponent;     };`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Character.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump(); // FPS camera UPROPERTY(VisibleAnywhere) UCameraComponent\* FPSCameraComponent; };
3.  Open `FPSCharacter.cpp` and add the following code to the constructor below `PrimaryActorTick.bCanEverTick = true:`.
    
    FPSCharacter.cpp
    
    ```
        `// Create a first person camera component.     FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));     check(FPSCameraComponent != nullptr);      // Attach the camera component to our capsule component.     FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent()));`
    Copy full snippet
    ```
    // Create a first person camera component. FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FPSCameraComponent != nullptr); // Attach the camera component to our capsule component. FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent()));
    
    This code creates a `UCameraComponent` and attaches it to the character's `CapsuleComponent`.
    
4.  Add the following code underneath the block that you just wrote in the constructor:
    
    FPSCharacter.cpp
    
    ```
        `// Position the camera slightly above the eyes.     FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight));               // Enable the pawn to control camera rotation.     FPSCameraComponent->bUsePawnControlRotation = true;`
    Copy full snippet
    ```
    // Position the camera slightly above the eyes. FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight)); // Enable the pawn to control camera rotation. FPSCameraComponent->bUsePawnControlRotation = true;
    
    This code adjusts the camera's position to be slightly above the character's eye position while allowing the pawn to control the camera's rotation.
    
    `SetRelativeLocation` sets the default for the component. However, the previous value will still be set in the Editor. To correct this, open the **Blueprint Editor**. Click the `FPSCameraComponent` and in the **Details** panel locate the **Transform > Location** value. Click the **Reset to Default** icon next to that value.
    
5.  `FPSCharacter.cpp` should now look like the following:
    
    FPSCharacter.cpp
    
    ```
        `// Copyright Epic Games, Inc. All Rights Reserved.                        #include "FPSCharacter.h"               // Sets default values     AFPSCharacter::AFPSCharacter()     {         // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.         PrimaryActorTick.bCanEverTick = true;                   // Create a first person camera component.         FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));         check(FPSCameraComponent != nullptr);                   // Attach the camera component to our capsule component.         FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent()));                   // Position the camera slightly above the eyes.         FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight));                   // Enable the pawn to control camera rotation.         FPSCameraComponent->bUsePawnControlRotation = true;     }               // Called when the game starts or when spawned     void AFPSCharacter::BeginPlay()     {         Super::BeginPlay();                   check(GEngine != nullptr)                      // Display a debug message for five seconds.          // The -1 "Key" value (first argument) indicates that we will never need to update or refresh this message.         GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));     }               // Called every frame     void AFPSCharacter::Tick( float DeltaTime )     {         Super::Tick( DeltaTime );               }               // Called to bind functionality to input     void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)     {         Super::SetupPlayerInputComponent(PlayerInputComponent);                   // Set up "movement" bindings.         PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);         PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);                   // Set up "look" bindings.         PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);         PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);                   // Set up "action" bindings.         PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AFPSCharacter::StartJump);         PlayerInputComponent->BindAction("Jump", IE_Released, this, &AFPSCharacter::StopJump);     }               void AFPSCharacter::MoveForward(float Value)     {         // Find out which way is "forward" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);         AddMovementInput(Direction, Value);     }               void AFPSCharacter::MoveRight(float Value)     {         // Find out which way is "right" and record that the player wants to move that way.         FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);         AddMovementInput(Direction, Value);     }               void AFPSCharacter::StartJump()     {         bPressedJump = true;     }               void AFPSCharacter::StopJump()     {         bPressedJump = false;     }`
    Copy full snippet
    ```
    // Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Create a first person camera component. FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FPSCameraComponent != nullptr); // Attach the camera component to our capsule component. FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent, UCapsuleComponent>(GetCapsuleComponent())); // Position the camera slightly above the eyes. FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight)); // Enable the pawn to control camera rotation. FPSCameraComponent->bUsePawnControlRotation = true; } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr) // Display a debug message for five seconds. // The -1 "Key" value (first argument) indicates that we will never need to update or refresh this message. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput); // Set up "action" bindings. PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &AFPSCharacter::StartJump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &AFPSCharacter::StopJump); } void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); } void AFPSCharacter::StartJump() { bPressedJump = true; } void AFPSCharacter::StopJump() { bPressedJump = false; }

### Testing the New Camera

It is now time to compile and test your newly implemented camera code.

1.  Save the **FPSCharacter** header `.h` and implementation `.cpp` files in VS.
    
2.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
3.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e3840002-b3bf-458d-baeb-5eb03d511ab4/05-build-project.png)
4.  After the build finishes, open your **FPSProject** in the Unreal Editor.
    
5.  Click the **Play** button in the **Level Editor Toolbar**.
    

The camera should now be slightly above your character's head.

You can also verify your newly added camera component by opening the **BP\_FPSCharacter** in the **Viewport**.

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5f52e1d3-137c-4412-978b-f647188b8d0f/30-camera-above-character.png)

If you open **BP\_FPSCharacter** in the **COntent Browser** and navigate to **Viewport** your character should look like the following:

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8a0e14af-b99a-40d1-ae83-400d520cfdb9/31-camera-above-character-viewport.png)

## 2.8 - Add a First Person Mesh to your Character

A common approach for building FPS games is to use two separate character meshes where one is the full-body mesh and the other is the "weapon and hands" mesh. The full-body mesh is used to see the character from a third-person perspective; however, it is hidden when the player is viewing the game in first-person perspective. The "weapon and hands" mesh is typically attached to the camera and is only visible to the player when they are viewing the map in first-person perspective. During this step, you are going to add a first person mesh to your character.

### Adding the First Person Character Mesh

1.  Switch back to Visual Studio and open `FPSCharacter.h` to add the following code under `public`:
    
    FPSCharacter.h
    
    ```
        `// First-person mesh (arms), visible only to the owning player.     UPROPERTY(VisibleDefaultsOnly, Category = Mesh)     USkeletalMeshComponent* FPSMesh;`
    Copy full snippet
    ```
    // First-person mesh (arms), visible only to the owning player. UPROPERTY(VisibleDefaultsOnly, Category = Mesh) USkeletalMeshComponent\* FPSMesh;
2.  Open `FPSCharacter.cpp`, go to the constructor, and add the following code to create and configure the first person mesh:
    
    FPSCharacter.cpp
    
    ```
        `// Create a first person mesh component for the owning player.     FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh"));     check(FPSMesh != nullptr);               // Only the owning player sees this mesh.     FPSMesh->SetOnlyOwnerSee(true);               // Attach the FPS mesh to the FPS camera.     FPSMesh->SetupAttachment(FPSCameraComponent);               // Disable some environmental shadows to preserve the illusion of having a single mesh.     FPSMesh->bCastDynamicShadow = false;     FPSMesh->CastShadow = false;`
    Copy full snippet
    ```
    // Create a first person mesh component for the owning player. FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh")); check(FPSMesh != nullptr); // Only the owning player sees this mesh. FPSMesh->SetOnlyOwnerSee(true); // Attach the FPS mesh to the FPS camera. FPSMesh->SetupAttachment(FPSCameraComponent); // Disable some environmental shadows to preserve the illusion of having a single mesh. FPSMesh->bCastDynamicShadow = false; FPSMesh->CastShadow = false;
    
    `SetOnlyOwnerSee` indicates that this mesh is only visible to the `PlayerController` that has possessed this Character. This code is also attaching the mesh to the camera and disabling some environmental shadowing. Allowing the arms to cast shadows would destroy the illusion of having a single mesh for the first person character.
    
3.  Finally, add the following code to the constructor in `PSCharacter.cpp` to hide the existing third-person mesh from the owning character:
    
    FPSCharacter.cpp
    
    ```
        `// The owning player doesn't see the regular (third-person) body mesh.     GetMesh()->SetOwnerNoSee(true);`
    Copy full snippet
    ```
    // The owning player doesn't see the regular (third-person) body mesh. GetMesh()->SetOwnerNoSee(true);
4.  Save the **FPSCharacter** header `.h` and implementation `.cpp` files in Visual Studio.
    
5.  Navigate to the **Solution Explorer** and select **FPSProject**.
    
6.  Right-click on **FPSProject** and select **Build** to compile your project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/0af11396-9869-4e8c-a7d0-d5c9aa7a685c/05-build-project.png)
7.  After the build finishes, open your **FPSProject** in the Unreal Editor.
    
8.  Click the **Play** button in the **Level Editor Toolbar**. Now you should not see shadow from your character in PIE mode. It should look like the following:
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/aca65b90-3234-4116-981b-cc0471f512d0/32-hidden-mesh-ingame.png)

At this point, your character mesh should not be visible inside the Editor.

If you still see your mesh and its shadow cast, close and restart the Editor.

### Building the Mesh Blueprint

Before continuing, download and extract the sample mesh from the following link:

-   [First Person Skeletal Mesh](https://d1iv7db44yhgxn.cloudfront.net/documentation/attachments/7684db32-2f4d-422d-bfe1-8ece9ba1f765/herofpp.zip)

1.  Navigate to the **Content Browser** and open the **Content** folder.
    
2.  Right-click inside the file window of the **Content Browser** to open the **Import Asset** dialog window.
    
3.  Click **Import to /Game...** to open the **Import** dialog window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1776fc84-12fd-45a5-b44e-7b42e588d43d/33-import-option.png)
4.  Locate and select the **HeroFPP.fbx** mesh file, where you have downloaded this file.
    
5.  Click **Open** to begin importing the mesh to your project.
    
6.  In the **Content Browser**, the **FBX Import Options** dialog windows appears.
    
7.  In the **FBX Import Options** dialog window from dropdown menu under **Sceleton** section select **Clear**, then click **Import All**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/02a4de30-9278-4807-8d2b-572627b1fd4b/34-clear-option.png)
8.  Close the following **Message Log** window.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2f2d4840-a259-4816-abb2-fb28812e7195/35-message-log.png)  
    
    This mesh still shows the first person mesh set-up and it will work with the animations you'll set-up in a later section.
    
9.  Click the **File** in the **Main** menu panel to save your imported mesh.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b3741e6e-3cc6-416f-9086-cb6b9afe787a/22-save-all.png)
10.  Navigate to the **Blueprints** folder in the **Content Browser**.
    
11.  Double-click the **BP\_FPSCharacter** icon to open it in the **Blueprint Editor**.
    
12.  In **Blueprint Editor** navigate to the **Components** tab and select the new **FPSMesh** component. You may need to open the **Full Blueprint Editor** first.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/371fab1b-1490-4eb3-8ecd-b813c1fa5385/36-select-mesh-component.png)
    
    The **FPSMesh** component is a child of the **FPSCameraComponent**, which means that it will always be attached to the camera.
    
13.  Navigate to the **Details** panel and scroll to the **Mesh** section, click the dropdown menu under **Skeletal Mesh**. In dropdown menu, select the **HeroFPP** skeletal mesh to add the arms to the **Viewport**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2b62cbb5-2ba6-4e5b-8ec3-7ef1d923ff25/37-select-hero-fpp.png)
14.  The added **HeroFPP** skeletal mesh should look like the following inside the **Viewport**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/35ec4df3-4beb-44c4-abb3-93bc9e57ac67/38-hero-fpp-viewport.png)
15.  Adjust the **Transform** option of added mesh. Set **Location** to **{220, 0, 35}** and **Rotation** to **{180, 50, 180}**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/4f222668-1c24-4e08-8b90-6fbd03c47bca/39-transform-settings.png)
16.  This settings transform **HeroFPP** skeletal mesh to be in front of the camera.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5632f1dd-2b3c-429e-a50e-c8f45863983c/40-bpfpscharacter-viewport.png)
17.  Make sure to **Compile** and **Save** the **BP\_FPSCharacter** Blueprint before closing the **Blueprint Editor**.
    

### Viewing the New Mesh In-Game

1.  Click the **Play** button in the **Level Editor Toolbar** to view the new mesh in-game.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5938115b-3e3c-426f-9ce6-47f1d42b9c36/41-result.png)
2.  Press the **Shift + Escape** or click **Stop** in the **Level Editor Toolbar** to exit PIE mode.
    

### Finished Section Code

FPSCharacter.h

```
`// Copyright Epic Games, Inc. All Rights Reserved.       #pragma once       #include "GameFramework/Character.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "FPSCharacter.generated.h"       UCLASS() class FPSPROJECT_API AFPSCharacter : public ACharacter {     GENERATED_BODY()   public:     // Sets default values for this character's properties     AFPSCharacter();       protected:               // Called when the game starts or when spawned     virtual void BeginPlay() override;       public:      // Called every frame     virtual void Tick( float DeltaTime ) override;           // Called to bind functionality to input     virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;           // Handles input for moving forward and backward.     UFUNCTION()     void MoveForward(float Value);           // Handles input for moving right and left.     UFUNCTION()     void MoveRight(float Value);           // Sets jump flag when key is pressed.     UFUNCTION()     void StartJump();           // Clears jump flag when key is released.     UFUNCTION()     void StopJump();           // FPS camera     UPROPERTY(VisibleAnywhere)     UCameraComponent* FPSCameraComponent;           // First-person mesh (arms), visible only to the owning player.     UPROPERTY(VisibleDefaultsOnly, Category = Mesh)     USkeletalMeshComponent* FPSMesh; };`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #pragma once #include "GameFramework/Character.h" #include "Camera/CameraComponent.h" #include "Components/CapsuleComponent.h" #include "FPSCharacter.generated.h" UCLASS() class FPSPROJECT\_API AFPSCharacter : public ACharacter { GENERATED\_BODY() public: // Sets default values for this character's properties AFPSCharacter(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaTime ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* PlayerInputComponent) override; // Handles input for moving forward and backward. UFUNCTION() void MoveForward(float Value); // Handles input for moving right and left. UFUNCTION() void MoveRight(float Value); // Sets jump flag when key is pressed. UFUNCTION() void StartJump(); // Clears jump flag when key is released. UFUNCTION() void StopJump(); // FPS camera UPROPERTY(VisibleAnywhere) UCameraComponent\* FPSCameraComponent; // First-person mesh (arms), visible only to the owning player. UPROPERTY(VisibleDefaultsOnly, Category = Mesh) USkeletalMeshComponent\* FPSMesh; };

FPSCharacter.cpp

```
`// Copyright Epic Games, Inc. All Rights Reserved.            #include "FPSCharacter.h"       // Sets default values AFPSCharacter::AFPSCharacter() {     // Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.     PrimaryActorTick.bCanEverTick = true;           // Create a first person camera component.     FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));     check(FPSCameraComponent != nullptr);           // Attach the camera component to our capsule component.     FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent>(GetCapsuleComponent()));           // Position the camera slightly above the eyes.     FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight));           // Enable the pawn to control camera rotation.     FPSCameraComponent->bUsePawnControlRotation = true;           // Create a first person mesh component for the owning player.     FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh"));     check(FPSMesh != nullptr);           // Only the owning player sees this mesh.     FPSMesh->SetOnlyOwnerSee(true);           // Attach the FPS mesh to the FPS camera.     FPSMesh->SetupAttachment(FPSCameraComponent);           // Disable some environmental shadowing to preserve the illusion of having a single mesh.     FPSMesh->bCastDynamicShadow = false;     FPSMesh->CastShadow = false;           // The owning player doesn't see the regular (third-person) body mesh.     GetMesh()->SetOwnerNoSee(true); }       // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() {     Super::BeginPlay();           check(GEngine != nullptr);              // Display a debug message for five seconds.      // The -1 "Key" value argument prevents the message from being updated or refreshed.       GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter."));          }       // Called every frame void AFPSCharacter::Tick( float DeltaTime ) {     Super::Tick( DeltaTime );   }       // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent) {     Super::SetupPlayerInputComponent(PlayerInputComponent);       // Set up "movement" bindings.     PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward);     PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight);           // Set up "look" bindings.     PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput);     PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput);           // Set up "action" bindings.     PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AFPSCharacter::StartJump);     PlayerInputComponent->BindAction("Jump", IE_Released, this, &AFPSCharacter::StopJump); }       void AFPSCharacter::MoveForward(float Value) {     // Find out which way is "forward" and record that the player wants to move that way.     FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X);     AddMovementInput(Direction, Value); }       void AFPSCharacter::MoveRight(float Value) {     // Find out which way is "right" and record that the player wants to move that way.     FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y);     AddMovementInput(Direction, Value); }       void AFPSCharacter::StartJump() {     bPressedJump = true; }       void AFPSCharacter::StopJump() {     bPressedJump = false; }`
Copy full snippet
```
// Copyright Epic Games, Inc. All Rights Reserved. #include "FPSCharacter.h" // Sets default values AFPSCharacter::AFPSCharacter() { // Set this character to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Create a first person camera component. FPSCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FPSCameraComponent != nullptr); // Attach the camera component to our capsule component. FPSCameraComponent->SetupAttachment(CastChecked<USceneComponent>(GetCapsuleComponent())); // Position the camera slightly above the eyes. FPSCameraComponent->SetRelativeLocation(FVector(0.0f, 0.0f, 50.0f + BaseEyeHeight)); // Enable the pawn to control camera rotation. FPSCameraComponent->bUsePawnControlRotation = true; // Create a first person mesh component for the owning player. FPSMesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh")); check(FPSMesh != nullptr); // Only the owning player sees this mesh. FPSMesh->SetOnlyOwnerSee(true); // Attach the FPS mesh to the FPS camera. FPSMesh->SetupAttachment(FPSCameraComponent); // Disable some environmental shadowing to preserve the illusion of having a single mesh. FPSMesh->bCastDynamicShadow = false; FPSMesh->CastShadow = false; // The owning player doesn't see the regular (third-person) body mesh. GetMesh()->SetOwnerNoSee(true); } // Called when the game starts or when spawned void AFPSCharacter::BeginPlay() { Super::BeginPlay(); check(GEngine != nullptr); // Display a debug message for five seconds. // The -1 "Key" value argument prevents the message from being updated or refreshed. GEngine->AddOnScreenDebugMessage(-1, 5.0f, FColor::Red, TEXT("We are using FPSCharacter.")); } // Called every frame void AFPSCharacter::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void AFPSCharacter::SetupPlayerInputComponent(UInputComponent\* PlayerInputComponent) { Super::SetupPlayerInputComponent(PlayerInputComponent); // Set up "movement" bindings. PlayerInputComponent->BindAxis("MoveForward", this, &AFPSCharacter::MoveForward); PlayerInputComponent->BindAxis("MoveRight", this, &AFPSCharacter::MoveRight); // Set up "look" bindings. PlayerInputComponent->BindAxis("Turn", this, &AFPSCharacter::AddControllerYawInput); PlayerInputComponent->BindAxis("LookUp", this, &AFPSCharacter::AddControllerPitchInput); // Set up "action" bindings. PlayerInputComponent->BindAction("Jump", IE\_Pressed, this, &AFPSCharacter::StartJump); PlayerInputComponent->BindAction("Jump", IE\_Released, this, &AFPSCharacter::StopJump); } void AFPSCharacter::MoveForward(float Value) { // Find out which way is "forward" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::X); AddMovementInput(Direction, Value); } void AFPSCharacter::MoveRight(float Value) { // Find out which way is "right" and record that the player wants to move that way. FVector Direction = FRotationMatrix(Controller->GetControlRotation()).GetScaledAxis(EAxis::Y); AddMovementInput(Direction, Value); } void AFPSCharacter::StartJump() { bPressedJump = true; } void AFPSCharacter::StopJump() { bPressedJump = false; }

Congratulations! You've learned how to:

✓ Make a New Character  
✓ Set-up Axis Mapping  
✓ Implement Character Movement Functions  
✓ Implement Mouse Camera Control  
✓ Implement Character Jumping  
✓ Add a Mesh to your Character  
✓ Change the Camera View  
✓ Add a First Person Mesh to your Character

You're now ready to learn how to implement projectiles in the next section.