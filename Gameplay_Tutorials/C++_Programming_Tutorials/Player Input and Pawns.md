# Player Input and Pawns

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-player-input-in-unreal-engine-cpp](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-player-input-in-unreal-engine-cpp)  
**Processed:** 2025-06-14 16:45:36

---

Over the course of this tutorial, you will learn to react to player input by extending the Pawn class.

## 1 - Customize a Pawn

If you are new to **Unreal Engine**, you might want to read our [Programming Quick Start](/documentation/en-us/unreal-engine/unreal-engine-cpp-quick-start) first. For this tutorial, we will assume you are familiar with creating a project, adding C++ code to it, and compiling your code.

1.  We will begin by creating a new, Basic Code project, with starter content, named HowTo\_PlayerInput. Then, we'll add a customized **Pawn** class, which we will call MyPawn, to the project.
    
    A Pawn is a type of **Actor** that is designed to be controlled by human players or AI.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6534455b-13b0-45cf-9cda-770ca78f2f75/addpawn.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e813bb93-1abf-40de-bf9b-1285fc4412bf/nameyournewpawn.png)
2.  The first thing we're going to do is set our MyPawn to respond to player input automatically upon the game starting. The Pawn class provides a variable we can set during initialization that handles this for us. In MyPawn.cpp, add the following code to **AMyPawn::AMyPawn**:
    
    ```
             `// Set this pawn to be controlled by the lowest-numbered player          AutoPossessPlayer = EAutoReceiveInput::Player0;`
    		
    Copy full snippet
    ```
    // Set this pawn to be controlled by the lowest-numbered player AutoPossessPlayer = EAutoReceiveInput::Player0;
3.  Next, we'll build a few basic **Components**. If you want to learn more about adding and managing Components in code, as well as some common types of Components you will encounter, try reading our [Components Tutorial](/documentation/en-us/unreal-engine/quick-start-guide-to-components-and-collision-in-unreal-engine-cpp). In order to keep track of the Component we will create, we should add the following code to MyPawn.h, at the bottom of our class definition:
    
    ```
             `UPROPERTY(EditAnywhere)          USceneComponent* OurVisibleComponent;`
    		
    Copy full snippet
    ```
    UPROPERTY(EditAnywhere) USceneComponent\* OurVisibleComponent;
    
    This variable is tagged as a **UPROPERTY** so that it will be visible to **Unreal Engine**. This is important because it prevents the variable from being reset when the game is launched, or when the project or level is closed and reloaded.
    
    And back in MyPawn.cpp, we should add the following code to AMyPawn::AMyPawn:
    
    ```
         `// Create a dummy root component we can attach things to.      RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent"));      // Create a camera and a visible object      UCameraComponent* OurCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("OurCamera"));      OurVisibleComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("OurVisibleComponent"));      // Attach our camera and visible object to our root component. Offset and rotate the camera.      OurCamera->SetupAttachment(RootComponent);      OurCamera->SetRelativeLocation(FVector(-250.0f, 0.0f, 250.0f));      OurCamera->SetRelativeRotation(FRotator(-45.0f, 0.0f, 0.0f));      OurVisibleComponent->SetupAttachment(RootComponent);`
    
    Copy full snippet
    ```
    // Create a dummy root component we can attach things to. RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent")); // Create a camera and a visible object UCameraComponent\* OurCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("OurCamera")); OurVisibleComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("OurVisibleComponent")); // Attach our camera and visible object to our root component. Offset and rotate the camera. OurCamera->SetupAttachment(RootComponent); OurCamera->SetRelativeLocation(FVector(-250.0f, 0.0f, 250.0f)); OurCamera->SetRelativeRotation(FRotator(-45.0f, 0.0f, 0.0f)); OurVisibleComponent->SetupAttachment(RootComponent);
4.  We are now ready to save our changes and compile with the **Build** command in **Visual Studio** or the **Compile** button in the **Unreal Editor**.
    

---

Now that we have a customized Pawn to react to our game's input, we'll need to define what that input will be. To do this, we'll configure our project's **Input Settings** in the **Unreal Editor**.

### Work-In-Progress Code

**MyPawn.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "GameFramework/Pawn.h" 	#include "MyPawn.generated.h"  	UCLASS() 	class HOWTO_PLAYERINPUT_API AMyPawn : public APawn 	{ 		GENERATED_BODY()  	public: 		// Sets default values 		AMyPawn();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		// Called to bind functionality to input 		virtual void SetupPlayerInputComponent(class UInputComponent* InputComponent) override;  		UPROPERTY(EditAnywhere) 		USceneComponent* OurVisibleComponent; 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "GameFramework/Pawn.h" #include "MyPawn.generated.h" UCLASS() class HOWTO\_PLAYERINPUT\_API AMyPawn : public APawn { GENERATED\_BODY() public: // Sets default values AMyPawn(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* InputComponent) override; UPROPERTY(EditAnywhere) USceneComponent\* OurVisibleComponent; };

**MyPawn.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "HowTo_PlayerInput.h" 	#include "MyPawn.h"  	// Sets default values 	AMyPawn::AMyPawn() 	{ 		// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		// Set this pawn to be controlled by the lowest-numbered player 		AutoPossessPlayer = EAutoReceiveInput::Player0;  		// Create a dummy root component we can attach things to. 		RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent")); 		// Create a camera and a visible object 		UCameraComponent* OurCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("OurCamera")); 		OurVisibleComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("OurVisibleComponent")); 		// Attach our camera and visible object to our root component. Offset and rotate the camera. 		OurCamera->SetupAttachment(RootComponent); 		OurCamera->SetRelativeLocation(FVector(-250.0f, 0.0f, 250.0f)); 		OurCamera->SetRelativeRotation(FRotator(-45.0f, 0.0f, 0.0f)); 		OurVisibleComponent->SetupAttachment(RootComponent); 	}  	// Called when the game starts or when spawned 	void AMyPawn::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void AMyPawn::Tick( float DeltaTime ) 	{ 		Super::Tick( DeltaTime );  	}  	// Called to bind functionality to input 	void AMyPawn::SetupPlayerInputComponent(class UInputComponent* InputComponent) 	{ 		Super::SetupPlayerInputComponent(InputComponent);  	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "HowTo\_PlayerInput.h" #include "MyPawn.h" // Sets default values AMyPawn::AMyPawn() { // Set this pawn to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Set this pawn to be controlled by the lowest-numbered player AutoPossessPlayer = EAutoReceiveInput::Player0; // Create a dummy root component we can attach things to. RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent")); // Create a camera and a visible object UCameraComponent\* OurCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("OurCamera")); OurVisibleComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("OurVisibleComponent")); // Attach our camera and visible object to our root component. Offset and rotate the camera. OurCamera->SetupAttachment(RootComponent); OurCamera->SetRelativeLocation(FVector(-250.0f, 0.0f, 250.0f)); OurCamera->SetRelativeRotation(FRotator(-45.0f, 0.0f, 0.0f)); OurVisibleComponent->SetupAttachment(RootComponent); } // Called when the game starts or when spawned void AMyPawn::BeginPlay() { Super::BeginPlay(); } // Called every frame void AMyPawn::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void AMyPawn::SetupPlayerInputComponent(class UInputComponent\* InputComponent) { Super::SetupPlayerInputComponent(InputComponent); }

## 2 - Configure Game Input

There are two types of input mappings: Action and Axis.

-   **Action Mappings** are useful to think of as "yes or no" inputs, like the buttons on a mouse or joystick. They report when they are pressed, released, double-clicked, or held down for a short time. Discrete actions like jumping, shooting, or interacting with objects are good candidates for this type of mapping.
-   **Axis Mappings** are continuous - think of them as "how much" inputs, like the stick on a joystick, or the position of a mouse cursor. They report their value every frame, even if they're not moving. Things with magnitude or direction, such as walking, looking around, and steering a vehicle are usually handled this way.

While input mappings can be defined directly in code, the usual method is to define them in the **Unreal Engine** editor, so that's how we'll do it in this tutorial.

1.  In the **Unreal Engine** editor, under the **Edit** dropdown menu, we'll click the **Project Settings** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/72835209-57fc-4750-a643-92475af4fb61/editprojectsettings.png)
2.  From there, we'll select the **Input** option from the **Engine** section on the left. We can then expand the **Bindings** category that appears on the right, and add one **Action Mapping** and two **Axis Mappings**.
    
    The plus sign next to the **Action Mapping** or **Axis Mapping** section headings will add a new mapping. The expander arrow on the left can be used to show or hide our mappings. To add an additional input to a mapping, click the plus sign next to that mapping. Following are the mappings and inputs we will need. Take note of the negative values for the S and A inputs.
    
    <table class="table" style="--columns-count: 3;"><tbody><tr><td>Action Mapping</td><td>&nbsp;</td><td>&nbsp;</td></tr><tr><td>Grow</td><td>Space Bar</td><td>&nbsp;</td></tr></tbody></table>
    
    <table class="table" style="--columns-count: 3;"><tbody><tr><td>Axis Mapping</td><td>&nbsp;</td><td>&nbsp;</td></tr><tr><td>MoveX</td><td>W</td><td>1.0</td></tr><tr><td>&nbsp;</td><td>S</td><td>-1.0</td></tr><tr><td>MoveY</td><td>A</td><td>-1.0</td></tr><tr><td>&nbsp;</td><td>D</td><td>1.0</td></tr></tbody></table>
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5079b4ba-9cc1-42ce-b0e6-d77b6c09cb45/configureinput.png)
3.  Now that our input is configured, let's set up a MyPawn in our level. The **MyPawn** class will appear in our **Content Browser**, and is ready to be dragged into the **Level Editor**.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ecde86ca-256c-490f-a845-03797b1bf47c/classincontentbrowser.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8c440231-f228-4687-a53f-1f54599d5ba2/pawninsceneview.png)
4.  One more step is needed to set up our MyPawn. We'll need to give it a **Static Mesh** so that we can see it in the game. We can do this by selecting the MyPawn we just created, selecting the component called **OurVisibleComponent (Inherited)** in the **Details Panel**, and assigning an asset to it through the dropdown box in the **Static Mesh** category. For this tutorial, **Shape\_Cylinder** is a good asset to use.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b65d8b5f-2382-41eb-b654-5824bebe5ac8/staticmesh.png)
5.  We can now save our level and return to **Visual Studio** to write code that will make the MyPawn we placed react to the inputs we defined.
    

---

We're now ready to finish coding our MyPawn class in **Visual Studio**.

## 3 - Program and Bind Game Actions

1\. In **Visual Studio**, open MyPawn.h and add the following code to the bottom of MyPawn's class definition:

//Input functions void Move\_XAxis(float AxisValue); void Move\_YAxis(float AxisValue); void StartGrowing(); void StopGrowing();

//Input variables FVector CurrentVelocity; bool bGrowing;

The four input functions are going to be bound to our input events. When they run, they will update the values stored in our new input variables, which MyPawn will use to determine what it should do during in the game.

1.  We'll switch over to MyPawn.cpp and program the four functions we just declared. Add the following code:
    
    ```
             `void AMyPawn::Move_XAxis(float AxisValue)          {              // Move at 100 units per second forward or backward              CurrentVelocity.X = FMath::Clamp(AxisValue, -1.0f, 1.0f) * 100.0f;          } 		          void AMyPawn::Move_YAxis(float AxisValue)          {              // Move at 100 units per second right or left              CurrentVelocity.Y = FMath::Clamp(AxisValue, -1.0f, 1.0f) * 100.0f;          } 		          void AMyPawn::StartGrowing()          {              bGrowing = true;          } 		          void AMyPawn::StopGrowing()          {              bGrowing = false;          }`
    Copy full snippet
    ```
    void AMyPawn::Move\_XAxis(float AxisValue) { // Move at 100 units per second forward or backward CurrentVelocity.X = FMath::Clamp(AxisValue, -1.0f, 1.0f) \* 100.0f; } void AMyPawn::Move\_YAxis(float AxisValue) { // Move at 100 units per second right or left CurrentVelocity.Y = FMath::Clamp(AxisValue, -1.0f, 1.0f) \* 100.0f; } void AMyPawn::StartGrowing() { bGrowing = true; } void AMyPawn::StopGrowing() { bGrowing = false; }
    
    We use **FMath::Clamp** to constrain the values we get from our inputs to the range of -1 to +1. Although it's not an issue in this example, if there were multiple keys that could affect an axis in the same way, the values would be added together if a player pressed those inputs at the same time. For example, if both W and Up Arrow were mapped to MoveX with scales of 1.0, pressing both would result in an AxisValue of 2.0, which would let the player move at double speed if we didn't clamp it.
    
    You may notice that the two "Move" functions take axis values as floats, while the "Grow" functions do not. This is because they will be mapped to MoveX and MoveY, which are Axis Mappings, and therefore will have a floating-point parameter. Action Mappings do not have this parameter.
    
2.  Now that we have our input functions defined, we'll need to bind them so that they will react to the appropriate inputs. Add the following code inside of **AMyPawn::SetupPlayerInputComponent**:
    
    ```
             `// Respond when our "Grow" key is pressed or released.          InputComponent->BindAction("Grow", IE_Pressed, this, &AMyPawn::StartGrowing);          InputComponent->BindAction("Grow", IE_Released, this, &AMyPawn::StopGrowing); 		          // Respond every frame to the values of our two movement axes, "MoveX" and "MoveY".          InputComponent->BindAxis("MoveX", this, &AMyPawn::Move_XAxis);          InputComponent->BindAxis("MoveY", this, &AMyPawn::Move_YAxis);`
    		
    Copy full snippet
    ```
    // Respond when our "Grow" key is pressed or released. InputComponent->BindAction("Grow", IE\_Pressed, this, &AMyPawn::StartGrowing); InputComponent->BindAction("Grow", IE\_Released, this, &AMyPawn::StopGrowing); // Respond every frame to the values of our two movement axes, "MoveX" and "MoveY". InputComponent->BindAxis("MoveX", this, &AMyPawn::Move\_XAxis); InputComponent->BindAxis("MoveY", this, &AMyPawn::Move\_YAxis);
3.  We now have variables that are updated by the inputs we configured. All we have left to do is write code to do something with them. Let's add the following code to **AMyPawn::Tick**:
    
    ```
             `// Handle growing and shrinking based on our "Grow" action          {              float CurrentScale = OurVisibleComponent->GetComponentScale().X;              if (bGrowing)              {                  // Grow to double size over the course of one second                  CurrentScale += DeltaTime;              }              else              {                  // Shrink half as fast as we grow                  CurrentScale -= (DeltaTime * 0.5f);              }              // Make sure we never drop below our starting size, or increase past double size.              CurrentScale = FMath::Clamp(CurrentScale, 1.0f, 2.0f);              OurVisibleComponent->SetWorldScale3D(FVector(CurrentScale));          } 		          // Handle movement based on our "MoveX" and "MoveY" axes          {              if (!CurrentVelocity.IsZero())              {                  FVector NewLocation = GetActorLocation() + (CurrentVelocity * DeltaTime);                  SetActorLocation(NewLocation);              }          }`
    		
    Copy full snippet
    ```
    // Handle growing and shrinking based on our "Grow" action { float CurrentScale = OurVisibleComponent->GetComponentScale().X; if (bGrowing) { // Grow to double size over the course of one second CurrentScale += DeltaTime; } else { // Shrink half as fast as we grow CurrentScale -= (DeltaTime \* 0.5f); } // Make sure we never drop below our starting size, or increase past double size. CurrentScale = FMath::Clamp(CurrentScale, 1.0f, 2.0f); OurVisibleComponent->SetWorldScale3D(FVector(CurrentScale)); } // Handle movement based on our "MoveX" and "MoveY" axes { if (!CurrentVelocity.IsZero()) { FVector NewLocation = GetActorLocation() + (CurrentVelocity \* DeltaTime); SetActorLocation(NewLocation); } }
4.  After compiling our code, we can return to the **Unreal Editor** and press **Play**. We should have control of our **Pawn** with the WASD keys, and we should be able to make it grow by holding **Space Bar**, and watch it shrink when we let go.
    

![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/917ef060-1cb3-47f8-920a-b573e17c46aa/playinggame1.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e74fb26b-9470-4542-a78a-a57dd957eb61/playinggame2.png)

### Finished Code

**MyPawn.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "GameFramework/Pawn.h" 	#include "MyPawn.generated.h"  	UCLASS() 	class HOWTO_PLAYERINPUT_API AMyPawn : public APawn 	{ 		GENERATED_BODY()  	public: 		// Sets default values 		AMyPawn();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick(float DeltaSeconds) override;  		// Called to bind functionality to input 		virtual void SetupPlayerInputComponent(class UInputComponent* InputComponent) override;  		UPROPERTY(EditAnywhere) 		USceneComponent* OurVisibleComponent;  		// Input functions 		void Move_XAxis(float AxisValue); 		void Move_YAxis(float AxisValue); 		void StartGrowing(); 		void StopGrowing();  		// Input variables 		FVector CurrentVelocity; 		bool bGrowing; 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "GameFramework/Pawn.h" #include "MyPawn.generated.h" UCLASS() class HOWTO\_PLAYERINPUT\_API AMyPawn : public APawn { GENERATED\_BODY() public: // Sets default values AMyPawn(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick(float DeltaSeconds) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* InputComponent) override; UPROPERTY(EditAnywhere) USceneComponent\* OurVisibleComponent; // Input functions void Move\_XAxis(float AxisValue); void Move\_YAxis(float AxisValue); void StartGrowing(); void StopGrowing(); // Input variables FVector CurrentVelocity; bool bGrowing; };

**MyPawn.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "HowTo_PlayerInput.h" 	#include "MyPawn.h"  	// Sets default values 	AMyPawn::AMyPawn() 	{ 		// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		// Set this pawn to be controlled by the lowest-numbered player 		AutoPossessPlayer = EAutoReceiveInput::Player0;  		// Create a dummy root component we can attach things to. 		RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent")); 		// Create a camera and a visible object 		UCameraComponent* OurCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("OurCamera")); 		OurVisibleComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("OurVisibleComponent")); 		// Attach our camera and visible object to our root component. Offset and rotate the camera. 		OurCamera->SetupAttachment(RootComponent); 		OurCamera->SetRelativeLocation(FVector(-250.0f, 0.0f, 250.0f)); 		OurCamera->SetRelativeRotation(FRotator(-45.0f, 0.0f, 0.0f)); 		OurVisibleComponent->SetupAttachment(RootComponent); 	}  	// Called when the game starts or when spawned 	void AMyPawn::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void AMyPawn::Tick(float DeltaTime) 	{ 		Super::Tick(DeltaTime);  		// Handle growing and shrinking based on our "Grow" action 		{ 			float CurrentScale = OurVisibleComponent->GetComponentScale().X; 			if (bGrowing) 			{ 				// Grow to double size over the course of one second 				CurrentScale += DeltaTime; 			} 			else 			{ 				// Shrink half as fast as we grow 				CurrentScale -= (DeltaTime * 0.5f); 			} 			// Make sure we never drop below our starting size, or increase past double size. 			CurrentScale = FMath::Clamp(CurrentScale, 1.0f, 2.0f); 			OurVisibleComponent->SetWorldScale3D(FVector(CurrentScale)); 		}  		// Handle movement based on our "MoveX" and "MoveY" axes 		{ 			if (!CurrentVelocity.IsZero()) 			{ 				FVector NewLocation = GetActorLocation() + (CurrentVelocity * DeltaTime); 				SetActorLocation(NewLocation); 			} 		} 	}  	// Called to bind functionality to input 	void AMyPawn::SetupPlayerInputComponent(class UInputComponent* InputComponent) 	{ 		Super::SetupPlayerInputComponent(InputComponent);  		// Respond when our "Grow" key is pressed or released. 		InputComponent->BindAction("Grow", IE_Pressed, this, &AMyPawn::StartGrowing); 		InputComponent->BindAction("Grow", IE_Released, this, &AMyPawn::StopGrowing);  		// Respond every frame to the values of our two movement axes, "MoveX" and "MoveY". 		InputComponent->BindAxis("MoveX", this, &AMyPawn::Move_XAxis); 		InputComponent->BindAxis("MoveY", this, &AMyPawn::Move_YAxis); 	}  	void AMyPawn::Move_XAxis(float AxisValue) 	{ 		// Move at 100 units per second forward or backward 		CurrentVelocity.X = FMath::Clamp(AxisValue, -1.0f, 1.0f) * 100.0f; 	}  	void AMyPawn::Move_YAxis(float AxisValue) 	{ 		// Move at 100 units per second right or left 		CurrentVelocity.Y = FMath::Clamp(AxisValue, -1.0f, 1.0f) * 100.0f; 	}  	void AMyPawn::StartGrowing() 	{ 		bGrowing = true; 	}  	void AMyPawn::StopGrowing() 	{ 		bGrowing = false; 	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "HowTo\_PlayerInput.h" #include "MyPawn.h" // Sets default values AMyPawn::AMyPawn() { // Set this pawn to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Set this pawn to be controlled by the lowest-numbered player AutoPossessPlayer = EAutoReceiveInput::Player0; // Create a dummy root component we can attach things to. RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent")); // Create a camera and a visible object UCameraComponent\* OurCamera = CreateDefaultSubobject<UCameraComponent>(TEXT("OurCamera")); OurVisibleComponent = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("OurVisibleComponent")); // Attach our camera and visible object to our root component. Offset and rotate the camera. OurCamera->SetupAttachment(RootComponent); OurCamera->SetRelativeLocation(FVector(-250.0f, 0.0f, 250.0f)); OurCamera->SetRelativeRotation(FRotator(-45.0f, 0.0f, 0.0f)); OurVisibleComponent->SetupAttachment(RootComponent); } // Called when the game starts or when spawned void AMyPawn::BeginPlay() { Super::BeginPlay(); } // Called every frame void AMyPawn::Tick(float DeltaTime) { Super::Tick(DeltaTime); // Handle growing and shrinking based on our "Grow" action { float CurrentScale = OurVisibleComponent->GetComponentScale().X; if (bGrowing) { // Grow to double size over the course of one second CurrentScale += DeltaTime; } else { // Shrink half as fast as we grow CurrentScale -= (DeltaTime \* 0.5f); } // Make sure we never drop below our starting size, or increase past double size. CurrentScale = FMath::Clamp(CurrentScale, 1.0f, 2.0f); OurVisibleComponent->SetWorldScale3D(FVector(CurrentScale)); } // Handle movement based on our "MoveX" and "MoveY" axes { if (!CurrentVelocity.IsZero()) { FVector NewLocation = GetActorLocation() + (CurrentVelocity \* DeltaTime); SetActorLocation(NewLocation); } } } // Called to bind functionality to input void AMyPawn::SetupPlayerInputComponent(class UInputComponent\* InputComponent) { Super::SetupPlayerInputComponent(InputComponent); // Respond when our "Grow" key is pressed or released. InputComponent->BindAction("Grow", IE\_Pressed, this, &AMyPawn::StartGrowing); InputComponent->BindAction("Grow", IE\_Released, this, &AMyPawn::StopGrowing); // Respond every frame to the values of our two movement axes, "MoveX" and "MoveY". InputComponent->BindAxis("MoveX", this, &AMyPawn::Move\_XAxis); InputComponent->BindAxis("MoveY", this, &AMyPawn::Move\_YAxis); } void AMyPawn::Move\_XAxis(float AxisValue) { // Move at 100 units per second forward or backward CurrentVelocity.X = FMath::Clamp(AxisValue, -1.0f, 1.0f) \* 100.0f; } void AMyPawn::Move\_YAxis(float AxisValue) { // Move at 100 units per second right or left CurrentVelocity.Y = FMath::Clamp(AxisValue, -1.0f, 1.0f) \* 100.0f; } void AMyPawn::StartGrowing() { bGrowing = true; } void AMyPawn::StopGrowing() { bGrowing = false; }

## 4 - On Your Own!

Using what you have learned, try to do the following:

-   Implement directional controls that increase speed after being held for a certain period of time.
-   Create a special input sequence that instantly expands the object to full scale when the user presses an **Action Mapping** immediately after starting to press an **Axis Mapping**.

As for the specifics covered in this tutorial:

-   For more information about **Input**, try the [%making-interactive-experiences/Input:title%](/documentation/en-us/unreal-engine/input-in-unreal-engine) page.
-   For further tutorials, see the [%programming-and-scripting/programming-language-implementation/cpp-in-unreal-engine/tutorials:title%](/documentation/en-us/unreal-engine/unreal-engine-cpp-programming-tutorials) page.