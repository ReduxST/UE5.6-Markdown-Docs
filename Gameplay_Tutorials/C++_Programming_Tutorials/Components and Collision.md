# Components and Collision

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-components-and-collision-in-unreal-engine-cpp](https://dev.epicgames.com/documentation/en-us/unreal-engine/quick-start-guide-to-components-and-collision-in-unreal-engine-cpp)  
**Processed:** 2025-06-14 16:45:31

---

This tutorial will show you how to create **Components**, put them into a hierarchy, control them during gameplay, and use them to move your **Pawn** around a world that contains solid objects.

## 1\. Creating and Attaching Components

If you are new to **Unreal Engine**, you might want to read our [Programming Quick Start](/documentation/en-us/unreal-engine/unreal-engine-cpp-quick-start) first. For this tutorial, it is assumed that you are familiar with creating a project and adding C++ code to it, as well as configuring input in Unreal Editor.

If you are unfamiliar with creating your own Pawn class or configuring input, the [Player Input tutorial](/documentation/en-us/unreal-engine/quick-start-guide-to-player-input-in-unreal-engine-cpp) might be a good place to start.

1.  Begin by creating a new C++ project with starter content, named `HowTo_Components`. The first thing we need to add to this project is a customized Pawn that will hold our Components, move around our level, and collide with solid objects. For this tutorial, name it `CollidingPawn`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d738fc15-72a8-4cfc-8d19-12f1797e49ef/chooseparentclass.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/3db23e35-b27b-4311-9f80-13cfd1c3922b/namepawnclass.png)
2.  In your code editor (usually **Visual Studio** or **Xcode**), open `CollidingPawn.h` and add the following code to the bottom of our class definition:
    
    ```
             `UPROPERTY()          class UParticleSystemComponent* OurParticleSystem;`
    		
    Copy full snippet
    ```
    UPROPERTY() class UParticleSystemComponent\* OurParticleSystem;
    
    This variable keeps track of a **Particle System Component** that we will create later. We can create Components without making variables to track them, but if we want to use those Components in our code, we should store them in class member variables.
    
3.  We can now open `CollidingPawn.cpp` and edit the constructor function, `ACollidingPawn::ACollidingPawn`, by adding code that will spawn a variety of useful Components and arrange them in a hierarchy. We will create a **Sphere Component** to interact with the physical world, a **Static Mesh Component** to represent our collision shape visually, a Particle System Component that we can turn on or off at will, and a **Spring Arm Component** that we can use to attach a **Camera Component** to control our in-game perspective. Before we do that, we should include the header files that we will eventually need to use these Components. Underneath the line that includes the class header file, we can add:
    
    ```
             `#include "UObject/ConstructorHelpers.h"          #include "Particles/ParticleSystemComponent.h"          #include "Components/SphereComponent.h"          #include "Camera/CameraComponent.h"          #include "GameFramework/SpringArmComponent.h"`
    		
    Copy full snippet
    ```
    #include "UObject/ConstructorHelpers.h" #include "Particles/ParticleSystemComponent.h" #include "Components/SphereComponent.h" #include "Camera/CameraComponent.h" #include "GameFramework/SpringArmComponent.h"
4.  Decide which Component will be the root of the hierarchy. In this tutorial, we use the Sphere Component, since it is the physical presence that can interact and collide with our game world. An **Actor** can have multiple physics-enabled Components in its hierarchy, but for this tutorial, we only need one.
    
    ```
             `// Our root component will be a sphere that reacts to physics          USphereComponent* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent"));          RootComponent = SphereComponent;          SphereComponent->InitSphereRadius(40.0f);          SphereComponent->SetCollisionProfileName(TEXT("Pawn"));`
    		
    Copy full snippet
    ```
    // Our root component will be a sphere that reacts to physics USphereComponent\* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); RootComponent = SphereComponent; SphereComponent->InitSphereRadius(40.0f); SphereComponent->SetCollisionProfileName(TEXT("Pawn"));
5.  Next, we will create and attach a visible sphere from a **Static Mesh** Asset that has a radius of 50. Since this doesn't perfectly line up with the 40-radius Sphere Component we just created, scale it down to 80%. We also need to move it down by 40 units in order to have its center line up with the center of the Sphere Component.
    
    ```
             `// Create and position a mesh component so we can see where our sphere is          UStaticMeshComponent* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation"));          SphereVisual->SetupAttachment(RootComponent);          static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Sphere.Shape_Sphere"));          if (SphereVisualAsset.Succeeded())          {              SphereVisual->SetStaticMesh(SphereVisualAsset.Object);              SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f));              SphereVisual->SetWorldScale3D(FVector(0.8f));          }`
    		
    Copy full snippet
    ```
    // Create and position a mesh component so we can see where our sphere is UStaticMeshComponent\* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation")); SphereVisual->SetupAttachment(RootComponent); static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape\_Sphere.Shape\_Sphere")); if (SphereVisualAsset.Succeeded()) { SphereVisual->SetStaticMesh(SphereVisualAsset.Object); SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f)); SphereVisual->SetWorldScale3D(FVector(0.8f)); }
    
    Hard-coding Asset paths, like the Static Mesh for the sphere in this example, is not generally considered a best practice; we would usually create the Component in the constructor, make it editable, then create a Blueprint Asset in Unreal Editor and set up the Static Mesh Asset there. However, it is possible to do this directly in code, and could be faster for programmers debugging or building new features.
    
6.  We can now attach an inactive Particle System Component to our hierarchy. We can manipulate this Component in code, and will later set up an input to turn it on or off. Notice that the Particle System Component is attached directly to the Static Mesh Component, not to the root. It is also slightly offset from the bottom-center of the mesh so that it will be more visible during play.
    
    ```
             `// Create a particle system that we can activate or deactivate          OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles"));          OurParticleSystem->SetupAttachment(SphereVisual);          OurParticleSystem->bAutoActivate = false;          OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f));          static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P_Fire.P_Fire"));          if (ParticleAsset.Succeeded())          {              OurParticleSystem->SetTemplate(ParticleAsset.Object);          }`
    		
    Copy full snippet
    ```
    // Create a particle system that we can activate or deactivate OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles")); OurParticleSystem->SetupAttachment(SphereVisual); OurParticleSystem->bAutoActivate = false; OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f)); static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P\_Fire.P\_Fire")); if (ParticleAsset.Succeeded()) { OurParticleSystem->SetTemplate(ParticleAsset.Object); }
7.  A Spring Arm Component can provide a smoother attachment point for our camera by allowing our camera to accelerate and decelerate more slowly than the Pawn it is following. It also has a built-in feature that prevents the camera from going through solid objects, for situations such as when a player backs into a corner in a third-person game. While it isn't necessary, the Spring Arm Component can be a very fast and easy way to get smoother camera work into a game.
    
    ```
             `// Use a spring arm to give the camera smooth, natural-feeling motion.          USpringArmComponent* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm"));          SpringArm->SetupAttachment(RootComponent);          SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f));          SpringArm->TargetArmLength = 400.0f;          SpringArm->bEnableCameraLag = true;          SpringArm->CameraLagSpeed = 3.0f;`
    		
    Copy full snippet
    ```
    // Use a spring arm to give the camera smooth, natural-feeling motion. USpringArmComponent\* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm")); SpringArm->SetupAttachment(RootComponent); SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f)); SpringArm->TargetArmLength = 400.0f; SpringArm->bEnableCameraLag = true; SpringArm->CameraLagSpeed = 3.0f;
8.  The actual Camera Component is easy to create, and doesn't require any special settings for our use case. The Spring Arm Component has a special built-in socket that we can attach to, rather than attaching directly to the Component's base.
    
    ```
             `// Create a camera and attach to our spring arm          UCameraComponent* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera"));          Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName);`
    		
    Copy full snippet
    ```
    // Create a camera and attach to our spring arm UCameraComponent\* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera")); Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName);
9.  Now that our Components are created and attached, we should set this Pawn to be controlled by the default player. The following code is all we need:
    
    ```
             `// Take control of the default player          AutoPossessPlayer = EAutoReceiveInput::Player0;`
    Copy full snippet
    ```
    // Take control of the default player AutoPossessPlayer = EAutoReceiveInput::Player0;

Our new Pawn now has a collection of useful Components attached to it, and is ready to be configured for user control. We can now return to Unreal Editor.

### Work-In-Progress Code

**CollidingPawn.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Pawn.h" 	#include "CollidingPawn.generated.h"  	UCLASS() 	class HOWTO_COMPONENTS_API ACollidingPawn : public APawn 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this pawn's properties 		ACollidingPawn();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		// Called to bind functionality to input 		virtual void SetupPlayerInputComponent(class UInputComponent* InInputComponent) override;  		UPROPERTY() 		class UParticleSystemComponent* OurParticleSystem; 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Pawn.h" #include "CollidingPawn.generated.h" UCLASS() class HOWTO\_COMPONENTS\_API ACollidingPawn : public APawn { GENERATED\_BODY() public: // Sets default values for this pawn's properties ACollidingPawn(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* InInputComponent) override; UPROPERTY() class UParticleSystemComponent\* OurParticleSystem; };

**CollidingPawn.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "CollidingPawn.h" 	#include "UObject/ConstructorHelpers.h" 	#include "Particles/ParticleSystemComponent.h" 	#include "Components/SphereComponent.h" 	#include "Camera/CameraComponent.h" 	#include "GameFramework/SpringArmComponent.h"  	// Sets default values 	ACollidingPawn::ACollidingPawn() 	{ 		// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		// Our root component will be a sphere that reacts to physics 		USphereComponent* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); 		RootComponent = SphereComponent; 		SphereComponent->InitSphereRadius(40.0f); 		SphereComponent->SetCollisionProfileName(TEXT("Pawn"));  		// Create and position a mesh component so we can see where our sphere is 		UStaticMeshComponent* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation")); 		SphereVisual->SetupAttachment(RootComponent); 		static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Sphere.Shape_Sphere")); 		if (SphereVisualAsset.Succeeded()) 		{ 			SphereVisual->SetStaticMesh(SphereVisualAsset.Object); 			SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f)); 			SphereVisual->SetWorldScale3D(FVector(0.8f)); 		}  		// Create a particle system that we can activate or deactivate 		OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles")); 		OurParticleSystem->SetupAttachment(SphereVisual); 		OurParticleSystem->bAutoActivate = false; 		OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f)); 		static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P_Fire.P_Fire")); 		if (ParticleAsset.Succeeded()) 		{ 			OurParticleSystem->SetTemplate(ParticleAsset.Object); 		}  		// Use a spring arm to give the camera smooth, natural-feeling motion. 		USpringArmComponent* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm")); 		SpringArm->SetupAttachment(RootComponent); 		SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f)); 		SpringArm->TargetArmLength = 400.0f; 		SpringArm->bEnableCameraLag = true; 		SpringArm->CameraLagSpeed = 3.0f;  		// Create a camera and attach to our spring arm 		UCameraComponent* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera")); 		Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName);  		// Take control of the default player 		AutoPossessPlayer = EAutoReceiveInput::Player0; 	}  	// Called when the game starts or when spawned 	void ACollidingPawn::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void ACollidingPawn::Tick( float DeltaTime ) 	{ 		Super::Tick( DeltaTime );  	}  	// Called to bind functionality to input 	void ACollidingPawn::SetupPlayerInputComponent(class UInputComponent* InInputComponent) 	{ 		Super::SetupPlayerInputComponent(InInputComponent); 	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "CollidingPawn.h" #include "UObject/ConstructorHelpers.h" #include "Particles/ParticleSystemComponent.h" #include "Components/SphereComponent.h" #include "Camera/CameraComponent.h" #include "GameFramework/SpringArmComponent.h" // Sets default values ACollidingPawn::ACollidingPawn() { // Set this pawn to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Our root component will be a sphere that reacts to physics USphereComponent\* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); RootComponent = SphereComponent; SphereComponent->InitSphereRadius(40.0f); SphereComponent->SetCollisionProfileName(TEXT("Pawn")); // Create and position a mesh component so we can see where our sphere is UStaticMeshComponent\* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation")); SphereVisual->SetupAttachment(RootComponent); static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape\_Sphere.Shape\_Sphere")); if (SphereVisualAsset.Succeeded()) { SphereVisual->SetStaticMesh(SphereVisualAsset.Object); SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f)); SphereVisual->SetWorldScale3D(FVector(0.8f)); } // Create a particle system that we can activate or deactivate OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles")); OurParticleSystem->SetupAttachment(SphereVisual); OurParticleSystem->bAutoActivate = false; OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f)); static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P\_Fire.P\_Fire")); if (ParticleAsset.Succeeded()) { OurParticleSystem->SetTemplate(ParticleAsset.Object); } // Use a spring arm to give the camera smooth, natural-feeling motion. USpringArmComponent\* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm")); SpringArm->SetupAttachment(RootComponent); SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f)); SpringArm->TargetArmLength = 400.0f; SpringArm->bEnableCameraLag = true; SpringArm->CameraLagSpeed = 3.0f; // Create a camera and attach to our spring arm UCameraComponent\* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera")); Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName); // Take control of the default player AutoPossessPlayer = EAutoReceiveInput::Player0; } // Called when the game starts or when spawned void ACollidingPawn::BeginPlay() { Super::BeginPlay(); } // Called every frame void ACollidingPawn::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void ACollidingPawn::SetupPlayerInputComponent(class UInputComponent\* InInputComponent) { Super::SetupPlayerInputComponent(InInputComponent); }

## 2\. Configuring Input and Creating a Pawn Movement Component

1.  Returning to Unreal Editor, it's time to configure our project's input settings. These settings can be found under **Project Settings** in the **Edit** dropdown menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/b7f81676-2f5b-45dc-8e36-0902141c9d66/editprojectsettings.png)
    
    Once there, we can select **Input** from the **Engine** section in the left panel. We will need an **Action Mapping** to set up our particle-system toggle, two **Axis Mappings** to move our **Pawn**, and one more **Axis Mapping** to turn our Pawn.
    
    <table class="table" style="--columns-count: 3;"><tbody><tr><td>Action Mapping</td><td>&nbsp;</td><td>&nbsp;</td></tr><tr><td>ParticleToggle</td><td>Space Bar</td><td>&nbsp;</td></tr></tbody></table>
    
    <table class="table" style="--columns-count: 3;"><tbody><tr><td>Axis Mapping</td><td>&nbsp;</td><td>&nbsp;</td></tr><tr><td>MoveForward</td><td>W</td><td>1.0</td></tr><tr><td>&nbsp;</td><td>S</td><td>-1.0</td></tr><tr><td>MoveRight</td><td>A</td><td>-1.0</td></tr><tr><td>&nbsp;</td><td>D</td><td>1.0</td></tr><tr><td>Turn</td><td>Mouse X</td><td>1.0</td></tr></tbody></table>
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/d6af2d42-8f47-4c01-95f3-d9b8c4926844/inputsettings.png)
2.  Instead of handling all our movement in our Pawn class directly, we will create a **Movement Component** to manage it for us. For this tutorial, we'll extend the **Pawn Movement Component** class. We'll start by selecting the **Add Code to Project** command from the **File** dropdown menu.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/8df025cb-ffbb-4b43-bddf-cde979d66905/addcppcode.png)
    
    Unlike our Pawn class, Pawn Movement Component is not visible by default. To find it, we need to check the **Show All Classes** option.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/6df2afdb-abfd-4f14-8524-6e1439f3b201/showallclasses.png)
    
    Typing "movement" into the search bar can help narrow the list quickly.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/ca22a142-0beb-44d6-808c-bcab386b51a8/chooseparentclass2.png)
    
    Pawn Movement Components have some powerful, built-in features to help with common physics functionality, and are a good way to share movement code between many Pawn types. Using Components to separate functionality is a good practice to reduce clutter as your project grows and your Pawns become more complex.
    
    Since we called our Pawn class `CollidingPawn`, let's call this `CollidingPawnMovementComponent`.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/9b1985d5-df49-4e08-85f6-c2897a64ec43/namecomponent.png)

We have just defined our input configuration and created a custom Pawn Movement Component. We're ready to go back to our code editor and write code to define how Pawns will move when our Pawn Movement Component is in use.

## 3\. Coding Our Pawn Movement Component's Behavior

1.  We can go back to our code editor now and program our customized Pawn Movement Component. All we really need to write is a `TickComponent` function (similar to an Actor's `Tick` function) to tell us how to move each frame. In `CollidingPawnMovementComponent.h`, we'll need to override `TickComponent` in the class definition:
    
    ```
             `public:              virtual void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction) override;`
    		
    Copy full snippet
    ```
    public: virtual void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction \*ThisTickFunction) override;
    
    We'll define this function in `CollidingPawnMovementComponent.cpp`:
    
    ```
         `void UCollidingPawnMovementComponent::TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction)      {          Super::TickComponent(DeltaTime, TickType, ThisTickFunction);           // Make sure that everything is still valid, and that we are allowed to move.          if (!PawnOwner || !UpdatedComponent || ShouldSkipUpdate(DeltaTime))          {              return;          }           // Get (and then clear) the movement vector that we set in ACollidingPawn::Tick          FVector DesiredMovementThisFrame = ConsumeInputVector().GetClampedToMaxSize(1.0f) * DeltaTime * 150.0f;          if (!DesiredMovementThisFrame.IsNearlyZero())          {              FHitResult Hit;              SafeMoveUpdatedComponent(DesiredMovementThisFrame, UpdatedComponent->GetComponentRotation(), true, Hit);               // If we bumped into something, try to slide along it              if (Hit.IsValidBlockingHit())              {                  SlideAlongSurface(DesiredMovementThisFrame, 1.f - Hit.Time, Hit.Normal, Hit);              }          }      };`
    
    Copy full snippet
    ```
    void UCollidingPawnMovementComponent::TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction \*ThisTickFunction) { Super::TickComponent(DeltaTime, TickType, ThisTickFunction); // Make sure that everything is still valid, and that we are allowed to move. if (!PawnOwner || !UpdatedComponent || ShouldSkipUpdate(DeltaTime)) { return; } // Get (and then clear) the movement vector that we set in ACollidingPawn::Tick FVector DesiredMovementThisFrame = ConsumeInputVector().GetClampedToMaxSize(1.0f) \* DeltaTime \* 150.0f; if (!DesiredMovementThisFrame.IsNearlyZero()) { FHitResult Hit; SafeMoveUpdatedComponent(DesiredMovementThisFrame, UpdatedComponent->GetComponentRotation(), true, Hit); // If we bumped into something, try to slide along it if (Hit.IsValidBlockingHit()) { SlideAlongSurface(DesiredMovementThisFrame, 1.f - Hit.Time, Hit.Normal, Hit); } } };
    
    This code will move our Pawn smoothly around the world, sliding off of surfaces where appropriate. There is no gravity applied to our Pawn, and its maximum speed is hard-coded to 150 **Unreal Units** per second.
    
    This `TickComponent` function makes use of a few of the powerful features offered by the `UPawnMovementComponent` class.
    
    -   `ConsumeInputVector` reports and clears the value of a built-in variable that we will use to store our movement inputs.
        
    -   \`SafeMoveUpdatedComponent uses Unreal Engine physics to move our Pawn Movement Component while respecting solid barriers.
        
    -   `SlideAlongSurface` handles the calculations and physics involved with sliding smoothly along collision surfaces like walls and ramps when a move results in a collision, rather than simply stopping in place and sticking to the wall or ramp.
        
    
    There are more features included in Pawn Movement Components that are worthy of examination, but they are not needed for the scope of this tutorial. Looking at other classes, such as **Floating Pawn Movement**, **Spectator Pawn Movement**, or **Character Movement Component**, could provide additional usage examples and ideas.
    

With our Pawn Movement Component's behavior defined, we can now write the code that will tie it all together in our customized Pawn class.

### Work-In-Progress Code

**CollidingPawn.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Pawn.h" 	#include "CollidingPawn.generated.h"  	UCLASS() 	class HOWTO_COMPONENTS_API ACollidingPawn : public APawn 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this pawn's properties 		ACollidingPawn();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		// Called to bind functionality to input 		virtual void SetupPlayerInputComponent(class UInputComponent* InInputComponent) override;  		UPROPERTY() 		class UParticleSystemComponent* OurParticleSystem; 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Pawn.h" #include "CollidingPawn.generated.h" UCLASS() class HOWTO\_COMPONENTS\_API ACollidingPawn : public APawn { GENERATED\_BODY() public: // Sets default values for this pawn's properties ACollidingPawn(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* InInputComponent) override; UPROPERTY() class UParticleSystemComponent\* OurParticleSystem; };

**CollidingPawn.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "CollidingPawn.h" 	#include "UObject/ConstructorHelpers.h" 	#include "Particles/ParticleSystemComponent.h" 	#include "Components/SphereComponent.h" 	#include "Camera/CameraComponent.h" 	#include "GameFramework/SpringArmComponent.h"  	// Sets default values 	ACollidingPawn::ACollidingPawn() 	{ 		// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		// Our root component will be a sphere that reacts to physics 		USphereComponent* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); 		RootComponent = SphereComponent; 		SphereComponent->InitSphereRadius(40.0f); 		SphereComponent->SetCollisionProfileName(TEXT("Pawn"));  		// Create and position a mesh component so we can see where our sphere is 		UStaticMeshComponent* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation")); 		SphereVisual->SetupAttachment(RootComponent); 		static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Sphere.Shape_Sphere")); 		if (SphereVisualAsset.Succeeded()) 		{ 			SphereVisual->SetStaticMesh(SphereVisualAsset.Object); 			SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f)); 			SphereVisual->SetWorldScale3D(FVector(0.8f)); 		}  		// Create a particle system that we can activate or deactivate 		OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles")); 		OurParticleSystem->SetupAttachment(SphereVisual); 		OurParticleSystem->bAutoActivate = false; 		OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f)); 		static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P_Fire.P_Fire")); 		if (ParticleAsset.Succeeded()) 		{ 			OurParticleSystem->SetTemplate(ParticleAsset.Object); 		}  		// Use a spring arm to give the camera smooth, natural-feeling motion. 		USpringArmComponent* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm")); 		SpringArm->SetupAttachment(RootComponent); 		SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f)); 		SpringArm->TargetArmLength = 400.0f; 		SpringArm->bEnableCameraLag = true; 		SpringArm->CameraLagSpeed = 3.0f;  		// Create a camera and attach to our spring arm 		UCameraComponent* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera")); 		Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName);  		// Take control of the default player 		AutoPossessPlayer = EAutoReceiveInput::Player0; 	}  	// Called when the game starts or when spawned 	void ACollidingPawn::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void ACollidingPawn::Tick( float DeltaTime ) 	{ 		Super::Tick( DeltaTime );  	}  	// Called to bind functionality to input 	void ACollidingPawn::SetupPlayerInputComponent(class UInputComponent* InInputComponent) 	{ 		Super::SetupPlayerInputComponent(InInputComponent); 	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "CollidingPawn.h" #include "UObject/ConstructorHelpers.h" #include "Particles/ParticleSystemComponent.h" #include "Components/SphereComponent.h" #include "Camera/CameraComponent.h" #include "GameFramework/SpringArmComponent.h" // Sets default values ACollidingPawn::ACollidingPawn() { // Set this pawn to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Our root component will be a sphere that reacts to physics USphereComponent\* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); RootComponent = SphereComponent; SphereComponent->InitSphereRadius(40.0f); SphereComponent->SetCollisionProfileName(TEXT("Pawn")); // Create and position a mesh component so we can see where our sphere is UStaticMeshComponent\* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation")); SphereVisual->SetupAttachment(RootComponent); static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape\_Sphere.Shape\_Sphere")); if (SphereVisualAsset.Succeeded()) { SphereVisual->SetStaticMesh(SphereVisualAsset.Object); SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f)); SphereVisual->SetWorldScale3D(FVector(0.8f)); } // Create a particle system that we can activate or deactivate OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles")); OurParticleSystem->SetupAttachment(SphereVisual); OurParticleSystem->bAutoActivate = false; OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f)); static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P\_Fire.P\_Fire")); if (ParticleAsset.Succeeded()) { OurParticleSystem->SetTemplate(ParticleAsset.Object); } // Use a spring arm to give the camera smooth, natural-feeling motion. USpringArmComponent\* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm")); SpringArm->SetupAttachment(RootComponent); SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f)); SpringArm->TargetArmLength = 400.0f; SpringArm->bEnableCameraLag = true; SpringArm->CameraLagSpeed = 3.0f; // Create a camera and attach to our spring arm UCameraComponent\* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera")); Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName); // Take control of the default player AutoPossessPlayer = EAutoReceiveInput::Player0; } // Called when the game starts or when spawned void ACollidingPawn::BeginPlay() { Super::BeginPlay(); } // Called every frame void ACollidingPawn::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void ACollidingPawn::SetupPlayerInputComponent(class UInputComponent\* InInputComponent) { Super::SetupPlayerInputComponent(InInputComponent); }

**CollidingPawnMovementComponent.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/PawnMovementComponent.h" 	#include "CollidingPawnMovementComponent.generated.h"  	/** 		* 		*/ 	UCLASS() 	class HOWTO_COMPONENTS_API UCollidingPawnMovementComponent : public UPawnMovementComponent 	{ 		GENERATED_BODY()  	public: 		virtual void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction) override; 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/PawnMovementComponent.h" #include "CollidingPawnMovementComponent.generated.h" /\*\* \* \*/ UCLASS() class HOWTO\_COMPONENTS\_API UCollidingPawnMovementComponent : public UPawnMovementComponent { GENERATED\_BODY() public: virtual void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction \*ThisTickFunction) override; };

**CollidingPawnMovementComponent.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "CollidingPawnMovementComponent.h"  	void UCollidingPawnMovementComponent::TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction) 	{ 		Super::TickComponent(DeltaTime, TickType, ThisTickFunction);  		// Make sure that everything is still valid, and that we are allowed to move. 		if (!PawnOwner || !UpdatedComponent || ShouldSkipUpdate(DeltaTime)) 		{ 			return; 		}  		// Get (and then clear) the movement vector that we set in ACollidingPawn::Tick 		FVector DesiredMovementThisFrame = ConsumeInputVector().GetClampedToMaxSize(1.0f) * DeltaTime * 150.0f; 		if (!DesiredMovementThisFrame.IsNearlyZero()) 		{ 			FHitResult Hit; 			SafeMoveUpdatedComponent(DesiredMovementThisFrame, UpdatedComponent->GetComponentRotation(), true, Hit);  			// If we bumped into something, try to slide along it 			if (Hit.IsValidBlockingHit()) 			{ 				SlideAlongSurface(DesiredMovementThisFrame, 1.f - Hit.Time, Hit.Normal, Hit); 			} 		} 	};`
Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "CollidingPawnMovementComponent.h" void UCollidingPawnMovementComponent::TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction \*ThisTickFunction) { Super::TickComponent(DeltaTime, TickType, ThisTickFunction); // Make sure that everything is still valid, and that we are allowed to move. if (!PawnOwner || !UpdatedComponent || ShouldSkipUpdate(DeltaTime)) { return; } // Get (and then clear) the movement vector that we set in ACollidingPawn::Tick FVector DesiredMovementThisFrame = ConsumeInputVector().GetClampedToMaxSize(1.0f) \* DeltaTime \* 150.0f; if (!DesiredMovementThisFrame.IsNearlyZero()) { FHitResult Hit; SafeMoveUpdatedComponent(DesiredMovementThisFrame, UpdatedComponent->GetComponentRotation(), true, Hit); // If we bumped into something, try to slide along it if (Hit.IsValidBlockingHit()) { SlideAlongSurface(DesiredMovementThisFrame, 1.f - Hit.Time, Hit.Normal, Hit); } } };

## 4\. Using Our Pawn and Components Together

1.  In order to use our custom Pawn Movement Component, we will first need to add a variable to our Pawn class to keep track of it. At the bottom of our class definition in `CollidingPawn.h`, near where we added the `OurParticleSystem` variable, we should add:
    
    ```
             `UPROPERTY()          class UCollidingPawnMovementComponent* OurMovementComponent;`
    		
    Copy full snippet
    ```
    UPROPERTY() class UCollidingPawnMovementComponent\* OurMovementComponent;
2.  Once we have a place to keep track of it, we will need to create a **Colliding Pawn Movement Component** to store in our new variable, so let's open `CollidingPawn.cpp` and add the following to the top of the file, underneath the line that includes `GameFramework/Pawn.h` line, so that our code will be able to reference our new class:
    
    ```
             `#include "CollidingPawnMovementComponent.h"`
    Copy full snippet
    ```
    #include "CollidingPawnMovementComponent.h"
    
    Be sure that the last header file included is the one ending with "generated.h"; you can encounter compiler errors if it is not.
    
    Creating a Pawn Movement Component and associating it with our Pawn is simple. At the bottom of `ACollidingPawn::ACollidingPawn`, we can add this code:
    
    ```
         `// Create an instance of our movement component, and tell it to update the root.      OurMovementComponent = CreateDefaultSubobject<UCollidingPawnMovementComponent>(TEXT("CustomMovementComponent"));      OurMovementComponent->UpdatedComponent = RootComponent;`
    
    Copy full snippet
    ```
    // Create an instance of our movement component, and tell it to update the root. OurMovementComponent = CreateDefaultSubobject<UCollidingPawnMovementComponent>(TEXT("CustomMovementComponent")); OurMovementComponent->UpdatedComponent = RootComponent;
    
    Unlike the other Components we've seen so far, we don't need to attach this Component to our own Component hierarchy. This is because our other Components are all types of **Scene Components**, which inherently require physical locations. **Movement Controllers**, however, are not Scene Components and do not represent physical objects, so the concept of existing at a physical location or being physically attached to another Component does not apply to them.
    
3.  Pawns have a function called `GetMovementComponent` that is used to enable other classes in the engine to access the Pawn Movement Component that the Pawn is currently using. We will need to override that function so that it returns our custom Pawn Movement Component. In the class definition in `CollidingPawn.h`, we need to add:
    
    ```
             `virtual UPawnMovementComponent* GetMovementComponent() const override;`
    		
    Copy full snippet
    ```
    virtual UPawnMovementComponent\* GetMovementComponent() const override;
    
    And in `CollidingPawn.cpp`, we need to add the definition of our overridden function, as follows:
    
    ```
         `UPawnMovementComponent* ACollidingPawn::GetMovementComponent() const      {          return OurMovementComponent;      }`
    
    Copy full snippet
    ```
    UPawnMovementComponent\* ACollidingPawn::GetMovementComponent() const { return OurMovementComponent; }
4.  With our new Pawn Movement Component set up, we can create code to handle the input that our Pawn will receive. We will start by declaring a few functions in our class definition in `CollidingPawn.h`:
    
    ```
             `void MoveForward(float AxisValue);          void MoveRight(float AxisValue);          void Turn(float AxisValue);          void ParticleToggle();`
    		
    Copy full snippet
    ```
    void MoveForward(float AxisValue); void MoveRight(float AxisValue); void Turn(float AxisValue); void ParticleToggle();
    
    In `CollidingPawn.cpp`, we will add the definitions of those functions as follows:
    
    ```
             `void ACollidingPawn::MoveForward(float AxisValue)          {              if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent))              {                  OurMovementComponent->AddInputVector(GetActorForwardVector() * AxisValue);              }          }           void ACollidingPawn::MoveRight(float AxisValue)          {              if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent))              {                  OurMovementComponent->AddInputVector(GetActorRightVector() * AxisValue);              }          }           void ACollidingPawn::Turn(float AxisValue)          {              FRotator NewRotation = GetActorRotation();              NewRotation.Yaw += AxisValue;              SetActorRotation(NewRotation);          }           void ACollidingPawn::ParticleToggle()          {              if (OurParticleSystem && OurParticleSystem->Template)              {                  OurParticleSystem->ToggleActive();              }          }`
    
    Copy full snippet
    ```
    void ACollidingPawn::MoveForward(float AxisValue) { if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent)) { OurMovementComponent->AddInputVector(GetActorForwardVector() \* AxisValue); } } void ACollidingPawn::MoveRight(float AxisValue) { if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent)) { OurMovementComponent->AddInputVector(GetActorRightVector() \* AxisValue); } } void ACollidingPawn::Turn(float AxisValue) { FRotator NewRotation = GetActorRotation(); NewRotation.Yaw += AxisValue; SetActorRotation(NewRotation); } void ACollidingPawn::ParticleToggle() { if (OurParticleSystem && OurParticleSystem->Template) { OurParticleSystem->ToggleActive(); } }
5.  All that remains is to bind our functions to our input events. Let's add the following code to `ACollidingPawn::SetupPlayerInputComponent`:
    
    ```
             `InInputComponent->BindAction("ParticleToggle", IE_Pressed, this, &ACollidingPawn::ParticleToggle); 		          InInputComponent->BindAxis("MoveForward", this, &ACollidingPawn::MoveForward);          InInputComponent->BindAxis("MoveRight", this, &ACollidingPawn::MoveRight);          InInputComponent->BindAxis("Turn", this, &ACollidingPawn::Turn);`
    		
    Copy full snippet
    ```
    InInputComponent->BindAction("ParticleToggle", IE\_Pressed, this, &ACollidingPawn::ParticleToggle); InInputComponent->BindAxis("MoveForward", this, &ACollidingPawn::MoveForward); InInputComponent->BindAxis("MoveRight", this, &ACollidingPawn::MoveRight); InInputComponent->BindAxis("Turn", this, &ACollidingPawn::Turn);
6.  We are done programming and can now return to Unreal Editor and press the **Compile** button to load our changes.
    

Our programming work is done, and we can now place our custom Pawn in the world and move it around.

### Finished Code

**CollidingPawn.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/Pawn.h" 	#include "CollidingPawn.generated.h"  	UCLASS() 	class HOWTO_COMPONENTS_API ACollidingPawn : public APawn 	{ 		GENERATED_BODY()  	public: 		// Sets default values for this pawn's properties 		ACollidingPawn();  	protected: 		// Called when the game starts or when spawned 		virtual void BeginPlay() override;  	public: 		// Called every frame 		virtual void Tick( float DeltaSeconds ) override;  		// Called to bind functionality to input 		virtual void SetupPlayerInputComponent(class UInputComponent* InInputComponent) override;  		UPROPERTY() 		class UParticleSystemComponent* OurParticleSystem;  		UPROPERTY() 		class UCollidingPawnMovementComponent* OurMovementComponent;  		virtual UPawnMovementComponent* GetMovementComponent() const override;  		void MoveForward(float AxisValue); 		void MoveRight(float AxisValue); 		void Turn(float AxisValue); 		void ParticleToggle(); 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/Pawn.h" #include "CollidingPawn.generated.h" UCLASS() class HOWTO\_COMPONENTS\_API ACollidingPawn : public APawn { GENERATED\_BODY() public: // Sets default values for this pawn's properties ACollidingPawn(); protected: // Called when the game starts or when spawned virtual void BeginPlay() override; public: // Called every frame virtual void Tick( float DeltaSeconds ) override; // Called to bind functionality to input virtual void SetupPlayerInputComponent(class UInputComponent\* InInputComponent) override; UPROPERTY() class UParticleSystemComponent\* OurParticleSystem; UPROPERTY() class UCollidingPawnMovementComponent\* OurMovementComponent; virtual UPawnMovementComponent\* GetMovementComponent() const override; void MoveForward(float AxisValue); void MoveRight(float AxisValue); void Turn(float AxisValue); void ParticleToggle(); };

**CollidingPawn.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "CollidingPawn.h" 	#include "CollidingPawnMovementComponent.h" 	#include "UObject/ConstructorHelpers.h" 	#include "Particles/ParticleSystemComponent.h" 	#include "Components/SphereComponent.h" 	#include "Camera/CameraComponent.h" 	#include "GameFramework/SpringArmComponent.h"  	// Sets default values 	ACollidingPawn::ACollidingPawn() 	{ 		// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it. 		PrimaryActorTick.bCanEverTick = true;  		// Our root component will be a sphere that reacts to physics 		USphereComponent* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); 		RootComponent = SphereComponent; 		SphereComponent->InitSphereRadius(40.0f); 		SphereComponent->SetCollisionProfileName(TEXT("Pawn"));  		// Create and position a mesh component so we can see where our sphere is 		UStaticMeshComponent* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation")); 		SphereVisual->SetupAttachment(RootComponent); 		static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape_Sphere.Shape_Sphere")); 		if (SphereVisualAsset.Succeeded()) 		{ 			SphereVisual->SetStaticMesh(SphereVisualAsset.Object); 			SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f)); 			SphereVisual->SetWorldScale3D(FVector(0.8f)); 		}  		// Create a particle system that we can activate or deactivate 		OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles")); 		OurParticleSystem->SetupAttachment(SphereVisual); 		OurParticleSystem->bAutoActivate = false; 		OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f)); 		static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P_Fire.P_Fire")); 		if (ParticleAsset.Succeeded()) 		{ 			OurParticleSystem->SetTemplate(ParticleAsset.Object); 		}  		// Use a spring arm to give the camera smooth, natural-feeling motion. 		USpringArmComponent* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm")); 		SpringArm->SetupAttachment(RootComponent); 		SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f)); 		SpringArm->TargetArmLength = 400.0f; 		SpringArm->bEnableCameraLag = true; 		SpringArm->CameraLagSpeed = 3.0f;  		// Create a camera and attach to our spring arm 		UCameraComponent* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera")); 		Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName);  		// Take control of the default player 		AutoPossessPlayer = EAutoReceiveInput::Player0;  		// Create an instance of our movement component, and tell it to update our root component. 		OurMovementComponent = CreateDefaultSubobject<UCollidingPawnMovementComponent>(TEXT("CustomMovementComponent")); 		OurMovementComponent->UpdatedComponent = RootComponent; 	}  	// Called when the game starts or when spawned 	void ACollidingPawn::BeginPlay() 	{ 		Super::BeginPlay();  	}  	// Called every frame 	void ACollidingPawn::Tick( float DeltaTime ) 	{ 		Super::Tick( DeltaTime );  	}  	// Called to bind functionality to input 	void ACollidingPawn::SetupPlayerInputComponent(class UInputComponent* InInputComponent) 	{ 		Super::SetupPlayerInputComponent(InInputComponent);  		InInputComponent->BindAction("ParticleToggle", IE_Pressed, this, &ACollidingPawn::ParticleToggle);  		InInputComponent->BindAxis("MoveForward", this, &ACollidingPawn::MoveForward); 		InInputComponent->BindAxis("MoveRight", this, &ACollidingPawn::MoveRight); 		InInputComponent->BindAxis("Turn", this, &ACollidingPawn::Turn); 	}  	UPawnMovementComponent* ACollidingPawn::GetMovementComponent() const 	{ 		return OurMovementComponent; 	}  	void ACollidingPawn::MoveForward(float AxisValue) 	{ 		if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent)) 		{ 			OurMovementComponent->AddInputVector(GetActorForwardVector() * AxisValue); 		} 	}  	void ACollidingPawn::MoveRight(float AxisValue) 	{ 		if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent)) 		{ 			OurMovementComponent->AddInputVector(GetActorRightVector() * AxisValue); 		} 	}  	void ACollidingPawn::Turn(float AxisValue) 	{ 		FRotator NewRotation = GetActorRotation(); 		NewRotation.Yaw += AxisValue; 		SetActorRotation(NewRotation); 	}  	void ACollidingPawn::ParticleToggle() 	{ 		if (OurParticleSystem && OurParticleSystem->Template) 		{ 			OurParticleSystem->ToggleActive(); 		} 	}`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "CollidingPawn.h" #include "CollidingPawnMovementComponent.h" #include "UObject/ConstructorHelpers.h" #include "Particles/ParticleSystemComponent.h" #include "Components/SphereComponent.h" #include "Camera/CameraComponent.h" #include "GameFramework/SpringArmComponent.h" // Sets default values ACollidingPawn::ACollidingPawn() { // Set this pawn to call Tick() every frame. You can turn this off to improve performance if you don't need it. PrimaryActorTick.bCanEverTick = true; // Our root component will be a sphere that reacts to physics USphereComponent\* SphereComponent = CreateDefaultSubobject<USphereComponent>(TEXT("RootComponent")); RootComponent = SphereComponent; SphereComponent->InitSphereRadius(40.0f); SphereComponent->SetCollisionProfileName(TEXT("Pawn")); // Create and position a mesh component so we can see where our sphere is UStaticMeshComponent\* SphereVisual = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("VisualRepresentation")); SphereVisual->SetupAttachment(RootComponent); static ConstructorHelpers::FObjectFinder<UStaticMesh> SphereVisualAsset(TEXT("/Game/StarterContent/Shapes/Shape\_Sphere.Shape\_Sphere")); if (SphereVisualAsset.Succeeded()) { SphereVisual->SetStaticMesh(SphereVisualAsset.Object); SphereVisual->SetRelativeLocation(FVector(0.0f, 0.0f, -40.0f)); SphereVisual->SetWorldScale3D(FVector(0.8f)); } // Create a particle system that we can activate or deactivate OurParticleSystem = CreateDefaultSubobject<UParticleSystemComponent>(TEXT("MovementParticles")); OurParticleSystem->SetupAttachment(SphereVisual); OurParticleSystem->bAutoActivate = false; OurParticleSystem->SetRelativeLocation(FVector(-20.0f, 0.0f, 20.0f)); static ConstructorHelpers::FObjectFinder<UParticleSystem> ParticleAsset(TEXT("/Game/StarterContent/Particles/P\_Fire.P\_Fire")); if (ParticleAsset.Succeeded()) { OurParticleSystem->SetTemplate(ParticleAsset.Object); } // Use a spring arm to give the camera smooth, natural-feeling motion. USpringArmComponent\* SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("CameraAttachmentArm")); SpringArm->SetupAttachment(RootComponent); SpringArm->SetRelativeRotation(FRotator(-45.f, 0.f, 0.f)); SpringArm->TargetArmLength = 400.0f; SpringArm->bEnableCameraLag = true; SpringArm->CameraLagSpeed = 3.0f; // Create a camera and attach to our spring arm UCameraComponent\* Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("ActualCamera")); Camera->SetupAttachment(SpringArm, USpringArmComponent::SocketName); // Take control of the default player AutoPossessPlayer = EAutoReceiveInput::Player0; // Create an instance of our movement component, and tell it to update our root component. OurMovementComponent = CreateDefaultSubobject<UCollidingPawnMovementComponent>(TEXT("CustomMovementComponent")); OurMovementComponent->UpdatedComponent = RootComponent; } // Called when the game starts or when spawned void ACollidingPawn::BeginPlay() { Super::BeginPlay(); } // Called every frame void ACollidingPawn::Tick( float DeltaTime ) { Super::Tick( DeltaTime ); } // Called to bind functionality to input void ACollidingPawn::SetupPlayerInputComponent(class UInputComponent\* InInputComponent) { Super::SetupPlayerInputComponent(InInputComponent); InInputComponent->BindAction("ParticleToggle", IE\_Pressed, this, &ACollidingPawn::ParticleToggle); InInputComponent->BindAxis("MoveForward", this, &ACollidingPawn::MoveForward); InInputComponent->BindAxis("MoveRight", this, &ACollidingPawn::MoveRight); InInputComponent->BindAxis("Turn", this, &ACollidingPawn::Turn); } UPawnMovementComponent\* ACollidingPawn::GetMovementComponent() const { return OurMovementComponent; } void ACollidingPawn::MoveForward(float AxisValue) { if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent)) { OurMovementComponent->AddInputVector(GetActorForwardVector() \* AxisValue); } } void ACollidingPawn::MoveRight(float AxisValue) { if (OurMovementComponent && (OurMovementComponent->UpdatedComponent == RootComponent)) { OurMovementComponent->AddInputVector(GetActorRightVector() \* AxisValue); } } void ACollidingPawn::Turn(float AxisValue) { FRotator NewRotation = GetActorRotation(); NewRotation.Yaw += AxisValue; SetActorRotation(NewRotation); } void ACollidingPawn::ParticleToggle() { if (OurParticleSystem && OurParticleSystem->Template) { OurParticleSystem->ToggleActive(); } }

**CollidingPawnMovementComponent.h**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#pragma once  	#include "CoreMinimal.h" 	#include "GameFramework/PawnMovementComponent.h" 	#include "CollidingPawnMovementComponent.generated.h"  	/** 		* 		*/ 	UCLASS() 	class HOWTO_COMPONENTS_API UCollidingPawnMovementComponent : public UPawnMovementComponent 	{ 		GENERATED_BODY()  	public: 		virtual void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction) override; 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #pragma once #include "CoreMinimal.h" #include "GameFramework/PawnMovementComponent.h" #include "CollidingPawnMovementComponent.generated.h" /\*\* \* \*/ UCLASS() class HOWTO\_COMPONENTS\_API UCollidingPawnMovementComponent : public UPawnMovementComponent { GENERATED\_BODY() public: virtual void TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction \*ThisTickFunction) override; };

**CollidingPawnMovementComponent.cpp**

```
	`// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved.  	#include "CollidingPawnMovementComponent.h"  	void UCollidingPawnMovementComponent::TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction *ThisTickFunction) 	{ 		Super::TickComponent(DeltaTime, TickType, ThisTickFunction);  		// Make sure that everything is still valid, and that we are allowed to move. 		if (!PawnOwner || !UpdatedComponent || ShouldSkipUpdate(DeltaTime)) 		{ 			return; 		}  		// Get (and then clear) the movement vector that we set in ACollidingPawn::Tick 		FVector DesiredMovementThisFrame = ConsumeInputVector().GetClampedToMaxSize(1.0f) * DeltaTime * 150.0f; 		if (!DesiredMovementThisFrame.IsNearlyZero()) 		{ 			FHitResult Hit; 			SafeMoveUpdatedComponent(DesiredMovementThisFrame, UpdatedComponent->GetComponentRotation(), true, Hit);  			// If we bumped into something, try to slide along it 			if (Hit.IsValidBlockingHit()) 			{ 				SlideAlongSurface(DesiredMovementThisFrame, 1.f - Hit.Time, Hit.Normal, Hit); 			} 		} 	};`

Copy full snippet
```
// Copyright 1998-2018 Epic Games, Inc. All Rights Reserved. #include "CollidingPawnMovementComponent.h" void UCollidingPawnMovementComponent::TickComponent(float DeltaTime, enum ELevelTick TickType, FActorComponentTickFunction \*ThisTickFunction) { Super::TickComponent(DeltaTime, TickType, ThisTickFunction); // Make sure that everything is still valid, and that we are allowed to move. if (!PawnOwner || !UpdatedComponent || ShouldSkipUpdate(DeltaTime)) { return; } // Get (and then clear) the movement vector that we set in ACollidingPawn::Tick FVector DesiredMovementThisFrame = ConsumeInputVector().GetClampedToMaxSize(1.0f) \* DeltaTime \* 150.0f; if (!DesiredMovementThisFrame.IsNearlyZero()) { FHitResult Hit; SafeMoveUpdatedComponent(DesiredMovementThisFrame, UpdatedComponent->GetComponentRotation(), true, Hit); // If we bumped into something, try to slide along it if (Hit.IsValidBlockingHit()) { SlideAlongSurface(DesiredMovementThisFrame, 1.f - Hit.Time, Hit.Normal, Hit); } } };

## 5\. Playing in Editor

1.  In Unreal Editor, we can press the **Compile** button to load our code changes.
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/e0eeb8a6-011e-42b2-9fd3-cc113f78c512/compilefromeditor.png)
2.  We need to drop an instance of our **CollidingPawn** into the world. We can find the class in the **Content Browser** under "C++ Classes/HowTo\_Components/CollidingPawn".
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/2ddfef5b-606a-44f7-8d5d-868804f0b01c/classincontentbrowser.png) ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/98460388-0244-40c9-b5c4-573487baac38/leveleditorbeforeplay.png)
3.  Press **Play** and our sphere will move with WASD, turn with the mouse, and collide-and-slide along world objects, such as our table and chairs, or any other physical objects you might want to place in the world. It can also light itself on fire (or put itself out) with the space bar!
    
    ![](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5675c75c-df5c-469f-a2d1-1648a6d09640/collidingandonfire.png)

**Unreal Engine** offers a wide variety of **Components** - we've only scratched the surface with a few of the more common ones. Try exploring the built-in Components, or writing some of your own! They are flexible, powerful, and help to keep your project's code organized and reusable.

## 6\. On Your Own!

Using what you have learned, try to do the following:

-   Create a **Component** that automatically orbits its parent.
-   Build a Component that spawns up to three children, each of which despawn on their own after a set amount of time.
-   Learn how to attach complete **Actors** to other Actors via Components.