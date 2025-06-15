# Add a First-Person Camera, Mesh, and Animation

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-a-firstperson-camera-mesh-and-animation](https://dev.epicgames.com/documentation/en-us/unreal-engine/adding-a-firstperson-camera-mesh-and-animation)  
**Processed:** 2025-06-14 16:04:55

---

## Before You Start

Ensure you've completed the following objectives in the previous section, [Configure Character Movement](https://dev.epicgames.com/documentation/en-us/unreal-engine/configure-character-movement-with-cplusplus-in-unreal-engine):

-   Understand how Input Actions and Input Mapping Contexts work.
    
-   Set up a character with forward, backward, left, right, and jump movements.
    

## First-Person Camera Controls

To change the camera orientation, we change the **Rotation** value of the camera’s **Transform** property. To rotate in a 3D space, objects use **Pitch**, **Roll**, and **Yaw** to control what direction they turn and along what axis. 

-   **Pitch**: Controls rotation along the horizontal (X) axis. Changing it rotates an object up or down, similar to nodding your head.
    
-   **Yaw**: Controls rotation along the vertical (Y) axis. Changing it rotates an object left or right, similar to rotating right or left.
    
-   **Roll**: Controls rotation along the longitudinal (Z) axis. Changing it rolls an object side to side, similar to leaning your head  right or left.
    

[![](https://dev.epicgames.com/community/api/documentation/image/68b6eac6-cc09-4775-ad76-952273e35772?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/68b6eac6-cc09-4775-ad76-952273e35772?resizing_type=fit)

Cameras in first-person games usually use Yaw and Pitch to control movement. Roll may become relevant if you’re programming a game where you need to rotate an airplane or spaceship or if you need to simulate peeking around corners.

### Explore Camera Movement in Blueprints

Open `BP_FirstPersonCharacter` to view the default character’s camera control logic in the **Blueprint Editor**. In the **EventGraph**, look at two nodes in the top-left corner of the **Camera Input** node group. 

[![](https://dev.epicgames.com/community/api/documentation/image/38921b15-a318-4652-a948-3b7f284c4a8e?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/38921b15-a318-4652-a948-3b7f284c4a8e?resizing_type=fit)

Just like with `IA_Move`, the `IA_Look` input action has an **Axis2D Value Type**, so it splits movement into both **X** and **Y** values. This time, X and Y become the custom **Aim** function's **Yaw** and **Pitch** inputs.

Double-click the **Aim** function node to see the logic inside. The **Add Controller Yaw Input** and **Pitch Input** function nodes add the values to the character. 

[![](https://dev.epicgames.com/community/api/documentation/image/9e327229-2f0b-4052-8f5f-72dad5050706?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/9e327229-2f0b-4052-8f5f-72dad5050706?resizing_type=fit)

### Explore First-Person Character Components

Go to `BP_FirstPersonCharacter`‘s **Viewport** tab to view a 3D preview of the Actor and its components. 

In the **Components** tab, you’ll see a structured hierarchy of attached components that define the character in the world. 

Character Blueprints are automatically instantiated with: 

-   a **Capsule Component** that makes the character collide with objects in the world.
    
-   a **Skeletal Mesh** component that enables animations and visualizes the character. In the **Details** panel, you’ll see this character uses `SKM_Manny_Simple` as its **Skeletal Mesh Asset**.
    
-   A **Character Movement Component** that allows the character to move around.
    

[![](https://dev.epicgames.com/community/api/documentation/image/c293fb8d-d025-4f6d-8a7b-b1773d7fad7f?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/c293fb8d-d025-4f6d-8a7b-b1773d7fad7f?resizing_type=fit)

This character also has a second **Skeletal Mesh** named **FirstPersonMesh** (also using `SKM_Manny_Simple`) that is a child of the main mesh component. In first-person games, characters usually have separate meshes for both third-person and first-person contexts. The third-person mesh is only visible to other players or when the player is in a third-person view. The first-person mesh is visible to the player when they are in first-person view. 

The **FirstPersonMesh** has a child **Camera Component** named **FirstPersonCamera**. This camera determines the player’s first-person view and rotates with the character as they look around. In this part of the tutorial, you’ll use C++ to instantiate a camera on your character at runtime and position it to match this camera’s position. 

For more information about Character components, see the [Characters Gameplay Framework documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/characters-in-unreal-engine).

## Implement Look Input in Code

To implement this camera functionality in code, just like the movement you implemented in the previous step, you’ll bind the `IA_Look` input action to a function and then bind that function to your character. 

### Declare the Look() Function and Variables

In Visual Studio, open your character’s `.h` file. 

The code samples in this tutorial use a Character class named `AdventureCharacter`.

When your character is built at runtime, you’ll tell UE to add a camera component to it and position the camera dynamically. To enable this functionality, add a new `#include` for `”Camera/CameraComponent.h”`:  

C++

`#include "CoreMinimal.h" #include "Camera/CameraComponent.h" #include "GameFramework/Character.h" #include "EnhancedInputComponent.h" #include "EnhancedInputSubsystems.h"  #include "InputActionValue.h" #include "AdventureCharacter.generated.h"`

#include "CoreMinimal.h" #include "Camera/CameraComponent.h" #include "GameFramework/Character.h" #include "EnhancedInputComponent.h" #include "EnhancedInputSubsystems.h" #include "InputActionValue.h" #include "AdventureCharacter.generated.h"

Copy full snippet(7 lines long)

In the header’s `protected` section, declare a new `UInputAction` pointer named `LookAction`. Give this pointer the same `UPROPERTY()` macro as `MoveAction` and `JumpAction`. This will point to the `IA_Look` Input Action.

C++

`// Look Input Actions UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input) UInputAction* LookAction;`

// Look Input Actions UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Input) UInputAction\* LookAction;

Copy full snippet(3 lines long)

In the `public` section, declare a new function named `Look()` that takes a const `FInputActionValue` reference named `Value`. Ensure you add a `UFUNCTION()` macro to the function. 

C++

`// Handles Look Input UFUNCTION() void Look(const FInputActionValue& Value);`

// Handles Look Input UFUNCTION() void Look(const FInputActionValue& Value);

Copy full snippet(3 lines long)

After the `Look()` function declaration, declare a new `UCameraComponent` pointer named `FirstPersonCameraComponent`. To expose this property to Unreal Editor, add a `UPROPERTY()` macro with the `VisibleAnywhere` argument. 

C++

`// First Person camera UPROPERTY(VisibleAnywhere) UCameraComponent* FirstPersonCameraComponent;`

// First Person camera UPROPERTY(VisibleAnywhere) UCameraComponent\* FirstPersonCameraComponent;

Copy full snippet(3 lines long)

After `FirstPersonCameraComponent`, declare a new `USkeletalMeshComponent` pointer named `FirstPersonMeshComponent`. Give it a `UPROPERTY()` macro with `VisibleAnywhere` and `Category = Mesh` arguments so it appears in the **Mesh** section of the **Details** panel. 

C++

`// First-person mesh, visible only to the owning player UPROPERTY(VisibleAnywhere, Category = Mesh) USkeletalMeshComponent* FirstPersonMeshComponent;`

// First-person mesh, visible only to the owning player UPROPERTY(VisibleAnywhere, Category = Mesh) USkeletalMeshComponent\* FirstPersonMeshComponent;

Copy full snippet(3 lines long)

You’ve now set up declarations for the following: 

-   First-person mesh (which correlates to the child FirstPersonMesh you saw in the Blueprint)
    
-   Camera
    
-   `Look()` function
    
-   `IA_Look` Input Action
    

Your character’s `.h` file should now look like this:

C++

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Camera/CameraComponent.h" #include "GameFramework/Character.h" #include "EnhancedInputComponent.h" #include "EnhancedInputSubsystems.h"  #include "InputActionValue.h"`

```

Expand codeCopy full snippet(67 lines long)

### Add Look Input with Look()

Open your character’s `.cpp` file to implement the Character Blueprint’s camera input logic using the `Look()` function.

Just as with `IA_Move`, `IA_Look` returns an FVector2d value when triggered. Add a new function definition for `Look()`. Inside the function, get the value of the `FInputActionValue` inside a new `FVector2d` named `LookAxisValue`.

C++

`void AAdventureCharacter::Look(const FInputActionValue& Value) { 	const FVector2D LookAxisValue = Value.Get<FVector2D>(); }`

void AAdventureCharacter::Look(const FInputActionValue& Value) { const FVector2D LookAxisValue = Value.Get<FVector2D>(); }

Copy full snippet(4 lines long)

Next, in an `if` statement, check if the Controller is valid. 

If it is, call `AddControllerYawInput()` and `AddControllerPitchInput()`, passing the `LookAxisValue.X` and `LookAxisValue.Y` values, respectively. Your complete `Look()` function should look like the following:

C++

`void AAdventureCharacter::Look(const FInputActionValue& Value) { 	const FVector2D LookAxisValue = Value.Get<FVector2D>();  	if (Controller) 	{ 		AddControllerYawInput(LookAxisValue.X); 		AddControllerPitchInput(LookAxisValue.Y); 	} }`

void AAdventureCharacter::Look(const FInputActionValue& Value) { const FVector2D LookAxisValue = Value.Get<FVector2D>(); if (Controller) { AddControllerYawInput(LookAxisValue.X); AddControllerPitchInput(LookAxisValue.Y); } }

Copy full snippet(10 lines long)

### Bind Look Functionality to Input with SetupPlayerInputComponent

Inside `SetupPlayerInputComponent()`, similar to the movement actions, you’ll bind the `Look()` function to the `LookAction` Input Action. 

C++

`EnhancedInputComponent->BindAction(LookAction, ETriggerEvent::Triggered, this, &AAdventureCharacter::Look);`

EnhancedInputComponent->BindAction(LookAction, ETriggerEvent::Triggered, this, &AAdventureCharacter::Look);

Copy full snippet(1 line long)

Your `SetupPlayerInputComponent()` function should now look like the following:

C++

```code
`// Called to bind functionality to input void AAdventureCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent) { 	// Check the UInputComponent passed to this function and cast it to an UEnhancedInputComponent 	if (UEnhancedInputComponent* EnhancedInputComponent = CastChecked<UEnhancedInputComponent>(PlayerInputComponent)) 	{ 		// Bind Movement Actions 		EnhancedInputComponent->BindAction(MoveAction, ETriggerEvent::Triggered, this, &AAdventurenCharacter::Move);  		// Bind Look Actions`

```

Expand codeCopy full snippet(18 lines long)

Save your code and compile it by clicking **Build** in Visual Studio. 

### Assign a Look Input Action in the Blueprint

Last, assign an Input Action to the Character Blueprint’s new **Look Action** property.

To assign look controls to your character, follow these steps:

1.  In Unreal Editor open your Character Blueprint.
    
2.  In the **Components** panel, ensure the root `BP_*[CharacterName]*` component is selected.
    
3.  In the **Details** panel, in the **Input** section, set **Look Action** to `IA_Look`.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/2be42f01-d466-46c8-bc75-f81a22d01dda?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/2be42f01-d466-46c8-bc75-f81a22d01dda?resizing_type=fit)
    
4.  Compile and save your Blueprint.
    

### Test Look Movements

If you press **Play** to test out your game, you’ll be able to look around and move your character in any direction you want! 

Note that while your in-game view appears to come from a first-person camera, you don’t actually have a camera component on your character yet. Instead, Unreal Engine simulates a view from the center of your character’s capsule component. In the next step, you’ll learn to change this by adding a camera to your Character class.

## Create Components at Runtime

Next, you’ll finish creating your character’s first-person mesh and camera by instantiating the `FirstPersonCameraComponent` and `FirstPersonMeshComponent` pointers you declared in the header file.

To get started, open your character’s `.cpp` file. 

At the top of the file, you’ll see the Construction Script function (`AAdventureCharacter()` in this tutorial) that sets the default values for your character. This is where you’ll add additional components. For an overview of what you can do with Construction Scripts, see the [Construction Script Blueprint node](https://dev.epicgames.com/documentation/en-us/unreal-engine/construction-script-in-unreal-engine) documentation.

### Add the Camera

To add components to the Character, you’ll use the `CreateDefaultSubobject()` template function. It returns a pointer to the new component and takes the following arguments:

`CreateDefaultSubobject<*type*>(TEXT(“*Name*”));`

Where *type* is the type of subobject you’re creating and *Name* is the internal name Unreal Engine uses to identify the subobject and display it in the editor.

In the Construction Script, set the `FirstPersonCameraComponent` pointer to the result of calling `CreateDefaultSubobject()` of type `UCameraComponent`. In the `TEXT` argument, name the object ”FirstPersonCamera”. 

C++

`FirstPersonCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));`

FirstPersonCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));

Copy full snippet(1 line long)

This creates a default camera object as a child of the Character class.  dsd, to ensure the camera was properly instantiated, check that `FirstPersonCameraComponent` isn’t null. 

C++

`// Create a first person camera component. FirstPersonCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FirstPersonCameraComponent != nullptr);`

// Create a first person camera component. FirstPersonCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); check(FirstPersonCameraComponent != nullptr);

Copy full snippet(3 lines long)

### Add the First-Person Mesh

Create another `CreateDefaultSubobject` function call for `FirstPersonMeshComponent` with `USkeletalMeshComponent` as the type and “FirstPersonMesh” as the name. Remember to add a `check` afterwards.

C++

`// Create a first person mesh component for the owning player. FirstPersonMeshComponent = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh")); 	check(FirstPersonMeshComponent != nullptr);`

// Create a first person mesh component for the owning player. FirstPersonMeshComponent = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("FirstPersonMesh")); check(FirstPersonMeshComponent != nullptr);

Copy full snippet(3 lines long)

### Attach the Mesh and Camera

Now that your mesh is created, you need to attach it to the character. 

The `SetupAttachment()` function attaches one scene component to another, establishing a parent-child relationship in the component hierarchy. It takes the parent component as an argument. 

Call the `SetupAttachment()` function on the object that `FirstPersonMeshComponent` points to. In this case, the parent component should be the character’s default skeletal mesh, which you can get using `GetMesh()`:

C++

`// Attach the FirstPerson mesh to the Skeletal Mesh FirstPersonMeshComponent->SetupAttachment(GetMesh());`

// Attach the FirstPerson mesh to the Skeletal Mesh FirstPersonMeshComponent->SetupAttachment(GetMesh());

Copy full snippet(2 lines long)

This attaches the first-person mesh as a child under the character’s third-person mesh.

Next, use another `SetupAttachment()` call to attach the camera component to the first-person mesh. This time, you’ll add an optional overload to specify an exact location (a **socket**) on the mesh where the component should attach.

The `SKM_Manny_Simple` mesh used in this tutorial has a collection of preset sockets (or bones) used for animation. You can reference sockets in code using an `FName` string. It’s best to position the camera near the character’s head, so you’ll pass the `Head` socket name to `SetupAttachment` to attach the camera to that socket. You’ll move the camera closer to the character’s eyes later.

`FName` is a special string-like type used in Unreal Engine to store unique, immutable names in a memory-efficient way.

C++

`// Attach the camera component to the first-person Skeletal Mesh. FirstPersonCameraComponent->SetupAttachment(FirstPersonMeshComponent, FName("Head"));`

// Attach the camera component to the first-person Skeletal Mesh. FirstPersonCameraComponent->SetupAttachment(FirstPersonMeshComponent, FName("Head"));

Copy full snippet(2 lines long)

For more information about what sockets are and how they’re created, see [Skeletal Mesh Sockets](https://dev.epicgames.com/documentation/en-us/unreal-engine/skeletal-mesh-sockets-in-unreal-engine).

Finally, set `FirstPersonCameraComponent`'s `bUsePawnControlRotation` property to `true`. This makes the camera inherit rotation from its parent Pawn so when the character turns, the camera follows. 

C++

`// Enable the pawn to control camera rotation. FirstPersonCameraComponent->bUsePawnControlRotation = true;`

// Enable the pawn to control camera rotation. FirstPersonCameraComponent->bUsePawnControlRotation = true;

Copy full snippet(2 lines long)

Your character’s constructor function should look like the following:

C++

```code
`// Sets default values AAdventureCharacter::AAdventureCharacter() { 	// Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;  	// Create a first person camera component. 	FirstPersonCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera")); 	check(FirstPersonCameraComponent != nullptr);`


```

Expand codeCopy full snippet(23 lines long)

### Hide Meshes

So far, your character has a first and third-person skeletal mesh that will overlap during gameplay. However, the first-person mesh should be invisible to other players and the third-person mesh should be invisible to you, the player. To handle this, add code to `BeginPlay()` to hide meshes when the game begins. 

After the global engine pointer check, call `SetOnlyOwnerSee()` on `FirstPersonMeshComponent`, passing `true` to make the first-person mesh visible only to the owning player. 

C++

`// Only the owning player sees the first person mesh FirstPersonMeshComponent->SetOnlyOwnerSee(true);`

// Only the owning player sees the first person mesh FirstPersonMeshComponent->SetOnlyOwnerSee(true);

Copy full snippet(2 lines long)

Use `SetOwnerNoSee()` to make the third-person mesh invisible to you. It remains visible to other players. 

C++

`// Hide the regular (third-person) body mesh from the owning player GetMesh()->SetOwnerNoSee(true);`

// Hide the regular (third-person) body mesh from the owning player GetMesh()->SetOwnerNoSee(true);

Copy full snippet(2 lines long)

### Offset the Camera Position

When you initialized your camera component, you attached it to the character’s Head socket. However, the camera looks more accurate when it’s positioned at the character’s eyes. To add an FVector offset that fine-tunes the camera position, call `SetRelativeLocation` on the camera component:

C++

`// Position the camera slightly above the eyes. FirstPersonCameraComponent->SetRelativeLocation(FVector(2.8f, 5.9f, 0.0f));`

// Position the camera slightly above the eyes. FirstPersonCameraComponent->SetRelativeLocation(FVector(2.8f, 5.9f, 0.0f));

Copy full snippet(2 lines long)

Offsetting the camera immediately after attaching it in the constructor may not work properly due to timing issues, so call `SetRelativeLocation` in `BeginPlay()` for best performance. 

Your `BeginPlay()` function should look like this:

C++

```code
`// Called when the game starts or when spawned void AAdventureCharacter::BeginPlay() { 	Super::BeginPlay();  	check(GEngine != nullptr);  	// Only the owning player sees the first person mesh 	FirstPersonMeshComponent->SetOnlyOwnerSee(true);`


```

Expand codeCopy full snippet(30 lines long)

Save your code and compile by clicking **Build** in Visual Studio. 

## Assign Meshes in Unreal Editor

Your camera controls are set up, but you still have one step left - use the editor to add the Skeletal Mesh assets to the variables you declared in code. 

To add a Skeletal Mesh to a Character Blueprint, follow these steps:

1.  In Unreal Editor, if it’s not open already, open your Character Blueprint.
    
2.  In the **Components** panel, ensure the root **BP\_*\[CharacterName\]*** is selected.
    
3.  In the **Details** panel, in the **Mesh** section, your character has two SkeletalMeshAsset slots instead of one because you created `FirstPersonMeshComponent` in code. Click the arrow in each property’s dropdown menu and select `SKM_Manny_Simple` for both meshes. 
    
    [![](https://dev.epicgames.com/community/api/documentation/image/33367aa6-9d42-40fe-8e7d-b3ef349c7b03?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/33367aa6-9d42-40fe-8e7d-b3ef349c7b03?resizing_type=fit)
    
    When you set the **FirstPersonMeshComponent**, your camera should move into position behind the character’s head.
    
4.  Save your Blueprint and click **Compile**.
    

If you Play your game and look down, you should see the first-person mesh on your character! The mesh rotates as you look around, and your camera matches that movement. The third-person mesh is hidden at runtime and only other players can see it. However, your character is still in a static T-pose, so next you'll use an Animation Blueprint to add animations to your character and finish bringing it to life!  

## Add Animations to Your Character

In code, you can access animation logic through instances of the **UAnimInstance** class, which is a controller that determines what animations are blended and played on a Skeletal Mesh based on state and other variables. Animation Blueprints also derive from `UAnimInstance`, and you can reference them in C++ with the `UAnimBlueprint` type. 

Building an Anim Instance class is outside the scope of this tutorial; instead, you’ll add the First Person template’s prebuild Animation Blueprint to your character. This Blueprint includes the animations and logic your character needs to play different movement and idle animations.

Animations in Unreal Engine are set on a per-mesh basis, so you’ll need separate animations for both your first and third-person meshes. Because your third-person mesh is hidden when the game begins, you only need to set animations on the first-person mesh. 

To add an animation property and Animation Blueprint to your character, follow these steps:

1.  At the top of your character's `.h` file, forward-declare the `UAnimBlueprint` class. This class represents the Animation Blueprints in your project.
    
    C++
    
    `class UAnimBlueprint; class UInputMappingContext; class UInputAction; class UInputComponent;`
    
    class UAnimBlueprint; class UInputMappingContext; class UInputAction; class UInputComponent;
    
    Copy full snippet(4 lines long)
    
2.  Then in the `public` section, declare a new `UAnimBlueprint` pointer named `FirstPersonDefaultAnim`. Give it the `UCLASS()` macro with `VisibleAnywhere` and `Category = Animation`.
    
    C++
    
    `// First Person animations UPROPERTY(VisibleAnywhere, Category = Animation) UAnimBlueprint* FirstPersonDefaultAnim;`
    
    // First Person animations UPROPERTY(VisibleAnywhere, Category = Animation) UAnimBlueprint\* FirstPersonDefaultAnim;
    
    Copy full snippet(3 lines long)
    
3.  In your character's `.cpp` file, in `BeginPlay()`, after the `FirstPersonMeshComponent->SetOnlyOwnerSee(true);` line, call `FirstPersonMeshComponent->SetAnimInstanceClass()`. Even though you haven’t defined an Anim Instance class in code, you can generate a class from the Animation Blueprint using `GeneratedClass`.
    
    C++
    
    `// Only the owning player sees the first person mesh. FirstPersonMeshComponent->SetOnlyOwnerSee(true);  // Set the animations on the first person mesh. FirstPersonMeshComponent->SetAnimInstanceClass(FirstPersonDefaultAnim->GeneratedClass);`
    
    // Only the owning player sees the first person mesh. FirstPersonMeshComponent-&gt;SetOnlyOwnerSee(true); // Set the animations on the first person mesh. FirstPersonMeshComponent-&gt;SetAnimInstanceClass(FirstPersonDefaultAnim-&gt;GeneratedClass);
    
    Copy full snippet(5 lines long)
    
4.  Save your code and compile it from Visual Studio.
    
5.  In Unreal Editor, reopen your Character Blueprint and select the root **BP\_*\[CharacterName\]*** component.
    
6.  In the **Details** panel, under **Animation**, set the **First Person Default Anim** to `ABP_Unarmed`.
    
    [![](https://dev.epicgames.com/community/api/documentation/image/4305278a-61a5-4c4f-bf2c-b92d7f222e81?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/4305278a-61a5-4c4f-bf2c-b92d7f222e81?resizing_type=fit)
    
7.  Save your Blueprint and compile it.
    

## Test Your Character

Press **Play** to test out your game. If you look down, you'll see the first-person mesh animate as you move! Try moving around and jumping to see the different animations controlled by this Blueprint.   

[![](https://dev.epicgames.com/community/api/documentation/image/8aba955b-967f-4b16-8ed1-9949cab10cae?resizing_type=fit)](https://dev.epicgames.com/community/api/documentation/image/8aba955b-967f-4b16-8ed1-9949cab10cae?resizing_type=fit)

## Next Up

In the next section, you’ll learn how to create an item for your character to pick up and use!

[

![Manage Items and Data](https://dev.epicgames.com/community/api/documentation/image/1db9f4bd-93e0-4ad8-8abf-c7be6ecec5e8?resizing_type=fit&width=640&height=640)

Manage Items and Data

Learn to use Item Data Structs, Data Assets, and Data Tables to define items and store and organize item data for scalability.





](https://dev.epicgames.com/documentation/en-us/unreal-engine/manage-item-and-data-in-an-unreal-engine-game)

## Complete Code

Here is the complete code built in this section:

C++

AdventureCharacter.h

```code
`// Copyright Epic Games, Inc. All Rights Reserved.  #pragma once  #include "CoreMinimal.h" #include "Camera/CameraComponent.h" #include "GameFramework/Character.h" #include "EnhancedInputComponent.h" #include "EnhancedInputSubsystems.h"  #include "InputActionValue.h"`

```

Expand codeCopy full snippet(73 lines long)

C++

AdventureCharacter.cpp

```code
`#include "AdventureCharacter.h"  // Sets default values AAdventureCharacter::AAdventureCharacter() { 	// Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 	PrimaryActorTick.bCanEverTick = true;  	// Create a first person camera component. 	FirstPersonCameraComponent = CreateDefaultSubobject<UCameraComponent>(TEXT("FirstPersonCamera"));`

```

Expand codeCopy full snippet(114 lines long)