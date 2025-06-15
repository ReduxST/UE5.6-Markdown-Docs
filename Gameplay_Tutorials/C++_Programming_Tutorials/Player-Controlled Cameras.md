# Player-Controlled Cameras

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-player-controlled-cameras-in-unreal-engine-cpp](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-player-controlled-cameras-in-unreal-engine-cpp)  
**Processed:** 2025-06-14 16:45:34

---

Attaching a spring arm and a camera to a Pawn provides the capability to adjust how our camera follows a Pawn in the world.

## 1\. Attach a Camera to a Pawn

1.  Begin by launching **Unreal Engine** and creating a new blank Template.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/43df973a-defa-423a-9c9c-c45ea572557f/templateselect.png)
2.  Select a new Games Project. In the Project Settings window, we will change the default code from Blueprint to C++, with starter content enabled. Choose the directory where you want your unreal project to save in, then name your project HowTo\_PlayerCamera and click Create Project.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d0419760-7d9b-4711-ad61-755a409c6a58/projectsettings.png)
3.  From the sources panel, navigate to your C++ Classes folder. You should notice a single class containing your Game mode base class. Right click on the adjacent gray space, and from the drop down window, select **New C++ class**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e9eb8c0a-fbf4-4a96-a8d4-a5a3b7b60abb/newclass.png)
4.  Select Pawn as your Parent Class and click Next. Name your new Pawn PawnWithCamera.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/42b52f27-df95-4ee4-bd74-1e6055b5698f/namepawn.png)
5.  in Visual Studio, Navigate to the `PawnWithCamera.h` file and add the following code to the protected namespace of your class definition:
    
    ```
             `protected:              UPROPERTY(EditAnywhere)              class USpringArmComponent* SpringArmComp; 		              UPROPERTY(EditAnywhere)              class UCameraComponent* CameraComp; 		              UPROPERTY(EditAnywhere)              UStaticMeshComponent* StaticMeshComp;`
    Copy full snippet
    ```
    protected: UPROPERTY(EditAnywhere) class USpringArmComponent\* SpringArmComp; UPROPERTY(EditAnywhere) class UCameraComponent\* CameraComp; UPROPERTY(EditAnywhere) UStaticMeshComponent\* StaticMeshComp;

These variables are used to create a **SpringArmComponent** with a **CameraComponent** attached to the end. Spring arms provide a simple way to attach cameras (or other Components) so that its motion is smooth and fluid as they move with the object they observe.

1.  Navigate to `PawnWithCamera.cpp` and declare the following includes:
    
    ```
             `#include "GameFramework/SpringArmComponent.h"          #include "Camera/Component.h"`
    		
    Copy full snippet
    ```
    #include "GameFramework/SpringArmComponent.h" #include "Camera/Component.h"
2.  Now, you will need to create your static mesh, spring arm and camera components. Declare the following code to PawnWithCamera.cpp from inside the class constructor **APawnWithCamera::APawnWithCamera:** Add the following code:
    
    ```
             `//Create our components          RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootSceneComponent"));          StaticMeshComp = CreateDefaultSubobject <UStaticMeshComponent>(TEXT("StaticMeshComponent"));          SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArmComponent"));          CameraComp = CreateDefaultSubobject<UCameraComponent>(TEXT("CameraComponent")); 		          //Attach our components          StaticMeshComp->SetupAttachment(RootComponent);          SpringArmComp->SetupAttachment(StaticMeshComp);          CameraComp->SetupAttachment(SpringArmComp,USpringArmComponent::SocketName); 		          //Assign SpringArm class variables.          SpringArmComp->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, 50.0f), FRotator(-60.0f, 0.0f, 0.0f));          SpringArmComp->TargetArmLength = 400.f;          SpringArmComp->bEnableCameraLag = true;          SpringArmComp->CameraLagSpeed = 3.0f;`
    Copy full snippet
    ```
    //Create our components RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootSceneComponent")); StaticMeshComp = CreateDefaultSubobject <UStaticMeshComponent>(TEXT("StaticMeshComponent")); SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArmComponent")); CameraComp = CreateDefaultSubobject<UCameraComponent>(TEXT("CameraComponent")); //Attach our components StaticMeshComp->SetupAttachment(RootComponent); SpringArmComp->SetupAttachment(StaticMeshComp); CameraComp->SetupAttachment(SpringArmComp,USpringArmComponent::SocketName); //Assign SpringArm class variables. SpringArmComp->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, 50.0f), FRotator(-60.0f, 0.0f, 0.0f)); SpringArmComp->TargetArmLength = 400.f; SpringArmComp->bEnableCameraLag = true; SpringArmComp->CameraLagSpeed = 3.0f;

This creates a SceneComponent as the root of our Component List Hierarchy, then creates and attaches a StaticMeshComponent to it. Afterwards, both a SpringArmComponent and a Camera Component is created and the Camera Component is attached to the end of the Spring ArmComponent's socket length. The Spring Arm is set to a default pitch of -60 degrees and a position of 50 units above the root. We also establish a few values specific to the SpringArmComponent class that will determine its length and the smoothness of its motion.

1.  Finally, we will set the default Player Controller to possess our Pawn from the constructor.
    
    ```
             `//Take control of the default Player          AutoPossessPlayer = EAutoReceiveInput::Player0;`
    		
    Copy full snippet
    ```
    //Take control of the default Player AutoPossessPlayer = EAutoReceiveInput::Player0;

We now have a simple Pawn that will allow us to control our camera comfortably. Next, we'll configure our input in the **Unreal Engine** editor and create code that reacts to it.

## Work-In-Progress Code

**PawnWithCamera.h**

```
	`// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Pawn.h" 	#include "PawnWithCamera.generated.h"  	UCLASS() 	class HOWTO_PLAYERCAMERA_API APawnWithCamera : public APawn 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this pawn's properties 		APawnWithCamera();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		// Called to bind functionality to input 		virtual void SetupPlayerInputComponent(class UInputComponent* InputComponent) override;  	protected: 		UPROPERTY(EditAnywhere) 		class USpringArmComponent* SpringArmComp;  		UPROPERTY(EditAnywhere) 		class UCameraComponent* CameraComp;  	    UPROPERTY(EditAnywhere) 		UStaticMeshComponent* StaticMeshComp;  	};`

Copy full snippet
```
// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Pawn.h" #include "PawnWithCamera.generated.h" UCLASS() class HOWTO\_PLAYERCAMERA\_API APawnWithCamera : public APawn { GENERATED\_BODY() public: // Sets default values for this pawn's properties APawnWithCamera(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* InputComponent) override; protected: UPROPERTY(EditAnywhere) class USpringArmComponent\* SpringArmComp; UPROPERTY(EditAnywhere) class UCameraComponent\* CameraComp; UPROPERTY(EditAnywhere) UStaticMeshComponent\* StaticMeshComp; };

**PawnWithCamera.cpp**

```
	`// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved.  	#include "HowTo_PlayerCamera.h" 	#include "PawnWithCamera.h" 	#include "GameFramework/SpringArmComponent.h" 	#include "Camera/CameraComponent.h"  	// Sets default values 	APawnWithCamera::APawnWithCamera() 	{ 		// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		//Create our components 		RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootSceneComponent")); 		StaticMeshComp = CreateDefaultSubobject <UStaticMeshComponent>(TEXT("StaticMeshComponent")); 		SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArmComponent")); 		CameraComp = CreateDefaultSubobject<UCameraComponent>(TEXT("CameraComponent"));  		//Attach our components 		StaticMeshComp->SetupAttachment(RootComponent); 		SpringArmComp->SetupAttachment(StaticMeshComp); 		CameraComp->SetupAttachment(SpringArmComp,USpringArmComponent::SocketName);  		//Assign SpringArm class variables. 		SpringArmComp->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, 50.0f), FRotator(-60.0f, 0.0f, 0.0f)); 		SpringArmComp->TargetArmLength = 400.f; 		SpringArmComp->bEnableCameraLag = true; 		SpringArmComp->CameraLagSpeed = 3.0f;  		//Take control of the default Player 		AutoPossessPlayer = EAutoReceiveInput::Player0; 	}  	// Called when the game starts or when spawned 	void APawnWithCamera::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void APawnWithCamera::Tick( float DeltaTime ) 	{ 		Super::Tick( DeltaTime );  	}  	// Called to bind functionality to input 	void APawnWithCamera::SetupPlayerInputComponent(class UInputComponent* InputComponent) 	{ 		Super::SetupPlayerInputComponent(InputComponent);  	}`

Copy full snippet
```
// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved. #include "HowTo\_PlayerCamera.h" #include "PawnWithCamera.h" #include "GameFramework/SpringArmComponent.h" #include "Camera/CameraComponent.h" // Sets default values APawnWithCamera::APawnWithCamera() { // Set this pawn to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; //Create our components RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootSceneComponent")); StaticMeshComp = CreateDefaultSubobject <UStaticMeshComponent>(TEXT("StaticMeshComponent")); SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArmComponent")); CameraComp = CreateDefaultSubobject<UCameraComponent>(TEXT("CameraComponent")); //Attach our components StaticMeshComp->SetupAttachment(RootComponent); SpringArmComp->SetupAttachment(StaticMeshComp); CameraComp->SetupAttachment(SpringArmComp,USpringArmComponent::SocketName); //Assign SpringArm class variables. SpringArmComp->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, 50.0f), FRotator(-60.0f, 0.0f, 0.0f)); SpringArmComp->TargetArmLength = 400.f; SpringArmComp->bEnableCameraLag = true; SpringArmComp->CameraLagSpeed = 3.0f; //Take control of the default Player AutoPossessPlayer = EAutoReceiveInput::Player0; } // Called when the game starts or when spawned void APawnWithCamera::BeginPlay() { Super::BeginPlay(); } // Called every frame void APawnWithCamera::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void APawnWithCamera::SetupPlayerInputComponent(class UInputComponent\* InputComponent) { Super::SetupPlayerInputComponent(InputComponent); }

## 2\. Configure Input to Control the Camera

You will need to decide the input keys that control your camera and pawn, then set up the inputs accordingly. For this project sample, let us allow our follow distance to shorten and field of view to zoom in when the right mouse button is held down.

1.  Let's also control our viewing angle with the mouse, and our **Pawn**'s movement with the WASD keys. To do this, we'll open the **Project Settings** from the Edit dropdown menu in the **Unreal Engine** editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/c4bc876c-a009-4cab-b8a1-f749c5a08dae/editprojectsettings.png)
2.  From the Project Settings window, navigate to **Engine>Input>Bindings**. From here, click the **+** signs next to Action and Axis mappings to add a new key map.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/452a6bc7-0e1a-4c70-b0b5-80b25c816e2c/inputnavigation.png)
3.  You will want to define the following input **Action Mapping** and **Axis Mapping**, which will be used to control our input logic.
    
    <table class="table" style="--columns-count: 3;"><tbody><tr><td><strong>Action Mapping:</strong></td><td>&nbsp;</td><td>&nbsp;</td></tr><tr><td>ZoomIn</td><td>Right Mouse Button</td><td>&nbsp;</td></tr></tbody></table>
    
    <table class="table" style="--columns-count: 3;"><tbody><tr><td><strong>Axis Mapping:</strong></td><td>&nbsp;</td><td>&nbsp;</td></tr><tr><td>MoveForward</td><td>W</td><td>1.0</td></tr><tr><td>&nbsp;</td><td>S</td><td>-1.0</td></tr><tr><td>MoveRight</td><td>A</td><td>-1.0</td></tr><tr><td>&nbsp;</td><td>D</td><td>1.0</td></tr><tr><td>CameraPitch</td><td>MouseY</td><td>1.0</td></tr><tr><td>CameraYaw</td><td>MouseX</td><td>1.0</td></tr></tbody></table>
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5adde8df-a697-46b1-a02b-50a6f91040fe/inputconfig.png)
    
    If you would like to understand more about how input mappings work, you may want to consult the [Player Input and Pawns](/documentation/en-us/unreal-engine/quick-start-guide-to-player-input-in-unreal-engine-cpp) tutorial.
    

Now that you've defined your inputs, return to **Visual Studio** to proceed onward to the next steps.

## 3\. Write C++ Code to React to Input

You will write the code necessary to utilize your input mappings by setting up member variables to store the input data you will receive. During the Event Tick Update, you will need to know the values of your movement and mouse-looking axes, each of which are two-dimensional vectors.

You will also want to know whether you should be moving toward a zoomed-in or zoomed-out camera view, and how far between those two states your camera currently is.

1.  Begin by adding the following code to your protected namespace in the class definition of PawnWithCamera.h:
    
    ```
             `//Input variables          FVector2D MovementInput;          FVector2D CameraInput;          float ZoomFactor;          bool bZoomingIn;`
    		
    Copy full snippet
    ```
    //Input variables FVector2D MovementInput; FVector2D CameraInput; float ZoomFactor; bool bZoomingIn;
2.  You will need to create functions to track your input, begin by adding the following to your class definition in PawnWithCamera.h:
    
    ```
             `//Input functions          void MoveForward(float AxisValue);          void MoveRight(float AxisValue);          void PitchCamera(float AxisValue);          void YawCamera(float AxisValue);          void ZoomIn();          void ZoomOut();`
    		
    Copy full snippet
    ```
    //Input functions void MoveForward(float AxisValue); void MoveRight(float AxisValue); void PitchCamera(float AxisValue); void YawCamera(float AxisValue); void ZoomIn(); void ZoomOut();
3.  Now you will want to navigate to your PawnWithCamera.Cpp file, where you will begin to implement your function logic by adding the following code:
    
    ```
             `//Input functions          void APawnWithCamera::MoveForward(float AxisValue)          {              MovementInput.X = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f);          } 		          void APawnWithCamera::MoveRight(float AxisValue)          {              MovementInput.Y = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f);          } 		          void APawnWithCamera::PitchCamera(float AxisValue)          {              CameraInput.Y = AxisValue;          } 		          void APawnWithCamera::YawCamera(float AxisValue)          {              CameraInput.X = AxisValue;          } 		          void APawnWithCamera::ZoomIn()          {              bZoomingIn = true;          } 		          void APawnWithCamera::ZoomOut()          {              bZoomingIn = false;          }`
    		
    Copy full snippet
    ```
    //Input functions void APawnWithCamera::MoveForward(float AxisValue) { MovementInput.X = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f); } void APawnWithCamera::MoveRight(float AxisValue) { MovementInput.Y = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f); } void APawnWithCamera::PitchCamera(float AxisValue) { CameraInput.Y = AxisValue; } void APawnWithCamera::YawCamera(float AxisValue) { CameraInput.X = AxisValue; } void APawnWithCamera::ZoomIn() { bZoomingIn = true; } void APawnWithCamera::ZoomOut() { bZoomingIn = false; }
    
    We haven't done anything with ZoomFactor yet. That variable will be updated during our **Pawn**'s **Tick** function, since its value changes constantly over time based to the state of a button.
    
4.  Now that you have created the code necessary to store your input data, the next step is to tell the engine when to call your code. Binding functions to input events for Pawns can be accomplished by adding code to **APawnWithCamera::SetupPlayerInputComponent** method, as follows:
    
    ```
           `//Hook up events for "ZoomIn"        InputComponent->BindAction("ZoomIn", IE_Pressed, this, &APawnWithCamera::ZoomIn);        InputComponent->BindAction("ZoomIn", IE_Released, this, &APawnWithCamera::ZoomOut); 		        //Hook up every-frame handling for our four axes        InputComponent->BindAxis("MoveForward", this, &APawnWithCamera::MoveForward);        InputComponent->BindAxis("MoveRight", this, &APawnWithCamera::MoveRight);        InputComponent->BindAxis("CameraPitch", this, &APawnWithCamera::PitchCamera);        InputComponent->BindAxis("CameraYaw", this, &APawnWithCamera::YawCamera);`
    		
    Copy full snippet
    ```
    //Hook up events for "ZoomIn" InputComponent->BindAction("ZoomIn", IE\_Pressed, this, &APawnWithCamera::ZoomIn); InputComponent->BindAction("ZoomIn", IE\_Released, this, &APawnWithCamera::ZoomOut); //Hook up every-frame handling for our four axes InputComponent->BindAxis("MoveForward", this, &APawnWithCamera::MoveForward); InputComponent->BindAxis("MoveRight", this, &APawnWithCamera::MoveRight); InputComponent->BindAxis("CameraPitch", this, &APawnWithCamera::PitchCamera); InputComponent->BindAxis("CameraYaw", this, &APawnWithCamera::YawCamera);
5.  Finally, you can use those values in your Tick function to update your Pawn and **Camera** each frame. The following code blocks should all be added to **APawnWithCamera::Tick** in PawnWithCamera.cpp:
    
    ```
             `//Zoom in if ZoomIn button is down, zoom back out if it's not          {              if (bZoomingIn)              {                  ZoomFactor += DeltaTime / 0.5f;			//Zoom in over half a second              }              else              {                  ZoomFactor -= DeltaTime / 0.25f;		//Zoom out over a quarter of a second              }              ZoomFactor = FMath::Clamp<float>(ZoomFactor, 0.0f, 1.0f); 		              //Blend our camera's FOV and our SpringArm's length based on ZoomFactor              CameraComp->FieldOfView = FMath::Lerp<float>(90.0f, 60.0f, ZoomFactor);              SpringArmComp->TargetArmLength = FMath::Lerp<float>(400.0f, 300.0f, ZoomFactor);          }`
    Copy full snippet
    ```
    //Zoom in if ZoomIn button is down, zoom back out if it's not { if (bZoomingIn) { ZoomFactor += DeltaTime / 0.5f; //Zoom in over half a second } else { ZoomFactor -= DeltaTime / 0.25f; //Zoom out over a quarter of a second } ZoomFactor = FMath::Clamp<float>(ZoomFactor, 0.0f, 1.0f); //Blend our camera's FOV and our SpringArm's length based on ZoomFactor CameraComp->FieldOfView = FMath::Lerp<float>(90.0f, 60.0f, ZoomFactor); SpringArmComp->TargetArmLength = FMath::Lerp<float>(400.0f, 300.0f, ZoomFactor); }
    
    This code uses several hard-coded values, like the half-second and quarter-second zoom times, the 90-degree zoomed-out and 60-degree zoomed-in field of view values, and the 400 zoomed-out and 300 zoomed-in camera distances. Values like this should generally be exposed to the editor as variables tagged with **UPROPERTY(EditAnywhere)** In our example, we used the UPROPERTY(EditAnywhere) specifier tag, which provides additional functionality to non-programmers who can change their values. This also enables programmers to change them without recompiling code, or dynamically while playing the game in the editor.
    
    ```
         `//Rotate our actor's yaw, which will turn our camera because we're attached to it      {          FRotator NewRotation = GetActorRotation();          NewRotation.Yaw += CameraInput.X;          SetActorRotation(NewRotation);      }       //Rotate our camera's pitch, but limit it so we're always looking downward      {          FRotator NewRotation = OurCameraSpringArm->GetComponentRotation();          NewRotation.Pitch = FMath::Clamp(NewRotation.Pitch + CameraInput.Y, -80.0f, -15.0f);          SpringArmComp->SetWorldRotation(NewRotation);      }`
    Copy full snippet
    ```
    //Rotate our actor's yaw, which will turn our camera because we're attached to it { FRotator NewRotation = GetActorRotation(); NewRotation.Yaw += CameraInput.X; SetActorRotation(NewRotation); } //Rotate our camera's pitch, but limit it so we're always looking downward { FRotator NewRotation = OurCameraSpringArm->GetComponentRotation(); NewRotation.Pitch = FMath::Clamp(NewRotation.Pitch + CameraInput.Y, -80.0f, -15.0f); SpringArmComp->SetWorldRotation(NewRotation); }
    
    This block of code rotates our Pawn's yaw directly with the mouse's X axis, but only the camera system responds to the pitch changes from the mouse's Y axis. Rotating any **Actor** or Actor subclass actually rotates the root-level **Component**, which indirectly affects everything attached to it.
    
    ```
         `//Handle movement based on our "MoveX" and "MoveY" axes      {          if (!MovementInput.IsZero())          {              //Scale our movement input axis values by 100 units per second              MovementInput = MovementInput.SafeNormal() * 100.0f;              FVector NewLocation = GetActorLocation();              NewLocation += GetActorForwardVector() * MovementInput.X * DeltaTime;              NewLocation += GetActorRightVector() * MovementInput.Y * DeltaTime;              SetActorLocation(NewLocation);          }      }`
    Copy full snippet
    ```
    //Handle movement based on our "MoveX" and "MoveY" axes { if (!MovementInput.IsZero()) { //Scale our movement input axis values by 100 units per second MovementInput = MovementInput.SafeNormal() \* 100.0f; FVector NewLocation = GetActorLocation(); NewLocation += GetActorForwardVector() \* MovementInput.X \* DeltaTime; NewLocation += GetActorRightVector() \* MovementInput.Y \* DeltaTime; SetActorLocation(NewLocation); } }
    
    Using **GetActorForwardVector** and **GetActorRightVector** allows us to move relative to the direction the actor is facing. Since the camera faces the same way as the actor, this ensures that our forward key is always forward relative to what the player sees.
    
6.  Congratulations! We have finished coding. You can now compile your code and drag an instance of your new class from the **Content Browser** into the **Level Editor** window inside the **Unreal Engine** editor.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/de98f67b-420d-4bc5-83c3-f7f3fa8143a9/classincontentbrowser.png)
    
    Feel free to add a **Static Mesh** or other visual Component, or play without one. You should feel a smooth acceleration and deceleration to your camera's movement as it follows you around the level, but your rotation should feel tight and instantaneous. Try changing some of the properties on the **SpringArmComponent** to see how they affect the feel of your controls, such as adding "Camera Rotation Lag" or increasing or decreasing Camera Lag.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/fe8f98d8-5a10-42e3-8b4b-2f4c8d107103/springarmvalues.png)
7.  The Completed functionality of the code provided should look as it does below:
    
    **Camera Pitch/Yaw**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca184685-2bd1-4055-aded-7864117a2b03/camera.gif)
    
    **Move Forward/Right**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5e8e72c2-fa9e-4942-9a2b-0f7eadfb8fa0/move.gif)
    
    **Zoom In/Out**
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/34f99132-7400-4386-808c-864d0b3fbf8a/zoom.gif)

## Finished Code

**PawnWithCamera.h**

```
	`// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Pawn.h" 	#include "PawnWithCamera.generated.h"  	UCLASS() 	class HOWTO_PLAYERCAMERA_API APawnWithCamera : public APawn 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this pawn's properties 		APawnWithCamera();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		// Called to bind functionality to input 		virtual void SetupPlayerInputComponent(class UInputComponent* InputComponent) override;  	protected:  		UPROPERTY(EditAnywhere) 		class USpringArmComponent* OurCameraSpringArm;  		UPROPERTY(EditAnywhere) 		class UCameraComponent* OurCamera;  		UPROPERTY(EditAnywhere) 		UStaticMeshComponent* StaticMeshComp;  		//Input variables 		FVector2D MovementInput; 		FVector2D CameraInput; 		float ZoomFactor; 		bool bZoomingIn;  		//Input functions 		void MoveForward(float AxisValue); 		void MoveRight(float AxisValue); 		void PitchCamera(float AxisValue); 		void YawCamera(float AxisValue); 		void ZoomIn(); 		void ZoomOut(); 	};`

Copy full snippet
```
// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Pawn.h" #include "PawnWithCamera.generated.h" UCLASS() class HOWTO\_PLAYERCAMERA\_API APawnWithCamera : public APawn { GENERATED\_BODY() public: // Sets default values for this pawn's properties APawnWithCamera(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* InputComponent) override; protected: UPROPERTY(EditAnywhere) class USpringArmComponent\* OurCameraSpringArm; UPROPERTY(EditAnywhere) class UCameraComponent\* OurCamera; UPROPERTY(EditAnywhere) UStaticMeshComponent\* StaticMeshComp; //Input variables FVector2D MovementInput; FVector2D CameraInput; float ZoomFactor; bool bZoomingIn; //Input functions void MoveForward(float AxisValue); void MoveRight(float AxisValue); void PitchCamera(float AxisValue); void YawCamera(float AxisValue); void ZoomIn(); void ZoomOut(); };

**PawnWithCamera.cpp**

```
	`// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved.  	#include "PawnWithCamera.h" 	#include "GameFramework/SpringArmComponent.h" 	#include "Camera/CameraComponent.h"  	// Sets default values 	APawnWithCamera::APawnWithCamera() 	{ 		// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		//Create our components 		RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent")); 		StaticMeshComp = CreateDefaultSubobject <UStaticMeshComponent>(TEXT("StaticMeshComponent")); 		SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArmComponent")); 		CameraComp = CreateDefaultSubobject<UCameraComponent>(TEXT("CameraComponent"));  		StaticMeshComp->SetupAttachment(RootComponent); 		SpringArmComp->SetupAttachment(StaticMeshComp); 		CameraComp->SetupAttachment(SpringArmComp,USpringArmComponent::SocketName);  		//Setting Default Variables and Behavior of the SpringArmComponent 		SpringArmComp->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, 50.0f), FRotator(-60.0f, 0.0f, 0.0f)); 		SpringArmComp->TargetArmLength = 400.f; 		SpringArmComp->bEnableCameraLag = true; 		SpringArmComp->CameraLagSpeed = 3.0f;  		//Take control of the default Player 		AutoPossessPlayer = EAutoReceiveInput::Player0; 	}  	// Called when the game starts or when spawned 	void APawnWithCamera::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void APawnWithCamera::Tick( float DeltaTime ) 	{ 		Super::Tick(DeltaTime);  		//Zoom in if ZoomIn button is down, zoom back out if it's not 		{ 			if (bZoomingIn) 			{ 				ZoomFactor += DeltaTime / 0.5f;			//Zoom in over half a second 			} 			else 			{ 				ZoomFactor -= DeltaTime / 0.25f;		//Zoom out over a quarter of a second 			} 			ZoomFactor = FMath::Clamp<float>(ZoomFactor, 0.0f, 1.0f); 			//Blend our camera's FOV and our SpringArm's length based on ZoomFactor 			CameraComp->FieldOfView = FMath::Lerp<float>(90.0f, 60.0f, ZoomFactor); 			SpringArmComp->TargetArmLength = FMath::Lerp<float>(400.0f, 300.0f, ZoomFactor); 		}  		//Rotate our actor's yaw, which will turn our camera because we're attached to it 		{ 			FRotator NewRotation = GetActorRotation(); 			NewRotation.Yaw += CameraInput.X; 			SetActorRotation(NewRotation); 		}  		//Rotate our camera's pitch, but limit it so we're always looking downward 		{ 			FRotator NewRotation = SpringArmComp->GetComponentRotation(); 			NewRotation.Pitch = FMath::Clamp(NewRotation.Pitch + CameraInput.Y, -80.0f, -15.0f); 			SpringArmComp->SetWorldRotation(NewRotation); 		}  		//Handle movement based on our "MoveX" and "MoveY" axes 		{ 			if (!MovementInput.IsZero()) 			{ 				//Scale our movement input axis values by 100 units per second 				MovementInput = MovementInput.SafeNormal() * 100.0f; 				FVector NewLocation = GetActorLocation(); 				NewLocation += GetActorForwardVector() * MovementInput.X * DeltaTime; 				NewLocation += GetActorRightVector() * MovementInput.Y * DeltaTime; 				SetActorLocation(NewLocation); 			} 		} 	}  	// Called to bind functionality to input 	void APawnWithCamera::SetupPlayerInputComponent(class UInputComponent* InputComponent) 	{ 		Super::SetupPlayerInputComponent(InputComponent);  		//Hook up events for "ZoomIn" 		InputComponent->BindAction("ZoomIn", IE_Pressed, this, &APawnWithCamera::ZoomIn); 		InputComponent->BindAction("ZoomIn", IE_Released, this, &APawnWithCamera::ZoomOut);  		//Hook up every-frame handling for our four axes 		InputComponent->BindAxis("MoveForward", this, &APawnWithCamera::MoveForward); 		InputComponent->BindAxis("MoveRight", this, &APawnWithCamera::MoveRight); 		InputComponent->BindAxis("CameraPitch", this, &APawnWithCamera::PitchCamera); 		InputComponent->BindAxis("CameraYaw", this, &APawnWithCamera::YawCamera); 	}  	//Input functions 	void APawnWithCamera::MoveForward(float AxisValue) 	{ 		MovementInput.X = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f); 	}  	void APawnWithCamera::MoveRight(float AxisValue) 	{ 		MovementInput.Y = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f); 	}  	void APawnWithCamera::PitchCamera(float AxisValue) 	{ 		CameraInput.Y = AxisValue; 	}  	void APawnWithCamera::YawCamera(float AxisValue) 	{ 		CameraInput.X = AxisValue; 	}  	void APawnWithCamera::ZoomIn() 	{ 		bZoomingIn = true; 	}  	void APawnWithCamera::ZoomOut() 	{ 		bZoomingIn = false; 	}`

Copy full snippet
```
// Copyright 1998-2021 Epic Games, Inc. All Rights Reserved. #include "PawnWithCamera.h" #include "GameFramework/SpringArmComponent.h" #include "Camera/CameraComponent.h" // Sets default values APawnWithCamera::APawnWithCamera() { // Set this pawn to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; //Create our components RootComponent = CreateDefaultSubobject<USceneComponent>(TEXT("RootComponent")); StaticMeshComp = CreateDefaultSubobject <UStaticMeshComponent>(TEXT("StaticMeshComponent")); SpringArmComp = CreateDefaultSubobject<USpringArmComponent>(TEXT("SpringArmComponent")); CameraComp = CreateDefaultSubobject<UCameraComponent>(TEXT("CameraComponent")); StaticMeshComp->SetupAttachment(RootComponent); SpringArmComp->SetupAttachment(StaticMeshComp); CameraComp->SetupAttachment(SpringArmComp,USpringArmComponent::SocketName); //Setting Default Variables and Behavior of the SpringArmComponent SpringArmComp->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, 50.0f), FRotator(-60.0f, 0.0f, 0.0f)); SpringArmComp->TargetArmLength = 400.f; SpringArmComp->bEnableCameraLag = true; SpringArmComp->CameraLagSpeed = 3.0f; //Take control of the default Player AutoPossessPlayer = EAutoReceiveInput::Player0; } // Called when the game starts or when spawned void APawnWithCamera::BeginPlay() { Super::BeginPlay(); } // Called every frame void APawnWithCamera::Tick( float DeltaTime ) { Super::Tick(DeltaTime); //Zoom in if ZoomIn button is down, zoom back out if it's not { if (bZoomingIn) { ZoomFactor += DeltaTime / 0.5f; //Zoom in over half a second } else { ZoomFactor -= DeltaTime / 0.25f; //Zoom out over a quarter of a second } ZoomFactor = FMath::Clamp<float>(ZoomFactor, 0.0f, 1.0f); //Blend our camera's FOV and our SpringArm's length based on ZoomFactor CameraComp->FieldOfView = FMath::Lerp<float>(90.0f, 60.0f, ZoomFactor); SpringArmComp->TargetArmLength = FMath::Lerp<float>(400.0f, 300.0f, ZoomFactor); } //Rotate our actor's yaw, which will turn our camera because we're attached to it { FRotator NewRotation = GetActorRotation(); NewRotation.Yaw += CameraInput.X; SetActorRotation(NewRotation); } //Rotate our camera's pitch, but limit it so we're always looking downward { FRotator NewRotation = SpringArmComp->GetComponentRotation(); NewRotation.Pitch = FMath::Clamp(NewRotation.Pitch + CameraInput.Y, -80.0f, -15.0f); SpringArmComp->SetWorldRotation(NewRotation); } //Handle movement based on our "MoveX" and "MoveY" axes { if (!MovementInput.IsZero()) { //Scale our movement input axis values by 100 units per second MovementInput = MovementInput.SafeNormal() \* 100.0f; FVector NewLocation = GetActorLocation(); NewLocation += GetActorForwardVector() \* MovementInput.X \* DeltaTime; NewLocation += GetActorRightVector() \* MovementInput.Y \* DeltaTime; SetActorLocation(NewLocation); } } } // Called to bind functionality to input void APawnWithCamera::SetupPlayerInputComponent(class UInputComponent\* InputComponent) { Super::SetupPlayerInputComponent(InputComponent); //Hook up events for "ZoomIn" InputComponent->BindAction("ZoomIn", IE\_Pressed, this, &APawnWithCamera::ZoomIn); InputComponent->BindAction("ZoomIn", IE\_Released, this, &APawnWithCamera::ZoomOut); //Hook up every-frame handling for our four axes InputComponent->BindAxis("MoveForward", this, &APawnWithCamera::MoveForward); InputComponent->BindAxis("MoveRight", this, &APawnWithCamera::MoveRight); InputComponent->BindAxis("CameraPitch", this, &APawnWithCamera::PitchCamera); InputComponent->BindAxis("CameraYaw", this, &APawnWithCamera::YawCamera); } //Input functions void APawnWithCamera::MoveForward(float AxisValue) { MovementInput.X = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f); } void APawnWithCamera::MoveRight(float AxisValue) { MovementInput.Y = FMath::Clamp<float>(AxisValue, -1.0f, 1.0f); } void APawnWithCamera::PitchCamera(float AxisValue) { CameraInput.Y = AxisValue; } void APawnWithCamera::YawCamera(float AxisValue) { CameraInput.X = AxisValue; } void APawnWithCamera::ZoomIn() { bZoomingIn = true; } void APawnWithCamera::ZoomOut() { bZoomingIn = false; }

## 4\. On Your Own!

Using what you have learned, try to do the following:

-   Give the player a run key to hold down that will increase the **Pawn's** movement speed.
-   Experiment with different ways to mix automatic and input-driven camera movement. This is a very deep area of game development with a lot of room to explore!
-   Increase, decrease, or remove the lag from your **Spring Component** to get a better understanding of how much lag can affect your camera's overall feel.
-   Implement a small amount of periodic motion, possibly slightly randomized or using a **Curve** asset, to create a handheld feel to your camera.
-   Give your **Camera** some amount of automatic turning, so that the camera gradually gets behind the moving player object and faces the direction the player is moving.

As for the specifics covered in this tutorial:

-   For more information on Cameras and ways to control them, see the [Camera](/documentation/en-us/unreal-engine/cameras-in-unreal-engine) framework page.
-   To learn more about **Components**, try the [Components](/documentation/en-us/unreal-engine/quick-start-guide-to-components-and-collision-in-unreal-engine-cpp) tutorial.